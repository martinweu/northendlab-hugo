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

Die Hue Geräte werden über ZigBee angesprochen für die Verbindung mit dem Netzwerk sorgt die Hue Bridge. Die Hue Bridge wird einfach über RJ45 mit dem lokalen Netzwerk verbunden. Die Hue Handy Apps und Home Assistant können diese dann automatisch erkennen. 

## Hue Lampen

### Hue Ambience Color + White

### Hue Ambience White

## Hue Motion Sensor

## Hue Remote

Die Hue Remote habe ich über die Custom Component [https://github.com/robmarkcole/Hue-remotes-HASS](https://github.com/robmarkcole/Hue-remotes-HASS "Hue Remote HASS") via HACS installiert. In der Home Assistant Konfiguration sieht das einfach so aus.

    remote:
      - platform: hueremote

Für die entsprechenden Aktionen die durch die 4 Knöpfe angewählt werden können kommt wieder NodeRed ins Spiel.

![](/images/hue_remote_node_red_trigger_switch.PNG)

Mit einem Switch können wir die Tasten anhand ihrer Payload unterscheiden und dann verschiedenen Aktionen auslösen.