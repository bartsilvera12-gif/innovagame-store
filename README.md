# Innovagame Store

Prototipo de la tienda online de Innovagame (Asunción, Paraguay).

- `Innovagame Store.dc.html`: la tienda (se sirve en `/` gracias a `vercel.json`).
- `support.js`: runtime de las plantillas.
- `catalogo/catalogo.js`: 1023 productos exportados del sitio público.
- `catalogo/fotos/`: fotos de cada producto.
- `brand/`: logos e imágenes de marca.

## Lista de bodas (integración con el ERP)

La página **Lista de bodas** lee `catalogo/listas-bodas.json` cada vez que se abre la tienda. El ERP solo tiene que publicar ese archivo (o un endpoint con el mismo formato) y la web se actualiza sola. Para leerlo desde otra dirección, definí `window.IG_BODAS_URL` antes de cargar la tienda.

```json
{
  "listas": [
    {
      "id": "garcia-lopez-2027",
      "novios": "María y Juan",
      "fecha": "2027-05-14",
      "mensaje": "Texto opcional de los novios",
      "productos": [
        { "id": 7466, "cantidad": 1, "regalados": 0 }
      ]
    }
  ]
}
```

- `novios` es el nombre que aparece como subcategoría.
- `productos[].id` es el ID del producto en el catálogo (el mismo de la web del sitio actual).
- `regalados` lo actualiza el ERP a medida que se venden los regalos.
- La lista con `"ejemplo": true` es solo de muestra: hay que borrarla cuando el ERP publique listas reales.

Es un sitio estático: no necesita build. En Vercel, importá el repo con el preset **Other** y dejá vacíos el comando de build y el directorio de salida.

Para verlo en local:

```
python -m http.server 8080
```

y abrí http://localhost:8080/Innovagame%20Store.dc.html
