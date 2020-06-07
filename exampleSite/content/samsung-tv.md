+++
author = "Martin Weber"
categories = ["Home Assistant"]
date = 2020-03-30T04:00:00Z
description = "This is meta description"
draft = false
image = "/images/post/samsung-tv.jpg"
title = "Samsung Smart TV"
type = "post"

+++

## Einbindung in Home Assistant
Grundsätzlich kann ein Samsung Smart TV-Gerät direkt in Home Assistant eingebunden werden. Der Funktionsumfang lässt sich aber durch die Installation eines Community Plugins deutlich erweitern.
Das entsprechende Plugin habe ich über HACS gefunden und installiert. Es ermöglicht mir unter Anderem das Starten von Apps am TV direkt aus Home Assistant heraus.
Somit kann ich über ein Script direkt aus dem Home Assistant UI Fernseher und das entsprechende Programm (Amazon Prime, Netflix, YouTube, etc.) starten.

## Wake on Lan
Wie man auf den Fotos erkennen kann ist mein TV-Gerät über einen Powerline Adapter mit dem Netzwerk verbunden. Viele TV Geräte (auch meines) beherrschen zwar bereits moderne WLAN Standards, können aber nicht über WLAN eingeschaltet werden. Das liegt daran dass das TV-Gerät die Verbindung im Standby-Modus nicht aufrechterhält und somit kein Wake On Lan (WOL) Paket empfangen werden kann. Über den Powerline-Adapter, der an die auch im Standy aktive Netzwerkkarte des Fernsehgeräts angeschlossen ist, lässt sich ein sochles WOL-Paket übertragen und damit der Fernseher aus dem Standy-Modus zurückholen.


![TV Powerline](/images/post/tv-powerline.jpg "TV Powerline")


## Links
* [Home Assistant Community Store (HACS)](https://community.home-assistant.io/t/custom-component-hacs/121727)
* [Samsung TV Home Assistant Community Plugin](https://github.com/jaruba/ha-samsungtv-tizen)
* [TP-Link Powerline auf Amazon](https://www.amazon.de/TP-Link-TL-PA4010-s-Ethernet-Port-energiesparend-kompatibel/dp/B00A0VBPLM/ref=sr_1_19?__mk_de_DE=%C3%85M%C3%85%C5%BD%C3%95%C3%91&dchild=1&keywords=powerline+tplink&qid=1591038717&sr=8-19&tag=napster220203-21)
