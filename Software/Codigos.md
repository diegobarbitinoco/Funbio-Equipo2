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
