# <p align="center"> Entregable 6 </p>
## 1. Hardware Electrónico ## 
## Esquema del Circuito Electrónico:

[![funbio3.png](https://i.postimg.cc/4N011fHk/funbio3.png)](https://postimg.cc/mtQMLGS8)

 ## Codigo para el actuador lineal(Cambio de polaridad) ##
    // Pines del L298N
    const int IN3 = 8;    // Dirección 1
    const int IN4 = 9;    // Dirección 2
    const int ENA = 10;   // Habilitador y control de velocidad (PWM)

    // Pin del joystick
    const int joystickY = A0; // Eje Y del joystick

    void setup() {
      pinMode(IN3, OUTPUT);
      pinMode(IN4, OUTPUT);
      pinMode(ENA, OUTPUT);

    digitalWrite(IN3, LOW);
    digitalWrite(IN4, LOW);

    Serial.begin(9600); // Monitor serial (opcional para depuración)
    }

    void loop() {
    int joystickValue = analogRead(joystickY); // Leer el valor del joystick
    Serial.println(joystickValue);            // Mostrar valor en el monitor serial

    // Determinar dirección y velocidad del motor
    if (joystickValue > 600) {  // Hacia adelante
    digitalWrite(IN3, HIGH);
    digitalWrite(IN4, LOW);

    int velocidad = map(joystickValue, 600, 1023, 0, 255); // Mapear a PWM
    analogWrite(ENA, velocidad);
    Serial.println("Motor hacia adelante");
    } else if (joystickValue < 400) {  // Hacia atrás
    digitalWrite(IN3, LOW);
    digitalWrite(IN4, HIGH);

    int velocidad = map(joystickValue, 400, 0, 0, 255); // Mapear a PWM
    analogWrite(ENA, velocidad);
    Serial.println("Motor hacia atrás");
    } else {  // Neutral (apagar motor)
    digitalWrite(IN3, LOW);
    digitalWrite(IN4, LOW);
    analogWrite(ENA, 0);
    Serial.println("Motor apagado");
    }

    delay(50); // Pausa para estabilidad
    }
## Diagrama de flujo:
[![temp-Image-LHw8n-M.avif](https://i.postimg.cc/CdT5s0Xc/temp-Image-LHw8n-M.avif)](https://postimg.cc/K3fmm6ZT)
## Codigo para Leds 5mm - FSR402 (Cambio de presión)

## 2. Avance del prototipado Electrónico: ## 
[![funbio2.jpg](https://i.postimg.cc/pXwSkY3B/funbio2.jpg)](https://postimg.cc/vcvXZ9Y1)
## 3. Impresión 3D: ##  
# <p align="center"> Actuador eléctrico</p>
[![Imagen-de-Whats-App-2024-10-29-a-las-16-14-08-513046b6.jpg](https://i.postimg.cc/fbLLN0W0/Imagen-de-Whats-App-2024-10-29-a-las-16-14-08-513046b6.jpg)](https://postimg.cc/18kP0Xq9)
# <p align="center"> Monitor </p>
[![Captura-de-pantalla-2024-10-29-235609.png](https://i.postimg.cc/vHVZ8sd3/Captura-de-pantalla-2024-10-29-235609.png)](https://postimg.cc/3d3T9zNv)
# <p align="center"> Base </p>
[![Captura-de-pantalla-2024-10-30-001553.jpg](https://i.postimg.cc/x8SnckQ5/Captura-de-pantalla-2024-10-30-001553.jpg)](https://postimg.cc/bDLK5wsS)
# <p align="center"> Brazo </p>
[![Captura-de-pantalla-2024-10-30-002056.jpg](https://i.postimg.cc/5Ngb2NR5/Captura-de-pantalla-2024-10-30-002056.jpg)](https://postimg.cc/WhdQ9jjt)
# <p align="center"> Ensamblado </p>
[![Captura-de-pantalla-2024-10-29-235704.png](https://i.postimg.cc/9fJWgXGF/Captura-de-pantalla-2024-10-29-235704.png)](https://postimg.cc/kVR3Bm1k)



