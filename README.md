# LIBRERIA INVERNADERO AUTOMATIZADO ESP32 (LIA)
Esta liberia es una implementacion en C++ especializada y versatil para el control y gestion de invernaderos inteligentes.
Utiliza una arquitectura de programacion orientada a objetos (POO) con clases abstractas que actuan como base para la definicion
concreta de sensores y actuadores para el conrtrol de temperatura, humedad, ph e iluminacion.
## Caracterizticas principales
1. Lectura en tiempo real (*actualizada cada segundo*) del estado general del invernadero.
2. **Arquitectura modular:** Uso de herencia y polimorfismo para el uso de las clases abstractas.
3. **Monitoreo multivariable:** Soporte nativo para el monitoreo en tiempo real de multiples sensores.
4. **Gestion de actuadores:** Soporte nativo para la gestion automatica y manual de multiples actuadores.
5. **Controlador centralizado:** Uso de una sola clase para la seguridad y actualizacion automatica del sistema.
## Instalacion
### Requisitos previos:
1. Tener instalado el entorno de desarrollo integrado (IDE) de Arduino y el **core** de esp32 dentro del mismo.
2. Instalar y agregar la libreria `SR_Keypad.h` a su codigo en el IDE.
>[!IMPORTANT]
>
>La libreria **LIA** requiere de `SR_Keypad.h` y sus dependencias (`PISO.h` & `SIPO.h`) para funcionar correctamente.
## Inicio Rapido (Ejemplo de uso)
Para utilizar la libreria de manera adecuada, sigue la siguiente implementacion como ejemplo:
```
//ESTE CODIGO NO ES EL EJEMPLO REAL, ES UN EJEMPLO DEL EJEMPLO. CORREGIR DESPUES
#include "SIPO.h"
#include "PISO.h"
#include "invernadero.h"

// Función para manejar eventos de botones
void miCallback(uint8_t id, bool state) {
    if(state) Serial.println("Botón presionado: " + String(id));
}

SR_Keypad::Controller controlador(miCallback);
ControladorInvernadero invernadero;

void setup() {
    Serial.begin(115200);

    // Inicializar pines de registros
    pinMode(PISO_DATA_PIN, INPUT);
    pinMode(PISO_CLOCK_PIN, OUTPUT);
    pinMode(SIPO_DATA_PIN, OUTPUT);
    // ... configurar resto de pines ...

    controlador.AttachSIPO(mySIPO);
    controlador.AttachPISO(myPISO);
    invernadero.inicializar();
}

void loop() {
    controlador.Scan();          // Escanea los 64 botones
    invernadero.actualizarSistema(); // Monitorea el invernadero
    delay(300);
}
```
## Referencia API
#### Clase `ControladorInvernadero`
| Metodo | Que hace? | Ejemplo |
|--- |--- |--- |
| `inicializar()` | Configura los pines y prepara los sensores/actuadores para su funcionamiento. | `myInvernadero.inicializar();` |
| `actualizarSistema()` | Realiza una lectura sincronizada de todos los sensores (Temperatura, pH, Humedad, Luz) | `myInvernadero.actualizarSistema();` |
| `verificarSeguridad()` | Comprueba que los parametros del sistema esten dentro de los rangos seguros de operacion | `if(myInvernadero.verificarSeguridad()){...};` |
| `controlarRiego()` | Activa o desactiva la bomba de agua basandose en la lectura del sensor de humedad. | `myInvernadero.controlarRiego();` |
| `esDeNoche()` | (Sensor de luz) Determina si la luz ambiental ha caido por debajo del umbral de obscuridad. | `if(sensorLuz.esDeNoche()){...};` |
| `abrirPorcentaje(int p)` | (Motor del Techo) Mueve el techo a una pocision especifica en terminos de porcentaje (0% - 100%) para ventilar. | `motorTecho.abrirPorcentaje(50);` |
>[!NOTE]
>
>Para los actuadores como `BombaAgua` o `LuzUv`, tambien se dispone de los metodos `.encender.()` & `.apagar()` heredados de la clase `Actuador`.
#### Clase `SR_Keypad::Controller`
Aqui va la misma tabla de arriba pero para lo de como usar el teclado con la libreria
## Licencia
#### MIT - Puede usar, modificar y distribuir esta licencia sin restricciones.
