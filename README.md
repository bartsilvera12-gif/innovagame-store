# Innovagame Store

Prototipo de la tienda online de Innovagame (Asunción, Paraguay).

- `Innovagame Store.dc.html`: la tienda (se sirve en `/` gracias a `vercel.json`).
- `support.js`: runtime de las plantillas.
- `catalogo/catalogo.js`: 1023 productos exportados del sitio público.
- `catalogo/fotos/`: fotos de cada producto.
- `brand/`: logos e imágenes de marca.

Es un sitio estático: no necesita build. En Vercel, importá el repo con el preset **Other** y dejá vacíos el comando de build y el directorio de salida.

Para verlo en local:

```
python -m http.server 8080
```

y abrí http://localhost:8080/Innovagame%20Store.dc.html
