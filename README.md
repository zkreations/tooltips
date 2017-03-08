# Before Tooltips
Tooltips pure CSS / Tooltips usando solo CSS

[Demostración](https://zkreations.github.io/Before-Tooltips/)

## Instalación

[Descargar](https://github.com/zkreations/Before-Tooltips/archive/master.zip) e incluir arriba de `</head>` el codigo css.

```html
<link type="text/css" rel="stylesheet" href="btips.min.css"/>
```

O puedes usar rawgit como cdn:

```html
<link type="text/css" rel="stylesheet" href="https://cdn.rawgit.com/zkreations/Before-Tooltips/master/dist/btips.min.css"/>
```

### Utilizar Before Tooltips

La forma mas fácil es mediante un enlace que contenga el atributo **data-title** y la class **btips**

```html
<a class="btips" data-title="texto del tooltip" href="#url">Hola mundo</a>
```

Before Tooltips no se limita únicamente a los enlaces, funciona con cualquier etiqueta:

```html
<span class="btips" data-title="Solo soy un tooltip">Hola mundo</span>
```

### Cambiar orientacion

Por defecto, Before Tooltips siempre se muestra arriba del objeto. Para cambiar la orientación se agrega el atributo **data-btips** y dentro se especifica la orientacion:

* Arriba (por defecto): `<a class="btips"></a>`
* Abajo: `<a class="btips" data-btips="bottom"></a>`
* Izquierda: `<a class="btips" data-btips="left"></a>`
* Derecha: `<a class="btips" data-btips="right"></a>`

## Animaciones

Por defecto Before Tooltips no muestra ninguna animacion, todas las animaciones se agregan a partir de un doble guion, puedes elegir entre las siguientes:

* Default: `<a class="btips"></a>`
* Fade: `<a class="btips--fade"></a>`
* Slide In: `<a class="btips--slide-in"></a>`
* Slide Out: `<a class="btips--slide-out"></a>`
* Bounce In: `<a class="btips--bounce-in"></a>`
* Bounce Out: `<a class="btips--bounce-out"></a>`

## Limitaciones

* Before Tooltips no funciona con etiquetas de auto cierre. Ejemplo: `<img/>` `<input/>`. Para que funcione es necesario un contenedor: `<a class="btips"><img/></a>`
