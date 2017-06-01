<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    
    <div class="block">

<h3 class="title">SVG Element Tooltips</h3>
<h3 class="title">SVG Elemento de información sobre herramientas</h3>


<p class="it">Para un control más visual sobre su información de herramientas, codificarlos como elementos SVG.</p>
<p class="p">For more visual control over your tooltips, code them as SVG elements.</p>



<p class="it">Como de costumbre, hay muchos enfoques diferentes que se pueden tomar. Voy a sugerir la adición de detectores de eventos, por lo que en cada uno encima del ratón, una nueva etiqueta de valor se crea, y al desplazar el ratón que se destruye. (Otra idea sería pregenerate todas las etiquetas, pero entonces sólo mostrar u ocultar ellas basadas en el estado estacionario del ratón. O simplemente seguir con una etiqueta, sino mostrar u ocultar y cambiar su posición según sea necesario.)</p>
<p class="p">As usual, there are many different approaches you could take.  I’ll suggest adding event listeners, so on each <code class="literal">mouseover</code>, a new value label is created, and on <code class="literal">mouseout</code> it is destroyed.  (Another idea would be to pregenerate all the labels, but then just show or hide them based on mouse hover status.  Or just stick with one label, but show or hide it and change its position as needed.)</p>



<p class="it">Volver a las barras que vamos. Vamos a añadir de nuevo en un detector de eventos por encima del ratón, en el que la primera obtenemos valores<code class="literal">x</code>e y para el elemento actual (esto, recuerda?). Vamos a necesitar esta información para saber dónde colocar la nueva pista, por lo que parece muy bien "en la parte superior de" la barra que está provocando el vuelco del vehículo.</p>
<p class="p">Back to the bars we go.  We’ll add back in a <code class="literal">mouseover</code> event listener, in which we first get the <code class="literal">x</code> and <code class="literal">y</code> values for the current element (<code class="literal">this</code>, remember?).  We’ll need this information to know where to place the new tooltip, so it appears nicely “on top of” the bar that’s triggering the rollover.</p>



<p class="it">Cuando recuperamos esos valores, nos envuelven en parseFloat(), que es una función de JavaScript de "Hey, incluso si esta información es una cadena de texto, por favor, convertirlo a un número de coma flotante para mí".</p>
<p class="p">When we retrieve those values, we wrap them in <code class="literal">parseFloat()</code>, which is a JavaScript function for “Hey, even if this information is a string of text, please convert it to a floating point number for me.”</p>

<pre class="programlisting" data-language="javascript" id="transition_id14">.on("mouseover", function(d) {

//Get this bar's x/y values, then augment for the tooltip
var xPosition = parseFloat(d3.select(this).attr("x")) + xScale.rangeBand() / 2;
var yPosition = parseFloat(d3.select(this).attr("y")) + 14;</pre>


<p class="it">Esa es la parte difícil. Ahora todo lo que hacemos es crear la descripción como un elemento de texto simple, en este caso, pero, por supuesto, se podría añadir un rect de fondo o hacer cualquier otra cosa aquí para el efecto visual:</p>

<p class="p">That’s the hard part.  Now all we do is create the tooltip as a simple <code class="literal">text</code> element, in this case, but of course you could add a background <code class="literal">rect</code> or do anything else here for visual effect:</p>

<pre class="programlisting" data-language="javascript" id="transition_id15">//Create the tooltip label
svg.append("text")
  .attr("id", "tooltip")
  .attr("x", xPosition)
  .attr("y", yPosition)
  .attr("text-anchor", "middle")
  .attr("font-family", "sans-serif")
  .attr("font-size", "11px")
  .attr("font-weight", "bold")
  .attr("fill", "black")
  .text(d);

})</pre>


<p class="it">Sí, esto se basa en nuestro código de etiqueta de valor anterior, sólo tiene que adaptar ligeramente. Tenga en cuenta que la<code class="literal">x</code>y Y. atributos se establecen en los nuevos valores de posición que acaba de calcular, y el contenido de texto real de la etiqueta se establece en d, el dato introducida en la función de detector de eventos.</p>

<p class="p">Yes, this is based on our earlier value label code, simply adapted slightly.  Note that the <code class="literal">x</code> and <code class="literal">y</code> attributes are set to the new position values we just calculated, and the actual text content of the label is set to <code class="literal">d</code>, the datum passed into the event listener function.</p>


<p class="it">También tenga en cuenta que he asignado este elemento siguiente texto una identificación de información sobre herramientas. Esto es por lo que puede seleccionar fácilmente (y borrar!) El elemento cuando hayamos terminado con ella, al desplazar el ratón:
</p>
<p class="p">Also note that I assigned this next <code class="literal">text</code> element an ID of <code class="literal">tooltip</code>.  This is so we can easily select (and delete!) the element when we’re done with it—on <code class="literal">mouseout</code>:</p>

<pre class="programlisting" data-language="javascript" id="transition_id16">.on("mouseout", function() {

//Remove the tooltip
d3.select("#tooltip").remove();

})</pre>


<p class="it">Probar el código en 13_svg_tooltip.html.</p>
<p class="p">Test out the code in 13_svg_tooltip.html.</p>



<p class="it">Como se puede ver en la figura 10-10, usted tiene mucho más control visual al utilizar elementos SVG como información sobre herramientas, pero son un poco más de tiempo para configurar. Y, por supuesto, usted puede conseguir mucho más elegante que este sencillo ejemplo.
</p>
<p class="p">As you can see in <pn>Figure 10-10</pn>, you have much more visual control when using SVG elements as tooltips, but they are a little more time-consuming to set up.  And of course, you can get much fancier than this simple example.</p>



<div>
<img alt="Imagen" src="/static/Fig107.png"/>
<p class="y"> El segundo tipo, ahora en orden descendente</p>


<p class="fig">Figure 10-10. An SVG element tooltip</p>

</div>


<h3 class="title">HTML div Tooltips</h3>






<p class="p">A similar approach can be used with HTML <code class="literal">div</code> elements as tooltips.  You might consider using a <code class="literal">div</code> when:</p>


<ul>


<li class="it">Quiere lograr un efecto visual que no es posible o bien apoyado con SVG (como sombras CSS)</li>
<li class="p">You want to achieve a visual effect that isn’t possible or well-supported with SVG (such as CSS drop shadows)</li>
<li class="it">Es necesaria la información sobre herramientas para extenderse más allá del marco de la imagen SVG
</li>
<li class="p">You need the tooltips to extend beyond the frame of the SVG image</li>

</ul>





<p class="p">See Figures <pn>10-11</pn> and <pn>10-12</pn> for examples. </p>

<div>

<img alt="Imagen" src="/static/Fig107.png"/>
<p class="fig">Figure 10-11. An HTML div tooltip</p>
</div>


<div>

<img alt="Imagen" src="/static/Fig107.png"/>

<p class="fig">Figure 10-12. An HTML div tooltip, overlapping the bounds of the SVG image beneath</p>
</div>


<p class="it">Una vez más, hay muchas maneras de hacer esto, pero me gusta hacer un div oculto en mi HTML que se rellena con el valor de los datos, y se activa no-oculto cuando es disparado. Puede seguir el código final en 14_div_tooltip.html</p>


<p class="p">Again, there are many ways to do this, but I like to make a hidden <code class="literal">div</code> in my HTML that gets populated with the data value, and is then unhidden when triggered.  You can follow along with the final code in <pn class="emphasis"><em>14_div_tooltip.html</em></pn></p>.


<p class="it">El div se podría crear dinámicamente con D3, pero me gusta simplemente escribirlo a mano:
</p>
<p class="p">The <code class="literal">div</code> itself could be created dynamically with D3, but I like to just type it in by hand:</p>


<pre class="programlisting" data-language="javascript" id="transition_id51">


&lt;div id ="tooltip" class="hidden"&gt;</p>
&lt;p&gt;&lt;strong&gt;Important Label Heading&lt;strong&gt;&lt;p&gt;
&lt;p&gt;&lt;span id="value"&gt;100&lt;span&gt;%&lt;p&gt;
&lt;/div&gt;</pre>



<p class="it">Ahora se van a necesitar algunas reglas especiales de estilo CSS:</p>
<p class="p">Now it’s going to need some special CSS styling rules:</p>

<pre class="programlisting" data-language="javascript" id="transition_id21">#tooltip {
        position: absolute;
        width: 200px;
        height: auto;
        padding: 10px;
        background-color: white;
        -webkit-border-radius: 10px;
        -moz-border-radius: 10px;
        border-radius: 10px;
        -webkit-box-shadow: 4px 4px 10px rgba(0, 0, 0, 0.4);
        -moz-box-shadow: 4px 4px 10px rgba(0, 0, 0, 0.4);
        box-shadow: 4px 4px 10px rgba(0, 0, 0, 0.4);
        pointer-events: none;
}

#tooltip.hidden {
        display: none;
}

#tooltip p {
        margin: 0;
        font-family: sans-serif;
        font-size: 16px;
        line-height: 20px;
}</pre>

<p class="it">Tenga en cuenta, en particular, que su posición es absoluta, por lo que podemos controlar exactamente donde debe aparecer en la página. También he añadido algunas esquinas redondeadas de lujo y una gota de sombra. Además, puntero-eventos: Ninguno garantiza que pasar el ratón sobre la propia información de herramienta no se disparará un evento mouseout en las barras, ocultando de esta manera la información sobre herramientas. (Prueba el código sin esta línea, y verá lo que quiero decir.) Por último, cuando la descripción se da una clase oculta, que no se muestra.</p>

<p class="p">Note in particular that its <code class="literal">position</code> is <code class="literal">absolute</code>, so we can control exactly where it should appear on the page.  I’ve also added some fancy rounded corners and a drop shadow.  Plus, <code class="literal">pointer-events: none</code> ensures that mousing over the tooltip itself won’t trigger a <code class="literal">mouseout</code> event on the bars, thereby hiding the tooltip.  (Try the code without this line, and you’ll see what I mean.)  Lastly, when the tooltip is given a class of <pn class="keep-together"><code class="literal">hidden</code></pn>, it is not displayed.</p>




<p class="it">Hice algunas modificaciones a la función <code class="literal">mouseover</code> , por lo que el div queda aproximadamente centrado verticalmente en la barra de disparo. El código revisado ahora también fija la posición izquierda y superior de la descripción según los requisitos de diseño CSS, establece el contenido del texto del pn <code class="literal">#value</code> a D, y entonces ahora que todo está en su lugar, elimina la clase oculta, por lo que la información de herramientas visibles:
El ocultamiento de la descripción de mouseout es mucho más fácil; sólo tiene que añadir a la clase oculta:</p>
<p class="p">I made some modifications to the <code class="literal">mouseover</code> function, so the <code class="literal">div</code> is roughly centered vertically against its triggering bar.  The revised code now also sets the tooltip’s <code class="literal">left</code> and <code class="literal">top</code> position per CSS layout requirements, sets the text content of the <code class="literal">#value</code> pn to <code class="literal">d</code>, and then—now that everything is in place—removes the <code class="literal">hidden</code> class, making the tooltip visible:</p>

<pre class="programlisting" data-language="javascript" id="transition_id22">.on("mouseover", function(d) {

//Get this bar's x/y values, then augment for the tooltip
var xPosition = parseFloat(d3.select(this).attr("x")) + xScale.rangeBand() / 2;
var yPosition = parseFloat(d3.select(this).attr("y")) / 2 + h / 2;

//Update the tooltip position and value
d3.select("#tooltip")
  .style("left", xPosition + "px")
  .style("top", yPosition + "px")
  .select("#value")
  .text(d);

//Show the tooltip
d3.select("#tooltip").classed("hidden", false);

})</pre>

<p class="it">El ocultamiento de la descripción de mouseout es mucho más fácil; sólo tiene que añadir a la clase hidden:</p>

<p class="p">Hiding the tooltip on <code class="literal">mouseout</code> is much easier; simply add on the <code class="literal">hidden</code> class:</p>

<pre class="programlisting" data-language="javascript" id="transition_id23">.on("mouseout", function() {

//Hide the tooltip
d3.select("#tooltip").classed("hidden", true);

})</pre>



<p class="it">El diseño de este sencillo ejemplo funciona bien, pero en una situación del mundo real, el gráfico D3 sería sólo uno de muchos otros elementos de la página. Como usted probablemente sabe, el perfeccionamiento de los diseños de HTML / CSS puede ser un reto, y esta es la mayor molestia de conseguir elementos HTML para interactuar correctamente con un gráfico SVG. Puede ayudar a poner tanto el div información sobre herramientas y el gráfico SVG dentro de un mismo elemento envolvente (como un contenedor div), por lo que a continuación, sólo tiene que preocuparse por las posiciones relativas. D3.mouse puede ser utilizado para obtener las coordenadas del ratón en relación con cualquier otro elemento en la página, y puede ser útil en casos cuando se necesita para posicionar elementos no SVG en relación con el ratón.</p>

<p class="p">The layout of this simple example works well, but in a real-world situation, the D3 chart would be just one of many other elements on the page.  As you probably know, perfecting HTML/CSS layouts can be a challenge, and this is the biggest hassle of getting HTML elements to interact properly with an SVG chart.  It can help to put both the tooltip <code class="literal">div</code> and SVG chart within the same enclosing element (like a container <code class="literal">div</code>), so then you only have to worry about relative positions.  <code class="literal">d3.mouse</code> can be used to get mouse coordinates relative to any other element on the page, and can be useful in cases when you need to position non-SVG elements in relationship to the mouse.</p>

<h3 class="title">Consideration for Touch Devices</h3>
<h3 class="title">Consideraciones para dispositivos</h3>



<p class="it">Los navegadores en dispositivos tales táctiles más populares como iOS y Android dispositivos de forma automática se traducen eventos táctiles en eventos de ratón, con fines de JavaScript. Por lo que un toque en un elemento es interpretado por el navegador como un evento de clic. Esto significa que, en su mayor parte, el código que se hace a mano para las interfaces de ratón también funciona muy bien para las interfaces táctiles.</p>
<p class="p">The browsers on most popular touch devices—such as iOS and Android devices—automatically translate touch events into mouse events, for JavaScript purposes.  So a tap on an element is interpreted by the browser as a <code class="literal">click</code> event.  This means that, for the most part, your code that was crafted for mouse interfaces will also work just fine for touch-based interfaces.</p>



<p class="it">La excepción principal a esto es multitouch, que no es automágicamente manejado por D3. No hay una respuesta fácil sobre cómo manejar las interacciones multitouch todavía, pero hace a D3 realizar un seguimiento de los detalles para usted (aunque le toca a usted decidir cómo usarlos). Ver la referencia de API para d3.touches</p>

<p class="p">The primary exception to this is multitouch, which is not automagically handled by D3.  There’s no easy answer on how to handle multitouch interactions yet, but D3 <pn class="emphasis"><em>does</em></pn> track the touches for you (although it’s up to you to decide how to use them).  See the API reference for d3.touches</p>

<h2 class="title">Moving Forward</h2>
<h3 class="it"> Avanzando</h3>



<p class="it">¡Felicitaciones! Ahora tiene todos los elementos básicos de D3 debajo de su casquillo. Usted es un profesional en el enlace de datos, la generación y elementos de diseño sobre la base de esos datos, la aplicación de las escalas y ejes de dibujo, y la modificación de sus creaciones con nuevos datos, transiciones animadas, y la interactividad. ¿Qué más se puede pedir?</p>
<p class="p">Congratulations!  You now have all the basics of D3 under your cap.  You are a pro at binding data, generating and styling elements based on that data, implementing scales and drawing axes, and modifying your creations with new data, animated transitions, and interactivity.  What more could you ask for?</p>



<p class="it">¿Qué hay de layouts y geomaps? Los dos capítulos siguientes se sumerge en estos temas más avanzados, pero te advierto, sin el mismo nivel de detalle que los capítulos anteriores. Ahora que sabes lo básico, no es necesario explicar cada pequeña cosa. ¡Aquí vamos!</p>
<p class="p">How about layouts and geomaps?  The next two chapters will dive into these more advanced topics, but—be warned—without the same level of detail as the prior chapters.  Now that you know the basics, you don’t need every little thing spelled out. Here we go!</p>


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