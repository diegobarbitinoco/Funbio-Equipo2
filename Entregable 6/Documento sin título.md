# <p align="center"> Entregable 6 </p>
## 1. Hardware Electrónico ## 
## Esquema del Circuito Electrónico:

[![funbio3.png](https://i.postimg.cc/4N011fHk/funbio3.png)](https://postimg.cc/mtQMLGS8)

 ## Ejecución del Código:
 
    // Declaración de pines  
    const int pinJoystickX \= A0; // Eje X del joystick  
    const int pinJoystickY \= A1; // Eje Y del joystick  
    const int pinJoystickBtn \= 2; // Botón del joystick  
      
    const int pinPressureSensor \= A2; // Sensor de presión  
    const int pinServo \= 9; // Servo motor  
    const int pinRelay \= 3; // Módulo relé  
    const int pinLED \= 13; // LED integrado en la placa Arduino  
      
    \#include \<Servo.h\> // Librería para manejar el servo motor  
    Servo myServo; // Creación del objeto servo  
      
    void setup() {  
      // Configuración de pines  
      pinMode(pinJoystickBtn, INPUT\_PULLUP); // Botón del joystick  
      pinMode(pinRelay, OUTPUT); // Relé  
      pinMode(pinLED, OUTPUT); // LED  
        
      myServo.attach(pinServo); // Asigna el pin del servo motor  
      myServo.write(90); // Posición inicial del servo (en grados)  
        
      Serial.begin(9600); // Inicia la comunicación serial para monitorear  
    }  
      
    void loop() {  
      // Lectura del joystick  
      int joystickX \= analogRead(pinJoystickX);  
      int joystickY \= analogRead(pinJoystickY);  
      int joystickBtnState \= digitalRead(pinJoystickBtn);  
      
      // Lectura del sensor de presión  
      int pressureValue \= analogRead(pinPressureSensor);  
        
      // Control del servo motor según el eje Y del joystick  
      int servoPosition \= map(joystickY, 0, 1023, 0, 180); // Mapea el valor del joystick a grados de 0 a 180  
      myServo.write(servoPosition); // Mueve el servo a la posición calculada  
      
      // Control del relé según el valor del sensor de presión  
      if (pressureValue \> 500\) { // Valor umbral ajustable para activar el relé  
        digitalWrite(pinRelay, HIGH); // Activa el relé  
      } else {  
        digitalWrite(pinRelay, LOW); // Desactiva el relé  
      }  
      
      // Control del LED con el botón del joystick  
      if (joystickBtnState \== LOW) { // Si el botón del joystick está presionado  
        digitalWrite(pinLED, HIGH); // Enciende el LED  
      } else {  
        digitalWrite(pinLED, LOW); // Apaga el LED  
      }  
      
      // Monitoreo de valores en el monitor serial  
      Serial.print("Joystick X: ");  
      Serial.print(joystickX);  
      Serial.print(" | Joystick Y: ");  
      Serial.print(joystickY);  
      Serial.print(" | Presión: ");  
      Serial.print(pressureValue);  
      Serial.print(" | Botón: ");  
      Serial.println(joystickBtnState);  
      
      delay(100); // Pequeña pausa para estabilidad}
      
## 2. Avance del prototipado Electrónico: ## 
[![funbio2.jpg](https://i.postimg.cc/pXwSkY3B/funbio2.jpg)](https://postimg.cc/vcvXZ9Y1)
## 3. Impresión 3D: ##  
# <p align="center"> Actuador eléctrico</p>

[![Captura-de-pantalla-2024-10-29-235418.png](https://i.postimg.cc/YSk9yyZ8/Captura-de-pantalla-2024-10-29-235418.png)](https://postimg.cc/yDQsDnVS)

# <p align="center"> Monitor </p>
[![Captura-de-pantalla-2024-10-29-235609.png](https://i.postimg.cc/vHVZ8sd3/Captura-de-pantalla-2024-10-29-235609.png)](https://postimg.cc/3d3T9zNv)
# <p align="center"> Base </p>
[![Captura-de-pantalla-2024-10-29-235631.png](https://i.postimg.cc/K8hvRHGF/Captura-de-pantalla-2024-10-29-235631.png)](https://postimg.cc/qzQdFQ6Z)
# <p align="center"> Brazo </p>
[![Captura-de-pantalla-2024-10-29-235647.png](https://i.postimg.cc/Jz37J50X/Captura-de-pantalla-2024-10-29-235647.png)](https://postimg.cc/dh1Kcd8Q)
# <p align="center"> Ensamblado </p>
[![Captura-de-pantalla-2024-10-29-235704.png](https://i.postimg.cc/9fJWgXGF/Captura-de-pantalla-2024-10-29-235704.png)](https://postimg.cc/kVR3Bm1k)



