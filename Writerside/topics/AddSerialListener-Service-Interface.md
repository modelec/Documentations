# AddSerialListener
`<modelec_interface/srv/add_serial_listener.hpp>`

## Objectif

## Interface
```cpp
string name
string serial_port
int64 bauds
---
bool success
string publisher
string subscriber
```

## Params

| Type   | Name        | Description                 |
|--------|-------------|-----------------------------|
| string | name        | nom du listener             |
| string | serial_port | port série à écouter        |
| int64  | bauds       | vitesse de la liaison série |

## Retour

| Type | Name    | Description            |
|------|---------|------------------------|
| bool | success | requête réussie ou non |

## Utilisé par
- [](Game-Controller-Listener-Node.md)
- [](Multiple-Serial-Listener-Node.md)
- [](PCB-Alim-Interface-Node.md)