+++
author = "Martin Weber"
categories = ["Hugo"]
date = 2019-11-07T05:00:00Z
description = "This is meta description"
image = "/images/post/post-3.jpg"
title = "Alexa"
type = "post"

+++
Gleich mal vorweg ich verwende Alexa (Amazon Echo Geräte) mit drei unterschiedlichen Anbindungen in meinem SmartHome.

1. via Spotify
2. Alexa Media Player (Community Paket)
3. NodeRed - Virtual Hue Bridge

Über die Spotify-HomeAssistant-Integration kann ich die Echo-Geräte wie auch andere mit Spotify verbunden Geräte als Wiedergabegeräte anwählen. Dies ist sowohl im UserInterface aber auch über verschiedene Abläufe welche ich in NodeRed erstellt habe möglich.

Die zweite Integration erfolgt über das Community Paket Alexa Media Player welches ich über HACS installiert habe. Damit habe ich die Möglichkeit Sprachausgaben an die jeweiligen Echo Geräte zu senden bzw. die für die einzelnen Geräte programmieren Wecker oder Timer auszulesen.

Die dritte Integration erfolgt über ein NodeRed-Paket welches eine HUE-Bridge simuliert. Alle Amazon Echo-Devices (auch die ohne SmartHome-Hub, also auch Dots) können über das lokale Netzwerk mit einer Philips-Hue Bridge kommunizieren. Soweit mir bekannt, ist das die einzige Integration die direkt imlokalen Netzwerk erfolgt. In Node-Red können dann virtuelle Philips-Hue Lampen mit beliebigen Namen erstellt werden. Diese müssen dann noch mit der Alexa App als SmartHome Geräte gesucht und gefunden werden. Danach kann mit "Alexa, schalte Haus verlassen ein" der Ablauf welcher an der virtuelle Philips-Hue Lampe mit dem Namen "Haus Verlassen" hängt gestartet werden.

Für diese virtuellen Lampen gelten die gleichen Befehlsmöglichkeiten wie für die realen Phlips-Hue Lampen. Man kann sie also auch dimmen oder die Lichtfarbe ändern. Auf die entsprechenden Nachrichten kann dann in NodeRed beliebig reagiert werden. Da es sich aber immer um Lampen handelt sind Befehle die in der Alexa Automatisierungswelt z.B. für Jalousien vorgesehen sind wie öffnen oder schließen nicht verfügbar. Ich verwende als Workaround also einfach "Alexa, Jalousien ein" und "Alexa, Jalousien aus".

Um das System etwas tolleranter gegenüber Missverständnissen zu machen, kann es helfen mehrere Schreibweisen (auch mit falscher Rechtschreibung) zu verwenden. In meinem SmartHome heißen die Jalousien zusätzlich noch "Schalusien", das Küchenlicht heißt auch noch "Kuchenlicht" usw. Die idealen Schreibweisen findet man am Besten heraus indem man in der Alexa Historie die nicht erkannten Befehle durch sieht. Die dabei gefunden Schreibweisen kann man dann als zusätzliche virtuelle Lampen in NodeRed vor den gewünschen Ablauf hängen.

Ein weiterer Schritt die Interaktion noch etwas zu verbessern ist Alexa Routinen zu verwenden. Diese müssen in der Alexa App konfiguriert werden und ermöglichen etwas mehr Freiheit bei der gestaltung des Sprachbefehls. Der Sprachbefehl muss nicht mehr direkt das schalten der einzelnen Geräte beinhalten. Zum Beispiel kann man eine Alexa Routine welche mit "Alexa, Guten Morgen" gestartet wird erstellen, welche dann die vorher in NodeRed erzeugte virtuelle "Guten Morgen"-Lampe einschaltet.