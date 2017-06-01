<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    
    <div class="block">
    <div class="" data-original-filename="3_tech_fundamentals.asciidoc345094" id="_the_web98">

    <div class="titlepage">

      <div>

    
         <h1 class="title">Chapter 3. Technology Fundamentals</h1>

      </div>

    </div>
  </div>
  <p class="it">La sólida familiaridad con los siguientes conceptos hará mucho menos frustrante su tiempo con D3 y mucho más gratificante. Considere esto un breve curso de actualización sobre la Web-Making 101.</p>
   <p class="p" id="if_youre_brand2">Solid familiarity with the following concepts will make your time with D3 a lot less frustrating and a lot more rewarding. Consider this a brief refresher course on Web-Making 101.</p>



      <div class="warning" id="warning">

<p class="it">¡Tenga cuidado! Este es un capítulo bastante denso, lleno de años con el valor de los  conocimientos en desarrollo web, y nada aquí es específico a D3. Recomiendo sólo rozar las secciones de información que son nuevas para usted, y omitir el resto. Siempre se puede posteriormente hacer referencia a este capítulo a medida que surgen las preguntas.</p>      
<p class="p" id="Beware11">Beware! This is a pretty dense chapter, packed with years’ worth of web development knowledge, and nothing in here is specific to D3. I recommend skimming just the sections on information that is new to you, and skipping the rest. You can always reference this chapter later as questions arise.</p>


</div>
  <div class="" data-original-filename="3_tech_fundamentals.asciidoc" id="_the_web765">

    <div class="titlepage">

      <div>

        <h2 class="title">The Web</h2>

      </div>

    </div>
    </div>
<p class="it">Si usted es nuevo haciendo páginas web, ahora tendrá que pensar en las cosas a las que la gente normal y extremadamente felíz hacen caso omiso de todos los días, como la siguiente: ¿Cómo realmente funciona la Web ?</p>
    <p class="p" id="if_youre_brand">If you’re brand new to making web pages, you will now have to think about things that regular people blissfully disregard every day, such as this: How does the Web actually work?<a id="id485280" class="indexterm" href=""></a></p>
<p class="it">Pensamos en la Web como un montón de páginas vinculadas entre sí, pero en realidad es una colección de conversaciones entre los servidores web y clientes web (browsers).</p>
    <p class="p" id="we_think_of_the">We think of the Web as a bunch of interlinked pages, but it’s really a collection of conversations between web servers and web clients (browsers).</p>
<p class="it">La siguiente escena es una dramatizacion de una típica conversación que sucede siempre que usted o cualquier otra persona hace clic en un vínculo o tipea una dirección en su navegador (es decir, esta breve conversación se tiene cerca de 88 millones de veces cada día):</p>
    <p class="p" id="the_following_s">The following scene is a dramatization of a typical such conversation that happens whenever you or anyone else clicks a link or types an address into your browser (meaning, this brief conversation is had about 88 zillion times every day):</p>
<div class="blockquote">

      <blockquote class="blockquote">
<p class="it">CLIENTE: Realmente me gustaria saber lo que está pasando en somewebsite.com. Mejor que llame allá para obtener la última información. [Está estableciendo el sonido silencioso de la conexión a Internet.]</p>
        <p class="p" id="client_id_rea">CLIENT: I’d really like to know what’s going on over at <span class="emphasis"><em>somewebsite.com</em></span>. I better call over there to get the latest info. [Silent sound of Internet connection being established.]</p>
<p class="it">SERVIDOR: Hola, cliente web desconocido! Soy el servidor que aloja somewebsite.com. ¿Qué página deseas?</p>
        <p class="p" id="server_hello_">SERVER: Hello, unknown web client! I am the server hosting <span class="emphasis"><em>somewebsite.com</em></span>. What page would you like?</p>
<p class="it">CLIENTE: Esta mañana, estoy interesado en la pagina de somewebsite.com/news/.</p>
        <p class="p" id="client_this_mo">CLIENT: This morning, I am interested in the page at <span class="emphasis"><em>somewebsite.com/news/</em></span>.</p>
<p class="it">SERVIDOR: Por supuesto, un momento.</p>
        <p class="p" id="server_of_cour">SERVER: Of course, one moment.</p>

<p class="it"><strong>El código se transmite desde el servidor al cliente.</strong></p>        
        <p class="p" id="code_is_transmi"><span class="emphasis"><strong>Code is transmitted from SERVER to CLIENT.</strong></span></p>

<p class="it">CLIENTE: Lo he recibido. ¡Gracias!</p>
        <p class="p" id="client_i_have_">CLIENT: I have received it. Thank you!</p>
<p class="it">SERVIDOR: Usted es bienvenido! Me encantaría permanecer en la línea y chat, pero tengo otros pedidos para procesar. ¡Adiós!</p>
        <p class="p" id="server_youre_">SERVER: You’re welcome! Would love to stay on the line and chat, but I have other requests to process. Bye!</p>

      </blockquote>

    </div>
<p class="it">Los clientes contactan con los servidores con solicitudes, y los servidores responden con datos. Pero, ¿qué es un servidor y que es un cliente?</p>
    <p class="p" id="clients_contact">Clients contact servers with <span class="emphasis"><em>requests</em></span>, and servers respond with data. But what is a server and what is a client?<a id="id485352" class="indexterm" href=""></a><a id="id485357" class="indexterm" href=""></a><a id="id485365" class="indexterm" href=""></a></p>
<p class="it">Los servidores web son ordenadores conectados a Internet que ejecutan software de servidor, así llamados porque sirven como buscadores de documentos. Los servidores normalmente estan siempre conectados, pero los desarrolladores web a menudo también ejecutan los servidores locales, lo que significa que se ejecutan en el mismo equipo que estás trabajando en medios locales aquí;. xxxxx en otro lugar, en cualquier ordenador pero el más adecuado está frente de ti.</p>
    <p class="p" id="web_servers_are"><span class="emphasis"><em>Web servers</em></span> are Internet-connected computers running server software, so called because they <span class="emphasis"><em>serve</em></span> web documents as requested. Servers are typically always on and always connected, but web developers often also run <span class="emphasis"><em>local</em></span> servers, meaning they run on the same computer that you’re working on. <span class="emphasis"><em>Local</em></span> means here; <span class="emphasis"><em>remote</em></span> means somewhere else, on any computer but the one right in front of you.<a id="id485393" class="indexterm" href=""></a><a id="id485398" class="indexterm" href=""></a></p>
<p class="it">Hay un montón de diferentes paquetes de software de servidor, pero Apache es el más común. El Software del servidor Web no es bonito, y nadie quiere mirarlo.</p>
 <p class="p" id="there_are_lots_">There are lots of different server software packages, but Apache is the most common. Web server software is not pretty, and no one ever wants to look at it.<a id="id485409" class="indexterm" href=""></a></p>
<p class="it">Por el contrario, los navegadores web pueden ser muy bonitos, y se pasa mucho tiempo buscando en ellos. La gente normal reconocen nombres como Firefox, Safari, Chrome e Internet Explorer, los cuales son los navegadores web o clientes.</p>
    <p class="p" id="in_contrast_we">In contrast, web <span class="emphasis"><em>browsers</em></span> can be very pretty, and we spend a lot of time looking at them. Regular people recognize names like Firefox, Safari, Chrome, and Internet Explorer, all of which are browsers or <span class="emphasis"><em>web clients</em></span>.<a id="id485426" class="indexterm" href=""></a></p>
<p class="it">Cada página web, en teoría, puede ser identificada por su dirección URL (Uniform Resource Locator) o URI (Uniform Resource Identifier). La mayoría de la gente no sabe qué significa URL, sino que reconoce a una cuando la ven. Por convención obsoleta, las URLs comienzan comúnmente con www, como en http://www.calmingmanatee.com, pero con un servidor configurado correctamente, la parte WWW es totalmente innecesaria.</p>
    <p class="p" id="every_web_page">Every web page, in theory, can be identified by its URL (Uniform Resource Locator) or URI (Uniform Resource Identifier). Most people don’t know what <span class="emphasis"><em>URL</em></span> stands for, but they recognize one when they see it. By obsolete convention, URLs commonly begin with <span class="emphasis"><em>www</em></span>, as in <a class="ulink" href="http://www.calmingmanatee.com/" target="_top">http://www.calmingmanatee.com</a>, but with a properly configured server, the <span class="emphasis"><em>www</em></span> part is wholly unnecessary.<a id="id485458" class="indexterm" href=""></a></p>
<p class="it">Las URL completas constan de cuatro partes:</p>
    <p class="p" id="complete_urls_c">Complete URLs consist of four parts:</p>

        <div class="itemizedlist" id="an_indication_o_id1">

      <ul class="itemizedlist">
<li class="it">Una indicación del protocolo de comunicación, tal como HTTP o HTTPS</li>
        <li class="p"> An indication of the <span class="emphasis"><em>communication protocol</em></span>, such as HTTP or HTTPS </li>
<br/>
<li class="it">El nombre de dominio del recurso, como calmingmanatee.com</li>
        <li class="p"> The <span class="emphasis"><em>domain name</em></span> of the resource, such as <span class="emphasis"><em>calmingmanatee.com</em></span> </li>
<br/>
<li class="it">El número de puerto, lo que indica sobre qué puerto se intenta la conexión con el servidor</li>
        <li class="p"> The <span class="emphasis"><em>port number</em></span>, indicating over which port the connection to the server should be attempted </li>
<br/>
<li class="it">Cualquier información de localización adicional, tal como la ruta del archivo solicitado, o los parámetros de consulta</li>
        <li class="p"> Any additional locating information, such as the path of the requested file, or any query parameters<a id="id485506" class="indexterm" href=""></a><a id="id485511" class="indexterm" href=""></a><a id="id485516" class="indexterm" href=""></a><a id="id485522" class="indexterm" href=""></a> </li>
<br/>
      </ul>

    </div>
    <p class="it">Una URL completa, a continuación, podría tener este aspecto: http://alignedleft.com:80/tutorials/d3/.</p>
    <p class="p" id="a_complete_url">A complete URL, then, might look like this: <a class="ulink" href="http://alignedleft.com/tutorials/d3/" target="_top">http://alignedleft.com:80/tutorials/d3/</a>.</p>
<p class="it">Por lo general, se excluye el número de puerto, dado que el web browser intentarán conectarse a través del puerto 80 de forma predeterminada. Así que la URL anterior es funcionalmente la misma que la siguiente: http://alignedleft.com/tutorials/d3/</p>
    <p class="p" id="typically_the_">Typically, the port number is excluded, as web browsers will try to connect over port 80 by default. So the preceding URL is functionally the same as the following: <a class="ulink" href="http://alignedleft.com/tutorials/d3/" target="_top">http://alignedleft.com/tutorials/d3/</a></p>
<p class="it">Tenga en cuenta que el protocolo se separa del nombre de dominio dcon dos puntos y dos diagonales (regular) barras. ¿Por qué dos barras? Sin razón. El inventor de la Web lamenta el error.</p>    
    <p class="p" id="note_that_the_p">Note that the protocol is separated from the domain name by a colon and two forward (regular) slashes. Why two slashes? No reason. The inventor of the Web <a class="ulink" href="http://nyti.ms/Xaol4j" target="_top">regrets the error</a>.</p>
<p class="it">HTTP significa protocolo de transferencia de hipertexto, y es el protocolo más común para transferir el contenido web del servidor al cliente. La "S" en el extremo de HTTPS significa Secure. Las conexiones HTTPS se utilizan siempre que la información debe ser encriptada en tránsito, tales como la banca en línea o el comercio electrónico.</p>
    <p class="p" id="http_stands_for">HTTP stands for Hypertext Transfer Protocol, and it’s the most common protocol for transferring web content from server to client. The “S” on the end of HTTPS stands for <span class="emphasis"><em>Secure</em></span>. HTTPS connections are used whenever information should be encrypted in transit, such as for online banking or e-commerce.<a id="id485569" class="indexterm" href=""></a></p>
<p class="it">Vamos a andar brevemente a través del proceso de lo que sucede cuando una persona va a visitar un sitio web.</p>
    <p class="p" id="lets_briefly_s">Let’s briefly step through the process of what happens when a person goes to visit a website.<a id="id485580" class="indexterm" href=""></a></p>

    <div class="orderedlist" id="user_runs_the_w_id1">

      <ol class="orderedlist" type="1">
 <li class="it">El usuario ejecuta el navegador web de su elección, tipea una URL en la barra de direcciones, como por ejemplo alignedleft.com/tutorials/d3/. Debido a que no especificó un protocolo se presupone que es http, y "http: //" se antepone a la URL.</li>
        <li class="p"> User runs the web browser of her choice, then types a URL into the address bar, such as <span class="emphasis"><em>alignedleft.com/tutorials/d3/</em></span>. Because she did not specify a protocol, HTTP is assumed, and “http://” is prepended to the URL. </li>


 <li class="it">Entonces el navegador intenta conectarse al servidor detrás de alignedleft.com a través de la red, via el puerto 80, el puerto por defecto para HTTP.</li>
        <li class="p"> The browser then attempts to connect to the server behind <span class="emphasis"><em>alignedleft.com</em></span> across the network, via port 80, the default port for HTTP. </li>

<li class="it">El servidor asociado con alignedleft.com reconoce la conexión y está tomando las solicitudes. ( "Voy a estar aquí toda la noche".)</li>
        <li class="p"> The server associated with <span class="emphasis"><em>alignedleft.com</em></span> acknowledges the connection and is taking requests. (“I’ll be here all night.”) </li>
 
<li class="it">El navegador envía una petición de la página que está en / tutoriales / d3 /.</li>
        <li class="p"> The browser sends a request for the page that lives at <span class="emphasis"><em>/tutorials/d3/</em></span>. </li>
<li class="it">El servidor envía el contenido HTML de esa página.</li>
        <li class="p"> The server sends back the HTML content for that page. </li>
<li class="it">A medida que el navegador del cliente recibe el código HTML, se descubrne referencias a otros archivos necesarios para montar y mostrar toda la página, incluyendo hojas de estilo CSS y archivos de imagen. Por lo tanto, contacto con el servidor de nuevo, una vez por cada archivo, solicitando la información adicional.</li> 
        <li class="p"> As the client browser receives the HTML, it discovers references to <span class="emphasis"><em>other files</em></span> needed to assemble and display the entire page, including CSS stylesheets and image files. So it contacts the same server again, once per file, requesting the additional information. </li>

<li class="it">El servidor responde, enviando cada archivo según sea necesario.</li>        
        <li class="p"> The server responds, dispatching each file as needed. </li>

     
 <li class="it">Por último, todos los documentos web han sido transferidos. Ahora el cliente realiza su tarea más ardua, que es la de renderizar el contenido. Se analiza primero a través de la HTML para comprender la estructura de los contenidos. A continuación, se revisan los selectores CSS, aplicando las propiedades de los elementos coincidentes. Por último, se conecta cualquier archivo de imagen y se ejecuta el código JavaScript.</li>
        <li class="p"> Finally, all the web documents have been transferred over. Now the client performs its most arduous task, which is to <span class="emphasis"><em>render</em></span> the content. It first parses through the HTML to understand the structure of the content. Then it reviews the CSS selectors, applying any properties to matched elements. Finally, it plugs in any image files and executes any JavaScript code. </li>

  </ol>
    </div>

    <p class="it">¿Se puede creer que todo esto es lo que sucede cada vez que hace clic en un enlace? Es mucho más complicado de lo que la mayoría de las personas se dan cuenta, pero es importante entender que las conversaciones cliente / servidor son fundamentales para la Web.</p>
    <p class="p" id="can_you_believe">Can you believe that all that happens every time you click a link? It’s a lot more complicated than most people realize, but it’s important to understand that client/server conversations are fundamental to the Web.</p>

 

  <div class="" data-original-filename="3_tech_fundamentals.asciidoc" id="_html">

    <div class="titlepage">

      <div>

        <h2 class="title">HTML</h2>

      </div>

    </div>
</div>
<p class="it">Hypertext Markup Language se utiliza para la estructura de contenido para los navegadores web. HTML se almacena en archivos de texto plano con el sufijo .html. Un documento HTML sencillo es el siguiente:</p>
    <p class="p" id="hypertext_marku">Hypertext Markup Language is used to structure content for web browsers. HTML is stored in plain text files with the <span class="emphasis"><em>.html</em></span> suffix. A simple<a id="ix_HTML" class="indexterm" href=""></a> HTML document looks like this:</p>

    <pre class="programlisting" data-language="html" id="doctype_html_id1">
    &lt;!DOCTYPE html&gt;
&lt;html&gt;
    &lt;head&gt;
        &lt;title&gt;Page Title&lt;/title&gt;
    &lt;/head&gt;
    &lt;body&gt;
        &lt;h1&gt;Page Title&lt;/h1&gt;
        &lt;p&gt;This is a really interesting paragraph.&lt;/p&gt;
    &lt;/body&gt;
&lt;/html&gt;</pre>
<p class="it">HTML es un lenguaje complejo con una rica historia. Esta visión general sólo se referirá a la iteración actual de HTML (anteriormente conocido como HTML 5) y se referirá a sólo lo que es inmediatamente relevante para nuestra práctica con D3.</p>
    <p class="p" id="html_is_a_compl">HTML is a complex language with a rich history. This overview will address only the current iteration of HTML (formerly known as HTML5) and will touch on only what is immediately relevant for our practice with D3.</p>

    <div class="sect2" id="_content_plus_structure">

      <div class="titlepage">

        <div>

          <h3 class="title">Content Plus Structure</h3>

        </div>

      </div>
      </div>

      <p class="it">La función básica de HTML es que pueda "marcar" el contenido, dándole así la estructura. Tomemos, por ejemplo, este texto sin formato:</p>
      <p class="p" id="the_core_functi">The core function of HTML is to enable you to “mark up” content, thereby<a id="id485792" class="indexterm" href=""></a> giving it structure. Take, for example, this raw text:</p>

      <pre class="programlisting" id="amazing_visuali_id1">Amazing Visualization Tool Cures All Ills A new open-source tool designed for visualization of data turns out to have an unexpected, positive side effect: it heals any ailments of the viewer. Leading scientists report that the tool,
called D3000, can cure even the following symptoms: fevers chills general malaise It achieves this end with a patented, three-step process. Load in data. Generate a visual representation. Activate magic healing function.</pre>

<p class="it">Leyendo entre líneas, podemos inferir que se trata de una noticia muy emocionante. Pero al no estar el contenido estructurado, es muy difícil de leer. Mediante la adición de la estructura, podemos diferenciar entre el titular, por ejemplo, y el cuerpo de la noticia.</p>
      <p class="p" id="reading_between">Reading between the lines, we can infer that this is a very exciting news story. But as unstructured content, it is very hard to read. By adding structure, we can differentiate between the headline, for example, and the body of the story.</p>

      <div class="blockquote">

        <blockquote class="blockquote">

          <p class="p" id="amazing_visuali_id2"><span class="strong"><strong>Amazing Visualization Tool Cures All Ills</strong></span></p>
<p class="it">Una nueva herramienta de código abierto diseñado para la visualización de datos resulta que tiene un positivo efecto secundario inesperado: se cura cualquier dolencia del espectador. Destacados científicos informan que la herramienta, denominada D3000, puede curar incluso los síntomas siguientes:</p>
          <p class="p" id="a_new_opensour">A new open-source tool designed for visualization of data turns out to have an unexpected, positive side effect: it heals any ailments of the viewer. Leading scientists report that the tool, called D3000, can cure even the following symptoms:</p>


          <div class="itemizedlist" id="fevers_chills_g">

            <ul class="itemizedlist">
<li class="it">fiebres</li>
              <li class="p"> fevers </li>
<br/><li class="it">resfriado</li>
              <li class="p"> chills </li>
<br/><li class="it">malestar general</li>
              <li class="p"> general malaise </li>
<br/>
            </ul>

          </div>
<p class="it">Se logra este objetivo con un proceso patentado, de tres pasos.</p>
          <p class="p" id="it_achieves_thi">It achieves this end with a patented, three-step process.</p>


          <div class="orderedlist" id="load_in_data_g">

            <ul class="orderedlist" type="1">
<li class="it">Carga de los datos.</li>
              <li class="p"> 1 - Load in data. </li>
<br/><li class="it">Generar una representación visual.</li>
              <li class="p"> 2 - Generate a visual representation. </li>

<br/><li class="it">Activar la función de curación mágica.</li>
              <li class="p"> 3 - Activate magic healing function. </li>
<br/>

            </ul>

          </div>

        </blockquote>

      </div>

<p class="it">Esto tiene el mismo contenido de texto sin formato, pero con una estructura visual que hace el contenido más accesible.</p>
      <p class="p" id="that_has_the_sa">That has the same raw text content, but with a <span class="emphasis"><em>visual structure</em></span> that makes the content more accessible.<a id="id485887" class="indexterm" href=""></a></p>



      <div class="blockquote">

        <blockquote class="blockquote">

          <p class="p" id="headline"><span class="strong"><strong>Headline</strong></span></p>

          <p class="p" id="paragraph_text_id1">Paragraph text</p>

          <div class="itemizedlist" id="unordered_list__id1">

            <ul class="itemizedlist">

              <li class="p"> Unordered list item </li>
<br/>
            <li class="p"> Unordered list item </li>
<br/>
              <li class="p"> Unordered list item </li>
<br/>
            </ul>

          </div>

          <p class="p" id="paragraph_text_id2">Paragraph text</p>







          <div class="orderedlist" id="numbered_list_i_id1">

            <ol class="orderedlist" type="1">

              <li class="p"> Numbered list item </li>
<br/>
              <li class="p"> Numbered list item </li>
<br/>
              <li class="p"> Numbered list item </li>
<br/>
            </ol>

          </div>

        </blockquote>
 </div>

<p class="it">Este es el tipo de estructura específica con el formato HTML.</p>
      <p class="p" id="this_is_the_kin">This is the kind of structure we specify with HTML markup.</p>
<br/>

    
    <div class="sect2" id="_adding_structure_with_elements">

      <div class="titlepage">

        

          <h3 class="title">Adding Structure with Elements</h3>

        </div>

      </div>

      <p class="it">“Marking up” es el proceso de añadir etiquetas para crear elementos. Las etiquetas HTML comienzan con <code class="literal">&lt;</code>y terminan con <code class="literal">&gt;</code> que es la etiqueta que indica un párrafo de texto. Las etiquetas con frecuencia estan en parejas, en cuyo caso la adición de un abrir y cerrar de un par de etiquetas crea un nuevo elemento en la estructura del documento.</p>

      <p class="p" id="marking_up_is">“Marking up” is the process of adding <span class="emphasis"><em>tags</em></span> to create <span class="emphasis"><em>elements</em></span>. HTML tags begin with <code class="literal">&lt;</code> and end with <code class="literal">&gt;</code>, as in <code class="literal">&lt;p&gt;</code>, which is the tag indicating a paragraph of text. Tags usually occur in pairs, in which case adding an opening and closing pair of tags creates a new <span class="emphasis"><em>element</em></span> in the document structure.<a id="id486020" class="indexterm" href=""></a><a id="id486027" class="indexterm" href=""></a><a id="id486033" class="indexterm" href=""></a></p>
<p class="it">Las etiquetas de cierre están indicadas con una barra que cierra o termina el elemento, como en  <code class="literal">&lt;/p&gt;</code>. De este modo, un párrafo de texto se puede marcar hasta el siguiente:</p>
      <p class="p" id="closing_tags_ar">Closing tags are indicated with a slash that closes or ends the element, as in <code class="literal">&lt;/p&gt;</code>. Thus, a paragraph of text may be marked up like the following:</p>
      <pre class="programlisting" data-language="html" id="pthis_is_a_re">&lt;p&gt;This is a really interesting paragraph.&lt;/p&gt;</pre>

      <p class="it">Algunos elementos pueden ser (anidados) <span class="emphasis"><em>nested</em></span>. Por ejemplo, aquí usamos el elemento <code class="literal">em </code>para añadir <span class="emphasis"> <em>énfasis</em></span>. </p>
<p class="p" id="some_elements_c">Some elements can be <span class="emphasis"><em>nested</em></span>. For example, here we use the <code class="literal">em</code> element to add <span class="emphasis"><em>emphasis</em></span>.</p>
      <pre class="programlisting" data-language="html" id="pthis_is_a_e">&lt;p&gt;This is a &lt;em&gt;really&lt;/em&gt; interesting paragraph.&lt;/p&gt;</pre>
      <p class="it">Los elementos de agrupamiento introducen jerarquía en el documento. En este caso, <code class="literal">em</code> es un hijo de <code class="literal">p</code>, ya que está contenida por <code class="literal">p</code>. (A la inversa, <code class="literal">p</code> es el padre de <code class="literal">em</code>.)</p>
      <p class="p" id="some_elements_c">Some elements can be <span class="emphasis"><em>nested</em></span>. For example, here we use the <code class="literal">em</code> element to add <span class="emphasis"><em>emphasis</em></span>.</p>
      <pre class="programlisting" data-language="html" id="pthis_is_a_e">&lt;p&gt;This is a &lt;em&gt;really&lt;/em&gt; interesting paragraph.&lt;/p&gt;</pre>

<p class="it">Cuando se anidan los elementos, no se pueden superponer los cierres de sus elementos primarios, ya que al hacerlo podría perturbar la jerarquía. Por ejemplo:</p>      
      <p class="p" id="when_elements_a">When elements are nested, they cannot overlap closures of their parent elements, as doing so would disrupt the hierarchy. For example:</p>
      <p class="p" id="nesting_element">Nesting elements introduces hierarchy to the document. In this case, <code class="literal">em</code> is a child of <code class="literal">p</code> because it is contained by <code class="literal">p</code>. (Conversely, <code class="literal">p</code> is <code class="literal">em</code>’s parent.)</p>
      <pre class="programlisting" data-language="html" id="pthis_could_c">&lt;p&gt;This could cause &lt;em&gt;unexpected&lt;/p&gt;
&lt;p&gt;results&lt;/em&gt;, and is best avoided.&lt;/p&gt;</pre>
<p class="it">Algunas etiquetas no se colocan en pares, tales como el elemento img, que hace referencia a un archivo de imagen. Aunque HTML ya no lo requiere, se le consulte a veces este tipo de etiquetas escritas en forma de cierre automático, con una barra final antes de poner el corchete de cierre:</p>
      <p class="p" id="some_tags_never">Some tags never occur in pairs, such as the <code class="literal">img</code> element, which references an image file. Although HTML no longer requires it, you will sometimes see such tags written in <span class="emphasis"><em>self-closing</em></span> fashion, with a trailing slash before the closing bracket:</p>

      <pre class="programlisting" data-language="html" id="img_srcphoto_id1">&lt;img src="photo.jpg" /&gt;</pre>
<p class="it">A partir de HTML 5, la barra de cierre automático es opcional, por lo que el siguiente código es equivalente al código anterior:</p>
      <p class="p" id="as_of_html_th">As of HTML5, the self-closing slash is optional, so the following code is equivalent to the preceding code:</p>


      <pre class="programlisting" data-language="html" id="img_srcphoto_id2">&lt;img src="photo.jpg"&gt;</pre>
      <div class="sect2" id="_common_elements">

      <div class="titlepage">

           <h3 class="title">Common Elements</h3>

        </div>

      </div>
<p class="it">Hay cientos de diferentes elementos HTML. Éstos son algunos de los más comunes. Vamos a cubrir elementos adicionales en los capítulos posteriores. (Consulte la excelente documentación de la red de desarrolladores de Mozilla para tener una lista completa.)</p>
      <p class="p" id="there_are_hundr">There are hundreds of different HTML elements. Here are some of the most common. We’ll cover additional elements in later chapters. (Reference the excellent <a class="ulink" href="https://developer.mozilla.org/en/HTML/Element" target="_top">Mozilla Developer Network documentation</a> for a complete listing.)<a id="id486271" class="indexterm" href=""></a></p>

            <div class="variablelist" id="doctype_html_id2">

        <dl class="variablelist">

          <dt><span class="term"> <code class="literal">&lt;!DOCTYPE html&gt;</code> </span></dt>
<dd class="it">La declaración de tipo de documento. Debe de ser lo primero que se pone en el documento.</dd> 
          <dd> The standard document type declaration. Must be the first thing in the document. </dd>

          <dt><span class="term"> <code class="literal">html</code> </span></dt>
<dd class="it">Rodea todo el contenido HTML en un documento.</dd>
          <dd> Surrounds all HTML content in a document. </dd>

          <dt><span class="term"> <code class="literal">head</code> </span></dt>
<dd class="it">Contiene todos los metadatos del documento, como el título y las referencias a stylesheets y scripts externos.</dd>
          <dd> The document <code class="literal">head</code> contains all metadata about the document, such as its <code class="literal">title</code> and any references to external stylesheets and scripts. </dd>

          <dt><span class="term"> <code class="literal">title</code> </span></dt>
<dd class="it">Los navegadores suelen mostrar esto en la parte superior de la ventana del navegador y utilizar este título, en la página de marcadores.</dd>
          <dd> The title of the document. Browsers typically display this at the top of the browser window and use this title when bookmarking a page. </dd>

          <dt><span class="term"> <code class="literal">body</code> </span></dt>
<dd class="it">Lo que no está en la cabeza debe ir en el cuerpo. Este es el contenido visible de la página principal.</dd>
          <dd> Everything not in the <code class="literal">head</code> should go in the <code class="literal">body</code>. This is the primary visible content of the page. </dd>

          <dt><span class="term"> <code class="literal">h1</code>, <code class="literal">h2</code>, <code class="literal">h3</code>, <code class="literal">h4</code> </span></dt>
<dd class="it">P permiten especificar los titulos de diferentes niveles. h1 es un título de nivel superior, h2 está por debajo, y así sucesivamente.</dd>
          <dd> These let you specify headings of different levels. <code class="literal">h1</code> is a top-level heading, <code class="literal">h2</code> is below that, and so on. </dd>

          <dt><span class="term"> <code class="literal">p</code> </span></dt>
<dd class="it">Un parrafo!</dd>
          <dd> A paragraph! </dd>

          <dt><span class="term"> <code class="literal">ul</code>, <code class="literal">ol</code>, <code class="literal">li</code> </span></dt>
          <dd class="it">Las listas no ordenadas se especifican con ul, la más utilizada para las listas con viñetas. Las listas ordenadas (ol) a menudo son contadas. Tanto ul y ol debe incluir elementos li para especificar elementos de la lista.</dd>
          <dd> Unordered lists are specified with <code class="literal">ul</code>, most often used for bulleted lists. Ordered lists (<code class="literal">ol</code>) are often numbered. Both <code class="literal">ul</code> and <code class="literal">ol</code> should include <code class="literal">li</code> elements to specify list items. </dd>


          <dt><span class="term"> <code class="literal">em</code> </span></dt>
<dd class="it">Indica énfasis. Por lo general dictada en cursiva.</dd>
          <dd> Indicates emphasis. Typically rendered in <span class="emphasis"><em>italics</em></span>. </dd>

          

          <dt><span class="term"> <code class="literal">strong</code> </span></dt>
<dd class="it"> Indica fuerte énfasis adicional. Por lo general dictada en <span class="strong"><strong>negrita</strong></span>.</dd>
          <dd> Indicates additional emphasis. Typically rendered in <span class="strong"><strong>boldface</strong></span>. </dd>
          
          

          <dt><span class="term"> <code class="literal">a</code> </span></dt>
<dd class="it">Un enlace. Típicamente subrayado, con texto azul, a menos que se especifique lo contrario.</dd>
          <dd> A link. Typically rendered as underlined, blue text, unless otherwise specified. </dd>

          <dt><span class="term"> <code class="literal">span</code> </span></dt>
<dd class="it">Un lapso arbitrario de texto, por lo general dentro de un elemento contenedor más grande, como p.</dd>
          <dd> An arbitrary <code class="literal">span</code> of text, typically within a larger containing element like <code class="literal">p</code>. </dd>

          <dt><span class="term"> <code class="literal">div</code> </span></dt>
<dd class="it">Una división arbitraria dentro del documento. Se utiliza para agrupar y contiene elementos relacionados.</dd>
          <dd> An arbitrary <span class="emphasis"><em>division</em></span> within the document. Used for grouping and containing related elements. </dd>

        </dl>

      </div>

      <p class="it">A nuestro ejemplo anterior se le podría dar estructura semántica usando algunos de estas etiquetas:</p>
      <p class="p" id="our_earlier_exa">Our earlier example could be given semantic structure by marking it up using some of these element’s tags:</p>
      
      <pre class="programlisting" data-language="html" id="hamazing_vis">&lt;h1&gt;Amazing Visualization Tool Cures All Ills&lt;/h1&gt;
&lt;p&gt;A new open-source tool designed for visualization of data turns out to have
an unexpected, positive side effect: it heals any ailments of the viewer.
Leading scientists report that the tool, called D3000, can cure even the
following symptoms:&lt;/p&gt;
&lt;ul&gt;
    &lt;li&gt;fevers&lt;/li&gt;
    &lt;li&gt;chills&lt;/li&gt;
    &lt;li&gt;general malaise&lt;/li&gt;
&lt;/ul&gt;
&lt;p&gt;It achieves this end with a patented, three-step process.&lt;/p&gt;
&lt;ol&gt;
    &lt;li&gt;Load in data.&lt;/li&gt;
    &lt;li&gt;Generate a visual representation.&lt;/li&gt;
    &lt;li&gt;Activate magic healing function.&lt;/li&gt;
&lt;/ol&gt;</pre>

<p class="it">Cuando se ve en un navegador web, el lenguaje de formato se representa como se muestra en la Figura 3-1.</p>
      <p class="p" id="when_viewed_in_">When viewed in a web browser, that markup is rendered as shown in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch03.html#Typical_default_rendering_of_simple_HTML" title="Figure 3-1. Typical default rendering of simple HTML">Figure 3-1</a>.</p>

            <div class="figure" id="Typical_default_rendering_of_simple_HTML">

        <div class="figure-contents">

          <div class="mediaobject">

            <img src="/static/KSnaJy9UI1-img1.png" alt="Typical default rendering of simple HTML"/>

          </div>

        </div>
<p class="fig">Figura 3-1. Representación predeterminada típica de HTML simple</p>

        <p class="fig">Figure 3-1. Typical default rendering of simple HTML</p>

      </div>

      <p class="it">Nótese que hemos especificado sólo la estructura semántica del contenido; sin especificar propiedades visuales, como el color, tamaño de letra, guiones, o el interlineado. Sin tales instrucciones, el navegador vuelve a caer en sus estilos predeterminados, que, francamente, no son demasiado emocionante.</p>
      <p class="p" id="notice_that_we_">Notice that we specified only the <span class="emphasis"><em>semantic</em></span> structure of the content; we didn’t specify any visual properties, such as color, type size, indents, or line spacing. Without such instructions, the browser falls back on its <span class="emphasis"><em>default styles</em></span>, which, frankly, are not too <span class="keep-together">exciting</span>.</p>
          <div class="sect2" id="_attributes">

      <div class="titlepage">

        <div>

          <h3 class="title">Attributes</h3>

        </div>
</div>
      </div>

      <p class="it">A todos los elementos HTML se le pueden asignar atributos mediante la inclusión de pares de propiedades/valor en la etiqueta de apertura.</p>
      <p class="p" id="all_html_elemen">All HTML elements can be assigned <span class="emphasis"><em>attributes</em></span> by including property/value pairs in the opening tag.<a id="id486753" class="indexterm" href=""></a><a id="id486760" class="indexterm" href=""></a></p>


      <pre class="programlisting" data-language="html" id="tagname_proper">&lt;tagname property="value"&gt;&lt;/tagname&gt;</pre>
<p class="it">El nombre de la propiedad es seguido por un signo igual y el valor está entre comillas dobles.</p>
      <p class="p" id="the_name_of_the">The name of the property is followed by an equals sign, and the value is enclosed within double quotation marks.</p>
      

<p class="it">A diferentes tipos de elementos se le pueden asignar diferentes atributos. Por ejemplo, a la etiqueta de un enlace se le puede dar un atributo href, cuyo valor especifica la dirección URL de ese enlace. (href es la abreviatura de "referencia HTTP".)</p>
      <p class="p" id="different_kinds">Different kinds of elements can be assigned different attributes. For example, the <code class="literal">a</code> link tag can be given an <code class="literal">href</code> attribute, whose value specifies the URL for that link. (<code class="literal">href</code> is short for “HTTP reference.”)</p>

      <pre class="programlisting" data-language="html" id="a_hrefhttp">&lt;a href="http://d3js.org/"&gt;The D3 website&lt;/a&gt;</pre>
<p class="it">Algunos atributos se pueden asignar a cualquier tipo de elemento, como class e id.</p>
      <p class="p" id="some_attributes">Some attributes can be assigned to <span class="emphasis"><em>any</em></span> type of element, such as <code class="literal">class</code> and <code class="literal">id</code>.</p>

          <div class="sect2" id="_classes_and_ids">

      <div class="titlepage">

        <div>

          <h3 class="title">Classes and IDs</h3>

        </div>

        </div>

      </div>
<p class="it">Las clases y los ID son muy útiles, ya que pueden ser referenciados más adelante para identificar elementos específicos del contenido. Su código CSS y JavaScript dependerá en gran medida de las clases y los IDs para identificar elementos. Por ejemplo:</p>
      <p class="p" id="classes_and_ids">Classes and IDs are extremely useful attributes, as they can be<a id="id486877" class="indexterm" href=""></a><a id="id486884" class="indexterm" href=""></a> referenced later to identify specific pieces of content. Your CSS and JavaScript code will rely heavily on classes and IDs to identify elements. For example:</p>


      <pre class="programlisting" data-language="html" id="pbrilliant_pa">&lt;p&gt;Brilliant paragraph&lt;/p&gt;
&lt;p&gt;Insightful paragraph&lt;/p&gt;
&lt;p class="awesome"&gt;Awe-inspiring paragraph&lt;/p&gt;</pre>

<p class="it">Estos son tres párrafos muy edificante, pero sólo uno de ellos es verdaderamente impresionante, como he indicado con class = "impresionante". El tercer párrafo se convierte en parte de una clase de elementos llamada impresionante, y se puede seleccionar y manipular junto con otros miembros de la clase. (El nombre contiene llegar a eso en un momento.)</p>
      <p class="p" id="these_are_three">These are three very uplifting paragraphs, but only one of them is truly awesome, as I’ve indicated with <code class="literal">class="awesome"</code>. The third paragraph becomes part of a <span class="emphasis"><em>class</em></span> of <span class="emphasis"><em>awesome</em></span> elements, and it can be selected and manipulated along with other class members. (We’ll get to that in a moment.)</p>

<p class="it">A los elementos se le pueden asignar múltiples clases, simplemente separándolas con un espacio:</p>
      <p class="p" id="elements_can_be">Elements can be assigned multiple classes, simply by separating them with a space:</p>


      <pre class="programlisting" data-language="html" id="p_classuplif">&lt;p class="uplifting"&gt;Brilliant paragraph&lt;/p&gt;
&lt;p class="uplifting"&gt;Insightful paragraph&lt;/p&gt;
&lt;p class="uplifting awesome"&gt;Awe-inspiring paragraph&lt;/p&gt;</pre>
<p class="it">Ahora, los tres párrafos son edificantes, pero sólo el último es a la vez estimulante e impresionante.</p>
      <p class="p" id="now_all_three_">Now, all three paragraphs are <code class="literal">uplifting</code>, but only the last one is both <code class="literal">uplifting</code> <span class="emphasis"><em>and</em></span> <code class="literal">awesome</code>.</p>
      
   <p class="it">Los identificaciones se utilizan de la misma manera, pero no puede haber un único ID por elemento, y cada valor de ID se puede utilizar sólo una vez en la página. Por ejemplo:</p>
      <p class="p" id="ids_are_used_in">IDs are used in much the same way, but there can be only one ID per<a id="id487075" class="indexterm" href=""></a> element, and each ID value can be used only once on the page. For example:</p>
   

      <pre class="programlisting" data-language="html" id="div_idconten">&lt;div id="content"&gt;
    &lt;div id="visualization"&gt;&lt;/div&gt;
    &lt;div id="button"&gt;&lt;/div&gt;
&lt;/div&gt;</pre>
<p class="it">Los IDs son útiles cuando un solo elemento tiene alguna cualidad especial, como un div que funciona como un botón o como contenedor para otro tipo de contenido en la página.</p>
      <p class="p" id="ids_are_useful_">IDs are useful when a single element has some special quality, like a <code class="literal">div</code> that functions as a button or as a container for other content on the page.<a id="id487160" class="indexterm" href=""></a><a id="id487165" class="indexterm" href=""></a></p>

<p class="it">Como regla general, si tendrá sólo uno de tales elementos en la página, se puede usar un id. De lo contrario, utilice una clase.</p>
      <p class="p" id="as_a_general_ru">As a general rule, if there will be only <span class="emphasis"><em>one</em></span> such element on the page, you can use an <code class="literal">id</code>. Otherwise, use a <code class="literal">class</code>.</p>
    
      <div class="warning" id="class_and_id_na_id1">
<p class="it">Los nombres de clases e IDs no puede comenzar con números; que deben comenzar con caracteres alfabéticos. Así que el id = "1" no corre y el id = "item1" si. El navegador no le dará ningún error; su código simplemente no corrio, y se volverá loco tratando de averiguar por qué.</p>
        <p class="p" id="class_and_id_na_id2">Class and ID names cannot begin with numerals; they must begin with alphabetic characters. So <code class="literal">id="1"</code> won’t work, but <code class="literal">id="item1"</code> will. The browser will not give you any errors; your code simply won’t work, and you will go crazy trying to figure out why.</p>
</div>

  <div class="" data-original-filename="3_tech_fundamentals.asciidoc" id="_dom">

    <div class="titlepage">

      <div>

        <h2 class="title">DOM</h2>

    </div>
    
      </div>

    </div>

<p class="it">El término Document Object Model (DOM) se refiere a la estructura jerárquica de HTML. Cada par de etiquetas brackeadas (o, en algunos casos, una sola etiqueta) es un elemento, y se refiere a las relaciones relativas entre los elementos en términos humanos: padres, hijos, hermanos, antepasado, y descendiente. Por ejemplo, en este HTML:</p>
    <p class="p" id="the_term_docume">The term Document Object Model refers to the hierarchical structure of<a id="id487284" class="indexterm" href=""></a><a id="id487291" class="indexterm" href=""></a><a id="id487299" class="indexterm" href=""></a><a id="id487304" class="indexterm" href=""></a><a id="id487309" class="indexterm" href=""></a><a id="id487314" class="indexterm" href=""></a><a id="id487319" class="indexterm" href=""></a> HTML. Each pair of bracketed tags (or, in some cases, a single tag) is an <span class="emphasis"><em>element</em></span>, and we refer to elements’ relative relationships to each other in human terms: parent, child, sibling, ancestor, and descendant. For example, in this HTML:</p>


    <pre class="programlisting" data-language="html" id="html_body_">&lt;html&gt;
    &lt;body&gt;
        &lt;h1&gt;Breaking News&lt;/h1&gt;
        &lt;p&gt;&lt;/p&gt;
    &lt;/body&gt;
&lt;/html&gt;</pre>
<p class="it">body es el elemento padre de sus dos hijos, h1 y p (que son hermanos entre sí). Todos los elementos de la página son descendientes de html.</p>
    <p class="p" id="body_is_the_par"><code class="literal">body</code> is the parent element to both of its children, <code class="literal">h1</code> and <code class="literal">p</code> (which are siblings to each other). All elements on the page are descendants of <code class="literal">html</code>.</p>

<p class="it">Los navegadores web analizan el DOM para dar sentido al contenido de una página. Como constructores de codigo de visualizacion, nos preocupamos por el DOM, porque nuestro código debe navegar su jerarquía para aplicar estilos y acciones a sus elementos. No queremos hacer todos los elementos div azul; necesitamos saber cómo seleccionar sólo los divs de la clase cielo para que se vuelvan azules.</p>
    <p class="p" id="web_browsers_pa">Web browsers parse the DOM to make sense of a page’s content. As coders building visualizations, we care about the DOM, because our code must navigate its hierarchy to apply styles and actions to its elements. We don’t want to make <span class="emphasis"><em>all</em></span> the <code class="literal">div</code> elements blue; we need to know how to select just the <code class="literal">div</code>s of the class <code class="literal">sky</code> and make <span class="emphasis"><em>them</em></span> blue.</p>

      <div class="" data-original-filename="3_tech_fundamentals.asciidoc" id="_rendering_and_the_box_model">

    <div class="titlepage">

        <h2 class="title">Rendering and the Box Model</h2>

      </div>

    </div>
<p class="it">El renderizado es el proceso por el cual los navegadores, después de analizar el código HTML y generar el DOM, le aplican reglas visuales al contenido DOM y dibujan los píxeles en la pantalla.</p>
    <p class="p" id="rendering_is_th"><span class="emphasis"><em>Rendering</em></span> is the process by which browsers, after parsing the HTML and generating the DOM, apply visual rules to the DOM contents and draw those pixels to the screen.<a id="id487711" class="indexterm" href=""></a><a id="id487716" class="indexterm" href=""></a></p>
<p class="it">Lo más importante para tener en cuenta al considerar la forma en que los navegadores muestran el contenido es la siguiente: para un navegador, todo es una caja.</p>
    <p class="p" id="the_most_import">The most important thing to keep in mind when considering how browsers render content is this: to a browser, everything is a box.</p>
<p class="it">Los párrafos, divs, etc. son cajas en el sentido de que son rectángulos de dos dimensiones, con propiedades que cualquier rectángulo puede tener, como anchura, altura y posición en el espacio. Incluso si algo se ve curvado o de forma irregular, puede estar seguro, para el navegador, no es más que otra caja rectangular.</p>
    <p class="p" id="paragraphs_div">Paragraphs, <code class="literal">div</code>s, <code class="literal">span</code>s—all are boxes in the sense that they are two-dimensional rectangles, with properties that any rectangle can have, such as width, height, and positions in space. Even if something looks curved or irregularly shaped, rest assured, to the browser, it is merely another rectangular box.<a id="id487746" class="indexterm" href=""></a><a id="id487751" class="indexterm" href=""></a><a id="id487758" class="indexterm" href=""></a></p>
   <p class="it">Se puedne ver estos cuadros con la ayuda del inspector web. Pasando el mouse sobre cualquier elemento, un cuadro asociado con ese elemento se pone de relieve en azul, como se muestra en la Figura 3-4.</p>
    <p class="p" id="you_can_see_the">You can see these boxes with the help of the web inspector. Just mouse over any element, and the box associated with that element is highlighted in blue, as shown in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch03.html#Inspector_with_element_box_highlighted" title="Figure 3-4. Inspector with element box highlighted">Figure 3-4</a>.</p>

       <div class="figure" id="Inspector_with_element_box_highlighted">

      <div class="figure-contents">

        <div class="mediaobject">

          <img src="/static/KSnaJy9UI1-img2.png" alt="Inspector with element box highlighted"/>

        </div>

      </div>
<p class="fig">Figura 3-4. Inspector con la caja del elemento resaltada</p>
      <p class="fig">Figure 3-4. Inspector with element box highlighted</p>


    </div>

    <p class="it">Hay una gran cantidad de información aquí acerca de la desordenada lista ul aquí. Tenga en cuenta que las  dimensiones totales de la lista (anchura y altura) se muestran en el cuadro amarillo en el elemento esquina inferior izquierda. Además, la posición de la lista en la jerarquía DOM se indica en la esquina inferior izquierda del inspector: html&gt; body&gt; ul.</p>
    <p class="p" id="theres_a_lot_o">There’s a lot of information about the <code class="literal">ul</code> unordered list here. Note that the list’s total dimensions (width and height) are shown in the yellow box at the element’s lower-left corner. Also, the list’s position in the DOM hierarchy is indicated in the lower-left corner of the inspector: <code class="literal">html &gt; body &gt; ul</code>.<a id="id487808" class="indexterm" href=""></a></p>
<p class="it">El cuadro de la ul expande o ajusta la anchura de la ventana completa, ya que es un elemento a nivel de bloque. (Nota muestran la cantidad que en "Estilo computarizada" aparece en la lista:. Bloque) Esto está en contraste con Elementos en línea, que descansan en línea entre sí, no apiladas una encima de la otra como bloques de elementos en línea. Comunes que incluyen strong, em, a.</p>
    <p class="p" id="the_box_for_the">The box for the <code class="literal">ul</code> expands to fill the width of the entire window because it is a <span class="emphasis"><em>block-level</em></span> element. (Note how under “Computed Style” is listed <code class="literal">display: block</code>.) This is in contrast to <span class="emphasis"><em>inline</em></span> elements, which rest <span class="emphasis"><em>in line</em></span> with each other, not stacked on top of each other like blocks. Common inline elements include <code class="literal">strong</code>, <code class="literal">em</code>, <code class="literal">a</code>, and <code class="literal">span</code>.<a id="id487860" class="indexterm" href=""></a><a id="id487866" class="indexterm" href=""></a></p>

<p class="it">De forma predeterminada, los elementos de bloque se expanden para llenar sus elementos contenedores y obligan a todos los elementos de hermanos posteriores al final de la página. Los elementos en línea no se expanden para llenar el espacio extra, y los apilan de lado a lado, junto a sus vecinos en línea compañeros. (Discusión pregunta: ¿qué tipo de elemento preferirías ser?)</p>
       <p class="p" id="by_default_blo">By default, block-level elements expand to fill their container elements and force any subsequent sibling elements further down the page. Inline elements do not expand to fill extra space, and happily exist side by side, next to their fellow inline neighbors. (Discussion question: what kind of element would you rather be?)</p>

         <div class="" data-original-filename="3_tech_fundamentals.asciidoc" id="_css">

    <div class="titlepage">

      <div>

        <h2 class="title">CSS</h2>

    </div>
      </div>

    </div>
<p class="it">La Cascading Style Sheets se utilizan para el estilo de la presentación visual de los elementos DOM. Una simple hoja de estilo CSS tiene el siguiente aspecto:</p>
    <p class="p" id="cascading_style">Cascading Style Sheets are used to style the visual presentation of DOM<a id="ix_CSS" class="indexterm" href=""></a><a id="id487900" class="indexterm" href=""></a> elements. A simple CSS stylesheet looks like the following:</p>


    <pre class="programlisting" data-language="css" id="body__backgrou">body {
    background-color: white;
    color: black;
}</pre>
<p class="it">Los estilos CSS consisten en selectores y propiedades. Los selectores son seguidos por propiedades, agrupadas entre llaves. Una propiedad y su valor están separados por dos puntos, y la línea se termina con un punto y coma, como la siguiente:</p>
    <p class="p" id="css_styles_cons">CSS styles consist of <span class="emphasis"><em>selectors</em></span> and <span class="emphasis"><em>properties</em></span>. Selectors are<a id="id487978" class="indexterm" href=""></a><a id="id487986" class="indexterm" href=""></a><a id="id487991" class="indexterm" href=""></a> followed by properties, grouped in curly brackets. A property and its value are separated by a colon, and the line is terminated with a semicolon, like the following:</p>

    <pre class="programlisting" data-language="css" id="selector__prop">selector {
    property: value;
    property: value;
    property: value;
}</pre>
<p class="it">Las mismas propiedades se pueden aplicar a varios selectores a la vez mediante la separación de los selectores con una coma, como en el codigo siguiente:</p>
    <p class="p" id="the_same_proper">The same properties can be applied to multiple selectors at once by separating the selectors with a comma, as in the following:</p>


    <pre class="programlisting" data-language="css" id="selectora_sele">selectorA,
selectorB,
selectorC {
    property: value;
    property: value;
    property: value;
}</pre>
<p class="it">Por ejemplo, es posible que desee especificar que ambos párrafos p y elementos de lista li deben utilizar el mismo tamaño de fuente, altura de la línea y color.</p>
    <p class="p" id="for_example_yo_id1">For example, you might want to specify that both <code class="literal">p</code> paragraphs and <code class="literal">li</code> list items should use the same font size, line height, and color.</p>


    <pre class="programlisting" data-language="css" id="p_li__fontsi">    p,
li {
    font-size: 12px;
    line-height: 14px;
    color: orange;
}</pre>
<p class="it">En conjunto, todo este trozo de código (selectores y propiedades entre corchetes) se llama una regla CSS.</p>
    <p class="p" id="collectively_t">Collectively, this whole chunk of code (selectors and bracketed properties) is called a <span class="emphasis"><em>CSS rule</em></span>.<a id="id488288" class="indexterm" href=""></a></p>
    <div class="sect2" id="_selectors">

      <div class="titlepage">

          <h3 class="title">Selectors</h3>

        </div>

      </div>
   <p class="it">D3 utiliza selectores de estilo CSS para identificar elementos en los que operar, por lo que es importante entender cómo usarlos.</p>
      <p class="p" id="d_uses_csssty">D3 uses CSS-style selectors to identify elements on which to operate, so it’s important to understand how to use them.</p>
   

 <p class="it">Los selectores son para identificar elementos específicos a los que se aplicarán los estilos. Hay varios tipos diferentes de selectores. Usaremos sólo los más simples en este libro.</p>
      <p class="p" id="selectors_ident">Selectors identify specific elements to which styles will be applied. There are several different kinds of selectors. We’ll use only the simplest ones in this book.</p>
     


      <div class="variablelist" id="type_selectors_">

        <dl class="variablelist">

          <dt><span class="term"> Type selectors </span></dt>
<dd>Estos son los más sencillos. Coinciden con los elementos DOM con el mismo nombre: </dd>
          <dd> These are the simplest. They match DOM elements with the same<a id="id488326" class="indexterm" href=""></a> name: </dd>
          
        </dl>

      </div>

      <pre class="programlisting" data-language="css" id="h__selects_a">h1          /* Selects all level 1 headings           */
p           /* Selects all paragraphs                 */
strong      /* Selects all strong elements            */
em          /* Selects all em elements                */
div         /* Selects all divs                       */</pre>

      <div class="variablelist" id="descendant_sele">

        <dl class="variablelist">

          <dt><span class="term"> Descendant selectors </span></dt>
<dd class="it">Estos elementos están contenidos por (o "descienden de") otro elemento. Vamos a depender en gran medida de los selectores de descendientes para aplicar estilos:</dd>
          <dd> These match elements that are contained by (or “descended from”) another element. We will rely heavily on descendant<a id="id488404" class="indexterm" href=""></a> selectors to apply styles: </dd>

        </dl>

      </div>

      <pre class="programlisting" data-language="css" id="h_em__select">h1 em       /* Selects em elements contained in an h1 */
div p       /* Selects p elements contained in a div  */</pre>

      <div class="variablelist" id="class_selectors">

        <dl class="variablelist">

          <dt><span class="term"> Class selectors </span></dt>
<dd class="it">selectores de clase estos elementos los partidos de cualquier tipo que se haya asignado una específico clase. Los nombres de clase, van precedidos por un período, como se muestra aquí:</dd>
          <dd> These match elements of any type that have been assigned a<a id="id488460" class="indexterm" href=""></a> specific class. Class names are preceded with a period, as shown here: </dd>
          

        </dl>

      </div>

            <pre class="programlisting" data-language="css" id="caption__sel">.caption    /* Selects elements with class "caption"  */
.label      /* Selects elements with class "label"    */
            /* Selecciona elementos de la class "label"    */
.axis       /* Selects elements with class "axis"     */
            /* Selecciona elementos de la class "axis"    */</pre>
<p class="it">Puesto que los elementos pueden tener más de un clase, puede orientar elementos con múltiples clases ensartando clases unidas, como en el codigo siguiente:</p>
      <p class="p" id="because_element">Because elements can have more than one class, you can target elements with multiple classes by stringing the classes together, as in the following:</p>


      <pre class="programlisting" data-language="css" id="barhighlight_">.bar.highlight  /* Could target highlighted bars      */
.axis.x         /* Could target an x-axis             */
.axis.y         /* Could target a y-axis              */</pre>

<p class="it">.axis se podría utilizar para aplicar estilos para ambos ejes, por ejemplo, mientras .axis.x se aplicará sólo al eje x.</p>
 <p class="p" id="axis_could_be_"><code class="literal">.axis</code> could be used to apply styles to both axes, for example, whereas <code class="literal">.axis.x</code> would apply only to the x-axis.</p>


      <div class="variablelist" id="id_selectors_th">

        <dl class="variablelist">

          <dt><span class="term"> ID selectors </span></dt>
<dd class="it">Estos coinciden con un solo elemento con un ID dado. (Recuerde, los ID se pueden utilizar sólo una vez en el DOM.) Los IDs son precedidos con un signo de numeral.</dd>
          <dd> These match the single element with a given ID. (Remember, IDs can be<a id="id488622" class="indexterm" href=""></a> used only once each in the DOM.) IDs are preceded with a hash mark. </dd>

        </dl>

      </div>

<p class="it">Los selectores se vuelven progresivamente más útiles cuando se combinan de diferentes maneras para apuntar a elementos específicos. Puede enlazar selectores en conjunto para obtener resultados muy específicos. Por ejemplo:</p>
      <p class="p" id="selectors_get_p">Selectors get progressively more useful as you combine them in different ways to target specific elements. You can string selectors together to get very specific results. For <span class="keep-together">example</span>:</p>

<p class="it">Recuerde, debido a que el DOM es dinámico, las clases y los identificadores se pueden agregar y quitar, por lo que las reglas CSS se aplican sólo en ciertos escenarios.</p>
      <p class="p" id="remember_becau">Remember, because the DOM is dynamic, classes and IDs can be added and removed, so you might have CSS rules that apply only in certain scenarios.</p>

      <p class="p" id="for_details_on_">For details on additional selectors, see the <a class="ulink" href="http://mzl.la/V27Mcr" target="_top">Mozilla Developer Network</a>.</p>
    <div class="sect2" id="_properties_and_values">

      <div class="titlepage">

          <h3 class="title">Properties and Values</h3>

        </div>

      </div>

<p class="it">Los grupos de pares de propiedad/valor acumulativamente forman los estilos:</p>
      <p class="p" id="groups_of_prope">Groups of property/value pairs cumulatively form the<a id="id488757" class="indexterm" href=""></a><a id="id488764" class="indexterm" href=""></a><a id="id488769" class="indexterm" href=""></a> styles:</p>

      <pre class="programlisting" data-language="css" id="margin_px_p">margin: 10px;
padding: 25px;
background-color: yellow;
color: pink;
font-family: Helvetica, Arial, sans-serif;</pre>

<p class="it">A riesgo de afirmar lo obvio, observe que cada propiedad espera un tipo diferente de información. el color requiere un color, el margen requiere una medida (aquí en px o píxeles), y etc.</p>
      <p class="p" id="at_the_risk_of_">At the risk of stating the obvious, notice that each property expects a different kind of information. <code class="literal">color</code> wants a color, <code class="literal">margin</code> requires a measurement (here in <code class="literal">px</code> or pixels), and so on.</p>

   <p class="it">Por cierto, los colores se pueden especificar en varios formatos diferentes:</p>
      <p class="p" id="by_the_way_col">By the way, colors can be specified in several different formats:</p>
 
      <div class="itemizedlist" id="named_colors_o_id1">

        <ul class="itemizedlist">

          <li class="p"> Named colors: <code class="literal">orange</code> </li>
<li class="it">Nombre de los colores: naranja</li>
          <li class="p"> Hex values: <code class="literal">#3388aa</code> or <code class="literal">#38a</code> </li>
<li class="it">Los valores hexadecimales: #3388aa  o  #38a</li>
          <li class="p"> RGB values: <code class="literal">rgb(10, 150, 20)</code> </li>
<li class="it">Valores RGB: rgb (10, 150, 20)</li>
          <li class="p"> RGB with alpha transparency: <code class="literal">rgba(10, 150, 20, 0.5)</code> </li>
<li class="it">RGB con transparencia alfa: RGBA (10, 150, 20, 0.5)</li>
        </ul>

      </div>

<p class="it">Puede encontrar una lista exhaustiva de las propiedades en línea; No intentaré enumerarlas aquí. En su lugar, sólo voy a introducir propiedades relevantes a medida que avanzamos.</p>
      <p class="p" id="you_can_find_ex">You can find <a class="ulink" href="https://developer.mozilla.org/en/CSS/CSS_Reference" target="_top">exhaustive lists of properties online</a>; I won’t try to list them here. Instead, I’ll just introduce relevant properties as we go.<a id="id488982" class="indexterm" href=""></a><a id="id488989" class="indexterm" href=""></a></p>

    <div class="sect2" id="_referencing_styles">

      <div class="titlepage">

          <h3 class="title">Referencing Styles</h3>

        </div>

      </div>

<p class="it">Hay tres formas comunes para aplicar las reglas de estilo CSS a su documento HTML.</p>
      <p class="p" id="there_are_three">There are three common ways to apply CSS style rules to your HTML document.<a id="id489037" class="indexterm" href=""></a><a id="id489044" class="indexterm" href=""></a></p>

      <div class="sect3" id="_embed_the_css_in_your_html">

        <div class="titlepage">

            <h4 class="title">Embed the CSS in your HTML.</h4>

          </div>

        </div>

<p class="it">Si incrusta reglas CSS en su documento HTML, puede mantener todo en un solo archivo. En el encabezado del documento se incluye todo el código CSS dentro de un elemento style.</p>
        <p class="p" id="if_you_embed_th">If you embed the CSS rules in your HTML document, you can keep everything in one file. In the document <code class="literal">head</code>, include all CSS code within a <code class="literal">style</code> element.</p>

        <pre class="programlisting" data-language="html" id="html_head__id1">&lt;html&gt;
    &lt;head&gt;
        &lt;style type="text/css"&gt;

            p {
                font-size: 24px;
                font-weight: bold;
                background-color: red;
                color: white;
            }

        &lt;/style&gt;
    &lt;/head&gt;
    &lt;body&gt;
        &lt;p&gt;If I were to ask you, as a mere paragraph, would you say that I
        have style?&lt;/p&gt;
    &lt;/body&gt;
&lt;/html&gt;</pre>

<p class="it">Esa página HTML con CSS se renderiza como se muestra en la Figura 3-5.</p>
        <p class="p" id="that_html_page_">That HTML page with CSS renders as shown in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch03.html#Rendering_of_an_embedded_CSS_rule" title="Figure 3-5. Rendering of an embedded CSS rule">Figure 3-5</a>.</p>
        <div class="figure" id="Rendering_of_an_embedded_CSS_rule">

          <div class="figure-contents">

            <div class="mediaobject">

              <img src="/static/KSnaJy9UI1-img3.png" alt="Rendering of an embedded CSS rule"/>

            </div>

          </div>
<p class="fig">Figura 3-5. Renderización de una regla CSS incrustada</p>
          <p class="fig">Figure 3-5. Rendering of an embedded CSS rule</p>


        </div>

        <p class="it">La inserción es la opción más sencilla, pero generalmente se prefieren mantener diferentes tipos de código (por ejemplo, HTML, CSS, JavaScript) en documentos separados.</p>
        <p class="p" id="embedding_is_th">Embedding is the simplest option, but I generally prefer to keep different kinds of code (for example, HTML, CSS, JavaScript) in separate documents.</p>
      


      <div class="sect3" id="_reference_an_external_stylesheet_from_the_html">

        <div class="titlepage">

          <div>

            <h4 class="title">Reference an external stylesheet from the HTML.</h4>

          </div>

        </div>

        </div>

        <p class="it">Para almacenar CSS fuera de su HTML, debe guardarlo en un archivo de texto plano con un sufijo Css, como style.css. A continuación, utilice un elemento de enlace en el encabezado del documento para hacer referencia al archivo CSS externo, así:</p> 

        <p class="p" id="to_store_css_ou">To store CSS outside of your HTML, save it in a plain-text file with a<a id="id489269" class="indexterm" href=""></a> <span class="emphasis"><em>.css</em></span> suffix, such as <span class="emphasis"><em>style.css</em></span>. Then use a <code class="literal">link</code> element in the document <code class="literal">head</code> to reference the external CSS file, like so:</p>
       <pre class="programlisting" data-language="html" id="html_head__id2">&lt;html&gt;
    &lt;head&gt;
        &lt;link rel="stylesheet" href="style.css"&gt;
    &lt;/head&gt;
    &lt;body&gt;
        &lt;p&gt;If I were to ask you, as a mere paragraph, would you say that
        I have style?&lt;/p&gt;
    &lt;/body&gt;
&lt;/html&gt;</pre>

<p class="it">Este ejemplo hace exactamente lo mismo que el ejemplo anterior.</p>
        <p class="p" id="this_example_re">This example renders exactly the same as the prior example.</p>



      <div class="sect3" id="_attach_inline_styles">

        <div class="titlepage">

          <div>
<h4 class="it">Coloque los estilos en línea.</h4>
            <h4 class="title">Attach inline styles.</h4>

          </div>

        </div>
      </div>
        
<p class="it">Un tercer método es adjuntar reglas de estilo en línea directamente a elementos en el HTML. Puede hacer esto añadiendo un atributo de estilo a cualquier elemento. A continuación, incluir las reglas CSS dentro de las comillas dobles. El resultado se muestra en la Figura 3-6.</p>
        <p class="p" id="a_third_method_">A third method is to attach style rules <span class="emphasis"><em>inline</em></span> directly to elements in<a id="id489386" class="indexterm" href=""></a> the HTML. You can do this by adding a <code class="literal">style</code> attribute to any element. Then include the CSS rules within the double quotation marks. The result is shown in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch03.html#Rendering_of_an_inline_CSS_rule" title="Figure 3-6. Rendering of an inline CSS rule">Figure 3-6</a>.</p>

        <pre class="programlisting" data-language="html" id="p_stylecolor">&lt;p style="color: blue; font-size: 48px; font-style: italic;"&gt;Inline styles
are kind of a hassle&lt;/p&gt;</pre>

        <div class="figure" id="Rendering_of_an_inline_CSS_rule">

          <div class="figure-contents">

            <div class="mediaobject">

              <img src="/static/KSnaJy9UI1-img4.png" alt="Rendering of an inline CSS rule"/>

            </div>

          </div>
<p class="fig">Figura 3-6. Renderización de una regla CSS en línea</p>
          <p class="fig">Figure 3-6. Rendering of an inline CSS rule</p>

        </div>

        <p class="it">Debido a que los estilos en línea se unen directamente a los elementos, no hay necesidad de selectores.</p>
        <p class="p" id="because_inline_">Because inline styles are attached directly to elements, there is no need for selectors.</p>

<p class="it">Los estilos en línea son desordenada y difícil de leer, pero son útiles para dar especial enlazado a un solo elemento, cuando esa información de estilo no tiene sentido en una hoja de estilo más grande. Vamos a aprender cómo aplicar estilos en línea mediante programación con D3 (que es mucho más fácil que escribir a mano, de uno a la vez).</p>

        <p class="p" id="inline_styles_a">Inline styles are messy and hard to read, but they are useful for giving special treatment to a single element, when that style information doesn’t make sense in a larger stylesheet. We’ll learn how to apply inline styles programmatically with D3 (which is much easier than typing them in by hand, one at a time).</p>



    <div class="sect2" id="_inheritance_cascading_and_specificity">

      <div class="titlepage">

          <h3 class="title">Inheritance, Cascading, and Specificity</h3>

        </div>

      </div>

      <p class="it">Muchas propiedades de estilo son heredadas por los descendientes de un elemento a menos que se especifique lo contrario. Por ejemplo, las reglas de estilo de este documento se aplican al div:</p>

      <p class="p" id="many_style_prop">Many style properties are <span class="emphasis"><em>inherited</em></span> by an element’s descendants unless otherwise specified. For example, this document’s style rule applies to<a id="id489476" class="indexterm" href=""></a><a id="id489484" class="indexterm" href=""></a> the <code class="literal">div</code>:</p>

      <pre class="programlisting" data-language="html" id="html_head__id3">&lt;html&gt;
    &lt;head&gt;
        &lt;title&gt;&lt;/title&gt;
        &lt;style type="text/css"&gt;

            div {
                background-color: red;
                font-size: 24px;
                font-weight: bold;
                color: white;
            }

        &lt;/style&gt;
    &lt;/head&gt;
    &lt;body&gt;
        &lt;p&gt;I am a sibling to the div.&lt;/p&gt;
        &lt;div&gt;
            &lt;p&gt;I am a descendant and child of the div.&lt;/p&gt;
        &lt;/div&gt;
    &lt;/body&gt;
&lt;/html&gt;</pre>

<p class="it">Sin embargo, cuando esta página se renderiza, las formas de presentación del <code class="literal">div</code> (fondo rojo, el texto en negrita, etc.) son heredados por el segundo párrafo, como se muestra en la Figura 3-7, ya que <code class="literal">p</code>  es un descendiente del estilo del <code class="literal">div</code>.</p>

      <p class="p" id="yet_when_this_p">Yet when this page renders, the styles intended for the <code class="literal">div</code> (red background, bold text, and so on) are <span class="emphasis"><em>inherited</em></span> by the second paragraph, as shown in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch03.html#Inherited_style" title="Figure 3-7. Inherited style">Figure 3-7</a>, because that <code class="literal">p</code> is a descendant of the styled <code class="literal">div</code>.</p>

      <div class="figure" id="Inherited_style">

        <div class="figure-contents">

          <div class="mediaobject">

            <img src="/static/KSnaJy9UI1-img5.png" alt="Inherited style"/>

          </div>

        </div>
<p class="fig">Figura 3-7. Hereda el estilo</p>
        <p class="fig">Figure 3-7. Inherited style</p>

      </div>

      <p class="it">La herencia es una gran característica de CSS, ya que los niños adoptan los estilos de sus padres. (Hay una metáfora en alguna parte.)</p>

      <p class="p" id="inheritance_is_">Inheritance is a great feature of CSS, as children adopt the styles of their parents. (There’s a metaphor in there somewhere.)</p>

<p class="it">Por último, una respuesta a la pregunta más apremiante del día: Por qué se llaman Cascading Style Sheets? Es porque selector corresponde en cascada desde la parte superior hacia abajo. Cuando más de un selector se aplica a un elemento, la regla general nueva anula la anterior. Por ejemplo, las siguientes reglas establecen el texto de todos los elementos de párrafo en el documento a ser azul con excepción de los que tienen la clase <code class="literal">highlight</code> aplicada, donde la letra es de color negro y tienen un fondo amarillo, como se muestra en la Figura 3-8. Las reglas para <code class="literal">p</code> se aplican primero, pero entonces las reglas para <code class="literal">p.highlight</code> tienen prioridad sobre las reglas específicas de <code class="literal">p</code> menores.</p>
      <p class="p" id="finally_an_ans">Finally, an answer to the most pressing question of the day: why are they called Cascading Style Sheets? It’s because selector matches cascade from the top down. When more than one selector applies to an element, the later rule generally overrides the earlier one. For<a id="id489739" class="indexterm" href=""></a><a id="id489746" class="indexterm" href=""></a> example, the following rules set the text of all paragraph elements in the document to be blue <span class="emphasis"><em>except</em></span> for those with the class of <code class="literal">highlight</code> applied, which will be black <span class="emphasis"><em>and</em></span> have a yellow background, as shown in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch03.html#CSS_cascading_and_inheritance_at_work" title="Figure 3-8. CSS cascading and inheritance at work">Figure 3-8</a>. The rules for <code class="literal">p</code> are applied first, but then the rules for <code class="literal">p.highlight</code> override the less specific <code class="literal">p</code> rules.</p>

      <pre class="programlisting" data-language="css" id="p__color_blue">p {
    color: blue;
}

p.highlight {
    color: black;
    background-color: yellow;
}</pre>

      <div class="figure" id="CSS_cascading_and_inheritance_at_work">

        <div class="figure-contents">

          <div class="mediaobject">

            <img src="/static/KSnaJy9UI1-img6.png" alt="CSS cascading and inheritance at work"/>

          </div>

        </div>
<p class="fig">Figura 3-8. Cascada CSS y la herencia en el trabajo</p>
        <p class="fig">Figure 3-8. CSS cascading and inheritance at work</p>

      </div>

          <p class="p" id="later_rules_gen">Later rules generally override earlier ones, but not always. The true logic has to do with the <span class="emphasis"><em>specificity</em></span> of each selector. The <code class="literal">p.highlight</code> selector would override the <code class="literal">p</code> rule even if it were listed first, simply because it is a more specific selector. If two selectors have the same specificity, then the later one will be applied.<a id="id489935" class="indexterm" href=""></a><a id="id489943" class="indexterm" href=""></a></p>
<p class="it">Normas posteriores prevalecen sobre las anteriores, pero no siempre. La lógica de verdad tiene que ver con la especificidad de cada selector. El selector <code class="literal">p.highlight</code> sería superpuesto por el selector <code class="literal">p</code>  aun cuando aparece en primer lugar, simplemente porque es un selector más específico. Si dos selectores tienen la misma especificidad, el que aparece más adelante será aplicado.</p>
 
<p class="it">Esta es una de las principales causas de confusión con CSS. Las reglas para calcular especificidades son inescrutables, y no se pueden cubrir aquí. Para ahorrarse dolores de cabeza más adelante, mantenga los selectores claros y fáciles de leer. Comience con selectores generales en la parte superior, y su forma de trabajo hasta los más específicos, y usted estará bien.</p>

      <p class="p" id="this_is_one_of_">This is one of the main causes of confusion with CSS. The rules for calculating specificity are inscrutable, and I won’t cover them here. To save yourself headaches later, keep your selectors clear and easy to read. Start with general selectors on top, and work your way down to more specific ones, and you’ll be all right.<a id="id489958" class="indexterm" href=""></a></p>

      <div class="" data-original-filename="3_tech_fundamentals.asciidoc" id="_javascript">

    <div class="titlepage">

        <h2 class="title">JavaScript</h2>

      </div>

    </div>

<p class="it">Javascript es el lenguaje de script que puede hacer a las páginas dinámicas mediante la manipulación del DOM después de que una página ya se ha cargado en el navegador. Como he mencionado anteriormente, llegar a conocer D3 es también un proceso de familiarización con JavaScript. Conviene ir más profundo a medida que avanzamos, pero lo de aquí es un adelanto para que pueda empezar.</p>    

    <p class="p" id="javascript_is_t">JavaScript is the scripting language that can make pages dynamic by manipulating the DOM after a page has already loaded in the browser. As I mentioned earlier, getting to know D3 is also a process of getting to know JavaScript. We’ll dig in deeper as we go, but here is a taste to get you started.<a id="ix_Java" class="indexterm" href=""></a></p>

    <div class="sect2" id="_hello_console">

      <div class="titlepage">

          <h3 class="title">Hello, Console</h3>

        </div>

      </div>

<p class="it">Normalmente, se escribe código JavaScript (o, un "script") en un archivo de texto, y luego se carga el archivo al navegador en una página web. Pero también puede simplemente escribir código JavaScript directamente en su navegador. Esta es una manera fácil y rápida de mojarse los pies y probar código. También utilizamos la consola de JavaScript para la depuración, ya que es una herramienta esencial para ver lo que está pasando con su código.</p>

      <p class="p" id="normally_we_wr">Normally, we write JavaScript code (or, a “script”) in a text file, and then load that file to the browser in a web page. But you can also just type JavaScript code directly into your browser. This is an easy and quick way to get your feet wet and test out code. We’ll also use the JavaScript console for debugging, as it’s an essential tool for seeing what’s going on with your code.<a id="id490006" class="indexterm" href=""></a></p>

      



<p class="it">En Chrome, seleccione Ver → → desarrollador Consola JavaScript. En Firefox, seleccione Herramientas → → Web Developer Web Console. En Safari, vaya a Desarrollar → Mostrar la Consola de errores (véase la Figura 3-9).</p>


      <p class="p" id="in_chrome_sele">In Chrome, select View→Developer→JavaScript Console. In Firefox, choose Tools→Web Developer→Web Console. In Safari, go to Develop→Show Error Console (see <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch03.html#A_fresh_JavaScript_console" title="Figure 3-9. A fresh JavaScript console… delicious!">Figure 3-9</a>).</p>

      <div class="figure" id="A_fresh_JavaScript_console">

        <div class="figure-contents">

          <div class="mediaobject">

            <img src="/static/KSnaJy9UI1-img7.png" alt="A fresh JavaScript console… delicious!"/>

          </div>
</div>
        </div>
<p class="fig">Figura 3-9. Una consola de JavaScript fresca ... deliciosa!</p>
        <p class="fig">Figure 3-9. A fresh JavaScript console… delicious!</p>
  <p class="it">La consola acepta una línea de código a la vez, y siempre devuelve el resultado de lo que ingresa. Por ejemplo, si se introduce el número 7, la consola devuelve el resultado abrumadoramente evidente de 7. Brillante.</p>

      <p class="p" id="the_console_acc">The console accepts one line of code at a time, and it always spits back the result of whatever you input. For example, if you enter the number <code class="literal">7</code>, the console returns the mind-numbingly obvious result of <code class="literal">7</code>. Brilliant.</p>

<p class="it">Otras veces, usted querrá la secuencia de comandos para imprimir los valores en la consola de forma automática, para que pueda mantener un ojo en lo que está pasando. Como se verá en algunos ejemplos que siguen, se puede utilizar console.log ("algo para imprimir"); Para hacer eso.</p>

      <p class="p" id="other_times_yo">Other times, you’ll want your script to print values out to the console automatically, so you can keep an eye on what’s going on. As you’ll see in some examples that follow, you can use <code class="literal">console.log("something");</code> to do that.</p>
    <div class="sect2" id="_variables">

      <div class="titlepage">


          <h3 class="title">Variables</h3>

        </div>

      </div>
      <p class="it">Las variables son contenedores para datos. Una variable simple tiene un valor:</p>
      <p class="p" id="variables_are_c">Variables are containers for data. A simple variable holds one value:</p>

      <pre class="programlisting" data-language="javascript" id="var_number__">var number = 5;</pre>

<p class="it">En esa declaración, var indica que se está declarando una nueva variable, cuyo nombre es el <code class="literal">número</code>. El signo igual es un operador de asignación, ya que toma el valor <code class="literal">(5)</code> de la derecha y lo asigna a la variable de la izquierda <code class="literal">(número)</code>. Así que cuando usted ve algo como:</p>

      <p class="p" id="in_that_stateme">In that statement, <code class="literal">var</code> indicates you are declaring a new variable, the name of which is <code class="literal">number</code>. The equals sign is an<a id="id490148" class="indexterm" href=""></a> <span class="emphasis"><em>assignment operator</em></span> because it takes the value on the right (<code class="literal">5</code>) and <span class="emphasis"><em>assigns</em></span> it to the variable on the left (<code class="literal">number</code>). So when you see something such as:</p>

      <pre class="programlisting" data-language="javascript" id="defaultcolor__">defaultColor = "hot pink";</pre>

<p class="it">Trate de leer el signo de igualdad no como "iguales", sino como "está ajustado a". Así que la declaración podría ser "La variable <code class="literal">defaultColor</code> se establece en rosa fuerte".</p>

      <p class="p" id="try_to_read_the">try to read the equals sign not as “equals” but as “is set to.” So that statement could be stated in plain English as “The variable <code class="literal">defaultColor</code> <span class="emphasis"><em>is set to</em></span> hot pink.”</p>

<p class="it">Como usted acaba de ver, las variables pueden almacenar valores numéricos, así como cadenas de texto, llamados así porque se forman por encadenar caracteres de texto individuales. Las cadenas deben estar encerradas entre comillas. Los valores true o false (booleano) también se pueden almacenar:</p>

      <p class="p" id="as_youve_just_">As you’ve just seen, variables can store numeric values as well as strings of text, so called because they are formed by stringing together individual characters of text. Strings must be enclosed by quotation marks. True or false (Boolean) values can also be stored:</p>

      <pre class="programlisting" data-language="javascript" id="var_thismakesse">var thisMakesSenseSoFar = true;</pre>

      <p class="p" id="also_note_that__id1">Also note that in JavaScript, statements are concluded with a semicolon.</p>
<p class="it">También tenga en cuenta que en JavaScript, las declaraciones se concluyen con un punto y coma.</p>
 
<p class="it">Usted puede intentar hacer algunas variables para sí mismo en la consola. Por ejemplo, <code class="literal">var cantidad = 200</code>, a continuación, pulse enter, a continuación, en una nueva línea sólo tiene que introducir <code class="literal">cantidad</code> y pulse Intro. Debería ver 200 que le devolverá a usted la consola - una prueba de que JavaScript ha recordado el valor que ha asignado a "continuación"!</p>

      <p class="p" id="you_can_try_mak">You can try making some variables yourself in the console. For example, type <code class="literal">var amount = 200</code>, then press Enter, then on a new line just enter <code class="literal">amount</code> and press Enter. You should see <code class="literal">200</code> returned to you in the console—proof that JavaScript remembered the value you assigned to <code class="literal">amount</code>!</p>

    <div class="sect2" id="_other_variable_types">

      <div class="titlepage">

          <h3 class="title">Other Variable Types</h3>

        </div>

      </div>

 
<p class="it">Una variable es un dato, el bloque de construcción más pequeño de datos. La variable es la base de todas las demás estructuras de datos, que son simplemente diferentes configuraciones de las variables.</p>

      <p class="p" id="a_variable_is_a">A variable is a datum, the smallest building block of data. The variable is the foundation of all other data structures, which are simply different configurations of variables.</p>


<p class="it">Ahora vamos a tratar algunas de estas formas más complejas de datos, incluidos los arrays, objetos y arrays de objetos. Es posible que desee omitir esta sección por ahora, pero hacer referencia a ella más tarde, una vez que esté listo para cargar sus propios datos en D3.</p>

      <p class="p" id="now_well_addre">Now we’ll address some of these more complex forms of data, including arrays, objects, and arrays of objects. You might want to skip this section for now, but reference it later, once you’re ready to load your own data into D3.</p>

  

    <div class="sect2" id="_arrays">

      <div class="titlepage">


          <h3 class="title">Arrays</h3>

        </div>

      </div>

<p class="it">Una array es una secuencia de valores, convenientemente almacenada en una sola variable.</p>

      <p class="p" id="an_array_is_a_s">An array is a sequence of values, conveniently stored in a single variable.<a id="id490355" class="indexterm" href=""></a><a id="id490363" class="indexterm" href=""></a></p>

<p class="it">Hacer un seguimiento de los valores relativos de las variables independientes es ineficiente:</p>
      <p class="p" id="keeping_track_o">Keeping track of related values in separate variables is inefficient:</p>

      <pre class="programlisting" data-language="javascript" id="var_numbera__">var numberA = 5;
var numberB = 10;
var numberC = 15;
var numberD = 20;
var numberE = 25;</pre>

<p class="it">Reescritos como un array, esos valores son mucho más simples. Los corchetes <code class="literal">[]</code> indican un array, y cada valor está separado por una coma:</p>

      <p class="p" id="rewritten_as_an">Rewritten as an array, those values are much simpler. Hard brackets <code class="literal">[]</code> indicate an array, and each value is separated by a comma:</p>

      <pre class="programlisting" data-language="javascript" id="var_numbers___id1">var numbers = [ 5, 10, 15, 20, 25 ];</pre>

<p class="it">Las arrays son omnipresentes en la visualización de datos, por lo que llegará a estar muy cómodo con ellos. Puede acceder (recuperar) un valor en un array utilizando notación de corchetes:</p>

      <p class="p" id="arrays_are_ubiq">Arrays are ubiquitous in data visualization, so you will become very comfortable with them. You can access (retrieve) a value in an array by using <span class="emphasis"><em>bracket notation</em></span>:</p>

      <pre class="programlisting" data-language="javascript" id="numbers_re_id1">numbers[2]  //Returns 15</pre>

<p class="it">El numeral entre parentesis se refiere a una posición correspondiente en el array. Recuerde, las posiciones del array empiezan a contarse desde cero, por lo que la primera posición es 0, la segunda posición es 1, y así sucesivamente:</p>

      <p class="p" id="the_numeral_in_">The numeral in the bracket refers to a corresponding position in the array. Remember, array positions begin counting at zero, so the first position is 0, the second position is 1, and so on:</p>

      <pre class="programlisting" data-language="javascript" id="numbers_re_id2">numbers[0]  //Returns 5
numbers[1]  //Returns 10
numbers[2]  //Returns 15
numbers[3]  //Returns 20
numbers[4]  //Returns 25</pre>

<p class="it">A algunas personas les resulta útil pensar en los arrays en términos espaciales, como si tuvieran filas y columnas, como en una hoja de cálculo:</p>
      <p class="p" id="some_people_fin">Some people find it helpful to think of arrays in spatial terms, as though they have rows and columns, like in a spreadsheet:</p>

     <div class="informaltable" id="position_value">

        <table> <colgroup> <col class="col_1"/> <col class="col_2"/> </colgroup> <thead><tr> <td>Position </td> <td> Value</td> </tr></thead> <tbody> <tr> <td>

        <p class="p" id="simpara_id1">0</p></td> <td>

        <p class="p" id="simpara_id2">5</p></td> </tr> <tr> <td>

       <p class="p" id="simpara_id3">1</p></td> <td>

       <p class="p" id="simpara_id4">10</p></td> </tr> <tr> <td>

        <p class="p" id="simpara_id5">2</p></td> <td>

        <p class="p" id="simpara_id6">15</p></td> </tr> <tr> <td>

        <p class="p" id="simpara_id7">3</p></td> <td>

        <p class="p" id="simpara_id8">20</p></td> </tr> <tr> <td>

        <p class="p" id="simpara_id9">4</p></td> <td>

        <p class="p" id="simpara_id10">25</p></td> </tr> </tbody> </table>

      </div>

<p class="it">Las arrays pueden contener cualquier tipo de datos, no simplemente enteros:</p>
      <p class="p" id="arrays_can_cont">Arrays can contain any type of data, not just integers:</p>

      <pre class="programlisting" data-language="javascript" id="var_percentages">var percentages = [ 0.55, 0.32, 0.91 ];
var names = [ "Ernie", "Bert", "Oscar" ];

percentages[1]  //Returns 0.32
names[1]        //Returns "Bert"</pre>

<p class="it">Incluso aunque yo no lo recomiendo, diferentes tipos de valores, se pueden almacenar en el mismo array:</p>
      <p class="p" id="although_i_don">Although I don’t recommend it, different types of values can even be stored within the same array:</p>

      <pre class="programlisting" data-language="javascript" id="var_mishmash__">var mishmash = [ 1, 2, 3, 4.5, 5.6, "oh boy", "say it isn't", true ];</pre>

    

    <div class="sect2" id="_objects">

      <div class="titlepage">


          <h3 class="title">Objects</h3>

        </div>
</div>
      

<p class="it">Las arrays son simplemente grandes listas de valores, pero con conjuntos de datos más complejos, que quieren poner sus datos en un objeto. Para nuestros propósitos, conviene pensar en un objeto JavaScript como una estructura de datos. Utilizamos entre llaves <code class="literal">{}</code> para indicar un objeto. En medio de las llaves, incluimos propiedades y valores. Los dos puntos: separa cada propiedad y su valor, y una coma separa cada par de propiedad / valor:</p>

      <p class="p" id="arrays_are_grea">Arrays are great for simple lists of values, but with more complex datasets, you’ll want to put your data into an object. For our purposes, think of a JavaScript object as a custom data structure. We use curly brackets <code class="literal">{}</code> to indicate an object. In between the brackets, we include<a id="id491168" class="indexterm" href=""></a><a id="id491173" class="indexterm" href=""></a><a id="id491179" class="indexterm" href=""></a><a id="id491187" class="indexterm" href=""></a> <span class="emphasis"><em>properties</em></span> and <span class="emphasis"><em>values</em></span>. A colon <code class="literal">:</code> separates each property and its value, and a comma separates each property/value pair:</p>

      <pre class="programlisting" data-language="javascript" id="var_fruit___k">var fruit = {
    kind: "grape",
    color: "red",
    quantity: 12,
    tasty: true
};</pre>

<p class="it">Para hacer referencia a cada valor, se utiliza el punto, especificando el nombre de la propiedad:</p>
      <p class="p" id="to_reference_ea">To reference each value, we use <span class="emphasis"><em>dot notation</em></span>, specifying the name of the property:</p>

      <pre class="programlisting" data-language="javascript" id="fruitkind_re">fruit.kind      //Returns "grape"
fruit.color     //Returns "red"
fruit.quantity  //Returns 12
fruit.tasty     //Returns true</pre>

   
<p class="it">Oh, mira, un poco de fruta. "¿Qué tipo de fruta es esa?" Usted puede pedir. Pues resulta que, fruit.kind es "uva". "¿Son sabrosas?" Oh, definitivamente, porque fruit.tasty es true.</p>
      <p class="p" id="think_of_the_va">Think of the value as “belonging” to the object. Oh, look, some fruit. “What kind of fruit is that?” you might ask. As it turns out, <code class="literal">fruit.kind</code> is <code class="literal">"grape"</code>. “Are they tasty?” Oh, definitely, because <code class="literal">fruit.tasty</code> is <code class="literal">true</code>.</p>


    <div class="sect2" id="_objects_and_arrays">

      <div class="titlepage">


          <h3 class="title">Objects and Arrays</h3>

        </div>

      </div>

<p class="it">Puede combinar en sí dos estructuras para crear arrays de objetos u objetos de arrays u objetos de los objetos o, bueno, básicamente, cualquier estructura tiene sentido para el conjunto de datos.</p>
      <p class="p" id="you_can_combine">You can combine these two structures to create arrays of objects, or objects of arrays, or objects of objects or, well, basically whatever structure makes sense for your dataset.<a id="id491462" class="indexterm" href=""></a><a id="id491470" class="indexterm" href=""></a></p>

<p class="it">Diremos que hemos adquirido un par de piezas de fruta, y queremos, en consecuencia, ampliar nuestro catálogo. Utilizamos corchetes [] en el exterior, para indicar un array, seguido de llaves <code class="literal">{}</code> y la anotación del objeto en el interior, con cada objeto separados por una coma:</p>
      <p class="p" id="lets_say_we_ha">Let’s say we have acquired a couple more pieces of fruit, and we want to expand our catalog accordingly. We use hard brackets <code class="literal">[]</code> on the outside, to indicate an array, followed by curly brackets <code class="literal">{}</code> and object notation on the inside, with each object separated by a comma:</p>

      <pre class="programlisting" data-language="javascript" id="var_fruits___">var fruits = [
    {
        kind: "grape",
        color: "red",
        quantity: 12,
        tasty: true
    },
    {
        kind: "kiwi",
        color: "brown",
        quantity: 98,
        tasty: true
    },
    {
        kind: "banana",
        color: "yellow",
        quantity: 0,
        tasty: true
    }
];</pre>

<p class="it">Para acceder a estos datos, sólo tienes que seguir el rastro de las propiedades a los valores que queremos. Recuerde, <code class="literal">[]</code>  significa array, y <code class="literal">{}</code> <code class="literal">significa objeto. class="literal"&gt;fruits</code>  es un array, por lo que primero se utiliza notación de corchetes para especificar un índice de array:</p>
      <p class="p" id="to_access_this_">To access this data, we just follow the trail of properties down to the values we want. Remember, <code class="literal">[]</code> means array, and <code class="literal">{}</code> means object. <code class="literal">fruits</code> is an array, so first we use bracket notation to specify an array index:</p>

      <pre class="programlisting" data-language="javascript" id="fruits">fruits[1]</pre>

<p class="it">A continuación, cada elemento de la array es un objeto, por lo que sólo tachuela en un punto y una propiedad:</p>
      <p class="p" id="next_each_arra">Next, each array element is an object, so just tack on a dot and a property:</p>

      <pre class="programlisting" data-language="javascript" id="fruitsquant">fruits[1].quantity   //Returns 98</pre>

<p class="it"> Este es un mapa de cómo acceder a todos los valores de la array de objetos <code className = "literal"> fruits </code>:</p>

      <p class="p" id="heres_a_map_of">Here’s a map of how to access every value in the <code class="literal">fruits</code> array of objects:</p>

      <pre class="programlisting" data-language="javascript" id="fruitskind_">fruits[0].kind      ==  "grape"
fruits[0].color     ==  "red"
fruits[0].quantity  ==  12
fruits[0].tasty     ==  true

fruits[1].kind      ==  "kiwi"
fruits[1].color     ==  "brown"
fruits[1].quantity  ==  98
fruits[1].tasty     ==  true

fruits[2].kind      ==  "banana"
fruits[2].color     ==  "yellow"
fruits[2].quantity  ==  0
fruits[2].tasty     ==  true</pre>

      <p class="p" id="yes_thats_rig">Yes, that’s right, we have <code class="literal">fruits[2].quantity</code> bananas.</p>

      <div class="sect3" id="_json">

        <div class="titlepage">

            <h4 class="title">JSON</h4>

          </div>

        </div>

<p class="it">En algún momento de su carrera en D3, se encontrará con JavaScript Object Notation. Puede leer sobre los detalles, pero JSON es básicamente una sintaxis específica para organizar los datos como objetos de JavaScript. La sintaxis está optimizada para su uso con JavaScript (obviamente) y peticiones AJAX, por lo que verá un montón de interfaces de software basadas en la Web (API) que devuelven datos con formato JSON. Es más rápido y más fácil de analizar con JavaScript de XML, y por supuesto D3 funciona bien con ella.</p>

        <p class="p" id="at_some_point_i">At some point in your D3 career, you will encounter JavaScript Object Notation. You can <a class="ulink" href="http://en.wikipedia.org/wiki/Json" target="_top">read up on the details</a>, but JSON is basically a specific syntax for organizing data as JavaScript objects. The syntax is optimized for use with JavaScript (obviously) and AJAX requests, which is why you’ll see a lot of <span class="keep-together">web-based</span> application programming interfaces (APIs) that return data formatted as JSON. It’s faster and easier to parse with JavaScript than XML, and of course D3 works well with it.<a id="id492336" class="indexterm" href=""></a><a id="id492344" class="indexterm" href=""></a></p>

<p class="it">Esto es, parece mucho más raro que lo que hemos visto ya:</p>

        <p class="p" id="all_that_and_i">All that, and it doesn’t look much weirder than what we’ve already seen:</p>

        <pre class="programlisting" data-language="javascript" id="kind_grap">{
    "kind": "grape",
    "color": "red",
    "quantity": 12,
    "tasty": true
}</pre>

<p class="it">La única diferencia aquí es que nuestros nombres de las propiedades están rodeados por comillas "", dando los valores del string</p>
        <p class="p" id="the_only_differ">The only difference here is that our property names are now surrounded by double quotation marks <code class="literal">""</code>, making them string values.</p>

<p class="it">Los objetos JSON, al igual que todos los demás objetos de JavaScript, pueden por supuesto ser almacenados en las variables, así:</p>
        <p class="p" id="json_objects_l">JSON objects, like all other JavaScript objects, can of course be stored in variables like so:</p>

        <pre class="programlisting" data-language="javascript" id="var_jsonfruit_">var jsonFruit = {
    "kind": "grape",
    "color": "red",
    "quantity": 12,
    "tasty": true
};</pre>


      <div class="sect3" id="_geojson">

        <div class="titlepage">

            <h4 class="title">GeoJSON</h4>

          </div>

        </div>

<p class="it">Así como JSON es sólo una formalización de sintaxis de objetos JavaScript existente, GeoJSON es una sintaxis formal de objetos JSON, optimizado para el almacenamiento de datos geográficos. Todo objeto GeoJSON es objeto JSON, y todos los objetos JSON son objetos JavaScript.</p>

        <p class="p" id="just_as_json_is">Just as JSON is just a formalization of existing JavaScript object syntax, <span class="keep-together">GeoJSON</span> is a formalized syntax of JSON objects, optimized for storing geodata. All GeoJSON object are JSON objects, and all JSON objects are JavaScript objects.<a id="id492597" class="indexterm" href=""></a><a id="id492606" class="indexterm" href=""></a></p>

   
<p class="it">GeoJSON no solo puede almacenar puntos en el espacio geográfico (por lo general como coordenadas de longitud / latitud), sino que también da forma (por ejemplo, líneas y polígonos) y otras características espaciales. Si usted tiene una gran cantidad de datos geográficos, vale la pena analizar usar el formato GeoJSON para su mejor uso con D3.</p>

        <p class="p" id="geojson_can_sto"><a class="ulink" href="http://geojson.org/geojson-spec.html" target="_top">GeoJSON</a> can store points in geographical space (typically as longitude/latitude coordinates), but also shapes (such as lines and polygons) and other spatial features. If you have a lot of geodata, it’s worth it to parse it into GeoJSON format for best use with D3.</p>

<p class="it">No vamos a entrar en los detalles de GeoJSON cuando hablamos de geomaps, pero por ahora, sólo sabemos que los simples datos de GeoJSON podrían tener el siguiente aspecto:</p>
        <p class="p" id="well_get_into_">We’ll get into the details of GeoJSON when we talk about geomaps, but for now, just know that this is what simple GeoJSON data could look like the following:</p>

        <pre class="programlisting" data-language="javascript" id="type_feat_id1">{
    "type": "FeatureCollection",
    "features": [
        {
            "type": "Feature",
            "geometry": {
                "type": "Point",
                "coordinates": [ 150.1282427, -24.471803 ]
            },
            "properties": {
                "type": "town"
            }
        }
    ]
}</pre>

<p class="it">Confusamente, longitud aparece siempre antes de latitud. Hay que acostumbrarse a pensar en términos de lon / lat en lugar de lat / lon.</p>
        <p class="p" id="confusingly_lo">Confusingly, longitude is always listed before latitude. Get used to thinking in terms of lon/lat instead of lat/lon.</p>

       
            <div class="sect2" id="_mathematical_operators">

      <div class="titlepage">


          <h3 class="title">Mathematical Operators</h3>

        </div>

      </div>

<p class="it">Puede sumar, restar, multiplicar y dividir los valores utilizando los siguientes operadores, respectivamente:</p>

      <p class="p" id="you_can_add_su">You can add, subtract, multiply, and divide values using the following<a id="id492857" class="indexterm" href=""></a><a id="id492864" class="indexterm" href=""></a> operators, <span class="keep-together">respectively</span>:</p>

      <pre class="screen" id="add__sub">+   //Add
-   //Subtract
*   //Multiply
/   //Divide</pre>

<p class="it">Por ejemplo Introdusca 8 * 2 en la consola, presione enter, y debería ver 16. Más ejemplos:</p>

      <p class="p" id="for_example_ty">For example, type <code class="literal">8 * 2</code> into the console, press Enter, and you should see <code class="literal">16</code>. More examples:</p>

      <pre class="programlisting" data-language="javascript" id="__returns">1 + 2       //Returns 3
10 - 0.5    //Retuns 9.5
33 * 3      //Returns 99
3 / 4       //Returns 0.75</pre>


    <div class="sect2" id="_comparison_operators">

      <div class="titlepage">

          <h3 class="title">Comparison Operators</h3>

        </div>

      </div>

<p class="it">Puede comparar los valores de uno contra el otro mediante los siguientes operadores:</p>
      <p class="p" id="you_can_compare">You can compare values against each other using the following<a id="id493012" class="indexterm" href=""></a><a id="id493020" class="indexterm" href=""></a> operators:</p>

      <pre class="programlisting" data-language="javascript" id="equal_to_">==  //Equal to
!=  //Not equal to
&lt;   //Less than
&gt;   //Greater than
&lt;=  //Less than or equal to
&gt;=  //Greater than or equal to</pre>

 
<p class="it">Todos ellos comparan algún valor de la izquierda con algún valor a la derecha. Si el resultado es verdadero, entonces se devuelve true. Si el resultado es falso, se devuelve false.</p> 
      <p class="p" id="these_all_compa">These all compare some value on the left to some value on the right. If the result is true, then <code class="literal">true</code> is returned. If the result is false, <code class="literal">false</code> is returned.</p>

<p class="it">¡Intentelo! Escriba cada una de las acciones siguientes en la consola y vera lo que hay:</p>

      <p class="p" id="try_it_type_ea">Try it! Type each of the following into the console and see what you get:</p>

      <pre class="programlisting" data-language="javascript" id="______id1">3 == 3
3 == 5
3 &gt;= 3
3 &gt;= 2
100 &lt; 2
298 != 298</pre>

 
<p class="it">(JavaScript también ofrece los Operadores === y! == , que realizan comparaciones de igualdad sin coacción pero no explicaré esa distinción en en este libro.)</p>
      <p class="p" id="javascript_als">(JavaScript also offers the <code class="literal">===</code> and <code class="literal">!==</code> operators, which perform equality comparisons without type coercion, but I won’t be addressing that distinction in this book.)</p>



    <div class="sect2" id="_control_structures">

      <div class="titlepage">

<p class="it">Estructuras de Control</p>
          <h3 class="title">Control Structures</h3>

        </div>

      </div>

<p class="it">Siempre que el código necesita para tomar una decisión o repetir algo, se necesita una estructura de control. Hay mucho para elegir, pero estamos principalmente interesados en las declaraciones <code class="literal">if</code> y los bucles <code class="literal">for</code>.</p>
      <p class="p" id="whenever_your_c">Whenever your code needs to make a decision or repeat something, you need a control structure. There are lots to choose from, but we are primarily interested in <code class="literal">if</code> statements and <code class="literal">for</code> loops.<a id="id493381" class="indexterm" href=""></a><a id="id493389" class="indexterm" href=""></a><a id="id493395" class="indexterm" href=""></a></p>

      <div class="sect3" id="_if_only">

        <div class="titlepage">

            <h4 class="title">if() only</h4>

          </div>

        </div>

<p class="it">Una sentencia if utiliza operadores de comparación para determinar si una afirmación es verdadera o falsa:</p>
        <p class="p" id="an_if_statement">An <code class="literal">if</code> statement uses comparison operators to determine if a statement is true or false:</p>

        <pre class="programlisting" data-language="javascript" id="if_test__c">if (test) {
    //Code to run if true
}</pre>

<p class="it">Si la prueba entre paréntesis es true, entonces el código entre las llaves se ejecuta. Si la prueba se convierte en falsa, entonces el código entre corchetes se ignora, y la vida sigue. (Técnicamente, la vida continúa en ambos sentidos).</p>
        <p class="p" id="if_the_test_bet">If the test between parentheses is <code class="literal">true</code>, then the code between the curly brackets is run. If the test turns up <code class="literal">false</code>, then the bracketed code is ignored, and life goes on. (Technically, life goes on either way.)</p>

        <pre class="programlisting" data-language="javascript" id="if_____co">if (3 &lt; 5) {
    console.log("Eureka! Three is less than five!");
}</pre>

<p class="it">En el ejemplo anterior, el código entre corchetes siempre se ejecuta, porque <code class="literal">3 &lt; 5</code> es siempre true. Las declaraciones son más útiles cuando se comparan las variables u otras condiciones que pueden cambiar.</p>
        <p class="p" id="in_the_precedin">In the preceding example, the bracketed code will always be executed, because <code class="literal">3 &lt; 5</code> is always true. <code class="literal">if</code> statements are more useful when comparing variables or other conditions that change.</p>

        <pre class="programlisting" data-language="javascript" id="if_somevalue_">if (someValue &lt; anotherValue) {
    //Set someValue to anotherValue, thereby restoring
    //a sense of balance and equilibrium to the world.
    someValue = anotherValue;
}</pre>

 

      <div class="sect3" id="_for_now">

        <div class="titlepage">


            <h4 class="title">for() now</h4>

          </div>

        </div>

<p class="it">Puede utilizar el bucles <code class="literal">for</code> en repetidas ocasiones ejecutando el mismo código, con ligeras variaciones. Un bucle <code class="literal">for</code> utiliza esta sintaxis:</p>
        <p class="p" id="you_can_use_for">You can use <code class="literal">for</code> loops to repeatedly execute the same code, with slight<a id="id493677" class="indexterm" href=""></a> variations. A <code class="literal">for</code> loop uses this syntax:</p>

        <pre class="programlisting" data-language="javascript" id="for_initializa">for (initialization; test; update) {
    //Code to run each time through the loop
}</pre>


<p class="it">Ellos son los llamados porque bucle a través del código para el mayor número de veces especificado. En primer lugar, se ejecuta la instrucción de inicialización. A continuación, se evalúa la prueba, como un mini si comunicado. Si la prueba es verdadera, entonces el código entre corchetes se ejecuta. Por último, la declaración <code class="literal">update</code> se ejecuta, y la prueba se vuelve a evaluar.</p>
        <p class="p" id="they_are_socal">They are so-called because they loop through the code <span class="emphasis"><em>for</em></span> as many times as specified. First, the initialization statement is run. Then, the test is evaluated, like a mini <code class="literal">if</code> statement. If the test is true, then the bracketed code is run. Finally, the <code class="literal">update</code> statement is run, and the test is reevaluated.</p>

<p class="it">La aplicación más común de un bucle <code class="literal">for</code> es aumentar alguna variable en 1 cada vez a través del bucle. La aseveración de ensayo se puede controlar el número de veces que el ciclo está dirigido por referencia a ese valor. (La variable a menudo se denomina i, puramente por convención, porque es corto y fácil de escribir.)</p>
        <p class="p" id="the_most_common">The most common application of a <code class="literal">for</code> loop is to increase some variable by 1 each time through the loop. The test statement can then control how many times the loop is run by referencing that value. (The variable is often named <code class="literal">i</code>, purely by convention, because it is short and easy to type.)</p>

        <pre class="programlisting" data-language="javascript" id="for_var_i__">for (var i = 0; i &lt; 5; i++) {
    console.log(i);  //Prints value to console
}</pre>

<p class="it">El precedente bucle for imprime lo siguiente en la consola:</p>
        <p class="p" id="the_preceding_f">The preceding <code class="literal">for</code> loop prints the following to the console:</p>

        <pre class="screen" id="____id1">0
1
2
3
4</pre>

<p class="it">La primera vez thr ough, una variable denominada i se declara y pone a cero. i es inferior a cinco, por lo que el código entre corchetes se ejecuta, imprimir el valor actual de i (cero) a la consola. Por último, el valor de i se incrementa en uno. (i ++ es una abreviación para i = i + 1) Así que ahora i es 1, s o la prueba de nuevo evalúa como verdadera, el código entre corchetes se ejecute de nuevo, pero esta vez con el valor impreso en la consola es 1.</p>
        <p class="p" id="the_first_time_">The first time through, a variable named <code class="literal">i</code> is declared and set to zero. <code class="literal">i</code> is less than five, so the bracketed code is run, printing the current value of <code class="literal">i</code> (zero) to the console. Finally, the value of <code class="literal">i</code> is increased by one. (<code class="literal">i++</code> is shorthand for <code class="literal">i = i + 1</code>.) So now <code class="literal">i</code> is <code class="literal">1</code>, so the test again evaluates as true, the bracketed code is run again, but this time the value printed to the console is 1.</p>


<p class="it">Como se puede ver, leer las descripciones en prosa de los bucles son tan interesante como su ejecución a mano. Es por esto que inventamos ordenadores. Así que vamos a seguir señalando que después de la iteración final, i se incrementa a 5, después de lo cual la prueba devuelve false, y el bucle termina.</p>
        <p class="p" id="as_you_can_see_id1">As you can see, reading prose descriptions of loops is about as interesting as executing them by hand yourself. This is why we invented computers. So I’ll skip to the end and point out that after the final iteration, <code class="literal">i</code> is increased to 5, after which the test returns false, and the loop is over.</p>

<p class="it">Es  importante tener en cuenta que el conteo se inició a cero, y no uno. Es decir, el " primer " valor <code class="literal">i</code> was <code class="literal">0</code>¿Por qué no 1? Esta es otra convención arbitraria, pero muy bien cómo es paralelo a las computadoras cuentan arrays de valores.</p>

        <p class="p" id="its_important__id1">It’s important to note that counting began at zero, and not one. That is, the “first” value of <code class="literal">i</code> was <code class="literal">0</code>. Why not <code class="literal">1</code>? This is another arbitrary convention, but it nicely parallels how computers count arrays of values.</p>



      <div class="sect3" id="_what_arrays_are_made_for">

        <div class="titlepage">

            <h4 class="title">What arrays are made for()</h4>

          </div>

        </div>


 <p class="it">La visualización de datos basada en código no sería posible sin las arrays y los poderosos de bucles <code class="literal">for()</code>. Juntos, forman un  dúo dinámico geek de datos. (Si no se considera un " friki de datos," ¿le recuerdo que usted está leyendo un libro titulado Interactive Data Visualization for the Web ?)</p>
        <p class="p" id="codebased_data">Code-based data visualization would not be possible without arrays and the mighty <code class="literal">for()</code> loop. Together, they form a data geek’s dynamic duo. (If you do not consider yourself a “data geek,” then may I remind you that you are reading a book titled <span class="emphasis"><em>Interactive Data Visualization for the Web</em></span>?)<a id="id494059" class="indexterm" href=""></a><a id="id494067" class="indexterm" href=""></a></p>

<p class="it">Un array organiza un montón de valores de datos en un solo lugar. Entonces, <code class="literal">for()</code> puede rápidamente "loopear" a través de todos los valores de una array y realizar alguna acción con ello - como por ejemplo, expresar el valor como una forma visual. D3 a menudo gestiona este bucle para nosotros, como con el mágico método data().</p>
        <p class="p" id="an_array_organi">An array organizes lots of data values in one convenient place. Then <code class="literal">for()</code> can quickly “loop” through every value in an array and perform some action with it—such as, express the value as a visual form. D3 often manages this looping for us, such as with its magical <code class="literal">data()</code> method.</p>

<p class="it">Tenga en cuenta este ejemplo, lo que coloca a través de cada uno de los valores en una array llamado números:</p>
        <p class="p" id="note_this_examp">Note this example, which loops through each of the values in an array called <code class="literal">numbers</code>:</p>
      
        <pre class="programlisting" data-language="javascript" id="var_numbers___id2">var numbers = [ 8, 100, 22, 98, 99, 45 ];

for (var i = 0; i &lt; numbers.length; i++) {
    console.log(numbers[i]);  //Print value to console
}</pre>

<p class="it">Ver que numbers.length? Esa es la parte hermosa. longitud es una característica de cada array. En este caso, los números contiene seis valores, por lo numbers.length resuelve a 6, y el bucle se ejecuta seis veces. Si los números eran 10 posiciones de longitud, el ciclo se ejecuta 10 veces. Si se tratara de 10 millones de posiciones de largo ... sí, usted lo consigue. Esto es lo que los ordenadores son buenos en: tomar un conjunto de instrucciones y ejecutar una y otra vez. Y esto es en el corazón y la razón por la que la visualización de datos puede ser tan gratificante porque el diseño y el código del sistema de visualización, y el sistema va a responder de manera apropiada, incluso cuando le da de comer diferentes datos. Las reglas de asignación del sistema son consistentes, incluso cuando los datos no lo son.</p> 

        <p class="p" id="see_that_number">See that <code class="literal">numbers.length</code>? That’s the beautiful part. <code class="literal">length</code> is a property of every array. In this case, <code class="literal">numbers</code> contains six values, so <code class="literal">numbers.length</code> resolves to <code class="literal">6</code>, and the loop runs six times. If <code class="literal">numbers</code> were 10 positions long, the loop would run 10 times. If it were 10 million positions long … yeah, you get it. This is what computers are good at: taking a set of instructions and executing them over and over. And this is at the heart of why data visualization can be so rewarding—you design and code the visualization system, and the system will respond appropriately, even as you feed it different data. The system’s mapping rules are consistent, even when the data is not.</p>


    <div class="sect2" id="_functions">

      <div class="titlepage">

          <h3 class="title">Functions</h3>

        </div>

      </div>

 
<p class="it">Las funciones son trozos de código que pueden hacer las cosas.</p>
      <p class="p" id="functions_are_c">Functions are chunks of code that do things.</p>

<p class="it">Más específicamente, las funciones son especiales ya que pueden tomar argumentos o parámetros como entrada, y luego devolver valores como salida. Los paréntesis se utilizan para llamar (ejecutar) una función. Si esa función requiere un argumento (valores de entrada), a continuación se pasa a la función mediante su inclusión en los paréntesis.</p>
      <p class="p" id="more_specifical">More specifically, functions are special because they can take arguments or parameters as input, and then return values as output. Parentheses are used to <span class="emphasis"><em>call</em></span> (execute) a function. If that function requires any arguments (input values), then they are <span class="emphasis"><em>passed</em></span> to the function by including them in the parentheses.<a id="id494401" class="indexterm" href=""></a><a id="id494409" class="indexterm" href=""></a><a id="id494417" class="indexterm" href=""></a></p>

<p class="it">Cada vez que vea algo como el siguiente código, usted sabe que es una función:</p>
      <p class="p" id="whenever_you_se">Whenever you see something like the following code, you know it’s a function:</p>

      <pre class="programlisting" data-language="javascript" id="calculategratui_id1">calculateGratuity(38);</pre>

 
<p class="it">De hecho, ya vio funciones cuando trabajó con en <code class="literal">console.log</code>, como en el siguiente: </p>
      <p class="p" id="in_fact_youve">In fact, you’ve already seen functions at work with <code class="literal">console.log</code>, as in the following:</p>

      <pre class="programlisting" data-language="javascript" id="consoleloglo">console.log("Look at me. I can do stuff!");</pre>

<p class="it">console.log ( "Mírame Puedo hacer cosas.!"); Pero la mejor parte de las funciones es que puede definir su propia función. Hay varias maneras de definir funciones en JavaScript, pero aquí está la más simple, que usaré a lo largo de este libro: </p>
      <p class="p" id="but_the_best_pa">But the best part about functions is that you can define your own. There are several ways to define functions in JavaScript, but here’s the simplest, which I’ll use throughout this book:</p>

      <pre class="programlisting" data-language="javascript" id="var_calculategr">var calculateGratuity = function(bill) {
    return bill * 0.2;
};</pre>

<p class="it">Esto declara una nueva variable denominada calculateGratuity. Entonces, en lugar de asignar un número o una cadena sencilla, almacenamos una función entera en la variable. En los paréntesis, w factura nombre de correo, otra variable a ser utilizado sólo por la propia función. proyecto de ley es la entrada esperada. Cuando se le llama, la función se llevará a esa entrada, se multiplica por 0,2, y devolver el resultado como su salida.</p>
      <p class="p" id="this_declares_a">This declares a new variable named <code class="literal">calculateGratuity</code>. Then, instead of assigning a simple number or string, we store an entire function in the variable. In the parentheses, we name <code class="literal">bill</code>, another variable to be used only by the function itself. <code class="literal">bill</code> is the expected input. When called, the function will take that input, multiply it by <code class="literal">0.2</code>, and <span class="emphasis"><em>return</em></span> the result as its output.</p>

<p class="it">Así que ahora si llamamos:</p>
      <p class="p" id="so_now_if_we_ca">So now if we call:</p>

      <pre class="programlisting" data-language="javascript" id="calculategratui_id2">calculateGratuity(38);</pre>

<p class="it">la función devuelve 7.6. No está mal - una punta de 20 por ciento!</p>
      <p class="p" id="the_function_re">the function returns 7.6. Not bad—a 20 percent tip!</p>

<p class="it">Por supuesto, se podría almacenar la salida para usarlo en otro lugar más tarde, como en:</p>
      <p class="p" id="of_course_you__id1">Of course, you could store the output to use it elsewhere later, as in:</p>

      <pre class="programlisting" data-language="javascript" id="var_tip__calcu">var tip = calculateGratuity(38);
console.log(tip);  //Prints 7.6 to the console</pre>

<p class="it">También hay funciones anónimas  que, a diferencia de <code class="literal">calculateGratuity</code>, no tienen nombre. Las funciones anónimas se utilizan todo el tiempo con D3, pero yo lo introducire en este asunto más tarde.</p>
      <p class="p" id="there_are_also_">There are also <span class="emphasis"><em>anonymous</em></span> functions that, unlike <code class="literal">calculateGratuity</code>, don’t have names. Anonymous functions are used all the time with D3, but I’ll introduce them later.<a id="id494768" class="indexterm" href=""></a><a id="id494774" class="indexterm" href=""></a></p>


    <div class="sect2" id="_referencing_scripts">

      <div class="titlepage">

          <h3 class="title">Referencing Scripts</h3>

        </div>

      </div>


<p class="it">Los scripts pueden ser incluidos directamente en HTML, entre dos etiquetas de script, como en:</p>
      <p class="p" id="scripts_can_be_">Scripts can be included directly in HTML, between two <code class="literal">script</code> tags, as <a id="id494879" class="indexterm" href=""></a><a id="id494887" class="indexterm" href=""></a>in:</p>

      <pre class="programlisting" data-language="html" id="body_script_">&lt;body&gt;
    &lt;script type="text/javascript"&gt;
        alert("Hello, world!");
    &lt;/script&gt;
&lt;/body&gt;</pre>

<p class="it">o almacenada en un archivo separado con el sufijo .js , y luego se hace referencia a él en alguna parte del HTML (podría ser en el head, como se muestra aquí, o también justo antes del final del cuerpo de la etiqueta de cierre):</p>
      <p class="p" id="or_stored_in_a_">or stored in a separate file with a <span class="emphasis"><em>.js</em></span> suffix, and then referenced somewhere in the HTML (could be in the <code class="literal">head</code>, as shown here, or also just before the end of the closing <code class="literal">body</code> tag):</p>

      <pre class="programlisting" data-language="html" id="head_titlep">&lt;head&gt;
    &lt;title&gt;Page Title&lt;/title&gt;
    &lt;script type="text/javascript" src="myscript.js"&gt;&lt;/script&gt;
&lt;/head&gt;</pre>

    <div class="sect2" id="_javascript_gotchas">

      <div class="titlepage">

          <h3 class="title">JavaScript Gotchas</h3>

        </div>

      </div>

 
<p class="it">Como beneficio extra, y sin cargo adicional, me gustaría compartir con ustedes mis cuatro mejores trampas de JavaScript: cosas que, si lo hubiera sabido antes, me habría ahorrado muchas horas de tarde-noche sesiones de depuración, el pánico inducido por la ansiedad, y aumento de los niveles de cortisol. Es posible que desee volver y hacer referencia a esta sección posteriormente.</p>
      <p class="p" id="as_a_bonus_and">As a bonus, and at no extra charge, I would like to share with you my top four JavaScript gotchas: things that, had I known earlier, would have saved me many hours of late-night debugging sessions, anxiety-induced panic, and increased cortisol levels. You might want to come back and reference this section later.<a id="id495055" class="indexterm" href=""></a><a id="id495063" class="indexterm" href=""></a></p>

      <div class="sect3" id="_dynamic_typing">

        <div class="titlepage">

            <h4 class="title">Dynamic typing</h4>

          </div>

        </div>

<p class="it">Me encanta cómo sus dedos revolotean a través del teclado, pero no es de lo que  estoy hablando. No, Javascript es un lenguaje escrito vagamente, lo que significa que no tiene que especificar qué tipo de información se almacena en una variable de antemano. Muchos otros lenguajes, como Java (que es completamente diferente a Javascript ), requieren que se declare el tipo, String, float o  boolean, de una variable :</p>
        <p class="p" id="i_do_love_how_y">I do love how your fingers flutter across the keyboard, but that’s not what I’m talking about. No, JavaScript is a <span class="emphasis"><em>loosely typed</em></span> language, meaning you don’t have to specify what <span class="emphasis"><em>type</em></span> of information will be stored in a variable in advance. Many other languages, like Java (which is completely different from Java<span class="emphasis"><em>Script</em></span>), require you to declare a variable’s type, such as <code class="literal">int</code>, <code class="literal">float</code>, <code class="literal">boolean</code>, or <code class="literal">String</code>:</p>

        <pre class="programlisting" data-language="java" id="declaring_var_id1">//Declaring variables in Java
int number = 5;
float value = 12.3467;
boolean active = true;
String text = "Crystal clear";</pre>

<p class="it">JavaScript, sin embargo, de forma automática asigna tipos de variables en función de qué tipo de información se asigna a la misma. (Tenga en cuenta que  o  indican los valores de cadena. Yo prefiero comillas dobles  "", pero algunas personas prefieren singles )</p>
        <p class="p" id="javascript_how">JavaScript, however, automatically <span class="emphasis"><em>types</em></span> a variable based on what kind of information you assign to it. (Note that <code class="literal">''</code> or <code class="literal">""</code> indicate string values. I prefer double quotation marks <code class="literal">""</code>, but some people like singles <code class="literal">''</code>.)</p>

        <pre class="programlisting" data-language="javascript" id="declaring_var_id2">//Declaring variables in JavaScript
var number = 5;
var value = 12.3467;
var active = true;
var text = "Crystal clear";</pre>

<p class="it">Qué aburrido - var, var, var, var! - Todavía útil, ya que podemos declarar las variables y nombres incluso antes de saber qué tipo de datos voy a entrar en ellos. Usted puede incluso cambiar un tipo de variable sobre la marcha sin que JavaScript este volviendo loco:</p>

        <p class="p" id="how_boringvar">How boring—<code class="literal">var</code>, <code class="literal">var</code>, <code class="literal">var</code>, <code class="literal">var</code>!—yet handy, as we can declare and name variables before we even know what type of data will go into them. You can even change a variable’s type on-the-fly without JavaScript freaking out on you:</p>

        <pre class="programlisting" data-language="javascript" id="var_value__">var value = 100;
value = 99.9999;
value = false;
value = "This can't possibly work".;
value = "Argh, it does work! No errorzzzz!";</pre>

<p class="it">Menciono esto porque un día un valor numérico será almacenado por accidente como una cadena, y esto va a causar un poco que parte de su código tenga un comportamiento extraño, y, básicamente, no quiero que venga a mí llorando cuando esto suceda. Por lo tanto, sabe que cada vez que un tipo de variable está en duda, se puede emplear el operador typeof:</p>

        <p class="p" id="i_mention_this_">I mention this because one day a numeric value will be accidentally stored as a string, and it will cause some part of your code to behave strangely, and basically I don’t want you to come crying to me when that happens. Thus, know that whenever a variable’s type is in doubt, you can<a id="id495546" class="indexterm" href=""></a> employ the <code class="literal">typeof</code> operator:</p>

        <pre class="programlisting" data-language="javascript" id="typeof__re">typeof 67;              //Returns "number"
var myName = "Scott";
typeof myName;          //Returns "string"
myName = true;
typeof myName;          //Returns "boolean"</pre>

      <div class="sect3" id="_variable_hoisting">

        <div class="titlepage">

            <h4 class="title">Variable hoisting</h4>

          </div>

        </div>

<p class="it">Al contrario de lo que cabría esperar, el código JavaScript es usualmente, pero no siempre, ejecutado en el lineal, en el orden de arriba hacia abajo . Por ejemplo, en este código, cuando would se espera que la variable i que se constituya?</p>
        <p class="p" id="contrary_to_wha_id1">Contrary to what you would expect, JavaScript code is usually, but not always, executed in linear, top-to-bottom order. For example, in this code, when would you expect the variable <code class="literal">i</code> to be established?<a id="id495695" class="indexterm" href=""></a><a id="id495703" class="indexterm" href=""></a></p>

        <pre class="programlisting" data-language="javascript" id="var_numloops___id1">var numLoops = 100;
for (var i = 0; i &lt; numLoops; i++) {
    console.log(i);
}</pre>

<p class="it">En muchos otros idiomas, i sería declarado justo cuando empieza el bucle <code class="literal">for</code>. Pero gracias al fenómeno de variable hoisting, en JavaScript las declaraciones de variables son hoisted hasta la parte superior de la función del contexto en el que residen. Así, en nuestro ejemplo, i se llegó a declarar antes que el bucle <code class="literal">for</code> comience. El siguiente es el codigo equivalente:</p>

        <p class="p" id="in_many_other_l">In many other languages, <code class="literal">i</code> would be declared right when the <code class="literal">for</code> loop begins, as you’d expect. But thanks to a phenomenon known as <span class="emphasis"><em>variable hoisting</em></span>, in JavaScript, variable declarations are <span class="emphasis"><em>hoisted</em></span> up to the top of the function context in which they reside. So in our example, <code class="literal">i</code> is actually declared <span class="emphasis"><em>before</em></span> the <code class="literal">for</code> loop even begins. The following is equivalent:</p>

        <pre class="programlisting" data-language="javascript" id="var_numloops___id2">var numLoops = 100;
var i;
for (i = 0; i &lt; numLoops; i++) {
    console.log(i);
}</pre>

 <p class="it">Esto puede ser problemático cuando se tienen nombres de variables en conflicto, como una variable que usted pensó que existía sólo más adelante en el código pero está realmente presente desde el principio.</p>
        <p class="p" id="this_can_be_pro">This can be problematic when you have conflicting variable names, as a variable that you thought existed only later in the code is actually present right at the beginning.</p>

      <div class="sect3" id="_function_level_scope">

        <div class="titlepage">

            <h4 class="title">Function-level scope</h4>


          </div>

        </div>

<p class="it">En la programación, el concepto de ámbito de variable nos ayuda a identificar qué variables son accesibles en qué contextos. En general, es una mala idea tener todos los valores accesibles desde cualquier otro lugar, ya que se termina con tantos conflictos y cambios accidentales en el valor de las variables que usted acaba por volverse loco.</p>   
        <p class="p" id="in_programming">In programming, the concept of <span class="emphasis"><em>variable scope</em></span> helps us identify which variables are accessible in which contexts. Generally, it is a bad idea to have every value accessible from everywhere else because you’d end up with so many conflicts and accidental value changes that you would just go crazy.<a id="id496066" class="indexterm" href=""></a><a id="id496074" class="indexterm" href=""></a><a id="id496080" class="indexterm" href=""></a></p>

<p class="it">Muchos lenguajes usan ámbito a nivel de bloque , en el que existen las variables sólo dentro de la corriente del bloque de código, por lo general se indica entre llaves. Con alcance a nivel de bloque, nuestra <code class="literal">i</code> volvería a existir sólo en el contexto del bucle, por ejemplo, por lo que cualquier intento de leer el valor de  <code class="literal">i</code>  o cambiar <code class="literal">i</code> fuera del bucle sería un fracaso. Esto es bueno porque se pueden establecer otras variables dentro de su bucle y saber que no hay conflicto con variables que estan en otro sitio.</p>

        <p class="p" id="many_languages_">Many languages use <span class="emphasis"><em>block-level scope</em></span>, in which variables exist only within the current “block” of code, usually indicated by curly braces. With block-level scope, our <code class="literal">i</code> would exist only within the context of the <code class="literal">for</code> loop, for example, so any attempts to read the value of <code class="literal">i</code> or change <code class="literal">i</code> outside of the loop would fail. This is nice because you could establish other variables from within your loop and know that they wouldn’t conflict with variables that exist elsewhere.<a id="id496124" class="indexterm" href=""></a></p>

<p class="it">En JavaScript, sin embargo, las variables están en el ámbito de la función, lo que significa que se puede acceder en cualquier lugar dentro de la función (no block) en el que residen.</p>
        <p class="p" id="in_javascript__id1">In JavaScript, however, variables are scoped at the function level, meaning they are accessible anywhere within the <span class="emphasis"><em>function</em></span> (not block) in which they reside.</p>

<p class="it">Esto es principalmente algo a tener en cuenta si usted reutiliza codigo para otros idiomas.Balance final: Usted puede mantener valores contenidos envolviéndolos dentro de las funciones.</p>

        <p class="p" id="this_is_primari">This is primarily something to be aware of if you’re used to other languages. Bottom line: You can keep values contained by wrapping them within functions.</p>

      <div class="sect3" id="_global_namespace">

        <div class="titlepage">

            <h4 class="title">Global namespace</h4>

          </div>

        </div>

<p class="it">Hablando de conflictos variables, le pido, hagame un favor: abra cualquier página web, active la consola JavaScript, tipo ventana , y haga clic en el triángulo gris para ver su contenido.</p>

        <p class="p" id="speaking_of_var">Speaking of variable conflicts, please do me a favor: open any web page, activate the JavaScript console, type <span class="strong"><strong><code class="literal">window</code></strong></span>, and click the gray disclosure triangle to view its <span class="keep-together">contents</span>.<a id="id496179" class="indexterm" href=""></a><a id="id496188" class="indexterm" href=""></a></p>

<p class="it">Sé que se siente como que acaba de introducir el array, pero esto se llama en realidad el global namespace, que puede parecer incluso más cool (ver Figura 3-10).</p>

        <p class="p" id="i_know_it_feels">I know it feels like you just entered the matrix, but this is actually called “the global namespace,” which might sound even cooler (see <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch03.html#The_global_namespace" title="Figure 3-10. The global namespace">Figure 3-10</a>).</p>

        <div class="figure" id="The_global_namespace">

          <div class="figure-contents">


              <img src="/static/KSnaJy9UI1-img8.png" alt="The global namespace"/>

            </div>

          </div>
<p class="fig">Figura 3-10. El espacio de nombres global</p>
          <p class="fig">Figure 3-10. The global namespace</p>

<p class="it">El window es el objeto en el tope de la jerarquía del navegador   dentro de los elementos de Javascript, y todos estos objetos y valores que se ven debajo de la ventana existen en el nivel global. Lo que esto significa es que cada vez que se declara una nueva variable, va a añadir un nuevo valor a la ventana. O, codificadores de JavaScript como justos les gusta decir, que están contaminando el espacio de nombres global. (Sorprendentemente, la mayoría de las personas que escriben cosas como esta en los foros en línea son en realidad muy agradable en persona).</p>
        <p class="p" id="window_is_the_t"><code class="literal">window</code> is the topmost object in the browser’s hierarchy of JavaScript elements, and all of these objects and values you see beneath <code class="literal">window</code> exist at the <span class="emphasis"><em>global</em></span> level. What this means is that every time you declare a new variable, you are adding a new value to <code class="literal">window</code>. Or, as righteous JavaScript coders like to say, you are polluting the global <span class="keep-together">namespace</span>. (Surprisingly, most people who write things like this in online forums are actually quite friendly in person.)</p>

<p class="it">Por ejemplo, pruebe a escribir esto en la consola:</p>

        <p class="p" id="for_example_tr">For example, try typing this into the console: <span class="strong"><strong><code class="literal">var zebras = "amazing"</code></strong></span>.</p>

<p class="it">A continuación, escriba en la ventana de nuevo, y desplacese todo el camino hasta la parte inferior, en el que ahora debe ver zebras, como se muestra en la Figura 3-11.</p>

        <p class="p" id="then_type_windo">Then type <span class="strong"><strong><code class="literal">window</code></strong></span> again, and scroll all the way down to the bottom, where you should now see <code class="literal">zebras</code>, as shown in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch03.html#The_global_namespace_now_with_zebras" title="Figure 3-11. The global namespace, now with zebras">Figure 3-11</a>.</p>

        <div class="figure" id="The_global_namespace_now_with_zebras">

          <div class="figure-contents">


              <img src="/static/KSnaJy9UI1-img9.png" alt="The global namespace, now with zebras"/>

            </div>

          </div>
<p class="fig">Figura 3-11. El espacio de nombres global, ahora con zebras</p>
          <p class="fig">Figure 3-11. The global namespace, now with zebras</p>
 <p>----</p>

<p class="it">(Confusamente, también es posible definir nuevas variables en JavaScript sin necesidad de utilizar la declaración var estándar, por lo que escribir simplemente cebras = "increíble" tendría el mismo efecto que el que se muestra.)</p>
        <p class="p" id="confusingly_i">(Confusingly, it is also possible to define new variables in JavaScript without using the standard <code class="literal">var</code> declaration, so typing simply <span class="strong"><strong><code class="literal">zebras = "amazing"</code></strong></span> would have the same effect as that shown.)</p>

<p class="it">¿Que es lo que  tan mal con la adición de los valores de la ventana? A medida que comienza, nada en absoluto. Pero a medida que sus proyectos crecen en complejidad, y sobre todo si se empieza a incorporar a D3 otro codigo que no seá JavaScript (como jQuery, Facebook “Like” buttons, o Google Analytics tracking code), en algún momento usted estará en una conflicto, ya que reutilizando las variables zebras para su proyecto, pero zebraTracker.js está también utilizando una variable con el mismo nombre! El resultado: el caos. O al menos algunos datos erróneos, lo que podría conducir a un comportamiento inesperado o errores.</p>

        <p class="p" id="whats_so_wrong">What’s so wrong with adding values to <code class="literal">window</code>? As you get started, nothing at all. But as your projects grow in complexity, and especially if you begin to incorporate other non-D3 JavaScript code (such as jQuery, Facebook “Like” buttons, or Google Analytics tracking code), at some point you’re bound to run into a conflict because you’re using the variable <code class="literal">zebras</code> for your project, but zebraTracker.js is <span class="emphasis"><em>also</em></span> using a variable with the same name! The result: chaos. Or at least some bad data, which could lead to unexpected behavior or errors.</p>

<p class="it">Hay dos soluciones fáciles (y, para aclarar, es probable que no tenga que preocuparse por esto hasta más tarde):</p>
        <p class="p" id="there_are_two_e">There are two easy workarounds (and, to clarify, you probably don’t have to worry about this until later):<a id="id496382" class="indexterm" href=""></a></p>

        <div class="itemizedlist" id="declare_variabl_id1">

          <ul class="itemizedlist">
<li class="it">Declarar variables sólo dentro de otras funciones. Esto no suele ser factible, pero en el nivel de la función evitará que las variables locales entren en conflicto con otras.</li>
            <li class="p"> Declare variables only within other functions. This is not usually feasible, but the function-level scope will prevent local variables from conflicting with others. </li>
<li class="it">Declarar un único objeto global, y adjuntar todos los aspirantes a las variables globales a ese objeto. Por ejemplo:</li>
            <li class="p"> Declare a single global object, and attach all of your would-be global variables to that object. For example: </li>

          </ul>

        </div>

        <pre class="programlisting" data-language="javascript" id="var_vis___">var Vis = {};  //Declare empty global object
Vis.zebras = "still pretty amazing";
Vis.monkeys = "too funny LOL";
Vis.fish = "you know, not bad";</pre>

<p class="it">Todas las variables relacionadas con los animales extraños ya no están contaminando el espacio de nombres global, sino que todas ellas existen en forma de valores almacenados dentro de su, objeto global <code class="literal">Vis</code>. Por supuesto, podría ser nombrado <code class="literal">Vis</code>  lo que quiera, pero la casa de fieras es más difícil de escribir. En cualquier caso, el conflicto sólo nombrarte  ll tienen con otras secuencias de comandos es si uno de ellos también quiere tener un objeto global con el mismo nombre (<code class="literal">Vis</code>), que es mucho menos probable.</p>
        <p class="p" id="all_of_your_wei">All of your weird animal-related variables are no longer polluting the global namespace, but instead they all exist as values stored within your single, global object, <code class="literal">Vis</code>. Of course, <code class="literal">Vis</code> could be named whatever you like, but <code class="literal">Menagerie</code> is harder to type. Regardless, the only naming conflict you’ll have with other scripts is if one of them <span class="emphasis"><em>also</em></span> wants to have a global object with the same name (<code class="literal">Vis</code>), which is far less likely.<a id="id496566" class="indexterm" href=""></a></p>



  <div class="" data-original-filename="3_tech_fundamentals.asciidoc" id="SVG_3">

    <div class="titlepage">

        <h2 class="title">SVG</h2>

      </div>

    </div>

    



<p class="it">D3 es más útil cuando se utiliza para generar y manipular elementos visuales como gráficos vectoriales escalables (SVG). Dibujo con divs y otros elementos HTML nativos son posibles, pero un poco torpes y con sujeción a las inconsistencias habituales a través de diferentes navegadores. El uso de SVG es más fiable, visualmente consistente, y más rápido.</p>

    <p class="p" id="d_is_most_usef">D3 is most useful when used to generate and manipulate visuals as Scalable Vector Graphics (SVG). Drawing with <code class="literal">div</code>s and other native HTML elements is possible, but a bit clunky and subject to the usual inconsistencies across different browsers. Using SVG is more reliable, visually consistent, and faster.<a id="ix_SVG" class="indexterm" href=""></a></p>


<p class="it">La figura 3-12 muestra un pequeño círculo, y su código SVG.</p>
    <p class="p" id="shows_a_small_c"><a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch03.html#A_small_SVG_circle" title="Figure 3-12. A small SVG circle">Figure 3-12</a> shows a small circle, and its SVG code follows.</p>

    <div class="figure" id="A_small_SVG_circle">

      <div class="figure-contents">

          <img src="/static/KSnaJy9UI1-img10.png" alt="A small SVG circle"/>

        </div>

      </div>
<p class="fig">Figura 3-12. Un pequeño círculo SVG</p>
      <p class="fig">Figure 3-12. A small SVG circle</p>


    <pre class="programlisting" data-language="html" id="svg_width_id1">&lt;svg width="50" height="50"&gt;
    &lt;circle cx="25" cy="25" r="22" fill="blue" stroke="gray" stroke-width="2"/&gt;
&lt;/svg&gt;</pre>


<p class="it">El software de dibujo vectorial como Illustrator se puede utilizar para generar archivos SVG, pero tenemos que aprender a generar con código.</p>
    <p class="p" id="vector_drawing_">Vector drawing software like Illustrator can be used to generate SVG files, but we need to learn how to generate them with code.</p>

    <div class="sect2" id="_the_svg_element">

      <div class="titlepage">

          <h3 class="title">The SVG Element</h3>

        </div>

      </div>

<p class="it">SVG es un formato de imagen basado en texto. Cada imagen SVG se define utilizando código de marcado similar al HTML, el código SVG se puede incluir directamente dentro de cualquier documento HTML, o se inserta de forma dinámica en el DOM. Cada navegador web es compatible con SVG , excepto las versiones de Internet Explorer 8 y versiones anteriores. SVG está basado en XML, por lo que se dará cuenta de que los elementos que no tiene una etiqueta de cierre deben ser de cierre. Por ejemplo:</p>

      <p class="p" id="svg_is_a_textb">SVG is a text-based image format. Each SVG image is defined using markup code similar to HTML, and SVG code can be included directly within any HTML document, or inserted dynamically into the DOM. Every web browser supports SVG <span class="emphasis"><em>except</em></span> <a class="ulink" href="http://caniuse.com/#feat=svg" target="_top">Internet Explorer versions 8 and earlier</a>. SVG is XML-based, so you’ll notice that elements<a id="id496785" class="indexterm" href=""></a><a id="id496794" class="indexterm" href=""></a> that don’t have a closing tag must be self-closing. For example:</p>

      <pre class="programlisting" data-language="html" id="elementelem">&lt;element&gt;&lt;/element&gt; &lt;!-- Uses closing tag --&gt;
&lt;element/&gt;          &lt;!-- Self-closing tag --&gt;</pre>

<p class="it">Antes de que pueda dibujar cualquier cosa, debe crear un elemento SVG. Piense en el elemento SVG como un lienzo en el que se representan los elementos visuales. (Al respecto, SVG es conceptualmente similar al  elemento canvas de HTML.) Como mínimo, es bueno para especificar los valores de anchura y altura. Si usted no  especifica estos, el SVG se comportará como un elemento HTML a nivel de bloque típicamente codicioso y ocupará tanto espacio como pueda dentro de su elemento envolvente:</p>
      <p class="p" id="before_you_can__id1">Before you can draw anything, you must create an SVG element. Think of the SVG element as a canvas on which your visuals are rendered. (In that respect, SVG is conceptually similar to HTML’s <code class="literal">canvas</code> element.) At a minimum, it’s good to specify <code class="literal">width</code> and <code class="literal">height</code> values. If you don’t specify these, the SVG will behave like a typically greedy, block-level HTML element and take up as much room as it can within its enclosing element:</p>

      <pre class="programlisting" data-language="html" id="svg_width_id2">&lt;svg width="500" height="50"&gt;
&lt;/svg&gt;</pre>

<p class="it">Tenga en cuenta que pixeles son las unidades de medida por defecto, por lo que podemos especificar las dimensiones de 500 y 50, no 500 píxeles y 50 píxeles. Podríamos haber especificado explícitamente px, o cualquier número de otras unidades compatibles, incluyendo em, pt, en, cm y mm.</p>

      <p class="p" id="note_that_pixel">Note that <span class="emphasis"><em>pixels</em></span> are the default measurement units, so we can specify dimensions of <code class="literal">500</code> and <code class="literal">50</code>, not <code class="literal">500px</code> and <code class="literal">50px</code>. We could have specified <code class="literal">px</code> explicitly, or any number of other supported units, including <code class="literal">em</code>, <code class="literal">pt</code>, <code class="literal">in</code>, <code class="literal">cm</code>, and <code class="literal">mm</code>.</p>


    <div class="sect2" id="_simple_shapes">

      <div class="titlepage">

          <h3 class="title">Simple Shapes</h3>

        </div>

      </div>

  <p class="it">Hay una serie de elementos visuales que se pueden incluir entre esas etiquetas <code class="literal">svg</code>, incluyendo <code class="literal">rect</code>, <code class="literal">circle</code>, <code class="literal">ellipse</code>, <code class="literal">line</code>, <code class="literal">text</code>, y <code class="literal">path</code>. (Lo siento, zebras no es válida en este contexto).</p> 

      <p class="p" id="there_are_a_num">There are a number of visual elements that you can include between those <code class="literal">svg</code> tags, including <code class="literal">rect</code>, <code class="literal">circle</code>, <code class="literal">ellipse</code>, <code class="literal">line</code>, <code class="literal">text</code>, and <code class="literal">path</code>. (Sorry, <code class="literal">zebras</code> is not valid in this context.)<a id="id497037" class="indexterm" href=""></a></p>

<p class="it">Si está familiarizado con la programación de gráficos por ordenador, que reconoce el sistema de coordenadas basado en píxeles por convención el <code class="literal">0,0</code> es la esquina superior izquierda del espacio de dibujo. El aumento de los valores de <code class="literal">x</code> se mueven hacia la derecha, mientras que el aumento de los valores de <code class="literal">y</code> se mueven hacia abajo (ver Figura 3-13).</p>

      <p class="p" id="if_youre_famil_id2">If you’re familiar with computer graphics programming, you’ll recognize the usual pixel-based coordinates system in which <code class="literal">0,0</code> is the top-left corner of the drawing space. Increasing <code class="literal">x</code> values move to the right,<a id="id497066" class="indexterm" href=""></a> while increasing <code class="literal">y</code> values move down (see <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch03.html#The_SVG_coordinates_system" title="Figure 3-13. The SVG coordinates system">Figure 3-13</a>).</p>

      <div class="figure" id="The_SVG_coordinates_system">

        <div class="figure-contents">

          <div class="mediaobject"> <img alt="Imagen" src="/static/Fig313.png"/> </div>

        </div>

        <p class="fig">Figure 3-13. The SVG coordinates system</p>

      </div>

<p class="it"><code class="literal">rect</code> dibuja un rectángulo. Utilice <code class="literal">x</code> e <code class="literal">y</code> para especificar las coordenadas de la esquina superior izquierda, y <code class="literal">width</code> y <code class="literal">height</code> para especificar las dimensiones. Este rectángulo llena todo el espacio de nuestra SVG</p>
      <p class="p" id="rect_draws_a_re"><code class="literal">rect</code> draws a rectangle. Use <code class="literal">x</code> and <code class="literal">y</code> to specify the coordinates of the upper-left corner, and <code class="literal">width</code> and <code class="literal">height</code> to specify the dimensions. This rectangle fills the entire space of our SVG</p>

      <pre class="programlisting" data-language="html" id="rect_x_y_id1">&lt;rect x="0" y="0" width="500" height="50"/&gt;</pre>

<p class="it"><code class="literal">circle</code> dibuja un círculo. Utilice CX y CY para especificar las coordenadas del centro , y R para especificar el radio. Este círculo se centra en el medio de nuestra SVG de 500 píxeles de ancho porque su cx (“center-x”) tiene como valor 250</p>
      <p class="p" id="circle_draws_a_"><code class="literal">circle</code> draws a circle. Use <code class="literal">cx</code> and <code class="literal">cy</code> to specify the coordinates of the <span class="emphasis"><em>center</em></span>, and <code class="literal">r</code> to specify the radius. This circle is centered in the middle of our 500-pixel-wide SVG because its <code class="literal">cx</code> (“center-x”) value is 250</p>

      <pre class="programlisting" data-language="html" id="circle_cx_id1">&lt;circle cx="250" cy="25" r="25"/&gt;</pre>

<p class="it"><code class="literal">ellipse</code> es similar, pero espera valores de radio independientes para cada eje. En lugar de r, utilice Rx y Ry</p>
      <p class="p" id="ellipse_is_simi"><code class="literal">ellipse</code> is similar, but expects separate radius values for each axis. Instead of <code class="literal">r</code>, use <code class="literal">rx</code> and <code class="literal">ry</code> </p>

      <pre class="programlisting" data-language="html" id="ellipse_cx">&lt;ellipse cx="250" cy="25" rx="100" ry="25"/&gt;</pre>

<p class="it"><code class="literal">line</code> dibuja una línea, como se muestra en la Figura 3-17. Utilice x1 e y1 para especificar las coordenadas de un extremo de la línea, y x2 e y2 para especificar las coordenadas del otro extremo. El color del trazo se debe especificar para que la línea sea visible</p>

      <p class="p" id="line_draws_a_li"><code class="literal">line</code> draws a line, as shown in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch03.html#An_SVG_line" title="Figure 3-17. An SVG line">Figure 3-17</a>. Use <code class="literal">x1</code> and <code class="literal">y1</code> to specify the coordinates of one end of the line, and <code class="literal">x2</code> and <code class="literal">y2</code> to specify the coordinates of the other end. A <code class="literal">stroke</code> color must be specified for the line to be visible</p>

      <pre class="programlisting" data-language="html" id="line_x_y">&lt;line x1="0" y1="0" x2="500" y2="50" stroke="black"/&gt;</pre>

<p class="it"><code class="literal">text</code> representa el texto. Utilice<code class="literal">x</code>para especificar la posición del borde izquierdo, e y para especificar la posición vertical de la línea de base del tipo . (Línea de base es un término tipográfico para la línea invisible en la que se apoyan las letras para. Las porciones de letras tales como " p " y " Y " que se extienden por debajo de la línea de base se denominan descendentes.)</p>
       <p class="p" id="text_renders_te"><code class="literal">text</code> renders text. Use <code class="literal">x</code> to specify the position of the left edge, and <code class="literal">y</code> to specify the vertical position of the type’s <span class="emphasis"><em>baseline</em></span>. (Baseline is a typographical term for the invisible line on which the letters appear to rest. Portions of letters such as “p” and “y” that extend below the baseline are called descenders.)</p>

      <pre class="programlisting" data-language="html" id="text_x_y_id1">&lt;text x="250" y="25"&gt;Easy-peasy&lt;/text&gt;</pre>

<p class="it"><code class="literal">text</code> heredará los estilos de fuente CSS especificados de su elemento padre a menos que se especifique lo contrario. (Más acerca de estilos de <code class="literal">text</code> en un momento) Podríamos anular que el formateo de la siguiente manera y obtener el resultado que se muestra en la Figura 3-19</p>
      <p class="p" id="text_will_inher"><code class="literal">text</code> will inherit the CSS-specified font styles of its parent element unless specified otherwise. (More on styling text in a moment.) We could override that formatting as follows and obtain the result shown in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch03.html#More_SVG_text" title="Figure 3-19. More SVG text">Figure 3-19</a></p>

      <pre class="programlisting" data-language="html" id="text_x_y_id2">&lt;text x="250" y="25" font-family="serif" font-size="25"
 fill="gray"&gt;Easy-peasy&lt;/text&gt;</pre>

<p class="it">También tenga en cuenta que cuando cualquier elemento visual choca con el borde de la SVG, se recorta. Tenga cuidado al usar <code class="literal">text</code> porque pueden cortarse los descendentes (ouch!). Se puede ver que esto sucede en la figura 3-20 cuando fijamos la línea de base (<code class="literal">y</code>) a 50, la misma medida que la altura de nuestra SVG:</p>
      <p class="p" id="also_note_that__id2">Also note that when any visual element runs up against the edge of the SVG, it will be clipped. Be careful when using <code class="literal">text</code> so your descenders don’t get cut off (ouch!). You can see this happen in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch03.html#Even_More_SVG_text" title="Figure 3-20. More SVG text">Figure 3-20</a> when we set the baseline (<code class="literal">y</code>) to 50, the same as the height of our SVG:</p>
<pre class="programlisting" data-language="html" id="text_x_y_id3">&lt;text x="250" y="50" font-family="serif" font-size="25"
 fill="gray"&gt;Easy-peasy&lt;/text&gt;</pre>



      <div class="figure" id="Even_More_SVG_text">

        <div class="figure-contents">

          <div class="mediaobject"><em class="dotEPUBProtected"> <img alt="Imagen" src="/static/Fig320.png"/> </em></div>

        </div>
      </div>

        <p class="fig">Figure 3-20. More SVG text</p>

      


<p class="it"><code class="literal">path</code> es para dibujar algo más complejo que las formas anteriores (como el esquema del país para geomaps), y se explicará por separado. Por ahora,  Trabajaremos con formas simples.</p>
      <p class="p" id="path_is_for_dra"><code class="literal">path</code> is for drawing anything more complex than the preceding shapes (like country outlines for geomaps), and will be explained separately. For now, we’ll work with simple shapes.</p>


    <div class="sect2" id="_styling_svg_elements">

      <div class="titlepage">


          <h3 class="title">Styling SVG Elements</h3>

        </div>

      </div>

<p class="it">El estilo por defecto de SVG es un relleno negro sin trazo. Si quiere algo más, tiene que aplicar estilos a los elementos. Las propiedades comunes de SVG son las siguientes:</p>
      <p class="p" id="svgs_default_s">SVG’s default style is a black fill with no stroke. If you want anything else, you’ll have to apply styles to your elements. Common SVG<a id="id497920" class="indexterm" href=""></a><a id="id497928" class="indexterm" href=""></a> properties are as follows:</p>

  <div class="variablelist" id="fill_a_color_va">

        <dl class="variablelist">

          <dt><span class="term"> <code class="literal">fill</code> </span></dt>
<dd class="it">Llenar un valor de color. Al igual que con CSS, los colores pueden ser especificados con los nombres de colores, los valores hexadecimales RGB o valores RGBA.</dd>
          <dd> A color value. Just as with CSS, colors can be specified as named colors, hex values, or RGB or RGBA values. </dd>

          <dt><span class="term"> <code class="literal">stroke</code> </span></dt>
<dd class="it">valor de color.</dd>
          <dd> A color value. </dd>

          <dt><span class="term"> <code class="literal">stroke-width</code> </span></dt>
<dd class="it"> Medición numérica (por lo general en píxeles).</dd>
          <dd> A numeric measurement (typically in pixels). </dd>

          <dt><span class="term"> <code class="literal">opacity</code> </span></dt>
<dd class="it">Un valor numérico entre 0.0 (completamente transparente) y 1.0 (totalmente opaco). </dd>
          <dd> A numeric value between 0.0 (completely transparent) and 1.0 (completely <span class="keep-together">opaque</span>). </dd>

        </dl>

      </div>

<p class="it">Con el texto, también puede utilizar estas propiedades, que funcionan igual que en el CSS: </p>
      <p class="p" id="with_text_you_">With <code class="literal">text</code>, you can also use these properties, which work just like in CSS:</p>

      <div class="itemizedlist" id="fontfamily_fon">

        <ul class="itemizedlist">
<li class="it">familia tipográfica</li>
          <li class="p"> <code class="literal">font-family</code> </li>
<li class="it">tamaño de fuente</li>
          <li class="p"> <code class="literal">font-size</code> </li>

        </ul>

      </div>

<p class="it">En otro paralelo a CSS, hay dos maneras de aplicar estilos a un elemento SVG: ya sea directamente (en línea) como un atributo del elemento, o con una regla de estilo CSS.</p>
      <p class="p" id="in_another_para">In another parallel to CSS, there are two ways to apply styles to an SVG element: either directly (inline) as an attribute of the element, or with a CSS style rule.</p>

<p class="it">Estas son algunas de las propiedades de estilo aplicadas directamente a un círculo como atributos, con el resultado que se muestra en la Figura 3-21:</p>
      <p class="p" id="here_are_some_s">Here are some style properties applied directly to a <code class="literal">circle</code> as attributes, with the result shown in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch03.html#An_SVG_circle2" title="Figure 3-21. An SVG circle">Figure 3-21</a>:</p>

      <pre class="programlisting" data-language="html" id="circle_cx_id2">&lt;circle cx="25" cy="25" r="22"
 fill="yellow" stroke="orange" stroke-width="5"/&gt;</pre>


<div class="figure" id="An_SVG_circle2">

        <div class="figure-contents">

          <div class="mediaobject"><em class="dotEPUBProtected"> <img alt="Imagen" src="/static/Fig321.png"/> </em></div>

        </div>

        <p class="fig">Figure 3-21. An SVG circle</p>

      </div>

<p class="it">Alternativamente, podríamos despojar a los atributos de estilo y asignar el círculo de una clase (como si se tratara de un elemento HTML normal):</p>
      <p class="p" id="alternatively__id1">Alternatively, we could strip the style attributes and assign the <code class="literal">circle</code> a class (just as if it were a normal HTML element):</p>

      <pre class="programlisting" data-language="html" id="circle_cx_id3">&lt;circle cx="25" cy="25" r="22" class="pumpkin"/&gt;</pre>

<p class="it">y luego poner el relleno, trazo y trazo reglas de ancho en un estilo CSS que se dirige a la nueva clase:</p>

      <p class="p" id="and_then_put_th">and then put the <code class="literal">fill</code>, <code class="literal">stroke</code>, and <code class="literal">stroke-width</code> rules into a CSS style that targets the new class:</p>

      <pre class="programlisting" data-language="css" id="pumpkin__fill">.pumpkin {
    fill: yellow;
    stroke: orange;
    stroke-width: 5;
 }</pre>

<p class="it">El enfoque CSS tiene algunas ventajas obvias:</p>
      <p class="p" id="the_css_approac">The CSS approach has a few obvious benefits:</p>

      <div class="itemizedlist" id="you_can_specify_id1">

        <ul class="itemizedlist">
<li class="it">Puede especificar un estilo de una vez y que se aplica a varios elementos.</li>
          <li class="p"> You can specify a style once and have it applied to multiple elements. </li>
<li class="it">El código CSS es más fácil de leer que los atributos en línea.</li>
          <li class="p"> CSS code is easier to read than inline attributes. </li>
<li class="it">Por estas razones, el enfoque CSS podría ser más fácil de mantener y tambien permite realizar un cambio de diseño de manera más rápida.</li>
          <li class="listitem"> For those reasons, the CSS approach might be more maintainable and make design changes faster to implement. </li>

        </ul>

      </div>    
  

   <p class="it">El uso de CSS para aplicar estilos SVG, sin embargo, puede ser desconcertante para algunos. <code class="literal">fill</code>, <code class="literal">stroke</code>, y <code class="literal">stroke-width</code>, después de todo, no son propiedades CSS. (Los equivalentes CSS más cercanos son <code class="literal">background-color</code> y <code class="literal">border</code>.) Es  sólo que estamos usando selectores CSS para aplicar propiedades SVG-específicas. Si le ayuda a recordar esta regla  en su hoja de estilo está SVG-específica, considere la inclusión de SVG en esos selectores:</p>
      <p class="p" id="using_css_to_ap">Using CSS to apply SVG styles, however, can be disconcerting for some. <code class="literal">fill</code>, <code class="literal">stroke</code>, and <code class="literal">stroke-width</code>, after all, are <span class="emphasis"><em>not</em></span> CSS properties. (The nearest CSS equivalents are <code class="literal">background-color</code> and <code class="literal">border</code>.) It’s just that we are using CSS selectors to apply SVG-specific properties. If it helps you remember which rules in your stylesheet are SVG-specific, consider including <code class="literal">svg</code> in those selectors:</p>

      <pre class="programlisting" data-language="css" id="svg_pumpkin__">svg .pumpkin {
    /* ... */
 }</pre>


    <div class="sect2" id="_layering_and_drawing_order">

      <div class="titlepage">

          <h3 class="title">Layering and Drawing Order</h3>

        </div>

      </div>

<p class="it">No hay capas en SVG y no hay un concepto real de la profundidad. SVG no soporta la propiedad CSS <code class="literal">z-index</code>, por lo que las formas pueden estar dispuestas sólo en dos dimensiones del plano<code class="literal">x</code>/ Y.</p>
      <p class="p" id="there_are_no_l">There are no “layers” in SVG and no real concept of depth. SVG does not support CSS’s <code class="literal">z-index</code> property, so shapes can be arranged only within the two-dimensional x/y plane.<a id="id498507" class="indexterm" href=""></a></p>

<p class="it">Y, sin embargo, si dibujamos múltiples formas, se superponen:</p>
      <p class="p" id="and_yet_if_we_">And yet, if we draw multiple shapes, they overlap:</p>

      <pre class="programlisting" data-language="html" id="rect_x_y_id2">
      &lt;rect x="0" y="0" width="30" height="30" fill="purple"/&gt;
&lt;rect x="20" y="5" width="30" height="30" fill="blue"/&gt;
&lt;rect x="40" y="10" width="30" height="30" fill="green"/&gt;
&lt;rect x="60" y="15" width="30" height="30" fill="yellow"/&gt;
&lt;rect x="80" y="20" width="30" height="30" fill="red"/&gt;</pre>

<p class="it">El orden en el que se codifican los elementos determina su orden de profundidad. En la figura 3-22, el cuadrado de color púrpura aparece por primera vez en el código, por lo que está primero. A continuación, el cuadrado azul se hace sobre el púrpura, entonces el aparece el cuadrado verde sobre ambos y así sucesivamente.</p>
      <p class="p" id="the_order_in_wh">The order in which elements are coded determines their depth order. In <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch03.html#Overlapping_SVG_elements" title="Figure 3-22. Overlapping SVG elements">Figure 3-22</a>, the purple square appears first in the code, so it is rendered first. Then, the blue square is rendered “on top” of the purple one, then the green square on top of that, and so on.</p>

   
         <div class="figure" id="Overlapping_SVG_elements">

<img alt="Imagen" src="/static/Fig322.png" />
<p class="fig">Figura 3-22. Elementos SVG superpuestos</p>
        <p class="fig">Figure 3-22. Overlapping SVG elements</p>

      </div>

<p class="it">Piense en las formas SVG como la pintura sobre un lienzo. El píxel-pintura que se aplica más tarde oscurece cualquier pintura anterior, y por lo tanto parece estar en el frente.</p>
      <p class="p" id="think_of_svg_sh">Think of SVG shapes as being rendered like paint on a canvas. The pixel-paint that is applied later obscures any earlier paint, and thus appears to be “in front.”</p>

<p class="it">Este aspecto de la orden de dibujo se vuelve importante cuando se tiene algunos elementos visuales que no deben quedar ocultos por los demás. Por ejemplo, es posible que tenga ejes o etiquetas de los valores que aparecen en un diagrama de dispersión. Los ejes y las etiquetas deben añadirse a la última SVG, por lo que aparecen delante de cualquier otro elemento.</p>

      <p class="p" id="this_aspect_of_">This aspect of drawing order becomes important when you have some visual elements that should not be obscured by others. For example, you might have axes or value labels that appear on a scatterplot. The axes and labels should be added to the SVG last, so they appear in front of any other elements.<a id="id498900" class="indexterm" href=""></a><a id="id498905" class="indexterm" href=""></a></p>


    <div class="sect2" id="_transparency">

      <div class="titlepage">


          <h3 class="title">Transparency</h3>

        </div>

      </div>

<p class="it">La transparencia puede ser útil cuando elementos de la superposición de visualización, sino que debe permanecer visible, o si desea quitar importancia a algunos elementos además de destacar otros, como se muestra en la Figura 3-23.</p>

      <p class="p" id="transparency_ca">Transparency can be useful when elements in your visualization overlap but must remain visible, or you want to deemphasize some elements while highlighting others, as shown in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch03.html#RGBA_SVG_shapes" title="Figure 3-23. RGBA SVG shapes">Figure 3-23</a>.</p>

<p class="it">Hay dos maneras de aplicar la transparencia: utilizar un color RGB con alfa, o establecer un valor de opacidad.</p>
      <p class="p" id="there_are_two_w">There are two ways to apply transparency: use an RGB color with alpha, or set an <code class="literal">opacity</code> value.<a id="id498946" class="indexterm" href=""></a><a id="id498954" class="indexterm" href=""></a></p>

<p class="it">Puede utilizar RGBA () en cualquier lugar que especifica un color, por ejemplo, con relleno o el trazo. RGBA () espera tres valores entre 0 y 255 para un alfa rojo, verde y azul, además de valor (transparencia) entre 0.0 y 1.0:</p>
      <p class="p" id="you_can_use_rgb">You can use <code class="literal">rgba()</code> anywhere you specify a color, such as with <code class="literal">fill</code> or <code class="literal">stroke</code>. <code class="literal">rgba()</code> expects three values between 0 and 255 for red, green, and blue, plus an alpha (transparency) value between 0.0 and 1.0:</p>

      <pre class="programlisting" data-language="html" id="circle_cx_id4">&lt;circle cx="25" cy="25" r="20" fill="rgba(128, 0, 128, 1.0)"/&gt;
&lt;circle cx="50" cy="25" r="20" fill="rgba(0, 0, 255, 0.75)"/&gt;
&lt;circle cx="75" cy="25" r="20" fill="rgba(0, 255, 0, 0.5)"/&gt;
&lt;circle cx="100" cy="25" r="20" fill="rgba(255, 255, 0, 0.25)"/&gt;
&lt;circle cx="125" cy="25" r="20" fill="rgba(255, 0, 0, 0.1)"/&gt;</pre>

      <div class="figure" id="RGBA_SVG_shapes">

        <div class="figure-contents">

          <div class="mediaobject"><em class="dotEPUBProtected"><img alt="Imagen" src="/static/Fig323.png"/> </em></div>

        </div>
<p class="fig">Figura 3-23. Formas RGBA SVG</p>
        <p class="fig">Figure 3-23. RGBA SVG shapes</p>

      </div>

<p class="it">Tenga en cuenta que con <code class="literal">rgba()</code>, la transparencia se aplica a los colores del <code class="literal">fill</code> y el <code class="literal">stroke</code> de forma independiente. Los siguientes circulos tienen los <code class="literal">fill</code> al 75 por ciento opacos, y sus <code class="literal">stroke</code> tan sólo al 25 por ciento opacos:</p>

      <p class="p" id="note_that_with_">Note that with <code class="literal">rgba()</code>, transparency is applied to the <code class="literal">fill</code> and <code class="literal">stroke</code> colors independently. The following circles’ <code class="literal">fill</code> is 75 percent opaque, and their <code class="literal">stroke</code>s are only 25 percent opaque:</p>

      <pre class="programlisting" data-language="html" id="circle_cx_id5">&lt;circle cx="25" cy="25" r="20" fill="rgba(128, 0, 128, 0.75)"
        stroke="rgba(0, 255, 0, 0.25)" stroke-width="10"/&gt;
&lt;circle cx="75" cy="25" r="20" fill="rgba(0, 255, 0, 0.75)"
        stroke="rgba(0, 0, 255, 0.25)" stroke-width="10"/&gt;
&lt;circle cx="125" cy="25" r="20" fill="rgba(255, 255, 0, 0.75)"
        stroke="rgba(255, 0, 0, 0.25)" stroke-width="10"/&gt;</pre>

<p class="it">Con esta transparencia aplicada, el resultado se muestra en la Figura 3-24, podemos ver que los stroke están alineados el centro de cada forma de  borde. Es decir, la carrera no es ni totalmente dentro ni fuera del objeto, pero es a la vez la mitad dentro y mitad fuera. Como resultado de esta transparencia, estos trazos individuales <code class="literal">10px</code> se parecen más a dos strokes <code class="literal">5px</code> separadas.</p>
      <p class="p" id="with_this_trans">With this transparency applied, and the result shown in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch03.html#More_RGBA_SVG_shapes" title="Figure 3-24. More RGBA SVG shapes">Figure 3-24</a>, we can see that strokes are aligned to the center of each shape’s edge. That is, the stroke is neither fully inside nor outside the object, but is both half in and half out. As a result of this transparency, these individual <code class="literal">10px</code> strokes look more like two separate <code class="literal">5px</code> strokes.</p>

      <div class="figure" id="More_RGBA_SVG_shapes">

        <div class="figure-contents">

          <div class="mediaobject"><em class="dotEPUBProtected"><img alt="Imagen" src="/static/Fig324.png"/> </em></div>

        </div>

        <p class="fig">Figure 3-24. More RGBA SVG shapes</p>

      </div>

       

      <p class="it">Para aplicar transparencia a un elemento completo, establecer un atributo de opacidad. La figura 3-25 ilustra algunos círculos completamente opacas.</p>
      <p class="p" id="to_apply_transp">To apply transparency to an entire element, set an <code class="literal">opacity</code> attribute. <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch03.html#Opaque_circles" title="Figure 3-25. Opaque circles">Figure 3-25</a> illustrates some completely opaque circles.</p>

      <div class="figure" id="Opaque_circles">

        <div class="figure-contents">

          <div class="mediaobject"><em class="dotEPUBProtected"><img alt="Imagen" src="/static/Fig325.png"/> </em></div>

        </div>
<p class="fig">Figura 3-25. Círculos opacos</p>
        <p class="fig">Figure 3-25. Opaque circles</p>

      </div>

<p class="it">La figura 3-26 muestra los mismos círculos, con valores de opacidad:</p>
      <p class="p" id="shows_the_same_"><a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch03.html#Semiopaque_circles" title="Figure 3-26. Semiopaque circles">Figure 3-26</a> shows the same circles, with <code class="literal">opacity</code> values:</p>

      <pre class="programlisting" data-language="html" id="circle_cx_id6">&lt;circle cx="25" cy="25" r="20" fill="purple" stroke="green" stroke-width="10"
        opacity="0.9"/&gt;
&lt;circle cx="65" cy="25" r="20" fill="green" stroke="blue" stroke-width="10"
        opacity="0.5"/&gt;
&lt;circle cx="105" cy="25" r="20" fill="yellow" stroke="red" stroke-width="10"
        opacity="0.1"/&gt;</pre>

      <div class="figure" id="Semiopaque_circles">

        <div class="figure-contents">

          <div class="mediaobject"><em class="dotEPUBProtected"> <img alt="Imagen" src="/static/Fig326.png"/> </em></div>

        </div>

        <p class="fig">Figure 3-26. Semiopaque circles</p>
      </div>

<p class="it">Usted puede emplear la <code class="literal">opacity</code> en un elemento que también tiene colores establecidos con <code class="literal">rgba()</code>. Al hacerlo, las transparencias se multiplican. Los círculos en la figura 3-27 utilizan los mismos valores RGBA para el <code class="literal">fill</code> y el <code class="literal">stroke</code>. El primer círculo no tiene conjunto de elementos de opacidad, pero los otros dos si:</p>

      <p class="p" id="you_can_employ_">You can employ <code class="literal">opacity</code> on an element that also has colors set with <code class="literal">rgba()</code>. When doing so, the transparencies are multiplied. The circles in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch03.html#More_opaque_circles" title="Figure 3-27. More opaque circles">Figure 3-27</a> use the same RGBA values for <code class="literal">fill</code> and <code class="literal">stroke</code>. The first circle has no element <code class="literal">opacity</code> set, but the other two do:</p>

      <pre class="programlisting" data-language="html" id="circle_cx_id7">&lt;circle cx="25" cy="25" r="20" fill="rgba(128, 0, 128, 0.75)"
        stroke="rgba(0, 255, 0, 0.25)" stroke-width="10"/&gt;
&lt;circle cx="65" cy="25" r="20" fill="rgba(128, 0, 128, 0.75)"
        stroke="rgba(0, 255, 0, 0.25)" stroke-width="10" opacity="0.5"/&gt;
&lt;circle cx="105" cy="25" r="20" fill="rgba(128, 0, 128, 0.75)"
        stroke="rgba(0, 255, 0, 0.25)" stroke-width="10" opacity="0.2"/&gt;</pre>

      <div class="figure" id="More_opaque_circles">

        <div class="figure-contents">

          <div class="mediaobject"><em class="dotEPUBProtected"> <img alt="Imagen" src="/static/Fig327.png"/> </em></div>

        </div>
<p class="fig">Figura 3-27. Círculos más opacos</p>
        <p class="fig">Figure 3-27. More opaque circles</p>

      </div>


<p class="it">Note como la opacidad del tercer círculo es de 0,2, o 20 por ciento. Sin embargo, su relleno púrpura ya tiene un valor alfa de 0,75, o 75 por ciento. El área púrpura, entonces, tiene una transparencia final de 0,2 veces 0,75 = 0,15, o 15 por ciento.</p>
      <p class="p" id="notice_how_the__id1">Notice how the third circle’s <code class="literal">opacity</code> is <code class="literal">0.2</code>, or 20 percent. Yet its purple fill already has an alpha value of <code class="literal">0.75</code>, or 75 percent. The purple area, then, has a final transparency of 0.2 times 0.75 = 0.15, or 15 percent.<a id="id500208" class="indexterm" href=""></a></p>



  <div class="" data-original-filename="3_tech_fundamentals.asciidoc" id="_a_note_on_compatibility">

    <div class="titlepage">

      <div>

        <h2 class="title">A Note on Compatibility</h2>

      </div>

    </div>
  </div>

<p class="it">Navegadores más viejo no soportan SVG. Por lo tanto, en términos generales, Internet Explorer versión 8 años en adelante no mostrar imágenes SVG en absoluto. Esto es un poco molesto porque la gente podría visitar su página sólo para ver el vacío en lugar de una visualización magnífica. Por otro lado, también D3 no funciona con los navegadores más antiguos (de nuevo, lo que significa IE8 y mayores), por lo que nunca hubiera funcionado en el primer lugar.</p>

    <p class="p" id="older_browsers_">Older browsers don’t support SVG. So, generally speaking, Internet Explorer version 8 and older will not display SVG images at all. This is a little annoying because people could visit your page only to see emptiness in place of a gorgeous visualization. On the other hand, D3 also does not work with older browsers (again, meaning IE8 and older), so it never would have worked in the first place.</p>

    <div class="note" id="d_can_be_made__id1">
<p class="it">D3 puede ser hecho para trabajar con Internet Explorer 8 mediante el empleo de la biblioteca Aight compatibilidad, pero que no te ayudan con las versiones antiguas de IE. r2d3 es una adaptación de D3 que integra Raphaël para efectos visuales dibujo, que debe conseguir que se remontan a IE7.</p>

      <p class="p" id="d_can_be_made__id2">D3 <span class="emphasis"><em>can</em></span> be made to work with IE8 by employing the <a class="ulink" href="https://github.com/shawnbot/aight" target="_top">Aight</a> compatibility library, but that doesn’t help with older versions of IE. <a class="ulink" href="https://github.com/mhemesath/r2d3/" target="_top">r2d3</a> is an adaptation of D3 that integrates <a class="ulink" href="http://raphaeljs.com/" target="_top">Raphaël</a> for drawing visuals, which should get you as far back as IE7.</p>

    </div>


<p class="it">En general, lo mejor es animar a la gente a mejorar y utilizar un navegador web que ha sido construido en los últimos años. Cuantas más personas se trasladan a los navegadores modernos, serán mejores sus experiencias en la web, y seran mayores a nuestras audiencias potenciales.</p>
    <p class="p" id="in_general_you">In general, your best bet is to encourage people to upgrade and use a web browser that has been built in the last few years. The more people move to modern browsers, the better their web experiences will be, and the larger our potential audiences.</p>


<p class="it">Dicho esto,  es educado notificar a los usuarios de navegadores antiguos la razón por cual la pieza no trabaja. Recomiendo usar Modernizr o una herramienta similar a JavaScript para  detectar si el navegador soporta SVG. Si lo hace, entonces usted puede cargar su código D3 y proceder como de costumbre. Si no admite SVG, a continuación, se puede visualizar una versión estática, no interactiva de sus visualización paralelamente a un mensaje que explica que es necesario un navegador actual. (Hay que ser agradable y proporcionan enlaces a las páginas de descarga de Chrome y Firefox. Solía enlazar a Safari también, pero Apple ahora se distribuye como parte del sistema operativo Mac, por lo que ya no está disponible como una descarga independiente.)</p>
    <p class="p" id="that_said_its">That said, it’s polite to notify users of older browsers why the piece isn’t working. I recommend using <a class="ulink" href="http://modernizr.com/" target="_top">Modernizr</a> or a similar JavaScript tool to detect whether or not the browser supports SVG. If it does, then you can load your D3 code and proceed as normal. If SVG is <span class="emphasis"><em>not</em></span> supported, then you can display a static, noninteractive version of your visualization alongside a message explaining that a current browser is needed. (Be nice and provide links to the <a class="ulink" href="http://www.google.com/chrome" target="_top">Chrome</a> and <a class="ulink" href="http://www.mozilla.org/en-US/firefox/new/" target="_top">Firefox</a> download pages. I used to link to <a class="ulink" href="http://www.apple.com/safari/" target="_top">Safari</a> as well, but Apple now distributes it as part of the Mac OS, so it’s no longer available as a separate download.)</p>

<p class="it">Por ejemplo, puede utilizar <code class="literal">Modernizr.load()</code> para comprobar los resultados de las   pruebas de Modernizr. Entonces, si pasan las pruebas (por ejemplo, porque el apoyo al SVG se detecta), luego le dice a Modernizr de seguir adelante y cargar D3 y su código JavaScript personalizado. Suelo tener algo como esto en la sección <code class="literal">head</code> de mi documento:</p>

    <p class="p">For example, you can use <code class="literal">Modernizr.load()</code> to check the results of Modernizr’s tests. Then, if the tests pass (for example, because SVG support <span class="emphasis"><em>is</em></span> detected), then tell Modernizr to go ahead and load D3 and your custom JavaScript code. I’d typically have something like this in the <code class="literal">&lt;head&gt;</code> of my document:</p>

    <pre class="programlisting" data-language="html" id="script_srcjs">&lt;script src="js/modernizr.js"&gt;&lt;/script&gt;

&lt;script type="text/javascript"&gt;
        Modernizr.load({
                test: Modernizr.svg &amp;&amp; Modernizr.inlinesvg,
                yep : [ 'js/d3.v3.min.js',
                        'js/script.js' ]
        });
&lt;/script&gt;</pre>

<p class="it">Esto carga en Modernizr, realiza las pruebas, y luego se molesta en cargar otro código sólo si las pruebas tienen éxito. (Esa es la parte “<code class="literal">yep</code>” .) Puede usar CSS o más JavaScript para definir lo que se muestra al usuario cuando la prueba falla , tales como una imagen estática de su visualización o un mensaje animando al usuario a que intente con un navegador más reciente . Aprenderá más acerca de cómo hacer esto en la documentación de Modernizr.</p>

    <p class="p">This loads Modernizr in, performs the tests, and then bothers loading the other code only if the tests succeed. (That’s the “<code class="literal">yep</code>” part.) You can use CSS or more JavaScript to define what shows up to the user when the test <span class="emphasis"><em>fails</em></span>, such as a static image of your visualization or a message encouraging the user to try a newer browser. Learn more about how to do this in the <a class="ulink" href="http://modernizr.com/docs/#load" target="_top">Modernizr documentation</a>.</p>
<p class="it">caniuse.com es un recurso fantástico para funciones del navegador compatibles. Ver la lista de navegadores con SVG s poyo.</p>


    <p class="p"><span class="emphasis"><em>caniuse.com</em></span> is a fantastic resource for supported browser features. See their list of <a class="ulink" href="http://caniuse.com/#search=svg" target="_top">browsers with SVG support</a>.</p>

<p class="it">La gente ha tratado de conseguir D3 trabajando en navegadores antiguos, a veces por mashing con Raphaël renderizar canvas, u otros medios hacky. Es técnicamente posible, pero yo no lo recomiendo.</p>

    <p class="p">People have tried to get D3 working in older browsers, sometimes by mashing it up with Raphaël to render to canvas, or other hacky means. It is technically possible, but I don’t recommend it.</p>


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