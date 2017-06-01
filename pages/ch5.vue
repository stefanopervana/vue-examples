<template>
  <main-layout>
  <div class="ch5">
    <h1>{{ msg }}</h1>
    
    <div class="block">
 <h1>Chapter 5. Data</h1>
<p class="it">Data es un término muy amplio, sólo un poco menos vago que la información de casi todo lo que abarca. Qué son los datos? (¿Qué no son los datos?) ¿Qué tipos de datos están ahí, y cuales podemos utilizar con D3?</p>
<p class="p" id="data_is_an_extr"><span class="emphasis"><em>Data</em></span> is an extremely broad term, only slightly less vague than the nearly all-encompassing <span class="emphasis"><em>information</em></span>. What is data? (What <span class="emphasis"><em>isn’t</em></span> data?) What kinds of data are there, and what can we use with D3?<a id="ix_data" class="indexterm" href=""></a></p>
 <p class="it">En términos generales, los datos son información estructurada con  significado potencial.</p>
  <p class="p" id="broadly_speakin" >Broadly speaking, data is structured information with potential for meaning.</p>

<p class="it">En el contexto de la programación para la visualización, los datos se almacenan en un archivo digital, típicamente en forma de texto o binario. Por supuesto, potencialmente cada pieza de material efímero digital puede ser considerada como "datos" - no sólo texto, sino bits y bytes que representan imágenes, audio, video, databases, streams, models, archivos, y cualquier otra cosa.</p>
  <p class="p" id="in_the_context_" >In the context of programming for visualization, data is stored in a digital file, typically in either text or binary form. Of course, potentially every piece of digital ephemera may be considered “data”—not just text, but bits and bytes representing images, audio, video, databases, streams, models, archives, and anything else.<a id="id501486" class="indexterm" href=""></a></p>
  <p class="it">Dentro del ámbito de D3 y visualización basada en el navegador, sin embargo, nos limitaremos a los datos basados en texto. Es decir, cualquier cosa que se puede representar como números y cadenas de caracteres alfabéticos. Si usted puede conseguir sus datos en un archivo .txt plano, un archivo .csv de valores separados por comas, o un documento JSON, puede utilizar D3.</p>
  <p class="p" id="within_the_scop" >Within the scope of D3 and browser-based visualization, however, we will limit ourselves to <span class="emphasis"><em>text-based data</em></span>. That is, anything that can be represented as numbers and strings of alpha characters. If you can get your data into a <span class="emphasis"><em>.txt</em></span> plain text file, a <span class="emphasis"><em>.csv</em></span> comma-separated value file, or a <span class="emphasis"><em>.json</em></span> JSON document, then you can use it with D3.<a id="id501517" class="indexterm" href=""></a><a id="id501525" class="indexterm" href=""></a><a id="id501531" class="indexterm" href=""></a><a id="id501537" class="indexterm" href=""></a><a id="id501543" class="indexterm" href=""></a></p>

<p class="it">Sean cuales sean sus datos, pueden ser útiles y visuales cuando se unen a algo. En la jerga de D3, los datos deben estar unidos a elementos dentro de la página. Vamos a abordar cómo crear nuevos elementos de la página primero. Luego adjuntar los datos de esos elementos será un juego de niños.</p>
  <p class="p" id="whatever_your_d" >Whatever your data, it can’t be made useful and visual until it is <span class="emphasis"><em>attached</em></span> to something. In D3 lingo, the data must be <span class="emphasis"><em>bound</em></span> to elements within the page. Let’s address how to create new page elements first. Then attaching data to those elements will be a cinch.<a id="ix_pgelem" class="indexterm" href=""></a></p>
    <div class="" data-original-filename="5_data.asciidoc" id="_generating_page_elements">

    <div class="titlepage">


        <h2 class="title">Generating Page Elements</h2>

      </div>

    </div>

<p class="it">Por lo general, cuando se utiliza D3 para generar nuevos elementos DOM, los nuevos elementos serán círculos, rectángulos u otras formas visuales que representan sus datos. Pero para evitar cuestiones confusas, Empezaremos con un ejemplo sencillo y creamos un humilde elemento de  párrafo <code class="literal">p</code>.</p>
    <p class="p" id="typically_when">Typically, when using D3 to generate new DOM elements, the new elements will be circles, rectangles, or other visual forms that represent your data. But to avoid confusing matters, we’ll start with a simple example and create a lowly <code class="literal">p</code> paragraph element.</p>
<p class="it">Comience por crear un nuevo documento con nuestra simple plantilla HTML a partir del último capítulo. Lo puede encontrar en los archivos de código de muestra como 01_empty_page_template.html, y parece que el siguiente código. (Ojos de águila espectadores se darán cuenta de que he modificado la ruta src aquí debido al trabajo con la estructura de directorios de los ejemplos de código. Si eso no significa nada para ti, no te preocupes al respecto.)</p>
    <p class="p" id="begin_by_creati">Begin by creating a new document with our simple HTML template from the last chapter. You can find it in the sample code files as <span class="emphasis"><em>01_empty_page_template.html</em></span>, and it looks like the following code. (Eagle-eyed viewers will notice that I’ve modified the <code class="literal">src</code> path here due to work with the directory structure of the code samples. If that doesn’t mean anything to you, don’t worry about it.)</p>

    <pre class="programlisting" data-language="html" id="doctype_html_id4">&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
    &lt;head&gt;
        &lt;meta charset="utf-8"&gt;
        &lt;title&gt;D3 Page Template&lt;/title&gt;
        &lt;script type="text/javascript" src="../d3/d3.v3.js"&gt;&lt;/script&gt;
    &lt;/head&gt;
    &lt;body&gt;
        &lt;script type="text/javascript"&gt;
            // Your beautiful D3 code will go here
        &lt;/script&gt;
    &lt;/body&gt;
&lt;/html&gt;</pre>
<p class="it">Abra esta página en el navegador web. Asegúrese de que usted está accediendo a la página a través de su servidor web local, como hemos comentado en el capítulo 4.</p>
    <p class="p" id="open_that_page_">Open that page in your web browser. Make sure you’re accessing the page via your local web server, as we discussed in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch04.html" title="Chapter 4. Setup">Chapter 4</a>. So the URL in your browser’s location bar should look something like this:</p>
    <pre class="programlisting" id="httplocalhos34">http://localhost:8888/d3-book/chapter_05/01_empty_page_template.html</pre>

  <p class="it">Por lo que la URL en la barra de direcciones de su navegador debería ser algo como esto: <span class="emphasis"><em>file:///</em></span> instead of <span class="emphasis"><em>http://</em></span>. Confirmar que la URL <span class="emphasis"><em>no</em></span> se parece a esto:</p>

    <p class="p" id="if_not_viewed_t">If not viewed through a web server, the URL path will start with <span class="emphasis"><em>file:///</em></span> instead of <span class="emphasis"><em>http://</em></span>. Confirm that the URL does <span class="emphasis"><em>not</em></span> look like this:</p>

    <pre class="programlisting" id="filedbo">file:///…/d3-book/chapter_05/01_empty_page_template.html</pre>

<p class="it">Una vez que este visualizando la página, abra el inspector web. (A modo de recordatorio, consulte "Herramientas de Desarrollo" sobre la manera de hacer eso.) Usted debe ver una página Web vacía, con el contenido del DOM que se muestran en la Figura 5-1.</p>
    <p class="p" id="once_youre_vie">Once you’re viewing the page, pop open the web inspector. (As a reminder, see <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch03.html#developer_tools_3" title="Developer Tools">“Developer Tools”</a> on how to do that.) You should see an empty web page, with the DOM contents shown in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch05.html#Web_inspector" title="Figure 5-1. Web inspector">Figure 5-1</a>.</p>

    

    <div class="figure" id="Web_inspector">

      <div class="figure-contents">

           <img src="/static/r8_mae2uVb-img1.png" alt="Web inspector"/>

        </div>

      </div>

            <p class="fig">Figure 5-1. Web inspector</p>




<p class="it">De vuelta en su editor de texto, se sustituye el comentario entre las etiquetas <code class="literal">script</code> con:</p>
    <p class="p" id="back_in_your_te">Back in your text editor, replace the comment between the <code class="literal">script</code> tags with:</p>
<pre class="programlisting" data-language="javascript" id="dselectbody_id1">d3.select("body").append("p").text("New paragraph!");</pre>
  <p class="it">Guardar y volver a cargar, y Voilà! Hay texto en la ventana del navegador antes vacía, y el inspector web se parece a la Figura 5-2.</p>

    <p class="p" id="save_and_refres">Save and refresh, and voilà! There is text in the formerly empty browser window, and the web inspector will look like <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch05.html#Web_inspector_again" title="Figure 5-2. Web inspector, again">Figure 5-2</a>.</p>  
    <div class="figure" id="Web_inspector_again">

      <div class="figure-contents">

        <div class="mediaobject">

          <img src="/static/r8_mae2uVb-img2.png" alt="Web inspector, again"/>

        </div>

      </div>

      <p class="fig">Figure 5-2. Web inspector, again</p>

    </div>
<p class="it">¿Ve la diferencia? Ahora, en el DOM, hay un nuevo elemento de párrafo que se generó sobre la marcha! Esto podría no ser emocionante todavía, pero pronto usara una técnica similar para generar dinámicamente decenas o cientos de elementos, cada uno correspondiente a una pieza de su dataset.</p>
    <p class="p" id="see_the_differe">See the difference? Now in the DOM, there is a new paragraph element that was generated on the fly! This might not be exciting yet, but you will soon use a similar technique to dynamically generate tens or hundreds of elements, 
 <p class="it">Vamos a ver lo que acaba de ocurrir. (Puede seguir junto con 02_new_element.html.) Para entender la primera línea de código D3 primero debe conocer la cadena sintáctica de su nuevo mejor amigo.</p>
    <p class="p" id="lets_walk_thro">Let’s walk through what just happened. (You can follow along with <span class="emphasis"><em>02_new_element.html</em></span>.) To understand that first line of D3 code, you must first meet your new best friend, <span class="emphasis"><em>chain syntax</em></span>.</p>

    <div class="sect2" id="_chaining_methods">

      <div class="titlepage">

        <div>

          <h3 class="title">Chaining Methods</h3>

          <h3>Los Métodos de Encadenamiento</h3>

        </div>

      </div>

<p class="it">D3 inteligentemente emplea una técnica llamada sintaxis de cadena, que se puede reconocer a partir de jQuery. Por métodos de "encadenamiento", junto con períodos, puede realizar varias acciones en una sola línea de código. Puede ser rápido y fácil, pero es importante entender cómo funciona, para ahorrarse horas de dolores de cabeza de depuración posterior.</p>
      <p class="p" id="d_smartly_empl">D3 smartly employs a technique called <span class="emphasis"><em>chain syntax</em></span>, which you might recognize from jQuery. By “chaining” methods together with periods, you can perform several actions in a single line of code. It can be fast and easy, but it’s important to understand how it works, to save yourself hours of debugging headaches later.<a id="id502050" class="indexterm" href=""></a><a id="id502056" class="indexterm" href=""></a></p>

 <p class="it">Por cierto, las funciones y los métodos son sólo dos palabras diferentes para el mismo concepto: un trozo de código que acepta un argumento como entrada, realiza alguna acción, y devuelve alguna otra información como salida.</p>
      <p class="p" id="by_the_way_fun">By the way, <span class="emphasis"><em>functions</em></span> and <span class="emphasis"><em>methods</em></span> are just two different words for the same concept: a chunk of code that accepts an argument as input, performs some action, and returns some other information as output.<a id="id502080" class="indexterm" href=""></a><a id="id502088" class="indexterm" href=""></a></p>

    

      <p class="p" id="the_following_c">The following code:</p>

      <pre class="programlisting" data-language="javascript" id="dselectbody_id2">d3.select("body").append("p").text("New paragraph!");</pre>

    <p class="it">podría parecer un lío grande, especialmente si usted es nuevo en la programación. Así que lo primero que debe saber es que JavaScript, como HTML, no prestan atención a espacios en blanco y saltos de línea, por lo que puede poner cada método en su propia línea de legibilidad:</p>
      <p class="p" id="might_look_like">might look like a big mess, especially if you’re new to programming. So the first thing to know is that JavaScript, like HTML, doesn’t care about whitespace and line breaks, so you can put each method on its own line for legibility:</p>

  

      <pre class="programlisting" data-language="javascript" id="dselectbody_id3">d3.select("body")
    .append("p")
    .text("New paragraph!");</pre>

<p class="it">Tanto yo como su optometrista recomendamos poner cada método en su propia línea con sangría. Sin embargo, los programadores tienen su propio estilo de codificación; utilizar guiones sean cuales sean, saltos de línea y espacios en blanco (tabuladores o espacios) es más legible para usted.</p>
      <p class="p" id="both_i_and_your">Both I and your optometrist highly recommend putting each method on its own indented line. But programmers have their own coding style; use whatever indents, line breaks, and whitespace (tabs or spaces) are most legible for you.<a id="id502275" class="indexterm" href=""></a><a id="id502283" class="indexterm" href=""></a></p>   

    </div>
    <div class="sect2" id="_one_link_at_a_time">

      <div class="titlepage">

        <div>

          <h3 class="title">One Link at a Time</h3>

          <h3>Un enlace a la vez</h3>

        </div>

      </div>

<p class="it">Vamos a deconstruir cada línea en esta cadena de código:</p>
      <p class="p" id="lets_deconstru">Let’s deconstruct each line in this chain of code:</p>

 
      <div class="variablelist" id="d_references_t">

        <dl class="variablelist">
          <dt class="programlisting"><span class="term"> <code class="literal">d3</code> </span></dt>
<dd class="p">Hace referencia al objeto D3, por lo que puede acceder a sus métodos. Nuestra aventura con D3 comienza aquí.</dd>
          <dd class="p"> References the D3 object, so we can access its methods. Our D3 adventure begins here. </dd>
          <dt class="programlisting"><span class="term"> <code class="literal">.select("body")</code> </span></dt>
<dd class="it"> Le da al método <code class="literal">select()</code> un selector CSS como entrada, y ha de devolver una referencia al primer elemento en el DOM que coincida. (Uso <code class="literal">selectAll()</code> cuando se necesita más de un elemento.) En este caso, sólo queremos el <code class="literal">body</code> del documento, por lo que una referencia al <code class="literal">body</code> se traspasa al siguiente método en nuestra cadena.</dd>
          <dd class="p"> Give the <a class="ulink" href="http://bit.ly/12h4SF1" target="_top"><code class="literal">select()</code></a> method a CSS selector as input, and it will return a reference to the first element in the DOM that matches. (Use <a class="ulink" href="http://bit.ly/WwINKs" target="_top"><code class="literal">selectAll()</code></a> when you need more than one element.) In this case, we just want the <code class="literal">body</code> of the document, so a reference to <code class="literal">body</code> is handed off to the next method in our chain. </dd>
          <dt class="programlisting"><span class="term"> <code class="literal">.append("p")</code> </span></dt>
<dd class="it"><code class="literal">append()</code> crea el nuevo elemento DOM que especifica y lo anexa al final (pero justo en el interior) cualquiera de las selecciones actúa sobre él. En nuestro caso, queremos crear una nueva página dentro del cuerpo. Especificamos <code class="literal">"p"</code> como argumento de entrada, pero este método también ve la referencia al cuerpo que fue aprobada por la cadena a partir del método de <code class="literal">select()</code>. Por lo que un punto <code class="literal">"p"</code> vacío se añade al cuerpo. Por último, <code class="literal">append()</code> toma una referencia al nuevo elemento que acaba de crear.</dd>
          <dd class="p"> <a class="ulink" href="https://github.com/mbostock/d3/wiki/Selections#wiki-append" target="_top"><code class="literal">append()</code></a> creates whatever new DOM element you specify and appends it to the end (but <span class="emphasis"><em>just inside</em></span>) of whatever selection it’s acting on. In our case, we want to create a new <code class="literal">p</code> within the <code class="literal">body</code>. We specified <code class="literal">"p"</code> as the input argument, but this method also sees the reference to <code class="literal">body</code> that was passed down the chain from the <code class="literal">select()</code> method. So an empty <code class="literal">p</code> paragraph is <span class="emphasis"><em>appended</em></span> to the <code class="literal">body</code>. Finally, <code class="literal">append()</code> hands off a reference to the new element it just created. </dd>
          <dt class="programlisting"><span class="term"> <code class="literal">.text("New paragraph!")</code> </span></dt>
<dd class="it">toma un string y lo inserta entre las etiquetas de apertura y cierre de la selección actual. Debido a que el método anterior transmite una referencia a nuestra nueva página, el código simplemente inserta el nuevo texto entre etiquetas. (En los casos donde hay contenido existente, se sobrescribe.)</dd>
          <dd class="p"> <a class="ulink" href="https://github.com/mbostock/d3/wiki/Selections#wiki-text" target="_top"><code class="literal">text()</code></a> takes a string and inserts it between the opening and closing tags of the current selection. Because the previous method passed down a reference to our new <code class="literal">p</code>, this code just inserts the new text between <code class="literal">&lt;p&gt;</code> and <code class="literal">&lt;/p&gt;</code>. (In cases where there is existing content, it will be overwritten.) </dd>
          <dt class="programlisting"><span class="term"> <code class="literal">;</code> </span></dt>
<dd class="it">El punto y coma lo más importante indica el final de esta línea de código. Cadena terminada.</dd>
          <dd class="p"> The all-important semicolon indicates the end of this line of code. Chain over. </dd>

        </dl>

      </div>

    </div>

    <div class="sect2" id="_the_hand_off">

      <div class="titlepage">

        <div>

          <h3 class="title">The Hand-off</h3>

        </div>

      </div>

      

<p class="it">Muchos, pero no todos, los métodos D3 devuelven una selección (en realidad, una referencia a una selección), lo que permite esta útil técnica de encadenamiento de método. Típicamente, un método devuelve una referencia al elemento que simplemente actúa sobre él, pero no siempre.</p>

      <p class="p" id="many_but_not_a">Many, but not all, D3 methods return a selection (actually, a reference to a selection), which enables this handy technique of method chaining. Typically, a method returns a reference to the element that it just acted on, but not always.<a id="id502536" class="indexterm" href=""></a></p>

<p class="it">Así que recuerde esto: cuando encadena métodos, ordena las cosas. El tipo de salida de un metodo tiene que coincidir con el tipo de entrada esperada por el método siguiente en la cadena. Si las entradas y salidas adyacentes no coinciden, el hand-off funcionará como un bastón caído en una carrera de relevos de la escuela media.</p>
      <p class="p" id="so_remember_thi">So remember this: when chaining methods, order matters. The output type of one method has to match the input type expected by the next method in the chain. If adjacent inputs and outputs are mismatched, the hand-off will function more like a dropped baton in a middle-school relay race.</p>
      
<p class="it">Cuando trata de reproducir lo que cada función espera y retorna, la referencia de la API es su amiga. Contiene información detallada sobre cada método, incluyendo si devuelve o no devuelve una selección.</p>


      <p class="p" id="when_sussing_ou">When sussing out what each function expects and returns, <a class="ulink" href="https://github.com/mbostock/d3/wiki/API-Reference" target="_top">the API reference</a> is your friend. It contains detailed information on each method, including whether or not it returns a selection.<a id="id502566" class="indexterm" href=""></a><a id="id502575" class="indexterm" href=""></a></p>

    </div>

    <div class="sect2" id="_going_chainless">

      <div class="titlepage">

        <div>

          <h3 class="title">Going Chainless</h3>

        </div>

      </div>

<p class="it">Nuestro código de ejemplo se podría reescribir sin sintaxis de cadena:</p>
      <p class="p" id="our_sample_code">Our sample code could be rewritten without chain syntax:</p>
      
      <pre class="programlisting" data-language="javascript" id="var_body__ds">var body = d3.select("body");
var p = body.append("p");
p.text("New paragraph!");</pre>

      

<p class="it">Uf! Que desastre. Sin embargo, habrá ocasiones en las que necesitará romper la cadena, como cuando usted está llamando tantas funciones que no tiene sentido juntarlas en un string. O simplemente porque desea organizar el código de una manera que tenga más sentido para usted.</p>

      <p class="p" id="ugh_what_a_mes">Ugh! What a mess. Yet there will be times you need to break the chain, such as when you are calling so many functions that it doesn’t make sense to string them all together. Or just because you want to organize your code in a way that makes more sense to you.</p>      

<p class="it">Ahora que ya sabe cómo generar nuevos elementos de página con D3, es el momento de adjuntar datos en ellas.</p>

      <p class="p" id="now_that_you_kn">Now that you know how to generate new page elements with D3, it’s time to attach data to them.<a id="id502733" class="indexterm" href=""></a><a id="id502742" class="indexterm" href=""></a></p>

  <div class="" data-original-filename="5_data.asciidoc" id="_binding_data">

    <div class="titlepage">

      <div>

        <h2 class="title">Binding Data</h2>

        <h2>El enlace de datos</h2>

      </div>

    </div>

<p class="it">Que es vinculante, y por qué iba a querer hacerlo con mis datos?</p>
    <p class="p" id="what_is_binding">What is binding, and why would I want to do it to my data?<a id="ix_databind" class="indexterm" href=""></a><a id="ix_pebind" class="indexterm" href=""></a></p>
   
<p class="it">La visualización de datos es un proceso de datos del mapping para efectos visuales. Los datos de las propiedades visuales, por fuera. Quizás los números más grandes hagan barras más altas, o las categorías especiales tenegan colores más brillantes. Las reglas de asignación las pone usted.</p>


    <p class="p" id="data_visualizat_id3">Data visualization is a process of <span class="emphasis"><em>mapping</em></span> data to visuals. Data in, visual properties out. Maybe bigger numbers make taller bars, or special categories trigger brighter colors. The mapping rules are up to you.<a id="id502809" class="indexterm" href=""></a></p>


<p class="it">Con D3, atamos nuestros valores de entrada de datos a los elementos en el DOM. La unión es como abrochar o asociar datos a los elementos específicos, por lo que más adelante se puede hacer referencia a esos valores para aplicar reglas de asignación. Sin la etapa de unión, tenemos un montón de datos en el DOM, imposibles de mapear. Nadie busca eso.</p>

    <p class="p" id="with_d_we_bin">With D3, we <span class="emphasis"><em>bind</em></span> our data input values to elements in the DOM. Binding is like “attaching” or associating data to specific elements, so that later you can reference those values to apply mapping rules. Without the binding step, we have a bunch of data-less, unmappable DOM elements. No one wants that.</p>

    <div class="sect2" id="_in_a_bind">

      <div class="titlepage">

        <div>

          <h3 class="title">In a Bind</h3>

        </div>

      </div>   

 <p class="it">Utilizamos el método de D3 <code class="literal">selection.data()</code> para enlazar datos a los elementos DOM. Pero hay dos cosas que necesitamos en primer lugar, antes de que podamos enlazar datos:</p>

      <p class="p" id="we_use_ds_sel">We use D3’s <a class="ulink" href="https://github.com/mbostock/d3/wiki/Selections#wiki-data" target="_top"><code class="literal">selection.data()</code></a> method to bind data to DOM elements. But there are two things we need in place first, before we can bind data:</p>

      <div class="itemizedlist" id="the_data_a_sele">

        <ul class="itemizedlist">

          <li class="p"> The data </li>

          <li class="p"> A selection of DOM elements </li>



        </ul>

      </div>

      

<p class="it">Vamos a enfrentarlos a estos de a uno a la vez.</p>

      <p class="p" id="lets_tackle_th">Let’s tackle these one at a time.</p>

    </div>

    <div class="sect2" id="_data"> <div class="titlepage"><div><h3 class="title">Data</h3></div></div> 


<p class="it">D3 es inteligente sobre el manejo de diferentes tipos de datos, por lo que aceptará prácticamente cualquier serie de números, cadenas u objetos (sí contiene otras arrays o  key/valor de a pares). Puede manejar JSON (y GeoJSON) con gracia, e incluso tiene un método integrado para ayudar a que se cargue en archivos CSV.</p>

    <p class="p" id="d_is_smart_abo">D3 is smart about handling different kinds of data, so it will accept practically any array of numbers, strings, or objects (themselves containing other arrays or key/value pairs). It can handle JSON (and GeoJSON) gracefully, and even has a built-in method to help you load in CSV files.<a id="id502899" class="indexterm" href=""></a><a id="id502907" class="indexterm" href=""></a></p> 

<p class="it">Sin embargo, para simplificar las cosas, por ahora vamos a empezar con un array de cinco números. Aquí está nuestra base de datos de ejemplo:</p>

<p class="p" id="but_to_keep_thi">But to keep things simple, for now we will start with a boring array of five numbers. Here is our sample dataset:</p> 

<pre class="programlisting" data-language="javascript" id="var_dataset___id1">var dataset = [ 5, 10, 15, 20, 25 ];</pre> 

<p class="it">Si usted está sintiendose aventurero, o ya tiene algunos datos en formato CSV o JSON que desea usar, aquí está la manera de hacer eso. De lo contrario, vaya directamente a "Por favor haga su selección".</p><a id="id503013" class="indexterm" href=""></a><a id="id503018" class="indexterm" href=""></a>
<p class="p" id="if_youre_feeli">If you’re feeling adventurous, or already have some data in CSV or JSON format that you want to play with, here’s how to do that. Otherwise, just skip ahead to <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch05.html#please_make_your_selection_5" title="Please Make Your Selection">“Please Make Your Selection”</a>. </p>

<div class="sect3" id="_loading_csv_data">

<div class="titlepage"><div>

<h4 class="title">Loading CSV data</h4><h4>Carga de datos de CSV</h4></div></div> 

<p class="it">CSV es sinónimo de valores separados por comas. Un archivo de datos CSV puede ser algo como esto:</p>
<p class="p" id="csv_stands_for_">CSV stands for comma-separated values. A CSV data file might look something like this:</p>

<pre class="screen" id="fooddeliciousn">Food,Deliciousness
Apples,9
Green Beans,5
Egg Salad Sandwich,4
Cookies,10
Vegemite,0.2
Burrito,7</pre> 

<p class="it">Cada línea del archivo tiene el mismo número de valores (dos, en este caso), y los valores están separados por una coma. La primera línea del archivo a menudo sirve como cabecera, proporcionando los nombres de cada una de las "columnas" de datos.</p>

<p class="p" id="each_line_in_th">Each line in the file has the same number of values (two, in this case), and values are separated by a comma. The first line in the file often serves as a header, providing names for each of the “columns” of data.</p> 

<p class="it">Si tiene datos en un archivo de Excel, es probable que este siga una estructura similar de filas y columnas. Para obtener esos datos en D3, abralo en Excel, a continuación, elija Guardar como ... y seleccione CSV como tipo de archivo.</p>
<p class="p" id="if_you_have_dat">If you have data in an Excel file, it probably follows a similar structure of rows and columns. To get that data into D3, open it in Excel, then choose Save as… and select CSV as the file type.</p>

<p class="it">Si hemos salvado los datos CSV precedentes en un archivo llamado food.csv, entonces podríamos cargar el archivo en D3 utilizando el método d3.csv():</p>

<p class="p" id="if_we_saved_the">If we saved the preceding CSV data into a file called <span class="emphasis"><em>food.csv</em></span>, then we could load the file into D3 by using the <code class="literal">d3.csv()</code> method:</p>

<pre class="programlisting" data-language="javascript" id="dcsvfoodcs">d3.csv("food.csv", function(data) {
    console.log(data);
});</pre>
 

<p class="it"><code class="literal">csv()</code> toma dos argumentos: una string que representa la ruta del archivo CSV para cargar, y una función anónima, para ser utilizada como una función de callback. La función de callback es citada sólo después de que el archivo CSV se ha cargado en la memoria. Así que usted puede estar seguro de que, en el momento de  callback, el metodo <code class="literal">d3.csv()</code> llevara a cabo la ejecución.</p>

 <p class="p" id="csv_takes_two"><code class="literal">csv()</code> takes two arguments: a string representing the path of the CSV file to load in, and an anonymous function, to be used as a <span class="emphasis"><em>callback function</em></span>. The callback function is “called” only <span class="emphasis"><em>after</em></span> the CSV file has been loaded into memory. So you can be sure that, by the time the callback is called, <code class="literal">d3.csv()</code> is done executing.<a id="id503200" class="indexterm" href=""></a><a id="id503206" class="indexterm" href=""></a></p>  


<p class="it">Cuando se la llama, la función anónima entrega el resultado del proceso de carga y el análisis del CSV; es decir, los datos. Aquí estoy dándole el nombre datos, pero esto podría llamarse como quiera. Debe utilizar esta función de callback para hacer todas las cosas que puede hacer sólo después de que los datos se han cargado. En el anterior codigo de ejemplo, sólo estamos logueando el valor del array de datos a la consola, para verificar que se cargo, como se muestra en la Figura 5-3. (Ver 03_csv_loading_example.html en el código de ejemplo.)</p>

<p class="p" id="when_called_th">When called, the anonymous function is handed the result of the CSV loading and parsing process; that is, the data. Here I’m naming it <code class="literal">data</code>, but this could be called whatever you like. You should use this callback function to do all the things you can do only <span class="emphasis"><em>after</em></span> the data has been loaded. In the preceding example, we are just logging the value of the <code class="literal">data</code> array to the console, to verify it, as shown in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch05.html#Array_logged_to_console" title="Figure 5-3. Array logged to console">Figure 5-3</a>. (See <span class="emphasis"><em>03_csv_loading_example.html</em></span> in the example code.)</p>


<div class="figure" id="Array_logged_to_console"> <div class="figure-contents"><div class="mediaobject"><img src="/static/r8_mae2uVb-img3.png" alt="Array logged to console"/></div></div>



<p class="fig">Figure 5-3. Array logged to console</p> 
</div> 


<p class="it">Se puede ver que la data es una array (debido a los corchetes [] en cada extremo) con seis elementos, cada uno de los cuales es un objeto. Mediante la selección de los triángulos desplegables junto a cada objeto, podemos ver sus valores (véase la Figura 5-4).</p>
<p class="p" id="you_can_see_tha">You can see that <code class="literal">data</code> is an array (because of the hard brackets <code class="literal">[]</code> on either end) with six elements, each of which is an object. By toggling the disclosure triangles next to each object, we can see their<a id="id503287" class="indexterm" href=""></a> values (see <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch05.html#Array_elements_expanded" title="Figure 5-4. Array elements expanded">Figure 5-4</a>).</p> 


<div class="figure" id="Array_elements_expanded"> <div class="figure-contents"><div class="mediaobject"><img src="/static/r8_mae2uVb-img4.png" alt="Array elements expanded"/></div></div>

<p class="fig">Figure 5-4. Array elements expanded</p> 
</div> 

<p class="it">Aha! Cada objeto tiene una propiedad Food y una propiedad Deliciousness, con valores que corresponden a los valores de nuestra CSV! (También hay una tercera propiedad, <code class="literal">__proto__</code>, pero eso tiene que ver con la forma en que JavaScript se encarga de los objetos, y puede ignorar eso por ahora.) D3 ha empleado la primera fila de la CSV para los nombres de propiedades, y las filas posteriores de valores. Es posible que no se de cuenta, pero esto sólo lo salvó de perder un montón de tiempo.</p>

<p class="p" id="aha_each_objec">Aha! Each object has both a <code class="literal">Food</code> property and a <code class="literal">Deliciousness</code> property, the values of which correspond to the values in our CSV! (There is also a third property, <code class="literal">__proto__</code>, but that has to do with how JavaScript handles objects, and you can ignore it for now.) D3 has employed the first row of the CSV for property names, and subsequent rows for values. You might not realize it, but this just saved you a <span class="emphasis"><em>lot</em></span> of time.<a id="id503347" class="indexterm" href=""></a></p>

<p class="it">Una cosa más a tener en cuenta es que cada valor de la CSV se almacena como una string, incluso los números. (Lo digo, porque 9 está rodeado por comillas, como en "9" y no simplemente 9.) Esto podría provocar un comportamiento inesperado después, si se intenta hacer referencia a su datos como un valor numérico, pero todavía se escribe como un string.</p>

<p class="p" id="one_more_thing__id1">One more thing to note is that each value from the CSV is stored as a string, even the numbers. (You can tell because 9 is surrounded by quotation marks, as in <code class="literal">"9"</code> and not simply <code class="literal">9</code>.) This could cause unexpected behavior later, if you try to reference your data as a numeric value but it is still typed as a string.</p>

 
<div class="sect33" id="pipe">

 <div class="titlepage">
<div><h4 class="title">Handling Data Loading Errors</h4></div>


</div> 

<p class="it">Tenga en cuenta que <code class="literal">d3.csv()</code> es un método asíncrono, lo que significa que el resto de su código se ejecuta simultáneamente incluso mientras se está a la espera de el archivo JavaScript  para terminar la descarga en el navegador. (Lo mismo es cierto que D3 tiene otras funciones que cargan los recursos externos, tales como <code class="literal">d3.json()</code>).</p>

<p class="p" id="note_that_dcs">Note that <code class="literal">d3.csv()</code> is an <span class="emphasis"><em>asynchronous</em></span> method, meaning that the rest of your code is executed even while JavaScript is simultaneously waiting for the file to finish downloading into the browser. (The same is true of D3’s other functions that load external resources, such as <code class="literal">d3.json()</code>.)<a id="id503406" class="indexterm" href=""></a><a id="id503412" class="indexterm" href=""></a></p> 



<p class="it">Esto puede potencialmente ser muy confuso, ya que - como un humano razonable - podría suponer que el archivo CSV de datos está disponible, cuando en realidad no se ha terminado de cargar aún. Un error común es incluir referencias a los datos externos fuera de la función de callback. Ahorrese algunos dolores de cabeza y asegúrese de hacer referencia a los datos sólo desde dentro de la función callback (o desde dentro de otras funciones que llamará dentro de la función de callback).</p>
<p class="p" id="this_can_potent">This can potentially be <span class="emphasis"><em>very</em></span> confusing, because you—as a reasonable human person—might assume that the CSV file’s data is available, when in fact it hasn’t finished loading yet. A common mistake is to include references to the external data <span class="emphasis"><em>outside of</em></span> the callback function. Save yourself some headaches and make sure to reference your data only from <span class="emphasis"><em>within</em></span> the callback function (or from within other functions that you call within the callback function).<a id="id503442" class="indexterm" href=""></a><a id="id503448" class="indexterm" href=""></a></p>

<p class="it">En lo personal, me gusta declarar una variable global en primer lugar, a continuación, llamar a <code class="literal">d3.csv()</code> para cargar los datos. Dentro de la función de callback, copio los datos en mi variable global (por lo que estan disponibles para todas mis funciones posteriores), finalmente llamo a cualquiera de las funciones que dependen de la presencia de esos datos. Por ejemplo:</p>

<p class="p" id="personally_i_l">Personally, I like to declare a global variable first, then call <code class="literal">d3.csv()</code> to load the data. Within the callback function, I copy the data into my global variable (so it’s available to all of my subsequent functions), and finally I call any functions that rely on that data being present. For example:</p>

<pre class="programlisting" data-language="javascript" id="var_dataset__id1">var dataset;  //Global variable

d3.csv("food.csv", function(data) {
    dataset = data;   

    <p class="it">//Una vez cargada, copie a dataset</p>
    <p> //Once loaded, copy to dataset.</p>

    
    generateVis();    <p> //Then call other functions that</p> 


    <p class="it">//Luego llame a otras funciones</p>

    hideLoadingMsg(); 

    <p class="it">//Depende de la presencia de datos</p>
    <p> //depend on data being present.</p> 
    
});</pre> 


<p class="it">Para confundir más las cosas, la función de callback <strong>se ejecuta si el archivo de datos se cargó correctamente o no</strong>. Eso esta bien, si la conexión de red falla o el nombre del archivo está mal escrito, o por alguna razón se produce un error en el extremo del servidor web, todavía se ejecutará la función de callback. Cuando los datos no se puede cargar, y llama a funciones que se basan en que esten presentes los datos, es probable que vea un error en la consola, y la visualización no sea creada. Este escenario podría ocurrir sólo en raras ocasiones, pero es útil saber cómo manejarlo.</p>
<p class="p" id="to_further_conf">To further confuse matters, the callback function is executed <span class="emphasis"><em>whether or not the datafile was loaded successfully</em></span>. That’s right, if the network connection fails, or the filename is misspelled, or for some reason an error occurs on the web server end, the callback function will <span class="emphasis"><em>still</em></span> be executed. When the data fails to load, and you call functions that rely on that data being present, you will probably see an error in the console, and the visualization won’t be created. This scenario might happen only rarely, but it’s useful to know how to handle it.</p> 

<p class="it">Afortunadamente, se puede incluir un parámetro de error opcional en la definición de la función de callback. Si hay un error al cargar el archivo, a continuación, el error se establece en el mensaje de error devuelto por el servidor web, y será de datos indefinido. Si se carga el archivo con éxito y no hay error, el error será nulo, y la array de datos se rellenará como se esperaba. Tenga en cuenta que el error debe ser el primer parámetro y data el segundo parámetro:</p>

<p class="p" id="fortunately_yo_id2">Fortunately, you can include an optional <code class="literal">error</code> parameter in the callback function definition. If there is a problem loading the file, then <code class="literal">error</code> will be set to the error message returned by the web server, and <code class="literal">data</code> will be <code class="literal">undefined</code>. If the file loads successfully and there is no error, then <code class="literal">error</code> will be <code class="literal">null</code>, and the <code class="literal">data</code> array will be populated as expected. Note that <code class="literal">error</code> must be the first parameter, and <code class="literal">data</code> the second:</p>

<pre class="programlisting" data-language="javascript" id="var_dataset_d">var dataset;

d3.csv("food.csv", function(error, data) {

        if (error) {  //If error is not null, something went wrong.
          console.log(error);  //Log the error.
        } else {      //If no error, the file loaded correctly. Yay!
          console.log(data);   //Log the data.

      //Include other code to execute after successful file load here
      dataset = data;
      generateVis();
      hideLoadingMsg();
        }

});</pre> 

</div>

 <p class="it">La verificación de los datos es un gran uso de la función de callback <code class="literal">csv()</code>, pero por lo general este es el lugar donde quiere llamar a otras funciones que construyen la visualización, ahora que los datos están disponibles, como en:</p>
<p class="p" id="verifying_your_">Verifying your data is a great use of the <code class="literal">csv()</code> callback function, but typically this is where you’d call other functions that construct the visualization, now that the data is available, as in:</p>
 
<pre class="programlisting" data-language="javascript" id="var_dataset__id2">var dataset;  //Declare global var

d3.csv("food.csv", function(data) {

    //Hand CSV data off to global var,
    //so it's accessible later.
    dataset = data;

    //Call some other functions that
    //generate your visualization, e.g.:
    generateVisualization();
    makeAwesomeCharts();
    makeEvenAwesomerCharts();
    thankAwardsCommittee();

});</pre> 

<p class="it">Un consejo más: si tiene datos  separados por tabulación en un archivo TSV, pruebe el método d3.tsv(), que de otro modo se comporta exactamente como el método anterior.</p>

<p class="p" id="one_more_tip_i">One more tip: if you have <span class="emphasis"><em>tab</em></span>-separated data in a TSV file, try the <code class="literal">d3.tsv()</code> method, which otherwise behaves exactly as the preceding method.<a id="id504146" class="indexterm" href=""></a></p>

<div class="sect3" id="_loading_json_data">
 <div class="titlepage">
<div><h4 class="title">Loading JSON data</h4>
</div>
</div>
</div> 


<p class="it">Vamos a pasar más tiempo hablando de JSON más adelante, pero por ahora, todo lo que necesita saber es que el método <code class="literal">d3.json()</code> funciona de la misma manera que <code class="literal">csv()</code>. Cargue sus datos JSON de esta manera:</p>

<p class="p" id="well_spend_mor">We’ll spend more time talking about JSON later, but for now, all you need<a id="id504167" class="indexterm" href=""></a> to know is that the <code class="literal">d3.json()</code> method works the same way as <code class="literal">csv()</code>. Load your JSON data in this way:</p>

<pre class="programlisting" data-language="javascript" id="djsonwaterf">d3.json("waterfallVelocities.json", function(json) {
    console.log(json);  //Log output to console
});</pre> 

 


<p class="it">Aquí, he llamado la salida <code class="literal">json</code>, pero se podría llamar <code class="literal">data</code> o lo que quiera.</p>
 <p class="p" id="here_ive_name">Here, I’ve named the parsed output <code class="literal">json</code>, but it could be called <code class="literal">data</code> or whatever you like.</p>


  <div class="sect2" id="please_make_your_selection_5"> <div class="titlepage"><div><h3 class="title">Please Make Your Selection</h3></div></div></div> 


<p class="it">Los datos están listos para partir. A modo de recordatorio, estamos trabajando con este sencillo array:</p>
 <p class="p" id="the_data_is_rea_id1">The data is ready to go. As a reminder, we are working with this simple array:</p> 

 
<pre class="programlisting" data-language="javascript" id="var_dataset___id2">var dataset = [ 5, 10, 15, 20, 25 ];</pre> 

<p class="it">Ahora tiene que decidir qué seleccionar. Es decir, qué elementos serán asociados con sus datos? Una vez más, vamos a mantenerlo super simple y decir que queremos hacer un nuevo párrafo para cada valor del conjunto de datos. Así que si se podría imaginar algo como esto sería de gran ayuda:</p>

<p class="p" id="now_you_need_to">Now you need to decide what to select. That is, what elements will your data be associated with? Again, let’s keep it super simple and say that we want to make a new paragraph for each value in the dataset. So you might imagine something like this would be helpful:</p> 


<pre class="programlisting" data-language="javascript" id="dselectbody_id4">d3.select("body").selectAll("p")</pre> 


<p class="it">y estaríamos en lo cierto, pero hay una trampa: los párrafos que desea seleccionar no existen todavía. Y este es uno de los puntos más comunes de confusión con D3: ¿cómo podemos seleccionar los elementos que todavía no existen? Tengan paciencia conmigo, ya que la respuesta tiene que doblar un poco la mente.</p>

<p class="p" id="and_youd_be_ri">and you’d be right, but there’s a catch: the paragraphs we want to select <span class="emphasis"><em>don’t exist yet</em></span>. And this gets at one of the most common points of confusion with D3: how can we select elements that don’t yet exist? Bear with me, as the answer might require bending your mind a bit.</p>

<p class="it">La respuesta se encuentra en <code class="literal">enter()</code>, un método verdaderamente mágico. Vea este código, que voy a explicar:</p>

<p class="p" id="the_answer_lies">The answer lies with <code class="literal">enter()</code>, a truly magical method. See this code,<a id="id504481" class="indexterm" href=""></a><a id="id504487" class="indexterm" href=""></a> which I’ll explain:</p>


<pre class="programlisting" data-language="javascript" id="dselectbody_id5">d3.select("body").selectAll("p")
    .data(dataset)
    .enter()
    .append("p")
    .text("New paragraph!");</pre> 

<p class="it">Abra el archivo con el código de ejemplo 04_creating_paragraphs.html y debería ver cinco nuevos párrafos, cada uno con el mismo contenido, como se muestra en la Figura 5-5.</p>

<p class="p" id="view_the_exampl">View the example code <span class="emphasis"><em>04_creating_paragraphs.html</em></span> and you should see five new paragraphs, each with the same content, as shown in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch05.html#Dynamic_paragraphs" title="Figure 5-5. Dynamic paragraphs">Figure 5-5</a>.</p>

    <div class="figure" id="Dynamic_paragraphs"> <div class="figure-contents"><div class="mediaobject"><img src="/static/r8_mae2uVb-img5.png" alt="Dynamic paragraphs"/></div></div>

    <p class="fig">Figure 5-5. Dynamic paragraphs</p>

    <p class="fig">Figura 5-5. Párrafos dinámicos</p></div> 

 <p class="it">Esto es lo que está pasando:</p>
 <p class="p" id="heres_whats_h">Here’s what’s happening:</p>

    <div class="variablelist" id="dselectbody_id6">

    <dl class="variablelist"> 

   <dd class="it"> Busca el <code class="literal">body</code> en el DOM y saca una referencia a la siguiente etapa de la cadena. </dd>
    <dt class="programlisting"><span class="term"> <code class="literal">d3.select("body")</code> </span></dt> <dd class="p"> Finds the <code class="literal">body</code> in the DOM and hands off a reference to the next step in the chain. </dd>

  <dd class="it"> Selecciona todos los párrafos del DOM. Debido a que no existen actualmente, esto devuelve una selección vacía. Piense en esta selección vacía como la representación de los párrafos que <span class="emphasis"><em>pronto va a existir</em></span>. </dd>

  <dd class="p"> Selects all paragraphs in the DOM. Because none exist yet, this returns an empty selection. Think of this empty selection as representing the paragraphs that <span class="emphasis"><em>will soon exist</em></span>. </dd>

    <dt class="programlisting"><span class="term"> <code class="literal">.selectAll("p")</code> </span></dt>

   <dd class="it"> Cuenta y analiza los valores de los datos. Hay cinco valores en nuestra array llamada <code class="literal">dataset</code>, por lo que este punto se ejecutará cinco veces, una para cada valor.</dd>
<dd class="p"> Counts and parses our data values. There are five values in our array called <code class="literal">dataset</code>, so everything past this point is executed five times, once for each value. </dd>

    <dt class="programlisting"><span class="term"> <code class="literal">.data(dataset)</code> </span></dt>

  <dd class="it"> Para crear nuevos elementos, enlazados a datos, deberá usar <code class="literal">enter()</code>. Este método busca en la selección actual del DOM, y luego los datos que se entregó a ella. Si hay más valores de datos que corresponden a elementos del DOM, a continuación, <code class="literal">enter()</code> crea un nuevo elemento de marcador de posición en el que puede trabajar su magia. A continuación, saca una referencia a este nuevo marcador de posición para el siguiente paso en la cadena. </dd> 
    <dt class="programlisting"><span class="term"> <code class="literal">.enter()</code> </span></dt> <dd class="p"> To create new, data-bound elements, you must use <code class="literal">enter()</code>. This method looks at the current DOM selection, and then at the data being handed to it. If there are more data values than corresponding DOM elements, then <code class="literal">enter()</code> <span class="emphasis"><em>creates a new placeholder element</em></span> on which you can work your magic. It then hands off a reference to this new placeholder to the next step in the chain. </dd> 

  <dd class="it"> Toma la selección del marcador de posición vacío creado por <code class="literal">enter()</code>  y anexa elementos <code class="literal">p</code> en el DOM. Hooray! A continuación, entrega una referencia al elemento que acaba de crear para el siguiente paso en la cadena. </dd> 
  <dd class="p"> Takes the empty placeholder selection created by <code class="literal">enter()</code> and appends a <code class="literal">p</code> element into the DOM. Hooray! Then it hands off a reference to the element it just created to the next step in the chain. </dd>
    <dt class="programlisting"><span class="term"> <code class="literal">.append("p")</code> </span></dt> 

     

<dd class="it">Toma la referencia a las nuevas <code class="literal">p</code> creadas e inserta un valor de texto.  </dd>
    <dt class="programlisting"><span class="term"> <code class="literal">.text("New paragraph!")</code> </span></dt> <dd class="p"> Takes the reference to the newly created <code class="literal">p</code> and inserts a text value. </dd>

    </dl></div> <div class="sect2" id="_bound_and_determined"> <div class="titlepage"><div><h3 class="title">Bound and Determined</h3></div></div> 

<p class="it">¡Todo bien! Nuestros datos se han leído, analizado, y se destinaron a los nuevos elementos <code class="literal">p</code> que hemos creado en el DOM. No me cree? Eche otro vistazo a 04_creating_paragraphs.html y abra su inspector de la web, como se muestra en la Figura 5-6.</p>

    <p class="p" id="all_right_our_">All right! Our data has been read, parsed, and bound to new <code class="literal">p</code> elements that we created in the DOM. Don’t believe me? Take another look at <span class="emphasis"><em>04_creating_paragraphs.html</em></span> and whip out your web inspector, shown in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch05.html#new_p_elements_in_the_inspector" title="Figure 5-6. New p elements in the web inspector">Figure 5-6</a>.</p>

 <div class="figure" id="new_p_elements_in_the_inspector"> <div class="figure-contents"><div class="mediaobject"><img src="/static/r8_mae2uVb-img6.png" alt="New p elements in the web inspector"/></div></div>



 <p class="fig">Figure 5-6. New <code class="literal">p</code> elements in the web inspector</p>
</div> 


<p class="it">Bien, veo cinco párrafos, pero donde están los datos? Cámbie a la consola de JavaScript, escriba el código siguiente y haga clic en Enter. Los resultados se muestran en la Figura 5-7:</p>
<p class="p" id="okay_i_see_fiv">Okay, I see five paragraphs, but where’s the data? Switch to the JavaScript console, type in the following code, and click Enter. The results are shown in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch05.html#logging_to_from_console" title="Figure 5-7. Logging to the console, from the console">Figure 5-7</a>:</p> 

<pre class="programlisting" data-language="javascript" id="consolelogd">console.log(d3.selectAll("p"))</pre> <div class="figure" id="logging_to_from_console"> <div class="figure-contents"><div class="mediaobject"><img src="/static/r8_mae2uVb-img7.png" alt="Logging to the console, from the console"/></div></div>



<p class="fig">Figure 5-7. Logging to the console, from the console</p> 

</div> 


<p class="it">¡Una array! O, en realidad, una array que contiene otra array. Haga clic en el triángulo gris para revelar su contenido, que se muestra en la Figura 5-8.</p>
<p class="p" id="an_array_or_r">An array! Or, really, an array containing another array. Click the gray disclosure triangle to reveal its contents, shown in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch05.html#array_of_arrays" title="Figure 5-8. Array of arrays, expanded">Figure 5-8</a>.</p> 

<div class="figure" id="array_of_arrays"> <div class="figure-contents"><div class="mediaobject"><img src="/static/r8_mae2uVb-img8.png" alt="Array of arrays, expanded"/></div></div>



<p class="fig">Figure 5-8. Array of arrays, expanded</p>

</div> 


<p class="it">Se dará cuenta de las cinco <code class="literal">p</code>s, numeradas del 0 al 4. Haga clic en el triángulo situado junto al primero (número cero), lo que resulta en la vista que se muestra en la Figura 5-9.</p>
<p class="p" id="youll_notice_t_id1">You’ll notice the five <code class="literal">p</code>s, numbered 0 through 4. Click the disclosure triangle next to the first one (number zero), which results in the view shown in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch05.html#the_p_element_expanded" title="Figure 5-9. The p element, expanded">Figure 5-9</a>.</p> 

<div class="figure" id="the_p_element_expanded"> <div class="figure-contents"><div class="mediaobject"><img src="/static/r8_mae2uVb-img9.png" alt="The p element, expanded"/></div></div>

<p class="fig">Figura 5-9. El elemento <code class="literal">p</code>, ampliado</p>
<p class="fig">Figure 5-9. The p element, expanded</p> 

</div> 

<p class="it">¿Míralo? ¿Lo ves? Apenas puedo contenerme. Hay esta. (Figura 5-10).</p>
<p class="p" id="see_it_do_you_">See it? Do you see it? I can barely contain myself. There it is (<a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch05.html#finally_bound_data" title="Figure 5-10. Finally, bound data">Figure 5-10</a>).</p> 

<div class="figure" id="finally_bound_data"> <div class="figure-contents"><div class="mediaobject"><img src="/static/r8_mae2uVb-img10.png" alt="Finally, bound data"/></div></div>


<p class="fig">Figura 5-10. Finalmente, la data</p>
<p class="fig">Figure 5-10. Finally, bound data</p> 

</div> 

<p class="it">Nuestro primer valor de datos, el número 5, aparece en el marco del primer atributo de parrafo <code class="literal">__data__</code>. Pulse sobre los otros elementos de párrafo, y verá que también contienen valores <code class="literal">__data__</code>: 10, 15, 20, y 25, del mismo modo que hemos especificado.</p>
<p class="p" id="our_first_data_">Our first data value, the number <code class="literal">5</code>, is showing up under the first paragraph’s <span class="keep-together"><code class="literal">__data__</code></span> attribute. Click into the other paragraph elements, and you’ll see they also contain <code class="literal">__data__</code> values: 10, 15, 20, and 25, just as we specified.</p> 

<p class="it">Usted ve, cuando D3 une data a un elemento, que la data no existe en el DOM, pero existe en la memoria como un atributo <code class="literal">__data__</code> de ese elemento. Y la consola es donde se puede ir a confirmar si la data se ha unido como se esperaba.</p>
<p class="p" id="you_see_when_d">You see, when D3 binds data to an element, that data doesn’t exist in the DOM, but it does exist in memory as a <code class="literal">__data__</code> attribute of that element. And the console is where you can go to confirm whether or not your data was bound as expected.</p> 

<p class="it">Los datos están listos. Vamos a hacer algo con ellos.</p>
<p class="p" id="the_data_is_rea_id2">The data is ready. Let’s do something with it.<a id="id505112" class="indexterm" href=""></a><a id="id505121" class="indexterm" href=""></a></p>

</div> <div class="sect2" id="_using_your_data"> <div class="titlepage"><div><h3 class="title">Using Your Data</h3><h3>El Uso de Sus Datos</h3></div></div>
 
<p class="it">Podemos ver que los datos se han cargado en la página y estan destinados a nuestros elementos de reciente creación en el DOM, pero podemos usarlos? Aquí está nuestro código hasta ahora:</p>
 <p class="p" id="we_can_see_that">We can see that the data has been loaded into the page and is bound to<a id="ix_bound" class="indexterm" href=""></a> our newly created elements in the DOM, but can we <span class="emphasis"><em>use</em></span> it? Here’s our code so far:</p> 

 <pre class="programlisting" data-language="javascript" id="var_dataset___id3">var dataset = [ 5, 10, 15, 20, 25 ];

d3.select("body").selectAll("p")
    .data(dataset)
    .enter()
    .append("p")
    .text("New paragraph!");</pre> 

<p class="it">Vamos a cambiar la última línea:</p>
    <p class="p" id="lets_change_th">Let’s change the last line to:</p> 
  
<pre class="programlisting" data-language="javascript" id="textfunction_id1">    .text(function(d) { return d; });</pre> 

<p class="it">Ahora pruebe el nuevo código en <span class="emphasis"><em>05_creating_paragraphs_text.html</em></span>. Debería ver el resultado que se muestra en la Figura 5-11.</p>
<p class="p" id="now_test_out_th">Now test out that new code in <span class="emphasis"><em>05_creating_paragraphs_text.html</em></span>. You should see the result shown in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch05.html#more_dynamic_paragraphs" title="Figure 5-11. More dynamic paragraphs">Figure 5-11</a>.</p> 

<div class="figure" id="more_dynamic_paragraphs"> <div class="figure-contents"><div class="mediaobject"><em class="dotEPUBProtected"> <img alt="Imagen" src="/static/Fig511.png" /> </em></div></div>

<p class="fig">Figura 5-11. Párrafos más dinámicos</p>

<p class="fig">Figure 5-11. More dynamic paragraphs</p> 

</div> 

<p class="it">Whoa! Utilizamos nuestros datos para rellenar el contenido de cada párrafo, todo gracias a la magia del metodo <code class="literal">data()</code> . Usted ve, cuando encadena métodos, en cualquier momento después de llamar al metodo <code class="literal">data()</code>, puede crear una función anonima que acepte como entrada <code class="literal">d</code>. El método magico  <code class="literal">data()</code> asegura que <code class="literal">d</code> se establece al valor correspondiente en el conjunto de datos original, dado el elemento actual que nos ocupa.</p>

<p class="p" id="whoa_we_used_o">Whoa! We used our data to populate the contents of each paragraph, all thanks to the magic of the <code class="literal">data()</code> method. You see, when chaining methods together, anytime after you call <code class="literal">data()</code>, you can create an anonymous function that accepts <code class="literal">d</code> as input. The magical <code class="literal">data()</code> method ensures that <code class="literal">d</code> is set to the corresponding value in your original dataset, given the current element at hand.<a id="id443742" class="indexterm" href=""></a></p> 



<p class="it">El valor "del elemento actual" cambia  con el tiempo porque D3 loopea a través de cada elemento. Por ejemplo, cuando un loop sucede por tercera vez, nuestro código crea la tercera etiqueta <code class="literal">p</code>, y el valor de <code class="literal">d</code> se corresponderá con el tercer valor en nuestra base de datos (o <code class="literal">dataset[2]</code>). Así que en el tercer párrafo se pone el contenido del texto "15".</p>
<p class="p" id="the_value_of_t">The value of “the current element” changes over time as D3 loops through each element. For example, when looping through the third time, our code creates the third <code class="literal">p</code> tag, and <code class="literal">d</code> will correspond to the third value in our dataset (or <code class="literal">dataset[2]</code>). So the third paragraph gets text content of “15”.</p> 

</div> <div class="sect2" id="_high_functioning"> <div class="titlepage"><div><h3 class="title">High-Functioning</h3> <h3>De alto funcionamiento</h3></div></div> 


<p class="it">En caso de que usted sea nuevo en la escritura de sus propias funciones (también conocidas como métodos), la estructura básica de una definición de función es:</p>
<p class="p" id="in_case_youre__id1">In case you’re new to writing your own functions (a.k.a. methods), the<a id="id506309" class="indexterm" href=""></a><a id="id506317" class="indexterm" href=""></a><a id="id506323" class="indexterm" href=""></a><a id="id506329" class="indexterm" href=""></a><a id="id506337" class="indexterm" href=""></a> basic structure of a function definition is:</p> 







 
<pre class="programlisting" data-language="javascript" id="functioninput_">function(input_value) {
    //Calculate something here
    return output_value;
    
}</pre> 


<p class="it">La función la utilizé anteriormente, es muy simple, nada de lujos:</p>
<p class="p" id="the_function_we">The function we used earlier is dead simple, nothing fancy:</p> 

<pre class="programlisting" data-language="javascript" id="functiond__r_id1">function(d) {
    return d;
}</pre> 

<p class="it">Esto se llama una función anónima, ya que no tiene un nombre. Esto contrasta con una función que se almacena en una variable, que es una función que se llama:</p>
<p class="p" id="this_is_called_">This is called an <span class="emphasis"><em>anonymous function</em></span>, because it doesn’t have a name. Contrast that with a function that’s stored in a variable, which is a <span class="emphasis"><em>named function</em></span>:</p>

<pre class="programlisting" data-language="javascript" id="var_dosomething">var doSomething = function() {
    //Code to do something here
};</pre> 

<p class="it">Nosotros escribiremos muchas funciones anónimas utilizando D3. Ellas son la clave para acceder a los valores de datos individuales y el cálculo de las propiedades dinámicas.</p>
<p class="p" id="well_write_lot">We’ll write lots of anonymous functions when using D3. They are the key to accessing individual data values and calculating dynamic properties.</p>

<p class="it">Esta función anónima particular, se envuelve dentro de la función D3 <code class="literal">text()</code>. Así que nuestra función anónima se ejecuta primero. Entonces el resultado se entrega al <code class="literal">text()</code>. A continuación, <code class="literal">text()</code>, finalmente hace su magia (insertando su argumento de entrada como texto dentro del elemento seleccionado del DOM):</p>

<p class="p" id="this_particular_id1">This particular anonymous function is wrapped within D3’s <code class="literal">text()</code> function. So our anonymous function is executed first. Then its result is handed off to <code class="literal">text()</code>. Then <code class="literal">text()</code> finally works its magic (by inserting its input argument as text within the selected DOM element):</p>

<pre class="programlisting" data-language="javascript" id="textfunction_id2">.text(function(d) {
    return d;
});</pre> 


<p class="it">Pero podemos (y lo haremos) conseguirlo de manera mucho más elegante porque se pueden personalizar estas funciones como quiera. Sí, esto es a la vez el placer y el dolor de escribir su propio código JavaScript. Tal vez le gustaría añadir un poco de texto adicional, como en:</p>
<p class="p" id="but_we_can_and">But we can (and will) get much fancier because you can customize these functions any way you like. Yes, this is both the pleasure and pain of writing your own JavaScript. Maybe you’d like to add some extra text, as in:</p>

<pre class="programlisting" data-language="javascript" id="textfunction_id3">.text(function(d) {
    return "I can count up to " + d;
});</pre> 

<p class="it">que produce el resultado que se muestra en la figura 5-12, como se ve en 06_creating_paragraphs_counting.html ejemplo de archivo.</p>
<p class="p" id="which_produces_">which produces the result shown in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch05.html#Still_more_dynamic_paragraphs" title="Figure 5-12. Still more dynamic paragraphs">Figure 5-12</a>, as seen in example file <span class="emphasis"><em>06_creating_paragraphs_counting.html</em></span>.</p>

<div class="figure" id="Still_more_dynamic_paragraphs"> <div class="figure-contents"><div class="mediaobject"><em class="dotEPUBProtected"> <img alt="Imagen" src="/static/Fig512.png" /> </em></div></div>


<p class="fig">Figura 5-12. Párrafos Todavía más dinámicos</p>
<p class="fig">Figure 5-12. Still more dynamic paragraphs</p>
 </div> </div> 

<div class="sect2" id="_data_wants_to_be_held"> <div class="titlepage"><div><h3 class="title">Data Wants to Be Held</h3> <h3>Datos quiere ser Held</h3></div></div> 


<p class="it">Tal vez se pregunte por qué tiene que escribir la función <code class="literal">function(d) { … }</code> en lugar de <code class="literal">d</code>. Por ejemplo, esto no funcionará:</p>
<p class="p" id="you_might_be_wo">You might be wondering why you have to write out <code class="literal">function(d) { … }</code> instead of just <code class="literal">d</code> on its own. For example, this won’t work:</p>

 <pre class="programlisting" data-language="javascript" id="texti_can_co">.text("I can count up to " + d);</pre>
  

  <p class="it">En este contexto, sin envolver <code class="literal">d</code>  en una función anónima, <code class="literal">d</code>  no tiene ningún valor. Pensar a <code class="literal">d</code> como un valor de marcador de posición un poco solitaria que sólo necesita un ambiente cálido, conteniendola en una especie de abrazo, al cuidado de los paréntesis de la función. (Extiendo esta metáfora un poco más, sí, es raro que el abrazo sea dado por una función anónima, porque sólo confunde las cosas.)</p>

  <p class="p" id="in_this_context">In this context, without wrapping <code class="literal">d</code> in an anonymous function, <code class="literal">d</code> has<a id="id506854" class="indexterm" href=""></a><a id="id506863" class="indexterm" href=""></a> no value. Think of <code class="literal">d</code> as a lonely little placeholder value that just needs a warm, containing hug from a kind, caring function’s parentheses. (Extending this metaphor further, yes, it is creepy that the hug is being given by an <span class="emphasis"><em>anonymous</em></span> function, but that only confuses matters.)</p>

<p class="it">Aquí esta <code class="literal">d</code> que es sostenido suave y apropiadamente por una función:</p>
 <p class="p" id="here_is_d_being">Here is <code class="literal">d</code> being held gently and appropriately by a function:</p> 

<pre class="programlisting" data-language="javascript" id="textfunction_id4">.text(function(d) {  // &lt;-- Note tender embrace at left //Note el abrazo suave a la izquierda
    return "I can count up to " + d;
});</pre> 

<p class="it">La razón de esto es que la sintaxis <code class="literal">.text()</code>, <code class="literal">attr()</code>, y muchos otros métodos D3 pueden tener una función como un argumento. Por ejemplo, el <code class="literal">.text()</code> puede tomar ya sea simplemente una cadena estática de texto como un argumento:</p>

<p class="p" id="the_reason_for_">The reason for this syntax is that <code class="literal">.text()</code>, <code class="literal">attr()</code>, and many other D3 methods can take a <span class="emphasis"><em>function</em></span> as an argument. For example, <code class="literal">text()</code> can<a id="id507002" class="indexterm" href=""></a><a id="id507008" class="indexterm" href=""></a> take either simply a static string of text as an argument:</p>

<pre class="programlisting" data-language="javascript" id="textsomestri">.text("someString")</pre> 


<p class="it">o el resultado de una función:</p>
<p class="p" id="or_the_result_o"><span class="emphasis"><em>or</em></span> the result of a function:</p>

<pre class="programlisting" data-language="javascript" id="textsomefunct">.text(someFunction())  // Presumably, someFunction() would return a string //Presumiblemente, someFunction() podría devolver una cadena </pre> 

<p class="it">  o una función anónima puede ser el argumento, por ejemplo, cuando se escribe:</p>
<p class="p" id="or_an_anonymous"><span class="emphasis"><em>or</em></span> an anonymous function itself can be the argument, such as when you write:</p>

<pre class="programlisting" data-language="javascript" id="textfunction_id5">.text(function(d) {
    return d;
})</pre>

<p class="it">En este caso, se está definiendo una función anónima. Si D3 ve una función allí, llamará a esa función, mientras la entrega fuera del origen actual <code class="literal">d</code> como argumento de la función. Aquí, he llamado al argumento <code class="literal">d</code> simplemente por convención. Se podría definir como dato o información o lo que quiera. Todo D3 busca cualquier nombre de argumento, en el que se puede pasar el dato actual. A lo largo de este libro, usaremos <code class="literal">d</code> porque es concisa y familiar, usada en muchos de los otros ejemplos D3 que se encuentran en línea.</p>
<p class="p" id="here_you_are_d">Here, you are defining an anonymous function. If D3 sees a function there, it will <span class="emphasis"><em>call</em></span> that function, while handing off the current datum <code class="literal">d</code> as the function’s argument. Here, I’ve named the argument <code class="literal">d</code> just by convention. You could call it <code class="literal">datum</code> or <code class="literal">info</code> or whatever you like. All D3 is looking for is <span class="emphasis"><em>any</em></span> argument name, into which it can pass the current datum. Throughout this book, we’ll use <code class="literal">d</code> because it is concise and familiar from many of the other D3 examples found online.</p>

<p class="it">En cualquier caso, sin esa función en su lugar, D3 no podría relacionar el valor de datos actual. Sin una función anónima y su argumento allí para recibir el valor de <code class="literal">d</code>, D3 podría confundirse e incluso comenzar a llorar. (Es esperable que D3 es más emocional que usted.)</p>
<p class="p" id="in_any_case_wi">In any case, without that function in place, D3 couldn’t relay the current data value. Without an anonymous function and its argument there to receive the value of <code class="literal">d</code>, D3 could get confused and even start crying. (D3 is more emotional than you’d expect.)</p>

<p class="it">Al principio, esto puede parecer un poco tonto como un montón de trabajo extra para obtener sólo <code class="literal">d</code>, pero el valor de este enfoque se pondrá de manifiesto a medida que trabajemos en piezas más complejas.</p></div> 

<div class="sect2" id="_beyond_text"> <div class="titlepage"><div>
<p class="p" id="at_first_this_">At first, this might seem silly and like a lot of extra work to just get at <code class="literal">d</code>, but the value of this approach will become clear as we work on more complex pieces.</p

<h3 class="title">Beyond Text</h3><h3>Más Allá del Texto</h3></div></div>

<p class="it">Las cosas se ponen mucho más interesante cuando exploramos otros métodos de D3, como <code class="literal">attr()</code> y <code class="literal">style()</code>, lo que nos permite establecer los atributos HTML y propiedades CSS en las selecciones, respectivamente.</p>
<p class="p" id="things_get_a_lo">Things get a lot more interesting when we explore D3’s other methods,<a id="id507246" class="indexterm" href=""></a> like <code class="literal">attr()</code> and <code class="literal">style()</code>, which allow us to set HTML attributes and<a id="id507267" class="indexterm" href=""></a> CSS properties on selections, <span class="keep-together">respectively</span>.<a id="id507282" class="indexterm" href=""></a><a id="id507288" class="indexterm" href=""></a></p>

<p class="it">Por ejemplo, añadir una línea más a nuestro código:</p>
<p class="p" id="for_example_ad">For example, adding one more line to our code:</p> 

<pre class="programlisting" data-language="javascript" id="stylecolor_id1">.style("color", "red");</pre> 

<p class="it">produce el resultado que se muestra en la figura 5-13, como se ve en <span class="emphasis"><em>07_creating_paragraphs_with_style.html</em></span>.</p>
<p class="p" id="produces_the_re">produces the result shown in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch05.html#Red_paragraphs" title="Figure 5-13. Red paragraphs">Figure 5-13</a>, as seen in <span class="emphasis"><em>07_creating_paragraphs_with_style.html</em></span>.</p>

<div class="figure" id="Red_paragraphs"> <div class="figure-contents"><div class="mediaobject"><em class="dotEPUBProtected"> <img alt="Imagen" src="/static/Fig513.png" /> </em></div></div>



<p class="fig">Figure 5-13. Red paragraphs</p> 
</div> 


<p class="it">Todo el texto es ahora de color rojo; Vaya cosa. Pero podríamos utilizar una función personalizada para hacer al texto de color rojo sólo si el punto de referencia actual supera un determinado umbral. Así se revisa la última línea para utilizar una función en lugar de una cadena:</p>
<p class="p" id="all_the_text_is">All the text is now red; big deal. But we could use a custom function to make the text red only if the current datum exceeds a certain threshold. So we revise that last line to use a function instead of a string:</p> 

<pre class="programlisting" data-language="javascript" id="stylecolor_id2">.style("color", function(d) {
    if (d &gt; 15) {   //Threshold of 15
        return "red";
    } else {
        return "black";
    }
});</pre> 


<p class="it">Ver el cambio resultante, que se muestra en la figura 5-14, en 08_creating_paragraphs_with_style_functions.html.</p>
<p class="p" id="see_the_resulti">See the resulting change, displayed in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch05.html#Dynamically_styled_paragraphs" title="Figure 5-14. Dynamically styled paragraphs">Figure 5-14</a>, in <span class="emphasis"><em>08_creating_paragraphs_with_style_functions.html</em></span>.</p> 

<div class="figure" id="Dynamically_styled_paragraphs"> <div class="figure-contents"><div class="mediaobject"><em class="dotEPUBProtected"> <img alt="Imagen" src="/static/Fig514.png" /> </em></div></div>

<p class="fig">Figura 5-14. Párrafos dinamicamente diseñados</p>
<p class="fig">Figure 5-14. Dynamically styled paragraphs</p> 

</div> 
<p class="it">Observe cómo las tres primeras líneas son de color negro, pero una vez que <code class="literal">d</code> supera el umbral arbitrario de 15, el texto se muestra en rojo.</p>
<p class="p" id="notice_how_the__id2">Notice how the first three lines are black, but once <code class="literal">d</code> exceeds the arbitrary threshold of 15, the text turns red.<a id="id507562" class="indexterm" href=""></a></p> 

<p class="it">De acuerdo, hemos conseguido cargar datos en el DOM, y crear elementos de forma dinámica con destino a esos datos. Yo diría que estamos listos para empezar a dibujar con los datos!</p>
<p class="p" id="okay_weve_got">Okay, we’ve got data loaded in, and dynamically created DOM elements bound to that data. I’d say we’re ready to start drawing with data!<a id="id507573" class="indexterm" href=""></a><a id="id507580" class="indexterm" href=""></a></p>

</div> </div>
</div>
</div>

       </div>

  </div>
    </div>
  </div>
  </main-layout>
</template>


<script>
  import MainLayout from '../layouts/Main.vue'

  export default {
  name: 'ch5',
    components: {
      MainLayout
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


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