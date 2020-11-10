# Support test

### ¿Qué es Envíame?

Envíame es una API que permite a e-commerces (nuestros clientes) despachar sus pedidos con diferentes proveedores lógisticos (CorreosChile, Starken, Bluexpress, etc). Cada cliente integrado a la API **ejecuta un request enviando un payload** con la información del pedido y dentro de los parámetros de entrada se puede o no indicar el proveedor logístico y servicio con el que se quiere despachar el producto. En caso de que el payload no indique el carrier y/o el servicio estos se determina utilizando una regla, que indica que operador logístico y servicio se debe utilizar (normal, express, etc.), y que se encuentra configurada en el sistema de envíame y almacenada en la base de datos de reglas del sistema. Además, cada envío cuenta con una **referencia**, que corresponde al número de orden asociado al despacho.

### Conceptos clave

- **Proveedor logístico o carrier:** Es la empresa que realizará el despacho del producto desde el e-commerce (nuestro cliente) hasta la dirección del comprador on-line.
- **Servicio:** Indica la forma en que el carrier despachará el producto, ya sea de forma normal, express, entrega en el mismo día, etc. Cada carrier cuenta con sus propios servicios.
- **Reglas:** Parametrización en base a peso (weight) del pedido y comuna de destino que permite determinar automáticamente el carrier y servicio con el que se debe despachar un envío cuando ninguno de estos dos parámetros son indicados explícitamente. Un ejemplo de regla es el siguiente:
-- Si el envío a Talca pesa **5 kg o menos**: envíar mediante Chilexpress, servicio express.
-- Si el envío a Talca pesa **más de 5 kg**: envíar mediante Starken, servicio normal.

### Pregunta 1: Análisis y gestión de incidencia en la creación de envío usando API Envíame

#### Situación

El cliente *A* reporta que el envío con la referencia *TI255826267* se creó con el servicio *normal* en vez del servicio *express* y piden al área TI determinar que ocurrió y cómo se debería solucionar. Usted es la persona de TI a cargo de atender esta incidencia, recopilar antecedentes técnicos e intentar determinar las causas del problema e idealmente entregar una respuesta al cliente.

En base a la situacion descrita anterioremente responda:

#### Pregunta 1.1
***¿Qué antecedentes debiese obtener para analizar el problema?***


Asumiendo que usted puede comunicarse con el área TI del e-commerce (Customer Team), con el equipo de desarrollo TI de Envíame (Dev Team) y que además tiene acceso a un sistema de log de transacciones de los envíos creados a través de la API, que es gestionado por el equipo de administración de sistemas de Envíame (SysAdm Team).

#### Pregunta 1.2
***¿Cuál sería su primer paso en la recopilación de antecedentes técnicos?***


Asumiendo que usted dispone de todas las herramientas de que dispone el cliente para utilizar la API de envíame, y que de usted depende determinar si para la resolución del incidente se requiere dar una indicación al cliente o bien determinar que el caso se debe derivar al área de desarrollo de TI de envíame.

#### Pregunta 1.3
***Antes de decidir si se responde o deriva la incidencia ¿Cuál sería su curso de acción para el diagnóstico técnico?***

#### Manos a la obra:

Dado el contexto anterior te pedimos que recopiles información técnica, analises y determines que hacer con la incidencia anterior.

Para ello puedes solicitar la información que tu creas necesaria para gestionar la incidencia a:
```
email: tech-test@enviame.io
```

Considera lo siguiente:
> Si necesitas solicitar información al equipo de TI Envíame, pon en el asunto de tu correo: [P1] Dev Team.
> Si necesitas solicitar información al equipo de TI de Cliente, pon en el asunto de tu correo: [P1] Customer Team.
> Si necesitas solicitar información al equipo de administración de sistemas de Envíame, pon en el asunto de tu correo: [P1] SysAdm Team.

```
email: tech-test@enviame.io
```

Una vez determines el curso de acción de la incidencia envía tu respuesta a *tech-test@enviame.io* para responder o derivar la incidencia.
> Si requieres mas información para resolver la incidencia pon en el asunto: [P1] Customer Issue [Action Required], e indica lo que requieres.
> Si requieres responder la incidencia pon en el asunto: [P1] Customer Issue [solved], e indica tu respuesta.
> Si requieres derivar la incidencia al equipo de desarrollo de Envíame pon en el asunto: [P1] Dev Issue [Action Required], e indica los antecedentes para que el área de desarrollo pueda resolver.

### Resultados Esperados

#### Pregunta 1.1
El postulante debería determinar que requiere conseguir el payload.

#### Pregunta 1.2
El postulante debería concluir que debe conseguir acceso al sistema de logs para recopilar la mayor cantidad de antecedentes posibles.

#### Pregunta 1.3
El postulante debiese haber conseguido acceso a los logs (pregunta anterior), y determinar que la causa del problema tiene que ver con una regla mal configurada de tal modo que debe ser capaz de concluir que puede resolver el incidente por si mismo.

#### Sección manos a la obra:
El postulante debería escribir a SysAdm Team para solicitar acceso al sistema de logs. La respuesta de SysAdm debería agregar que si requiere acceso a las reglas debe solicitarlas al Dev Team.

> Con el acceso a Telescope el postulante debería determinar que el envío al no tener en el payload de entrada carrier_code y carrier_service se determinó el servicio de forma automática a través de la regla de la empresa y debería solicitar el detalle de la regla de la empresa.

El postulante debería escribir a Dev Team para solicitar las reglas del cliente y de este modo concluir que el problema se debe a que la regla está mal configurada.

```
regla empresa en formato json
```

> El postulante debería poder resolver la incidencia por si mismo al determinar que el envío se creó con el servicio incorrecto porque la regla de la empresa estaba mal configurada.

 
### Pregunta 2: Análisis y gestión de incidencia en la creación de envío usando Integración Shopify

Las empresas de ecommerce pueden gestionar los envíos de productos vendidos en sus tiendas de Shopify a través de la plataforma de Envíame. Para hacerlo, primero deben hacerse clientes de Envíame, quien les crea una cuenta de empresa y les entrega todo lo necesario para configurar y operar en la plataforma, pero además para poder activar la sincronización  de ordenes y envíos entre Shopify y Envíame deben seguir las instrucciones descritas en el siguiente [manual de integración](https://platform.enviame.io/doc/paso-a-paso-shopify.pdf). De este modo cada vez que se venda un producto en Shopify, y se haga click en la opción ***Fulfill*** de Shopify se creará automáticamente un envío en Envíame, de acuerdo a las reglas configuradas por el cliente y con todos los datos necesarios para realizar el despacho del producto.

#### Situación:

Un nuevo cliente reporta un problema a los ejecutivos del chat de soporte Envíame, quienes a su vez te reportan que ***el cliente indica que no funciona la integración con Shopify, y que los envíos no se están creando en la plataforma de Envíame al hacer click en el botón Fullfill.***

En base al [manual de integración](https://platform.enviame.io/doc/paso-a-paso-shopify.pdf) y a los antencedentes que se adjuntan debes validar que la integración está correctamente configurada, orientar al cliente en caso de que corresponda que haga algo o derivar al área de desarrollo envíame.

Antecedentes:
[screenshot 1](https://storage.googleapis.com/technical-test/shopify_antes_que_todo_1.png)
[screenshot 2](https://storage.googleapis.com/technical-test/shopify_antes_que_todo_2.png)
[screenshot 3](https://storage.googleapis.com/technical-test/shopify_paso_4.png)
[screenshot 4](https://storage.googleapis.com/technical-test/shopify_paso_7.png)

Escribe a *tech-test@enviame.io* para solicitar mas antecedentes, resolver o derivar la incidencia.
> Si requieres mas información para resolver la incidencia pon en el asunto: [P2] Customer Issue [Action Required], e indica la información que requieres del cliente.
> Si resuelves la incidencia pon en el asunto: [P2] Customer Issue [solved], e indica tu respuesta al cliente.
> Si requieres derivar la incidencia al equipo de desarrollo de Envíame pon en el asunto: [P2] Dev Issue [Action Required], e indica los antecedentes para que el área de desarrollo pueda resolver.


### Resultados Esperados

> El postulante debería ir válidando cada uno de los pasos del manual y detectar que en el paso 5, en que se añade una url en shopify, el cliente ingresó esta: `https://us-central1-easypoint-latam...4%E2%80%9D`. Con esta url el postulante debería identificar que la url no es válida y debería dar solucion al problema indicando el formato correcto.


### Pregunta 3: Análisis de incidencia de bug web

El equipo de operaciones le reportó un problema al intentar ingresar a la plataforma. Usted intentó reproducir la situación que produce el problema utilitzando el inspect de su navegador y observó lo indicado en el video adjunto [video](https://storage.googleapis.com/technical-test/videop3.mov). En base a los antecedentes disponibles documente la incidencia técnica para que el equipo de desarrollo pueda entender lo ocurrido y así poder solucionar.

Escribe a *tech-test@enviame.io* para derivar la incidencia.
> Usa el asunto: [P3] Dev Issue [Action Required], incluyendo los antecedentes necesarios para que el equipo de desarrollo pueda resolver.

### Resultados Esperados

> El postulante debería documentar el problema utilizando antecedentes técnicos que permitan reproducir la situación utilizando la mayor cantidad de elementos técnicos posibles.
 

### Pregunta 4: reporte de bug de backend

Envíame dispone de una API que permite a sus clientes crear un ticket de reclamo asociado a un problema cualquiera. 

Para utilizar las APIs de envíame los clientes deben haber sido creados y activados en la plataforma Envíame. Esta acción realizada por el área de ventas, quienes entregan al cliente un usuario y contraseña que permite al usuario administrador del cliente editar datos como: Nombre, Rut, Código, Razón Social, Dirección; y también le permite crear, editar y eliminar Usuarios y Bodegas.

La empresa MULTIMARCAS es un nuevo cliente y necesita crear un ticket de reclamo para informar que uno de sus envíos que presenta un retraso en su entrega pero tiene problemas para crear el ticket.

El Cliente reporta que recibe un código de error al intentar crear un ticket utilizando la API de creación de tickets de envíame. Usted le ha solicitado al equipo TI del Cliente los datos del request que genera el error para poder reproducir el problema y recibe una respuesta con los siguientes antecedentes:

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

Además de los antecedentes proporcionados por el Cliente, Usted dispone de endpoints que le permiten conocer detalles de una Empresa y Usuario que se señalan a continuación:

#### Otros endpoints de interés:

###### Detalle de una empresa
GET https://platform.enviame.io/support-test/companies/{id}

###### Detalle de un usuario
GET https://platform.enviame.io/support-test/users/{id}

Escribe a *tech-test@enviame.io* para solicitar mas antecedentes, resolver o derivar la incidencia.
> Si requieres mas información para resolver la incidencia pon en el asunto: [P4] Customer Issue [Action Required], e indica la información que requieres del cliente.
> Si resuelves la incidencia pon en el asunto: [P4] Customer Issue [solved], e indica tu respuesta al cliente.
> Si requieres derivar la incidencia al equipo de desarrollo de Envíame pon en el asunto: [P4] Dev Issue [Action Required], e indica los antecedentes para que el área de desarrollo pueda resolver.


### Resultados Esperados

> El postulante debería concluir que a la empresa le falta el dato 'code' y determinar que este dato es "modificable" por el usuario administrador del Cliente por lo tanto resolver la incidencia con una indicación al usuario.

### Pregunta 5: Búsqueda de datos:

El Cliente empresa con ***código "EVIL_CORP"*** señala que se le han cobrado mal los envíos entre el ***2020-09-01 y el 2020-11-01*** y el área de atención a cliente te solicite que extraigas información de la Base de Datos para poder verificar información sobre los envíos del cliente para poder analizar la situación.

Usted tiene acceso a una base de datos MySQL con los siguientes datos de conexión:

###### Datos de conexión:
```
Conexión a la base de datos:
dirección ip: 130.211.126.67 
puerto: 3306
usuario: expecto
contraseña: patronum
base de datos: enviame
```

La base de datos contiene las tablas y relaciones descritas en el siguiente modelo:
[Modelo de datos](https://storage.googleapis.com/technical-test/database.jpg)

Utilizando sus conocimientos en SQL y explorando la base de datos diseñe las consultas en SQL necesarias para proporcionar la siguiente información:

#### Pregunta 5.1
Obtenga un listado de envíos (tabla deliveries) ordenado por fecha de manera descendente y que contenga los siguientes datos: id, imported_id, tracking_numbe, company_id, delivery_status_id y created_at, donde la empresa sea ***EVIL_CORP***, el estado de los envíos sea ***ENTREGADO*** y la fecha de creación se encuentre entre las fechas indicadas en el enunciado.

#### Pregunta 5.2
Mejore la consulta anterior, incluyendo mas tablas, para en lugar de entregar el dato company_id entregue el dato name1 (companies) y en lugar del dato delivery_status_id entregue el dato name (delivery_statuses).

#### Pregunta 5.3
Extienda la consulta anterior, incluyendo mas tablas, para agregar los siguientes datos código de bodega (warehouses), dirección de la bodega (address) y comuna de la bodega (places).

Escribe a *tech-test@enviame.io* para enviar las consultas diseñadas para cada ítem usando el asunto [P5] SQL, e indicando el número de ítem antes de tu script SQL (Ej: Item 5.1: SELECT ... FROM ... WHERE ...;)


### Resultados Esperados

#### Pregunta 5.1
```
select d.id, d.imported_id, d.tracking_number, d.company_id, d.delivery_status_id, d.created_at
from deliveries as d
where d.tracking_number is not null
and d.company_id = 620
and d.delivery_status_id = 10
and created_at > '2020-09-01'
and created_at <= '2020-11-01'
order by created_at desc;
```

#### Pregunta 5.2
```
select d.id, d.imported_id, d.tracking_number, c.name1, ds.name, d.created_at
from deliveries as d
join delivery_statuses as ds on ds.id = d.delivery_status_id
join companies as c on c.id = d.company_id
where d.tracking_number is not null
and d.company_id = 620
and d.delivery_status_id = 10
order by created_at desc;
```

#### Pregunta 5.3
```
select d.id, d.imported_id, d.tracking_number, c.name1, ds.name,  w.code, a.full_address, p.name, d.created_at
from deliveries as d
join delivery_statuses as ds on ds.id = d.delivery_status_id
join companies as c on c.id = d.company_id
join warehouses as w on w.company_id = c.id
join addresses as a on w.address_id = a.id
join places as p on p.id = a.place_id
where d.tracking_number is not null
and d.company_id = 620
and d.delivery_status_id = 10
order by created_at desc;
```

### Pregunta 6: Reporte

Para los 5 casos anteriormente descritos envíe un reporte sencillo, que conste de una tabla donde se agrupen las incidencias por tipo y estado, y donde se indique:
* Tipo de incidencia: soporte o requerimiento
* Estado: solucionado o pendiente


### Resultados Esperados
| Tipo   |      Estado      |  Cantidad |
|----------|:-------------:|------:|
| Soporte |  solucionado | 4 |
| Requerimiento |    Solucionado   |   1 |







