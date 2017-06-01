<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    
    <div class="block">

<h1>Chapter 6. Drawing with Data</h1>
<p class="it">Es hora de empezar a dibujar con datos.</p>
<p class="p">It’s time to start drawing with data.</p>

<p class="it">Por ahora vamos a seguir trabajando con nuestro sencillo conjunto de datos:</p>
<p class="p">Let’s continue working with our simple dataset for now:</p>

<pre class="programlisting" data-language="javascript" id="width_and_hei_id20">

     var dataset = [ 5, 10, 15, 20, 25 ];</pre>


<h3>Drawing divs</h3>

<p class="it">Usaremos esto para generar un super-simple gráfico de barras. Los gráficos de barras sólo son esencialmente  rectángulos, y un div HTML es la manera más fácil de dibujar un rectángulo. (Por otra parte, para un navegador web, todo es un rectángulo, por lo que fácilmente podría adaptar este ejemplo para utilizar spans o el elemento que prefiera.)</p>

<p class="p">We’ll use this to generate a super-simple bar chart. Bar charts are essentially just rectangles, and an HTML div is the easiest way to draw a rectangle. (Then again, to a web browser, everything is a rectangle, so you could easily adapt this example to use spans or whatever element you prefer.)</p>

<p class="it">Formalmente, un gráfico con rectángulos orientados verticalmente es un gráfico de columnas, y uno con rectángulos horizontales es un gráfico de barras. En la práctica, la mayoría de la gente simplemente los llama a todos  gráficos de barras, como lo haré a partir de ahora.</p>

<p class="p">Formally, a chart with vertically oriented rectangles is a column chart, and one with horizontal rectangles is a bar chart. In practice, most people just call them all bar charts, as I’ll do from now on.</p>

<p class="it">Este div podría funcionar bien como una barra de datos. Lo muestro en la Figura 6-1 </p>
<p class="p">This div could work well as a data bar, shown in Figure 6-1.</p>

<h3>A humble div</h3>

<p class="fig">Figura 6-1. Un humilde div</p>
<p class="fig">Figure 6-1. A humble div</p>

<p class="it">Dentro de los estándares web, se trata de una semántica no-no. Normalmente, no se debe utilizar un div vacío para lograr un efecto puramente visual, pero estoy haciendo una excepción por el bien de este ejemplo.</p>
<p class="p">Among web standards folks, this is a semantic no-no. Normally, one shouldn’t use an empty div for purely visual effect, but I am making an exception for the sake of this example.</p>

<p class="it">Debido a que este es un div, su anchura y altura se establecen con estilos CSS. A excepción de la altura, cada barra en nuestro chart compartirá las mismas propiedades de la pantalla, por lo que voy a poner los estilos compartidos en una clase llamada bar, como un estilo incrustado en el encabezado del documento:</p>

<p class="p">Because this is a div, its width and height are set with CSS styles. Except for height, each bar in our chart will share the same display properties, so I’ll put those shared styles into a class called bar, as an embedded style up in the head of the document:</p>


<pre class="programlisting" data-language="javascript" id="width_and_hei_id24">      div.bar {
          display: inline-block;
          width: 20px;
          height: 75px;   /* We'll override height later. Anularemos la altura más tarde*/
          background-color: teal;
    }</pre>
<p class="it">Ahora cada div necesita ser asignado a la clase de barras, por lo que se aplicará la nueva regla CSS. Si estuviera escribiendo el código HTML a mano, podría escribir lo siguiente:</p>

<p class="p">Now each div needs to be assigned the bar class, so our new CSS rule will apply. If you were writing the HTML code by hand, you would write the following:</p>


<pre class="programlisting" data-language="html" id="width_and_hei_id223"> 
        &lt;div class="bar"&gt;&lt;/div&gt;
        </pre>
<p class="it">Usando D3, para agregar una clase a un elemento, se utiliza el método de selection.attr(). Es importante entender la diferencia entre attr() y su primo cercano, el style(). El metodo attr() establece los valores de atributos DOM, mientras que el metodo style() aplica estilos CSS directamente a un elemento.</p>

<p class="p">Using D3, to add a class to an element, we use the selection.attr() method. It’s important to understand the difference between attr() and its close cousin, style(). attr() sets DOM attribute values, whereas style() applies CSS styles directly to an element.</p>


<h3>Setting Attributes</h3>

<p class="it">attr() se utiliza para establecer un atributo HTML y su valor en un elemento. Un atributo HTML es cualquier pareja de propiedad/valor que se podría incluir entre corchetes &lt;&gt; de un elemento. Por ejemplo, estos elementos HTML:</p>

<p class="p">attr() is used to set an HTML attribute and its value on an element. An HTML attribute is any property/value pair that you could include between an element’s &lt;&gt; brackets. For example, these HTML elements:</p>



<pre class="programlisting" data-language="html" id="width_and_hei_id23345">        &lt;p class="caption"&gt;
        &lt;select id="country"&gt;
        &lt;img src="logo.png" width="100px" alt="Logo" /&gt;</pre>


<p class="it">contiene un total de cinco atributos (y los valores correspondientes), todo lo cual podría configurarlo con attr():</p>
<p class="p">contain a total of five attributes (and corresponding values), all of which could be set with attr():</p>

<div>
<table>
<tr>
  <td><strong>Attribute</strong></td>
  <td><strong>Value</strong></td>
</tr>
 
<tr>
  <td>class</td>
  <td>caption</td>

</tr>
 
<tr>
  <td>ID</td>
  <td>country</td>

</tr>
 
<tr>
  <td>src</td>
  <td>logo.png</td>

</tr>
<tr>
  <td>width</td>
  <td>100px</td>

</tr><tr>
  <td>alt</td>
  <td>Logo</td>

</tr>
</table>

</div>


<p class="it">Para asignar una clase de barra, podemos utilizar:</p>

<p class="p">To assign a class of bar, we can use:</p>



<pre class="programlisting" data-language="javascript" id="width_and_hei_id22">        .attr("class", "bar")</pre>


<h3>A Note on Classes</h3>

<p class="it">Tenga en cuenta que la clase de un elemento se almacena como un atributo HTML. La clase, a su vez, se utiliza para hacer referencia a una regla de estilo CSS. Esto podría causar cierta confusión porque hay una diferencia entre el establecimiento de una clase (de la que se infieren estilos) y la aplicación de un estilo directamente a un elemento. Puede hacer ambas cosas con D3. Aunque se debe usar independientemente del enfoque que tiene más sentido para usted, recomiendo el uso de clases de propiedades que son compartidas por múltiples elementos, y la aplicación de reglas de estilo directamente sólo cuando se desvía de la norma. (De hecho, eso es lo que haremos en un momento).</p>
<p class="p">Note that an element’s class is stored as an HTML attribute. The class, in turn, is used to reference a CSS style rule. This could cause some confusion because there is a difference between setting a class (from which styles are inferred) and applying a style directly to an element. You can do both with D3. Although you should use whatever approach makes the most sense to you, I recommend using classes for properties that are shared by multiple elements, and applying style rules directly only when deviating from the norm. (In fact, that’s what we’ll do in just a moment.)</p>

<p class="it">También quiero mencionar brevemente otro método D3, classed(), que se puede utilizar para aplicar rápidamente o eliminar clases de elementos. La línea de código anterior podría reescribirse como la siguiente:</p>
<p class="p">I also want to briefly mention another D3 method, classed(), which can be used to quickly apply or remove classes from elements. The preceding line of code could be rewritten as the following:</p>


    <pre class="programlisting" data-language="javascript" id="width_and_hei_id31">.classed("bar", true)</pre>

<p class="it">Esta línea simplemente toma lo que la selección le pasa a la misma y se aplica a la clase bar. Si se especificara falsa, haría lo contrario, eliminando la clase bar de cualquier elemento en la selección:</p>
<p class="p">This line simply takes whatever selection is passed to it and applies the class bar. If false were specified, it would do the opposite, removing the class of bar from any elements in the selection:</p>

    
    <pre class="programlisting" data-language="javascript" id="width_and_hei_id32">.classed("bar", false)</pre>
<h3>Back to the Bars</h3>

<p class="it">Poniendo todo junto en nuestro conjunto de datos, aquí está el código D3 completo hasta el momento:</p>
<p class="p">Putting it all together with our dataset, here is the complete D3 code so far:</p>


    <pre class="programlisting" data-language="javascript" id="width_and_hei_id47">var dataset = [ 5, 10, 15, 20, 25 ];

d3.select("body").selectAll("div")
    .data(dataset)
    .enter()
    .append("div")
    .attr("class", "bar");</pre>

<p class="it">Para ver lo que está pasando, mire 01_drawing_divs.html en su navegador, vea el código fuente, y abra su inspector web. Debería ver cinco barras verticales, un div generado para cada punto de nuestro conjunto de datos. Sin embargo, sin espacio entre ellas, se ven como un gran rectángulo, como puede verse en las figuras 6-2 y 6-3 .</p>
<p class="p">To see what’s going on, look at 01_drawing_divs.html in your browser, view the source, and open your web inspector. You should see five vertical div bars, one generated for each point in our dataset. However, with no space between them, they look like one big rectangle, as seen in Figures 6-2 and 6-3.</p>



<img alt="Imagen" src="/static/Fig602.png" />

<p class="fig">Figure 6-2. Five divs masquerading as one</p>

<p class="p">Five divs masquerading as one, as seen through the web inspector</p>

<img alt="Imagen" src="/static/Fig603.png" />
<p class="fig">Figure 6-3. Five divs masquerading as one, as seen through the web inspector</p>


<h3>Setting Styles</h3>


<p class="it">El método style() se utiliza para aplicar una propiedad CSS y valorar directamente a un elemento HTML. Es el equivalente de incluir reglas CSS dentro de un atributo de estilo justo en el código HTML, como en:</p>
<p class="p">The style() method is used to apply a CSS property and value directly to an HTML element. This is the equivalent of including CSS rules within a style attribute right in your HTML, as in:</p>



<pre class="programlisting" data-language="html" id="width_and_hei_id46">

&lt;div style="height: 75px;"&gt;&lt;/div &gt;
</pre>

<p class="it">Para hacer un gráfico de barras, la altura de cada barra debe estar en función de su valor correspondiente de datos. Así que vamos a añadir esto al final de nuestro código D3 (teniendo cuidado de mantener el punto y coma al finalizar la cadena):</p>
<p class="p">To make a bar chart, the height of each bar must be a function of its corresponding data value. So let’s add this to the end of our D3 code (taking care to keep the final semicolon at the very end of the chain):</p>



<pre class="programlisting" data-language="javascript" id="width_and_hei_id45">.style("height", function(d) {
    return d + "px";
});
</pre>

<p class="it">Ver el código en 02_drawing_divs_height.html. Debería ver un pequeño gráfico de barras, como el de la Figura 6-4 .</p>

<p class="p">See that code in 02_drawing_divs_height.html. You should see a very small bar chart, like the one in Figure 6-4.</p>


<img alt="Imagen" src="/static/Fig604.png" />


<p class="fig">Figure 6-4. A small bar chart</p>

<p class="it">Cuando el loop D3 atraviesa cada punto de datos, el valor de <strong>d</strong> se ajustará al valor correspondiente. Así que estamos estableciendo un valor de altura de <strong>d</strong> (el valor actual de datos), añadiendo el texto px (para especificar, las unidades son píxeles). Las alturas resultantes son 5px, 10px, 15px, 20px y 25px.</p>
<p class="p">When D3 loops through each data point, the value of <strong>d</strong> will be set to that of the corresponding value. So we are setting a height value of <strong>d</strong> (the current data value) while appending the text px (to specify the units are pixels). The resulting heights are 5px, 10px, 15px, 20px, and 25px.</p>

<p class="it">Esto parece un poco tonto, por lo que vamos a hacer esas barras más altas:</p>
<p class="p">This looks a little bit silly, so let’s make those bars taller:</p>

<pre class="programlisting" data-language="javascript" id="width_and_hei_id40">.style("height", function(d) {
    var barHeight = d * 5;  //Scale up by factor of 5
    return barHeight + "px";
});</pre>

<p class="it">Pongamos un poco de espacio a la derecha de cada barra (en el estilo CSS incrustado, en el encabezado del documento), para espaciar las cosas:</p>
<p class="p">Add some space to the right of each bar (in the embedded CSS style, in the document head), to space things out:</p>

<pre class="programlisting" data-language="html" id="width_and_hei_id41">margin-right: 2px;</pre>

<p class="it">¡Bonito! Podríamos ir a SIGGRAPH con esa tabla ( Figura 6-5 ).</p>
<p class="p">Nice! We could go to SIGGRAPH with that chart (Figure 6-5).</p>

<h3>A taller bar chart</h3>
<img alt="Imagen" src="/static/Fig605.png" />

<p class="fig">Figura 6-5. Un gráfico de barras más alto</p>
<p class="fig">Figure 6-5. A taller bar chart</p>

<p class="it">Pruebe el código de ejemplo 03_drawing_divs_spaced.html. Una vez más, vea la fuente y utilize el inspector web para contrastar el HTML original con el DOM final.</p>
<p class="p">Try out the sample code 03_drawing_divs_spaced.html. Again, view the source and use the web inspector to contrast the original HTML against the final DOM.</p>


<h3>The Power of data()</h3>

<p class="it">Esto es emocionante, pero los datos del mundo real nunca son tan limpios:</p>
<p class="p">This is exciting, but real-world data is never this clean:</p>



<pre class="programlisting" data-language="javascript" id="width_and_hei_id42">var dataset = [ 5, 10, 15, 20, 25 ];</pre>


<p class="it">Hagamos a nuestros datos un poco más sucios, como en el código 04_power_of_data.html:</p>
<p class="p">Let’s make our data a bit messier, as in 04_power_of_data.html:</p>



<pre class="programlisting" data-language="javascript" id="width_and_hei_id51">var dataset = [ 25, 7, 5, 26, 11 ];
</pre>

<p class="it">Ese cambio en los resultados de datos en las barras se muestra en la Figura 6-6 . No estamos limitados a cinco puntos de datos, por supuesto. Vamos a añadir muchos más! (Ver 05_power_of_data_more_points.html.)</p>
<p class="p">That change in data results in the bars shown in Figure 6-6. We’re not limited to five data points, of course. Let’s add many more! (See 05_power_of_data_more_points.html.)</p>



<pre class="programlisting" data-language="javascript" id="width_and_hei_id52">var dataset = [ 25, 7, 5, 26, 11, 8, 25, 14, 23, 19,
                14, 11, 22, 29, 11, 13, 12, 17, 18, 10,
                24, 18, 25, 9, 3 ];
              </pre>



<h3>New data values</h3>
<img alt="Imagen" src="/static/Fig606.png" />
<p class="fig">Figura 6-6. Los nuevos valores de datos</p>
<p class="fig">Figure 6-6. New data values</p>

<p class="p">Twenty-five data points instead of five (see Figure 6-7)!</p>

<h3>Lots more data values</h3>

<img alt="Imagen" src="/static/Fig607.png" />

<p class="it">Figura 6-7. Más valores de datos</p>
<p class="p">Figure 6-7. Lots more data values</p>

<p class="it">¿Cómo se expande automáticamente nuestra tabla D3 según sea necesario?</p>
<p class="p">How does D3 automatically expand our chart as needed?</p>

<pre class="programlisting" data-language="javascript" id="width_and_hei_id53">d3.select("body").selectAll("div")
    .data(dataset)  //  The answer is here!
    .enter()
    .append("div")
    .attr("class", "bar")
    .style("height", function(d) {
        var barHeight = d * 5;
        return barHeight + "px";
    });</pre>

<p class="it">Entregamos 10 valores de data(), y se hará un loop 10 veces. Le damos un millón de valores, y se hará un loop de un millón de veces. (Sea paciente.)</p>
<p class="p">Give data() 10 values, and it will loop through 10 times. Give it one million values, and it will loop through one million times. (Just be patient.)</p>

<p class="it">Ese es el poder del metodo data() -siendo lo suficientemente inteligente como para recorrer toda la longitud de cualquier conjunto de datos que se le lance, la ejecución de cada método debajo de ella en la cadena, mientras que la actualización del contexto en el que opera cada método, por lo que se refiere a <strong>d</strong> siempre punto de referencia actual en ese punto en el bucle.</p>
<p class="p">That is the power of data()—being smart enough to loop through the full length of whatever dataset you throw at it, executing each method beneath it in the chain, while updating the context in which each method operates, so d always refers to the current datum at that point in the loop.</p>

<p class="it">Esto podría ser un bocadillo, y asi y todo no tiene sentido, sin embargo, pronto lo tendrá. Lo animo a hacer una copia de 05_power_of_data_more_points.html, ajustar los valores del conjunto de datos, teniendo en cuenta cómo cambia el gráfico de barras.</p>
<p class="p">That might be a mouthful, and if it all doesn’t make sense yet, it will soon. I encourage you to make a copy of 05_power_of_data_more_points.html, tweak the dataset values, and note how the bar chart changes.</p>

<p class="it">Ajuste los valores del conjunto de datos en el código de abajo a la izquierda y observe cómo cambia el gráfico de barras a la derecha.</p>

<p class="p">Tweak the dataset values in the code below at left, and note how the bar chart changes at right.</p>

<h3>Open in new window</h3>

<p class="it">Recuerde, los datos estan impulsando la visualización, y no al revés.</p>
<p class="p">Remember, the data is driving the visualization—not the other way around.</p>


<h3>Random Data</h3>

<p class="it">A veces es divertido el generar valores de datos al azar, ya sea con fines de prueba o  sólo puros geekiness. Eso es justo lo que he hecho en 06_power_of_data_random.html. Tenga en cuenta que cada vez que vuelva a cargar la página, las barras estaran de manera diferente, como se muestra en la Figura 6-8 .</p>
<p class="p">Sometimes it’s fun to generate random data values, whether for testing purposes or just pure geekiness. That’s just what I’ve done in 06_power_of_data_random.html. Notice that each time you reload the page, the bars render differently, as shown in Figure 6-8.</p>


<h3>Bar charts with random values</h3>
<img alt="Imagen" src="/static/Fig608.png" />
<p class="fig">Figura 6-8. Los gráficos de barras con valores aleatorios</p>
<p class="fig">Figure 6-8. Bar charts with random values</p>


<p class="it">Al ver el código fuente, tendrá este código:</p>
<p class="p">View the source, and you’ll see this code:</p>

<pre class="programlisting" data-language="javascript" id="width_and_hei_id29532">var dataset = [];                         //Initialize empty array
for (var i = 0; i &lt; 25; i++) {            //Loop 25 times
    var newNumber = Math.random() * 30;   //New random number (0-30)
    dataset.push(newNumber);              //Add new number to array
}</pre>

<p class="it">Ese código no utiliza ningún método D3; es sólo JavaScript. Sin entrar en demasiados detalles, este código hace lo siguiente:</p>
<p class="p">That code doesn’t use any D3 methods; it’s just JavaScript. Without going into too much detail, this code does the following:</p>

<p class="it">Crea un array vacío llamado conjunto de datos.</p>
<p class="p">Creates an empty array called dataset.</p>

<p class="it">Inicia un loop, que se ejecuta 25 veces.</p>
<p class="p">Initiates a for loop, which is executed 25 times.</p>

<p class="it">Cada vez, genera un nuevo número aleatorio con un valor entre 0 y 30. (Bueno, técnicamente, casi 30. Math.random() devuelve valores tan bajos como 0,0 y todo el camino hasta 1.0, pero sin incluirlo. Así que si Math.random() devuelve 0,99999, entonces el resultado sería 0,99999 veces 30, que es 29,9997, o el bit anterior a 30.)</p>
<p class="p">Each time, it generates a new random number with a value between 0 and 30. (Well, technically, almost 30. Math.random() returns values as low as 0.0 all the way up to, but not including, 1.0. So if Math.random() returned 0.99999, then the result would be 0.99999 times 30, which is 29.9997, or the teensiest bit less than 30.)</p>

<p class="p">Ese nuevo número se añade al array de datos. (push() es un método de array que añade un nuevo valor al final de una array.)</p>
<p class="p">That new number is appended to the dataset array. (push() is an array method that appends a new value to the end of an array.)</p>


<p class="it">Sólo por diversión, abra la consola de JavaScript y escriba console.log(dataset). Debería ver la gama completa de 25 valores de datos aleatorios, como se muestra en la Figura 6-9 .</p>
<p class="p">Just for kicks, open up the JavaScript console and enter console.log(dataset). You should see the full array of 25 randomized data values, as shown in Figure 6-9.</p>


<h3>Random values in console</h3>
<img alt="Imagen" src="/static/Fig609.png" />

<p class="p">Figure 6-9. Random values in console</p>

<p class="it">Tenga en cuenta que todos ellos son valores decimales o de punto flotante (tales como 14,793717765714973), no números enteros o números enteros (como 14) al igual que los utilizados inicialmente. Para este ejemplo, los valores decimales están muy bien, pero si alguna vez necesita números enteros, se podrían utilizar los métodos Math.floor() o Math.round() de JavaScript. Math.round() redondea un número al entero más próximo, mientras que Math.floor() siempre redondea hacia abajo, para un mayor control sobre el resultado. Por ejemplo, se puede envolver al generador de números aleatorios de esta línea:</p>
<p class="p">Notice that they are all decimal or floating point values (such as 14.793717765714973), not whole numbers or integers (such as 14) like we used initially. For this example, decimal values are fine, but if you ever need whole numbers, you could use JavaScript’s Math.round() or Math.floor() methods. Math.round() rounds any number to the nearest integer, whereas Math.floor() always rounds down, for greater control over the result. For example, you could wrap the random number generator from this line:</p>

<pre class="programlisting" data-language="javascript" id="width_and_hei_id22432">    var newNumber = Math.random() * 30;</pre>

<p class="it">como sigue:</p>
<p class="p">as follows:</p>

<pre class="programlisting" data-language="javascript" id="width_and_hei_id285743">    var newNumber = Math.floor(Math.random() * 30);</pre>

<p class="it">El uso de este código, newNumber siempre sería o bien 0 o 29, o cualquier número entero en el medio. ¿Por qué no 30? Debido a que Math.random() siempre devuelve valores inferiores a 1,0, y Math.floor() siempre se redondea hacia abajo, por lo que 29 es el valor de retorno más alto posible.</p>
<p class="p">Using this code, newNumber would always be either 0 or 29, or any integer in between. Why not 30? Because Math.random() always returns values less than 1.0, and Math.floor() will always round down, so 29 is the highest possible return value.</p>

<p class="it">Inténtelo con 07_power_of_data_rounded.html, y utilize la consola para verificar que los números de hecho han sido redondeados a enteros, como se muestra en la figura 6-10 .</p>
<p class="p">Try it out in 07_power_of_data_rounded.html, and use the console to verify that the numbers have indeed been rounded to integers, as displayed in Figure 6-10.</p>


<p class="p">Random integer values in console</p>

<img alt="Imagen" src="/static/Fig610.png" />

<p class="fig">Figura 6-10. Valores enteros aleatorios en la consola</p>
<p class="fig">Figure 6-10. Random integer values in console</p>


<p class="it">Eso es todo lo que podemos hacer visualmente con divs. Vamos a ampliar nuestras posibilidades visuales con SVG.</p>
<p class="p">That’s about all we can do visually with divs. Let’s expand our visual possibilities with SVG.</p>


<h3>Drawing SVGs</h3>


<p class="it">Para hacer un repaso rápido sobre la sintaxis SVG, consulte "SVG" .</p>
<p class="p">For a quick refresher on SVG syntax, see “SVG”.</p>

<p class="it">Una cosa que puede observar sobre los elementos SVG es que todas sus propiedades se especifican como atributos. Es decir, que se incluyen como pares de propiedad/valor dentro de cada etiqueta de elemento, como esta:</p>
<p class="it">One thing you might notice about SVG elements is that all of their properties are specified as attributes. That is, they are included as property/value pairs within each element tag, like this:</p>



<pre class="programlisting" data-language="html" id="width_and_hei_id2754">
&lt;element property="value"/&gt;</pre>


<p class="p">Hmm, that looks strangely like HTML!</p>

<pre class="programlisting" data-language="html" id="width_and_hei_id98">&lt;p class="eureka"&gt;Eureka!&lt;/p&gt;
</pre>
<p class="it">Ya hemos utilizado los métodos  de D3 attr() y append() para crear nuevos elementos HTML y establecer sus atributos. Debido a que existen elementos SVG en el DOM, al igual que lo hacen los elementos HTML, podemos usar append() y attr() exactamente de la misma manera para generar imágenes SVG.</p>
<p class="p">We have already used D3’s handy append() and attr() methods to create new HTML elements and set their attributes. Because SVG elements exist in the DOM, just as HTML elements do, we can use append() and attr() in exactly the same way to generate SVG images.</p>


<h3>Create the SVG</h3>

<p class="it">En primer lugar, tenemos que crear el elemento SVG en el que colocar todas nuestras formas:</p>
<p class="p">First, we need to create the SVG element in which to place all our shapes:</p>



<pre class="programlisting" data-language="javascript" id="width_and_hei_id25700">d3.select("body").append("svg");</pre>

<p class="it">Con esto se va a encontrar el cuerpo del documento y añadirá un nuevo elemento SVG justo antes de la etiqueta de cierre &lt;/body&gt;. Ese código funcionará, pero me gustaría sugerir una ligera modificación:</p>
<p class="p">That will find the document’s body and append a new svg element just before the closing &lt;/body&gt; tag. That code will work, but I’d like to suggest a slight modification:</p>



<pre class="programlisting" data-language="javascript" id="width_and_hei_id29456">var svg = d3.select("body").append("svg");</pre>

<p class="it">Recuerda que, cómo la mayoría de los métodos D3, devuelve una referencia al elemento DOM sobre el que actúa?</p>
<p class="p">Remember how most D3 methods return a reference to the DOM element on which they act? </p>

<p class="it"> Mediante la creación de una nueva variable de SVG, somos capaces de capturar la referencia devuelta por apend(). Piense en SVG no como una variable pero, que señala una referencia al objeto SVG que acabamos de crear. Esta referencia nos ahorrará una gran cantidad de código más tarde. En lugar de tener que buscar SVG cada ves, con d3.select("svg") -nos dará los SVG:</p>

<p class="p">By creating a new variable svg, we are able to capture the reference handed back by append(). Think of svg not as a variable but as a reference pointing to the SVG object that we just created. This reference will save us a lot of code later. Instead of having to search for that SVG each time—as in d3.select("svg")—we just say svg:</p>


<pre class="programlisting" data-language="javascript" id="width_and_hei_id209">svg.attr("width", 500)
   .attr("height", 50);
 </pre>

<p class="it">Por otra parte, todo se podría escribir en una sola línea de código:</p>
<p class="p">Alternatively, that could all be written as one line of code:</p>

<pre class="programlisting" data-language="javascript" id="width_and_hei_id277">var svg = d3.select("body")
            .append("svg")
            .attr("width", 500)
            .attr("height", 50);</pre>

<p class="it">Ver 08_drawing_svgs.html para ese código. Inspeccione el DOM y observe que hay, de hecho, un elemento SVG vacío.</p>            
<p class="p">See 08_drawing_svgs.html for that code. Inspect the DOM and notice that there is, indeed, an empty SVG element.</p>

<p class="it">Para simplificar su vida, yo recomiendo poner los valores de anchura y altura en variables en la parte superior de su código, como en 09_drawing_svgs_size.html. Observe el código fuente, y verá el siguiente código:</p>
<p class="p">To simplify your life, I recommend putting the width and height values into variables at the top of your &lt;/code&lt;, as in 09_drawing_svgs_size.html. View the source, and you’ll see the following code:</p>

<pre class="programlisting" data-language="javascript" id="width_and_hei_id297">//Width and height
var w = 500;
var h = 50;</pre>

<p class="it">Voy a estar haciendo eso con todos los ejemplos futuros.</p>
<p class="p">I’ll be doing that with all future examples. </p>

<p class="it"> Para variabalizing los valores de tamaño, puede hacer referencia fácilmente a través de su código, como en el siguiente:</p>
<p class="p">By variabalizing the size values, they can be easily referenced throughout your code, as in the following:</p>

<pre class="programlisting" data-language="javascript" id="width_and_hei_id20644">var svg = d3.select("body")
            .append("svg")
            .attr("width", w)   // &lt;-- Here
            .attr("height", h); // &lt;-- and here!</pre>

<p class="it">Además, si usted me envía una petición para hacer de  "variabalize" una palabra real, con mucho gusto lo firmare.</p>            
<p class="p">Also, if you send me a petition to make “variabalize” a real word, I will gladly sign it.</p>


<h3>Data-Driven Shapes</h3>

<p class="it">Es hora de añadir algunas formas. Voy a traer de vuelta nuestra vieja base de datos de confianza:</p>
<p class="p">Time to add some shapes. I’ll bring back our trusty old dataset:</p>

<pre class="programlisting" data-language="javascript" id="width_and_hei_id26890">var dataset = [ 5, 10, 15, 20, 25 ];</pre>
<p class="it">y luego utilizare data() para iterar a través de cada punto de datos, creando un círculo para cada uno:</p>
<p class="p">and then use data() to iterate through each data point, creating a circle for each one:</p>


<pre class="programlisting" data-language="javascript" id="width_and_hei_id2088">svg.selectAll("circle")
    .data(dataset)
    .enter()
    .append("circle");</pre>

<p class="it">Recuerde, selectAll() devolverá referencias vacías de todos los círculos (que aún no existen), data() une nuestros datos a los elementos que estamos a punto de crear, data() devuelve una referencia al marcador de posición del nuevo elemento, y append() finalmente añade un círculo para el DOM. En este caso, añade los círculos al extremo del elemento SVG, como nuestra selección inicial es nuestra SVG de referencia (en comparación con el cuerpo del documento, por ejemplo).</p>    
<p class="p">Remember, selectAll() will return empty references to all circles (which don’t exist yet), data() binds our data to the elements we’re about to create, enter() returns a placeholder reference to the new element, and append() finally adds a circle to the DOM. In this case, it appends those circles to the end of the SVG element, as our initial selection is our reference svg (as opposed to the document body, for example).</p>

<p class="it">Para que sea más fácil hacer referencia a todos los círculos mas tarde, podemos crear una nueva variable para almacenar referencias a todos ellos:</p>
<p class="p">To make it easy to reference all of the circles later, we can create a new variable to store references to them all:</p>

<pre class="programlisting" data-language="javascript" id="width_and_hei_id2979">var circles = svg.selectAll("circle")
                 .data(dataset)
                 .enter()
                 .append("circle");</pre>

<p class="it">Grandioso, pero todos estos círculos todavía tienen posiciones y tamaños, que se muestran en la Figura 6-11 . Tenga en cuenta que el siguiente código podría soplar su mente:</p>                 
<p class="p">Great, but all these circles still need positions and sizes, displayed in Figure 6-11. Be warned, the following code might blow your mind:</p>

<pre class="programlisting" data-language="javascript" id="width_and_hei_id2086">circles.attr("cx", function(d, i) {
            return (i * 50) + 25;
        })
       .attr("cy", h/2)
       .attr("r", function(d) {
            return d;
       });</pre>
<h3>Row of data circles</h3>
<img alt="Imagen" src="/static/Fig611.png" />
<p class="p">Figure 6-11. Row of data circles</p>
<p class="it">Figura 6-11. Fila de los círculos de datos</p>
<p class="p">Feast your eyes on the demo 10_drawing_svgs_circles.html. Let’s step through the code, one line at a time:</p>
<p class="it">Un regalo para los ojos en el demo 10_drawing_svgs_circles.html. Vamos paso a paso a través del código, una línea a la vez:</p>
<pre class="programlisting" data-language="javascript" id="width_and_hei_id28756">circles.attr("cx", function(d, i) {
            return (i * 50) + 25;
        })</pre>
<p class="p">This takes the reference to all circles and sets the cx attribute for each one. (Remember that, in SVG lingo, cx is the<code class="literal">x</code>position value of the center of the circle.) Our data has already been bound to the circle elements, so for each circle, the value <strong>d</strong> matches the corresponding value in our original dataset (5, 10, 15, 20, or 25).</p>
<p class="p">Esto toma de referencia a todos los círculos y establece el atributo cx para cada uno. (Recuerde que en la jerga SVG, cx es el valor de la posición <code class="literal">x</code> del centro del círculo.) Nuestros datos ya se han unido a los elementos del círculo, por lo que para cada círculo, el valor <strong>d</strong> coincide con el valor correspondiente en nuestra base de datos original ( 5, 10, 15, 20, y 25).</p>

<p class="p">Another value, <strong>i</strong>, is also automatically populated for us. (Thanks, D3!) Just as with <strong>d</strong>, the name <strong>i</strong> here is arbitrary and could be set to whatever you like, such as <strong>counter</strong> or <strong>elementID</strong>. I prefer to use <strong>i</strong> because it is concise, it alludes to the convention of using <strong>i</strong> in for loops, and it is very common, as you’ll see it in all the online examples.</p>
<p class="it">Otro valor, <strong>i</strong>, también se rellena automáticamente para nosotros. (Gracias, D3!) Al igual que con <strong>d</strong>, el nombre <strong>i</strong> aquí es arbitrario y podría ajustarse a lo que usted desee, como <strong>counter</strong> o <strong>elementID</strong>. Yo prefiero usar <strong>i</strong> porque es conciso, y alude a la convención de usar <strong>i</strong> en los loops, y es muy común, como se verá en todos los ejemplos en línea.</p>

<p class="p">So, i is a numeric index value of the current element. Counting starts at zero, so for our “first” circle i == 0, the second circle’s i == 1, and so on. We’re using i to push each subsequent circle over to the right, because each subsequent loop through, the value of i increases by one:</p>
<p class="it">Por lo tanto, <strong>i</strong> es un valor de índice numérico del elemento actual. El recuento comienza en cero, por lo que para nuestro "primer" círculo i == 0,  en el segundo círculo i == 1, y así sucesivamente. Estamos utilizando <strong>i</strong> para empujar cada círculo posterior a la derecha, ya que cada loop posterior a través de, el valor de <strong>i</strong> se incrementa en uno:</p>
<pre class="programlisting" data-language="javascript" id="width_and_hei_id29565">(0 * 50) + 25   //Returns 25
(1 * 50) + 25   //Returns 75
(2 * 50) + 25   //Returns 125
(3 * 50) + 25   //Returns 175
(4 * 50) + 25   //Returns 225
</pre>
<p class="p">To make sure <strong>i</strong> is available to your custom function, you must include it as an argument in the function definition, function(d, i). You must also include <strong>d</strong>, even if you don’t use <strong>d</strong> within your function (as in the preceding case). This is because, again, the actual names used for these arguments are not important, but the total number of arguments (one or two) is.</p>
<p class="it">Para asegurarse de que <strong>i</strong> está disponible para la función personalizada, debe incluirlo como un argumento en la definición de la función, la <strong>function(d, i)</strong>. También debe incluir <strong>d</strong>, incluso si usted no usa <strong>d</strong> dentro de su función (como en el caso anterior). Esto es porque, de nuevo, los nombres reales utilizados para estos argumentos no son importantes, pero el número total de argumentos es (uno o dos).</p>

<p class="p">Also, in case you’re feeling a surge of parameter anxiety, don’t worry. You’ll only ever have to worry about <strong>d</strong> and <strong>i</strong>. There are no additional anonymous function parameters to learn about later.</p>
<p class="it">Además, en caso de que esté sintiendo una oleada de parámetro-ansiedad, no se preocupe. Sólo tiene que preocuparse por <strong>d</strong> o <strong>i</strong>. No existen parámetros de la función anónimos adicionales para aprender más adelante.</p>

<p class="p">On to the next line:</p>
<p class="it">A la siguiente línea:</p>

<pre class="programlisting" data-language="javascript" id="width_and_hei_id2687">.attr("cy", h/2)</pre>
<p class="p">cy is the y position value of the center of each circle. We’re setting cy to <strong>h</strong> divided by two, or one-half of <strong>h</strong>. You’ll recall that <strong>h</strong> stores the height of the entire SVG, so <strong>h/2</strong> has the effect of aligning all circles in the vertical center of the image:</p>
<p class="it"><strong>cy</strong> es el valor de la posición y del centro de cada círculo. Estamos estableciendo <strong>cy</strong> a <strong>h</strong> dividido por dos, o de un medio de <strong>h</strong>. Usted recordará que <strong>h</strong> almacena la altura de todo el SVG, por lo que <strong>h/2</strong> tiene el efecto de alinear todos los círculos en el centro vertical de la imagen:</p>
<pre class="programlisting" data-language="javascript" id="width_and_hei_id255436">.attr("r", function(d) {
    return d;
});</pre>
<p class="p">Finally, the radius <strong>r</strong> of each circle is simply set to <strong>d</strong>, the corresponding data value.</p>
<p class="it">Por último, el radio <strong>r</strong> de cada círculo está configurado simplemente para el valor de datos correspondiente a <strong>d</strong>.</p>

<p class="p">Pretty Colors, Oooh!</p>

<p class="p">Color fills and strokes are just other attributes that you can set using the same methods. Simply by appending this code:</p>
<p class="it">El color fills y strokes son sólo otros atributos que se pueden establecer utilizando los mismos métodos. Simplemente añadiendo este código:</p>
<pre class="programlisting" data-language="javascript" id="width_and_hei_id275674">.attr("fill", "yellow")
.attr("stroke", "orange")
.attr("stroke-width", function(d) {
    return d/2;
});</pre>
<p class="p">we get the colorful circles shown in Figure 6-12, as seen in 11_drawing_svgs_color.html.</p>
<p class="p">Así obtenemos los círculos de colores que se muestran en la figura 6-12 , como se ve en 11_drawing_svgs_color.html.</p>

<h3>Colorful data circles</h3>
<img alt="Imagen" src="/static/Fig612.png" />
<p class="p">Figure 6-12. Colorful data circles</p>
<p class="p">Figura 6-12. Coloridos círculos de datos</p>


<p class="p">Of course, you can mix and match attributes and custom functions to apply any combination of properties. The trick with data visualization, of course, is choosing appropriate mappings, so the visual expression of your data is understandable and useful for the viewer.</p>

<p class="it">Por supuesto, usted puede mezclar, atribuir y hacer funciones para aplicar cualquier combinación de propiedades. El truco con la visualización de datos, por supuesto, es la elección de los mappings apropiados para que la expresión visual de sus datos sea comprensible y útil para el espectador.</p>



<h3>Making a Bar Chart</h3>

<p id="now_well_integ" class="">Now we’ll integrate everything we’ve learned so far to generate a simple bar chart as an SVG image.<a id="ix_bchrt" class="indexterm" href=""></a></p>
<p class="it">Ahora integraremos todo lo que han aprendido hasta ahora para generar un gráfico de barras simple como una imagen SVG.</p>

<p id="well_start_by__id1" class="">We’ll start by adapting the <code class="literal">div</code> bar chart code to draw its bars with SVG instead, giving us more flexibility over the visual presentation. Then we’ll add labels, so we can see the data values clearly.</p>
<p class="it">Empezaremos por la adaptación del código gráfico de barras div para dibujar en cambio sus bars con SVG, esto nos dara más flexibilidad en la presentación visual. A continuación, vamos a añadir etiquetas, para que podamos ver con claridad los valores de los datos.</p>

  <div class="" id="_the_old_chart">

    <div class="titlepage">

      <div>

        <h3 class="title">The Old Chart</h3>


      </div>

    </div>

<p id="see_the_div_cha">See the <code class="literal">div</code> chart, updated with some new data, in <span class="emphasis"><em>12_making_a_bar_chart_divs.html</em></span>:</p>
<p class="it">Vea la tabla div, actualizada con nuevos datos, en el código 12_making_a_bar_chart_divs.html:</p>
<pre class="programlisting" data-language="javascript" id="var_dataset___id11">var dataset = [ 5, 10, 13, 19, 21, 25, 22, 18, 15, 13,
                11, 12, 15, 20, 18, 17, 16, 18, 23, 25 ];

d3.select("body").selectAll("div")
    .data(dataset)
    .enter()
    .append("div")
    .attr("class", "bar")
    .style("height", function(d) {
        var barHeight = d * 5;
        return barHeight + "px";
    });</pre>

<p id="it_might_be_har">It might be hard to imagine, but we can definitely improve on the simple bar chart in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch06.html#Bar_chart_with_divs" title="Figure 6-13. Bar chart with divs">Figure 6-13</a> made of <code class="literal">div</code>s.</p>
<p class="it">Puede ser que sea difícil de imaginar, pero sin duda puede mejorar el simple gráfico de barras hecho de divs en la figura 6-13.</p>

    <div class="figure" id="Bar_chart_with_divs">

      <div class="figure-contents">

        <div class="mediaobject">

<img alt="Imagen" src="/static/Fig613.png" />

        </div>

      </div>

<p class="p">Figure 6-13. Bar chart with <code class="literal">div</code>s</p>

    </div>

  </div>

  <div class="" id="_the_new_chart">

    <div class="titlepage">

      <div>

        <h3 class="title">The New Chart</h3>



      </div>

    </div>

    <p id="first_we_need__id2">First, we need to decide on the size of the new SVG:</p>

<p class="it">En primer lugar, tenemos que decidir sobre el tamaño del nuevo SVG:</p>
    <pre class="programlisting" data-language="javascript" id="width_and_hei_id2">//Width and height
var w = 500;
var h = 100;</pre>

    <p id="of_course_you__id3">Of course, you could name <code class="literal">w</code> and <code class="literal">h</code> something else, like <code class="literal">svgWidth</code> and <code class="literal">svgHeight</code>. Use whatever is most clear to you. JavaScript programmers, as a group, are fixated on efficiency, so you’ll often see single-character variable names, code written with no spaces, and other hard-to-read, yet programmatically efficient, syntax.</p>
<p class="it">Por supuesto, usted podría nombrar a <stroke>w</stroke> y <stroke>h</stroke> de otra manera, como <stroke>svgWidth</stroke> y <stroke>svgHeight</stroke>. Use lo que sea más claro para usted. Los programadores de JavaScript, tienen una fijación en la eficiencia, por lo que usan a menudo un solo carácter para los nombres de las variables, código escrito sin espacios, y otros difíciles de leer, sin embargo, la sintaxis hace eficiente a la programación.</p>

    <p id="then_we_tell_d">Then, we tell D3 to create an empty SVG element and add it to the DOM:</p>
<p class="it">A continuación, le decimos a D3 que cree un elemento SVG vacío y lo añada al DOM:</p>



    <pre class="programlisting" data-language="javascript" id="create_svg_el_id1">//Create SVG element
var svg = d3.select("body")
            .append("svg")
            .attr("width", w)
            .attr("height", h);</pre>

    <p id="to_recap_this_">To recap, this inserts a new <code class="literal">&lt;svg&gt;</code> element just before the closing <code class="literal">&lt;/body&gt;</code> tag, and assigns the SVG a width and height of 500 by 100 pixels. This statement also puts the result into our new variable called <code class="literal">svg</code>, so we can easily reference the new SVG without having to reselect it later using something like <code class="literal">d3.select("svg")</code>.</p>

<p class="it">En resumen, esto introduce un nuevo elemento <code class="literal">svg</code> justo antes de la etiqueta de cierre <code class="literal">/ body</code>, y asigna al SVG una anchura y una altura de 500 por 100 píxeles. Este comunica el resultado en nuestra nueva variable llamada SVG, por lo que puede hacer fácilmente una referencia al nuevo SVG sin tener que volver a seleccionarlo más adelante con algo así como <code class="literal">d3.select("svg")</code>.</p>
    <p id="next_instead_o">Next, instead of creating <code class="literal">div</code>s, we generate <code class="literal">rect</code>s and add them to <code class="literal">svg</code>:</p>

      <p class="it">A continuación, en lugar de crear <code class="literal">div</code>s, generamos <code class="literal">rect</code>s y los añadimos a <code class="literal">svg</code>:</p>
    <pre class="programlisting" data-language="javascript" id="svgselectall_id2">svg.selectAll("rect")
   .data(dataset)
   .enter()
   .append("rect")
   .attr("x", 0)
   .attr("y", 0)
   .attr("width", 20)
   .attr("height", 100);</pre>

    <p id="this_code_selec">This code selects all <code class="literal">rect</code>s inside of <code class="literal">svg</code>. Of course, there aren’t any yet, so an empty selection is returned. (Weird, yes, but stay with me. With D3, you always have to first select whatever it is you’re about to act on, even if that selection is momentarily empty.)</p>
<p class="it">Este código selecciona todos los rects al interior de SVG. Por supuesto, todavía no hay ninguno, por lo que devuelve una selección vacía. (Extraño, sí, pero quedese conmigo. Con D3, siempre hay que seleccionar en primer lugar lo que sea que está a punto de actuar, incluso si esa selección está momentáneamente vacía.)</p>

    <p id="then_datadata">Then, <code class="literal">data(dataset)</code> sees that we have 20 values in the dataset, and those values are handed off to for processing. <code class="literal">enter()</code>, in turn, returns a placeholder selection for each data point that does <code class="literal">enter()</code> not yet have a corresponding <code class="literal">rect</code>—which is to say, all of them.</p>

<p class="it">A continuación, <code class="literal">data(dataset)</code> ve que tenemos 20 valores del conjunto de datos, y esos valores son entregados fuera por <code class="literal">enter()</code>  para su procesamiento. <code class="literal">enter()</code> , a su vez, devuelve una selección de marcadores de posición para cada punto de datos que aún no cuenta con un rect correspondiente - es decir, todos ellos.</p>

    <p id="for_each_of_the">For each of the 20 placeholders, <code class="literal">append("rect")</code> inserts a <code class="literal">rect</code> into the DOM. As we learned in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch03.html" title="Chapter 3. Technology Fundamentals">Chapter 3</a>, every <code class="literal">rect</code> must have <code class="literal">x</code>, <code class="literal">y</code>, <code class="literal">width</code>, and <code class="literal">height</code> values. We use <code class="literal">attr()</code> to add those attributes onto each newly created <code class="literal">rect</code>.</p>

<p class="it">Para cada uno de los 20 marcadores de posición, append ( "rect") inserta un rect en el DOM. Como aprendimos en el capítulo 3, cada rect debe tener x, y, ancho, y los valores de altura. Utilizamos attr() para agregar estos atributos en cada rect recién creado.
    </p><p id="beautiful_no_">Beautiful, no? Okay, maybe not. All of the bars are there (check the DOM of <span class="emphasis"><em>13_making_a_bar_chart_rects.html</em></span> with your web inspector), but they all share the same <code class="literal">x</code>, <code class="literal">y</code>, <code class="literal">width</code>, and <code class="literal">height</code> values, with the result that they all overlap (see <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch06.html#One_lonely_bar" title="Figure 6-14. One lonely bar">Figure 6-14</a>). This isn’t a visualization of data yet.</p>
<p class="it">Hermoso, ¿no? De acuerdo, tal vez no. Todas las barras están allí (marque el DOM de 13_making_a_bar_chart_rects.html con su web a inspeccionar o), pero todos comparten las mismas propiedades x, y, ancho, y los valores de altura, con el resultado de que todos ellos se solapan (véase la Figura 6-14 ). Esto no es visualización de datos aún.</p>

    <div class="figure" id="One_lonely_bar">

      <div class="figure-contents">

        <div class="mediaobject">

<img alt="Imagen" src="/static/Fig614.png" />

        </div>

      </div>





      <p class="p">Figure 6-14. One lonely bar</p>
<p class="it">Figura 6-14. Una barra solitaria</p>

    </div>

    <p id="lets_fix_the_o">Let’s fix the overlap issue first. Instead of an <code class="literal">x</code> of <code class="literal">0</code>, we’ll assign a dynamic value that corresponds to <code class="literal">i</code>, or each value’s position in the dataset. So the first bar will be at <code class="literal">0</code>, but subsequent bars will be at <code class="literal">21</code>, then <code class="literal">42</code>, and so on. (In a later chapter, we’ll learn about D3’s <span class="emphasis"><em>scales</em></span>, which offer a better, more flexible way to accomplish this same feat.)</p>
<p class="it">Vamos a solucionar el solapamiento primero. En lugar de una <code class="literal">x</code> de <code class="literal">0</code>, vamos a asignar un valor dinámico que corresponde a <code class="literal">i</code>, o cada valor de la posición en el conjunto de datos. Así que la primera barra será a <code class="literal">0</code>, pero las barras posteriores serán la 21, luego 42, y así sucesivamente. (En un capítulo posterior, vamos a aprender sobre <strong>escalas</strong> en D3, que ofrecen una mejor manera, más flexible para lograr esta misma hazaña.)</p>
    <pre class="programlisting" data-language="javascript" id="attrx_func_id1">.attr("x", function(d, i) {
    return i * 21;  //Bar width of 20 plus 1 for padding. // Ancho de barra de 20 más 1 para relleno
})</pre>

    <p id="see_that_code_i_id2">See that code in action with <span class="emphasis"><em>14_making_a_bar_chart_offset.html</em></span> and the result in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch06.html#Twenty_bars" title="Figure 6-15. Twenty bars">Figure 6-15</a>.</p>

<p class="it">Vemos este código en acción en <span class="emphasis"><em>14_making_a_bar_chart_offset.html</em></span> y el resultado en la figura 6-15.</p>

    <div class="figure" id="Twenty_bars">

      <div class="figure-contents">

        <div class="mediaobject">

<img alt="Imagen" src="/static/Fig615.png" />

        </div>

      </div>

      <p class="p">Figure 6-15. Twenty bars</p>


    </div>

    <p id="that_works_but">That works, but it’s not particularly flexible. If our dataset were longer, then the bars would just run off to the right, past the end of the SVG! Because each bar is 20 pixels wide, plus 1 pixel of padding, a 500-pixel wide SVG can only accommodate 23 data points. Note how the 24th bar gets clipped in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch06.html#Twentyfour_bars" title="Figure 6-16. Twenty-four bars">Figure 6-16</a>.</p>
<p class="it">Esto funciona, pero no es especialmente flexible. Si nuestro conjunto de datos fuera más largo, a continuación, las barras simplemente correrían hacia la derecha, más allá del final de la SVG! Debido a que cada barra es de 20 píxeles de ancho, además de 1 píxel de relleno, una amplia SVG 500 píxeles sólo puede acomodar a 23 puntos de datos. Nótese cómo la barra 24 se recorta en la figura 6-16.</p>

    <div class="figure" id="Twentyfour_bars">

      <div class="figure-contents">

        <div class="mediaobject">

          <img src="/static/E9gUN3MUJz-img4.png" alt="Twenty-four bars"/>

        </div>

      </div>

      <p class="p">Figure 6-16. Twenty-four bars</p>


    </div>

    <p id="its_good_pract">It’s good practice to use flexible, dynamic coordinates—heights, widths, x values, and y values—so your visualization can scale appropriately along with your data.</p>
<p class="it">Es una buena práctica el hacerlas flexibles, coordinar dinámicamente los valores de -heights, widths, x e y para que su visualización puede escalarse adecuadamente junto con sus datos.</p>

    <p id="as_with_anythin">As with anything else in programming, there are a thousand ways to achieve that end. I’ll use a simple one. First, I’ll amend the line where we set each bar’s <code class="literal">x</code> position:</p>
<p class="it">Al igual que con cualquier otra cosa en la programación, hay mil maneras de lograr ese fin. Voy a utilizar una sencilla. En primer lugar, voy a modificar la línea donde se parte cada barra en la posición <strong>x</strong>:</p>

    <pre class="programlisting" data-language="javascript" id="attrx_func_id2">.attr("x", function(d, i) {
    return i * (w / dataset.length);
})</pre>

    <p id="notice_how_the__id3">Notice how the <code class="literal">x</code> value is now tied directly to the width of the SVG (<code class="literal">w</code>) and the number of values in the dataset (<code class="literal">dataset.length</code>). This is exciting because now our bars will be evenly spaced, whether we have 20 data values, as in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch06.html#Twenty_evenly_spaced_bars" title="Figure 6-17. Twenty evenly spaced bars">Figure 6-17</a>.</p>
<p class="it">Nótese cómo el valor de <code class="literal">x</code> está ligado directamente a la anchura de la <code>SVG (w)</code> y al número de valores en el conjunto de datos (<code class="literal">dataset.length</code>). Esto es emocionante porque ahora se espacian uniformemente nuestras bars, si tenemos 20 valores de datos, como en la figura 6-17.</p>

    <div class="figure" id="Twenty_evenly_spaced_bars">

      <div class="figure-contents">

        <div class="mediaobject">

          <img src="/static/E9gUN3MUJz-img5.png" alt="Twenty evenly spaced bars"/>

        </div>

      </div>

      <p class="p">Figure 6-17. Twenty evenly spaced bars</p>
      <p class="it">Figura 6-17. Veinte barras espaciadas uniformemente</p>

    </div>

    <p id="or_only_five_a">Or only five, as in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch06.html#Five_evenly_spaced_bars" title="Figure 6-18. Five evenly spaced bars">Figure 6-18</a>.</p>
    <div class="figure" id="Five_evenly_spaced_bars">

      <div class="figure-contents">

        <div class="mediaobject">

          <img src="/static/E9gUN3MUJz-img6.png" alt="Five evenly spaced bars"/>

        </div>

      </div>

      <p class="p">Figure 6-18. Five evenly spaced bars</p>

    </div>

    <p id="see_that_code_s">See that code so far in <span class="emphasis"><em>15_making_a_bar_chart_even.html</em></span>.</p>


    <p id="now_we_should_s">Now we should set the bar <span class="emphasis"><em>widths</em></span> to be proportional, too, so they get narrower as more data is added, or wider when there are fewer values. I’ll add a new variable near where we set the SVG’s width and height:</p>
<p class="it">Ahora debemos setear los anchos de las barras, también de forma proporcional, así se estrechan a medida que se agregan más datos, o se ensanchan cuando hay menos valores. Voy a añadir una nueva variable junto a donde fijamos el ancho y la altura del SVG:</p>

    <pre class="programlisting" data-language="javascript" id="width_and_hei_id3">//Width and height
var w = 500;
var h = 100;
var barPadding = 1;  // &lt;-- New!</pre>


    <p id="and_then_refere">and then reference that variable in the line where we set each bar’s <code class="literal">width</code>. Instead of a static value of <code class="literal">20</code>, the width will now be set as a fraction of the SVG width and number of data points, minus a padding value:</p>
<p class="it">y después hacemos referencia a esa variable en la línea donde se parte el ancho de cada barra. En lugar de un valor estático de 20, la anchura se definirá como una fracción de la anchura SVG y el número de puntos de datos, menos uno el valor de relleno (padding value):</p>

    <pre class="programlisting" data-language="javascript" id="attrwidth__id1">.attr("width", w / dataset.length - barPadding)</pre>

    <p id="it_works_see_">It works! (See <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch06.html#Twenty_evenly_spaced_bars_with_dynamic_widths" title="Figure 6-19. Twenty evenly spaced bars with dynamic widths">Figure 6-19</a> and <span class="emphasis"><em>16_making_a_bar_chart_widths.html</em></span>.)</p>

    <div class="figure" id="Twenty_evenly_spaced_bars_with_dynamic_widths">

      <div class="figure-contents">

        <div class="mediaobject">

          <img src="/static/E9gUN3MUJz-img7.png" alt="Twenty evenly spaced bars with dynamic widths"/>

        </div>

      </div>

      <p class="p">Figure 6-19. Twenty evenly spaced bars with dynamic widths</p>

    </div>

    <p id="the_bar_widths">The bar widths and x positions scale correctly whether there are 20 points, only 5 (see <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch06.html#Five_evenly_spaced_bars_with_dynamic_widths" title="Figure 6-20. Five evenly spaced bars with dynamic widths">Figure 6-20</a>), or even 100 (see <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch06.html#One_hundred_evenly_spaced_bars_with_dynamic_widths" title="Figure 6-21. One hundred evenly spaced bars with dynamic widths">Figure 6-21</a>).</p>
<p class="it">Los anchos de las barras y las posiciones <strong>x</strong> escalan correctamente si existen 20 puntos, solamente  5 (ver Figura 6-20), o incluso 100 (véase la figura 6-21).</p>

    <div class="figure" id="Five_evenly_spaced_bars_with_dynamic_widths">

      <div class="figure-contents">

        <div class="mediaobject">

          <img src="/static/E9gUN3MUJz-img8.png" alt="Five evenly spaced bars with dynamic widths"/>

        </div>

      </div>

      <p class="p">Figure 6-20. Five evenly spaced bars with dynamic widths</p>

    </div>

    <div class="figure" id="One_hundred_evenly_spaced_bars_with_dynamic_widths">

      <div class="figure-contents">

        <div class="mediaobject">

          <img src="/static/E9gUN3MUJz-img9.png" alt="One hundred evenly spaced bars with dynamic widths"/>

        </div>

      </div>

      <p class="p">Figure 6-21. One hundred evenly spaced bars with dynamic widths</p>
      <p class="it">Figura 6-21. Cien barras espaciadas uniformemente con anchos dinámicos</p>

    </div>

    <p id="finally_we_enc">Finally, we encode our data as the <span class="emphasis"><em>height</em></span> of each bar. You would hope it were as easy as referencing the <code class="literal">d</code> data value when setting each bar’s <code class="literal">height</code>:</p>
<p class="it">Finalmente, codificamos nuestros datos como la altura de cada barra.
  Uno esperaría que fuera tan fácil como referenciar el valor <code class="literal">d</code> de datos al establecer la <code class="literal">height</code> de cada barra:</p>

    <pre class="programlisting" data-language="javascript" id="attrheight_id1">.attr("height", function(d) {
    return d;
});</pre>

    <p id="hmm_the_chart_">Hmm, the chart in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch06.html#Dynamic_heights" title="Figure 6-22. Dynamic heights">Figure 6-22</a> looks funky. Maybe we can just scale up our numbers a bit?</p>

    <pre class="programlisting" data-language="javascript" id="attrheight_id2">.attr("height", function(d) {
    return d * 4;  // &lt;-- Times four!
});</pre>

    <div class="figure" id="Dynamic_heights">

      <div class="figure-contents">

        <div class="mediaobject">

          <img src="/static/E9gUN3MUJz-img10.png" alt="Dynamic heights"/>

        </div>

      </div>

      <p class="p">Figure 6-22. Dynamic heights</p>
</div>
    <p id="alas_it_is_not">Alas, it is not that easy! We want our bars to grow upward from the bottom edge, not down from the top, as in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch06.html#Dynamic_heights_magnified" title="Figure 6-23. Dynamic heights, magnified">Figure 6-23</a>—but don’t blame D3, blame SVG.</p>

<p class="it">Por desgracia, no es así de fácil! Queremos que nuestras barras crezcan hacia arriba desde el borde inferior, no hacia abajo desde la parte superior, como en la figura 6-23 - pero no es culpa de D3, es culpa de SVG.
    </p><div class="figure" id="Dynamic_heights_magnified">

      <div class="figure-contents">

<img alt="Imagen" src="/static/Fig623.png" />

      </div>

      <p class="p">Figure 6-23. Dynamic heights, magnified</p>
<p class="it">Figura 6-23. Alturas dinámicas, magnificada</p>

    </div>

    <p id="youll_recall_t_id1">You’ll recall that, when drawing SVG <code class="literal">rect</code>s, the <code class="literal">x</code> and <code class="literal">y</code> values specify the coordinates of the <span class="emphasis"><em>upper-left corner</em></span>. That is, the origin or reference point for every <code class="literal">rect</code> is its top-left. For our purposes, it would be soooooo much easier to set the origin point as the bottom-left corner, but that’s just not how SVG does it, and frankly, SVG is pretty indifferent about our feelings on the matter.</p>
<p class="it">Se recordará que, al elaborar valores SVG <code class="literal">rect</code>s, <code class="literal">x</code> e <code class="literal">y</code> se especifican las coordenadas de la esquina superior izquierda. Es decir, el punto de origen o de referencia para cada <code class="literal">rect</code> es su esquina superior izquierda. Para nuestros propósitos, que sería taaaaaaaaaaaaaaaan fácil establecer el punto de origen en la esquina inferior izquierda, pero esa no es la forma en que SVG lo hace, y francamente, SVG es bastante indiferente con respecto a nuestros sentimientos sobre el asunto.

    </p><p id="given_that_our_">Given that our bars do have to “grow down from the top,” then where is “the top” of each bar in relationship to the top of the SVG? Well, the top of each bar could be <span class="keep-together">expressed</span> as a relationship between the height of the SVG and the corresponding data value, as in:</p>

<p class="it">Dado que nuestras barras tienen que "crecer hacia abajo desde la parte superior," ¿dónde está "encima" de cada barra en relación a la parte superior de la SVG? Pues bien, la parte superior de cada barra se podría expresar como una relación entre la altura de la SVG y el valor de datos correspondiente, como en:
    </p><pre class="programlisting" data-language="javascript" id="attry_func_id1">.attr("y", function(d) {
    return h - d;  //Height minus data value. Altura menos valor de datos
})</pre>

    <p id="then_to_put_th">Then, to put the “bottom” of the bar on the bottom of the SVG (see <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch06.html#Growing_down_from_above" title="Figure 6-24. Growing down from above">Figure 6-24</a>), each <code class="literal">rect</code>’s height can be just the data value itself:</p>
<p class="it">A continuación, poner el "bottom" de la barra en la parte inferior de la SVG (ver Figura 6-24) la altura de cada rect puede ser sólo el valor de los datos en sí:

    </p><pre class="programlisting" data-language="javascript" id="attrheight_id3">.attr("height", function(d) {
    return d;  //Just the data value. Sólo el valor de los datos
});</pre>

    <div class="figure" id="Growing_down_from_above">

      <div class="figure-contents">

<img alt="Imagen" src="/static/Fig624.png" />

      </div>

      <p class="p">Figure 6-24. Growing down from above</p>
<p class="it">Figura 6-24. Creciente desde arriba

    </p></div>

    <p id="lets_scale_thi">Let’s scale things up a bit by changing <code class="literal">d</code> to <code class="literal">d * 4</code>, with the result shown in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch06.html#Growing_bigger_from_above" title="Figure 6-25. Growing bigger from above">Figure 6-25</a>. (Just as with the bar placements, this can be done more properly using D3 scales, but we’re not there yet.)</p>

<p class="it">Escalemos un poco cambiando <strong>d</strong> a <strong>d * 4</strong>, con el resultado que se muestra en la Figura 6-25. (Al igual que con las colocaciones de barras, esto se puede hacer más adecuadamente mediante escalas D3, pero no llegamos allí todavía.)</p>
    <div class="figure" id="Growing_bigger_from_above">

      <div class="figure-contents">

<img alt="Imagen" src="static/Fig625.png" />

      </div>

      <p class="p">Figure 6-25. Growing bigger from above</p>
<p class="it">Figura 6-25. Cada vez más grande hacía lo alto</p>

    </div>

    <p id="the_working_cod">The working code for our growing-down-from-above, SVG bar chart is in <span class="emphasis"><em>17_making_a_bar_chart_heights.html</em></span>.</p>
<p class="it">El código de trabajo para nuestro crecimiento del gráfico de barras SVG hacia abajo desde arriba está en <span class="emphasis"><em>17_making_a_bar_chart_heights.html.</em></span></p>

<h3>Color</h3>

<p class="p">Adding color is easy. Just use attr() to set a fill:</p>
<pre class="programlisting" data-language="javascript" id="transition_id123">
.attr("fill", "teal");</pre>
<p class="p">Find the all-teal bar chart shown in Figure 6-26 in 18_making_a_bar_chart_teal.html.</p>

<h3>Teal bars</h3>
<img alt="Imagen" src="static/Fig626.png" />
<p class="p">Figure 6-26. Teal bars</p>
<p class="p">Teal is nice, but you’ll often want a shape’s color to reflect some quality of the data. That is, you might want to encode the data values as color. (In the case of our bar chart, that makes a dual encoding, in which the same data value is encoded in two different visual properties: both height and color.)</p>
<p class="it">El color teal es agradable, pero a menudo querrá que el color de una forma refleje una cierta cualidad de los datos. Es decir, es posible que desee codificar los valores de datos como color. (En el caso de nuestro gráfico de barras, hace una codificación dual, en el que el mismo valor de los datos se codifica en dos diferentes propiedades visuales: la altura y el color.)</p>

<p class="p">Using data to drive color is as easy as writing a custom function that again references d. Here, we replace "teal" with a custom function, resulting in the chart in Figure 6-27:</p>
<p class="it">El uso de datos para manejar el color es tan fácil como escribir una función personalizada que hace referencia a <strong>d</strong>. Aquí, reemplazamos "teal" por una función personalizada, resultando en el gráfico de la Figura 6-27:</p>
<pre class="programlisting" data-language="javascript" id="transition_id121">
.attr("fill", function(d) {
    return "rgb(0, 0, " + (d * 10) + ")";
});</pre>
<img alt="Imagen" src="static/Fig627.png" />
<p class="p">Figure 6-27. Data-driven blue bars</p>
<p class="p">See the code in 19_making_a_bar_chart_blues.html. This is not a particularly useful visual encoding, but you can get the idea of how to translate data into color. Here, d is multiplied by 10, and then used as the blue value in an rgb() color definition. So the greater values of<code class="literal">d</code>(taller bars) will be more blue. Smaller values of<code class="literal">d</code>(shorter bars) will be less blue (closer to black). The red and green components of the color are fixed at zero.</p>
<p class="it">Vea el código en 19_making_a_bar_chart_blues.html. Esto no es una codificación visual particularmente útil, pero puede obtener la idea de cómo traducir los datos en color. Aquí, <strong>d</strong> se multiplica por 10, y luego se utiliza como valor del azul en una definición de color rgb(). Así que los valores mayores de <strong>d</strong> (barras más altas) serán más azules. Los valores más pequeños de <strong>d</strong> (barras más cortas) serán menos azules (más cerca del negro). Los componentes rojo y verde del color se fijan en cero.</p>
<div class="sect33">
<h3>Multivalue Maps</h3>
<p class="p">You might have noticed we now have a total of five different calls to attr() in the chain, one each to specify the bars’ x, y, width, height, and fill values.</p>
<p class="it">Es posible que haya notado que ahora tenemos un total de cinco llamadas diferentes a attr() en la cadena, una para especificar los valores x, y, width, height y fill de las barras.</p>
<p class="p">If you get tired of typing attr() over and over again, you might appreciate D3’s support for multivalue maps, with which you can set multiple attribute values using a single attr() statement. For example, to move a circle to the top-left corner of the SVG and make it red, I could use separate attr() statements:</p>
<p class="it">Si se cansa de escribir attr() una y otra vez, apreciará la compatibilidad de D3 con mapas multivalores, con los cuales puedes establecer múltiples valores de atributos usando una única sentencia attr(). Por ejemplo, para mover un círculo a la esquina superior izquierda del SVG y hacerlo rojo, podría usar declaraciones separadas attr():</p>
<pre class="programlisting" data-language="javascript" id="transition_id122">
svg.select("circle")
   .attr("cx", 0)
   .attr("cy", 0)
   .attr("fill", "red");</pre>
<p class="p">or I could define all three of these attributes and their values within a single object, which is then relayed to a single attr() statement:</p>
<p class="it">O podría definir tres de estos atributos y sus valores dentro de un solo objeto, que es entonces retransmitido a una sola instrucción attr():</p>
<pre class="programlisting" data-language="javascript" id="transition_id125">
svg.select("circle")
   .attr({
        cx: 0,
        cy: 0,
        fill: red
   });</pre>
<p class="p">The resulting code is more concise, and if you’ve used jQuery, this syntax of tucking property/value pairs into objects might already be familiar. The value portion of each pair can include anonymous functions, referencing<code class="literal">d</code>and i to generate dynamic values, per usual. We could rewrite our bar-creation code thus far using multivalue maps as:</p>
<p class="it">El código resultante es más conciso, y si ha utilizado jQuery, esta sintaxis de agrupar pares de propiedad/valor en objetos podría serle familiar. La parte de valor de cada par puede incluir funciones anónimas, haciendo referencia a <strong>d</strong> e <strong>i</strong> para generar valores dinámicos, por habituales. Podríamos reescribir nuestro código de creación de barras hasta ahora usando mapas multivalores como:</p>
<pre class="programlisting" data-language="javascript" id="transition_id12080">
svg.selectAll("rect")
   .data(dataset)
   .enter()
   .append("rect")
   .attr({
        x: function(d, i) { return i * (w / dataset.length); },
        y: function(d) { return h - (d * 4); },
        width: w / dataset.length - barPadding,
        height: function(d) { return d * 4; },
        fill: function(d) { return "rgb(0, 0, " + (d * 10) + ")"; }
   });</pre>
<p class="p">If you like this sort of thing, you’ll be happy to know it also works with style() and a few other methods. Throughout this book, I’ve used the more verbose structure of individual attribute statements, but it’s always good to know you have options.</p>
<p class="it">Si te gustan este tipo de cosas, estarás feliz de saber que también funciona con style() y algunos otros métodos. A lo largo de este libro, he utilizado la estructura más detallada de declaraciones de atributos individuales, pero siempre es bueno saber que tiene opciones.</p>

  <div class="" data-key="README.md">
  <h3>Multivalue Maps Mike Bostock</h3><p class="p">D3 2.10.0 adds support for multi-value maps. Where previously you might have written:</p>
<p class="it">D3 2.10.0 agrega soporte para multi-value maps. Donde anteriormente usted podría haber escrito:</p>
<pre>svg.attr("width", width).attr("height", height);
</pre><p class="p">You can now write:</p><pre>svg.attr({width: width, height: height});
</pre><p class="p">The new syntax (familiar to jQuery users) is slightly more concise. Like other methods in D3, the values in the maps can be specified as constants or functions of data. Multi-value maps also provide a convenient, declarative way to share code. For example, if you have the following map:</p>
<p class="it">La nueva sintaxis (familiar para los usuarios de jQuery) es ligeramente más concisa. Al igual que otros métodos en D3, los multi-value maps se pueden especificar como constantes o funciones de datos. Los multi-value maps también proporcionan una manera conveniente y declarativa de compartir código. Por ejemplo, si tiene el siguiente mapa:</p>
<pre>var dotAttrs = {
  cx: function() { return Math.random() * width; },
  cy: function() { return Math.random() * height; },
  r: function() { return 100 + Math.random() * 100; }
};
</pre><p class="p">You can later reference this map like so:</p><pre>circle.attr(dotAttrs);
</pre><p class="p">This technique is similar to creating reusable functions with <a href="https://github.com/mbostock/d3/wiki/Selections#wiki-call">selection.call</a>.</p><p class="p">Multi-value maps are supported on the following methods: <a href="https://github.com/mbostock/d3/wiki/Selections#wiki-attr">selection.attr</a>, <a href="https://github.com/mbostock/d3/wiki/Selections#wiki-style">selection.style</a>, <a href="https://github.com/mbostock/d3/wiki/Selections#wiki-classed">selection.classed</a>, <a href="https://github.com/mbostock/d3/wiki/Selections#wiki-property">selection.property</a>, <a href="https://github.com/mbostock/d3/wiki/Selections#wiki-on">selection.on</a>, <a href="https://github.com/mbostock/d3/wiki/Transitions#wiki-attr">transition.attr</a> and <a href="https://github.com/mbostock/d3/wiki/Transitions#wiki-style">transition.style</a>.</p></div><div class=""> <div class="gist-source" data-key="index.html"> <h3>index.html<a name="index.html" class="anchor" href="http://bl.ocks.org/mbostock/3305515#index.html">#</a></h3> <pre>&lt;!DOCTYPE html&gt;
&lt;meta charset="utf-8"&gt;
&lt;style&gt;

circle {
  fill-opacity: .1;
  stroke: #000;
}

&lt;/style&gt;
&lt;body&gt;
&lt;script src="//d3js.org/d3.v3.min.js"&gt;&lt;/script&gt;
&lt;script&gt;

var width = 960,
    height = 500;

// Setting two constant attributes.
var svg = d3.select("body").append("svg")
    .attr({width: width, height: height});

// Setting three attributes as functions of data.
svg.selectAll("circle")
    .data(d3.range(10))
  .enter().append("circle")
    .attr({
      cx: function() { return Math.random() * width; },
      cy: function() { return Math.random() * height; },
      r: function() { return 100 + Math.random() * 100; }
    });

// Setting attributes and styles.
svg.append("text")
    .attr({x: width / 2, y: height / 2, dy: ".35em"})
    .style({"text-anchor": "middle"})
    .text("Hello, multi-value maps!");

&lt;/script&gt;
</pre> </div> </div>



<p class="p">This module adds multi-value syntax to selections and transitions, allowing you to set multiple attributes, styles or properties simultaneously with more concise syntax. For example:</p>
<p class="it">Este módulo añade la sintaxis multi-value maps a selecciones y transiciones , que le permite establecer múltiples atributos, propiedades o estilos simultáneamente con una sintaxis más concisa. Por ejemplo:</p>
<pre class="programlisting" data-language="javascript" id="transition_id12081">
d3.select("body").append("div")
    .attrs({
      title: "A cheery, timeless greeting.",
      class: "greeting"
    })
    .text("Hello, world!");</pre>
<p class="p">This is equivalent to:</p>
<p class="it"></p>
<pre class="programlisting" data-language="javascript" id="transition_id12082">
d3.select("body").append("div")
    .attr("title", "A cheery, timeless greeting.")
    .attr("class", "greeting")
    .text("Hello, world!");</pre>
<p class="p">Like selection.attr, the values in the multi-value object can be functions of data:</p>
<p class="it">Al igual que la selección .attr , los valores del objeto de valor múltiple pueden ser funciones de los datos:</p>
<pre class="programlisting" data-language="javascript" id="transition_id12083">
d3.select("body").append("div")
    .attrs({
      title: function(d) { return d.title; },
      id: function(d, i) { return "id-" + i; },
    });</pre>
<p class="p">Alternatively, you can pass a function which returns an object, allowing you to share some computational effort across multiple attributes, or to determine which attribute to set dynamically:</p>
<p class="it">Como alternativa, puede pasar una función que devuelve un objeto, que le permite compartir un poco de esfuerzo computacional a través de múltiples atributos, o para determinar qué atributo configurar dinámicamente:</p>
<pre class="programlisting" data-language="javascript" id="transition_id12084">
d3.select("body").append("div")
    .attrs(function(d, i) { return {title: d.title, id: "id-" + i}; });</pre>
<p class="p">This module is not included in the default D3 bundle for parsimony’s sake: the single-value methods such as selection.attr are recommended for most users, as there is little benefit to the shorter syntax provided by these convenience method.</p>
<p class="it">Este módulo no está incluido en el paquete predeterminado de D3 por el bien de la parsimonia: los métodos de un solo valor, tales como la selección .attr se recomiendan para la mayoría de los usuarios, ya que hay poco beneficio con la sintaxis más corta proporcionada por estos métodos de conveniencia.</p>

<h2>Installing</h2>

<p class="p">If you use NPM, npm install d3-selection-multi. Otherwise, download the latest release or load directly from d3js.org as a standalone library. AMD, CommonJS, and vanilla environments are supported. In vanilla, a d3 global is exported:</p>
<p class="it">Si utiliza la NGP, npm install d3-selection-multi. De lo contrario, descargar la última versión o cargar directamente desde d3js.org como una biblioteca independiente . AMD, CommonJS y entornos de vainilla son compatibles. En la vainilla, un d3 global es exportado:</p>
<pre class="programlisting" data-language="javascript" id="transition_id12085">
&lt;script src="https://d3js.org/d3-color.v1.min.js"&gt;&lt;/script&gt;
&lt;script src="https://d3js.org/d3-dispatch.v1.min.js"&gt;&lt;/script&gt;
&lt;script src="https://d3js.org/d3-ease.v1.min.js"&gt;&lt;/script&gt;
&lt;script src="https://d3js.org/d3-interpolate.v1.min.js"&gt;&lt;/script&gt;
&lt;script src="https://d3js.org/d3-selection.v1.min.js"&gt;&lt;/script&gt;
&lt;script src="https://d3js.org/d3-timer.v1.min.js"&gt;&lt;/script&gt;
&lt;script src="https://d3js.org/d3-transition.v1.min.js"&gt;&lt;/script&gt;
&lt;script src="https://d3js.org/d3-selection-multi.v1.min.js"&gt;&lt;/script&gt;
&lt;script&gt;

var div = d3.selectAll("div")
    .attrs({title: "Hello, world!"})
    .styles({"color": "red"});

&lt;/script&gt;
</pre>
<p class="p">Or, in combination with the D3 default bundle:</p>
<pre class="programlisting" data-language="javascript" id="transition_id10120">
&lt;script src="https://d3js.org/d3.v4.min.js"&gt;&lt;/script&gt;
&lt;script src="https://d3js.org/d3-selection-multi.v1.min.js"&gt;&lt;/script&gt;
&lt;script&gt;


var div = d3.selectAll("div")
    .attrs({title: "Hello, world!"})
    .styles({"color": "red"});

&lt;/script&gt;&lt;/pre&gt;
&lt;/script&gt;</pre>
<h3>Try d3-selection-multi in your browser.</h3>

<h2>API Reference</h2>

<h3># selection.attrs(values)</h3>

<p class="p">A convenience method on top of selection.attr for setting multiple attributes. If the specified values is an object, the values may be specified either as strings or functions. For example:</p>
<p class="it">Un método conveniente en la parte superior de la selección .attr para configurar varios atributos. Si los valores especificados son un objeto, los valores pueden ser especificados ya sea en forma de cadenas o funciones. Por ejemplo:</p>
<pre class="programlisting" data-language="javascript" id="transition_id1120">
selection.attrs({foo: "foo-value", bar: function(d) { return d.bar; }});</pre>
<p class="p">If a value is a constant, all elements are given the same attribute value; otherwise, if a value is a function, the function is evaluated for each selected element, in order, being passed the current datum (d), the current index (i), and the current group (nodes), with this as the current DOM element. The function’s return value is then used to set each element’s attribute. A null value will remove the specified attribute.</p>
<p class="it">Si un valor es una constante, a todos los elementos se les da el mismo valor de atributo; de lo contrario, si un valor es una función, la función se evalúa para cada elemento seleccionado, en orden, habiendo pasado el punto de referencia actual ( d ), el índice actual ( i ), y el grupo actual ( nodos ), con este como el actual elemento DOM. El valor devuelto por la función se utiliza para establecer el atributo de cada elemento. Un valor nulo eliminará el atributo especificado.</p>
<p class="p">If the specified values is a function, the function is evaluated for each selected element, in order, being passed the current datum (d), the current index (i), and the current group (nodes), with this as the current DOM element. The function’s return value must be an object with string values, which are then used to set attributes on the current element. For example:</p>
<p class="it">Si los valores especificados son una función, la función se evalúa para cada elemento seleccionado, con el fin, que se pasa el punto de referencia actual ( d ), el índice actual ( i ), y el grupo actual ( nodos ), con esto como el DOM actual del elemento. El valor devuelto por la función debe ser un objeto con valores de cadena, que luego se utilizan para establecer los atributos en el elemento actual. Por ejemplo:</p>
<pre class="programlisting" data-language="javascript" id="transition_id2120">selection.attrs(function(d) { return {foo: "foo-value", bar: d.bar}; });</pre>
<p class="p">Passing a function to selection.attrs is convenient for sharing some computational effort or state across multiple attributes, or for specifying dynamically which attributes to set.</p>
<p class="it">Al pasar de una función a la selección .attrs es conveniente para compartir un poco de esfuerzo computacional o estado a través de múltiples atributos, o para especificar dinámicamente los atributos que desea establecer.</p>
<h3># selection.styles(values[, priority])</h3>

<p class="p">A convenience method on top of selection.style for setting multiple style properties. If the specified values is an object, the values may be specified either as strings or functions. For example:</p>
<p class="it">Un método de conveniencia en la parte superior de la selección .style para establecer múltiples propiedades de estilo. Si los especificados valores es un objeto, los valores pueden ser especificados ya sea en forma de cadenas o funciones. Por ejemplo:</p>
<pre class="programlisting" data-language="javascript" id="transition_id3120">selection.styles({fill: "red", stroke: function(d) { return d.stroke; }});</pre>
<p class="p">If a value is a constant, all elements are given the same style property value; otherwise, if a value is a function, the function is evaluated for each selected element, in order, being passed the current datum (d), the current index (i), and the current group (nodes), with this as the current DOM element. The function’s return value is then used to set each element’s style properties. A null value will remove the specified style properties.</p>
<p class="it">Si un valor es una constante, todos los elementos se les da el valor de la propiedad mismo estilo; de lo contrario, si un valor es una función, la función se evalúa para cada elemento seleccionado, en orden, siendo pasado el punto de referencia actual ( d ), el índice actual ( i ), y el grupo actual ( nodos ), con este como el actual elemento DOM. El valor devuelto por la función se utiliza para definir propiedades de estilo de cada elemento. Un valor nulo eliminará las propiedades de estilo especificadas.</p>
<p class="p">If the specified values is a function, the function is evaluated for each selected element, in order, being passed the current datum (d), the current index (i), and the current group (nodes), with this as the current DOM element. The function’s return value must be an object with string values, which are then used to set style properties on the current element. For example:</p>
<p class="it">Si los especificados valores es una función, la función se evalúa para cada elemento seleccionado, con el fin, que se pasa el punto de referencia actual ( d ), el índice actual ( i ), y el grupo actual ( nodos ), con esto como el actual del DOM elemento. El valor devuelto por la función debe ser un objeto con valores de cadena, que luego se utilizan para definir propiedades de estilo sobre el elemento actual. Por ejemplo:</p>
<pre class="programlisting" data-language="javascript" id="transition_id12086">selection.styles(function(d) { return {fill: "red", stroke: d.stroke}; });</pre>
<p class="p">Passing a function to selection.styles is convenient for sharing some computational effort or state across multiple style properties, or for specifying dynamically which style properties to set.</p>
<p class="it">Al pasar de una función a la selección .styles es conveniente para compartir un poco de esfuerzo computacional o estado a través de múltiples propiedades de estilo, o para especificar dinámicamente que las propiedades de estilo que deben establecerse.</p>
<h3># selection.properties(values)</h3>

<p class="p">A convenience method on top of selection.property for setting multiple element properties. If the specified values is an object, the values may be specified either as strings or functions. For example:</p>
<p class="it">Un método de conveniencia en la parte superior de la selección .property para establecer múltiples propiedades de los elementos. Si los especificados valores es un objeto, los valores pueden ser especificados ya sea en forma de cadenas o funciones. Por ejemplo:</p>
<pre class="programlisting" data-language="javascript" id="transition_id12087">selection.properties({foo: "foo-value", id: function(d, i) { return "id-" + i; }});</pre>
<p class="p">If a value is a constant, all elements are given the same property value; otherwise, if a value is a function, the function is evaluated for each selected element, in order, being passed the current datum (d), the current index (i), and the current group (nodes), with this as the current DOM element. The function’s return value is then used to set each element’s properties. A null value will remove the specified properties.</p>
<p class="it">Si un valor es una constante, todos los elementos se les da el mismo valor de la propiedad; de lo contrario, si un valor es una función, la función se evalúa para cada elemento seleccionado, en orden, siendo pasado el punto de referencia actual ( d ), el índice actual ( i ), y el grupo actual ( nodos ), con este como el actual elemento DOM. El valor devuelto por la función se utiliza para establecer las propiedades de cada elemento. Un valor nulo eliminará las propiedades especificadas.</p>
<p class="p">If the specified values is a function, the function is evaluated for each selected element, in order, being passed the current datum (d), the current index (i), and the current group (nodes), with this as the current DOM element. The function’s return value must be an object with string values, which are then used to set properties on the current element. For example:</p>
<p class="it">Si los especificados valores es una función, la función se evalúa para cada elemento seleccionado, con el fin, que se pasa el punto de referencia actual ( d ), el índice actual ( i ), y el grupo actual ( nodos ), con esto como el actual del DOM elemento. El valor devuelto por la función debe ser un objeto con valores de cadena, que luego se utilizan para establecer propiedades en el elemento actual. Por ejemplo:</p>
<pre class="programlisting" data-language="javascript" id="transition_id12088">selection.properties(function(d, i) { return {foo: "foo-value", id: "id-" + i}; });</pre>
<p class="p">Passing a function to selection.properties is convenient for sharing some computational effort or state across multiple properties, or for specifying dynamically which properties to set.</p>
<p class="it">Al pasar de una función a la selección .properties es conveniente para compartir un poco de esfuerzo computacional o estado a través de múltiples propiedades, o para especificar dinámicamente las propiedades que se establece.</p>
<h3># transition.attrs(values)</h3>

<p class="p">Like selection.attrs, but for transition.attr.</p>

<h3># transition.styles(values[, priority])</h3>

<p class="p">Like selection.styles, but for transition.style.</p>
</div>


  <div class="" id="_labels">

    <div class="titlepage">

      <div>

        <h3 class="title">Labels</h3>


      </div>

    </div>

    <p id="visuals_are_gre4">Visuals are great, but sometimes you need to show the actual data values as text within the visualization. Here’s where value labels come in, and they are very, very easy to generate with D3.<a id="id5170635" class="indexterm" href=""></a></p>
    <p class="it">Las visuales son grandiosas, pero a veces se necesitan mostrar datos de valores, como por ejemplo texto, dentro de la visualización. Aquí es donde las etiquetas de valor entran, y son muy, muy fáciles de generar con D3.</p>

    <p id="youll_recall_fwsws">You’ll recall from the SVG primer that you can add <code class="literal">text</code> elements to an SVG element. Let’s start with:</p>
<p class="it">Te recuerdo a partir del primer SVG se pueden agregar elementos <code class="literal">text</code> a un elemento SVG. Vamos a empezar:</p>

    <pre class="programlisting" data-language="javascript" id="svgselectall_id4">svg.selectAll("text")
   .data(dataset)
   .enter()
   .append("text")</pre>

    <p id="look_familiar_">Look familiar? Just as we did for the <code class="literal">rect</code>s, here we do for the <code class="literal">text</code>s. First, select what you want, bring in the data, enter the new elements (which are just placeholders at this point), and finally append the new <code class="literal">text</code> elements to the DOM.</p>
<p class="it">¿Parecer familiar? Al igual que hicimos para los rects, aquí hacemos lo mismo con los textos. En primer lugar, seleccione los datos que desea aportar, introduzca los nuevos elementos (que son simplemente marcadores de posición en este punto), y, finalmente, añada los nuevos elementos de texto en el DOM.</p>

   


    <p id="well_extend_th">We’ll extend that code to include a data value within each <code class="literal">text</code> element by using the <code class="literal">text()</code> method:</p>
<p class="it">Extenderemos ese código para incluir un valor de data dentro de cada elemento de texto utilizando el método de text():</p>

    <pre class="programlisting" data-language="javascript" id="textfunction_id6">   .text(function(d) {
        return d;
   })</pre>

 <p id="and_then_extend">and then extend it further, by including <code class="literal">x</code> and <code class="literal">y</code> values to position the text. It’s easiest if I just copy and paste the same x/y code we previously used for the bars:</p>
<p class="it">y luego extenderlo más, mediante la inclusión de valores <code class="literal">x</code> e <code class="literal">y</code> para colocar el texto. Es más fácil si simplemente se copia y pega el mismo código de <code class="literal">x/y</code> que previamente utilizó para las barras:</p>
    <pre class="programlisting" data-language="javascript" id="attrx_func_id3">   .attr("x", function(d, i) {
        return i * (w / dataset.length);
   })
   .attr("y", function(d) {
        return h - (d * 4);
   });</pre>

    <p id="aha_value_labe">Aha! Value labels! But some are getting cut off at the top (see <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch06.html#Baby_value_labels" title="Figure 6-28. Baby value labels!">Figure 6-28</a>).</p>
<p class="it">Aha! Las etiquetas de valor! Pero algunas están siendo cortadas en la parte superior (ver Figura 6-28).</p>

    <div class="figure" id="Baby_value_labels">

      <div class="figure-contents">

        <div class="mediaobject"><em class="dotEPUBProtected"> <img alt="Imagen" src="/static/Fig628.png" /> </em></div>

      </div>

      <p class="p">Figure 6-28. Baby value labels!</p>

    </div>

    <p id="lets_try_movin">Let’s try moving them down, inside the bars, by adding a small amount to the <code class="literal">x</code> and <code class="literal">y</code> calculations:</p>
<p class="it">Trataremos el movimiento del texto hacia abajo, dentro de las barras, mediante agregando una pequeña cantidad de cálculos a <code class="literal">x</code> e <code class="literal">y</code>:</p>

    <pre class="programlisting" data-language="javascript" id="attrx_func_id4">   .attr("x", function(d, i) {
        return i * (w / dataset.length) + 5;  // Le sumo 5
   })
   .attr("y", function(d) {
        return h - (d * 4) + 15;              // Le sumo 15
   });</pre>

    <p id="the_chart_in_iswewe">The chart in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch06.html#Inbar_value_labels" title="Figure 6-29. In-bar value labels">Figure 6-29</a> is better, but not legible.</p>


    <div class="figure" id="Inbar_value_labels1">

      <div class="figure-contents">

        <div class="mediaobject"><em class="dotEPUBProtected"> <img alt="Imagen" src="/static/Fig629.png" /> </em></div>

      </div>

      <p class="p">Figure 6-29. In-bar value labels</p>


    </div>

    <p id="fortunately_we_id2">Fortunately, we can fix that:</p>
<p class="it">Afortunadamente, podemos arreglar eso:</p>

    <pre class="programlisting" data-language="javascript" id="attrfontfam_id1">   .attr("font-family", "sans-serif")
   .attr("font-size", "11px")
   .attr("fill", "white");</pre>

    <p id="fantasticode_">Fantasti-code! See <span class="emphasis"><em>20_making_a_bar_chart_labels.html</em></span> for the brilliant visualization shown in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch06.html#Really_nice_value_labels" title="Figure 6-30. Really nice value labels">Figure 6-30</a>.</p>


    <div class="figure" id="Really_nice_value_labels">

      <div class="figure-contents">

        <div class="mediaobject"><em class="dotEPUBProtected"> <img alt="Imagen" src="/static/Fig630.png" /> </em></div>

      </div>

      <p class="p">Figure 6-30. Really nice value labels</p>


    </div>

    <p id="if_you_are_not_">If you are not typographically obsessive, then you’re all done. If, however, you are like me, you’ll notice that the value labels aren’t perfectly aligned within their bars. (For example, note the “5” in the first column.) That’s easy enough to fix. Let’s use the SVG <code class="literal">text-anchor</code> attribute to center the text horizontally at the assigned <code class="literal">x</code> value:</p>
<p class="it">Si no es alguien tipográficamente obsesivo, entonces está todo hecho. Sin embargo, si usted es como yo, notará que las etiquetas de valor no estan perfectamente alineadas dentro de sus barras. (Por ejemplo, tenga en cuenta el "5" en la primera columna.) Eso es bastante fácil de solucionar. Vamos a utilizar el atributo SVG <code class="literal">text-anchor</code> introduciendo el texto horizontalmente en el valor asignado a <code class="literal">x</code>:</p>

    <pre class="programlisting" data-language="javascript" id="attrtextanc">    .attr("text-anchor", "middle")</pre>

    <p id="then_lets_cha">Then, let’s change the way we calculate the <code class="literal">x</code> position by setting it to the left edge of each bar <span class="emphasis"><em>plus</em></span> half the bar width:</p>

<p class="it">A continuación, vamos a cambiar la forma en que se calcula la posición <code class="literal">x</code> estableciéndola en el borde izquierdo de cada barra más la mitad del ancho de la barra:</p>
    <pre class="programlisting" data-language="javascript" id="attrx_func_id5">    .attr("x", function(d, i) {
        return i * (w / dataset.length) + (w / dataset.length - barPadding) / 2;
    })</pre>

    <p id="and_ill_also_b">And I’ll also bring the labels up one pixel for perfect spacing, as you can see in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch06.html#Centered_labels" title="Figure 6-31. Centered labels">Figure 6-31</a> and <span class="emphasis"><em>21_making_a_bar_chart_aligned.html</em></span>:</p>
<p class="it">Y voy a traer también las etiquetas hasta un píxel para el espaciamiento perfecto, como se puede ver en la figura 6-31 y <span class="emphasis"><em>21_making_a_bar_chart_aligned.html</em></span></p>

    <pre class="programlisting" data-language="javascript" id="attry_func_id2">    .attr("y", function(d) {
        return h - (d * 4) + 14;  //15 is now 14
    })</pre>

    <div class="figure" id="Centered_labels">

      <div class="figure-contents">

        <div class="mediaobject"><em class="dotEPUBProtected"> <img alt="Imagen" src="/static/Fig631.png" /> </em></div>

      </div>
      <p class="p">Figure 6-31. Centered labels</p>


    </div>

  </div>

<div class="" id="_MakingaScat">

    <div class="titlepage">

      <div>

        <h3 class="title">Making a Scatterplot</h3>
      </div>

    </div>

    <p id="visuals_are_gre">So far, we’ve drawn only bar charts with simple data—just one-dimensional sets of numbers.<a id="id517063" class="indexterm" href=""></a></p>
<p class="it">Hasta ahora, hemos disponerse sólo gráficos de barras con los datos sencilla - sólo conjuntos unidimensionales de números.</p>

    <p id="youll_recall_f">But when you have two sets of values to plot against each other, you need a second dimension. The scatterplot is a common type of visualization that represents two sets of corresponding values on two different axes: horizontal and vertical,<code class="literal">x</code>and y.</p>
<p class="it">Pero cuando se tienen dos conjuntos de valores para trazar una contra la otra, se necesita una segunda dimensión. El diagrama de dispersión es un tipo común de visualización que representa dos conjuntos de valores correspondiente en dos ejes diferentes: horizontal y vertical, <code class="literal">x</code> e <code class="literal">y</code>.</p>
    
    <h3>The Data</h3>

    <p id="As_you">As you saw in Chapter 3, you have a lot of flexibility around how to structure a dataset. For our scatterplot, I’m going to use an array of arrays. The primary array will contain one element for each data “point.” Each of those “point” elements will be another array, with just two values: one for the <code class="literal">x</code> value, and one for y:</p>
<p class="it">Como se vio en el capítulo 3, que tiene una gran cantidad de flexibilidad en la manera de estructurar un conjunto de datos. Para nuestro diagrama de dispersión, que voy a utilizar una array de matrices. La array primaria contendrá un elemento por cada datos Cada uno de esos elementos "puntuales" será otra array, con sólo dos valores de "punto".: Una para el valor x, y uno para y:</p>

    <pre class="programlisting" data-language="javascript" id="svgselectall_id44">var dataset = [
                [5, 20], [480, 90], [250, 50], [100, 33], [330, 95],
                [410, 12], [475, 44], [25, 67], [85, 21], [220, 88]
              ];</pre>

    <p id="Remember">Remember, <code class="literal">[] </code>means array, so nested hard brackets<code class="literal"> [[]] </code>indicate an array within another array. We separate array elements with commas, so an array containing three other arrays would look like this:</p>
    <pre class="programlisting" data-language="javascript" id="svgselectall_id45">[[],[],[]].</pre>
<p class="it">Recuerde, [] significa array, por lo que los soportes duros anidadas [[]] indican una array dentro de otra array. Nos separamos con comas elementos del array, por lo que una array que contiene otras tres arrays se vería así:</p>

    <p id="we_could">We could rewrite our dataset with more whitespace so it’s easier to read:</p>
<p class="it">Podríamos reescribir nuestra base de datos con más espacio en blanco así que es más fácil de leer:</p>

    <pre class="programlisting" data-language="javascript" id="textfunction_id66">var dataset = [
                  [ 5,     20 ],
                  [ 480,   90 ],
                  [ 250,   50 ],
                  [ 100,   33 ],
                  [ 330,   95 ],
                  [ 410,   12 ],
                  [ 475,   44 ],
                  [ 25,    67 ],
                  [ 85,    21 ],
                  [ 220,   88 ]
              ];</pre>

      <p id="now_you">Now you can see that each of these 10 rows will correspond to one point in our visualization. With the row [5, 20], for example, we’ll use 5 as the<code class="literal">x</code>value, and 20 for the y.</p>
<p class="it">Ahora se puede ver que cada uno de estos 10 filas corresponderá a un punto en nuestra visualización. Con la fila [5, 20], por ejemplo, usaremos 5 como el valor de x, y 20 para la ordenada.</p>
      <h3>The Scatterplot</h3>


      <p id="Let_carry">Let’s carry over most of the code from our bar chart experiments, including the piece that creates the SVG element:</p>
<p class="it">Vamos a recoger la mayor parte del código de nuestros experimentos gráficos de barras, incluyendo la pieza que crea el elemento SVG:</p>

    <pre class="programlisting" data-language="javascript" id="attrx_func_id33">//Create SVG element
var svg = d3.select("body")
            .append("svg")
            .attr("width", w)
            .attr("height", h);</pre>

    <p id="create_svg_pi">Instead of creating rects, however, we’ll make a circle for each data point:</p>
<p class="it">En lugar de crear rects, sin embargo, vamos a hacer un circle para cada punto de datos:</p>
    
    <pre class="programlisting" data-language="html" id="attrx_func_id444">   svg.selectAll("circle")  // &lt;-- No longer "rect"
   .data(dataset)
   .enter()
   .append("circle")     // &lt;-- No longer "rect"</pre>    

   <p id="also_inst">Also, instead of specifying the rect attributes of x, y, width, and height, our circles need cx, cy, and r:</p>

<p class="it">Además, en lugar de especificar los atributos x, y, ancho y alto del rect, nuestros círculos necesitan definir cx, cy, y r:</p>

    <pre class="programlisting" data-language="javascript" id="attrx_func_id456">      .attr("cx", function(d) {
        return d[0];
   })
   .attr("cy", function(d) {
        return d[1];
   })
   .attr("r", 5);</pre>

    <p id="the_chart_in_is">See the working scatterplot code that recreates the result shown in Figure 6-32 in <span class="emphasis"><em>22_scatterplot.html.</em></span></p>
<p class="it">Ver el código de dispersión de trabajo que recrea el resultado que se muestra en el archivo <span class="emphasis"><em>22_scatterplot.html.</em></span></p>

    <div class="figure" id="Inbar_value_labels">

      <div class="figure-contents">

        <div class="mediaobject"><em class="dotEPUBProtected"> <a href="http://orm-chimera-prod.s3.amazonaws.com/1230000000345/images/idvw_0629.png"><img alt="Imagen" src="/static/Fig632.png" /></a> </em></div>

      </div>

      <p class="p">Figure 6-32. Simple scatterplot</p>
</div>

    <p class="p">Notice how we access the data values and use them for the cx and cy values. When using function(d), D3 automatically hands off the current data value as <code class="literal">d</code> to your function. In this case, the current data value is one of the smaller, subarrays in our larger dataset array.</p>
<p class="it">Observe cómo se accede a los valores de los datos y se utilizan para los valores de cy y cx. Cuando se utiliza la function(d), D3 da automáticamente el valor de los datos actuales, <code class="literal">d</code> para su función. En este caso, el valor de datos actual es uno de los más pequeños, subarrays en nuestro mayor conjunto de datos array.</p>

    <p class="p">When each single datum d is itself an array of values (and not just a single value, like 3.14159), you need to use bracket notation to access its values. Hence, instead of return d, we use return d[0] and return d[1], which return the first and second values of the array, respectively.</p>

<p class="it">Cuando cada único dato d es en sí mismo un array de valores (y no sólo un valor único, como 3,14159), es necesario utilizar notación de corchetes para acceder a sus valores. Por lo tanto, en lugar de retorno d, utilizamos el retorno d[0] y d[1], que devuelve el primero y segundo valor de la array respectivamente.</p>

    <p class="p">For example, in the case of our first data point [5, 20], the first value (array position 0) is 5, and the second value (array position 1) is 20. Thus:</p>
<p class="it">Por ejemplo, en el caso de nuestro primer punto de datos [5, 20], el primer valor (posición de array 0) es 5, y el segundo valor (posición de array 1) es 20. Por lo tanto:</p>

    <pre class="programlisting" data-language="javascript" id="attrx_func_id45641">   d[0] returns 5 d[1] returns 20</pre>
    <p class="p">By the way, if you ever want to access any value in the larger dataset (outside of D3, say), you can do so using bracket notation. For example:</p>
<p class="it">Por cierto, si alguna vez desea acceder a cualquier valor en el conjunto de datos más grande (fuera de D3, por ejemplo), puede hacerlo utilizando notación de corchetes. Por ejemplo:</p>

    <pre class="programlisting" data-language="javascript" id="attrx_func_id4560">  dataset[5] returns [410, 12]</pre>
    <p class="p">You can even use multiple sets of brackets to access values within nested arrays:</p>
<p class="it">Incluso puede utilizar varios conjuntos de corchetes para los valores de acceso dentro de las arrays anidadas:</p>

<pre class="programlisting" data-language="javascript" id="attrx_func_id45601"> dataset[5][1] returns 12</pre>

    <p class="p">Don’t believe me? Take another look at the scatterplot page 22_scatterplot.html, open your JavaScript console, type in <code class="literal">dataset[5]</code> or <code class="literal">dataset[5][1]</code>, and see what happens.</p>
ee<p class="it">No me creen? Eche otro vistazo a la página 22_scatterplot.html diagrama de dispersión, abra la consola de JavaScript, el tipee <code class="literal">dataset[5]</code> o <code class="literal">dataset[5][1]</code>, y vea lo que sucede.

</p><h3>Ejercicio</h3>

<h3>Size</h3>

<p class="p">Maybe you want the circles to be different sizes, so each circle’s area corresponds to its y value. As a general rule, when visualizing quantitative values with circles, make sure to encode the values as area, not as a circle’s radius. Perceptually, we understand the overall amount of “ink” or pixels to reflect the data value. A common mistake is to map the value to the radius. (I’ve done this many times myself.) Mapping to the radius is easier to do, as it requires less math, but the result will visually distort your data.</p>
<p class="it">Tal vez usted quiere que los círculos sean de tamaños diferentes, por lo que cada área del círculo corresponde a su valor de y. Como regla general, cuando hace visualización de valores cuantitativos con círculos, asegúrese de codificar los valores como la zona, no como un radio del círculo. Perceptualmente, entendemos la cantidad total de "tinta" o píxeles para reflejar el valor de los datos. Un error común es asignar el valor al radio. (He hecho esto muchas veces.) La correspondencia con el radio es más fácil de hacer, ya que requiere matemáticas, pero el resultado distorsionará visualmente sus datos.</p>

<p class="p">Yet when creating SVG circles, we can’t specify an area value; we have to calculate the radius r and then set that. So, starting with a data value as area, how do we get to a radius value?</p>
<p class="it">Sin embargo, cuando creamos círculos SVG, podemos especificar un valor de área; tenemos que calcular el radio r y luego fijar eso. Así, a partir de un valor de datos como área, ¿cómo podemos llegar a un valor de radio?


</p><p class="p">Let’s say the area, then, is our data value, which is d[1], in this case. Actually, let’s subtract that value from h, so the circles at the top are larger. So our area value is h - d[1]. (We’ll cover a cleaner way to achieve this effect using scales in Chapter 7.)</p>
<p class="it">Vamos dicen que el área, entonces, es nuestro valor de datos, que es <code class="literal">d[1]</code>, en este caso. En realidad, vamos a restar ese valor de h, por lo que los círculos en la parte superior serán más grandes. Así que nuestro valor del área es <code class="literal">h-d[1]</code>.(Lo cubriremos de una manera más clara para conseguir este efecto utilizando escalas en el capítulo 7.)</p>

<p class="p">You might remember that the area of a circle equals π times the radius squared, or A = πr2.</p>
<p class="it">Usted recordará que el área de un círculo es igual a π  por radio al cuadrado, o A = π r2.</p>
<p class="p">To convert this area to a radius value, we simply have to take its square root. We can do that using JavaScript’s built-in <code class="literal">Math.sqrt()</code> function, as in <code class="literal">Math.sqrt(h-d[1])</code>.</p>
<p class="it"> Para convertir esta zona en un valor de radio, simplemente tenemos que tomar su raíz cuadrada. Podemos usar la función integrada de JavaScript <code class="literal">Math.sqrt()</code>, como en <code class="literal">Math.sqrt(h-d[1])</code>.</p>


<p class="p">Now, instead of setting all r values to the static value of 5, try:</p>

<p class="it">Ahora, en lugar de establecer todos los valores de r al valor estático de 5, probaremos:</p>

<pre class="programlisting" data-language="javascript" id="attrfontfam_id56575"> 
.attr("r", function(d) {
    return Math.sqrt(h - d[1]);
});</pre>
<p class="p">See <span class="emphasis"><em>23_scatterplot_sqrt.html</em></span> for the code that results in the scatterplot shown in Figure 6-33.</p>
<p class="it">Ver <span class="emphasis"><em>23_scatterplot_sqrt.html</em></span> para el código que resulta en el diagrama de dispersión se muestra en la figura 6-33.</p>
<img alt="Imagen" src="/static/Fig633.png" />
<p class="p">Figure 6-33. Scatterplot with sized circles</p>
<p class="it">Figura 6-33. Diagrama de dispersión con los círculos de tamaño</p>

<p class="p">After arbitrarily subtracting the datum’s y value <code class="literal">d[1]</code> from the SVG height h, and then taking the square root, we see that circles with greater y values (those circles lower down) have smaller areas (and shorter radii).</p>
<p class="it">Después de restar arbitrariamente el dato y el valor <code class="literal">d[1]</code> en la altura SVG h, y luego tomando la raíz cuadrada, vemos que los círculos con mayores valores y (los círculos inferiores de abajo) tienen áreas más pequeñas (y radios más cortos).</p>

<p class="p">This particular use of circle area as a visualization tool isn’t necessarily useful. I simply want to illustrate how you can use d, along with bracket notation, to reference an individual datum, apply some transformation to that value, and use the newly calculated value to return a value back to the attribute-setting method (a value used for r, in this case).</p>
<p class="it">Este uso particular del área del círculo como una herramienta de visualización no es necesariamente útil. Quiero simplemente ilustrar cómo se puede utilizar d, junto con la notación de corchetes, al referenciar un dato individual, aplicar un poco de transformación a ese valor, y utilizar el valor calculado de nuevo para devolver un valor de nuevo al método de ajuste de atributos (un valor utilizado para r, en este caso).</p>

<h3>Labels</h3>

<p class="p">Let’s label our data points with text elements. I’ll adapt the label code from our bar chart experiments, starting with the following:</p>
<p class="it">Vamos a etiquetar nuestros puntos de datos con elementos de texto. Voy a adaptar la etiqueta de código de nuestros experimentos gráfico de barras, a partir de lo siguiente:</p>
<pre class="programlisting" data-language="javascript" id="attrx_func_id45642"> 
svg.selectAll("text")  // &lt;-- Note "text", not "circle" or "rect"
   .data(dataset)
   .enter()
   .append("text")     // &lt;-- Same here!</pre>
<p class="p">This looks for all text elements in the SVG (there aren’t any yet), and then appends a new text element for each data point. Then we use the text() method to specify each element’s contents:</p>
<p class="it">Esto se parece a todos los elementos de texto en el SVG (no tenemos ninguno aún), y luego se añade un nuevo elemento de texto para cada punto de datos. A continuación, utilizamos el método de text() para especificar el contenido de cada elemento:</p>
<pre class="programlisting" data-language="javascript" id="attrx_func_id45643"> 
   .text(function(d) {
        return d[0] + "," + d[1];
   })</pre>
<p class="p">This looks messy, but bear with me. Once again, we’re using function(d) to access each data point. Then, within the function, we’re using both d[0] and d[1] to get both values within that data point array.</p>
<p class="it">Esto se ve desordenado, pero tengan paciencia conmigo. Una vez más, estamos usando las function(d) para acceder a cada punto de datos. Luego, dentro de la función, estamos utilizando ambos d[0] y d[1] para obtener ambos valores dentro de ese array de punto de datos.</p>

<p class="p">The plus + symbols, when used with strings, such as the comma between quotation marks ",", act as append operators. So what this one line of code is really saying is this: get the values of d[0] and d[1] and smush them together with a comma in the middle. The end result should be something like 5,20 or 25,67.</p>
<p class="it">Los símbolos +, además, cuando se utilizan con strings, como la coma entre comillas ",", actúan como operadores anexos. Entonces, lo qué esta línea de código está diciendo en realidad es lo siguiente: obtenga los valores de d[0] y d[1] y juntelos poniendo una coma en el medio. El resultado final debería ser algo así como 5,20 o 25,67.</p>

<p class="p">Next, we specify where the text should be placed with <code class="literal">x</code> and <code class="literal">y</code>  values. For now, let’s just use <code class="literal">d[0]</code>  and <code class="literal">d[1]</code> , the same values that we used to specify the circle positions:</p>
<p class="it">A continuación, se especifica que el texto debe estar en el lugar de d con los valores de <code class="literal">x</code> e <code class="literal">y</code>. Por ahora, sólo tiene que utilizar <code class="literal">d[0]</code> y <code class="literal">d[1]</code>, los mismos valores que usamos para especificar las posiciones del círculo:</p>
<pre class="programlisting" data-language="javascript" id="attrx_func_id45644"> 
   .attr("x", function(d) {
        return d[0];
   })
   .attr("y", function(d) {
        return d[1];
   })</pre>
<p class="p">Finally, add a bit of font styling with:</p>
<p class="it">Por último, añadir un poco de estilo de fuente con:</p>
<pre class="programlisting" data-language="javascript" id="attrx_func_id45645"> 
   .attr("font-family", "sans-serif")
   .attr("font-size", "11px")
   .attr("fill", "red");</pre>
<p class="p">The result in Figure 6-34 might not be pretty, but we got it working! See <span class="emphasis"><em>24_scatterplot_labels.html for the latest.</em></span></p>
<p class="it">El resultado en la figura 6-34 no es agradable, pero tengo trabajo! Ver 24_scatterplot_labels.html para la última.</p>

<img alt="Imagen" src="/static/Fig634.png" />

<p class="p">Figure 6-34. Scatterplot with labels</p>
<p class="it">Figura 6-34. Diagrama de dispersión con etiquetas</p>

<h3>Ejercicio</h3>

<h3>Next Steps</h3>
<p class="p">Hopefully, some core concepts of D3 are becoming clear: loading data, generating new elements, and using data values to derive attribute values for those elements.</p>
<p class="it">Con suerte, algunos conceptos básicos de la D3 se están tornando claros: la carga de datos, la generación de nuevos elementos, y el uso de valores de datos para derivar en valores de atributos para esos elementos.</p>

<p class="p">Yet the image in Figure 6-34 is barely passable as a data visualization. The scatterplot is hard to read, and the code doesn’t use our data flexibly. To be honest, we haven’t yet improved on—gag—Excel’s Chart Wizard!</p>
<p class="it">Sin embargo, la imagen de la Figura 6-34 apenas permite la visualización de datos. El diagrama de dispersión es difícil de leer, y el código no utiliza nuestros datos de forma flexible. Para ser honesto, no hemos todavía mejorado al Asistente para gráficos Excel!</p>

<p class="p">Not to worry: D3 is way cooler than Chart Wizard (not to mention Clippy), but generating a shiny, interactive chart involves taking our D3 skills to the next level. To use data flexibly, we’ll learn about D3’s scales in the next chapter. And to make our scatterplot easier to read, we’ll learn about axis generators and axis labels.</p>
<p class="it">No hay que preocuparse: D3 es la forma más cool para el Chart Wizard (por no hablar de Clippy), pero generar un brillante gráfico interactivo consiste en pasar nuestras habilidades D3 al siguiente nivel. Para utilizar datos de forma flexible, vamos a aprender acerca de escalas D3 en el siguiente capítulo. Y para hacer a nuestro diagrama de dispersión más fácil de leer, vamos a aprender acerca de generadores de eje y etiquetas de los ejes.</p>

<p class="p">This would be a good time to take a break and stretch your legs. Maybe go for a walk, or grab a coffee or a sandwich. I’ll hang out here (if you don’t mind), and when you get back, we’ll jump into D3 scales!</p>
<p class="it">Este sería un buen momento para tomar un descanso y estirar las piernas. Tal vez ir a dar un paseo, o tomar un café o un bocadillo. Voy a pasar el tiempo aquí (si no te importa), y cuando vuelvas, vamos a saltar a las escalas D3!</p>


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