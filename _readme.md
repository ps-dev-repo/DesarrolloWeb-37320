# Registro de cambios - Changelog

# ➡ [ENTREGA DEL PROYECTO FINAL]


- Se movieron las reglas sass correspondientes al `<Main>`, a su propio `component`
    ```diff
        [...]
        @import "./components/header_navBar";
    -   @import "./components/resto_css_original";
    +   @import "./components/mainSection";
        [...]
    ```

- Se eliminó TODO el código Sass y HTML que no se estaba usando (comentarios no específicos, etc)

- Se anidó algunas propiedades más:
    ```diff
    -   header>nav>ul {
    -       [...]
    -   }

    +       &>ul{
    +           [...]
    +       }
    +   }
    ```

- Se cambió el color de:
    - Fondo NavBar
    - Tipografía NavBar
    - Efecto Hover en enlaces NavBar
    - Efecto background en enlaces NavBar
    - Efecto lava del Logo "Paolo Sartori")

- Se agregó un efecto Hover sobre las imágenes de la sección `#proyectos`. Cuyo valor es tomado de un atributo `"title"` del contenedor. Y se hicieron las adecuaciones necesarias en el DOM y en las reglas Sass/CSS que eran necesarias. (incluyendo `clamp` para adecuar tamaño de letra al tamaño de su padre y del viewport)
    ```html
        <div class="div_img_hover" title="Reconocimiento de Lenguaje de señas">
    ```
    ```scss
        /* efecto hover */
        position: relative;
        overflow: hidden;
        &[title]::before{
            @extend h2;
            position: absolute;
            content: attr(title);
            width: 100%;
            height: 100%;
            text-align: center;
            display: flex;
            align-items: center;
            color: lighten($color: $color-texto, $amount: 15%) ;
            font-size: clamp(0.75rem, 5.5vw, 1rem);
            background: rgba($color: black, $alpha: 0.65);
            transform: translateY(100%);
            transition: transform 0.25s ease;

            @media screen and (max-width: 414px) {
                font-size: smaller;
            }

        }
        &[title]:hover::before{
            transform: none;
        }
        /* FIN efecto hover */
    ```

- Se pasaron *todas* las variables de tipo CSS a su equivalente en SASS
    ```diff
    -   :root {
    -       --color-texto: rgb(147, 125, 209);
        [...]
    +   $color-texto: rgb(147, 125, 209);
    ```
    ```diff
    -   background-image: linear-gradient(-45deg, var(--gradiente-fondo-h2-1), var(--gradiente-fondo-h2-2));
        [...]
    +   background-image: linear-gradient(-45deg, $gradiente-fondo-h2-1, $gradiente-fondo-h2-2);
    ```

-   Se hizo una limpieza de código, eliminando código y etiquetas no usadas
    ```diff
        <li>Análisis y comprobación mediante pruebas y simulación de los circuitos analógicos condicionadores de señales.</li>
    -   <!-- <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Ratione, sit?</p> -->
    -   <!-- <li>Análisis, diseño, armado y prueba de la placa prototipo para el procesamiento mediante microcontrolador.</li> -->
    ```

- Se deshizo la utilización de ciertas recursos de Sass que ya no eran necesarios
    ```diff
    -   @mixin flex_centrado($direction: row) {
    -       display: flex;
    -       justify-content: center;
    -       align-items: center;
    -       @if $direction==column {
    -           flex-direction: column;
    -       }
    -   }
    ```
    ```diff
    -   @include flex_centrado(column);

    +   display: flex;
    +   flex-direction: column;
    +   justify-content: center;
    ```

- Correción en las capas del NAV para permitir usar el "Logo" como anchor al Home

- Mejoras estéticas en la sección `#idiomas`
    ```diff
        <p>Español</p>
    +   <h3>🟊🟊🟊🟊🟊</h3>
    *   <p><em>Nativo.</em></p>
    ```

- Se convirtió los items `<li>` de la sección `#experiencia` a "Card" que voltean al pasar el mouse por encima. Para ello se adaptó tanto el CSS/Sass con el uso de pseudo clases `:after` y `:before` para evitar una re-estructuración radical del HTML.
    - Los títulos se toman mediante `attr()` de un atributo `[title-card]` de los contenedores respectivos
    ```scss
    &#experiencia {
        div>ul>li[title-card]{

            &>*{
                transform: rotateY(180deg);
                transform-style: preserve-3d;
                perspective: 100px;
                transition: transform 0.5s ease;
                backface-visibility: hidden;
            }
            &:hover>*{
                transform: rotateY(0);
            }

            /* efecto de Card Hover */
            position: relative;
            /* se usa ::after para el Card-Front*/
            /* y se usa ::before para darle un background de 100% x 100% */
            &::before, &::after{
                content: attr(title-card);
                font-size: x-large;
                display: flex;
                justify-content: center;
                align-items: center;
                text-align: center;
                height: 100%;
                width: 100%;
                position: absolute;
                top: 0;
                right: 0;
                backface-visibility: hidden;
                transition: transform 0.5s ease;
                background-color: darken($background-intercalado, $amount: 3%);
                /* efecto para la ¿esquina? */
                border: 2px solid $background-intercalado;
                border-bottom-right-radius: 40px;
            }
            // sólo para que el background de fondo quede al 100%
            &::before{
                content: "";
                backface-visibility: initial;
                border-bottom-right-radius: initial;
                background-color: $background-intercalado;
            }
            &:hover::before, &:hover::after{
                transform: rotateY(180deg);
            }
            /* FIN efecto de Card Hover */
        }
    }
    ```

- Se adaptó la página al hosting `000webhost.com`
    ```html
    <meta name="twitter:domain" content="https://psartori.000webhostapp.com/index.html">
    <link rel="canonical" href="https://psartori.000webhostapp.com/index.html">
    ```
    ```html
    <script>
        window.addEventListener("load", function (event) {
            document.getElementsByClassName("disclaimer")[0].remove();
            console.log("Eliminado!");
        });
    </script>
    ```


---
***
## Entregas anteriores 👇🏻👇🏻👇🏻👇🏻👇🏻👇🏻
***
---

# [Entrega: **SASS II + SEO**]
## SEO

- Cambio de Titulo por un título más descriptivo:
    ```html
    <title>Portfolio Desarrollador Web - Paolo Sartori</title>
    ```

- Incorporación de keywords *(aunque estén deprecadas en Google)* :
    ```html
    <meta name="keywords" content="Desarrollo Web, Portfolio, web, web3, Software, HTML, CSS, Inteligencia Artificial, Deep Learning, Machine Learning">
    ```

- Incorporación del resto de meta tags referentes al SEO como `description`, `author`, `robots`, etc :
    ```html
    <!-- SEO -->
    <title>Portfolio Desarrollador Web - Paolo Sartori</title>
    <meta name="description" content="Soy una persona que le gusta buscar soluciones a problemas utilizando herramientas tecnológicas, y facilitar la vida de las personas de este modo. Apasionado de las Finanzas, Stocks, Crypto y DeFi. Estoy buscando nuevos desafíos hacia el camino de la Programación y el Software.">
    <meta name="keywords" content="Desarrollo Web, Portfolio, web, web3, Software, HTML, CSS, Inteligencia Artificial, Deep Learning, Machine Learning">
    <meta name="robots" content="index">
    <meta name="author" content="Paolo Sartori">
    <link rel="canonical" href="./index.html">
    ```

- Incorporación de los Open Graph tags para redes sociales:
    ```html
    <!-- Open Graph - Social Netw -->
    <meta name="og:title" content="Portfolio Desarrollador Web - Paolo Sartori">
    <meta name="og:site_name" content="Portfolio Desarrollador Web - Paolo Sartori">
    <meta name="og:type" content="website">
    <meta name="og:description" content="Soy una persona que le gusta buscar soluciones a problemas utilizando herramientas tecnológicas, y facilitar la vida de las personas de este modo. Apasionado de las Finanzas, Stocks, Crypto y DeFi. Estoy buscando nuevos desafíos hacia el camino de la Programación y el Software.">
    <meta name="og:image" content="./assets/img/imagenPerfil.jfif">
    <meta name="og:url" content="./index.html">
    <meta name="twitter:card" content="summary">
    <meta name="twitter:title" content="Portfolio Desarrollador Web - Paolo Sartori">
    <meta name="twitter:image:src" content="./assets/img/perfil.jfif">
    <meta name="twitter:domain" content="./index.html">
    ```

- Mejora en las descripciones de los `alt` de los elementos multimedia (repitiendo la descripción en el atributo `title`):
    ```html
    <img src="./assets/img/Real_Time_IA_deaf_sign_MVP.gif" alt="Reconocimiento de Lenguaje de señas" title="Reconocimiento de Lenguaje de señas">
    ```
    ```html
    <img src="./assets/img/Blind_IA_prototype.png" alt="Asistencia virtual discapacitado Visual" title="Asistencia virtual discapacitado Visual">
    ```
    ```html
    <img src="../assets/img/imagen-formulario.jfif" alt="imagen adorno formulario" title="Complete su formulario">
    ```
    ```html
        ...
    ```

- incorporación del atributo `title` a los anchor del footer para que sea más descriptivo para el usuario:
    ```html
    <a href="https://api.whatsapp.com/#####" target="_blank" rel="noopener noreferrer" title="Contante mediante Whatsapp">
            ...
                ...
    <a href="https://api.telegram.com/#####" target="_blank" rel="noopener noreferrer" title="Contacte mediante Telegram">
            ...
                ...
    <a href="https://api.github.com/#####" target="_blank" rel="noopener noreferrer" title="Acceda a nuestro Repositorio">
    ```

- Se quitó el `title` antiguo y el `<script src="./css/style.css` antiguo anterior a la implementación de **Sass**

- Se reemplazo el "logo" estático del NavBar por un anchor anidado que diriga al usuario hacia la página principal/Home:
    ```HTML
        <header id="headerId">
    +		<a href="./index.html">
                <h2>Paolo Sartori</h2>
    +		</a>
            <nav>
    ```
    - con su respectivo `text-decoration`:
    ```scss
        a {
            text-decoration: none;
        }
    ```

- Se eliminó código comentado ya inutilizado
    ```html
        ...
    <!-- <br> -->
        ...
    ```

- Reemplazo de un GIF que pesaba demasiado y retardaba el tiempo de carga del sitio, por un video `video/mp4` más comprimido y eficiente:
    ```html
    -	<!-- <img src="./assets/img/Real_Time_IA_deaf_sign_MVP.gif" alt="Reconocimiento de Lenguaje de señas" title="Reconocimiento de Lenguaje de señas"> -->
    ```
    ```html
    +	<video src="./assets/video/Real_Time_IA_deaf_sign_MVP (veed.io).mp4" muted autoplay loop></video>
    ```
	- con su correspondiente estilo en Sass:
        ```css
            section#proyectos>div#proyectos_personales_1>div {
                img, video {
                    object-position: 42%;
                }
            }
        ...	img, video {
                width: 10rem;
                height: 10rem;
                max-height: 45vw;
                max-width: 45vw;
                object-fit: cover;
                box-shadow: 0 0 20px -5px;
                margin-inline: 15px;
            }
        ```


## SASS II

- MIXIN:
    ```scss
    @mixin flex_centrado($direction: row) {
        display: flex;
        justify-content: center;
        align-items: center;
        @if $direction==column {
            flex-direction: column;
        }
    }
    ```

- MAPA:
    ```scss
    $list_bulletsMaps: (
        (section: "experiencia", nChild: 3, bullet: "•"),
        (section: "experiencia", nChild: 4, bullet: "•"),
        (section: "experiencia", nChild: 5, bullet: "-"),
        (section: "proyectosLaborales", nChild: 2, bullet: "•"),
        (section: "proyectosLaborales", nChild: 3, bullet: "*"),
        (section: "proyectosLaborales", nChild: 4, bullet: "-"),
        (section: "proyectosLaborales", nChild: 5, bullet: "-"),
    )
    ...
    @each $item in $list_bulletsMaps {
        section##{map-get($item, section)}>div>ul>li:nth-child(#{map-get($item, nChild)})>ul {
            --estilo-lista-dentro-lista: "#{map-get($map: $item, $key: bullet)}";
        }
    }
    ```

- EXTEND:
    ```scss
        ...
            ...
            &>input[type=reset] {
                background-color: $gradiente-borde-1;
                color: white;
                font-weight: bold;
                padding: 5px;
                flex-grow: 1;
                box-shadow: 0px 0px 7px $color-texto;
                
                &:hover{
                background-color: $color-3;
                background-image: url("https://uploads-ssl.webflow.com/61f03747d8d407ed117df27f/61f116f06248585a2739061f_Button%20BG.png");
                }
            }
        
            &>input[type=submit] {
                @extend [type=reset];
                
                &:hover{
                    background-color: $gradiente-fondo-h2-1;
                    background-image: url("https://uploads-ssl.webflow.com/61f03747d8d407ed117df27f/61f116f06248585a2739061f_Button%20BG.png");
                    background-size: cover;
                }
            }
        ...
    ```
 