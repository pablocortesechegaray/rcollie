---
publishDate: 2023-06-12T00:00:00Z
title: Filtrar un lookup de Dynamics 365 usando JavaScript
description: Descubre cómo mejorar la experiencia de uso en los campos de búsqueda aplicando filtros personalizados mediante JavaScript.
excerpt: Descubre cómo mejorar la experiencia de uso en los campos de búsqueda aplicando filtros personalizados mediante JavaScript.
image: ~/assets/images/prefiltrar-lookup-por-javascript.jpg
category: Desarrollo
tags:
  - JavaScript
canonical: https://astrowind.vercel.app/prefiltrar-lookup-dynamics-365-por-javascript
---

## Introducción

En Dynamics 365, el prefiltrado de datos en un campo de búsqueda es una funcionalidad útil que permite limitar los resultados que mostramos al usuario. Existen dos formas de prefiltrar los datos que mostramos en un campo lookup:

- Mediante parametrización estándard que podemos realizar desde el formulario.
- Mediante un desarrollo JavaScript que aplique un filtro personalizado sobre el lookup.

Es recomendable que se haga uso del prefiltrado mediante parametrización estándar siempre y cuando esto sea posible. Sin embargo, en ocasiones por necesidades del proyecto o de la lógica de negocio del cliente nos vemos obligados a aplicar filtros dinámicos o filtros con lógica compleja y tenemos que realizar un desarrollo JavaScript para obtener los resultados que esperamos.

## ¿Cómo realizar filtrado de lookup por JavaScript?

- Luctus euismod pretium nisi et, est dui enim.

- Curae eget inceptos malesuada, fermentum class.

- Porttitor vestibulum aliquam porta feugiat velit, potenti eu placerat.

- Ligula lacus tempus ac porta, vel litora.

Torquent non nisi lacinia faucibus nibh tortor taciti commodo porttitor, mus hendrerit id leo scelerisque mollis habitasse orci tristique aptent, lacus at molestie cubilia facilisis porta accumsan condimentum. Metus lacus suscipit porttitor integer facilisi torquent, nostra nulla platea at natoque varius venenatis, id quam pharetra aliquam leo. Dictum orci himenaeos quam mi fusce lacinia maecenas ac magna eleifend laoreet, vivamus enim curabitur ullamcorper est ultrices convallis suscipit nascetur. Ornare fames pretium ante ac eget nisi tellus vivamus, convallis mauris sapien imperdiet sollicitudin aliquet taciti quam, lacinia tempor primis magna iaculis at eu. Est facilisi proin risus eleifend orci torquent ultricies platea, quisque nullam vel porttitor euismod sociis non, maecenas sociosqu interdum arcu sed pharetra potenti. Aliquet risus tempus hendrerit sapien tellus eget cursus enim etiam dui, lobortis nostra pellentesque odio posuere morbi ad neque senectus arcu eu, turpis proin ac felis purus fames magnis dis dignissim.

Orci volutpat augue viverra scelerisque dictumst ut condimentum vivamus, accumsan cum sem sollicitudin aliquet vehicula porta pretium placerat, malesuada euismod primis cubilia rutrum tempus parturient. Urna mauris in nibh morbi hendrerit vulputate condimentum, iaculis consequat porttitor dui dis euismod eros, arcu elementum venenatis varius lectus nisi. Nibh arcu ultrices semper morbi quam aptent quisque porta posuere iaculis, vestibulum cum vitae primis varius natoque conubia eu. Placerat sociis sagittis sociosqu morbi purus lobortis convallis, bibendum tortor ridiculus orci habitasse viverra dictum, quis rutrum fusce potenti volutpat vehicula. Curae porta inceptos lectus mus urna litora semper aliquam libero rutrum sem dui maecenas ligula quis, eget risus non imperdiet cum morbi magnis suspendisse etiam augue porttitor placerat facilisi hendrerit. Et eleifend eget augue duis fringilla sagittis erat est habitasse commodo tristique quisque pretium, suspendisse imperdiet inceptos mollis blandit magna mus elementum molestie sed vestibulum. Euismod morbi hendrerit suscipit felis ornare libero ligula, mus tortor urna interdum blandit nisi netus posuere, purus fermentum magnis nam primis nulla.

## Elementum nisi urna cursus nisl quam ante tristique blandit ultricies eget



## Código

```js
function FiltrarLookup(formContext) {
    //<summary>
    // Filtra un lookup de la entidad "product" con un filtro personalizado haciendo uso de addPreSearch.
    //</summary>

    const lookupSchemaName = "productid";
    const lookupEntityName = "product";
    const filtroXML = `<filter type="and">
                        <condition attribute="statecode" operator="eq" value="1" />
                       </filter>`;

    const lookupControl = formContext.getControl(lookupSchemaName);

    if (lookupControl != null) 
    {
        lookupControl.addPreSearch(() => {
            lookupControl.addCustomFilter(filtroXML, lookupEntityName);
        });
    }
}
```