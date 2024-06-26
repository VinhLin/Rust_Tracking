## Rust_Tracking: 
- Đây là project **GPS-Tracking** được viết bằng **Rust**.
- Framwork được sử dụng là: [Embassy](https://embassy.dev/)

----------------------------------------------------------------------------------
### Kết nối phần cứng:
- MCU: STM32F303RDT6
- Module GPS: SIM68ML

Kết nối:
STT	|	GPS SIM68ML	|	STM32F303RDT6	|
--------|-----------------------|-----------------------|
1	|	V_GPS		| GPS_PWR (PIN PA4)	|
2	|	GND		|	GND		|
3	|	TXD0 (GPIO 2)	| USART2_RX (PIN PA3)	|
4	|	RXD0 (GPIO 3)	| USART2_TX (PIN PA2)	|
5	|	RESET (GPIO 9)	| 	PIN PA1		|
6	|	-		| Led GPS (PIN PC2)	|

DEBUG Serial
```
PA9 - USART1_TX
PA10 - USART1_RX
```

---------------------------------------------------------------------------------
## [GPS NMEA](https://aprs.gids.nl/nmea/)

### [GGA](https://aprs.gids.nl/nmea/#gga) -  Các thông tin sẽ lấy bao gồm:
- Latitude
- Longitude
- Number of Satellites

### [RMC](https://aprs.gids.nl/nmea/#rmc) -  Các thông tin sẽ lấy bao gồm:
- Speed
- DateTime

----------------------------------------------------------------------------------
## gps_stm32f3
- Tạo project:
```
cargo new gps_stm32f3
cd gps_stm32f3
code .
```

### Kiểm tra dòng chip
```
probe-rs chip list | Select-String "STM32F303RDT"
probe-rs run --chip STM32F303RDTx --probe 0483:3748 target\thumbv7em-none-eabihf\debug\gps_stm32f3
```

### Build and Run:
```
cargo clean
cargo run --bin gps_stm32f3
```

### Convert file ELF sang loại file khác
```
cargo-objcopy --bin gps_stm32f3 -- -O binary gps_stm32f3.bin
cargo-objcopy --bin gps_stm32f3 -- -O binary gps_stm32f3.hex
```

-------------------------------------------------------------------
### TODO List

Step	| Status	|	Detail		|
--------|---------------|-----------------------|
Step 1	| **DONE**	| Khởi tạo dự án và Test debug Serial UART_1 |
Step 2	| **DONE**	| Đọc dữ liệu data GPS từ UART_2 |
Step 3	| **DONE**	| Parse data GPS	|
Step 4	| `Todo`	| Watchdog-Timer cho MCU |
Step 5	| `Todo`	| Kết nối với module sim |
Step 6	| `Todo`	| Gửi data GPS lên IoT Platform |













