# TP monitoreo de temperatura BMP280

Este ejemplo conecta el ESP32 al BMP280, transmite los datos al backend por MQTT, los guarda en la base MongoDB para despues ser visualizados desde frontend.


## Sistema embebido

cd sistema_embebido  
     	
code .     

Configuracion SSID y PASS WiFi

Este ejemplo usa la funcion "example_connect()" de la platarforma ESP-IDF.

Para configurar el SSID y PASSWORD se debe hacer clic en el icono "engranaje" (configuración)
de la barra inferior del VSCode y allí en la sección de WiFi se podrán configurar los datos
necesarios

Compilar, flashear y monitorear el dispositivo. Se deberia ver esta salida:

```
I (12819) esp_netif_handlers: example_connect: sta ip: 192.168.0.21, mask: 255.255.255.0, gw: 192.168.0.1
I (12819) example_connect: Got IPv4 event: Interface "example_connect: sta" address: 192.168.0.21
I (13619) example_connect: Got IPv6 event: Interface "example_connect: sta" address: fe80:0000:0000:0000:bad6:1aff:fe41:ff4c, type: ESP_IP6_ADDR_IS_LINK_LOCAL
I (13619) example_connect: Connected to example_connect: sta
I (13629) example_connect: - IPv4 address: 192.168.0.21
I (13629) example_connect: - IPv6 address: fe80:0000:0000:0000:bad6:1aff:fe41:ff4c, type: ESP_IP6_ADDR_IS_LINK_LOCAL
I (13649) bmp280: [APP] Free memory: 233352 bytes
I (13649) bmp280: Other event id:7
I (13659) bmp280: Temperature: 23.67 C
I (13669) bmp280: MQTT_EVENT_ENVIAR
I (13699) wifi:<ba-add>idx:1 (ifx:0, 08:7b:12:9b:45:a8), tid:0, ssn:1, winSize:64
I (18059) bmp280: MQTT_EVENT_CONNECTED
I (18259) bmp280: MQTT_EVENT_PUBLISHED, msg_id=475
I (38069) bmp280: Temperature: 21.89 C
I (38069) bmp280: MQTT_EVENT_ENVIAR
I (38139) bmp280: MQTT_EVENT_PUBLISHED, msg_id=62529
I (58079) bmp280: Temperature: 21.85 C
I (58079) bmp280: MQTT_EVENT_ENVIAR
I (58299) bmp280: MQTT_EVENT_PUBLISHED, msg_id=7688
```

## Backend 

cd backend  
code .  
node index.js  

Se deberia ver esta salida:
```
MQTT:mqtts://localhost
Rutas registradas:  prueba
Rutas registradas:  alumno
API Funcionando... en: http://localhost:3000
[MQTT] Init: Connected
DATABASE IS CONNECTED TO mongodb+srv://mongodb:###@test.k6kpvxv.mongodb.net/?retryWrites=true&w=majority
Subscribed to topics: 
[ '/PLANTA_BAJA/TEMPERATURA' ]
[MQTT] Mensaje recibido: /PLANTA_BAJA/TEMPERATURA: {
	"dispositivoId":	1,
	"nombre":	"ESP32_BMP280_TEMPERATURA",
	"ubicacion":	"Planta Baja",
	"temperatura":	21.8799991607666,
	"nodoId":	0
}
elTime:Mon Jun 10 2024 11:03:24 GMT-0300 (hora estándar de Argentina)
[LOG] id: {
  _id: new ObjectId("6666888978c66007113070b7"),
  logId: 24,
  ts: 2024-06-10T05:00:57.480Z,
  etemperatura: 21.48,
  nodoId: 1,
  __v: 0
}
termino el calculo del id del LOG :24
REGISTRO DE LOG AGREGADO CORRECTAMENTE.
DISPOSITIVO ACTUALIZADO.
```

## Frontend

cd frontend  
code .  
npm run dev  

Se deberia ver esta salida:

```
npm run dev

> 2022-front-react@0.1.0 dev
> next dev

warn  - Port 3000 is in use, trying 3001 instead.
ready - started server on 0.0.0.0:3001, url: http://localhost:3001
info  - Loaded env from /home/cristian/DDA3/TP/frontend/.env
wait  - compiling...
event - compiled client and server successfully in 504 ms (168 modules)
```


## NOTA

ESTE EJEMPLO TIENE CARGADOS LOS DATOS DE CONEXION A MI ROUTER LOCAL, LOS CERTIFICADOS ESTAN GENERADOS CON LOS MISMOS, EN CASO DE CORRER EL EJEMPLO EN OTRA MAQUINA SEGUIR EL README.md DE
CADA SUBDIRECTORIO(sistema_embebido,backend y frontend).

