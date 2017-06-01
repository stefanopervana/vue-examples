<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    
    <div class="block">
    <div  data-original-filename="3_tech_fundamentals.asciidoc345094" id="_the_web98">

    <div class="titlepage">

         <h1 class="title">Chapter 2. Introducing D3</h1>

  </div>

<p class="it">D3-también conocida como D-3 o d3.js es una biblioteca JavaScript para crear visualizaciones de datos.</p>

<p class="p" id="dalso_referre">D3—also referred to as D<sup>3</sup> or d3.js—is a JavaScript library for creating data visualizations. But that kind of undersells it.<a id="id483913" class="indexterm" href=""></a></p>

<p class="it">La abreviatura D3 hace referencia al nombre completo de la herramienta, los documentos basados en datos. Los datos son aportados por usted, y los documentos son documentos basados en la web, es decir, cualquier cosa que se puede representar en un navegador web, como HTML y SVG. D3 hace la conducción, en el sentido de que conecta los datos con los documentos.</p>

<p class="p" id="the_abbreviatio" >The abbreviation D3 references the tool’s full name, <span class="emphasis"><em>Data-Driven Documents</em></span>. The <span class="emphasis"><em>data</em></span> is provided by you, and the <span class="emphasis"><em>documents</em></span> are web-based documents, meaning anything that can be rendered by a web browser, such as HTML and SVG. D3 does the <span class="emphasis"><em>driving</em></span>, in the sense that it connects the data to the documents.<a id="id483940" class="indexterm" href=""></a><a id="id483948" class="indexterm" href=""></a></p>

<p class="it">Por supuesto, el nombre también funciona como una alusión inteligente a la red de las tecnologías subyacentes de la herramienta en sí misma: ". La Web" la W3, o World Wide Web, o, en la actualidad, sólo "la Web".</p>

<p class="p" id="of_course_the_">Of course, the name also functions as a clever allusion to the network of technologies underlying the tool itself: the W3, or World Wide Web, or, today, simply “the Web”.</p>

<p class="it">El principal autor del D3 es el brillante Mike Bostock, aunque hay algunos otros colaboradores dedicados. El proyecto es completamente de código abierto y está disponible libremente en GitHub.</p>

<p class="p" id="ds_primary_au">D3’s primary author is the brilliant <a class="ulink" href="http://bost.ocks.org/mike/" target="_top">Mike Bostock</a>, although there are a few other dedicated contributors. The project is entirely open source and freely available on<a id="id483971" class="indexterm" href=""></a> <a class="ulink" href="https://github.com/mbostock/d3/" target="_top">GitHub</a>.</p>

<p class="it">D3 es liberado bajo una licencia BSD, por lo que puede usar, modificar y adaptar el código para uso no comercial o comercial, sin costo alguno.</p>


<p class="p" id="d_is_released_">D3 is released under a BSD license, so you may use, modify, and adapt the code for noncommercial or commercial use at no cost.</p>

<p class="it">Fundamentalmente, D3 es una elegante pieza de software que facilita la generación y manipulación de documentos web con datos. Esto se hace mediante:</p>


<p class="p" id="fundamentally_">Fundamentally, D3 is an elegant piece of software that facilitates<a id="id484016" class="indexterm" href=""></a> generation and manipulation of web documents with data. It does this by:</p>

    <div class="itemizedlist" id="loading_data_in_id1">

      <ul class="itemizedlist">
 <li class="it">Carga de datos en la memoria del navegador</li>
        <li class="p"> <span class="emphasis"><em>Loading</em></span> data into the browser’s memory </li>
   
<br/><li class="it">Uniendo los datos de los elementos dentro del documento, creandose tantos nuevos elementos como sea necesario</li>
    <br/>
        <li class="p"> <span class="emphasis"><em>Binding</em></span> data to elements within the document, creating new elements as needed </li>
     <li class="it">La transformación de estos elementos mediante la interpretación de dato consolidado de cada elemento estableciendo  en consecuencia sus propiedades visuales</li>
    <br/>
        <li class="p"> <span class="emphasis"><em>Transforming</em></span> those elements by interpreting each element’s bound datum and setting its visual properties accordingly </li>
    <li class="it">La transición entre los elementos de los estados en respuesta al input del usuario</li>
        <li class="p"> <span class="emphasis"><em>Transitioning</em></span> elements between states in response to user input </li>
   
      </ul>

    </div>

    <p class="it">La etapa de transformación es más importante, ya que es donde ocurre la asignación. D3 proporciona una estructura para la aplicación de estas transformaciones, pero, como veremos, se definen las reglas de asignación. En que caso los valores más grandes corresponden a las barras más altas o círculos brillantes? Los grupos se pueden ordenar en el eje<code class="literal">x</code>por la edad o categoría? Que paleta de colores se utiliza para llenar los países en su mapa del mundo? Todas las decisiones de diseño visual son de usted. Usted proporciona el concepto, al diseñar las reglas, y D3 lo ejecuta, sin que le diga qué hacer. (Sí, es lo opuesto al agresivo "Asistente para gráficos" de Excel).</p>
    

<p class="p" id="the_transformat">The <span class="emphasis"><em>transformation</em></span> step is most important, as this is where the <span class="emphasis"><em>mapping</em></span> happens. D3 provides a structure for applying these transformations, but, as we’ll see, you define the mapping rules. Should larger values make taller bars or brighter circles? Will clusters be sorted on the x-axis by age or category? What color palette is used to fill in countries on your world map? All of the visual design decisions are up to you. You provide the concept, you craft the rules, and D3 executes it—without telling you what to do. (Yes, it’s like the opposite of Excel’s pushy “Chart Wizard.”)<a id="id484092" class="indexterm" href=""></a><a id="id484099" class="indexterm" href=""></a></p>


<p class="p" id="here_is_a_list_">Here is a list of things D3 does not do:</p>

<p class="it">Está es una lista de cosas que D3 no hace:</p>
    

    <div class="itemizedlist" id="d_doesnt_gene_id1">

      <ul class="itemizedlist">
<li class="it">D3 no genera visualizaciones predefinidas o "enlatadas" para usted. Esto es a propósito. D3 está destinado principalmente para el trabajo de la visualización de motivos, en lugar de las visualizaciones de exploración. Las herramientas de exploración ayudan a descubrir en los datos patrones con sentido y significado. Estas son herramientas como <a class="ulink" href="http://bit.ly/13KrhFH" target="_top">Tableau</a> and <a class="ulink" href="http://ggplot2.org/" target="_top">ggplot2</a>, que le ayudan a generar rápidamente múltiples puntos de vista sobre el mismo conjunto de datos. Eso es un paso esencial, pero diferente a la generación de una presentación explicativa de los datos, una vista de los datos que pone de relieve lo que ya has descubierto. Vistas explicativas que están más restringidas y limitadas, pero también se concentraron, y diseñaron para comunicar únicamente los puntos importantes. D3 se destaca en esta última etapa, pero no es ideal para los primeros. (Para obtener ideas sobre otras herramientas, consulte la sección "Alternativas" más adelante en este capítulo).</li>
        
<li class="p"> D3 doesn’t generate predefined or “canned” visualizations for you. This is on purpose. D3 is intended primarily for <span class="emphasis"><em>explanatory</em></span> visualization work, as opposed to <span class="emphasis"><em>exploratory</em></span> visualizations. Exploratory tools help you discover significant, meaningful patterns in data. These are tools like <a class="ulink" href="http://bit.ly/13KrhFH" target="_top">Tableau</a> and <a class="ulink" href="http://ggplot2.org/" target="_top">ggplot2</a>, which help you quickly generate multiple views on the same data set. That’s an essential step, but different from generating an <span class="emphasis"><em>explanatory</em></span> presentation of the data, a view of the data that highlights what you’ve already discovered. Explanatory views are more constrained and limited, but also focused, and designed to communicate only the important points. D3 excels at this latter step, but is not ideal for the former. (For ideas on other tools, see the section <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch02.html#alternatives_2" title="Alternatives">“Alternatives”</a> later in this chapter.)<a id="id484160" class="indexterm" href=""></a><a id="id484167" class="indexterm" href=""></a> </li>
        <br/>

<br/>
<li class="it">D3 ni siquiera trata de apoyar a los navegadores antiguos. Esto ayuda a mantener la base de código D3 limpia y libre de hacks para apoyar las versiones antiguas de Internet Explorer, por ejemplo. La filosofía es crear herramientas más convincentes y negarse a apoyar a los navegadores antiguos, animamos a más personas para actualizar (en lugar de impedir el proceso, requiriendonos por lo tanto a nosotros el eguir apoyando a los navegadores, y así sucesivamente continuar el círculo vicioso). D3 nos quiere hacer avanzar.</li>

<li class="p"> D3 doesn’t even try to support older browsers. This helps keep the D3 codebase clean and free of hacks to support old versions of Internet Explorer, for example. The philosophy is that by creating more compelling tools and refusing to support older browsers, we encourage more people to upgrade (rather than forestall the process, thereby requiring us to continue to support those browsers, and so on—a vicious cycle). D3 wants us to move forward.<a id="id484184" class="indexterm" href=""></a><a id="id484191" class="indexterm" href=""></a> </li>
        <br/>

<br/>
<li class="it">La funcionalidad central de D3 no maneja los mosaicos de bitsmaps, tales como los proporcionados por Google Maps o Cloudmade. D3 es bueno con cualquier clase de datos que tenga imágenes vectoriales SVG-o-GeoJSON pero no fue pensado originalmente para trabajar con bitsmap tradicionales. (Las imágenes de bitsmaps se componen de píxeles, por lo que cambiar su tamaño a más grande o más pequeño es difícil sin una pérdida de calidad. Las imágenes vectoriales se definen por puntos, líneas y curvas- ecuaciones matemáticas, de verdad, y se pueden escalar hacia arriba o hacia abajo sin una pérdida en calidad.) Esto está empezando a cambiar, con la introducción de la d3.geo.tile plug-in. Antes de este plug-in, geomapping con D3 significaba bien va todo-SVG y evitar las baldosas o utilizando D3 para crear efectos visuales SVG en la parte superior de una capa base de mosaicos de mapas (que sería administrado por otra biblioteca, como prospecto o Polymaps-ver la sección "Alternativas" más adelante en este capítulo). Esta cuestión de cómo integrar las baldosas de mapa de bits y gráficos vectoriales aparece mucho en la comunidad D3. Al día de hoy, no hay una respuesta super sencilla y perfecta, pero creo que se puede esperar ver una gran cantidad de trabajo realizado en esta área y, posiblemente, los nuevos métodos de baldosas de manipulación integrados en el núcleo D3 en algún momento en el futuro.</li>
        
<li class="p"> D3’s core functionality doesn’t handle bitmap map tiles, such as those provided by Google Maps or Cloudmade. D3 is great with anything vector—SVG images or GeoJSON data—but wasn’t originally intended to work with traditional map tiles. (<span class="emphasis"><em>Bitmap</em></span> images are made up of pixels, so resizing them larger or smaller is difficult without a loss in quality. <span class="emphasis"><em>Vector</em></span> images are defined by points, lines, and curves—mathematical equations, really—and can be scaled up or down without a loss in quality.) This is starting to change, with the introduction of the <a class="ulink" href="http://bit.ly/W8L18u" target="_top">d3.geo.tile plug-in</a>. Prior to this plug-in, geomapping with D3 meant either going all-SVG and avoiding tiles or using D3 to create SVG visuals <span class="emphasis"><em>on top of</em></span> a base layer of map tiles (which would be managed by another library, like Leaflet or Polymaps—see the section <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch02.html#alternatives_2" title="Alternatives">“Alternatives”</a> later in this chapter). This question of how to integrate bitmap tiles and vector graphics comes up a lot in the D3 community. As of today, there is no super-simple and perfect answer, but I think you can expect to see lots of work done in this area, and possibly the new tile-handling methods integrated into the D3 core at some point in the future.<a id="id484239" class="indexterm" href=""></a><a id="id484246" class="indexterm" href=""></a><a id="id484254" class="indexterm" href=""></a><a id="id484259" class="indexterm" href=""></a><a id="id484264" class="indexterm" href=""></a><a id="id484269" class="indexterm" href=""></a><a id="id484274" class="indexterm" href=""></a> </li>
        <br/>

<li class="it">D3 no oculta sus datos originales. Dado que el código D3 se ejecuta en el lado del cliente (es decir, en el navegador web del usuario, en lugar del servidor web), los datos que desea visualizar deben ser enviados al cliente. Si los datos no se pueden compartir, a continuación, no utilice D3. Las alternativas incluyen el uso de herramientas propietarias (como Flash) o previa a la representación como visualizaciones de imágenes estáticas y el envío al navegador. (Si usted no está interesado en compartir sus datos, sin embargo, ¿para qué molestarse en visualizarlo? El propósito de la visualización es comunicar los datos, por lo que puede dormir mejor por la noche por la elección de la apertura y la transparencia, en lugar de tener pesadillas acerca de los data thieves)(ver http://www.datathief.org).</li>
<br/>

<li class="p"> D3 doesn’t hide your original data. Because D3 code is executed on the client side (meaning, in the user’s web browser, as opposed to on the web server), the data you want visualized must be sent to the client. If your data can’t be shared, then don’t use D3. Alternatives include using proprietary tools (like Flash) or prerendering visualizations as static images and sending those to the browser. (If you’re not interested in sharing your data, though, why would you bother visualizing it? The purpose of visualization is to communicate the data, so you might sleep better at night by choosing openness and transparency, rather than having nightmares about <a class="ulink" href="http://www.datathief.org/" target="_top">data thieves</a>.)<a id="id484305" class="indexterm" href=""></a><a id="id484310" class="indexterm" href=""></a></li>
        <br/>

      </ul>

    </div>

    <p class="it">Aprender a usar D3 es simplemente un proceso de aprendizaje de la sintaxis utilizada para decirle cómo desea que cargue y enlase los datos, y transforme y comunique los elementos.</p>


<p class="p" id="learning_to_use">Learning to use D3 is simply a process of learning the syntax used to tell it how you want it to load and bind data, and transform and transition elements.</p>

<div class="" data-original-filename="2_introducing_d3.asciidoc" id="_origins_and_context">

<p class="it">Los primeros navegadores Web representaban páginas estáticas; la interactividad se limitaba a hacer clic en enlaces. En 1996, Netscape introduce el primer navegador con JavaScript, un nuevo lenguaje de programación que puede ser interpretado por el navegador mientras que la página se está visualizando.</p>

<p class="p" id="the_first_web_b">The first web browsers rendered static pages; interactivity was limited to clicking links. In 1996, Netscape introduced the first browser with JavaScript, a new scripting language that could be interpreted <span class="emphasis"><em>by the browser while the page was being viewed</em></span>.<a id="id484335" class="indexterm" href=""></a></p>

<p class="it">Esto no suena tan innovador como resultó ser, pero esto permitió a los <span class="emphasis"><em>web browsers</em></span> a partir de la navegación meramente pasiva evolucionar a los marcos dinámicos para las experiencias interactivas en la red. Este cambio en última instancia habilita cada interacción intrapage que tenemos en la web hoy en día. Sin JavaScript, D3 no existiría, y las visualizaciones de datos basadas en la Web se limitarian a GIF pre-renderisados, no interactivos. (Yuck. Gracias, Netscape!)</p>

<p class="p" id="this_doesnt_so">This doesn’t sound as groundbreaking as it turned out to be, but this enabled web browsers to evolve from merely passive <span class="emphasis"><em>browsers</em></span> to dynamic frames for interactive, networked experiences. This shift ultimately enabled every intrapage interaction we have on the Web today. Without JavaScript, D3 would never exist, and web-based data visualizations would be limited to prerendered, noninteractive GIFs. (Yuck. Thank you, Netscape!)<a id="id484355" class="indexterm" href=""></a><a id="id484362" class="indexterm" href=""></a></p>

<p class="it">Saltamos a 2005, cuando Jeffrey Heer, Stuart Card, y James Landay introdujeron <a class="ulink" href="http://prefuse.org/" target="_top">prefuse</a>, un conjunto de herramientas para llevar la visualización de datos a la Web. prefuse (escrito con todas las letras en minúscula) fue escrito en Java, un lenguaje compilado, con programas que podrían funcionar en los navegadores web a través de un plug-in de Java. (Tenga en cuenta que Java es un lenguaje de programación completamente diferente de JavaScript, a pesar de sus nombres similares.)</p>

<p class="p" id="jump_ahead_to_">Jump ahead to 2005, when Jeffrey Heer, Stuart Card, and James Landay introduced <a class="ulink" href="http://prefuse.org/" target="_top">prefuse</a>, a toolkit for bringing data visualization to the Web. prefuse (spelled with all lowercase letters) was written in Java, a compiled language, with programs that could run in web browsers via a Java plug-in. (Note that <span class="emphasis"><em>Java</em></span> is a completely different programming language than <span class="emphasis"><em>JavaScript</em></span>, despite their similar names.)<a id="id484388" class="indexterm" href=""></a><a id="id484393" class="indexterm" href=""></a><a id="id484398" class="indexterm" href=""></a><a id="id484404" class="indexterm" href=""></a><a id="id484409" class="indexterm" href=""></a></p>
  
<p class="it">prefuse era una aplicación pionera en hacer la visualización basada en la web accesible a los programadores menos-que-expertos. Hasta que llegó prefuse, cualquier datavis en la Web fue en gran medida un asunto de costumizado.</p>

<p class="p" id="prefuse_was_a_b">prefuse was a breakthrough application—the first to make web-based visualization accessible to less-than-expert programmers. Until prefuse came along, any datavis on the Web was very much a custom affair.</p>
  
<p class="it">Dos años más tarde, Jeff Heer introdujo <a class="ulink" href="http://flare.prefuse.org/" target="_top">Flare</a>, un conjunto de herramientas similares, pero escrito en ActionScript, por lo que sus visualizaciones podian ser vistas en la web a través del Adobe’s Flash Player. Flare, como prefuse, se basó en un navegador plug-in. Flare fue una gran mejora, pero a medida que los navegadores web continuaron evolucionando, estaba claro que las visualizaciones podian ser creadas con la tecnología  nativa del navegador, sin necesidad de plug-ins.</p>

<p class="p" id="two_years_later">Two years later, Jeff Heer introduced <a class="ulink" href="http://flare.prefuse.org/" target="_top">Flare</a>, a similar toolkit, but written in ActionScript, so its visualizations could be viewed on the Web through Adobe’s Flash Player. Flare, like prefuse, relied on a browser plug-in. Flare was a huge improvement, but as web browsers continued to evolve, it was clear that visualizations could be created with native browser technology, no plug-ins required.<a id="id484439" class="indexterm" href=""></a><a id="id484445" class="indexterm" href=""></a></p>


<p class="it">Para el año 2009, Jeff Heer se había trasladado a Stanford, donde estaba aconsejando a un estudiante graduado llamado Michael Bostock. Juntos, en el Grupo Vis de Stanford, crearon <a class="ulink" href="http://mbostock.github.com/protovis/" target="_top">Protovis</a>, un conjunto de herramientas de visualización basado en JavaScript que se basó exclusivamente en tecnologías de navegador nativo. (Si ha utilizado Protovis, asegúrese de hacer referencia a la introducción de Mike a D3 para los usuarios Protovis.)</p>

<p class="p" id="by__jeff_h">By 2009, Jeff Heer had moved to Stanford, where he was advising a graduate student named Michael Bostock. Together, in Stanford’s Vis Group, they created <a class="ulink" href="http://mbostock.github.com/protovis/" target="_top">Protovis</a>, a JavaScript-based visualization toolkit that relied <span class="keep-together">exclusively</span> on native browser technologies. (If you have used Protovis, be sure to reference Mike’s <a class="ulink" href="http://bit.ly/XxebvX" target="_top">introduction to D3 for Protovis users</a>.)<a id="id484474" class="indexterm" href=""></a><a id="id484479" class="indexterm" href=""></a></p>

  
<p class="it">Protovis hizo generar visualizaciones sencillas, incluso para usuarios sin experiencia previa en programación. Sin embargo, para lograr este objetivo, se creó una capa de representación abstracta. El diseñador podría abordar esta capa utilizando la sintaxis Protovis, pero no era accesible a través de métodos estándar, por lo que era de difícil depuración.</p>

<p class="p" id="protovis_made_g">Protovis made generating visualizations simple, even for users without prior programming experience. Yet to achieve this, it created an abstract representation layer. The designer could address this layer using Protovis syntax, but it wasn’t accessible through standard methods, so debugging was difficult.</p>

<p class="it">En 2011, Mike Bostock, Vadim Ogievetsky, y Jeff Heer anunciaron oficialmente D3, la próxima evolución en las herramientas de visualización web. A diferencia de Protovis, D3 opera directamente en el documento. Esto significa una  depuración más fácil, fáciles tambien la experimentación, y las posibilidades visuales. La única desventaja de este enfoque es una curva de aprendizaje potencialmente más pronunciada, pero este libro hará que sea lo menos doloroso posible. Además, todas las habilidades que adquieren mientras aprenden sobre D3 le seran útiles incluso más allá del ámbito de la datavis.</p> 

<p class="p" id="in__mike_b">In 2011, Mike Bostock, Vadim Ogievetsky, and Jeff Heer <a class="ulink" href="http://vis.stanford.edu/papers/d3" target="_top">officially announced D3</a>, the next evolution in web visualization tools. Unlike Protovis, D3 operates directly on the web document itself. This means easier debugging, easier experimentation, and more visual possibilities. The only downside to this approach is a potentially steeper learning curve, but this book will make that as painless as possible. Plus, all the skills you gain while learning about D3 will prove useful even beyond the realm of datavis.<a id="id484507" class="indexterm" href=""></a><a id="id484512" class="indexterm" href=""></a></p>
   
<p class="it">Si está familiarizado con cualquiera de estas herramientas innovadoras, apreciará que D3 desciende de un linaje prestigioso. Y si usted tiene algún interés en la filosofía que subyace en el elegante diseño técnico de D3, le recomiendo ver el <a class="ulink" href="http://vis.stanford.edu/files/2011-D3-InfoVis.pdf" target="_top">InfoVis paper</a> de Mike, Vadim, y Jeff, que articula claramente la necesidades de este tipo de herramienta. En el documento se encapsulan años de valor de aprendizaje y las reflexiones realizadas durante el desarrollo de herramientas de visualización. Podes verlo al final de este capítulo)</p>

<p class="p" id="if_youre_famil_id1">If you’re familiar with any of these groundbreaking tools, you’ll appreciate that D3 descends from a prestigious lineage. And if you have any interest in the philosophy underlying D3’s elegant technical design, I highly recommend Mike, Vadim, and Jeff’s <a class="ulink" href="http://vis.stanford.edu/files/2011-D3-InfoVis.pdf" target="_top">InfoVis paper</a>, which clearly articulates the need for this kind of tool. The paper encapsulates years’ worth of learning and insights made while developing visualization tools.<a id="id484536" class="indexterm" href=""></a></p>

</div>

<p class="it">D3 podría no ser perfecto para cada proyecto. A veces sólo necesita un gráfico rápido y no tiene tiempo para escribir codigo desde cero. O puede que tenga que soportar los navegadores más antiguos y no se puede confiar en las recientes tecnologías como SVG.</p>

<p class="p" id="d_might_not_be">D3 might not be perfect for every project. Sometimes you just need a quick chart and you don’t have time to code it from scratch. Or you might need to support older browsers and can’t rely on recent technologies like SVG.</p>

<p class="it">Para esas situaciones, es bueno saber qué otras herramientas están ahí fuera. He aquí una breve lista  no exhaustiva de alternativas a D3, las cuales utilizan tecnologías web estándar (en su mayoría JavaScript) para descargar y usar en forma gratuita.</p>  

<p class="p" id="for_those_situa">For those situations, it’s good to know what other tools are out there. Here is a brief, noncomprehensive list of D3 alternatives, all of which use web-standard technologies (mostly JavaScript) and are free to download and use.</p>

<br/>



<h3>Easy Charts</h3>


<div class="variablelist" id="datawrapper_a_b_y">


<dl class="variablelist">

<dt><span class="term"> <a class="ulink" href="http://datawrapper.de/" target="_top">DataWrapper</a> </span></dt>

<dd class="it">Un servicio web hermoso que le permite cargar sus datos y generar rápidamente una tabla que se puede volver a publicar en otro lugar o incrustar en su sitio. Este servicio fue pensado originalmente para los periodistas, pero es útil para todo el mundo. DataWrapper muestra gráficos interactivos en los navegadores actuales e imágenes estáticas para los antiguos. (Genial!) También puede descargar todo el código y ejecutarlo en su propio servidor en lugar de utilizar el suyo.</dd>

<dd class="p"> A beautiful web service that lets you upload your data and quickly generate a chart that you can republish elsewhere or embed on your site. This service was originally intended for journalists, but it is helpful for everyone. DataWrapper displays interactive charts in current browsers and static images for old ones. (Brilliant!) You can also download all the code and run it on your own server instead of using theirs.<a id="id484612" class="indexterm" href=""></a> </dd>
<br/>

<dt><span class="term"> <a class="ulink" href="http://www.flotcharts.org/" target="_top">Flot</a> </span></dt>

<dd class="it">Un recorte de la biblioteca de jQuery que utiliza el elemento HTML canvas y es compatible con los navegadores más antiguos, incluso todo lo transitado hasta Internet Explorer 6. Es compatible con las formas visuales básicas (líneas, puntos, barras, áreas), pero es fácil de usar.</dd>

<dd class="p"> A plotting library for jQuery that uses the HTML canvas element and supports older browsers, even all the way back to Internet Explorer 6. It supports limited visual forms (lines, points, bars, areas), but it is easy to use. </dd>
<br/>

<dt><span class="term"> <a class="ulink" href="https://developers.google.com/chart/" target="_top">Google Chart Tools</a> </span></dt>

<dd class="it">Después de haber evolucionado a partir de su anterior <a class="ulink" href="https://developers.google.com/chart/image/" target="_top">Image Charts API</a>, Las herramientas de gráficos de Google pueden ser usadas para generar varios tipos de gráficos estándar, con soporte para las versiones antiguas de IE.</dd>

<dd class="p"> Having evolved from their earlier <a class="ulink" href="https://developers.google.com/chart/image/" target="_top">Image Charts API</a>, Google’s Chart Tools can be used to generate several standard chart types, with support for old versions of IE. </dd>
<br/>
         
<dt><span class="term"> <a class="ulink" href="http://g.raphaeljs.com/" target="_top">gRaphaël</a> </span></dt>

<dd class="it">Una biblioteca de gráficos basada en Raphaël (véase más adelante en este capítulo) que soporta los navegadores más antiguos, incluyendo IE6. Cuenta con más flexibilidad visual que Flot, y algunos podrían decir, es más bonita.</dd>

<dd class="p"> A charting library based on Raphaël (see later in this chapter) that supports older browsers, including IE6. It has more visual flexibility than Flot, and—some might say—it is prettier. </dd>
<br/>

<dt><span class="term"> <a class="ulink" href="http://www.highcharts.com/" target="_top">Highcharts JS</a> </span></dt>

<dd class="it">Una Biblioteca de gráficos basada en JavaScript con varios temas prediseñados y tipos de gráficos. Utiliza SVG para los navegadores modernos y <a class="ulink" href="http://www.highcharts.com/documentation/compatibility" target="_top">cae nuevamente en VML</a> para las versiones antiguas de IE, incluyendo IE6 y versiones posteriores. La herramienta es gratuita sólo para uso no comercial.</dd>

<dd class="p"> A JavaScript-based charting library with several predesigned themes and chart types. It uses SVG for modern browsers and <a class="ulink" href="http://www.highcharts.com/documentation/compatibility" target="_top">falls back on VML</a> for old versions of IE, including IE6 and later. The tool is free only for noncommercial use. </dd>
<br/>

<dt><span class="term"> <a class="ulink" href="http://thejit.org/" target="_top">JavaScript InfoVis Toolkit</a> </span></dt>

<dd class="it">El JIT ofrece varios estilos predefinidos de visualización de datos. Incluye un montón de ejemplos, pero la documentación es bastante técnica. El conjunto de herramientas es ideal si te gusta uno de los estilos predefinidos, pero el apoyo del browser no es claro.</dd>

<dd class="p"> The JIT provides several preset visualization styles for your data. It includes lots of examples, but the documentation is pretty technical. The toolkit is great if you like one of the preset styles, but browser support is unclear. </dd>
<br/>

<dt><span class="term"> <a class="ulink" href="http://www.jqplot.com/" target="_top">jqPlot</a> </span></dt>

<dd class="it">Un plug-in para dibujar con jQuery. Esto es compatible con gráficos muy simples y es ideal si estas de acuerso con los estilos predefinidos. jqPlot es compatible con Internet Explorer 7 y versiones posteriores.</dd>
     
<dd class="p"> A plug-in for charting with jQuery. This supports very simple charts and is great if you are okay with the predefined styles. jqPlot supports IE7 and newer. </dd>
<br/>

<dt><span class="term"> <a class="ulink" href="http://omnipotent.net/jquery.sparkline/" target="_top">jQuery Sparklines</a> </span></dt>

<dd class="it">Un plug-in para sparklines generando, pequeños tipicos  bar, una línea o gráficos de áreas utilizadas en línea con el texto. Es compatible con la mayoría de los navegadores, incluso anteriores a IE6.</dd>

<dd class="p"> A jQuery plug-in for generating sparklines, typically small bar, line, or area charts used inline with text. Supports most browsers, even back to IE6. </dd>
<br/>

<dt><span class="term"> <a class="ulink" href="http://benpickles.github.com/peity/" target="_top">Peity</a> </span></dt>

<dd class="it">Un plug-in de jQuery para los gráficos de barras, de líneas y de sectores muy simples y muy pequeños que sólo es compatible con los navegadores más recientes. ¿He mencionado que esto hace sólo muy pequeñas visualizaciones? +10 Puntos ternura.</dd>

<dd class="p"> A jQuery plug-in for very simple and very <span class="emphasis"><em>tiny</em></span> bar, line, and pie charts that supports only recent browsers. Did I mention that this makes only very <span class="emphasis"><em>tiny</em></span> visualizations? +10 cuteness points. </dd>
<br/>

<dt><span class="term"> <a class="ulink" href="http://timeline.verite.co/" target="_top">Timeline.js</a> </span></dt>

<dd class="it">Una biblioteca específica para generar líneas de tiempo interactivas. No se requiere codificación; sólo tiene que utilizar el generador de código. No hay mucho espacio para la personalización, pero bueno, las líneas de tiempo son realmente difíciles de hacer bien. Timeline.js sólo es compatible con Internet Explorer 8 y versiones posteriores.</dd>

<dd class="p"> A library specifically for generating interactive timelines. No coding is required; just use the code generator. There is not much room for customization, but hey, timelines are really hard to do well. Timeline.js supports only IE8 and newer. </dd>
<br/>

<dt><span class="term"> <a class="ulink" href="http://yuilibrary.com/yui/docs/charts/" target="_top">YUI Charts</a> </span></dt>

<dd class="it">El módulo de la Biblioteca de Gráficos Yahoo! permite la creación de gráficos simples con el objeto de ser soportado por los navegadores de ancho.</dd>          

<dd class="p"> The Charts module for the Yahoo! User Interface Library enables creation of simple charts with a goal of wide browser support. </dd>

</dl>

</div>

<div class="sect2" id="_graph_visualizations">

<h3>Graph Visualizations</h3>

<p class="p" id="a_graph_is_ju">A “graph” is just data with a networked structure (for example, B is connected to A, and A is connected to C).<a id="id484804" class="indexterm" href=""></a></p>

<p class="it">Un "gráfico" es sólo datos con una estructura de red (por ejemplo, B está conectado a A, y A está conectado a C).</p>
      
<br/>

<div class="variablelist" id="arborjs_a_libr">

<dl class="variablelist">

<dt><span class="term"> <a class="ulink" href="http://arborjs.org/" target="_top">Arbor.js</a> </span></dt>

<dd class="it">Una biblioteca para la visualización gráfica usando jQuery. Incluso si nunca utiliza esto, usted debe comprobar la documentación de cómo se presenta como un gráfico, utilizando la herramienta en sí. (Es tan <span class="emphasis"><em>meta</em></span>.) Utiliza el canvas HTML, por lo que funciona sólo en IE9 o navegadores actuales, aunque algunas soluciones están disponibles.</dd>

<dd class="p"> A library for graph visualization using jQuery. Even if you never use this, you should check out how the documentation is presented as a graph, using the tool itself. (It’s so <span class="emphasis"><em>meta</em></span>.) It uses the HTML canvas, so it works only in IE9 or current browsers, although some workarounds are available. </dd>
<br/>

<dt><span class="term"> <a class="ulink" href="http://sigmajs.org/" target="_top">Sigma.js</a> </span></dt>

<dd class="it">Una biblioteca muy ligera para la visualización gráfica. Tienes que visitar este sitio web, mover el puntero del ratón sobre el gráfico de cabecera, y luego jugar con las demostraciones. Es hermoso y rápido, y también utiliza canvas.</dd>

<dd class="p"> A very lightweight library for graph visualization. You have to visit this website, move your mouse over the header graphic, and then play with the demos. Sigma.js is beautiful and fast, and it also uses canvas. </dd>

</dl>

 </div>

</div>

<div class="sect2" id="_geomapping">

<h3>Geomapping</h3>

<p class="p" id="i_distinguish_b">I distinguish between <span class="emphasis"><em>mapping</em></span> (all visualizations are maps) and <span class="emphasis"><em>geomapping</em></span> (visualizations that include geographic data, or geodata, such as traditional maps). D3 has a lot of geomapping functionality, but you should know about these other tools.<a id="id484868" class="indexterm" href=""></a></p>

<p class="it">Distingo entre el mapping  (todas las visualizaciones son mapas) y geomapping (visualizaciones que incluyen datos geográficos, o datos geográficos, tales como mapas tradicionales). D3 tiene una gran cantidad de funcionalidad geomapping, pero usted debe saber acerca de estas otras herramientas.</p>
     
<br/>

<div class="variablelist" id="kartograph_a_ja">


<dl class="variablelist">


<dt><span class="term"> <a class="ulink" href="http://kartograph.org/" target="_top">Kartograph</a> </span></dt>

<dd class="it">Un combo con JavaScript y Python precioso para el mapeo, totalmente basado en vectores de Gregor Aisch con demos. Por favor, ir a buscarlos ahora. Prometo que nunca has visto mapas en línea tan hermosos. Kartograph funciona con Internet Explorer 7 y versiones posteriores.</dd>

<dd class="p"> A JavaScript-and-Python combo for gorgeous, entirely vector-based mapping by Gregor Aisch with must-see demos. Please go look at them now. I promise you’ve never seen online maps this beautiful. Kartograph works with IE7 and newer. </dd>
<br/>

<dt><span class="term"> <a class="ulink" href="http://leaflet.cloudmade.com/" target="_top">Leaflet</a> </span></dt>

<dd class="it">Una biblioteca para los mapas, diseñados para la interacción fluida tanto en el escritorio como en los dispositivos móviles. Incluye un poco de apoyo para la visualización de capas de datos de SVG en la parte superior de las baldosas del mapa. (Ver demostración de Mike "Uso D3 con Folleto".) Leaflet funciona con IE6 (apenas) o Internet Explorer 7 (mejor!) Y por supuesto todos los navegadores actuales.</dd>
          <dd class="p"> A library for tiled maps, designed for smooth interaction on both desktop and mobile devices. It includes some support for displaying data layers of SVG on top of the map tiles. (See Mike’s demo <a class="ulink" href="http://bost.ocks.org/mike/leaflet/" target="_top">“Using D3 with Leaflet”</a>.) Leaflet works with IE6 (barely) or IE7 (better!) and of course all current browsers.</dd>
<br/>
        </dl>

      </div>

      <p class="p" id="of_the_map_tile"></p>

      <div class="variablelist" id="modest_maps_the">

        <dl class="variablelist">

          <dt><span class="term"> <a class="ulink" href="http://modestmaps.com/" target="_top">Modest Maps</a> </span></dt>
<dd class="it">El abuelo de tiled map, Modest Maps ha sido sucedido por Polymaps, pero a mucha gente todavía le encanta, ya que es ligero y funciona con las versiones antiguas de Internet Explorer y otros navegadores. Modest Maps ha sido adaptado para ActionScript, Processing, Python, PHP, Cinder, openFrameworks…yeah, básicamente todo. De momento, esto bajo "oldie, pero bueno".</dd>
          <dd class="p"> The granddaddy of tiled map libraries, Modest Maps has been succeeded by Polymaps, but lots of people still love it, as it is lightweight and works with old versions of IE and other browsers. Modest Maps has been adapted for ActionScript, Processing, Python, PHP, Cinder, openFrameworks…yeah, basically everything. File this under “oldie, but goodie.” </dd>
<br/>
          <dt><span class="term"> <a class="ulink" href="http://polymaps.org/" target="_top">Polymaps</a> </span></dt>
<dd class="it">Una biblioteca para la visualización de tiled maps, con capas de datos en la parte superior de las baldosas. Polymaps se basa en SVG y por lo tanto funciona mejor con los navegadores actuales.</dd>
          <dd class="p"> A library for displaying tiled maps, with layers of data on top of the tiles. Polymaps relies on SVG and thus works best with current browsers. </dd>
<br/>
        </dl>

      </div>

    </div>


    <h3>Almost from Scratch</h3>

      <p class="it">Estas herramientas, como D3, proporcionan métodos de dibujo de formas visuales, pero sin plantillas visuales pre diseñadas. Si usted disfruta de la libertad creativa de empezar desde cero, es posible disfrutar de esta herramienta.</p>
    <p class="p">These tools, like D3, provide methods of drawing visual forms, but without predesigned visual templates. If you enjoy the creative freedom of starting from scratch, you might enjoy these.</p>
  <br/>

    <div class="sect2" id="_almost_from_scratch">

      <div class="variablelist" id="processingjs_a">

        <dl class="variablelist">

<dt><span class="term"> <a class="ulink" href="http://processingjs.org/" target="_top">Processing.js</a> </span></dt>

<dd class="it">Una aplicación nativa de JavaScript procesamiento, el lenguaje de programación fantástica para artistas y diseñadores de nuevo en la programación. Procesamiento está escrito en Java, por lo que exportar esquemas de proceso para la Web tradicionalmente involucrados applets de Java torpe. Gracias a Processing.js, código de procesamiento regular puede ejecutarse de forma nativa en el navegador. Se hace uso de la lona, por lo que sólo los navegadores modernos son compatibles.</dd>

<dd class="p"> A native JavaScript implementation of <a class="ulink" href="http://processing.org/" target="_top">Processing</a>, the fantastic programming language for artists and designers new to programming. Processing is written in Java, so exporting Processing sketches to the Web traditionally involved clunky Java applets. Thanks to Processing.js, regular Processing code can run natively, in the browser. It renders using canvas, so only modern browsers are supported. </dd>
<br/>

<dt><span class="term"> <a class="ulink" href="http://paperjs.org/" target="_top">Paper.js</a> </span></dt>

<dd class="it">Un framework para la representación de gráficos vectoriales a la lona. Además, su sitio web es uno de los más bellos en la Internet, y sus demostraciones son increíbles. (Ve a jugar con ellos ahora.)</dd>

<dd class="p"> A framework for rendering vector graphics to canvas. Also, its website is one of the most beautiful on the Internet, and their demos are unbelievable. (Go play with them now.) </dd>
<br/>

<dt><span class="term"> <a class="ulink" href="http://raphaeljs.com/" target="_top">Raphaël</a> </span></dt>

<dd class="it">Otra biblioteca para dibujar gráficos vectoriales, populares debido a su sintaxis sencilla y soporte para navegadores antiguos.</dd>
          <dd class="p"> Another library for drawing vector graphics, popular due to its friendly syntax and support for older browsers. </dd>
<br/>
        </dl>

      </div>

    </div>

    <div class="sect2" id="_three_dimensional">
<p class="p" id="d_is_not_the_b">D3 is not the best at 3D, simply because web browsers are historically two-dimensional beasts. But with increased support for WebGL, there are now more opportunities for 3D web experiences.<a id="id485046" class="indexterm" href=""></a></p>    
<p class="it">D3 no es el mejor en 3D, simplemente porque los navegadores web son bestias históricamente bidimensionales. Pero con un mayor apoyo a WebGL, ahora hay más oportunidades para experiencias Web 3D.</p>
      <br/>
<br/>
      <div class="variablelist" id="philogl_a_webgl">

        <dl class="variablelist">

          <dt><span class="term"> <a class="ulink" href="http://www.senchalabs.org/philogl/" target="_top">PhiloGL</a> </span></dt>
<dd class="it">Un framework WebGL específico para la visualización en 3D.</dd>
          <dd class="p"> A WebGL framework specifically for 3D visualization. </dd>
<br/>
          <dt><span class="term"> <a class="ulink" href="http://mrdoob.github.com/three.js/" target="_top">Three.js</a> </span></dt>
<dd class="it">Una biblioteca para generar cualquier tipo de escena en 3D que se pueda imaginar, producido por el equipo de Artes de datos de Google. Se puede pasar todo el día explorando las demostraciones alucinantes en su sitio.</dd>
          <dd class="p"> A library for generating any sort of 3D scene you could imagine, produced by Google’s Data Arts team. You could spend all day exploring the mind-blowing demos on their site. </dd>

        </dl><br/>
        <h3>Tools Built with D3</h3>
        <dl class="variablelist">
<p class="it">Cuando se desea utilizar D3 sin tener que escribir ningún código D3, se puede elegir una de las muchas herramientas integradas en la parte superior de la D3!</p>        
<p>When you want to use D3 without actually writing any D3 code, you can choose one of the many tools built on top of D3!</p>
<br/>

<dt><span class="term"> <a class="ulink" href="http://square.github.io/crossfilter//" target="_top">Crossfilter</a> </span></dt>
<dd class="it">Una biblioteca para trabajar con conjuntos de datos grandes, multivariados, escrita principalmente por Mike Bostock. Esto es útil para tratar de exprimir su "Big Data" en un relativamente pequeño navegador web.</dd>
<dd class="p">A library for working with large, multivariate datasets, written primarily by Mike Bostock. This is useful for trying to squeeze your “big data” into a relatively small web browser.</dd>
<br/>
<dt><span class="term"> <a class="ulink" href="http://square.github.io/cubism/" target="_top">Cubism</a> </span></dt>
<dd class="it">Un plug-in D3 para la visualización de datos de series de tiempo, también escrito por Mike Bostock. (Uno de mis demos favoritos.)</dd>
<dd class="p">A D3 plug-in for visualizing time series data, also written by Mike Bostock. (One of my favorite demos.)</dd>
<br/>
<dt><span class="term"> <a class="ulink" href="https://dashku.com//" target="_top">Dashku</a> </span></dt>
<dd class="it">Una herramienta en línea para los data dashboards y widgets updated en tiempo real, por Paul Jensen.</dd>
<dd class="p">An online tool for data dashboards and widgets updated in real time, by Paul Jensen.</dd>
<br/>
<dt><span class="term"> <a class="ulink" href="http://dc-js.github.io/dc.js//" target="_top">dc.js</a> </span></dt>
<dd class="it">El "dc" es la abreviatura de la cartografía tridimensional, ya que esta biblioteca está optimizada para explorar grandes, multidimensionales datasets</dd>
<dd class="p">The “dc” is short for dimensional charting, as this library is optimized for exploring large, multidimensional datasets.</dd>
<br/>
<dt><span class="term"> <a class="ulink" href="http://nvd3.org/" target="_top">NVD3</a> </span></dt>

<dd class="it">Tablas reusables con D3. NVD3 ofrece gran cantidad de bellos ejemplos, con espacio para las personalizaciones visuales sin necesidad de código en la medida de D3 solo.</dd>
<dd class="p">Reusable charts with D3. NVD3 offers lots of beautiful examples, with room for visual customizations without requiring as much code as D3 alone.</dd>
<br/>
<dt><span class="term"> <a class="ulink" href="http://polychart.com/" target="_top">Polychart.js</a> </span></dt>

<dd class="it">Mas tablas reusables, con una amplia gama de tipos de gráficos disponibles. Polychart.js es libre solo para uso no comercial.</dd>
<dd class="p">More reusable charts, with a range of chart types available. Polychart.js is free only for noncommercial use.</dd>
<br/>

<dt><span class="term"> <a class="ulink" href="http://code.shutterstock.com/rickshaw/" target="_top">Rickshaw</a> </span></dt>
<dd class="it">Un juego de herramientas para la visualización de los datos de series de tiempo que también es muy personalizable.</dd>
<dd class="p">A toolkit for displaying time series data that is also very customizable.</dd>
<br/>
<dt><span class="term"> <a class="ulink" href="http://enjalot.com/" target="_top">Tributary</a> </span></dt>
<dd class="it">Una gran herramienta para experimentar con la codificación en directo utilizando D3, por Ian Johnson.</dd>
<dd class="p">A great tool for experimenting with live coding using D3, by Ian Johnson.</dd>

</dl>
      </div>

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