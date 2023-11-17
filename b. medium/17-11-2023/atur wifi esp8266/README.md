# Cara atur wifi ESP8266

## intro
![series](ss/fully-fledged%20matter%20solution.jpg)
Apakah kalian tahu bahwa esp-series seperti `esp8266, esp32` dan lainnya sudah terdapat wifi builtin ?

![architecture](ss/esp8266_architecture.png)
tujuannya adalah untuk memungkinkan antar mikrokontroler ini dapat saling berkomunikasi dengan IP(Internet Protocol) melalui jaringan nirkabel wifi(wireless fidelity)

![esp8266 part](ss/esp8266_board.png)
sangat canggih bukan ? dengan demikian kalian tidak perlu menambahkan modul wireless tambahan untuk memulai project (seperti yang biasa kita lakukan jika hanya menggunakan Arduino Uno atau mikrokontroler sejenis) dimana belum tentu terdapat rangkaian wifi secara builtin seperti mikro kontroler esp8266 [baca selengkapnya tentang espressif](/pustaka/mikrokontroler%20espressif%20kompetitor%20baru%20arduino%20dalam%20industri%20IoT%20dan%20Robotik/README.md)


## Walkthrough
Secara dasar Arduino X ESPressif sebenarnya sudah merilis library mereka supaya mikrokontroler ini dapat digunakan pada lingkungan kerja Arduino/Arduino IDE. Yakni kita dapat menggunakan library berikut [Arduino/Wifi](https://www.arduino.cc/reference/en/libraries/wifi/)

adapun library opsional yang turut dapat kita gunakan untuk pengembangan lebih lanjut [yakni sebagai berikut](https://github.com/tzapu/WiFiManager)
## Alat
* Sebuah Komputer atau Laptop
* Arduino IDE versi: 2.2.1\
![versi arduino](ss/arduino%20version.png)



## Bahan
* sebuah micro controller : Esp8266\
![versi arduino](ss/varian%20esp8266.png)

## Langkah


## Referensi
https://www.espressif.com/sites/default/files/documentation/0a-esp8266ex_datasheet_en.pdf
https://www.warriornux.com/beginners-guide-belajar-esp8266-iot-dari-dasar/
https://arduino-esp8266.readthedocs.io/en/latest/esp8266wifi/readme.html
https://room-15.github.io/blog/2015/03/26/esp8266-at-command-reference/
## CODE
https://tttapa.github.io/ESP8266/Chap07%20-%20Wi-Fi%20Connections.html