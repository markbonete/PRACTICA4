# PRACTICA4
## Codi sencer
```cpp
#include <Arduino.h>

void anotherTask( void * parameter );

void setup() {
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

void loop() {
  Serial.println("this is ESP32 Task");
  delay(1000);
}

void anotherTask( void * parameter ) {
  /* loop forever */
  for(;;)
  {
  Serial.println("this is another Task");
  delay(1000);
  }
/* delete a task when finish, this will never happen because this is infinity loop */
vTaskDelete( NULL );
}
```

### Llibreries Necessàries
```cpp
#include <Arduino.h>
```
Aquesta línia inclou la llibreria bàsica d'Arduino necessària per al funcionament del codi.

### Declaració de la Funció de la Nova Tasca
```cpp
void anotherTask(void * parameter);
```
Es declara la funció anotherTask que defineix el codi que s'executarà a la nova tasca.

### Setup
```cpp
void setup() {
  Serial.begin(115200);
  /* we create a new task here */
  xTaskCreate(
    anotherTask, /* Task function. */
    "another Task", /* name of task. */
    10000, /* Stack size of task */
    NULL, /* parameter of the task */
    1, /* priority of the task */
    NULL); /* Task handle to keep track of created task */
}
```
1. Inicialització Serial: S'inicia la comunicació serial a 115200 bps per permetre la comunicació amb l'ordinador o un altre dispositiu a través del port serial.
2. Creació de Nova Tasca: Es crea una nova tasca utilitzant xTaskCreate():
- anotherTask: La funció que defineix el codi que s'executarà en la nova tasca.
- "another Task": El nom de la tasca (per a finalitats de depuració).
- 10000: La mida de la pila de la tasca (en paraules, no en bytes).
- NULL: Paràmetre de la tasca (en aquest cas, no s'envia cap paràmetre).
- 1: La prioritat de la tasca (les prioritats més altes tenen més preferència).
- NULL: El manejador de la tasca (no es guarda el manejador en aquest cas).

### Loop
```cpp
void loop() {
  Serial.println("this is ESP32 Task");
  delay(1000);
}
```
El bucle principal (loop) fa el següent:
1. Imprimir Missatge: Mostra "this is ESP32 Task" a la consola serial.
2. Retard Curt: Introduïu un retard d'1 segon (delay(1000)) abans de repetir el bucle.

### Funció de la Nova Tasca
```cpp
void anotherTask(void * parameter) {
  /* loop forever */
  for(;;) {
    Serial.println("this is another Task");
    delay(1000);
  }
  /* delete a task when finish, this will never happen because this is infinity loop */
  vTaskDelete(NULL);
}
```
1. Bucle Infinit: La tasca s'executa en un bucle infinit:
- Imprimir Missatge: Mostra "this is another Task" a la consola serial.
- Retard Curt: Introduïu un retard d'1 segon (delay(1000)) abans de repetir el bucle.
2. Eliminar la Tasca: Si el bucle mai acaba (cosa que no passarà aquí perquè el bucle és infinit), la tasca s'elimina amb vTaskDelete(NULL).
