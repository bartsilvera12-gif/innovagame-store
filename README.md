# Innovagame Store

Prototipo de la tienda online de Innovagame (Asunción, Paraguay).

- `Innovagame Store.dc.html`: la tienda (se sirve en `/` gracias a `vercel.json`).
- `support.js`: runtime de las plantillas.
- `catalogo/catalogo.js`: 1023 productos exportados del sitio público.
- `catalogo/fotos/`: fotos de cada producto.
- `brand/`: logos e imágenes de marca.

## Integración con el ERP (innovagames.neura.com.py)

La tienda toma todo del ERP de Innovagames (`window.IG_ERP` en el `<head>`):

- **Catálogo:** `<script src="https://innovagames.neura.com.py/api/publico/tienda/catalogo?js=1">` define `window.IG_CATALOG` con los productos marcados *En la tienda web* en Inventario (precio, stock, fotos). Si el ERP no responde, se carga el catálogo guardado `catalogo/catalogo.js`.
- **Listas de bodas:** `window.IG_BODAS_URL` = `/api/publico/tienda/bodas` (se arman en el ERP › Tienda web).
- **Pedidos:** el checkout hace `POST /api/publico/tienda/pedido` y el pedido entra al ERP como presupuesto (origen web). Sin ERP, el checkout manda el pedido por WhatsApp.

### Formato de las listas de bodas

El formato es el mismo de `catalogo/listas-bodas.json` (respaldo):

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

## Logos de marcas

La sección **Marcas** (página y panel del encabezado) muestra el nombre de cada marca como texto. Si el ERP define `window.IG_MARCAS` con logos, se usan en lugar del texto:

```js
window.IG_MARCAS = [
  { "nombre": "SAMSUNG", "logo": "https://…/samsung.png" }
];
```

También sirve una ruta local, por ejemplo `brand/marcas/samsung.png`. El nombre tiene que coincidir con la marca del catálogo (no importan mayúsculas).

Es un sitio estático: no necesita build. En Vercel, importá el repo con el preset **Other** y dejá vacíos el comando de build y el directorio de salida.

Para verlo en local:

```
python -m http.server 8080
```

y abrí http://localhost:8080/Innovagame%20Store.dc.html
