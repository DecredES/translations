# Revista Decred — Junio 2020

![Ambiente a 3000k](./assets/202006.png) 

Imagen : Ambiente a 3000k por @saender

## Lo más destacado de junio:

- Las aplicaciones para Android e iOS fueron actualizadas a la versión 1.5.
- La implementación de Decred para el nuevo estándar Rosetta de Coinbase fue lanzada, esto va a simplificar el proceso para integrar DCR en cualquier comercio o exchange que use Rosetta.
- @Richardred publicó el primer resultado de su investigación (on-chain-research), también puede ver en la sección de Integraciones la actividad de staking por parte de Kucoin.
- El DEX está listo para un lanzamiento inicial soportando DEXing en mainnet.
- La actividad en Reddit ha incrementado y también han aparecido varios artistas inspirados por Decred en Twitter.

## Carteras móviles V1.5

Después de ~1 año de desarrollo, las carteras para Android e iOS v1.5 se encuentran en [Google Play Store](https://play.google.com/store/apps/details?id=com.decred.dcrandroid.mainnet) y [Apple Store](https://apps.apple.com/us/app/decred-wallet/id1462247643).  Algunos de los cambios realizados:
- Rediseño completo de la interfaz de usuario.
- Soporte para múltiples carteras y carteras en modo lectura (watch-only) que no requiere ingresar claves privadas.
- Se movió la pantalla de confirmación de la frase semilla para simplificar la instalación.

¡Gracias a todos los colaboradores!

Por favor revise el [anuncio completo en Reddit](https://www.reddit.com/r/decred/comments/hc5jut/decred_mobile_wallet_v150_has_been_released_for/) y comparte el [tweet](https://twitter.com/planetdecred/status/1274041667520090112).

## Implementación del Middleware Rosetta

A principios de julio se [lanzó](https://twitter.com/decredproject/status/1279127834137636866) una [implementación](https://community.rosetta-api.org/t/decreds-rosetta-middleware-implementation/79) de la [API de Rosetta](https://www.rosetta-api.org/) para Decred, solo 2 semanas después de que Coinbase [lanzara](https://twitter.com/coinbase/status/1273269255610531841) Rosetta:

> Inicialmente, Coinbase desarrolló Rosetta como el middleware utilizado para las integraciones dentro de su plataforma de forma más segura y sencilla (…)
>
> Para los desarrolladores de nuevos proyectos blockchain, la interfaz de Rosetta hace que sea más fácil garantizar la compatibilidad y puede acelerar drásticamente el tiempo que toman los exchanges para integrar una nueva blockchain o moneda y proteger los fondos de los clientes al garantizar que se cumplan las condiciones de seguridad específicas.
>
> Rosetta facilita la creación de aplicaciones de cadena de bloques, como exploradores, carteras y dapps. En lugar de escribir un análisis personalizado para cada cadena de bloques compatible, las aplicaciones pueden usar la implementación Rosetta de un proyecto de cadena de bloques para leer datos en cadena y construir transacciones en un formato estándar; minimizando el código y el mantenimiento.

Rosetta presenta unos [principios](https://www.rosetta-api.org/docs/principles_introduction.html) de diseño interesantes, [ninguna política de gatekeepers](https://www.rosetta-api.org/docs/no_gatekeepers.html), estrictos requisitos de seguridad para la implementación de [carteras](https://www.rosetta-api.org/docs/wallet_api_introduction.html), soporte para [staking](https://www.rosetta-api.org/docs/staking_contract_support.html) y un conjunto de pruebas para validar las implementaciones. El primer [SDK](https://www.rosetta-api.org/docs/rosetta_sdk_go.html) lanzado es para el lenguaje Go, ya que [se usa mucho](https://github.com/coinbase/rosetta-specifications#user-content-sdks-in-more-languages) en Coinbase.

## Desarrollo
[dcrd](https://github.com/decred/dcrd):
- refactorización en el paquete del rpcserver para simplificar la realización de pruebas
- corrección en la construcción de vistas del mempool con relación a los bloques rechazados (resuelve el problema en el que algunas transacciones en el testnet estaban siendo rechazadas cuando en realidad no debería suceder eso)
- corrección  del servidor del RPC con un JSON
- eliminación de las funciones Encrypt y Decrypt para desalentar su uso y empezar a usar esquemas más modernos de encriptación (p. ej. Cifrados de AEAD)

En progreso:
- indexación asíncrona 

La mayoría de los esfuerzos de Decred en junio se destinaron al trabajo de la descentralización del fondo de tesorería. El pull request está pasando por el proceso de revisión y la realización de pruebas para garantizar su funcionamiento, pero parece que la función está completa. Una vez que haya terminado, seguirá con una propuesta de cambio en Decred.

[dcrwallet](https://github.com/decred/dcrwallet):
- [métodos](https://github.com/decred/dcrwallet/pull/1705) para obtener filtros y bloques no relacionados con los datos de la cartera, útil para las llamadas externas como dcrlnd
- evitar cantidades [poco comunes de CoinJoin](https://github.com/decred/dcrwallet/pull/1751)
- [limitación](https://github.com/decred/dcrwallet/pull/1759) en la cantidad de salidas producidas por el downmixing
- corrección de errores

[Decrediton](https://github.com/decred/decrediton):
- integración de la siguiente parte del [CSPP](https://github.com/decred/decrediton/pull/2475) implementando restricciones de seguridad para cuentas mixtas
- [unificación](https://github.com/decred/decrediton/pull/2468) del procesamiento de transacciones regulares y de staking
- permitir [múltiples pagos](https://github.com/decred/decrediton/pull/2491) pendientes en LN
- creación de un nuevo [componente](https://github.com/decred/decrediton/pull/2510) para los tickets elegibles
- creación de una [ventana](https://github.com/decred/decrediton/pull/2482) que muestre los VSP configurados
- [conversión](https://github.com/decred/decrediton/pull/2537) hacia más componentes funcionales y modulares
- reutilización de más componentes de pi-ui
- ajustes de UI y corrección de errores

En progreso:
- [integración](https://github.com/decred/decrediton/pull/2516) del PoC para el nuevo vspd

[Politeia](https://github.com/decred/politeia)
- implementación de una mejor forma de [almacenar](https://github.com/decred/politeia/pull/1226) los resultados de las votaciones
- [retraso en la carga de los votos en los comentarios](https://github.com/decred/politeia/pull/1219) ya que rara vez se accede a propuestas antiguas
- [unit testing](https://github.com/decred/politeia/pull/1203) al nuevo código del RFP
- función de [cierre de sesión](https://github.com/decred/politeiagui/pull/1903) que elimina la identidad del usuario y los borradores del navegador, este cambio también elimina el uso del correo electrónico como clave de almacenamiento para tener menos datos personales en el almacenamiento local del navegador
- permitir los [enlaces acortados de los tokens](https://github.com/decred/politeiagui/pull/1962)
- correciones mínimas en la [pantalla de vista previa para los cambios realizados](https://github.com/decred/politeiagui/pull/1988)
- [evitar comentarios y envíos de propuestas](https://github.com/decred/politeiagui/pull/1966) durante el proceso de anclaje
- CMS: [vista para las versiones pasadas](https://github.com/decred/politeiagui/pull/1980) de una factura
- CMS: [solicitudes de datos de propuestas a traves de cms.decred.org](https://github.com/decred/politeia/pull/1171) para evitar solicitudes externas que causan problemas de seguridad
- ajuste y correción de errores en el backend e interfaz

En progreso:
- agregar TOTP 2FA
- añadir capacidad a los administradores del CMS para revisar el gasto de las propuestas aprobadas

[La implementación de tlog](https://github.com/decred/politeia/pull/1180) en el backend de politeiad está completo. Los complementos se encuentran en proceso de integración. La funcionalidad de los complementos incluyen: comentarios, me gusta en los comentarios y votos en las propuestas. El siguiente paso será cargar la implementación de tlog con los datos de mainnet existentes y ejecutar pruebas de rendimiento. Es posible que algunas cosas necesiten ser revisadas si se descubre algún problema.

[vspd](https://github.com/decred/vspd)
- [marco de tolerancia](https://github.com/decred/vspd/pull/104) a fallas de conexión al dcrwallet
- [rechazo](https://github.com/decred/vspd/pull/93) de tickets que aún no pueden votar (están inmaduros)
- [firmar](https://github.com/decred/vspd/pull/109) mensajes de error
- creación de una [página inicial para los administradores](https://github.com/decred/vspd/pull/119)
- [mejora](https://github.com/decred/vspd/pull/138) en la interfaz GUI
- múltiples cambios para mejorar la validación en el inicio, manejo de errores, salida, etc

La funcionalidad principal está completa y los desarrolladores están en el proceso de probar a fondo los casos del límite con tickets mixtos / sin mezclar, con / sin el comprador del ticket automático. vspd se ha utilizado para votar en decenas de miles de tickets en testnet.

[dcrpool](https://github.com/decred/dcrpool):
- La versión final v1.1 se [anunció](https://twitter.com/dnldd/status/1280455233945194496) el 7 de julio después de dos candidatos de versión que solucionaron problemas en el RC1. Consulte las [notas de la versión completa](https://github.com/decred/dcrpool/releases/tag/v1.1.0) para obtener más detalles.

[dcrdex](https://github.com/decred/dcrdex):
- agregar en la línea de comandos las siguientes rutas: [cancelar órden](https://github.com/decred/dcrdex/pull/411), [retirar](https://github.com/decred/dcrdex/pull/422) y [cerrar sesión](https://github.com/decred/dcrdex/pull/423)
- [listar cuentas](https://github.com/decred/dcrdex/pull/441) para el administrador del servidor
- IU del navegador del cliente para [agregar servidores DEX adicionales](https://github.com/decred/dcrdex/pull/404)
- [widget](https://github.com/decred/dcrdex/pull/454) para mostrar saldos
- [manejo de mensajes](https://github.com/decred/dcrdex/pull/269) al cancelar un pedido
- [reembolso automático](https://github.com/decred/dcrdex/pull/401) cuando una operación fálla
- [apagado elegante](https://github.com/decred/dcrdex/pull/406) y guardar / cargar su estado
- ocultar [formularios de pedido](https://github.com/decred/dcrdex/pull/353) hasta que se complete el registro
- especificaciones para cubrir [la suspensión de las operaciones y la API de administración](https://github.com/decred/dcrdex/pull/482)
- [pruebas](https://github.com/decred/dcrdex/pull/432) en simnet
- hacer más robustas [las pruebas](https://github.com/decred/dcrdex/pull/435)
- se eliminó el [requisito mínimo de financiar la cuenta para confirmarla](https://github.com/decred/dcrdex/pull/499)
- [manejo y rastreo](https://github.com/decred/dcrdex/issues/361) de las operaciones con potencial a ser interrupidas

Se [fusionaron](https://github.com/decred/dcrdex/pulls?q=is%3Apr+merged%3A2020-06-01..2020-06-30+sort%3Aupdated-asc) un total de 48 PR por parte de 8 contribuyentes, agregando 11K y eliminando 4K líneas de código.

En progreso:
- manejo en la [reanudación](https://github.com/decred/dcrdex/pull/442) de operaciones
- [conversión de los complementos](https://github.com/decred/dcrdex/pull/362) a Go

> El Mainnet en beta será este verano. El plan de desarrollo es hacerlo para fines del segundo trimestre de 2020. Además, la interfaz del navegador del cliente apenas se insinuó en la [propuesta](https://proposals.decred.org/proposals/417607aaedff2942ff3701cdb4eff76637eca4ed7f7ba816e5c0bd2e971602e1) de desarrollo y ampliamos drásticamente el alcance del proyecto para que se vea bien. LTC y el soporte genérico de clones de BTC no formaban parte del apoyo, pero también lo hicimos. También concebimos un nuevo algoritmo basado en compromisos criptográficos de los clientes, cuyas preimágenes se revelan al cierre de la época, y lo reimplementamos por completo a la mitad del proyecto. No es fácil ni rápido, pero también se hace y es una gran mejora con respecto a las especificaciones originales. ([2020–06–01](https://matrix.to/#/!MgQoetFiyjrHAywokv:decred.org/$15910318461825cyXfI:decred.org))

El equipo está trabajando en los problemas restantes de UX y preparándose para una implementación limitada de mainnet en unas pocas semanas.

[dcrandroid](https://github.com/planetdecred/dcrandroid):
- mover el repositorio hacia la organización de PlanetDecred
- traducción al [chino](https://github.com/planetdecred/dcrios/pull/695)
- [corregir varios errores](https://github.com/planetdecred/dcrios/pull/694) en la UI

[godcr](https://github.com/planetdecred/godcr):

godcr es una nueva versión de la cartera SPV de escritorio escrita con [Gio](https://gioui.org/), una herramienta para construir interfaces escrita en GO.  Permitiendo que la cartera este construida 100% con golang, sin la necesidad de un cliente de navegador usando JS, esto hace que tenga un tamaño mucho menor.
El peso del código es de tan solo ~30 MB.

El proyecto con Gio empezó en enero del 2020, pero antes de decidirse por Gio, los desarrolladores construyeron múltiples prototipos de GUI que ahora están archivados en el [antiguo repositorio](https://github.com/raedahgroup/godcr-old). El trabajo para explorar y crear prototipos con este enfoque comenzó en septiembre de 2018.

Los próximos pasos son lanzar una versión de demostración disponible públicamente con funcionalidades básicas de cartera e integrar el nuevo vspd.

[documentación](https://github.com/decred/dcrdocs):
- [agregar](https://docs.decred.org/lightning-network/backups/) [página](https://github.com/decred/dcrdocs/pull/1106) sobre cómo realizar una copia de seguridad a los datos de la red lightning
- listar y enumerar [relatos e historias de contratistas](https://github.com/decred/dcrdocs/pull/1101) en la página de [contribución](https://docs.decred.org/contributing/overview/)

## Comunidad

Damos bienvenida a los nuevos colaboradores con un merge completado en el master:
@svitekpavel ([dcrdocs](https://github.com/decred/dcrdocs/commits?author=svitekpavel)), @Daniel-Leedan ([dcrdocs](https://github.com/decred/dcrdocs/commits?author=Daniel-Leedan)) y @shjackson ([dcrdocs](https://github.com/decred/dcrdocs/commits?author=shjackson)).

Felicidades a los nuevos contratistas aceptados por el Decred Contractor Clearance(DCC):
@ammarooni ([comunidad](https://twitter.com/ammarooni)) y @guilhermemntt ([desarrollo](https://github.com/guilhermemntt)).

Estadísticas de la comunidad a partir del 2 de julio: 

- Seguidores en Twitter: 40,517 (+25)
- Suscriptores en Reddit: 9,854 (+62)
- Usuarios en la sala #general en Matrix: 622 (-33) (56 bots expulsados, +23 usuarios nuevos)
- Usuarios en Discord: 1,288 (+66)
- Usuarios en Telegram: 2,607 (+4)
- Suscriptores en YouTube: 4,110 (+80), vistas: 148K (+4K)
- Seguidores en Facebook: 3,655 (+23), likes: 3,311 (+20)
- Seguidores en LinkedIn: 836 (+26)
- Estrellas en el repositorio dcrd en GitHub: 549 (+6), forks: 241 (+1)

## Gobernanza

En junio, el fondo de tesorería recibió 12,629 DCR y gastó 8,340 DCR. Con la tasa promedio diaria de DCR / USD en junio de $16.05, esto es $203K recibidos y $134K gastados. A la tasa promedio diaria de mayo de $14.11, la cifra en USD facturada por el trabajo completado en ese mes es de $118K. A partir del 1 de julio, el saldo del fondo de la tesorería es de 633,820 DCR (9.08 millones de dólares a $14.32).

Se votaron seis propuestas en junio, 4 aprobadas y 2 rechazadas, con una participación relativamente alta para estas propuestas en comparación con algunas otras propuestas recientes. Las propuestas aprobadas fueron:

- Decred OnChain - A Research and Charting Resource por parte de @Checkmate - 86% de aprobación (38% de participación).
- Decred Latam Marketing and Events Proposal 2 por @elian - 61% de aprobación (41% de participación).
- DCR On-Chain Research: Phase 2 por @PermabullNino — 74% de aprobación (31% de participación).
- Decred Bug Bounty Program: Phase 3 por @degeri — 98% de aprobación (32% de participación). El porcentaje de aprobación ha aumentado en comparación con la fase 1 (90%) y la fase 2 (94%).

La [propuesta](https://proposals.decred.org/proposals/4affceb07f5b8126366e8b73ed3d164ebc010bc6fefba19375c4c2e2b252beb0) de patrocinar un libro (CoinStory) por $500 fue rechazada con un 11.6% de aprobación y un 34% de participación, mientras que la [propuesta](https://proposals.decred.org/proposals/9eaafc20f206776e38642e272233390f351c5562c3835369a558cc7d7e341018) de TV marketing tuvo un 8% de aprobación y un 29% de participación.

El [#32](https://medium.com/decred-es/politeia-digest-32-mayo-23-junio-12-2020-69937842d972) del Politeia Digest tiene más detalles.

En junio se publicó una nueva [propuesta](https://proposals.decred.org/proposals/df11d7ac85061e6a02d6503555e585a1a37fffd82101eeea14670537c951926f) de @ivandecredfan para la producción de contenido en Ruso y se comenzó a votar en julio. @ivandecredfan presentó una [propuesta](https://proposals.decred.org/proposals/92e3f2176b332c1aea5887acd2324c2cd730ec450e563df52ddae9d5927d5d36) similar en febrero que fue rechazada con un 21% de aprobación, pero continuó con su producción de video y recibió algunos comentarios sobre la primera propuesta.

Se ha enviado una propuesta que sugiere elegir un nuevo nombre para el proyecto ("Bitcoin Evolution"). Los administradores de Politeia indicaron que el propietario de la propuesta (@decredinator) debe agregar un presupuesto y un plan de implementación antes de que la propuesta se considere válida para su publicación en el sitio de propuestas. @decredinator [publicó](https://www.reddit.com/r/decred/comments/hh2ult/a_better_name_for_decred_to_broaden_the_reach_of/) la propuesta en Reddit para que la comunidad pueda leerla y contribuir a hacerla realidad. La mayoría de los comentarios no están interesados en la idea y el autor no respondió a ninguno de ellos. @decredinator también ha sido [señalado](https://www.reddit.com/r/decred/comments/hh2ult/a_better_name_for_decred_to_broaden_the_reach_of/fwbfmst/) por enviar spam en varios tweets no relacionados.

Para recibir notificaciones al momento de publicarse una propuesta, puede seguir la cuenta de [@pi_crumbs](https://twitter.com/pi_crumbs) en twitter, o configurar un email de notificaciones en la página de [Politeia](https://proposals.decred.org/).

## Red

Hashrate: el [hashrate](https://explorer.dcrdata.org/charts?chart=hashrate&zoom=kavllavw-kc326nyn&scale=linear&bin=block&axis=time) de junio abrió a ~ 390 Ph/s y cerró a ~ 412 Ph/s, tuvo un mínimo en 280 Ph/s y alcanzó un máximo de 569 Ph/s durante todo el mes. [Distribución del hashrate](https://dcrstats.com/pow) en los pools a partir del 1 de julio (aproximado): UUPool 36%, Poolin 32%, lab.antpool.com 11%, BTC.com 3.4%, Luxor 1.07%, F2Pool 0.86%, BeePool 0.09%, CoinMine 0.04%, Suprnova 0.02% y otros ~ 15%.

Staking: el [precio promedio del ticket](https://dcrstats.com/) a 30 días fue de 139.4 DCR (-2.1). El precio varió entre 135.1–149.8 DCR. [El monto bloqueado por stake](https://explorer.dcrdata.org/charts?chart=ticket-pool-value&zoom=kavllavw-kc326nyn&scale=linear&bin=block&axis=time) fue de 5.63–5.86 millones de DCR, que correspondió al [48.7–50.6%](https://explorer.dcrdata.org/charts?chart=stake-participation&zoom=kavllavw-kc326nyn&scale=linear&bin=block&axis=time) del suministro total en circulación.

Del 29 al 31 de mayo se produjo un aumento inusual del uso del tamaño por bloque (no relacionado con las transacciones del fondo de tesorería) Se extrajeron docenas de [bloques](https://explorer.dcrdata.org/blocks?height=453840&rows=50) casi completos con transacciones de 90–100 KB que consolidaron gran cantidad de pequeñas salidas en 6 salida. El 31 de mayo, la cadena de bloques creció en un [récord](https://explorer.dcrdata.org/charts?chart=block-size&zoom=ikd7pc00-kcl65mo0&bin=day&axis=time) de 13 MB, en comparación con un crecimiento promedio de 4 MB / día. [Parece que un VSP estaba consolidando las tarifas de los tickets](https://matrix.to/#/!MgQoetFiyjrHAywokv:decred.org/$15913552414776FisdN:decred.org). Muchas de las 6 salidas de DCR terminaron en una misma [dirección](https://explorer.dcrdata.org/tx/ef562befa1f8eeee6250d98b6ccb1722b8fba508dd4919d5b85139df9c761e0c) con ~ 240K DCR (~ 3.4M USD, ~ 2% de suministro), que se sabe que están asociadas con un exchange de criptomonedas popular. tl; dr, un operador de VSP envió alrededor de 200 DCR (tarifas de votación pagadas por los usuarios de VSP) a un exchange, usó mucho espacio en bloque porque involucraba miles de pequeños pagos de tarifas asociados con tickets individuales procesados por ese VSP.

Nodos: en [junio](https://charts.dcr.farm/d/000000014/nodes?orgId=1&from=1590969600000&to=1593561600000) hubo un promedio de 126 nodos públicos y 208 nodos por parte de dcr.farm. Distribución promedio por versión en junio: 50% dcrd v1.5.1, 9.5% dcrd v1.5.0, 5.6% dcrd v1.6.0 dev builds, 3.2% dcrd v1.5.0 dev builds, 1.8% dcrd v1.4.0, 9.5% dcrwallet v1. 5.1, 1% dcrwallet v1.5.0, 0.9% dcrwallet v1.4.0 y 18.7% otros.

@Checkmate publicó un [gráfico](https://twitter.com/_Checkmatey_/status/1269825167133306881) que muestra un aumento en el volumen de DCR en la cadena de bloques.

@PermabullNino [tuiteó](https://twitter.com/PermabullNino/status/1278055245050855424) una serie de gráficas actualizadas sobre el pulso en la minería, dificultad, entradas y salidas en los pools de tickets. Ya antes había compartido un [gráfico](https://twitter.com/PermabullNino/status/1272512290814902275) que muestra el Momentum actual en el staking.

@richardred publicó la [primera parte](https://blockcommons.red/post/dcr-on-chain-1/) sobre el análisis de datos en la blockchain de Decred, los aspectos más destacados incluyen:

- 465K de los 840K DCR [pre-minados por los fundadores](https://docs.decred.org/advanced/premine/#bring-up-costs) aún permanecen intactos
- 290K de los 840K DCR repartidos en el [airdrop inicial](https://docs.decred.org/advanced/premine/#airdrop) no se han movido
- ~ 27% de los 345K DCR pagados por el fondo de tesorería a los contratistas siguen intactos desde que los recibieron, ~ 24% de los DCR se encuentran bloqueados en stake, ~ 24% terminó en una dirección de un exchange conocido, ~ 1.7% uso el servicio de mixing
- De ~ 5.8M de DCR ganados por POW, 60% terminó en direcciones asociadas con exchanges, 10% se han bloqueado en stake, el (6%) no se ha gastado y un (24%) se desconoce donde terminaron

El mismo tipo de análisis se publicó con datos nuevos y mejoras en el formato para el [#27](https://ournetwork.substack.com/p/our-network-issue-27) del boletín en Our Network.

## Integraciones

El VSP DecredVoting [anunció](https://www.reddit.com/r/decred/comments/hbofz4/tired_of_keeping_track_of_your_staking_activities/) un nuevo panel de análisis de tickets que muestra las estadísticas de los usuarios sobre sus tickets, incluidas algunas estadísticas específicas para el ticket split que fueron diseñadas por el propio @decreddave y no están disponibles en otros lados.

Hotbit [anunció](https://hotbit.zendesk.com/hc/en-us/articles/360049302534-Hotbit-s-Announcement-Regarding-the-Launch-of-DCR-Investment-Product-and-Current-Deposit-Investment-Plan-on-June-11th-2020-UTC-8-) un producto de inversión de Decred el 11 de junio, con un rendimiento anual del 4,27% y un "período de reembolso (T + 30)". Hay una compra mínima de 100 DCR y parece que la "unidad mínima para el cálculo de intereses en el plan de inversión será de 1 DCR", sea lo que sea que eso signifique.

Tras el [lanzamiento](https://www.kucoin.com/news/en-decred-soft-staking-official-rules) del servicio de staking por parte de KuCoin en marzo de 2020, @richardred ha investigado la actividad asociada con las direcciones relacionadas en KuCoin. Las observaciones sugieren que hasta finales de junio de 2020 KuCoin ha comprado 213 tickets, y 185 de ellos han votado. Los primeros tickets comprados por direcciones que se creen controladas por KuCoin se compraron en diciembre de 2019, varios meses antes de que se anunciara el servicio en febrero, y los clientes se inscribieran automáticamente dentro de las 48 horas posteriores a ese anuncio. Ninguno de estos tickets se ha usado para votar sobre las propuestas en Politeia: KuCoin no participa en la toma de decisiones. Según los informes, los saldos de DCR de los usuarios parecen haber obtenido ~ 0.45% de DCR adicional, considerando que aproximadamente un trimestre ha pasado, esto lo pondría en curso para una tasa anual de aproximadamente ~ 1.8%, que es considerablemente más baja que la tasa proyectada por [dcrdata](https://explorer.dcrdata.org/) (~ 6% al momento de la redacción).

El procesador de pagos [CoinPayments](https://www.coinpayments.net/) eliminó de la lista 37 activos, incluido DCR, luego de una [advertencia](https://twitter.com/CoinPaymentsNET/status/1264645627750649856) en mayo. Después de que algunos de sus usuarios se quejaron de esto, [tuitearon](https://twitter.com/CoinPaymentsNET/status/1268925474052268032) que se debía al bajo volumen.

Advertencia: los autores de la Revista Decred no tienen idea de la confiabilidad de ninguno de los servicios anteriores. Haga su propia investigación antes de confiar su información personal o activos.

## Alcance

@Checkmate tomó la iniciativa en Reddit y comenzó discusiones enfocadas para mejorar el alcance de Decred. La primera publicación fue explorar ideas para una campaña / estrategia de marketing y encontrar usuarios dispuestos a ayudar a ejecutarla. Uno de los resultados es la campaña de hashtag [#DidYouKnowDecred](https://twitter.com/hashtag/DidYouKnowDecred) en Twitter. Esto fue seguido por dos hilos de Scepticism Sunday y dos Forward Thinking Friday diseñados para analizar las debilidades y soluciones a ellos, así como ideas para impulsar a Decred. En total, recopilaron 155 comentarios y fueron algunas de las publicaciones más activas de este mes.

La segunda [propuesta](https://proposals.decred.org/proposals/3c02b677462d6d22d61bf786798e975b38df7a203c2467429d4ec91f75ef0c40) de Latam Marketing and Events fue aprobada, pero apenas cruzó el umbral de aprobación del 60% en las últimas horas de votación. Para abordar casi el 40% de los votos en No, @elian comenzó una [encuesta](https://www.reddit.com/r/decred/comments/gzw6hl/what_are_the_thoughts_of_the_394/) en Reddit pidiendo cualquier comentario para saber qué falta y en qué se puede mejorar.

A principios de julio, Decred Latam publicó un [informe de actividades](https://www.reddit.com/r/decred/comments/hn4sve/activities_report_decred_en_espa%C3%B1ol_proposal_2/) para el primer mes de la nueva propuesta.

Los logros de Monde PR para junio:

- creó y lanzó dos ideas de historias para publicaciones financieras, empresariales y tecnológicas

- obtuvo dos Q&As por correo electrónico con publicaciones criptográficas

Cobertura de noticias por parte de Monde PR:

- un artículo en [Cointelegraph](https://cointelegraph.com/news/bitcoin-still-faces-on-chain-scaling-trouble-ahead-decred-co-founder-says) con comentarios de @jy-p sobre la escalabilidad de Bitcoin
- un artículo en [Cointelegraph](https://cointelegraph.com/news/decred-co-founder-cbdcs-can-facilitate-crony-capitalism) con comentarios de @jy-p sobre la aparición de las CBDC, distribuido a 7 medios de comunicación
- un artículo en [Cointelegraph](https://cointelegraph.com/news/decred-co-founder-calls-paypal-and-crypto-an-odd-combination) con comentarios de @jy-p sobre los rumores de que PayPal aceptará criptomonedas. También se incluyó como noticia principal en Holder’s Digest en [Cointelegraph](https://cointelegraph.com/news/paypal-crypto-rumors-rip-wirecard-telegram-settles-hodlers-digest-june-2228), distribuido en 5 medios de comunicación

Se [publicó](https://github.com/decredcommunity/pr/blob/release/monde-pr-media-coverage.csv) en GitHub una hoja de cálculo de toda la cobertura de los medios por parte de Monde PR desde febrero de 2020.

## Eventos

Atendidos:

- 11 de junio — [Decred Virtual Meetup](https://www.meetup.com/es/Decred-Australia/events/271159615/) — Internet. Organizado por @DecredAustralia, esta fue una segunda entrega del análisis en cadena de @Checkmate para BTC y DCR. ([video](https://www.youtube.com/watch?v=HbquQIv9EYw))
- 25 de junio — [Criptotips con Lorena](https://twitter.com/bitcoinemb/status/1276289966440681473) — Internet. @elian habló sobre las estafas criptográficas en este evento organizado por el Bitcoin Embassy Bar (Ciudad de México). ([video](https://www.youtube.com/watch?v=Bxdxzs6Bgpw))
- 25 de junio — [Hablemos Decred 6](https://twitter.com/Decred_ES/status/1275164449448607748) — Internet. @pablito dio una introducción a Git y GitHub en español como parte de la estrategia del equipo de Latam para crear contenido orientado a desarrolladores. ([video](https://www.youtube.com/watch?v=4b0xYYk6xlY))
- 30 de junio — [Decred Webinar](https://www.meetup.com/es/BlockchainMelbourne/events/271516517/) — Internet. @eSizeDave, @richardred, @elian, @mrbulb and @degeri discutieron "Sociología, el futuro del trabajo y la alineación de incentivos" junto con Ellie Rennie y el Dr. Julian Waters-Lynch de la Universidad RMIT. Organizado por Decred Australia. ([video](https://www.youtube.com/watch?v=1dcHwap7xHQ))

Próximos eventos:

- 11 de julio — [Campus Party](https://reboot-the-world.campus-party.org/) — Internet. La comunidad brasileña de Decred tendrá 3 oradores. Rafaela Romano hablará sobre la descentralización en criptomonedas en el escenario Living Better con el título "Monetization via Blockchain". Otros dos oradores serán confirmados pronto.


## Media

Artículos seleccionados:

- Decred blockchain analysis part 1 por @richardred ([blog.decred.org](https://blog.decred.org/2020/06/08/Decred-blockchain-analysis-Part-1/))
- Decred On-chain: Realised cap, MVRV ratio and gradient oscillators por @Checkmate ([medium](https://medium.com/decred/decred-on-chain-realised-cap-mvrv-ratio-and-gradient-oscillators-a36ed2cc8182))
- Why we need Decred: An inclusive approach to sound money por @ammarooni ([medium](https://medium.com/@Ammarooni/why-we-need-decred-an-inclusive-approach-to-sound-money-db2f990c107b))
- The Decred node or: How I learned to stop worrying and love the command line por @kozel ([primera parte](https://medium.com/@artikozel/the-decred-node-or-how-i-learned-to-stop-worrying-and-love-the-command-line-part-one-1eca9420a1b2), [segunda parte](https://medium.com/@artikozel/the-decred-node-or-how-i-learned-to-stop-worrying-and-love-the-command-line-part-two-e629b8579ce2))
- BTC, ETH y DCR son parte de la mayor revolución económica y tecnológica de nuestra generación por Fernando Quirós ([es.cointelegraph.com](https://es.cointelegraph.com/news/elian-huesca-btc-eth-and-decred-are-part-of-the-greatest-technological-and-economic-revolution-of-our-generation)) - entrevista con @elian

Traducciones:

- Una forma más privada de hacer staking: en [árabe](https://insaf01.github.io/decred-arabic/articles/a-more-private-way-to-stake.html) por @arij y en [español](https://medium.com/decred-es/una-forma-m%C3%A1s-privada-de-hacer-staking-en-dcr-36785ad54a47) por @francov_.
- [Decred en Español](https://medium.com/decred-es) tiene un mes completo del [Decred Drive](https://medium.com/decred-es/decred-drive-spanish/home) por @francov_ y un [nuevo número](https://medium.com/decred-es/politeia-digest-32-mayo-23-junio-12-2020-69937842d972) del Politeia Digest por @pablito.
- @ivandecredfan tradujo [5 artículos](https://medium.com/@ivandecredfan) y [3 videos](https://www.youtube.com/channel/UCFjXbEDeyhhj2bH2t_eGKGA/videos) al ruso.
- Tutorial de configuración de un nodo completo y configuración en Tor para el Raspberry Pi [2020] - en [chino](https://github.com/DominicTing/decred-ZH-translations/blob/master/%E6%A0%91%E8%8E%93%E6%B4%BE%E8%BE%85%E5%8A%A9%E5%AE%89%E8%A3%85%E8%84%9A%E6%9C%AC.md) por @Dominic.
- El Decred Journal edición de mayo 2020 se tradujo al árabe (@arij), chino (@Dominic) y el español (@francov_). ¡Gracias a todos por [traducir](https://xaur.github.io/decred-news/) el DJ durante tantos meses!

Videos:

- La cuenta de @Bitcoin tuiteó un video con citas sobre la capacidad infinita de la Reserva Federal para imprimir dinero con adornos por parte de @Exitus, incluida una mención de **Decentralized Credits** al final. El tweet fue bien recibido, con 41K vistas, ~ 900 me gusta y ~ 300 retweets. ([twitter](https://twitter.com/Bitcoin/status/1269313539056922624))
- Decred fue mencionado en el programa Good Morning Crypto de Ivan on Tech ([youtube](https://www.youtube.com/watch?v=JZhl2Atm4VI&t=42m50s), a las 42:50). El video tiene 24K vistas. Gracias a Steve de boo por dejar la pregunta en el chat de transmisión en vivo: ¡un buen ejemplo de trabajo de divulgación de calidad!
- Animación - Stakey awakens ([youtube](https://www.youtube.com/watch?v=LHgGyoDcFPI))
- Actualizaciones de noticias de Decred quincenales ([10](https://www.youtube.com/watch?v=INKSkBpCT_0) y [23](https://www.youtube.com/watch?v=4GqdgsgUX7c) de junio) por @Exitus
- Tutorial de configuración de un nodo completo y configuración en Tor para el Raspberry Pi por @Exitus ([youtube](https://www.youtube.com/watch?v=B-5O_GBcbV0))
- El canal Decred Society de Phoenix Green agregó 7 nuevos videos [crypto society](https://www.youtube.com/watch?v=zM4dfmPYXfo), [Decred and the 21 million crypto market](https://www.youtube.com/watch?v=yhEAXTJHr3o), [Decred and why 21 million is enough by design](https://www.youtube.com/watch?v=0b241mW8Yto), [Decred and the divisive nature of forks](https://www.youtube.com/watch?v=PZ4aAgz2JcM), [Peer to peer payments with Decred](https://www.youtube.com/watch?v=0VjKIHCXD50), [The Decred treasury and a self funded future](https://www.youtube.com/watch?v=-1zmojjvGtg), y [Get a strategy or get wrecked](https://www.youtube.com/watch?v=R1F_GVj76Qw).
- Decred Australia Virtual Meetup #2 Feat. On-Chain Analyst Checkmate ([youtube](https://www.youtube.com/watch?v=HbquQIv9EYw))

> Lo único que detiene a Decred en mi sincera opinión es que más personas inventen formas creativas de gritar al respecto. Es todo lo que esto necesita. Porque una vez que obtienes el nivel de atención adecuada, los fundamentos hablan por sí mismos.

Los videos de Decred ahora también se publican en [BitChute](https://www.bitchute.com/channel/decred/) como alternativa en caso de que algo le pase al canal de YouTube. Este es un buen momento ya que, como se esperaba anteriormente, YouTube [eliminó](https://cointelegraph.com/news/youtubes-algorithm-is-punishing-crypto-content-and-no-one-knows-why) varios videos cripto.

Audio:

- Decred in Depth 26 — DCR use cases and growth con @Checkmate, @akinsawyerr y @mrbulb ([libsyn](https://decredindepth.libsyn.com/akin-checkmate-mr-bulb-dcr-use-case-growth))
- Decred in Depth 27 — Theft by another name con @jy-p ([libsyn](https://decredindepth.libsyn.com/jake-yocom-piatt-theft-by-another-name))
- Rough Consensus 7 — The rigged game ([libsyn](https://roughconsensus.libsyn.com/episode-7-the-rigged-game)) — @mr.black, @Checkmate y @PermabullNino discuten sobre el estado actual de la unión global con el aumento de los disturbios sociales, la recuperación en forma de V y las manipulaciones en el mercado
- Rough Consensus 8 — Talking macro con Ammar ([libsyn](https://roughconsensus.libsyn.com/episode-8-talking-macro-with-ammar)) — Ammar se une al escuadrón spidey para discutir la inflación, la deflación, las tesis de criptomonedas y las inversiones
- Zach Segal (Jefe de listados en Coinbase) ha mencionado a Decred como un proyecto interesante en el podcast de Trading Places ([spotify](https://open.spotify.com/episode/7BkEEDgSDPU1XQsmveksgv), [clip](https://open.spotify.com/episode/7BkEEDgSDPU1XQsmveksgv))

Hay un aumento en [las obras de arte](https://twitter.com/_Checkmatey_/status/1278972757796159489) relacionadas con Decred publicadas este mes. @OfficialCryptos impresionó a la gente con un [Decred Dragon](https://twitter.com/OfficialCryptos/status/1273926304027508738) (que podría ser el lagarto blindado mencionado por Murad en [un podcast](https://www.youtube.com/watch?v=XkvcdjSH0c0&t=50m24s)), un [unicornio](https://twitter.com/OfficialCryptos/status/1275426618610196480) y una [maquina de perforación](https://twitter.com/OfficialCryptos/status/1275507751511371780) btcsuite. @aithzakaria1 publicó una [ciudad digital](https://twitter.com/aithzakaria1/status/1277109552857710592), un [transbordador](https://twitter.com/aithzakaria1/status/1277472194256347137) y otras imágenes en su Twitter. @AGNFAB [anunció](https://twitter.com/AGNFAB1/status/1271157067097792514) que algunas de sus obras de arte estarán disponibles exclusivamente en [descentralizedboutique.com](https://decentralizedboutique.com/?product_cat=art), una nueva tienda que vende joyas y obras de arte relacionadas con la criptografía (incluido DCR).

## Discusiones en la comunidad

Noticias en los medios de comunicación:

El servidor de [Discord](https://discord.com/invite/GJ2GXfz) en Decred se ha reestructurado y los canales se han agrupado en 3 categorías: canales exclusivos de Discord para una experiencia más informal en comparación con Matrix (donde muchas salas son oficinas virtuales para coordinar el trabajo), canales de solo lectura conectados a Matrix y salas con un puente entre ambos lados #decred-101, #proposals, #support, #ticket-splitting y #trading.

Se creó un nuevo canal [DecredSupport](https://t.me/DecredSupport) en Telegram y se conectó a la sala #support en Matrix.

Los desarrolladores de Matrix [lanzaron](https://matrix.org/blog/2020/06/02/introducing-p-2-p-matrix/) una versión actualizada del prototipo de cliente entre pares que permite a los usuarios tomar más control de sus datos.

Publicaciones en Reddit:

- La [publicación](https://www.reddit.com/r/decred/comments/hbb3iz/decred_grassroots_marketing_campaign/) más discutida del mes fue por parte de @Checkmate, resumiendo una serie de iniciativas de marketing para la discusión y para reclutar participantes.

- Forward Thinking Friday [18 de junio](https://www.reddit.com/r/decred/comments/hbp6y4/forward_thinking_friday_1_moving_the_peg_forwards/) y 
Decred Narratives [26 de junio](https://www.reddit.com/r/decred/comments/hg2a9k/forward_thinking_friday_decred_narratives_26_june/).

- Skepticism Sunday [21 de junio](https://www.reddit.com/r/decred/comments/hd4mwv/decred_skepticism_sunday_21_june_2020/) y [28 de junio](https://www.reddit.com/r/decred/comments/hh7lo2/decred_skepticism_sunday_28_june_2020/)

- u / g687 [publicó](https://www.reddit.com/r/decred/comments/hghw3a/why_people_do_not_care_about_decred/) un análisis de cuántas veces se menciona a un proyecto mediante comentarios en una variedad de subreddits, señalando que Decred se mencionó relativamente poco en subreddits distintos de r / decred. Esto provocó 36 comentarios en respuesta, incluido uno de alta puntuación de @jy-p que expuso algunas posibles razones para la falta de menciones. También se señaló que los otros proyectos incluidos en la comparación tienen una capitalización de mercado más alto.

La idea de [patrocinar](https://www.reddit.com/r/decred/comments/hcfkei/draft_decred_cypherpunk_prize/) una investigación y software recibió respuestas variadas, en parte debido a la falta de detalles y a las personas dispuestas a ejecutarlo.

u / OpenWithRuiLopez se dió cuenta que Coinbase ha [adquirido](https://www.reddit.com/r/decred/comments/guri3s/coinbase_acquires_tagomi_tagomi_lists_decred/) la plataforma institucional de corretaje Tagomi, que comercializa DCR como uno de sus 14 activos.

Discusiones en Twitter:

- @moo31337 ha dado [un aviso](https://twitter.com/marco_peereboom/status/1271200577272385538) sobre su siguiente propuesta.
- @Doctor_Bitocin_ [comparó](https://twitter.com/Doctor_Bitcoin_/status/1277352638502375424) a Decred como un continente virtual al que todos pueden unirse.
- @Checkmate creó un nuevo [#DecredChallenge](https://twitter.com/_Checkmatey_/status/1272680543612628997) donde debes adivinar qué métrica se muestra en el gráfico.
- @Frenchy_DCR [reveló](https://twitter.com/Frenchy_DCR/status/1273811301844709387) por qué DCR no es popular.
- Después de ver muchos gráficos de análisis técnico, @Mattgetsbarrel1 por fin encontró una [estrategia](https://twitter.com/Mattgetsbarrel1/status/1274072597597024257) definitiva para negociar con DCR.

![disfrutando de DCR en las montañas polacas](./assets/pol-mountains.jpg)

imagen: @LolekBolek74 disfrutando de DCR en las montañas polacas

## Mercados

En junio, DCR cotizaba entre 14.01-18.76 USD / 0.0015–0.0019 BTC La tarifa diaria promedio fue de 16.05 USD.

En la última [publicación](https://medium.com/decred/decred-on-chain-realised-cap-mvrv-ratio-and-gradient-oscillators-a36ed2cc8182) de @Checkmate analizó cómo se aplica a Decred la capitalización de mercado realizada, la relación entre el MVRV y los osciladores. La capitalización de mercado tiende a actuar como un nivel de soporte o resistencia tanto para Decred como para Bitcoin, pero para Decred está más relacionado, porque se reevalora de forma más frecuente.

> La capitalización de mercado representa un nivel importante psicológico en el precio ya que ha demostrado interacciones importantes en el pasado.
> Las personas que interactuan con DCR bloqueando las monedas en staking, usando los servicios de CoinShuffle++ mixing  o votando en la gobernanza de Decred de manera frecuente, tienen una mayor percepción del precio y sus niveles. La compra de un ticket en vez de enviar las monedas a un exchange para colocar una órden de venta es una buena señal de un sentimiento alcista y aplica también para el caso contrario.

Otro [análisis](https://twitter.com/_Checkmatey_/status/1267945637980463104/photo/1) por parte de @Checkmate relacionado con el mercado muestra una divergencia alcista del RSI en el par DCR/USD.

@PermabullNino realizó un gráfico de cómo la capitalización de mercado en DCR se está [acercando](https://twitter.com/PermabullNino/status/1268181399879790592) a la capitalización realizada y una posible [correlación](https://twitter.com/PermabullNino/status/1268270041759432704) entre las salidas de tickets en los pools y las tendencias bajistas pasadas.

## Noticias relevantes externas

Ha habido cierta controversia sobre un [error](https://medium.com/blockstream/patching-the-liquid-timelock-issue-b4b2f5f9a973) con el servicio Liquid de Blockstream por el cual las "claves de respaldo de emergencia" en poder de Blockstream estaban tomando la custodia de los fondos de una manera que solo debería haber sucedido en una emergencia. La controversia se basa principalmente en cómo se ha manejado la divulgación del error, con James Prestwich (quien lo descubrió) no [impresionado](https://twitter.com/_prestwich/status/1277090512126660608) por la forma en que Blockstream ha minimizado su gravedad. Este [comentario](https://www.reddit.com/r/CryptoCurrency/comments/hhwwcb/vulnerability_discovered_in_liquid_allowing/fwdqbxc/) en r / cryptocurrency tiene una buena cronología del hecho, incluida una observación de que no se estaba hablando de ello en r / bitcoin.

En Reddit se ha abierto una [convocatoria](https://www.reddit.com/r/ethereum/comments/hbjx25/the_great_reddit_scaling_bakeoff/) de ideas sobre cómo podrían escalar el sistema de puntos recientemente lanzado (que actualmente se ejecuta en el testnet Rinkeby de Ethereum) a toda la plataforma.

El costo de las transacciones en Ethereum ha [aumentado](https://www.coindesk.com/ethereum-developers-consider-new-fee-model-as-gas-costs-climb) en un 500% desde abril y los desarrolladores están buscando formas de reducir esto, incluido un EIP (1559) que vería a los usuarios pagar una "tarifa base" a la red más una propina.

Un usuario de Ethereum ha estado pagando tarifas particularmente altas este mes, con dos transacciones separadas de $2.6 millones en ETH como tarifa de transacción a los mineros, por una transferencia de una pequeña cantidad de ETH (~ $ 100). La especulación sobre la causa de las altas tarifas incluyen errores e intentos de [chantaje](https://twitter.com/VitalikButerin/status/1271463564440678401). Además del misterio, el grupo que extrajo una de las transacciones parecía [ofrecer](https://twitter.com/sparkpool_eth/status/1270688700968480768) devolver parte de la tarifa, pero nadie reclamó.

Se detectó un [error](https://cointelegraph.com/news/bancors-bug-exposes-dangerously-common-practice-in-ethereum-defi) con los contratos inteligentes de Bancor que habría permitido a los atacantes robar los fondos de cualquiera que interactuara con él, por lo que "Bancor actuó preventivamente para" tomar "los fondos de los usuarios antes de que intervinieran partes maliciosas". La gravedad del problema se vio agravada por el uso de "aprobaciones infinitas", que ahorran en tarifas de transacción y ofrecen una mejor experiencia de usuario, pero exponen a los usuarios a un riesgo mucho mayor (en este caso, el atacante potencial podría obtener todos los tokens del depositante, no solo la cantidad que eligieron depositar). El uso de aprobaciones infinitas es común en muchas aplicaciones de DeFi.

La oferta del USDT ha [superado](https://bitcoinexchangeguide.com/tether-usdt-surpasses-10-billion-in-market-capitalization/) los $10 mil millones.

Chainalysis [anunció](https://cointelegraph.com/news/chainalysis-can-now-track-your-privacy-coins-zcash-dash) el soporte de las monedas de privacidad Zcash y Dash en sus productos. La gran mayoría de las transacciones en estas redes se pueden rastrear porque muy pocas personas usan las características de privacidad. Esto se produce después de las noticias de mayo en la que varios exchanges [eliminaron el soporte](https://cointelegraph.com/news/another-exchange-delists-monero-amidst-ongoing-sex-scandal) a Monero, y los investigadores de la Universidad de Carnegie Mellon afirman que el 99% + de las transacciones de Zcash son rastreables y que las entradas de las transacciones de Monero se pueden revelar con una precisión del 30 % ([artículo completo](https://eprint.iacr.org/2020/593.pdf)).

## Envía tus noticias para la siguiente edición

A medida que los ecosistemas de criptomonedas se expanden, se hace más difícil rastrear todos los eventos o acontecimientos importantes. Puede ayudar a capturar las noticias más relevantes enviándolas en GitHub. Para hacerlo, abra un [issue](https://github.com/xaur/decred-news/issues) en GitHub, encuentre el issue con el label de "[next release](https://github.com/xaur/decred-news/labels/next%20release)" (por ejemplo, "DJ July 2020") y comente con un enlace y una breve descripción de la noticia o evento importante.

## Sobre esta edición

Este es la edición #27 de la Revista Decred, un índice de todos los números originales y traducciones se encuentran disponibles [aquí](https://xaur.github.io/decred-news/).

La mayoría de la información de terceros se transmite directamente desde la fuente después de un control de fiabilidad mínimo. Los autores de la Revista Decred no tienen la capacidad de verificar todas las reclamaciones. Tenga cuidado con las estafas y haga su propia investigación.

Sus [comentarios](https://github.com/xaur/decred-news/blob/docs/contributing.md#feedback) y [contribuciones](https://github.com/xaur/decred-news/blob/docs/contributing.md) siempre son bienvenidas.

Créditos:

- Redacción y edición: bee, degeri, l1ndseymm, richardred
- Revisión y comentarios: chappjc, davecgh, jholdstock, jz, lukebp, raedah
- Imagen de portada: saender
