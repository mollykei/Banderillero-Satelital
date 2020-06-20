## Manejo de GPIOs para módulo ESP32

Para el proyecto del Banderillero Satelital se utilizará la placa [Wipy 3.0](https://docs.pycom.io/datasheets/development/wipy3/) Esta placa tiene un micro ESP32, y se puede usar MicroPython como lenguage para desarrollar.


Lo primero que hice fue investigar las librerías que podía usar en esa placa con ese lenguaje, y llegué a documentación de MicroPython para la ESP32: [docs.micropython.org](https://docs.micropython.org/en/latest/esp32/quickref.html#pins-and-gpio)

![GPIO en ESP32](https://i.imgur.com/qw8sex3.png)



 A partir de esa documentación, llegué a la documentación del framework Espressif específico para el ESP32: [docs.espressif.com](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-reference/peripherals/gpio.html)
 
 ![doc-espressif](https://i.imgur.com/k2JOssT.png)
 
  En la documentación se muestran funciones básicas para menejo de los puertos GPIO, y también indica el link del repositorio de la librería y se llega a:
  
  [driver/include/driver/gpio.h](https://github.com/espressif/esp-idf/blob/7d75213/components/driver/include/driver/gpio.h)
  
  Entrando en el respoitorio entonces, en el directorio: ```esp-idf/components/driver/include/driver/gpio.h```
  
 Se encuentra el detalle de como configurar los puertos, por ejemplo:
 
 ```C
   esp_err_t gpio_reset_pin(gpio_num_t gpio_num);
```
 
 
