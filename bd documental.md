Aquí tienes un ejemplo claro de cómo crear una **base de datos documental (tipo MongoDB)** para una tienda que vende **jerseys, shorts, tenis, mochilas y termos**, incluyendo **colecciones, atributos y tipos de datos**.

---

# 📦 Base de Datos: `tienda_deportiva`

## 🧾 Colección: `productos`

Representa todos los productos de la tienda.

**Ejemplo de documento:**

```json
{
  "_id": ObjectId,
  "nombre": "Jersey Barcelona",
  "categoria": "Jerseys",
  "precio": 1200.50,
  "stock": 25,
  "marca": "Nike",
  "talla": "M",
  "color": "Rojo/Azul",
  "descripcion": "Jersey oficial del Barcelona",
  "fecha_registro": ISODate("2026-04-27"),
  "activo": true
}
```

**Atributos y tipos:**

* `_id`: ObjectId
* `nombre`: String
* `categoria`: String
* `precio`: Number (Decimal)
* `stock`: Number (Int)
* `marca`: String
* `talla`: String
* `color`: String
* `descripcion`: String
* `fecha_registro`: Date
* `activo`: Boolean

---

## 👤 Colección: `clientes`

Información de los clientes.

**Ejemplo:**

```json
{
  "_id": ObjectId,
  "nombre": "Juan",
  "apellido": "Perez",
  "correo": "juan@gmail.com",
  "telefono": "6561234567",
  "direccion": {
    "calle": "Av. Tecnologico",
    "ciudad": "Juarez",
    "pais": "Mexico"
  },
  "fecha_registro": ISODate("2026-04-27")
}
```

**Tipos:**

* `nombre`: String
* `apellido`: String
* `correo`: String
* `telefono`: String
* `direccion`: Object
* `fecha_registro`: Date

---

## 🛒 Colección: `ventas`

Registra las compras realizadas.

**Ejemplo:**

```json
{
  "_id": ObjectId,
  "cliente_id": ObjectId,
  "productos": [
    {
      "producto_id": ObjectId,
      "nombre": "Tenis Nike",
      "cantidad": 2,
      "precio": 1800
    }
  ],
  "total": 3600,
  "fecha": ISODate("2026-04-27"),
  "metodo_pago": "Tarjeta"
}
```

**Tipos:**

* `cliente_id`: ObjectId
* `productos`: Array de objetos
* `total`: Number
* `fecha`: Date
* `metodo_pago`: String

---

## 📦 Colección: `categorias`

Para organizar los productos.

**Ejemplo:**

```json
{
  "_id": ObjectId,
  "nombre": "Jerseys",
  "descripcion": "Playeras deportivas de equipos"
}
```

**Tipos:**

* `nombre`: String
* `descripcion`: String

---

## 🏷️ Colección: `proveedores`

Información de proveedores.

**Ejemplo:**

```json
{
  "_id": ObjectId,
  "nombre": "Nike Mexico",
  "telefono": "5551234567",
  "correo": "contacto@nike.com",
  "direccion": "CDMX"
}
```

---

# 📌 Ejemplo de categorías válidas

* Jerseys
* Shorts
* Tenis
* Mochilas
* Termos

---

# 🧠 Nota importante (Modelo documental)

* No hay tablas como en SQL ❌
* Se usan **colecciones** y **documentos JSON** ✔️
* Puedes **anidar datos** (como productos dentro de ventas)

---

Si quieres, puedo ayudarte a:
✅ Convertir esto a **SQL (tablas y relaciones)**
✅ Hacerlo en **MongoDB paso a paso**
✅ O crear un **diagrama visual para DB Designer**

Solo dime 👍
