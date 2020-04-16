+++
author = "Martin Weber"
categories = ["Hugo"]
date = 2019-11-07T05:00:00Z
description = "This is meta description"
image = "/images/post/post-1.jpg"
title = "Philips Hue"
type = "post"

+++
## Hue Bridge

Die Hue Geräte werden über ZigBee angesprochen für die Verbindung mit dem Netzwerk sorgt die Hue Bridge. Die Hue Bridge wird einfach über RJ45 mit dem lokalen Netzwerk verbunden. Die Hue Handy Apps und Home Assistant können diese dann automatisch erkennen. Die moderneren Hue Lampen können grundsätzlich auch über Bluetooth Low Energy für eine zentrale Steuerung eignet sich diese Variante aber nicht.

## Hue Lampen

Alle Philips Hue Lampen sind dimmbar. Abgesehen von unterschiedlichen Fassungen und Designs unterscheiden sich die Lampen auch bei den möglichen Lichtfarben.

* White (ein Weißton, dimmbar)
* White Ambiance (warmweiß bis kaltweiß, dimmbar)
* White & Color Ambiance (Farbe oder warmweiß bis kaltweiß, dimmbar)

Es gibt auch zahlreiche Lampen von anderen Herstellern welche mit dem Hue System kompatibel sind. Diese sind meißtens günstiger, kommen aber in der Qualität nicht immer ganz an die Philips Modelle heran. 

## Hue Motion Sensor

Das Hue System besteht mittlerweile nicht mehr ausschließlich aus Lampen sondern auch aus anderen Geräten im Bereich Smarthome dazu gehören auch die Bewegungssensoren. Diese liefern zusätzlich zu der Bewegungsinformation auch Messwerte für Temperatur und Helligkeit. Home Assistant kann auf diese Sensoren auch ohne zusätzliche Erweiterungen einbinden.

## Hue Remote

Die Hue Remote habe ich über die Custom Component [https://github.com/robmarkcole/Hue-remotes-HASS](https://github.com/robmarkcole/Hue-remotes-HASS "Hue Remote HASS") via HACS installiert. In der Home Assistant Konfiguration sieht das einfach so aus.

    remote:
      - platform: hueremote

Für die entsprechenden Aktionen die durch die 4 Knöpfe angewählt werden können kommt wieder NodeRed ins Spiel.

![](/images/hue_remote_node_red_trigger_switch.PNG)

Mit einem Switch können wir die Tasten anhand ihrer Payload unterscheiden und dann verschiedenen Aktionen auslösen.