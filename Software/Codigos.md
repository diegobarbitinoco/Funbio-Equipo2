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
