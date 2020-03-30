+++
author = "Martin Weber"
categories = ["Design Tools"]
date = 2019-11-07T05:00:00Z
description = "This is meta description"
image = "/images/post/post-2.jpg"
title = "Shelly 2.5 with Shades"
type = "post"

+++
Ich verwende einen Shelly 2.5 um meine Jalousien welche über einen propritären Controller angesteuert werden in mein SmartHome einzubinden. Da der propritäre Controller keine möglichkeit bietet ihn über LAN/USB/Wifi/Zigbee anzusteueren simuliere ich das drücken der Wandschalter über einen Shelly 2.5. Die regulärenen an den WÄnden verbauten Doppelschalter werden hierbei mit zwei Anoden und einer Kathode versorgt. Da der Shelly 2.5 im Gegensatz zu seinem älteren Bruder, dem Shelly 1 nicht potentialfrei schaltet muss der Shelly mit 12V versorgt werden. Da mein propritärer Controller neben den Sensor Eingängen und Schaltausgängen auch über einen 12V Anschluss verfügt, habe ich mich dazu entschlossen den Shelly 2.5 direkt im Schaltkasten zuverbauen. An meinem Controller sind 4 Jalousien mit jeweils seperaten Schaltern angeschlossen. Zusätzlich gibt es einen Schalter der alle 4 Jalousien zentral nach oben oder unten fahren lässt. Da ich meißtens alle Jalousien nach oben oder unten fahre, habe ich mich entschlossen nur die diesen Zentralschalter mit einem Shelly 2.5 auszustatten und so ins SmartHome zu integrieren. 

I use Shelly 2.5 to control my shades which are controlled via some proprietary controller. To overcome this barrier I use Shelly 2.5 to simulate the press of the actual control switches. Therefore, the Shelly needs to switch the 12V signal. The Shelly 2.5 needs the same voltage for operation as it is switching. The Shelly 1 allows running with a different voltage.