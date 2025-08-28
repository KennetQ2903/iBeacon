# ESP32 iBeacon + BLE Service

Este proyecto implementa un **servidor BLE en un ESP32** que envía tramas **iBeacon** periódicamente y expone un **servicio BLE** con una característica que puede **leer, escribir y notificar** datos a los clientes conectados.

## 📌 Descripción

El código realiza lo siguiente:

1. Inicializa un servidor BLE en el ESP32.
2. Define un servicio BLE y una característica con propiedades de lectura, escritura y notificación.
3. Configura y emite paquetes **iBeacon** con un UUID, Major, Minor y potencia de señal definidos.
4. Permite que un cliente se conecte, reciba notificaciones periódicas y escriba datos en la característica.
5. Si el cliente se desconecta, el ESP32 reinicia automáticamente la publicidad para mantenerse visible y conectable.

## 🚀 Requisitos

* **Hardware**:

  * ESP32 (cualquier modelo con soporte BLE).
* **Software/Librerías**:

  * [Arduino IDE](https://www.arduino.cc/en/software) o [PlatformIO](https://platformio.org/).
  * Librerías incluidas en el ESP32 Arduino Core:

    * `BLEDevice.h`
    * `BLEServer.h`
    * `BLEUtils.h`
    * `BLE2902.h`
    * `BLEBeacon.h`

## ⚙️ Configuración principal

En el código se definen varios UUIDs y parámetros de iBeacon que pueden personalizarse:

```cpp
#define DEVICE_NAME         "ESP32"
#define SERVICE_UUID        "7A0247E7-8E88-409B-A959-AB5092DDB03E"
#define BEACON_UUID         "2D7A9F0C-E0E8-4CC9-A71B-A21DB2D034A1"
#define BEACON_UUID_REV     "A134D0B2-1DA2-1BA7-C94C-E8E00C9F7A2D"
#define CHARACTERISTIC_UUID "82258BAA-DF72-47E8-99BC-B73D7ECD08A5"
```

* `DEVICE_NAME`: Nombre del dispositivo visible al escanear.
* `SERVICE_UUID`: UUID del servicio BLE.
* `CHARACTERISTIC_UUID`: UUID de la característica.
* `BEACON_UUID_REV`: UUID utilizado en la emisión iBeacon.

## 📡 Funcionamiento

* Al iniciar, el ESP32:

  * Crea el servidor BLE.
  * Inicializa el servicio y la característica.
  * Comienza a emitir como **iBeacon**.
* Cuando un cliente se conecta:

  * El ESP32 envía notificaciones periódicas con un valor incremental cada 2 segundos.
* Si el cliente escribe en la característica, el valor recibido se imprime en el monitor serie.
* Al desconectarse el cliente, el ESP32 reinicia la publicidad automáticamente.

## 🖥️ Ejemplo de salida en el monitor serie

```
Initializing...
iBeacon + service defined and advertising!
deviceConnected = true
*** NOTIFY: 0 ***
*** NOTIFY: 1 ***
Received Value: Hello
deviceConnected = false
iBeacon advertising restarted
```

## 👥 Autores

* Daniela Salguero
* Kennet Quiroz
* Lisbeth Garcia

