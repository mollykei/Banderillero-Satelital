## Manejo de GPIOs para módulo ESP32

Para el proyecto del Banderillero Satelital se utilizará la placa [Wipy 3.0](https://docs.pycom.io/datasheets/development/wipy3/) Esta placa tiene un micro ESP32, y se puede usar MicroPython como lenguahe para desarrollar.[docs.micropython.org](https://docs.micropython.org/en/latest/esp32/quickref.html#pins-and-gpio)


Lo primero que hice fue investigar las librerías que podía usar en esa placa con ese lenguaje, y llegué a documentación de MicroPython para la ESP32: 

![GPIO en ESP32](https://imgur.com/qw8sex3)



 A partir de esa documentación, llegué al repositorio del framework Espressif específico para el ESP32, y pude revisar la estrucura a mas bajo nivel y  el manejo de los GPIOs [https://github.com/espressif/esp-idf](https://github.com/espressif/esp-idf)
