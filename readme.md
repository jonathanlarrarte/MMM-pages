

# MMM-páginas

Este módulo [MagicMirror²] [mm] te permite tener páginas en tu espejo mágico. ¿Quieres tener más módulos en tu espejo mágico, pero quieres mantener el formato? O bien, ¿desea tener módulos agrupados que tengan temas juntos? ¡No busque más!

[Haga clic aquí para ver un ejemplo de ello en acción!] (Https://www.youtube.com/watch?v=1NQ-sGtdUdg)

Tenga en cuenta que este módulo no proporciona ningún método para cambiar manualmente la página. ¡Debería pedirles a otros desarrolladores que agreguen una notificación a sus módulos, o añada uno usted mismo!

## Instalación

En tu terminal, ve a la carpeta Módulo MagicMirror:

```bash
cd ~/MagicMirror/modules
```
Clone this repository:
```bash
git clone https://github.com/edward-shen/MMM-pages.git
```
Configure the module in your config.js file.

\<self-promotion>
To display what page you're on, I'd highly recommend checking out my [page indicator module][page indicator].
\<\\self-promotion>


## Uso del módulo

Para usar este módulo, agréguelo a la matriz de módulos en `config/config.js` file:
```js
modules: [
    {
        module: 'MMM-pages',
        config: {
                modules:
                    [[ "weatherforecast", "newsfeed"],
                     [ "calendar", "compliments" ]],
                excludes: ["clock", "currentweather", "MMM-page-indicator"],
        }
    }
]
```

## Opciones de configuración

Opción | Descripción
------ | -----------
`modules` | Una matriz de cadenas 2D de lo que debe ser cada módulo en cada página. Tenga en cuenta que todas las entradas deben tomar su nombre de clase (por ejemplo, el nombre de clase de este módulo es `MMM-pages`, mientras que los módulos predeterminados pueden tener` newsfeed`, sin el prefijo `MMM-`. <br/> ** Tipo de valor esperado : ** `[[String, String, ...], [String, String, ...], ...]`.
`excludes` | Qué módulos deberían aparecer todo el tiempo. <br/> ** Tipo de valor esperado: **` [String, String, ...] `.
`animationTime` | Tiempo de animación de desvanecimiento. Establecer en `0` para un cambio instantáneo. El valor está en milis. <br/> ** Tipo de valor esperado: ** `int`.
`rotationTime` | Time, en milisegundos (1 segundo = 1000 milisegundos), entre cambios automáticos de página. <br/> ** Tipo de valor esperado: **` int`. <br/> ** Valor predeterminado: ** `0 `
`delayTime` | Tiempo, en milisegundos, de cuánto tiempo debe demorar el cambio de una página manual antes de volver al cambio automático de página. En otras palabras, ¿cuánto tiempo debe esperar el temporizador después de cambiar manualmente una página? Esto incluye el tiempo de animación, por lo que es posible que desee aumentarlo unos segundos más o menos para tener en cuenta el tiempo de animación. <br/> ** Tipo de valor esperado: ** `int`. <br/> ** Predeterminado valor: ** `10000

Para la opción de configuración `module`, el primer elemento de la matriz externa debe consistir en elementos que deberían estar en la primera página. El segundo elemento debe consistir en elementos que deben estar en la segunda página, y así sucesivamente.

## En cuanto a las notificaciones

Este módulo responde a la notificación `PAGE_CHANGED`. La carga útil debe ser un `entero '. Tenga en cuenta que esto tiene una estricta comprobación de errores, por lo que `" 3 "` no funcionará, mientras que `3` lo hará. También tenga en cuenta que para pasar a la página 1, debe enviar `0` al módulo. ** Esto usa un sistema de numeración basado en cero. **

Digamos que quiere cambiar el indicador a la página 3. En su código, debería escribir:
`` `js
this.sendNotification ("PAGE_CHANGED", 2);
`` `
Esto causaría que el módulo cambie y muestre que está en la página 3.

También puede enviar `PAGE_INCREMENT` o` PAGE_DECREMENT` sin ninguna carga útil (o con, pero se ignorará) para que el módulo cambie la página mostrada por uno.

Este módulo mantiene un registro interno de cuántas páginas tiene, definidas por su configuración en el archivo de configuración. No hay forma de cambiar dinámicamente las páginas que tienes. Si surge una necesidad, crea un problema.

Este módulo envía una notificación, `MAX_PAGES_CHANGED` para ayudar a mostrar los módulos con cuántas páginas deben mostrar. Sin embargo, este módulo no impone qué página deberían indicar otros módulos. Esto es intencional, porque cualquier otro módulo que necesite una notificación de cambio de página debería estar recibiendo del sistema de notificación.
[mm]: https://github.com/MichMich/MagicMirror
[page indicator]: https://github.com/edward-shen/MMM-page-indicator
