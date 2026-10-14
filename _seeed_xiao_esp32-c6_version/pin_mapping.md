Goal, use ESP32-S3 dev board for wifi and SEEED XIAO ESP32-C6 (mini version) for flashing tags

Pin mapping as of now

| Pin Function            | S3 Pin | C6 Pin | C6 GPIO | Notes                          |
|-------------------------|--------|--------|---------|--------------------------------|
| GND                     | GND    | GND    | -       |                                |
| 3V                      | 3V     | 3V     | -       |                                |
| UART1 TX (S3→C6)        | 17     | D2     | GPIO20  | Runtime comms (second_uart RX) |
| UART1 RX (C6→S3)        | 18     | D3     | GPIO21  | Runtime comms (second_uart TX) |
| UART0 RX (C6→S3, flash) | 19     | D6     | GPIO16  | C6 UART0 TX, used for OTA flash|
| UART0 TX (S3→C6, flash) | 20     | D7     | GPIO17  | C6 UART0 RX, used for OTA flash|
| BOOT trigger            | 21     | BOOT   | GPIO9   | Held low to enter bootloader   |
| RESET                   | 47     | EN     | -       | Reset pulse to enter bootloader|

C6 firmware must be built with sdkconfig.defaults:
  CONFIG_OEPL_HARDWARE_PROFILE_CUSTOM=y
  CONFIG_OEPL_HARDWARE_UART_TX=21
  CONFIG_OEPL_HARDWARE_UART_RX=20
