 # **Integración Hardware \-Software \- Manufactura Digital** #

## 1. Introducción y Contextualización del Prototipo ##
   1.1 Descripción breve del proyecto: 

Un dispositivo que sirve como apoyo para realizar bipedestación y marcha corta, cuyo principal objetivo es permitir a personas con lesión medular incompleta realizar estas actividades con mayor independencia y comodidad.

## 2. Problemática abordada: ##

La necesidad principal es la de ayudar a las personas con lesión medular incompleta, con visto bueno a bipedestación y marcha corta, a tener un dispositivo de asistencia tecnológica/biomédica que permita al paciente pasar de una posición sentada a parada de manera independiente y más cómoda.

## 3. Objetivos de la fase de integración: ##
- Permitir al usuario controlar todo el proceso de bipedestación y marcha corta, mediante correas ajustables, un actuador lineal, soportes con agarre graduables y sensores de presión.  
- Tener los controles de las correas, el actuador lineal y los brazos de soporte graduables al alcance del usuario sin necesidad de movimientos incómodos o que requieran de asistencia.  
-  Brindar soporte, seguridad y comodidad al usuario mediante tres puntos de apoyo clave: rodillas, torso y pelvis.  
- Permitir al usuario tener las extremidades superiores libres manteniendo la bipedestación.  
  Un adicional es el de permitir al usuario simular el movimiento de agacharse para alcanzar nivel medios como cajones, repisas bajas, etc.  
    
## 4. Componentes del Prototipos: ##
   1. Lista de componentes principales:   
- Almacenar de energía:  
  	Bateria LiPo  
  	Bateria 6V-4A  
- Puente de recarga  
  	Módulo  TP4056
- Regular carga:  
  	Módulo MT3608  
    
- Detectar datos de presión:  
  	Sensor de presión FSR  
  	  
- Procesar datos de sensores:   
  	Arduino Uno
- Notificar buen ajuste de las correas  
  	Leds (rojo, amarillo y verde)  
  	  
- Controlar las correas:  
  	Controlador de motor L298N  
  	  
- Ayudar al usuario levantarse y sentarse:  
  	Actuador lineal   
  	  
- Controlar el actuador lineal:  
  	Joystick analógico   
  	  
- Motor DC  
  	  
- Ajustar el soporte de pelvis:  
  	Servomotor

		

- Dar apoyo para realizar bipedestación:  
  	Actuador lineal   
  2. Interacción entre componentes: 

La energía es suministrada por una batería Lipo y una batería 6V-4A, donde la primera alimenta los circuitos electrónicos como el Arduino Uno y los sensores, y la segunda se encarga de dispositivos de mayor consumo como el motor DC y el actuador lineal. El módulo TP4056 gestiona la recarga segura de la batería, mientras que el módulo MT3608 regula el voltaje para mantener un suministro estable.   
El sensor de presión FSR detecta la presion en las correas y envia datos al arduino uno, que procesa estas señales y activa los LEDs (rojo, amarillo y verde) para notificar el ajuste adecuado para el paciente. Además, el arduino controla el motor DC y el actuador lineal mediante el controlador de motor L298N y un joystick analógico, permitiendo ajustes dinámicos en las correas y asistencia para que el usuario se levante o se siente. Finalmente el servomotor ajusta el soporte de pelvis según las necesidades del usuario.

## 5. Diagrama de integración: ##
[![Captura-de-pantalla-2024-11-30-081327.jpg](https://i.postimg.cc/02bCQJhv/Captura-de-pantalla-2024-11-30-081327.jpg)](https://postimg.cc/rK24Zz8Z) 
## 6. Proceso de Integración ##
  ### 1. Plan de integración: ###
   El plan inicial consistía en:
- Identificar partes fáciles de modelar y empezar por esas.  
- Identificar partes que requerían de averiguar el mecanismo interno necesario para que cumpliesen sus funciones (brazos externos, brazo principal, monitor, etc.).  
- Verificar que los modelos 3D tuvieran las medidas correctas para el dispositivo a escala. Para ello realizar pruebas en el ensamblaje general.
- Realizar una lista de compra de los componentes necesarios para que el dispositivo cumpla con las funciones planificadas.  
- Programar cada componente por separado. Realizar pruebas del funcionamiento de cada una y anotar según los resultados que otro componente se iba a necesitar o que ajuste requería la programación.  
- Unir las programaciones  
## 7. Pruebas y Verificación ## 
     
   1. Descripción de pruebas funcionales:   
      El dispositivo cumple con los requerimientos de diseño establecidos, asegurando su funcionalidad, seguridad y comodidad. Se realizarán pruebas de resistencia estructural, ajuste, sensores de presión, así como portabilidad en espacios reducidos.  
        
   2. Resultados de pruebas:   
      Se estima que el dispositivo soporte 80kg sin presentar deformaciones, y las correas proporcionarán un soporte estable, la batería alcanzará 2 horas y el actuador lineal responderá adecuadamente a la transición de sentado a parado.  
        
   3. Evaluación de desempeño   
      El prototipo cumplió el objetivo buscado, nos brindará un adecuado soporte, comodidad y facilidad de uso para lograr una bipedestación segura de la posición sentada corta con un paciente con control de tronco a bipedo para luego continuar con la marcha.  
        
## 8. Conclusiones y Próximos Pasos ##  
     
   1. Integración de componentes: Se espera que el circuito eléctrico cumpla su función una vez ya integrado a la estructura impresa y cortada a láser.  
        
   2. Prueba de componentes: Los componentes FSR402, Motor de actuador funcionan correctamente. Se espera que los servomotores actúen de acuerdo a el joystick que los acciona.

