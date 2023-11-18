# Cara atur wifi ESP8266

## intro
![architecture](ss/esp8266_architecture.png)\
Apakah kalian tahu bahwa esp-series seperti `esp8266, esp32` dan lainnya sudah terdapat wifi builtin ?

![series](ss/fully-fledged%20matter%20solution.jpg)\
tujuannya adalah untuk memungkinkan antar mikrokontroler ini dapat saling berkomunikasi dengan IP(Internet Protocol) melalui jaringan nirkabel wifi(wireless fidelity)

![esp8266 part](ss/esp8266_board.png)\
sangat canggih bukan ? dengan demikian kalian tidak perlu menambahkan modul wireless tambahan untuk memulai project (seperti yang biasa kita lakukan jika hanya menggunakan Arduino Uno atau mikrokontroler sejenis) dimana belum tentu terdapat rangkaian wifi secara builtin seperti mikro kontroler esp8266 [baca selengkapnya tentang espressif](/pustaka/mikrokontroler%20espressif%20kompetitor%20baru%20arduino%20dalam%20industri%20IoT%20dan%20Robotik/README.md)


## Walkthrough
Secara dasar Espressif atau ESP sebenarnya sudah merilis library mereka supaya mikrokontroler ini dapat digunakan pada lingkungan kerja Arduino/Arduino IDE. Yakni kita dapat menggunakan library berikut [Arduino/Wifi](https://www.arduino.cc/reference/en/libraries/wifi/)

adapun library opsional yang turut dapat kita gunakan untuk pengembangan lebih lanjut [yakni sebagai berikut](https://github.com/tzapu/WiFiManager)

nah, pada artikel kali ini kita akan mulai dengan yang paling dasar beserta contoh yang dapat kita coba terapkan berdasarkan manfaat yang nantinya akan kita peroleh.

## Alat
* Sebuah Komputer atau Laptop
* Arduino IDE versi: 2.2.1\
![versi arduino](ss/arduino%20version.png)



## Bahan
* sebuah micro controller : Esp8266\
![versi arduino](ss/varian%20esp8266.png)
* Arduino IDE sudah terinstall Board ESP8266, jika belum [klik untuk melihat cara install board ESP8266 di Arduino IDE](/a.dasar/11-11-2023/cara%20install%20board%20Esp8266%20di%20Arduino%20IDE/README.md)

## Langkah
1. Buka Arduino IDE
2. Hubungkan Esp8266 ke Komputer dengan menggunakan kabel data
    ```
    a. pastikan Esp8266 sudah terhubung ke komputer
    b. lakukan cek dengan cara membuka Device Manager > cari pada bagian Ports
    ```
    ![silicon labs cp210x](ss/silicon%20labs%20cp210.png)

3. pilih port dan board di Arduino IDE
    ![Alt text](ss/port%20board%20select.png)
4. buka halaman berikut [klik untuk membuka](https://arduino-esp8266.readthedocs.io/en/3.1.2/esp8266wifi/readme.html)
5. sebagaimana yang tertampil di halaman tersebut, kita copy program nya, kemudian kita paste kan di workspace/sketch Arduino IDE
    ```cpp
    #include <ESP8266WiFi.h>

    void setup(){
       Serial.begin(115200);
       Serial.println();

       WiFi.begin("network-name", "pass-to-network");

       Serial.print("Connecting");
       while (WiFi.status() != WL_CONNECTED){
           delay(500);
           Serial.print(".");
       }
       Serial.println();

       Serial.print("Connected, IP address: ");
       Serial.println(WiFi.localIP());
    }

    void loop() {}
    ```
6. ganti `network-name` dengan nama wifi yang ada di sekitarmu\
   ![cek wifi](ss/cek%20wifi.png)
7. ganti juga `pass-to-network` dengan password wifi tersebut
8. maka hasilnya akan nampak seperti ini\
   ![hasil coding](ss/hasil%20coding.png)

9. setelah coding selesai, lanjut kita flash atau upload ke dalam mikrokontroler dengan cara
   ```
   klik sketch di pojok atas > klik upload

   atau di keyboard tekan: ctrl + u
   ```
10. setelah berhasil maka bagian Output akan nampak seperti gambar berikut\
    ![hasil upload](ss/hasil%20upload.png)
11. untuk memastikan apakah program sudah berjalan dengan benar kita dapat melakukan cek menggunakan serial monitor.\
    [klik disini untuk memahami cara kerja serial monitor lebih lanjut](/pustaka/memahami%20cara%20kerja%20serial%20monitor/README.md)
    ```
    caranya klik Tools > klik Serial Monitor

    atau di keyboard tekan: ctrl + shift + m
    ```
    ![Alt text](ss/serial%20monitor.png)
12. sebagaimana yang tertulis dalam program seperti contoh baris berikut
    ```
    Serial.print("Connected, IP address: ");
    Serial.println(WiFi.localIP());
    ```
    maka di serial monitor akan tertampil tulisan seperti ini
    ```
    09:26:33.163 -> Connected, IP address: 172.16.1.55
    ```
    bukti lengkapnya:\
    ![Alt text](ss/inspeksi%20coding.png)

13. di Serial Monitor tertulis IP Address: 172.16.1.55 yang artinya sudah terhubung ke jaringan wifi dan mendapatkan ip tersebut, Menarik...

    mari kita buktikan dengan coba melakukan ping dari komputer yang sudah terhubung pada jaringan wifi yang sama apakah bisa atau tidak
    ```
    caranya: buka cmd di windows
    ketik: ping 172.16.1.55
    ```
    berikut adalah hasilnya:\
    ![Alt text](ss/cek%20ping.png)

    ternyata berhasil terhubung dengan baik tanpa kendala. keren!!
14. bagi teman-teman yang sudah berhasil mencapai step-13 selamat. karena dari sini nanti dapat kita kembangkan menuju ide-ide yang lebih gila lagi
    * [cara mengontrol esp8266 melalui jaringan wifi](/b.%20medium/17-11-2023/cara%20mengontrol%20esp8266%20melalui%20jaringan%20wifi/README.md)
    * cara menggunakan esp8266 untuk mengontrol lampu
    * cara menggunakan esp8266 untuk membuat drone(robot tanpa awak)
    * cara menggunakan esp8266 untuk menyalakan dan mematikan motor
    * lanjutkan sendiri dengan ide-ide yang lebih gila lagi

## Referensi
* https://www.espressif.com/sites/default/files/documentation/0a-esp8266ex_datasheet_en.pdf
* https://www.warriornux.com/beginners-guide-belajar-esp8266-iot-dari-dasar/
* https://arduino-esp8266.readthedocs.io/en/latest/esp8266wifi/readme.html
* https://room-15.github.io/blog/2015/03/26/esp8266-at-command-reference/
  
## CODE
https://tttapa.github.io/ESP8266/Chap07%20-%20Wi-Fi%20Connections.html
