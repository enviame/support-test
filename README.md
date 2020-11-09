# Support test

### ¿Qué es Envíame?

Envíame es una API que permite a e-commerces (nuestros clientes) despachar sus pedidos con diferentes proveedores lógisticos (CorreosChile, Starken, Bluexpress, etc). Cada cliente integrado a la API **ejecuta un request enviando un payload** con la información del pedido y dentro de los parámetros de entrada se puede o no indicar el proveedor logístico y servicio con el que se quiere despachar el producto. En caso de que el payload no indique el carrier y/o el servicio estos se determina utilizando una regla, que indica que operador logístico y servicio se debe utilizar (normal, express, etc.), y que se encuentra configurada en el sistema de envíame y almacenada en la base de datos de reglas del sistema. Además, cada envío cuenta con una **referencia**, que corresponde al número de orden asociado al despacho.

### Conceptos clave

- **Proveedor logístico o carrier:** Es la empresa que realizará el despacho del producto desde el e-commerce (nuestro cliente) hasta la dirección del comprador on-line.
- **Servicio:** Indica la forma en que el carrier despachará el producto, ya sea de forma normal, express, entrega en el mismo día, etc. Cada carrier cuenta con sus propios servicios.
- **Reglas:** Parametrización en base a peso (weight) del pedido y comuna de destino que permite determinar automáticamente el carrier y servicio con el que se debe despachar un envío cuando ninguno de estos dos parámetros son indicados explícitamente. Un ejemplo de regla es el siguiente:
-- Si el envío a Talca pesa **5 kg o menos**: envíar mediante Chilexpress, servicio express.
-- Si el envío a Talca pesa **más de 5 kg**: envíar mediante Starken, servicio normal.

### Pregunta 1: Análisis

Evalue y reporte la siguiente incidencia.

#### Situación

El cliente *A* reporta que el envío con la referencia *TI255826267* se creó con el servicio *normal* en vez del servicio *express* y piden al área TI determinar que ocurrió y cómo se debería solucionar. Usted es la persona de TI a cargo de atender esta incidencia, recopilar antecedentes técnicos e intentar determinar las causas del problema e idealmente entregar una respuesta al cliente.

#### Responda
***¿Qué antecedentes debiese obtener para analizar el problema?***


Asumiendo que usted puede comunicarse con el área TI del e-commerce (Customer Team), con el equipo de desarrollo TI de Envíame (Dev Team) y que además tiene acceso a un sistema de log de transacciones de los envíos creados a través de la API, que es gestionado por el equipo de administración de sistemas de Envíame (SysAdm Team).

#### Responda
***¿Cuál sería su primer paso en la recopilación de antecedentes técnicos?***


Asumiendo que usted dispone de todas las herramientas de que dispone el cliente para utilizar la API de envíame, y que de usted depende determinar si para la resolución del incidente se requiere dar una indicación al cliente o bien determinar que el caso se debe derivar al área de desarrollo de TI de envíame.

#### Responda
***Antes de decidir si se responde o deriva la incidencia ¿Cuál sería su curso de acción para el diagnóstico técnico?***

#### Manos a la obra:

Dado el contexto anterior te pedimos que recopiles información técnica, analises y determines que hacer con la incidencia anterior.
Para ello puedes solicitar la información que tu creas necesaria a *it@enviame.io* para gestionar la incidencia.

> Si necesitas solicitar información al equipo de TI Envíame, parte tu correo con Dev Team:
> Si necesitas solicitar información al equipo de TI del Cliente, parte tu correo con Customer Team:
> Si necesitas solicitar información al equipo de administración de sistemas de Envíame , parte tu correo con SysAdm Team

```
email: it@enviame.io
```

### Resultados Esperados

#### Pregunta 1
El postulante debería determinar que requiere conseguir el payload.

#### Pregunta 2
El postulante debería concluir que debe conseguir acceso al sistema de logs para recopilar la mayor cantidad de antecedentes posibles.

#### Pregunta 3
El postulante debiese haber conseguido acceso a los logs (pregunta anterior), y determinar que la causa del problema tiene que ver con una regla mal configurada de tal modo que debe ser capaz de concluir que puede resolver el incidente por si mismo.

#### Sección práctica
El postulante debería escribir a SysAdm Team para solicitar acceso al sistema de logs. La respuesta de SysAdm debería indicar que si requiere acceso a las reglas debe solicitarlas al Dev Team.

> Con el acceso a Telescope el postulante debería determinar que el envío al no tener en el payload de entrada carrier_code y carrier_service se determinó el servicio de forma automática a través de la regla de la empresa y debería solicitar el detalle de la regla de la empresa.

El postulante debería escribir a Dev Team para solicitar las reglas del cliente y de este modo concluir que el problema se debe a que la regla está mal configurada.

```
regla empresa en formato json
```

> El postulante debería determinar que el envío se creó con el servicio incorrecto porque la regla de la empresa estaba mal configurada.

 
### Pregunta 2: integración Shopify

Los ejecutivos del chat de Envíame reportan que un cliente no puede crear envíos a través de la integración con Shopify. El cliente indica que al hacer click en el botón Fullfill no se ve reflejado el envío en la plataforma de Envíame. En base al siguiente [manual de integración](https://platform.enviame.io/doc/paso-a-paso-shopify.pdf) debes validar que la integración está correctamente configurada. Si necesitas más información sobre la empresa y sus envíos, nos puedes contactar a it@enviame.io.

### Resultados Esperados

> El postulante debería ir válidando cada uno de los pasos del manual, como respuesta se debe indicar que todos los pasos estan correctos, pero en el paso 5 que se añade una url especial en shopify enviarle que la url que esta usando el cliente es esta: `https://us-central1-easypoint-latam...4%E2%80%9D`. Con esta url el postulante debería identificar que la url no es válida y debería dar solucion al problema indicando el formato correcto.


### Pregunta 3: reporte de bug web


El equipo de operaciones reporta el siguiente [video]('./assets/videop3.mov') con un bug presentado en la plataforma, en base a este video describe los antecedentes necesarios para que el equipo de desarrollo pueda entender lo ocurrido y así poder solucionar.
 

### Pregunta 4: reporte de bug backend

La empresa MULTIMARCAS quiere abrir un ticket de reclamo para uno de sus envíos que presenta un retraso en su entrega. El usuario reporta problemas a la hora de crear el ticket. ¿Cómo se puede solucionar esto?

El request para crear un ticket es el siguiente:

**Endpoint:** https://platform.enviame.io/support-test/create-ticket
**Method:** POST
**Headers:**
- Content-Type: application/json
- Accept: application/json

**Body:**
```
{
    "company_id": 345,
    "user_id": 1566,
    "subject": "Envío atrasado",
    "message": "Buenos días, el envío P45678 debía ser entregado el día 25/10/2020 y aún no llega a destino, por favor gestionar la entrega lo antes posible"
}
```

#### Otros endpoints de interés:

###### Detalle de una empresa

GET https://platform.enviame.io/support-test/companies/ID

###### Detalle de un usuario

GET https://platform.enviame.io/support-test/users/ID
