<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    
    <div class="block">

      <div>

        <h1 class="title">Chapter 8. Axes</h1>

      </div>

<p class="it">Después de haber dominado el uso de las escalas D3, ahora tenemos el diagrama de dispersión que se muestra en la Figura 8-1.</p>
    <p class="p" id="having_mastered">Having mastered the use of D3 scales, we now have the scatterplot shown in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch08.html#Large_scaled_scatterplot2" title="Figure 8-1. Large, scaled scatterplot">Figure 8-1</a>.</p>


    <div>

          <img src="/static/Y8KhUkEF36-img1.png" alt="Large, scaled scatterplot"/>

<p class="fig">Figura 8-1. Gran, diagrama de dispersión escalado</p>
      <p class="fig">Figure 8-1. Large, scaled scatterplot</p>


    </div>
<p class="it">Vamos a añadir los ejes horizontal y vertical, por lo que podemos acabar con números rojos horribles que saturaran nuestra tabla.</p>
    <p class="p" id="lets_add_horiz">Let’s add horizontal and vertical axes, so we can do away with the horrible red numbers cluttering up our chart.<a id="ix_axes" class="indexterm" href=""></a><a id="id526376" class="indexterm" href=""></a></p>



        <div>

          <h2 class="title">Introducing Axes</h2>


      </div>
<p class="it">Al igual que sus escalas, los ejes de D3 son en realidad funciones cuyos parámetros definimos. A diferencia de las escalas, cuando una función del eje se llama, no devuelve un valor, sino que genera los elementos visuales del eje, incluyendo líneas, etiquetas y ticks.</p>
      <p class="p" id="much_like_its_s">Much like its scales, <a class="ulink" href="https://github.com/mbostock/d3/wiki/SVG-Axes" target="_top">D3’s <span class="emphasis"><em>axes</em></span></a> are actually <span class="emphasis"><em>functions</em></span> whose parameters you define. Unlike scales, when an axis function is called, it doesn’t return a value, but generates the visual elements of the axis, including lines, labels, and ticks.<a id="id526415" class="indexterm" href=""></a><a id="id526421" class="indexterm" href=""></a></p>

<p class="it">Tenga en cuenta que las funciones de eje son SVG-específica, ya que generan elementos SVG. Además, los ejes están diseñados para su uso con las escalas cuantitativas (en comparación con los ordinales).</p>
      <p class="p" id="note_that_the_a">Note that the axis functions are SVG-specific, as they generate SVG elements. Also, axes are intended for use with quantitative scales (as opposed to ordinal ones).<a id="id526436" class="indexterm" href=""></a><a id="id526441" class="indexterm" href=""></a><a id="id526447" class="indexterm" href=""></a></p>



        <div>
<p class="h2">Configuración de un eje</p>
          <h2 class="title">Setting Up an Axis</h2>


        </div>

<p class="it">Utilice <code class="literal">d3.svg.axis()</code> para crear una función de eje genérico:</p>


<p class="p" id="use_dsvgaxis">Use <code class="literal">d3.svg.axis()</code> to create a generic axis <a id="id526477" class="indexterm" href=""></a>function:</p>


      <pre class="programlisting" data-language="javascript" id="var_xaxis__d_id1">var xAxis = d3.svg.axis();</pre>
<p class="it">Como mínimo, cada eje también necesita que le digan en qué escala debe operar. Aquí vamos a pasar en el <code class="literal">xScale</code> a partir del código de dispersión: </p>

<p class="p" id="at_a_minimum_e">At a minimum, each axis also needs to be told on what <span class="emphasis"><em>scale</em></span> to operate. Here we’ll pass in the <code class="literal">xScale</code> from the scatterplot code:</p>



      <pre class="programlisting" data-language="javascript" id="xaxisscalexsc">xAxis.scale(xScale);</pre>
<p class="it">También podemos especificar donde deben aparecer las etiquetas en relación con el propio eje. El valor predeterminado es inferior, es decir, las etiquetas aparecerán debajo de la línea del eje. (Aunque este es el valor por defecto, no se pierde nada con especificarlo explícitamente.) Las orientaciones posibles para ejes horizontales son parte superior e inferior. Para los ejes verticales, el uso de izquierda a derecha:</p>

<p class="p" id="we_can_also_spe">We can also specify where the labels should appear relative to the axis<a id="id526595" class="indexterm" href=""></a> itself. The default is <code class="literal">bottom</code>, meaning the labels will appear below the axis line. (Although this is the default, it can’t hurt to specify it explicitly.) Possible orientations for horizontal axes are <code class="literal">top</code> and <code class="literal">bottom</code>. For vertical axes, use <code class="literal">left</code> and <code class="literal">right</code>:</p>


      <pre class="programlisting" data-language="javascript" id="xaxisorientb">xAxis.orient("bottom");</pre>


<p class="it">Por supuesto, podemos ser más concisos y encadenar todo esto en una sola línea:</p>
      <p class="p" id="of_course_we_c">Of course, we can be more concise and string all this together into one line:</p>


      <pre class="programlisting" data-language="javascript" id="var_xaxis__d_id2">var xAxis = d3.svg.axis()
                  .scale(xScale)
                  .orient("bottom");</pre>


<p class="it">Por último, para generar realmente el eje e insertar todas esas pequeñas líneas y etiquetas en nuestra SVG, hay que llamar a la función <code class="literal">xAxis</code>. Esto es similar a las funciones de escala, que en primer lugar configurada por los parámetros de ajuste, y luego más tarde llamado, para ponerlos en acción.</p>
      <p class="p" id="finally_to_act">Finally, to actually generate the axis and insert all those little lines and labels into our SVG, we must <span class="emphasis"><em>call</em></span> the <code class="literal">xAxis</code> function. This is similar to the scale functions, which we first configured by setting parameters, and then later <span class="emphasis"><em>called</em></span>, to put them into action.<a id="id526795" class="indexterm" href=""></a></p>


<p class="it">Voy a poner este código al final de nuestro script, por lo que se genera el eje después de los otros elementos en el SVG, y por lo tanto aparece "en la parte superior":</p>
      <p class="p" id="ill_put_this_c">I’ll put this code at the end of our script, so the axis is generated after the other elements in the SVG, and therefore appears “on top”:</p>

      <pre class="programlisting" data-language="javascript" id="svgappendg_id1">svg.append("g")
    .call(xAxis);</pre>
<p class="it">Aquí es donde las cosas se ponen un poco raro. Tal vez se pregunte por qué esto se ve tan diferente de nuestras funciones amigables escala. He aquí por qué: porque una función del eje realidad dibuja algo a la pantalla (añadiendo elementos SVG a la DOM), tenemos que especificar en qué parte del DOM debe colocar esos nuevos elementos. Esto es en contraste a escala funciones como xScale (), por ejemplo, que calculan un valor y devolver esos valores, por lo general para su uso por otra función, sin afectar el DOM en absoluto.</p>

<p class="p" id="this_is_where_t">This is where things get a little funky. You might be wondering why this looks so different from our friendly scale functions. Here’s why: because an <span class="emphasis"><em>axis</em></span> function actually draws something to the screen (by appending SVG elements to the DOM), we need to specify <span class="emphasis"><em>where</em></span> in the DOM it should place those new elements. This is in contrast to scale functions like <code class="literal">xScale()</code>, for example, which calculate a value and return those values, typically for use by yet another function, without impacting the DOM at all.<a id="id526892" class="indexterm" href=""></a></p>


<p class="it">Así que lo que estamos haciendo con el código anterior es que la imagen SVG en el DOM SVG primera referencia,. A continuación, añadimos () un nuevo elemento g al final de la SVG. En SVG tierra, elemento AG es un elemento del grupo. Elementos del grupo son invisibles, a diferencia de la línea, rect, y el círculo, y no tienen ninguna presencia visual a sí mismos. Sin embargo, nos ayudan de dos maneras: en primer lugar, los elementos de G se puede realizar para contener (o "grupo") otros elementos, lo que mantiene a nuestro buen código y ordenado. En segundo lugar, podemos aplicar transformaciones a los elementos g, lo que afecta el dibujo de los elementos visuales dentro de ese grupo (tales como líneas, rects y círculos). Vamos a llegar a transformaciones en tan sólo un minuto.</p>


<p class="p" id="so_what_were_d">So what we’re doing with the preceding code is to first reference <code class="literal">svg</code>, the SVG image in the DOM. Then, we <code class="literal">append()</code> a new <code class="literal">g</code> element to the end of the SVG. In SVG land, a <code class="literal">g</code> element is a <span class="emphasis"><em>group</em></span> element. Group<a id="id526935" class="indexterm" href=""></a><a id="id526943" class="indexterm" href=""></a> elements are invisible, unlike <code class="literal">line</code>, <code class="literal">rect</code>, and <code class="literal">circle</code>, and they have no visual presence themselves. Yet they help us in two ways: first, <code class="literal">g</code> elements can be used to contain (or “group”) other elements, which keeps our code nice and tidy. Second, we can apply <span class="emphasis"><em>transformations</em></span> to <code class="literal">g</code> elements, which affects how visual elements within that group (such as <code class="literal">line</code>s, <code class="literal">rect</code>s, and <code class="literal">circle</code>s) are rendered. We’ll get to transformations in just a minute.</p>

<p class="it">Para ello hemos creado un nuevo g, y, finalmente, la llamada de función () se llama en nuestra nueva g. Entonces, ¿qué es llamada (), y que se lo llama?</p>
      <p class="p" id="so_weve_create">So we’ve created a new <code class="literal">g</code>, and then finally, the function <code class="literal">call()</code> is called on our new <code class="literal">g</code>. So what is <code class="literal">call()</code>, and who is it calling?</p>

<p class="it">La función de llamada D3 () realiza la selección de entrada, tal como se recibió desde el enlace anterior en la cadena, y las manos que la selección fuera de cualquier función. En este caso, la selección es nuestro nuevo elemento g del grupo. Aunque la g no es estrictamente necesario, lo estamos usando porque la función del eje está a punto de generar gran cantidad de líneas locas y números, y es agradable para contener todos los elementos dentro de un objeto de grupo único. llame al () fuera de las manos a la función g ejeX, por lo que nuestro eje se genera dentro de g.</p>
      <p class="p" id="ds_call_fun"><a class="ulink" href="https://github.com/mbostock/d3/wiki/Selections#wiki-call" target="_top">D3’s <code class="literal">call()</code> function</a> takes the incoming <span class="emphasis"><em>selection</em></span>, as received from the prior link in the chain, and hands that selection off to any <span class="emphasis"><em>function</em></span>. In this case, the selection is our new <code class="literal">g</code> group element. Although the <code class="literal">g</code> isn’t strictly necessary, we are using it because the axis function is about to generate lots of crazy lines and numbers, and it’s nice to contain all those elements within a single group object. <code class="literal">call()</code> hands off <code class="literal">g</code> to the <code class="literal">xAxis</code> function, so our axis is generated <span class="emphasis"><em>within</em></span> <code class="literal">g</code>.</p>

<p class="it">Si tuviéramos las personas  desordenadas que amaban código desordenado, podríamos también reescribir el fragmento anterior con esto equivalente exacto:</p>
      <p class="p" id="if_we_were_mess">If we were messy people who loved messy code, we could also rewrite the preceding snippet as this exact equivalent:</p>


      <pre class="programlisting" data-language="javascript" id="svgappendg_id2">svg.append("g")
    .call(d3.svg.axis()
    .scale(xScale)
    .orient("bottom"));</pre>
<p class="it">Ve, se podía meter toda la función del eje dentro de la llamada (), pero por lo general es más fácil en nuestro cerebro para definir funciones en primer lugar, a continuación, llamar más tarde.</p>
      <p class="p" id="see_you_could_">See, you could cram the whole axis function within <code class="literal">call()</code>, but it’s usually easier on our brains to define functions first, then call them later.</p>

<p class="it">En cualquier caso, la Figura 8-2 muestra lo que parece. Consulte el código de ejemplo 01_axes.html.</p>
      <p class="p" id="in_any_case_sh">In any case, <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch08.html#Simple_but_ugly_axis" title="Figure 8-2. Simple, but ugly axis">Figure 8-2</a> shows what that looks like. See code example <span class="emphasis"><em>01_axes.html</em></span>.</p>


      <div>

            <img src="/static/Y8KhUkEF36-img2.png" alt="Simple, but ugly axis"/>


<p class="fig">Figura 8-2. Simple, pero feo el eje</p>
<p class="fig">Figure 8-2. Simple, but ugly axis</p>


   </div>


        <div>

          <h2 class="title">Cleaning It Up</h2>

        </div>

<p class="it">Técnicamente, es un eje, pero no es ni bonito ni útil. Para limpiarlo, primero vamos a asignar una clase de eje para el nuevo elemento g, por lo que podemos apuntar con CSS:</p>
      <p class="p" id="technically_th">Technically, that is an axis, but it’s neither pretty nor useful. To<a id="id527319" class="indexterm" href=""></a><a id="id527327" class="indexterm" href=""></a> clean it up, let’s first assign a class of <code class="literal">axis</code> to the new <code class="literal">g</code> element, so we can target it with CSS:</p>


      <pre class="programlisting" data-language="javascript" id="svgappendg_id3">svg.append("g")
    .attr("class", "axis") //Assign "axis" class
    .call(xAxis);</pre>
<p class="it">A continuación, presentamos nuestros primeros estilos CSS, en el head de nuestra página:</p>
      <p class="p" id="then_we_introd">Then, we introduce our first CSS styles, up in the <code class="literal">&lt;head&gt;</code> of our page:</p>


      <pre class="programlisting" data-language="css" id="axis_path_ax">.axis path,
.axis line {
    fill: none;
    stroke: black;
    shape-rendering: crispEdges;
}

.axis text {
    font-family: sans-serif;
    font-size: 11px;
}</pre>
<p class="it">ver lo útil que es agrupar todos los elementos de eje dentro de un grupo g? Ahora podemos aplicar muy fácilmente estilos a cualquier cosa dentro del grupo utilizando los simples .axis selector CSS. Los ejes mismos se componen de ruta, la línea y elementos de texto, por lo que esos son los tres elementos que nos dirigimos en nuestro CSS. Los caminos y las líneas pueden ser de estilo con las mismas reglas, y el texto para crear sus propias reglas en torno a la fuente y tamaño de fuente.</p>
      <p class="p" id="see_how_useful_">See how useful it is to group all the axis elements within one <code class="literal">g</code> group? Now we can very easily apply styles to anything within the group using the simple CSS selector <code class="literal">.axis</code>. The axes themselves are made up of <code class="literal">path</code>, <code class="literal">line</code>, and <code class="literal">text</code> elements, so those are the three elements that we target in our CSS. The <code class="literal">path</code>s and <code class="literal">line</code>s can be styled with the same rules, and <code class="literal">text</code> gets its own rules around font and font size.</p>

<p class="it">Usted puede notar que cuando usamos las reglas CSS a elementos SVG estilo, SVG nombres de atributo-no-deben propiedades CSS regular de usarse. Esto es confuso, ya que muchas propiedades comparten los mismos nombres, tanto en CSS y SVG, pero algunos no lo hacen. Por ejemplo, en el CSS regular, para establecer el color del texto, se utiliza la propiedad de color, como en:</p>
      <p class="p" id="you_might_notic_id1">You might notice that when we use CSS rules to style SVG elements, only SVG attribute names—not regular CSS properties—should be used. This is confusing, because many properties share the same names in both CSS and SVG, but some do not. For example, in regular CSS, to set the color<a id="id527692" class="indexterm" href=""></a> of some text, you would use the <code class="literal">color</code> property, as in:</p>


      <pre class="programlisting" data-language="css" id="p__color_oliv">p {
    color: olive;
}</pre>
<p class="it">Esto establecerá el color oliva del texto de todos los párrafos <code class="literal">p</code>. Pero trate de aplicar esta propiedad a un elemento SVG, como con:
      <p class="p" id="that_will_set_t">That will set the text color of all <code class="literal">p</code> paragraphs to be <code class="literal">olive</code>. But try to apply this property to an SVG element, as with:</p>


      </p><pre class="programlisting" data-language="css" id="text__color_o">text {
    color: olive;
}</pre>
<p class="it">y no tendrá ningún efecto ya que el color no es una propiedad reconocida por SVG. En su lugar, debe utilizar el equivalente de SVG, fill:</p>
      <p class="p" id="and_it_will_hav">and it will have no effect because <code class="literal">color</code> is not a property recognized by SVG. Instead, you must use SVG’s equivalent, <code class="literal">fill</code>:</p>


      <pre class="programlisting" data-language="css" id="text__fill_ol">text {
    fill: olive;
}</pre>
<p class="it">Si alguna vez se encuentra tratando de elementos SVG estilo, pero por alguna razón el código CSS estúpida no está funcionando, le sugiero que tome una respiración profunda, hacer una pausa, y luego revisar sus nombres de propiedades muy de cerca para asegurarse de que' re el uso de nombres SVG, CSS no queridos. (Puede hacer referencia a la lista completa de atributos SVG en el sitio MDN).</p>
      <p class="p" id="if_you_ever_fin">If you ever find yourself trying to style SVG elements, but for some reason the stupid CSS code just isn’t working, I suggest you take a deep breath, pause, and then review your <span class="emphasis"><em>property names</em></span> very closely to ensure you’re using SVG names, not CSS ones. (You can reference the complete SVG attribute list on <a class="ulink" href="https://developer.mozilla.org/en-US/docs/SVG/Attribute" target="_top">the MDN site</a>.)<a id="id527891" class="indexterm" href=""></a></p>

<p class="it">La propiedad forma de representación es otro atributo SVG raro que usted debe saber. La usamos aquí para asegurarnos de que nuestros ejes y sus líneas de marca de graduación son píxel perfecto. No hay ejes borrosas para nosotros!</p>
      <p class="p" id="the_shaperende"><a class="ulink" href="https://developer.mozilla.org/en/SVG/Attribute/shape-rendering" target="_top">The <code class="literal">shape-rendering</code> property</a> is another weird SVG attribute you should know. We use it here to make sure our axis and its tick mark lines are pixel-perfect. No blurry axes for us!<a id="id527918" class="indexterm" href=""></a><a id="id527924" class="indexterm" href=""></a></p>

<p class="it">El gráfico se ve como en la Figura 8-3 después de nuestro CSS limpieza.</p>

      <p class="p" id="the_chart_looks">The chart looks like <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch08.html#Cleaner_axis" title="Figure 8-3. Cleaner axis">Figure 8-3</a> after our CSS clean-up.</p>



      <div>

            <img src="/static/Y8KhUkEF36-img3.png" alt="Cleaner axis"/>



<p class="fig">Figura 8-3. eje más limpias</p>
<p class="fig">Figure 8-3. Cleaner axis</p>


      </div>
<p class="it">Eso es mejor, pero la línea horizontal superior del eje se corta, y el eje sí mismo debería estar abajo en la base de la tabla de todos modos. Aquí es donde las transformaciones SVG vienen en Al añadir una línea de código, podemos transformar todo el grupo de ejes, empujándolo hasta el fondo.:</p>
      <p class="p" id="thats_better_">That’s better, but the top horizontal line of the axis is cut off, and the axis itself should be down at the base of the chart anyway. Here’s where SVG <span class="emphasis"><em>transformations</em></span> come in. By adding one line of code, we can<a id="id527974" class="indexterm" href=""></a><a id="id527980" class="indexterm" href=""></a> <code class="literal">transform</code> the entire axis group, pushing it to the bottom:</p>


      <pre class="programlisting" data-language="javascript" id="svgappendg_id4">svg.append("g")
    .attr("class", "axis")
    .attr("transform", "translate(0," + (h - padding) + ")")
    .call(xAxis);</pre>
<p class="it">Observe que utilizamos attr() para aplicar la transformada como un atributo de g. Transformaciones SVG son muy poderosos, y pueden aceptar varios tipos diferentes de transformar las definiciones, incluyendo escalas y rotaciones. Pero estamos manteniendo la sencillez aquí con sólo una traducción transformar, que simplemente empuja todo el grupo G encima y hacia abajo por una cierta cantidad.</p>
      <p class="p" id="note_that_we_us">Note that we use <code class="literal">attr()</code> to apply <code class="literal">transform</code> as an attribute of <code class="literal">g</code>. <a class="ulink" href="https://developer.mozilla.org/en-US/docs/SVG/Attribute/transform" target="_top">SVG transforms</a> are quite powerful, and can accept several different kinds of transform definitions, including scales and rotations. But we are keeping it simple here with only a <span class="emphasis"><em>translation</em></span> transform, which simply pushes the whole <code class="literal">g</code> group over and down by some amount.<a id="id528197" class="indexterm" href=""></a></p>



<p class="it">Transformadas de traducción se especifican con el fácil sintaxis de traducir (x, y), donde <code class="literal">x</code> e <code class="literal">y</code> son, obviamente, el número de píxeles horizontales y verticales que se trasladará al elemento. Así que, al final, nos gustaría nuestra <code class="literal">g</code> para parecerse a esto en el DOM:</p>
      <p class="p" id="translation_tra">Translation transforms are specified with the easy syntax of <code class="literal">translate(x,y)</code>, where <code class="literal">x</code> and <code class="literal">y</code> are, obviously, the number of horizontal and vertical pixels by which to translate the element. So, in the end, we would like our <code class="literal">g</code> to look like this in the DOM:</p>


      <pre class="programlisting" data-language="html" id="g_classaxis">&lt;g class="axis" transform="translate(0,280)"&gt;</pre>
<p class="it">Como puede ver, el <code class="literal">g.axis</code> no se mueve horizontalmente en absoluto, sino que es empujado 280 píxeles hacia abajo, convenientemente a la base de nuestra tabla. Especificamos tanto en esta línea de código:</p>
      <p class="p" id="as_you_can_see_id2">As you can see, the <code class="literal">g.axis</code> isn’t moved horizontally at all, but it is pushed 280 pixels down, conveniently to the base of our chart. We specify as much in this line of code:</p>


      <pre class="programlisting" data-language="javascript" id="attrtransfor">    .attr("transform", "translate(0," + (h - padding) + ")")</pre>
<p class="it">Tenga en cuenta el uso de <code class="literal">(h - padding)</code>, por lo que el borde superior del grupo se establece en <code class="literal">h</code>, la altura de la imagen completa , menos el valor de relleno que hemos creado antes. <code class="literal">(h - padding)</code> se calcula que es 280, y luego conecta con el resto de la cadena, por lo que el valor final para transformar la propiedad es <code class="literal">translate(0,280)</code>.</p>
      <p class="p" id="note_the_use_of">Note the use of <code class="literal">(h - padding)</code>, so the group’s top edge is set to <code class="literal">h</code>, the height of the entire image, minus the <code class="literal">padding</code> value we created earlier. <code class="literal">(h - padding)</code> is calculated to be <code class="literal">280</code>, and then connected to the rest of the string, so the final transform property value is<a id="id528402" class="indexterm" href=""></a> <code class="literal">translate(0,280)</code>.</p>

<p class="it">El resultado en la Figura 8-4 es mucho mejor! Salida del código hasta ahora en 02_axes_bottom.html.</p>
      <p class="p" id="the_result_in_i">The result in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch08.html#Nice_clean_axis" title="Figure 8-4. Nice, clean axis">Figure 8-4</a> is much better! Check out the code so far in <span class="emphasis"><em>02_axes_bottom.html</em></span>.</p>


      <div>

            <img src="/static/Y8KhUkEF36-img4.png" alt="Nice, clean axis"/>

<p class="fig">Figura 8-4. Lindo eje, limpio</p>
<p class="fig">Figure 8-4. Nice, clean axis</p>

    </div>


        <div>

          <h2 class="title">Check for Ticks</h2>


      </div>
<p class="it">Algunas garrapatas transmiten enfermedades, pero las ticks de D3 comunican información. Sin embargo, las ticks no son necesariamente mejores, y en cierto punto, comienzan a saturar su chart. Se dará cuenta de que nunca especificamos el número de ticks para incluir en el eje, ni qué intervalos deben aparecer. Sin instrucción clara, D3 ha examinado automagicamente nuestra escala <code class="literal">xScale</code> y hecho juicios informados sobre el número de ticks para incluir y en qué intervalos (cada 50, en este caso).</p>
      <p class="p" id="some_ticks_spre">Some ticks spread disease, but <a class="ulink" href="https://github.com/mbostock/d3/wiki/Quantitative-Scales#wiki-linear_ticks" target="_top">D3’s ticks</a> communicate information. Yet more ticks are not necessarily better, and at a certain point, they begin to clutter your chart. You’ll notice that we never specified how many ticks to include on the axis, nor at what intervals they should appear. Without clear instruction, D3 has automagically examined our scale <code class="literal">xScale</code> and made informed judgments about how many ticks to include, and at what intervals (every 50, in this case).<a id="id528482" class="indexterm" href=""></a><a id="id528490" class="indexterm" href=""></a><a id="id528496" class="indexterm" href=""></a></p>

<p class="it">Como era de esperar, puede personalizar todos los aspectos de sus ejes, empezando por el número aproximado de las ticks, utilizando <code class="literal">ticks()</code>:</p>
      <p class="p" id="as_you_would_ex">As you would expect, you can customize all aspects of your axes, starting with the rough number of ticks, using <code class="literal">ticks()</code>:</p>



      <pre class="programlisting" data-language="javascript" id="var_xaxis__d_id3">var xAxis = d3.svg.axis()
                  .scale(xScale)
                  .orient("bottom")
                  .ticks(5);  //Set rough # of ticks</pre>
<p class="it">Ver 03_axes_clean.html para ese código.</p>
      <p class="p" id="see__axes_cle">See <span class="emphasis"><em>03_axes_clean.html</em></span> for that code.</p>

<p class="it">Se dará cuenta de que en la Figura 8-5, a pesar de que especificamos sólo cinco ticks, D3 ha tomado una decisión ejecutiva y ordenada hasta un total de siete. Esto se debe a que D3 tiene su parte posterior, y ha descubierto que la inclusión de sólo cinco ticks requeriría cortar el dominio de entrada a menos que magnífico valores, en este caso, 0, 150, 300, 450, y 600. D3 intepreta los valores <code class="literal">ticks()</code> como una mera sugerencia y anulará su sugerencia con lo que se determina que son los valores más limpios y legibles en este caso, intervalos de 100, incluso cuando eso requiere incluyendo poco más o menos que las ticks requeridos. Esto es en realidad una característica totalmente brillante que aumenta la escalabilidad de su diseño; como los cambios de conjuntos de datos y el dominio de entrada expande o se contrae (números más grandes o números más pequeños), D3 asegura que las etiquetas señalizadoras siguen siendo fáciles de leer.</p>
      <p class="p" id="youll_notice_i">You’ll notice in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch08.html#Fewer_ticks" title="Figure 8-5. Fewer ticks">Figure 8-5</a> that, although we specified only five ticks, D3 has made an executive decision and ordered up a total of seven. That’s because D3 has got your back, and figured out that including only <span class="emphasis"><em>five</em></span> ticks would require slicing the input domain into less-than-gorgeous values—in this case, 0, 150, 300, 450, and 600. D3 inteprets the <code class="literal">ticks()</code> value as merely a suggestion and will override your suggestion with what it determines to be the most clean and human-readable values—in this case, intervals of 100—even when that requires including slightly more or fewer ticks than you requested. This is actually a totally brilliant feature that increases the scalability of your design; as the dataset changes and the input domain expands or contracts (bigger numbers or smaller numbers), D3 ensures that the tick labels remain easy to read.</p>



      <div>

            <img src="/static/Y8KhUkEF36-img5.png" alt="Fewer ticks"/>

<p class="fig">Figura 8-5. menos ticks</p>
<p class="fig">Figure 8-5. Fewer ticks</p>


      </div>

        <div>

          <h2 class="title">Y Not?</h2>

      </div>
<p class="it">Tiempo para etiquetar el eje vertical! Copiando y modificando el código que ya escribió para el <code class="literal">xAxis</code>, añadimos este cerca de la parte superior de nuestro código:</p>
      <p class="p" id="time_to_label_t">Time to label the vertical axis! By copying and tweaking the code we<a id="id528716" class="indexterm" href=""></a><a id="id528722" class="indexterm" href=""></a><a id="id528730" class="indexterm" href=""></a> already wrote for the <code class="literal">xAxis</code>, we add this near the top of of our code:</p>

<pre class="programlisting" data-language="javascript" id="define_y_axis">//Define Y axis
var yAxis = d3.svg.axis()
                  .scale(yScale)
                  .orient("left")
                  .ticks(5);</pre>
<p class="it">y esto, en la parte inferior:</p>
      <p class="p" id="and_this_near_">and this, near the bottom:</p>


      <pre class="programlisting" data-language="javascript" id="create_y_axis">//Create Y axis
svg.append("g")
    .attr("class", "axis")
    .attr("transform", "translate(" + padding + ",0)")
    .call(yAxis);</pre>
<p class="it">Nota en la Figura 8-6 que las etiquetas se orientarán a la izquierda y que el grupo <code class="literal">g</code> <code class="literal">yAxis</code> se traslada a la derecha por la cantidad de relleno.</p>
      <p class="p" id="note_in_that_th">Note in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch08.html#Initial_Y_axis" title="Figure 8-6. Initial y-axis">Figure 8-6</a> that the labels will be oriented <code class="literal">left</code> and that the <code class="literal">yAxis</code> group <code class="literal">g</code> is translated to the right by the amount <code class="literal">padding</code>.</p>


      <div>

            <img src="/static/Y8KhUkEF36-img6.png" alt="Initial y-axis"/>

<p class="fig">Figure 8-6. Initial y-axis</p>


      </div>
<p class="it">Esto empieza a parecerse a una tabla de verdad! Pero las etiquetas <code class="literal">yAxis</code> están siendo cortadas. Para darles más espacio en el lado izquierdo, voy a subir el valor de padding de 20 a 30:</p>
      <p class="p" id="this_is_startin">This is starting to look like a real chart! But the <code class="literal">yAxis</code> labels are getting cut off. To give them more room on the left side, I’ll bump up the value of <code class="literal">padding</code> from 20 to 30:</p>


      <pre class="programlisting" data-language="javascript" id="var_padding___id2">var padding = 30;</pre>
<p class="it">Por supuesto, también se puede introducir las variables<code class="literal">padding</code>  independientes para cada eje, y decir <code class="literal">xPadding</code> y <code class="literal">yPadding</code>, para obtener más control sobre el diseño.</p>
      <p class="p" id="of_course_you__id4">Of course, you could also introduce separate <code class="literal">padding</code> variables for each axis, say <span class="keep-together"><code class="literal">xPadding</code></span> and <code class="literal">yPadding</code>, for more control over the layout.<a id="id529154" class="indexterm" href=""></a></p>

<p class="it">Ver el código actualizado en 04_axes_y.html. Se parece a la Figura 8-7.</p>
      <p class="p" id="see_the_updated">See the updated code in <span class="emphasis"><em>04_axes_y.html</em></span>. It looks like <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch08.html#Scatterplot_with_Y_axis" title="Figure 8-7. Scatterplot with y-axis">Figure 8-7</a>.</p>

      
      <div>

            <img src="/static/Y8KhUkEF36-img7.png" alt="Scatterplot with y-axis"/>

<p class="fig">Figura 8-7. Diagrama de dispersión con eje Y</p>
        <p class="fig">Figure 8-7. Scatterplot with y-axis</p>


</div>



        <div>

          <h2 class="title">Final Touches</h2>

        </div>
<p class="it">Soy consciente de que hasta ahora ha estado muy tranquilo y educado, y no confrontamos de ningúna manera. Sin embargo, todavía siento que tengo que ganar más. Así que para demostrarle a usted que nuestros nuevos ejes son dinámicos y escalables, me gustaría pasar del uso de un conjunto de datos estáticos al uso de números aleatorios:</p>
      <p class="p" id="i_appreciate_th">I appreciate that so far you have been very quiet and polite, and not at all confrontational. Yet I still feel as though I have to win you over. So to prove to you that our new axes are dynamic and scalable, I’d like<a id="id529241" class="indexterm" href=""></a><a id="id529249" class="indexterm" href=""></a> to switch from using a static dataset to using randomized numbers:</p>


      <pre class="programlisting" data-language="javascript" id="dynamic_rand">//Dynamic, random dataset
var dataset = [];
var numDataPoints = 50;
var xRange = Math.random() * 1000;
var yRange = Math.random() * 1000;
for (var i = 0; i &lt; numDataPoints; i++) {
    var newNumber1 = Math.floor(Math.random() * xRange);
    var newNumber2 = Math.floor(Math.random() * yRange);
    dataset.push([newNumber1, newNumber2]);
}</pre>
<p class="it">Este código inicializa una array vacía, a continuación, recorre 50 veces, elige dos números aleatorios cada vez, y se suma ("empuja") el par de valores en la array <code class="literal">dataset</code> (véase la Figura 8-8).</p>
      <p class="p" id="this_code_initi">This code initializes an empty array, then loops through 50 times, chooses two random numbers each time, and adds (“pushes”) that pair of values to the <code class="literal">dataset</code> array (see <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch08.html#Scatterplot_with_random_data" title="Figure 8-8. Scatterplot with random data">Figure 8-8</a>).</p>


      <div>

            <img src="/static/Y8KhUkEF36-img8.png" alt="Scatterplot with random data"/>

<p class="it">Figura 8-8. Diagrama de dispersión con datos aleatorios</p>
        <p class="fig">Figure 8-8. Scatterplot with random data</p>


      </div>
<p class="it">Pruebe el código aleatorio en el conjunto de datos</p> 05_axes_random.html. Cada vez que vuelva a cargar la página, obtendrá diferentes valores de los datos. Observe cómo la escala de ambos ejes se adapta a los nuevos dominios, y las ticks y los valores de la etiqueta se eligen en consecuencia.<p></p>
      <p class="p" id="try_out_that_ra">Try out that randomized dataset code in <span class="emphasis"><em>05_axes_random.html</em></span>. Each time you reload the page, you’ll get different data values. Notice how both axes scale to fit the new domains, and ticks and label values are chosen accordingly.</p>

<p class="it">Después de haber probado mi punto, creo que por fin podemos cortar esas etiquetas horribles, rojo, comentando las líneas correspondientes del código.</p>
      <p class="p" id="having_made_my_">Having made my point, I think we can finally cut those horrible, red labels, by commenting out the relevant lines of code.</p>

<p class="it">El resultado se muestra en la Figura 8-9. Nuestro código de dispersión definitiva vive en 06_axes_no_labels.html.</p>
      <p class="p" id="the_result_is_s">The result is shown in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch08.html#Scatterplot_with_random_data_and_no_red_labels" title="Figure 8-9. Scatterplot with random data and no red labels">Figure 8-9</a>. Our final scatterplot code lives in <span class="emphasis"><em>06_axes_no_labels.html</em></span>.</p>


      <div>

            <img src="/static/Y8KhUkEF36-img9.png" alt="Scatterplot with random data and no red labels"/>

<p class="fig">Figura 8-9. Diagrama de dispersión con datos aleatorios y sin etiquetas rojas</p>
<p class="fig">Figure 8-9. Scatterplot with random data and no red labels</p>


      </div>

        <div>

          <h2 class="title">Formatting Tick Labels</h2>

        </div>
<p class="it">Una última cosa: hasta ahora, hemos estado trabajando con números enteros -que son agradables y fáciles-. Pero los datos a menudo son más sucios, y en esos casos, es posible que desee más control sobre cómo se formatean las etiquetas de los ejes. Introduzca <code class="literal">tickFormat()</code>, que le permite especificar cómo se deben formatear sus números. Por ejemplo, es posible que desee incluir tres lugares después del punto decimal, los valores de indicación o como porcentajes, o ambas cosas.</p>
      <p class="p" id="one_last_thing">One last thing: so far, we’ve been working with integers—whole numbers—which are nice and easy. But data is often messier, and in those cases, you might want more control over how the axis labels are formatted.<a id="id529796" class="indexterm" href=""></a><a id="id529804" class="indexterm" href=""></a> Enter <a class="ulink" href="https://github.com/mbostock/d3/wiki/Quantitative-Scales#wiki-linear_tickFormat" target="_top"><code class="literal">tickFormat()</code></a>, which enables you to specify how your numbers should be formatted. For example, you might want to include three places after the decimal point, or display values as percentages, or both.</p>


<p class="it">Para utilizar <code class="literal">tickFormat()</code>, primero debe definir una nueva función de formato de número. Éste, por ejemplo, indica tratar los valores como porcentajes con una precisión de punto decimal. Es decir, si se le da esta función al número 0.23, devolverá la cadena de 23,0%. (Véase la entrada de referencia para <code class="literal">d3.format()</code> para más opciones.)</p>      
      <p class="p" id="to_use_tickform">To use <code class="literal">tickFormat()</code>, first define a new number-formatting function. This one, for example, says to treat values as percentages with one decimal point precision. That is, if you give this function the number <code class="literal">0.23</code>, it will return the string <code class="literal">23.0%</code>. (See <a class="ulink" href="https://github.com/mbostock/d3/wiki/Formatting#wiki-d3_format" target="_top">the reference entry for <code class="literal">d3.format()</code></a> for more options.)</p>


      <pre class="programlisting" data-language="javascript" id="var_formatasper">var formatAsPercentage = d3.format(".1%");</pre>
<p class="it">A continuación, informe a su eje de usar esa función de formato para sus ticks, por ejemplo:</p>
      <p class="p" id="then_tell_your">Then, tell your axis to use that formatting function for its ticks, for example:</p>


      <pre class="programlisting" data-language="javascript" id="xaxistickforma">xAxis.tickFormat(formatAsPercentage);</pre>

<p class="it">Me resulta más fácil de probar estas funciones de formato en la consola de JavaScript. Por ejemplo, basta con abrir cualquier página que carga D3, como 06_axes_no_labels.html, y escriba su regla de formato en la consola. A continuación, compruebelo introduciendo un valor, como lo haría con cualquier otra función.</p>
        <p class="p" id="i_find_it_easie_id2">I find it easiest to test these formatting functions out in the JavaScript console. For example, just open any page that loads D3, such as <span class="keep-together"><span class="emphasis"><em>06_axes_no_labels.html</em></span></span>, and type your format rule into the console. Then test it by feeding it a value, as you would with any other function.<a id="id529975" class="indexterm" href=""></a></p>

<p class="it">Se puede ver en la figura 8-10 que un valor de datos de 0,54321 se convierte en un 54,3% a los fines de una visualización perfecta!</p>
        <p class="p" id="you_can_see_in_">You can see in<a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch08.html#Testing_format_console" title="Figure 8-10. Testing format() in the console">Figure 8-10</a> that a data value of <code class="literal">0.54321</code> is converted to <code class="literal">54.3%</code> for display purposes—perfect!</p>


        <div>

              <img src="/static/Y8KhUkEF36-img10.png" alt="Testing format() in the console"/>

<p class="fig">Figure 8-10. Testing format() in the console</p>

      </div>
<p class="it">Se puede jugar con ese código en 07_axes_format.html. Obviamente, un formato de porcentaje no tiene sentido con el conjunto de datos actual de nuestro diagrama de dispersión, sino como un ejercicio, usted podría intentar ajustar cómo se generan los números al azar, para hacer, los valores de números no enteros más apropiadas, o simplemente experimentar con la función de formateo en sí misma.</p>
      <p class="p" id="you_can_play_wi">You can play with that code in <span class="emphasis"><em>07_axes_format.html</em></span>. Obviously, a percentage format doesn’t make sense with our scatterplot’s current dataset, but as an exercise, you could try tweaking how the random numbers are generated, to make more appropriate, non-whole number values, or just experiment with the format function itself.<a id="id530107" class="indexterm" href=""></a></p>



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