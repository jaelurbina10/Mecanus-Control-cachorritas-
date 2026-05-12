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
Instalar un compilador C++ (GCC o MSVC) compatible con C++11 o superior
### Clonacion o descarga
Copiar y pegar o descargar los archivos ubicados en `\src` -> `invernadero.h` & `invernadero.cpp`
### Inicio Rapido
Para utilizar la libreria de manera rapida y sencilla en su 
