# Developpement


### Debug
Pour interconnecter rasp + pc
```bash
source <modelec-serge-ROS install>/install/setup.bash
export RMW_IMPLEMENTATION=rmw_fastrtps_cpp
export FASTRTPS_DEFAULT_PROFILES_FILE=<modelec-serge-ROS install>/fastdds_setup.xml
export ROS_DOMAIN_ID=128
```

Ensuite rajouté ce bout de code dans le fichier `fastdds_setup.xml` :
```xml
<locator>
    <udpv4>
         <address>Tailscale IPv4 address / domain name</address>
    </udpv4>
</locator>
```
(Update coté client ET coté serveur (sur le rasp))

(Ps: pour se connecter au [tailscale](connect-rasp.md))
