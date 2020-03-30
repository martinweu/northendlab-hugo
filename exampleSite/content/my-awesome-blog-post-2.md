+++
author = "Martin Weber"
categories = ["Design Tools"]
date = 2020-03-30T04:00:00Z
description = "This is meta description"
image = "/images/photo-1528501905679-0eb90962e249.jfif"
title = "Shelly 2.5 als Jalousiensteuerung"
type = "post"

+++
Ich verwende einen Shelly 2.5 um meine Jalousien welche über einen propritären Controller angesteuert werden in mein SmartHome einzubinden. Da der propritäre Controller keine möglichkeit bietet ihn über LAN/USB/Wifi/Zigbee anzusteueren simuliere ich das drücken der Wandschalter über einen Shelly 2.5. Die regulärenen an den WÄnden verbauten Doppelschalter werden hierbei mit zwei Anoden und einer Kathode versorgt. Da der Shelly 2.5 im Gegensatz zu seinem älteren Bruder, dem Shelly 1 nicht potentialfrei schaltet muss der Shelly mit 12V versorgt werden. Da mein propritärer Controller neben den Sensor Eingängen und Schaltausgängen auch über einen 12V Anschluss verfügt, habe ich mich dazu entschlossen den Shelly 2.5 direkt im Schaltkasten zuverbauen. An meinem Controller sind 4 Jalousien mit jeweils seperaten Schaltern angeschlossen. Zusätzlich gibt es einen Schalter der alle 4 Jalousien zentral nach oben oder unten fahren lässt. Da ich meißtens alle Jalousien nach oben oder unten fahre, habe ich mich entschlossen nur die diesen Zentralschalter mit einem Shelly 2.5 auszustatten und so ins SmartHome zu integrieren. 

![Shelly 2.5](https://shelly.cloud/wp-content/uploads/2019/01/shelly-25.png "Shelly 2.5 (source: shelly.cloud)")