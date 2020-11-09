# Pregunta 3

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