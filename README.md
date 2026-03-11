# Interrupción de Botón con ESP32

![ESP32](https://img.shields.io/badge/ESP32-Interrupt-blue)
![PlatformIO](https://img.shields.io/badge/PlatformIO-Compatible-orange)
![Arduino](https://img.shields.io/badge/Arduino-Compatible-green)

Este proyecto demuestra cómo utilizar interrupciones externas en un ESP32 para detectar pulsaciones de un botón. El código cuenta el número de veces que se presiona un botón y desactiva la interrupción después de 1 minuto.

## 📋 Descripción

El programa configura un botón en el pin GPIO18 con resistencia pull-up interna y utiliza una interrupción para detectar flancos de bajada (FALLING). Cada vez que se presiona el botón, se incrementa un contador y se establece una bandera. En el loop principal, se muestra por el puerto serial el número de pulsaciones. Después de 60 segundos, la interrupción se desactiva automáticamente.

## 🚀 Características

- Configuración de interrupción externa en ESP32
- Detección de pulsaciones de botón con anti-rebote por hardware (pull-up)
- Contador de pulsaciones
- Desactivación automática de la interrupción después de 1 minuto
- Comunicación serial para monitoreo

## 📁 Estructura del Código

### Componentes Principales

1. **Estructura Button**: Almacena la configuración y estado del botón
   - `PIN`: Número del pin GPIO
   - `numberKeyPresses`: Contador de pulsaciones
   - `pressed`: Bandera de estado

2. **Función ISR** (Interrupt Service Routine):
   - Se ejecuta en cada pulsación
   - Incrementa el contador
   - Activa la bandera `pressed`

3. **Setup**: Configuración inicial
   - Inicializa comunicación serial
   - Configura el pin como entrada con pull-up
   - Adjunta la interrupción

4. **Loop**: 
   - Monitorea y reporta pulsaciones
   - Controla el temporizador de 1 minuto
   - Desactiva la interrupción cuando expira el tiempo

## 🔧 Requisitos

- PlatformIO o Arduino IDE
- ESP32
- 1 botón pulsador
- Cables de conexión
- Protoboard (opcional)

## 📌 Conexiones

| Componente | Pin ESP32 |
|------------|-----------|
| Botón      | GPIO 18   |
| GND        | GND       |

El botón debe conectarse entre el pin GPIO18 y GND. La resistencia pull-up interna del ESP32 elimina la necesidad de resistencias externas.

## 💻 Instalación

1. Clona este repositorio:
   ```bash
   git clone https://github.com/tu-usuario/esp32-button-interrupt.git
Abre el proyecto en PlatformIO o Arduino IDE

Conecta tu ESP32

Compila y sube el código

📊 Uso
Preparación:

Conecta el botón al GPIO18 y GND según el diagrama de conexiones
Asegúrate de que el ESP32 esté correctamente conectado a tu computadora

Ejecución:
Abre el monitor serial a 115200 baudios
Presiona el botón conectado al GPIO18
Observa el contador incrementarse en el monitor serial
Después de 60 segundos, la interrupción se desactiva automáticamente

Comportamiento esperado:

Cada pulsación del botón incrementa el contador en 1
El monitor serial muestra el número actual de pulsaciones
Después de 1 minuto, el botón deja de responder y aparece el mensaje "Interrupt Detached!"

📝 Ejemplo de Salida Serial
text
Button 1 has been pressed 1 times
Button 1 has been pressed 2 times
Button 1 has been pressed 3 times
Button 1 has been pressed 4 times
Button 1 has been pressed 5 times
Button 1 has been pressed 6 times
Button 1 has been pressed 7 times
Button 1 has been pressed 8 times
Button 1 has been pressed 9 times
Button 1 has been pressed 10 times
Interrupt Detached!
