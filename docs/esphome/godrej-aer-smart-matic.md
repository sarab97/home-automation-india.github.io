## Control Godrej Aer Smart matic

[Godrej aer Smart Matic Kit](https://www.amazon.in/Godrej-aer-Smart-Matic-BLUETOOTH/dp/B07YFBYRTG/ref=sr_1_1?keywords=godrej%2Bbluetooth&qid=1665497329&qu=eyJxc2MiOiIxLjI1IiwicXNhIjoiMS4yNyIsInFzcCI6IjEuMDAifQ%3D%3D&sr=8-1&th=1) is a BLE enabled air freshner kit. You can hook it up to sensors like PIR to only spray when someone is detected. 

You can control it using [BLE Client](https://esphome.io/components/ble_client.html) functionality in ESPHome. 
- Find the device MAC address. It is displayed in the app when you pair with the device or use a scanner app.
- Use an ESP32 to create a switch for spraying. You can control it using the UI or any automations 
```
ble_client:
  - mac_address: <MAC Address>
    id: godrej_aer

switch:
  - platform: template
    name: "Air Freshner"
    turn_on_action:
      - ble_client.ble_write:
          id: godrej_aer
          service_uuid: 6E400000-B5A3-F393-E0A9-E50E24DCCA9E
          characteristic_uuid: 6E400003-B5A3-F393-E0A9-E50E24DCCA9E
          value: [0xbf, 0x62, 0x6d, 0x54, 0x18, 0x68, 0x62, 0x6d, 0x4e, 0x18, 0x9a, 0x62, 0x72, 0x49, 0x00, 0xff]
```
