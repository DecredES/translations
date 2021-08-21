Bug en política de los gastos de la tesorería
=============================================

por MATHEUS DEGIOVANI - 25 DE JUNIO DEL 2021

Los pagos de la nueva infraestructura del fondo de la tesorería descentralizada están actualmente bloqueados y se retrasarán hasta que se lleve a cabo una nueva votación para implementar un cambio en las reglas de consenso. Los pagos a los contratistas continuarán a través de la tesorería heredada hasta que se implementen y activen dichos cambios.

*Ningún fondo de la tesorería descentralizada o de la tesorería heredada corre el riesgo de perderse.*

Las únicas consecuencias prácticas de este problema son algunos inconvenientes para los operadores del Sistema de Gestión de Contratistas (CMS) junto a la necesidad de una nueva votación por consenso y la demora para que la nueva tesorería comience a funcionar de manera efectiva. *Todos los fondos de la red* *(incluyendo, pero no limitado a la tesorería) están seguros.*

El problema reside en el control excesivo de la política de gasto máximo. Esta política define el valor máximo que un conjunto de transacciones de gasto de la tesorería se debe incluir en un bloque para que este pueda ser extraído.

Debido a la prueba en mainnet de la transacción extraída de gasto de la tesorería en el [bloque 556,716](https://www.notion.so/2360163cd0c879f0db35514f9456b2c1) el monto máximo que ahora se puede gastar de la cuenta descentralizada durante los próximos meses es aproximadamente 0.15 DCR, que es demasiado bajo para poder cumplir con todas las facturas mensuales en el sistema CMS.

Si bien a ningún equipo de desarrollo disfruta encontrar problemas en el software ya enviado y doblemente en el código de consenso distribuido, debemos resaltar que el modelo de gobierno de Decred y la forma en que se introdujeron las funciones de tesorería descentralizadas funcionaron según lo diseñado para prevenir un problema aún mayor.

-   El plan de migración de la tesorería heredada a la tesorería descentralizada se creó para manejar casos como este.
-   Los pagos a los contratistas continuarán como de costumbre, provenientes de la billetera de la tesorería heredada.
-   No hay riesgos de que la red se bifurque, dado que el correspondiente voto en cadena ya activó las nuevas reglas y todas las versiones anteriores del software ya no siguen en la cadena principal.
-   La cuenta de la tesorería descentralizada todavía está acumulando su recompensa de bloque del 10%.
-   Finalmente, todos los fondos en la billetera de la tesorería heredada aún se encuentran intactos y disponibles para gastar donde finalmente se trasladarán al nuevo sistema de cuenta.

El resto de este documento proporcionará más detalles técnicos sobre el problema: cómo se introdujo, cómo se solucionará y su impacto en la red.

Análisis profundo
-----------------

Para el resto de este documento, asumimos que el lector tiene algunos conocimientos básicos sobre cómo funciona la nueva función de la tesorería descentralizada y cómo se propone, codifica, implementa y se activan los cambios en las reglas de consenso de Decred.

La historia de la política de los gastos en el Código
-----------------------------------------------------

La propuesta inicial de Politeia para la [tesorería descentralizada](https://proposals-archive.decred.org/proposals/c96290a) incluía una disposición para limitar la cantidad total de fondos que podrían retirarse de la tesorería durante un período de tiempo. Para citar parte de la propuesta:

> *`OP_TSPEND` evitará [...] gastar más del valor acumulado de tesorería de este mes + 50%*

*Esto se perfeccionó aún más en algunos comentarios y en general, se denomino "control de la política de gasto máximo".*

La motivación para agregar esta restricción es evitar gastar en exceso el fondo de la tesorería, es decir, evitar retirar demasiado DCR de la cuenta en un corto período de tiempo.

Esto tiene dos aplicaciones principales:

-   Un mecanismo de seguridad y protección de modo que en caso de errores de implementación o compromiso de las claves de la tesorería, la cuenta no se agote demasiado rápido antes de que se pueda abordar el problema.
-   Una política "fiscal" genérica sobre los fondos del tesoro, para que no sea susceptible de ser gastado en exceso por intereses a corto plazo.

Esta restricción se aplicaría a través de reglas de consenso en el software por lo tanto no se podría cambiar sin que se lleve a cabo algún otro proceso de votación y los stakeholders intervengan sí o sí en el asunto.

Es importante tener en cuenta que ninguna propuesta está completamente detallada al nivel requerido por el código de software real e incluso esta restricción aparentemente simple tiene ambigüedad: la cadena de bloques de Decred no tiene el concepto de "mes" y los meses de calendario estándar no se pueden trasladar fácilmente a una ventana en la cadena de bloques, bloques de tamaño fijo. Sin embargo los desarrolladores y los stakeholders asumieron que esta restricción podría implementarse después de haber sido especificada correctamente en términos de primitivas de blockchain.

Sin embargo alrededor de octubre del 2020, durante el desarrollo de la función de la tesorería, se formularon dos objeciones contra esta forma específica de política de gastos:

-   El tesoro ya estaba gastando más de lo que estaba recibiendo a través de la recompensa en bloque debido al tipo de cambio USD / DCR. Cualquier disminución adicional ya haría imposible pagar todas las facturas mensuales de los contratistas.
-   Esta política no es estable durante un período de tiempo prolongado, ya que la recompensa del bloque se reduce constantemente. Seguirlo estrictamente significaría que la tesorería no podría gastar la mayor parte de sus fondos, incluso si hubiera acumulado una gran cantidad de valor ya que los ingresos mensuales serían pequeños.

Por lo tanto se propuso y se discutió un cambio en la política de gastos entre los desarrolladores. La redacción general de esta política se indica en el [código fuente](https://github.com/decred/dcrd/blob/afff2fdbcd4c57ade4f0d13e78ad2d3efaebcdec/blockchain/treasury.go#L651-L655):

> *La suma de los tspends dentro de una ventana de gastos no puede exceder el promedio de los tspends en las N ventanas anteriores además de un aumento del X%.*

Una `ventana` aquí es un número específico de bloques, tal como lo definen algunas constantes en el paquete [chaincfg](https://github.com/decred/dcrd/blob/afff2fdbcd4c57ade4f0d13e78ad2d3efaebcdec/chaincfg/mainnetparams.go#L395-L411). Para mainnet, esto funciona de la siguiente manera:

> *La suma de los gastos dentro de una ventana de 6,912 (aproximadamente 24 días) no puede exceder el promedio de los 41,472 bloques anteriores (aproximadamente 144 días o 4,8 meses de 30 días) además de un aumento del 50%.*

Esta redacción tenía la intención de preservar las características originales de seguridad y política tal como se definen en la propuesta de Politeia, al limitar la tasa a la que los gastos podrían crecer pero aún permitiendo la suficiente flexibilidad para manejar los casos en que el tipo de cambio caiga significativamente o que la tesorería tenga suficiente acumuló en los fondos para que los stakeholders se sintieran cómodos gastando una fracción mayor de ellos.

Debemos reiterar que este no es el único mecanismo por el cual se limita el gasto de la tesorería: además del cheque de gasto máximo, las transacciones de gasto aún están sujetas a ser firmadas por las claves de Politeia y pasan por el proceso de votación en cadena antes de ser incluidas en un bloque por un minero de proof-of-work.

Por lo tanto, se consideró que aunque se trataba de un cambio que se discutió explícitamente en la propuesta, fue considerado un cambio bastante razonable ya que los otros mecanismos estarían vigentes para evitar cualquier retiro excesivo de la cuenta: la política de gastos; Así que se volvió a considerar una protección *adicional,* la más primordial que es la votación en cadena realizada por los stakeholders.

La cantidad de gasto de Bootstrap
---------------------------------

Basado en el control de la política de gasto máximo en el gasto pasado promedio en contraposición al *ingreso* anterior absoluto introduce **un desafío adicional: ¿qué hacer al inicio del nuevo sistema de contabilidad de la tesorería cuando no haya gastos pasados? O de manera más general, cuál debería ser el gasto máximo permitido cuando no hay gastos dentro de la ventana anterior de bloques utilizados como referencia.

Por lo tanto, se introdujo un nuevo parámetro de cadena: el monto de arranque de gasto, que especifica cuánto DCR se puede retirar de la tesorería cuando el historial inmediato no tenga transacciones de gasto.

Para mainnet se eligió que este valor fuera 16 000 DCR, que era un valor cercano al máximo de la cantidad gastada en los meses anteriores, manteniendo la capacidad de la tesorería descentralizada de continuar pagando a los contratistas existentes.

Fue la implementación de esta característica específica lo que provocó que la verificación de la política fallara cuando una transacción de gasto de prueba estuvo presente en el historial inmediato.

Desencadenante del problema
---------------------------

El código relacionado con la cantidad de arranque se puede resumir de la siguiente manera (esta es una sección editada de la función [`maxTreasuryExpenditure ()`](https://github.com/decred/dcrd/blob/afff2fdbcd4c57ade4f0d13e78ad2d3efaebcdec/blockchain/treasury.go#L650) redactada para mayor claridad):

```
policyWindow := b.chainParams.TreasuryVoteInterval *
		b.chainParams.TreasuryVoteIntervalMultiplier *
		b.chainParams.TreasuryExpenditureWindow

	// ...

	// Next, sum up all tspends inside the N prior policy windows. If a
	// given policy window does not have _any_ tspends, it isn't counted
	// towards the average.
	for i := uint64(0); i < b.chainParams.TreasuryExpenditurePolicy && node != nil; i++ {
		var spent int64
		spent, _, node, err = b.sumPastTreasuryExpenditure(node, policyWindow)
		// ...

		if spent > 0 {
			spentPriorWindows += spent
			nbNonEmptyWindows++
		}
	}

	// Calculate the average spent in each window. If there were _zero_
	// prior windows with tspends, fall back to using the bootstrap
	// average.
	var avgSpentPriorWindows int64
	if nbNonEmptyWindows > 0 {
		avgSpentPriorWindows = spentPriorWindows / nbNonEmptyWindows
	} else {
		avgSpentPriorWindows = int64(b.chainParams.TreasuryExpenditureBootstrap)
	}

	//...

```

Tenga en cuenta la última declaración if: si hay al menos una ventana anterior en la que se extrajo una transacción de gasto de la tesorería ("tspend") entonces el promedio utilizado para derivar el límite se calcula como el total gastado en todos los tspends sobre el número de -Ventanas vacías. De lo contrario, se utiliza la cantidad de arranque.

En otras palabras, una sola transacción tspend en el historial reciente de blockchain ya cambia la verificación de gastos de usar la cantidad de arranque al usar la cantidad histórica.

Por lo tanto, cuando la transacción tspend de prueba se publicó y se extrajo en mainnet, gastando un total de 0.1 DCR de la nueva cuenta, el código de verificación de gastos se "bloqueó" para permitir solo un aumento del 50% de esta cantidad.

Si bien las pruebas unitarias se escribieron para afirmar el comportamiento correcto de la verificación de gastos en el límite superior de la operación (es decir cuando un conjunto de transacciones intenta gastar más de lo permitido) ninguna prueba verifica el comportamiento en la operación de límite inferior. Tampoco se realizaron pruebas manuales para este caso particular.

Recuperándose del bug
---------------------

Los efectos resultantes de bloquear la tesorería descentralizada en un nivel tan bajo de gasto posible son los siguientes:

-   El pago de los contratistas durante los próximos meses tendrá que seguir procediendo de la billetera de la tesorería heredada. Esto no tiene ninguna implicación práctica para los contratistas.
-   Los operadores del CMS tendrán un poco más de trabajo por hacer dado que tendrán que crear las transacciones de pago habituales.
-   El funcionamiento de la tesorería de forma descentralizada se retrasará unos meses más.

Si bien estos son efectos desafortunados, no son críticos. En particular cómo se presentó en la sección anterior esta emisión *no se puede* utilizar para retirar fondos adicionales de la tesorería.

También es importante destacar que todos los demás controles de los gastos están intactos. Y que la decisión de realizar un movimiento escalonado de los fondos y no vaciar por completo la billetera de la tesorería heredada también nos brinda mucho espacio para maniobrar en torno a este problema.

Finalmente ahora nos enfrentamos a una decisión sobre cómo recuperarnos de aquí en adelante. Hay dos opciones principales:

-   Esperar unos 4 meses (hasta el bloque 598,188) en donde el tspend de prueba salga de la ventana de la póliza reciente y la tesorería pueda gastar de la cuenta con regularidad para que luego reanude los pagos como está.
-   Realizar una votación en cadena para solucionar este problema.

Siendo *muy* optimista cualquier voto en cadena tomaría al menos 3 meses para escribir, implementar y activar. Por otro lado, simplemente esperar a qué se desbloquee la tesorería para volver a intentarlo no resuelve el problema subyacente y podría hacer que el problema vuelva a suceder.

Dadas esas perspectivas el hecho de que el tipo de cambio ya no es un factor inmediato para decidir el nivel de gasto de la tesorería (en comparación con el monto recibido de la recompensa en bloque) junto al hecho de que la verificación de gastos implementada actualmente fue un cambio explícito de el que se discutió en la propuesta, hemos decidido escribir un cambio en el cheque de gasto máximo implementado actualmente para alinearlo con lo que estaba en la propuesta original y someterlo a votación en cadena.

Este cambio tomará la forma de un [DCP](https://github.com/decred/dcps) junto con el código apropiado para implementarlo que se lanzará en unos días. La votación a favor de este cambio de regla de consenso ocurrirá una vez que se publique una nueva versión de software que implemente esta agenda (muy probablemente también con el cambio explícito de actualización de la versión).

Mejoramientos a futuro
----------------------

Si bien el cambio propuesto para este problema es la restricción de contexto mínima de la propuesta inicial en donde los stakeholders ya han votado a través de Politeia y resuelve la situación inmediata, vale la pena señalar que no aborda la preocupación a largo plazo sobre el uso de la política de gastos en regímenes donde el tipo de cambio USD / DCR es mucho más bajo que el actual o cuando los ingresos generados por la recompensa en bloque son significativamente menores que la tasa de retiro que necesita la tesorería.

Como se demostró imponer restricciones de gasto algorítmicas que sean lo suficientemente flexibles para manejar las operaciones en curso así como los pagos esporádicos de alta variación y al mismo tiempo evitar a los actores maliciosos es un equilibrio delicado para acertar y cualquier solución propuesta puede tener modos de falla sutiles que deberán abordarse.

El trabajo futuro deberá refinar las restricciones de gasto utilizando información sobre los patrones de gasto que surjan a través del uso continuo de la tesorería descentralizada.

Agradecimientos
---------------

Gracias a las siguientes personas que contribuyeron a esta publicación (orden alfabético):

-   Dave Collins (@davecgh)
-   Jake Yocom-Piatt (@jy-p)
-   Jonathan Chappelow (@chappjc)
-   Marco Peereboom (@marcopeereboom)

**Sobre [MATHEUS DEGIOVANI](https://blog.decred.org//authors/matheusd)**

Decred Developer
