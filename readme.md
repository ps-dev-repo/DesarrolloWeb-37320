# Registro de cambios - Changelog

# ➡ [PROYECTO FINAL]

- Se convirtió el listado de `#proyectosLaborales` a un Linea de tiempo (haciendo uso de atributos `[data-*]`) para resoluciones mayores a 415px.
    Para ello se adaptó tanto el CSS/Sass con el uso de todos los recursos aprendidos en el curso, para evitar una re-estructuración radical del HTML y de las reglas css/sass ya productivas.
    ```scss
        [...]
        &#proyectosLaborales {
                /* efecto de timeline (para dimensiones mayores a Mobile) */
                @media screen and (min-width: 415px){
                &>div{
                        position: relative;
                        justify-content: center;
                        &>ul{
                            grid-template-columns: repeat(2, 48%);
                            justify-content: center;
                            gap: 5.5rem; 
                            column-gap: calc(5vw + 5px);
                            column-gap: 0;
                            position: relative;

                            &>li{
                                padding: 0.5rem;
                                margin-left: 1.25rem;
                                grid-column: 2 / 3;
                                border: 2px solid $color-texto;
                                border-radius: 10px;
                                &:nth-of-type(odd){
                                    transform-origin: -1.2rem;  /* ajustado a ojo */
                                    transform: rotateY(-180deg);
                                    >*{
                                        transform-origin: center;
                                        transform: rotateY(+180deg);
                                    }
                                }

                                position: relative;
                                &::after{
                                    content: attr(data-year);
                                    position: absolute;
                                    font-size: 2.1rem;
                                    top: 7.5px; /* ajustado a ojo */
                                    transform-origin: right;
                                    transform: translateX(-7.5rem);
                                }
                                &:nth-of-type(odd)::after{
                                    content: attr(data-year);
                                    transform-origin: center;
                                    transform: rotateY(-180deg) translateX(7.5rem);
                                }
                            }
                        }

                        &>ul::after{
                            /* linea vertical del medio */
                            content: "";
                            position: absolute;
                            text-align: center;
                            width: 2.5px;
                            height: 100%;
                            background-color: $color-texto;
                            grid-column: 2;
                            z-index: -1;
                        }
                    }
                }
            }
        [...]
    ```

    - Se le agreguó a la Linea de Tiempo, efectos de animación al scrollear con la librería 'AOS'. Además se realizaron los ajustes necesarios para adecuarlo a las reglas `transform:(...)` ya existentes, y para desactivar la animación en las vistas Mobile < 415px.
        ```html
        <script src="https://unpkg.com/aos@2.3.1/dist/aos.js"></script>
        <script>
            //// obtengo el mediaQuery que uso para desactivar el timeline y lo reutilízo para desactivar la AoS ////
            let mediaQuery = Array.prototype.slice.call(document.styleSheets[1].cssRules).filter(cssRule=> { return cssRule.type==4}).find(item=> {return item.cssRules[0].cssText.startsWith("main section#proyectosLaborales")}).conditionText;
                AOS.init({
                // Settings that can be overridden on per-element basis, by `data-aos-*` attributes:
                disable: (!window.matchMedia(mediaQuery).matches),
                [...]
        ```

- Por consejo estético, se mejoró la Tipografía de los textos `<p>` y `<li>`
    ```scss
        [...]
            font-family: Verdana, Geneva, Tahoma, sans-serif;
            font-size: 0.74rem;
            line-height: 1.25rem;
        }
        [...]
    ```

- Se mejoró la respuesta Responsive del sitio, prescindiendo del uso de reglas `@media query` para la respuesta de las columnas grids, incorporando la función `min(#,##)` dentro de la función `minmax(##, ##, ##)` de la regla `grid-template-columns`:
    ```scss
        [...]
            grid-template-columns: repeat(auto-fit, minmax(min(250px,100%), 1fr));
        [...]
            grid-template-columns: repeat(auto-fit, minmax(min(100px,100%), 1fr));
        [...]
    ```
    - Ahora el Resposive Grid ya no depende de una media query hardcodeada.

- Se mejoró el efecto de borde degradé con animación spin alrededor de la "Foto de Perfil" llevandoló a elemento `:before` de manera de dejar de afectar los respectivos hijos del contenedor:
    ```scss
        [...]
        position: relative;

        &::before{
            content: "";
            position: absolute;
            width: inherit;
            height: inherit;
            max-height: inherit;
            max-width: inherit;
            border-radius: inherit;
            background: linear-gradient(45deg, $gradiente-borde-1, $gradiente-borde-2);
            animation: rotar 5s infinite ease-in-out , radio 5s infinite linear;
            box-shadow: 1px 0 10px;
            z-index: -1;
        }
        [...]
    ```

- Se agregó un delay al salir del efecto `:hover` en los Cards de "#experiencia"

- Limpieza de todo el contenido multimedia (assets) que no estaba siendo utilizado.
- Adecuación de los nombres de todos los assets multimedia a camelCase

- Se arregló el problema de compatibilidad de los caractéres ★ que impedían que se renderizada correctamente en todas las plataformas, por una solución compatible cross-OS


- Se mejoró algunas reglas CSS/SASS, como por ejemplo el indentado de de los subelementos de listas, y las listas `<ul>` anidadas dentro de otras listas `<ul>`
    ```diff
        [...]
    -   &>li::first-letter {
    -       padding-left: 0.5rem;
        }

    +   &>li{
    +       text-indent: 0.5rem;
        }
        [...]
    ```

- Se rehizo el script que bloquea el banner de `000webhostapp.com`

- Se adaptó las paginas del sitio al nuevo hosting de `000webhost.com`
    ```html
    <meta name="twitter:domain" content="https://psartori01.000webhostapp.com/index.html">
    <link rel="canonical" href="https://psartori01.000webhostapp.com/index.html">
    ```
    ```html
    <script>
        window.addEventListener("load", function (event) {
            console.log(document.getElementsByClassName("disclaimer")[0]);
            document.getElementsByClassName("disclaimer")[0]?.remove();
            console.log(document.querySelector('img[src="https://cdn.000webhost.com/000webhost/logo/footer-powered-by-000webhost-white2.png"]').parentElement.parentElement);
            document.querySelector('img[src="https://cdn.000webhost.com/000webhost/logo/footer-powered-by-000webhost-white2.png"]').parentElement.parentElement?.remove();
            console.log("Eliminado!");
        });
    </script>
    ```


---
***
## Puedes acceder a la lista de cambios de la entrega previa en 👉🏻[previousChangelog](./previousChangelog.md)
***
---