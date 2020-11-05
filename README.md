# support-test

#### Prueba


##### Pregunta 1)


Evalue y reporte la siguiente situación


**Palabras clave**

- Provedor logistico o carrier: Es la empresa que realizará el despacho del producto desde el ecommerce a la dirección del cliente.
- Servicio: Indica la forma en que el carrier despachará el producto ya sea de forma express, el mismo día, normal, etc. Cada carrier cuenta con sus propios servicios.
- Reglas: Parametrización en base a peso (weight) del pedido y comuna de destino que permite determinar automaticamente el carrier y servicio con el que se debe despachar este.


**Contexto**

Enviame es una API que que permite a e-commerces despachar sus pedidos con diferentes proveedores lógisticos (Correos de Chile, Starkn, Bluexpress, etc), cada cliente integrado a la API envia un payload con la información del pedido, dentro de los paramentros de entrada se puede o no indicar el provedor logistico y servicio con el que se quiere despachar el producto. En caso que el payload no indique el carrier y servicio este se determina a través de las reglas.



**Situación**


- El cliente *A* reporta que el envío con la referencia *TI255826267* se creó con el servicio *normal* en vez del servicio *express* y piden a ti determinar que ocurrio y como se debería solucionar, para esto puedes solicitar la información que tu creas necesaria a *email@enviame.io* para ver que sucedió con el envio. 


> Si el postulante lo solicita se debe dar acceso a sitio del log con el siguiente usuario y contraseña


```
email: support@enviame.io
contraseña:postulacion
```


> Con el acceso al log el postulante debería determinar que el envio al no tener en el payload de entrada carrier_code y carrier_service se determino de forma automatica a través de la regla de la empresa y debería solicitar el detalle de la regla de la empresa.


```

regla empresa en formato json

```

> El postulante debería determinar que el envio se creo con el servicio incorrecto por que la regla de la empresa estaba mal configurada.

 

##### Pregunta 2)



Ejecutivos del chat de Enviame repotan que un cliente no puede crear envios a través de la integración con shopify, en base al siguiente (documento de integración)[https://platform.enviame.io/doc/paso-a-paso-shopify.pdf] solicita la información y/o antecedentes necesarios para poder determinar el problema.


> El postulante debería ir válidando cada uno de los pasos del manual, como respuesta se debe indicar que todos los paso estan correcto, pero en el paso 5 que se añade una url especial en shopify enviarle que la url que esta usando el cliente es esta: `https://us-central1-easypoint-latam...4%E2%80%9D`. Con esta url el postulante debería identificar que la url no es válida y debería dar solucion al problema indicando el formato correcto.



##### Pregunta 3)


El equipo de operaciones reporta el siguiente (video)[link] con un bug presentado en la plataforma, en base a este video describe los antecedentes necesarios para que el equipo de desarrollo pueda entender lo ocurrido y así poder solucionar.
 

##### Pregunta 4)

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

### Otros endpoints de interés:

#### Detalle de una empresa

GET https://platform.enviame.io/support-test/companies/ID

#### Detalle de un usuario

GET https://platform.enviame.io/support-test/users/ID
