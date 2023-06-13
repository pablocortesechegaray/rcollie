---
publishDate: 2023-06-12T00:00:00Z
title: Filtrar un lookup de Dynamics 365 usando JavaScript
description: Descubre cómo mejorar la experiencia de uso en los campos de búsqueda aplicando filtros personalizados mediante JavaScript.
excerpt: Descubre cómo mejorar la experiencia de uso en los campos de búsqueda aplicando filtros personalizados mediante JavaScript.
image: ~/assets/images/javascript-mug.jpg
category: Desarrollo
tags:
  - JavaScript
canonical: https://astrowind.vercel.app/prefiltrar-lookup-dynamics-365-por-javascript
---

## Introducción

En **Dynamics 365**, el prefiltrado de datos en un campo de búsqueda es una funcionalidad muy útil que nos permite limitar los resultados que mostramos al usuario. Existen dos formas de prefiltrar los datos que mostramos en un campo lookup:

- Mediante parametrización estándard que podemos realizar desde el formulario.
- Mediante un desarrollo JavaScript que aplique un filtro personalizado sobre el lookup.

Es recomendable que se haga uso del prefiltrado mediante parametrización estándar siempre y cuando esto sea posible. Te dejo por aquí el **link** por si quieres ver cómo llevarlo a cabo.
En otras ocasiones por necesidades del proyecto o de la lógica de negocio del cliente nos vemos obligados a aplicar filtros dinámicos o filtros con lógica compleja y tenemos que realizar un desarrollo JavaScript para obtener los resultados que esperamos.

## ¿Cómo realizar prefiltrado de lookup por JavaScript?

Para realizar el filtrado de un lookup mediante JavaScript es necesario utilizar el método [**addPreSearch()**](https://learn.microsoft.com/es-es/power-apps/developer/model-driven-apps/clientapi/reference/controls/addpresearch). Para ello, es necesario que recuperemos el control del campo sobre el que vamos a filtrar y le indiquemos el filtro personalizado que queremos aplicar. Si para obtener el filtro hacemos uso de una búsqueda avanzada es importante que nos acordemos que este método únicamente soporta que le pasemos el contenido que hay dentro de las etiquetas `<filter></filter>`. Si le pasamos el fetchXML completo el desarrollo dará error.

Añado un ejemplo en el cual estoy filtrando un campo lookup que se llama "productid" de la entidad "product" y le estoy pasando un filtro personalizado para que únicamente me devuelva productos en estado Inactivo.

## Ejemplo de cómo poner prefiltro personalizado

```js
function FiltrarLookup(formContext) {
    //<summary>
    // Filtra un lookup de la entidad "product" con un filtro personalizado haciendo uso de addPreSearch.
    //</summary>

    const lookupSchemaName = "productid";
    const lookupEntityName = "product";
    const filterXML = `<filter type="and">
                        <condition attribute="statecode" operator="eq" value="1" />
                       </filter>`;

    const lookupControl = formContext.getControl(lookupSchemaName);

    if (lookupControl != null) 
    {
        lookupControl.addPreSearch(() => {
            lookupControl.addCustomFilter(filterXML, lookupEntityName);
        });
    }
}
```

En caso de hacer uso de este código, acuérdate que tendrás que modificar los valores de las variables **lookupSchemaName**, **lookupEntityName** y **filterXML**.

## ¿Cómo quitar prefiltrado de lookup por JavaScript?

Por otro lado, en ocasiones me he visto con el requerimiento de tener que poner un prefiltro personalizado en base al valor de otro campo del formulario y tener que quitarlo si el usuario borraba el valor. Para poder hacer esto, al igual que en el caso anterior tenemos el método addPreSearch(), existe otro método para quitar un filtro personalizado que previamente hayamos implementado sobre el lookup. El método para realizar esto es [**removePreSearch()**](https://learn.microsoft.com/es-es/power-apps/developer/model-driven-apps/clientapi/reference/controls/removepresearch) y su funcionamiento es muy similar.

Añado un ejemplo en el cuál quito el prefiltro que he aplicado previamente sobre el campo "productid":

## Ejemplo de cómo quitar prefiltro personalizado

```js
function QuitarFiltroLookup(formContext) {
    //<summary>
    // Quita el filtro de un lookup de la entidad "product" haciendo uso de removePreSearch.
    //</summary>

    const lookupSchemaName = "productid";
    const lookupEntityName = "product";
    const filterXML = `<filter type="and">
                        <condition attribute="statecode" operator="eq" value="1" />
                       </filter>`;

    const lookupControl = formContext.getControl(lookupSchemaName);

    if (lookupControl != null) 
    {
        lookupControl.removePreSearch(() => {
            lookupControl.addCustomFilter(filterXML, lookupEntityName);
        });
    }
}
```

Espero que este post te haya sido de ayuda a la hora de **aplicar filtros personalizados en campos de búsqueda mediante JavaScript**.
