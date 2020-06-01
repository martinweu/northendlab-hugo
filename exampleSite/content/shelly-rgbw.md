+++
author = "Martin Weber"
categories = ["Home Automation"]
date = 2020-03-30T04:00:00Z
description = "This is meta description"
draft = false
image = "/images/post/shelly-rgbw.jpg"
title = "Shelly RGBW2"
type = "post"

+++

Seit neuestem hat auch der Shelly RGBW2 in mein Smart Home Einzug gehalten. Der Shelly RGBW2 bietet die bekannten Einstellungsmöglichkeiten der Shelly Familie ([siehe mein erster Shelly Blogpost](../shelly-switches/)). Der Shelly RGBW2 kann mit 12V oder 24V versorgt werden und ist für das Einbinden von LED Streifen konzipiert. Wie der Name schon verspricht hat der Shelly 4 einzeln regelbare Ausgänge welche mit dem RGBW-Schema oder auch als einzelne Kanäle angesprochen werden können.
Nach der Einrichtung der MQTT Verbindung kann der Shelly als Licht in Home Assistant konfiguriert werden.

### Shelly RGBW2 Konfiguration in Home Assistant im RGBW Modus

ABCDEF muss durch die jeweilige shelly seriennummer ersetzt werden.

    light:
      - platform: mqtt
        schema: template
        name: "LEDstrip MQTT"
        command_topic: "shellies/shellyrgbw2-ABCDEF/color/0/set"
        state_topic: "shellies/shellyrgbw2-ABCDEF/color/0/status"
        effect_list:
          - 0
          - 1
          - 2
          - 3
          - 4
          - 5
          - 6
        command_on_template: >
          {"turn": "on"
          {%- if brightness is defined -%}
          , "gain": {{brightness | float | multiply(0.3922) | round(0)}}
          {%- endif -%}
          {%- if red is defined and green is defined and blue is defined -%}
          , "red": {{ red }}, "green": {{ green }}, "blue": {{ blue }}
          {%- endif -%}
          {%- if white_value is defined -%}
          , "white": {{ white_value }}
          {%- endif -%}
          {%- if effect is defined -%}
          , "effect": {{ effect }}
          {%- endif -%}
          }
        command_off_template: '{"turn":"off"}'
        state_template: "{% if value_json.ison %}on{% else %}off{% endif %}"
        brightness_template: "{{ value_json.gain | float | multiply(2.55) | round(0) }}"
        red_template: '{{ value_json.red }}'
        green_template: '{{ value_json.green }}'
        blue_template: '{{ value_json.blue }}'
        white_value_template: '{{ value_json.white }}'
        effect_template: '{{ value_json.effect }}'
        qos: 2

original von ["Shelly RGBW2 thehookup"](https://github.com/thehookup/Shelly-RGBW2)

## Links
* [Shelly](https://shelly.cloud)
* [Shelly RGBW2 auf Amazon](https://www.amazon.de/Shelly-RGBW-2/dp/B07N49TXLQ/ref=sr_1_1?__mk_de_DE=%C3%85M%C3%85%C5%BD%C3%95%C3%91&dchild=1&keywords=shelly+rgbw2&qid=1591034842&sr=8-1)