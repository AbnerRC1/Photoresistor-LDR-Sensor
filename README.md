<img src="Img_Escuela.png">

**Tecnológico​ ​Nacional​ ​de​ ​México Instituto Tecnológico de Tijuana**

***Departamento de Sistemas y Computación - Ingeniería en Sistemas Computacionales***

Sistemas Programables

  > Rene Solis Reyes

Abner Ramírez Castañeda

  > No. de control: 20211828

# Presentación

<center>
  <img src="Img_Titulo.png">
  <div>
    <h1>Descripción</h1>
    <p align="justify">
      El Photoresistor es un componente electrónico dependiente de la luz, esto significa que detecta y mide la intensidad de la luz que atrapa por medio de su sensor, con esta entrada puede manejar las operaciones del circuito al que está conectado.
    </p>
  <img src="Img_Sensor.png" width="200" height="170">
    <h1>Como se Componente</h1>
    <p align="justify">
      El Resistor Dependiente de la Luz es creado de materiales semiconductores para dejar al componente tener propiedades de sensibilidad a la luz; normalmente se han usado materiales como el sulfuro de cadmio “CdSe”, sulfuro de plomo “PbS” o antimoniuro de indio “InSb”.
    </p>
  <img src="Img_Estructura1.png" width="200" height="200">
    <p align="justify">
      Para fabricar un LDR de sulfuro de cadmio, se mezclan polvo de sulfuro de cadmio altamente purificado y materiales aglutinantes inertes. Luego esta mezcla se prensa y sinteriza. Los electrodos se evaporan al vacío sobre la superficie de un lado para formar peines entrelazados y se conectan los cables de conexión. Luego, el disco se monta en una envoltura de vidrio o se encapsula en plástico transparente para evitar la contaminación de la superficie. La curva de respuesta espectral del sulfuro de cadmio coincide con la del ojo humano. La longitud de onda de máxima sensibilidad es de aproximadamente 560-600 nm, que se encuentra en la parte visible del espectro. Cabe señalar que los dispositivos que contienen plomo o cadmio no cumplen con RoHS y su uso está prohibido en países que cumplen con las leyes RoHS.
    </p>
  <img src="Img_Estructura3.PNG" width="200" height="100">
    <h1>Cómo Funciona</h1>
    <p align="justify">
      Cuando la luz es atrapada por el material semiconductor, los fotones de luz son absorbidos por la red del semiconductor y parte de su energía se transfiere a los electrones.
    </p>
  <img src="Img_Estructura2.PNG" width="270" height="150">
    <p align="justify">
      La cantidad de energía transferida a los electrones les da a algunos de ellos suficiente energía para liberarse de la red cristalina y luego poder conducir electricidad. Esto da como resultado una reducción de la resistencia del semiconductor y, por tanto, de la resistencia global del LDR. El proceso es progresivo y, a medida que más luz incide sobre el semiconductor LDR, se liberan más electrones para conducir la electricidad y la resistencia cae aún más.
    </p>
    <h1>Tipos de Photoresistores</h1>
    <p align="justify">
      Fotorresistores intrínsecos: los fotorresistores intrínsecos utilizan materiales semiconductores no dopados, incluidos silicio o germanio. Los fotones que caen sobre el LDR excitan a los electrones moviéndose desde la banda de valencia a la banda de conducción. Como resultado, estos electrones quedan libres para conducir electricidad. Cuanta más luz incide sobre el dispositivo, más electrones se liberan y mayor es el nivel de conductividad, y esto se traduce en un menor nivel de resistencia.
    </p>
    <p align="justify">
      Fotorresistores extrínsecos: los fotorresistores extrínsecos se fabrican a partir de semiconductores de materiales dopados con impurezas. Estas impurezas o dopantes crean una nueva banda de energía por encima de la banda de valencia existente. Como resultado, los electrones necesitan menos energía para transferirse a la banda de conducción debido a la menor brecha de energía.
    </p>
    <h1>Símbolo del Photoresistor</h1>
    <p align="justify">
      En base al estándar IEC el símbolo dentro de un circuito tiene forma de un rectángulo con una entrada y una salida, y dos punteros apuntando hacia abajo. Algunas veces puede que se encuentre plasmado el símbolo con un círculo rodeandolo.
    </p>
  <img src="Img_Simbolo.PNG" width="150" height="100">
    <h1>Ejemplo de su uso</h1>
    <p align="justify">
      ...
    </p>
  <img src="Img_Circuito.PNG" width="200" height="300">
    <p align="justify">
      ...
    </p>
  <img src="Img_CircuitoIntensidad.PNG" width="350" height="100">
  </div>
</center>

# Código

```cpp
#include <LiquidCrystal_I2C.h>
#define LDR_PIN 2

const float GAMMA = 0.7;
const float RL10 = 50;

LiquidCrystal_I2C lcd(0x27, 20, 4);

void setup() {
  pinMode(LDR_PIN, INPUT);
  lcd.init();
  lcd.backlight();
}

void loop() {
  int analogValue = analogRead(A0);
  float voltage = analogValue / 1024. * 5;
  float resistance = 2000 * voltage / (1 - voltage / 5);
  float lux = pow(RL10 * 1e3 * pow(10, GAMMA) / resistance, (1 / GAMMA));

  lcd.setCursor(2, 0);
  lcd.print("Room: ");
  if (lux > 50)
  {
    lcd.print("Light!");
  }
  else
  {
    lcd.print("Dark  ");
  }

  lcd.setCursor(0, 1);
  lcd.print("Lux: ");
  lcd.print(lux);
  lcd.print("          ");

  delay(100);
}
```
