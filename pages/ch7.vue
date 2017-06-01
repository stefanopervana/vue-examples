<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    
    <div class="block">
    

        <h1 class="title">Chapter 7. Scales</h1>

    <p class="it"><strong>"Las escalas son las funciones que se asignan desde un dominio de entrada a un rango de salida".</strong></p>
    <p class="p" id="scales_are_fun">“Scales are functions that map from an input domain to an output range.”<a id="ix_scales" class="indexterm" href=""></a></p>

    <p class="it">Esa es la definición de escalas D3 de Mike Bostock, y no hay una manera más clara que decirlo.</p>
    <p class="p" id="thats_mike_bos">That’s <a class="ulink" href="https://github.com/mbostock/d3/wiki/Quantitative-Scales" target="_top">Mike Bostock’s definition of D3 scales</a>, and there is no clearer way to say it.<a id="id521048" class="indexterm" href=""></a></p>

    <p class="it">Los valores en cualquier conjunto de datos es poco probable que se correspondan exactamente con las medidas de píxeles para su uso en su visualización. Las escalas proporcionan una manera conveniente para mapear los valores de los datos a los nuevos valores útiles a los fines de la visualización.</p>
    <p class="p" id="the_values_in_a">The values in any dataset are unlikely to correspond exactly to pixel measurements for use in your visualization. Scales provide a convenient way to map those data values to new values useful for visualization purposes.</p>

    <p class="it">Las escalas D3 son funciones con parámetros que se definen. Una vez que se crean, se llama a la función de escala, le pasa un valor de datos, y devuelve un valor limpio de salida escalado. Se pueden definir y utilizar tantas escalas como desee.</p>
    <p class="p" id="d_scales_are_f">D3 scales are <span class="emphasis"><em>functions</em></span> with parameters that you define. Once they are created, you call the <code class="literal">scale</code> function, pass it a data value, and it nicely returns a scaled output value. You can define and use as many scales as you like.<a id="id521081" class="indexterm" href=""></a></p>

    <p class="it">Podría ser tentador pensar en una escala como algo que aparece visualmente al final de un conjunto de imágenes como de marcas de graduación, lo que indica una progresión de valores. No se deje engañar! Esas marcas de graduación son parte de un eje, que es una representación visual que representa una escala. Una escala es una relación matemática, sin representación visual directa. Lo invito a pensar en escalas y ejes como dos elementos diferentes pero relacionados entre si.</p>
    <p class="p" id="it_might_be_tem">It might be tempting to think of a scale as something that appears visually in the final image—like a set of tick marks, indicating a progression of values. <span class="emphasis"><em>Do not be fooled!</em></span> Those tick marks are part of an <span class="emphasis"><em>axis</em></span>, which is a <span class="emphasis"><em>visual representation</em></span> of a scale. A scale is a mathematical relationship, with no direct visual output. I encourage you to think of scales and axes as two different, yet related, elements.<a id="id521111" class="indexterm" href=""></a><a id="id521119" class="indexterm" href=""></a></p>

    <p class="it">Este capítulo trata solamente sobre escalas lineales, debido a que son más comunes y más fáciles de entender. Una vez que entienda las escalas lineales, las demás - ordinales, logarítmica, de raíz cuadrada, y así sucesivamente - serán un pedazito de to
    <p class="p" id="this_chapter_ad">This chapter addresses only <a class="ulink" href="https://github.com/mbostock/d3/wiki/Quantitative-Scales#wiki-linear" target="_top"><span class="emphasis"><em>linear</em></span></a> scales, because they are most common and easiest understood. Once you understand linear scales, the others—ordinal, logarithmic, square root, and so <span class="keep-together">on—will be a piece of cake.</span><a id="id521148" class="indexterm" href=""></a></p>

          <h2 class="title">Apples and Pixels</h2>

      <p class="it">Imagine que el siguiente conjunto de datos representa el número de manzanas que se venden cada mes en una fruteria de carretera:</p>
      <p class="p" id="imagine_that_th">Imagine that the following dataset represents the number of apples sold at a roadside fruit stand each month:</p>

      <pre class="programlisting" data-language="javascript" id="var_dataset___id14">var dataset = [ 100, 200, 300, 400, 500 ];</pre>

      <p class="it">En primer lugar, esta es una gran noticia, ya que el stand tiene una venta de 100 manzanas adicionales por mes! Los negocios están prosperando. Para mostrar este éxito, usted desea hacer un gráfico de barras que ilustre el ascenso empinado de las ventas de manzanas, con cada valor de datos correspondiendo a la altura de una barra.</p>
      <p class="p" id="first_of_all_t">First of all, this is great news, as the stand is selling 100 additional apples each month! Business is booming. To showcase this success, you want to make a bar chart illustrating the steep upward climb of apple sales, with each data value corresponding to the height of one bar.</p>

      <p class="it">Hasta ahora, hemos usado los valores de datos directamente como valores de visualización, haciendo caso omiso de las diferencias de unidades. Así que si se vendieron 500 manzanas, la barra correspondiente sería de 500 píxeles de alto.</p>
      <p class="p" id="until_now_wev">Until now, we’ve used data values directly as display values, ignoring unit differences. So if 500 apples were sold, the corresponding bar would be 500 pixels tall.</p>

      <p class="it">Eso podría funcionar, pero ¿qué pasa el próximo mes, cuando se vendan 600 manzanas? Y un año más tarde, cuando se vendan 1.800 manzanas? Su público tendría que comprar pantallas cada vez más grandes sólo para ser capaz de ver en toda su altura esas barras de manzana! (Mmm, barras de manzana!)</p>
      <p class="p" id="that_could_work">That could work, but what about next month, when 600 apples are sold? And a year later, when 1,800 apples are sold? Your audience would have to purchase ever-larger displays just to be able to see the full height of those very tall apple bars! (Mmm, apple bars!)</p>

      <p class="it">Aquí es donde aparecen las escalas. Debido a que las manzanas no son píxeles (que tampoco son naranjas), se necesitan escalas para comunicarse entre ellas.</p>
      <p class="p" id="this_is_where_s">This is where scales come in. Because apples are not pixels (which are also not oranges), we need scales to translate between them.</p>


          <h2 class="title">Domains and Ranges</h2>


      <p class="it">El dominio de entrada de una escala es el rango de posibles valores de datos de entrada. Dados los  datos anteriores de las manzanas, los dominios de entrada apropiados serían o bien 100 y 500 o bien 0 y 500 (los valores máximo y mínimo y el conjunto de datos).</p>
      <p class="p" id="a_scales_input">A scale’s <span class="emphasis"><em>input domain</em></span> is the range of possible input data values. Given the preceding apples data, appropriate input domains would be either 100 and 500 (the minimum and maximum values of the dataset) or 0 and 500.<a id="id521300" class="indexterm" href=""></a><a id="id521305" class="indexterm" href=""></a><a id="id521311" class="indexterm" href=""></a></p>

      <p class="it">El rango de salida de una escala es el rango de posibles valores de salida, que se utiliza comúnmente como valores indicados en unidades de píxel. El rango de salida es totalmente suyo, lo maneja usted, como el diseño de la información. Si decide que la barra de manzanas séa más corta será de 10 píxeles de alto y la más alta será de 350 píxeles de alto, entonces podría establecer un rango de salida de 10 y 350.</p>
      <p class="p" id="a_scales_outpu">A scale’s <span class="emphasis"><em>output range</em></span> is the range of possible output values, commonly used as display values in pixel units. The output range is completely up to you, as the information designer. If you decide the shortest apple bar will be 10 pixels tall, and the tallest will be 350 pixels tall, then you could set an output range of 10 and 350.</p>


      <p class="it">Por ejemplo, crear una escala con un dominio de entrada de <code class="literal">[100,500]</code> y un rango de salida de <code class="literal">[10,350]</code>. Si se entregarán el valor de entrada baja de 100 a esa escala, sería devolver su valor de más bajo rango, 10. Si usted le dio 500, escupiria en la vuelta 350. Si usted le dio 300, le entregaría 180 de nuevo a usted en una bandeja de plata. (300 está en el centro del dominio, y 180 está en el centro del rango.)</p>
      <p class="p" id="for_example_cr">For example, create a scale with an input domain of <code class="literal">[100,500]</code> and an output range of <code class="literal">[10,350]</code>. If you handed the low input value of <code class="literal">100</code> to that scale, it would return its lowest range value, <code class="literal">10</code>. If you gave it <code class="literal">500</code>, it would spit back <code class="literal">350</code>. If you gave it <code class="literal">300</code>, it would hand <code class="literal">180</code> back to you on a silver platter. (<code class="literal">300</code> is in the center of the domain, and <code class="literal">180</code> is in the center of the range.)</p>


      <p class="it">Podemos visualizar el dominio y el rango como ejes correspondientes, de lado a lado, como se muestra en la Figura 7-1.</p>
      <p class="p" id="we_can_visualiz">We can visualize the domain and range as corresponding axes, side-by-side, displayed in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch07.html#input_output_axes" title="Figure 7-1. An input domain and an output range, visualized as parallel axes">Figure 7-1</a>.</p>

<div>
            <img src="/static/fHijhiLmT1-img1.png" alt="An input domain and an output range, visualized as parallel axes"/>

        <p class="fig">Figure 7-1. An input domain and an output range, visualized as parallel axes</p>

</div>
      <p class="it">Una cosa más: para evitar que el cerebro pueda mezclar la terminología dominio de entrada y rango de salida, me gustaría proponer un poco de ejercicio. Cuando digo "de entrada", se dice "dominio". Entonces digo "de salida", y se dice "rango". Listo? Bueno:</p>


      <p class="p" id="one_more_thing_id2">One more thing: to prevent your brain from mixing up the <span class="emphasis"><em>input domain</em></span> and <span class="emphasis"><em>output range</em></span> terminology, I’d like to propose a little exercise. When I say “input,” you say “domain.” Then I say “output,” and you say “range.” Ready? Okay:</p>
      <div class="blockquote">

        <blockquote class="blockquote">

          <p class="it">¡Entrada! ¡Dominio!</p>


          <p class="p" id="input_domain_id1">Input! Domain!</p>
        </blockquote>

      </div>

      <div class="blockquote">

        <blockquote class="blockquote">

          <p class="it">¡Salida! ¡Rango!</p>


          <p class="p" id="output_range_id1">Output! Range!</p>
        </blockquote>

      </div>

      <div class="blockquote">

        <blockquote class="blockquote">

          <p class="it">¡Entrada! ¡Dominio!</p>


          <p class="p" id="input_domain_id2">Input! Domain!</p>
        </blockquote>

      </div>

      <div class="blockquote">

        <blockquote class="blockquote">

          <p class="it">¡Salida! ¡Rango!</p>


          <p class="p" id="output_range_id2">Output! Range!</p>
        </blockquote>

      </div>

      <p class="it">¿Lo tengo? Estupendo.</p>


      <p class="p" id="got_it_great">Got it? Great.</p>



        <div>

          <h2 class="title">Normalization</h2>


      </div>

      <p class="it">Si está familiarizado con el concepto de normalización, podría serle útil saber que, es una escala lineal, eso es todo lo que realmente está pasando aquí.</p>


      <p class="p" id="if_youre_famil_id3">If you’re familiar with the concept of <span class="emphasis"><em>normalization</em></span>, it might be helpful to know that, with a linear scale, that’s all that is really going on here.<a id="id521500" class="indexterm" href=""></a><a id="id521508" class="indexterm" href=""></a></p>
      <p class="it">La normalización es el proceso de asignar un valor numérico a un nuevo valor entre 0 y 1, en base a los posibles valores mínimo y máximo. Por ejemplo, con 365 días en el año, el día número 310 se asigna a aproximadamente 0,85, o 85 por ciento del camino a través del año.</p>


      <p class="p" id="normalization_i">Normalization is the process of mapping a numeric value to a new value between 0 and 1, based on the possible minimum and maximum values. For example, with 365 days in the year, day number 310 maps to about 0.85, or 85 percent of the way through the year.</p>
      <p class="it">Con escalas lineales, sólo estamos dejando a d3 manejar la matemática del proceso de normalización. El valor de entrada se normaliza de acuerdo con el dominio, y luego el valor normalizado se escala al rango de salida.</p>


      <p class="p" id="with_linear_sca">With linear scales, we are just letting D3 handle the math of the normalization process. The input value is normalized according to the domain, and then the normalized value is scaled to the output range.</p>

    <div>

          <h2 class="title">Creating a Scale</h2>


      </div>

      <p class="it">A los generadores de funciones de escala D3 se tiene acceso con <strong>d3.scale</strong> seguido por el tipo de escala que desee. Recomiendo la apertura del archivo 01_scale_test.html y escribir lo siguiente en la consola:</p>


      <p class="p" id="ds_scale_func">D3’s scale function generators are accessed with <code class="literal">d3.scale</code> followed by<a id="id521552" class="indexterm" href=""></a> the type of scale you want. I recommend opening up the sample code page <span class="emphasis"><em>01_scale_test.html</em></span> and typing each of the following into the console:</p>
      <pre class="programlisting" data-language="javascript" id="var_scale__d_id1">var scale = d3.scale.linear();</pre>

      <p class="it">¡Felicitaciones! Ahora la escala es una función a la que se le pueden pasar valores de entrada. (No se deje engañar por la <code class="literal">var</code>. Recuerde que en JavaScript, las variables pueden almacenar funciones.)</p>


      <p class="p" id="congratulations_id1">Congratulations! Now <code class="literal">scale</code> is a function to which you can pass input values. (Don’t be misled by the <code class="literal">var</code>. Remember that in JavaScript, variables can store functions.)</p>
      <pre class="programlisting" data-language="javascript" id="scale_r_id1">scale(2.5);  //Returns 2.5</pre>

      <p class="it">Debido a que no hemos establecido un dominio y un rango, esta función mapeara la entrada y la salida en una escala de 1:1. Es decir, todo lo que entra se devolverá sin cambios.</p>


      <p class="p" id="because_we_have">Because we haven’t set a domain and a range yet, this function will map input to output on a 1:1 scale. That is, whatever we input will be returned unchanged.</p>
      <p class="it">Podemos establecer el dominio de entrada de la escala para <code class="literal">100,500</code> pasando esos valores con el método de <span class="keep-together"><code class="literal">domain()</code></span> como un array. Tenga en cuenta los corchetes que indican un array:</p>


      <p class="p" id="we_can_set_the_">We can set the scale’s input domain to <code class="literal">100,500</code> by passing those values to the <span class="keep-together"><code class="literal">domain()</code></span> method as an array. Note the hard brackets indicating an array:</p>
      <pre class="programlisting" data-language="javascript" id="scaledomain">scale.domain([100, 500]);</pre>

      <p class="it">Ajuste el rango de salida de forma similar, con un <code class="literal">range()</code>:</p>


      <p class="p" id="set_the_output_">Set the output range in similar fashion, with <code class="literal">range()</code>:</p>
      <pre class="programlisting" data-language="javascript" id="scalerange">scale.range([10, 350]);</pre>

      <p class="it">Estos pasos se pueden hacer por separado, como se acaba de mostrar, o encadenados juntos en una sola línea de código:</p>


      <p class="p" id="these_steps_can">These steps can be done separately, as just shown, or chained together into one line of code:</p>
      <pre class="programlisting" data-language="javascript" id="var_scale__d_id2">var scale = d3.scale.linear()
                    .domain([100, 500])
                    .range([10, 350]);</pre>

      <p class="it">De cualquier manera, nuestra escala está lista para usarse!</p>


      <p class="p" id="either_way_our">Either way, our scale is ready to use!</p>
      <pre class="programlisting" data-language="javascript" id="scale_r_id2">scale(100);  //Returns 10
scale(300);  //Returns 180
scale(500);  //Returns 350</pre>

      <p class="it">Por lo general, se llamará a las funciones de escala dentro de un método attr() o similar, no por su propia cuenta. Vamos a modificar nuestra visualización gráfica de dispersión al usar escalas dinámicas.</p>


      <p class="p" id="typically_you_">Typically, you will call scale functions from within an <code class="literal">attr()</code> method or similar, not on their own. Let’s modify our scatterplot visualization to use dynamic scales.<a id="id522089" class="indexterm" href=""></a><a id="id522097" class="indexterm" href=""></a><a id="id522103" class="indexterm" href=""></a></p>


        <div>

          <h2 class="title">Scaling the Scatterplot</h2>

        </div>


      <p class="it">Revisitamos nuestra base de datos de la gráfica de dispersión:</p>


      <p class="p" id="to_revisit_our_">To revisit our dataset from the scatterplot:</p>
      <pre class="programlisting" data-language="javascript" id="var_dataset___id15">var dataset = [
                [5, 20], [480, 90], [250, 50], [100, 33], [330, 95],
                [410, 12], [475, 44], [25, 67], [85, 21], [220, 88]
              ];</pre>

      <p class="it">Usted recordará que este conjunto de datos es un array de arrays. Hemos trazado el primer valor de cada array en el eje <strong>x</strong>, y el segundo valor en el eje <strong>y</strong>. Vamos a empezar con el eje <strong>x</strong>.</p>


      <p class="p" id="youll_recall_t_id2">You’ll recall that this <code class="literal">dataset</code> is an array of arrays. We mapped the first value in each array onto the x-axis, and the second value onto the y-axis. Let’s start with the x-axis.</p>
      <p class="it">Con sólo echar un vistazo a los valores de <strong>x</strong>, parece que van desde 5 hasta 480, por lo que un razonable dominio de entrada a especificar podría ser <code class="literal">0,500</code>, ¿verdad?</p>


      <p class="p" id="just_by_eyeball">Just by eyeballing the <code class="literal">x</code> values, it looks like they range from 5 to 480, so a reasonable input domain to specify might be <code class="literal">0,500</code>, right?</p>
      <p class="it">¿Por qué me mira así? Oh, porque quiere mantener su código flexible y escalable, por lo que seguirá trabajando así incluso si cambian los datos en el futuro. ¡Muy inteligente! Recuerde, si estábamos construyendo un panel de datos para el stand de manzanas al borde de la carretera, nos gustaría que nuestro código pueda dar cabida al enorme crecimiento previsto de las ventas de manzanas. Nuestro chart debería funcionar igual de bien con 5 manzanas que se venden como con 5 millones.</p>


      <p class="p" id="why_are_you_giv">Why are you giving me that look? Oh, because you want to keep your code flexible and scalable, so it will continue to work even if the data changes in the future. Very smart! Remember, if we were building a data dashboard for the roadside apple stand, we’d want our code to accommodate the enormous projected growth in apple sales. Our chart should work just as well with 5 apples sold as 5 million.</p>


          <div>

            <h3 class="title">d3.min() and d3.max()</h3>


        </div>

        <p class="it">En lugar de especificar valores fijos para el dominio, podemos utilizar el conveniente array de las funciones <strong>d3.min()</strong> y <strong>d3.max()</strong> para analizar nuestro conjunto de datos sobre la marcha. Por ejemplo, este metodo loopea a través de cada uno de los valores de <code class="literal">x</code> en nuestras arrays y devuelve el valor mayor</p>


        <p class="p" id="instead_of_spec">Instead of specifying fixed values for the domain, we can use the convenient array functions <code class="literal">d3.min()</code> and <code class="literal">d3.max()</code> to analyze our data set on the fly. For example, this loops through each of the x values in our arrays and returns the value of the greatest one:</p>
        <pre class="programlisting" data-language="javascript" id="dmaxdataset_id1">d3.max(dataset, function(d) {
    return d[0];  //References first value in each subarray.
    Referencia el primer valor en cada subarray.
});</pre>

        <p class="it">Ese código devolverá el valor 480, porque 480 es el valor de <code class="literal">x</code> más grande de nuestro conjunto de datos. Voy a explicar cómo funciona.</p>


        <p class="p" id="that_code_will_">That code will return the value 480, because 480 is the largest x value in our dataset. Let me explain how it works.</p>
        <p class="it">Tanto los metodos <code class="literal">min()</code> y <code class="literal">max()</code> funcionan de la misma manera, y pueden tener uno o dos argumentos. El primer argumento debe ser una referencia al rango de valores que se desean evaluar, que es el conjunto de datos, en este caso. Si usted tiene un array simple, unidimensional de valores numéricos, como [7, 8, 4, 5, 2], entonces es obvio cómo comparar los valores de uno contra el otro, y no se necesita el segundo argumento. Por ejemplo:</p>


        <p class="p" id="both_min_and_">Both <code class="literal">min()</code> and <code class="literal">max()</code> work the same way, and they can take either one or two arguments. The first argument must be a reference to the array of values you want evaluated, which is <code class="literal">dataset</code>, in this case. If you have a simple, one-dimensional array of numeric values, like <code class="literal">[7, 8, 4, 5, 2]</code>, then it’s obvious how to compare the values against each other, and no second argument is needed. For example:</p>
        <pre class="programlisting" data-language="javascript" id="var_simpledatas">var simpleDataset = [7, 8, 4, 5, 2];
d3.max(simpleDataset);  // Returns 8</pre>

        <p class="it">La función <code class="literal">max()</code> simplemente recorre cada valor en el array, e identifica el más grande.</p>


        <p class="p" id="the_max_funct">The <code class="literal">max()</code> function simply loops through each value in the array, and identifies the largest one.</p>
        <p class="it">Sin embargo, nuestro conjunto de datos no es sólo un conjunto de números; es una array de arrays. Llamando a <strong>d3.max(dataset)</strong> puede producir resultados inesperados:</p>


        <p class="p" id="but_our_dataset">But our <code class="literal">dataset</code> is not just an array of numbers; it is an array of arrays. Calling <code class="literal">d3.max(dataset)</code> might produce unexpected results:</p>
        <pre class="programlisting" data-language="javascript" id="var_dataset___id16">var dataset = [
                [5, 20], [480, 90], [250, 50], [100, 33], [330, 95],
                [410, 12], [475, 44], [25, 67], [85, 21], [220, 88]
              ];
d3.max(dataset);  // Returns [85, 21].  What???</pre>

        <p class="it">Al decir a max() los valores específicos que queremos comparar, debemos incluir un segundo argumento, una <strong>función accesoria</strong>:</p>


        <p class="p" id="to_tell_max_w">To tell <code class="literal">max()</code> which <span class="emphasis"><em>specific</em></span> values we want compared, we must include a second argument, an <span class="emphasis"><em>accessor function</em></span>:</p>
        <pre class="programlisting" data-language="javascript" id="dmaxdataset_id2">d3.max(dataset, function(d) {
    return d[0];
});</pre>

        <p class="it">La <strong>función accesoria</strong> es una función anónima con la que <strong>max()</strong> maneja cada valor en la array de datos, uno a la vez, como <strong>d</strong>. La función accesoria especifica <strong>cómo acceder</strong> al valor que se utilizará para la comparación.</p>


        <p class="p" id="the_accessor_fu">The accessor function is an anonymous function to which <code class="literal">max()</code> hands<a id="id523137" class="indexterm" href=""></a><a id="id523142" class="indexterm" href=""></a> off each value in the data array, one at a time, as <code class="literal">d</code>. The accessor function specifies <span class="emphasis"><em>how to access</em></span> the value to be used for the comparison.</p>
        <p class="it"> En este caso, nuestra array de datos es el conjunto de datos, y queremos comparar solamente los valores de <strong>x</strong>, que son los primeros valores de cada subconjunto, es decir, en la posición [0]. Por lo tanto nuestra función accesoria es la siguiente:</p>


        <p class="p">In this case, our data array is <code class="literal">dataset</code>, and we want to compare only the x values, which are the first values in each subarray, meaning in position <code class="literal">[0]</code>. So our accessor function looks like this:</p>
        <pre class="programlisting" data-language="javascript" id="functiond__r_id2">function(d) {
    return d[0];  //Return the first value in each subarray. Devuelve el primer valor en cada subarray.
}</pre>

        <p class="it">Tenga en cuenta que esto es sospechosamente similar a la sintaxis que usamos cuando generamos nuestros scatterplot circles, que también utilizan funciones anónimas para recuperar y devolver valores :</p>


        <p class="p" id="note_that_this_">Note that this looks suspiciously similar to the syntax we used when generating our scatterplot circles, which also used anonymous functions to retrieve and return values:</p>
        <pre class="programlisting" data-language="javascript" id="attrcx_fun_id2">.attr("cx", function(d) {
    return d[0];
})
.attr("cy", function(d) {
    return d[1];
})</pre>

        <p class="it">Este es un patrón D3 común. Pronto va a estar muy cómodo con todo tipo de funciones anónimas merodeando por todo su código.</p>


        <p class="p" id="this_is_a_commo">This is a common D3 pattern. Soon you will be very comfortable with all manner of anonymous functions crawling all over your code.</p>

          <div>

            <h3 class="title">Setting Up Dynamic Scales</h3>

          </div>


        <p class="it">Para elaborar lo que hemos cubierto, vamos a crear la función de escala para nuestro eje <strong>x</strong>:</p>


        <p class="p" id="putting_togethe">Putting together what we’ve covered, let’s create the scale function for<a id="id523424" class="indexterm" href=""></a><a id="id523432" class="indexterm" href=""></a> our x-axis:</p>
        <pre class="programlisting" data-language="javascript" id="var_xscale__d_id1">var xScale = d3.scale.linear()
                     .domain([0, d3.max(dataset, function(d) { return d[0]; })])
                     .range([0, w]);</pre>

        <p class="it">En primer lugar, note que la he denominado xScale. Por supuesto, puede asignar nombres a las escalas según su deseo, pero un nombre como xScale me ayuda a recordar lo que hace esta función.</p>


        <p class="p" id="first_notice_t">First, notice that I named it <code class="literal">xScale</code>. Of course, you can name your scales whatever you want, but a name like <code class="literal">xScale</code> helps me remember what this function does.</p>
        <p class="it">En segundo lugar, observe que tanto el dominio y el rango se especifican como arrays de dos valores entre corchetes.</p>


        <p class="p" id="second_notice_">Second, notice that both the domain and range are specified as two-value arrays in hard brackets.</p>
        <p class="it">En tercer lugar, le aviso que puse el extremo más bajo del dominio de entrada a 0. (Alternativamente, se puede usar min() para calcular un valor dinámico.) El extremo superior del dominio se establece en el valor máximo en el conjunto de datos (que se encuentra actualmente en 480, pero podría cambiar en el futuro).</p>


        <p class="p" id="third_notice_t">Third, notice that I set the low end of the input domain to 0. (Alternatively, you could use <code class="literal">min()</code> to calculate a dynamic value.) The upper end of the domain is set to the maximum value in <code class="literal">dataset</code> (which is currently 480, but could change in the future).</p>
        <p class="it">Por último, tenga en cuenta que el rango de salida se pone a <code class="literal">0</code> y <code class="literal">w</code>, y nos da el ancho del SVG.</p>


        <p class="p" id="finally_observ">Finally, observe that the output range is set to <code class="literal">0</code> and <code class="literal">w</code>, the SVG’s width.</p>
        <p class="it">Vamos a utilizar un código muy similar para crear la función de escala para el eje <strong>y</strong>:</p>


        <p class="p" id="well_use_very_">We’ll use very similar code to create the scale function for the y-axis:</p>
        <pre class="programlisting" data-language="javascript" id="var_yscale__d_id1">var yScale = d3.scale.linear()
                     .domain([0, d3.max(dataset, function(d) { return d[1]; })])
                     .range([0, h]);</pre>

        <p class="it">Tenga en cuenta que la función <code class="literal">max()</code> se referencia a <code class="literal">d[1]</code>, el valor <strong>y</strong> de cada subarray. Además, el extremo superior del <code class="literal">range()</code> se establece en <code class="literal">h</code> en lugar de <code class="literal">w</code>.</p>


        <p class="p" id="note_that_the_m">Note that the <code class="literal">max()</code> function here references <code class="literal">d[1]</code>, the y value of each subarray. Also, the upper end of <code class="literal">range()</code> is set to <code class="literal">h</code> instead of <code class="literal">w</code>.</p>
        <p class="it">Las funciones de la escala están en su lugar! Ahora todo lo que tenemos que hacer es usarlas.</p>


        <p class="p" id="the_scale_funct">The scale functions are in place! Now all we need to do is use them.</p>


          <div>

            <h3 class="title">Incorporating Scaled Values</h3>

          </div>

        <p class="it">Revisando nuestro código de dispersión, que ahora simplemente modifica la línea original donde creamos un <code class="literal">circle</code> para cada valor de datos:</p>


        <p class="p" id="revisiting_our_">Revisiting our scatterplot code, we now simply modify the original line<a id="id523930" class="indexterm" href=""></a> where we created a <code class="literal">circle</code> for each data value:</p>
        <pre class="programlisting" data-language="javascript" id="attrcx_fun_id3">.attr("cx", function(d) {
    return d[0];  //Returns original value bound from dataset. Devuelve el valor original enlazado desde el conjunto de datos
})</pre>

        <p class="it">para devolver un valor escalado (en lugar del valor original):</p>


        <p class="p" id="to_return_a_sca">to return a scaled value (instead of the original value):</p>
        <pre class="programlisting" data-language="javascript" id="attrcx_fun_id4">.attr("cx", function(d) {
    return xScale(d[0]);  //Returns scaled value
})</pre>

        <p class="it">Del mismo modo, para el siguiente eje <strong>y</strong>, :</p>


        <p class="p" id="likewise_for_t">Likewise, for the y-axis, this:</p>
        <pre class="programlisting" data-language="javascript" id="attrcy_fun_id1">.attr("cy", function(d) {
    return d[1];
})</pre>

        


        <p class="p" id="is_modified_as">is modified as:</p>
        <pre class="programlisting" data-language="javascript" id="attrcy_fun_id2">.attr("cy", function(d) {
    return yScale(d[1]);
})</pre>

        <p class="it">Por si fuera poco, vamos a hacer el mismo cambio en el que establecer las coordenadas para las etiquetas de texto, por lo que estas líneas:</p>


        <p class="p" id="for_good_measur">For good measure, let’s make the same change where we set the coordinates for the text labels, so these lines:</p>
        <pre class="programlisting" data-language="javascript" id="attrx_func_id7">.attr("x", function(d) {
    return d[0];
})
.attr("y", function(d) {
    return d[1];
})</pre>

        <p class="it">se convierten en estas :</p>


        <p class="p" id="become_this">become this:</p>
        <pre class="programlisting" data-language="javascript" id="attrx_func_id8">.attr("x", function(d) {
    return xScale(d[0]);
})
.attr("y", function(d) {
    return yScale(d[1]);
})</pre>

        <p class="it">Y ahí estamos!</p>


        <p class="p" id="and_there_we_ar">And there we are!</p>
        <p class="it">Chequee el código de trabajo en 02_scaled_plot.html. Visualmente, el resultado en la Figura 7-2 es decepcionantemente similar a nuestro diagrama de dispersión original! Sin embargo, estamos haciendo más progresos que podrían ser aparentes.</p>


        <p class="p" id="check_out_the_w">Check out the working code in <span class="emphasis"><em>02_scaled_plot.html</em></span>. Visually, the result in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch07.html#Scatterplot_using_x_and_y_scales" title="Figure 7-2. Scatterplot using x and y scales">Figure 7-2</a> is disappointingly similar to our original scatterplot! Yet we are making more progress than might be apparent.<a id="id524683" class="indexterm" href=""></a></p>
        <div>

              <img src="/static/fHijhiLmT1-img2.png" alt="Scatterplot using x and y scales"/>



          <p class="fig">Figure 7-2. Scatterplot using x and y scales</p>


        </div>



          <h2 class="title">Refining the Plot</h2>


      <p class="it">Usted puede haber notado que los valores de <strong>y</strong> son más pequeños en la parte superior de la trama, y los valores de <strong>y</strong> son de mayor tamaño hacia la parte inferior. Ahora que estamos utilizando escalas D3, es super fácil revertir eso, así los valores mayores van arriba, como era de esperar. Es sólo una cuestión de cambiar el rango de salida de <code class="literal">yScale</code>  de:</p>


      <p class="p" id="you_might_have__id2">You might have noticed that smaller y values are at the top of the plot, and the larger y values are toward the bottom. Now that we’re using D3 scales, it’s super easy to reverse that, so greater values are higher up, as you would expect. It’s just a matter of changing the output range of <code class="literal">yScale</code> from:</p>


      <pre class="programlisting" data-language="javascript" id="range_h">.range([0, h]);</pre>

      


      <p class="p" id="to">to:</p>



      <pre class="programlisting" data-language="javascript" id="rangeh_">.range([h, 0]);</pre>

      <p class="it">Ver 03_scaled_plot_inverted.html para el código que resulta en la Figura 7-3.</p>


      <p class="p" id="see__scaled_p">See <span class="emphasis"><em>03_scaled_plot_inverted.html</em></span> for the code that results in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch07.html#Scatterplot_with_y_scale_inverted" title="Figure 7-3. Scatterplot with y scale inverted">Figure 7-3</a>.</p>

      <div>

            <img src="/static/fHijhiLmT1-img3.png" alt="Scatterplot with y scale inverted"/>


        <p class="fig">Figure 7-3. Scatterplot with <strong>y</strong> scale inverted</p>

        <p class="fig">Diagrama de dispersión <strong>y</strong> con escala invertida</p>

      </div>

      <p class="it">Sí, una entrada más pequeña para <code class="literal">yScale</code> producirá un valor de salida más grande, lo que empuja los círculos y los elementos de texto hacia abajo, más cerca de la base de la imagen. Yo sé, es casi demasiado fácil!</p>

      <p class="p" id="yes_now_a_smal">Yes, now a <span class="emphasis"><em>smaller</em></span> input to <code class="literal">yScale</code> will produce a <span class="emphasis"><em>larger</em></span> output value, thereby pushing those <code class="literal">circle</code>s and <code class="literal">text</code> elements down, closer to the base of the image. I know, it’s almost too easy!</p>

      
      <p class="it">Sin embargo, algunos elementos están siendo cortados. Vamos a introducir una variable padding:</p>

      <p class="p" id="yet_some_elemen">Yet some elements are getting cut off. Let’s introduce a <code class="literal">padding</code> variable:</p>

      
      <pre class="programlisting" data-language="javascript" id="var_padding___id1">var padding = 20;</pre>

      <p class="it">A continuación, vamos a incorporar la cantidad de <code class="literal">padding</code> (relleno) cuando se ajusta el rango de ambas escalas. Esto ayudará a empujar nuestros elementos, lejos de los bordes de la SVG, para evitar que se recorte.</p>

      <p class="p" id="then_well_inco">Then we’ll incorporate the <code class="literal">padding</code> amount when setting the range of both scales. This will help push our elements in, away from the edges of the SVG, to prevent them from being clipped.<a id="id524978" class="indexterm" href=""></a></p>

      
      <p class="it">El rango para <code class="literal">xScale</code> fue <code class="literal">range([0, w])</code>, pero ahora es:</p>

      <p class="p" id="the_range_for_x">The range for <code class="literal">xScale</code> was <code class="literal">range([0, w])</code>, but now it’s:</p>

      
      <pre class="programlisting" data-language="javascript" id="rangepadding_id1">.range([padding, w - padding]);</pre>

      <p class="it">El rango para yScale fue el rango ([h, 0]), pero ahora es:</p>

      <p class="p" id="the_range_for_y">The range for <code class="literal">yScale</code> was <code class="literal">range([h, 0])</code>, but now it’s:</p>

      
      <pre class="programlisting" data-language="javascript" id="rangeh__pad">.range([h - padding, padding]);</pre>

      <p class="it">Esto nos debe proveer de 20 píxeles de espacio extra a la izquierda, derecha, arriba, y los bordes inferiores de la SVG. Y lo hace (ver Figura 7-4)!</p>

      <p class="p" id="this_should_pro">This should provide us with 20 pixels of extra room on the left, right, top, and bottom edges of the SVG. And it does (see <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch07.html#Scatterplot_with_padding" title="Figure 7-4. Scatterplot with padding">Figure 7-4</a>)!</p>

                <div>

            <img src="/static/fHijhiLmT1-img4.png" alt="Scatterplot with padding"/>        <p class="fig">Figure 7-4. Scatterplot with padding</p>


      </div>

      <p class="it">Sin embargo, las etiquetas de texto en el extremo derecho todavía están cortadas, así que el doble de la cantidad de relleno de <code class="literal">xScale</code> en el lado derecho para multiplicar por dos para conseguir el resultado que se muestra en la Figura 7-5:</p>

      <p class="p" id="but_the_text_la">But the text labels on the far right are still getting cut off, so I’ll double the amount of <code class="literal">xScale</code>’s padding on the right side by multiplying by two to achieve the result shown in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch07.html#Scatterplot_with_more_padding" title="Figure 7-5. Scatterplot with more padding">Figure 7-5</a>:</p>

      
      <pre class="programlisting" data-language="javascript" id="rangepadding_id2">.range([padding, w - padding * 2]);</pre>

      <div>


            <img src="/static/fHijhiLmT1-img5.png" alt="Scatterplot with more padding"/>


        <p class="fig">Figure 7-5. Scatterplot with more padding</p>

        <p class="fig">Figura 7-5. Diagrama de dispersión con más padding</p>

      </div>        <p class="it">La forma en que he introducido el padding aquí es simple, pero no elegante. Eventualmente, usted podría querer más control sobre la cantidad de padding en cada lado de los gráficos (arriba, derecha, abajo, izquierda), y es útil para estandarizar la forma de especificar los valores en los proyectos. Aunque no he utilizado el margen por convención de Mike Bostock de los ejemplos de código de este libro, recomiendo echar un vistazo para ver si podría funcionar para usted.</p>

        <p class="p" id="the_way_ive_in_id2">The way I’ve introduced padding here is simple, but not elegant. Eventually, you’ll want more control over how much padding is on each side of your charts (top, right, bottom, left), and it’s useful to standardize how you specify those values across projects. Although I haven’t used <a class="ulink" href="http://bl.ocks.org/3019563" target="_top">Mike Bostock’s margin convention</a> for the code samples in this book, I recommend taking a look to see if it could work for you.</p>

              <p class="it">¡Mejor! Hacer referencia al código hasta ahora en 04_scaled_plot_padding.html. Pero hay un cambio más que me gustaría hacer. En lugar de establecer el radio de cada círculo como la raíz cuadrada de su valor (que era un poco un truco, y no visualmente útil), porqué no crear otra escala personalizada?</p>

      <p class="p" id="better_referen">Better! Reference the code so far in <span class="emphasis"><em>04_scaled_plot_padding.html</em></span>. But there’s one more change I’d like to make. Instead of setting the radius of each <code class="literal">circle</code> as the square root of its y value (which was a bit of a hack, and not visually useful), why not create another custom scale?</p>

      
      <pre class="programlisting" data-language="javascript" id="var_rscale__d">var rScale = d3.scale.linear()
                     .domain([0, d3.max(dataset, function(d) { return d[1]; })])
                     .range([2, 5]);</pre>

      <p class="it">A continuación, estableceremos el radio como el siguiente:</p>

      <p class="p" id="then_setting_t">Then, setting the radius looks like this:</p>

      
      <pre class="programlisting" data-language="javascript" id="attrr_func_id3">.attr("r", function(d) {
    return rScale(d[1]);
});</pre>

      <p class="it">Esto es emocionante porque estamos garantizando que nuestros valores de radio siempre estarán dentro del rango de 2,5. (O casi siempre, véase la referencia al metodo <code class="literal">clamp()</code> más adelante.) Por lo tanto los valores de datos de 0 (mínimo de la entrada) obtendrán círculos de radio 2 (o un diámetro de 4 píxeles). El valor de datos muy grande obtendrá un círculo de radio 5 (diámetro de 10 píxeles).</p>

      <p class="p" id="this_is_excitin_id2">This is exciting because we are guaranteeing that our radius values will <span class="emphasis"><em>always</em></span> fall within the range of <code class="literal">2,5</code>. (Or <span class="emphasis"><em>almost</em></span> always; see reference to <code class="literal">clamp()</code> later.) So data values of <code class="literal">0</code> (the minimum input) will get circles of radius <code class="literal">2</code> (or a diameter of 4 pixels). The very largest data value will get a circle of radius <code class="literal">5</code> (diameter of 10 pixels).</p>

      
      <p class="it">Voila: La figura 7-6 muestra nuestra primera escala utilizada para una propiedad visual que no sea un valor del eje. (Ver 05_scaled_plot_radii.html.)</p>

      <p class="p" id="voila_shows_ou">Voila: <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch07.html#Scatterplot_with_scaled_radii" title="Figure 7-6. Scatterplot with scaled radii">Figure 7-6</a> shows our first scale used for a visual property other than an axis value. (See <span class="emphasis"><em>05_scaled_plot_radii.html</em></span>.)</p>

      
      <div>            <img src="/static/fHijhiLmT1-img6.png" alt="Scatterplot with scaled radii"/>


        <p class="fig">Figure 7-6. Scatterplot with scaled radio</p>


      </div>

      <p class="it">Por último, en caso de que el poder de escalas aún no se ha fundido en su mente, me gustaría añadir una variedad más al conjunto de datos: [600, 150].</p>

      <p class="p" id="finally_just_i">Finally, just in case the power of scales hasn’t yet blown your mind, I’d like to add one more array to the dataset: <code class="literal">[600, 150]</code>.</p>

      
      <p class="it">¡Boom! Chequee el archivo 06_scaled_plot_big.html. Observe cómo todos los viejos puntos en la Figura 7-7 mantuvieron sus posiciones relativas, pero han migrado más juntos, hacia abajo y hacia la izquierda, para dar cabida a los recién llegados en la esquina superior derecha.</p>

      <p class="p" id="boom_check_out">Boom! Check out <span class="emphasis"><em>06_scaled_plot_big.html</em></span>. Notice how all the old points in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch07.html#Scatterplot_with_big_numbers_added" title="Figure 7-7. Scatterplot with big numbers added">Figure 7-7</a> maintained their relative positions but have migrated closer together, down and to the left, to accommodate the newcomer in the top-right corner.</p>

      
      <div>            <img src="/static/fHijhiLmT1-img7.png" alt="Scatterplot with big numbers added"/>

  

        <p class="fig">Figure 7-7. Scatterplot with big numbers added</p>

        <p class="fig">Figura 7-7. Diagrama de dispersión con grandes números añadidos</p>

      </div>

      <p class="it">Y ahora, una última revelación: ahora podemos cambiar fácilmente el tamaño de nuestra SVG, y escalarla en consecuencia. En la Figura 7-8, he aumentado el valor de <strong>h</strong> de 100 a 300 y no se hizo ningún otro cambio.</p>

      <p class="p" id="and_now_one_fi">And now, one final revelation: we can now very easily change the size of our SVG, and <span class="emphasis"><em>everything scales accordingly</em></span>. In <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch07.html#Large_scaled_scatterplot" title="Figure 7-8. Large, scaled scatterplot">Figure 7-8</a>, I’ve increased the value of <code class="literal">h</code> from <code class="literal">100</code> to <code class="literal">300</code> and made <span class="emphasis"><em>no other changes</em></span>.</p>

        
        <div>            <img src="/static/fHijhiLmT1-img8.png" alt="Large, scaled scatterplot"/>        <p class="fig">Figure 7-8. Large, scaled scatterplot</p>

        <p class="fig">Figura 7-8. Gran diagrama de dispersión reducido</p>

      </div>

      <p class="it">Boom, de nuevo! Ver 07_scaled_plot_large.html. Con suerte, usted está viendo esto para darse cuenta: no más horas nocturnas para ajustar su código porque el cliente decide que el gráfico debe ser de 800 píxeles de ancho en lugar de 600. Sí, obtendrá más horas de sueño debido a mí (y los brillantes métodos incorporados de D3). El estar bien descansado es una ventaja competitiva. Me lo puedes agradecer después.</p>

      <p class="p" id="boom_again_se">Boom, again! See <span class="emphasis"><em>07_scaled_plot_large.html</em></span>. Hopefully, you are seeing this and realizing: no more late nights tweaking your code because the client decided the graphic should be 800 pixels wide instead of 600. Yes, you will get more sleep because of me (and D3’s brilliant built-in methods). Being well-rested is a competitive advantage. You can thank me later.</p>

                <h2 class="title">Other Methods</h2>
      <p class="it"><code class="literal">d3.scale.linear()</code>tiene varios otros métodos útiles que merecen una breve mención aquí:</p>

      <p class="p" id="dscalelinear"><code class="literal">d3.scale.linear()</code> has several other handy methods that deserve a brief<a id="id525812" class="indexterm" href=""></a> mention here:</p>

      
      <div class="variablelist" id="nice_this_tel">

        <dl class="variablelist">

          <dt><span class="term"> <a class="ulink" href="http://bit.ly/ZR9Si0" target="_top"><code class="literal">nice()</code></a> </span></dt>

          <dd> This tells the scale to take whatever input domain that you gave to <code class="literal">range()</code> and expand both ends to the nearest round value. From the D3 wiki: “For example, <span class="keep-together">for a domain of</span> [0.20147987687960267, 0.996679553296417], the nice domain is [0.2, 1].” This is useful for normal people, who are not computers and find it hard to read numbers like 0.20147987687960267. </dd>

          <dd>Esto le dice a la escala de tomar cualquier dominio de entrada que le dio al <code class="literal">range()</code> y ampliar ambos extremos para el valor circundante más cercano. Tomado de la D3 wiki: "Por ejemplo, para un dominio de [,20147987687960267, ,996679553296417], el buen dominio es [0,2, 1]". Esto es útil para la gente normal, que no son ordenadores y les resulta difíciles de leer números como 0.20147987687960267.</dd>

          <dt><span class="term"> <a class="ulink" href="http://bit.ly/Z2ZLke" target="_top"><code class="literal">rangeRound()</code></a> </span></dt>

          <dd> Use <code class="literal">rangeRound()</code> in place of <code class="literal">range()</code>, and all values output by the scale will be rounded to the nearest whole number. This is useful if you want shapes to have exact pixel values, to avoid the fuzzy edges that could arise with antialiasing. </dd>

          <dd>Use <code class="literal">rangeRound()</code> en lugar de <code class="literal">range()</code>, y todos los valores de salida por la escala se redondearán al número entero más próximo. Esto es útil si desea que las formas tengan valores exactos de píxeles, para evitar los bordes borrosos que podrían surgir con el antialiasing.</dd>

          <dt><span class="term"> <a class="ulink" href="http://bit.ly/12h7uTf" target="_top"><code class="literal">clamp()</code></a> </span></dt>

          <dd> By default, a linear scale <span class="emphasis"><em>can</em></span> return values outside of the specified range. For example, if given a value outside of its expected input domain, a scale will return a number also outside of the output range. Calling <code class="literal">clamp(true)</code> on a scale, however, forces all output values to be within the specified range. This means excessive values will be rounded to the range’s low or high value (whichever is nearest). </dd>

          <dd>Por defecto, una escala lineal puede devolver valores fuera del rango especificado. Por ejemplo, si se le da un valor fuera de su dominio esperado de entrada, una escala devolverá un número también fuera del rango de salida. Llamando a la función <code class="literal">clamp(true)</code> en una escala, sin embargo, obliga a todos los valores de salida para estar dentro del rango especificado. Esto significa que los valores excesivos serán redondeados a bajo o alto valor del rango (el que sea más cercano).</dd>

        </dl>

      </div>

      <p class="it">  Para utilizar cualquiera de estos métodos especiales, simplemente cambiar por ellos en la cadena en la que se define la función original escala. Por ejemplo, para utilizar <code class="literal">nice()</code>:</p>

      <p class="p" id="to_use_any_of_t">To use any of these special methods, just tack them onto the chain in which you define the original scale function. For example, to use <code class="literal">nice()</code>:</p>

      
      <pre class="programlisting" data-language="javascript" id="var_scale__d_id3">var scale = d3.scale.linear()
                    .domain([0.123, 4.567])
                    .range([0, 500])
                    .nice();</pre>        <div>

          <h2 class="title">Other Scales</h2>


      <p class="it">Además de las escalas lineales (discutidas anteriormente), D3 tiene varios otros métodos de escala incorporadas:</p>

      <p class="p" id="in_addition_to_">In addition to<a id="id526084" class="indexterm" href=""></a> <a class="ulink" href="https://github.com/mbostock/d3/wiki/Quantitative-Scales#wiki-linear" target="_top"><code class="literal">linear</code> scales</a> (discussed earlier), D3 has several other built-in scale methods:</p>

      
      <div class="variablelist" id="sqrt_a_square_r">

        <dl class="variablelist">

          <dt><span class="term"> <a class="ulink" href="http://bit.ly/15ePKWb" target="_top"><code class="literal">sqrt</code></a> </span></dt>

          <dd> A square root scale. </dd>

          <dd style="font-style: italic;"> La escala de raíz cuadrada. </dd>

          <dt><span class="term"> <a class="ulink" href="http://bit.ly/XBKvuq" target="_top"><code class="literal">pow</code></a> </span></dt>

          <dd> A power scale (good for the gym, er, I mean, useful when working with exponential series of values, as in “to the power of” some exponent). </dd>

          <dd style="font-style: italic;"> Una escala de potencia (buena para el gimnasio, quiero decir, útil cuando se trabaja con la serie exponencial de los valores, como en "el poder de" algún exponente). </dd>

          <dt><span class="term"> <a class="ulink" href="http://bit.ly/YTuRdX" target="_top"><code class="literal">log</code></a> </span></dt>

          <dd> A logarithmic scale. </dd>

          <dt><span class="term"> <a class="ulink" href="http://bit.ly/ZEJXtP" target="_top"><code class="literal">quantize</code></a> </span></dt>

          <dd> A linear scale with discrete values for its output range, for when you want to sort data into “buckets”. </dd>

          <dd style="font-style: italic;">Una escala lineal con valores discretos para su rango de salida, para cuando se desea ordenar los datos en "cubos".</dd>

          <dt><span class="term"> <a class="ulink" href="http://bit.ly/XxlWlr" target="_top"><code class="literal">quantile</code></a> </span></dt>

          <dd> Similar to <code class="literal">quantize</code>, but with discrete values for its input domain (when you already have “buckets”). </dd>

          <dd style="font-style: italic;">Similares para <code class="literal">quantize</code>, pero con valores discretos para su dominio de entrada (cuando ya se tienen "cubos"). </dd>

          <dt><span class="term"> <a class="ulink" href="http://bit.ly/XWSVvB" target="_top"><code class="literal">ordinal</code></a> </span></dt>

          <dd> Ordinal scales use nonquantitative values (like category names) for output; perfect for comparing apples and oranges. </dd>

          <dd style="font-style: italic;">Las escalas ordinales utilizan valores no cuantitativos (como nombres de las categorías) para la salida; perfecto para comparar manzanas y naranjas.</dd>

          <dt><span class="term"> <a class="ulink" href="http://bit.ly/X6O0fT" target="_top"><code class="literal">d3.scale.category10()</code></a>, <a class="ulink" href="http://bit.ly/Wn3QPH" target="_top"><code class="literal">d3.scale.category20()</code></a>, <a class="ulink" href="http://bit.ly/13bmamp" target="_top"><code class="literal">d3.scale.category20b()</code></a>, and <a class="ulink" href="http://bit.ly/Wn3Saf" target="_top"><code class="literal">d3.scale.category20c()</code></a> </span></dt>

          <dd> Handy preset ordinal scales that output either 10 or 20 categorical colors. </dd>

          <dd style="font-style: italic;">Práctico ordinal preestablecido de escalas que produce 10 ó 20 colores categóricos.</dd>

          <dt><span class="term"> <a class="ulink" href="http://bit.ly/Xxm6tc" target="_top"><code class="literal">d3.time.scale()</code></a> </span></dt>

          <dd> A scale method for date and time values, with special handling of ticks for dates. </dd>

          <dd style="font-style: italic;">Un método de escala para los valores de fecha y hora, con un manejo especial de las fechas.</dd>

        </dl>

      </div>

      <p class="it"> Ahora que ha dominado el poder de las escalas, es el momento de expresarlo visualmente, sí, con los ejes!</p>

      <p class="p" id="now_that_you_ha">Now that you have mastered the power of scales, it’s time to express them visually as, yes, <span class="emphasis"><em>axes</em></span>!</p>

            <h1 name="5ef3" id="5ef3" class="graf graf--h3 graf--leading graf--title">Introducing d3-scale by Mick Bostock</h1>

      <p class="it">Me gustaría que D3 se convirtiese en la biblioteca estándar de visualización de datos: no sólo una herramienta que se utiliza directamente para visualizar los datos de la escritura de código, sino también un conjunto de herramientas que se basa een un software más potente.</p>

      <p class="p">I’d like D3 to become the standard library of data visualization: not just a tool you use directly to visualize data by writing code, but also a suite of tools that underpin more powerful software.</p>      <p class="it">Con este fin, D3 propugna abstracciones que son útiles para cualquier aplicación de visualización y rechaza la tiranía de los gráficos.</p>

      <p class="p"><span class="markup--quote markup--p-quote is-other" name="anon_e093b1359fb0" data-creator-ids="anon">To this end, D3 espouses abstractions that are useful for any visualization application and rejects the tyranny of charts.</span></p>

     <div>

<img alt="Imagen" src="/static/5WXgdV3lBY-img2.png"/>

</div>

      <p name="c608" id="c608" class="graf graf--p graf-after--figure">As Leland Wilkinson wrote in <a href="https://books.google.com/books?id=_kRX4LoFfGQC" data-href="https://books.google.com/books?id=_kRX4LoFfGQC" class="markup--anchor markup--p-anchor" rel="nofollow"><em class="markup--em markup--p-em">The Grammar of Graphics</em></a>,</p>
<blockquote class="it">Si nos esforzamos en desarrollar una cartografía en lugar de un programa de gráficos, vamos a lograr dos cosas. En primer lugar, inevitablemente, a ofrecer un menor número de charts que la gente quiere. En segundo lugar, el paquete no tendrá ninguna estructura profunda. Nuestro programa de ordenador será innecesariamente compleja, porque vamos a dejar de reutilizar objetos o rutinas que funcionan de manera similar en diferentes tablas. Y no tendremos manera de añadir nuevos charts a nuestro sistema sin generar código nuevo complejo. El diseño elegante nos obliga a pensar en una teoría de gráficos y no gráficos.</blockquote>
      <blockquote name="54e6" id="54e6" class="p">If we endeavor to develop a charting instead of a graphing program, we will accomplish two things. First, we inevitably will offer fewer charts than people want. Second, our package will have no deep structure. Our computer program will be unnecessarily complex, because we will fail to reuse objects or routines that function similarly in different charts. And we will have no way to add new charts to our system without generating complex new code. Elegant design requires us to think about a theory of graphics, not charts.</blockquote>

      <p class="it">Si la visualización está construyendo "representaciones visuales de datos abstractos para amplificar la cognición ", entonces tal vez el concepto más importante en D3 es la escala , que asigna una dimensión de datos abstractos para una variable visual.</p>
<p name="4f37" id="4f37" class="graf graf--p graf-after--blockquote">If visualization is constructing “visual representations of abstract data to <a href="https://books.google.com/books?id=wdh2gqWfQmgC" data-href="https://books.google.com/books?id=wdh2gqWfQmgC" class="markup--anchor markup--p-anchor" rel="nofollow">amplify cognition</a>”, then perhaps the most important concept in D3 is the <em class="markup--em markup--p-em">scale</em>, which maps a dimension of abstract data to a visual variable.</p>

      
<p class="it">Y ahora las escalas están disponibles en una biblioteca, independiente, d3-scale.</p>
<p name="544f" id="544f" class="p">And now scales are available in a standalone library, <a href="https://github.com/d3/d3-scale" data-href="https://github.com/d3/d3-scale" class="markup--anchor markup--p-anchor" rel="nofollow">d3-scale</a>.</p>

<p class="it">Pero que es una "dimensión" de los datos? O una "variable visual"? Considere una tabla de datos, como en una hoja de cálculo. Cada fila de la tabla es un vector, y cada columna es una dimensión. Una dimensión es sólo un atributo denominado cuyos valores tienen un significado particular, tal como un precio en dólares.</p>
<p name="b83f" id="b83f" class="p">But what is a “dimension” of data? Or a “visual variable”? Consider a table of data, as in a spreadsheet. Each row in the table is a vector, and each column is a dimension. A dimension is just a named attribute whose values have a particular meaning, such as a price in dollars.</p>

      <div>


<img alt="Imagen" src="/static/5WXgdV3lBY-img4.png" />


      </div>
<p class="it">Por lo general pensamos en dimensiones como espacial y cuantitativa, tal como una posición en el espacio representado por números reales ⟨ x, y, z ⟩. Sin embargo, con los datos abstractos también existen dimensiones no cuantitativos; por ejemplo, la calidad de corte de diamante (regular, bueno, muy bueno, ideal) es ordinal, mientras que la forma del diamante de corte (la princesa, redondo, marquesa, etc. ) es categórico.</p>
<p name="c433" id="c433" class="graf graf--p graf-after--figure">We typically think of dimensions as spatial and quantitative, such as a position in space represented by real numbers ⟨<em class="markup--em markup--p-em">x, y, z</em>⟩. Yet with abstract data there are also non-quantitative dimensions; for example, diamond cut quality (fair, good, very good, ideal) is ordinal, while diamond cut shape (princess, round, marquise, <em class="markup--em markup--p-em">etc.</em>) is categorical.</p>

<p class="it">Las variables visuales son mejor explicadas por Jacques Bertin en Semiología de Gráficos . Describió la forma gráfica de marcas (digamos, puntos en un diagrama de dispersión) se pueden representar los datos utilizando la posición plana ⟨ x, y ⟩ y una dimensión luminosa z :</p>

<p name="fee3" id="fee3" class="graf graf--p graf-after--p">Visual variables are best explained by Jacques Bertin in <a href="http://esripress.esri.com/display/index.cfm?fuseaction=display&amp;websiteID=190" data-href="http://esripress.esri.com/display/index.cfm?fuseaction=display&amp;websiteID=190" class="markup--anchor markup--p-anchor" rel="nofollow"><em class="markup--em markup--p-em">Semiology of Graphics</em></a><em class="markup--em markup--p-em">.</em> He described how graphical marks (say, dots in a scatterplot) can represent data using planar position ⟨<em class="markup--em markup--p-em">x, y</em>⟩ and a luminous dimension <em class="markup--em markup--p-em">z</em>:</p>





<p class="tipit">Dentro del plano de una marca puede ser en la parte superior o la parte inferior, a la derecha oa la izquierda. El ojo percibe dos dimensiones independientes a lo largo de X e Y, que se distinguen de forma ortogonal. Una variación en la energía luminosa produce tercera dimensión en Z, que es independiente de X e Y ...</p>


<p class="tip">Within the plane a mark can be at the top or the bottom, to the right or the left. The eye perceives two independent dimensions along X and Y, which are distinguished orthogonally. A variation in light energy produces a third dimension in Z, which is independent of X and Y…</p>

<p class="tipit">El ojo es sensible, a lo largo de la dimensión Z, a 6 variables independientes visuales, que pueden ser superpuestas sobre las figuras planas: el tamaño de las marcas, su valor, textura, color, orientación y forma. Pueden representar diferencias (≠), similitudes (≡), una orden cuantificada (Q), o una orden de no cuantificados (O), y pueden expresar los grupos, las jerarquías, o movimientos verticales.</p>

<p class="tip">The eye is sensitive, along the Z dimension, to 6 independent visual variables, which can be superimposed on the planar figures: the size of the marks, their value, texture, color, orientation, and shape. They can represent differences (≠), similarities (≡), a quantified order (Q), or a nonquantified order (O), and can express groups, hierarchies, or vertical movements.</p>


      <div>


<img alt="Imagen" src="/static/5WXgdV3lBY-img6.png" />



        <p class="fig">From <a href="http://esripress.esri.com/display/index.cfm?fuseaction=display&amp;websiteID=190" data-href="http://esripress.esri.com/display/index.cfm?fuseaction=display&amp;websiteID=190" class="markup--anchor markup--figure-anchor" rel="nofollow"><em class="markup--em markup--figure-em">Semiology of Graphics</em></a>, colorized by the author.</p>

      </div>
<p class="it">Por lo tanto, una escala es una función que toma un valor abstracto de datos, tales como la masa de un diamante en quilates, y devuelve un valor visual tal como la posición horizontal de un punto en píxeles. Con dos escalas (uno para cada x y y ), tenemos la base para un diagrama de dispersión.</p>
      <p name="0ce2" id="0ce2" class="graf graf--p graf-after--figure">Thus, a scale is a function that takes an <em class="markup--em markup--p-em">abstract value</em> of data, such as the mass of a diamond in carats, and returns a <em class="markup--em markup--p-em">visual value</em> such as the horizontal position of a dot in pixels. With two scales (one each for <em class="markup--em markup--p-em">x</em> and <em class="markup--em markup--p-em">y</em>), we have the basis for a scatterplot.</p>



      <div>



  <img alt="Imagen" src="/static/5WXgdV3lBY-img8.png" />




        <p class="fig">The relationship between diamond mass <em class="markup--em markup--figure-em">and</em> price. <a href="http://bl.ocks.org/mbostock/ebb45892cc6ec5e6c902" data-href="http://bl.ocks.org/mbostock/ebb45892cc6ec5e6c902" class="markup--anchor markup--figure-anchor" rel="nofollow">View source.</a></p>

      </div>


    <pre name="0405556" id="040rt2" class="graf tgraf--pre graf-after--p">&lt;!DOCTYPE html&gt;
&lt;meta charset="utf-8"&gt;
&lt;style&gt;

canvas,
svg {
  position: absolute;
}

.grid .tick line {
  stroke: #fff;
}

.grid--x .domain {
  fill: #e7e7e7;
  stroke: none;
}

.grid--y .domain,
.axis .domain {
  display: none;
}

&lt;/style&gt;
&lt;svg width="960" height="960"&gt;&lt;/svg&gt;
&lt;canvas width="960" height="960"&gt;&lt;/canvas&gt;
&lt;script src="//d3js.org/d3.v4.0.0-alpha.49.min.js"&gt;&lt;/script&gt;
&lt;script&gt;

var canvas = d3.select("canvas").node(),
    context = canvas.getContext("2d");

var margin = {top: 20, right: 20, bottom: 30, left: 40},
    width = canvas.width - margin.left - margin.right,
    height = canvas.height - margin.top - margin.bottom;

var svg = d3.select("svg").append("g")
    .attr("transform", "translate(" + margin.left + "," + margin.top + ")");

var x = d3.scaleLinear()
    .rangeRound([0, width - 2]);

var y = d3.scaleLinear()
    .rangeRound([height - 2, 0]);

context.translate(margin.left, margin.top);
context.globalCompositeOperation = "multiply";
context.fillStyle = "rgba(60,180,240,0.6)";

d3.tsv("diamonds.tsv", type, function(error, diamonds) {
  if (error) throw error;

  x.domain(d3.extent(diamonds, function(d) { return d.carat; }));
  y.domain(d3.extent(diamonds, function(d) { return d.price; }));

  svg.append("g")
      .attr("class", "grid grid--x")
      .call(d3.axisLeft(y)
          .tickSize(-width)
          .tickFormat(""));

  svg.append("g")
      .attr("class", "grid grid--y")
      .attr("transform", "translate(0," + height + ")")
      .call(d3.axisBottom(x)
          .tickSize(-height)
          .tickFormat(""));

  svg.append("g")
      .attr("class", "axis axis--y")
      .call(d3.axisLeft(y)
          .ticks(10, "s"))
    .append("text")
      .attr("x", 10)
      .attr("y", 10)
      .attr("dy", ".71em")
      .attr("fill", "#000")
      .attr("font-weight", "bold")
      .attr("text-anchor", "start")
      .text("Price (US$)");

  svg.append("g")
      .attr("class", "axis axis--x")
      .attr("transform", "translate(0," + height + ")")
      .call(d3.axisBottom(x))
    .append("text")
      .attr("x", width - 10)
      .attr("y", -10)
      .attr("dy", "-.35em")
      .attr("fill", "#000")
      .attr("font-weight", "bold")
      .attr("text-anchor", "end")
      .text("Mass (carats)");

  d3.shuffle(diamonds);
  var t = d3.timer(function() {
    for (var i = 0, n = 500, d; i &lt; n; ++i) {
      if (!(d = diamonds.pop())) return t.stop();
      context.fillRect(x(d.carat), y(d.price), Math.max(2, x(d.carat + 0.01) - x(d.carat)), 2);
    }
  });
});

function type(d) {
  d.carat = +d.carat;
  d.price = +d.price;
  return d;
}

&lt;/script&gt;</pre>

<p class="it">Para ilustrar cómo funcionan las escalas, imaginar cómo se puede calcular x e y para cada punto por encima. Teniendo en cuenta algunos valores derivados de los datos (minCarat, maxCarat, minprice, maxprice) y algunas del tamaño del gráfico (anchura, altura), que podría hacer algo como esto:</p>

      <p class="p">To illustrate how scales work, imagine how you might compute <em class="markup--em markup--p-em">x</em> and <em class="markup--em markup--p-em">y</em> for each dot above. Given some values derived from data (minCarat, maxCarat, minPrice, maxPrice) and some from the chart size (width, height), you might do something like this:</p>

      <pre name="0402" id="0402" class="graf graf--pre graf-after--p">function x(carat) {  return (carat - minCarat)      / (maxCarat - minCarat)      * width;}</pre>

      <pre name="a3d9" id="a3d9" class="graf graf--pre graf-after--pre">function y(price) {  return height      - (price - minPrice)      / (maxPrice - minPrice)      * height;}</pre>
<p class="it">El diamante más ligero se coloca en el borde izquierdo de la tabla, el diamante más pesado se coloca en el borde derecho de la tabla, y así sucesivamente. Tenga en cuenta que el rango de la Y -scale se invierte ya que los sistemas gráficos ponen el origen en la esquina superior izquierda, mientras que los diagramas de dispersión pusieron en la parte inferior izquierda.
</p>
      <p class="p">The lightest diamond is placed at the chart’s left edge, the heaviest diamond is placed at the chart’s right edge, and so on. Note that the range of the <em class="markup--em markup--p-em">y</em>-scale is inverted because graphics systems put the origin in the top-left corner whereas scatterplots put it in the bottom-left.</p>
<p class="it">Al igual que el anterior, escalas cuantitativas de D3 son funciones configuradas por dos intervalos. La entrada de dominio es un intervalo en la dimensión resumen de los datos, a menudo el grado de los valores observados. La salida de gama es un intervalo en la variable visual, tales como el área visible definido por el tamaño del gráfico.</p>
      <p class="p">Like the above, D3’s quantitative scales are functions configured by two intervals. The input <em class="markup--em markup--p-em">domain</em> is an interval in the abstract dimension of data, often the <a href="https://github.com/d3/d3-array#extent" data-href="https://github.com/d3/d3-array#extent" class="markup--anchor markup--p-anchor" rel="nofollow">extent</a> of the observed values. The output <em class="markup--em markup--p-em">range</em> is an interval in the visual variable, such as the visible area defined by the chart size.</p>

      <pre name="492b" id="492b" class="graf graf--pre graf-after--p">var x = d3_scale.linear()    .domain(d3_array.extent(data, function(d) { return d.carat; }))    .range([0, width]);</pre>

      <pre name="a16c" id="a16c" class="graf graf--pre graf-after--pre">var y = d3_scale.linear()    .domain(d3_array.extent(data, function(d) { return d.price; }))    .range([height, 0]);</pre>
<p class="it">Pero las escalas hacen mucho más que aritmética básica!
</p>
      <p class="p">But scales do much more than basic arithmetic!</p>
<p class="it">Por un lado, ahora es trivial para aplicar transformaciones cuantitativas: reemplazar un lineal de escala con una logarítmica o poder escala. Una escala lineal es una buena opción por defecto, ya que preserva la proporcionalidad, pero un registro o la escala prisionero de guerra puede ayudar a la diferenciación de los datos que no se distribuye de manera uniforme. (Entre las escalas también son buenos para mostrar el cambio .)</p>
      <p class="p">For one, it is now trivial to apply quantitative transformations: replace a <a href="https://github.com/d3/d3-scale#linear" data-href="https://github.com/d3/d3-scale#linear" class="markup--anchor markup--p-anchor" rel="nofollow">linear</a> scale with a <a href="https://github.com/d3/d3-scale#log-scales" data-href="https://github.com/d3/d3-scale#log-scales" class="markup--anchor markup--p-anchor" rel="nofollow">logarithmic</a> or <a href="https://github.com/d3/d3-scale#power-scales" data-href="https://github.com/d3/d3-scale#power-scales" class="markup--anchor markup--p-anchor" rel="nofollow">power</a> scale. A linear scale is a good default choice because it preserves proportionality, but a log or pow scale may aid the differentiation of data that is not uniformly distributed. (Log scales are also good for <a href="http://bl.ocks.org/mbostock/c69f5960c6b1a95b6f78" data-href="http://bl.ocks.org/mbostock/c69f5960c6b1a95b6f78" class="markup--anchor markup--p-anchor" rel="nofollow">showing change</a>.)</p>



      <div>


<img alt="Imagen" src="/static/5WXgdV3lBY-img10.png" />



        <p class="fig">The previous scatterplot modified to use log scales. <a href="http://bl.ocks.org/mbostock/c3034eef9d73b5fdf274" data-href="http://bl.ocks.org/mbostock/c3034eef9d73b5fdf274" class="markup--anchor markup--figure-anchor" rel="nofollow">View source.</a></p>


    </div>
    <pre>&lt;!DOCTYPE html&gt;
&lt;meta charset="utf-8"&gt;
&lt;style&gt;

canvas,
svg {
  position: absolute;
}

.grid .tick line {
  stroke: #fff;
}

.grid--x .domain {
  fill: #e7e7e7;
  stroke: none;
}

.grid--y .domain,
.axis .domain {
  display: none;
}

&lt;/style&gt;
&lt;svg width="960" height="960"&gt;&lt;/svg&gt;
&lt;canvas width="960" height="960"&gt;&lt;/canvas&gt;
&lt;script src="//d3js.org/d3.v4.0.0-alpha.49.min.js"&gt;&lt;/script&gt;
&lt;script&gt;

var canvas = d3.select("canvas").node(),
    context = canvas.getContext("2d");

var margin = {top: 20, right: 20, bottom: 30, left: 40},
    width = canvas.width - margin.left - margin.right,
    height = canvas.height - margin.top - margin.bottom;

var svg = d3.select("svg").append("g")
    .attr("transform", "translate(" + margin.left + "," + margin.top + ")");

var x = d3.scaleLog()
    .rangeRound([0, width - 2]);

var y = d3.scaleLog()
    .rangeRound([height - 2, 0]);

context.translate(margin.left, margin.top);
context.globalCompositeOperation = "multiply";
context.fillStyle = "rgba(60,180,240,0.6)";

d3.tsv("diamonds.tsv", type, function(error, diamonds) {
  if (error) throw error;

  x.domain(d3.extent(diamonds, function(d) { return d.carat; }));
  y.domain(d3.extent(diamonds, function(d) { return d.price; }));

  svg.append("g")
      .attr("class", "grid grid--x")
      .call(d3.axisLeft(y)
          .tickSize(-width)
          .tickFormat(""));

  svg.append("g")
      .attr("class", "grid grid--y")
      .attr("transform", "translate(0," + height + ")")
      .call(d3.axisBottom(x)
          .tickSize(-height)
          .tickFormat(""));

  svg.append("g")
      .attr("class", "axis axis--y")
      .call(d3.axisLeft(y)
          .ticks(20, ".1s"))
    .append("text")
      .attr("x", 10)
      .attr("y", 10)
      .attr("dy", ".71em")
      .attr("fill", "#000")
      .attr("font-weight", "bold")
      .attr("text-anchor", "start")
      .text("Price (US$)");

  svg.append("g")
      .attr("class", "axis axis--x")
      .attr("transform", "translate(0," + height + ")")
      .call(d3.axisBottom(x)
          .ticks(20, ".1f"))
    .append("text")
      .attr("x", width - 10)
      .attr("y", -10)
      .attr("dy", "-.35em")
      .attr("fill", "#000")
      .attr("font-weight", "bold")
      .attr("text-anchor", "end")
      .text("Mass (carats)");

  d3.shuffle(diamonds);
  var t = d3.timer(function() {
    for (var i = 0, n = 500, d; i &lt; n; ++i) {
      if (!(d = diamonds.pop())) return t.stop();
      context.fillRect(x(d.carat), y(d.price), Math.max(2, x(d.carat + 0.01) - x(d.carat)), 2);
    }
  });
});

function type(d) {
  d.carat = +d.carat;
  d.price = +d.price;
  return d;
}

&lt;/script&gt;</pre>

<p class="it">Para dos, escalas aliviar el tedio de dibujo ejes legibles por generar y dar formato agradable, valores redondos ( garrapatas ) del dominio. Garrapatas de una escala son de tipo adecuado: por ejemplo, el registro de las garrapatas por encima están espaciados uniformemente dentro de cada potencia de diez, mientras que una escala de tiempo utiliza intervalos de calendario.
</p>
      <p class="p">For two, scales alleviate the tedium of drawing legible axes by <a href="https://github.com/d3/d3-scale#continuous_ticks" data-href="https://github.com/d3/d3-scale#continuous_ticks" class="markup--anchor markup--p-anchor" rel="nofollow">generating</a> and <a href="https://github.com/d3/d3-scale#continuous_tickFormat" data-href="https://github.com/d3/d3-scale#continuous_tickFormat" class="markup--anchor markup--p-anchor" rel="nofollow">formatting</a> nice, round values (<em class="markup--em markup--p-em">ticks</em>) from the domain. A scale’s ticks are type-appropriate: for example, the log ticks above are uniformly-spaced within each power of ten, while a time scale uses calendar intervals.</p>
<p class="it">La mayoría de las escalas son bidireccionales : se puede invertir el mapeo de representación visual de nuevo a los datos abstractos, facilitando la interacción. Por ejemplo, un intervalo de cepillado en píxeles se puede invertir para extraer datos para la consulta.</p>
      <p class="p">Most scales are bidirectional<em class="markup--em markup--p-em">: </em>you can <a href="https://github.com/d3/d3-scale#continuous_invert" data-href="https://github.com/d3/d3-scale#continuous_invert" class="markup--anchor markup--p-anchor" rel="nofollow">invert</a> the mapping from visual representation back to abstract data, facilitating interaction. For example, a brushed interval in pixels can be inverted to abstract data for querying.</p>

      <div>

<img alt="Imagen" src="/static/241_1.png" />



        <p class="fig">Brushing a scatterplot matrix. <a href="http://bl.ocks.org/mbostock/4063663" data-href="http://bl.ocks.org/mbostock/4063663" class="markup--anchor markup--figure-anchor" rel="nofollow">View source.</a></p>

      </div>
      <pre>&lt;!DOCTYPE html&gt;
&lt;meta charset="utf-8"&gt;
&lt;style&gt;

svg {
  font: 10px sans-serif;
  padding: 10px;
}

.axis,
.frame {
  shape-rendering: crispEdges;
}

.axis line {
  stroke: #ddd;
}

.axis path {
  display: none;
}

.cell text {
  font-weight: bold;
  text-transform: capitalize;
}

.frame {
  fill: none;
  stroke: #aaa;
}

circle {
  fill-opacity: .7;
}

circle.hidden {
  fill: #ccc !important;
}

.extent {
  fill: #000;
  fill-opacity: .125;
  stroke: #fff;
}

&lt;/style&gt;
&lt;body&gt;
&lt;script src="//d3js.org/d3.v3.min.js"&gt;&lt;/script&gt;
&lt;script&gt;

var width = 960,
    size = 230,
    padding = 20;

var x = d3.scale.linear()
    .range([padding / 2, size - padding / 2]);

var y = d3.scale.linear()
    .range([size - padding / 2, padding / 2]);

var xAxis = d3.svg.axis()
    .scale(x)
    .orient("bottom")
    .ticks(6);

var yAxis = d3.svg.axis()
    .scale(y)
    .orient("left")
    .ticks(6);

var color = d3.scale.category10();

d3.csv("flowers.csv", function(error, data) {
  if (error) throw error;

  var domainByTrait = {},
      traits = d3.keys(data[0]).filter(function(d) { return d !== "species"; }),
      n = traits.length;

  traits.forEach(function(trait) {
    domainByTrait[trait] = d3.extent(data, function(d) { return d[trait]; });
  });

  xAxis.tickSize(size * n);
  yAxis.tickSize(-size * n);

  var brush = d3.svg.brush()
      .x(x)
      .y(y)
      .on("brushstart", brushstart)
      .on("brush", brushmove)
      .on("brushend", brushend);

  var svg = d3.select("body").append("svg")
      .attr("width", size * n + padding)
      .attr("height", size * n + padding)
    .append("g")
      .attr("transform", "translate(" + padding + "," + padding / 2 + ")");

  svg.selectAll(".x.axis")
      .data(traits)
    .enter().append("g")
      .attr("class", "x axis")
      .attr("transform", function(d, i) { return "translate(" + (n - i - 1) * size + ",0)"; })
      .each(function(d) { x.domain(domainByTrait[d]); d3.select(this).call(xAxis); });

  svg.selectAll(".y.axis")
      .data(traits)
    .enter().append("g")
      .attr("class", "y axis")
      .attr("transform", function(d, i) { return "translate(0," + i * size + ")"; })
      .each(function(d) { y.domain(domainByTrait[d]); d3.select(this).call(yAxis); });

  var cell = svg.selectAll(".cell")
      .data(cross(traits, traits))
    .enter().append("g")
      .attr("class", "cell")
      .attr("transform", function(d) { return "translate(" + (n - d.i - 1) * size + "," + d.j * size + ")"; })
      .each(plot);

  // Titles for the diagonal.
  cell.filter(function(d) { return d.i === d.j; }).append("text")
      .attr("x", padding)
      .attr("y", padding)
      .attr("dy", ".71em")
      .text(function(d) { return d.x; });

  cell.call(brush);

  function plot(p) {
    var cell = d3.select(this);

    x.domain(domainByTrait[p.x]);
    y.domain(domainByTrait[p.y]);

    cell.append("rect")
        .attr("class", "frame")
        .attr("x", padding / 2)
        .attr("y", padding / 2)
        .attr("width", size - padding)
        .attr("height", size - padding);

    cell.selectAll("circle")
        .data(data)
      .enter().append("circle")
        .attr("cx", function(d) { return x(d[p.x]); })
        .attr("cy", function(d) { return y(d[p.y]); })
        .attr("r", 4)
        .style("fill", function(d) { return color(d.species); });
  }

  var brushCell;

  // Clear the previously-active brush, if any.
  function brushstart(p) {
    if (brushCell !== this) {
      d3.select(brushCell).call(brush.clear());
      x.domain(domainByTrait[p.x]);
      y.domain(domainByTrait[p.y]);
      brushCell = this;
    }
  }

  // Highlight the selected circles.
  function brushmove(p) {
    var e = brush.extent();
    svg.selectAll("circle").classed("hidden", function(d) {
      return e[0][0] &gt; d[p.x] || d[p.x] &gt; e[1][0]
          || e[0][1] &gt; d[p.y] || d[p.y] &gt; e[1][1];
    });
  }

  // If the brush is empty, select all circles.
  function brushend() {
    if (brush.empty()) svg.selectAll(".hidden").classed("hidden", false);
  }
});

function cross(a, b) {
  var c = [], n = a.length, m = b.length, i, j;
  for (i = -1; ++i &lt; n;) for (j = -1; ++j &lt; m;) c.push({x: a[i], i: i, y: b[j], j: j});
  return c;
}

&lt;/script&gt;</pre>
<p class="it">Y hay escalas para datos ordinales y categóricas. La banda de escala, por ejemplo, simplifica el cálculo de anchos de las barras y posiciones, lo que permite el relleno configurable, la alineación y redondeo.</p>
      <p class="p">And there are scales for ordinal and categorical data. The <a href="https://github.com/d3/d3-scale#band-scales" data-href="https://github.com/d3/d3-scale#band-scales" class="markup--anchor markup--p-anchor" rel="nofollow">band</a> scale, for instance, simplifies the calculation of bar widths and positions, allowing configurable padding, alignment and rounding.</p>

      <div>

<img alt="Imagen" src="/static/1-cIYJvJvpPlsC0i1eD69nqw.png" /></div>

       

        <p class="p">The frequency of English letters. <a href="http://bl.ocks.org/mbostock/946ddf8a32b3b660ffd8" data-href="http://bl.ocks.org/mbostock/946ddf8a32b3b660ffd8" class="markup--anchor markup--figure-anchor" rel="nofollow">View source.</a></p>

  
      <pre>&lt;!DOCTYPE html&gt;
&lt;meta charset="utf-8"&gt;
&lt;canvas width="960" height="500"&gt;&lt;/canvas&gt;
&lt;script src="//d3js.org/d3.v4.0.0-alpha.4.min.js"&gt;&lt;/script&gt;
&lt;script&gt;

var canvas = document.querySelector("canvas"),
    context = canvas.getContext("2d");

var margin = {top: 20, right: 20, bottom: 30, left: 40},
    width = canvas.width - margin.left - margin.right,
    height = canvas.height - margin.top - margin.bottom;

var x = d3.scaleBand()
    .rangeRound([0, width])
    .padding(0.1);

var y = d3.scaleLinear()
    .rangeRound([height, 0]);

context.translate(margin.left, margin.top);

d3.requestTsv("data.tsv", function(d) {
  d.frequency = +d.frequency;
  return d;
}, function(error, data) {
  if (error) throw error;

  x.domain(data.map(function(d) { return d.letter; }));
  y.domain([0, d3.max(data, function(d) { return d.frequency; })]);

  var yTickCount = 10,
      yTicks = y.ticks(yTickCount),
      yTickFormat = y.tickFormat(yTickCount, "%");

  context.beginPath();
  x.domain().forEach(function(d) {
    context.moveTo(x(d) + x.bandwidth() / 2, height);
    context.lineTo(x(d) + x.bandwidth() / 2, height + 6);
  });
  context.strokeStyle = "black";
  context.stroke();

  context.textAlign = "center";
  context.textBaseline = "top";
  x.domain().forEach(function(d) {
    context.fillText(d, x(d) + x.bandwidth() / 2, height + 6);
  });

  context.beginPath();
  yTicks.forEach(function(d) {
    context.moveTo(0, y(d) + 0.5);
    context.lineTo(-6, y(d) + 0.5);
  });
  context.strokeStyle = "black";
  context.stroke();

  context.textAlign = "right";
  context.textBaseline = "middle";
  yTicks.forEach(function(d) {
    context.fillText(yTickFormat(d), -9, y(d));
  });

  context.beginPath();
  context.moveTo(-6.5, 0 + 0.5);
  context.lineTo(0.5, 0 + 0.5);
  context.lineTo(0.5, height + 0.5);
  context.lineTo(-6.5, height + 0.5);
  context.strokeStyle = "black";
  context.stroke();

  context.save();
  context.rotate(-Math.PI / 2);
  context.textAlign = "right";
  context.textBaseline = "top";
  context.font = "bold 10px sans-serif";
  context.fillText("Frequency", -10, 10);
  context.restore();

  context.fillStyle = "steelblue";
  data.forEach(function(d) {
    context.fillRect(x(d.letter), y(d.frequency), x.bandwidth(), height - y(d.frequency));
  });
});

&lt;/script&gt;</pre>


<p class="it">Sin embargo, las escalas no son sólo para posicionamiento; son para el cálculo de cualquier variable de visual. Las escalas se pueden interpolar tamaños símbolo, tamaños de fuente, colores, grosores de trazo en varios espacios de color, transformaciones geométricas, formas e incluso objetos están anidadas. A continuación, una escala representa cantidad por medio de la orientación angular, con los números pequeños reclinado a la izquierda (\) y un gran número inclina a la derecha (/). Esto revela el comportamiento de un algoritmo de clasificación en una serie de números:</p>

      <p name="431f" id="431f" class="graf graf--p graf-after--figure">Yet scales are not just for positioning; they are for computing <em class="markup--em markup--p-em">any</em> visual variable. Scales can <a href="https://github.com/d3/d3-scale#continuous_interpolate" data-href="https://github.com/d3/d3-scale#continuous_interpolate" class="markup--anchor markup--p-anchor" rel="nofollow">interpolate</a> symbol sizes, font sizes, stroke widths, colors in various color spaces, geometric transforms, shapes and even deeply-nested objects. Below, a scale represents quantity using angular orientation, with small numbers leaning left (\) and large numbers leaning right (/). This reveals the behavior of a sorting algorithm on an array of numbers:</p>



      <div>
<img alt="Imagen" src="/static/1-IUn5Qb-VneCovMfH8PqAsA.png" />



        <p class="fig">Visualizing quicksort. From <a href="http://bost.ocks.org/mike/algorithms/" data-href="http://bost.ocks.org/mike/algorithms/" class="markup--anchor markup--figure-anchor" rel="nofollow">Visualizing Algorithms.</a></p>

      </div>

<p class="it">A continuación, una escala de raíz cuadrada calcula el radio apropiado para que el área de la burbuja de cada condado es proporcional al número de personas que viven allí:</p>
      <p name="8fa8" id="8fa8" class="graf graf--p graf-after--figure">Below, a square-root scale computes the appropriate radius so that the area of each county’s bubble is proportional to the number of people living there:</p>

  



      <div>

<img alt="Imagen" src="/static/1-K1xOjX_qc_6TtP7hU_o5hA.png" />

      
<p class="fig">Población en 2008. Desde vamos a hacer un mapa de la burbuja.</p>
        <p class="fig">Population in 2008. From <a href="http://bost.ocks.org/mike/bubble-map/" data-href="http://bost.ocks.org/mike/bubble-map/" class="markup--anchor markup--figure-anchor" rel="nofollow">Let’s Make a Bubble Map</a>.</p>

      </div>





      <p name="8c61" id="8c61" class="p">Below, a comparison of perceptually-uniform sequential color scales used for a choropleth of unemployment rate:</p>
<p class="it">A continuación, una comparación de escalas de color secuenciales perceptualmente uniformes utilizados para una coropletas de tasa de desempleo:</p>


      <div>

<img alt="Imagen" src="/static/1-0ptljP-upBOkJG0_8o05zg.png" />
 </div>

      <div>


<img alt="Imagen" src="/static/1-bG7dyONArCRSUSJFgFFehA.png" />

        </div>
 <div>
      

          <img alt="Imagen" src="/static/1-MAOWJ7_NI5yVrYDUzcRJug.png" />

        
<p class="fig">El desempleo en 2008, utilizando el magma, viridis y cubehelix. Los colores más oscuros indican una tasa de desempleo. </p>
        <p class="fig">Unemployment in 2008, using magma, viridis and cubehelix. Darker colors indicate a higher unemployment rate. <a href="http://bl.ocks.org/mbostock/4060606" data-href="http://bl.ocks.org/mbostock/4060606" class="markup--anchor markup--figure-anchor" rel="nofollow">View source.</a></p>

      </div>



<p class="it">Incluso puede crear escalas trozos de colores divergentes, o cuantificar las escalas para la aplicación de las pausas discretos para los datos continuos.</p>
      <p name="b841" id="b841" class="p">You can even create piecewise scales for diverging colors, or quantize scales for applying discrete breaks to continuous data.</p>

      
<p class="it">Por lo tanto, probarlo ! Y echa un vistazo a los otros nuevos módulos D3 , también, por ejemplo d3-tiempo , d3-formato , y d3-forma.</p>
      <p name="1580" id="1580" class="p">So, <a href="https://github.com/d3/d3-scale" data-href="https://github.com/d3/d3-scale" class="markup--anchor markup--p-anchor" rel="nofollow">try it out</a>! And check out the other <a href="https://github.com/d3" data-href="https://github.com/d3" class="markup--anchor markup--p-anchor" rel="nofollow">new D3 modules</a>, too, such as <a href="https://github.com/d3/d3-time" data-href="https://github.com/d3/d3-time" class="markup--anchor markup--p-anchor" rel="nofollow">d3-time</a>, <a href="https://github.com/d3/d3-format" data-href="https://github.com/d3/d3-format" class="markup--anchor markup--p-anchor" rel="nofollow">d3-format</a>, and <a href="https://medium.com/@mbostock/introducing-d3-shape-73f8367e6d12" data-href="https://medium.com/@mbostock/introducing-d3-shape-73f8367e6d12" class="markup--anchor markup--p-anchor">d3-shape</a>.</p>



      
<p class="it">Feliz Escalamiento!</p>
      <p name="e0d7" id="e0d7" class="graf graf--p graf-after--p">Happy scaling!</p>



      <h3 name="95f3" id="95f3" class="graf graf--h3 graf-after--p graf--last"><a href="https://github.com/d3/d3-scale" data-href="https://github.com/d3/d3-scale" class="markup--anchor markup--h3-anchor" rel="nofollow">https://github.com/d3/d3-scale</a></h3>




    <h1>d3-scale by Mick Bostock</h1>
 <p class="it">Las escalas son una abstracción conveniente para una tarea fundamental en la visualización: asignar una dimensión de los datos abstractos a una representación visual. Aunque la mayoría de las veces se utiliza para codificar datos cuantitativos, como asignar una medición en metros a una posición en píxeles para puntos en un diagrama de dispersión, las escalas pueden representar virtualmente cualquier codificación visual, como colores divergentes, anchos de trazo o tamaño de símbolo. Las escalas también se pueden utilizar con virtualmente cualquier tipo de datos, tales como datos categóricos nombrados o datos discretos que requieran pausas razonables.</p>
    <p class="p">Scales are a convenient abstraction for a fundamental task in visualization: mapping a dimension of abstract data to a visual representation. Although most often used for position-encoding quantitative data, such as mapping a measurement in meters to a position in pixels for dots in a scatterplot, scales can represent virtually any visual encoding, such as diverging colors, stroke widths, or symbol size. Scales can also be used with virtually any type of data, such as named categorical data or discrete data that requires sensible breaks.</p>

   
  <p class="it">Para datos cuantitativos continuos, normalmente se desea una escala lineal. (Para datos de series de tiempo, una escala de tiempo.) Si la distribución lo solicita, considere la posibilidad de transformar datos usando una escala de potencia o escala de log. Una escala de cuantización puede ayudar a la diferenciación redondeando datos continuos a un conjunto fijo de valores discretos; De manera similar, una escala de cuantía calcula cuantiles de una población de muestra, y una escala de umbral le permite especificar interrupciones arbitrarias en datos continuos. También se proporcionan varios esquemas de colores secuenciales incorporados; Para más información ver d3-scale-chromatic.</p>
    <p class="p">For continuous quantitative data, you typically want a linear scale. (For time series data, a time scale.) If the distribution calls for it, consider transforming data using a power or log scale. A quantize scale may aid differentiation by rounding continuous data to a fixed set of discrete values; similarly, a quantile scale computes quantiles from a sample population, and a threshold scale allows you to specify arbitrary breaks in continuous data. Several built-in sequential color schemes are also provided; see d3-scale-chromatic for more.</p>

  

    <p class="it">Para datos ordenados discretos (ordenados) o categóricos (no ordenados), una escala ordinal especifica una asignación explícita de un conjunto de valores de datos a un conjunto correspondiente de atributos visuales (como colores). Las escalas de banda y punto relacionadas son útiles para codificar posiciones de datos ordinales, como barras en un gráfico de barras o puntos en un diagrama de dispersión categórico. También se proporcionan varias escalas de color categóricas incorporadas.</p>
    <p class="p">For discrete ordinal (ordered) or categorical (unordered) data, an ordinal scale specifies an explicit mapping from a set of data values to a corresponding set of visual attributes (such as colors). The related band and point scales are useful for position-encoding ordinal data, such as bars in a bar chart or dots in an categorical scatterplot. Several built-in categorical color scales are also provided.</p>


 <p class="it">Las escalas no tienen representación visual intrínseca. Sin embargo, la mayoría de las escalas pueden generar y dar formato a las señales de las marcas de referencia para ayudar en la construcción de ejes.</p>
    <p class="p">Scales have no intrinsic visual representation. However, most scales can generate and format ticks for reference marks to aid in the construction of axes.</p>

   

    <h2>Installing</h2>
<p class="it">Si usa NPM, npm instala la escala d3. De lo contrario, descargue la última versión. También puede cargar directamente desde d3js.org, ya sea como una biblioteca independiente o como parte de D3 4.0. Los entornos AMD, CommonJS y vainilla son compatibles. En vainilla, se exporta un d3 global:</p>
    <p class="p">If you use NPM, npm install d3-scale. Otherwise, download the latest release. You can also load directly from d3js.org, either as a standalone library or as part of D3 4.0. AMD, CommonJS, and vanilla environments are supported. In vanilla, a d3 global is exported:</p>

    

    <pre class="programlisting" data-language="javascript" id="113"> 
&lt;script src="https://d3js.org/d3-array.v1.min.js"&gt;&lt;/script&gt;
&lt;script src="https://d3js.org/d3-collection.v1.min.js"&gt;&lt;/script&gt;
&lt;script src="https://d3js.org/d3-color.v1.min.js"&gt;&lt;/script&gt;
&lt;script src="https://d3js.org/d3-format.v1.min.js"&gt;&lt;/script&gt;
&lt;script src="https://d3js.org/d3-interpolate.v1.min.js"&gt;&lt;/script&gt;
&lt;script src="https://d3js.org/d3-time.v1.min.js"&gt;&lt;/script&gt;
&lt;script src="https://d3js.org/d3-time-format.v2.min.js"&gt;&lt;/script&gt;
&lt;script src="https://d3js.org/d3-scale.v1.min.js"&gt;&lt;/script&gt;

&lt;script&gt;

var x = d3.scaleLinear();

&lt;/script&gt;
</pre>

    <p class="p">(You can omit d3-time and d3-time-format if you’re not using <code class="literal">d3.scaleTime</code> or <code class="literal">d3.scaleUtc</code>.)</p>

  

<h2>API Reference</h2>
<ul>
<li>Continuous (Linear, Power, Log, Identity, Time)</li>
<li>Sequential</li>
<li>Quantize</li>
<li>Quantile</li>
<li>Threshold</li>
<li>Ordinal (Band, Point, Category)</li>
<li>Continuous Scales</li>
</ul>
<p class="it">Las escalas continuas asignan un dominio de entrada cuantitativo continuo a un rango de salida continuo. Si el rango es también numérico, la asignación puede invertirse. Una escala continua no se construye directamente; En su lugar, pruebe una escala de color lineal, de energía, de registro, de identidad, de tiempo o secuencial.</p>
<p class="p">Continuous scales map a continuous, quantitative input domain to a continuous output range. If the range is also numeric, the mapping may be inverted. A continuous scale is not constructed directly; instead, try a linear, power, log, identity, time or sequential color scale.</p>




<h3># continuous(value) </h3>
<p class="it">Dado un valor del dominio, devuelve el valor correspondiente del rango. Si el valor dado está fuera del dominio, y el bloqueo no está habilitado, la correlación se puede extrapolar de tal manera que el valor devuelto esté fuera del rango. Por ejemplo, para aplicar una codificación de posición:</p>
<p class="p">Given a value from the domain, returns the corresponding value from the range. If the given value is outside the domain, and clamping is not enabled, the mapping may be extrapolated such that the returned value is outside the range. For example, to apply a position encoding:</p>


<pre class="programlisting" data-language="javascript" id="100">
var x = d3.scaleLinear()
    .domain([10, 130])
    .range([0, 960]);

x(20); // 80
x(50); // 320
</pre>
Or to apply a color encoding:
<pre class="programlisting" data-language="javascript" id="101">
var color = d3.scaleLinear()
    .domain([10, 100])
    .range(["brown", "steelblue"]);

color(20); // "#9a3439"
color(50); // "#7b5167"
</pre>

<h3># continuous.invert(value) </h3>
<p class="it">Dado un valor del rango, devuelve el valor correspondiente de dominio. La inversión es útil para la interacción, por ejemplo para determinar el valor de los datos correspondiente a la posición del ratón. Por ejemplo, para invertir una codificación de posición:</p>
<p class="p">Given a value from the range, returns the corresponding value from the domain. Inversion is useful for interaction, say to determine the data value corresponding to the position of the mouse. For example, to invert a position encoding:</p>

<pre class="programlisting" data-language="javascript" id="112">
var x = d3.scaleLinear()
    .domain([10, 130])
    .range([0, 960]);

x.invert(80); // 20
x.invert(320); // 50
</pre>
<p class="it">Si el valor dado está fuera del rango, y el bloqueo no está habilitado, la correlación se puede extrapolar de tal manera que el valor devuelto esté fuera del dominio. Este método sólo se admite si el rango es numérico. Si el rango no es numérico, devuelve NaN.</p>
<p class="p">If the given value is outside the range, and clamping is not enabled, the mapping may be extrapolated such that the returned value is outside the domain. This method is only supported if the range is numeric. If the range is not numeric, returns NaN.</p>
<p class="it">Para un valor válido <strong>y</strong> en el rango, continuo (continuo.invert (y)) es aproximadamente igual a <strong>y</strong>; De manera similar, para un valor <strong>x</strong> válido en el dominio, continuous.invert (continuo (x)) aproximadamente igual a <strong>x</strong>. La escala y su inversa pueden no ser exactas debido a las limitaciones de la precisión de punto flotante.</p>
<p class="p">For a valid value <strong>y</strong> in the range, continuous(continuous.invert(y)) approximately equals <strong>y</strong>; similarly, for a valid value <strong>x</strong> in the domain, continuous.invert(continuous(x)) approximately equals <strong>x</strong>. The scale and its inverse may not be exact due to the limitations of floating point precision.</p>

<h3># continuous.domain([domain])</h3>
<p class="it">Si se especifica dominio, establece el dominio de la escala en el array de números especificada. el array debe contener dos o más elementos. Si los elementos del array dado no son números, serán forzados a números. Si no se especifica dominio, devuelve una copia del dominio actual de la escala.</p>
<p class="p">If domain is specified, sets the scale’s domain to the specified array of numbers. The array must contain two or more elements. If the elements in the given array are not numbers, they will be coerced to numbers. If domain is not specified, returns a copy of the scale’s current domain.</p>
<p class="it">Aunque las escalas continuas típicamente tienen dos valores cada uno en su dominio y rango, especificando más de dos valores produce una escala por piezas. Por ejemplo, para crear una escala de color divergente que interpola entre blanco y rojo para valores negativos y blanco y verde para valores positivos, digamos:</p>
<p class="p">Although continuous scales typically have two values each in their domain and range, specifying more than two values produces a piecewise scale. For example, to create a diverging color scale that interpolates between white and red for negative values, and white and green for positive values, say:</p>

<pre class="programlisting" data-language="javascript" id="103">
var color = d3.scaleLinear()
    .domain([-1, 0, 1])
    .range(["red", "white", "green"]);

color(-0.5); // "rgb(255, 128, 128)"
color(+0.5); // "rgb(128, 192, 128)"
</pre>
<p class="it">Internamente, una escala por pieza realiza una búsqueda binaria para el interpolador de rango correspondiente al valor de dominio dado. Por lo tanto, el dominio debe estar en orden ascendente o descendente. Si el dominio y el rango tienen diferentes longitudes N y M, sólo se observan los primeros elementos min (N, M) en cada uno.</p>
<p class="p">Internally, a piecewise scale performs a binary search for the range interpolator corresponding to the given domain value. Thus, the domain must be in ascending or descending order. If the domain and range have different lengths N and M, only the first min(N,M) elements in each are observed.</p>

<h3># continuous.range([range])</h3>
<p class="it">Si se especifica rango, establece el rango de la escala en la array de valores especificada. La array debe contener dos o más elementos. A diferencia del dominio, los elementos de la array dada no necesitan ser números; Cualquier valor que es soportado por el interpolador subyacente funcionará, aunque tenga en cuenta que se requieren intervalos numéricos para invertir. Si no se especifica rango, devuelve una copia del rango actual de la escala. Vea continuous.interpolate para más ejemplos.</p>
<p class="p">If range is specified, sets the scale’s range to the specified array of values. The array must contain two or more elements. Unlike the domain, elements in the given array need not be numbers; any value that is supported by the underlying interpolator will work, though note that numeric ranges are required for invert. If range is not specified, returns a copy of the scale’s current range. See continuous.interpolate for more examples.</p>

<h3># continuous.rangeRound([range])</h3>
<p class="it">Establece el rango de la escala a la array de valores especificada al mismo tiempo que se establece el interpolador de escala a interpolator. Este es un método de conveniencia equivalente a:</p>
<pre class="program
<p class="p">Sets the scale’s range to the specified array of values while also setting the scale’s interpolator to interpolateRound. This is a convenience method equivalent to:</p>
listing" data-language="javascript" id="104">
continuous
    .range(range)
    .interpolate(d3.interpolateRound);</pre>
<p class="it">El interpolador de redondeo es a veces útil para evitar artefactos de antialiasing, aunque también considere los estilos "crispEdges" de representación de formas. Tenga en cuenta que este interpolador sólo se puede utilizar con rangos numéricos.</p>

<p class="p">The rounding interpolator is sometimes useful for avoiding antialiasing artifacts, though also consider the shape-rendering “crispEdges” styles. Note that this interpolator can only be used with numeric ranges.</p>

<h3># continuous.clamp(clamp)</h3>


<p class="it">Si se especifica clamp, habilita o deshabilita la clamping en consecuencia. Si el bloqueo se desactiva y la escala pasa a un valor fuera del dominio, la escala puede devolver un valor fuera del rango mediante extrapolación. Si el bloqueo está activado, el valor de retorno de la escala está siempre dentro del rango de la escala. El clamping se aplica de manera similar a la inversión continua. Por ejemplo:</p>
<p class="p">If clamp is specified, enables or disables clamping accordingly. If clamping is disabled and the scale is passed a value outside the domain, the scale may return a value outside the range through extrapolation. If clamping is enabled, the return value of the scale is always within the scale’s range. Clamping similarly applies to continuous.invert. For example:</p>

<pre class="programlisting" data-language="javascript" id="105">
var x = d3.scaleLinear()
    .domain([10, 130])
    .range([0, 960]);

x(-10); // -160, outside range
x.invert(-160); // -10, outside domain

x.clamp(true);
x(-10); // 0, clamped to range
x.invert(-160); // 10, clamped to domain</pre>
<p class="it">Si el clamp no se especifica, devuelve si la escala mantiene o no los valores dentro del rango.</p>
<p class="p">If clamp is not specified, returns whether or not the scale currently clamps values to within the range.</p>

<h3># continuous.interpolate(interpolate)</h3>
<p class="it">Si se especifica interpolación, se establece la fábrica del interpolador de rango de la escala. Esta fábrica de interpolación se utiliza para crear interpoladores para cada par adyacente de valores de la gama; Estos interpoladores asignan un parámetro de dominio normalizado t en [0, 1] al valor correspondiente en el intervalo. Si no se especifica la fábrica, devuelve la fábrica del interpolador actual, que por defecto interpola. Consulte interpolación d3 para obtener más interpoladores.</p>

<p class="p">If interpolate is specified, sets the scale’s range interpolator factory. This interpolator factory is used to create interpolators for each adjacent pair of values from the range; these interpolators then map a normalized domain parameter t in [0, 1] to the corresponding value in the range. If factory is not specified, returns the scale’s current interpolator factory, which defaults to interpolate. See d3-interpolate for more interpolators.</p>


<p class="p">For example, consider a diverging color scale with three colors in the range:</p>


<pre class="programlisting" data-language="javascript" id="106">
var color = d3.scaleLinear()
    .domain([-100, 0, +100])
    .range(["red", "white", "green"]);</pre>

<p class="p">Two interpolators are created internally by the scale, equivalent to:</p>



<pre class="programlisting" data-language="javascript" id="107">
var i0 = d3.interpolate("red", "white"),
    i1 = d3.interpolate("white", "green");</pre>

<p class="it">Una razón común para especificar un interpolador personalizado es cambiar el espacio de color de la interpolación. Por ejemplo, para usar HCL:</p>
<p class="p">A common reason to specify a custom interpolator is to change the color space of interpolation. For example, to use HCL:</p>

<pre class="programlisting" data-language="javascript" id="108">
var color = d3.scaleLinear()
    .domain([10, 100])
    .range(["brown", "steelblue"])
    .interpolate(d3.interpolateHcl);</pre>


<p class="p">Or for Cubehelix with a custom gamma:</p>
<pre class="programlisting" data-language="javascript" id="109">
var color = d3.scaleLinear()
    .domain([10, 100])
    .range(["brown", "steelblue"])
    .interpolate(d3.interpolateCubehelix.gamma(3));</pre>

<p class="it">Nota: el interpolador predeterminado puede volver a usar valores de retorno. Por ejemplo, si los valores de rango son objetos, el interpolador de valores siempre devuelve el mismo objeto, modificándolo en su lugar. Si la escala se utiliza para establecer un atributo o estilo, esto es típicamente aceptable (y deseable para el rendimiento); Sin embargo, si necesita almacenar el valor devuelto de la escala, debe especificar su propio interpolador o hacer una copia según corresponda.</p>
<p class="p">Note: the default interpolator may reuse return values. For example, if the range values are objects, then the value interpolator always returns the same object, modifying it in-place. If the scale is used to set an attribute or style, this is typically acceptable (and desirable for performance); however, if you need to store the scale’s return value, you must specify your own interpolator or make a copy as appropriate.</p>

<h3># continuous.ticks([count])</h3>

<p class="it">Devuelve aproximadamente los valores representativos de cuenta del dominio de la escala. Si count no se especifica, el valor predeterminado es 10. Los valores de tick devueltos están espaciados uniformemente, tienen valores legibles por humanos (como múltiplos de potencias de 10) y se garantiza que están dentro del alcance del dominio. Las garrapatas se utilizan a menudo para mostrar líneas de referencia o marcas de marcación, junto con los datos visualizados. El recuento especificado es sólo una pista; La escala puede devolver valores más o menos dependiendo del dominio. Vea también las garrapatas de d3-array.</p>
<p class="p">Returns approximately count representative values from the scale’s domain. If count is not specified, it defaults to 10. The returned tick values are uniformly spaced, have human-readable values (such as multiples of powers of 10), and are guaranteed to be within the extent of the domain. Ticks are often used to display reference lines, or tick marks, in conjunction with the visualized data. The specified count is only a hint; the scale may return more or fewer values depending on the domain. See also d3-array’s ticks.</p>

<h3># continuous.tickFormat([count[, specifier]])</h3>

<p class="it">Devuelve una función de formato numérico adecuada para mostrar un valor de tick, calculando automáticamente la precisión adecuada en función del intervalo fijo entre los valores de tick. El recuento especificado debe tener el mismo valor que el recuento que se utiliza para generar los valores de tick.</p>

<p class="p">Returns a number format function suitable for displaying a tick value, automatically computing the appropriate precision based on the fixed interval between tick values. The specified count should have the same value as the count that is used to generate the tick values.</p>

<p class="it">Un especificador opcional permite un formato personalizado donde la precisión del formato se establece automáticamente por la escala como apropiado para el intervalo de marca. Por ejemplo, para dar formato al porcentaje de cambio, podría decir:</p>


<p class="p">An optional specifier allows a custom format where the precision of the format is automatically set by the scale as appropriate for the tick interval. For example, to format percentage change, you might say:</p>

<pre class="programlisting" data-language="javascript" id="110">
var x = d3.scaleLinear()
    .domain([-1, 1])
    .range([0, 960]);

var ticks = x.ticks(5),
    tickFormat = x.tickFormat(5, "+%");

ticks.map(tickFormat); // ["-100%", "-50%", "+0%", "+50%", "+100%"]</pre>


<p class="it">Si el especificador utiliza el tipo de formato s, la escala devolverá un formato de prefijo SI basado en el valor más grande del dominio. Si el especificador ya especifica una precisión, este método es equivalente a locale.format.</p>


<p class="p">If specifier uses the format type s, the scale will return a SI-prefix format based on the largest value in the domain. If the specifier already specifies a precision, this method is equivalent to locale.format.</p>

<h3># continuous.nice([count])</h3>

<p class="it">Extiende el dominio para que comience y termine en valores redondeados agradables. Este método normalmente modifica el dominio de la escala y sólo puede extender los límites al valor redondo más cercano. Un argumento de cuenta de tictac opcional permite un mayor control sobre el tamaño de paso utilizado para extender los límites, garantizando que las garrapatas devueltas cubrirán exactamente el dominio. Nicing es útil si el dominio se calcula a partir de datos, digamos utilizando el grado, y puede ser irregular. Por ejemplo, para un dominio de [0.201479 ..., 0.996679 ...], un dominio agradable podría ser [0.2, 1.0]. Si el dominio tiene más de dos valores, nicing el dominio sólo afecta al primer y último valor. Véase también tickStep de d3-array.</p>

<p class="p">Extends the domain so that it starts and ends on nice round values. This method typically modifies the scale’s domain, and may only extend the bounds to the nearest round value. An optional tick count argument allows greater control over the step size used to extend the bounds, guaranteeing that the returned ticks will exactly cover the domain. Nicing is useful if the domain is computed from data, say using extent, and may be irregular. For example, for a domain of [0.201479…, 0.996679…], a nice domain might be [0.2, 1.0]. If the domain has more than two values, nicing the domain only affects the first and last value. See also d3-array’s tickStep.</p>

<p class="it">Nicing escaleras sólo modifica el dominio actual; No lo hace automáticamente que Niza dominios están utilizando posteriormente continuous.domain septiembre. Debe volver a la escalera agradable después de establecer el nuevo dominio, si se desea.</p>


<p class="p">Nicing a scale only modifies the current domain; it does not automatically nice domains that are subsequently set using continuous.domain. You must re-nice the scale after setting the new domain, if desired.</p>

<h3># continuous.copy()</h3>

<p class="it">Devuelve una copia exacta de esta escalera. Cambios en esta escala no afectarán a las escaleras de retorno, y viceversa.</p>


<p class="p">Returns an exact copy of this scale. Changes to this scale will not affect the returned scale, and vice versa.</p>

<h2>Linear Scales</h2>

<h3># d3.scaleLinear()</h3>

<p class="it">Construye una nueva escala continua con el dominio de unidad [0, 1], el rango de unidades [0, 1], el interpolador por defecto y el bloqueo están deshabilitados. Las escalas lineales son una buena opción por defecto para los datos cuantitativos continuos porque preservan las diferencias proporcionales. Cada valor de intervalo y puede expresarse como una función del valor de dominio x: y = mx + b.</p>


<p class="p">Constructs a new continuous scale with the unit domain [0, 1], the unit range [0, 1], the default interpolator and clamping disabled. Linear scales are a good default choice for continuous quantitative data because they preserve proportional differences. Each range value y can be expressed as a function of the domain value x: y = mx + b.</p>

<h2>Power Scales</h2>
<p class="it">Las escalas de potencia son similares a las escalas lineales, excepto que se aplica una transformada exponencial al valor del dominio de entrada antes de calcular el valor del rango de salida. Cada valor de intervalo y puede expresarse como una función del valor de dominio x: y = mx ^ k + b, donde k es el valor del exponente. Las escalas de potencia también admiten valores de dominio negativo, en cuyo caso el valor de entrada y el valor de salida resultante se multiplican por -1.</p>

<p class="p">Power scales are similar to linear scales, except an exponential transform is applied to the input domain value before the output range value is computed. Each range value y can be expressed as a function of the domain value x: y = mx^k + b, where k is the exponent value. Power scales also support negative domain values, in which case the input value and the resulting output value are multiplied by -1.</p>

<h3># d3.scalePow()</h3>


<p class="it">Construye una nueva escala continua con el dominio de la unidad [0, 1], el intervalo unidad [0, 1], el exponente 1, el interpolador defecto y sujeción discapacitados. (Tenga en cuenta que esto es efectivamente una escalera lineal hasta que los conjuntos de diferente exponente.)</p>

<p class="p">Constructs a new continuous scale with the unit domain [0, 1], the unit range [0, 1], the exponent 1, the default interpolator and clamping disabled. (Note that this is effectively a linear scale until you set a different exponent.)</p>


<h3># pow(value)</h3>


<p class="p">See continuous.</p>

<h3># pow.invert(value)</h3>

<p class="p">See continuous.invert.</p>

<h3># pow.exponent([exponent])</h3>
<p class="it">Si no se especifica exponente, establece el exponente actual al valor numérico dado. Si no se especifica exponente, devuelve el exponente actual, que por defecto es 1. (Tenga en cuenta que esto es efectivamente una escalera lineal hasta que los conjuntos de diferente exponente.)</p>

<p class="p">If exponent is specified, sets the current exponent to the given numeric value. If exponent is not specified, returns the current exponent, which defaults to 1. (Note that this is effectively a linear scale until you set a different exponent.)</p>

<h3># pow.domain([domain])</h3>

<p class="p">See continuous.domain.</p>

<h3># pow.range([range])</h3>


<p class="p">See continuous.range.</p>

<h3># pow.rangeRound([range])</h3>

<p class="p">See continuous.rangeRound.</p>

<h3># pow.clamp(clamp)</h3>

<p class="p">See continuous.clamp.</p>

<h3># pow.interpolate(interpolate)</h3>

<p class="p">See continuous.interpolate.</p>

<h3># pow.ticks([count])</h3>


<p class="p">See continuous.ticks.</p>

<h3># pow.tickFormat([count[, specifier]])</h3>

<p class="p">See continuous.tickFormat.</p>

<h3># pow.nice([count])</h3>

<p class="p">See continuous.nice.</p>

<h3># pow.copy()</h3>


<p class="p">See continuous.copy.</p>

<h3># d3.scaleSqrt()</h3>

<p class="it">Construye un nuevo escalas de potencia continua con el dominio de la unidad [0, 1], el intervalo unidad [0, 1], el exponente 0,5, el interpolador defecto y sujeción discapacitados. Este es un método de conveniencia equivalente a d3.scalePow (). Exponente (0.5).</p>
<p class="p">Constructs a new continuous power scale with the unit domain [0, 1], the unit range [0, 1], the exponent 0.5, the default interpolator and clamping disabled. This is a convenience method equivalent to d3.scalePow().exponent(0.5).</p>

<h2>Log Scales</h2>

<p class="p">Log scales are similar to linear scales, except a logarithmic transform is applied to the input domain value before the output range value is computed. The mapping to the range value y can be expressed as a function of the domain value x: y = m log(x) + b.</p>

<p class="p">As log(0) = -∞, a log scale domain must be strictly-positive or strictly-negative; the domain must not include or cross zero. A log scale with a positive domain has a well-defined behavior for positive values, and a log scale with a negative domain has a well-defined behavior for negative values. (For a negative domain, input and output values are implicitly multiplied by -1.) The behavior of the scale is undefined if you pass a negative value to a log scale with a positive domain or vice versa.</p>

<h3># d3.scaleLog()</h3>

<p class="p">Constructs a new continuous scale with the domain [1, 10], the unit range [0, 1], the base 10, the default interpolator and clamping disabled.</p>


<h3># log(value)</h3>
<p class="p">See continuous.</p>

<h3># log.invert(value)</h3>

<p class="p">See continuous.invert.</p>

<h3># log.base([base])</h3>

<p class="p">If base is specified, sets the base for this logarithmic scale to the specified value. If base is not specified, returns the current base, which defaults to 10.</p>

<h3># log.domain([domain])</h3>

<p class="p">See continuous.domain.</p>

<h3># log.range([range])</h3>

<p class="p">See continuous.range.</p>

<h3># log.rangeRound([range])</h3>

<p class="p">See continuous.rangeRound.</p>

<h3># log.clamp(clamp)</h3>

<p class="p">See continuous.clamp.</p>

<h3># log.interpolate(interpolate)</h3>

<p class="p">See continuous.interpolate.</p>

<h3># log.ticks([count])</h3>

<p class="p">Like continuous.ticks, but customized for a log scale. If the base is an integer, the returned ticks are uniformly spaced within each integer power of base; otherwise, one tick per power of base is returned. The returned ticks are guaranteed to be within the extent of the domain. If the orders of magnitude in the domain is greater than count, then at most one tick per power is returned. Otherwise, the tick values are unfiltered, but note that you can use log.tickFormat to filter the display of tick labels. If count is not specified, it defaults to 10.</p>

<h3># log.tickFormat([count[, specifier]])</h3>

<p class="p">Like continuous.tickFormat, but customized for a log scale. The specified count typically has the same value as the count that is used to generate the tick values. If there are too many ticks, the formatter may return the empty string for some of the tick labels; however, note that the ticks are still shown. To disable filtering, specify a count of Infinity. When specifying a count, you may also provide a format specifier or format function. For example, to get a tick formatter that will display 20 ticks of a currency, say log.tickFormat(20, "$,f"). If the specifier does not have a defined precision, the precision will be set automatically by the scale, returning the appropriate format. This provides a convenient way of specifying a format whose precision will be automatically set by the scale.</p>

<h3># log.nice()</h3>

<p class="p">Like continuous.nice, except extends the domain to integer powers of base. For example, for a domain of [0.201479…, 0.996679…], and base 10, the nice domain is [0.1, 1]. If the domain has more than two values, nicing the domain only affects the first and last value.</p>

<h3># log.copy()</h3>

<p class="p">See continuous.copy.</p>

<h2>Identity Scales</h2>

<p class="p">Identity scales are a special case of linear scales where the domain and range are identical; the scale and its invert method are thus the identity function. These scales are occasionally useful when working with pixel coordinates, say in conjunction with an axis or brush. Identity scales do not support rangeRound, clamp or interpolate.</p>

<h3># d3.scaleIdentity()</h3>

<p class="p">Constructs a new identity scale with the unit domain [0, 1] and the unit range [0, 1].</p>

<h2>Time Scales</h2>




<p class="p">Time scales are a variant of linear scales that have a temporal domain: domain values are coerced to dates rather than numbers, and invert likewise returns a date. Time scales implement ticks based on calendar intervals, taking the pain out of generating axes for temporal domains.</p>

<p class="p">For example, to create a position encoding:</p>

<pre class="programlisting" data-language="javascript" id="122">
var x = d3.scaleTime()
    .domain([new Date(2000, 0, 1), new Date(2000, 0, 2)])
    .range([0, 960]);

x(new Date(2000, 0, 1,  5)); // 200
x(new Date(2000, 0, 1, 16)); // 640
x.invert(200); // Sat Jan 01 2000 05:00:00 GMT-0800 (PST)
x.invert(640); // Sat Jan 01 2000 16:00:00 GMT-0800 (PST)</pre>

<p class="p">For a valid value y in the range, time(time.invert(y)) equals y; similarly, for a valid value x in the domain, time.invert(time(x)) equals x. The invert method is useful for interaction, say to determine the value in the domain that corresponds to the pixel location under the mouse.</p>

<h3># d3.scaleTime()</h3>

<p class="p">Constructs a new time scale with the domain [2000-01-01, 2000-01-02], the unit range [0, 1], the default interpolator and clamping disabled.</p>

<h3># time(value)</h3>

<p class="p">See continuous.</p>

<h3># time.invert(value)</h3>

<p class="p">See continuous.invert.</p>

<h3># time.domain([domain])</h3>

<p class="p">See continuous.domain.</p>

<h3># time.range([range])</h3>

<p class="p">See continuous.range.</p>

<h3># time.rangeRound([range])</h3>

<p class="p">See continuous.rangeRound.</p>

<h3># time.clamp(clamp)</h3>

<p class="p">See continuous.clamp.</p>

<h3># time.interpolate(interpolate)</h3>

<p class="p">See continuous.interpolate.</p>

<h3># time.ticks([count]) </h3>
<h3># time.ticks([interval])</h3>

<p class="p">Returns representative dates from the scale’s domain. The returned tick values are uniformly-spaced (mostly), have sensible values (such as every day at midnight), and are guaranteed to be within the extent of the domain. Ticks are often used to display reference lines, or tick marks, in conjunction with the visualized data.</p>

<p class="p">An optional count may be specified to affect how many ticks are generated. If count is not specified, it defaults to 10. The specified count is only a hint; the scale may return more or fewer values depending on the domain. For example, to create ten default ticks, say:</p>

<pre class="programlisting" data-language="javascript" id="132">
var x = d3.scaleTime();

x.ticks(10);
// [Sat Jan 01 2000 00:00:00 GMT-0800 (PST),
//  Sat Jan 01 2000 03:00:00 GMT-0800 (PST),
//  Sat Jan 01 2000 06:00:00 GMT-0800 (PST),
//  Sat Jan 01 2000 09:00:00 GMT-0800 (PST),
//  Sat Jan 01 2000 12:00:00 GMT-0800 (PST),
//  Sat Jan 01 2000 15:00:00 GMT-0800 (PST),
//  Sat Jan 01 2000 18:00:00 GMT-0800 (PST),
//  Sat Jan 01 2000 21:00:00 GMT-0800 (PST),
//  Sun Jan 02 2000 00:00:00 GMT-0800 (PST)]</pre>

<p class="p">The following time intervals are considered for automatic ticks:</p>

1-, 5-, 15- and 30-second.
1-, 5-, 15- and 30-minute.
1-, 3-, 6- and 12-hour.
1- and 2-day.
1-week.
1- and 3-month.
1-year.

<p class="p">In lieu of a count, a time interval may be explicitly specified. To prune the generated ticks for a given time interval, use interval.every. For example, to generate ticks at 15-minute intervals:</p>

<pre class="programlisting" data-language="javascript" id="142">
var x = d3.scaleTime()
    .domain([new Date(2000, 0, 1, 0), new Date(2000, 0, 1, 2)]);

x.ticks(d3.timeMinute.every(15));
// [Sat Jan 01 2000 00:00:00 GMT-0800 (PST),
//  Sat Jan 01 2000 00:15:00 GMT-0800 (PST),
//  Sat Jan 01 2000 00:30:00 GMT-0800 (PST),
//  Sat Jan 01 2000 00:45:00 GMT-0800 (PST),
//  Sat Jan 01 2000 01:00:00 GMT-0800 (PST),
//  Sat Jan 01 2000 01:15:00 GMT-0800 (PST),
//  Sat Jan 01 2000 01:30:00 GMT-0800 (PST),
//  Sat Jan 01 2000 01:45:00 GMT-0800 (PST),
//  Sat Jan 01 2000 02:00:00 GMT-0800 (PST)]</pre>




<p class="p">Alternatively, pass a test function to interval.filter:
<pre class="programlisting" data-language="javascript" id="152">
x.ticks(d3.timeMinute.filter(function(d) {
  return d.getMinutes() % 15 === 0;
}));</pre>




<p class="p">Note: in some cases, such as with day ticks, specifying a step can result in irregular spacing of ticks because time intervals have varying length.</p>









<h3># time.tickFormat([count[, specifier]])</h3> 
<h3># time.tickFormat([interval[, specifier]])</h3>





<p class="p">Returns a time format function suitable for displaying tick values. The specified count or interval is currently ignored, but is accepted for consistency with other scales such as continuous.tickFormat. If a format specifier is specified, this method is equivalent to format. If specifier is not specified, the default time format is returned. The default multi-scale time format chooses a human-readable representation based on the specified date as follows:</p>









%Y - for year boundaries, such as 2011.
%B - for month boundaries, such as February.
%b %d - for week boundaries, such as Feb 06.
%a %d - for day boundaries, such as Mon 07.
%I %p - for hour boundaries, such as 01 AM.
%I:%M - for minute boundaries, such as 01:23.
:%S - for second boundaries, such as :45.
.%L - milliseconds for all other times, such as .012.




<p class="p">Although somewhat unusual, this default behavior has the benefit of providing both local and global context: for example, formatting a sequence of ticks as [11 PM, Mon 07, 01 AM] reveals information about hours, dates, and day simultaneously, rather than just the hours [11 PM, 12 AM, 01 AM]. See d3-time-format if you’d like to roll your own conditional time format.</p>

<h3># time.nice([count])</h3>
<h3># time.nice([interval[, step]])</h3>





<p class="p">Extends the domain so that it starts and ends on nice round values. This method typically modifies the scale’s domain, and may only extend the bounds to the nearest round value. See continuous.nice for more.</p>













<p class="p">An optional tick count argument allows greater control over the step size used to extend the bounds, guaranteeing that the returned ticks will exactly cover the domain. Alternatively, a time interval may be specified to explicitly set the ticks. If an interval is specified, an optional step may also be specified to skip some ticks. For example, time.nice(d3.timeSecond, 10) will extend the domain to an even ten seconds (0, 10, 20, etc.). See time.ticks and interval.every for further detail.</p>













<p class="p">Nicing is useful if the domain is computed from data, say using extent, and may be irregular. For example, for a domain of [2009-07-13T00:02, 2009-07-13T23:48], the nice domain is [2009-07-13, 2009-07-14]. If the domain has more than two values, nicing the domain only affects the first and last value.</p>









<h3># d3.scaleUtc()</h3>





<p class="p">Equivalent to time, but the returned time scale operates in Coordinated Universal Time rather than local time.</p>

<h2>Sequential Scales</h2>





<p class="p">Sequential scales are similar to continuous scales in that they map a continuous, numeric input domain to a continuous output range. However, unlike continuous scales, the output range of a sequential scale is fixed by its interpolator and not configurable. These scales do not expose invert, range, rangeRound and interpolate methods.</p>

<h3># d3.scaleSequential(interpolator)</h3>





<p class="p">Constructs a new sequential scale with the given interpolator function. When the scale is applied, the interpolator will be invoked with a value typically in the range [0, 1], where 0 represents the start of the domain, and 1 represents the end of the domain. For example, to implement the ill-advised HSL rainbow scale:</p>









<pre class="programlisting" data-language="javascript" id="162">
var rainbow = d3.scaleSequential(function(t) {
  return d3.hsl(t * 360, 1, 0.5) + "";
});</pre>




<p class="p">A more aesthetically-pleasing and perceptually-effective cyclical hue encoding is to use d3.interpolateRainbow:</p>









<pre class="programlisting" data-language="javascript" id="172">
var rainbow = d3.scaleSequential(d3.interpolateRainbow);</pre>




<p class="p">For even more sequential color schemes, see d3-scale-chromatic.</p>









<h3># sequential(value)</h3>





<p class="p">See continuous.</p>

<h3># sequential.domain([domain])</h3>





<p class="p">See continuous.domain. Note that a sequential scale’s domain must be numeric and must contain exactly two values.</p>









<h3># sequential.clamp([clamp])</h3>





<p class="p">See continuous.clamp.</p>

<h3># sequential.interpolator([interpolator])</h3>





<p class="p">If interpolator is specified, sets the scale’s interpolator to the specified function. If interpolator is not specified, returns the scale’s current interpolator.</p>










<h3># sequential.copy()</h3>





<p class="p">See continuous.copy.</p>

<h3># d3.interpolateViridis(t)</h3>

<h2>viridis</h2>





<p class="p">Given a number t in the range [0,1], returns the corresponding color from the “viridis” perceptually-uniform color scheme designed by van der Walt, Smith and Firing for matplotlib, represented as an RGB string.</p>










<h3># d3.interpolateInferno(t)</h3>

<h2>inferno</h2>





<p class="p">Given a number t in the range [0,1], returns the corresponding color from the “inferno” perceptually-uniform color scheme designed by van der Walt and Smith for matplotlib, represented as an RGB string.</p>










<h3># d3.interpolateMagma(t)</h3>

<h2>magma</h2>





<p class="p">Given a number t in the range [0,1], returns the corresponding color from the “magma” perceptually-uniform color scheme designed by van der Walt and Smith for matplotlib, represented as an RGB string.</p>










<h3># d3.interpolatePlasma(t)</h3>

<h2>plasma</h2>





<p class="p">Given a number t in the range [0,1], returns the corresponding color from the “plasma” perceptually-uniform color scheme designed by van der Walt and Smith for matplotlib, represented as an RGB string.</p>










<h3># d3.interpolateWarm(t)</h3>

<h2>warm</h2>





<p class="p">Given a number t in the range [0,1], returns the corresponding color from a 180° rotation of Niccoli’s perceptual rainbow, represented as an RGB string.</p>

<h3># d3.interpolateCool(t)</h3>

<h2>cool</h2>





<p class="p">Given a number t in the range [0,1], returns the corresponding color from Niccoli’s perceptual rainbow, represented as an RGB string.</p>










<h3># d3.interpolateRainbow(t)</h3>

<h2>rainbow</h2>





<p class="p">Given a number t in the range [0,1], returns the corresponding color from d3.interpolateWarm scale from [0.0, 0.5] followed by the d3.interpolateCool scale from [0.5, 1.0], thus implementing the cyclical less-angry rainbow color scheme.</p>










<h3># d3.interpolateCubehelixDefault(t)</h3>

<h2>cubehelix</h2>





<p class="p">Given a number t in the range [0,1], returns the corresponding color from Green’s default Cubehelix represented as an RGB string.</p>










<h2>Quantize Scales</h2>





<p class="p">Quantize scales are similar to linear scales, except they use a discrete rather than continuous range. The continuous input domain is divided into uniform segments based on the number of values in (i.e., the cardinality of) the output range. Each range value y can be expressed as a quantized linear function of the domain value x: y = m round(x) + b. See bl.ocks.org/4060606 for an example.</p>










<h3># d3.scaleQuantize()</h3>





<p class="p">Constructs a new quantize scale with the unit domain [0, 1] and the unit range [0, 1]. Thus, the default quantize scale is equivalent to the Math.round function.</p>










<h3># quantize(value)</h3>





<p class="p">Given a value in the input domain, returns the corresponding value in the output range. For example, to apply a color encoding:</p>









<pre class="programlisting" data-language="javascript" id="182">
var color = d3.scaleQuantize()
    .domain([0, 1])
    .range(["brown", "steelblue"]);

color(0.49); // "brown"
color(0.51); // "steelblue"</pre>




<p class="p">Or dividing the domain into three equally-sized parts with different range values to compute an appropriate stroke width:</p>









<pre class="programlisting" data-language="javascript" id="192">
var width = d3.scaleQuantize()
    .domain([10, 100])
    .range([1, 2, 4]);

width(20); // 1
width(50); // 2
width(80); // 4</pre>
<h3># quantize.invertExtent(value)</h3>





<p class="p">Returns the extent of values in the domain [x0, x1] for the corresponding value in the range: the inverse of quantize. This method is useful for interaction, say to determine the value in the domain that corresponds to the pixel location under the mouse.</p>









<pre class="programlisting" data-language="javascript" id="1102">
var width = d3.scaleQuantize()
    .domain([10, 100])
    .range([1, 2, 4]);

width.invertExtent(2); // [40, 70]</pre>
<h3># quantize.domain([domain])</h3>





<p class="p">If domain is specified, sets the scale’s domain to the specified two-element array of numbers. If the elements in the given array are not numbers, they will be coerced to numbers. If domain is not specified, returns the scale’s current domain.</p>










<h3># quantize.range([range])</h3>





<p class="p">If range is specified, sets the scale’s range to the specified array of values. The array may contain any number of discrete values. The elements in the given array need not be numbers; any value or type will work. If range is not specified, returns the scale’s current range.</p>










<h3># quantize.ticks([count])</h3>





<p class="p">Equivalent to continuous.ticks.</p>










<h3># quantize.tickFormat([count[, specifier]])</h3> 





<p class="p">Equivalent to continuous.tickFormat.</p>










<h3># quantize.nice()</h3>





<p class="p">Equivalent to continuous.nice.</p>










<h3># quantize.copy() </h3>





<p class="p">Returns an exact copy of this scale. Changes to this scale will not affect the returned scale, and vice versa.</p>










<h2>Quantile Scales</h2>





<p class="p">Quantile scales map a sampled input domain to a discrete range. The domain is considered continuous and thus the scale will accept any reasonable input value; however, the domain is specified as a discrete set of sample values. The number of values in (the cardinality of) the output range determines the number of quantiles that will be computed from the domain. To compute the quantiles, the domain is sorted, and treated as a population of discrete values; see d3-array’s quantile. See bl.ocks.org/8ca036b3505121279daf for an example.</p>










<h3># d3.scaleQuantile()</h3>





<p class="p">Constructs a new quantile scale with an empty domain and an empty range. The quantile scale is invalid until both a domain and range are specified.</p>










<h3># quantile(value)</h3>





<p class="p">Given a value in the input domain, returns the corresponding value in the output range.</p>










<h3># quantile.invertExtent(value)</h3>





<p class="p">Returns the extent of values in the domain [x0, x1] for the corresponding value in the range: the inverse of quantile. This method is useful for interaction, say to determine the value in the domain that corresponds to the pixel location under the mouse.</p>










<h3># quantile.domain([domain])</h3>





<p class="p">If domain is specified, sets the domain of the quantile scale to the specified set of discrete numeric values. The array must not be empty, and must contain at least one numeric value; NaN, null and undefined values are ignored and not considered part of the sample population. If the elements in the given array are not numbers, they will be coerced to numbers. A copy of the input array is sorted and stored internally. If domain is not specified, returns the scale’s current domain.</p>










<h3># quantile.range([range])</h3>





<p class="p">If range is specified, sets the discrete values in the range. The array must not be empty, and may contain any type of value. The number of values in (the cardinality, or length, of) the range array determines the number of quantiles that are computed. For example, to compute quartiles, range must be an array of four elements such as [0, 1, 2, 3]. If range is not specified, returns the current range.</p>










<h3># quantile.quantiles()</h3>





<p class="p">Returns the quantile thresholds. If the range contains n discrete values, the returned array will contain n - 1 thresholds. Values less than the first threshold are considered in the first quantile; values greater than or equal to the first threshold but less than the second threshold are in the second quantile, and so on. Internally, the thresholds array is used with bisect to find the output quantile associated with the given input value.</p>










<h3># quantile.copy()</h3>





<p class="p">Returns an exact copy of this scale. Changes to this scale will not affect the returned scale, and vice versa.</p>










<h2>Threshold Scales</h2>





<p class="p">Threshold scales are similar to quantize scales, except they allow you to map arbitrary subsets of the domain to discrete values in the range. The input domain is still continuous, and divided into slices based on a set of threshold values. See bl.ocks.org/3306362 for an example.</p>










<h3># d3.scaleThreshold()</h3>





<p class="p">Constructs a new threshold scale with the default domain [0.5] and the default range [0, 1]. Thus, the default threshold scale is equivalent to the Math.round function for numbers; for example threshold(0.49) returns 0, and threshold(0.51) returns 1.</p>










<h3># threshold(value)</h3>





<p class="p">Given a value in the input domain, returns the corresponding value in the output range. For example:</p>









<pre class="programlisting" data-language="javascript" id="2102">
var color = d3.scaleThreshold()
    .domain([0, 1])
    .range(["red", "white", "green"]);

color(-1);   // "red"
color(0);    // "white"
color(0.5);  // "white"
color(1);    // "green"
color(1000); // "green"</pre>
<h3># threshold.invertExtent(value)</h3>





<p class="p">Returns the extent of values in the domain [x0, x1] for the corresponding value in the range, representing the inverse mapping from range to domain. This method is useful for interaction, say to determine the value in the domain that corresponds to the pixel location under the mouse. For example:</p>









<pre class="programlisting" data-language="javascript" id="3102">
var color = d3.scaleThreshold()
    .domain([0, 1])
    .range(["red", "white", "green"]);

color.invertExtent("red"); // [undefined, 0]
color.invertExtent("white"); // [0, 1]
color.invertExtent("green"); // [1, undefined]</pre>
<h3># threshold.domain([domain]) </h3>





<p class="p">If domain is specified, sets the scale’s domain to the specified array of values. The values must be in sorted ascending order, or the behavior of the scale is undefined. The values are typically numbers, but any naturally ordered values (such as strings) will work; a threshold scale can be used to encode any type that is ordered. If the number of values in the scale’s range is N+1, the number of values in the scale’s domain must be N. If there are fewer than N elements in the domain, the additional values in the range are ignored. If there are more than N elements in the domain, the scale may return undefined for some inputs. If domain is not specified, returns the scale’s current domain.</p>










<h3># threshold.range([range]) </h3>





<p class="p">If range is specified, sets the scale’s range to the specified array of values. If the number of values in the scale’s domain is N, the number of values in the scale’s range must be N+1. If there are fewer than N+1 elements in the range, the scale may return undefined for some inputs. If there are more than N+1 elements in the range, the additional values are ignored. The elements in the given array need not be numbers; any value or type will work. If range is not specified, returns the scale’s current range.</p>









<h3># threshold.copy() </h3>





<p class="p">Returns an exact copy of this scale. Changes to this scale will not affect the returned scale, and vice versa.</p>









Ordinal Scales





<p class="p">Unlike continuous scales, ordinal scales have a discrete domain and range. For example, an ordinal scale might map a set of named categories to a set of colors, or determine the horizontal positions of columns in a column chart.</p>









<h3># d3.scaleOrdinal([range]) </h3>





<p class="p">Constructs a new ordinal scale with an empty domain and the specified range. If a range is not specified, it defaults to the empty array; an ordinal scale always returns undefined until a non-empty range is defined.</p>









<h3># ordinal(value) </h3>





<p class="p">Given a value in the input domain, returns the corresponding value in the output range. If the given value is not in the scale’s domain, returns the unknown; or, if the unknown value is implicit (the default), then the value is implicitly added to the domain and the next-available value in the range is assigned to value, such that this and subsequent invocations of the scale given the same input value return the same output value.</p>









<h3># ordinal.domain([domain]) </h3>





<p class="p">If domain is specified, sets the domain to the specified array of values. The first element in domain will be mapped to the first element in the range, the second domain value to the second range value, and so on. Domain values are stored internally in a map from stringified value to index; the resulting index is then used to retrieve a value from the range. Thus, an ordinal scale’s values must be coercible to a string, and the stringified version of the domain value uniquely identifies the corresponding range value. If domain is not specified, this method returns the current domain.</p>













<p class="p">Setting the domain on an ordinal scale is optional if the unknown value is implicit (the default). In this case, the domain will be inferred implicitly from usage by assigning each unique value passed to the scale a new value from the range. Note that an explicit domain is recommended to ensure deterministic behavior, as inferring the domain from usage will be dependent on ordering.</p>









<h3># ordinal.range([range]) </h3>





<p class="p">If range is specified, sets the range of the ordinal scale to the specified array of values. The first element in the domain will be mapped to the first element in range, the second domain value to the second range value, and so on. If there are fewer elements in the range than in the domain, the scale will reuse values from the start of the range. If range is not specified, this method returns the current range.</p>









<h3># ordinal.unknown([value]) </h3>





<p class="p">If value is specified, sets the output value of the scale for unknown input values and returns this scale. If value is not specified, returns the current unknown value, which defaults to implicit. The implicit value enables implicit domain construction; see ordinal.domain.</p>









<h3># ordinal.copy()</h3>





<p class="p">Returns an exact copy of this ordinal scale. Changes to this scale will not affect the returned scale, and vice versa.</p>










<h3># d3.scaleImplicit</h3>





<p class="p">A special value for ordinal.unknown that enables implicit domain construction: unknown values are implicitly added to the domain.</p>










<h2>Band Scales</h2>





<p class="p">Band scales are like ordinal scales except the output range is continuous and numeric. Discrete output values are automatically computed by the scale by dividing the continuous range into uniform bands. Band scales are typically used for bar charts with an ordinal or categorical dimension. The unknown value of a band scale is effectively undefined: they do not allow implicit domain construction.</p>










<h2>band</h2>

<h3># d3.scaleBand()</h3> 





<p class="p">Constructs a new band scale with the empty domain, the unit range [0, 1], no padding, no rounding and center alignment.</p>










<h3># band(value) </h3>





<p class="p">Given a value in the input domain, returns the start of the corresponding band derived from the output range. If the given value is not in the scale’s domain, returns undefined.</p>










<h3># band.domain([domain])</h3> 





<p class="p">If domain is specified, sets the domain to the specified array of values. The first element in domain will be mapped to the first band, the second domain value to the second band, and so on. Domain values are stored internally in a map from stringified value to index; the resulting index is then used to determine the band. Thus, a band scale’s values must be coercible to a string, and the stringified version of the domain value uniquely identifies the corresponding band. If domain is not specified, this method returns the current domain.</p>










<h3># band.range([range]) </h3>





<p class="p">If range is specified, sets the scale’s range to the specified two-element array of numbers. If the elements in the given array are not numbers, they will be coerced to numbers. If range is not specified, returns the scale’s current range, which defaults to [0, 1].</p>










<h3># band.rangeRound([range]) </h3>





<p class="p">Sets the scale’s range to the specified two-element array of numbers while also enabling rounding. This is a convenience method equivalent to:</p>









<pre class="programlisting" data-language="javascript" id="4102">
band
    .range(range)
    .round(true);</pre>
Rounding is sometimes useful for avoiding antialiasing artifacts, though also consider the shape-rendering “crispEdges” styles.</p>










<h3># band.round([round]) </h3>





<p class="p">If round is specified, enables or disables rounding accordingly. If rounding is enabled, the start and stop of each band will be integers. Rounding is sometimes useful for avoiding antialiasing artifacts, though also consider the shape-rendering “crispEdges” styles. Note that if the width of the domain is not a multiple of the cardinality of the range, there may be leftover unused space, even without padding! Use band.align to specify how the leftover space is distributed.</p>










<h3># band.paddingInner([padding])</h3>





<p class="p">If padding is specified, sets the inner padding to the specified value which must be in the range [0, 1]. If padding is not specified, returns the current inner padding which defaults to 0. The inner padding determines the ratio of the range that is reserved for blank space between bands.</p>










<h3># band.paddingOuter([padding])</h3>





<p class="p">If padding is specified, sets the outer padding to the specified value which must be in the range [0, 1]. If padding is not specified, returns the current outer padding which defaults to 0. The outer padding determines the ratio of the range that is reserved for blank space before the first band and after the last band.</p>

<h3># band.padding([padding])</h3>





<p class="p">A convenience method for setting the inner and outer padding to the same padding value. If padding is not specified, returns the inner padding.</p>









<h3># band.align([align])</h3>





<p class="p">If align is specified, sets the alignment to the specified value which must be in the range [0, 1]. If align is not specified, returns the current alignment which defaults to 0.5. The alignment determines how any leftover unused space in the range is distributed. A value of 0.5 indicates that the leftover space should be equally distributed before the first band and after the last band; i.e., the bands should be centered within the range. A value of 0 or 1 may be used to shift the bands to one side, say to position them adjacent to an axis.</p>









<h3># band.bandwidth() </h3>




<p class="p">Returns the width of each band.</p>









<h3># band.step()</h3>





<p class="p">Returns the distance between the starts of adjacent bands.</p>









<h3># band.copy()</h3>





<p class="p">Returns an exact copy of this scale. Changes to this scale will not affect the returned scale, and vice versa.</p>









<h2>Point Scales</h2>





<p class="p">Point scales are a variant of band scales with the bandwidth fixed to zero. Point scales are typically used for scatterplots with an ordinal or categorical dimension. The unknown value of a point scale is always undefined: they do not allow implicit domain construction.</p>









<h2>point</h2>

<h3># d3.scalePoint()</h3>





<p class="p">Constructs a new point scale with the empty domain, the unit range [0, 1], no padding, no rounding and center alignment.</p>









<h3># point(value)</h3>





<p class="p">Given a value in the input domain, returns the corresponding point derived from the output range. If the given value is not in the scale’s domain, returns undefined.</p>









<h3># point.domain([domain])</h3>





<p class="p">If domain is specified, sets the domain to the specified array of values. The first element in domain will be mapped to the first point, the second domain value to the second point, and so on. Domain values are stored internally in a map from stringified value to index; the resulting index is then used to determine the point. Thus, a point scale’s values must be coercible to a string, and the stringified version of the domain value uniquely identifies the corresponding point. If domain is not specified, this method returns the current domain.</p>









<h3># point.range([range])</h3>





<p class="p">If range is specified, sets the scale’s range to the specified two-element array of numbers. If the elements in the given array are not numbers, they will be coerced to numbers. If range is not specified, returns the scale’s current range, which defaults to [0, 1].</p>









<h3># point.rangeRound([range])</h3>





<p class="p">Sets the scale’s range to the specified two-element array of numbers while also enabling rounding. This is a convenience method equivalent to:</p>









<pre class="programlisting" data-language="javascript" id="5102">
point
    .range(range)
    .round(true);</pre>




<p class="p">Rounding is sometimes useful for avoiding antialiasing artifacts, though also consider the shape-rendering “crispEdges” styles.</p>









<h3># point.round([round])</h3>





<p class="p">If round is specified, enables or disables rounding accordingly. If rounding is enabled, the position of each point will be integers. Rounding is sometimes useful for avoiding antialiasing artifacts, though also consider the shape-rendering “crispEdges” styles. Note that if the width of the domain is not a multiple of the cardinality of the range, there may be leftover unused space, even without padding! Use point.align to specify how the leftover space is distributed.</p>









<h3># point.padding([padding])</h3>





<p class="p">If padding is specified, sets the outer padding to the specified value which must be in the range [0, 1]. If padding is not specified, returns the current outer padding which defaults to 0. The outer padding determines the ratio of the range that is reserved for blank space before the first point and after the last point. Equivalent to band.paddingOuter.</p>









<h3># point.align([align])</h3>





<p class="p">If align is specified, sets the alignment to the specified value which must be in the range [0, 1]. If align is not specified, returns the current alignment which defaults to 0.5. The alignment determines how any leftover unused space in the range is distributed. A value of 0.5 indicates that the leftover space should be equally distributed before the first point and after the last point; i.e., the points should be centered within the range. A value of 0 or 1 may be used to shift the points to one side, say to position them adjacent to an axis.</p>









<h3># point.bandwidth()</h3>





<p class="p">Returns zero.</p>

<h3># point.step()</h3>





<p class="p">Returns the distance between the starts of adjacent points.</p>









<h3># point.copy()</h3>





<p class="p">Returns an exact copy of this scale. Changes to this scale will not affect the returned scale, and vice versa.</p>









<h2>Category Scales</h2>





<p class="p">These color schemes are designed to work with d3.scaleOrdinal. For example:</p>









<pre class="programlisting" data-language="javascript" id="6102">
var color = d3.scaleOrdinal(d3.schemeCategory10);</pre>




<p class="p">For even more category scales, see d3-scale-chromatic.</p>

<h3># d3.schemeCategory10 </h3>





<p class="p">category10</p>





<p class="p">An array of ten categorical colors represented as RGB hexadecimal strings.</p>









<h3># d3.schemeCategory20 </h3>





<p class="p">category20</p>





<p class="p">An array of twenty categorical colors represented as RGB hexadecimal strings.</p>









<h3># d3.schemeCategory20b </h3>





<p class="p">category20b</p>





<p class="p">An array of twenty categorical colors represented as RGB hexadecimal strings.</p>









<h3># d3.schemeCategory20c</h3> 





<p class="p">category20c</p>





<p class="p">An array of twenty categorical colors represented as RGB hexadecimal strings. This color scale includes color specifications and designs developed by Cynthia Brewer (colorbrewer2.org).</p>









</div>

  <div id="" class="jerome">
<h1>d3: scales, and color by Jerome Cuker</h1>

    



    <p class="p">In <a href="http://mbostock.github.com/protovis/docs/scale.html" onclick="_gaq.push(['_trackEvent', 'outbound-article', 'http://mbostock.github.com/protovis/docs/scale.html', 'protovis']);">protovis</a>, scales were super-useful in just about everything. That much hasn’t changed in d3, even though <a href="https://github.com/mbostock/d3/wiki/Scales" onclick="_gaq.push(['_trackEvent', 'outbound-article', 'https://github.com/mbostock/d3/wiki/Scales', 'd3.scale']);">d3.scale</a> is a bit different from pv.Scale. (do note that <strong>d3.scale</strong> is in lowercase for starters).</p>








<p class="it">En protovis, las escalas eran super útiles en casi todo. Eso no ha cambiado en d3, aunque d3.scale es un poco diferente de pv.Scale. (Tenga en cuenta que d3.scale está en minúsculas para los iniciados).</p>

   <h2>Scales: the main idea</h2>

    



    <p class="p">Simply put: scales transform a number in a certain interval (called the <em>domain</em>) into a number in another interval (called the <em>range</em>).</p>
    







    <p class="it">En pocas palabras: las escalas transforman un número en un intervalo determinado (llamado el dominio) en un número en otro intervalo (llamado el rango.) </p>
   <span class="filler"></span><img alt="Imagen" src="/static/_tGq7dexRJ-img1.png"/><br/><span class="filler"></span> 



   <p class="p">For instance, let’s suppose you <em>know</em> your data is always over 20 and always below 80. You would like to plot it, say, in a bar chart, which can be only 120 pixels tall.<br/><span class="filler"></span>You could, obviously, do the math:</p>
    







    <p class="it">Por ejemplo, supongamos que usted sabe que sus datos están siempre sobre 20 y siempre debajo de 80. Usted quisiera trazarlo, digamos, en un gráfico de barras, que puede ser solamente de 120 pixeles de alto.
Usted podría, obviamente, hacer las matemáticas:</p>

    <div>

      <div id="highlighter_896807" class="syntaxhighlighter jscript">

        <table border="0" cellpadding="0" cellspacing="0">

          <tbody>

            <tr>
              <td class="gutter">
                



                <p class="p">1</p>
              </td>
              <td class="code">
                <div class="container">

                  



                  <p class="p"><code class="jscript plain">.attr(</code><code class="jscript string">"height"</code><code class="jscript plain">, </code><code class="jscript keyword">function</code><code class="jscript plain">(d) {</code><code class="jscript keyword">return</code> <code class="jscript plain">(d-20)*2;})</code></p>

                </div>
              </td>
            </tr>

          </tbody>

        </table>

      </div>

    </div>

    



    <p class="p">But what if you suddenly have more or less space? or your data changes? you’d have to go back to the entrails of your code and make the change. This is very error prone. So instead, you can use a scale:</p>








<p class="it">Pero ¿qué pasa si de repente tiene más o menos espacio? O sus datos cambian? Tendría que volver a las entrañas de su código y hacer el cambio. Esto es muy propenso a errores. Así que en su lugar, puede utilizar una escala:</p>
    <div>

      <div id="highlighter_609869" class="syntaxhighlighter jscript">

        <table border="0" cellpadding="0" cellspacing="0">

          <tbody>

            <tr>
              <td class="gutter">
                



                <p class="p">1</p>
                



                <p class="p">2</p>
                



                <p class="p">3</p>
              </td>
              <td class="code">
                <div class="container">

                  



                  <p class="p"><code class="jscript keyword">var</code> <code class="jscript plain">y=d3.scale.linear().domain(20,80).range(0,120);</code></p>

                  



                  <p class="p"><code class="jscript plain">...</code></p>

                  



                  <p class="p"><code class="jscript plain">.attr(</code><code class="jscript string">"height"</code><code class="jscript plain">, y)</code></p>

                </div>
              </td>
            </tr>

          </tbody>

        </table>

      </div>

    </div>

    



    <p class="p">this is much simpler, elegant, and easy to maintain. Oh, and the latter notation is equivalent to</p>








<p class="it">Esto es mucho más simple, elegante y fácil de mantener. Oh, y la última notación es equivalente a</p>
    <div>

      <div id="highlighter_894022" class="syntaxhighlighter jscript">

        <table border="0" cellpadding="0" cellspacing="0">

          <tbody>

            <tr>
              <td class="gutter">
                



                <p class="p">1</p>
              </td>
              <td class="code">
                <div class="container">

                  



                  <p class="p"><code class="jscript plain">.attr(</code><code class="jscript string">"height"</code><code class="jscript plain">, </code><code class="jscript keyword">function</code><code class="jscript plain">(d) {</code><code class="jscript keyword">return</code> <code class="jscript plain">y(d);})</code></p>

                </div>
              </td>
            </tr>

          </tbody>

        </table>

      </div>

    </div>

    



    <p class="p">… only more legible and shorter.<br/><span class="filler"></span>And, there are tons of possibility with scales.</p>








<p class="it">... Sólo es más legible y más corto.<br/><span class="filler"></span>Y, hay un montón de posibilidades de escalas.</p>
    <h2>Fun with scales</h2>

    



    <p class="p">In d3, quantitative scales can be of several types:</p>

    <ul>

      <li>linear scales (including <em>quantize</em> and <em>quantile</em> scales,</li>









      <li>logarithmic scales,</li>









      <li>power scales (including <em>square root</em> scales)</li>









    </ul>

    



    <p class="p">While they behave differently, they have a lot in common.</p>








<p class="it">Si bien se comportan de manera diferente, tienen mucho en común.</p>
    <h2>Domain and range</h2>

    



    <p class="p">For all scales, with the exception of quantize and quantile scales which are a bit different, domain and range work the same.<br/><span class="filler"></span>First, note that <strong>unlike in protovis</strong>, domain and range take an array as argument. Compare:</p>








<p class="it">Para todas las escalas, con excepción de las escalas de cuantización y cuantiles que son un poco diferentes, dominio y rango trabajan de la misma manera. 
En primer lugar, cabe destacar que a diferencia de Protovis , el dominio y el rango toman una array como argumento. Comparar:</p>
    <div>

      <div id="highlighter_602519" class="syntaxhighlighter jscript">

        <table border="0" cellpadding="0" cellspacing="0">

          <tbody>

            <tr>
              <td class="gutter">
                



                <p class="p">1</p>
                



                <p class="p">2</p>
              </td>
              <td class="code">
                <div class="container">

                  



                  <p class="p"><code class="jscript keyword">var</code> <code class="jscript plain">y=pv.Scale.linear().range(20,60).domain(0,120);</code></p>

                  



                  <p class="p"><code class="jscript keyword">var</code> <code class="jscript plain">y=d3.scale.linear().range([20,60]).domain([0,120]);</code></p>

                </div>
              </td>
            </tr>

          </tbody>

        </table>

      </div>

    </div>

    



    <p class="p">This is because <strong>contrary to protovis</strong>, where domain could be a whole dataset, in d3, domain contains the bounds of the interval that is going to be transformed.<br/><span class="filler"></span>Typically, this is two numbers. If this is more, we are talking about a polypoint scale: there are as many segments in the intervals as there are numbers in the domain (minus one). The range must have as many numbers, and so as many segments. When using the scale, if a number is in the n-th segment of the domain, it is transformed into a number in the n-th segment of the range.



    <p class="p"></p>
    







    <p class="it">Esto es porque al contrario de Protovis , donde el dominio podría ser todo un conjunto de datos, en d3, el dominio contiene los límites del intervalo que va a ser transformado. 
Típicamente, esto es de dos números. Si esto es más, estamos hablando de una escala polypoint: Hay tantos segmentos en los intervalos, ya que hay números en el dominio (menos uno). El rango debe tener tantos números, y así como muchos segmentos. Cuando se utiliza la escala, si un número está en el segmento n-ésimo del dominio, se transforma en un número en el segmento n-ésimo del rango. </p>
<span class="filler"></span><img alt="Imagen" src="/static/_tGq7dexRJ-img2.png"/><br/><span class="filler"></span>





<p class="p">With this example, 30 finds itself in the first segment of the domain. So it’s transformed to a value in the first segment of the range. 60, however, is in the 2nd segment, so it’s transformed into a value in the 2nd segment of the range.<br/><span class="filler"></span>Also, bounds of domain and range need not be numbers, as long as they can be converted to numbers. One useful examples are colors. Color names can be used as range, for instance, to create <em>color ramps</em>:</p>








<p class="it">Con este ejemplo, 30 se encuentra en el primer segmento del dominio. Así que ha transformado a un valor en el primer segmento del rango. 60, sin embargo, está en el segundo segmento, por lo que es transformado en un valor en el segundo segmento del rango. 
Además, límites de dominio y el rango no necesitan ser números, siempre que pueden ser convertidos en números. Uno ejemplos útiles son los colores. Nombres de los colores se pueden utilizar como intervalo de, por ejemplo, para crear rampas de color :</p>
    <div>

      <div id="highlighter_337111" class="syntaxhighlighter jscript">

        <table border="0" cellpadding="0" cellspacing="0">

          <tbody>

            <tr>
              <td class="gutter">
                



                <p class="p">1</p>
              </td>
              <td class="code">
                <div class="container">

                  



                  <p class="p"><code class="jscript keyword">var</code> <code class="jscript plain">ramp=d3.scale.linear().domain([0,100]).range([</code><code class="jscript string">"red"</code><code class="jscript plain">,</code><code class="jscript string">"blue"</code><code class="jscript plain">]);</code></p>

                </div>
              </td>
            </tr>

          </tbody>

        </table>

      </div>

    </div>

    



    <p class="p">This will transform any value betwen 0 and 100 into the corresponding color between red and blue.</p>

    <h3>Clamping</h3>

    



    <p class="p">What happends if the scale is asked to process a number outside of the domain? That’s what clamping controls. If it is set, then the bounds of the range are the minimum and maximum value that can be returned by the scale. Else, the same transformation applies to all numbers, whether they fall within the domain or not.</p>
    







    <p class="it">Qué sucede si se pide la escala para procesar un número fuera del dominio? Para eso son los clamping controls (controles de sujeción). Si son establecidos, entonces los límites del rango son los valores mínimo y máximo que pueden ser devueltos por la escala. La misma transformación se aplica a todos los números, si están incluidos en el dominio o no. </p>
    <span class="filler"></span><img alt="Imagen" src="/static/_tGq7dexRJ-img3.png"/>
    



    <p class="p"><span class="filler"></span>Here, with clamping, the result of the linear transformation is 120, but without it, it’s 160.</p>
    







    <p class="it">En este caso, con clamping, el resultado de la transformación lineal es de 120, pero sin ella, es 160.</p>

    <div>

      <div id="highlighter_768580" class="syntaxhighlighter jscript">

        <table border="0" cellpadding="0" cellspacing="0">

          <tbody>

            <tr>
              <td class="gutter">
                



                <p class="p">1</p>
                



                <p class="p">2</p>
                



                <p class="p">3</p>
                



                <p class="p">4</p>
              </td>
              <td class="code">
                <div class="container">

                  



                  <p class="p"><code class="jscript keyword">var</code> <code class="jscript plain">clamp=d3.scale.linear().domain([20,80]).range([0,120]);</code></p>

                  



                  <p class="p"><code class="jscript plain">clamp(100); // 160</code></p>

                  



                  <p class="p"><code class="jscript plain">clamp.clamp(</code><code class="jscript keyword">true</code><code class="jscript plain">);</code></p>

                  



                  <p class="p"><code class="jscript plain">clamp(100); // 120</code></p>

                </div>
              </td>
            </tr>

          </tbody>

        </table>

      </div>

    </div>

    <h2>Scales and nice numbers</h2>

    



    <p class="p">More often than not, the bounds of the domain and/or those of the ranges will be calculated. So, chances are they won’t be round numbers, or numbers a human would like. Scales, however, come with a bunch of method to address that. d3 keeps in mind that scales are often used to position marks along an axis.</p>








<p class="it">Más a menudo que no, se calcularán los límites del dominio y / o los de los rangos. Por lo tanto, lo más probable es que no serán números redondos, o números que a un ser humano le gustarían. Las escalas, sin embargo, vienen con un montón de métodos para hacer frente a eso. d3 tiene en cuenta que las escalas se utilizan a menudo para marcas de posición a lo largo de un eje.</p>
    <h4>.nice()</h4>

    



    <p class="p">When applied to a scale, the nice method expends the domain to “nicer” numbers. You wouldn’t want your axis to start at -2.347 and end at 7.431, right?<br/><span class="filler"></span>So, there.</p>








<p class="it">Cuando se aplica a una escala, el método .nice() está en el dominio de los números "lindos". Usted no quiere que su eje comience en -2.347 y termine en 7.431, ¿verdad? 
Así que, ahí va.</p>
    <div>

      <div id="highlighter_594402" class="syntaxhighlighter jscript">

        <table border="0" cellpadding="0" cellspacing="0">

          <tbody>

            <tr>
              <td class="gutter">
                



                <p class="p">1</p>
                



                <p class="p">2</p>
                



                <p class="p">3</p>
                



                <p class="p">4</p>
                



                <p class="p">5</p>
              </td>
              <td class="code">
                <div class="container">

                  



                  <p class="p"><code class="jscript keyword">var</code> <code class="jscript plain">data=[-2.347, 4, 5.23,-1.234,6.234,7.431];  // or whatever.</code></p>

                  



                  <p class="p"><code class="jscript keyword">var</code> <code class="jscript plain">y=d3.scale.linear().range([0,120]);</code></p>

                  



                  <p class="p"><code class="jscript plain">y.domain([d3.min(data), d3.max(data)]); // domain takes bounds as arguments, not all numbers </code></p>

                  



                  <p class="p"><code class="jscript plain">y.domain() // [-2.347, 7.431]; </code></p>

                  



                  <p class="p"><code class="jscript plain">y.nice() // [-3, 8] </code></p>

                </div>
              </td>
            </tr>

          </tbody>

        </table>

      </div>

    </div>

    <h4>.ticks(n)</h4>

    



    <p class="p">Given a domain, and a number n (which, <strong>contrary to protovis, is mandatory in d3</strong>), the ticks method will split your domain in (more or less) n convenient, human-readable values, and return an array of these values. This is especially useful to label axes. Passing these values to the scale allows them to position ticks nicely on an axis.</p>








<p class="it">Dado un dominio y un número n (que, contrariamente a Protovis, es obligatorio en d3), el método de las garrapatas (.ticks(n))se dividirá su dominio en (más o menos) n, valores legibles convenientes, y devolvera una array de estos valores. Esto es especialmente útil a los ejes de la etiqueta. La superación de estos valores a la escala a la posición les permite garrapatear muy bien en un eje.</p>
    <div>

      <div id="highlighter_157139" class="syntaxhighlighter jscript">

        <table border="0" cellpadding="0" cellspacing="0">

          <tbody>

            <tr>
              <td class="gutter">
                



                <p class="p">1</p>
                



                <p class="p">2</p>
                



                <p class="p">3</p>
                



                <p class="p">4</p>
                



                <p class="p">5</p>
                



                <p class="p">6</p>
                



                <p class="p">7</p>
                



                <p class="p">8</p>
                



                <p class="p">9</p>
              </td>
              <td class="code">
                <div class="container">

                  



                  <p class="p"><code class="jscript keyword">var</code> <code class="jscript plain">y=d3.scale.linear([20,80]).range([0,120]);</code></p>

                  



                  <p class="p"><code class="jscript plain">...</code></p>

                  



                  <p class="p"><code class="jscript keyword">var</code> <code class="jscript plain">ticks=axis.selectAll(</code><code class="jscript string">"line"</code><code class="jscript plain">)</code></p>

                  



                  <p class="p"><code class="jscript spaces">  </code><code class="jscript plain">.data(y.ticks(4)) // 20, 40, 60 and 80 </code></p>

                  



                  <p class="p"><code class="jscript spaces">  </code><code class="jscript plain">.enter().append(</code><code class="jscript string">"svg:line"</code><code class="jscript plain">);</code></p>

                  



                  <p class="p"><code class="jscript plain">ticks</code></p>

                  



                  <p class="p"><code class="jscript spaces">  </code><code class="jscript plain">.attr(</code><code class="jscript string">"x1"</code><code class="jscript plain">,0).attr(</code><code class="jscript string">"x2"</code><code class="jscript plain">,5)</code></p>

                  



                  <p class="p"><code class="jscript spaces">  </code><code class="jscript plain">.attr(</code><code class="jscript string">"y1"</code><code class="jscript plain">,y).attr(</code><code class="jscript string">"y2"</code><code class="jscript plain">,y)  // short and simple.</code></p>

                  



                  <p class="p"><code class="jscript spaces">  </code><code class="jscript plain">.attr(</code><code class="jscript string">"stroke"</code><code class="jscript plain">,</code><code class="jscript string">"black"</code><code class="jscript plain">);</code></p>

                </div>
              </td>
            </tr>

          </tbody>

        </table>

      </div>

    </div>

    <h4>.rangeRound()</h4>

    



    <p class="p">If used instead of .range(), this will guarantee that the output of the scales are integers, which is better to position marks on the screen with pixel precision than numbers with decimals.</p>








<p class="it">Si se utiliza en lugar de .range(), esto garantiza que la salida de las escalas sean números enteros, que es mejor que las marcas de posición en la pantalla con precisión de píxel de números con decimales.</p>
    <h4>.invert()</h4>

    



    <p class="p">The invert function turns the scale upside down: for one given number in the range, it returns which number of the domain would have been transformed into that number.<br/><span class="filler"></span>For instance:</p>








<p class="it">La función de la escala invertida gira al revés: para un número dado en el rango, no devuelve en qué número del dominio habría sido transformado en ese número.</p>
    <div>

      <div id="highlighter_877198" class="syntaxhighlighter jscript">

        <table border="0" cellpadding="0" cellspacing="0">

          <tbody>

            <tr>
              <td class="gutter">
                



                <p class="p">1</p>
                



                <p class="p">2</p>
                



                <p class="p">3</p>
              </td>
              <td class="code">
                <div class="container">

                  



                  <p class="p"><code class="jscript keyword">var</code> <code class="jscript plain">y=d3.scale.linear([20,80]).range([0,120]);</code></p>

                  



                  <p class="p"><code class="jscript plain">y(50); // 60</code></p>

                  



                  <p class="p"><code class="jscript plain">y.invert(60); // 50</code></p>

                </div>
              </td>
            </tr>

          </tbody>

        </table>

      </div>

    </div>

    



    <p class="p">That’s quite useful, for instance, when a user mouses over a chart, and you would like to know to what value the mouse coordinates correspond.</p>








<p class="it">Eso es muy útil, por ejemplo, cuando un usuario pasa el ratón sobre un gráfico, y le gustaría saber a qué valor de las coordenadas del ratón corresponden.</p>
    <h2>Power scales and log scales</h2>

    



    <p class="p">The <em>linear</em>scale is a function of the form y=ax+b which works for both ends of the domain and range. In the example we’ve used most often until now, this function is really f(x): y=2x-40.</p>
     







     <p class="it">La escala lineal es una función de la forma y = ax + b que funciona para ambos extremos del dominio y el rango. En el ejemplo que hemos utilizado más a menudo hasta ahora, esta función es f (x):. Y = 2x-40.</p>   
    
<p>---</p>
<p class="it">Las potencia y escalas logarítmicas funcionan de la misma manera, sólo que estamos buscando una función de la forma y = ax k + b o y = a.log (x) + b. </p> 

    <p class="p">Power and logarithm scales work the same, only we are looking for a function of the form y=ax<sup>k</sup>+b, or y=a.log(x)+b.</p>
 







    
    

<p class="it">Para las escalas de potencia, se puede especificar un exponente (k) con el método .exponent(). Por ejemplo, si especificamos un exponente de 2, la escala se vería así: </p>

    <p class="p">For the power scales, you can specify an exponent (k) with the .exponent() method. For instance, if we specify an exponent of 2, here is what the scale would look like:</p>
 







 
<img alt="Imagen" src="/static/img/_tGq7dexRJ-img4.png"/>

<p class="it">La ecuación es ahora f (x): y = x² / 50-8. Así que 20 todavía se convierte en 0 y 80 todavía se convierte en 120, pero aparte de eso los valores al principio del dominio serían menor que con la escala lineal, y los que están en el extremo de la escala serán más altos. 
</p>

<p class="p">The equation is now f(x): y=x²/50-8. So 20 still becomes 0 and 80 still becomes 120, but other than that the values at the beginning of the domain would be lower than with the linear scale, and those at the end of the scale will be higher.</p>









    



    <p class="p"><span class="filler"></span>For convenience, d3 includes a d3.scale.sqrt() (the square root scale) so you never have to type d3.scale.pow.exponent(0.5) in full.<br/><span class="filler"></span>Also note that if you are using a log scale, you <strong>cannot</strong> have 0 in the domain.</p>








<p class="it">Por conveniencia, d3 incluye una d3.scale.sqrt () (la escala de raíz cuadrada) para que nunca tenga que escribir d3.scale.pow.exponent (0.5) en su totalidad. <br/>
También tenga en cuenta que si está utilizando una escala logarítmica, que no puede tener 0 en el dominio.</p>
    <h2>Quantize and quantile</h2>

    

<p class="p">cuantizar trabajos con una discreta, y no continuo, rango: en otros términos, la salida de cuantización sólo puede tener un cierto número de valores. </p>

    <p class="p">quantize and quantile are specific linear scales.<br/><span class="filler"></span>quantize works with a discrete, rather than continuous, range: in other terms, the output of quantize can only take a certain number of values.<br/><span class="filler"></span>For instance:</p>






 

<p class="it">la cuantización y cuantil son escalas lineales específicas.<br/> 
 




    <div>

      <div id="highlighter_886870" class="syntaxhighlighter jscript">

        <table border="0" cellpadding="0" cellspacing="0">

          <tbody>

            <tr>
              <td class="gutter">
                



                <p class="p">1</p>
                



                <p class="p">2</p>
                



                <p class="p">3</p>
                



                <p class="p">4</p>
                



                <p class="p">5</p>
                



                <p class="p">6</p>
                



                <p class="p">7</p>
                



                <p class="p">8</p>
                



                <p class="p">9</p>
                



                <p class="p">10</p>
              </td>
              <td class="code">
                <div class="container">

                  



                  <p class="p"><code class="jscript keyword">var</code> <code class="jscript plain">q=d3.scale.quantize().domain([0,10]).range([0,2,8]); </code></p>

                  



                  <p class="p"><code class="jscript plain">q(0); // 0</code></p>

                  



                  <p class="p"><code class="jscript plain">q(3); // 0</code></p>

                  



                  <p class="p"><code class="jscript plain">q(3.33); // 0</code></p>

                  



                  <p class="p"><code class="jscript plain">q(3.34); // 2</code></p>

                  



                  <p class="p"><code class="jscript plain">q(5); // 2</code></p>

                  



                  <p class="p"><code class="jscript plain">q(6.66); // 2</code></p>

                  



                  <p class="p"><code class="jscript plain">q(6.67); // 8</code></p>

                  



                  <p class="p"><code class="jscript plain">q(8); // 8</code></p>

                  



                  <p class="p"><code class="jscript plain">q(1000); // 8</code></p>

                </div>
              </td>
            </tr>

          </tbody>

        </table>

      </div>

    </div>

    

<p class="it">cuantil por otra parte coincide con los valores en el dominio (que, esta vez, es el conjunto de datos completo) con su respectiva cuantil. El número de cuantiles se especifica por la gama. </p>

    <p class="p">quantile on the other hand matches values in the domain (which, this time, is the full dataset) with their respective quantile. The number of quantiles is specified by the range.<br/><span class="filler"></span>For instance:</p>









    <div>

      <div id="highlighter_764421" class="syntaxhighlighter jscript">

        <table border="0" cellpadding="0" cellspacing="0">

          <tbody>

            <tr>
              <td class="gutter">
                



                <p class="p">1</p>
                



                <p class="p">2</p>
                



                <p class="p">3</p>
                



                <p class="p">4</p>
                



                <p class="p">5</p>
                



                <p class="p">6</p>
                



                <p class="p">7</p>
                



                <p class="p">8</p>
                



                <p class="p">9</p>
                



                <p class="p">10</p>
                



                <p class="p">11</p>
                



                <p class="p">12</p>
                



                <p class="p">13</p>
                



                <p class="p">14</p>
                



                <p class="p">15</p>
                



                <p class="p">16</p>
              </td>
              <td class="code">
                <div class="container">

                  



                  <p class="p"><code class="jscript keyword">var</code> <code class="jscript plain">q=d3.scale.quantile().domain([0,1,5,6,2,4,6,2,4,6,7,8]).range([0,100]);</code></p>

                  



                  <p class="p"><code class="jscript plain">q.quantiles(); // [4.5], only one quantile - the median</code></p>

                  



                  <p class="p"><code class="jscript plain">q(0); // 0 </code></p>

                  



                  <p class="p"><code class="jscript plain">q(4); // 0 </code></p>

                  



                  <p class="p"><code class="jscript plain">q(4.499); // 0 </code></p>

                  



                  <p class="p"><code class="jscript plain">q(4.5); // 100 - over the median </code></p>

                  



                  <p class="p"><code class="jscript plain">q(5); // 100 </code></p>

                  



                  <p class="p"><code class="jscript plain">q(10000); // 100 </code></p>

                  



                  <p class="p"><code class="jscript plain">q.range([0,25,50,75,100]);</code></p>

                  



                  <p class="p"><code class="jscript plain">q.quantiles(); // [2, 4, 5.6, 6]; </code></p>

                  



                  <p class="p"><code class="jscript plain">q(0); // 0  </code></p>

                  



                  <p class="p"><code class="jscript plain">q(2); // 25 - greater than the first quantile limit </code></p>

                  



                  <p class="p"><code class="jscript plain">q(3); // 25  </code></p>

                  



                  <p class="p"><code class="jscript plain">q(4); // 50  </code></p>

                  



                  <p class="p"><code class="jscript plain">q(6); // 100  </code></p>

                  



                  <p class="p"><code class="jscript plain">q(10000); // 100 </code></p>

                </div>
              </td>
            </tr>

          </tbody>

        </table>

      </div>

    </div>

    <h2>Ordinal scales</h2>

    
<p class="it">Todas las escalas que hemos visto hasta el momento han sido cuantitativa, pero ¿qué hay de las escalas ordinales? 
La gran diferencia es que las escalas ordinales tienen un dominio discreto, en otras palabras, que a su vez un número limitado de valores en otra cosa, sin preocuparse por lo que es entre esos valores. 
Las escalas ordinales son muy útiles para marcas de posicionamiento a lo largo de un eje x. Supongamos que tiene 10 barras de posición para el gráfico de barras, cada una correspondiente a una categoría, un mes o lo que sea. </p>


    <p class="p">All the scales we’ve seen so far have been quantitative, but how about ordinal scales?<br/><span class="filler"></span>The big difference is that ordinal scales have <strong>a discrete domain</strong>, in other words, they turn a limited number of values into something else, without caring for what’s between those values.<br/><span class="filler"></span>Ordinal scales are very useful for positioning marks along an x axis. Let’s suppose you have 10 bars to position for your bar chart, each corresponding to a category, a month or whatever.<br/><span class="filler"></span>For instance:</p>









    <div>

      <div id="highlighter_653218" class="syntaxhighlighter jscript">

        <table border="0" cellpadding="0" cellspacing="0">

          <tbody>

            <tr>
              <td class="gutter">
                



                <p class="p">1</p>
                



                <p class="p">2</p>
                



                <p class="p">3</p>
                



                <p class="p">4</p>
              </td>
              <td class="code">
                <div class="container">

                  



                  <p class="p"><code class="jscript keyword">var</code> <code class="jscript plain">x=d3.scale.ordinal()</code></p>

                  



                  <p class="p"><code class="jscript spaces">  </code><code class="jscript plain">.domain([</code><code class="jscript string">"Sunday"</code><code class="jscript plain">,</code><code class="jscript string">"Monday"</code><code class="jscript plain">,</code><code class="jscript string">"Tuesday"</code><code class="jscript plain">,</code><code class="jscript string">"Wednesday"</code><code class="jscript plain">,</code><code class="jscript string">"Thursday"</code><code class="jscript plain">,</code><code class="jscript string">"Friday"</code><code class="jscript plain">,</code><code class="jscript string">"Saturday"</code><code class="jscript plain">]) // 7 items </code></p>

                  



                  <p class="p"><code class="jscript spaces">  </code><code class="jscript plain">.rangeBands([0,120]);</code></p>

                  



                  <p class="p"><code class="jscript plain">x(</code><code class="jscript string">"Tuesday"</code><code class="jscript plain">); // 34.285714285714285 </code></p>

                </div>
              </td>
            </tr>

          </tbody>

        </table>

      </div>

    </div>

    

<p class="it">Hay 3 posibilidades para la gama. Dos son similares: los metodos .rangePoints () y .rangeBands (), que trabajan con una serie de dos números - es decir .rangeBands([0120]). El último es para especificar todos los valores en el rango con .range().</p>

    <p class="p">There are 3 possibilites for range. Two are similar: the .rangePoints() and .rangeBands() methods, which both work with an array of two numbers – i.e. .rangeBands([0,120]). The last one is to specify all values in the range with .range().</p>









    <h2>rangePoints() and rangeBands()</h2>

    

<p class="it">Con .rangePoints(intervalo), d3 encaja n puntos dentro del intervalo, siendo n el número de categorías en el dominio. En ese caso, el valor del primer punto es el comienzo del intervalo, el del último punto es el final del intervalo.</p> 

    <p class="p">With .rangePoints(<em>interval</em>), d3 fits n points within the interval, n being the number of categories in the domain. In that case, the value of the first point is the beginning of the interval, that of the last point is the end of the interval.</p>









    

<p class="it">Con .rangeBands ( intervalo ), D3 encaja n bandas dentro del intervalo. En este caso, el valor del último elemento en el dominio es menor que el límite superior del intervalo. 
Esos métodos reemplazan los métodos Protovis .split () y .splitBanded (). </p>

    <p class="p"><span class="filler"></span>With .rangeBands(<em>interval</em>), d3 fit n <em>bands</em> within the interval. Here, the value of the last item in the domain is less than the upper bound of the interval.<br/><span class="filler"></span>Those methods <strong>replace the protovis methods</strong> .split() and .splitBanded().</p>
  








    
    <span class="filler"></span><img alt="Imagen" src="/static/_tGq7dexRJ-img5.png"/><br/><span class="filler"></span>This chart illustrates the difference between using rangeBands and rangePoints.</p>


    <div>

      <div id="highlighter_576383" class="syntaxhighlighter jscript">

        <table border="0" cellpadding="0" cellspacing="0">

          <tbody>

            <tr>
              <td class="gutter">
                



                <p class="p">1</p>
                



                <p class="p">2</p>
                



                <p class="p">3</p>
                



                <p class="p">4</p>
                



                <p class="p">5</p>
                



                <p class="p">6</p>
                



                <p class="p">7</p>
              </td>
              <td class="code">
                <div class="container">

                  



                  <p class="p"><code class="jscript keyword">var</code> <code class="jscript plain">x=d3.scale.ordinal()</code></p>

                  



                  <p class="p"><code class="jscript spaces">  </code><code class="jscript plain">.domain([</code><code class="jscript string">"Sunday"</code><code class="jscript plain">,</code><code class="jscript string">"Monday"</code><code class="jscript plain">,</code><code class="jscript string">"Tuesday"</code><code class="jscript plain">,</code><code class="jscript string">"Wednesday"</code><code class="jscript plain">,</code><code class="jscript string">"Thursday"</code><code class="jscript plain">,</code><code class="jscript string">"Friday"</code><code class="jscript plain">,</code><code class="jscript string">"Saturday"</code><code class="jscript plain">]);</code></p>

                  



                  <p class="p"><code class="jscript plain">x.rangePoints([0,120]);</code></p>

                  



                  <p class="p"><code class="jscript plain">x(</code><code class="jscript string">"Saturday"</code><code class="jscript plain">); // 120 </code></p>

                  



                  <p class="p"><code class="jscript plain">x.rangeBands([0,120]);</code></p>

                  



                  <p class="p"><code class="jscript plain">x(</code><code class="jscript string">"Saturday"</code><code class="jscript plain">); // 102.85714285714286</code></p>

                  



                  <p class="p"><code class="jscript plain">x(</code><code class="jscript string">"Saturday"</code><code class="jscript plain">)+x.rangeBand(); // 120 </code></p>

                </div>
              </td>
            </tr>

          </tbody>

        </table>

      </div>

    </div>

    <h4>the range method</h4>

    

<p class="it">Por último, también podemos utilizar el método .range con varios valores. 
Podemos especificar el dominio, o no. Entonces, si utilizamos una escala tan grande en un valor que no es parte del dominio (o si el dominio se deja vacío), este valor se agrega al dominio. Si existen N valores en el rango, y más en el dominio, entonces el n + 1ª valor del dominio se corresponde con el 1er valor en el rango, etc.</p>

    <p class="p">Finally, we can also use the .range method with several values.<br/><span class="filler"></span>We can specify the domain, or not. Then, if we use such a scale on a value which is not part of the domain (or if the domain is left empty), this value is added to the domain. If there are <em>n</em> values in the range, and more in the domain, then the n+1<sup>th</sup> value of the doamin is matched with the 1st value in the range, etc.</p>









    <div>

      <div id="highlighter_523836" class="syntaxhighlighter jscript">

        <table border="0" cellpadding="0" cellspacing="0">

          <tbody>

            <tr>
              <td class="gutter">
                



                <p class="p">1</p>
                



                <p class="p">2</p>
                



                <p class="p">3</p>
                



                <p class="p">4</p>
                



                <p class="p">5</p>
                



                <p class="p">6</p>
              </td>
              <td class="code">
                <div class="container">

                  



                  <p class="p"><code class="jscript keyword">var</code> <code class="jscript plain">x=d3.scale.ordinal().range([</code><code class="jscript string">"hello"</code><code class="jscript plain">, </code><code class="jscript string">"world"</code><code class="jscript plain">]); </code></p>

                  



                  <p class="p"><code class="jscript plain">x.domain(); //  [] - empty still. </code></p>

                  



                  <p class="p"><code class="jscript plain">x(0); // "hello" </code></p>

                  



                  <p class="p"><code class="jscript plain">x(1); // "world"  </code></p>

                  



                  <p class="p"><code class="jscript plain">x(2); // "hello" </code></p>

                  



                  <p class="p"><code class="jscript plain">x.domain(); // [0,1,2]</code></p>

                </div>
              </td>
            </tr>

          </tbody>

        </table>

      </div>

    </div>

    <h2>Color palettes</h2>

    

  <p class="it">A diferencia de Protovis , que ellos tenían bajo pv.Colors - es decir pv.Colors.category10 (), en d3, a una función de paletas de colores se puede acceder a través de escalas. Pues bien, incluso en Protovis que habían sido escalas ordinales todo el tiempo, no sólo se denominan de esta manera.</p>
    1a1radcontrol

    <p class="p"><strong>Unlike in protovis</strong>, which had them under pv.Colors – i.e. pv.Colors.category10(), in d3, built-in color palettes can be accessed through scales. Well, even in protovis they had been ordinal scales all along, only not called this way.</p>
    










 <p class="it">Hay 4 incorporado en la paleta de colores en Protovis:</p>
    <p class="p"><span class="filler"></span>There are <a href="https://github.com/mbostock/d3/wiki/Ordinal-Scales#category10" onclick="_gaq.push(['_trackEvent', 'outbound-article', 'https://github.com/mbostock/d3/wiki/Ordinal-Scales#category10', '4 built-in color palette']);">4 built-in color palette</a> in protovis:</p>
    











    <p class="p">d3.scale.category10(), d3.scale.category20(), d3.scale.category20b(), and d3.scale.category20c().</p>

    

<p class="it">Una paleta como d3.scale.category10 () funciona exactamente igual que una escala ordinal.</p>

    <p class="p">A palette like d3.scale.category10() works exactly like an ordinal scale.</p>









    <div>

      <div id="highlighter_327059" class="syntaxhighlighter jscript">

        <table border="0" cellpadding="0" cellspacing="0">

          <tbody>

            <tr>
              <td class="gutter">
                



                <p class="p">1</p>
                



                <p class="p">2</p>
                



                <p class="p">3</p>
                



                <p class="p">4</p>
                



                <p class="p">5</p>
                



                <p class="p">6</p>
                



                <p class="p">7</p>
                



                <p class="p">8</p>
                



                <p class="p">9</p>
                



                <p class="p">10</p>
                



                <p class="p">11</p>
                



                <p class="p">12</p>
                



                <p class="p">13</p>
                



                <p class="p">14</p>
              </td>
              <td class="code">
                <div class="container">

                  



                  <p class="p"><code class="jscript keyword">var</code> <code class="jscript plain">p=d3.scale.category10();</code></p>

                  



                  <p class="p"><code class="jscript keyword">var</code> <code class="jscript plain">r=p.range(); // ["#1f77b4", "#ff7f0e", "#2ca02c", "#d62728", "#9467bd", 
                      // "#8c564b", "#e377c2", "#7f7f7f", "#bcbd22", "#17becf"]</code></p>

                  



                  <p class="p"><code class="jscript keyword">var</code> <code class="jscript plain">s=d3.scale.ordinal().range(r); </code></p>

                  



                  <p class="p"><code class="jscript plain">p.domain(); // [] - empty</code></p>

                  



                  <p class="p"><code class="jscript plain">s.domain(); // [] - empty, see above</code></p>

                  



                  <p class="p"><code class="jscript plain">p(0); // "#1f77b4"</code></p>

                  



                  <p class="p"><code class="jscript plain">p(1); // "#ff7f0e"</code></p>

                  



                  <p class="p"><code class="jscript plain">p(2); // "#2ca02c"</code></p>

                  



                  <p class="p"><code class="jscript plain">p.domain(); // [0,1,2];</code></p>

                  



                  <p class="p"><code class="jscript plain">s(0); // "#1f77b4"</code></p>

                  



                  <p class="p"><code class="jscript plain">s(1); // "#ff7f0e"</code></p>

                  



                  <p class="p"><code class="jscript plain">s(2); // "#2ca02c"</code></p>

                  



                  <p class="p"><code class="jscript plain">s.domain(); // [0,1,2];</code></p>

                </div>
              </td>
            </tr>

          </tbody>

        </table>

      </div>

    </div>

    

<p class="it">Es de destacar que en d3, devuelve cadenas de paleta de colores, no se opone pv.Color como en Protovis. </p>

    <p class="p">It’s noteworthy that in d3, color palette return strings, not pv.Color objects like in protovis.<br/><span class="filler"></span>Also:</p>









    <div>

      <div id="highlighter_388830" class="syntaxhighlighter jscript">

        <table border="0" cellpadding="0" cellspacing="0">

          <tbody>

            <tr>
              <td class="gutter">
                



                <p class="p">1</p>
                



                <p class="p">2</p>
              </td>
              <td class="code">
                <div class="container">

                  



                  <p class="p"><code class="jscript plain">d3.scale.category10(1); // this doesn't work </code></p>

                  



                  <p class="p"><code class="jscript plain">d3.scale.category10()(1); // this is the way. </code></p>

                </div>
              </td>
            </tr>

          </tbody>

        </table>

      </div>

    </div>

    <h2>Colors</h2>

    

<p class="it">En comparación con Protovis, d3.color es más simple. La razón principal es que Protovis manejan el color y la transparencia junto con el objeto pv.Color, mientras que en SVG, los dos son distintos atributos: manejar el color de fondo de un objeto relleno con relleno , su transparencia con la opacidad , el color del contorno con accidente cerebrovascular y la transparencia de ese color con accidente cerebrovascular-opacidad .</p>

    <p class="p">Compared to protovis, d3.color is simpler. The main reason is that protovis handled color and transparency together with the pv.Color object, whereas in SVG, those two are distinct attributes: you handle the background color of a filled object with <em>fill</em>, its transparency with <em>opacity</em>, the color of the outline with <em>stroke</em> and the transparency of that color with <em>stroke-opacity</em>.</p>









    


<p class="it">d3 tiene dos objetos de color: d3_Rgb y d3_Hsl, que describen colores en los dos de los espacios de color más populares: rojo / verde / azul, y el tono / saturación / luz.</p>
    <p class="p">d3 has two color objects: d3_Rgb and d3_Hsl, which describe colors in the two of the most popular color spaces: red/green/blue, and hue/saturation/light.</p>









    

<p class="it">Con d3.color, puede realizar operaciones de este tipo de objetos, como la conversión de colores entre distintos formatos, o que los colores sean más claras u oscuras.</p>

    <p class="p">With d3.color, you can make operations on such objects, like converting colors between various formats, or make colors lighter or darker.</p>









    

<p class="it">d3.rgb ( de color ), y d3.hsl ( de color ) crea este tipo de objetos. 
En este contexto, el color puede ser (directamente desde el manual: https://github.com/d3/d3/wiki/Colors):</p>

    <p class="p">d3.rgb(<em>color</em>), and d3.hsl(<em>color</em>) create such objects.<br/><span class="filler"></span>In this context, <em>color</em> can be (straight from <a href="https://github.com/mbostock/d3/wiki/Colors" onclick="_gaq.push(['_trackEvent', 'outbound-article', 'https://github.com/mbostock/d3/wiki/Colors', 'the manual']);">the manual</a>):</p>
    









    <ul>

      <li>rgb decimal – “rgb(255,255,255)”</li>

      <li>hsl decimal – “hsl(120,50%,20%)”</li>

      <li>rgb hexadecimal – “#ffeeaa”</li>

      <li>rgb shorthand hexadecimal – “#fea”</li>

      <li>named – “red”, “white”, “blue”</li>

    </ul>








<p class="it">Una vez que tenga ese objeto, puede hacer que sea más brillante o más oscura con el método apropiado. 
Puede utilizar .toString() para obtener de nuevo en formato RGB hexadecimal (decimal o HSL), y .rgb() o .hsl() para convertir al objeto en otro espacio de color.</p>
    



    <p class="p">Once you have that object, you can make it brighter or darker with the appropriate method.<br/><span class="filler"></span>You can use .toString() to get it back in rgb hexadecimal format (or hsl decimal), and .rgb() or .hsl() to convert it to the object in the other color space.</p>

    <div>

      <div id="highlighter_172569" class="syntaxhighlighter jscript">

        <table border="0" cellpadding="0" cellspacing="0">

          <tbody>

            <tr>
              <td class="gutter">
                



                <p class="p">1</p>
                



                <p class="p">2</p>
                



                <p class="p">3</p>
                



                <p class="p">4</p>
                



                <p class="p">5</p>
                



                <p class="p">6</p>
                



                <p class="p">7</p>
                



                <p class="p">8</p>
              </td>
              <td class="code">
                <div class="container">

                  



                  <p class="p"><code class="jscript keyword">var</code> <code class="jscript plain">c=d3.rgb(</code><code class="jscript string">"violet"</code><code class="jscript plain">) // d3_Rgb object</code></p>

                  



                  <p class="p"><code class="jscript plain">c.toString(); // "#ee82ee"</code></p>

                  



                  <p class="p"><code class="jscript plain">c.darker().toString(); // "#a65ba6"</code></p>

                  



                  <p class="p"><code class="jscript plain">c.darker(2).toString(); // "#743f74" - even darker</code></p>

                  



                  <p class="p"><code class="jscript plain">c.brighter().toString();// "ffb9ff"</code></p>

                  



                  <p class="p"><code class="jscript plain">c.brighter(0.1).toString(); // "#f686f6" - only slightly brighter </code></p>

                  



                  <p class="p"><code class="jscript plain">c.hsl(); // d3_Hsl object </code></p>

                  



                  <p class="p"><code class="jscript plain">c.hsl().toString()  // "hsl(300, 76, 72)" </code>
                  </p>

                </div>
              </td>
            </tr>

          </tbody>

        </table>

      </div>



        <h1 class="title">Chapter 7. Scales</h1>

    <p class="it"><strong>"Las escalas son las funciones que se asignan desde un dominio de entrada a un rango de salida".</strong></p>
    <p class="p" id="scales_are_fun">“Scales are functions that map from an input domain to an output range.”<a id="ix_scales" class="indexterm" href=""></a></p>

    <p class="it">Esa es la definición de escalas D3 de Mike Bostock, y no hay una manera más clara que decirlo.</p>
    <p class="p" id="thats_mike_bos">That’s <a class="ulink" href="https://github.com/mbostock/d3/wiki/Quantitative-Scales" target="_top">Mike Bostock’s definition of D3 scales</a>, and there is no clearer way to say it.<a id="id521048" class="indexterm" href=""></a></p>

    <p class="it">Los valores en cualquier conjunto de datos es poco probable que se correspondan exactamente con las medidas de píxeles para su uso en su visualización. Las escalas proporcionan una manera conveniente para mapear los valores de los datos a los nuevos valores útiles a los fines de la visualización.</p>
    <p class="p" id="the_values_in_a">The values in any dataset are unlikely to correspond exactly to pixel measurements for use in your visualization. Scales provide a convenient way to map those data values to new values useful for visualization purposes.</p>

    <p class="it">Las escalas D3 son funciones con parámetros que se definen. Una vez que se crean, se llama a la función de escala, le pasa un valor de datos, y devuelve un valor limpio de salida escalado. Se pueden definir y utilizar tantas escalas como desee.</p>
    <p class="p" id="d_scales_are_f">D3 scales are <span class="emphasis"><em>functions</em></span> with parameters that you define. Once they are created, you call the <code class="literal">scale</code> function, pass it a data value, and it nicely returns a scaled output value. You can define and use as many scales as you like.<a id="id521081" class="indexterm" href=""></a></p>

    <p class="it">Podría ser tentador pensar en una escala como algo que aparece visualmente al final de un conjunto de imágenes como de marcas de graduación, lo que indica una progresión de valores. No se deje engañar! Esas marcas de graduación son parte de un eje, que es una representación visual que representa una escala. Una escala es una relación matemática, sin representación visual directa. Lo invito a pensar en escalas y ejes como dos elementos diferentes pero relacionados entre si.</p>
    <p class="p" id="it_might_be_tem">It might be tempting to think of a scale as something that appears visually in the final image—like a set of tick marks, indicating a progression of values. <span class="emphasis"><em>Do not be fooled!</em></span> Those tick marks are part of an <span class="emphasis"><em>axis</em></span>, which is a <span class="emphasis"><em>visual representation</em></span> of a scale. A scale is a mathematical relationship, with no direct visual output. I encourage you to think of scales and axes as two different, yet related, elements.<a id="id521111" class="indexterm" href=""></a><a id="id521119" class="indexterm" href=""></a></p>

    <p class="it">Este capítulo trata solamente sobre escalas lineales, debido a que son más comunes y más fáciles de entender. Una vez que entienda las escalas lineales, las demás - ordinales, logarítmica, de raíz cuadrada, y así sucesivamente - serán un pedazito de to
    <p class="p" id="this_chapter_ad">This chapter addresses only <a class="ulink" href="https://github.com/mbostock/d3/wiki/Quantitative-Scales#wiki-linear" target="_top"><span class="emphasis"><em>linear</em></span></a> scales, because they are most common and easiest understood. Once you understand linear scales, the others—ordinal, logarithmic, square root, and so <span class="keep-together">on—will be a piece of cake.</span><a id="id521148" class="indexterm" href=""></a></p>

          <h2 class="title">Apples and Pixels</h2>

      <p class="it">Imagine que el siguiente conjunto de datos representa el número de manzanas que se venden cada mes en una fruteria de carretera:</p>
      <p class="p" id="imagine_that_th">Imagine that the following dataset represents the number of apples sold at a roadside fruit stand each month:</p>

      <pre class="programlisting" data-language="javascript" id="var_dataset___id14">var dataset = [ 100, 200, 300, 400, 500 ];</pre>

      <p class="it">En primer lugar, esta es una gran noticia, ya que el stand tiene una venta de 100 manzanas adicionales por mes! Los negocios están prosperando. Para mostrar este éxito, usted desea hacer un gráfico de barras que ilustre el ascenso empinado de las ventas de manzanas, con cada valor de datos correspondiendo a la altura de una barra.</p>
      <p class="p" id="first_of_all_t">First of all, this is great news, as the stand is selling 100 additional apples each month! Business is booming. To showcase this success, you want to make a bar chart illustrating the steep upward climb of apple sales, with each data value corresponding to the height of one bar.</p>

      <p class="it">Hasta ahora, hemos usado los valores de datos directamente como valores de visualización, haciendo caso omiso de las diferencias de unidades. Así que si se vendieron 500 manzanas, la barra correspondiente sería de 500 píxeles de alto.</p>
      <p class="p" id="until_now_wev">Until now, we’ve used data values directly as display values, ignoring unit differences. So if 500 apples were sold, the corresponding bar would be 500 pixels tall.</p>

      <p class="it">Eso podría funcionar, pero ¿qué pasa el próximo mes, cuando se vendan 600 manzanas? Y un año más tarde, cuando se vendan 1.800 manzanas? Su público tendría que comprar pantallas cada vez más grandes sólo para ser capaz de ver en toda su altura esas barras de manzana! (Mmm, barras de manzana!)</p>
      <p class="p" id="that_could_work">That could work, but what about next month, when 600 apples are sold? And a year later, when 1,800 apples are sold? Your audience would have to purchase ever-larger displays just to be able to see the full height of those very tall apple bars! (Mmm, apple bars!)</p>

      <p class="it">Aquí es donde aparecen las escalas. Debido a que las manzanas no son píxeles (que tampoco son naranjas), se necesitan escalas para comunicarse entre ellas.</p>
      <p class="p" id="this_is_where_s">This is where scales come in. Because apples are not pixels (which are also not oranges), we need scales to translate between them.</p>


          <h2 class="title">Domains and Ranges</h2>


      <p class="it">El dominio de entrada de una escala es el rango de posibles valores de datos de entrada. Dados los  datos anteriores de las manzanas, los dominios de entrada apropiados serían o bien 100 y 500 o bien 0 y 500 (los valores máximo y mínimo y el conjunto de datos).</p>
      <p class="p" id="a_scales_input">A scale’s <span class="emphasis"><em>input domain</em></span> is the range of possible input data values. Given the preceding apples data, appropriate input domains would be either 100 and 500 (the minimum and maximum values of the dataset) or 0 and 500.<a id="id521300" class="indexterm" href=""></a><a id="id521305" class="indexterm" href=""></a><a id="id521311" class="indexterm" href=""></a></p>

      <p class="it">El rango de salida de una escala es el rango de posibles valores de salida, que se utiliza comúnmente como valores indicados en unidades de píxel. El rango de salida es totalmente suyo, lo maneja usted, como el diseño de la información. Si decide que la barra de manzanas séa más corta será de 10 píxeles de alto y la más alta será de 350 píxeles de alto, entonces podría establecer un rango de salida de 10 y 350.</p>
      <p class="p" id="a_scales_outpu">A scale’s <span class="emphasis"><em>output range</em></span> is the range of possible output values, commonly used as display values in pixel units. The output range is completely up to you, as the information designer. If you decide the shortest apple bar will be 10 pixels tall, and the tallest will be 350 pixels tall, then you could set an output range of 10 and 350.</p>


      <p class="it">Por ejemplo, crear una escala con un dominio de entrada de <code class="literal">[100,500]</code> y un rango de salida de <code class="literal">[10,350]</code>. Si se entregarán el valor de entrada baja de 100 a esa escala, sería devolver su valor de más bajo rango, 10. Si usted le dio 500, escupiria en la vuelta 350. Si usted le dio 300, le entregaría 180 de nuevo a usted en una bandeja de plata. (300 está en el centro del dominio, y 180 está en el centro del rango.)</p>
      <p class="p" id="for_example_cr">For example, create a scale with an input domain of <code class="literal">[100,500]</code> and an output range of <code class="literal">[10,350]</code>. If you handed the low input value of <code class="literal">100</code> to that scale, it would return its lowest range value, <code class="literal">10</code>. If you gave it <code class="literal">500</code>, it would spit back <code class="literal">350</code>. If you gave it <code class="literal">300</code>, it would hand <code class="literal">180</code> back to you on a silver platter. (<code class="literal">300</code> is in the center of the domain, and <code class="literal">180</code> is in the center of the range.)</p>


      <p class="it">Podemos visualizar el dominio y el rango como ejes correspondientes, de lado a lado, como se muestra en la Figura 7-1.</p>
      <p class="p" id="we_can_visualiz">We can visualize the domain and range as corresponding axes, side-by-side, displayed in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch07.html#input_output_axes" title="Figure 7-1. An input domain and an output range, visualized as parallel axes">Figure 7-1</a>.</p>

<div>
            <img src="/static/fHijhiLmT1-img1.png" alt="An input domain and an output range, visualized as parallel axes"/>

        <p class="fig">Figure 7-1. An input domain and an output range, visualized as parallel axes</p>

</div>
      <p class="it">Una cosa más: para evitar que el cerebro pueda mezclar la terminología dominio de entrada y rango de salida, me gustaría proponer un poco de ejercicio. Cuando digo "de entrada", se dice "dominio". Entonces digo "de salida", y se dice "rango". Listo? Bueno:</p>


      <p class="p" id="one_more_thing_id2">One more thing: to prevent your brain from mixing up the <span class="emphasis"><em>input domain</em></span> and <span class="emphasis"><em>output range</em></span> terminology, I’d like to propose a little exercise. When I say “input,” you say “domain.” Then I say “output,” and you say “range.” Ready? Okay:</p>
      <div class="blockquote">

        <blockquote class="blockquote">

          <p class="it">¡Entrada! ¡Dominio!</p>


          <p class="p" id="input_domain_id1">Input! Domain!</p>
        </blockquote>

      </div>

      <div class="blockquote">

        <blockquote class="blockquote">

          <p class="it">¡Salida! ¡Rango!</p>


          <p class="p" id="output_range_id1">Output! Range!</p>
        </blockquote>

      </div>

      <div class="blockquote">

        <blockquote class="blockquote">

          <p class="it">¡Entrada! ¡Dominio!</p>


          <p class="p" id="input_domain_id2">Input! Domain!</p>
        </blockquote>

      </div>

      <div class="blockquote">

        <blockquote class="blockquote">

          <p class="it">¡Salida! ¡Rango!</p>


          <p class="p" id="output_range_id2">Output! Range!</p>
        </blockquote>

      </div>

      <p class="it">¿Lo tengo? Estupendo.</p>


      <p class="p" id="got_it_great">Got it? Great.</p>
    </div>

    <div class="sect1" data-original-filename="7_scales.asciidoc" id="_normalization">

      <div class="titlepage">

        <div>

          <h2 class="title">Normalization</h2>

        </div>

      </div>

      <p class="it">Si está familiarizado con el concepto de normalización, podría serle útil saber que, es una escala lineal, eso es todo lo que realmente está pasando aquí.</p>


      <p class="p" id="if_youre_famil_id3">If you’re familiar with the concept of <span class="emphasis"><em>normalization</em></span>, it might be helpful to know that, with a linear scale, that’s all that is really going on here.<a id="id521500" class="indexterm" href=""></a><a id="id521508" class="indexterm" href=""></a></p>
      <p class="it">La normalización es el proceso de asignar un valor numérico a un nuevo valor entre 0 y 1, en base a los posibles valores mínimo y máximo. Por ejemplo, con 365 días en el año, el día número 310 se asigna a aproximadamente 0,85, o 85 por ciento del camino a través del año.</p>


      <p class="p" id="normalization_i">Normalization is the process of mapping a numeric value to a new value between 0 and 1, based on the possible minimum and maximum values. For example, with 365 days in the year, day number 310 maps to about 0.85, or 85 percent of the way through the year.</p>
      <p class="it">Con escalas lineales, sólo estamos dejando a d3 manejar la matemática del proceso de normalización. El valor de entrada se normaliza de acuerdo con el dominio, y luego el valor normalizado se escala al rango de salida.</p>


      <p class="p" id="with_linear_sca">With linear scales, we are just letting D3 handle the math of the normalization process. The input value is normalized according to the domain, and then the normalized value is scaled to the output range.</p>
    </div>

    <div class="sect1" data-original-filename="7_scales.asciidoc" id="_creating_a_scale">

      <div class="titlepage">

        <div>

          <h2 class="title">Creating a Scale</h2>

        </div>

      </div>

      <p class="it">A los generadores de funciones de escala D3 se tiene acceso con <strong>d3.scale</strong> seguido por el tipo de escala que desee. Recomiendo la apertura del archivo 01_scale_test.html y escribir lo siguiente en la consola:</p>


      <p class="p" id="ds_scale_func">D3’s scale function generators are accessed with <code class="literal">d3.scale</code> followed by<a id="id521552" class="indexterm" href=""></a> the type of scale you want. I recommend opening up the sample code page <span class="emphasis"><em>01_scale_test.html</em></span> and typing each of the following into the console:</p>
      <pre class="programlisting" data-language="javascript" id="var_scale__d_id1">var scale = d3.scale.linear();</pre>

      <p class="it">¡Felicitaciones! Ahora la escala es una función a la que se le pueden pasar valores de entrada. (No se deje engañar por la <code class="literal">var</code>. Recuerde que en JavaScript, las variables pueden almacenar funciones.)</p>


      <p class="p" id="congratulations_id1">Congratulations! Now <code class="literal">scale</code> is a function to which you can pass input values. (Don’t be misled by the <code class="literal">var</code>. Remember that in JavaScript, variables can store functions.)</p>
      <pre class="programlisting" data-language="javascript" id="scale_r_id1">scale(2.5);  //Returns 2.5</pre>

      <p class="it">Debido a que no hemos establecido un dominio y un rango, esta función mapeara la entrada y la salida en una escala de 1:1. Es decir, todo lo que entra se devolverá sin cambios.</p>


      <p class="p" id="because_we_have">Because we haven’t set a domain and a range yet, this function will map input to output on a 1:1 scale. That is, whatever we input will be returned unchanged.</p>
      <p class="it">Podemos establecer el dominio de entrada de la escala para <code class="literal">100,500</code> pasando esos valores con el método de <span class="keep-together"><code class="literal">domain()</code></span> como un array. Tenga en cuenta los corchetes que indican un array:</p>


      <p class="p" id="we_can_set_the_">We can set the scale’s input domain to <code class="literal">100,500</code> by passing those values to the <span class="keep-together"><code class="literal">domain()</code></span> method as an array. Note the hard brackets indicating an array:</p>
      <pre class="programlisting" data-language="javascript" id="scaledomain">scale.domain([100, 500]);</pre>

      <p class="it">Ajuste el rango de salida de forma similar, con un <code class="literal">range()</code>:</p>


      <p class="p" id="set_the_output_">Set the output range in similar fashion, with <code class="literal">range()</code>:</p>
      <pre class="programlisting" data-language="javascript" id="scalerange">scale.range([10, 350]);</pre>

      <p class="it">Estos pasos se pueden hacer por separado, como se acaba de mostrar, o encadenados juntos en una sola línea de código:</p>


      <p class="p" id="these_steps_can">These steps can be done separately, as just shown, or chained together into one line of code:</p>
      <pre class="programlisting" data-language="javascript" id="var_scale__d_id2">var scale = d3.scale.linear()
                    .domain([100, 500])
                    .range([10, 350]);</pre>

      <p class="it">De cualquier manera, nuestra escala está lista para usarse!</p>


      <p class="p" id="either_way_our">Either way, our scale is ready to use!</p>
      <pre class="programlisting" data-language="javascript" id="scale_r_id2">scale(100);  //Returns 10
scale(300);  //Returns 180
scale(500);  //Returns 350</pre>

      <p class="it">Por lo general, se llamará a las funciones de escala dentro de un método attr() o similar, no por su propia cuenta. Vamos a modificar nuestra visualización gráfica de dispersión al usar escalas dinámicas.</p>


      <p class="p" id="typically_you_">Typically, you will call scale functions from within an <code class="literal">attr()</code> method or similar, not on their own. Let’s modify our scatterplot visualization to use dynamic scales.<a id="id522089" class="indexterm" href=""></a><a id="id522097" class="indexterm" href=""></a><a id="id522103" class="indexterm" href=""></a></p>
    </div>

    <div class="sect1" data-original-filename="7_scales.asciidoc" id="_scaling_the_scatterplot">

      <div class="titlepage">

        <div>

          <h2 class="title">Scaling the Scatterplot</h2>

        </div>

      </div>

      <p class="it">Revisitamos nuestra base de datos de la gráfica de dispersión:</p>


      <p class="p" id="to_revisit_our_">To revisit our dataset from the scatterplot:</p>
      <pre class="programlisting" data-language="javascript" id="var_dataset___id15">var dataset = [
                [5, 20], [480, 90], [250, 50], [100, 33], [330, 95],
                [410, 12], [475, 44], [25, 67], [85, 21], [220, 88]
              ];</pre>

      <p class="it">Usted recordará que este conjunto de datos es un array de arrays. Hemos trazado el primer valor de cada array en el eje <strong>x</strong>, y el segundo valor en el eje <strong>y</strong>. Vamos a empezar con el eje <strong>x</strong>.</p>


      <p class="p" id="youll_recall_t_id2">You’ll recall that this <code class="literal">dataset</code> is an array of arrays. We mapped the first value in each array onto the x-axis, and the second value onto the y-axis. Let’s start with the x-axis.</p>
      <p class="it">Con sólo echar un vistazo a los valores de <strong>x</strong>, parece que van desde 5 hasta 480, por lo que un razonable dominio de entrada a especificar podría ser <code class="literal">0,500</code>, ¿verdad?</p>


      <p class="p" id="just_by_eyeball">Just by eyeballing the <code class="literal">x</code> values, it looks like they range from 5 to 480, so a reasonable input domain to specify might be <code class="literal">0,500</code>, right?</p>
      <p class="it">¿Por qué me mira así? Oh, porque quiere mantener su código flexible y escalable, por lo que seguirá trabajando así incluso si cambian los datos en el futuro. ¡Muy inteligente! Recuerde, si estábamos construyendo un panel de datos para el stand de manzanas al borde de la carretera, nos gustaría que nuestro código pueda dar cabida al enorme crecimiento previsto de las ventas de manzanas. Nuestro chart debería funcionar igual de bien con 5 manzanas que se venden como con 5 millones.</p>


      <p class="p" id="why_are_you_giv">Why are you giving me that look? Oh, because you want to keep your code flexible and scalable, so it will continue to work even if the data changes in the future. Very smart! Remember, if we were building a data dashboard for the roadside apple stand, we’d want our code to accommodate the enormous projected growth in apple sales. Our chart should work just as well with 5 apples sold as 5 million.</p>
      <div class="sect2" id="_d3_min_and_d3_max">

        <div class="titlepage">

          <div>

            <h3 class="title">d3.min() and d3.max()</h3>

          </div>

        </div>

        <p class="it">En lugar de especificar valores fijos para el dominio, podemos utilizar el conveniente array de las funciones <strong>d3.min()</strong> y <strong>d3.max()</strong> para analizar nuestro conjunto de datos sobre la marcha. Por ejemplo, este metodo loopea a través de cada uno de los valores de <code class="literal">x</code> en nuestras arrays y devuelve el valor mayor</p>


        <p class="p" id="instead_of_spec">Instead of specifying fixed values for the domain, we can use the convenient array functions <code class="literal">d3.min()</code> and <code class="literal">d3.max()</code> to analyze our data set on the fly. For example, this loops through each of the x values in our arrays and returns the value of the greatest one:</p>
        <pre class="programlisting" data-language="javascript" id="dmaxdataset_id1">d3.max(dataset, function(d) {
    return d[0];  //References first value in each subarray.
    Referencia el primer valor en cada subarray.
});</pre>

        <p class="it">Ese código devolverá el valor 480, porque 480 es el valor de <code class="literal">x</code> más grande de nuestro conjunto de datos. Voy a explicar cómo funciona.</p>


        <p class="p" id="that_code_will_">That code will return the value 480, because 480 is the largest x value in our dataset. Let me explain how it works.</p>
        <p class="it">Tanto los metodos <code class="literal">min()</code> y <code class="literal">max()</code> funcionan de la misma manera, y pueden tener uno o dos argumentos. El primer argumento debe ser una referencia al rango de valores que se desean evaluar, que es el conjunto de datos, en este caso. Si usted tiene un array simple, unidimensional de valores numéricos, como [7, 8, 4, 5, 2], entonces es obvio cómo comparar los valores de uno contra el otro, y no se necesita el segundo argumento. Por ejemplo:</p>


        <p class="p" id="both_min_and_">Both <code class="literal">min()</code> and <code class="literal">max()</code> work the same way, and they can take either one or two arguments. The first argument must be a reference to the array of values you want evaluated, which is <code class="literal">dataset</code>, in this case. If you have a simple, one-dimensional array of numeric values, like <code class="literal">[7, 8, 4, 5, 2]</code>, then it’s obvious how to compare the values against each other, and no second argument is needed. For example:</p>
        <pre class="programlisting" data-language="javascript" id="var_simpledatas">var simpleDataset = [7, 8, 4, 5, 2];
d3.max(simpleDataset);  // Returns 8</pre>

        <p class="it">La función <code class="literal">max()</code> simplemente recorre cada valor en el array, e identifica el más grande.</p>


        <p class="p" id="the_max_funct">The <code class="literal">max()</code> function simply loops through each value in the array, and identifies the largest one.</p>
        <p class="it">Sin embargo, nuestro conjunto de datos no es sólo un conjunto de números; es una array de arrays. Llamando a <strong>d3.max(dataset)</strong> puede producir resultados inesperados:</p>


        <p class="p" id="but_our_dataset">But our <code class="literal">dataset</code> is not just an array of numbers; it is an array of arrays. Calling <code class="literal">d3.max(dataset)</code> might produce unexpected results:</p>
        <pre class="programlisting" data-language="javascript" id="var_dataset___id16">var dataset = [
                [5, 20], [480, 90], [250, 50], [100, 33], [330, 95],
                [410, 12], [475, 44], [25, 67], [85, 21], [220, 88]
              ];
d3.max(dataset);  // Returns [85, 21].  What???</pre>

        <p class="it">Al decir a max() los valores específicos que queremos comparar, debemos incluir un segundo argumento, una <strong>función accesoria</strong>:</p>


        <p class="p" id="to_tell_max_w">To tell <code class="literal">max()</code> which <span class="emphasis"><em>specific</em></span> values we want compared, we must include a second argument, an <span class="emphasis"><em>accessor function</em></span>:</p>
        <pre class="programlisting" data-language="javascript" id="dmaxdataset_id2">d3.max(dataset, function(d) {
    return d[0];
});</pre>

        <p class="it">La <strong>función accesoria</strong> es una función anónima con la que <strong>max()</strong> maneja cada valor en la array de datos, uno a la vez, como <strong>d</strong>. La función accesoria especifica <strong>cómo acceder</strong> al valor que se utilizará para la comparación.</p>


        <p class="p" id="the_accessor_fu">The accessor function is an anonymous function to which <code class="literal">max()</code> hands<a id="id523137" class="indexterm" href=""></a><a id="id523142" class="indexterm" href=""></a> off each value in the data array, one at a time, as <code class="literal">d</code>. The accessor function specifies <span class="emphasis"><em>how to access</em></span> the value to be used for the comparison.</p>
        <p class="it"> En este caso, nuestra array de datos es el conjunto de datos, y queremos comparar solamente los valores de <strong>x</strong>, que son los primeros valores de cada subconjunto, es decir, en la posición [0]. Por lo tanto nuestra función accesoria es la siguiente:</p>


        <p class="p">In this case, our data array is <code class="literal">dataset</code>, and we want to compare only the x values, which are the first values in each subarray, meaning in position <code class="literal">[0]</code>. So our accessor function looks like this:</p>
        <pre class="programlisting" data-language="javascript" id="functiond__r_id2">function(d) {
    return d[0];  //Return the first value in each subarray. Devuelve el primer valor en cada subarray.
}</pre>

        <p class="it">Tenga en cuenta que esto es sospechosamente similar a la sintaxis que usamos cuando generamos nuestros scatterplot circles, que también utilizan funciones anónimas para recuperar y devolver valores :</p>


        <p class="p" id="note_that_this_">Note that this looks suspiciously similar to the syntax we used when generating our scatterplot circles, which also used anonymous functions to retrieve and return values:</p>
        <pre class="programlisting" data-language="javascript" id="attrcx_fun_id2">.attr("cx", function(d) {
    return d[0];
})
.attr("cy", function(d) {
    return d[1];
})</pre>

        <p class="it">Este es un patrón D3 común. Pronto va a estar muy cómodo con todo tipo de funciones anónimas merodeando por todo su código.</p>


        <p class="p" id="this_is_a_commo">This is a common D3 pattern. Soon you will be very comfortable with all manner of anonymous functions crawling all over your code.</p>
      </div>

      <div class="sect2" id="_setting_up_dynamic_scales">

        <div class="titlepage">

          <div>

            <h3 class="title">Setting Up Dynamic Scales</h3>

          </div>

        </div>

        <p class="it">Para elaborar lo que hemos cubierto, vamos a crear la función de escala para nuestro eje <strong>x</strong>:</p>


        <p class="p" id="putting_togethe">Putting together what we’ve covered, let’s create the scale function for<a id="id523424" class="indexterm" href=""></a><a id="id523432" class="indexterm" href=""></a> our x-axis:</p>
        <pre class="programlisting" data-language="javascript" id="var_xscale__d_id1">var xScale = d3.scale.linear()
                     .domain([0, d3.max(dataset, function(d) { return d[0]; })])
                     .range([0, w]);</pre>

        <p class="it">En primer lugar, note que la he denominado xScale. Por supuesto, puede asignar nombres a las escalas según su deseo, pero un nombre como xScale me ayuda a recordar lo que hace esta función.</p>


        <p class="p" id="first_notice_t">First, notice that I named it <code class="literal">xScale</code>. Of course, you can name your scales whatever you want, but a name like <code class="literal">xScale</code> helps me remember what this function does.</p>
        <p class="it">En segundo lugar, observe que tanto el dominio y el rango se especifican como arrays de dos valores entre corchetes.</p>


        <p class="p" id="second_notice_">Second, notice that both the domain and range are specified as two-value arrays in hard brackets.</p>
        <p class="it">En tercer lugar, le aviso que puse el extremo más bajo del dominio de entrada a 0. (Alternativamente, se puede usar min() para calcular un valor dinámico.) El extremo superior del dominio se establece en el valor máximo en el conjunto de datos (que se encuentra actualmente en 480, pero podría cambiar en el futuro).</p>


        <p class="p" id="third_notice_t">Third, notice that I set the low end of the input domain to 0. (Alternatively, you could use <code class="literal">min()</code> to calculate a dynamic value.) The upper end of the domain is set to the maximum value in <code class="literal">dataset</code> (which is currently 480, but could change in the future).</p>
        <p class="it">Por último, tenga en cuenta que el rango de salida se pone a <code class="literal">0</code> y <code class="literal">w</code>, y nos da el ancho del SVG.</p>


        <p class="p" id="finally_observ">Finally, observe that the output range is set to <code class="literal">0</code> and <code class="literal">w</code>, the SVG’s width.</p>
        <p class="it">Vamos a utilizar un código muy similar para crear la función de escala para el eje <strong>y</strong>:</p>


        <p class="p" id="well_use_very_">We’ll use very similar code to create the scale function for the y-axis:</p>
        <pre class="programlisting" data-language="javascript" id="var_yscale__d_id1">var yScale = d3.scale.linear()
                     .domain([0, d3.max(dataset, function(d) { return d[1]; })])
                     .range([0, h]);</pre>

        <p class="it">Tenga en cuenta que la función <code class="literal">max()</code> se referencia a <code class="literal">d[1]</code>, el valor <strong>y</strong> de cada subarray. Además, el extremo superior del <code class="literal">range()</code> se establece en <code class="literal">h</code> en lugar de <code class="literal">w</code>.</p>


        <p class="p" id="note_that_the_m">Note that the <code class="literal">max()</code> function here references <code class="literal">d[1]</code>, the y value of each subarray. Also, the upper end of <code class="literal">range()</code> is set to <code class="literal">h</code> instead of <code class="literal">w</code>.</p>
        <p class="it">Las funciones de la escala están en su lugar! Ahora todo lo que tenemos que hacer es usarlas.</p>


        <p class="p" id="the_scale_funct">The scale functions are in place! Now all we need to do is use them.</p>


          <div>

            <h3 class="title">Incorporating Scaled Values</h3>

          </div>



        <p class="it">Revisando nuestro código de dispersión, que ahora simplemente modifica la línea original donde creamos un <code class="literal">circle</code> para cada valor de datos:</p>


        <p class="p" id="revisiting_our_">Revisiting our scatterplot code, we now simply modify the original line<a id="id523930" class="indexterm" href=""></a> where we created a <code class="literal">circle</code> for each data value:</p>
        <pre class="programlisting" data-language="javascript" id="attrcx_fun_id3">.attr("cx", function(d) {
    return d[0];  //Returns original value bound from dataset. Devuelve el valor original enlazado desde el conjunto de datos
})</pre>

        <p class="it">para devolver un valor escalado (en lugar del valor original):</p>


        <p class="p" id="to_return_a_sca">to return a scaled value (instead of the original value):</p>
        <pre class="programlisting" data-language="javascript" id="attrcx_fun_id4">.attr("cx", function(d) {
    return xScale(d[0]);  //Returns scaled value
})</pre>

        <p class="it">Del mismo modo, para el siguiente eje <strong>y</strong>, :</p>


        <p class="p" id="likewise_for_t">Likewise, for the y-axis, this:</p>
        <pre class="programlisting" data-language="javascript" id="attrcy_fun_id1">.attr("cy", function(d) {
    return d[1];
})</pre>



        <p class="p" id="is_modified_as">is modified as:</p>
        <pre class="programlisting" data-language="javascript" id="attrcy_fun_id2">.attr("cy", function(d) {
    return yScale(d[1]);
})</pre>

        <p class="it">Por si fuera poco, vamos a hacer el mismo cambio en el que establecer las coordenadas para las etiquetas de texto, por lo que estas líneas:</p>


        <p class="p" id="for_good_measur">For good measure, let’s make the same change where we set the coordinates for the text labels, so these lines:</p>
        <pre class="programlisting" data-language="javascript" id="attrx_func_id7">.attr("x", function(d) {
    return d[0];
})
.attr("y", function(d) {
    return d[1];
})</pre>

        <p class="it">se convierten en estas :</p>


        <p class="p" id="become_this">become this:</p>
        <pre class="programlisting" data-language="javascript" id="attrx_func_id8">.attr("x", function(d) {
    return xScale(d[0]);
})
.attr("y", function(d) {
    return yScale(d[1]);
})</pre>

        <p class="it">Y ahí estamos!</p>


        <p class="p" id="and_there_we_ar">And there we are!</p>
        <p class="it">Chequee el código de trabajo en 02_scaled_plot.html. Visualmente, el resultado en la Figura 7-2 es decepcionantemente similar a nuestro diagrama de dispersión original! Sin embargo, estamos haciendo más progresos que podrían ser aparentes.</p>


        <p class="p" id="check_out_the_w">Check out the working code in <span class="emphasis"><em>02_scaled_plot.html</em></span>. Visually, the result in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch07.html#Scatterplot_using_x_and_y_scales" title="Figure 7-2. Scatterplot using x and y scales">Figure 7-2</a> is disappointingly similar to our original scatterplot! Yet we are making more progress than might be apparent.<a id="id524683" class="indexterm" href=""></a></p>
       

        <div>

              <img src="/static/fHijhiLmT1-img2.png" alt="Scatterplot using x and y scales"/>


          <p class="fig">Figure 7-2. Scatterplot using x and y scales</p>

    </div>




        <div>

          <h2 class="title">Refining the Plot</h2>

      </div>

      <p class="it">Usted puede haber notado que los valores de <strong>y</strong> son más pequeños en la parte superior de la trama, y los valores de <strong>y</strong> son de mayor tamaño hacia la parte inferior. Ahora que estamos utilizando escalas D3, es super fácil revertir eso, así los valores mayores van arriba, como era de esperar. Es sólo una cuestión de cambiar el rango de salida de <code class="literal">yScale</code>  de:</p>


      <p class="p" id="you_might_have__id2">You might have noticed that smaller y values are at the top of the plot, and the larger y values are toward the bottom. Now that we’re using D3 scales, it’s super easy to reverse that, so greater values are higher up, as you would expect. It’s just a matter of changing the output range of <code class="literal">yScale</code> from:</p>


      <pre class="programlisting" data-language="javascript" id="range_h">.range([0, h]);</pre>

      


      <p class="p" id="to">to:</p>



      <pre class="programlisting" data-language="javascript" id="rangeh_">.range([h, 0]);</pre>

      <p class="it">Ver 03_scaled_plot_inverted.html para el código que resulta en la Figura 7-3.</p>


      <p class="p" id="see__scaled_p">See <span class="emphasis"><em>03_scaled_plot_inverted.html</em></span> for the code that results in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch07.html#Scatterplot_with_y_scale_inverted" title="Figure 7-3. Scatterplot with y scale inverted">Figure 7-3</a>.</p>



          <div>

            <img src="/static/fHijhiLmT1-img3.png" alt="Scatterplot with y scale inverted"/>


        <p class="fig">Figure 7-3. Scatterplot with <strong>y</strong> scale inverted</p>

        <p class="fig">Diagrama de dispersión <strong>y</strong> con escala invertida</p>

      </div>

      <p class="it">Sí, una entrada más pequeña para <code class="literal">yScale</code> producirá un valor de salida más grande, lo que empuja los círculos y los elementos de texto hacia abajo, más cerca de la base de la imagen. Yo sé, es casi demasiado fácil!</p>

      <p class="p" id="yes_now_a_smal">Yes, now a <span class="emphasis"><em>smaller</em></span> input to <code class="literal">yScale</code> will produce a <span class="emphasis"><em>larger</em></span> output value, thereby pushing those <code class="literal">circle</code>s and <code class="literal">text</code> elements down, closer to the base of the image. I know, it’s almost too easy!</p>

      
      <p class="it">Sin embargo, algunos elementos están siendo cortados. Vamos a introducir una variable padding:</p>

      <p class="p" id="yet_some_elemen">Yet some elements are getting cut off. Let’s introduce a <code class="literal">padding</code> variable:</p>

      
      <pre class="programlisting" data-language="javascript" id="var_padding___id1">var padding = 20;</pre>

      <p class="it">A continuación, vamos a incorporar la cantidad de <code class="literal">padding</code> (relleno) cuando se ajusta el rango de ambas escalas. Esto ayudará a empujar nuestros elementos, lejos de los bordes de la SVG, para evitar que se recorte.</p>

      <p class="p" id="then_well_inco">Then we’ll incorporate the <code class="literal">padding</code> amount when setting the range of both scales. This will help push our elements in, away from the edges of the SVG, to prevent them from being clipped.<a id="id524978" class="indexterm" href=""></a></p>

      
      <p class="it">El rango para <code class="literal">xScale</code> fue <code class="literal">range([0, w])</code>, pero ahora es:</p>

      <p class="p" id="the_range_for_x">The range for <code class="literal">xScale</code> was <code class="literal">range([0, w])</code>, but now it’s:</p>

      
      <pre class="programlisting" data-language="javascript" id="rangepadding_id1">.range([padding, w - padding]);</pre>

      <p class="it">El rango para yScale fue el rango ([h, 0]), pero ahora es:</p>

      <p class="p" id="the_range_for_y">The range for <code class="literal">yScale</code> was <code class="literal">range([h, 0])</code>, but now it’s:</p>

      
      <pre class="programlisting" data-language="javascript" id="rangeh__pad">.range([h - padding, padding]);</pre>

      <p class="it">Esto nos debe proveer de 20 píxeles de espacio extra a la izquierda, derecha, arriba, y los bordes inferiores de la SVG. Y lo hace (ver Figura 7-4)!</p>

      <p class="p" id="this_should_pro">This should provide us with 20 pixels of extra room on the left, right, top, and bottom edges of the SVG. And it does (see <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch07.html#Scatterplot_with_padding" title="Figure 7-4. Scatterplot with padding">Figure 7-4</a>)!</p>

                <div>

            <img src="/static/fHijhiLmT1-img4.png" alt="Scatterplot with padding"/>        

            <p class="fig">Figure 7-4. Scatterplot with padding</p>


      </div>

      <p class="it">Sin embargo, las etiquetas de texto en el extremo derecho todavía están cortadas, así que el doble de la cantidad de relleno de <code class="literal">xScale</code> en el lado derecho para multiplicar por dos para conseguir el resultado que se muestra en la Figura 7-5:</p>

      <p class="p" id="but_the_text_la">But the text labels on the far right are still getting cut off, so I’ll double the amount of <code class="literal">xScale</code>’s padding on the right side by multiplying by two to achieve the result shown in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch07.html#Scatterplot_with_more_padding" title="Figure 7-5. Scatterplot with more padding">Figure 7-5</a>:</p>

      
      <pre class="programlisting" data-language="javascript" id="rangepadding_id2">.range([padding, w - padding * 2]);</pre>

      <div>


            <img src="/static/fHijhiLmT1-img5.png" alt="Scatterplot with more padding"/>


        <p class="fig">Figure 7-5. Scatterplot with more padding</p>

        <p class="fig">Figura 7-5. Diagrama de dispersión con más padding</p>

      </div>

      <p class="it">La forma en que he introducido el padding aquí es simple, pero no elegante. Eventualmente, usted podría querer más control sobre la cantidad de padding en cada lado de los gráficos (arriba, derecha, abajo, izquierda), y es útil para estandarizar la forma de especificar los valores en los proyectos. Aunque no he utilizado el margen por convención de Mike Bostock de los ejemplos de código de este libro, recomiendo echar un vistazo para ver si podría funcionar para usted.</p>

        <p class="p" id="the_way_ive_in_id2">The way I’ve introduced padding here is simple, but not elegant. Eventually, you’ll want more control over how much padding is on each side of your charts (top, right, bottom, left), and it’s useful to standardize how you specify those values across projects. Although I haven’t used <a class="ulink" href="http://bl.ocks.org/3019563" target="_top">Mike Bostock’s margin convention</a> for the code samples in this book, I recommend taking a look to see if it could work for you.</p>

              <p class="it">¡Mejor! Hacer referencia al código hasta ahora en 04_scaled_plot_padding.html. Pero hay un cambio más que me gustaría hacer. En lugar de establecer el radio de cada círculo como la raíz cuadrada de su valor (que era un poco un truco, y no visualmente útil), porqué no crear otra escala personalizada?</p>

      <p class="p" id="better_referen">Better! Reference the code so far in <span class="emphasis"><em>04_scaled_plot_padding.html</em></span>. But there’s one more change I’d like to make. Instead of setting the radius of each <code class="literal">circle</code> as the square root of its y value (which was a bit of a hack, and not visually useful), why not create another custom scale?</p>

      
      <pre class="programlisting" data-language="javascript" id="var_rscale__d">var rScale = d3.scale.linear()
                     .domain([0, d3.max(dataset, function(d) { return d[1]; })])
                     .range([2, 5]);</pre>

      <p class="it">A continuación, estableceremos el radio como el siguiente:</p>

      <p class="p" id="then_setting_t">Then, setting the radius looks like this:</p>

      
      <pre class="programlisting" data-language="javascript" id="attrr_func_id3">.attr("r", function(d) {
    return rScale(d[1]);
});</pre>

      <p class="it">Esto es emocionante porque estamos garantizando que nuestros valores de radio siempre estarán dentro del rango de 2,5. (O casi siempre, véase la referencia al metodo <code class="literal">clamp()</code> más adelante.) Por lo tanto los valores de datos de 0 (mínimo de la entrada) obtendrán círculos de radio 2 (o un diámetro de 4 píxeles). El valor de datos muy grande obtendrá un círculo de radio 5 (diámetro de 10 píxeles).</p>

      <p class="p" id="this_is_excitin_id2">This is exciting because we are guaranteeing that our radius values will <span class="emphasis"><em>always</em></span> fall within the range of <code class="literal">2,5</code>. (Or <span class="emphasis"><em>almost</em></span> always; see reference to <code class="literal">clamp()</code> later.) So data values of <code class="literal">0</code> (the minimum input) will get circles of radius <code class="literal">2</code> (or a diameter of 4 pixels). The very largest data value will get a circle of radius <code class="literal">5</code> (diameter of 10 pixels).</p>

      
      <p class="it">Voila: La figura 7-6 muestra nuestra primera escala utilizada para una propiedad visual que no sea un valor del eje. (Ver 05_scaled_plot_radii.html.)</p>

      <p class="p" id="voila_shows_ou">Voila: <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch07.html#Scatterplot_with_scaled_radii" title="Figure 7-6. Scatterplot with scaled radii">Figure 7-6</a> shows our first scale used for a visual property other than an axis value. (See <span class="emphasis"><em>05_scaled_plot_radii.html</em></span>.)</p>

      
      <div>            <img src="/static/fHijhiLmT1-img6.png" alt="Scatterplot with scaled radii"/>


        <p class="fig">Figure 7-6. Scatterplot with scaled radio</p>


      </div>

      <p class="it">Por último, en caso de que el poder de escalas aún no se ha fundido en su mente, me gustaría añadir una variedad más al conjunto de datos: [600, 150].</p>

      <p class="p" id="finally_just_i">Finally, just in case the power of scales hasn’t yet blown your mind, I’d like to add one more array to the dataset: <code class="literal">[600, 150]</code>.</p>

      
      <p class="it">¡Boom! Chequee el archivo 06_scaled_plot_big.html. Observe cómo todos los viejos puntos en la Figura 7-7 mantuvieron sus posiciones relativas, pero han migrado más juntos, hacia abajo y hacia la izquierda, para dar cabida a los recién llegados en la esquina superior derecha.</p>

      <p class="p" id="boom_check_out">Boom! Check out <span class="emphasis"><em>06_scaled_plot_big.html</em></span>. Notice how all the old points in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch07.html#Scatterplot_with_big_numbers_added" title="Figure 7-7. Scatterplot with big numbers added">Figure 7-7</a> maintained their relative positions but have migrated closer together, down and to the left, to accommodate the newcomer in the top-right corner.</p>

      
      <div>            <img src="/static/fHijhiLmT1-img7.png" alt="Scatterplot with big numbers added"/>

  

        <p class="fig">Figure 7-7. Scatterplot with big numbers added</p>

        <p class="fig">Figura 7-7. Diagrama de dispersión con grandes números añadidos</p>

      </div>

      <p class="it">Y ahora, una última revelación: ahora podemos cambiar fácilmente el tamaño de nuestra SVG, y escalarla en consecuencia. En la Figura 7-8, he aumentado el valor de <strong>h</strong> de 100 a 300 y no se hizo ningún otro cambio.</p>

      <p class="p" id="and_now_one_fi">And now, one final revelation: we can now very easily change the size of our SVG, and <span class="emphasis"><em>everything scales accordingly</em></span>. In <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch07.html#Large_scaled_scatterplot" title="Figure 7-8. Large, scaled scatterplot">Figure 7-8</a>, I’ve increased the value of <code class="literal">h</code> from <code class="literal">100</code> to <code class="literal">300</code> and made <span class="emphasis"><em>no other changes</em></span>.</p>

        
        <div>            <img src="/static/fHijhiLmT1-img8.png" alt="Large, scaled scatterplot"/>        <p class="fig">Figure 7-8. Large, scaled scatterplot</p>

        <p class="fig">Figura 7-8. Gran diagrama de dispersión reducido</p>

      </div>

      <p class="it">Boom, de nuevo! Ver 07_scaled_plot_large.html. Con suerte, usted está viendo esto para darse cuenta: no más horas nocturnas para ajustar su código porque el cliente decide que el gráfico debe ser de 800 píxeles de ancho en lugar de 600. Sí, obtendrá más horas de sueño debido a mí (y los brillantes métodos incorporados de D3). El estar bien descansado es una ventaja competitiva. Me lo puedes agradecer después.</p>

      <p class="p" id="boom_again_se">Boom, again! See <span class="emphasis"><em>07_scaled_plot_large.html</em></span>. Hopefully, you are seeing this and realizing: no more late nights tweaking your code because the client decided the graphic should be 800 pixels wide instead of 600. Yes, you will get more sleep because of me (and D3’s brilliant built-in methods). Being well-rested is a competitive advantage. You can thank me later.</p>

                <h2 class="title">Other Methods</h2>
      <p class="it"><code class="literal">d3.scale.linear()</code>tiene varios otros métodos útiles que merecen una breve mención aquí:</p>

      <p class="p" id="dscalelinear"><code class="literal">d3.scale.linear()</code> has several other handy methods that deserve a brief<a id="id525812" class="indexterm" href=""></a> mention here:</p>

            <div class="variablelist" id="nice_this_tel">

        <dl class="variablelist">

          <dt><span class="term"> <a class="ulink" href="http://bit.ly/ZR9Si0" target="_top"><code class="literal">nice()</code></a> </span></dt>

          <dd> This tells the scale to take whatever input domain that you gave to <code class="literal">range()</code> and expand both ends to the nearest round value. From the D3 wiki: “For example, <span class="keep-together">for a domain of</span> [0.20147987687960267, 0.996679553296417], the nice domain is [0.2, 1].” This is useful for normal people, who are not computers and find it hard to read numbers like 0.20147987687960267. </dd>

          <dd>Esto le dice a la escala de tomar cualquier dominio de entrada que le dio al <code class="literal">range()</code> y ampliar ambos extremos para el valor circundante más cercano. Tomado de la D3 wiki: "Por ejemplo, para un dominio de [,20147987687960267, ,996679553296417], el buen dominio es [0,2, 1]". Esto es útil para la gente normal, que no son ordenadores y les resulta difíciles de leer números como 0.20147987687960267.</dd>

          <dt><span class="term"> <a class="ulink" href="http://bit.ly/Z2ZLke" target="_top"><code class="literal">rangeRound()</code></a> </span></dt>

          <dd> Use <code class="literal">rangeRound()</code> in place of <code class="literal">range()</code>, and all values output by the scale will be rounded to the nearest whole number. This is useful if you want shapes to have exact pixel values, to avoid the fuzzy edges that could arise with antialiasing. </dd>

          <dd>Use <code class="literal">rangeRound()</code> en lugar de <code class="literal">range()</code>, y todos los valores de salida por la escala se redondearán al número entero más próximo. Esto es útil si desea que las formas tengan valores exactos de píxeles, para evitar los bordes borrosos que podrían surgir con el antialiasing.</dd>

          <dt><span class="term"> <a class="ulink" href="http://bit.ly/12h7uTf" target="_top"><code class="literal">clamp()</code></a> </span></dt>

          <dd> By default, a linear scale <span class="emphasis"><em>can</em></span> return values outside of the specified range. For example, if given a value outside of its expected input domain, a scale will return a number also outside of the output range. Calling <code class="literal">clamp(true)</code> on a scale, however, forces all output values to be within the specified range. This means excessive values will be rounded to the range’s low or high value (whichever is nearest). </dd>

          <dd>Por defecto, una escala lineal puede devolver valores fuera del rango especificado. Por ejemplo, si se le da un valor fuera de su dominio esperado de entrada, una escala devolverá un número también fuera del rango de salida. Llamando a la función <code class="literal">clamp(true)</code> en una escala, sin embargo, obliga a todos los valores de salida para estar dentro del rango especificado. Esto significa que los valores excesivos serán redondeados a bajo o alto valor del rango (el que sea más cercano).</dd>

        </dl>

      </div>

      <p class="it">  Para utilizar cualquiera de estos métodos especiales, simplemente cambiar por ellos en la cadena en la que se define la función original escala. Por ejemplo, para utilizar <code class="literal">nice()</code>:</p>

      <p class="p" id="to_use_any_of_t">To use any of these special methods, just tack them onto the chain in which you define the original scale function. For example, to use <code class="literal">nice()</code>:</p>

      
      <pre class="programlisting" data-language="javascript" id="var_scale__d_id3">var scale = d3.scale.linear()
                    .domain([0.123, 4.567])
                    .range([0, 500])
                    .nice();</pre>       



          <h2 class="title">Other Scales</h2>

      <p class="it">Además de las escalas lineales (discutidas anteriormente), D3 tiene varios otros métodos de escala incorporadas:</p>

      <p class="p" id="in_addition_to_">In addition to<a id="id526084" class="indexterm" href=""></a> <a class="ulink" href="https://github.com/mbostock/d3/wiki/Quantitative-Scales#wiki-linear" target="_top"><code class="literal">linear</code> scales</a> (discussed earlier), D3 has several other built-in scale methods:</p>

      
      <div class="variablelist" id="sqrt_a_square_r">

        <dl class="variablelist">

          <dt><span class="term"> <a class="ulink" href="http://bit.ly/15ePKWb" target="_top"><code class="literal">sqrt</code></a> </span></dt>

          <dd> A square root scale. </dd>

          <dd style="font-style: italic;"> La escala de raíz cuadrada. </dd>

          <dt><span class="term"> <a class="ulink" href="http://bit.ly/XBKvuq" target="_top"><code class="literal">pow</code></a> </span></dt>

          <dd> A power scale (good for the gym, er, I mean, useful when working with exponential series of values, as in “to the power of” some exponent). </dd>

          <dd style="font-style: italic;"> Una escala de potencia (buena para el gimnasio, quiero decir, útil cuando se trabaja con la serie exponencial de los valores, como en "el poder de" algún exponente). </dd>

          <dt><span class="term"> <a class="ulink" href="http://bit.ly/YTuRdX" target="_top"><code class="literal">log</code></a> </span></dt>

          <dd> A logarithmic scale. </dd>

          <dt><span class="term"> <a class="ulink" href="http://bit.ly/ZEJXtP" target="_top"><code class="literal">quantize</code></a> </span></dt>

          <dd> A linear scale with discrete values for its output range, for when you want to sort data into “buckets”. </dd>

          <dd style="font-style: italic;">Una escala lineal con valores discretos para su rango de salida, para cuando se desea ordenar los datos en "cubos".</dd>

          <dt><span class="term"> <a class="ulink" href="http://bit.ly/XxlWlr" target="_top"><code class="literal">quantile</code></a> </span></dt>

          <dd> Similar to <code class="literal">quantize</code>, but with discrete values for its input domain (when you already have “buckets”). </dd>

          <dd style="font-style: italic;">Similares para <code class="literal">quantize</code>, pero con valores discretos para su dominio de entrada (cuando ya se tienen "cubos"). </dd>

          <dt><span class="term"> <a class="ulink" href="http://bit.ly/XWSVvB" target="_top"><code class="literal">ordinal</code></a> </span></dt>

          <dd> Ordinal scales use nonquantitative values (like category names) for output; perfect for comparing apples and oranges. </dd>

          <dd style="font-style: italic;">Las escalas ordinales utilizan valores no cuantitativos (como nombres de las categorías) para la salida; perfecto para comparar manzanas y naranjas.</dd>

          <dt><span class="term"> <a class="ulink" href="http://bit.ly/X6O0fT" target="_top"><code class="literal">d3.scale.category10()</code></a>, <a class="ulink" href="http://bit.ly/Wn3QPH" target="_top"><code class="literal">d3.scale.category20()</code></a>, <a class="ulink" href="http://bit.ly/13bmamp" target="_top"><code class="literal">d3.scale.category20b()</code></a>, and <a class="ulink" href="http://bit.ly/Wn3Saf" target="_top"><code class="literal">d3.scale.category20c()</code></a> </span></dt>

          <dd> Handy preset ordinal scales that output either 10 or 20 categorical colors. </dd>

          <dd style="font-style: italic;">Práctico ordinal preestablecido de escalas que produce 10 ó 20 colores categóricos.</dd>

          <dt><span class="term"> <a class="ulink" href="http://bit.ly/Xxm6tc" target="_top"><code class="literal">d3.time.scale()</code></a> </span></dt>

          <dd> A scale method for date and time values, with special handling of ticks for dates. </dd>

          <dd style="font-style: italic;">Un método de escala para los valores de fecha y hora, con un manejo especial de las fechas.</dd>

        </dl>

      </div>

      <p class="it"> Ahora que ha dominado el poder de las escalas, es el momento de expresarlo visualmente, sí, con los ejes!</p>

      <p class="p" id="now_that_you_ha">Now that you have mastered the power of scales, it’s time to express them visually as, yes, <span class="emphasis"><em>axes</em></span>!</p>

            <h1 name="5ef3" id="5ef3" class="graf graf--h3 graf--leading graf--title">Introducing d3-scale by Mick Bostock</h1>

      <p class="it">Me gustaría que D3 se convirtiese en la biblioteca estándar de visualización de datos: no sólo una herramienta que se utiliza directamente para visualizar los datos de la escritura de código, sino también un conjunto de herramientas que se basa een un software más potente.</p>

      <p class="p">I’d like D3 to become the standard library of data visualization: not just a tool you use directly to visualize data by writing code, but also a suite of tools that underpin more powerful software.</p>      <p class="it">Con este fin, D3 propugna abstracciones que son útiles para cualquier aplicación de visualización y rechaza la tiranía de los gráficos.</p>

      <p class="p"><span class="markup--quote markup--p-quote is-other" name="anon_e093b1359fb0" data-creator-ids="anon">To this end, D3 espouses abstractions that are useful for any visualization application and rejects the tyranny of charts.</span></p> 



        <div>

<img alt="Imagen" src="/static/5WXgdV3lBY-img2.png"/>

</div>

      <p name="c608" id="c608" class="graf graf--p graf-after--figure">As Leland Wilkinson wrote in <a href="https://books.google.com/books?id=_kRX4LoFfGQC" data-href="https://books.google.com/books?id=_kRX4LoFfGQC" class="markup--anchor markup--p-anchor" rel="nofollow"><em class="markup--em markup--p-em">The Grammar of Graphics</em></a>,</p>
<blockquote class="it">Si nos esforzamos en desarrollar una cartografía en lugar de un programa de gráficos, vamos a lograr dos cosas. En primer lugar, inevitablemente, a ofrecer un menor número de charts que la gente quiere. En segundo lugar, el paquete no tendrá ninguna estructura profunda. Nuestro programa de ordenador será innecesariamente compleja, porque vamos a dejar de reutilizar objetos o rutinas que funcionan de manera similar en diferentes tablas. Y no tendremos manera de añadir nuevos charts a nuestro sistema sin generar código nuevo complejo. El diseño elegante nos obliga a pensar en una teoría de gráficos y no gráficos.</blockquote>
      <blockquote name="54e6" id="54e6" class="p">If we endeavor to develop a charting instead of a graphing program, we will accomplish two things. First, we inevitably will offer fewer charts than people want. Second, our package will have no deep structure. Our computer program will be unnecessarily complex, because we will fail to reuse objects or routines that function similarly in different charts. And we will have no way to add new charts to our system without generating complex new code. Elegant design requires us to think about a theory of graphics, not charts.</blockquote>

      <p class="it">Si la visualización está construyendo "representaciones visuales de datos abstractos para amplificar la cognición ", entonces tal vez el concepto más importante en D3 es la escala , que asigna una dimensión de datos abstractos para una variable visual.</p>
<p name="4f37" id="4f37" class="graf graf--p graf-after--blockquote">If visualization is constructing “visual representations of abstract data to <a href="https://books.google.com/books?id=wdh2gqWfQmgC" data-href="https://books.google.com/books?id=wdh2gqWfQmgC" class="markup--anchor markup--p-anchor" rel="nofollow">amplify cognition</a>”, then perhaps the most important concept in D3 is the <em class="markup--em markup--p-em">scale</em>, which maps a dimension of abstract data to a visual variable.</p>

      
<p class="it">Y ahora las escalas están disponibles en una biblioteca, independiente, d3-scale.</p>
<p name="544f" id="544f" class="p">And now scales are available in a standalone library, <a href="https://github.com/d3/d3-scale" data-href="https://github.com/d3/d3-scale" class="markup--anchor markup--p-anchor" rel="nofollow">d3-scale</a>.</p>

<p class="it">Pero que es una "dimensión" de los datos? O una "variable visual"? Considere una tabla de datos, como en una hoja de cálculo. Cada fila de la tabla es un vector, y cada columna es una dimensión. Una dimensión es sólo un atributo denominado cuyos valores tienen un significado particular, tal como un precio en dólares.</p>
<p name="b83f" id="b83f" class="p">But what is a “dimension” of data? Or a “visual variable”? Consider a table of data, as in a spreadsheet. Each row in the table is a vector, and each column is a dimension. A dimension is just a named attribute whose values have a particular meaning, such as a price in dollars.</p>

      <div>


<img alt="Imagen" src="/static/5WXgdV3lBY-img4.png" />


      </div>

      <p class="it">Por lo general pensamos en dimensiones como espacial y cuantitativa, tal como una posición en el espacio representado por números reales ⟨ x, y, z ⟩. Sin embargo, con los datos abstractos también existen dimensiones no cuantitativos; por ejemplo, la calidad de corte de diamante (regular, bueno, muy bueno, ideal) es ordinal, mientras que la forma del diamante de corte (la princesa, redondo, marquesa, etc. ) es categórico.</p>
<p name="c433" id="c433" class="graf graf--p graf-after--figure">We typically think of dimensions as spatial and quantitative, such as a position in space represented by real numbers ⟨<em class="markup--em markup--p-em">x, y, z</em>⟩. Yet with abstract data there are also non-quantitative dimensions; for example, diamond cut quality (fair, good, very good, ideal) is ordinal, while diamond cut shape (princess, round, marquise, <em class="markup--em markup--p-em">etc.</em>) is categorical.</p>

<p class="it">Las variables visuales son mejor explicadas por Jacques Bertin en Semiología de Gráficos . Describió la forma gráfica de marcas (digamos, puntos en un diagrama de dispersión) se pueden representar los datos utilizando la posición plana ⟨ x, y ⟩ y una dimensión luminosa z :</p>

<p name="fee3" id="fee3" class="graf graf--p graf-after--p">Visual variables are best explained by Jacques Bertin in <a href="http://esripress.esri.com/display/index.cfm?fuseaction=display&amp;websiteID=190" data-href="http://esripress.esri.com/display/index.cfm?fuseaction=display&amp;websiteID=190" class="markup--anchor markup--p-anchor" rel="nofollow"><em class="markup--em markup--p-em">Semiology of Graphics</em></a><em class="markup--em markup--p-em">.</em> He described how graphical marks (say, dots in a scatterplot) can represent data using planar position ⟨<em class="markup--em markup--p-em">x, y</em>⟩ and a luminous dimension <em class="markup--em markup--p-em">z</em>:</p>

<p class="tipit">Dentro del plano de una marca puede ser en la parte superior o la parte inferior, a la derecha oa la izquierda. El ojo percibe dos dimensiones independientes a lo largo de X e Y, que se distinguen de forma ortogonal. Una variación en la energía luminosa produce tercera dimensión en Z, que es independiente de X e Y ...</p>


<p class="tip">Within the plane a mark can be at the top or the bottom, to the right or the left. The eye perceives two independent dimensions along X and Y, which are distinguished orthogonally. A variation in light energy produces a third dimension in Z, which is independent of X and Y…</p>

<p class="tipit">El ojo es sensible, a lo largo de la dimensión Z, a 6 variables independientes visuales, que pueden ser superpuestas sobre las figuras planas: el tamaño de las marcas, su valor, textura, color, orientación y forma. Pueden representar diferencias (≠), similitudes (≡), una orden cuantificada (Q), o una orden de no cuantificados (O), y pueden expresar los grupos, las jerarquías, o movimientos verticales.</p>

<p class="tip">The eye is sensitive, along the Z dimension, to 6 independent visual variables, which can be superimposed on the planar figures: the size of the marks, their value, texture, color, orientation, and shape. They can represent differences (≠), similarities (≡), a quantified order (Q), or a nonquantified order (O), and can express groups, hierarchies, or vertical movements.</p>


      <div>


<img alt="Imagen" src="/static/5WXgdV3lBY-img6.png" />



        <p class="fig">From <a href="http://esripress.esri.com/display/index.cfm?fuseaction=display&amp;websiteID=190" data-href="http://esripress.esri.com/display/index.cfm?fuseaction=display&amp;websiteID=190" class="markup--anchor markup--figure-anchor" rel="nofollow"><em class="markup--em markup--figure-em">Semiology of Graphics</em></a>, colorized by the author.</p>

      </div>
<p class="it">Por lo tanto, una escala es una función que toma un valor abstracto de datos, tales como la masa de un diamante en quilates, y devuelve un valor visual tal como la posición horizontal de un punto en píxeles. Con dos escalas (uno para cada x y y ), tenemos la base para un diagrama de dispersión.</p>
      <p name="0ce2" id="0ce2" class="graf graf--p graf-after--figure">Thus, a scale is a function that takes an <em class="markup--em markup--p-em">abstract value</em> of data, such as the mass of a diamond in carats, and returns a <em class="markup--em markup--p-em">visual value</em> such as the horizontal position of a dot in pixels. With two scales (one each for <em class="markup--em markup--p-em">x</em> and <em class="markup--em markup--p-em">y</em>), we have the basis for a scatterplot.</p>



      <div>



  <img alt="Imagen" src="/static/5WXgdV3lBY-img8.png" />



        <p class="fig">The relationship between diamond mass <em class="markup--em markup--figure-em">and</em> price. <a href="http://bl.ocks.org/mbostock/ebb45892cc6ec5e6c902" data-href="http://bl.ocks.org/mbostock/ebb45892cc6ec5e6c902" class="markup--anchor markup--figure-anchor" rel="nofollow">View source.</a></p>

      </div>


    <pre name="0405556" id="040rt2" class="graf tgraf--pre graf-after--p">&lt;!DOCTYPE html&gt;
&lt;meta charset="utf-8"&gt;
&lt;style&gt;

canvas,
svg {
  position: absolute;
}

.grid .tick line {
  stroke: #fff;
}

.grid--x .domain {
  fill: #e7e7e7;
  stroke: none;
}

.grid--y .domain,
.axis .domain {
  display: none;
}

&lt;/style&gt;
&lt;svg width="960" height="960"&gt;&lt;/svg&gt;
&lt;canvas width="960" height="960"&gt;&lt;/canvas&gt;
&lt;script src="//d3js.org/d3.v4.0.0-alpha.49.min.js"&gt;&lt;/script&gt;
&lt;script&gt;

var canvas = d3.select("canvas").node(),
    context = canvas.getContext("2d");

var margin = {top: 20, right: 20, bottom: 30, left: 40},
    width = canvas.width - margin.left - margin.right,
    height = canvas.height - margin.top - margin.bottom;

var svg = d3.select("svg").append("g")
    .attr("transform", "translate(" + margin.left + "," + margin.top + ")");

var x = d3.scaleLinear()
    .rangeRound([0, width - 2]);

var y = d3.scaleLinear()
    .rangeRound([height - 2, 0]);

context.translate(margin.left, margin.top);
context.globalCompositeOperation = "multiply";
context.fillStyle = "rgba(60,180,240,0.6)";

d3.tsv("diamonds.tsv", type, function(error, diamonds) {
  if (error) throw error;

  x.domain(d3.extent(diamonds, function(d) { return d.carat; }));
  y.domain(d3.extent(diamonds, function(d) { return d.price; }));

  svg.append("g")
      .attr("class", "grid grid--x")
      .call(d3.axisLeft(y)
          .tickSize(-width)
          .tickFormat(""));

  svg.append("g")
      .attr("class", "grid grid--y")
      .attr("transform", "translate(0," + height + ")")
      .call(d3.axisBottom(x)
          .tickSize(-height)
          .tickFormat(""));

  svg.append("g")
      .attr("class", "axis axis--y")
      .call(d3.axisLeft(y)
          .ticks(10, "s"))
    .append("text")
      .attr("x", 10)
      .attr("y", 10)
      .attr("dy", ".71em")
      .attr("fill", "#000")
      .attr("font-weight", "bold")
      .attr("text-anchor", "start")
      .text("Price (US$)");

  svg.append("g")
      .attr("class", "axis axis--x")
      .attr("transform", "translate(0," + height + ")")
      .call(d3.axisBottom(x))
    .append("text")
      .attr("x", width - 10)
      .attr("y", -10)
      .attr("dy", "-.35em")
      .attr("fill", "#000")
      .attr("font-weight", "bold")
      .attr("text-anchor", "end")
      .text("Mass (carats)");

  d3.shuffle(diamonds);
  var t = d3.timer(function() {
    for (var i = 0, n = 500, d; i &lt; n; ++i) {
      if (!(d = diamonds.pop())) return t.stop();
      context.fillRect(x(d.carat), y(d.price), Math.max(2, x(d.carat + 0.01) - x(d.carat)), 2);
    }
  });
});

function type(d) {
  d.carat = +d.carat;
  d.price = +d.price;
  return d;
}

&lt;/script&gt;</pre>

<p class="it">Para ilustrar cómo funcionan las escalas, imaginar cómo se puede calcular x e y para cada punto por encima. Teniendo en cuenta algunos valores derivados de los datos (minCarat, maxCarat, minprice, maxprice) y algunas del tamaño del gráfico (anchura, altura), que podría hacer algo como esto:</p>

      <p class="p">To illustrate how scales work, imagine how you might compute <em class="markup--em markup--p-em">x</em> and <em class="markup--em markup--p-em">y</em> for each dot above. Given some values derived from data (minCarat, maxCarat, minPrice, maxPrice) and some from the chart size (width, height), you might do something like this:</p>

      <pre name="0402" id="0402" class="graf graf--pre graf-after--p">function x(carat) {  return (carat - minCarat)      / (maxCarat - minCarat)      * width;}</pre>

      <pre name="a3d9" id="a3d9" class="graf graf--pre graf-after--pre">function y(price) {  return height      - (price - minPrice)      / (maxPrice - minPrice)      * height;}</pre>
<p class="it">El diamante más ligero se coloca en el borde izquierdo de la tabla, el diamante más pesado se coloca en el borde derecho de la tabla, y así sucesivamente. Tenga en cuenta que el rango de la Y -scale se invierte ya que los sistemas gráficos ponen el origen en la esquina superior izquierda, mientras que los diagramas de dispersión pusieron en la parte inferior izquierda.
</p>
      <p class="p">The lightest diamond is placed at the chart’s left edge, the heaviest diamond is placed at the chart’s right edge, and so on. Note that the range of the <em class="markup--em markup--p-em">y</em>-scale is inverted because graphics systems put the origin in the top-left corner whereas scatterplots put it in the bottom-left.</p>
<p class="it">Al igual que el anterior, escalas cuantitativas de D3 son funciones configuradas por dos intervalos. La entrada de dominio es un intervalo en la dimensión resumen de los datos, a menudo el grado de los valores observados. La salida de gama es un intervalo en la variable visual, tales como el área visible definido por el tamaño del gráfico.</p>
      <p class="p">Like the above, D3’s quantitative scales are functions configured by two intervals. The input <em class="markup--em markup--p-em">domain</em> is an interval in the abstract dimension of data, often the <a href="https://github.com/d3/d3-array#extent" data-href="https://github.com/d3/d3-array#extent" class="markup--anchor markup--p-anchor" rel="nofollow">extent</a> of the observed values. The output <em class="markup--em markup--p-em">range</em> is an interval in the visual variable, such as the visible area defined by the chart size.</p>

      <pre name="492b" id="492b" class="graf graf--pre graf-after--p">var x = d3_scale.linear()    .domain(d3_array.extent(data, function(d) { return d.carat; }))    .range([0, width]);</pre>

      <pre name="a16c" id="a16c" class="graf graf--pre graf-after--pre">var y = d3_scale.linear()    .domain(d3_array.extent(data, function(d) { return d.price; }))    .range([height, 0]);</pre>
<p class="it">Pero las escalas hacen mucho más que aritmética básica!
</p>
      <p class="p">But scales do much more than basic arithmetic!</p>
<p class="it">Por un lado, ahora es trivial para aplicar transformaciones cuantitativas: reemplazar un lineal de escala con una logarítmica o poder escala. Una escala lineal es una buena opción por defecto, ya que preserva la proporcionalidad, pero un registro o la escala prisionero de guerra puede ayudar a la diferenciación de los datos que no se distribuye de manera uniforme. (Entre las escalas también son buenos para mostrar el cambio .)</p>
      <p class="p">For one, it is now trivial to apply quantitative transformations: replace a <a href="https://github.com/d3/d3-scale#linear" data-href="https://github.com/d3/d3-scale#linear" class="markup--anchor markup--p-anchor" rel="nofollow">linear</a> scale with a <a href="https://github.com/d3/d3-scale#log-scales" data-href="https://github.com/d3/d3-scale#log-scales" class="markup--anchor markup--p-anchor" rel="nofollow">logarithmic</a> or <a href="https://github.com/d3/d3-scale#power-scales" data-href="https://github.com/d3/d3-scale#power-scales" class="markup--anchor markup--p-anchor" rel="nofollow">power</a> scale. A linear scale is a good default choice because it preserves proportionality, but a log or pow scale may aid the differentiation of data that is not uniformly distributed. (Log scales are also good for <a href="http://bl.ocks.org/mbostock/c69f5960c6b1a95b6f78" data-href="http://bl.ocks.org/mbostock/c69f5960c6b1a95b6f78" class="markup--anchor markup--p-anchor" rel="nofollow">showing change</a>.)</p>



      <div>


<img alt="Imagen" src="/static/5WXgdV3lBY-img10.png" />



        <p class="fig">The previous scatterplot modified to use log scales. <a href="http://bl.ocks.org/mbostock/c3034eef9d73b5fdf274" data-href="http://bl.ocks.org/mbostock/c3034eef9d73b5fdf274" class="markup--anchor markup--figure-anchor" rel="nofollow">View source.</a></p>


    </div>

        <pre>&lt;!DOCTYPE html&gt;
&lt;meta charset="utf-8"&gt;
&lt;style&gt;

canvas,
svg {
  position: absolute;
}

.grid .tick line {
  stroke: #fff;
}

.grid--x .domain {
  fill: #e7e7e7;
  stroke: none;
}

.grid--y .domain,
.axis .domain {
  display: none;
}

&lt;/style&gt;
&lt;svg width="960" height="960"&gt;&lt;/svg&gt;
&lt;canvas width="960" height="960"&gt;&lt;/canvas&gt;
&lt;script src="//d3js.org/d3.v4.0.0-alpha.49.min.js"&gt;&lt;/script&gt;
&lt;script&gt;

var canvas = d3.select("canvas").node(),
    context = canvas.getContext("2d");

var margin = {top: 20, right: 20, bottom: 30, left: 40},
    width = canvas.width - margin.left - margin.right,
    height = canvas.height - margin.top - margin.bottom;

var svg = d3.select("svg").append("g")
    .attr("transform", "translate(" + margin.left + "," + margin.top + ")");

var x = d3.scaleLog()
    .rangeRound([0, width - 2]);

var y = d3.scaleLog()
    .rangeRound([height - 2, 0]);

context.translate(margin.left, margin.top);
context.globalCompositeOperation = "multiply";
context.fillStyle = "rgba(60,180,240,0.6)";

d3.tsv("diamonds.tsv", type, function(error, diamonds) {
  if (error) throw error;

  x.domain(d3.extent(diamonds, function(d) { return d.carat; }));
  y.domain(d3.extent(diamonds, function(d) { return d.price; }));

  svg.append("g")
      .attr("class", "grid grid--x")
      .call(d3.axisLeft(y)
          .tickSize(-width)
          .tickFormat(""));

  svg.append("g")
      .attr("class", "grid grid--y")
      .attr("transform", "translate(0," + height + ")")
      .call(d3.axisBottom(x)
          .tickSize(-height)
          .tickFormat(""));

  svg.append("g")
      .attr("class", "axis axis--y")
      .call(d3.axisLeft(y)
          .ticks(20, ".1s"))
    .append("text")
      .attr("x", 10)
      .attr("y", 10)
      .attr("dy", ".71em")
      .attr("fill", "#000")
      .attr("font-weight", "bold")
      .attr("text-anchor", "start")
      .text("Price (US$)");

  svg.append("g")
      .attr("class", "axis axis--x")
      .attr("transform", "translate(0," + height + ")")
      .call(d3.axisBottom(x)
          .ticks(20, ".1f"))
    .append("text")
      .attr("x", width - 10)
      .attr("y", -10)
      .attr("dy", "-.35em")
      .attr("fill", "#000")
      .attr("font-weight", "bold")
      .attr("text-anchor", "end")
      .text("Mass (carats)");

  d3.shuffle(diamonds);
  var t = d3.timer(function() {
    for (var i = 0, n = 500, d; i &lt; n; ++i) {
      if (!(d = diamonds.pop())) return t.stop();
      context.fillRect(x(d.carat), y(d.price), Math.max(2, x(d.carat + 0.01) - x(d.carat)), 2);
    }
  });
});

function type(d) {
  d.carat = +d.carat;
  d.price = +d.price;
  return d;
}

&lt;/script&gt;</pre>

<p class="it">Para dos, escalas aliviar el tedio de dibujo ejes legibles por generar y dar formato agradable, valores redondos ( garrapatas ) del dominio. Garrapatas de una escala son de tipo adecuado: por ejemplo, el registro de las garrapatas por encima están espaciados uniformemente dentro de cada potencia de diez, mientras que una escala de tiempo utiliza intervalos de calendario.
</p>
      <p class="p">For two, scales alleviate the tedium of drawing legible axes by <a href="https://github.com/d3/d3-scale#continuous_ticks" data-href="https://github.com/d3/d3-scale#continuous_ticks" class="markup--anchor markup--p-anchor" rel="nofollow">generating</a> and <a href="https://github.com/d3/d3-scale#continuous_tickFormat" data-href="https://github.com/d3/d3-scale#continuous_tickFormat" class="markup--anchor markup--p-anchor" rel="nofollow">formatting</a> nice, round values (<em class="markup--em markup--p-em">ticks</em>) from the domain. A scale’s ticks are type-appropriate: for example, the log ticks above are uniformly-spaced within each power of ten, while a time scale uses calendar intervals.</p>
<p class="it">La mayoría de las escalas son bidireccionales : se puede invertir el mapeo de representación visual de nuevo a los datos abstractos, facilitando la interacción. Por ejemplo, un intervalo de cepillado en píxeles se puede invertir para extraer datos para la consulta.</p>
      <p class="p">Most scales are bidirectional<em class="markup--em markup--p-em">: </em>you can <a href="https://github.com/d3/d3-scale#continuous_invert" data-href="https://github.com/d3/d3-scale#continuous_invert" class="markup--anchor markup--p-anchor" rel="nofollow">invert</a> the mapping from visual representation back to abstract data, facilitating interaction. For example, a brushed interval in pixels can be inverted to abstract data for querying.</p>

      <div>

<img alt="Imagen" src="/static/241_1.png" /></div>



        <p class="fig">Brushing a scatterplot matrix. <a href="http://bl.ocks.org/mbostock/4063663" data-href="http://bl.ocks.org/mbostock/4063663" class="markup--anchor markup--figure-anchor" rel="nofollow">View source.</a></p>

      </div>
      <pre>&lt;!DOCTYPE html&gt;
&lt;meta charset="utf-8"&gt;
&lt;style&gt;

svg {
  font: 10px sans-serif;
  padding: 10px;
}

.axis,
.frame {
  shape-rendering: crispEdges;
}

.axis line {
  stroke: #ddd;
}

.axis path {
  display: none;
}

.cell text {
  font-weight: bold;
  text-transform: capitalize;
}

.frame {
  fill: none;
  stroke: #aaa;
}

circle {
  fill-opacity: .7;
}

circle.hidden {
  fill: #ccc !important;
}

.extent {
  fill: #000;
  fill-opacity: .125;
  stroke: #fff;
}

&lt;/style&gt;
&lt;body&gt;
&lt;script src="//d3js.org/d3.v3.min.js"&gt;&lt;/script&gt;
&lt;script&gt;

var width = 960,
    size = 230,
    padding = 20;

var x = d3.scale.linear()
    .range([padding / 2, size - padding / 2]);

var y = d3.scale.linear()
    .range([size - padding / 2, padding / 2]);

var xAxis = d3.svg.axis()
    .scale(x)
    .orient("bottom")
    .ticks(6);

var yAxis = d3.svg.axis()
    .scale(y)
    .orient("left")
    .ticks(6);

var color = d3.scale.category10();

d3.csv("flowers.csv", function(error, data) {
  if (error) throw error;

  var domainByTrait = {},
      traits = d3.keys(data[0]).filter(function(d) { return d !== "species"; }),
      n = traits.length;

  traits.forEach(function(trait) {
    domainByTrait[trait] = d3.extent(data, function(d) { return d[trait]; });
  });

  xAxis.tickSize(size * n);
  yAxis.tickSize(-size * n);

  var brush = d3.svg.brush()
      .x(x)
      .y(y)
      .on("brushstart", brushstart)
      .on("brush", brushmove)
      .on("brushend", brushend);

  var svg = d3.select("body").append("svg")
      .attr("width", size * n + padding)
      .attr("height", size * n + padding)
    .append("g")
      .attr("transform", "translate(" + padding + "," + padding / 2 + ")");

  svg.selectAll(".x.axis")
      .data(traits)
    .enter().append("g")
      .attr("class", "x axis")
      .attr("transform", function(d, i) { return "translate(" + (n - i - 1) * size + ",0)"; })
      .each(function(d) { x.domain(domainByTrait[d]); d3.select(this).call(xAxis); });

  svg.selectAll(".y.axis")
      .data(traits)
    .enter().append("g")
      .attr("class", "y axis")
      .attr("transform", function(d, i) { return "translate(0," + i * size + ")"; })
      .each(function(d) { y.domain(domainByTrait[d]); d3.select(this).call(yAxis); });

  var cell = svg.selectAll(".cell")
      .data(cross(traits, traits))
    .enter().append("g")
      .attr("class", "cell")
      .attr("transform", function(d) { return "translate(" + (n - d.i - 1) * size + "," + d.j * size + ")"; })
      .each(plot);

  // Titles for the diagonal.
  cell.filter(function(d) { return d.i === d.j; }).append("text")
      .attr("x", padding)
      .attr("y", padding)
      .attr("dy", ".71em")
      .text(function(d) { return d.x; });

  cell.call(brush);

  function plot(p) {
    var cell = d3.select(this);

    x.domain(domainByTrait[p.x]);
    y.domain(domainByTrait[p.y]);

    cell.append("rect")
        .attr("class", "frame")
        .attr("x", padding / 2)
        .attr("y", padding / 2)
        .attr("width", size - padding)
        .attr("height", size - padding);

    cell.selectAll("circle")
        .data(data)
      .enter().append("circle")
        .attr("cx", function(d) { return x(d[p.x]); })
        .attr("cy", function(d) { return y(d[p.y]); })
        .attr("r", 4)
        .style("fill", function(d) { return color(d.species); });
  }

  var brushCell;

  // Clear the previously-active brush, if any.
  function brushstart(p) {
    if (brushCell !== this) {
      d3.select(brushCell).call(brush.clear());
      x.domain(domainByTrait[p.x]);
      y.domain(domainByTrait[p.y]);
      brushCell = this;
    }
  }

  // Highlight the selected circles.
  function brushmove(p) {
    var e = brush.extent();
    svg.selectAll("circle").classed("hidden", function(d) {
      return e[0][0] &gt; d[p.x] || d[p.x] &gt; e[1][0]
          || e[0][1] &gt; d[p.y] || d[p.y] &gt; e[1][1];
    });
  }

  // If the brush is empty, select all circles.
  function brushend() {
    if (brush.empty()) svg.selectAll(".hidden").classed("hidden", false);
  }
});

function cross(a, b) {
  var c = [], n = a.length, m = b.length, i, j;
  for (i = -1; ++i &lt; n;) for (j = -1; ++j &lt; m;) c.push({x: a[i], i: i, y: b[j], j: j});
  return c;
}

&lt;/script&gt;</pre>
<p class="it">Y hay escalas para datos ordinales y categóricas. La banda de escala, por ejemplo, simplifica el cálculo de anchos de las barras y posiciones, lo que permite el relleno configurable, la alineación y redondeo.</p>
      <p class="p">And there are scales for ordinal and categorical data. The <a href="https://github.com/d3/d3-scale#band-scales" data-href="https://github.com/d3/d3-scale#band-scales" class="markup--anchor markup--p-anchor" rel="nofollow">band</a> scale, for instance, simplifies the calculation of bar widths and positions, allowing configurable padding, alignment and rounding.</p>

      <div>

<img alt="Imagen" src="/static/1-cIYJvJvpPlsC0i1eD69nqw.png" />

       

        <p class="p">The frequency of English letters. <a href="http://bl.ocks.org/mbostock/946ddf8a32b3b660ffd8" data-href="http://bl.ocks.org/mbostock/946ddf8a32b3b660ffd8" class="markup--anchor markup--figure-anchor" rel="nofollow">View source.</a></p>

      </div>
      <pre>&lt;!DOCTYPE html&gt;
&lt;meta charset="utf-8"&gt;
&lt;canvas width="960" height="500"&gt;&lt;/canvas&gt;
&lt;script src="//d3js.org/d3.v4.0.0-alpha.4.min.js"&gt;&lt;/script&gt;
&lt;script&gt;

var canvas = document.querySelector("canvas"),
    context = canvas.getContext("2d");

var margin = {top: 20, right: 20, bottom: 30, left: 40},
    width = canvas.width - margin.left - margin.right,
    height = canvas.height - margin.top - margin.bottom;

var x = d3.scaleBand()
    .rangeRound([0, width])
    .padding(0.1);

var y = d3.scaleLinear()
    .rangeRound([height, 0]);

context.translate(margin.left, margin.top);

d3.requestTsv("data.tsv", function(d) {
  d.frequency = +d.frequency;
  return d;
}, function(error, data) {
  if (error) throw error;

  x.domain(data.map(function(d) { return d.letter; }));
  y.domain([0, d3.max(data, function(d) { return d.frequency; })]);

  var yTickCount = 10,
      yTicks = y.ticks(yTickCount),
      yTickFormat = y.tickFormat(yTickCount, "%");

  context.beginPath();
  x.domain().forEach(function(d) {
    context.moveTo(x(d) + x.bandwidth() / 2, height);
    context.lineTo(x(d) + x.bandwidth() / 2, height + 6);
  });
  context.strokeStyle = "black";
  context.stroke();

  context.textAlign = "center";
  context.textBaseline = "top";
  x.domain().forEach(function(d) {
    context.fillText(d, x(d) + x.bandwidth() / 2, height + 6);
  });

  context.beginPath();
  yTicks.forEach(function(d) {
    context.moveTo(0, y(d) + 0.5);
    context.lineTo(-6, y(d) + 0.5);
  });
  context.strokeStyle = "black";
  context.stroke();

  context.textAlign = "right";
  context.textBaseline = "middle";
  yTicks.forEach(function(d) {
    context.fillText(yTickFormat(d), -9, y(d));
  });

  context.beginPath();
  context.moveTo(-6.5, 0 + 0.5);
  context.lineTo(0.5, 0 + 0.5);
  context.lineTo(0.5, height + 0.5);
  context.lineTo(-6.5, height + 0.5);
  context.strokeStyle = "black";
  context.stroke();

  context.save();
  context.rotate(-Math.PI / 2);
  context.textAlign = "right";
  context.textBaseline = "top";
  context.font = "bold 10px sans-serif";
  context.fillText("Frequency", -10, 10);
  context.restore();

  context.fillStyle = "steelblue";
  data.forEach(function(d) {
    context.fillRect(x(d.letter), y(d.frequency), x.bandwidth(), height - y(d.frequency));
  });
});

&lt;/script&gt;</pre>



<p class="it">Sin embargo, las escalas no son sólo para posicionamiento; son para el cálculo de cualquier variable de visual. Las escalas se pueden interpolar tamaños símbolo, tamaños de fuente, colores, grosores de trazo en varios espacios de color, transformaciones geométricas, formas e incluso objetos están anidadas. A continuación, una escala representa cantidad por medio de la orientación angular, con los números pequeños reclinado a la izquierda (\) y un gran número inclina a la derecha (/). Esto revela el comportamiento de un algoritmo de clasificación en una serie de números:</p>

      <p name="431f" id="431f" class="graf graf--p graf-after--figure">Yet scales are not just for positioning; they are for computing <em class="markup--em markup--p-em">any</em> visual variable. Scales can <a href="https://github.com/d3/d3-scale#continuous_interpolate" data-href="https://github.com/d3/d3-scale#continuous_interpolate" class="markup--anchor markup--p-anchor" rel="nofollow">interpolate</a> symbol sizes, font sizes, stroke widths, colors in various color spaces, geometric transforms, shapes and even deeply-nested objects. Below, a scale represents quantity using angular orientation, with small numbers leaning left (\) and large numbers leaning right (/). This reveals the behavior of a sorting algorithm on an array of numbers:</p>



      <div>
<img alt="Imagen" src="/static/1-IUn5Qb-VneCovMfH8PqAsA.png" />



        <p class="fig">Visualizing quicksort. From <a href="http://bost.ocks.org/mike/algorithms/" data-href="http://bost.ocks.org/mike/algorithms/" class="markup--anchor markup--figure-anchor" rel="nofollow">Visualizing Algorithms.</a></p>

      </div>

<p class="it">A continuación, una escala de raíz cuadrada calcula el radio apropiado para que el área de la burbuja de cada condado es proporcional al número de personas que viven allí:</p>
      <p name="8fa8" id="8fa8" class="graf graf--p graf-after--figure">Below, a square-root scale computes the appropriate radius so that the area of each county’s bubble is proportional to the number of people living there:</p>

  



      <div>

<img alt="Imagen" src="/static/1-K1xOjX_qc_6TtP7hU_o5hA.png" />

      
<p class="fig">Población en 2008. Desde vamos a hacer un mapa de la burbuja.</p>
        <p class="fig">Population in 2008. From <a href="http://bost.ocks.org/mike/bubble-map/" data-href="http://bost.ocks.org/mike/bubble-map/" class="markup--anchor markup--figure-anchor" rel="nofollow">Let’s Make a Bubble Map</a>.</p>

      </div>





      <p name="8c61" id="8c61" class="p">Below, a comparison of perceptually-uniform sequential color scales used for a choropleth of unemployment rate:</p>
<p class="it">A continuación, una comparación de escalas de color secuenciales perceptualmente uniformes utilizados para una coropletas de tasa de desempleo:</p>
 

      <div>

<img alt="Imagen" src="/static/1-0ptljP-upBOkJG0_8o05zg.png" />
 </div>

      <div>


<img alt="Imagen" src="/static/1-bG7dyONArCRSUSJFgFFehA.png" /></div>

        </div>
 <div>
      

          <img alt="Imagen" src="/static/1-MAOWJ7_NI5yVrYDUzcRJug.png" /></div>

        
<p class="fig">El desempleo en 2008, utilizando el magma, viridis y cubehelix. Los colores más oscuros indican una tasa de desempleo. </p>
        <p class="fig">Unemployment in 2008, using magma, viridis and cubehelix. Darker colors indicate a higher unemployment rate. <a href="http://bl.ocks.org/mbostock/4060606" data-href="http://bl.ocks.org/mbostock/4060606" class="markup--anchor markup--figure-anchor" rel="nofollow">View source.</a></p>

      


<p class="it">Incluso puede crear escalas trozos de colores divergentes, o cuantificar las escalas para la aplicación de las pausas discretos para los datos continuos.</p>
      <p name="b841" id="b841" class="p">You can even create piecewise scales for diverging colors, or quantize scales for applying discrete breaks to continuous data.</p>

      
<p class="it">Por lo tanto, probarlo ! Y echa un vistazo a los otros nuevos módulos D3 , también, por ejemplo d3-tiempo , d3-formato , y d3-forma.</p>
      <p name="1580" id="1580" class="p">So, <a href="https://github.com/d3/d3-scale" data-href="https://github.com/d3/d3-scale" class="markup--anchor markup--p-anchor" rel="nofollow">try it out</a>! And check out the other <a href="https://github.com/d3" data-href="https://github.com/d3" class="markup--anchor markup--p-anchor" rel="nofollow">new D3 modules</a>, too, such as <a href="https://github.com/d3/d3-time" data-href="https://github.com/d3/d3-time" class="markup--anchor markup--p-anchor" rel="nofollow">d3-time</a>, <a href="https://github.com/d3/d3-format" data-href="https://github.com/d3/d3-format" class="markup--anchor markup--p-anchor" rel="nofollow">d3-format</a>, and <a href="https://medium.com/@mbostock/introducing-d3-shape-73f8367e6d12" data-href="https://medium.com/@mbostock/introducing-d3-shape-73f8367e6d12" class="markup--anchor markup--p-anchor">d3-shape</a>.</p>



      
<p class="it">Feliz Escalamiento!</p>
      <p name="e0d7" id="e0d7" class="graf graf--p graf-after--p">Happy scaling!</p>



      <h3 name="95f3" id="95f3" class="graf graf--h3 graf-after--p graf--last"><a href="https://github.com/d3/d3-scale" data-href="https://github.com/d3/d3-scale" class="markup--anchor markup--h3-anchor" rel="nofollow">https://github.com/d3/d3-scale</a></h3>




    <h1>d3-scale by Mick Bostock</h1>
 <p class="it">Las escalas son una abstracción conveniente para una tarea fundamental en la visualización: asignar una dimensión de los datos abstractos a una representación visual. Aunque la mayoría de las veces se utiliza para codificar datos cuantitativos, como asignar una medición en metros a una posición en píxeles para puntos en un diagrama de dispersión, las escalas pueden representar virtualmente cualquier codificación visual, como colores divergentes, anchos de trazo o tamaño de símbolo. Las escalas también se pueden utilizar con virtualmente cualquier tipo de datos, tales como datos categóricos nombrados o datos discretos que requieran pausas razonables.</p>
    <p class="p">Scales are a convenient abstraction for a fundamental task in visualization: mapping a dimension of abstract data to a visual representation. Although most often used for position-encoding quantitative data, such as mapping a measurement in meters to a position in pixels for dots in a scatterplot, scales can represent virtually any visual encoding, such as diverging colors, stroke widths, or symbol size. Scales can also be used with virtually any type of data, such as named categorical data or discrete data that requires sensible breaks.</p>

   
  <p class="it">Para datos cuantitativos continuos, normalmente se desea una escala lineal. (Para datos de series de tiempo, una escala de tiempo.) Si la distribución lo solicita, considere la posibilidad de transformar datos usando una escala de potencia o escala de log. Una escala de cuantización puede ayudar a la diferenciación redondeando datos continuos a un conjunto fijo de valores discretos; De manera similar, una escala de cuantía calcula cuantiles de una población de muestra, y una escala de umbral le permite especificar interrupciones arbitrarias en datos continuos. También se proporcionan varios esquemas de colores secuenciales incorporados; Para más información ver d3-scale-chromatic.</p>
    <p class="p">For continuous quantitative data, you typically want a linear scale. (For time series data, a time scale.) If the distribution calls for it, consider transforming data using a power or log scale. A quantize scale may aid differentiation by rounding continuous data to a fixed set of discrete values; similarly, a quantile scale computes quantiles from a sample population, and a threshold scale allows you to specify arbitrary breaks in continuous data. Several built-in sequential color schemes are also provided; see d3-scale-chromatic for more.</p>

  

    <p class="it">Para datos ordenados discretos (ordenados) o categóricos (no ordenados), una escala ordinal especifica una asignación explícita de un conjunto de valores de datos a un conjunto correspondiente de atributos visuales (como colores). Las escalas de banda y punto relacionadas son útiles para codificar posiciones de datos ordinales, como barras en un gráfico de barras o puntos en un diagrama de dispersión categórico. También se proporcionan varias escalas de color categóricas incorporadas.</p>
    <p class="p">For discrete ordinal (ordered) or categorical (unordered) data, an ordinal scale specifies an explicit mapping from a set of data values to a corresponding set of visual attributes (such as colors). The related band and point scales are useful for position-encoding ordinal data, such as bars in a bar chart or dots in an categorical scatterplot. Several built-in categorical color scales are also provided.</p>


 <p class="it">Las escalas no tienen representación visual intrínseca. Sin embargo, la mayoría de las escalas pueden generar y dar formato a las señales de las marcas de referencia para ayudar en la construcción de ejes.</p>
    <p class="p">Scales have no intrinsic visual representation. However, most scales can generate and format ticks for reference marks to aid in the construction of axes.</p>

   

    <h2>Installing</h2>
<p class="it">Si usa NPM, npm instala la escala d3. De lo contrario, descargue la última versión. También puede cargar directamente desde d3js.org, ya sea como una biblioteca independiente o como parte de D3 4.0. Los entornos AMD, CommonJS y vainilla son compatibles. En vainilla, se exporta un d3 global:</p>
    <p class="p">If you use NPM, npm install d3-scale. Otherwise, download the latest release. You can also load directly from d3js.org, either as a standalone library or as part of D3 4.0. AMD, CommonJS, and vanilla environments are supported. In vanilla, a d3 global is exported:</p>

     <pre class="programlisting" data-language="javascript" id="113"> 
&lt;script src="https://d3js.org/d3-array.v1.min.js"&gt;&lt;/script&gt;
&lt;script src="https://d3js.org/d3-collection.v1.min.js"&gt;&lt;/script&gt;
&lt;script src="https://d3js.org/d3-color.v1.min.js"&gt;&lt;/script&gt;
&lt;script src="https://d3js.org/d3-format.v1.min.js"&gt;&lt;/script&gt;
&lt;script src="https://d3js.org/d3-interpolate.v1.min.js"&gt;&lt;/script&gt;
&lt;script src="https://d3js.org/d3-time.v1.min.js"&gt;&lt;/script&gt;
&lt;script src="https://d3js.org/d3-time-format.v2.min.js"&gt;&lt;/script&gt;
&lt;script src="https://d3js.org/d3-scale.v1.min.js"&gt;&lt;/script&gt;

&lt;script&gt;

var x = d3.scaleLinear();

&lt;/script&gt;
</pre>

    <p class="p">(You can omit d3-time and d3-time-format if you’re not using <code class="literal">d3.scaleTime</code> or <code class="literal">d3.scaleUtc</code>.)</p>

  

<h2>API Reference</h2>
<ul>
<li>Continuous (Linear, Power, Log, Identity, Time)</li>
<li>Sequential</li>
<li>Quantize</li>
<li>Quantile</li>
<li>Threshold</li>
<li>Ordinal (Band, Point, Category)</li>
<li>Continuous Scales</li>
</ul>
<p class="it">Las escalas continuas asignan un dominio de entrada cuantitativo continuo a un rango de salida continuo. Si el rango es también numérico, la asignación puede invertirse. Una escala continua no se construye directamente; En su lugar, pruebe una escala de color lineal, de energía, de registro, de identidad, de tiempo o secuencial.</p>
<p class="p">Continuous scales map a continuous, quantitative input domain to a continuous output range. If the range is also numeric, the mapping may be inverted. A continuous scale is not constructed directly; instead, try a linear, power, log, identity, time or sequential color scale.</p>




<h3># continuous(value) </h3>
<p class="it">Dado un valor del dominio, devuelve el valor correspondiente del rango. Si el valor dado está fuera del dominio, y el bloqueo no está habilitado, la correlación se puede extrapolar de tal manera que el valor devuelto esté fuera del rango. Por ejemplo, para aplicar una codificación de posición:</p>
<p class="p">Given a value from the domain, returns the corresponding value from the range. If the given value is outside the domain, and clamping is not enabled, the mapping may be extrapolated such that the returned value is outside the range. For example, to apply a position encoding:</p>


<pre class="programlisting" data-language="javascript" id="100">
var x = d3.scaleLinear()
    .domain([10, 130])
    .range([0, 960]);

x(20); // 80
x(50); // 320
</pre>
<div>
Or to apply a color encoding:
</div>
<pre class="programlisting" data-language="javascript" id="101">
var color = d3.scaleLinear()
    .domain([10, 100])
    .range(["brown", "steelblue"]);

color(20); // "#9a3439"
color(50); // "#7b5167"
</pre>

<h3># continuous.invert(value) </h3>
<p class="it">Dado un valor del rango, devuelve el valor correspondiente de dominio. La inversión es útil para la interacción, por ejemplo para determinar el valor de los datos correspondiente a la posición del ratón. Por ejemplo, para invertir una codificación de posición:</p>
<p class="p">Given a value from the range, returns the corresponding value from the domain. Inversion is useful for interaction, say to determine the data value corresponding to the position of the mouse. For example, to invert a position encoding:</p>

<pre class="programlisting" data-language="javascript" id="112">
var x = d3.scaleLinear()
    .domain([10, 130])
    .range([0, 960]);

x.invert(80); // 20
x.invert(320); // 50
</pre>
<p class="it">Si el valor dado está fuera del rango, y el bloqueo no está habilitado, la correlación se puede extrapolar de tal manera que el valor devuelto esté fuera del dominio. Este método sólo se admite si el rango es numérico. Si el rango no es numérico, devuelve NaN.</p>
<p class="p">If the given value is outside the range, and clamping is not enabled, the mapping may be extrapolated such that the returned value is outside the domain. This method is only supported if the range is numeric. If the range is not numeric, returns NaN.</p>
<p class="it">Para un valor válido <strong>y</strong> en el rango, continuo (continuo.invert (y)) es aproximadamente igual a <strong>y</strong>; De manera similar, para un valor <strong>x</strong> válido en el dominio, continuous.invert (continuo (x)) aproximadamente igual a <strong>x</strong>. La escala y su inversa pueden no ser exactas debido a las limitaciones de la precisión de punto flotante.</p>
<p class="p">For a valid value <strong>y</strong> in the range, continuous(continuous.invert(y)) approximately equals <strong>y</strong>; similarly, for a valid value <strong>x</strong> in the domain, continuous.invert(continuous(x)) approximately equals <strong>x</strong>. The scale and its inverse may not be exact due to the limitations of floating point precision.</p>

<h3># continuous.domain([domain])</h3>
<p class="it">Si se especifica dominio, establece el dominio de la escala en el array de números especificada. el array debe contener dos o más elementos. Si los elementos del array dado no son números, serán forzados a números. Si no se especifica dominio, devuelve una copia del dominio actual de la escala.</p>
<p class="p">If domain is specified, sets the scale’s domain to the specified array of numbers. The array must contain two or more elements. If the elements in the given array are not numbers, they will be coerced to numbers. If domain is not specified, returns a copy of the scale’s current domain.</p>
<p class="it">Aunque las escalas continuas típicamente tienen dos valores cada uno en su dominio y rango, especificando más de dos valores produce una escala por piezas. Por ejemplo, para crear una escala de color divergente que interpola entre blanco y rojo para valores negativos y blanco y verde para valores positivos, digamos:</p>
<p class="p">Although continuous scales typically have two values each in their domain and range, specifying more than two values produces a piecewise scale. For example, to create a diverging color scale that interpolates between white and red for negative values, and white and green for positive values, say:</p>

<pre class="programlisting" data-language="javascript" id="103">
var color = d3.scaleLinear()
    .domain([-1, 0, 1])
    .range(["red", "white", "green"]);

color(-0.5); // "rgb(255, 128, 128)"
color(+0.5); // "rgb(128, 192, 128)"
</pre>
<p class="it">Internamente, una escala por pieza realiza una búsqueda binaria para el interpolador de rango correspondiente al valor de dominio dado. Por lo tanto, el dominio debe estar en orden ascendente o descendente. Si el dominio y el rango tienen diferentes longitudes N y M, sólo se observan los primeros elementos min (N, M) en cada uno.</p>
<p class="p">Internally, a piecewise scale performs a binary search for the range interpolator corresponding to the given domain value. Thus, the domain must be in ascending or descending order. If the domain and range have different lengths N and M, only the first min(N,M) elements in each are observed.</p>

<h3># continuous.range([range])</h3>
<p class="it">Si se especifica rango, establece el rango de la escala en la array de valores especificada. La array debe contener dos o más elementos. A diferencia del dominio, los elementos de la array dada no necesitan ser números; Cualquier valor que es soportado por el interpolador subyacente funcionará, aunque tenga en cuenta que se requieren intervalos numéricos para invertir. Si no se especifica rango, devuelve una copia del rango actual de la escala. Vea continuous.interpolate para más ejemplos.</p>
<p class="p">If range is specified, sets the scale’s range to the specified array of values. The array must contain two or more elements. Unlike the domain, elements in the given array need not be numbers; any value that is supported by the underlying interpolator will work, though note that numeric ranges are required for invert. If range is not specified, returns a copy of the scale’s current range. See continuous.interpolate for more examples.</p>

<h3># continuous.rangeRound([range])</h3>
<p class="it">Establece el rango de la escala a la array de valores especificada al mismo tiempo que se establece el interpolador de escala a interpolator. Este es un método de conveniencia equivalente a:</p>

<p class="p">Sets the scale’s range to the specified array of values while also setting the scale’s interpolator to interpolateRound. This is a convenience method equivalent to:</p>
<pre class="programlisting" data-language="javascript" id="104">
continuous
    .range(range)
    .interpolate(d3.interpolateRound);</pre>
<p class="it">El interpolador de redondeo es a veces útil para evitar artefactos de antialiasing, aunque también considere los estilos "crispEdges" de representación de formas. Tenga en cuenta que este interpolador sólo se puede utilizar con rangos numéricos.</p>

<p class="p">The rounding interpolator is sometimes useful for avoiding antialiasing artifacts, though also consider the shape-rendering “crispEdges” styles. Note that this interpolator can only be used with numeric ranges.</p>

<h3># continuous.clamp(clamp)</h3>







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