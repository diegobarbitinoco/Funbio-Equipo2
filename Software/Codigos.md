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
## Codigo para Leds 5mm - FSR402 (Cambio de presión) ##

     // Pines para los LEDs
    const int ledRojo = 8;
    const int ledAmarillo = 9;
    const int ledVerde = 10;

    // Pin del sensor de presión
    const int sensorPresion = A0;

    // Umbrales de presión (ajustar según el rango del FR402)
    const int umbralRojo = 50;    // Presión baja
    const int umbralAmarillo = 100; // Presión media
    const int umbralVerde = 150;   // Presión alta

    void setup() {
      // Configurar pines de los LEDs como salida
      pinMode(ledRojo, OUTPUT);
      pinMode(ledAmarillo, OUTPUT);
      pinMode(ledVerde, OUTPUT);

      // Iniciar comunicación serial para depuración
      Serial.begin(9600);
    }

    void loop() {
      // Leer el valor del sensor de presión
      int presion = analogRead(sensorPresion);
      Serial.print("Presión: ");
      Serial.println(presion);

      // Encender LEDs según los niveles de presión
      if (presion < umbralRojo) {
    encenderLed(ledRojo);       // Baja presión → LED rojo
      } else if (presion > umbralRojo && presion < umbralAmarillo) {
    encenderLed(ledAmarillo);   // Media presión → LED amarillo
      } else if (presion > umbralAmarillo) {
    encenderLed(ledVerde);      // Alta presión → LED verde
      } else {
    apagarLeds();               // Apagar LEDs si no se cumple ningún umbral
      }

      delay(100); // Pequeña pausa para estabilidad
    }

    // Función para encender un LED y apagar los demás
    void encenderLed(int led) {
      digitalWrite(ledRojo, led == ledRojo ? HIGH : LOW);
      digitalWrite(ledAmarillo, led == ledAmarillo ? HIGH : LOW);
      digitalWrite(ledVerde, led == ledVerde ? HIGH : LOW);
    }

    // Función para apagar todos los LEDs
    void apagarLeds() {
      digitalWrite(ledRojo, LOW);
      digitalWrite(ledAmarillo, LOW);
      digitalWrite(ledVerde, LOW);
    }
## Codigo Final ##
    #include <Servo.h> // Librería para controlar servomotores

    // --- Control de Servomotores ---
    const int joystickYServos = A0; // Eje Y del joystick para los servos
    Servo servo1; // Servomotor 1
    Servo servo2; // Servomotor 2

    // Pines de control para los servos
    const int servo1Pin = 9;
    const int servo2Pin = 10;
    
    // Zona muerta para el eje Y del joystick
    int deadZoneMin = 480;
    int deadZoneMax = 530;
    
    // --- Control del Motor Lineal ---
    const int IN3 = 3;   // Dirección 1
    const int IN4 = 4;   // Dirección 2
    const int ENA = 5;   // Habilitador y control de velocidad (PWM)
    const int joystickYMotor = A1; // Eje Y del joystick para el motor
    
    // --- Control de LEDs y Sensor de Presión ---
    const int ledRojo = 6;
    const int ledAmarillo = 7;
    const int ledVerde = 8;
    const int sensorPresion = A2;
    
    // Umbrales de presión
    const int umbralRojo = 100;    
    const int umbralAmarillo = 150; 
    const int umbralVerde = 200;

    // Estado de los servos (para evitar múltiples llamadas a attach/detach innecesarias)
    bool servosActivos = true;
    
    void setup() {
      // Configuración de los servos
      servo1.attach(servo1Pin);
      servo2.attach(servo2Pin);
      servo1.write(90);
      servo2.write(90);
    
      // Configuración del motor lineal
      pinMode(IN3, OUTPUT);
      pinMode(IN4, OUTPUT);
      pinMode(ENA, OUTPUT);
      digitalWrite(IN3, LOW);
      digitalWrite(IN4, LOW);
    
      // Configuración de LEDs
      pinMode(ledRojo, OUTPUT);
      pinMode(ledAmarillo, OUTPUT);
      pinMode(ledVerde, OUTPUT);
    
      // Comunicación serial para depuración
      Serial.begin(9600);
    }

    void loop() {
      // --- Control de Servomotores ---
      controlarServos();
    
      // --- Control del Motor Lineal ---
      controlarMotorLineal();
    
      // --- Control de LEDs y Sensor de Presión ---
      controlarLeds();
    }
    
    // Función para controlar los servomotores
    void controlarServos() {
      int joystickValueY = analogRead(joystickYServos);
    
      if (joystickValueY > deadZoneMax || joystickValueY < deadZoneMin) {
        // Mapear valores y mover servos
        int servo1Pos = map(joystickValueY, 0, 1023, 0, 180);
        int servo2Pos = map(joystickValueY, 0, 1023, 180, 0);

    if (!servosActivos) { // Conectar servos si no estaban activos
      servo1.attach(servo1Pin);
      servo2.attach(servo2Pin);
      servosActivos = true;
    }

    servo1.write(servo1Pos);
    servo2.write(servo2Pos);

    Serial.print("Joystick (Y - Servos): ");
    Serial.print(joystickValueY);
    Serial.print(" → Servo1: ");
    Serial.print(servo1Pos);
    Serial.print(" | Servo2: ");
    Serial.println(servo2Pos);
      } else {
        if (servosActivos) { // Desconectar servos si están en la zona muerta
          servo1.detach();
          servo2.detach();
          servosActivos = false;
        }

    Serial.println("Joystick (Y - Servos) en zona muerta, señales desactivadas");
      }
    
      delay(15);
    }

    // Función para controlar el motor lineal
    void controlarMotorLineal() {
      int joystickValue = analogRead(joystickYMotor);
      Serial.print("Joystick (Y - Motor): ");
      Serial.println(joystickValue);
    
      if (joystickValue > 600) {
        digitalWrite(IN3, HIGH);
        digitalWrite(IN4, LOW);
        int velocidad = map(joystickValue, 600, 1023, 0, 255);
        analogWrite(ENA, velocidad);
        Serial.println("Motor hacia adelante");
      } else if (joystickValue < 400) {
        digitalWrite(IN3, LOW);
        digitalWrite(IN4, HIGH);
        int velocidad = map(joystickValue, 400, 0, 0, 255);
        analogWrite(ENA, velocidad);
        Serial.println("Motor hacia atrás");
      } else {
        digitalWrite(IN3, LOW);
        digitalWrite(IN4, LOW);
        analogWrite(ENA, 0);
        Serial.println("Motor apagado");
      }
    
      delay(100);
    }

    // Función para controlar LEDs según la presión
    void controlarLeds() {
      int presion = analogRead(sensorPresion);
      Serial.print("Presión: ");
      Serial.println(presion);
    
      if (presion < umbralRojo && presion> 50) {
        encenderLed(ledRojo);
      } else if (presion > umbralRojo && presion < umbralAmarillo) {
        encenderLed(ledAmarillo);
      } else if (presion > umbralAmarillo) {
        encenderLed(ledVerde);
      } else {
        apagarLeds();
      }
    
      delay(100);
    }
    
    // Encender un LED y apagar los demás
    void encenderLed(int led) {
      digitalWrite(ledRojo, led == ledRojo ? HIGH : LOW);
      digitalWrite(ledAmarillo, led == ledAmarillo ? HIGH : LOW);
      digitalWrite(ledVerde, led == ledVerde ? HIGH : LOW);
    }
    
    // Apagar todos los LEDs
    void apagarLeds() {
      digitalWrite(ledRojo, LOW);
      digitalWrite(ledAmarillo, LOW);
      digitalWrite(ledVerde, LOW);
    }
