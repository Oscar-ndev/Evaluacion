# Evaluación Plataformas Especiales

Se debe realizar una aplicación basada en APIs para procesar los datos de una transacción, como se describe a continuación:

### API 1

Esta API recibe el siguiente JSON:

```json
{
  "operacion": "venta",
  "importe": "100.00",
  "cliente": "elesban",
  "secreto": "jejdjw134&3#$$"
}
```

Debe cumplir con los siguientes puntos:

- Validar los atributos del JSON usando:
  - `@Valid`, `@Pattern`, `@RestControllerAdvice`
  - `operacion`: debe ser texto
  - `importe`: debe ser formato moneda
  - `cliente`: debe ser texto (longitud libre)
- El atributo `secreto` se cifra con AES-256. Al llegar a la API se descifra y se envía en claro a la segunda API.
- Si el JSON es válido, se envía a la segunda API usando `@FeignClient`, `RestTemplate` o `Apache Client`.

### API 2

Debe cumplir con lo siguiente:

- Almacena los datos recibidos usando `Spring Data JPA` en una base de datos en memoria (H2).
- Estructura de la base de datos:

  ```
  PK, operacion, importe, cliente, referencia, estatus, secreto
  ```

- Al guardar los datos:
  - Se genera una referencia aleatoria de 6 dígitos
  - Se asigna el estatus “Aprobada”
  - Se envía una respuesta a la primera API con el siguiente formato:

```json
{
  "id": "2376",
  "estatus": "Aprobada",
  "referencia": "262737",
  "operacion": "venta"
}
```

### Frontend

Se debe generar una página web utilizando JavaScript (React, Angular o Vue). El formulario incluye:

- Textfield operación: `_______`
- Textfield importe: `_______`
- Textfield cliente: `_______`
- Textfield secreto: `_______`
- Botón que manda la petición POST

---

- **Backend**
  - API 1: Spring Boot, FeignClient, AES-256
  - API 2: Spring Boot, Spring Data JPA, H2
- **Frontend**
  - React, Bootstrap, CryptoJS

---

## ▶️ Ejecución 

```bash

git clone https://github.com/Oscar-ndev/Evaluacion
cd mi-proyecto

# Terminal 1
cd api1
./mvnw spring-boot:run

# Terminal 2
cd api2
./mvnw spring-boot:run

#Terminal 3
cd frontend
npm install
npm start
```

---
