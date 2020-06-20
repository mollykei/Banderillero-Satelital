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
   // Resetear un GPIO
   esp_err_t gpio_reset_pin(gpio_num_t gpio_num);
   // Setear direccion en un GPIO
   esp_err_t gpio_set_direction(gpio_num_t gpio_num, gpio_mode_t mode);
   // Obtener valor de un GPIO
   int gpio_get_level(gpio_num_t gpio_num);
```
 
 
 Investigo más sobre la función para resetear un GPIO y llego al directorio ```esp-idf/components/driver/gpio.c```donde se detalla  ```esp_err_t gpio_reset_pin(gpio_num_t gpio_num)```:

```C
 esp_err_t gpio_reset_pin(gpio_num_t gpio_num)
 {
     assert(gpio_num >= 0 && GPIO_IS_VALID_GPIO(gpio_num));
     gpio_config_t cfg = {
         .pin_bit_mask = BIT64(gpio_num),
         .mode = GPIO_MODE_DISABLE,
         //for powersave reasons, the GPIO should not be floating, select pullup
         .pull_up_en = true,
         .pull_down_en = false,
         .intr_type = GPIO_INTR_DISABLE,
     };
     gpio_config(&cfg);
     return ESP_OK;
 }
```
 
 La variable ```gpio_num_t```se encuentra definida en ```esp-idf/components/soc/include/hal/gpio_types.h```
 
 ```C
 typedef enum {
     GPIO_NUM_NC = -1,    /*!< Use to signal not connected to S/W */
     GPIO_NUM_0 = 0,     /*!< GPIO0, input and output */
     GPIO_NUM_1 = 1,     /*!< GPIO1, input and output */
     GPIO_NUM_2 = 2,     /*!< GPIO2, input and output */
     GPIO_NUM_3 = 3,     /*!< GPIO3, input and output */
     GPIO_NUM_4 = 4,     /*!< GPIO4, input and output */
     GPIO_NUM_5 = 5,     /*!< GPIO5, input and output */
     GPIO_NUM_6 = 6,     /*!< GPIO6, input and output */
     GPIO_NUM_7 = 7,     /*!< GPIO7, input and output */
     GPIO_NUM_8 = 8,     /*!< GPIO8, input and output */
     GPIO_NUM_9 = 9,     /*!< GPIO9, input and output */
     GPIO_NUM_10 = 10,   /*!< GPIO10, input and output */
     GPIO_NUM_11 = 11,   /*!< GPIO11, input and output */
     GPIO_NUM_12 = 12,   /*!< GPIO12, input and output */
     GPIO_NUM_13 = 13,   /*!< GPIO13, input and output */
     GPIO_NUM_14 = 14,   /*!< GPIO14, input and output */
     GPIO_NUM_15 = 15,   /*!< GPIO15, input and output */
     GPIO_NUM_16 = 16,   /*!< GPIO16, input and output */
     GPIO_NUM_17 = 17,   /*!< GPIO17, input and output */
     GPIO_NUM_18 = 18,   /*!< GPIO18, input and output */
     GPIO_NUM_19 = 19,   /*!< GPIO19, input and output */
     GPIO_NUM_20 = 20,   /*!< GPIO20, input and output */
     GPIO_NUM_21 = 21,   /*!< GPIO21, input and output */
 #if CONFIG_IDF_TARGET_ESP32
     GPIO_NUM_22 = 22,   /*!< GPIO22, input and output */
     GPIO_NUM_23 = 23,   /*!< GPIO23, input and output */

     GPIO_NUM_25 = 25,   /*!< GPIO25, input and output */
 #endif
     /* Note: The missing IO is because it is used inside the chip. */
     GPIO_NUM_26 = 26,   /*!< GPIO26, input and output */
     GPIO_NUM_27 = 27,   /*!< GPIO27, input and output */
     GPIO_NUM_28 = 28,   /*!< GPIO28, input and output */
     GPIO_NUM_29 = 29,   /*!< GPIO29, input and output */
     GPIO_NUM_30 = 30,   /*!< GPIO30, input and output */
     GPIO_NUM_31 = 31,   /*!< GPIO31, input and output */
     GPIO_NUM_32 = 32,   /*!< GPIO32, input and output */
     GPIO_NUM_33 = 33,   /*!< GPIO33, input and output */
     GPIO_NUM_34 = 34,   /*!< GPIO34, input mode only(ESP32) / input and output(ESP32-S2) */
     GPIO_NUM_35 = 35,   /*!< GPIO35, input mode only(ESP32) / input and output(ESP32-S2) */
     GPIO_NUM_36 = 36,   /*!< GPIO36, input mode only(ESP32) / input and output(ESP32-S2) */
     GPIO_NUM_37 = 37,   /*!< GPIO37, input mode only(ESP32) / input and output(ESP32-S2) */
     GPIO_NUM_38 = 38,   /*!< GPIO38, input mode only(ESP32) / input and output(ESP32-S2) */
     GPIO_NUM_39 = 39,   /*!< GPIO39, input mode only(ESP32) / input and output(ESP32-S2) */
 #if GPIO_PIN_COUNT > 40
     GPIO_NUM_40 = 40,   /*!< GPIO40, input and output */
     GPIO_NUM_41 = 41,   /*!< GPIO41, input and output */
     GPIO_NUM_42 = 42,   /*!< GPIO42, input and output */
     GPIO_NUM_43 = 43,   /*!< GPIO43, input and output */
     GPIO_NUM_44 = 44,   /*!< GPIO44, input and output */
     GPIO_NUM_45 = 45,   /*!< GPIO45, input and output */
     GPIO_NUM_46 = 46,   /*!< GPIO46, input mode only */
 #endif
     GPIO_NUM_MAX,
 /** @endcond */
 } gpio_num_t;
```
