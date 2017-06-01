<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    
    <div class="block">
    
<h1 class="title">Chapter 11. Layouts</h1>
<p class="it">Contrariamente a lo que su nombre indica, los diseños de D3 no, de hecho, ponen nada para usted en la pantalla. Los métodos de diseño no tienen salida visual directa. Por el contrario, los diseños D3 toman los datos que se proporcionan y reasignar el mapa o de otro tipo transformarla, generando así nuevos datos que es más conveniente para una tarea visual específico. Es todavía depende de usted para tomar que los nuevos datos y generar representaciones visuales de ella.</p>
<p class="p" id="contrary_to_wha_id2">Contrary to what the name implies, D3 <span class="emphasis"><em>layouts</em></span> do not, in fact, lay anything out for you on the screen. The layout methods have no direct <span class="emphasis"><em>visual</em></span> output. Rather, D3 layouts take data that you provide and remap or otherwise transform it, thereby generating <span class="emphasis"><em>new</em></span> data that is more convenient for a specific visual task. It’s still up to you to take that new data and generate visuals from it.<a id="ix_lay" class="indexterm" href=""></a><a id="id556286" class="indexterm" href=""></a></p>


    <p class="it">Aquí está una lista completa de todos los diseños D3:</p>
    <p class="p" id="here_is_a_compl">Here is a complete list of all D3 layouts:</p>


    <div>

      <ul class="itemizedlist">

        <li class="p"> Bundle </li>
        <li class="it"> Haz</li>

        <li class="p"> Chord </li>
        <li class="it"> Dividir</li>
        
        <li class="p"> Cluster </li>
        <li class="it"> Acorde</li>

        <li class="p"> Force </li>
        <li class="it"> Fuerza</li>

        <li class="p"> Histogram </li>
        <li class="it"> histograma</li>

        <li class="p"> Pack </li>
        <li class="it"> Racimo</li>

        <li class="p"> Partition </li>
        <li class="it"> Paquete</li>

        <li class="p"> Pie </li>
        <li class="it"> Tarta</li>

        <li class="p"> Stack </li>
        <li class="it"> Apilar</li>

        <li class="p"> Tree </li>
        <li class="it"> Árbol</li>

        <li class="p"> Treemap </li>
        <li class="it"> treemap</li>

      </ul>

    </div>
 <p class="it">En este capítulo, presento tres de los más comunes: Torta, Pila, y Fuerza. Cada diseño realiza una función diferente, y cada uno tiene su propia idiosincrasia.</p>
    <p class="p" id="in_this_chapter">In this chapter, I introduce three of the most common: <span class="emphasis"><em>pie</em></span>, <span class="emphasis"><em>stack</em></span>, and <span class="emphasis"><em>force</em></span>. Each layout performs a different function, and each has its own idiosyncrasies.</p>
   
<p class="it">Si es curioso acerca de cualquiera de los otros diseños D3, eche un vistazo a los muchos ejemplos en la página web D3, y asegúrese de hacer referencia a la documentación oficial de la API en los diseños.</p>
    <p class="p" id="if_you_are_curi">If you are curious about any of the other D3 layouts, check out <a class="ulink" href="https://github.com/mbostock/d3/wiki/Gallery" target="_top">the many examples on the D3 website</a>, and be sure to reference <a class="ulink" href="https://github.com/mbostock/d3/wiki/Layouts" target="_top">the official API documentation on layouts</a>.</p>

    

          <h2 class="title">Pie Layout</h2>
 <p class="it">d3.layout.pie() podría no ser tan deliciosa como suena, pero aún así es digno de su atención. Obviamente, su uso típico es para la creación de gráficos de sectores, como el ejemplo de la Figura 11-1.</p>
      <p class="p" id="dlayoutpie"><code class="literal">d3.layout.pie()</code> might not be as delicious as it sounds, but it’s still worthy of your attention. Obviously, its typical use is for creating pie charts, like the example in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch11.html#simple_pie_chart" title="Figure 11-1. A simple pie chart">Figure 11-1</a>.</p>
       

      <div>

            <img src="/static/wfeBxecqcH-img1.png" alt="A simple pie chart"/>


        <p class="fig">Figure 11-1. A simple pie chart</p>


      </div>
 <p class="it">Sientase libre de abrir el codigo de ejemplo en <span class="emphasis"><em>01_pie.html</em></span></p>
      <p class="p" id="feel_free_to_op">Feel free to open up the sample code for this in <span class="emphasis"><em>01_pie.html</em></span> and poke around.<a id="id556477" class="indexterm" href=""></a><a id="id556485" class="indexterm" href=""></a><a id="id556491" class="indexterm" href=""></a></p>
     
 <p class="it">Para dibujar esas porciones bonitas, necesitamos conocer una serie de medidas, incluyendo un radio interior y exterior de cada porción, además de la partida, el ángulo que terminan. El propósito de la disposición de la torta es tomar sus datos y calcular todos los ángulos desordenado para usted, que evitará tener que pensar en radianes.</p>
      <p class="p" id="to_draw_those_p">To draw those pretty wedges, we need to know a number of measurements, including an inner and outer radius for each wedge, plus the starting and ending angles. The purpose of the pie layout is to take your data and calculate all those messy angles for you, sparing you from ever having to think about radians.</p>
       
<p class="it">Recuerde radianes? En caso de que no lo haga, aquí hay un rápido repaso. Del mismo modo que hay 360 ° en un círculo, hay 2π radianes. Así π radianes es igual a 180 °, o la mitad de un círculo. La mayoría de las personas les resulta más fácil pensar en términos de grados; los ordenadores prefieren radianes.</p>
      <p class="p" id="remember_radian">Remember radians? In case you don’t, here’s a quick refresher. Just as there are 360° in a circle, there are 2π radians. So π radians equals 180°, or half a circle. Most people find it easier to think in terms of degrees; computers prefer radians.<a id="id556518" class="indexterm" href=""></a><a id="id556523" class="indexterm" href=""></a></p>
  <p class="it">Para este gráfico circular, vamos a empezar, como de costumbre, con un conjunto de datos muy simple:</p>
        
        <p class="p" id="for_this_pie_ch">For this pie chart, let’s start, as usual, with a very simple dataset:</p>
      

      <pre class="programlisting">var dataset = [ 5, 10, 20, 45, 6, 25 ];</pre>
 <p class="it">Podemos definir un diseño de torta predeterminado muy simplemente como:</p>
      <p class="p" id="we_can_define_a">We can define a default pie layout very simply as:</p>
       

 
      <pre class="programlisting">var pie = d3.layout.pie();</pre>
<p class="it">Entonces, todo lo que queda es transferir nuestros datos a la función nueva <code class="literal">pie()</code>, como en el pastel (conjunto de datos). Comparación de los conjuntos de datos antes y después en la figura 11-2.</p>
      <p class="p" id="then_all_that_">Then, all that remains is to hand off our data to the new <code class="literal">pie()</code> function, as in <span class="keep-together"><code class="literal">pie(dataset)</code></span>. Compare the datasets before and after in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch11.html#pieified_data" title="Figure 11-2. Your data, pie-ified">Figure 11-2</a>.</p>
        

      <div>

            <img src="/static/wfeBxecqcH-img2.png" alt="Your data, pie-ified"/>

  

         <p class="fig">Figure 11-2. Your data, pie-ified</p>

      </div>
  <p class="it">El diseño de la torta lleva nuestro simple array de números y genera un array de objetos, un objeto para cada valor. Cada uno de estos objetos tiene ahora unos nuevos valores más importantes, <code class="literal">startAngle</code> y <code class="literal">endAngle</code>. Wow, eso fue fácil!</p>
      <p class="p" id="the_pie_layout_">The pie layout takes our simple array of numbers and generates an array of objects, one object for each value. Each of those objects now has a few new values—most important, <code class="literal">startAngle</code> and <code class="literal">endAngle</code>. Wow, that was easy!</p>
      
 <p class="it">Ahora, para dibujar en realidad las porciones, volvemos a <code class="literal">d3.svg.arc()</code>, una función incorporada en práctico para la elaboración de arcos como elementos de <code class="literal">path</code> SVG. No hemos hablado acerca de los <code class="literal">path</code> todavía, pero son la respuesta de SVG para dibujar formas irregulares. Cualquier cosa que no es un <code class="literal">rect</code>, <code class="literal">circle</code>, u otra forma básica se puede dibujar como un <code class="literal">path</code>. El problema es, la sintaxis para definir los valores de ruta no es especialmente humana de usar. Por ejemplo, aquí está el código para la gran porción de color rojo en la Figura 11-1:</p>
      <p class="p" id="now_to_actuall">Now, to actually draw the wedges, we turn to <code class="literal">d3.svg.arc()</code>, a handy built-in function for drawing arcs as SVG <code class="literal">path</code> elements. We haven’t talked about <code class="literal">path</code>s yet, but they are SVG’s answer to drawing irregular forms. Anything that’s not a <code class="literal">rect</code>, <code class="literal">circle</code>, or another basic shape can be drawn as a <code class="literal">path</code>. The catch is, the syntax for defining <code class="literal">path</code> values is not particularly human-friendly.<a id="id556797" class="indexterm" href=""></a><a id="id556803" class="indexterm" href=""></a> For example, here’s the code for the big, red wedge in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch11.html#simple_pie_chart" title="Figure 11-1. A simple pie chart">Figure 11-1</a>:</p>
     

<pre class="programlisting">&lt;path fill="#d62728" d="M9.184850993605149e-15,-150A150,150 0 0,1         83.99621792063931,124.27644738657631L0,0Z"/&gt;</pre>
 <p class="it"> Si se puede entender que, a continuación, que no necesitan esta libro.</p>
      <p class="p" id="if_you_can_unde">If you can understand that, then you don’t need this book.</p>
   
   <p class="it">La conclusión es, lo mejor es dejar que funciona como <code class="literal">d3.svg.arc()</code> controlar <code class="literal">path</code> que generan mediante programación. Usted no quiere probar a escribir estas cosas a mano.</p>
      <p class="p" id="the_bottom_line">The bottom line is, it’s best to let functions like <code class="literal">d3.svg.arc()</code> handle generating <code class="literal">path</code>s programatically. You don’t want to try writing this stuff out by hand.</p>

     <p class="it">Los arcos se definen como funciones personalizadas, y requieren valores de radio interior y exterior:</p>
      <p class="p" id="arcs_are_define">Arcs are defined as custom functions, and they require inner and outer radius values:</p>
        

      <pre class="programlisting">var w = 300;
var h = 300;

var outerRadius = w / 2;
var innerRadius = 0;
var arc = d3.svg.arc()
                .innerRadius(innerRadius)
                .outerRadius(outerRadius);</pre>
<p class="it">Aquí estoy estableciendo el tamaño de todo el gráfico sea 300 por 300 cuadrado. Entonces estoy estableciendo el outerRadius a la mitad, o 150. El innerRadius es cero. Volveremos a innerRadius en un momento.</p>
      <p class="p" id="here_im_settin">Here I’m setting the size of the whole chart to be 300 by 300 square. Then I’m setting the <code class="literal">outerRadius</code> to half of that, or 150. The <code class="literal">innerRadius</code> is zero. We’ll revisit <span class="keep-together"><code class="literal">innerRadius</code></span> in a moment.</p>

       <p class="it">Estamos listos para sacar algunas cuñas! En primer lugar, vamos a crear el elemento SVG, de costumbre:</p>   
      <p class="p" id="were_ready_to_">We’re ready to draw some wedges! First, we create the SVG element, per usual:</p>
       

      <pre class="programlisting">//Create SVG element
var svg = d3.select("body")
            .append("svg")
            .attr("width", w)
            .attr("height", h);</pre>
 <p class="it">Entonces podemos crear nuevos grupos para cada cuña entrante, el enlace de datos de la empanada-cado a los nuevos elementos, y la traducción de cada grupo en el centro de la tabla, por lo que las rutas aparecerán en el lugar correcto:</p>
      <p class="p" id="then_we_can_cre">Then we can create new groups for each incoming wedge, binding the pie-ified data to the new elements, and translating each group into the center of the chart, so the <code class="literal">path</code>s will appear in the right place:</p>
   
      <pre class="programlisting" data-language="javascript" id="set_up_groups">//Set up groups
var arcs = svg.selectAll("g.arc")
        .data(pie(dataset))
        .enter()
        .append("g")
        .attr("class", "arc")
        .attr("transform", "translate(" + outerRadius + ", " + outerRadius + ")");</pre>

      <p class="p" id="note_that_were">Note that we’re saving a reference to each newly created <code class="literal">g</code> in a variable called <code class="literal">arcs</code>.</p>
<p class="it">Consejo adicional: Recuerde cómo arco() requiere un valor innerRadius? Podemos expandir eso para nada mayor que cero, y nuestro gráfico circular se convierte en un gráfico de anillo como el que se muestra en la Figura 11-3:</p>


<p class="it">Disposición pila</p>


<p class="it">d3.layout.stack() convierte los datos bidimensionales en datos "apilados"; se calcula un valor de referencia para cada dato, para que puedas capas "pila" de datos en la parte superior de uno al otro. Esto puede ser usado para generar los gráficos de barras apiladas, gráficos de áreas apiladas, e incluso streamgraphs (que simplemente se apilan las gráficas de áreas, pero sin el valor de línea de base a partir rígida de cero).</p>


<p class="it">Por ejemplo, vamos a empezar con el gráfico de barras apiladas en la figura 11-4.</p>
 <p class="it">Tenga en cuenta que estamos ahorrando una referencia a cada g de nueva creación en una variable llamada arcos.</p>
      
<p class="it">Por último, dentro de cada nueva g, añadimos un camino. Una descripción camino caminos se define en el atributo d. Así que aquí llamamos el generador de arco, que genera la información de ruta en base a los datos ya unidos a este grupo:</p>
      <p class="p" id="finally_within">Finally, within each new <code class="literal">g</code>, we append a <code class="literal">path</code>. A <code class="literal">path</code>s path description is defined in the <code class="literal">d</code> attribute. So here we call the <code class="literal">arc</code> generator, which generates the path information based on the data already bound to this group:</p>


      <pre class="programlisting" data-language="javascript" id="draw_arc_path">//Draw arc paths
arcs.append("path")
    .attr("fill", function(d, i) {
        return color(i);
    })
    .attr("d", arc);</pre>
<p class="it"> Ah, y puede que se pregunte donde los colores están viniendo. Si se echa un vistazo 01_pie.html, se le nota esta línea:</p>
      <p class="p" id="oh_and_you_mig">Oh, and you might be wondering where those colors are coming from. If you check out <span class="emphasis"><em>01_pie.html</em></span>, you’ll note this line:</p>


      <pre class="programlisting" data-language="javascript" id="var_color__d_id1">var color = d3.scale.category10();</pre>
<p class="it">D3 tiene un número de maneras útiles para generar colores categóricas. Estos pueden no ser sus colores preferidos, pero son rápidos para caer en cualquier visualización mientras se encuentra en la fase de creación de prototipos. d3.scale.category10 () crea una escala ordinal con un rango de salida de 10 colores diferentes. (Véase el wiki para más información sobre estas escalas de color, así como paletas de colores calibrados perceptualmente, basado en la investigación por Cynthia Brewer, que se incluye con D3).</p>

<p class="p" id="d_has_a_number">D3 has a number of handy ways to generate categorical colors. These might not be your favorite colors, but they are quick to drop into any visualization while you’re in the prototyping stage. <code class="literal">d3.scale.category10()</code> creates an <span class="emphasis"><em>ordinal</em></span> scale with an output range of 10 different colors. (See <a class="ulink" href="https://github.com/mbostock/d3/wiki/Ordinal-Scales" target="_top">the wiki</a> for more information on these color scales as well as perceptually calibrated color palettes, based on research by Cynthia Brewer, that are included with D3.)<a id="id557821" class="indexterm" href=""></a><a id="id557827" class="indexterm" href=""></a><a id="id557833" class="indexterm" href=""></a></p>


<p class="it">Por último, podemos generar etiquetas de texto para cada cuña:</p>

<p class="p" id="lastly_we_can_">Lastly, we can generate text labels for each wedge:</p>


      <pre class="programlisting" data-language="javascript" id="arcsappendte">arcs.append("text")
    .attr("transform", function(d) {
        return "translate(" + arc.centroid(d) + ")";
    })
    .attr("text-anchor", "middle")
    .text(function(d) {
        return d.value;
    });</pre>
<p class="it">Observamos que en el texto (), hacemos referencia al valor con d.value en lugar de sólo d. Esto se debe a que los datos de la empanada con destino-cado, así que en vez de hacer referencia a nuestra array original (d), tenemos que hacer referencia a la array de objetos (d.value).</p>

<p class="p" id="note_that_in_te">Note that in <code class="literal">text()</code>, we reference the value with <code class="literal">d.value</code> instead of just <code class="literal">d</code>. This is because we bound the pie-ified data, so instead of referencing our original array (<code class="literal">d</code>), we have to reference the array of objects (<code class="literal">d.value</code>).</p>

<p class="it">Lo único nuevo aquí es arc.centroid (d). WTH? Un centro de gravedad es el punto central calculado de cualquier forma, si esa forma es regular (como un cuadrado) o muy irregular (como un resumen del estado de Maryland). arc.centroid () es una función de super-útil que calcula y devuelve el punto central de cualquier arco. Traducimos cada elemento de etiqueta de texto a centroide de cada arco, y así es como conseguimos las etiquetas de texto que flotan en el centro de cada cuña.</p>

<p class="p" id="the_only_thing_">The only thing new here is <code class="literal">arc.centroid(d)</code>. WTH? A <span class="emphasis"><em>centroid</em></span> is the calculated center point of any shape, whether that shape is regular (like a square) or highly irregular (like an outline of the state of Maryland). <code class="literal">arc.centroid()</code> is a super-helpful function that calculates and returns the center point of any arc. We translate each <code class="literal">text</code> label element to each arc’s centroid, and that’s how we get the text labels to float right in the middle of each wedge.<a id="id558152" class="indexterm" href=""></a></p>


<p class="it">Consejo adicional: Recuerde cómo arco () requiere un valor de Radio interior? Podemos expandir eso para nada mayor que cero, y nuestro gráfico circular se convierte en un gráfico de anillo como el que se muestra en la Figura 11-3:</p>

<p class="p" id="bonus_tip_reme">Bonus tip: Remember how <code class="literal">arc()</code> required an <code class="literal">innerRadius</code> value? We can expand that to anything greater than zero, and our pie chart becomes a <span class="emphasis"><em>ring</em></span> chart like the one<a id="id558209" class="indexterm" href=""></a><a id="id558215" class="indexterm" href=""></a> shown in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch11.html#simple_ring_chart" title="Figure 11-3. A simple ring chart">Figure 11-3</a>:</p>

      <pre class="programlisting" data-language="javascript" id="var_innerradius">var innerRadius = w / 3;</pre>

      <div>

            <img src="/static/wfeBxecqcH-img3.png" alt="A simple ring chart"/>

<p class="fig">Figure 11-3. A simple ring chart</p>
<p class="fig">imagen Figura 11-3. Un gráfico simple anillo</p>

      </div>

<p class="it">Comprobar que en 02_ring.html.</p>
<p class="p" id="check_it_out_in_id2">Check it out in <span class="emphasis"><em>02_ring.html</em></span>.</p>

<p class="it">Una cosa más: El diseño de la empanada reordena automáticamente nuestros valores de datos de mayor a menor. Recordemos, empezamos con [5, 10, 20, 45, 6, 25], por lo que el valor pequeño de 6 debería haber aparecido entre el 45 y el 25, pero sin la disposición ordenada de nuestros valores en orden descendente, por lo que la tabla se inició con 45 en la posición de las 12 en punto, y todo se va hacia la derecha a partir de ahí.</p>

<p class="p" id="one_more_thing_id3">One more thing: The pie layout automatically reordered our data values from largest to smallest. Remember, we started with <code class="literal">[ 5, 10, 20, 45, 6, 25 ]</code>, so the small value of 6 should have appeared between 45 and 25, but no—the layout sorted our values in descending order, so the chart began with 45 at the 12 o’clock position, and everything just goes clockwise from there.</p>


          <h2 class="title">Stack Layout</h2>

<p class="p" id="dlayoutstack"><code class="literal">d3.layout.stack()</code> converts two-dimensional data into “stacked” data; it calculates a baseline value for each datum, so you can “stack” layers of data on top of one another. This can be used to generate stacked bar charts, stacked area charts, and even <span class="keep-together">streamgraphs</span> (which are just stacked area charts but without the rigid starting baseline value of zero).<a id="id558380" class="indexterm" href=""></a><a id="id558388" class="indexterm" href=""></a><a id="id558393" class="indexterm" href=""></a></p>

<p class="p" id="for_example_we">For example, we’ll start with the stacked bar chart in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch11.html#simple_stacked_bar_chart" title="Figure 11-4. A simple stacked bar chart">Figure 11-4</a>.</p>

      <div>

<img src="/static/wfeBxecqcH-img4.png" alt="A simple stacked bar chart"/>
<p class="fig">imagen Figura 11-4. Un simple gráfico de barras apiladas</p>
<p class="fig">Figure 11-4. A simple stacked bar chart</p>


      </div>
<p class="it">Digamos que usted tenía algunos datos como estos:</p>

<p class="p" id="lets_say_you_h">Let’s say you had some data like this:</p>


      <pre class="programlisting" data-language="javascript" id="var_dataset___id20">var dataset = [
        { apples: 5, oranges: 10, grapes: 22 },
        { apples: 4, oranges: 12, grapes: 28 },
        { apples: 2, oranges: 19, grapes: 32 },
        { apples: 7, oranges: 23, grapes: 35 },
        { apples: 23, oranges: 17, grapes: 43 }
];</pre>
<p class="it">La primera etapa es la de reorganizar esos datos en una array de matrices. Cada serie representa los datos correspondientes a una categoría (por ejemplo, manzanas, naranjas o uvas). Dentro de cada categoría array, que necesita un objeto para cada valor de datos, que a su vez debe contener una <code class="literal">x</code> y un valor de y. La <code class="literal">x</code> en nuestro caso es sólo un número de identificación. La <code class="literal">y</code> es el valor real de los datos:</p>

<p class="p" id="the_first_step_">The first step is to rearrange that data into an array of arrays. Each array represents the data for one category (e.g., apples, oranges, or grapes). Within each category array, you’ll need an object for each data value, which itself must contain an <code class="literal">x</code> and a <code class="literal">y</code> value. The <code class="literal">x</code> in our case is just an ID number. The <code class="literal">y</code> is the actual data value:</p>


      <pre class="programlisting" data-language="javascript" id="var_dataset___id21">var dataset = [
        [
                { x: 0, y: 5 },
                { x: 1, y: 4 },
                { x: 2, y: 2 },
                { x: 3, y: 7 },
                { x: 4, y: 23 }
        ],
        [
                { x: 0, y: 10 },
                { x: 1, y: 12 },
                { x: 2, y: 19 },
                { x: 3, y: 23 },
                { x: 4, y: 17 }
        ],
        [
                { x: 0, y: 22 },
                { x: 1, y: 28 },
                { x: 2, y: 32 },
                { x: 3, y: 35 },
                { x: 4, y: 43 }
        ]
];</pre>
<p class="it">Nuestra base de datos original se ve como en la Figura 11-5 en la consola.</p>
<p class="p" id="our_original_da">Our original <code class="literal">dataset</code> looks like <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch11.html#prestacked_data" title="Figure 11-5. The data before stacking">Figure 11-5</a> in the console.</p>


      <div>

            <img src="/static/wfeBxecqcH-img5.png" alt="The data before stacking"/>
<p class="fig">imagen Figura 11-5. Los datos antes de apilarlas</p>
<p class="fig">Figure 11-5. The data before stacking</p>


      </div>

<p class="p" id="then_we_initial">Then we initialize our stack layout function, and call it on <code class="literal">dataset</code>:</p>

<p class="it">Entonces inicializamos nuestra función de disposición de pila, y lo llamamos el conjunto de datos:</p>
      <pre class="programlisting" data-language="javascript" id="var_stack__d">var stack = d3.layout.stack();
stack(dataset);</pre>


<p class="it">Ahora los datos apilados se muestra en la Figura 11-6.</p>

<p class="p" id="now_the_stacked">Now the stacked data is shown in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch11.html#stacked_data" title="Figure 11-6. The data after stacking">Figure 11-6</a>.</p>


      <div>

            <img src="/static/wfeBxecqcH-img6.png" alt="The data after stacking"/>

<p class="fig">imagen Figura 11-6. Los datos después de apilar</p>
<p class="fig">Figure 11-6. The data after stacking</p>


      </div>
<p class="it">¿Puedes ver la diferencia? En los datos de apilados, cada objeto se le ha dado un valor y0. Este es el valor de línea de base. Observe que el valor y0 línea de base es igual a la suma de todos los valores de y en las categorías anteriores. Por ejemplo, la lectura de izquierda a derecha en la parte superior, y el valor del primer objeto es 5, y su y0 es cero. A la derecha (en la columna de las naranjas), el primer objeto tiene un valor de y de 10, y un y0 de 5. (Aha! Eso es sólo el valor de y del primer objeto!) En el extremo derecho (en la columna de la uva), vemos Ay valor de 22, y un y0 de 15 (que está a sólo 5 + 10).</p>


<p class="p" id="can_you_spot_th">Can you spot the difference? In the stacked data, each object has been given a <code class="literal">y0</code> value. This is the <span class="emphasis"><em>baseline</em></span> value. Notice that the <code class="literal">y0</code> baseline value is equal to the sum of all the <code class="literal">y</code> values in the preceding categories. For example, reading left to right across the top, the first object’s <code class="literal">y</code> value is 5, and its <code class="literal">y0</code> is zero. To the right (in the oranges column), the first object has a <code class="literal">y</code> value of 10, and a <code class="literal">y0</code> of 5. (Aha! That’s just the value of the first object’s <code class="literal">y</code>!) On the far right (in the grapes column), we see a <code class="literal">y</code> value of 22, and a <code class="literal">y0</code> of 15 (which is just 5 + 10).</p>

<p class="it">Para los elementos "apilar" visualmente, ya que pueden hacer referencia a los valores basales del cada objeto de datos, así como su altura. Ver todo el código en 03_stacked_bar.html. (Lo dejo como ejercicio para que usted pueda alinear las pilas contra el eje<code class="literal">x</code>inferior.) Este es el pasaje crítico:</p>

      <p class="p" id="to_stack_elem">To “stack” elements visually, now we can reference each data object’s baseline value as well as its height. See all the code in <span class="emphasis"><em>03_stacked_bar.html</em></span>. (I leave it as an exercise to you to align the stacks against the bottom x-axis.) Here’s the critical excerpt:</p>


      <pre class="programlisting" data-language="javascript" id="var_rects__gro">var rects = groups.selectAll("rect")
        .data(function(d) { return d; })
        .enter()
        .append("rect")
        .attr("x", function(d, i) {
                return xScale(i);
        })
        .attr("y", function(d) {
                return yScale(d.y0);
        })
        .attr("height", function(d) {
                return yScale(d.y);
        })
        .attr("width", xScale.rangeBand());</pre>
<p class="it">Nota cómo para yy altura la referencia d.y0 y dy, respectivamente.</p>

<p class="p" id="note_how_for_y_">Note how for <code class="literal">y</code> and <code class="literal">height</code> we reference <code class="literal">d.y0</code> and <code class="literal">d.y</code>, respectively.</p>


          <h2 class="title">Force Layout</h2>
<h2 class="title">Disposición vigor</h2>
    
<p class="it">Diseños de la fuerza dirigida son los llamados, ya que utilizan simulaciones de fuerzas físicas para organizar los elementos en la pantalla. Podría decirse que son un poco gastada, pero que construyen una gran demostración y apenas se ven tan maldito frío. Todo el mundo quiere aprender a hacer uno, así que vamos a hablar de ello.</p>


<p class="p" id="forcedirected_">Force-directed layouts are so-called because they use simulations of physical <span class="emphasis"><em>forces</em></span> to arrange elements on the screen. Arguably, they are a bit overused, yet they make a great demo and just look <span class="emphasis"><em>so darn cool</em></span>. Everyone wants to learn how to make one, so let’s talk about it.<a id="ix_lflay" class="indexterm" href=""></a><a id="ix_force" class="indexterm" href=""></a></p>

<p class="it">Diseños de la fuerza se utilizan normalmente con datos de la red. En informática, este tipo de conjunto de datos se llama un gráfico. Un gráfico simple es una lista de nodos y bordes. Los nodos son las entidades en el conjunto de datos, y los bordes son las conexiones entre los nodos. Algunos nodos serán conectados por los bordes, y otros no. Los nodos están representados comúnmente como círculos, y los bordes como líneas. Pero, por supuesto, la representación visual depende de usted-D3 solo ayuda a gestionar todos los mecanismos detrás de las escenas.</p>

<p class="p" id="force_layouts_a">Force layouts are typically used with network data. In computer science, this kind of dataset is called a <span class="emphasis"><em>graph</em></span>. A simple graph is a list of <span class="emphasis"><em>nodes</em></span> and <span class="emphasis"><em>edges</em></span>. The nodes are entities in the dataset, and the edges are the <span class="emphasis"><em>connections</em></span> between nodes. Some nodes will be connected by edges, and others won’t. Nodes are commonly represented as circles, and edges as lines. But of course the visual representation is up to you—D3 just helps manage all the mechanics behind the scenes.<a id="id560340" class="indexterm" href=""></a><a id="id560351" class="indexterm" href=""></a><a id="id560356" class="indexterm" href=""></a></p>

<p class="it">La metáfora física aquí es de partículas que se repelen entre sí, sin embargo, también están conectados por resortes. Las fuerzas de repulsión empujan partículas de distancia el uno del otro, evitando la superposición visual, y los resortes evitan que acaba de volar hacia el espacio, manteniendo de ese modo en la pantalla en la que podemos ver.</p>
    
<p class="p" id="the_physical_me">The physical metaphor here is of particles that repel each other, yet are also connected by springs. The repelling forces push particles away from each other, preventing visual overlap, and the springs prevent them from just flying out into space, thereby keeping them on the screen where we can see them.</p>

<p class="it">La figura 11-7 proporciona una vista previa de lo que estamos de codificación hacia.</p>
      <p class="p" id="provides_a_visu"><a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch11.html#force_layouta" title="Figure 11-7. A simple force layout">Figure 11-7</a> provides a visual preview of what we’re coding toward.</p>


<div>

<img src="/static/wfeBxecqcH-img7.png" alt="A simple force layout"/>

<p class="fig">imagen Figura 11-7. Un diseño simple fuerza</p>
<p class="fig">Figure 11-7. A simple force layout</p>


      </div>
<p class="it">Diseño de la fuerza de D3 nos espera proporcionar los nodos y los bordes por separado, como las arrays de objetos. Aquí tenemos un objeto conjunto de datos que contiene dos elementos, nodos y bordes, cada uno de los cuales es en sí una serie de objetos:</p>
<p class="p" id="ds_force_layo">D3’s force layout expects us to provide nodes and edges separately, as arrays of objects. Here we have one <code class="literal">dataset</code> object that contains two elements, <code class="literal">nodes</code> and <code class="literal">edges</code>, each of which is itself an array of objects:</p>

      <pre class="programlisting" data-language="javascript" id="var_dataset___id22">var dataset = {
        nodes: [
                { name: "Adam" },
                { name: "Bob" },
                { name: "Carrie" },
                { name: "Donovan" },
                { name: "Edward" },
                { name: "Felicity" },
                { name: "George" },
                { name: "Hannah" },
                { name: "Iris" },
                { name: "Jerry" }
        ],
        edges: [
                { source: 0, target: 1 },
                { source: 0, target: 2 },
                { source: 0, target: 3 },
                { source: 0, target: 4 },
                { source: 1, target: 5 },
                { source: 2, target: 5 },
                { source: 2, target: 5 },
                { source: 3, target: 4 },
                { source: 5, target: 8 },
                { source: 5, target: 9 },
                { source: 6, target: 7 },
                { source: 7, target: 8 },
                { source: 8, target: 9 }
        ]
};</pre>

<p class="it">Como es habitual en D3, puede almacenar todos los datos que te gusta dentro de estos objetos. Nuestros nodos son simples-sólo nombres de personas. Los bordes contienen dos valores cada uno: un ID de origen y un ID de destino. Estos ID corresponden a los nodos anteriores, por lo que el número de identificación 3 es Donovan, por ejemplo. Si 3 está conectado a 4, a continuación, Donovan está conectado a Edward.</p>

<p class="p" id="as_usual_for_d">As usual for D3, you can store whatever data you like within these objects. Our nodes are simple—just names of people. The edges contain two values each: a source ID and a target ID. These IDs correspond to the nodes above, so ID number 3 is Donovan, for example. If 3 is connected to 4, then Donovan is connected to Edward.</p>

<p class="it">Los datos mostrados son un mínimo para el uso de la disposición de la fuerza. Puede añadir más información, y, de hecho, D3 sí añadir muchos más datos sobre lo que hemos proporcionado, como veremos en un momento.</p>

<p class="p" id="the_data_shown_">The data shown is a bare minimum for using the force layout. You can add more information, and, in fact, D3 will itself add a lot more data to what we’ve provided, as we’ll see in a moment.</p>

<p class="it">Aquí es cómo inicializar un diseño vigor:</p>

<p class="p" id="heres_how_to_i">Here’s how to initialize a force layout:</p>


      <pre class="programlisting" data-language="javascript" id="var_force__d_id1">var force = d3.layout.force()
                     .nodes(dataset.nodes)
                     .links(dataset.edges)
                     .size([w, h])
                     .start();</pre>
<p class="it">Una vez más, esto es sólo el mínimo indispensable. Especificamos los nodos y enlaces a utilizar, el tamaño del espacio disponible, y luego llamar a start () cuando estemos listos para ir.</p>

<p class="p" id="again_this_is_">Again, this is just the bare minimum. We specify the nodes and links to be used, the size of the available space, and then call <code class="literal">start()</code> when we’re ready to go.</p>

<p class="it">Esto genera una fuerza de diseño por defecto, pero el defecto no será ideal para cada conjunto de datos. Como era de esperar, hay todo tipo de opciones de personalización. Ver el wiki de API para todos los detalles morbosos. Aquí, he aumentado la linkDistance (la longitud de las aristas entre los nodos conectados), así como la carga negativa entre los nodos, por lo que se repelen entre sí más. (No es personal, sólo quiero que se propaguen fuera un poco.)</p>

<p class="p" id="this_generates_">This generates a default force layout, but the default won’t be ideal for every dataset. As you would expect, there are all kinds of options for customization. <a class="ulink" href="https://github.com/mbostock/d3/wiki/Force-Layout" target="_top">See the API wiki</a> for all the gory details. Here, I’ve increased the <code class="literal">linkDistance</code> (the length of the edges between connected nodes) as well as the negative <code class="literal">charge</code> between nodes, so they will repel each other more. (It’s not personal; I just want them to spread out a bit.)</p>


      <pre class="programlisting" data-language="javascript" id="var_force__d_id2">var force = d3.layout.force()
                     .nodes(dataset.nodes)
                     .links(dataset.edges)
                     .size([w, h])
                     .linkDistance([50])        // &lt;-- New!
                     .charge([-100])            // &lt;-- New!
                     .start();</pre>

<p class="it">A continuación, creamos una línea de SVG para cada borde:</p>

<p class="p" id="next_we_create">Next, we create an SVG line for each edge:</p>


      <pre class="programlisting" data-language="javascript" id="var_edges__svg">var edges = svg.selectAll("line")
        .data(dataset.edges)
        .enter()
        .append("line")
        .style("stroke", "#ccc")
        .style("stroke-width", 1);</pre>

<p class="it">Nótese que he establecido todas las líneas que tienen el mismo color del trazo y el peso, pero por supuesto se podría establecer esta dinámica en función de los datos (por ejemplo, líneas más gruesas o más oscuros para conexiones "más fuerte", o algún otro valor).</p>

<p class="p" id="note_that_i_set">Note that I set all the lines to have the same stroke color and weight, but of course you could set this dynamically based on data (say, thicker or darker lines for “stronger” connections, or some other value).</p>

<p class="it">A continuación, creamos un círculo SVG para cada nodo:</p>

<p class="p" id="then_we_create">Then, we create an SVG circle for each node:</p>

      <pre class="programlisting" data-language="javascript" id="var_nodes__svg">var nodes = svg.selectAll("circle")
        .data(dataset.nodes)
        .enter()
        .append("circle")
        .attr("r", 10)
        .style("fill", function(d, i) {
                return colors(i);
        })
        .call(force.drag);</pre>

<p class="it">Puedo configurar todos los círculos para tener el mismo radio, pero cada uno obtiene un relleno de color diferente, sólo porque es más bonito de esa manera. Por supuesto, estos valores se podrían establecer dinámicamente, también, para una visualización más útil.</p>
      
<p class="p" id="i_set_all_circl">I set all circles to have the same radius, but each gets a different color fill, just because it’s prettier that way. Of course, these values could be set dynamically, too, for a more useful visualization.</p>

<p class="it">Se dará cuenta de la última línea de código, lo que permitió la interacción de arrastrar y soltar. (Comentario que fuera, y el usuario no será capaz de moverse alrededor de los nodos).</p>

<p class="p" id="youll_notice_t_id2">You’ll notice the last line of code, which enabled drag-and-drop interaction. (Comment that out, and the user won’t be able to move nodes around.)</p>

<p class="it">Por último, tenemos que especificar lo que sucede cuando la disposición de la fuerza "ticks". Sí, estas ticks son diferentes de las ticks de los ejes abordados anteriormente, y sin duda diferente de esos pequeños insectos chupadores de sangre. Simulaciones de física usan la palabra "tick" para referirse al paso de una cierta cantidad de tiempo, como el tic-tac segundero de un reloj. Por ejemplo, si una animación estaban corriendo a 30 cuadros por segundo, usted podría tener un tick representan 1 / 30avo de segundo. Entonces cada vez que la simulación marcada, que vería los cálculos de actualización de movimiento en tiempo real. En algunas aplicaciones, es útil ejecutar las ticks rápido que en tiempo real. Por ejemplo, si estuviera tratando de modelar los efectos del cambio climático en el planeta 50 años a partir de ahora, usted no quiere esperar 50 años para ver los resultados, por lo que sería programar el sistema para marcar en adelante, más rápido que tiempo real.</p>

<p class="p" id="lastly_we_have">Lastly, we have to specify what happens when the force layout “ticks.” Yes, these ticks are different from the axis ticks addressed earlier, and definitely different from those little blood-sucking insects. Physics simulations use the word “tick” to refer to the passage of some amount of time, like the ticking second hand of a clock. For example, if an animation were running at 30 frames per second, you could have one tick represent 1/30th of a second. Then each time the simulation ticked, you’d see the calculations of motion update in real time. In some applications, it’s useful to run ticks faster than actual time. For example, if you were trying to model the effects of climate change on the planet 50 years from now, you wouldn’t want to wait 50 years to see the results, so you’d program the system to tick on ahead, faster than real time.<a id="id562279" class="indexterm" href=""></a></p>

<p class="it">Para nuestros propósitos, lo que necesita saber es que el diseño de la fuerza D3 "ticks" hacia adelante en el tiempo, al igual que cualquier otra simulación física. Con cada tic, la disposición vigor ajusta los valores de posición para cada nodo y el borde de acuerdo con las normas que especificamos cuando el diseño fue inicializado en primer lugar. Para ver este progreso visualmente, necesitamos actualizar los elementos -los asociados líneas y círculos:</p>

<p class="p" id="for_our_purpose_id2">For our purposes, what you need to know is that D3’s force layout “ticks” forward through time, just like every other physics simulation. With each tick, the force layout adjusts the position values for each node and edge according to the rules we specified when the layout was first intialized. To see this progress visually, we need to update the associated elements—the lines and circles:</p>

      <pre class="programlisting" data-language="javascript" id="forceontick">force.on("tick", function() {

edges.attr("x1", function(d) { return d.source.x; })
     .attr("y1", function(d) { return d.source.y; })
     .attr("x2", function(d) { return d.target.x; })
     .attr("y2", function(d) { return d.target.y; });

nodes.attr("cx", function(d) { return d.x; })
     .attr("cy", function(d) { return d.y; });

});</pre>

      <p class="p" id="this_tells_d_">This tells D3, “Okay, every time you tick, take the new x/y values for each line and circle and update them in the DOM.”</p>

<p class="it">Espera un minuto. ¿De dónde estos valores<code class="literal">x</code>/ Y vienen? Sólo habíamos especificado nombres, fuentes, y las metas!</p>

<p class="it">Esto le dice a D3, "Está bien, cada vez que marque, tomar los nuevos valores<code class="literal">x</code>/ Y para cada línea y el círculo y actualizarlos en el DOM".</p>
      <p class="p" id="wait_a_minute_">Wait a minute. Where did these x/y values come from? We had only specified <code class="literal">name</code>s, <code class="literal">source</code>s, and <code class="literal">target</code>s!</p>

<p class="it">D3 calcula esos valores <code class="literal">x/y</code> y les añade a los objetos existentes en nuestra base de datos original (ver Figura 11-8). Vaya por delante y abrir 04_force.html, y escribe datos en la consola. Ampliar cualquier nodo o borde, y verá una gran cantidad de datos adicionales que no proporcionamos. Ahí es donde D3 almacena la información que necesita para seguir ejecutando la simulación física. Con el ( "tick", ...), sólo estamos especificando cómo tomar esas coordenadas y un mapa actualizados ellos a los elementos visuales en el DOM.</p>

<p class="p" id="d_calculated_t">D3 calculated those x/y values and appended them to the existing objects in our original <code class="literal">dataset</code> (see <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch11.html#force_data_added" title="Figure 11-8. The first node in dataset, with lots of supplemental data added by D3">Figure 11-8</a>). Go ahead and open up <span class="emphasis"><em>04_force.html</em></span>, and type <span class="strong"><strong><code class="literal">dataset</code></strong></span> into the console. Expand any node or edge, and you’ll see lots of additional data that we didn’t provide. That’s where D3 stores the information it needs to continue running the physics simulation. With <code class="literal">on("tick", …)</code>, we are just specifying how to take those updated coordinates and map them on to the visual elements in the DOM.</p>



      <div>

            <img src="/static/wfeBxecqcH-img8.png" alt="The first node in dataset, with lots of supplemental data added by D3"/>
<p class="fig">Figura 11-8. El primer nodo en el conjunto de datos, con una gran cantidad de datos suplementarios añadidos por D3</p>
<p class="fig">Figure 11-8. The first node in dataset, with lots of supplemental data added by D3</p>


      </div>
<p class="it">El resultado final es, pues, la hermosa enredo que se muestra en la Figura 11-9.</p>

<p class="p" id="the_final_resul">The final result, then, is the lovely entanglement displayed in <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch11.html#force_layout" title="Figure 11-9. A simple force layout with 10 nodes and 12 edges">Figure 11-9</a>.</p>


      <div>

            <img src="/static/wfeBxecqcH-img9.png" alt="A simple force layout with 10 nodes and 12 edges"/>
<p class="fig">imagen Figura 11-9. Un diseño simple fuerza con 10 nodos y 12 aristas</p>

<p class="fig">Figure 11-9. A simple force layout with 10 nodes and 12 edges</p>

      </div>

<p class="it">Una vez más, se puede ejecutar el código de ti mismo final en 04_force.html.</p>

<p class="p" id="again_you_can_">Again, you can run the final code youself in <span class="emphasis"><em>04_force.html</em></span>.</p>


<p class="it">Tenga en cuenta que cada vez que vuelva a cargar la página, los círculos y las líneas surgen a la vida, el tiempo de descanso en un estado de equilibrio. Pero ese estado final de reposo es diferente cada vez, porque hay un elemento de aleatoriedad de cómo los circuitos entran en la etapa. Esto ilustra la naturaleza impredecible de los diseños basados en la fuerza: podrían ser bastante diferente cada vez que se usan, y que se basan en los datos para proporcionar estructura. Si los datos son más estructurado, es posible obtener un mejor resultado visual.</p>


<p class="p" id="note_that_each_">Note that each time you reload the page, the circles and lines spring to life, eventually resting in a state of equilibrium. But that final state of rest is different every time because there is an element of randomness to how the circles enter the stage. This illustrates the unpredictable nature of force-based layouts: they might be quite different each time you use them, and they rely on the data to provide structure. If your data is more structured, you might get a better visual result.</p>


<p class="it">La interactividad puede ser útil para mejorar nuestra visión de los datos. No me gusta la forma en que los bordes se superponen aquí, así que voy a arrastrar el círculo rosado fuera y alrededor (ver Figura 11-10), a continuación, voy a mover el rojo arriba y hacia la izquierda (véase la figura 11-11) .</p>
      <p class="p" id="interactivity_c">Interactivity can be useful for improving our view of the data. I don’t like how the edges overlap here, so I’ll drag the pink circle out and around (see <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch11.html#force_drag" title="Figure 11-10. Dragging a node to change the arrangement of nodes">Figure 11-10</a>), then I’ll move the red one up and to the left (see <a class="xref" href="http://chimera.labs.oreilly.com/books/1230000000345/ch11.html#force_drag_2" title="Figure 11-11. Dragging some more to untangle nodes">Figure 11-11</a>).</p>


      <div>

            <img src="/static/wfeBxecqcH-img10.png" alt="Dragging a node to change the arrangement of nodes"/>

<p class="fig">Figura 11-10. Al arrastrar un nodo para cambiar la disposición de los nodos</p>
<p class="fig">Figure 11-10. Dragging a node to change the arrangement of nodes</p>


      </div>
      
            <div>

            <img src="/static/wfeBxecqcH-img11.png" alt="Dragging a node to change the arrangement of nodes"/>

      
<p class="fig">Figura 11-11. Al arrastrar un poco más para desenredar los nodos</p>
<p class="fig">Figure 11-11. Dragging some more to untangle nodes</p>


      </div>
<p class="it">Como beneficio adicional, la interactividad física de simulación + = demostración irresistible. No puedo explicarlo, pero es cierto. Por alguna razón, los humanos simplemente les gusta ver las cosas del mundo real replicados en las pantallas.</p>
      <p class="p" id="as_a_bonus_int">As a bonus, interactivity + physics simulation = irresistable demo. I can’t explain it, but it’s true. For some reason, we humans just love seeing real-world things replicated on screens.<a id="id563073" class="indexterm" href=""></a><a id="id563082" class="indexterm" href=""></a><a id="id563092" class="indexterm" href=""></a></p>


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