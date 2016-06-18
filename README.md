# Before Tooltips
Tooltips pure CSS / Tooltips usando solo CSS

[Demostración](https://zkreations.github.io/Before-Tooltips/)

## Instalación

[Descargar](https://github.com/zkreations/Before-Tooltips/archive/master.zip) e incluir arriba de `</head>` el codigo css.

```html
<link rel="stylesheet" href="btooltips.min.css"/>
```

### Utilizar Before Tooltips

La forma mas fácil es mediante un enlace que contenga el atributo **title** y la class **btips**

```html
<a class="btips" title="Solo soy un tooltip" href="#url">Hola mundo</a>
```

Before Tooltips no se limita únicamente a los enlaces, funciona con cualquier etiqueta, pero en lugar del atributo **title** se requiere **data-title**

```html
<span class="btips" data-title="Solo soy un tooltip">Hola mundo</span>
```

### Cambiar orientacion

Por defecto, Before Tooltips siempre se muestra arriba del objeto. Para cambiar la orientación se agrega la class **l**, **r** o **b**:

* Arriba (por defecto): `<a class="btips" title="Arriba">Arriba</a>`
* Abajo: `<a class="btips b" title="Abajo">Abajo</a>`
* Izquierda: `<a class="btips l" title="Izquierda">Izquierda</a>`
* Derecha: `<a class="btips r" title="Derecha">Derecha</a>`

## Limitaciones

* Before Tooltips no funciona con etiquetas de auto cierre. Ejemplo: `<img/>` `<input/>`. Pero estas etiquetas pueden ser encerradas para hacer uso de **Before Tooltips** de la siguiente manera: `<a class="btips"><img/></a>`
