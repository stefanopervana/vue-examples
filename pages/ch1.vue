<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    
    <div class="block">
    
  <div id="introduction" >

    <div class="titlepage">

      <div>

        <h1 class="title">Chapter 1. Introduction</h1>

      </div>

    </div>

    <div class="sect1" data-original-filename="1_intro.asciidoc" id="_why_data_visualization">

      <div class="titlepage">

        <div>

          <h2 class="title">Why Data Visualization?</h2>

        </div>

      </div>

      <p class="it">Nuestra era de la información a menudo se siente como una era de sobrecarga de información. Las excesivas cantidades de información son abrumadoras; Los datos en bruto se convierten en útiles sólo cuando aplicamos métodos para conseguir la comprensión de los mismos.</p>

      <p class="p" id="our_information">Our information age more often feels like an era of information overload. Excess amounts of information are overwhelming; raw data becomes useful only when we apply methods of deriving insight from it.</p>



<p class="it">Afortunadamente, los seres humanos somos criaturas intensamente visuales. Pocos de nosotros podemos detectar patrones entre las filas de números, pero incluso los niños pequeños pueden interpretar los gráficos de barras, extraer el significado de las representaciones visuales de esos números. Por esa razón, la visualización de datos es un ejercicio de gran alcance. La visualización de datos es la manera más rápida de comunicar a los demás.</p>
      <p class="p" id="fortunately_we_id1">Fortunately, we humans are intensely visual creatures. Few of us can detect patterns among rows of numbers, but even young children can interpret bar charts, extracting meaning from those numbers’ visual representations. For that reason, data visualization is a powerful exercise. Visualizing data is the fastest way to communicate it to others.</p>


<p class="it">Por supuesto, las visualizaciones, como las palabras, pueden ser usadas para mentir, engañar, o distorsionar la verdad. Pero cuando se practica con honestidad y con cuidado, el proceso de visualización puede ayudarnos a ver el mundo de una manera nueva, revelando patrones y tendencias inesperadas en la información, de otro modo oculta, que nos rodea. En su mejor versión, la visualización de datos es una experta narración.</p>


      <p class="p" id="of_course_visu">Of course, visualizations, like words, can be used to lie, mislead, or distort the truth. But when practiced honestly and with care, the process of visualization can help us see the world in a new way, revealing unexpected patterns and trends in the otherwise hidden information around us. At its best, data visualization is expert storytelling.</p>


<p class="it">Más literalmente, la visualización es un proceso de mapping de la información a efectos visuales. Hemos elaborado normas que interpretan los datos y expresar sus valores como propiedades visuales. Por ejemplo, el humilde gráfico de barras en la figura 1-1 se genera a partir de una regla muy sencilla: los valores más grandes se asignan en forma de barras más altas.</p>

      <p class="p" id="more_literally">More literally, visualization is a process of <span class="emphasis"><em>mapping</em></span> information to visuals. We craft rules that interpret data and express its values as visual properties. For example, the humble bar chart in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch01.html#data_values_mapped_to_visuals" title="Figure 1-1. Data values mapped to visuals">Figure 1-1</a> is generated from a very simple rule: larger values are <span class="emphasis"><em>mapped</em></span> as taller bars.<a id="id483388" class="indexterm" href=""></a></p>

      <div class="figure" id="data_values_mapped_to_visuals">

        <div class="figure-contents">

          <div class="mediaobject">

            <img src="/static/mnqPpLUu0Q-img1.png" alt="Data values mapped to visuals"/>

          </div>

        </div>
<p class="fig">Figura 1-1. Los valores de datos se asignan a elementos visuales.</p>
<p class="fig">Figure 1-1. Data values mapped to visuals</p>

      </div>
<p class="it">Las visualizaciones más complejas se generan a partir de conjuntos de datos más complejos que la secuencia de números mostrada en la Figura 1-1 y conjuntos más complejos de reglas de asignación.</p>
      <p class="p" id="more_complex_vi">More complex visualizations are generated from datasets more complex than the sequence of numbers shown in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch01.html#data_values_mapped_to_visuals" title="Figure 1-1. Data values mapped to visuals">Figure 1-1</a> and more complex sets of mapping rules.</p>


    </div>

    <div class="sect1" data-original-filename="1_intro.asciidoc" id="_why_write_code">

      <div class="titlepage">

        <div>

          <h2 class="title">Why Write Code?</h2>

        </div>

      </div>
<p class="it">Los datos del maping a mano pueden ser satisfactorios, sin embargo, es lento y tedioso. Por lo que normalmente empleamos el poder de la computación para acelerar las cosas. El aumento de la velocidad nos permite trabajar con conjuntos de datos mucho más grandes de miles o millones de valores; lo que habría llevado años de esfuerzo por parte de lo que se pudo mapear a mano en algun momento. Igual de importante, podemos experimentar rápidamente con asignaciones alternativas, ajustar nuestras reglas y ver su representación inmediatamente. Este bucle de escritura / render / evaluaación es fundamental para el proceso iterativo de refinamiento de un diseño.</p>
      <p class="p" id="mapping_data_by">Mapping data by hand can be satisfying, yet is slow and tedious. So we usually employ the power of computation to speed things up. The increased speed enables us to work with much larger datasets of thousands or millions of values; what would have taken years of effort by hand can be mapped in a moment. Just as important, we can rapidly experiment with <span class="emphasis"><em>alternate mappings</em></span>, tweaking our rules and seeing their output re-rendered immediately. This loop of write/render/evaluate is critical to the iterative process of refining a design.<a id="id483437" class="indexterm" href=""></a></p>

<p class="it">Los conjuntos de reglas de asignación funcionan como sistemas de diseño. La mano humana ya no ejecuta la salida visual; la computadora lo hace. Nuestro papel humano es conceptualizar, construir, y escribir las reglas del sistema, que es finalmente ejecutado por el software.</p>
      <p class="p" id="sets_of_mapping">Sets of mapping rules function as <span class="emphasis"><em>design systems</em></span>. The human hand no longer executes the visual output; the computer does. Our human role is to conceptualize, craft, and write out the rules of the system, which is then finally executed by software.<a id="id483453" class="indexterm" href=""></a><a id="id483458" class="indexterm" href=""></a></p>

<p class="it">Desafortunadamente, el software (y la computación en general) es muy mala en la comprensión de qué es exactamente lo que la gente quiere. (Para ser justos, muchos seres humanos también no son buenos en esta difícil tarea.) Debido a que las computadoras son sistemas binarios, todo está encendido o apagado, sí o no, tal o cual, existe o no. Los seres humanos son criaturas más blandas, más suaves, y los equipos no están dispuestos a reunirse con nosotros en el medio, hay que ir a ellos. De ahí la inevitable lucha de aprender a escribir software, en la que nos entrenamos para comunicanos en la sintaxis muy limitada y precisa que el ordenador puede entender.</p>
      <p class="p" id="unfortunately_">Unfortunately, software (and computation generally) is extremely bad at understanding what, exactly, people want. (To be fair, many humans are also not good at this challenging task.) Because computers are binary systems, everything is either on or off, yes or no, this or that, there or not there. Humans are mushier, softer creatures, and the computers are not willing to meet us halfway—we must go to them. Hence the inevitable struggle of learning to write software, in which we train ourselves to communicate in the very limited and precise syntax that the computer can understand.</p>

<p class="it">Sin embargo, seguimos escribiendo código porque ver como nuestras creaciones visuales llegan a la vida es tan gratificante. Practicamos la visualización de datos, ya que es emocionante ver lo que nunca antes se había visto. Es como convocar un genio mágico, visual fuera de una botella de datos inescrutable.</p>

      <p class="p" id="yet_we_continue">Yet we continue to write code because seeing our visual creations come to life is so rewarding. We practice data visualization because it is exciting to see what has never before been seen. It is like summoning a magical, visual genie out of an inscrutable data bottle.<a id="id483484" class="indexterm" href=""></a></p>


    </div>

    <div class="sect1" data-original-filename="1_intro.asciidoc" id="_why_interactive">

      <div class="titlepage">

        <div>

          <h2 class="title">Why Interactive?</h2>

        </div>

      </div>
<p class="it">Las visualizaciones estáticas pueden ofrecer "puntos de vista", sólo precompuesto de los datos, por lo que múltiples puntos de vista estáticos son a menudo necesarios para presentar una variedad de perspectivas sobre la misma información. El número de dimensiones de datos son limitados, también, cuando todos los elementos visuales deben estar presentes en la misma superficie al mismo tiempo. La representación de conjuntos de datos multidimensionales de manera justa en imágenes estáticas es notoriamente difícil. Una imagen fija es ideal cuando las vistas alternativas no son ni necesarias ni deseadas, y requiere ser publicado en un medio estático, como el impreso.</p>
      <p class="p" id="static_visualiz">Static visualizations can offer only precomposed “views” of data, so multiple static views are often needed to present a variety of perspectives on the same information. The number of dimensions of data are limited, too, when all visual elements must be present on the same surface at the same time. Representing multidimensional datasets fairly in static images is notoriously difficult. A fixed image is ideal when alternate views are neither needed nor desired, and required when publishing to a static medium, such as print.<a id="id483509" class="indexterm" href=""></a><a id="id483517" class="indexterm" href=""></a></p>



<p class="it">Dinámicas, visualizaciones interactivas pueden capacitar a las personas para explorar los datos por sí mismos. Las funciones básicas de la mayoría de las herramientas de visualización interactivas han cambiado poco desde 1996, cuando Ben Shneiderman, de la Universidad de Maryland propuso por primera vez una “Visual Information-Seeking Mantra”: visión general de la primera, el zoom y el filtro, detalla a continuación a la carta.</p>

      <p class="p" id="dynamic_intera">Dynamic, interactive visualizations can empower people to explore the data for themselves. The basic functions of most interactive visualization tools have changed little since 1996, when Ben Shneiderman of the University of Maryland first proposed a “Visual Information-Seeking Mantra”: <span class="emphasis"><em>overview first, zoom and filter, then details-on-demand.</em></span></p>


<p class="it">Este patrón de diseño se encuentra en la mayoría de visualizaciones interactivas hoy. La combinación de funciones se realiza correctamente, ya que hace a los datos accesibles a diferentes públicos, desde los que simplemente están navegando o exploran el conjunto de datos a los que se acercan a la visualización de imágenes con una pregunta específica en busca de una respuesta. Una visualización interactiva que ofrece una visión general de los datos, junto con herramientas para "profundizar" en los detalles pueden cumplir con éxito muchas funciones a la vez, hacer frente a las diferentes inquietudes de los diferentes públicos, desde los nuevos en la materia a los que ya están profundamente familiarizados con los datos.</p>

      <p class="p" id="this_design_pat">This design pattern is found in most interactive visualizations today. The combination of functions is successful, because it makes the data accessible to different audiences, from those who are merely browsing or exploring the dataset to those who approach the visualization with a specific question in search of an answer. An interactive visualization that offers an overview of the data alongside tools for “drilling down” into the details may successfully fulfill many roles at once, addressing the different concerns of different audiences, from those new to the subject matter to those already deeply familiar with the data.</p>

<p class="it">Por supuesto, la interactividad también puede alentar el compromiso con los datos de una manera que las imágenes estáticas no pueden. Con transiciones animadas e interfaces bien elaboradas, algunas visualizaciones de datos puede hacer que la exploración se sienta más como un juego. La visualización interactiva puede ser un gran medio para enganchar a un público que de otra manera no se preocupa por el tema o los datos a mano.</p>

      <p class="p" id="of_course_inte">Of course, interactivity can also encourage engagement with the data in ways that static images cannot. With animated transitions and well-crafted interfaces, some visualizations can make exploring data feel more like playing a game. Interactive visualization can be a great medium for engaging an audience who might not otherwise care about the topic or data at hand.</p>

    </div>

    <div class="sect1" data-original-filename="1_intro.asciidoc" id="_why_on_the_web">

      <div class="titlepage">

        <div>

          <h2 class="title">Why on the Web?</h2>

        </div>

      </div>
<p class="it">Las visualizaciones no son verdaderamente visuales a menos que se vean. Conseguir que tu trabajo seá visto por otros es crítico, y la publicación en la Web es la manera más rápida para llegar a una audiencia global. Trabajar con tecnologías web estándar significa que su trabajo puede ser visto y experimentado por cualquier persona que utilice un navegador web reciente, independientemente del sistema operativo (Windows, Mac, Linux) y el tipo de dispositivo (portátil, de escritorio, teléfono inteligente, tableta).</p>

      <p class="p" id="visualizations_">Visualizations aren’t truly visual unless they are <span class="emphasis"><em>seen</em></span>. Getting your work out there for others to see is critical, and publishing on the Web is the quickest way to reach a global audience. Working with web-standard technologies means that your work can be seen and experienced by anyone using a recent web browser, regardless of the operating system (Windows, Mac, Linux) and device type (laptop, desktop, smartphone, tablet).<a id="id483578" class="indexterm" href=""></a><a id="id483585" class="indexterm" href=""></a></p>

<p class="it">Lo mejor de todo, todo lo explicado en este libro se puede hacer con herramientas de libre acceso, por lo que la única inversión necesaria es su tiempo. Y todo lo que hablaremos utiliza código abierto, tecnologías web estándar.</p>

      <p class="p" id="best_of_all_ev">Best of all, everything covered in this book can be done with freely accessible tools, so the only investment required is your time. And everything we’ll talk about uses open source, web-standard technologies.</p>

<p class="it">Al evitar el software propietario y plug-ins, puede asegurarse de que sus proyectos son accesibles en la gama más amplia posible de dispositivos, desde ordenadores de sobremesa típicos para tabletas e incluso teléfonos. Cuanto más accesible su visualización, mayor es su audiencia y su impacto.</p>

      <p class="p" id="by_avoiding_pro">By avoiding proprietary software and plug-ins, you can ensure that your projects are accessible on the widest possible range of devices, from typical desktop computers to tablets and even phones. The more accessible your visualization, the greater your audience and your impact.</p>

    </div>

    <div class="sect1" data-original-filename="1_intro.asciidoc" id="_what_this_book_is">

      <div class="titlepage">

        <div>

          <h2 class="title">What This Book Is</h2>

        </div>

      </div>
<p class="it">Este libro es una introducción práctica a la fusión de tres prácticas de visualización de datos, diseño interactivo y desarrollo web utilizando D3, una poderosa herramienta para customizar, la visualización basada en web.</p>

      <p class="p" id="this_book_is_a_">This book is a practical introduction to merging three practices—data visualization, interactive design, and web development—using D3, a powerful tool for custom, web-based visualization.<a id="id483620" class="indexterm" href=""></a></p>

<p class="it">Estos capítulos surgieron de mi propio proceso de aprender cómo utilizar D3. Mucha gente, incluido yo mismo, vienen al D3 con experiencia en el diseño, maping y visualización de datos, pero no la programación y la informática.</p>

      <p class="p" id="these_chapters_">These chapters grew out of my own process of learning how to use D3. Many people, including myself, come to D3 with backgrounds in design, mapping, and data visualization, but not programming and computer science.</p>


<p class="it">D3 tiene un poco de una injusta reputación por ser difícil de aprender. D3 en sí no es tan complicado, pero opera en el dominio de la Web y la Web es complicada. Usar D3 requiere cómodamente algún conocimiento previo de las tecnologías web con los que interactúa, como HTML, CSS, JavaScript y SVG. Muchas personas (me incluyo) son autodidactas cuando se trata de habilidades web. Esto es muy bueno, ya que la barrera de entrada es tan baja, pero problemático, ya que significa que probablemente no aprenderá cada una de estas tecnologías desde el principio. A menudo, simplemente hackearemos algo juntos hasta que parece que funciona, y lo llaman algún día. Sin embargo, el uso exitoso de D3 requiere la comprensión de algunas de estas tecnologías de una manera fundamental.</p>

      <p class="p" id="d_has_a_bit_of">D3 has a bit of an unfair reputation for being hard to learn. D3 itself is not so complicated, but it operates in the domain of the Web, and the Web <span class="emphasis"><em>is</em></span> complicated. Using D3 comfortably requires some prior knowledge of the web technologies with which it interacts, such as HTML, CSS, JavaScript, and SVG. Many people (myself included) are self-taught when it comes to web skills. This is great, because the barrier to entry is so low, but problematic because it means we probably didn’t learn each of these technologies from the ground up—more often, we just hack something together until it seems to work, and call it a day. Yet successful use of D3 requires understanding some of these technologies in a fundamental way.</p>


<p class="it">Debido a que D3 está escrito en JavaScript, aprender a usar D3 a menudo significa aprender mucho acerca de JavaScript. Para muchas personas que hacen datavis, D3 es su introducción a JavaScript (o incluso el desarrollo web en general). Es suficiente para aprender un nuevo lenguaje de programación difícil, por no hablar de una nueva herramienta integrada en ese idioma. D3 le permitirá hacer grandes cosas con JavaScript que nunca se ha intentado siquiera. El tiempo que pasa en el aprendizaje tanto de la lengua y la herramienta le proporcionará una rentabilidad increíble.</p>

<p class="p" id="because_d_is_w">Because D3 is written in JavaScript, learning to use D3 often means learning a lot about JavaScript. For many datavis folks, D3 <span class="emphasis"><em>is</em></span> their introduction to JavaScript (or even web development generally). It’s hard enough to learn a new programming language, let alone a new tool built on that language. D3 will enable you to do great things with JavaScript that you never would have even attempted. The time you spend learning both the language and the tool will provide an incredible payoff.<a id="id483666" class="indexterm" href=""></a></p>

<p class="it">Mi objetivo es reducir ese tiempo de aprendizaje, para que pueda empezar a crear cosas increíbles antes. Tomaremos un enfoque de abajo hacia arriba, a partir de los conceptos fundamentales, añadiendo poco a poco complejidad. No tengo la intención de mostrar cómo hacer determinados tipos de visualizaciones tanto como para ayudar a entender el funcionamiento de D3 suficientemente bien como para tomar esos bloques de construcción y generar diseños de su propia creación.</p>

<p class="p" id="my_goal_is_to_r">My goal is to reduce that learning time, so you can start creating awesome stuff sooner. We’ll take a ground-up approach, starting with the fundamental concepts and gradually adding complexity. I don’t intend to show you how to make specific kinds of visualizations so much as to help you understand the workings of D3 well enough to take those building blocks and generate designs of your own creation.</p>

    </div>

    <div class="sect1" data-original-filename="1_intro.asciidoc" id="_who_you_are">

      <div class="titlepage">

        <div>

          <h2 class="title">Who You Are</h2>

        </div>

      </div>
<p class="it">Usted puede ser un principiante absoluto, alguien nuevo en datavis, desarrollo web, o ambas cosas. (Bienvenido!) Tal vez usted es un periodista interesado en las nuevas formas de comunicar los datos recopilados durante la presentación de informes. O quizás usted es un diseñador, haciendo comodamente infografía estática, pero listo para dar el salto a proyectos interactivos en la Web. Usted podría ser un artista, interesado en el arte generativo, basado en datos. O un programador, que ya está familiarizado con el lenguaje Java y la Web, pero contento de aprender una nueva herramienta y recoger un poco de experiencia en el diseño visual a lo largo del camino.</p>

<p class="p" id="you_may_be_an_a">You may be an absolute beginner, someone new to datavis, web development, or both. (Welcome!) Perhaps you are a journalist interested in new ways to communicate the data you collect during reporting. Or maybe you’re a designer, comfortable drawing static infographics but ready to make the leap to interactive projects on the Web. You could be an artist, interested in generative, data-based art. Or a programmer, already familiar with JavaScript and the Web, but excited to learn a new tool and pick up some visual design experience along the way.<a id="id483705" class="indexterm" href=""></a></p>

<p class="it">Quien quiera que sea, espero que usted:</p>

<p class="p" id="whoever_you_are">Whoever you are, I hope that you:</p>


      <div class="itemizedlist" id="have_heard_of_t_id1">

        <ul class="itemizedlist">
<li class="it"> Haya oído hablar de esta nueva cosa llamada la "World Wide Web" </li><br/>
<li class="p"> Have heard of this new thing called the “World Wide Web” </li>
<li class="it"> Incluso ya podría tener un poco de experiencia en programación</li><br/>
<li class="p"> Might even have a little programming experience already </li>
<li class="it"> Esta un poco familiarizado con HTML, el DOM y CSS </li><br/>
<li class="p"> Are a bit familiar with HTML, the DOM, and CSS </li>
<li class="it"> Ha oído hablar de jQuery o escrito algo de JavaScript antes</li><br/>
<li class="p"> Have heard of jQuery or written some JavaScript before </li>
<li class="it"> No se asusta por siglas desconocidas como CSV, SVG, o JSON </li><br/>
<li class="p"> Aren’t scared by unknown initialisms like CSV, SVG, or JSON </li>
<li class="it"> Busca hacer visualizaciones interactivas útiles </li><br/>
<li class="p"> Want to make useful, interactive visualizations </li>

        </ul>

      </div>
<p class="it">Si alguna de esas cosas le es desconocida o poco clara, no tema. Es posible que quieran pasar más tiempo con el capítulo 3, que cubre lo que realmente necesita saber antes de sumergirse en D3.</p>

<p class="p" id="if_any_of_those">If any of those things are unknown or unclear, don’t fear. You might just want to spend more time with <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch03.html" title="Chapter 3. Technology Fundamentals">Chapter 3</a>, which covers what you really need to know before diving into D3.</p>

    </div>

    <div class="sect1" data-original-filename="1_intro.asciidoc" id="_what_this_book_is_not">

      <div class="titlepage">

        <div>

          <h2 class="title">What This Book Is Not</h2>

        </div>

      </div>
<p class="it">Dicho esto, este definitivamente no es un libro de texto de ciencias de la computación, y no se pretende enseñar las complejidades de cualquier tecnología web (HTML, CSS, JavaScript, SVG) en profundidad.</p>

<p class="p" id="that_said_this">That said, this is definitely not a computer science textbook, and it is not intended to teach the intricacies of any one web technology (HTML, CSS, JavaScript, SVG) in depth.</p>


<p class="it">En ese espíritu, que podría pasar por alto algunos puntos técnicos, simplificando enormemente importantes conceptos fundamentales de la informática de una manera que hará que los ingenieros de software retrocedan. Eso está bien, porque estoy escribiendo para artistas y diseñadores, no ingenieros. Vamos a cubrir lo básico, y luego se puede bucear en las piezas más complejas, una vez que se sienta cómodo.</p>

<p class="p" id="in_that_spirit">In that spirit, I might gloss over some technical points, grossly oversimplifying important concepts fundamental to computer science in ways that will make true software engineers recoil. That’s fine, because I’m writing for artists and designers here, not engineers. We’ll cover the basics, and then you can dive into the more complex pieces once you’re comfortable.</p>

<p class="it">Deliberadamente no referiré a todos los enfoques posibles para un problema dado, sino que suelo presentar lo que siento es la solución más simple, o, si no es la más simple, por lo menos la más comprensible.</p>

<p class="p" id="i_will_delibera">I will deliberately <span class="emphasis"><em>not</em></span> address every possible approach to a given problem, but will typically present what I feel is the simplest solution, or, if not the simplest, then the most understandable.</p>

<p class="it">Mi objetivo es enseñar los conceptos y métodos de D3 fundamentales. Como tal, este libro no está decididamente organizado en torno a proyectos de ejemplo específicos. Los datos de todos los usuarios y las necesidades de diseño serán diferentes. Es hasta usted para integrar estos conceptos en la forma que mejor se adapte a su proyecto particular.</p>

<p class="p" id="my_goal_is_to_t">My goal is to teach you the fundamental concepts and methods of D3. As such, this book is decidedly <span class="emphasis"><em>not</em></span> organized around specific example projects. Everyone’s data and design needs will be different. It’s up to you to integrate these concepts in the way best suited to your particular project.</p>

    </div>

    <div class="sect1" data-original-filename="1_intro.asciidoc" id="_using_sample_code">

      <div class="titlepage">

        <div>

          <h2 class="title">Using Sample Code</h2>

        </div>

      </div>
<p class="it">Si usted es un genio loco, entonces es probable que pueda aprender a utilizar D3 sin tener que mirar en los archivos de código de ejemplo, en cuyo caso se puede omitir el resto de esta sección.</p>
      
<p class="p" id="if_you_are_a_ma">If you are a mad genius, then you can probably learn to use D3 without ever looking at any sample code files, in which case you can skip the rest of this section.<a id="id483824" class="indexterm" href=""></a></p>

<p class="it">Si todavía estás conmigo, sos probablemente aún muy brillante, pero no loco, en cuyo caso debe usar este libro acompañado con el conjunto completo de ejemplos de código en la mano. Antes de ir más lejos, por favor descargue los archivos de muestra de GitHub.</p>

<p class="p" id="if_youre_still">If you’re still with me, you are probably still very bright but not mad, in which case you should undertake this book with the full set of accompanying code samples in hand. Before you go any further, please download the sample files from <a class="ulink" href="http://bit.ly/V25Xw6" target="_top">GitHub</a>.</p>

<p class="it">La gente normal va a querer hacer clic en el enlace postal para descargar un archivo ZIP comprimido con todos los archivos. El Hardcore Geeksters va a querer clonar el repositorio usando Git. Si esta última frase suena como un galimatías total, por favor utilice la primera opción.</p>

<p class="p" id="normal_people_w">Normal people will want to click the ZIP link to download a compressed ZIP archive with all the files. Hardcore geeksters will want to clone the repository using Git. If that last sentence sounds like total gibberish, please use the first option.</p>

<p class="it">Dentro de la descarga, se dará cuenta de que hay una carpeta para cada capítulo que tiene el código para ir con ella:</p>

<p class="p" id="within_the_down">Within the download, you’ll notice there is a folder for each chapter that has code to go with it:</p>

<pre class="screen" id="chapter__chap">
chapter_04
chapter_05
chapter_06
chapter_07
chapter_08

…</pre>
<p class="it">Los archivos están organizados por capítulo, por lo que en el capítulo 9, cuando me refiero a 01_bar_chart.html, sabe que puede encontrar ese archivo en la ubicación correspondiente: d3-libro / chapter_9 / 01_bar_chart.html.</p>

<p class="p" id="files_are_organ">Files are organized by chapter, so in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch09.html" title="Chapter 9. Updates, Transitions, and Motion">Chapter 9</a> when I reference <span class="emphasis"><em>01_bar_chart.html</em></span>, know that you can find that file in the corresponding location: <span class="emphasis"><em>d3-book/chapter_9/01_bar_chart.html</em></span>.</p>

<p class="it">Usted es bienvenido a copiar, adaptar, modificar y volver a utilizar el código de ejemplo en estos tutoriales para cualquier propósito no comercial.</p>

<p class="p" id="you_are_welcome">You are welcome to copy, adapt, modify, and reuse the example code in these tutorials for any noncommercial purpose.</p>

    </div>

    <div class="sect1" data-original-filename="1_intro.asciidoc" id="_thank_you">

      <div class="titlepage">

        <div>

          <h2 class="title">Thank You</h2>

        </div>

      </div>
<p class="it">Por último, este libro ha sido cosido a mano, cuidadosamente escrito, y pedagógicamente puesto a punto para lograr un máximo efecto. Gracias por leerlo. Espero que aprenda mucho, e incluso tenga un poco de diversión en el camino.</p>

<p class="p" id="finally_this_b">Finally, this book has been handcrafted, carefully written, and pedagogically fine-tuned for maximum effect. Thank you for reading it. I hope you learn a great deal, and even have some fun along the way.</p>

    </div>

  </div>

    </div>
  </div>
</template>
<style>
ul {
  list-style-type: none;
  padding: 0;
}

.block {
                          border-radius: 4px;
                          overflow: hidden;
                          box-shadow: 0 9px 9px rgba(0, 0, 0, 0.9);
                          display: block;
                          min-height: 70%;
                          font-family: Verdana;
                          max-width: 1100px;
                          background-color: #E8EDEE;
                          margin: auto;
                          margin-top: auto;
                          margin-right: auto;
                          margin-bottom: auto;
                          margin-left: auto;
                          white-space: pre-wrap;
                          border: none;
                          box-sizing: border-box;
                          color: #2D0D0D;
                          line-height: 1.1;
                          padding: 4.7em;

}
                .programlisting {
                          border-radius: 2px;
                          overflow: hidden;
                          box-shadow: 0 9px 9px rgba(0, 0, 0, 0.9);
                          display: block;
                          min-height: 100%;
                          font-family: courrier;
                          max-width: 1000px;
                          background-color: #547B83;
                          margin: auto;
                          margin-top: auto;
                          margin-right: auto;
                          margin-bottom: auto;
                          margin-left: auto;
                          white-space: pre-wrap;
                          border: none;
                          box-sizing: border-box;
                          font-size: 18px;
                          color: #592C2C;
                          line-height: 1.1;
                          padding: 4.7em;
                          text-align: left;
                          font-size: 25px;
}

                .home {
                        margin: 1.5em 0;
                        
                    }

                    h1 {
                        color: #867452;
                        font-size: 60px;
                    }

                    h2 {
                        color: #867452;
                        font-size: 40px;
                    }
                        h3 {
                        color: #867452;
                        font-size: 30px;
                    }
                   
                   h4 {
                        color: #867452;
                        font-size: 25px;
                    }


                    .it {
                        color: brown;
                        font-size: 24px;
                        font-style: italic;
                        letter-spacing: 0.04em;
                        text-align: justify;
                    }
                    .p {
                        color: #75AFAD;
                        font-size: 24px;
                        font-style: italic;
                        letter-spacing: 0.04em;
                        text-align: justify;
                    }
                    .fig {
                        color: #3A5756;
                        font-size: 20px;
                        letter-spacing: 0.04em;
                        text-align: center;
                    }

                    pre {display: block;
                    font-family: monospace;
                    white-space: pre;
                    margin: 1em 0;
                    font-size: 16px
                    }
                    
                    code strong
                    {color:#000;
                        background:#F5FD11;
                        padding:1px;
                        font-weight:normal;
                    }

                    .interno {
                    font-family: verdana;
                    font-style: italic;
                    color: #395C73;
                    font-size: 24px;    
                    }

a {
  color: #42b983;
}
</style>