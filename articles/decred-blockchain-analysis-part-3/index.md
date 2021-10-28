Análisis de la Blockchain de Decred - Parte 3
=============================================

### Historia de los dos tickets pools

Este informe aplica las agrupaciones de direcciones de todos los tickets en los pools en determinadas alturas del bloque, el objetivo es explorar qué tipo de información se puede resumir sobre la composición de los pools de tickets, preguntas como cuántas entidades operan allí y cuánta actividad está siendo ofuscada por la mezcla. He seleccionado dos bloques y perfilaré los pools de tickets a la altura de cada bloque, además de ver como votan los clusters en staking.

El objetivo es construir una imagen de qué entidades estaban haciendo staking activamente con su DCR con técnicas de agrupación de direcciones disponibles y considerar si la imagen que muestran estas métricas indican algún cambio significativo en el período intermedio. Esto está destinado a ser parte de la construcción de una historia más completa de la blockchain de Decred que vendrá más adelante.

Las alturas de bloque que seleccioné son 485,000 (15 de septiembre del 2020) y 525,000 (1 de febrero del 2021). El período intermedio vio un aumento significativo en el precio de los tickets y un aumento en las tasas de participación en el voto de Politeia, es por eso que seleccioné estas alturas de bloque. Esperaba dar la vuelta al análisis con bastante rapidez, pero a lo largo del camino:

1) se destacó errores importantes en el nuevo código del cluster que escribí
2) me dio una forma de rastrear la fuente de esos errores. Escribí esta aventura en un propio [mini-informe](https://www.blockcommons.red/publication/clustering-deep-dive/), probablemente solo sea de interés para las personas que quieran comprender el cluster y el tipo de problemas que conlleva.

tl; dr aproximadamente el 1% de los tickets aún se están asignando a un clúster que no es real, se une a un operador de VSP y las direcciones de los usuarios de VSP. Todo lo demás parece muy sólido, al menos en la era de Politeia (más abajo).

### ¿Quién está en el pool?

![bufalo](./assets/bufalodcr.jpeg)

Lo que nos interesa aquí es la *gente que compra* y vota con los tickets, pero lo más cerca que podemos llegar a eso es la entidad que controla un cluster de direcciones. Entonces, la primera pregunta que debe hacerse es ¿cuántas entidades diferentes hay en un pool de tickets?

En el bloque 485,000 contó con 22,239 entidades distintas; sin embargo la mayoría (21,262) de estas entidades solo están asociadas con un ticket cada una. Si bien algunas de estas entidades serán usuarios con un solo ticket, los usuarios que participan en la mezcla de Stake Shuffle también se ven así, pero estos pueden controlar muchos más tickets.

Hay una parte del pool de tickets que opera en claro y se puede rastrear y una parte que se mezcla solo se puede considerar en conjunto. Me resulta más fácil tratar estos conjuntos por separado, así que comencemos con el conjunto de tickets mixtos.

**Shuffled Stake** 

19,125 de los 485,000 tickets del bloque se compraron con insumos mixtos (47%) por lo que no hay mucho que decir sobre ellos, excepto sí votaron  y como lo hicieron.

Imagen

**Bloque 485.000 Tickets Mixtos en Votaciones de Politeia (Block 485,000 Mixed Tickets Politeia Voting)**


Estos parecen estar ampliamente en línea con los resultados de la votación de la propuesta, por lo que parece que los tickets mixtos votaron de manera similar a los tickets sin mezclar.

Cada tickets tiene su propio ciclo de vida variable, desde que se compra hasta que se selecciona para votar al azar o vence después de 142 días. Un ticket puede votar en cada propuesta de Politeia que se vota mientras el ticket este en vivo. Al tomar una snapshot del pool de tickets, los tickets serán de diferente edad e historial de votaciones, por lo que he optado por excluir las propuestas para las cuales el conjunto de tickets tenía una elegibilidad muy baja (menos del 5% de los tickets elegibles en comparación con la propuesta para la que tenían el mayor número de tickets) - esto es principalmente para mantener los gráficos legibles. En los gráficos, las barras más altas significan principalmente que la propuesta fue votada cerca del bloque de snapshot, pero al mirar la barra de abstención puede ver qué proporción del pool de tickets mixtos (en esta snapshot) votó de qué manera en las propuestas antes y también después de ese tiempo.
