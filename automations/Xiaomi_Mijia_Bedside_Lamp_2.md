# Xiaomi Mijia Bedside Lamp 2

## States

- Long Press
- Press
- Rotate Left
- Rotate Left (Pressed)
- Rotate Right
- Rotate Right (Pressed)

## Dimmer Press

```yaml
alias: Dimmer_Press
description: ""
triggers:
  - device_id: defd42d5517df84480bc151db714a0d3
    domain: xiaomi_ble
    type: dimmer
    subtype: press
    trigger: device
conditions: []
actions:
  - action: light.toggle
    metadata: {}
    target:
      entity_id: light.mibedsidelamp2_77c5_mijia_bedside_lamp_sw_auth
    data:
      rgb_color:
        - 173
        - 216
        - 230
mode: single

```

## Dimmer Long Press

```yaml
alias: Dimmer_LongPress_ColorToggle
description: ""
triggers:
  - device_id: defd42d5517df84480bc151db714a0d3
    domain: xiaomi_ble
    type: dimmer
    subtype: long_press
    trigger: device
conditions: []
actions:
  - if:
      - condition: template
        value_template: >-
          {{ state_attr('light.mibedsidelamp2_77c5_mijia_bedside_lamp_sw_auth',
          'rgb_color') == [0, 0, 255] }}
    then:
      - action: light.turn_on
        target:
          entity_id: light.mibedsidelamp2_77c5_mijia_bedside_lamp_sw_auth
        data:
          kelvin: 2700
    else:
      - action: light.turn_on
        target:
          entity_id: light.mibedsidelamp2_77c5_mijia_bedside_lamp_sw_auth
        data:
          rgb_color:
            - 173
            - 216
            - 230
mode: single

```

## Dimmer Rotate Right

```yaml
alias: Dimmer_Rotate_Right
description: ""
triggers:
  - trigger: event.received
    target:
      device_id: defd42d5517df84480bc151db714a0d3
    options:
      event_type:
        - rotate_right
conditions: []
actions:
  - action: light.turn_on
    target:
      entity_id: light.mibedsidelamp2_77c5_mijia_bedside_lamp_sw_auth
    data:
      brightness_pct: >-
        {{ [state_attr('light.mibedsidelamp2_77c5_mijia_bedside_lamp_sw_auth',
        'brightness') | int(0) / 2.55 + 10, 100] | min | int }}
mode: single
```

## Dimmer Rotate Left

```yaml
alias: Dimmer_Rotate_Left
description: ""
triggers:
  - trigger: event.received
    target:
      device_id: defd42d5517df84480bc151db714a0d3
    options:
      event_type:
        - rotate_left
conditions: []
actions:
  - action: light.turn_on
    target:
      entity_id: light.mibedsidelamp2_77c5_mijia_bedside_lamp_sw_auth
    data:
      brightness_pct: >-
        {{ [state_attr('light.mibedsidelamp2_77c5_mijia_bedside_lamp_sw_auth',
        'brightness') | int(0) / 2.55 - 10, 1] | max | int }}
mode: single

```
