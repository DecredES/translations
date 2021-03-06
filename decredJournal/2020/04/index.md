# Revista Decred — Abril 2020

![abstract art](./assets/202004.png)

_Imagen: Puentes verticales por @saender_

Lo más destacado de abril:

- Continua la optimización para dcrd, el cual ya es mucho más rápido que las versiones anteriores.
- @moo31337 publicó un PR WIP para el trabajo de la descentralización del gasto en el fondo de tesorería.
- ¡Damos la bienvenida a 6 nuevos contribuidores en los repositorios de Decred en GitHub!
- Éste ha sido un gran mes para las integraciones, con los procesadores de pago de Transak y Metal Pay. Steelbackup (solución de almacenamiento de semillas DCR en metal) también añadieron una nueva opción de presupuesto.
- Los eventos en persona no han podido llevarse a cabo, pero en cambio hay muchos eventos online, ¡Especialmente en LATAM!

## Desarrollo
A menos que se indique lo contrario, el trabajo que se informa aquí tiene el estado "fusionado al master". Significa que el trabajo se completó, revisó e integró en el código fuente en el que los usuarios avanzados pueden construir y ejecutar, pero aún no está disponible en los binarios de lanzamiento para usuarios regulares.

[dcrd](https://github.com/decred/dcrd)
- Se migraron más partes de la base de código de los grandes enteros estándar de Go a tipos de campo especializados, con mejoras de rendimiento significativas
- paquete `schnorr`: se realizaron mejoras en seguridad, pruebas y rendimiento, así como un archivo [README](https://github.com/decred/dcrd/blob/master/dcrec/secp256k1/schnorr/README.md) completo que describe el esquema de firma personalizado basado en Schnorr utilizado en Decred

> Una firma Schnorr es un esquema de firma digital que es conocido por su simplicidad, seguridad demostrable y generación eficiente de firmas cortas. Proporciona muchas ventajas sobre las firmas ECDSA que los hacen ideales para usar con el único inconveniente real de que no están bien estandarizados al momento de escribir este artículo.

Si bien el consenso respalda las firmas de Schnorr, el resto de la infraestructura necesaria para aprovechar al máximo sus beneficios no está bien desarrollada y, por lo tanto, todavía no se utilizan ampliamente. El objetivo es arreglarlo.

Con todo el trabajo reciente, la verificación de firma de ECDSA y Schnorr es aproximadamente un [25% más rápida](https://matrix.to/#/!HEeJkbPRpAqgAwhXWO:decred.org/$15862341309060voZvJ:decred.org) en comparación con v1.5.1.

Muchas optimizaciones en dcrd realizadas en los últimos meses han llevado a un [meme](https://twitter.com/degeri_crypto/status/1248522626210897921) de "sufrimiento por el éxito": los nodos más antiguos ahora piensan que la nueva versión está solicitando demasiados datos demasiado rápido y [prohibiéndolos](https://matrix.to/#/!HEeJkbPRpAqgAwhXWO:decred.org/$158650272611269MJQhM:decred.org). Los parámetros de "tasa de prohibición" deberán ajustarse para reflejar las nuevas velocidades.

El repositorio dcrd ya no está configurado como una bifurcación de [btcd](https://github.com/btcsuite/btcd). Se han agregado tantas características nuevas y se han realizado mejoras generales que todavía hay muy poco código en común entre ellas. Además, una de las razones principales para tener una bifurcación es poder realizar cambios fácilmente. Sin embargo, ese ya no es el caso porque el código es tan diferente que cualquier cambio deseado para dcrd tendría que ser portado efectivamente de todos modos. E incluso entonces, la mayoría de los cambios realizados en btcd simplemente ya no se aplican a dcrd. El "sin bifurcaciones" también elimina la confusión sobre el conteo de bifurcaciones, donde la página dcrd mostró el número de todos los bifurcaciones de btcd (más de 1,500). Ahora muestra 235 bifurcaciones para dcrd y 1,290 para btcd. Finalmente, elimina la molestia y la posibilidad de error cuando presionan "Nueva solicitud de extracción" abriría un PR contra el repositorio btcd ascendente con todos los cambios en la rama maestra de Decred.

La aplicación de línea de comandos `dcrctl` que controla dcrd y dcrwallet se dividió de dcrd en su propio [repositorio](https://github.com/decred/dcrctl) para abordar [problemas](https://github.com/decred/dcrd/issues/2133) de dependencia y mantenimiento.

En progreso:
- se publicó el trabajo de [desarrollo](https://github.com/decred/dcrd/pull/2170) de Descentralizar el gasto de la tesorería para hacerlo más visible y permitir que más personas se unan a la discusión. El trabajo se basa en la [propuesta](https://proposals.decred.org/proposals/c96290a2478d0a1916284438ea2c59a1215fe768a87648d04d45f6b7ecb82c3f), pero agrega cambios significativos a la especificación.

[dcrwallet](https://github.com/decred/dcrwallet):

- se agregó un nuevo comando [`addtransaction`](https://github.com/decred/dcrwallet/pull/1712) que será particularmente útil para el próximo diseño de VSP basado en tickets
- se realizaron correcciones de errores y mantenimiento de código
- dcrwallet ya no es una bifurcación de [btcwallet](https://github.com/btcsuite/btcwallet) por las mismas razones que dcrd y tiene 137 de sus propias bifurcaciones al momento de escribir

En progreso:
- [apoyo](https://github.com/decred/dcrwallet/pull/1714) al gasto descentralizado del Tesoro para la cartera correspondiente al trabajo en dcrd.

[Decrediton](https://github.com/decred/decrediton):
- se realizaron los [primeros](https://github.com/decred/decrediton/pull/2448) [pasos](https://github.com/decred/decrediton/pull/2449) para migrar a componentes funcionales (un [enfoque](https://programmingwithmosh.com/react/react-functional-components/) más nuevo en el marco React; son más fáciles de razonar y probar)
- una nueva acción fue agregada para [abandonar las transacciones](https://github.com/decred/decrediton/pull/2467) que no se extraen o se atascan
- [se comenzó](https://github.com/decred/decrediton/pull/2457) a reutilizar la biblioteca pi-ui para varios componentes con el fin de tener una apariencia consistente en los diferentes productos de Decred
-  se realizaron los primeros [pasos](https://github.com/decred/decrediton/pull/2452) hacia el [soporte CSPP](https://github.com/decred/decrediton/issues/2455)

[Politeia](https://github.com/decred/politeia):

- se agregó un nuevp [método](https://github.com/decred/politeia/pull/1137) para consultar las líneas de pedido de factura que se han facturado a la propuesta
- se ha [separado](https://github.com/decred/politeia/pull/1175) los metadatos fuera de las propuestas de Politeia y las facturas de CMS esto elimina una forma poco inteligente de almacenar el título de la propuesta que se utilizó anteriormente y permite agregar metadatos arbitrarios, incluidos los campos requeridos por las propuestas de RFP
- se realizó parte del trabajo para permitir ver a Politeia [sin javascript](https://github.com/decred/politeiagui/pull/1833)
- se normalizó el [almacenamiento en caché](https://github.com/decred/politeiagui/pull/1844) para los datos de paywall
- [se terminó](https://github.com/decred/politeiagui/pull/1857) la [refactorización](https://github.com/decred/politeiagui/issues/1490) del sistema de gestión del estado.
- se realizó trabajo en la UI para apoyar la propuesta de [RFP](https://github.com/decred/politeiagui/pull/1820)
- se realizaron varios ajustes de UI para el CMS
- se realizaron múltiples correcciones de errores en Politeia y CMS

[dcrstakepool](https://github.com/decred/dcrstakepool):

- se realizaron actualizaciones de dependencia y correcciones de errores

[dcrpool](https://github.com/decred/dcrpool):

- se agregó el [caché](https://github.com/decred/dcrpool/pull/180), que mejoró el flujo de datos (el concentrador ahora introduce nuevos datos en la caché en lugar de la votación de la GUI)
- se añadió paginación en múltiples lugares - esto completa el trabajo en la [UI](https://github.com/decred/dcrpool/issues/146) adecuada proporcionada por los diseñadores
- se configuró la [cuenta](https://github.com/decred/dcrpool/pull/191) para pagar recompensas
- se agregó una GUI para [solicitar un pago](https://github.com/decred/dcrpool/pull/198) manualmente y borrar el saldo restante (útil al salir del grupo)
- se hizo una mayor cobertura en la prueba

[dcrlnd](https://github.com/decred/dcrlnd): En progreso:

- habilitar y probar el [modo SPV](https://github.com/decred/dcrlnd/pull/95) para carteras remotas (consulte [la edición de marzo](202003.md#development) para obtener más información)
- [portabilidad](https://github.com/decred/dcrlnd/pull/99) de cambios upstream de lnd entre v0.9.0-beta y 0.10.0-beta -  se consideraron 139 upstream PRs (más algunos commits no relacionados con los PR ).

[dcrdex](https://github.com/decred/dcrdex):

- se agregó un [notificación](https://github.com/decred/dcrdex/pull/244) del sistema para habilitar las actualizaciones en vivo dentro del navegador GUI
- se agregaron comandos para las cuentas admin dentro del [servidor web](https://github.com/decred/dcrdex/pull/221)
- se agregó[encriptación](https://github.com/decred/dcrdex/pull/259) para las llaves de firma
- se agregaron ajustes [anarquistas](https://github.com/decred/dcrdex/pull/268)
- se completó la [página de mercados](https://github.com/decred/dcrdex/pull/278)
- se agrego [un input seguro](https://github.com/decred/dcrdex/pull/246) hacia los argumentos sensibles de la línea de comandos
- correcciones de errores, refactorización de código, registro y mejoras de prueba

[dcrandroid](https://github.com/decred/dcrandroid):

- se rediseñó la página [principal](https://github.com/decred/dcrandroid/pull/451)
- se añadió un [switch](https://github.com/decred/dcrandroid/pull/461) para ver entre DCR y un equivalente fiat en la página de Enviar
- se añadió la traducción a [francés](https://github.com/decred/dcrandroid/pull/423)
- otros ajustes en la UX y correcciones de errores

[dcrios](https://github.com/raedahgroup/dcrios):

- se añadió soporte [biométrico](https://github.com/raedahgroup/dcrios/pull/613) como autenticación de inicio con Touch ID o Face ID
- se rediseñó la página [inicial](https://github.com/raedahgroup/dcrios/pull/615) y fué [fusionada](https://github.com/raedahgroup/dcrios/pull/628) con la configuración de la cartera.
- se agregó una nueva página de [estadísticas](https://github.com/raedahgroup/dcrios/pull/627) con actualizaciones en [tiempo real](https://github.com/raedahgroup/dcrios/pull/666)
- se agregó un [sonido](https://github.com/raedahgroup/dcrios/pull/667) al crearse un nuevo bloque
- se realizó otros ajustes en la UX y correcciones de errores

[dcrdata](https://github.com/decred/dcrdata):

- se realizaron algunas [mejoras](https://github.com/decred/dcrdata/pull/1690) y una refactorización de la [base de datos](https://github.com/decred/dcrdata/pull/1720) para la gráfica de monedas mixtas
- se agregó un nueva API para consultar la dirección [existente](https://github.com/decred/dcrdata/pull/1714)
- se agregó una API simple para la [circulación](https://github.com/decred/dcrdata/pull/1697) de monedas actual
- se buscó por una transacción [outpoint](https://github.com/decred/dcrdata/pull/1711)
- se realizó una corrección de errores

Guías detalladas sobre cómo [consultar dcrdata](https://stakey.club/en/querying-dcrdata/) y como ejecutar [tu propia instancia](https://stakey.club/en/dcrdata-running-your-own-block-explorer/) del explorador de bloques fueron publicados por @mm en inglés y en
 [Portugués](https://stakey.club/pt/articles/).

[tinydecred](https://github.com/decred/tinydecred):

- se agregaron [formularios y configuraciones](https://github.com/decred/tinydecred/pull/156) necesarios para conectarse a dcrd
- se agregó un soporte básico para lo [filtros GCS](https://github.com/decred/tinydecred/pull/149)
- se agregó una mayor cobertura de prueba en un [crusade](https://github.com/decred/tinydecred/issues/70) para una suite de prueba implacable
- todas las pruebas se han migrado a [pytest](https://github.com/decred/tinydecred/pull/161)
- se impulsó el rendimiento de las cripto primitivas con[Cython](https://github.com/decred/tinydecred/pull/160), reduciendo el tiempo de ejecución de la prueba de 21 a 4 segundos (las pruebas rápidas permiten un desarrollo productivo)

[docs](https://github.com/decred/dcrdocs):

- se [añadió](https://github.com/decred/dcrdocs/pull/1087) un [página](https://docs.decred.org/advanced/mnemonic-seed/) documentando las diferencias entre Decred y las semillas BIP-0039

[decred.org](https://github.com/decred/dcrweb):

- se mejoró el [modo nojs](https://github.com/decred/dcrweb/pull/875)
- exchanges actualizados

Otros:

- la herramienta de [lanzamiento](https://github.com/decred/release) para construir ejecutables reproducibles se movió bajo la organización GitHub decred
- @Checkmate publicó [cálculos](https://github.com/checkmatey/checkonchain/blob/master/research_articles/checkonchain_charts/checkonchain_charts.md) para implementar sus métricas
- GitHub ha hecho que todas las funciones principales sean [gratuitas](https://help.github.com/en/github/getting-started-with-github/faq-about-changes-to-githubs-plans) para todos, lo que incluye repositorios privados para usuarios ilimitados

Estadísticas de actividad de desarrollo para abril: 313 Pull Request activos, 247 fusiones al master completados, 39,000 líneas agregadas y 23,000 líneas eliminadas distribuidas en 16 repositorios. Las contribuciones vinieron de 2-7 desarrolladores por repositorio.

## Comunidad
Bienvenidos a los nuevos contribuidores con código fusionado al master: @jdambron ([dcrandroid](https://github.com/decred/dcrandroid/commits?author=jdambron)), @matthawkins90 ([dcrd](https://github.com/decred/dcrd/commits?author=matthawkins90)), @leRequinNoir ([dcrdata](https://github.com/decred/dcrdata/commits?author=leRequinNoir)), @kevinstl ([dcrdex](https://github.com/decred/dcrdex/commits?author=kevinstl)) y @chillviben ([dcrios](https://github.com/raedahgroup/dcrios/issues?q=is%3Aissue+author%3Achillviben)).

Estadísticas de las redes sociales al 1° de mayo:

- Seguidores en Twitter: 40,570 (-124)
- Suscriptores en Reddit: 9,761 (+1)
- Usuarios en Matrix: 624 (+23)
- Usuarios en Discord: 1,184 (+24)
- Usuarios en Telegram: 2,557 (-50)
- Suscriptores de Youtube: 3,990 (+10)
- Seguidores en Facebook: 3,618 (+12), likes: 3,280 (+7)
- Seguidores en LinkedIn: 774 (+30)
- Estrellas en el repo dcrd en GitHub : 539 (+3), forks: 235 (-1,272) — el pasado conteo de forks incluían todas las bifurcaciones de btcd lo cual el número era engañoso, ahora que se ha eliminado el conteo de esos forks el número corresponde solo a los forks de dcrd

## Gobernanza

En abril, [la tesorería](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx) recibió 13,250 DCR y gastó 17,228 DCR. Con la tasa promedio diaria en abril de $12.34 / DCR, esto es $164K recibidos y $213K gastados. A la tasa diaria promedio en marzo de $13.40, la cifra en USD facturada por el trabajo completado en ese mes es de $231K. Al 3 de mayo, el saldo de la tesorería es de 636,000 DCR (9.17 millones de dólares a $14.42).

En abril se presentaron dos nuevas propuestas, una para una [campaña de marketing de cartelera](https://proposals.decred.org/proposals/bce7bf3cd1f74d571d23ac8a330ddf29a14a547ed0cc9c995f1a97dce733d1e1) la cual fue rechazada con un 17% de aprobación (31% de participación) y otra de [CryptoNoticias](https://proposals.decred.org/proposals/83b59ef5ab40193a86073abbd93cea13ed6d071eecc78918ab5cf98cba7c7a67) para una campaña de marketing de contenido también fue rechazada con una aprobación del 31% y 30% de participación.

Las dos propuestas de marzo votadas este mes también fueron rechazadas. [DCR Comic 2](https://proposals.decred.org/proposals/2f08f8518bc7672069a10ac6461fd9ab341d4a9e4c343fd4a7ec426250f3896f) contó con el apoyo del 49.4% de los tickets que votaron (participación del 19%), mientras que la propuesta [Decred Daily](https://proposals.decred.org/proposals/7d42c6f4bf3059b64789185af615c1df97cb61a379425933be5ff01d074ed4d5) tuvo un 44% de aprobación del 17% de los tickets elegibles que votaron. Ambos no alcanzaron el quórum del 20% de los votos.

Para más detalles sobre esto, vea el [número 30 de Politeia Digest](https://blockcommons.red/politeia-digest/issue030/).

## Red

Hashrate: el hashrate de [abril](https://explorer.dcrdata.org/charts?chart=hashrate&zoom=k8f3rvwm-k9oqhibz&scale=linear&bin=block&axis=time) se abrió a ~ 302 Ph/s y cerró  en ~ 360 Ph / s, tocó fondo a 240 Ph/s y alcanzó un máximo de 470 Ph /s durante todo el mes. [Distribución del hashrate](https://dcrstats.com/pow) del pool a partir del 1 de mayo: UUPool 46%, Poolin 22%, lab.antpool.com 17%, F2Pool 2%, Luxor 2%, BTC.com 1.6%, BeePool 0.12%, CoinMine 0.05%, Suprnova 0.02% y otros ~ 9%. Los números de distribución en los pools son aproximados y no se pueden determinar con precisión.

Staking: el precio promedio del ticket a [30 días](https://dcrstats.com/) fue de 137.8 DCR (-4.1). El [precio](https://explorer.dcrdata.org/charts?chart=ticket-price&zoom=k8f3rvwm-k9oqhibz&bin=window&axis=time&visibility=true-false) varió entre 131.7–142.8 DCR. El monto [bloqueado](https://explorer.dcrdata.org/charts?chart=ticket-pool-value&zoom=k8f3rvwm-k9oqhibz&scale=linear&bin=block&axis=time) fue de 5.62–5.71 millones de DCR, que correspondió al 49.2–50.3% del suministro disponible que [participan](https://explorer.dcrdata.org/charts?chart=stake-participation&zoom=k8f3rvwm-k9oqhibz&scale=linear&bin=block&axis=time) en PoS.
Nodos: a lo largo de [abril](https://charts.dcr.farm/d/000000014/nodes?orgId=1&from=1585699200000&to=1588291200000) hubo un promedio de 131 nodos públicos y 206 nodos totales por dcr.farm. Distribución promedio de versiones para abril: 44% dcrd v1.5.1, 16% dcrd v1.5, 6% dcrd v1.6 dev builds, 5% dcrd v1.5 dev y RC builds, 4% dcrd v1.4, 9% dcrwallet v1.5.1, 2.4% dcrwallet v1.4, 1.4% dcrwallet v1.5.

### Actualizaciones de @Checkmate:
- Sección de Decred en el boletín de [Our Network](https://ournetwork.substack.com/p/our-network-issue-15) ([tweet](https://twitter.com/_Checkmatey_/status/1247649984473894912)). Múltiples métricas basadas en el modelo Stock-to-Flow de @Checkmate, el ingreso de mineros PoW y la investigación de datos de los tickets de @permabullnino, indican que la red está infravalorada.
-	Volumen considerable en la cadena en relación con la valoración de la red, métricas [NVT y RVT](https://twitter.com/_Checkmatey_/status/1252754120345182210).
-	Aumento de los [volúmenes de transacciones](https://twitter.com/_Checkmatey_/status/1255084712386654209) debido al mayor uso de la privacidad.

## Integraciones

[dcr.blue](https://dcr.blue/) anunció que se [cerrará](https://github.com/decred/dcrwebapi/pull/97) en un mensaje enviado a todos los usuarios con un correo electrónico verificado el 20 de abril. Se eliminó de la [lista](https://www.decred.org/vsp/) y Decrediton, pero permanecerá en línea por el resto de 2020. Dado que la vida útil máxima de un ticket es aproximadamente 4,7 meses, esto les da a los usuarios alrededor de 3 meses para dejar de comprar tickets asignados a DCR.Blue. Se recomienda a los usuarios que hagan una copia de seguridad de sus scripts de canje si aún no lo han hecho (hay una copia disponible en la cuenta de VSP) y comiencen a comprar tickets para un VSP diferente. Evite unirse a VSPs demasiado grandes para mantener una distribución saludable y una mejor seguridad para la red. Este es el primer VSP que intenta un "cierre correcto" en lugar de simplemente desaparecer sin previo aviso, como lo han hecho otros VSP en el pasado.

El VSP [decred.raqamiya.net](https://decred.raqamiya.net/) que se [retiró](https://github.com/decred/dcrwebapi/pull/95) de la lista en marzo ahora vuelve a estar operativo y se volvió a [agregar](https://github.com/decred/dcrwebapi/pull/96) a la lista. Al momento de escribir, tiene alrededor de 330 boletos en vivo (0.8%), tiene 4 servidores y presenta una interfaz de usuario personalizada.

Metal Pay [agregó](https://twitter.com/metalpaysme/status/1249745420206686208) [soporte](https://blog.metalpay.com/metal-pay-welcomes-decred/) para DCR en su mercado. Proporciona otro acceso fiat y funciona en la mayoría de los estados de EE. UU. Siguieron el anuncio con [tuits](https://twitter.com/metalpaysme/status/1250424090172612615) sobre Decred.

[Transak](https://global.transak.com/) [anunció](https://twitter.com/transak_finance/status/1256654711412776961) que el intercambio de DCR - EUR, GBP e INR está [disponible](https://global.transak.com/?defaultCryptoCurrency=DCR) en su pasarela de pago criptográfico fiat <>. Los pares de USD llegarán pronto.

Un intercambio instantáneo [SwapSpace](https://swapspace.co/) [agregó](https://twitter.com/SwapSpaceCo/status/1250078395884539906) soporte para Decred.

[Steelbackup](https://steelbackup.com/), una solución de respaldo de semilla física, agregó una [versión ligera](https://twitter.com/steelbackup/status/1248058631523905538) del producto. Actualmente, hay dos tipos de placas de acero: [grabado con láser](https://steelbackup.com/product/decred-laser-engraved/) y [marcado con láser](https://steelbackup.com/product/decred-laser-marked/). El grabado es la solución más robusta ya que se elimina el acero, lo que hace que la rejilla de marcado sea tan permanente como el acero. El producto marcado con láser está marcado con una solución de disulfuro de molibdeno que lo hace resistente a arañazos, ácidos y altas temperaturas (hasta 340 grados C). Los productos están diseñados para ser simples sin partes móviles, los usuarios solo necesitan un punzón central (que se encuentra en una ferretería local. Se incluyen bolsas a prueba de manipulaciones. SteelBackup fue lanzado en febrero de 2020 por @zubair y se envía a todo el mundo.

Advertencia: los autores de la Revista Decred no tienen idea de la confiabilidad de alguno de los servicios anteriores. Haga su propia investigación antes de confiar su información personal o activos a cualquier entidad.

## Alcance

El [canal](https://www.youtube.com/decredchannel) de YouTube de Decred creció en 4 videos nuevos, mientras que los podcasts de Decred in Depth and Rough Consensus publicaron 3 episodios en total (ver [Medios](https://xaur.github.io/decred-news/journal/202004#media) a continuación).

El [canal](https://www.youtube.com/channel/UC73wa2ddXuPWsmenVfeFTYg) Decred Brazil sigue generando contenido activamente. Decred Semanal ("Decred Weekly") publicó 5 nuevos episodios en abril que recibieron ~ 150 vistas en promedio, en comparación con ~ 50 vistas en meses anteriores (probablemente como [resultado](https://matrix.to/#/!kdpEDksmOMNrlMqffD:decred.org/$158896614628001AwmOM:decred.org) de mejores tácticas de distribución). La serie también está disponible en formato de podcast en todas las plataformas principales como [Apple](https://podcasts.apple.com/podcast/decred-brasil/id1451017413) (59 episodios en total), Google, Spotify, [SoundCloud](https://soundcloud.com/decredbrasil) y otros.

En Medium, [Decred Drive](https://twitter.com/decreddrive) sigue ofreciendo actualizaciones semanales agradables, [Decred en Español](https://medium.com/decred-es) está agregando nuevos artículos y traducciones, y [Phoenix Green](https://medium.com/phoenix-green) ha surgido con escritos sobre su viaje criptográfico / Decred.

@ jy-p comentó sobre la emisión de crédito fiduciario y el trabajo remoto en una encuesta de proyectos realizada por [8btc.com](https://news.8btc.com/8btc-interview-cryptos-and-coronavirus-what-we-learned-from-foreign-communities). 8btc es el foro de Bitcoin más antiguo de China.

Los logros de Monde PR para abril:

- creó y lanzó una idea de historia dirigida a inversiones, publicaciones de capital de riesgo y publicaciones tecnológicas
- creó y lanzó una idea de historia dirigida a publicaciones de criptografía y fintech
- creó y lanzó una idea de historia dirigida a publicaciones de finanzas personales
- envió comentarios de portavoces de Decred a 8 historias de noticias
- aseguró una entrevista en los medios con un canal de noticias convencional y 3 preguntas y respuestas por correo electrónico con publicaciones principales y de cifrado

Cobertura de noticias asegurada por Monde PR:

- una pieza de liderazgo de pensamiento en [ValueWalk](https://www.valuewalk.com/2020/04/open-source-response-covid-19/) por @richardred
- un artículo en [Cointelegraph](https://cointelegraph.com/news/harsh-stablecoin-recommendations-from-g-20-are-a-step-in-the-right-direction-but-regulators-need-more-education) con comentarios de @jy-p sobre el futuro de los stablecoins, enlazado a [Investing.com](https://www.investing.com/news/cryptocurrency-news/g20s-harsh-stance-on-stablecoin-is-a-step-forward-but-regulators-have-more-to-learn-2144200) y [Bitcoin News Network](https://www.btcnn.com/harsh-stablecoin-recommendations-from-g-20-are-a-step-in-the-right-direction-but-regulators-need-more-education/)

## Eventos

Asistidos:

- 4 de abril - [Paxful Conversations](https://twitter.com/paxful_LATAM/status/1245066931155148800) - Internet. @elian fue invitado por Paxful LATAM para hablar sobre cómo detectar estafas y qué mirar al investigar los fundamentos de la criptomoneda. No fue una charla directa de Decred pero se mencionó como un ejemplo de buenas prácticas dentro de la industria. El seminario web fue "impulsado por Decred" y fue visto por ~ 70 personas.
- 9 de abril - Hablemos Decred 03 - Internet. @pablito y @elian explicaron el sistema PoS. Esta vez solo hubo 3 espectadores nuevos, aunque se aprendieron algunas lecciones sobre la promoción del evento y la elección del momento óptimo. ([report](https://github.com/decredcommunity/events/blob/master/reports/20200409-hablemosdecred-03-internet.md))
- 16 de abril - [Jalisco Talend Land @ Home](https://www.talent-land.tv/) - Internet. El equipo de Decred presentó un panel titulado "El futuro del dinero y el trabajo remoto" para explorar la intersección del dinero, la tecnología y el trabajo remoto a través de la lente y la experiencia de los contratistas de Decred en LATAM. Compartieron su experiencia trabajando desde Argentina, Colombia y México, y cubrieron los desafíos y oportunidades de trabajar para Decred de forma remota. ([report](https://github.com/decredcommunity/events/blob/master/reports/20200416-talent-land-at-home-internet.md))
- 16 de abril - Hablemos de Criptomonedas - Internet. El seminario web fue organizado conjuntamente con la Universidad Ibero a través de su centro de innovación IDIT. @adcade y @elian hablaron sobre criptomonedas y blockchain a una audiencia de 22 (de 34 registros), en su mayoría estudiantes. ([report](https://github.com/decredcommunity/events/blob/master/reports/20200416-hablemos-de-criptomonedas-internet.md))
- 23 de abril - Hablemos Decred 04 - Internet. @pablito y @elian se centraron en los intercambios y el DEX que Decred está construyendo. Esta vez, la asistencia fue de hasta 15 y el equipo de LATAM continúa explorando las mejores formas de organizar tales eventos. ([report](https://github.com/decredcommunity/events/blob/master/reports/20200423-hablemosdecred-04-internet.md))
- 30 de abril - [Decred Virtual Meetup](https://www.meetup.com/Decred-Australia/events/270252645/) -Internet. @Checkmate presentó sus análisis en cadena BTC y DCR. La grabación se subió en [YouTube](https://www.youtube.com/watch?v=H_COE9A-t3I).

Eventos próximos:

- 12 de mayo - [Decred Foundations en Consensus Distributed](https://next.brella.io/events/consensusdistributed/schedule/118434) (requiere registrarse en brella.io para ver y "asistir") - Internet. Consensus Distributed es el reemplazo remoto de la conferencia anual de Consensus, y Decred es uno de los proyectos que fue invitado a contribuir con una hora de contenido, dividido en 3 segmentos. En Construct, @richardred se registra con los contribuyentes de algunos subproyectos Decred importantes. Con @lukebp en Politeia, @matheusd en dcrlnd, @chappjc y @buck54321 en dcrdex, dcrdata y TinyDecred. El segundo segmento es Trade Secrets, donde @Checkmate dará una introducción rápida a sus 5 métricas en cadena más importantes. Para finalizar, @jy-p presentará una revisión del progreso del año en todos los aspectos principales del proyecto en ChangeLog, seguido de una sesión de preguntas y respuestas en vivo de 10 minutos con Lucas Nuzzi. Posteriormente, el video estará disponible en el sitio web de Coindesk y se subirá a Youtube una versión extendida de Trade Secrets.
- 14 de mayo - [Meetup virtual con BlockchainEx](https://twitter.com/Decred_ES/status/1258905004510973953) - Internet. Decred participará en el panel "¿Qué es la gobernanza descentralizada y las DAO?" coadministrado por @adcade y @caibarrad de Decred, Nadia Alvarez de MakerDAO, Gustavo Segovia de Colony y Jhonny Gomez de BlockchainEx. Este panel se transmitirá en vivo a la comunidad blockchain en Colombia.
- 14 de mayo - [Decred meetup con BlockConf](https://twitter.com/Decred_ES/status/1258165218204618759) - Internet. Esta será una reunión virtual para mostrar la plataforma y un chat antes de la conferencia principal. El equipo dará un resumen de los fundamentos de Decred y los nuevos desarrollos.
- 25 de mayo - [BlockConf](https://blockconf.digital/) - Internet. Decred es un [patrocinador bronce](https://twitter.com/BlockconfD/status/1251194332079697922). El equipo de Decred LATAM ejecutará un stand virtual para que Decred responda las preguntas de los asistentes. Si alguien quiere ayudar a mantener el stand activo en varias zonas horarias durante el evento de 48 horas, comuníquese con @elian.

![Jalisco Talent Land @ Home shot](./assets/talent-land-april-2020.jpg)

_Imagen: No hay escasez de Stakey en LATAM_

## Media

Artículos seleccionados:

- Decred on-chain: Strongest hand market cap + ratio por @PermabullNino ([medium](https://medium.com/@permabullnino/decred-on-chain-strongest-hand-market-cap-ratio-146d6854e1d6))
- Decred market maker monitoring - Phase 1 wrap-up por @richardred ([blockcommons.red](https://blockcommons.red/publication/mm-phase1-wrapup/))
- Our Network issue #15 - featuring Decred updates por @Checkmate ([substack.com](https://ournetwork.substack.com/p/our-network-issue-15))
- Decred governance proposal: Protecting the Treasury por Phoenix Green ([medium](https://medium.com/phoenix-green/decred-governance-proposal-protecting-the-treasury-2bcab84800ad))
- Finance 2.0 por Phoenix Green ([medium](https://medium.com/@kencameron77/finance-2-0-5dea40e4b60e))
- The open-sourced mindset for finance por Phoenix Green ([medium](https://medium.com/@kencameron77/open-sourced-finance-7ce8a3fdb648)) - calls to think collectively and find common grounds, and lists tools to build a community
- 3 things everyone should know about cryptocurrencies por Phoenix Green ([medium](https://medium.com/@kencameron77/3-things-everyone-should-know-about-cryptocurrencies-e38c3db4127b))
- The Bitcoin time machine por Phoenix Green ([medium](https://medium.com/@kencameron77/the-bitcoin-time-machine-29f228656cd3)) - Comparación entre Bitcoin y Decred
- What if Bitcoin had a Treasury? por Ryan Watkins ([messari.io](https://messari.io/article/what-if-bitcoin-had-a-treasury), paywalled)
- Project Rundown interview para Decred por The Capital (former Altcoin Magazine, [medium](https://medium.com/the-capital/project-rundown-interview-with-decred-on-the-capital-8b647919a339))
- Hablemos sobre el proyecto y el trabajo remoto por by @adcade ([medium](https://medium.com/decred-es/hablemos-decred-sobre-el-proyecto-y-sobre-el-trabajo-remoto-e5a2510364ae))
- Artículo sobre la cuarta reunión virtual Decred sobre los CEX y DEX ([es.cointelegraph.com](https://es.cointelegraph.com/news/decred-organizes-virtual-meeting-on-decentralized-exchanges-for-the-spanish-speaking-community))

Traducciones:

- Secrets they missed at DevCon: What it's really like in a working DAO - [en Portugués](https://stakey.club/translated/working-dao/) por @mm.
- Decred Journal March 2020 fue traducida al Árabe (@arij), Chino (@Dominic), Polaco (@kozel), y Español (@francov\_). @kozel está de vuelta en el juego con 4 números traducidos desde diciembre. Las versiones en español abreviadas están disponibles en [Medium](https://medium.com/decred-es/revista-2020/home). ¡Gracias a todos por crear conciencia sobre el proyecto!

Videos:

- DCR 101 - Working for the Decred DAO por @Exitus ([youtube](https://www.youtube.com/watch?Ud4LVhFwL9g))
- Decred bi-weekly news update - April 18th, 2020 por @Exitus ([youtube](https://www.youtube.com/watch?v=3TLeEO8Mz1k))
- Decred Australia virtual meetup - BTC & DCR on-chain analytics event con @Checkmate ([youtube](https://www.youtube.com/watch?v=H_COE9A-t3I))
- El psíquico Andre tiene buenos sentimientos sobre las cosas que suceden, el video trata principalmente de la Reserva Federal, pero sobre el tema de Decred Andre dice "todo bien" ([youtube](https://www.youtube.com/watch?v=ddjelXN5KZs))
- The Federal Reserve in its own words. Protect your wealth, buy Decentralized Credits ([twitter](https://twitter.com/coveryfire7777/status/1246169256020107266))
- DCR 101 - How to stake Decred por @Exitus ([youtube](https://www.youtube.com/watch?v=m5lcm6yttEk))
- Decred price analysis - 17th April 2020 por Brave New Coin ([youtube](https://www.youtube.com/watch?v=Q33i6xK_SPg))

Audio:

- Rough Consensus Ep. 4 - Gold, Bitcoin, and Decred. @mr.black, @Checkmate, y @PermabullNino discuten el estado de los mercados macro y criptográficos en el contexto del colapso de las economías y la QE ilimitada. La conversación considera la naturaleza del dinero sólido y cómo el oro, Bitcoin y Decred representan diferentes áreas del espectro del dinero sólido. ([libsyn](https://roughconsensus.libsyn.com/rough-consensus-4-gold-bitcoin-and-decred))
- Decred in Depth - Round Up 2 con @mr.black, @Checkmate y @PermabullNino. ([libsyn](https://decredindepth.libsyn.com/dcr-round-up-2-with-checkmate-permabull-nio), [youtube](https://www.youtube.com/watch?v=eb_GFdOkjwA), [soundcloud](https://soundcloud.com/decredindepth/dcr-round-up-2-with-checkmate))
- Decred in Depth (ha renunciado a la numeración) - Chris Burniske de Placeholder VC habla sobre desarrollos recientes, por qué Decred es HAS (Hypersecure Adaptable Sustainable), las oportunidades para dcrdex y Politeia para expandir el ecosistema Decred, ¡y mucho más! ([libsyn](https://decredindepth.libsyn.com/chris-burniske-institutional-investment-dcr-as-a-sov-current-events-dcr-custody-solutions), [youtube](https://www.youtube.com/watch?v=Q4wbt0JLA5k), [soundcloud](https://soundcloud.com/decredindepth/chris-burniske-crypto-in-the))

## Discusiones de la comunidad

Publicaciones seleccionadas de Reddit:

- ¡La [publicación](https://www.reddit.com/r/decred/comments/fy493y/decred_journal_march_2020/) de Reddit del Decred Journal fue la más discutida en el subreddit este mes con 42 comentarios!
- La discusión sobre la idea de @bee de agregar información sobre el [motivo del voto](https://github.com/decredcommunity/issues/issues/118) a los votos de Politeia [concluyó](https://www.reddit.com/r/decred/comments/g2ozqc/reason_bits_for_politeia_no_votes_feature_idea/) que su implementación adecuada requiere una solución de privacidad como un esquema de votación a ciegas.
- La [discusión](https://www.reddit.com/r/decred/comments/g5he83/decred_market_maker_monitoring_phase_1_wrapup/) del informe de la fase 1 de creación de mercado especuló sobre la tasa de adopción.
- El hilo de las [perspectivas](https://www.reddit.com/r/decred/comments/g66onn/perspectives/) recolectó 33 comentarios de los cuales muchos son pensamiento de calidad de lectura larga.
- [Decred - Hacerlo diferente](https://www.reddit.com/r/decred/comments/g66msa/decred_challenge_do_different/): Minijuego.
- [La publicación](https://www.reddit.com/r/decred/comments/fyi49j/checkmate_on_twitter_cost_to_launch_a_1hr_double/) analiza la metodología de @Checkmate para comparar el costo de ataque de Decred y otras cadenas.

Debates seleccionados en Twitter:

- @Checkmate [tuiteó](https://twitter.com/_Checkmatey_/status/1248498765113126912) sobre que el costo de ataque de doble gasto en DCR es 54 veces más alto que BTC, lo que estimula mucha discusión.
- @Checkmate [anunció](https://twitter.com/_Checkmatey_/status/1253116008639811585) el lanzamiento de un nuevo proyecto, con un equipo de contribuyentes trabajando en un nuevo sitio Decred on-chain metrics.
- Messari [reflexiona](https://twitter.com/MessariCrypto/status/1255579343973232640) sobre qué pasaría si Bitcoin tuviera a el fondo de tesorería de Decred, y [calcula](https://twitter.com/MessariCrypto/status/1255579345319596033) cuánto hubiera valido si Bitcoin hubiera gastado ~ 23% de sus ingresos mensuales del tesoro y ahorrado el resto.
- @moo31337 [tuiteó](https://twitter.com/marco_peereboom/status/1251174260925779977) acerca de un WIP PR para trabajar en la propuesta de gasto descentralizado del fondo de tesorería, pero más de la mitad de los comentarios estaban realmente preocupados por su próxima aventura culinaria.

![pork](./assets/marco-cooking.jpg)

## Mercados
En abril, DCR cotizaba entre USD 11.08-15.01 / BTC 0.00151-0.00179. La tarifa diaria promedio fue de $12.34.

@richardred escribió un [reporte](https://blockcommons.red/publication/mm-phase1-wrapup/) sobre el desempeño de los creadores de mercado durante el período de su primera [propuesta](https://proposals.decred.org/proposals/2eb7ddb29f151691ba14ac8c54d53f6692c1f5e8fe06244edf7d3c33fb440bd9).

## Noticias externas relevantes

Se produjo [otro](https://www.coindesk.com/dforce-hacker-returns-almost-all-of-stolen-25m-in-crypto) ataque de DeFi, aunque esta vez dForce recuperó la mayor parte de sus $25 millones perdidos del atacante y se reembolsará a los usuarios.

En la red más oscura de la red estable de [PegNet](https://www.coindesk.com/miners-trick-stablecoin-protocol-pegnet-turning-11-into-almost-7m-hoard), los mineros deshonestos convirtieron un saldo pJYP de $11 en un saldo pUSD de 6.7 millones manipulando oráculos de precios con una forma de ataque del 51%. Los atacantes no pudieron liquidar más que una pequeña proporción del pUSD, y posteriormente se acercaron para decir que solo estaban tratando de probar la red con la pluma, y ​​quemaron el pUSD creado mágicamente.

La gente se [pregunta](https://twitter.com/econoar/status/1254063336779444226) por qué ProgPoW está de vuelta en la agenda de desarrolladores de Ethereum Core, y si la imposibilidad de sacudirse significa que hay algo podrido en el gobierno de Ethereum.

El programa de préstamos del Gobierno de los Estados Unidos de $349 mil millones para pequeñas empresas ha generado hasta el momento $10 mil millones en [comisiones](https://www.npr.org/2020/04/22/840678984/small-business-rescue-earned-banks-10-billion-in-fees) para los bancos, del 1% al 5% por cada préstamo procesado, a pesar del muy bajo riesgo que los préstamos representaban para los bancos, considerando que efectivamente los estaban pasando a la Administración de Pequeñas Empresas que garantizó todos los préstamos. ([versión en texto sin formato](https://www.npr.org/2020/04/22/840678984/small-business-rescue-earned-banks-10-billion-in-fees))

La Fundación Maker está sujeta a una [demanda](https://www.coindesk.com/makerdao-users-sue-stablecoin-issuer-following-black-thursday-losses) de los inversionistas que perdieron dinero en Black Thursday.

Ha habido una gran cantidad de [demandas](https://www.theblockcrypto.com/post/60930/top-crypto-exchanges-token-issuers-named-in-friday-barrage-of-u-s-class-action-lawsuits) colectivas presentadas contra criptocambios y emisores de tokens.

El saldo del USDT en las bolsas alcanzó un nuevo ATH de [$1.8 mil millones](https://twitter.com/glassnodealerts/status/1253343292403724294) el 23 de abril, según las alertas de glassnode.

YouTube ha actualizado sus políticas para no permitir nada sobre COVID-19 que vaya en contra de "fuentes autorizadas" como las pautas de la Organización Mundial de la Salud, como se reveló en una [entrevista](https://reclaimthenet.org/youtube-ceo-coronavirus-right-information-misinformation/) con el CEO de YouTube. Si bien YouTube censura videos sobre ciertos temas no es nuevo, hacer que estas decisiones se determinen de manera fluida con referencia a lo que dicen las "fuentes autorizadas", y canalizar deliberadamente el tráfico a esas fuentes, es nuevo.

En una actualización de la historia sobre la venta del dominio .org a una firma de capital privado, ICANN ha votado a favor de [rechazar](https://twitter.com/EFF/status/1256053946289774594) la venta, bloqueándola efectivamente.

## Sobre esta edición

Esta es la Revista Decred número 25. El índice completo, y de todas las traducciones se encuentran [aquí](https://xaur.github.io/decred-news/).

La mayoría de la información de terceros se transmite directamente desde la fuente después de un control mínimo. Los autores de la Revista Decred no tienen la capacidad de verificar todas las reclamaciones. Tenga cuidado con las estafas y haga su propia investigación.

Sus [comentarios](https://github.com/xaur/decred-news/blob/docs/contributing.md#feedback) y [contribuciones](https://github.com/xaur/decred-news/blob/docs/contributing.md) son siempre bienvenidos.

Créditos (orden alfabético):
Escritura y edición: bee, degeri, elian, Exitus, l1ndseymm, pablito, richardred, s_ben, zubair
Revisiones y comentarios: chappjc, davecgh, emiliomann, jholdstock, jrick, lukebp
Imagen del título: saender
