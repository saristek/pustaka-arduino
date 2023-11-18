# Cara menggunakan L298N

## Alat
* Sebuah Komputer atau Laptop
* Arduino IDE versi: 2.2.1\
![versi arduino](ss/arduino%20version.png)



## Bahan
* sebuah micro controller : Esp8266\
![versi arduino](ss/varian%20esp8266.png)
* sebuah L298N

## SCHEMATIC
![diagram](ss/diagram.png)

## PROGRAM

### DASAR
```cpp
int ENA = 3; // -> pin 3
int IN1 = 2; // -> pin 2
int IN2 = 4; // -> pin 4

void setup() {
  Serial.begin(115200);
  pinMode(ENA, OUTPUT);
  pinMode(IN1, OUTPUT);
  pinMode(IN2, OUTPUT);
  Serial.println("Memulai Test...");
}

void loop() {
  Serial.println("tes putar: ");
  digitalWrite(ENA, HIGH);
  digitalWrite(IN1, HIGH);
  digitalWrite(IN2, LOW);
}

```


### MENGGUNAKAN WEB SERVER
```cpp
#include <ESP8266WiFi.h>
#include <ESP8266WebServer.h>

const char* ssid = "Portal Sransa (Barat)";
const char* password = "SupportSransa1!";

uint8_t nyala = LOW;
uint8_t roda = LOW;

int ENA = 3;  //4;
int IN1 = 2;  //0;
int IN2 = 4;  //2;

ESP8266WebServer server(80);

String SendHTML(uint8_t state,uint8_t nyala) {
  String ptr = "<!DOCTYPE html> <html>\n";
  ptr += "<head><meta name=\"viewport\" content=\"width=device-width, initial-scale=1.0, user-scalable=no\">\n";
  ptr += "<title>LED Control</title>\n";
  ptr += "<style>html { font-family: Helvetica; display: inline-block; margin: 0px auto; text-align: center;}\n";
  ptr += "body{margin-top: 50px;} h1 {color: #444444;margin: 50px auto 30px;} h3 {color: #444444;margin-bottom: 50px;}\n";
  ptr += ".button {display: block;width: 80px;background-color: #1abc9c;border: none;color: white;padding: 13px 30px;text-decoration: none;font-size: 25px;margin: 0px auto 35px;cursor: pointer;border-radius: 4px;}\n";
  ptr += ".button-on {background-color: #1abc9c;}\n";
  ptr += ".button-on:active {background-color: #16a085;}\n";
  ptr += ".button-off {background-color: #34495e;}\n";
  ptr += ".button-off:active {background-color: #2c3e50;}\n";
  ptr += "p {font-size: 14px;color: #888;margin-bottom: 10px;}\n";
  ptr += "</style>\n";
  ptr += "</head>\n";
  ptr += "<body>\n";
  ptr += "<h1>Atur L298N dengan ESP8266</h1>\n";
  ptr += "<h3>Menggunakan WIFI</h3>\n";

  if (nyala) {
    ptr += "<p>status: hidup</p><a class=\"button button-off\" href=\"/mati\">Mati</a>\n";
    if (state==true) {
      ptr += "<p>Laju: Maju</p><a class=\"button button-off\" href=\"/mundur\">Mundur</a>\n";
    } else if(state==false){
      ptr += "<p>Laju: Mundur</p><a class=\"button button-on\" href=\"/maju\">MAJU</a>\n";
    }
  } else {
    ptr += "<p>status: mati</p><a class=\"button button-on\" href=\"/hidup\">Hidup</a>\n";
  }

  ptr += "</body>\n";
  ptr += "</html>\n";

  return ptr;
}


void setup() {
  Serial.begin(115200);
  pinMode(ENA, OUTPUT);
  pinMode(IN1, OUTPUT);
  pinMode(IN2, OUTPUT);

  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) {
    delay(1000);
    Serial.println("Connecting to WiFi..");
  }

  Serial.println(WiFi.localIP());
  Serial.println("Memulai Test...");

  // atur endpoint server
  server.on("/", handle_OnConnect);
  server.on("/maju", handle_Maju);
  server.on("/mundur", handle_Mundur);

  server.on("/hidup", handle_Hidup);
  server.on("/mati", handle_Mati);
  server.onNotFound(handle_NotFound);

  // Start server
  server.begin();
}

void handle_OnConnect() {
  nyala = LOW;
  roda = LOW;
  Serial.println("init roda");
  server.send(200, "text/html", SendHTML(roda,nyala));
}

void handle_Hidup() {
  nyala = HIGH;
  resetRoda();
  Serial.println("Perintah Menghidupkan roda");
  server.send(200, "text/html", SendHTML(true,true));
}

void handle_Mati() {
  nyala = LOW;
  Serial.println("Perintah Mematikan roda");
  server.send(200, "text/html", SendHTML(true,false));
}

void handle_Maju() {
  roda = HIGH;
  Serial.println("Perintah Laju Roda: Maju");
  server.send(200, "text/html", SendHTML(true,true));
}

void handle_Mundur() {
  roda = LOW;
  Serial.println("Perintah Laju Roda: Mundur");
  server.send(200, "text/html", SendHTML(false, true));
}

void handle_NotFound(){
  server.send(404, "text/plain", "Not found");
}

void RodaKananMundur() {
  digitalWrite(ENA, HIGH);
  digitalWrite(IN1, HIGH);
  digitalWrite(IN2, LOW);
}

void RodaKananMaju() {
  digitalWrite(ENA, HIGH);
  digitalWrite(IN1, LOW);
  digitalWrite(IN2, HIGH);
}

void resetRoda(){
  digitalWrite(ENA, LOW);
  digitalWrite(IN1, LOW);
  digitalWrite(IN2, LOW);
}

void loop() {
  server.handleClient();
  if(nyala){
    if (roda) {
      Serial.println("test roda: kanan, laju: mundur");
      RodaKananMundur();
    } else {
      Serial.println("test roda: kanan, laju: maju");
      RodaKananMaju();
    }
  }else{
    resetRoda();
  }
}
```