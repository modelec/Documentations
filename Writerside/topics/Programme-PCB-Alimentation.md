# Programme PCB Alimentation

Le programme du PCB Alimentation (en l'état actuel) implémente deux fonctionnalités principales.

- Récupération des données capteurs et contrôle de l'arrêt d'urgence logiciel.
- Implémentation du protocole USB-PD.

## Récupération des données capteurs et contrôle de l'arrêt d'urgence logiciel

Le code de récupération des capteurs et de contrôle de l'arrêt d'urgence implémente le protocole de communication spécifié sur la page [](Pilotage-PCB-alimentation.md).

Le code de gestion de la communication est séparé dans un fichier dédié (comm.c) et est généré par IA à l'aide des spécifications.

Le code dédié à l'interface avec les composants est séparé dans un fichier dédié (alim.c) et est à écrire en se basant sur la doc des composants.

## Implémentation du protocole USB-PD

### Configuration matérielle

STM32G491KEU6 du PCB alimentation est connectée à une puce TCPP02-M18 via :
- PA9 <-> EN
- PA12 <-> FLGn
- I2C, CC1 et CC2
Point d'attention : il n'y a pas d'ADC ni d'IANA connectée au STM32 comme dans les tutoriels proposés par ST.

Alimentation pour l'USB est fournie par un Traco Power THN_30-2411WI réglé sur 5V15.

Le TCPP02-M18 est connecté à un mosfet STL40DN3LLH5 via ses pins Gate et Source. Le mosfet est situé entre le Traco et le port USB.

Il y a une résistance de Shunt entre le mosfet et le port usb connectée à ISENSE et VBUSC du TCPP02-M18.

Le port USB-C est connecté aux pins CC1 et CC2 du TCPP02, à VBUS et à la masse de la carte.

### Configuration logicielle

La configuration est réalisée avec le STM32CubeIDE en suivant les conseils du wiki ST :

- Ajout des middlewares:
  - FREERTOS
  - USBPD
  - X-CUBE-TCPP
- Configuration de FreeRTOS en CMSISV1
- Configuration de l'USBPD
  - profil par défaut en source avec tension 5V et courant 3000mA
  - autre profil en source avec tension 5V et courant 5000mA
- Configuration de X-CUBE-TCPP avec l'I2C, PA9 et PA12 mais sans ADC
- Fonctions de traces et de débug activées pour le Cube Monitor USBPD

Une fois le code généré, on applique des patchs manuels directement dans le code pour palier à l'absence d'ADC.

- Dans custom_board_usbpd_pwr.c remplacer PWR_TCPP0203_ConvertADCDataToVoltage et PWR_TCPP0203_ConvertADCDataToCurrent pour renvoyer 5000 et 3000
- Builder et retirer tout ce qui fait référence à ADC **/!\ les parties ADC sont à retirer après chaque build du projet et avant chaque compilation.**
- Dans usbpd_pwr_if.c, modifier la fonction USBPD_PWR_IF_GetVBUSStatus de la sorte :
`uint8_t USBPD_PWR_IF_GetVBUSStatus(uint8_t PortNum, USBPD_VBUSPOWER_STATUS PowerTypeStatus)
{
/* USER CODE BEGIN USBPD_PWR_IF_GetVBUSStatus */
return USBPD_TRUE;
/* USER CODE END USBPD_PWR_IF_GetVBUSStatus */
}`

### Debug

Pour débugger la partie USB-PD on peut utiliser le logiciel STM32CubeMonitor-UCPD

Logs dans le cube monitor :
On retrouve bien la carte connectée et on observe correctement une inversion CC1 ou CC2

Logs en boucle :
4	PE	41628	0	PE_SRC_DISCOVERY
5	PE	41778	0	PE_SRC_SEND_CAPABILITIES
6	OUT	41780	0	SOP	 PD3	s:006	    H:0x17A1    	(id:3, DR:DFP, PR:SRC) 	SRC_CAPABILITIES	DATA: F4910102	Option: 	DRD	 [1] Fixed : 5V - 5A /
7	OUT	41781	0	SOP	 PD3	s:006	    H:0x17A1    	(id:3, DR:DFP, PR:SRC) 	SRC_CAPABILITIES	DATA: F4910102	Option: 	DRD	 [1] Fixed : 5V - 5A /
8	OUT	41783	0	SOP	 PD3	s:006	    H:0x17A1    	(id:3, DR:DFP, PR:SRC) 	SRC_CAPABILITIES	DATA: F4910102	Option: 	DRD	 [1] Fixed : 5V - 5A /
9	PE	41784	0	PE_SRC_DISCOVERY

Logs au plug du cable :
6	DEBUG	1	0	-- BSP_USBPD_PWR_VBUSInit --
7	DEBUG	1	0	-- BSP_USBPD_PWR_SetPowerMode --
8	DEBUG	1	0	-- Normal --
9	CAD	1	0	USBPD_CAD_STATE_ATTACHED_WAIT
10	CAD	123	0	USBPD_CAD_STATE_ATTACHED
11	NOTIF	123	0	USBSTACK_START
12	DEBUG	123	0	ADVICE: USBPD_DPM_Notification:104
13	EVENT	123	0	EVENT_ATTACHED
14	DEBUG	123	0	VBUS ON
15	DEBUG	123	0	-- BSP_USBPD_PWR_VBUSOn --
16	DEBUG	126	0	-- GDP/GDC setting : SRC --
17	PE	126	0	PE_SRC_STARTUP
18	NOTIF	126	0	POWER_STATE_CHANGE
19	DEBUG	126	0	ADVICE: USBPD_DPM_Notification:90
20	PE	126	0	PE_SRC_SEND_CAPABILITIES

**Pour que l'échange USP-PD se passe bien il faut utiliser un câble compatible USB-PD (e-marked et supportant 5A de courant).**
 
On devrait observer dans les logs les réponses de la raspberry pi et l'éventuel changement de courant.