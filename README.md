# PR4_EricAyala

# PR4_PD_EricAyala

## PRACTICA 4:  SISTEMAS OPERATIVOS EN TIEMPO REAL

### Ejercicio Practico 1

**PROGRAMA:**

``` cpp
void setup()
{
Serial.begin(112500);
/* we create a new task here */
xTaskCreate(
anotherTask, /* Task function. */
"another Task", /* name of task. */
10000, /* Stack size of task */
NULL, /* parameter of the task */
1, /* priority of the task */
NULL); /* Task handle to keep track of created task */
}
/* the forever loop() function is invoked by Arduino ESP32 loopTask */
void loop()
{
Serial.println("this is ESP32 Task");
delay(1000);
}
/* this function will be invoked when additionalTask was created */
void anotherTask( void * parameter )
{
/* loop forever */
for(;;)
{
Serial.println("this is another Task");
delay(1000);
}
/* delete a task when finish,
Practica4.MD 2024-03-12
6 / 6
this will never happen because this is infinity loop */
vTaskDelete( NULL );
}
```
**FUNCIONAMIENTO**
- Utilizando la función `xTaskCreate()`, se crea una tarea, como su nombre indica. La funcion `AnotherTask()`, es la tarea creada en la funcion `setup()`, en la cual se imprime repetidamente el mensaje *"this is another task"*.

- En el bucle principal `loop()`, se imprime repetidamente el mensaje *"this is ESP32 Task"*. 

- Finalmente, se llama a `vTaskDelete(NULL)` para eliminar la tarea. Sin embargo, esta llamada nunca se ejecutará debido al bucle infinito dentro de anotherTask(), por lo que la tarea creada seguirá ejecutándose indefinidamente.

**Salida por el puerto serie**

Al ejecutar el programa, vemos:
```
this is ESP32 Task - (espera 1 segundo) - this is another Task - (espera 1 segundo) - this is ESP32 Task - (espera 1 segundo) - etc.
```

Después de las soluciones:
```
this is ESP32 Task -  this is another Task - (espera 1 segundo) - this is ESP32 Task -  this is another Task - (espera 1 segundo) - etc.
```
