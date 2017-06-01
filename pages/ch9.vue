<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    
    <div class="block">
    <h1 class="title">Chapter 9. Updates, Transitions, and Motion</h1><p class="it">Hasta este punto, hemos utilizado solamente conjuntos de datos estáticos. Pero los datos del mundo real casi siempre cambian con el tiempo. Y es posible que desee su visualización para reflejar esos cambios.</p>

<p class="p" id="until_this_poin">Until this point, we have used only static datasets. But real-world data almost always <span class="emphasis"><em>changes</em></span> over time. And you might want your visualization to reflect those changes.<a id="ix_updates" class="indexterm" href=""></a></p>
<p class="it">En términos D3, esos cambios son manejados por las actualizaciones. Los ajustes visuales se hacen bastante con las transiciones, pudiendo emplear el movimiento para beneficiar la percepción.</p>

<p class="p" id="in_d_terms_th">In D3 terms, those changes are handled by <span class="emphasis"><em>updates</em></span>. The visual adjustments are made pretty with <span class="emphasis"><em>transitions</em></span>, which can employ <span class="emphasis"><em>motion</em></span> for perceptual benefit.<a id="id530167" class="indexterm" href=""></a></p>
 
  <p class="it">Empezaremos por generar una visualización con un conjunto de datos, y luego cambiar los datos por completo.</p>

  <p class="p" id="well_start_by__id2" >We’ll start by generating a visualization with one dataset, and then changing the data completely.</p>


        <h2 class="title">Modernizing the Bar Chart</h2>

   <p class="bar">Listo? De acuerdo, sólo dame un segundo ...</p>   <p class="bar">02_bar_chart_with_scales.html.</p>
    

    <p class="it"> Vamos a revisar nuestro viejo gráfico de barras de confianza en la Figura 9-1.</p>

    <p class="p" id="lets_revisit_o">Let’s revisit our trusty old bar chart in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch09.html#The_bar_chart_as_seen_last" title="Figure 9-1. The bar chart, as seen last">Figure 9-1</a>.</p>
    


    <div>

          <img src="/static/oSwB5mh6Ca-img1.png" alt="The bar chart, as seen last"/>

<p class="fig">Figura 9-1. El gráfico de barras, como se ha visto por última vez</p>
<p class="fig">Figure 9-1. The bar chart, as seen last</p>
            

    </div>

    

    <p class="it">Si examina el código en 01_bar_chart.html, verá que hemos utilizado este conjunto de datos estático:</p>

    <p class="p" id="if_you_examine_">If you examine the code in <span class="emphasis"><em>01_bar_chart.html</em></span>, you’ll see that we used this static dataset:</p>
    


    <pre class="programlisting" data-language="javascript" id="var_dataset___id17">var dataset = [ 5, 10, 13, 19, 21, 25, 22, 18, 15, 13,
                11, 12, 15, 20, 18, 17, 16, 18, 23, 25 ];</pre>

    

    <p class="it">Desde entonces, hemos aprendido cómo escribir código más flexible, por lo que cambiar el tamaño de nuestro elemento gráfico para dar cabida a diferentes tamaños de conjuntos de datos(es decir arrays más cortas o más largas) y diferentes valores de datos (números más pequeños o más grandes). Hemos logrado flexibilidad usando escalas D3, por lo que me gustaría empezar por llevar nuestro gráfico de barras a mas velocidad.</p>

    <p class="p" id="since_then_we">Since then, we’ve learned how to write more flexible code, so our chart elements resize to accommodate different sized datasets (meaning shorter or longer arrays) and different data values (smaller or larger numbers). We accomplished that flexibility using D3 scales, so I’d like to start by bringing our bar chart up to speed.<a id="ix_ubcht" class="indexterm" href=""></a></p>
    


    

    <p class="it">Listo? De acuerdo, sólo dame un segundo ...</p>

    <p class="p" id="ready_okay_ju">Ready? Okay, just give me a sec…</p>
    

   
    

    <p class="it">Aaaaaand, hecho! Gracias por esperar.</p>

    <p class="p" id="aaaaaand_done">Aaaaaand, done! Thanks for waiting.</p>
    

    

    <p class="it">Figura 9-2 se ve bastante similar, pero mucho ha cambiado bajo el capó. Puede seguir junto al abrir 02_bar_chart_with_scales.html.</p>

    <p class="p" id="looks_pretty_si"><a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch09.html#A_scalable_flexible_bar_chart" title="Figure 9-2. A scalable, flexible bar chart">Figure 9-2</a> looks pretty similar, but a lot has changed under the hood. You can<a id="ix_bcscal" class="indexterm" href=""></a> follow along by opening up <span class="emphasis"><em>02_bar_chart_with_scales.html</em></span>.</p>
    

    <div>

          <img src="/static/oSwB5mh6Ca-img2.png" alt="A scalable, flexible bar chart"/>

<p class="fig">Figura 9-2. Un flexible y escalable gráfico de barras</p>
      <p class="fig">Figure 9-2. A scalable, flexible bar chart</p>
            
    </div>
   
    

    <p class="it">Para empezar, ajusté la anchura y la altura, para hacer el gráfico más alto y ancho:</p>

    <p class="p" id="to_start_i_adj">To start, I adjusted the width and height, to make the chart taller and wider:</p>
    
<pre class="programlisting" data-language="javascript" id="var_w___va_id1">var w = 600;
var h = 250;</pre>

    

    <p class="it">A continuación, introduje una escala ordinal para manejar el posicionamiento izquierda/derecha de barras y etiquetas a lo largo del eje x:</p>

    <p class="p" id="next_i_introdu">Next, I introduced an <span class="emphasis"><em>ordinal scale</em></span> to handle the left/right<a id="id530613" class="indexterm" href=""></a> positioning of bars and labels along the x-axis:</p>
    <pre class="programlisting" data-language="javascript" id="var_xscale__d_id2">var xScale = d3.scale.ordinal()
                .domain(d3.range(dataset.length))
                .rangeRoundBands([0, w], 0.05);</pre>

    

    <p class="it">Esto puede parecer un galimatías, así que voy a avanzar de una línea a la vez.</p>

    <p class="p" id="this_may_seem_l">This may seem like gobbledegook, so I’ll walk through it one line at a time.</p>


          <h3 class="title">Ordinal Scales, Explained</h3>

      <p class="it">En primer lugar, en esta línea:</p>

      <p class="p" id="first_in_this_">First, in this line:</p>
      

      <pre class="programlisting" data-language="javascript" id="var_xscale__d_id3">var xScale = d3.scale.ordinal()</pre>

      

      <p class="it">declaramos una nueva variable llamada <code class="literal">xScale</code>, tal como lo habíamos hecho con nuestro diagrama de dispersión. Sólo que aquí, en lugar de una escala lineal, creamos un ordinal. Las escalas ordinales se usan típicamente para datos ordinales, típicamente categorías con alguna orden inherente a ellos, tal como aqui:</p>

      <p class="p" id="we_declare_a_ne">we declare a new variable called <code class="literal">xScale</code>, just as we had done with our scatterplot. Only here, instead of a <span class="emphasis"><em>linear</em></span> scale, we create an <span class="emphasis"><em>ordinal</em></span> one. Ordinal scales are typically used for ordinal data, typically categories with some inherent <span class="emphasis"><em>order</em></span> to them, such as:</p>
      <div class="itemizedlist" id="freshman_sopho_id1">

        <ul class="itemizedlist">

          <li class="p"> freshman, sophomore, junior, senior </li>

          <li class="p"> grade B, grade A, grade AA </li>

          <li class="p"> strongly dislike, dislike, neutral, like, strongly like </li>

        </ul>

      </div>

      

      <p class="it">Nosotros no tenemos los datos ordinales verdaderos para su uso con este gráfico de barras. En su lugar, sólo queremos que las barras que se puedan extraer de izquierda a derecha en el mismo orden en el que los valores se dan en nuestra base de datos. La escala ordinal D3 es útil en esta situación, cuando tenemos muchos elementos visuales (barras verticales) que se colocan en un orden arbitrario (de izquierda a derecha), sino que debe ser espaciados uniformemente. Esto se aclarará en un momento.</p>

      <p class="p" id="we_dont_have_t">We don’t have true ordinal data for use with this bar chart. Instead, we just want the bars to be drawn from left to right using the same order in which values occur in our dataset. D3’s ordinal scale is useful in this situation, when we have many visual elements (vertical bars) that are positioned in an arbitrary order (left to right), but must be evenly spaced. This will become clear in a moment.<a id="id530893" class="indexterm" href=""></a></p>
      

      <pre class="programlisting" data-language="javascript" id="domaindrang_id1">.domain(d3.range(dataset.length))</pre>

      

      <p class="it">La siguiente línea de código establece el dominio de entrada para la escala. Recuerda cómo las escalas lineales necesitan una array de dos valores para establecer sus dominios, como en [0, 100]? Para una escala lineal, esa array fijaría los valores bajos y altos de dominio. Pero dominios ordinales son, así, ordinales, por lo que no se piensan en forma lineal, en términos cuantitativos. Para establecer el dominio de una escala ordinal, generalmente se especifican una array con los nombres de las categorías, como en:</p>

      <p class="p" id="this_next_line_">This next line of code sets the input domain for the scale. Remember how linear scales need a two-value array to set their domains, as in <code class="literal">[0, 100]</code>? For a linear scale, that array would set the low and high values of the domain. But ordinal domains are, well, ordinal, so they don’t think in linear, quantitative terms. To set the domain of an ordinal scale, you typically specify an array with the category names, as in:</p>
      


      <pre class="programlisting" data-language="javascript" id="domainfresh">.domain(["freshman", "sophomore", "junior", "senior"])</pre>

      

      <p class="it">Para nuestro gráfico de barras, que no tiene categorías explícitas, pero podríamos asignar a cada punto de los datos o bar un valor de ID correspondiente a su posición dentro de la array de datos, como en 0, 1, 2, 3, y así sucesivamente. Así que tal vez nuestro estado de dominio se podría leer:</p>

      <p class="p" id="for_our_bar_cha">For our bar chart, we don’t have explicit categories, but we could assign each data point or bar an ID value corresponding to its position within the <code class="literal">dataset</code> array, as in 0, 1, 2, 3, and so on. So perhaps our domain statement could read:</p>
      


      <pre class="programlisting" data-language="javascript" id="domain__">.domain([0, 1, 2, 3, 4, 5, 6, 7, 8, 9,
         10, 11, 12, 13, 14, 15, 16, 17, 18, 19])</pre>

      

      <p class="it">Resulta que hay una manera muy simple para generar rápidamente una serie de números secuenciales: el método <code class="literal">d3.range()</code>.</p>

      <p class="p" id="it_turns_out_th">It turns out there is a very simple way to quickly generate an array of sequential numbers: the <code class="literal">d3.range()</code> method.<a id="id531267" class="indexterm" href=""></a><a id="id531273" class="indexterm" href=""></a></p>
      

     

      

      <p class="it">Mientras ve 02_bar_chart_with_scales.html, abra la consola, y escriba lo siguiente:</p>

      <p class="p" id="while_viewing_">While viewing <span class="emphasis"><em>02_bar_chart_with_scales.html</em></span>, go ahead and open up the console, and type the following:</p>
      <pre class="screen" id="drange">d3.range(10)</pre>

      

      <p class="it">Debería ver el siguiente array de salida:</p>

      <p class="p" id="you_should_see__id2">You should see the following output array:</p>
      <pre class="screen" id="____id2">[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]</pre>

      

      <p class="it">¿Qué lindo que es? D3 le ahorra tiempo, una vez más (y la molestia de los loops extra para <code class="literal">for()</code>).</p>

      <p class="p" id="how_nice_is_tha">How nice is that? D3 saves you time once again (and the hassle of extra <code class="literal">for()</code> loops).</p>
      

      <p class="it">Volviendo al código, debería estar claro lo que está pasando aquí:</p>

      <p class="p" id="coming_back_to_">Coming back to our code, it should now be clear what’s happening here:</p>
      <pre class="programlisting" data-language="javascript" id="domaindrang_id2">.domain(d3.range(dataset.length))</pre>

      <div class="orderedlist" id="datasetlength_id1">

        <ol class="orderedlist" type="1">
 <li class="it"> <code class="literal">dataset.length</code>, en este caso, se evalua como <code class="literal">20</code>, porque tenemos 20 artículos en nuestra base de datos. </li>
          <li class="p"> <code class="literal">dataset.length</code>, in this case, is evaluted as <code class="literal">20</code>, because we have 20 items in our dataset. </li>
         
<li class="it"> <code class="literal">d3.range(20)</code> a continuación, se evalúa, que devuelve este array: <code class="literal">[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19]</code>. </li>
          <li class="p"> <code class="literal">d3.range(20)</code> is then evaluated, which returns this array: <code class="literal">[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19]</code>. </li>
          
<li class="it"> Por último, <code class="literal">domain()</code> establece el dominio de nuestra nueva escala ordinal a esos valores. </li>
          <li class="p"> Finally, <code class="literal">domain()</code> sets the domain of our new ordinal scale to those values. </li>
          

        </ol>

      </div>

      

      <p class="it">Esto podría ser un tanto confuso porque estamos utilizando números (0, 1, 2 ...) como valores ordinales, pero los valores ordinales son típicamente no numéricos.</p>

      <p class="p" id="this_might_be_s">This might be somewhat confusing because we are using numbers (0, 1, 2…) as ordinal values, but ordinal values are typically nonnumeric.</p>
      
          <h3 class="title">Round Bands Are All the Range These Days</h3>


      

      <p class="it">Lo bueno de <code class="literal">d3.scale.ordinal()</code> es que es compatible con los rangos de bandas. En lugar de devolver un rango continuo, como cualquier escala cuantitativa (como <code class="literal">d3.scale.linear()</code>), las escalas ordinales utilizan rangos discretos, es decir, los valores de salida están determinados de antemano, y podrían ser numéricos o no.</p>

      <p class="p" id="the_great_thing">The great thing about <code class="literal">d3.scale.ordinal()</code> is it supports <span class="emphasis"><em>range banding</em></span>. Instead of returning a continuous range, as any quantitative scale (like <code class="literal">d3.scale.linear()</code>) would, ordinal scales use <span class="emphasis"><em>discrete</em></span> ranges, meaning the output values are determined in advance, and could be numeric or not.<a id="id531496" class="indexterm" href=""></a><a id="id531502" class="indexterm" href=""></a><a id="id531507" class="indexterm" href=""></a></p>
      

      <p class="it">Podríamos usar <code class="literal">range()</code> como todos los demás, o podemos hacerla facil y utilizar <code class="literal">rangeBands()</code>, que toma un valor bajo y alto, y automáticamente lo divide en trozos o incluso "bandas", basado en la longitud del dominio. Por ejemplo:</p>

      <p class="p" id="we_could_use_ra">We could use <code class="literal">range()</code> like everyone else, <span class="emphasis"><em>or</em></span> we can be smooth and use <code class="literal">rangeBands()</code>, which takes a low and high value, and automatically divides it into even chunks or “bands,” based on the length of the domain. For example:</p>
      <pre class="programlisting" data-language="javascript" id="rangebands_id1">.rangeBands([0, w])</pre>

      

      <p class="it"> esto dice ". calcular incluso bandas que empiezan en 0 y terminan en <code class="literal">w</code>, a continuación, ajustar la gama de la escala de esas bandas" En nuestro caso, hemos especificado 20 valores en el dominio, por lo que D3 calculará:</p>

      <p class="p" id="this_says_calc">this says “calculate even bands starting at 0 and ending at <code class="literal">w</code>, then set this scale’s range to those bands.” In our case, we specified 20 values in the domain, so D3 will calculate:</p>
      <pre class="screen" id="w____xscal">(w - 0) / xScale.domain().length
(600 - 0) / 20
600 / 20
30</pre>

      

      <p class="it">Al final, cada banda será de 30 "de ancho".</p>

      <p class="p" id="in_the_end_eac">In the end, each band will be <code class="literal">30</code> “wide.”</p>
      

      <p class="it">También es posible incluir un segundo parámetro, que pone un poco de espacio entre cada banda. Aquí, he utilizado 0.2, lo que significa que 20 por ciento de la anchura de cada banda se utilizará para el espaciado entre bandas:</p>

      <p class="p" id="it_is_also_poss">It is also possible to include a second parameter, which includes a bit of spacing between each band. Here, I’ve used <code class="literal">0.2</code>, meaning that 20 percent of the width of each band will be used for spacing in between bands:</p>
      <pre class="programlisting" data-language="javascript" id="rangebands_id2">.rangeBands([0, w], 0.2)</pre>

      

      <p class="it">Podemos ser incluso más suaves usando <code class="literal">rangeRoundBands()</code>, que es el mismo que <code class="literal">rangeBands()</code>, excepto que los valores de salida se redondean al entero más cercano de píxeles, por lo que se convierte 12.3456 en sólo 12 , por ejemplo. Esto es útil para mantener los elementos visuales alineados precisamente en la cuadrícula de píxeles, para limpiar, bordes afilados.</p>

      <p class="p" id="we_can_be_even_">We can be even smoother and use <code class="literal">rangeRoundBands()</code>, which is the same as <code class="literal">rangeBands()</code>, except that the output values are rounded to the nearest whole pixel, so 12.3456 becomes just 12, for example. This is helpful for keeping visual elements lined up precisely on the pixel grid, for clean, sharp edges.<a id="id531695" class="indexterm" href=""></a><a id="id531703" class="indexterm" href=""></a><a id="id531709" class="indexterm" href=""></a></p>
      

      <p class="it">Puedo también disminuir la cantidad de espacio a sólo el 5 por ciento. Por lo tanto, en nuestra última línea de código la declaración será:</p>

      <p class="p" id="ill_also_decre">I’ll also decrease the amount of spacing to just 5 percent. So, our final line of code in that statement is:</p>
      <pre class="programlisting" data-language="javascript" id="rangeroundband">.rangeRoundBands([0, w], 0.05);</pre>

      

      <p class="it">Esto nos da buenos valores de píxel, limpios, con un poco de Teensy de espacio visual entre ellos.</p>

      <p class="p" id="this_gives_us_n">This gives us nice, clean pixel values, with a teensy bit of visual space between them.</p>


          <h3 class="title">Referencing the Ordinal Scale</h3>
      

      <p class="it">Más adelante en el código (y yo recomiendo la visualización de la fuente), cuando creamos los elementos<code class="literal">rect</code>, establecemos sus posiciones, de eje horizontal x, así:</p>

      <p class="p" id="later_in_the_co">Later in the code (and I recommend viewing the source), when we create<a id="id531795" class="indexterm" href=""></a> the <code class="literal">rect</code> elements, we set their horizontal, x-axis positions like so:</p>
      <pre class="programlisting" data-language="javascript" id="create_bars_s_id1">//Create bars
svg.selectAll("rect")
   .data(dataset)
   .enter()
   .append("rect")
   .attr("x", function(d, i) {
      return xScale(i);         // &lt;-- Set x values
   })
           …</pre>

      

      <p class="it">Tenga en cuenta que, debido a que incluyen <strong>d</strong> e <strong>i</strong> como parámetros a la función anónima, D3 a transmitir automáticamente los valores correctos. Por supuesto, <strong>d</strong> es el punto de referencia actual, e <strong>i</strong> es el valor del índice. Así que se pasará 0, 1, 2, 3, y así sucesivamente.</p>

      <p class="p" id="note_that_beca">Note that, because we include <code class="literal">d</code> and <code class="literal">i</code> as parameters to the anonymous function, D3 will automatically pass in the correct values. Of course, <code class="literal">d</code> is the current datum, and <code class="literal">i</code> is its index value. So <code class="literal">i</code> will be passed 0, 1, 2, 3, and so on.</p>
      

      <p class="it">Casualmente (mmm!), Se utilizaron esos mismos valores (0, 1, 2, 3 ...) para el dominio de entrada de nuestra escala ordinal. Así que cuando llamamos a <code class="literal">xScale(i)</code> y <code class="literal">xScale()</code> va a buscar el valor ordinal <strong>i</strong>  y devuelve su valor (banda) asociado de salida. (Usted puede verificar todo esto por sí mismo en la consola. Sólo trate de escribir <code class="literal">xScale(0)</code> o <code class="literal">xScale(5)</code>).</p>

      <p class="p" id="coincidentally_">Coincidentally (hmmm!), we used those same values (0, 1, 2, 3…) for our ordinal scale’s input domain. So when we call <code class="literal">xScale(i)</code>, <code class="literal">xScale()</code> will look up the ordinal value <code class="literal">i</code> and return its associated output (band) value. (You can verify all this for yourself in the console. Just try typing <code class="literal">xScale(0)</code> or <code class="literal">xScale(5)</code>.)</p>
      

      <p><strong>Ejercicio</strong></p>

      

      <p class="it">Aún mejor, el establecimiento de las anchuras de estas barras es ahora mucho más fácil. Antes de usar la escala ordinal, teniamos:</p>

      <p class="p" id="even_better_se">Even better, setting the widths of these bars just got a lot easier. Before using the ordinal scale, we had:</p>
      <pre class="programlisting" data-language="javascript" id="attrwidth__id2">.attr("width", w / dataset.length - barPadding)</pre>

      

      <p class="it">No necesitamos mas siquiera a <code class="literal">barPadding</code> porque ahora el relleno está integrado en <code class="literal">rangeRoundBands()</code>. Ajusta el ancho de cada <code class="literal">rect</code> sólo lo que esta necesita:</p>

      <p class="p" id="we_dont_even_n">We don’t even need <code class="literal">barPadding</code> anymore because now the padding is built into <span class="keep-together"><code class="literal">rangeRoundBands()</code></span>. Setting the width of each <code class="literal">rect</code> needs only<a id="id532238" class="indexterm" href=""></a><a id="id532244" class="indexterm" href=""></a> this:</p>
      <pre class="programlisting" data-language="javascript" id="attrwidth__id3">.attr("width", xScale.rangeBand())</pre>

      

      <p class="it">¿No es agradable cuando D3 hace los cálculos por usted?</p>

      <p class="p" id="isnt_it_nice_w">Isn’t it nice when D3 does the math for you?</p>


          <h3 class="title">Other Updates</h3>
   

      <p class="it">He hecho varias otras actualizaciones en 02_bar_chart_with_scales.html, incluyendo la creación de una nueva escala lineal <code class="literal">yScale</code> para calcular los valores verticales. Usted ya sabe cómo utilizar las escalas lineales, por lo que puede rozar la fuente y tenga en cuenta la forma en que la utiliza para ajustar las alturas de las barras.</p>

      <p class="p" id="ive_made_sever">I’ve made several other updates in <span class="emphasis"><em>02_bar_chart_with_scales.html</em></span>, including creating a new linear scale <code class="literal">yScale</code> to calculate vertical values. You already know how to use linear scales, so you can skim the source and note how that’s being used to set the bar heights.<a id="id532334" class="indexterm" href=""></a></p>


        <h2 class="title">Updating Data</h2>


    <p class="it"> De acuerdo, una vez más, tenemos el gráfico de barras increíble mostrado en la Figura 9-3, lo suficientemente flexible como para manejar cualquier dato que pueda lanzar en él.</p>

    <p class="p" id="okay_once_agai">Okay, once again, we have the amazing bar chart shown in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch09.html#The_bar_chart" title="Figure 9-3. The bar chart">Figure 9-3</a>, flexible enough to handle any data we can throw at it.<a id="id532367" class="indexterm" href=""></a></p>
    <div>

          <img src="/static/oSwB5mh6Ca-img3.png" alt="The bar chart"/>


      <p class="fig">Figure 9-3. The bar chart</p>

    </div>

    

    <p class="it"> ¿O es eso? Vamos a ver.</p>

    <p class="p" id="or_is_it_lets">Or is it? Let’s see.</p>
    

    <p class="it">El tipo más simple de actualización es cuando todos los valores de los datos se actualizan al mismo tiempo y el número de valores sigue siendo el mismo.</p>

    <p class="p" id="the_simplest_ki">The simplest kind of update is when all data values are updated at the same time <span class="emphasis"><em>and</em></span> the number of values stays the same.</p>
    

    <p class="it">El enfoque básico en este escenario es la siguiente:</p>

    <p class="p" id="the_basic_appro">The basic approach in this scenario is this:</p>
    <div>

      <ol class="orderedlist" type="1">
<li class="it">Modificar los valores del conjunto de datos.</li>
        

        <li class="p"> Modify the values in your dataset. </li>
        


        
<li class="it">Volver a vincular los nuevos valores de los elementos existentes (sobrescribir con ello los valores originales).</li>
        <li class="p"> Rebind the new values to the existing elements (thereby overwriting the original values). </li>
        


        <li class="it"> Establecer nuevos valores de los atributos según sea necesario para actualizar la presentación visual.</li>

        <li class="p"> Set new attribute values as needed to update the visual display. </li>
        


      </ol>

    </div>
<p class="it">Puede suceder antes de cualquiera de esos pasos , sin embargo, un cierto acontecimiento tiene que poner las cosas fuera. Hasta ahora, todo nuestro código se ha ejecutado inmediatamente al cargar la página. Podríamos tener nuestra actualización pasa justo después de que el código de dibujo inicial, pero va a pasar imperceptiblemente rápido. Para asegurarnos de que podemos observar el cambio como es el caso, vamos a separar nuestro código de actualización de todo lo demás. Vamos a necesitar un "gatillo" algo que sucede después de la carga de la página para aplicar las actualizaciones. ¿Qué tal un clic del ratón?</p>

    <p class="p" id="before_any_of_t">Before any of those steps can happen, though, some <span class="emphasis"><em>event</em></span> needs to kick things off. So far, all of our code has executed immediately on page load. We <span class="emphasis"><em>could</em></span> have our update run right after the initial drawing code, but it would happen imperceptibly fast. To make sure we can observe the change as it happens, we will separate our update code from everything else. We will need a “trigger,” something that happens <span class="emphasis"><em>after</em></span> page load to apply the updates. How about a mouse click?</p>


          <h3 class="title">Interaction via Event Listeners</h3>
          <h3 class="title">La interacción a través de detectores de eventos</h3>


      

      <p class="it">Cualquier elemento DOM se puede usar, por lo que en lugar de diseñar un botón de fantasía, voy a añadir un simple punto <code class="literal">p</code>  en el body del código HTML:</p>

      <p class="p" id="any_dom_element">Any DOM element can be used, so rather than design a fancy button, I’ll<a id="id532487" class="indexterm" href=""></a><a id="id532495" class="indexterm" href=""></a> add a simple <code class="literal">p</code> paragraph to the HTML’s <code class="literal">body</code>:</p>
      <pre class="programlisting" data-language="html" id="pclick_on_thi_id1">&lt;p&gt;Click on this text to update the chart with new data values (once).&lt;/p&gt;</pre>

      

      <p class="it"> Luego, hacia el final de nuestro código D3, agreguemos lo siguiente:</p>

      <p class="p" id="then_down_at_t">Then, down at the end of our D3 code, let’s add the following:</p>
      <pre class="programlisting" data-language="javascript" id="dselectp__id1">d3.select("p")
    .on("click", function() {
        //Do something  on click
    });</pre>

      

      <p class="it">Esto selecciona nuestro nuevo <code class="literal">p</code>, y luego se añade un detector de eventos para ese elemento. Eh?</p>

      <p class="p" id="this_selects_ou">This selects our new <code class="literal">p</code>, and then adds an <span class="emphasis"><em>event listener</em></span> to that element. Huh?</p>
      

      <p class="it">En JavaScript, los acontecimientos están sucediendo todo el tiempo. Acontecimientos no interesantes, como grandes fiestas, pero los acontecimientos realmente insignificantes como un <code class="literal">mouseover</code> y haga clic. La mayoría de las veces, estos acontecimientos insignificantes son ignorados (como en la vida, tal vez). Pero si alguien está escuchando, entonces el evento será oído, y puede pasar a la posteridad, o al menos provocar algún tipo de interacción DOM. (Rough JavaScript paralelo de koan clásico: si se produce un evento, y ningún oyente lo escucha, lo hizo siempre sucede en absoluto?)</p>

      <p class="p" id="in_javascript__id2">In JavaScript, events are happening all the time. Not exciting events, like huge parties, but really insignificant events like <code class="literal">mouseover</code> and <code class="literal">click</code>. Most of the time, these insignificant events go ignored (just as in life, perhaps). But if someone is <span class="emphasis"><em>listening</em></span>, then the event will be <span class="emphasis"><em>heard</em></span>, and can go down in posterity, or at least trigger some sort of DOM interaction. (Rough JavaScript parallel of classic koan: if an event occurs, and no listener hears it, did it ever happen at all?)<a id="id532667" class="indexterm" href=""></a><a id="id532676" class="indexterm" href=""></a></p>
      


      <p class="p" id="an_event_listen">An event <span class="emphasis"><em>listener</em></span> is an anonymous function that <span class="emphasis"><em>listens</em></span> for a<a id="id532698" class="indexterm" href=""></a><a id="id532703" class="indexterm" href=""></a><a id="id532711" class="indexterm" href=""></a> specific event <span class="emphasis"><em>on</em></span> a specific element or elements. D3’s method <code class="literal">selection.on()</code> provides a nice shorthand for adding event listeners. As you can see, <code class="literal">on()</code> takes two arguments: the event <span class="emphasis"><em>type</em></span> (<code class="literal">"click"</code>) and the listener itself (the anonymous function).<a id="id532748" class="indexterm" href=""></a></p>

      


      <p class="it">Un detector de eventos es una función anónima que detecta un evento específico en un elemento o elementos específicos. El método D3 <code class="literal">selection.on()</code> proporciona una agradable forma abreviada de la adición de los detectores de eventos. Como se puede ver, <code class="literal">on()</code> toma dos argumentos: tipo e evento ( <code class="literal">"click"</code>) y el propio oyente (la función anónima). En este caso, el oyente escucha para un evento de <code class="literal">"click"</code> que ocurre en nuestra selección <code class="literal">p</code>. Cuando eso sucede, se ejecuta la función de detector. Usted puede poner lo que desee en el código entr n los soportes de la función anónima:</p>

      <p class="p" id="in_this_case_t_id1">In this case, the listener listens for a <code class="literal">click</code> event occurring on our<a id="id532766" class="indexterm" href=""></a> selection <code class="literal">p</code>. When that happens, the listener function is executed. You can put whatever code you want in between the brackets of the anonymous function:
      </p>

      <pre class="programlisting" data-language="javascript" id="dselectp__id2">d3.select("p")
    .on("click", function() {
        //Do something mundane and annoying on click
        alert("Hey, don't click that!");
    });</pre>

      

      <p class="it">Hablaremos mucho más sobre la interactividad en el capítulo 10.</p>

      <p class="p" id="well_talk_a_lo">We’ll talk a lot more about interactivity in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch10.html" title="Chapter 10. Interactivity">Chapter 10</a>.</p>          <h3 class="title">Changing the Data</h3>      

      <p class="it">   En vez de generar molestos pop-ups, yo prefiero simplemente actualizar el <code class="literal">dataset</code>  al sobrescribir sus valores originales. Este es el paso 1, de antes:</p>

      <p class="p" id="instead_of_gene">Instead of generating annoying pop-ups, I’d rather simply update<a id="id532906" class="indexterm" href=""></a> <code class="literal">dataset</code> by overwriting its original values. This is step 1, from earlier:</p>
      <pre class="programlisting" data-language="javascript" id="dataset___">dataset = [ 11, 12, 15, 20, 18, 17, 16, 18, 23, 25,
            5, 10, 13, 19, 21, 25, 22, 18, 15, 13 ];</pre>

      

      <p class="it">El paso 2 es volver a enlazar los valores a los elementos existentes. Podemos hacer que seleccionando aquellas <code class="literal">rect</code> y simplemente llamando a <code class="literal">data()</code> una vez más:</p>

      <p class="p" id="step__is_to_re">Step 2 is to rebind the new values to the existing elements. We can do that by selecting those <code class="literal">rect</code>s and simply calling <code class="literal">data()</code> one more time:</p>
      <pre class="programlisting" data-language="javascript" id="svgselectall_id7">svg.selectAll("rect")
   .data(dataset);     //New data successfully bound, sir!</pre>          <h3 class="title">Updating the Visuals</h3>  


      <p class="it">Por último, el paso 3 es actualizar los atributos visuales, haciendo referencia a los valores de datos (ahora actualizada). Esto es muy fácil, ya que simplemente copia y pega el código en cuestión que ya has escrito. En este caso, los <code class="literal">rect</code> pueden mantener sus posiciones horizontales y anchuras; todo lo que necesitamos para actualizar son sus <code class="literal">height</code>y posiciones <code class="literal">y</code> he añadido las líneas aquí:</p>

      <p class="p" id="finally_step_">Finally, step 3 is to update the visual attributes, referencing the (now-updated) data values. This is super easy, as we simply copy and paste the relevant code that we’ve already written. In this case, the <code class="literal">rect</code>s can maintain their horizontal positions and widths; all we really need to update are their <code class="literal">height</code>s and <code class="literal">y</code> positions. I’ve added those lines here:</p>
      <pre class="programlisting" data-language="javascript" id="svgselectall_id8">svg.selectAll("rect")
   .data(dataset)
   .attr("y", function(d) {
        return h - yScale(d);
   })
   .attr("height", function(d) {
        return yScale(d);
   });</pre>

      

      <p class="it">Observe esto se ve casi exactamente igual que el código que generan los <code class="literal">rect</code>s inicialmente, sólo que sin <code class="literal">enter()</code> y <code class="literal">append()</code>.</p>

      <p class="p" id="notice_this_loo">Notice this looks almost exactly like the code that generates the <code class="literal">rect</code>s initially, only without <code class="literal">enter()</code> and <code class="literal">append()</code>.</p>
      

      <p class="it">Poniendo todo junto, aquí esta todo nuestro código de actualización en un solo lugar:</p>

      <p class="p" id="putting_it_all__id2">Putting it all together, here is all of our update code in one place:</p>
      <pre class="programlisting" data-language="javascript" id="on_click_upd">//On click, update with new data
d3.select("p")
    .on("click", function() {

        //New values for dataset
        dataset = [ 11, 12, 15, 20, 18, 17, 16, 18, 23, 25,
                    5, 10, 13, 19, 21, 25, 22, 18, 15, 13 ];

        //Update all rects
        svg.selectAll("rect")
           .data(dataset)
           .attr("y", function(d) {
                return h - yScale(d);
           })
           .attr("height", function(d) {
                return yScale(d);
           });

    });</pre>

      

      <p class="it">Echa un vistazo a la gráfica de barras revisada en 03_updates_all_data.html. Se parece a la Figura 9-4 para empezar.</p>

      <p class="p" id="check_out_the_r">Check out the revised bar chart in <span class="emphasis"><em>03_updates_all_data.html</em></span>. It looks like <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch09.html#Updateable_bar_chart" title="Figure 9-4. Updatable bar chart">Figure 9-4</a> to start.</p>

<div>

            <img src="/static/oSwB5mh6Ca-img4.png" alt="Updatable bar chart"/>

<p class="fig">Figura 9-4. Diagrama de barras que se pueden actualizar</p>
<p class="fig">Figure 9-4. Updatable bar chart</p>

</div>

      
<p class="it">A continuación, haga clic en cualquier parte del párrafo, y se convierte en la figura 9-5.</p>

<p class="p" id="then_click_anyw">Then click anywhere on the paragraph, and it turns into <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch09.html#Bar_chart_data_updated" title="Figure 9-5. Bar chart, data updated">Figure 9-5</a>.</p>
      <div>

            <img src="/static/oSwB5mh6Ca-img5.png" alt="Bar chart, data updated"/>
<p class="fig">Figura 9-5. Diagrama de barras, con los datos actualizados</p>

        <p class="fig">Figure 9-5. Bar chart, data updated</p>


      </div>

      

      <p class="it">Buenas noticias: los valores en el conjunto de datos se modificaron, por rebote, y se utilizan para ajustar los <code class="literal">rect</code>s. Las malas noticias: parece raro porque nos olvidamos de actualizar las etiquetas, y también los colores de la barra. Buenas noticias (Porque siempre me gusta terminar con buenas noticias): esto es fácil de solucionar.</p>

      <p class="p" id="good_news_the_">Good news: the values in <code class="literal">dataset</code> were modified, rebound, and used to adjust the <code class="literal">rect</code>s. Bad news: it looks weird because we forgot to update the labels, and also the bar colors. Good news (because I always like to end with good news): this is easy to fix.</p>
      

      <p class="it">Para asegurar que los colores cambian en la actualización, sólo debemos copiar y pegar en la línea donde se parte del relleno:</p>

      <p class="p" id="to_ensure_the_c">To ensure the colors change on update, we just copy and paste in the<a id="id534088" class="indexterm" href=""></a> line where we set the <code class="literal">fill</code>:</p>
      <pre class="programlisting" data-language="javascript" id="svgselectall_id9">svg.selectAll("rect")
   .data(dataset)
   .attr("y", function(d) {
        return h - yScale(d);
   })
   .attr("height", function(d) {
        return yScale(d);
   })
   .attr("fill", function(d) {   // &lt;-- Down here!
        return "rgb(0, 0, " + (d * 10) + ")";
   });</pre>

      

      <p class="it">Para actualizar las etiquetas, se utiliza un patrón similar, sólo que aquí nos ajustamos a su contenido de texto y valores x/y:</p>

      <p class="p" id="to_update_the_l">To update the labels, we use a similar pattern, only here we adjust<a id="id534436" class="indexterm" href=""></a><a id="id534444" class="indexterm" href=""></a> their text content and x/y values:</p>
      <pre class="programlisting" data-language="javascript" id="svgselectall_id10">svg.selectAll("text")
   .data(dataset)
   .text(function(d) {
        return d;
   })
   .attr("x", function(d, i) {
        return xScale(i) + xScale.rangeBand() / 2;
   })
   .attr("y", function(d) {
        return h - yScale(d) + 14;
   });</pre>

      

      <p class="it">Se dará cuenta de que tiene el mismo aspecto para empezar, pero clickee en el gatillo y ahora los colores de las barras y etiquetas se actualizaran correctamente, como se muestra en la Figura 9-6.</p>

      <p class="p" id="take_a_look_at_">Take a look at <span class="emphasis"><em>04_updates_all_data_fixed.html</em></span>. You’ll notice it looks the same to start, but click the trigger and now the bar colors and labels update correctly, as shown in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch09.html#Updated_chart_with_correct_colors_and_labels" title="Figure 9-6. Updated chart with correct colors and labels">Figure 9-6</a>.</p>
      <div>

            <img src="/static/oSwB5mh6Ca-img6.png" alt="Updated chart with correct colors and labels"/>


        <p class="fig">Figure 9-6. Updated chart with correct colors and labels</p>
<p class="fig">Figura 9-6. Gráfico actualizado con colores y etiquetas correctas</p>
      </div>



<p><strong>Ejercicio</strong></p>

<h2 class="title">Transitions</h2>    

    <p class="it">Las transiciones de la vida pueden ser aterradoras: el primer día de clases, mudarse a una nueva ciudad, dejar su trabajo del día para hacer la visualización de datos independiente a tiempo completo. Pero las transiciones con D3 son divertidas, hermosas, y no gravan en absoluto emocionalmente.</p>

    <p class="p" id="life_transition">Life transitions can be scary: the first day of school, moving to a new city, quitting your day job to do freelance data visualization full-time. But D3 transitions are fun, beautiful, and not at all emotionally taxing.<a id="ix_trans" class="indexterm" href=""></a></p>
    

    <p class="it">Hacer una buena transición, súper suave, animada es tan simple como añadir una línea de código:</p>

    <p class="p" id="making_a_nice_">Making a nice, super smooth, animated transition is as simple as adding<a id="id534879" class="indexterm" href=""></a> one line of code:</p>
    <pre class="programlisting" data-language="javascript" id="transition_id1">.transition()</pre>

    

    <p class="it">En concreto, se debe añadir este eslabón de la cadena por debajo de donde se hace la selección, y sobre el que se aplican los cambios de atributos:</p>

    <p class="p" id="specifically_a">Specifically, add this link in the chain below where your selection is made, and <span class="emphasis"><em>above</em></span> where any attribute changes are applied:</p>
    <pre class="programlisting" data-language="javascript" id="update_all_re_id1">//Update all rects
svg.selectAll("rect")
   .data(dataset)
   .transition()    // &lt;-- This is new! Everything else here is unchanged.
   .attr("y", function(d) {
        return h - yScale(d);
   })
   .attr("height", function(d) {
        return yScale(d);
   })
   .attr("fill", function(d) {
        return "rgb(0, 0, " + (d * 10) + ")";
   });</pre>


     <p><strong>Ejercicio</strong></p>
         

         <p class="it">Ahora ejecute el código en 05_transition.html, y haga clic en el texto para ver la transición en acción. Tenga en cuenta que el resultado final tiene el mismo aspecto visual, pero la transición desde el estado inicial de la tabla hasta su estado final es mucho, mucho mejor.</p>

         <p class="p" id="now_run_the_cod">Now run the code in <span class="emphasis"><em>05_transition.html</em></span>, and click the text to see the transition in action. Note that the end result looks the same visually, but the transition from the chart’s initial state to its end state is much, much nicer.</p>
    

    <p class="it">No es loco? No soy un psicólogo, pero creo que es literalmente loco que podamos añadir una sola línea de código, y D3 se animará a realizar nuestros cambios de valor por nosotros en tiempo real.</p>

    <p class="p" id="isnt_that_insa">Isn’t that <span class="emphasis"><em>insane</em></span>? I’m not a psychologist, but I believe it is literally insane that we can add a single line of code, and D3 will <span class="emphasis"><em>animate</em></span> our value changes for us over time.<a id="id535314" class="indexterm" href=""></a><a id="id535319" class="indexterm" href=""></a></p>
    

    <p class="it">Sin <code class="literal">transition()</code>, D3 evalúa cada estado <code class="literal">attr()</code> de inmediato, por lo que los cambios en la altura y el terraplén ocurre de inmediato. Cuando se agrega <code class="literal">transition()</code>, D3 introduce el elemento tiempo. En lugar de aplicar los nuevos valores a la vez, D3 interpola entre los valores antiguos y los nuevos valores, lo que significa que se normalizan Los valores iniciales y finales, y calcula todos sus estados en el medio. D3 también es lo suficientemente inteligente como para reconocer e interpolar entre diferentes formatos de valores de atributos. Por ejemplo, si ha especificado una altura de 200 píxeles para empezar, pero la transición a poco 100 (sin la px). O si un relleno azul se convierte RGB (0,255,0). Usted no tiene necesidad de preocuparse por ser coherente; D3 se encarga de ello.</p>

    <p class="p" id="without_transit">Without <code class="literal">transition()</code>, D3 evaluates every <code class="literal">attr()</code> statement immediately, so the changes in height and fill happen right away. When you add <code class="literal">transition()</code>, D3 introduces the element of time. Rather than applying new values all at once, D3 <span class="emphasis"><em>interpolates</em></span> between the old values and the new values, meaning it normalizes the beginning and ending values, and calculates all their in-between states. D3 is also smart enough to recognize and interpolate between different attribute value formats. For example, if you specified a height of <code class="literal">200px</code> to start but transition to just <code class="literal">100</code> (without the <code class="literal">px</code>). Or if a <code class="literal">blue</code> fill turns <code class="literal">rgb(0,255,0)</code>. You don’t need to fret about being consistent; D3 takes care of it.</p>
    

    <p class="it">¿No me crees todavía? Esto es realmente una locura. Y super útil.</p>

    <p class="p" id="do_you_believe_">Do you believe me yet? This is really insane. And super helpful.</p>


          <h3 class="title">duration(), or How Long Is This Going to Take?</h3>
          <h3 class="title">duration(), o Cuánto Tiempo ¿Esto Va a Tomar?</h3>        


      

      <p class="it">Por lo que los valores <code class="literal">attr()</code> son interpolados con el tiempo, pero ¿cuánto tiempo? Resulta que el valor predeterminado es 250 milisegundos, o una cuarta parte de segundo (1.000 milisegundos = 1 segundo). Es por eso que la transición en 05_transition.html es tan rápida.</p>

      <p class="p" id="so_the_attr_v">So the <code class="literal">attr()</code> values are interpolated over time, but how <span class="emphasis"><em>much</em></span> time? It turns out the default is 250 milliseconds, or one-quarter second (1,000 milliseconds = 1 second). That’s why the transition in <span class="emphasis"><em>05_transition.html</em></span> is so fast.<a id="id535425" class="indexterm" href=""></a></p>
      

      <p class="it">Afortunadamente, se puede controlar cuanto tiempo se gasta en cualquier transición - de nuevo, no es broma - con la adición de una sola línea de código:</p>

      <p class="p" id="fortunately_yo_id3">Fortunately, you can control how much time is spent on any transition by—again, I kid you not—adding a single line of code:</p>
      <pre class="programlisting" data-language="javascript" id="duration">.duration(1000)</pre>

      

      <p class="it">La <code class="literal">duration()</code> debe especificarse después de la <code class="literal">transition()</code>, la duración siempre se especifica en milisegundos, por lo que la duración (1000) es un segundo de duración sucesivamente.</p>

      <p class="p" id="the_duration_">The <code class="literal">duration()</code> must be specified <span class="emphasis"><em>after</em></span> the <code class="literal">transition()</code>, and durations are always specified in milliseconds, so <code class="literal">duration(1000)</code> is a one-second duration.</p>
      

      <p class="it">Aquí está esa línea en su contexto:</p>

      <p class="p" id="here_is_that_li">Here is that line in context:</p>
      <pre class="programlisting" data-language="javascript" id="update_all_re_id2">//Update all rects
svg.selectAll("rect")
   .data(dataset)
   .transition()
   .duration(1000)  // &lt;-- Now this is new!
   .attr("y", function(d) {
        return h - yScale(d);
   })
   .attr("height", function(d) {
        return yScale(d);
   })
   .attr("fill", function(d) {
        return "rgb(0, 0, " + (d * 10) + ")";
   });</pre>

      

      <p class="it">Abra 06_duration.html y mire la diferencia. Ahora haga una copia de ese archivo, y trate de conectar algunos números diferentes para ralentizar o acelerar la transición. Por ejemplo, trate de 0 a 300 para una transición de tres segundos, o 100 para una décima de segundo.</p>

      <p class="p" id="open_up__dura">Open up <span class="emphasis"><em>06_duration.html</em></span> and see the difference. Now make a copy of that file, and try plugging in some different numbers to slow or speed the transition. For example, try <code class="literal">3000</code> for a three-second transition, or <code class="literal">100</code> for one-tenth of a second.</p>
      

      <p class="it"> Las duraciones reales que elija dependerá del contexto de su diseño y lo que provoca la transición. En la práctica, me parece que las transiciones de alrededor de 150 ms son útiles para proporcionar retroalimentación interfaz menor (tal como se cierne sobre los elementos), y cerca de 1.000 ms es ideal para muchas transiciones visuales significativas más, como por ejemplo cambiar de una vista de los datos a otro 1,000 ms (un segundo) no es demasiado largo, ni demasiado corto.</p>

      <p class="p" id="the_actual_dura">The actual durations you choose will depend on the context of your design and what triggers the transition. In practice, I find that transitions of around 150 ms are useful for providing minor interface feedback (such as hovering over elements), and about 1,000 ms is ideal for many more significant visual transitions, such as switching from one view of the data to another. 1,000 ms (one second) is not too long, not too short.</p>
      

      <p class="it"> En caso de que usted este sintiendose perezoso, hice el archivo 07_duration_slow.html, que utiliza 5000 para una transición de cinco segundos.</p>

      <p class="p" id="in_case_youre__id2">In case you’re feeling lazy, I made <span class="emphasis"><em>07_duration_slow.html</em></span>, which uses <code class="literal">5000</code> for a five-second transition.</p>

      

      <p class="it">Con tal lenta transición, se hace evidente que las etiquetas de valor no están haciendo la transición sin problemas junto con las alturas de las barras. Como usted sabe, podemos corregir ese descuido mediante la adición de sólo dos nuevas líneas de código, esta vez en la sección en la que actualizamos las etiquetas:</p>

      <p class="p" id="with_such_a_slo">With such a slow transition, it becomes obvious that the value labels are not transitioning smoothly along with the bar heights. As you now know, we can correct that oversight by adding only two new lines of code, this time in the section where we update the labels:</p>
      <pre class="programlisting" data-language="javascript" id="update_all_la">//Update all labels
svg.selectAll("text")
   .data(dataset)
   .transition()        // &lt;-- This is new,
   .duration(5000)      //     and so is this.
   .text(function(d) {
        return d;
   })
   .attr("x", function(d, i) {
        return xScale(i) + xScale.rangeBand() / 2;
   })
   .attr("y", function(d) {
        return h - yScale(d) + 14;
   });</pre>

      

      <p class="it">¡Mucho mejor! Nótese en el archivo 08_duration_slow_labels_fixed.html cómo las etiquetas ahora animan suavemente a lo largo de las barras.</p>

      <p class="p" id="much_better_no">Much better! Note in <span class="emphasis"><em>08_duration_slow_labels_fixed.html</em></span> how the labels now animate smoothly along with the bars.</p>
       

       <p><strong>Ejercicio</strong></p>          <h3 class="title">ease()-y Does It</h3>

 

      

      <p class="it">Con unos 5.000 ms, la transición es lenta como melaza, también podemos percibir la calidad de movimiento. En este caso, observe como comienza la animación muy lentamente, luego se acelera, entonces se ralentiza de nuevo como la altura de las barras de destino. Es decir, la velocidad de movimiento no es lineal, sino variable</p>

      <p class="p" id="with_a_ms">With a 5,000-ms, slow-as-molasses transition, we can also perceive the <span class="emphasis"><em>quality</em></span> of motion. In this case, notice how the animation begins very slowly, then accelerates, then slows down again as the bars reach their destination heights. That is, the rate of motion is not <span class="emphasis"><em>linear</em></span>, but <span class="emphasis"><em>variable</em></span>.<a id="id536370" class="indexterm" href=""></a><a id="id536378" class="indexterm" href=""></a></p>
      

      <p class="it">   La calidad de movimiento que se utiliza para una transición se llama <strong>easing</strong>. En términos de animación, pensamos en elementos de <strong>easing</strong> en su lugar, moviéndose de aquí para allá.</p>

      <p class="p" id="the_quality_of_">The quality of motion used for a transition is called <span class="emphasis"><em>easing</em></span>. In animation terms, we think about elements <span class="emphasis"><em>easing</em></span> into place, moving from here to there.</p>
      

      <p class="it">Con D3, se pueden especificar diferentes tipos de <strong>easing</strong> mediante el uso de <code class="literal">ease()</code>. La flexibilización por defecto es "cúbico-in-out", que produce la aceleración y desaceleración gradual que vemos en nuestra tabla. Es una buena forma predeterminada, ya que por lo general no puede ir mal con una buena transición, suave.</p>

      <p class="p" id="with_d_you_ca">With D3, you can specify different kinds of easing by using <code class="literal">ease()</code>. The default easing is <code class="literal">"cubic-in-out"</code>, which produces the gradual acceleration and deceleration we see in our chart. It’s a good default because you generally can’t go wrong with a nice, smooth transition.</p>
      

      <p class="it">Esto contrasta con la suavidad 09_ease_linear.html, que utiliza ease("linear") para especificar una función de aceleración lineal. Observe cómo la tasa de movimiento es constante. Es decir, no hay aceleración y deceleración gradual - los elementos simplemente comienzan a moverse a un ritmo constante, y luego se detienen bruscamente. (También, bajé la duración de 2,000 ms.)</p>

      <p class="p" id="contrast_that_s">Contrast that smoothness to <span class="emphasis"><em>09_ease_linear.html</em></span>, which uses <code class="literal">ease("linear")</code> to specify a linear easing function. Notice how the rate of motion is constant. That is, there is no gradual acceleration and deceleration—the elements simply begin moving at an even pace, and then they stop abruptly. (Also, I lowered the duration to 2,000 ms.)</p>
      

      <p class="it"><code class="literal">ease()</code>también debe especificarse después de la <code class="literal">transition()</code>, pero antes de la <code class="literal">attr()</code> declaraciones a las que se aplica la transición. <code class="literal">attr()</code> puede aparecer antes o después de la <code class="literal">duration()</code>, pero esta secuencia es la que tiene más sentido para mí:</p>

      <p class="p" id="ease_must_als"><code class="literal">ease()</code> must also be specified after <code class="literal">transition()</code>, but before the <code class="literal">attr()</code> statements to which the transition applies. <code class="literal">ease()</code> can come before or after <code class="literal">duration()</code>, but this sequence makes the most sense to me:</p>
      <pre class="programlisting" data-language="javascript" id="selection_s">…   //Selection statement(s)
.transition()
.duration(2000)
.ease("linear")
…   //attr() statements</pre>

<p class="it">Afortunadamente, hay varios otros elementos de construcción en funciones de aceleración para elegir. Algunos de mis favoritos son:</p>

      <p class="p" id="fortunately_th_id1">Fortunately, there are several other built-in easing functions to choose from. Some of my favorites are:</p>
      <div>

        <dl class="variablelist">

          <dt><span class="term"> <code class="literal">circle</code> </span></dt>

          <dd> Gradual ease in and acceleration until elements snap into place. </dd>
          <dd> Gradual desaceleración y aceleración hasta que los elementos encajan en su lugar.  </dd>
          <dt><span class="term"> <code class="literal">elastic</code> </span></dt>

          <dd> The best way to describe this one is “sproingy.” </dd>
          <dd> La mejor manera de describir esta es "sproingy."  </dd>
          <dt><span class="term"> <code class="literal">bounce</code> </span></dt>

          <dd> Like a ball bouncing, then coming to rest. </dd>
          <dd> Al igual que una pelota que rebota, hasta llegar al descanso. </dd>
        </dl>

      </div>

      

      <p class="it">Archivos de código de muestra 10_ease_circle.html, 11_ease_elastic.html, y 12_ease_bo unce.html ilustran estas tres funciones. La lista completa de las funciones de aceleración está en la wiki D3.</p>

      <p class="p" id="sample_code_fil">Sample code files <span class="emphasis"><em>10_ease_circle.html</em></span>, <span class="emphasis"><em>11_ease_elastic.html</em></span>, and <span class="emphasis"><em>12_ease_bounce.html</em></span> illustrate these three functions. The complete list of easing functions is on <a class="ulink" href="https://github.com/mbostock/d3/wiki/Transitions#wiki-d3_ease" target="_top">the D3 wiki</a>.</p>
 
      

 <p><strong>Ejercicio</strong></p>
      

      <p class="it">Vaya, ya me arrepiento de lo que le dije acerca del rebote. Por favor, use rebote sólo si usted está haciendo una infografía satírica que se burla de otros malos graficos. Perceptualmente, no pienso que haya un caso real que se utilizará para la flexibilización de rebote en la visualización.  Por una razón cubic-in-out es el valor predeterminado.</p>

      <p class="p" id="wow_i_already_">Wow, I already regret telling you about <code class="literal">bounce</code>. Please use <code class="literal">bounce</code> only if you are making a satirical infographic that is mocking other bad graphics. Perceptually, I don’t think there is a real case to be used for <code class="literal">bounce</code> easing in visualization. <code class="literal">cubic-in-out</code> is the default for a reason.</p>
   

  

          <h3 class="title">Please Do Not delay()</h3>
          <h3 class="title">Por favor, que no sea delay()</h3>

      

      <p class="it">Mientras que la <code class="literal">ease()</code> controla la calidad de movimiento, <code class="literal">delay()</code> especifica cuándo empieza la transición. </p>

      <p class="p" id="whereas_ease_">Whereas <code class="literal">ease()</code> controls the quality of motion, <code class="literal">delay()</code> specifies when the transition begins.<a id="id536724" class="indexterm" href=""></a></p>

      

      <p class="it">A <code class="literal">delay()</code> se le puede dar un valor estático, también en milisegundos, como en:</p>

      <p class="p" id="delay_can_be_"><code class="literal">delay()</code> can be given a static value, also in milliseconds, as in:</p>
      <pre class="programlisting" data-language="javascript" id="transition_id2">…
.transition()
.delay(1000)     //1,000 ms or 1 second
.duration(2000)  //2,000 ms or 2 seconds
…</pre>

      

      <p class="it">Al igual que con la <code class="literal">duration()</code> y la <code class="literal">ease()</code>, el orden aquí es algo flexible, pero me gusta incluir <code class="literal">delay()</code> antes de <code class="literal">duration()</code>. Eso tiene más sentido para mí porque la demora ocurrira primero, seguida de la propia transición.</p>

      <p class="p" id="as_with_duratio">As with <code class="literal">duration()</code> and <code class="literal">ease()</code>, the order here is somewhat flexible, but I like to include <code class="literal">delay()</code> before <code class="literal">duration()</code>. That makes more sense to me because the delay happens first, followed by the transition itself.</p>
      

      <p class="it">Ver 13_delay_static.html, en el que haciendo clic en el texto activa primero un retardo de 1,000 ms (en el que no pasa nada), seguido por una transición de 2000-ms.</p>

      <p class="p" id="see__delay_st">See <span class="emphasis"><em>13_delay_static.html</em></span>, in which clicking the text triggers first a 1,000-ms delay (in which nothing happens), followed by a 2,000-ms transition.</p>
      

      <p class="it">Los retrasos estáticos pueden ser útiles, pero más emocionante son los valores de retardo que se calculan dinámicamente. Un uso común de esto es para generar retardos escalonados, por lo que algún elemento de transición antes que otros. Los retrasos escalonados pueden ayudar con la percepción, ya que <strong>es más fácil para nuestros ojos seguir un elemento individual de movimiento cuando se está un poco fuera de sincronía con el movimiento de sus elementos vecinos.</strong></p>

      <p class="p" id="static_delays_c">Static delays can be useful, but more exciting are delay values that we calculate dynamically. A common use of this is to generate staggered delays, so some elements transition before others. Staggered delays can assist with perception, as it’s easier for our eyes to follow an individual element’s motion when it is slightly out of sync with its neighboring elements’ motion.<a id="id536886" class="indexterm" href=""></a><a id="id536891" class="indexterm" href=""></a></p>
      

      <p class="it">Para ello, en lugar de dar <code class="literal">delay()</code> como valor estatico, le damos una función, a la manera típica de D3:</p>

      <p class="p" id="to_do_this_ins">To do this, instead of giving <code class="literal">delay()</code> a static value, we give it a function, in typical D3 fashion:</p>
      <pre class="programlisting" data-language="javascript" id="transition_id3">…
.transition()
.delay(function(d, i) {
    return i * 100;
})
.duration(500)
…</pre>

      

      <p class="it"></p>

      <p class="p" id="just_as_weve_s">Just as we’ve seen with other D3 methods, when given an anonymous function, the datum bound to the current element is passed into <code class="literal">d</code>, and the index position of that element is passed into <code class="literal">i</code>. So, in this case, as D3 loops through each element, the delay for each element is set to <code class="literal">i * 100</code>, meaning each subsequent element will be delayed 100 ms <span class="emphasis"><em>more</em></span> than the preceding element.</p>


      <p class="it">Así como hemos visto con otros métodos D3, cuando se le da una función anónima, el dato unido al elemento actual se hace pasar a <code class="literal">d</code>, y la posición de índice de ese elemento se hace pasar a <code class="literal">i</code>. Por lo tanto, en este caso, como los loops de D3 a través de cada elemento, el retardo de cada elemento está ajustado en i * 100, es decir, cada elemento posterior se retrasará 100 ms más que el anterior elemento. Todo esto quiere decir que ahora tenemos transiciones escalonadas. Echa un vistazo a los bars muy animados en 14_delay_dynamic.html y vealo por usted mismo.</p>

      <p class="p" id="all_this_is_to__id2">All this is to say that we now have staggered transitions. Check out the beautifully animated bars in <span class="emphasis"><em>14_delay_dynamic.html</em></span> and see for yourself.</p>

      

      <p class="it"> Tenga en cuenta que también disminuyó la duración de 500 ms para que se sienta un poco más ágil. También tenga en cuenta que <code class="literal">duration()</code>  establece la duración de cada transición individual, no para todas las transiciones en su conjunto. Así, por ejemplo, si hay 20 elementos tienen transiciones de 500 ms aplicadas sin retraso, entonces todo habrá terminado en 500 ms, o medio segundo. Pero si un retardo de 100 ms se aplica a cada elemento posterior (i * 100), entonces el tiempo total de ejecución de todas las transiciones será 2.400 m:</p>

      <p class="p" id="note_that_i_als">Note that I also decreased the duration to 500 ms to make it feel a bit snappier. Also note that <code class="literal">duration()</code> sets the duration for each <span class="emphasis"><em>individual transition</em></span>, not for all transitions in aggregate. So, for example, if 20 elements have 500-ms transitions applied with no delay, then it will all be over in 500 ms, or one-half second. But if a 100-ms delay is applied to each subsequent element (<code class="literal">i * 100</code>), then the total running time of all transitions will be 2,400 ms:</p>
      <pre class="screen" id="max_value_of_i_">Max value of i times 100ms delay plus 500ms duration =
19 * 100 + 500 =
2400</pre>

      

      <p class="it">Debido a que estos retrasos se calculan en función de cada elemento, si se han añadido más datos, entonces el tiempo total de ejecución de todas las transiciones se incrementará. Esto es algo a tener en cuenta si tiene un conjunto de datos dinámicamente cargado con una longitud variable de array. Si de repente se ha cargado 10.000 puntos de datos en lugar de 20, usted pasara mucho tiempo viendo esas barras moverse (1,000,400 ms o de 16,67 minutos para ser exactos). De repente, no son tan lindos (nunca mas).</p>

      <p class="p" id="because_these_d">Because these delays are being calculated on a per-element basis, if you added more data, then the total running time of all transitions will increase. This is something to keep in mind if you have a dynamically loaded dataset with a variable array length. If you suddenly loaded 10,000 data points instead of 20, you could spend a long time watching those bars wiggle around (1,000,400 ms or 16.67 minutes to be precise). Suddenly, they’re not so cute anymore.</p>
      

      <p class="it">Afortunadamente, podemos escalar  nuestros valores de retardo dinámicamente a la longitud del conjunto de datos. Esto no es fantasía de D3; es solo matemáticas.</p>

      <p class="p" id="fortunately_we_id3">Fortunately, we can <span class="emphasis"><em>scale</em></span> our delay values dynamically to the length of the dataset. This isn’t fancy D3 stuff; it’s just math.</p>
      

      <p class="it">Ver 15_delay_dynamic_scaled.html, en el que 30 valores se incluyen en el conjunto de datos. Si se levanta de su cronómetro, verá que el tiempo total de transición es de 1,5 segundos, o alrededor de 1.500 ms.</p>

      <p class="p" id="see__delay_dy">See <span class="emphasis"><em>15_delay_dynamic_scaled.html</em></span>, in which 30 values are included in the dataset. If you get out your stopwatch, you’ll see that the total transition time is 1.5 seconds, or around 1,500 ms.</p>
      

      <p class="it">Ahora mire 16_delay_dynamic_scaled_fewer.html, que utiliza exactamente el mismo código de transición, pero con sólo 10 puntos de datos. Observe cómo los retrasos son ligeramente más largos (bueno, un 200 por ciento más), por lo que el tiempo total de transición es el mismo: 1,5 segundos! ¿Cómo es esto posible?</p>

      <p class="p" id="now_see__dela">Now see <span class="emphasis"><em>16_delay_dynamic_scaled_fewer.html</em></span>, which uses exactly the same transition code, but with only 10 data points. Notice how the delays are slightly longer (well, 200 percent longer), so the total transition time is the same: 1.5 seconds! How is this possible?</p>
      

       <p><strong>Ejercicio</strong></p>

   

      

      

      <pre class="programlisting" data-language="javascript" id="transition_id4">…
.transition()
.delay(function(d, i) {
    return i / dataset.length * 1000;   // &lt;-- Where the magic happens
})
.duration(500)
…</pre>

      

      <p class="it">Las dos páginas de ejemplo anterior utilizan los mismos cálculos de retardo aquí. En lugar de multiplicar <strong>i</strong> por una cierta cantidad estática, primero dividimos <strong>i</strong> por <code class="literal">dataset.length</code>, en efecto normaliza el valor. Entonces, ese valor normalizado se multiplica por 1.000, o 1 segundo. El resultado es que la cantidad máxima de retardo para el último elemento será 1000, y para todos los elementos anteriores se retrasó por una cierta cantidad menor que eso. Un retraso máximo de 1000 más una duración de 500 es igual a 1,5 segundos de tiempo total de transición.</p>

      <p class="p" id="the_two_precedi">The two preceding sample pages use the same delay calculations here. Instead of multiplying <code class="literal">i</code> by some static amount, we first divide <code class="literal">i</code> by <code class="literal">dataset.length</code>, in effect normalizing the value. Then, that normalized value is multiplied by <code class="literal">1000</code>, or 1 second. The result is that the maximum amount of delay for the last element will be <code class="literal">1000</code>, and all prior elements will be delayed by some amount less than that. A max delay of <code class="literal">1000</code> plus a duration of <code class="literal">500</code> equals 1.5 seconds total transition time.</p>
      

      <p class="it">Este enfoque a los retrasos es grande, ya que mantiene nuestro código escalable. La duración total será tolerable si tenemos 10 puntos de datos solamente o 10.000.</p>

      <p class="p" id="this_approach_t">This approach to delays is great because it keeps our code <span class="emphasis"><em>scalable</em></span>. The total duration will be tolerable whether we have only 10 data points or 10,000.</p>


          <h3 class="title">Randomizing the Data</h3>
          <h3 class="title">La aleatorización de los Datos</h3>


<p class="it">Sólo para ilustrar cómo enfriar esto es, vamos a cambiar la finalidad de nuestro código de generación de números aleatorios en el capítulo 5 aquí, para que podamos actualizar la tabla tantas veces como queramos, con nuevos datos cada vez.</p>

<p class="p" id="just_to_illustr">Just to illustrate how cool this is, let’s repurpose our random number generating code from <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch05.html" title="Chapter 5. Data">Chapter 5</a> here, so we can update the chart as many times as we want, with new data each time.<a id="id537421" class="indexterm" href=""></a></p>

<p class="it">Abajo, en nuestra función de clic-actualización, vamos a reemplazar el conjunto de datos estático por uno generado aleatoriamente:</p>

 <p class="p" id="down_in_our_cli">Down in our click-update function, let’s replace the static <code class="literal">dataset</code> with a randomly generated one:</p>

      <pre class="programlisting" data-language="javascript" id="new_values_fo">//New values for dataset
var numValues = dataset.length;               //Count original length of dataset
dataset = [];                                       //Initialize empty array
for (var i = 0; i &lt; numValues; i++) {               //Loop numValues times
    var newNumber = Math.floor(Math.random() * 25); //New random integer (0-24)
    dataset.push(newNumber);                        //Add new number to array
}</pre>

      



<p class="it">Este conjunto de datos se sobrescribe con una serie de números enteros aleatorios con valores entre 0 y 24. La nueva array será de la misma longitud que una array original.</p>

<p class="p" id="this_will_overw">This will overwrite <code class="literal">dataset</code> with an array of random integers with values between 0 and 24. The new array will be the same length as the original array.</p>


<p class="it">A continuación, voy a actualizar el texto del párrafo:</p>

 <p class="p" id="then_ill_upda">Then, I’ll update the paragraph text:</p>

<pre class="programlisting" data-language="html" id="pclick_on_thi_id2">&lt;p&gt;Click on this text to update the chart with new data values as many times as you like!&lt;/p&gt;</pre>

      


<p class="it"> Haga clic en este texto para actualizar el gráfico con los nuevos valores de los datos tantas veces como desee!. Ahora abra 17_randomized_data.html, y debería ver algo parecido a la Figura 9-7.</p>


      <p class="p" id="now_open_up__">Now open up <span class="emphasis"><em>17_randomized_data.html</em></span>, and you should see something like <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch09.html#Initial_view" title="Figure 9-7. Initial view">Figure 9-7</a>.</p>

      <div>

            <img src="/static/oSwB5mh6Ca-img7.png" alt="Initial view"/>


<p class="fig">Figure  9-7 Vista inicial</p>

<p class="fig">Figure 9-7. Initial view</p>

</div>

    
<p class="it">Cada vez que se hace clic en el párrafo en la parte superior, el código hará lo siguiente:</p>

      <p class="p" id="every_time_you_">Every time you click the paragraph at top, the code will do the following:</p>





      <div class="orderedlist" id="generate_new_r_id1">

        <ol class="orderedlist" type="1">

          
<li class="li"> Crea nuevos valores aleatorios. </li>
          <li class="p"> Generate new, random values. </li>
          


           <li class="li"> Obliga esos valores a acomodarse a los elementos existentes. </li>

          <li class="p"> Bind those values to the existing elements. </li>
         


          <li class="li">  Los elementos en transición a las nuevas posiciones, alturas y colores, utilizando los nuevos valores (ver Figura 9-8). </li>

          <li class="p"> Transition elements to new positions, heights, and colors, using the new values (see <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch09.html#Random_data_applied" title="Figure 9-8. Random data applied">Figure 9-8</a>). </li>
          


        </ol>

      </div>

      <div>

            <img src="/static/oSwB5mh6Ca-img8.png" alt="Random data applied"/>




<p class="fig">Figura 9-8. Datos aleatorios aplicados</p>
<p class="fig">Figure 9-8. Random data applied</p>




      </div>
       <p><strong>Ejercicio</strong></p>

      


<p class="it">¡Muy genial! Si esto no se siente muy bien, o incluso un poco bien para usted, por favor apague la computadora y vaya a dar un paseo para aclarar su cabeza, haciendo así espacio para toda la tranquilidad por venir. Sin embargo, si usted está suficientemente bien con este conocimiento, sigua leyendo.</p>


<p class="p" id="pretty_cool_if">Pretty cool! If this does not feel pretty cool or even a little cool to you, please turn off your computer and go for a short walk to clear your head, thereby making room for all the coolness to come. If, however, you are sufficiently cooled by this knowledge, read on.</p>

<h3 class="title">La actualización de las escalas</h3>

<h3 class="title">Updating Scales</h3>



<p class="it">Los lectores astutos pueden discrepar con esta línea de antes:</p>

<p class="p" id="astute_readers_">Astute readers might take issue with this line from <a id="id537882" class="indexterm" href=""></a>earlier:</p>

<pre class="programlisting" data-language="javascript" id="var_newnumber__id3">var newNumber = Math.floor(Math.random() * 25);</pre>

<p class="it"> ¿Por qué 25? En la programación, esto se dice como un número mágico. Lo sé, suena divertido, pero el problema con números mágicos es que es difícil decir por qué existen (por lo tanto, la "magia"). En lugar de 25, algo como<code class="literal">maxValue</code>  sería más significativo:</p>

<p class="p" id="why__in_prog">Why 25? In programming, this is referred to as a <span class="emphasis"><em>magic number</em></span>. I<a id="id537975" class="indexterm" href=""></a><a id="id537980" class="indexterm" href=""></a> know, it sounds fun, but the problem with magic numbers is that it’s difficult to tell why they exist (hence, the “magic”). Instead of <code class="literal">25</code>, something like <code class="literal">maxValue</code> would be more meaningful:</p>

<pre class="programlisting" data-language="javascript" id="var_newnumber__id4">var newNumber = Math.floor(Math.random() * maxValue);</pre>

<p class="it">Ah, ver, ahora la magia se ha ido, y yo puedo recordar que el 25 estaba actuando como el valor máximo que se podía calcular y poner en NewNumber. Como regla general, es mejor evitar los números mágicos, y en lugar de ello almacenar esos números dentro de las variables con nombres significativos, como <code class="literal">maxValue</code> o <code class="literal">numberOfTimesWatchedTheMovieTopSecret</code>.</p>


<p class="p" id="ah_see_now_th">Ah, see, now the magic is gone, and I can remember that <code class="literal">25</code> was acting as the <span class="emphasis"><em>maximum value</em></span> that could be calculated and put into <code class="literal">newNumber</code>. As a general rule, it’s best to avoid magic numbers, and instead store those numbers inside variables with meaningful names, like <code class="literal">maxValue</code> or <code class="literal">numberOfTimesWatchedTheMovieTopSecret</code>.</p>

<p class="it"> Más importante, ahora recuerdo que me eligí arbitrariamente 25 porque los valores más grandes exceden el rango de escala de nuestro chart, por lo que las barras se cortaron. Por ejemplo, en la Figura 9-9, He sustituido 25 con 50.</p>


 <p class="p" id="more_important_id1">More important, I now remember that I arbitrarily chose <code class="literal">25</code> because values larger than that exceeded the range of our chart’s scale, so those bars were cut off. For example, in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch09.html#Tootallwrongnumber" title="Figure 9-9. Too tall! We used the wrong magic number!">Figure 9-9</a>, I replaced <code class="literal">25</code> with <code class="literal">50</code>.</p>
  
<div>

            <img src="/static/oSwB5mh6Ca-img9.png" alt="Too tall! We used the wrong magic number!"/>


<p class="fig">Figura 9-9. Demasiado alto! Se utilizó el número mágico mal!</p>

<p class="fig">Figure 9-9. Too tall! We used the wrong magic number!</p>
        

 </div> 

 <p class="it">El problema real no es que he elegido el número mágico equivocado; Es que nuestra escala necesita ser actualizada cada vez que se actualiza el conjunto de datos. Cada vez que nos conectamos con nuevos valores de datos, también hay que recalibrar nuestra escala para asegurar que las barras ¡No se pongan demasiado altas o demasiado bajas.</p>

<p class="p" id="the_real_proble">The real problem is not that I chose the <span class="emphasis"><em>wrong</em></span> magic number; it’s that our <span class="emphasis"><em>scale</em></span> needs to be updated whenever the dataset is updated. Whenever we plug in new data values, we should also recalibrate our scale to ensure that bars don’t get too tall or too short.</p>

<p class="it">La actualización de una escala es fácil. Usted recordará que creamos <code class="literal">yScale</code> con este código:</p>

<p class="p" id="updating_a_scal">Updating a scale is easy. You’ll recall we created <code class="literal">yScale</code> with this code:</p>

<pre class="programlisting" data-language="javascript" id="var_yscale__d_id2">var yScale = d3.scale.linear()
                .domain([0, d3.max(dataset)])
                .range([0, h]);</pre>

<p class="it">El rango puede permanecer igual (como el tamaño visual de nuestra tabla no cambio), pero después de que el nuevo conjunto de datos se ha generado, se debe actualizar la escala del dominio</p>

 <p class="p" id="the_range_can_s">The <span class="emphasis"><em>range</em></span> can stay the same (as the visual size of our chart isn’t changing), but after the new dataset has been generated, we should update the scale’s <span class="emphasis"><em>domain</em></span>:</p>

<pre class="programlisting" data-language="javascript" id="update_scale_">//Update scale domain
yScale.domain([0, d3.max(dataset)]);</pre>

<p class="it">Esto fija el extremo superior del dominio de entrada al valor de datos más grande en el <code class="literal">dataset</code>.. Más tarde, cuando actualizamos todas las barras y etiquetas, que ya referenciar <code class="literal">yScale</code>. para calcular sus posiciones, por lo que no  son necesarios otros cambios en el código.</p>

 <p class="p" id="this_sets_the_u">This sets the upper end of the input domain to the largest data value in <code class="literal">dataset</code>. Later, when we update all the bars and labels, we already reference <code class="literal">yScale</code> to calculate their positions, so no other code changes are necessary.</p>


<p class="it">Comproba esto en 18_dynamic_scale.html. Seguí adelante y sustitui nuestro número mágico 25 con <code class="literal">maxValue</code> que yo pongo aquí a 100. Así que ahora cuando se hace clic para actualizar, obtenemos un número aleatorio entre 0 y 100. Si el valor máximo en el conjunto de datos es 100, entonces la <code class="literal">yScale</code> del dominio va a subir a 100, como vemos en la figura 9-10</p>


<p class="p" id="check_it_out_in_id1">Check it out in <span class="emphasis"><em>18_dynamic_scale.html</em></span>. I went ahead and replaced our magic number <code class="literal">25</code> with <code class="literal">maxValue</code>, which I set here to <code class="literal">100</code>. So now when we click to update, we get random numbers between 0 and 100. If the <span class="emphasis"><em>maximum</em></span> value in the dataset is 100, then <code class="literal">yScale</code>’s domain will go up to 100, as we see in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch09.html#Randomdatabuttheyaxisscaleautomaticallyaccommodates" title="Figure 9-10. Random data, but the y-axis scale automatically accommodates">Figure 9-10</a>.</p>

<div>

            <img src="/static/oSwB5mh6Ca-img10.png" alt="Random data, but the y-axis scale automatically accommodates"/>

<p class="fig">Figura 9-10. Datos aleatorios, pero la escala del eje <strong>y</strong> se acomoda automáticamente</p>        

<p class="fig">Figure 9-10. Random data, but the y-axis scale automatically accommodates</p>


      </div>

      
<p class="it">Pero debido a que los números son aleatorios, no pudieron siempre llegar a ese valor máximo de 100. En la figura 9-11, alcanzan un máximo de 85.</p>

<p class="p" id="but_because_the">But because the numbers are random, they won’t always reach that maximum value of 100. In <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch09.html#Aslightlydifferentscaleduetoslightlydifferentdata" title="Figure 9-11. A slightly different scale, due to slightly different data">Figure 9-11</a>, they top out at 85.</p>

<div>

 <img alt="Imagen" src="/static/Fig911.png"/>


<p class="fig">Figura 9-11. Escala ligeramente diferente, debido a datos ligeramente diferentes</p>

<p class="fig">Figure 9-11. A slightly different scale, due to slightly different data</p>


      </div>

<p class="it">Tenga en cuenta que la altura de la barra 100 en la primera tabla es la misma que la altura de la barra 85 aquí. Los datos está cambiando; el dominio de entrada escala está cambiando; el alcance visual en la salida no cambia.</p>


<p class="p" id="note_that_the_h">Note that the height of the 100 bar in the first chart is <span class="emphasis"><em>the same</em></span> as the height of the 85 bar here. The data is changing; the scale input domain is changing; the output visual range does <span class="emphasis"><em>not</em></span> change.</p>
      





          <h3 class="title">Updating Axes</h3>
          <h3 class="title">Actualización de los ejes</h3>
 
<p class="it">El gráfico de barras no tiene ningún eje, pero nuestro diagrama de dispersión del último capítulo hace (Figura 9-12). Lo he traído de nuevo, con algunos retoques, en 19_axes_static.html.</p>

<p class="p" id="the_bar_chart_d">The bar chart doesn’t have any axes, but our scatterplot from the last<a id="id538546" class="indexterm" href=""></a><a id="id538554" class="indexterm" href=""></a> chapter does (<a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch09.html#Updatedscatterplotnowwithdataupdatesanddynamicscales" title="Figure 9-12. Updated scatterplot, now with data updates and dynamic scales">Figure 9-12</a>). I’ve brought it back, with a few tweaks, in <span class="emphasis"><em>19_axes_static.html</em></span>.</p>

<div>

<img alt="Imagen" src="/static/Fig912.png"/>

<p class="fig">Figura 9-12. Actualización de dispersión, ahora con actualizaciones de datos y escalas dinámicas</p>
<p class="fig">Figure 9-12. Updated scatterplot, now with data updates and dynamic scales</p>       
      </div>

      


<p class="it">Para resumir los cambios en el diagrama de dispersión:</p>


      <p class="p" id="to_summarize_th">To summarize the changes to the scatterplot:</p>





      <div class="itemizedlist" id="you_can_now_cli_id1">

        <ul class="itemizedlist">

         
          <li class="it">Ahora puede hacer clic en el texto en la parte superior para generar y actualizar con nuevos datos.</li> 

          <li class="p"> You can now click the text at top to generate and update with new data. </li>
          

          
 <li class="it">Las transiciones animadas se utilizan después de las actualizaciones de datos.</li>
          <li class="p"> Animated transitions are used after data updates. </li>
          


          
<li class="it">He eliminado el retraso escalonado, y puse todas las transiciones que se produzca durante un segundo completo (1.000 m).</li>
          <li class="p"> I eliminated the staggered delay, and set all transitions to occur over a full second (1,000 ms). </li>
          


          
<li class="it">Tanto las escalas de los ejes X e Y son actualizadas, también.</li>
          <li class="p"> Both the x- and y-axis scales are updated, too. </li>
          


          
<li class="it">Los círculos ahora tienen un radio constante.</li>
          <li class="p"> Circles now have a constant radius. </li>
          


        </ul>

      </div>

  
<p class="it">Trate de hacer clic en el texto y mire todos esos pequeños puntos de zoom alrededor. ¡Lindo! En cierto modo me gustaría que representaran alguna información significativa, pero bueno, los datos aleatorios pueden ser divertidos, también.</p>

<p class="p" id="try_clicking_th_id1">Try clicking the text and watch all those little dots zoom around. Cute! I sort of wish they represented some meaningful information, but hey, random data can be fun, too.</p>
    
 <p><strong>Ejercicio</strong></p>
      
<p class="it">Lo que no está pasando todavía es que los ejes se actualizan. Afortunadamente, es fácil de hacer.</p>

<p class="p" id="whats_not_happ_id1">What’s <span class="emphasis"><em>not</em></span> happening yet is that the axes aren’t updating. Fortunately, that is simple to do.</p>


<p class="it"> Primero, voy a añadir los nombres de clase <code class="literal">x</code> e <code class="literal">y</code> en nuestros ejes <code class="literal">x</code> e <code class="literal">y</code>, respectivamente. Esto nos ayudará a seleccionar los ejes más tarde:</p>

<p class="p" id="first_i_am_goi">First, I am going to add the class names <code class="literal">x</code> and <code class="literal">y</code> to our x- and y-axes, respectively. This will help us select those axes later:</p>


<pre class="programlisting" data-language="javascript" id="create_xaxis">//Create x-axis
svg.append("g")
    .attr("class", "x axis")    // &lt;-- Note x added here
    .attr("transform", "translate(0," + (h - padding) + ")")
    .call(xAxis);

//Create y-axis
svg.append("g")
    .attr("class", "y axis")    // &lt;-- Note y added here
    .attr("transform", "translate(" + padding + ",0)")
    .call(yAxis);</pre>


      <p class="p" id="then_down_in_o">Then, down in our click function, we simply add:</p>


      <pre class="programlisting" data-language="javascript" id="update_xaxis">//Update x-axis
svg.select(".x.axis")
    .transition()
    .duration(1000)
    .call(xAxis);

//Update y-axis
svg.select(".y.axis")
    .transition()
    .duration(1000)
    .call(yAxis);</pre>


<p class="it">Para cada eje, hacemos lo siguiente:</p>
      <p class="p" id="for_each_axis_">For each axis, we do the following:</p>


      <div class="orderedlist" id="select_the_axis_id1">

        <ol class="orderedlist" type="1">
<li class="it"> Seleccionar el eje. </li>
<li class="p"> Select the axis. </li>
          
<li class="it"> Iniciar una transición.</li>
<li class="p"> Initiate a transition. </li>
          
<li class="it"> Establecer la duración de la transición. </li>
<li class="p">Set the transition’s duration.</li>
      
<li class="it"> Llamar al generador de eje apropiado.</li>
<li class="p"> Call the appropriate axis generator. </li>
</ol>

      </div>

      


<p class="it">Recuerde que cada generador de eje ya se hace referencia a una escala (ya sea <code class="literal">xScale</code> o <code class="literal">yScale</code>). Debido a que esas escalas están siendo actualizadas, los generadores de eje pueden calcular cuáles deben ser las nuevas marcas de graduación.</p>


      <p class="p" id="remember_that_e">Remember that each axis generator is already referencing a scale (either <code class="literal">xScale</code> or <code class="literal">yScale</code>). Because those scales are being updated, the axis generators can calculate what the new tick marks should be.</p>


  <p class="it">Abre 20_axes _dynamic.html y dale una oportunidad.</p>

      <p class="p" id="open_up__axes">Open up <span class="emphasis"><em>20_axes_dynamic.html</em></span> and give it a try.</p>
  
    
       <p><strong>Ejercicio</strong></p>


<p class="it">Una vez más, <code class="literal">transition()</code> se encarga de toda la magia de la interpolación para usted - Mira esas garrapatas aparecen y desaparecen. Simplemente hermoso, y apenas se tenía que mover un dedo.</p>

      <p class="p" id="once_again_tra">Once again, <code class="literal">transition()</code> handles all the interpolation magic for you—watch those ticks fade in and out. Just beautiful, and you barely had to lift a finger.</p>

          <h3 class="title">each() Transition Starts and Ends</h3>


<p class="it">Habrá momentos cuando se quiere hacer que algo suceda al comienzo o al final de una transición. En esos momentos, puede utilizar cada <code class="literal">each()</code> para ejecutar código arbitrario para cada elemento en la selección.</p>


      <p class="p" id="there_will_be_t">There will be times when you want to make something happen at the start or end of a transition. In those times, you can use <code class="literal">each()</code> to execute arbitrary code for each element in the selection.<a id="id539339" class="indexterm" href=""></a><a id="id539345" class="indexterm" href=""></a></p>

<p class="it">cada <code class="literal">each()</code> espera dos argumentos:</p>


<p class="p" id="each_expects_"><code class="literal">each()</code> expects two arguments:</p>

      <div class="itemizedlist" id="either_start__id1">

        <ul class="itemizedlist">

          <li class="it">Ya sea "Inicio" o "fin"</li>

          <li class="p"> Either <code class="literal">"start"</code> or <code class="literal">"end"</code> </li>
          


          <li class="it">Una función anónima, para ser ejecutada ya sea en el inicio de una transición, o tan pronto como se ha terminado</li>

          <li class="p"> An anonymous function, to be executed either at the start of a transition, or as soon as it has ended </li>
          


        </ul>

      </div>

      <p class="it">Por ejemplo, aquí está nuestro  código-círculo-actualizado, con dos declaraciones <code class="literal">each()</code> añadidas:</p>


      <p class="p" id="for_example_he">For example, here is our circle-updating code, with two <code class="literal">each()</code> statements added:</p>

      <pre class="programlisting" data-language="javascript" id="update_all_ci">//Update all circles
svg.selectAll("circle")
   .data(dataset)
   .transition()
   .duration(1000)
   .each("start", function() {      // &lt;-- Executes at start of transition
       d3.select(this)
         .attr("fill", "magenta")
         .attr("r", 3);
   })
   .attr("cx", function(d) {
        return xScale(d[0]);
   })
   .attr("cy", function(d) {
        return yScale(d[1]);
   })
   .each("end", function() {        // &lt;-- Executes at end of transition
       d3.select(this)
         .attr("fill", "black")
         .attr("r", 2);
   });</pre>

<p class="p" id="you_can_see_thi_id1">You can see this in action in <span class="emphasis"><em>21_each.html</em></span>.</p>

<p class="it">Ahora haga clic en el gatillo, e inmediatamente cada relleno de círculo se establecerá en magenta, y su radio se establecerá en 3 (ver Figura 9-13). A continuación, la transición se ejecutara, por costumbre. Cuando se hayan completado, los rellenos y los radios vuelven a sus valores originales.</p>


<p class="p" id="now_you_click_t">Now you click the trigger, and immediately each circle’s fill is set to magenta, and its radius is set to 3 (see <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch09.html#Hotpinkcirclesinmidtransition" title="Figure 9-13. Hot pink circles, midtransition">Figure 9-13</a>). Then the transition is run, per usual. When complete, the fills and radii are restored to their original values.</p>





      

      <div>
<img alt="Imagen" src="/static/Fig913.png"/>

 <p class="fig">Figure 9-13. Figura 9-13. Círculos rosas fuertes, midtransition</p>

 <p class="fig">Figure 9-13. Hot pink circles, midtransition</p>

      </div>

      




<p class="it">Algo a destacar es que dentro de la función anónima pasada a <code class="literal">each()</code>, el contexto de esta se mantiene como "el elemento actual." Esto es práctico porque entonces esto puede ser referenciado con la funcion para volver a seleccionar fácilmente el elemento actual y modificarlo, como se ha hecho aquí:</p>

      <p class="p" id="something_to_no">Something to note is that within the anonymous function passed to <code class="literal">each()</code>, the context of <code class="literal">this</code> is maintained as “the current element.” This is handy because then <code class="literal">this</code> can be referenced with the function to easily reselect the current element and modify it, as done here:</p>




      <pre class="programlisting" data-language="javascript" id="eachstart__id1">   .each("start", function() {
       d3.select(this)              // Selects 'this', the current element
         .attr("fill", "magenta")   // Sets fill of 'this' to magenta
         .attr("r", 3);             // Sets radius of 'this' to 3
   })</pre>



            <h4 class="title">Warning: Start carefully</h4>
            <h4 class="title">Advertencia: Comienza con cuidado</h4>


        



<p class="it">Usted puede verse tentado a tirar otra transición aquí, lo que resulta en un fundido suave del negro al color magenta. No hacerlo! O hacerlo, pero tenga en cuenta que esto se va a romper:</p>

        <p class="p" id="you_might_be_te">You might be tempted to throw another transition in here,<a id="id540188" class="indexterm" href=""></a><a id="id540196" class="indexterm" href=""></a> resulting in a smooth fade from black to magenta. Don’t do it! Or do it, but note that this will break:</p>





        <pre class="programlisting" data-language="javascript" id="eachstart__id2">   .each("start", function() {
       d3.select(this)
         .transition()              // New transition
         .duration(250)             // New duration
         .attr("fill", "magenta")
         .attr("r", 3);
   })</pre>

        



<p class="it"> Si intenta esto, y le recomiendo que lo haga, usted encontrará que los círculos en efecto, se desvanecen al rosa, pero ya no cambian de posición en el espacio. Porque, de forma predeterminada, sólo una transición puede estar activa en cualquier elemento dado en un momento dado. <strong>Las transiciones nuevas interrumpen y anulan las transiciones anteriores.</strong> </p>

        <p class="p" id="if_you_try_this">If you try this, and I recommend that you do, you’ll find that the circles do indeed fade to pink, but they no longer change positions in space. That’s because, by default, only one transition can be active on any given element at any given time. Newer transitions interrupt and override older transitions.</p>


<p class="it"> Esto podría parecer una falla de diseño, pero D3 opera de esta manera a propósito. Imagínese si usted tenía varios botones diferentes, cada uno de los cuales desencadenara una visión diferente de los datos, y un visitante va accediendo a ellos en rápida sucesión. No desea una transición antes de ser interrumpido, por lo que la vista seleccionada por última vez podría ser puesta en lugar de inmediato?</p>

        <p class="p" id="this_might_seem">This might seem like a design flaw, but D3 operates this way on purpose. Imagine if you had several different buttons, each of which triggered a different view of the data, and a visitor was clicking through them in rapid succession. Wouldn’t you want an earlier transition to be interrupted, so the last-selected view could be put in place right away?</p>



<p class="it">Si está familiarizado con jQuery, notará una diferencia aquí. De forma predeterminada, jQuery pone en cola transiciones, para que ejecute una tras otra, y llamar a una nueva transición no interrumpe automáticamente las ya existentes. A veces, esto se traduce en comportamientos molestos de la interfaz, como los menús que se desvanecen al pasar el ratón por encima de ellos, pero empiezan a desvanecerse después que el fundido de entrada se ha completado.</p>

<p class="p" id="if_youre_famil_id4">If you’re familiar with jQuery, you’ll notice a difference here. By default, jQuery queues transitions, so they execute one after another, and calling a new transition doesn’t automatically interrupt any existing ones. This sometimes results in annoying interface behavior, like menus that fade in when you mouse over them, but won’t start fading out until <span class="emphasis"><em>after</em></span> the fade-in has completed.<a id="id540433" class="indexterm" href=""></a><a id="id540438" class="indexterm" href=""></a></p>


<p class="it">En este caso, el código "rompe", porque se comienza la primera transición (espacial), entonces <code class="literal">each("start", …)</code> es llamado en cada elemento. Dentro de <code class="literal">each()</code>, una segunda transición se inicia (el fundido de color rosa), anulando la primera transición, por lo que los círculos nunca llegan a su destino final (aunque se ven muy bien, simplemente sentado en su casa).</p>

        <p class="p" id="in_this_case_t_id2">In this case, the code “breaks” because the first (spatial) transition is begun, then <code class="literal">each("start", …)</code> is called on each element. Within <code class="literal">each()</code>, a second transition is initiated (the fade to pink), overriding the first transition, so the circles never make it to their final destinations (although they look great, just sitting at home).</p>

    <p class="it">Debido a esta peculiaridad de las transiciones, sólo recuerda que <code class="literal">each("start", …)</code> se debe utilizar solamente para las transformaciones inmediatas, sin transiciones.</p>

<p class="p" id="because_of_this">Because of this quirk of transitions, just remember that <code class="literal">each("start", …)</code> should be used only for immediate transformations, with no transitions.<a id="id540478" class="indexterm" href=""></a></p>


            <h4 class="title">End gracefully</h4>
            <h4 class="title">Terminar con gracia</h4>

<p class="it"><code class="literal">each("end", …)</code>  hace transiciones de apoyo. En el momento en que <code class="literal">each("end", …)</code>  es llamado, la transición primaria ha terminado ya, por lo que inicia una nueva transición sin causar ningún daño.</p>

<p class="p" id="eachend_"><code class="literal">each("end", …)</code>, however, <span class="emphasis"><em>does</em></span> support transitions. By the time <code class="literal">each("end", …)</code> is called, the primary transition has already ended, so initiating a new transition won’t cause any harm.</p>

<p class="it">Vea 22_each_combo_transition.html . Dentro de la primera <code class="literal">each()</code> , me encontré con el tamaño rosado del círculo radio de hasta 7. En la segunda, he añadido dos líneas de transición y una duración:</p>

<p class="p" id="see__each_com">See <span class="emphasis"><em>22_each_combo_transition.html</em></span>. Within the first <code class="literal">each()</code> statement, I bumped the pink circle radius size up to 7. In the second, I added two lines for transition and a duration:</p>

        <pre class="programlisting" data-language="javascript" id="eachend_fu">.each("end", function() {
    d3.select(this)
      .transition()             // &lt;-- New!
      .duration(1000)           // &lt;-- New!
      .attr("fill", "black")
      .attr("r", 2);
});</pre>

        



<p class="it">Vea esa transición: es cool! Tenga en cuenta la secuencia de eventos: </p>

<p class="p" id="watch_that_tran">Watch that transition: so cool! Note the sequence of events:</p>

<div>

          <ol class="orderedlist" type="1">
            <li class="it">Haga clic en el texto p. </li>
         <li class="p"> You click the p text.</li>

          

           <li class="it"> Los círculos se vuelven de color rosa e incrementan su tamaño inmediatamente. </li>
            <li class="p"> Circles turn pink and increase in size immediately. </li>
            

             <li class="it"> Los círculos transitan a nuevas posiciones. </li>
            <li class="p"> Circles transition to new positions. </li>
            

            <li class="it"> Los círculos transitan al color y tamaños originales. </li>
            <li class="p"> Circles transition to original color and size. </li>
            

          </ol>

        </div>

        


<p class="it">También, intente hacer clic en el trigger <code class="literal">p</code> varias veces seguidas. Vaya por delante, sólo tiene que ir rapido, haga clic tan rápido como sea posible. Observe cómo cada clic interrumpe el progreso de los círculos. (Lo siento, chico!) Usted esta viendo cada nueva petición de transición anular la anterior. Los círculos nunca alcanzarán sus posiciones finales y el fundido a negro a menos que deje de hacer clic y les de tiempo para descansar.</p>

<p class="p" id="also_try_click">Also, try clicking on the <code class="literal">p</code> trigger several times in a row. Go ahead, just go nuts, click as fast as you can. Notice how each click interrupts the circles’ progress. (Sorry, guys!) You’re seeing each new transition request override the old one. The circles will never reach their final positions and fade to black unless you stop clicking and give them time to rest.<a id="id540790" class="indexterm" href=""></a></p>

<p class="it"> Tan cool como sea, esta es una forma aún más fácil de programar múltiples transiciones para ejecutar una tras otra: simplemente encadenamos transiciones juntas. (Esta es una nueva característica de la versión 3.0 y no quiere trabajar con las versiones anteriores.) Por ejemplo, en lugar de reseleccionar elementos llama a seleccionar una nueva transición de cada uno dentro de <code class="literal">each("end", …)</code>, podemos simplemente virar un segundo la transición en el extremo de la cadena:</p>

<p class="p" id="as_cool_as_that">As cool as that is, there is an even simpler way to schedule multiple transitions to run one after the other: we simply chain transitions together. (This is a new feature in version 3.0 and won’t work with older versions.) For example, instead of reselecting elements and calling a new transition on each one within <code class="literal">each("end", …)</code>, we can just tack a second transition onto the end of the chain:</p>

        <pre class="programlisting" data-language="javascript" id="svgselectall_id11">svg.selectAll("circle")
   .data(dataset)
   .transition()    // &lt;-- Transition #1
   .duration(1000)
   .each("start", function() {
           d3.select(this)
             .attr("fill", "magenta")
             .attr("r", 7);
   })
   .attr("cx", function(d) {
                return xScale(d[0]);
   })
   .attr("cy", function(d) {
                return yScale(d[1]);
   })
   .transition()    // &lt;-- Transition #2
   .duration(1000)
   .attr("fill", "black")
   .attr("r", 2);</pre>

        


<p><strong>Ejercicio</strong></p>
<p class="it">Pruebe este código en 23_each_combo_transition_chained.html, y usted vera que tiene el mismo comportamiento. </p>


<p class="p" id="try_that_code_o">Try that code out in <span class="emphasis"><em>23_each_combo_transition_chained.html</em></span>, and you’ll see it has the same behavior.</p>

<p class="it">Cuando secuenciamos múltiples transiciones, recomiendo este enfoque de encadenamiento. Sólo entonces utilize <code class="literal">each()</code> para los cambios inmediatos (nontransitioned) que necesitan ocurrir justo antes o justo después de las transiciones. Como se puede imaginar, es posible crear secuencias muy complejas de cambios discretos y animados por el encadenamiento de múltiples transiciones, cada uno de los cuales pueden tener sus propias llamadas a <code class="literal">each( "start", ... )</code> y <code class="literal">each( "end", ... )</code>.</p>

<p class="p" id="when_sequencing">When sequencing multiple transitions, I recommend this chaining approach. Then only use <code class="literal">each()</code> for immediate (nontransitioned) changes that need to occur right before or right after transitions. As you can imagine, it’s possible to create quite complex sequences of discrete and animated changes by chaining together multiple transitions, each of which can have its own calls to <code class="literal">each("start", …)</code> and <code class="literal">each("end", …)</code>.</p>

            <h4 class="title">Transition less each()</h4>
            <h4 class="title">Transiciones menos each()</h4>

<p class="it">También puede utilizar cada línea <code class="literal">each()</code> de una transición, sólo para ejecutar código arbitrario para cada elemento de una selección. Fuera de las transiciones, basta con omitir el parámetro <code class="literal">"start"</code> o <code class="literal">"end"</code>, y sólo pasan en la función anónima.
 </p>

 <p class="p" id="you_can_also_us">You can also use <code class="literal">each()</code> outside of a transition, just to execute arbitrary code for each element in a selection. Outside of transitions, just omit the <code class="literal">"start"</code> or <code class="literal">"end"</code> parameter, and only pass in the anonymous function.</p>

<p class="it">  Aunque yo no haré esto aquí, también se pueden incluir referencias a <code class="literal">d</code> e <code class="literal">i</code>, dentro de su definición de la función, y D3 entregará al fin esos valores, como usted espera:</p>

<p class="p" id="although_i_didn">Although I didn’t do this here, you can also include references to <code class="literal">d</code> and <code class="literal">i</code> within your function definition, and D3 will hand off those values, as you’d expect:</p>

        <pre class="programlisting" data-language="javascript" id="eachfunctio">…
.each(function(d, i) {
    //Do something with d and i here
});</pre>



            <h4 class="title">Containing visual elements with clipping paths</h4>

<p class="it">Es de notar que ligeramente relacionados, usted puede haber notado que durante estas transiciones, los valores de x e y excederan los límites del área del gráfico, y la superposición de las líneas de eje, como se muestra en la Figura 9-14.</p>

<p class="p" id="on_a_slightly_r">On a slightly related note, you might have noticed that during these<a id="id541511" class="indexterm" href=""></a><a id="id541516" class="indexterm" href=""></a><a id="id541524" class="indexterm" href=""></a> transitions, points with low x or y values would exceed the boundaries of the chart area, and overlap the axis lines, as displayed in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch09.html#Pointsexceedingthechartarea" title="Figure 9-14. Points exceeding the chart area">Figure 9-14</a>.</p>


<div class="figure-contents">
<img alt="Imagen" src="/static/Fig914.png"/>


          <p class="fig"> Figura 9-14. Los puntos que excedan el área del gráfico</p>

          <p class="fig"> Figure 9-14. Points exceeding the chart area</p>
</div>

        



<p class="it">Afortunadamente, SVG tiene soporte para los clipping path (trazados de recorte), que podrían ser más familiares para usted si los llamamos máscaras, al igual que en Photoshop o Illustrator. Un clipping path es un elemento SVG que contiene elementos visuales que, en conjunto, conforman el trazado de recorte o máscara para ser aplicados a otros elementos. Cuando una máscara se aplica a un elemento, sólo los píxeles que se posan dentro de esa máscara se muestran.</p>

<p class="p" id="fortunately_sv">Fortunately, SVG has support for <span class="emphasis"><em>clipping paths</em></span>, which might be more familiar to you as <span class="emphasis"><em>masks</em></span>, as in Photoshop or Illustrator. A clipping path is an SVG element that contains visual elements that, together, make up the clipping path or mask to be applied to other elements. When a mask is applied to an element, only the pixels that land within that mask’s shape are displayed.</p>
      

<p class="it">Al igual <code class="literal">g</code>, un <code class="literal">clipPath</code>  no tiene una presencia visual o propia, pero contiene elementos visuales (que se utilizan para hacer la máscara). Por ejemplo, aquí un <code class="literal">clipPath</code> simple:</p>



<p class="p" id="much_like_g_a_">Much like <code class="literal">g</code>, a <code class="literal">clipPath</code> has no visual presence of its own, but it contains visual elements (which are used to make the mask). For example, here’s a simple <code class="literal">clipPath</code>:</p>


<pre class="programlisting" data-language="html" id="clippath_idc">&lt;clipPath id="chart-area"&gt;
    &lt;rect x="30" y="30" width="410" height="240"&gt;&lt;/rect&gt;
&lt;/clipPath&gt;</pre>

        



<p class="it">Tenga en cuenta que al elemento <code class="literal">clipPath</code>exterior le ha sido dada un ID de chart-area. Podemos usar ese ID para hacer referencia a ella más tarde. Dentro de la <code class="literal">clipPath</code>hay un<code class="literal">rect</code>, que funcionará como la máscara. </p>

        <p class="p" id="note_that_the_o">Note that the outer <code class="literal">clipPath</code> element has been given an ID of <code class="literal">chart-area</code>. We can use that ID to reference it later. Within the <code class="literal">clipPath</code> is a <code class="literal">rect</code>, which will function as the mask.</p>





        



<p class="it">Así que hay tres pasos para utilizar un trazado de recorte</p>

        <p class="p" id="so_there_are_th">So there are three steps to using a clipping path:</p>





        <div class="orderedlist" id="define_the_clip_id1">

          <ol class="orderedlist" type="1">

            
<li class="it">Definir el <code class="literal">clipPath</code>y darle una identificación.</li>
            <li class="p"> Define the <code class="literal">clipPath</code> and give it an ID. </li>
            


            
<li class="it">Poner los elementos visuales dentro del <code class="literal">clipPath</code> (por lo general sólo un<code class="literal">rect</code>, pero podrían ser círculos o cualesquiera otros elementos visuales).</li>
            <li class="p"> Put visual elements within the <code class="literal">clipPath</code> (usually just a <code class="literal">rect</code>, but this could be <code class="literal">circle</code>s or any other visual elements). </li>
            


            
<li class="it"> Añadir una referencia al <code class="literal">clipPath</code>de cualquier elemento(s) que desea enmascarar.</li>
            <li class="p"> Add a reference to the <code class="literal">clipPath</code> from whatever element(s) you wish to be masked. </li>
            


          </ol>

        </div>

        


<p class="it"> Continuando con el diagrama de dispersión, Definir el trazado de recorte con este nuevo código (pasos 1 y 2):</p>

<p class="p" id="continuing_with_id1">Continuing with the scatterplot, I’ll define the clipping path with this new code (steps 1 and 2):</p>





        <pre class="programlisting" data-language="javascript" id="define_clippi">//Define clipping path
svg.append("clipPath")                  //Make a new clipPath
    .attr("id", "chart-area")           //Assign an ID
    .append("rect")                     //Within the clipPath, create a new rect
    .attr("x", padding)                 //Set rect's position and size…
    .attr("y", padding)
    .attr("width", w - padding * 3)
    .attr("height", h - padding * 2);</pre>

        



<p class="it">Quiero que todos los círculos sean enmascarados por este <code class="literal">clipPath</code>. Podría agregar una referencia a cada <code class="literal">circle</code> <code class="literal">clipPath</code> por separado, pero es mucho más fácil y más limpio si sólo hay que poner todos los <code class="literal">circle</code> en el grupo <code class="literal">g</code>, y luego añadir la referencia a ese (este es el paso 3). 
</p>

        <p class="p" id="i_want_all_of_t">I want all of the <code class="literal">circle</code>s to be masked by this <code class="literal">clipPath</code>. I could add a <code class="literal">clipPath</code> reference to every single circle, but it’s much easier and cleaner to just put all the <code class="literal">circle</code>s into a <code class="literal">g</code> group, and then add the reference to that (this is step 3).</p>

<p class="it">Por lo tanto, voy a modificar este código:</p>

        <p class="p" id="so_i_will_modi">So, I will modify this code:</p>

        <pre class="programlisting" data-language="javascript" id="create_circle_id1">//Create circles
svg.selectAll("circle")
   .data(dataset)
   .enter()
   .append("circle")
   …</pre>

   <p class="it"> mediante la adición de tres nuevas líneas, la creación de un nuevo <code class="literal">g</code>, dándole un ID arbitrario, y finalmente añadiendo la referencia a la <code class="literal">chart-area</code> <code class="literal">clipPath</code>: </p>

<p class="p" id="by_adding_three">by adding three new lines, creating a new <code class="literal">g</code>, giving it an arbitrary ID, and finally adding the reference to the <code class="literal">chart-area</code> <code class="literal">clipPath</code>:</p>

<pre class="programlisting" data-language="javascript" id="create_circle_id2">//Create circles
svg.append("g")                             //Create new g
   .attr("id", "circles")                   //Assign ID of 'circles'
   .attr("clip-path", "url(#chart-area)")   //Add reference to clipPath
   .selectAll("circle")                     //Continue as before…
   .data(dataset)
   .enter()
   .append("circle")
   …</pre>

        


<p class="it">Observe que el nombre del atributo es clip-path y el nombre del elemento es clipPath. Argh! Lo sé; me vuelve loco, también.</p>


        <p class="p" id="notice_that_the_id2">Notice that the attribute name is <code class="literal">clip-path</code>, and the element name is <code class="literal">clipPath</code>. Argh! I know; it drives me crazy, too.</p>





        



<p class="it">Ver la página de ejemplo 24_clip-path.html y abra el inspector web. Vamos a echar un vistazo a ese nuevo rect en la figura 9-15.</p>

        <p class="p" id="view_the_sample">View the sample page <span class="emphasis"><em>24_clip-path.html</em></span> and open the web inspector. Let’s look at that new <code class="literal">rect</code> in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch09.html#ThedimensionsofarectwithinaclipPath" title="Figure 9-15. The dimensions of a rect within a clipPath">Figure 9-15</a>.</p>





       

          <div class="figure-contents">


            <img alt="Imagen" src="/static/Fig915.png"/>

          <p class="fig"> Figura 9-15. Las dimensiones de un rect dentro de un clipPath</p>

          <p class="fig"> Figure 9-15. The dimensions of a rect within a clipPath</p>
          
        </div>
        

        



<p class="it">Debido a que los clipPaths no tienen la representación visual (sólo enmascaran otros elementos), es muy útil destacarlos en el inspector web, para luego delinear el camino, la posición y el tamaño con una marca azul. En la figura 9-15 podemos ver que el <code class="literal">clipPath rect</code> está en el lugar correcto y es del tamaño correcto.</p>

        <p class="p" id="because_clippat">Because <code class="literal">clipPath</code>s have no visual rendering (they only mask other elements), it’s helpful to highlight them in the web inspector, which will then outline the path’s position and size with a blue highlight. In <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch09.html#ThedimensionsofarectwithinaclipPath" title="Figure 9-15. The dimensions of a rect within a clipPath">Figure 9-15</a> we can see that the <code class="literal">clipPath rect</code> is in the right place and is the right size.</p>





        



<p class="it"> Notece, también, que ahora todos los <code class="literal">circle</code> se agrupan en un solo elemento <code class="literal">g</code>, cuyo atributo <code class="literal">clip-path</code> hace referencia a nuestro nuevo trazado de recorte, utilizando la sintaxis url poco peculiar <code class="literal">url(#chart-area)</code>. Gracias por eso, a la especificación SVG.</p>
        

        <p class="p" id="notice_too_th">Notice, too, that now all the <code class="literal">circle</code>s are grouped within a single <code class="literal">g</code> element, whose <code class="literal">clip-path</code> attribute references our new clipping path, using the slightly peculiar syntax <code class="literal">url(#chart-area)</code>. Thanks for that, SVG specification.</p>








<p class="it">El resultado final es que nuestros píxeles de <code class="literal">circle</code> consiguen recortar cuando se acercan demasiado cerca del borde del área de la gráfica. Note los puntos en los extremos superior e bordes derecho.</p>
        

        <p class="p" id="the_end_result__id1">The end result is that our <code class="literal">circle</code>s’ pixels get clipped when they get too close to the edge of the chart area. Note the points at the extreme top and right edges.</p>







<p class="it">El recorte es más fácil de ver a mitad de la transición, como en la figura 9-16</p>


        <p class="p" id="the_clipping_is">The clipping is easier to see midtransition, as in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch09.html#Pointscontainedwithinthechartarea" title="Figure 9-16. Points contained within the chart area">Figure 9-16</a>.</p>







          <div class="figure-contents">

<img alt="Imagen" src="/static/Fig916.png"/>

   
<p class="fig"> Figura 9-16. Los puntos contenidos dentro del área del gráfico</p>
<p class="fig"> Figure 9-16. Points contained within the chart area</p>
          



          

        </div>

        



<p class="it">Voilà! Ya no exceden los puntos el limite de la tabla.</p>

        <p class="p" id="voil_the_poin">Voilà! The points no longer exceed the chart boundaries.<a id="id542631" class="indexterm" href=""></a></p>





 





        <h1 class="title">Other Kinds of Data Updates</h1>
        <h1 class="title">Otros tipos de Actualizaciones de Datos</h1>



    


<p class="it">Hasta ahora, cuando sucede la actualización de los datos, hemos tomado el enfoque “whole kit-and-kaboodle”: cambiando de valores en el array de datos, y luego volviendo a vincular ese conjunto de datos revisada, sobrescribiendo los valores originales unidos a nuestros elementos DOM.</p>


    <p class="p" id="until_now_when">Until now, when updating data, we have taken the “whole kit-and-kaboodle” approach: changing values in the dataset array, and then rebinding that revised dataset, overwriting the original values bound to our DOM elements.</p>





    



<p class="it">Este enfoque es más útil cuando todos los valores están cambiando, y cuando la longitud del conjunto de datos (es decir, el número de valores) se mantiene igual. Pero, como sabemos, los datos de la vida real son sucios, y piden una mayor flexibilidad, por ejemplo, cuando sólo desea actualizar uno o dos valores, o que incluso tienen que sumar o restarse los valores. D3, una vez más, viene al rescate.</p>


    <p class="p" id="that_approach_i">That approach is most useful when <span class="emphasis"><em>all</em></span> the values are changing, and when the length of the dataset (i.e., the number of values) stays the same. But as we know, real-life data is messy, and calls for even more flexibility, such as when you only want to update one or two values, or you even need to add or subtract values. D3, again, comes to the rescue.</p>






          <h3 class="title">Adding Values (and Elements)</h3>



      



<p class="it">Vamos a volver a nuestro amado gráfico de barras, y algunos dicen que la interacción del usuario (un clic del ratón) ahora debe dar lugar a la adición de un nuevo valor a nuestra base de datos. Es decir, la longitud del conjunto de datos de array se incrementará en uno.</p>

      <p class="p" id="lets_go_back_t">Let’s go back to our lovely bar chart, and say that some user interaction (a mouse click) should now trigger adding a <span class="emphasis"><em>new</em></span> value to our dataset. That is, the length of the array <code class="literal">dataset</code> will increase by one.<a id="ix_upadd" class="indexterm" href=""></a><a id="id542712" class="indexterm" href=""></a><a id="id542720" class="indexterm" href=""></a></p>





      




<p class="it">Pues bien, la generación de un número random y empujándolo al array es bastante fácil:</p>
      <p class="p" id="well_generatin">Well, generating a random number and pushing it to the array is easy enough:</p>





      <pre class="programlisting" data-language="javascript" id="add_one_new_v">//Add one new value to dataset
var maxValue = 25;
var newNumber = Math.floor(Math.random() * maxValue);
dataset.push(newNumber);</pre>

      



<p class="it">Liberar espacio para una barra adicional requerirá volver a calibrar la escala de nuestro eje x. Esto es sólo una cuestión de la actualización de su dominio de entrada para reflejar la nueva longitud del conjunto de datos:</p>

      <p class="p" id="making_room_for">Making room for an extra bar will require recalibrating our x-axis scale. That’s just a matter of updating its input domain to reflect the new length of <code class="literal">dataset</code>:</p>





      <pre class="programlisting" data-language="javascript" id="xscaledomaind">xScale.domain(d3.range(dataset.length));</pre>

      




<p class="it">Esto es lo fácil. Ahora preparese para doblar su cerebro una vez más, a medida que se sumerja en las profundidades de las selecciones D3. </p>
      <p class="p" id="thats_the_easy">That’s the easy stuff. Now prepare to bend your brain yet again, as we dive into the depths of D3 <span class="emphasis"><em>selections</em></span>.</p>







            <h4 class="title">Select</h4>


        



<p class="it">Por ahora, usted se siente cómodo usando <code class="literal">select()</code> y <code class="literal">selectAll()</code> para agarrar y volver selecciones de elementos DOM. Y usted puede incluso ver cómo, cuándo se encadenan estos métodos, agarran las selecciones dentro de las selecciones, y así sucesivamente, como en:</p>

        <p class="p" id="by_now_you_are">By now, you are comfortable using <code class="literal">select()</code> and <code class="literal">selectAll()</code> to grab and return DOM element selections. And you’ve even seen how, when these methods are chained, they grab selections within selections, and so on,<a id="id542980" class="indexterm" href=""></a><a id="id542985" class="indexterm" href=""></a> as in:</p>





        <pre class="programlisting" data-language="javascript" id="dselectbody_id9">d3.select("body").selectAll("p");   //Returns all 'p' elements within 'body'</pre>

        


<p class="it">Al almacenar los resultados de estos métodos de selección, el resultado más específico - es decir, el resultado de la última selección en la cadena - es la referencia fuera entregado a la variable. Por ejemplo:</p>


        <p class="p" id="when_storing_th">When storing the <span class="emphasis"><em>results</em></span> of these selection methods, the most specific result—meaning the result of the last selector in the chain—is the reference handed off to the variable. For example:</p>





        <pre class="programlisting" data-language="javascript" id="var_paragraphs_">var paragraphs = d3.select("body").selectAll("p");</pre>

        


<p class="it">Ahora los <code class="literal">paragraphs</code>  contiene una selección de todos los elementos <code class="literal">p</code> en el DOM, a pesar de que pasamos a través del <code class="literal">body</code> para llegar allí.</p>


        <p class="p" id="now_paragraphs_">Now <code class="literal">paragraphs</code> contains a selection of all <code class="literal">p</code> elements in the DOM, even though we traversed through <code class="literal">body</code> to get there.</p>





        



<p class="it">El giro aquí es que el método <code class="literal">data()</code> también devuelve una selección. En concreto, <code class="literal">data()</code> devuelve una referencia a todos los elementos a la que solo estaba obligado de datos, lo que llamamos la actualización de la selección.</p>

        <p class="p" id="the_twist_here_">The twist here is that the <code class="literal">data()</code> method <span class="emphasis"><em>also</em></span> returns a selection. Specifically, <span class="keep-together"><code class="literal">data()</code></span> returns references to all elements to which data was just bound, which we call the <span class="emphasis"><em>update</em></span> selection.</p>





        




<p class="it">En el caso de nuestro gráfico de barras, esto significa que podemos seleccionar todos los bars, a continuación, volver a enlazar los nuevos datos a los bars, y agarrar la selección Actualizar todo de una sola vez:</p>

        <p class="p" id="in_the_case_of_">In the case of our bar chart, this means that we can select all the bars, then rebind the new data to those bars, and grab the update selection all in one fell swoop:</p>




        <pre class="programlisting" data-language="javascript" id="select_var_b">//Select…
var bars = svg.selectAll("rect")
    .data(dataset);</pre>

        



<p class="it">Ahora la selección de actualización se almacena en las bars. </p>

        <p class="p" id="now_the_update_">Now the update selection is stored in <code class="literal">bars</code>.</p>








            <h4 class="title">Enter</h4>



        



<p class="it">Cuando cambiamos de valores de datos, pero no la longitud de todo el conjunto de datos, no tenemos por que preocuparnos acerca de una actualización de la selection—we simply el rebote de la data, y la transición a los nuevos valores de los atributos.</p>

        <p class="p" id="when_we_changed">When we changed our data values, but not the <span class="emphasis"><em>length</em></span> of the whole data set, we didn’t have to worry about an update selection—we simply rebound the data, and transitioned to new attribute values.</p>





        



<p class="it">Pero ahora hemos añadido un valor. Así <code class="literal">dataset.length</code> originalmente era 20, pero ahora es 21. ¿Cómo podemos hacerle frente a ese nuevo valor de datos, en concreto, para dibujar una nueva<code class="literal">rect</code> para ello? Quédese conmigo aquí; su paciencia será recompensada.</p>


        <p class="p" id="but_now_we_have">But now we have <span class="emphasis"><em>added</em></span> a value. So <code class="literal">dataset.length</code> was originally 20, but now it is 21. How can we address that new data value, specifically, to draw a new <code class="literal">rect</code> for it? Stay with me here; your patience will be rewarded.</p>




        



<p class="it">El genio de la selección de actualización es el que contiene en su interior y hace referencia a las subopciones enter y exit.</p>

        <p class="p" id="the_genius_of_t">The genius of the update selection is that it contains within it references to <span class="emphasis"><em>enter</em></span> and <span class="emphasis"><em>exit</em></span> subselections.</p>





        



<p class="it">La introducción de elementos son los que son nuevos en la escena. Eso considera una buena forma de dar la bienvenida a estos elementos a la zona con un plato de cookies.</p>


        <p class="p" id="entering_elemen"><span class="emphasis"><em>Entering</em></span> elements are those that are new to the scene. It’s considered good form to welcome such elements to the neighborhood with a plate of cookies.</p>




        



<p class="it">Cada vez hay más valores de datos que corresponden a elementos DOM, la selección enter contiene referencias a los elementos que todavía no existen. Usted ya sabe cómo acceder a la selección enter: mediante el uso de <code class="literal">enter()</code> después de unir los nuevos datos, como lo hacemos cuando se crea por primera vez el gráfico de barras. Ya ha visto el código siguiente:</p>

        <p class="p" id="whenever_there__id1">Whenever there are more data values than corresponding DOM elements, the <span class="emphasis"><em>enter</em></span> selection contains references to those elements <span class="emphasis"><em>that do not yet exist</em></span>. You already know how to access the enter selection: by using <code class="literal">enter()</code> after binding the new data, as we do when first creating the bar chart. You have already seen the following code:</p>
        



        
        <pre class="programlisting" data-language="javascript" id="svgselectall_id12">svg.selectAll("rect") //Selects all rects (as yet nonexistent)
   .data(dataset)     //Binds data to selection, returns update selection
   .enter()           //Extracts the enter selection, i.e., 20 placeholder elements
   .append("rect")    //Creates a 'rect' inside each of the placeholder elements
   …</pre>

        

<p class="it">Usted ya ha visto esta secuencia de <code class="literal">selectAll()</code>→<code class="literal">data()</code>→<code class="literal">enter()</code>→<span class="keep-together"><code class="literal">append()</code></span> muchas veces, pero sólo en el contexto de creación de muchos elementos inmediatamente, cuando la página se carga por primera vez.</p>
        



        <p class="p" id="you_have_alread">You have already seen this sequence of <code class="literal">selectAll()</code>→<code class="literal">data()</code>→<code class="literal">enter()</code>→<span class="keep-together"><code class="literal">append()</code></span> many times, but only in the context of creating many elements at once, when the page first loads.</p>








<p class="it">Ahora que hemos añadido un valor al <code class="literal">dataset</code>, podemos utilizar <code class="literal">enter()</code>  para abordar el correspondiente nuevo elemento DOM, sin tocar todos los rects existentes. Después de la Select code anterior, agregaré:</p>


        <p class="p" id="now_that_we_hav">Now that we have added one value to <code class="literal">dataset</code>, we can use <code class="literal">enter()</code> to address the one new corresponding DOM element, without touching all the existing <code class="literal">rect</code>s. Following the preceding <code class="literal">Select</code> code, I’ll add:</p>




        <pre class="programlisting" data-language="javascript" id="enter_barse">//Enter…
bars.enter()
    .append("rect")
    .attr("x", w)
    .attr("y", function(d) {
        return h - yScale(d);
    })
    .attr("width", xScale.rangeBand())
    .attr("height", function(d) {
        return yScale(d);
    })
    .attr("fill", function(d) {
        return "rgb(0, 0, " + (d * 10) + ")";
    });</pre>

        

<p class="it">Recuerde, <code class="literal">bars</code> contiene la selección de actualización, por lo <code class="literal">bars.enter()</code> extrae el ingreso en la selección de eso. En este caso, la selección introducir es una referencia a un nuevo elemento DOM. Seguimos con la que <code class="literal">append()</code> para crear la nueva <code class="literal">rect</code>, y todo el <code class="literal">attr()</code> declaraciones como de costumbre, a excepción de la línea siguiente:</p>



<p class="p" id="remember_bars_">Remember, <code class="literal">bars</code> contains the update selection, so <code class="literal">bars.enter()</code> extracts the enter selection from that. In this case, the enter selection is one reference to one new DOM element. We follow that with <code class="literal">append()</code> to create the new <code class="literal">rect</code>, and all the other <code class="literal">attr()</code> statements as usual, except for the following line:</p>





        <pre class="programlisting" data-language="javascript" id="attrx_w">.attr("x", w)</pre>

        



<p class="it">Usted puede notar que esto establece la posición horizontal de la nueva <code class="literal">rect</code> que estará un poco más allá del borde extremo derecho de la SVG. Quiero que la nueva barra se cree fuera de la vista, así que puedo utilizar una buena transición, sin problemas para moverla suavemente hacia la vista. </p>

<p class="p" id="you_might_notic_id2">You might notice that this sets the horizontal position of the new <code class="literal">rect</code> to be just past the far right edge of the SVG. I want the new bar to be created just out of sight, so I can use a nice, smooth transition to move it gently into view.</p>

                <h4 class="title">Update</h4>


        


<p class="it">Hicimos el nuevo <code class="literal">rect</code>; Ahora todo lo que esta a la izquierda es actualizar todos los<code class="literal">rect</code> atributos visuales. Una vez más, bares aquí almacena la selección actualización completa (que incluye la selección entrar):</p>


<p class="p" id="we_made_the_new">We made the new <code class="literal">rect</code>; now all that’s left is to update all <code class="literal">rect</code>’s visual attributes. Again, <code class="literal">bars</code> here stores the complete update selection (which includes the enter selection):</p>

        <pre class="programlisting" data-language="javascript" id="update_bars">//Update…
bars.transition()
    .duration(500)
    .attr("x", function(d, i) {
        return xScale(i);
    })
    .attr("y", function(d) {
        return h - yScale(d);
    })
    .attr("width", xScale.rangeBand())
    .attr("height", function(d) {
        return yScale(d);
    });</pre>

        


<p class="it">Esto tiene el efecto de tomar todos los bares y la transición a sus nuevos valores de x, y, width y height. No me cree? Vea el código de trabajo en 25_adding_values.html . 
</p>

<p class="p" id="this_has_the_ef">This has the effect of taking <span class="emphasis"><em>all</em></span> the bars and transitioning them to their new x, y, width, and height values. Don’t believe me? See the working code in <span class="emphasis"><em>25_adding_values.html</em></span>.</p>

<p class="it">La figura 9-17 muestra el diagrama inicial.</p>

<p class="p" id="shows_the_initi"><a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch09.html#Initialbarchart" title="Figure 9-17. Initial bar chart">Figure 9-17</a> shows the initial chart.</p>


<div class="figure-contents">

<img alt="Imagen" src="/static/Fig917.png"/>

<p>Figure 9-17. Initial bar chart</p>

<p class="it">Figura 9-17. En gráfico de barras inicial</p>

</div>


<p class="it"> La figura 9-18 muestra el gráfico después de un clic en el texto. Tenga en cuenta la nueva barra de la derecha.</p>

<p class="p" id="shows_the_chart"><a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch09.html#Afteroneclick" title="Figure 9-18. After one click">Figure 9-18</a> shows the chart after one click on the text. Note the new bar on the right.</p>

<div class="figure-contents">

<img alt="Imagen" src="/static/Fig918.png"/>

<p class="fig">Figura 9-18. Después de un clic</p>

<p class="fig">Figure 9-18. After one click</p>
          
</div>

        
<p class="p" id="after_two_click_id1">After two clicks, we get the chart shown in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch09.html#Aftertwoclicks" title="Figure 9-19. After two clicks">Figure 9-19</a>. <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch09.html#Afterthreeclicks" title="Figure 9-20. After three clicks">Figure 9-20</a> shows the result after three clicks.</p>


<div class="figure-contents">

<img alt="Imagen" src="/static/Fig919.png"/>

<p class="fig">Figura 9-19. Después de dos clics</p>

<p class="fig">Figure 9-19. After two clicks</p>
          
</div>

<div>

<img alt="Imagen" src="/static/Fig920.png"/>


<p class="fig"> 9-20. Después de tres clics</p>

<p class="fig">Figure 9-20. After three clicks</p>
          
</div>

<p class="p" id="after_several_m">After several more clicks, you’ll see the chart shown in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch09.html#Aftermanyclicks" title="Figure 9-21. After many clicks">Figure 9-21</a>.</p>
        
<p class="it">Después de varios clics, usted puede ver el gráfico que se muestra en la Figura 9-21.</p>


<div class="figure-contents">

<img alt="Imagen" src="/static/Fig921.png"/>

<p class="fig"> 9-21. Después de muchos clics</p>

<p class="fig">Figure 9-21. After many clicks</p>

</div>

<p class="it"> No sólo se están creando nuevos bares, tamaño, y posicion, pero en cada clic, todas las otras barras se reajustarán y se colocan en posición también.</p>

<p class="p" id="not_only_are_ne">Not only are new bars being created, sized, and positioned, but on every click, <span class="emphasis"><em>all other bars</em></span> are rescaled and moved into position as well.</p>

<p class="it">Lo que no sucede es que las nuevas etiquetas de valor no se crean y la transición en su lugar. Eso lo dejo como ejercicio para que usted pueda seguir.</p>

<p class="p" id="whats_not_happ_id2">What’s <span class="emphasis"><em>not</em></span> happening is that new value labels aren’t being created and transitioned into place. I leave that as an exercise for you to pursue.<a id="id544578" class="indexterm" href=""></a></p>

<p><strong>Ejercicio</strong></p>
  
<h3 class="title">Removing Values (and Elements)</h3>

<p class="it">La extracción de elementos es más fácil.</p>

<p class="p" id="removing_elemen">Removing elements is easier.<a id="ix_uprem" class="indexterm" href=""></a></p>

<p class="it">Cada vez hay más elementos DOM que los valores de datos, la salida de la selección contiene referencias a esos elementos sin datos. A medida que ya hemos adivinado, podemos acceder a la selección de salida con el metodo <code class="literal">exit()</code>.</p>

<p class="p" id="whenever_there__id2">Whenever there are more DOM elements than data values, the <span class="emphasis"><em>exit</em></span> selection contains references to those elements without data. As you’ve<a id="id544650" class="indexterm" href=""></a> already guessed, we can access the exit selection with <code class="literal">exit()</code>.</p>

<p class="it">En primer lugar, cambiaré nuestro texto de trigger para indicar que valores de eliminación:</p>

<p class="p" id="first_ill_cha">First, I’ll change our trigger text to indicate we’re removing values:</p>

<pre class="programlisting" data-language="html" id="pclick_on_thi_id3">&lt;p&gt;Click on this text to remove a data value from the chart!&lt;/p&gt;</pre>

<p class="it">Luego, el click, en lugar de generar un nuevo valor aleatorio y añadiéndola al <code class="literal">dataset</code>, que contiene el cambio de <code class="literal">shift()</code>, que elimina el primer elemento del array: </p>

<p class="p" id="then_on_click">Then, on click, instead of generating a new random value and adding it to <code class="literal">dataset</code>, we’ll use <code class="literal">shift()</code>, which removes the first element from the array:</p>

<pre class="programlisting" data-language="javascript" id="remove_one_va">//Remove one value from dataset
dataset.shift();</pre>

<h4 class="title">Exit</h4>

<p class="it">Extrae elementos son los que están en salida. Nosotros somos educados y le deseamos a estos elementos un viaje seguro.</p>

<p class="p" id="exiting_element"><span class="emphasis"><em>Exiting</em></span> elements are those that are on their way out. We should be polite and wish these elements a safe journey.<a id="id544757" class="indexterm" href=""></a></p>

<p class="it">Así que tomamos la selección de salida, el elemento de transición que sale fuera hacia el lado derecho, y, por último, lo quitamos:</p>

<p class="p" id="so_we_grab_the_">So we grab the exit selection, transition the exiting element off to the right side, and, finally, remove it:</p>

<pre class="programlisting" data-language="javascript" id="exit_barsex_id1">//Exit…
bars.exit()
    .transition()
    .duration(500)
    .attr("x", w)
    .remove();</pre>

<p class="it"><code class="literal">remove()</code> es un método especial de transición que espera a que se complete la transición, y luego elimina el elemento de la DOM para siempre. (Lo sentimos, no podemos volver atras.)</p>

<p class="p" id="remove_is_a_s"><code class="literal">remove()</code> is a special transition method that waits until the transition is complete, and then deletes the element from the DOM forever. (Sorry, there’s no getting it back.)</p>

<h4 class="title">Making a smooth exit</h4>

<p class="it">Visualmente hablando, se recomienda llevar a cabo una tránsición en primer lugar, en lugar de simplemente <code class="literal">remove()</code> elementos de forma inmediata. En este caso, estamos moviendo la barra hacia la derecha, pero sólo hicimos una transición tan fácilmente con <code class="literal">opacity</code> a cero, o aplicamos alguna otra transición visual.</p>        

<p class="p" id="visually_speaki">Visually speaking, it’s good practice to perform a transition first, rather than simply <code class="literal">remove()</code> elements right away. In this case, we’re moving the bar off to the right, but you could just as easily transition <code class="literal">opacity</code> to zero, or apply some other visual transition.</p>

<p class="it">Dicho esto, si alguna vez tiene que acaba de deshacerse de un elemento ASAP, por todos los medios, puede utilizar <code class="literal">remove()</code> sin llamar a una transición en primer lugar.</p>

<p class="p" id="that_said_if_y">That said, if you ever need to just get rid of an element ASAP, by all means, you can use <code class="literal">remove()</code> without calling a transition first.</p>

<p class="it">Bien, ahora a probar el código en 26_removing_values.html . La figura 9-22 muestra la vista inicial.</p>

<p class="p" id="okay_now_try_o">Okay, now try out the code in <span class="emphasis"><em>26_removing_values.html</em></span>. <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch09.html#Initial_bar_chart" title="Figure 9-22. Initial bar chart">Figure 9-22</a> shows the initial view.</p>

<div class="figure-contents">

<img alt="Imagen" src="/static/Fig922.png"/>


<p class="fig">Figure 9-22. Initial bar chart</p>
<p class="fig">Figura 9-22. Gráfico de barras Inicial</p>

</div>

<p class="it">Entonces, después de un clic en el texto, tenga en cuenta la pérdida de un bar en la figura 9-23.</p>

<p class="p" id="then_after_one">Then, after one click on the text, note the loss of one bar in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch09.html#After_one_click" title="Figure 9-23. After one click">Figure 9-23</a>.</p>

<div class="figure-contents">

<img alt="Imagen" src="/static/Fig923.png"/>

<p class="fig">9-23. Después de un clic</p>
<p class="fig">Figure 9-23. After one click</p>
          
</div>

<p class="it">Después de dos clics, usted puede ver el gráfico en la Figura 9-24. La figura 9-25 muestra lo que aparece después de tres clics.</p>

<p class="p" id="after_two_click_id2">After two clicks, you’ll see the chart in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch09.html#After_two_clicks" title="Figure 9-24. After two clicks">Figure 9-24</a>. <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch09.html#After_three_clicks" title="Figure 9-25. After three clicks">Figure 9-25</a> shows what displays after three clicks.</p>

<div class="figure" id="After_two_clicks">

<img alt="Imagen" src="/static/Fig924.png"/>

<p class="fig"> 9-24. Después de dos clics</p>
<p class="fig">Figure 9-24. After two clicks</p>
          
</div>


<div class="figure-contents">

<img alt="Imagen" src="/static/Fig925.png"/>

<p class="fig"> 9-25. Después de tres clics</p>

<p class="fig">Figure 9-25. After three clicks</p>

</div>

<p class="it">Después de muchos clics, el resultado se muestra en la Figura 9-26.</p>
<p class="p" id="after_many_clic">After many clicks, the result is shown in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch09.html#After_many_clicks" title="Figure 9-26. After many clicks">Figure 9-26</a>.</p>

<div class="figure" id="After_many_clicks">

<img alt="Imagen" src="/static/Fig926.png"/>

<p class="it"> 9-26. Después de muchos clics</p>

<p>Figure 9-26. After many clicks</p>
</div>

        




<p class="it"> En cada clic, una barra se mueve hacia la derecha, y luego se retira del DOM. (Se puede confirmar esto con el inspector web).</p>

<p class="p" id="on_each_click_">On each click, one bar moves off to the right, and then is removed from the DOM. (You can confirm this with the web inspector.)</p>

<p class="it">Pero que es lo que no está funcionando como se esperaba? Para empezar , las etiquetas de valor no se han eliminado, por eso el desorden de la parte superior derecha de nuestra tabla. Una vez más, voy a dejar la fijación de este aspecto como un ejercicio para usted.</p>
<p><strong>Ejercicio</strong></p>

<p class="p" id="but_whats_not_">But what’s not working as expected? For starters, the value labels aren’t being removed, so they clutter up the top right of our chart. Again, I will leave fixing this aspect as an exercise to you.</p>
         
<p class="it">Más importante aún, a pesar de que estamos utilizando el método <code class="literal">Array.shift()</code> para eliminar el primer valor de aquí para allá el array de <code class="literal">dataset</code>, que " no es la primera barra que se retira, ¿verdad? En cambio, la última barra en el DOM, la forma visual en el extremo derecho, siempre se retira. A pesar de que los valores de los datos se actualizan correctamente (tenga en cuenta cómo se mueven hacia la izquierda con cada clic - 5, 1 0, 13, 19, etc.), las barras se asignan nuevos valores, en lugar de " pegarse " con sus valores iniciales . Es decir, la esperada constancia del objeto se rompe - la barra " 5 " se convierte en la barra " 10 ", y así sucesivamente, sin embargo, percivo que preferiría que la barra " 5 " se corra hacia la izquierda y dejar que los demás barras mantengan sus valores originales.</p>

<p class="p" id="more_important_id2">More important, although we are using the <code class="literal">Array.shift()</code> method to remove the <span class="emphasis"><em>first</em></span> value from the <code class="literal">dataset</code> array, it’s not the <span class="emphasis"><em>first</em></span> bar that is removed, is it? Instead, the last bar in the DOM, the one visually on the far right, is always removed. Although the data values are updating correctly (note how they move to the left with each click—5, 10, 13, 19, and so on), the bars are assigned new values, rather than “sticking” with their intial values. That is, the anticipated <span class="emphasis"><em>object constancy</em></span> is broken—the “5” bar becomes the “10” bar, and so on, yet perceptually we would prefer that the “5” bar simply scoot off to the left and let all the other bars keep their original values.</p>
      
<p class="it">¿Por qué, por qué, oh, por qué sucede esto?! No es para preocuparse; hay una explicación perfectamente razonable. La clave para mantener la constancia del objeto es, así, las llaves. (En una nota lateral, Mike Bostock tiene un panorama muy claro del valor de la constancia del objeto, la cual recomiendo).</p>

<p class="p" id="why_why_oh_w">Why, why, oh, why is this happening?! Not to worry; there’s a perfectly reasonable explanation. The key to maintaining object constancy is, well, keys. (On a side note, Mike Bostock has a very eloquent <a class="ulink" href="http://bost.ocks.org/mike/constancy/" target="_top">overview of the value of object constancy</a>, which I recommend.)<a id="id545180" class="indexterm" href=""></a></p>

          <h3 class="title">Data Joins with Keys</h3>
          <h3 class="title">Los Datos se Unen con Keys</h3>

<p class="it">Ahora que comprende la actualización de  las selecciones, enter, y exit que el tiempo profundiza en los datos que une.</p>

<p class="p" id="now_that_you_un">Now that you understand update, enter, and exit selections, it’s time to dig deeper into data joins.<a id="ix_dajoin" class="indexterm" href=""></a><a id="ix_updajoin" class="indexterm" href=""></a><a id="id545229" class="indexterm" href=""></a><a id="id545237" class="indexterm" href=""></a></p>

<p class="it">Los datos se unen, esto sucede cada vez que agrega datos a los elementos DOM; es decir, cada vez que se enlaza los datos ().</p>

<p class="p" id="a_data_join_hap">A data join happens whenever you bind data to DOM elements; that is, every time you call <code class="literal">data()</code>.<a id="id545258" class="indexterm" href=""></a></p>

<p class="it">El valor predeterminado es unirse por orden de índice , es decir, el primer valor de datos está unido al primer elemento de DOM en la selección, el segundo valor se une al segundo elemento, y así sucesivamente.</p>

<p class="p" id="the_default_joi">The default join is by <span class="emphasis"><em>index order</em></span>, meaning the first data value is bound to the first DOM element in the selection, the second value is bound to the second element, and so on.<a id="id545277" class="indexterm" href=""></a></p>

<p class="it">Pero por que si los valores de datos electrónicos y elementos DOM no están en el mismo orden? Luego hay que decir a D3 cómo unirse o pares de valores y elementos. Afortunadamente, se puede definir esas reglas especificando una función del key</p>

<p class="p" id="but_what_if_the">But what if the data values and DOM elements are not in the same order? Then you need to tell D3 how to join or pair values and elements. Fortunately, you can define those rules by specifying a <span class="emphasis"><em>key function</em></span>.<a id="id545294" class="indexterm" href=""></a></p>

<p class="it">Esto explica el problema con nuestros bares. Después quitamos el primer valor del array de datos, para volver a vincular el nuevo conjunto de datos en la parte superior de los elementos existentes. Esos valores se unieron con el fin índice, por lo que la primera<code class="literal">rect</code>, que originalmente tenía un valor de 5, ahora se le asigna 10. La primera barra 10 se le asigna 13, y así sucesivamente. Al final deja un elemento de datos sin<code class="literal">rect</code>, el último en el extremo derecho.</p>

<p class="p" id="this_explains_t">This explains the problem with our bars. After we remove the first value from the <code class="literal">dataset</code> array, we rebind the new <code class="literal">dataset</code> on top of the existing elements. Those values are joined in index order, so the first <code class="literal">rect</code>, which originally had a value of 5, is now assigned 10. The former 10 bar is assigned 13, and so on. In the end, that leaves one <code class="literal">rect</code> element without data—the last one on the far right.</p>

<p class="it"> Podemos utilizar una función key para controlar los datos y unirlos con mayor especificidad y asegurarse de que el dato de la derecha se une al elemento<code class="literal">rect</code> derecho.</p>

<p class="p" id="we_can_use_a_ke">We can use a <span class="emphasis"><em>key function</em></span> to control the data join with more specificity and ensure that the right datum is bound to the right <code class="literal">rect</code> element.</p>

<div>

            <h4 class="title">Preparing the data</h4>

<p class="it">Hasta ahora, nuestra base de datos ha sido una simple array de valores. Sin embargo, para utilizar una key function, cada valor debe tener alguna "key" asociada a él. Piense en la key como un medio para identificar el valor sin tener en cuenta el valor en sí, ya que los valores propios pueden cambiar o existir en forma duplicada. (Si hay dos valores independientes de <code class="literal">3</code>, ¿cómo podría diferenciarlos?)</p>

<p class="p" id="until_now_our_">Until now, our dataset has been a simple array of values. But to use a key function, each value must have some “key” associated with it. Think of the key as a means of identifying the value without looking at the value itself, as the values themselves might change or exist in duplicate form. (If there were two separate values of <code class="literal">3</code>, how could you tell them apart?)<a id="id545374" class="indexterm" href=""></a></p>

<p class="it"> En lugar de una array de valores, deje de usar una gran variedad de objetos, en el que cada objeto puede contener tanto un valor de key y el valor real de los datos:</p>

<p class="p" id="instead_of_an_a">Instead of an array of values, let’s use an array of <span class="emphasis"><em>objects</em></span>, within which each object can contain both a key value and the actual data value:</p>

<pre class="programlisting" data-language="javascript" id="var_dataset___id18">var dataset = [ { key: 0, value: 5 },
                { key: 1, value: 10 },
                { key: 2, value: 13 },
                { key: 3, value: 19 },
                { key: 4, value: 21 },
                { key: 5, value: 25 },
                { key: 6, value: 22 },
                { key: 7, value: 18 },
                { key: 8, value: 15 },
                { key: 9, value: 13 },
                { key: 10, value: 11 },
                { key: 11, value: 12 },
                { key: 12, value: 15 },
                { key: 13, value: 20 },
                { key: 14, value: 18 },
                { key: 15, value: 17 },
                { key: 16, value: 16 },
                { key: 17, value: 18 },
                { key: 18, value: 23 },
                { key: 19, value: 25 } ];</pre>

<p class="it">Recuerde, los corchetes <code class="literal">[]</code> indican un array, y entre llaves <code class="literal">{}</code> indican un objeto. </p>
        
<p class="p" id="remember_hard_">Remember, hard brackets <code class="literal">[]</code> indicate an array, and curly brackets <code class="literal">{}</code> indicate an object.</p>

<p class="it">Tenga en cuenta que los valores de los datos aquí no han cambiado desde nuestros <code class="literal">dataset</code> originales. ¿Qué traen de nuevo las <code class="literal">key</code>, que simplemente enumeran cada objeto en su posición original dentro del array de <code class="literal">dataset</code>. (Por cierto, su nombre clave elegido no tiene que ser key. El nombre puede ser cualquier cosa, como ID, año o fruitType estoy usando key aquí para simplificar).</p>

<p class="p" id="note_that_the_d">Note that the data values here are unchanged from our original <code class="literal">dataset</code>. What’s new are the keys, which just enumerate each object’s original position within the <code class="literal">dataset</code> array. (By the way, your chosen key name doesn’t have to be <code class="literal">key</code>—the name can be anything, like <code class="literal">id</code>, <code class="literal">year</code>, or <code class="literal">fruitType</code>. I am using <code class="literal">key</code> here for simplicity.)</p>

<h4 class="title">Updating all references</h4>


<p class="it">  El siguiente paso ISN ' t divertido, pero ' no es difícil. Ahora que nuestros valores de datos están enterrados dentro de los objetos, ya no podemos simplemente hacer referencia d. (Ah, los buenos viejos días.) En cualquier parte del código donde queremos acceder a los datos reales de valor , ahora tenemos que especificar <code class="literal">d.value</code>. Cuando usamos funciones anónimas dentro de los métodos D3, d es mano lo que está en la posición actual en l arraye. En este caso, cada posición en el array contiene ahora un objeto, tal como<code class="literal">{ key: 12, value: 15 }</code>. Así que para obtener el valor 15, ahora tenemos que escribir <code class="literal">d.value</code> para llegar en el objeto y agarrar ese valor <code class="literal">value</code>. (Espero que vea un montón de valor en este párrafo.)</p>

<p class="p" id="the_next_step_i">The next step isn’t fun, but it’s not hard. Now that our data values are buried within objects, we can no longer just reference <code class="literal">d</code>. (Ah, the good old days.) Anywhere in the code where we want to access the actual data <span class="emphasis"><em>value</em></span>, we now need to specify <code class="literal">d.value</code>. When we use anonymous functions within D3 methods, <code class="literal">d</code> is handed whatever is in the current position in the array. In this case, each position in the array now contains an object, such as <code class="literal">{ key: 12, value: 15 }</code>. So to get at the value <code class="literal">15</code>, we now must write <code class="literal">d.value</code> to reach <span class="emphasis"><em>into</em></span> the object and grab that <code class="literal">value</code> value. (I hope you see a lot of value in this paragraph.)<a id="id546440" class="indexterm" href=""></a></p>

<p class="it">En primer lugar, eso significa un cambio en la definición <code class="literal">yScale</code>:</p>
<p class="p" id="first_that_mea">First, that means a change to the <code class="literal">yScale</code> definition:</p>

<pre class="programlisting" data-language="javascript" id="var_yscale__d_id3">var yScale = d3.scale.linear()
                .domain([0, d3.max(dataset, function(d) { return d.value; })])
                .range([0, h]);</pre>
<p class="it"> en la segunda línea, que solía tener simplemente d3.max (conjunto de datos), pero que sólo funciona con una simple array. Ahora que nos ' re el uso de objetos, tenemos que incluir una función de acceso que le dice d3.max() cómo llegar a los valores correctos para comparar. Así como d3.max () recorre todos los elementos del array de datos, ahora se sabe que no debe mira d (que es un objeto, y no fácilmente en comparación con otros objetos), pero d.value (un número, que es comparar fácilmente d a otros números). </p>

<p class="p" id="in_the_second_l">In the second line, we used to have simply <code class="literal">d3.max(dataset)</code>, but that only works with a simple array. Now that we’re using objects, we have to include an <span class="emphasis"><em>accessor function</em></span> that tells <code class="literal">d3.max()</code> how to get at the correct values to compare. So as <code class="literal">d3.max()</code> loops through all the elements in the <code class="literal">dataset</code> array, now it knows not to look at <code class="literal">d</code> (which is an object, and not easily compared to other objects), but <code class="literal">d.value</code> (a number, which is easily compared to other numbers).<a id="id546691" class="indexterm" href=""></a><a id="id546697" class="indexterm" href=""></a></p>


<p class="it"> Observamos también tenemos que cambiar la segunda referencia a yScale, en nuestra función de clic al día:</p>

<p class="p" id="note_we_also_ne">Note we also need to change the second reference to <code class="literal">yScale</code>, down in our click-update function:</p>


        <pre class="programlisting" data-language="javascript" id="yscaledomain">yScale.domain([0, d3.max(dataset, function(d) { return d.value; })]);</pre>

<p class="it">El siguiente, por todos lados d se utiliza para establecer los atributos, debemos Chan ge d a d .valor. Por ejemplo, esto: </p>

<p class="p" id="next_up_everyw">Next up, everywhere <code class="literal">d</code> is used to set attributes, we must change <code class="literal">d</code> to <code class="literal">d.value</code>. For example, this:</p>

        <pre class="programlisting" data-language="javascript" id="attry_fu_id1">…
.attr("y", function(d) {
    return h - yScale(d);        // &lt;-- d
})
…</pre>

        <p class="p" id="becomes_this">becomes this:</p>

        <pre class="programlisting" data-language="javascript" id="attry_fu_id2">…
.attr("y", function(d) {
    return h - yScale(d.value);  // &lt;-- d.value!
})
…</pre>


            <h4 class="title">Key functions</h4>
            <h4 class="title">Funciones de las teclas</h4>


<p class="it"> Por último, definimos una key function, que se utilizará cada vez que querramos enlazar datos a los elementos:
</p>


<p class="p" id="finally_we_def">Finally, we define a key function, to be used whenever we bind data to<a id="id547101" class="indexterm" href=""></a><a id="id547106" class="indexterm" href=""></a> elements:</p>


        <pre class="programlisting" data-language="javascript" id="var_key__funct">var key = function(d) {
    return d.key;
};</pre>

<p class="it">Tenga en cuenta que, en forma típica D3, la función toma como entrada d. A continuación, esta función muy sencilla especifica que se debe tomar el valor de la clave de cualquier objeto que se pasa d int o ella. </p>

<p class="p" id="notice_that_in">Notice that, in typical D3 form, the function takes <code class="literal">d</code> as input. Then this very simple function specifies to take the <code class="literal">key</code> value of whatever <code class="literal">d</code> object is passed into it.</p>

<p class="it"> Ahora, en los cuatro lugares en los que se unen los datos, reemplazamos esta línea:</p>

<p class="p" id="now_in_all_fou">Now, in all four places where we bind data, we replace this line:</p>


        <pre class="programlisting" data-language="javascript" id="datadataset">.data(dataset)</pre>

        <p class="p" id="with_this">with this:</p>


        <pre class="programlisting" data-language="javascript" id="datadataset__id1">.data(dataset, key)</pre>


<p class="it"> Tenga en cuenta que en lugar de definir la función de la tecla en primer lugar, a continuación, hacer referencia a ella, usted podría, por supuesto, simplemente escribir la función de la tecla directa mente en la llamada a los datos (), así: </p>


<p class="p" id="note_that_rathe">Note that rather than defining the key function first, then referencing it, you could of course simply write the key function directly into the call to <code class="literal">data()</code> like so:</p>

<pre class="programlisting" data-language="javascript" id="datadataset__id2">.data(dataset, function(d) {
    return d.key;
})</pre>

<p class="it">Tendría que escriben que cuatro veces, lo que es redundante, por lo que creo que define la función de la tecla una vez en el la parte superior es más limpio.</p>

<p class="p" id="but_in_this_cas">But in this case, you’d have to write that four times, which is redundant, so I think defining the key function once at the top is cleaner.</p>



   <p class="it">Eso ' es todo! Tenga en cuenta sus datos se unieron.</p>
        <p class="p" id="thats_it_cons">That’s it! Consider your data joined.</p>
        

    



            <h4 class="title">Exit transition</h4>
            <h4 class="title">Transición de salida</h4>
 


<p class="it"> Un último truco: Let ' s puesto el listón de salir a deslizarse hacia el lado izquierdo en lugar del derecho:</p>

<p class="p" id="one_last_tweak">One last tweak: Let’s set the exiting bar to scoot off to the left side<a id="id547422" class="indexterm" href=""></a><a id="id547430" class="indexterm" href=""></a> instead of the right:</p>

       <pre class="programlisting" data-language="javascript" id="exit_barsex_id2">//Exit…
bars.exit()
    .transition()
    .duration(500)
    .attr("x", -xScale.rangeBand())  // &lt;-- Exit stage left
    .remove();</pre>


 <p class="it">¡Estupendo! Chec k el código de ejemplo, con todos esos cambios, en 27_data_join_with_key.html . La vista inicial se muestra en la figura 9-27 se modifica.</p>

<p class="p" id="great_check_ou">Great! Check out the sample code, with all of those changes, in <span class="emphasis"><em>27_data_join_with_key.html</em></span>. The initial view shown in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch09.html#Initial-bar-chart" title="Figure 9-27. Initial bar chart">Figure 9-27</a> is unchanged.</p>

<div class="figure-contents">

<img alt="Imagen" src="/static/Fig927.png"/>


<p class="fig">Figura 9-27. Gráfico de barras Inicial</p>
<p class="fig">Figure 9-27. Initial bar chart</p>


        </div>

<p class="it">Intenta hacer clic en el texto, sin embargo, y los toboganes más a la izquierda de la barra limpiamente hacia la izquierda, todos los otros bares ' anchuras Cambiar la escala para adaptarse, y luego la barra salido se eliminan del DOM. (Una vez más, que ca n confirmar esto observando los<code class="literal">rect</code>s desaparecen uno por uno en el inspector web).</p>

<p class="p" id="try_clicking_th_id2">Try clicking the text, though, and the leftmost bar slides cleanly off to the left, all other bars’ widths rescale to fit, and then the exited bar is deleted from the DOM. (Again, you can confirm this by watching the <code class="literal">rect</code>s disappear one by one in the web inspector.)</p>


<p class="it"> La figura 9-28 muestra la vista después de retirar una barra</p>        

<p class="p" id="shows_the_view_"><a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch09.html#After-one-click" title="Figure 9-28. After one click">Figure 9-28</a> shows the view after one bar is removed.</p>



          <div>

<img alt="Imagen" src="/static/Fig928.png"/>

         
<p class="fig">Figura 9-28. Después de un clic</p>
<p class="fig">Figure 9-28. After one click</p>


        </div> 

          <div>

<img alt="Imagen" src="/static/Fig929.png"/>


<p class="fig">Figura 9-29. Después de dos clics</p>
<p class="fig">Figure 9-29. After two clicks</p>


        </div>

<p class="it">La figura 9-30 muestra los resultados después de tres clics, y después de varios clics, usted ' ll ver el resultado se muestra en la Figura 9-31.</p>

<p class="p" id="displays_the_re"><a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch09.html#After-three-clicks" title="Figure 9-30. After three clicks">Figure 9-30</a> displays the results after three clicks, and after several clicks, you’ll see the result shown in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch09.html#After-many-clicks" title="Figure 9-31. After many clicks">Figure 9-31</a>.</p>

<div>

<img alt="Imagen" src="/static/Fig930.png"/>

          

<p class="fig">Figure 9-30. After three clicks</p>
<p class="fig">Figura 9-30. Después de tres clics</p>
        </div>



          <div class="figure-contents">

<img alt="Imagen" src="/static/Fig931.png"/>

<p class="fig">Figura 9-31. Después de muchos clics</p>
<p class="fig">Figure 9-31. After many clicks</p>


        </div>
<p class="it">Esto está funcionando mejor que nunca. El único problema es que las etiquetas aren ' t que sale a la izquierda, y además no se quitan de la DOM, por lo que el desorden por el lado izquierdo de t él gráfico. Una vez más, les dejo lo que sucede; poner sus nuevos chuletas de D3 a la prueba y limpiar esas etiquetas.</p>

<p class="p" id="this_is_working">This is working better than ever. The only hitch is that the labels aren’t exiting to the left, and also are not removed from the DOM, so they clutter up the left side of the chart. Again, I leave this to you; put your new D3 chops to the test and clean up those labels.<a id="id547743" class="indexterm" href=""></a><a id="id547752" class="indexterm" href=""></a></p>


          <h3 class="title">Add and Remove: Combo Platter</h3>


<p class="it">Podríamos parar allí y estar muy satisfechos con nuestras nuevas habilidades. Pero ¿por qué no ir hasta el final, y ajustar nuestra tabla de modo que unos valores pueden añadirse y eliminarse?</p>

<p class="p" id="we_could_stop_t">We could stop there and be very satisfied with our newfound skills. But why not go all the way, and adjust our chart so data values can be added <span class="emphasis"><em>and</em></span> removed?<a id="id547804" class="indexterm" href=""></a></p>

<p class="it">Esto es más fácil de lo que parece. En primer lugar, necesitaremos de dos diferentes triggers para la interacción con el usuario. Dividiré el párrafo en dos, y daré a cada uno un ID, así que puedo decir que uno se hace clic:</p>

<p class="p" id="this_is_easier_">This is easier than you might think. First, we’ll need two different triggers for the user interaction. I’ll split the one paragraph into two, and give each a unique ID, so we can tell which one is clicked:</p>

<pre class="programlisting" data-language="html" id="p_idaddadd">&lt;p id="add"&gt;Add a new data value&lt;/p&gt;
&lt;p id="remove"&gt;Remove a data value&lt;/p&gt;</pre>


<p class="it">Más tarde, hacia abajo, donde hemos creado la función de clic, select() debe convertirse a selectAll(), ahora podemos seleccionar más de un elemento <code class="literal">p</code>:</p>


<p class="p" id="later_down_whe">Later, down where we set up the click function, <code class="literal">select()</code> must become <span class="keep-together"><code class="literal">selectAll()</code></span>, now that we’re selecting more than one <code class="literal">p</code> element:</p>


<pre class="programlisting" data-language="javascript" id="dselectallp">d3.selectAll("p")
    .on("click", function() { …</pre>


<p class="it">Ahora esta click function se une a ambos párrafos, hemos de introducir algo de lógica para contar la función para comportarse de forma diferente en función del apartado que se clickeo. Hay muchas maneras de lograr esto; Yo voy con el más sencillo. </p>


<p class="p" id="now_that_this_c">Now that this click function will be bound to both paragraphs, we have to introduce some logic to tell the function to behave differently depending on which paragraph was clicked. There are many ways to achieve this; I’ll go with the most straightforward one.</p>

<p class="it">Afortunadamente, dentro del contexto de nuestra función de clic en el anonimato, esto se refiere al elemento que se ha hecho clic - el párrafo. Así podemos obtener el valor de la identificación del elemento hecho clic al seleccionar este y preguntando usando attr():</p>

<p class="p" id="fortunately_wi">Fortunately, within the context of our anonymous click function, <code class="literal">this</code> refers to the element that was clicked—the paragraph. So we can get the ID value of the clicked element by selecting <code class="literal">this</code> and inquiring using <code class="literal">attr()</code>:</p>


      <pre class="programlisting" data-language="javascript" id="dselectthis">d3.select(this).attr("id")</pre>

<p class="it">Esto volverá "add" cuando se clickea en p#add, y "elimina" cuando se clickea en p#remove. Vamos a almacenar el valor de una variable, y lo utilizare para controlar una sentencia if: </p>

<p class="p" id="that_statement_">That statement will return <code class="literal">"add"</code> when <code class="literal">p#add</code> is clicked, and <code class="literal">"remove"</code> when <span class="keep-together"><code class="literal">p#remove</code></span> is clicked. Let’s store that value in a variable, and use it to control an <code class="literal">if</code> statement:</p>


      <pre class="programlisting" data-language="javascript" id="see_which_p_w">//See which p was clicked
var paragraphID = d3.select(this).attr("id");

//Decide what to do next
if (paragraphID == "add") {
    //Add a data value
    var maxValue = 25;
    var newNumber = Math.floor(Math.random() * maxValue);
    var lastKeyValue = dataset[dataset.length - 1].key;
    console.log(lastKeyValue);
    dataset.push({
        key: lastKeyValue + 1,
        value: newNumber
    });
} else {
    //Remove a value
    dataset.shift();
}</pre>


<p class="it"> Por lo tanto, si se clickea en p#add, se calcula un nuevo valor aleatorio, y luego buscar el valor de la clave del último elemento del conjunto de datos. Entonces se crea un nuevo objeto con una incremented key (para asegurarse de que no se hagan claves duplicadas; inserte una broma al cerrajero aquí) y el valor de datos al azar.</p>



<p class="p" id="so_if_padd_is">So, if <code class="literal">p#add</code> is clicked, we calculate a new random value, and then look up the key value of the last item in <code class="literal">dataset</code>. Then we create a new object with an incremented key (to ensure we don’t duplicate keys; insert locksmith joke here) and the random data value.</p>

<p class="it">No se necesitan cambios adicionales! La actualización del código enter/update/exit que escribimos es ya lo suficientemente flexible como para manejar la adición o eliminación de valores de datos - que es la belleza misma.</p>

<p class="p" id="no_additional_c">No additional changes are needed! The enter/update/exit code we wrote is already flexible enough to handle adding <span class="emphasis"><em>or</em></span> removing data values—that’s the beauty of it.</p>

 <p class="it">Probarlo en 28_adding_and_removing.html . Usted verá que puede hacer clic para añadir o eliminar puntos de datos a voluntad. Por supuesto, los datos del mundo real no se crean de esta manera, pero se puede imaginar estas actualizaciones de datos que se desencadenan por algún otro evento - como los datos que se refrescan en un servidor - y no los clics del ratón.</p>

<p class="p" id="try_it_out_in__id2">Try it out in <span class="emphasis"><em>28_adding_and_removing.html</em></span>. You’ll see that you can click to add or remove data points at will. Of course, real-world data isn’t created this way, but you can imagine these data updates being triggered by some other event—such as data refreshes being pulled from a server—and not mouse clicks.</p>


<p class="it">También ver 29_dynamic_labels.html , lo que es lo mismo, sólo que yo he actualizado el código para add, transition, y remove las etiquetas también.</p>

<p class="p" id="also_see__dyn">Also see <span class="emphasis"><em>29_dynamic_labels.html</em></span>, which is the same thing, only I’ve updated the code to add, transition, and remove the labels as well.</p>
           

<p><strong>Ejercicio</strong></p>

          <h3 class="title">Recap</h3>
          <h3 class="title">Resumen</h3>


<p class="it">Esa fue una gran cantidad de información! Revisemosla:</p>
      <p class="p" id="that_was_a_lot_">That was a lot of information! Let’s review:</p>


      <div class="itemizedlist" id="data_binds_da_id1">

        <ul class="itemizedlist">
<li class="it">data() se une a los elementos de datos, pero también devuelve la selección update.</li>
          <li class="p"> <code class="literal">data()</code> binds data to elements, but also returns the <span class="emphasis"><em>update selection</em></span>.<a id="id548636" class="indexterm" href=""></a> </li>
<li class="it">La selección update pueden contener selecciones de entrada y salida, a las que pueda accederse a través de enter() y exit().</li>          
          <li class="p"> The update selection can contain <span class="emphasis"><em>enter</em></span> and <span class="emphasis"><em>exit</em></span> selections, which can be accessed via <code class="literal">enter()</code> and <code class="literal">exit()</code>. </li>
<li class="it">Cuando hay más valores que los elementos , una selección enter hará referencia al marcador de posición, los elementos que aún no existen.</li>
          <li class="p"> When there are <span class="emphasis"><em>more values than elements</em></span>, an enter selection will reference the placeholder, not-yet-existing elements. </li>
<li class="it">Cuando hay más elementos que los valores, una selección de salida hará referencia a los elementos sin data.</li>
          <li class="p"> When there are <span class="emphasis"><em>more elements than values</em></span>, an exit selection will reference the elements without data. </li>
<li class="it">Los datos se unen determinando cómo los valores se corresponden con los elementos.</li>
          <li class="p"> Data joins determine how values are matched with elements. </li>
<li class="it">Por defecto, las  combinaciones de datos se llevan a cabo de acuerdo al índice, es decir, en orden de aparición.</li>
          <li class="p"> By default, data joins are performed by index, meaning in order of appearance. </li>
<li class="it"> Para obtener más control sobre los datos que se unen, puede especificar una key function.</li>
          <li class="p"> For more control over data joins, you can specify a key function. </li>

        </ul>

      </div>
<p class="it">Como nota final, en el ejemplo gráfico de barras, se utilizó la siguiente secuencia:</p>
      <p class="p" id="as_a_final_note">As a final note, in the bar chart example, we used this sequence:</p>


      <div class="orderedlist" id="enter_update_ex">

        <ol class="orderedlist" type="1">

          <li class="p"> Enter </li>

          <li class="p"> Update </li>

          <li class="p"> Exit </li>

        </ol>

      </div>
<p class="it">A pesar de esto funcionó bien para nosotros, esto no está escrito en piedra. En función de sus objetivos de diseño, es posible que desee actualizar en primer lugar, a continuación, introducir nuevos elementos, y, finalmente, salir de los anteriores. Todo depende - sólo recuerde que una vez que tenga la selección update en la mano, alcanzara para tomar selecciones enter y exit en cualquier momento. El orden en que lo hace es flexible y totalmente suyo.</p>
      <p class="p" id="although_this_w">Although this worked well for us, this order isn’t set in stone. Depending on your design goals, you might want to update first, then enter new elements, and finally exit old ones. It all depends—just remember that once you have the update selection in hand, you can reach in to grab the enter and exit selections anytime. The order in which you do so is flexible and completely up to you.</p>




<p class="it">Fantástico. Usted está en camino a convertirse en un mago del D3. Ahora llegamos a las cosas realmente divertidas: la interactividad!</p>

<p class="p" id="fantastic_you_">Fantastic. You are well on your way to becoming a D3 wizard. Now let’s get to the really fun stuff: interactivity!<a id="id548777" class="indexterm" href=""></a></p>

      

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