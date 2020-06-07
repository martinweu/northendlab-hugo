+++
author = "Martin Weber"
categories = ["Light"]
date = 2019-11-07T05:00:00Z
description = "This is meta description"
image = "/images/post/hue-bridge.jpg"
title = "Philips Hue"
type = "post"

+++
## Hue Bridge

Die Hue Geräte werden über ZigBee angesprochen für die Verbindung mit dem Netzwerk sorgt die Hue Bridge. Die Hue Bridge wird einfach über RJ45 mit dem lokalen Netzwerk verbunden. Die Hue Handy Apps und Home Assistant können diese dann automatisch erkennen. Die moderneren Hue Lampen können grundsätzlich auch über Bluetooth Low Energy für eine zentrale Steuerung eignet sich diese Variante aber nicht.

## Hue Lampen
![Hue Lamp](/images/post/hue-cyan-closeup.jpg "Hue White and Color")

Alle Philips Hue Lampen sind dimmbar. Abgesehen von unterschiedlichen Fassungen und Designs unterscheiden sich die Lampen auch bei den möglichen Lichtfarben.

* White (ein Weißton, dimmbar)
* White Ambiance (warmweiß bis kaltweiß, dimmbar)
* White & Color Ambiance (Farbe oder warmweiß bis kaltweiß, dimmbar)

Es gibt auch zahlreiche Lampen von anderen Herstellern welche mit dem Hue System kompatibel sind. Diese sind meistens günstiger, kommen aber in der Qualität nicht immer ganz an die Philips Modelle heran.
Zusätzlich zu den normalen Hue Leuchtmitteln gibt es mittlerweile die dekorative Filament Serie in 3 unterschiedlichen Formen.

![Hue Filament](/images/post/hue-filament.jpg "Hue Filament")

## Hue Motion Sensor
![Hue Sensor](/images/post/hue-sensor.jpg "Hue Sensor")

Das Hue System besteht mittlerweile nicht mehr ausschließlich aus Lampen sondern auch aus anderen Geräten im Bereich Smarthome dazu gehören auch die Bewegungssensoren. Diese liefern zusätzlich zu der Bewegungsinformation auch Messwerte für Temperatur und Helligkeit. Home Assistant kann auch diese Sensoren auch ohne zusätzliche Erweiterungen einbinden.

## Hue Remote
![Hue Remote](/images/post/hue-dimmer-switch.jpg "Hue Remote")

Auch die Hue Remotes können mittlerweile direkt ohne eigene Erweiterung in Home Assistant eingebunden werden. Es gibt insgesamt 8 Events die durch kurzes und langes Drücken auf den 4 Schaltern ausgelöst werden können.


## Links
* [Philips Hue](https://www2.meethue.com/)
* [Philips Hue auf Amazon](https://www.amazon.de/s?k=philips+hue&__mk_de_DE=%C3%85M%C3%85%C5%BD%C3%95%C3%91&ref=nb_sb_noss_2&tag=napster220203-21)