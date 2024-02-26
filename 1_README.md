# Primeros Pasos

Se usara el ARDUINO con el CHIP ATMEGA 328P. Cuando se use otro se especificara.

## Prendiendo y Apagado en BuildIn LED

```c++
void setup() {
  // Configura el pin del LED incorporado como salida
  pinMode(LED_BUILTIN, OUTPUT);
}

void loop() {
  // Enciende el LED
  digitalWrite(LED_BUILTIN, HIGH);
  // Espera 1 segundo
  delay(1000);
  // Apaga el LED
  digitalWrite(LED_BUILTIN, LOW);
  // Espera 1 segundo
  delay(1000);
}
```

Recuerda que Arduino IDE trabaja con un dialecto simplificado de C++ que incluye algunas bibliotecas y funciones específicas de Arduino para simplificar la programación de microcontroladores Arduino. Aunque la sintaxis básica es similar a la de C++, el entorno Arduino proporciona algunas abstracciones y simplificaciones para facilitar la escritura de código para personas con menos experiencia en programación.

Tambien podemos usar otra version, donde se declara el PIN 13 como salida, esta vez el led se prendera y apagara mas rapido:

```c++
void setup() {
  pinMode(13, OUTPUT);
}

void loop() {
  digitalWrite(13, HIGH);   // turn the LED on (HIGH is the voltage level)
  delay(250);                       // wait for a second
  digitalWrite(13, LOW);    // turn the LED off by making the voltage LOW
  delay(250);                       // wait for a second
}
```

Tambien es posible sacar un cable desde el PIN13 para que muestre la salida del BuildIn Led en un Led externo, veremos que se prende y apaga el LED:

![](https://i.imgur.com/FfTWnpc.png)

### Usando el ATtiny85

Basado en: **ATMEGA/ATtiny85/1_Blink**

https://www.instructables.com/How-to-Program-an-Attiny85-From-an-Arduino-Uno/

https://homemadehardware.com/guides/programming-an-attiny85/



https://onedrive.live.com/?WT.mc_id=PROD%5FOL%2DWeb%5FInApp%5FLeftNav%5FFreeOfficeBarOD&ocid=PROD%5FOL%2DWeb%5FInApp%5FLeftNav%5FFreeOfficeBarOD&cid=AD9B83AB948A9AAF&id=AD9B83AB948A9AAF%2125951&parId=AD9B83AB948A9AAF%2125623&o=OneUp 

https://www.youtube.com/watch?v=AmpHIHM41Hw 

The ATtiny85 is a microcontroller in a similar vein to the Arduino, but with much less IO pins, smaller memory and a smaller form factor. Ideal para pequeños proyectos.

1.  install los *supportive drivers*: ir al ArduinoIDE

File--> Additional preferences y copiar este codigo: 

https://raw.githubusercontent.com/damellis/attiny/ide-1.6.x-boards-manager/package_damellis_attiny_index.json

![](https://i.imgur.com/tjZ8iC0.png)

Una vez le des OK indicara que esta descargando el .json

2. Ir a Tools-->Board Manager y buscar ATtiny, e instala la de David A. Mellis

![](https://i.imgur.com/n74N8J7.png)

The ATtiny85 board should now be added ! Go to Tools--> Board-->Attiny85.

3. Set the Arduino Uno Into ISP Mode

In the Arduino IDE select File-->Examples--> 11. Arduino ISP-->ArduinoISP

and uploaded to the Arduino Uno as a normal code.

4. Configuracion de Pines 

![](https://i.imgur.com/PJUJwlj.png)

5. Conectando el Arduino Uno al ATtiny85

![](https://i.imgur.com/56Lim6P.png)

Recuerda colocar un capacitor de 10uF entre GND y RESET en el ARDUINO. This is to avoid Arduino from being auto-reset when we upload the program to the Attiny85.

6. Making the ATtiny85 Arduino Compatible

- Go to Tools -> Board switch to attiny(ATtiny25/45/85)

![](https://i.imgur.com/nTiUGtq.png)

- Go to Tools -> Board scroll to the bottom select ATtiny25/45/85

- Under Tools -> Processor--> 8 MHz (internal)

- Under Tools-->Programmer-->Arduino as ISP

- Check that all wiring, capacitor, and board selections are correct

![](https://i.imgur.com/38mPuZi.png)

- Finally select Burn Bootloader: sin problemas

7. Uploading the Blink Sketch

```c++
int LED = 0;
// the setup function runs once when you press reset or power the board
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalWrite(LED, HIGH);   // turn the LED on (HIGH is the voltage level)
  delay(1000);                       // wait for a second
  digitalWrite(LED, LOW);    // turn the LED off by making the voltage LOW
  delay(1000);                       // wait for a second
}
```

Y no funciono 😫😫😫: dice que A programmer is required to upload.

Corregi el problema asi: We are going to upload code using our ISP, we are NOT going to use the normal serial port method of uploading code. So, with everything powered on and connected, go up to the Sketch menu and select **Upload Using Programmer**. 🆗

![](https://i.imgur.com/6WFyy0h.png)

Realizamos el montaje, conectano un LED al pin 5 del ATtiny85. El Led se prende y apaga cada segundo😊
