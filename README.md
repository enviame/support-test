# Support test

### ¿Qué es Envíame?

Envíame es una API que que permite a e-commerces despachar sus pedidos con diferentes proveedores lógisticos (CorreosChile, Starken, Bluexpress, etc). Cada cliente integrado a la API envía un payload con la información del pedido y dentro de los parámetros de entrada se puede o no indicar el proveedor logístico y servicio con el que se quiere despachar el producto. En caso de que el payload no indique el carrier y el servicio este se determina a través de las reglas.

### Conceptos clave

- **Proveedor logístico o carrier:** Es la empresa que realizará el despacho del producto desde el e-commerce hasta la dirección del cliente.
- **Servicio:** Indica la forma en que el carrier despachará el producto, ya sea de forma normal, express, entrega en el mismo día, etc. Cada carrier cuenta con sus propios servicios.
- **Reglas:** Parametrización en base a peso (weight) del pedido y comuna de destino que permite determinar automáticamente el carrier y servicio con el que se debe despachar un envío cuando ninguno de estos dos parámetros son indicados explícitamente. Un ejemplo de regla es el siguiente:
-- Si el envío a Talca pesa **5 kg o menos**: envíar mediante Chilexpress, servicio express.
-- Si el envío a Talca pesa **más de 5 kg**: envíar mediante Starken, servicio normal.

### Pregunta 1: análisis 

Evalue y reporte la siguiente incidencia.

#### Situación

El cliente *A* reporta que el envío con la referencia *TI255826267* se creó con el servicio *normal* en vez del servicio *express* y piden al área TI determinar que ocurrió y cómo se debería solucionar. Para esto puedes solicitar la información que tu creas necesaria a *email@enviame.io* para ver que sucedió con el envío.

> Si el postulante lo solicita se debe dar acceso a Telescope con el siguiente usuario y contraseña

```
email: support@enviame.io
contraseña:postulacion
```


> Con el acceso a Telescope el postulante debería determinar que el envío al no tener en el payload de entrada carrier_code y carrier_service se determinó el servicio de forma automática a través de la regla de la empresa y debería solicitar el detalle de la regla de la empresa.


```
regla empresa en formato json
```

> El postulante debería determinar que el envío se creó con el servicio incorrecto porque la regla de la empresa estaba mal configurada.

 

### Pregunta 2: integración Shopify

Los ejecutivos del chat de Envíame reportan que un cliente no puede crear envíos a través de la integración con Shopify. El cliente indica que al hacer click en el botón Fullfill no se ve reflejado el envío en la plataforma de Envíame. En base al siguiente [manual de integración](https://platform.enviame.io/doc/paso-a-paso-shopify.pdf) debes validar que la integración está correctamente configurada. Si necesitas más información sobre la empresa y sus envíos, nos puedes contactar a email@enviame.io.

> El postulante debería ir válidando cada uno de los pasos del manual, como respuesta se debe indicar que todos los paso estan correcto, pero en el paso 5 que se añade una url especial en shopify enviarle que la url que esta usando el cliente es esta: `https://us-central1-easypoint-latam...4%E2%80%9D`. Con esta url el postulante debería identificar que la url no es válida y debería dar solucion al problema indicando el formato correcto.


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
