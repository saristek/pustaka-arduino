# Cara install Esp8266 di Arduino IDE
## Alat
* Sebuah Komputer atau Laptop
* Arduino IDE versi: 2.2.1\
![versi arduino](ss/arduino%20version.png)



## Bahan
* sebuah micro controller : Esp8266\
![versi arduino](ss/varian%20esp8266.png)

## Langkah
1. buka `Arduino IDE` di komputer atau laptop
2. install driver Esp8266: <b>biasanya menggunakan CH341</b>\
buka link berikut untuk melihat [cara menginstall driver ch341](/a.dasar//11-11-2023/cara%20install%20driver%20ch341/README.md)
3. copy link berikut
    ```
    https://arduino.esp8266.com/stable/package_esp8266com_index.json
    ```
4. buka `Preferences` di Arduino IDE dengan cara
    ```
    klik File > Preferences
    ```
    atau tekan di keyboard
    ```
    ctrl + comma
    ```
5. pada bagian Additional boards manager kemudian paste-kan link tersebut.
![additional boards manager](ss/additional%20boards%20manager.PNG)
6. kemudian buka `Boards Manager` dengan cara
    ```
    klik Tools > Board > Boards Manager
    ```
    atau tekan di keyboard
    ```
    ctrl + shift + b
    ```
7. ketik `esp8266` pada kolom pencarian
8. klik install pada hasil pencarian esp8266
![board manager install esp8266](ss/board%20manager%20install%20esp8266.PNG)


langkah selanjutnya silahkan klik link berikut untuk melihat [cara menggunakan esp8266 di arduino](/a.dasar/11-11-2023/cara%20menggunakan%20esp8266%20di%20arduino/README.md)
## varian Esp8266
## Referensi
https://github.com/esp8266/Arduino