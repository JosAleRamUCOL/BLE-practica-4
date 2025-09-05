## README – Actividad IV: Fundamentos y aplicación del módulo Bluetooth AT09



##### 1\. Objetivo General



Implementar un sistema inalámbrico con Bluetooth AT-09 y ESP32 para intercambio de mensajes JSON vía MQTT en un entorno inteligente.

##### 

##### 2\. Objetivos Específicos



1. Identificar los parámetros eléctricos y de comunicación del módulo AT-09.
2. Configurar el módulo AT-09 utilizando comandos AT y posteriormente automatizar la conexión en ESP32.	



1. Implementar una conexión bidireccional entre el ESP32, el módulo BLE y un dispositivo móvil.
2. Formatear mensajes en JSON utilizando la librería ArduinoJSON.
3. Transmitir y recibir mensajes JSON a través de un broker MQTT público.
4. Visualizar estados y validaciones mediante indicadores LED.



##### 3\. Competencias



* Integración de hardware y software en sistemas BLE.
* Configuración y validación de conexiones Bluetooth y MQTT.
* Diseño de mensajes JSON estructurados.
* Trabajo en equipo y documentación profesional.
* Aplicación de prácticas éticas en el manejo de datos inalámbricos.



##### 4\. Tabla de Contenidos



1. Objetivo General
2. Objetivos Específicos
3. Competencias
4. Tabla de Contenidos
5. Descripción
6. Requisitos
7. Instalación y Configuración
8. Conexiones de Hardware
9. Parámetros Técnicos del AT-09
10. Uso y ejemplos de Código
11. Resultados de Prueba
12. Consideraciones Éticas y de Seguridad
13. Formato de Salida (JSON)
14. Solución de Problemas
15. Contribuciones
16. Referencias



##### 5\. Descripción



En el marco de los entornos inteligentes y el Internet de las Cosas (IoT), la comunicación inalámbrica de bajo consumo es fundamental. El módulo AT-09, que usa Bluetooth Low Energy, nos permite enlazar un ESP32 con un celular para enviar y recibir información. En esta práctica lo usamos para armar un pequeño gateway que conecta Bluetooth con WiFi, y que a través de un broker MQTT intercambia mensajes en formato JSON. Además, se añadieron LEDs como indicadores para mostrar de forma clara el estado de la conexión y las acciones realizadas.

##### 

##### 6\. Requisitos



Hardware



* ESP32 con cable USB.
* Módulo Bluetooth AT-09 (o HM-10).
* 7 LEDs de colores (rojo, azul, verde, amarillo, blanco, naranja y violeta/rosa).
* Resistencias para cada LED según su color.
* Protoboard(400 u 830 puntos).
* Cables Dupont (Ya sea HxH, MxM, HxM).
* Equipo de computo y/o laptop.



Software y Bibliotecas



* Arduino IDE.
* MQTT Explorer
* Librería ArduinoJSON, PubSuclient, Time.h, SoftwareSerial.h y el Wifi.
* Cliente MQTT (Broker público Mosquitto).
* Aplicación móvil “Serial Bluetooth Terminal”(O aplicación similar compatible con el estándar para WiFi del ESP-32).



Conocimientos Previos



* Programación básica en C/C++ con Arduino IDE.
* Fundamentos de redes inalámbricas (BLE, Wi-Fi).
* Uso de JSON para estructuración de datos.
* Conexiones en protoboard.



##### 7\. Instalación y Configuración



* Instalar Arduino IDE y MQTT Explorer en los equipo de computos y/o laptops.
* Agregar soporte para placas ESP32 en el gestor de placas.
* Instalar la librería Wifi, Time.h, ArduinoJSON, SoftwareSerial.h y PubSubClient desde el gestor de librerías del ArduinoID.
* Configurar el ESP32 con los pines de salida para LEDs.
* Emparejar el AT-09 con la aplicación móvil Serial Bluetooth Terminal.
* Configurar el broker MQTT(Mosquitto).



 

##### 8\. Conexiones de Hardware



Conexiones del módulo AT-09 con el ESP32:



| Módulo AT-09 | Pin de la placa (ESP32) | Función                               |

| ------------ | ----------------------- | ------------------------------------- |

| VCC          | 3.3V                    | Alimentación del módulo BLE           |

| GND          | GND                     | Tierra común                          |

| TXD          | GPIO16                  | Comunicación del AT-09 hacia el ESP32 |

| RXD          | GPIO17                  | Comunicación del ESP32 hacia el AT-09 |

| STATE        | GPIO27                  | Inicliaza con los datos               |



Conexiones de LEDs al ESP32:



| LED (color)  | Pin de la placa (ESP32) | Función                                                    |

| ------------ | ----------------------- | ---------------------------------------------------------- |

| Verde        | GPIO13                  | Mensaje enviado (1 s)                                      |

| Amarillo     | GPIO14                  | Mensaje recibido con ID válido (1 s)                       |

| Rojo         | GPIO12                  | Bluetooth no emparejado (fijo)                             |

| Azul         | GPIO26                  | Bluetooth emparejado (fijo) / emparejando (parpadeo 0.5 s) |

| Blanco       | GPIO25                  | Estado Wi-Fi: parpadeo (buscando), fijo (conectado)        |

| Naranja      | GPIO33                  | Mensaje recibido con ID inválido (1 s)                     |

| Rojo         | GPIO32                  | Controlado mediante el campo "accion" del JSON             |



##### 9\. Parámetros Técnicos del AT-09 







| Parámetro                | Valor Típico | Unidad |

|--------------------------|--------------|--------|

| Voltaje de operación     | 3.3          | V      |

| Corriente de operación   | 8.5          | mA     |

| Interfaz de comunicación | UART         | -      |

| Frecuencia de operación  | 2.4          | GHz    |

| Versión de Bluetooth     | 4.0 (BLE)    | -      |



##### 10\. Uso y ejemplos de Código









##### 11\. Resultados de Prueba 

* Registro exitoso del nombre del dispositivo y del estado de emparejamiento.  
* Visualización exitosa en serial de los mensajes enviados y las respuestas recibidas desde el módulo.  
* Registro exitoso en MQTT para cada evento del paquete JSON.  



##### 12\. Consideraciones Éticas y de Seguridad 

* Respetar la privacidad de los usuarios, evitando la recolección innecesaria de datos.  
* Asegurar la transmisión de datos mediante protocolos de cifrado.  
* Prevenir vulnerabilidades que permitan accesos no autorizados.  
* Limitar el uso del módulo a fines académicos y de investigación.  
* Garantizar la seguridad física del dispositivo durante las pruebas.  



##### 13\. Formato de Salida (JSON)

Estructura JSON:

{

&nbsp; "id": "Nombre del equipo",

&nbsp; "origen": "dispositivo",

&nbsp; "accion": "ON/OFF",

&nbsp; "fecha": "DD-MM-AAAA",	



&nbsp; "hora": "HH:MM:SS"

}



Campos:

* id: String - Iniciales identificadoras del equipo.  
* origen: String - Dispositivo que envió el mensaje.  
* accion: String - Comando ON/OFF para controlar LED.  
* fecha: String - Fecha de generación del mensaje.  
* hora: String - Hora de generación del mensaje.  



La salida del JSON será mediante los topics CPRIH/TX y CPRIH/RX.

El topic CPRIH/TX envia los datos de la consola Serial al Bróker MQTT.

En cambio, el topic CPRIH/RX envia datos desde el Bróker MQTT hacia la consola Serial,



##### 14\. Solución de Problemas

| Problema                                       | Solución |

|------------------------------------------------|----------|

| El módulo no responde                          | Verificar las conexiones de alimentación (3.3V y GND). Revisar que el voltaje no exceda el rango permitido. |

| No se establece conexión Bluetooth             | Asegurarse de que el dispositivo esté visible en el escaneo. Confirmar que se utiliza la versión BLE adecuada y que el módulo no esté emparejado previamente con otro dispositivo. |

| Datos ilegibles en la comunicación de la UART  | Revisar la configuración de baudios en el microcontrolador y en el monitor serie. Ajustar a 9600 bps, que es el valor por defecto. |

| Desconexión frecuente del módulo               | Comprobar la distancia entre los dispositivos. Evitar interferencias en la banda de 2.4 GHz (Wi-Fi, microondas). |

| El módulo responde con comandos AT incorrectos | Verificar que los comandos estén escritos en mayúsculas y con el retorno de carro adecuado (`\\r\\n`). |

| No se conecta a la red Wi-Fi                   | 1. Verificar que las credenciales SSID y contraseña en el código sean correctas. <br> 2. Comprobar que la red Wi-Fi esté disponible y tenga cobertura. <br> 3. Asegurarse de que el firmware del ESP32 soporte el estándar Wi-Fi de la red (ej., 2.4 GHz). <br> 4. Reiniciar el ESP32 para forzar un nuevo intento de conexión. |

| La conexión Wi-Fi es inestable y se cae        | 1. Revisar la potencia de la señal Wi-Fi (RSSI). Si es baja, acercar el dispositivo al router. <br> 2. Implementar una rutina de reconexión automática en el código para manejar caídas de red. |

| No se puede publicar mensajes en el bróker MQTT | 1. Confirmar que las credenciales del bróker (usuario, contraseña) sean correctas. <br> 2. Verificar que la URL o IP del bróker y el puerto (usualmente 1883) estén bien configurados.  3. Comprobar la conexión a Internet del ESP32. Si el Wi-Fi falla, MQTT también lo hará. <br> 4. Usar un cliente MQTT de prueba (como MQTT Explorer) para verificar que el bróker esté funcionando. |

| No se reciben mensajes suscritos del bróker MQTT | 1. Verificar que el tópico de suscripción esté escrito exactamente igual, respetando mayúsculas y minúsculas. <br> 2. Asegurarse de que la suscripción se realice correctamente después de que la conexión MQTT se haya establecido. <br> 3. Comprobar que el bróker esté enviando los mensajes al tópico correcto. |



##### 15\. Contribuciones 

La práctica fue realizada en modalidad colaborativa, mediante sesiones presenciales con la participación de todos los integrantes del equipo. Cada miembro asumió un rol específico en la configuración, pruebas y documentación de la actividad.





##### 16\. Referencias bibliográficas



* Llamas, L. (2024, 8 diciembre). Cómo instalar Mosquitto, el popular broker MQTT. Luis Llamas. https://www.luisllamas.es/como-instalar-mosquitto-el-broker-mqtt/
* Arduino Software. (2018, 3 abril). arduino.cc. Recuperado 4 de septiembre de 2025, de https://www.arduino.cc/en/software/
* Llamas, L. (2023, 18 agosto). Pinout y detalles del hardware del ESP32. Luis Llamas. https://www.luisllamas.es/esp32-detalles-hardware-pinout/
* Santos, S., \& Santos, S. (2024, 12 junio). Getting Date and Time with ESP32 (NTP Client) | Random Nerd Tutorials. Random Nerd Tutorials. https://randomnerdtutorials.com/esp32-ntp-client-date-time-arduino-ide/
* UNIT Electronics. (2025, 3 septiembre). Bluetooth 4.0 AT09 HM10 CC2541 BLE - UNIT Electronics. https://uelectronics.com/producto/bluetooth-4-0-at09-hm10-cc2541-ble/?srsltid=AfmBOoo7cPtdSfseKJYwUbs\_qV-K4L84qhJ9lfj-W78SETI1upG53Tkr
* Santos, S., \& Santos, S. (2023, 23 febrero). ESP32 Useful Wi-Fi Library Functions (Arduino IDE) | Random Nerd Tutorials. Random Nerd Tutorials. https://randomnerdtutorials.com/esp32-useful-wi-fi-functions-arduino/
* SoftwareSerial Library | Arduino Documentation. (n.d.). https://docs.arduino.cc/learn/built-in-libraries/software-serial/
* Bluetooth Special Interest Group (SIG). (2022). Bluetooth Core Specification Version 5.3. https://www.bluetooth.com/specifications/specs/core-specification-5-3/  
* Ovidiu, I. (2019). Arduino Bluetooth: Blueprints. Packt Publishing. 
