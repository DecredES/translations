Análisis de la Blockchain de Decred - Parte 3
=============================================

### Historia de los dos tickets pools

Este informe aplica las agrupaciones de direcciones de todos los tickets en los pools en determinadas alturas del bloque, el objetivo es explorar qué tipo de información se puede resumir sobre la composición de los pools de tickets, preguntas como cuántas entidades operan allí y cuánta actividad está siendo ofuscada por la mezcla. He seleccionado dos bloques y perfilaré los pools de tickets a la altura de cada bloque, además de ver como votan los clusters en staking.

El objetivo es construir una imagen de qué entidades estaban haciendo staking activamente con su DCR con técnicas de agrupación de direcciones disponibles y considerar si la imagen que muestran estas métricas indican algún cambio significativo en el período intermedio. Esto está destinado a ser parte de la construcción de una historia más completa de la blockchain de Decred que vendrá más adelante.

Las alturas de bloque que seleccioné son 485,000 (15 de septiembre del 2020) y 525,000 (1 de febrero del 2021). El período intermedio vio un aumento significativo en el precio de los tickets y un aumento en las tasas de participación en el voto de Politeia, es por eso que seleccioné estas alturas de bloque. Esperaba dar la vuelta al análisis con bastante rapidez, pero a lo largo del camino:

1) se destacó errores importantes en el nuevo código del cluster que escribí
2) me dio una forma de rastrear la fuente de esos errores. Escribí esta aventura en un propio [mini-informe](https://www.blockcommons.red/publication/clustering-deep-dive/), probablemente solo sea de interés para las personas que quieran comprender el cluster y el tipo de problemas que conlleva.

tl; dr aproximadamente el 1% de los tickets aún se están asignando a un clúster que no es real, se une a un operador de VSP y las direcciones de los usuarios de VSP. Todo lo demás parece muy sólido, al menos en la era de Politeia (más abajo).
