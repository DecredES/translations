Revista Decred Julio 2021
=========================

![portada](./assets/07_2021.jpg)

Lo más destacado de julio:

-   Ahora hay 3 cambios de consenso en varias etapas de desarrollo y la revocación de tickets ya está atrayendo algo de cobertura por medio de la prensa.
-   Progreso sólido en todos los repositorios habituales: dcrd obtuvo de nuevo un porcentaje del 10% de rápidez en el tiempo de descarga inicial de blockchain y DCRDEX ha agregado la integración central de ETH.
-   Ha sido un gran mes para las entrevistas: con Decred in Depth grabando episodios con varios miembros conocidos de la comunidad y algunas otras publicaciones junto con podcasts y entrevistas con desarrolladores del proyecto.

Contenido:

- [Desarrollo](https://github.com/DecredES/translations/blob/master/decredJournal/2021/07/index.md#desarrollo)
- [Comunidad](https://github.com/DecredES/translations/blob/master/decredJournal/2021/07/index.md#comunidad)
- [Gobernanza](https://github.com/DecredES/translations/blob/master/decredJournal/2021/07/index.md#gobernanza)
- [Red](https://github.com/DecredES/translations/blob/master/decredJournal/2021/07/index.md#red)
- [Ecosistema](https://github.com/DecredES/translations/blob/master/decredJournal/2021/07/index.md#ecosistema)
- [Alcance](https://github.com/DecredES/translations/blob/master/decredJournal/2021/07/index.md#alcance)
- [Eventos](https://github.com/DecredES/translations/blob/master/decredJournal/2021/07/index.md#eventos)
- [Medios](https://github.com/DecredES/translations/blob/master/decredJournal/2021/07/index.md#medios)
- [Discusiones](https://github.com/DecredES/translations/blob/master/decredJournal/2021/07/index.md#discusiones)
- [Mercados](https://github.com/DecredES/translations/blob/master/decredJournal/2021/07/index.md#mercados)
- [Noticias Relevantes](https://github.com/DecredES/translations/blob/master/decredJournal/2021/07/index.md#noticias-relevantes)
- [Sobre esta edición](https://github.com/DecredES/translations/blob/master/decredJournal/2021/07/index.md#sobre-esta-edici%C3%B3n)

## Desarrollo
El trabajo que se informa a continuación tiene el estado "fusionado con el maestro" al menos que se indique lo contrario. Significa que el trabajo se completa, se revisa e integra en el código fuente para que los usuarios avanzados puedan [crear y ejecutar](https://medium.com/@artikozel/the-decred-node-back-to-the-source-part-one-27d4576e7e1c) pero aún no está disponible en la versión de binarios para los usuarios habituales.

### [dcrd](https://github.com/decred/dcrd)

- se actualizó la implementación de `UtxoBackend` para usar `leveldb` directamente en lugar de usar el paquete de `database`. Esto da como resultado una descarga inicial de la blockchain  un 10% más rápida y un uso de memoria reducido en un 12%
- índice de bloque modificado para usar [llaves cortas](https://github.com/decred/dcrd/pull/2685), lo que resulta en un ahorro de memoria de ~ 30 MiB
- se agregaron [límites](https://github.com/decred/dcrd/pull/2675) de tamaño para las solicitudes de RPC para ayudar a fortalecer aún más el servidor contra posibles abusos en configuraciones no estándar en redes mal configuradas.
- se agregó una verificación de [origen](https://github.com/decred/dcrd/pull/2676) más estricta para las conexiones WebSocket
pequeñas correcciones y limpieza

En este punto tenemos 3 próximos cambios de consenso en diferentes etapas de desarrollo:

- volver a la política de gastos de tesorería propuesta originalmente (para [arreglar los gastos](https://github.com/DecredES/translations/blob/master/decredJournal/2021/06/index.md#nuevo-bug-en-el-fondo-de-tesorer%C3%ADa) de la nueva tesorería) tiene un borrador de [DCP](https://github.com/decred/dcps/pull/20) y un borrador de [pull request](https://github.com/decred/dcrd/pull/2680)
- las actualizaciones de versión explícitas tienen una [propuesta](https://github.com/decred/dcrd/pull/2680) aprobada y algún código de soporte ya combinado (como el manejo de scripts estándar que cubrimos [en junio](https://github.com/DecredES/translations/blob/master/decredJournal/2021/06/index.md#dcrd))
- la revocación automática de tickets tiene una [propuesta](https://proposals.decred.org/record/e2d7b7d) aprobada

Un beneficio menos obvio de la revocación automática de tickets es que simplifica la implementación del [ticket splitting](https://www.reddit.com/r/decred/comments/ot8x7o/decred_memelord_13_part_tweet_thread_113_decreds/h6w1vnk/).

### [dcrwallet](https://github.com/decred/dcrwallet)

- se agregó un método RPC que permitirá a Decrediton descubrir direcciones activas de manera más eficiente
- se agregó un método RPC para [revocar](https://github.com/decred/dcrwallet/pull/2061) tickets en modo SPV (también para Decrediton)
- se solucionó los problemas de concurrencia al [desbloquear](https://github.com/decred/dcrwallet/pull/2067) la billetera

### [Decrediton](https://github.com/decred/decrediton)

Orientado al usuario:

- se agregó una ventana de [confirmación de semillas](https://github.com/decred/decrediton/pull/3521) al flujo de creación de la billetera
- se diseñó la interfaz de usuario mejorada para la página de [conexión](https://github.com/decred/decrediton/pull/3530) para la billetera LN
- [puntos de interrupción](https://github.com/decred/decrediton/pull/3525) de diseño receptivos simplificados (para facilitar la integración con DCRDEX)
- no se permitió algunos [caracteres](https://github.com/decred/decrediton/pull/3511) problemáticos en los nombres de las billeteras
- se corrigió la selección de [filtros tx](https://github.com/decred/decrediton/issues/3528) en la página de Historial de transacciones
- ~ 7 correcciones.

Interno:

- migración a la nueva [API de Politeia](https://github.com/decred/decrediton/pull/3495)
- pruebas automatizadas para la página de [transacciones](https://github.com/decred/decrediton/pull/3518)
- se eliminó el uso de la biblioteca de registro de [Winston](https://github.com/decred/decrediton/pull/3536) para reducir el árbol de dependencia del proyecto (y la superficie de ataque de la cadena de suministro).

![LV](./assets/LN.png)

### [Politeia](https://github.com/decred/politeia)

Orientado al usuario:

- capturación de los [metadatos](https://github.com/decred/politeiagui/pull/2469) de las propuestas adicionales como límite de financiación en USD, fecha de inicio, fecha de finalización estimada y dominio. Esto nos permitirá mejorar y automatizar la validación de facturas de contratistas y también generar estadísticas de propuestas en Politeia.
- se agregó una [limitación](https://github.com/decred/politeia/pull/1448) de velocidad para notificaciones por correo electrónico para evitar comportamientos maliciosos
- mostrar quién [censuró](https://github.com/decred/politeiagui/pull/2454) un registro su por qué y cuándo
- UX mejorada para la descarga de [paquetes de propuestas](https://github.com/decred/politeiagui/pull/2453)
- se prohibió algunos elementos de [Markdown](https://github.com/decred/politeiagui/pull/2494) en los comentarios para evitar el abuso del tamaño del texto
- se puede mostrar [placeholders](https://github.com/decred/politeiagui/pull/2484) mientras se cargan los datos de la propuesta
- se puede mostrar una [advertencia](https://github.com/decred/politeiagui/pull/2500) sobre la posible pérdida de datos al guardar borradores
- ~ 11 correcciones de errores de frontend y ~ 1 backend

Desarrollo interno:

- se permite múltiples valores en la [configuración del plugin](https://github.com/decred/politeia/pull/1451)
- cobertura de prueba agregada para la [validación](https://github.com/decred/politeia/pull/1453) de las propuestas
- pruebas de IU automatizadas para la [lista de propuestas](https://github.com/decred/politeiagui/pull/2473)
- documentos de desarrollado extendidos
- ~ 1 frontend y ~ 7 correcciones de errores de backend

CMS:

- ~ 1 frontend y ~ 2 correcciones de errores de backend

Los cambios pendientes de implementación están marcados con una etiqueta `pi-not-deployed` en los repositorios [politeiagui](https://github.com/decred/politeiagui/issues?q=label%3Api-not-deployed) y [politeia](https://github.com/decred/politeia/pulls?q=label%3Api-not-deployed). De manera similar los cambios en el alcance de la [propuesta](https://proposals.decred.org/record/91cfcc8) de desarrollo se denominan [`91cfcc8`](https://github.com/decred/politeia/issues?q=label%3A91cfcc8).

### [DCRDEX](https://github.com/decred/dcrdex)

Orientado al usuario:

- manejar los intentos de registrarse con [saldo insuficiente](https://github.com/decred/dcrdex/pull/1092)
- registro de transacciones de [swap refund](https://github.com/decred/dcrdex/pull/1110) para que el usuario pueda recuperar fondos cuando se pierda el acceso al cliente y los registros se puedan encuentrar aún disponibles
- se puede [exportar](https://github.com/decred/dcrdex/pull/1109) las ordenes en archivo CSV
- agrupación de las ordenes con la [misma](https://github.com/decred/dcrdex/pull/1090) tarifa en una table row
- se muestra el precio actual en el [título](https://github.com/decred/dcrdex/pull/1117) de la ventana del navegador
- se muestra errores del pedido en el [formulario](https://github.com/decred/dcrdex/pull/1093) en lugar de la campana de notificación
- 4+ correcciones de errores

Interno:

- solo permite solicitar una [preimagen](https://github.com/decred/dcrdex/pull/1106) al cliente para protegerse contra un comportamiento malicioso del servidor
- el tamaño del lote y el paso de la tasa hicieron [parámetros de mercado](https://github.com/decred/dcrdex/pull/1102) en lugar de ser parámetros de assets
- [dependencias](https://github.com/decred/dcrdex/pull/1111) npm actualizadas
- migración al paquete [`stdaddr`](https://github.com/decred/dcrdex/pull/1096) de dcrd
- 4+ correcciones de errores

Soporte de Ethereum:

- Infraestructura básica de [ETH](https://github.com/decred/dcrdex/pull/1005) del lado del cliente (el uso de la red principal está deshabilitado por ahora)
- almacenamiento de saldo de ETH en unidades [gwei](https://github.com/decred/dcrdex/pull/1078) para adaptarse a enteros de 64 bits
- implementación del [estado de sincronización](https://github.com/decred/dcrdex/pull/1082) de ETH junto a información de tasa de tarifa (con una solución se solicitó la función de Geth [faltante](https://github.com/ethereum/go-ethereum/issues/23099))

Se han actualizado algunas [correcciones](https://github.com/decred/dcrdex/commits/release-v0.2) a una próxima versión v0.2.1.

Se comenzó a trabajar para reemplazar la tarifa de registro con [bonos de fidelidad](https://github.com/decred/dcrdex/pull/1120) donde los usuarios bloquean fondos para usar DCRDEX (como un [desincentivo](https://twitter.com/lukebp_/status/1412061031061508098) contra el mal comportamiento) pero pueden canjearlos después de cierto tiempo. Esto crea un costo de tiempo para usar DCRDEX en lugar de un costo monetario.

### [dcrandroid](https://github.com/planetdecred/dcrandroid)

@raedah comentó sobre la cuestión de cuándo se admitirá el staking en las aplicaciones móviles:

> El soporte para el staking vspd de nuevo estilo se ha integrado en dcrlibwallet para godcr y actualmente se encuentra en prueba final. Después de que se lance godcr, será fácil para los desarrolladores importar la misma funcionalidad de staking en las aplicaciones móviles. Sin embargo, no hay un gran incentivo para priorizar la construcción de la IU de staking móvil hasta que haya una billetera de hardware funcional con la que se pueda emparejar. [(2021–07–19)](https://www.reddit.com/r/decred/comments/okrlg1/mobile_staking/h5rps6h/)

### [dcrios](https://github.com/planetdecred/dcrios)

traducción al [vietnamita](https://github.com/planetdecred/dcrios/pull/809) actualizada

### [godcr](https://github.com/planetdecred/godcr)

- [renderizado en HTML](https://github.com/planetdecred/godcr/pull/469) implementado para mostrar texto con estilo
- implementación de [toggle](https://github.com/planetdecred/godcr/pull/487) widget personalizado
- se ahora se puede [ocultar](https://github.com/planetdecred/godcr/pull/493) los saldos de staking y la cuenta importada cuando no tienen fondos
- página de [licencia](https://github.com/planetdecred/godcr/pull/516) agregada
- actualizaciones de la interfaz de usuario y limpieza masiva de código para: lista de [propuestas](https://github.com/planetdecred/godcr/pull/513) y detalles, [billetera](https://github.com/planetdecred/godcr/pull/496), [billeteras](https://github.com/planetdecred/godcr/pull/493), [envío](https://github.com/planetdecred/godcr/pull/524), [StakeShuffle](https://github.com/planetdecred/godcr/pull/534) y varias páginas de [tickets](https://github.com/planetdecred/godcr/pull/539)
- páginas y modales agrupados en [paquetes](https://github.com/planetdecred/godcr/pull/512)
- 6+ correcciones de errores

![godcr](./assets/godcr.png)

### [dcrdata](https://github.com/decred/dcrdata)

Orientado al usuario:

- se corrigió el cambio de [status del voto](https://github.com/decred/dcrdata/pull/1838) en la página de Proposals
- [umbral](https://github.com/decred/dcrdata/pull/1813) de quórum de agenda fijo
- se cambió la página de bloqueo para usar términos ["aprobados" y "rechazados"](https://github.com/decred/dcrdata/pull/1841) en lugar de "válidos" / "no válidos".

Interno y desarrollador:

- sincronización inicial [optimizada](https://github.com/decred/dcrdata/pull/1840), tabla de vouts, caché de direcciones y rendimiento de la página de búsqueda
- rendimiento [optimizado](https://github.com/decred/dcrdata/pull/1844) e inicio mejorado
- se pasó de la codificación gob a la [serialización](https://github.com/decred/dcrdata/pull/1843) personalizada del grupo de tickets, lo que hace que el inicio sea ~ 5 segundos más rápido
- [purga](https://github.com/decred/dcrdata/pull/1842) fija de vouts
- se agregó un [arnés de prueba](https://github.com/decred/dcrdata/pull/1778) usando la cadena simnet en lugar del snapshot dcrdata

### [docs](https://github.com/decred/dcrdocs)

- arreglo de [enlaces](https://github.com/decred/dcrdocs/pull/1177) caídos
- docs de [gominer](https://github.com/decred/dcrdocs/pull/1178) eliminados
- [archivo](https://docs.decred.org/governance/consensus-rule-voting/consensus-vote-archive/) [actualizado](https://github.com/decred/dcrdocs/pull/1174) de votos por consenso

### [decred.org](http://decred.org/)

- porcentaje agregado de tickets [revocados](https://github.com/decred/dcrweb/pull/993) a la lista de VSP
- mostrar los [comunicados](https://decred.org/) de prensa y las publicaciones más recientes en la página de inicio de [decred.org](http://decred.org/)
- agregó el [comunicado de prensa](https://decred.org/press/2021-05-25_dex_decrediton/) sobre la integración de DCRDEX en Decrediton

### [Plugin WooCommerce](https://github.com/karamble/decred-woocommerce-plugin)

@karamble lanzó un nuevo complemento para aceptar pagos DCR en las tiendas WooCommerce. Puede generar direcciones de pago utilizando XPUB (clave pública extendida) de la cuenta de billetera. De esta manera cada pago utiliza una nueva dirección única mientras el servidor web de la tienda no tiene acceso a la billetera.

![commerce](./assets/commerce.png)

Otro:

- hemos perdido por completo dos repositorios jovenes de Rust en donde se implementaban las API de Decred a pesar de no recibir nuevas confirmaciones desde noviembre-diciembre del 2020
- el programa Bug Bounty informó estadísticas al final de la Fase 3 (30 de junio): un total de 193 envíos procesados de los cuales 18 son elegibles para un pago. Se han aumentado las cantidades máximas de recompensas.

## Comunidad

¡Damos la bienvenida a los nuevos contribuidores con código fusionado en la rama principal: @briancolecoinmetrics ([dcrd](https://github.com/decred/dcrd/commits?author=briancolecoinmetrics)), @devchoplife ([godcr](https://github.com/planetdecred/godcr/commits?author=devchoplife)) y @jcezetah ([godcr](https://github.com/planetdecred/godcr/commits?author=jcezetah))!

Estadísticas de la comunidad a partir del 1 de agosto:

- Seguidores de [Twitter](https://twitter.com/decredproject): 47 586 (+667)
- Suscriptores de [Reddit](https://www.reddit.com/r/decred/): 11 449 (+127)
- Usuarios en la sala #general de [Matrix](https://chat.decred.org/): 513 (+12)
- Usuarios de [Discord](https://discord.com/invite/GJ2GXfz): 1 960 (+27)
- Usuarios de [Telegram](https://t.me/Decred): 2 833 (+100)
- Suscriptores de [Youtube](https://www.youtube.com/decredchannel): 4 600 (+30), views: 191 mil (+3 mil)

## Gobernanza

En julio, el nuevo fondo de la [tesorería](https://dcrdata.decred.org/treasury?chart=balance&zoom=knj8yxs0-kse64gw0&bin=month) recibió 11 338 DCR por un valor de 1.44 millones de dólares a la tasa promedio de julio de 127.48 dólares. Se gastaron 770 DCR para pagar a los contratistas por un valor de $98 000 a la tasa de julio o bien $101 000 a la tasa de facturación de junio de $131.52. Al 2 de agosto el saldo combinado de la nueva tesorería [heredada](https://dcrdata.decred.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx?chart=balance&zoom=ijhhasg0-kr5vh280&bin=month) es de 703 655 DCR (96.3 millones de dólares a 136.80 dólares).

La tesorería heredada recibió una [“donación”](https://www.notion.so/4cf536fb2f7dd51b96d63c9087766e10) inusual de ~ 90 DCR proveniente de una transacción mixta.

En julio se publicaron 4 nuevas propuestas y dos aún están en discusión al momento de escribir este artículo.

- Una [propuesta](https://proposals.decred.org/record/ae609f1) de @frizzers para realizar un documental copyleft que se pueda compartir libremente basado en su libro “Daylight Robbery” por un costo de $ 300 000.
- Una [propuesta](https://proposals.decred.org/record/51c4128) para financiar un equipo para que asista al evento Crypto Expo Dubai en octubre del 2021. Han presentado dos opciones, el primero con un costo de $21 240 para llevar a 4 representantes de Decred a Dubai o bien la segunda opción de $26 240 para obtener un espacio de presentación en el evento. @sz1 elegirá una de estas opciones según los comentarios de la comunidad.
- Un propietario retiró su [propuesta](https://proposals.decred.org/record/a3fa55f) para financiar una miniserie de ciencia ficción dividida en tres partes.
- Se aprobaron propuestas para el [Cambio](https://proposals.decred.org/record/e2d7b7d) de Consenso de Revocaciones Automáticas en Tickets (95% de aprobación y 51% de participación) y un [bot](https://proposals.decred.org/record/2895755) de gráficas en Twitter (85% de aprobación y 46% de participación).

Consulte el [issue #44](https://blockcommons.red/politeia-digest/issue044/) y el [issue #45](https://blockcommons.red/politeia-digest/issue045/) de Politeia Digest para obtener más detalles sobre las propuestas del mes.

## Red

**Hashrate**: el [hashrate](https://dcrdata.decred.org/charts?chart=hashrate&zoom=kqhwurpw-kru2wj65&scale=linear&bin=block&axis=time) de julio se abrió a ~ 71 Ph / s y cerró ~ 316 Ph / s, tocando fondo en 70 Ph / s alcanzando un máximo de 334 Ph / s durante todo el mes.

Distribución del hashrate [reportada](https://miningpoolstats.stream/decred) en los pools el 1 de agosto:

- Poolin 58%
- F2Pool 23%
- AntPool 6%
- BTC.com 4%
- Easy2Mine 4%
- Luxor 2.3%
- HuobiPool 1%
- ViaBTC 0.4%
- CoinMine 0.09%
- OKEx 0.08%
- UUPool 0.06%.

La distribución de 1 000 bloques [minados](https://miningpoolstats.stream/decred) antes del 1 de agosto coincidió estrechamente con el hashrate informado.

Hashrate se está recuperando de los eventos de junio en [China](https://www.coindesk.com/chinas-bitcoin-mining-crackdown-is-a-boon-for-miners-elsewhere) y nuevos grupos de minería se están uniendo a la red.

**Staking**: el [precio de los tickets](https://dcrdata.decred.org/charts?chart=ticket-price&zoom=kqhwurpw-kru2wj65&bin=window&axis=time&visibility=true-true) varió entre 146.3 – 203.2 DCR con un [promedio](https://dcrstats.com/) de 30 días de 190.7 DCR (+ 6).

La [cantidad bloqueada](https://dcrdata.decred.org/charts?chart=ticket-pool-value&zoom=kqhwurpw-kru2wj65&scale=linear&bin=block&axis=time) fue de 7.43 a 7.88 millones DCR lo que significa que entre el 56.3 y 59.8% del suministro circulante [participó](https://dcrdata.decred.org/charts?chart=stake-participation&zoom=kqhwurpw-kru2wj65&scale=linear&bin=block&axis=time) en el proof-of-stake.

El precio de los tickets tuvo una caída inusual por debajo de los mínimos del 2020 pero luego se recuperó rápidamente con un fuerte soporte de compra.

**VSP**: El 1 de agosto los servidores vspd [administraron](https://decred.org/vsp/) ~ 8 600 (+600) tickets en vivo y los servidores dcrstakepool enumerados aproximadamente 400 (-200). En conjunto, los 11 VSP heredados y los 14 nuevos administraron el 22.9%  (+2%) del grupo de tickets. Los VSP heredados excluidos de la lista que aún siguen activos administraron 12 tickets en vivo (-14).

Los mayores ganadores de tickets en términos absolutos fueron [stakey.com](http://stakey.com/) (+474), 123.dcr.rocks (+126) y [ubiqsmart.com](http://ubiqsmart.com/) (+51). Los dos primeros tienen comisiones por debajo del 0.5%.

**Nodos**: a lo largo de julio hubo alrededor de 211 nodos accesibles según [dcrextdata](https://analytics.planetdecred.org/).

Versiones de nodo a partir del [snapshot](https://nodes.jholdstock.uk/user_agents) del 1 de agosto (250 dcrd nodos):

- v1.6.2–57%
- v1.6.0–16%
- v1.6.1–13%
- v1.7 dev builds — 7%
- v1.6 dev builds — 3%
- v1.5.2–2%
- v1.5.1–1.6%.

La red [Lightning Network](https://ln-map.jholdstock.uk/) de Decred ha visto 36 nodos (+2), 66 canales (+6) con una capacidad total de 25.5 DCR (+3.7) al 1 de agosto.

## Ecosistema

Le damos la bienvenida a la nueva instancia de vspd [dcrvsp.dittrex.com](http://dcrvsp.dittrex.com/) que reemplaza su VSP heredado, este mismo fue [eliminado](https://github.com/decred/dcrwebapi/pull/140) de la lista en mayo y se cerró en julio.

Legacy VSP [pool.d3c.red](https://pool.d3c.red/) de @karamble votó su ticket final y fue cerrado. Los usuarios son bienvenidos al servidor de reemplazo en [vsp.decredcommunity.org](http://vsp.decredcommunity.org/).

Hasta ahora 8 VSP heredados se han eliminado de la lista (3 cierres, 1 estado desconocido, 4 aún votando) y 9 todavía están en la lista. El estado de la migración al [nuevo sistema VSP](https://blog.decred.org/2020/06/02/A-More-Private-Way-to-Stake/) se resume en [esta tabla](https://github.com/decred/vspd/issues/231#issuecomment-774877129). Se [recomienda](https://twitter.com/JamieHoldstock/status/1405069123453784065) que los usuarios de VSP heredados se actualicen a vspd para evitar el riesgo de perder tickets cuando dcrstakepool deje de funcionar (por ejemplo: si se activa una nueva actualización de consenso).

La [lista de VSP](https://decred.org/vsp/) se actualizó para mostrar el porcentaje de tickets revocados ya que es una métrica útil al elegir un VSP.

[ViaBTC](https://www.viabtc.com/) anunció el [lanzamiento](https://viabtc.medium.com/viabtc-pool-unveils-dcr-on-chain-co-governance-under-hybrid-consensus-61fcbd133a55) de la minería DCR celebrado por un "Carnaval de minería sin cargos" hasta el 25 de agosto. El grupo admite los [métodos](https://support.viabtc.com/hc/en-us/articles/4403972374297-DCR-Mining-Pool-Launched-Mine-with-ZERO-Fees-For-30-days) de pago PPS +, PPLNS y SOLO.

El pool [OKEx](https://www.okex.com/pool) ha estado minando DCR desde [agosto del 2020](https://www.okex.com/academy/en/how-to-earn-cryptocurrency-with-okex-pool) pero en julio finalmente minó algunos bloques según [miningpoolstats.stream](https://miningpoolstats.stream/decred).

[Bitfinex](https://www.bitfinex.com/) [anunció previamente](https://twitter.com/bitfinex/status/1421032832848302081) un listado de DCR y fue a principios de [agosto](https://twitter.com/bitfinex/status/1423210403774009345) donde publicó el trading entre DCR / USD.

Advertencia: los autores de la revista Decred no tienen idea de la confiabilidad de ninguno de los servicios mencionados anteriormente. Haga su propia investigación antes de confiar su información personal o sus activos a cualquier entidad.

Únase a nuestro chat  [#services](https://chat.decred.org/#/room/#services:decred.org) para seguir las actualizaciones del ecosistema Decred.

## Alcance

Logros de Monde PR para julio:

- lanzó 1 historia para publicaciones financieras y criptográficas
- tuvo 4 oportunidades de relaciones públicas para Decred
- consiguió 2 entrevistas con los medios.

Cheque los siguientes artículos de noticias: 

- @lukebp fue entrevistado por el podcast de Geek Insider. [Geek Speak](https://www.youtube.com/watch?v=a9IQyMf_724) cubre todos los aspectos principales de Decred.
- Un artículo en [The Street](https://www.thestreet.com/personal-finance/should-you-worry-about-crypto-crashing-nw) con comentarios de @ jy-p sobre cómo comprar criptomonedas distribuido por NerdWallet.
- Un artículo en [MarketWatch](https://www.marketwatch.com/story/what-to-do-when-your-digital-assets-take-a-dive-11625258295) con comentarios de @ jy-p sobre cómo comprar criptomonedas, distribuido por NerdWallet. El artículo también se distribuyó a otras 7 publicaciones incluido [MSN](https://www.msn.com/en-us/money/savingandinvesting/what-to-do-when-your-digital-assets-take-a-dive/ar-AALOVNE).
- [Bankless Times](https://www.banklesstimes.com/2021/07/28/decred-continues-to-evolve-without-contentious-hard-forks/), [Crowdfund Insider](https://www.crowdfundinsider.com/2021/07/178473-decred-dcr-a-virtual-currency-focused-on-security-and-scalability-to-enhance-user-experience/) y [Geek Insider](https://geekinsider.com/no-contentious-hardforks-as-decred-evolves/) cubrieron las noticias sobre la aprobación de Decred para realizar un cambio de consenso en las revocaciones de tickets. @lukebp también fue entrevistado por el podcast Crypto and Cigars para hablar sobre la capacidad de actualización de Decred.
- [Finder.com](http://finder.com/) publicó los resultados de su encuesta de predicciones de criptomonedas con citas de @jz en un artículo sobre la [predicción de precios de Bitcoin](https://www.finder.com/bitcoin-btc-price-prediction) y un artículo sobre la [predicción de precios de Doge](https://www.finder.com/hk/dogecoin-doge-price-prediction). La noticia fue recogida por [The Block News](https://theblocknews.io/finders-experts-predict-dogecoin-price-should-hit-1-21-by-2025-and-3-60-by-2030/), [FinBold](https://finbold.com/50-of-crypto-experts-expect-bitcoin-to-overtake-global-finance-by-2040/), [CryptoKnowmics](https://www.cryptoknowmics.com/news/crypto-experts-optimistic-for-bitcoin-believes-btc-will-replace-fiat-currency-by-2040-in-hyperbitcoinisation), [Bitcoin News](https://news.bitcoin.com/crypto-experts-predict-bitcoin-price-rising-to-318417-by-december-2025/), un segundo artículo en [Bitcoin News](https://news.bitcoin.com/finders-experts-predict-dogecoin-price-should-hit-1-21-by-2025-and-3-60-by-2030/) y [The Hack Posts](https://thehackposts.com/crypto-experts-predict-bitcoin-price-rising-to-318417-by-december-2025-markets-and-prices-bitcoin-news/). Los artículos mencionan que Decred fue parte de un panel de 42 expertos que completaron la encuesta incluidos representantes de Thomson Reuters, UCL School of Management y la Universidad de Australia Occidental.
- @raedah fue entrevistado para la serie [The Future is Now](https://medium.com/authority-magazine/the-future-is-now-steven-wagner-of-raedah-group-on-how-their-technological-innovation-will-shake-4f272ced222f) de la revista Authority hablando de todo lo relacionado con Decred y las criptomonedas incluida la privacidad, la gobernanza, siendo Decred la primer DAO criptográfica verdadera y el uso de Decred en las elecciones de Brasil.

El autor del bot de @StakeShuffle_ está recopilando [comentarios](https://twitter.com/StakeShuffle_/status/1418895005050155011) sobre qué métricas implementar en la próxima fase de desarrollo. Los tweets generados con gráficas proporcionarán contenido actualizado que se puede usar en conversaciones en Twitter.

## Eventos

Asistido:

- 5 de julio - [Talent Land Digital](https://github.com/decredcommunity/events/pull/95) - Internet. @pablito dio una charla de 25 min sobre “What is Decred” (34 000 vistas) y un taller de 58 min “Introducción a Blockchain usando la API dcrdata” (47 000 vistas). Decred es un patrocinador de bronce en Talent Land.
- 10 de julio - [YOUCATHON: Juventud por el cambio y la acción (100% digital)](https://decredcommunity.github.io/events/index/20210710.1) - Youssoufia, Marruecos. La escuela de informática YouCode organizó un hackathon entre dos campus en Youssoufia y Safi, conectados a través de una videoconferencia. @arij fue invitada a hablar sobre la tecnología blockchain. En su charla de ~ 80 minutos explicó la tecnología y demostró una billetera Decred y la plataforma Politeia. Las preguntas se referían a cómo se puede usar esto para crear aplicaciones y qué oportunidades existen para trabajar en proyectos de blockchain por lo que @arij explicó su papel en Decred y como unirse.
- Desde principios del 2021 Decred es partidario del [programa educativo](https://twitter.com/IECarballo/status/1417491314191519751) sobre criptomonedas y tecnología blockchain organizado por la Escuela de Negocios de la Universidad Católica de Argentina y la ONG Bitcoin Argentina.

## Medios

Artículos seleccionados:

- The coming rise and fall of central bank digital currencies por @ammarooni ([bitcoinmagazine.com](http://bitcoinmagazine.com/))

Videos:

- What is Decred? Decentralized Autonomous Organization Politeia Decred crypto por MarketSquare ([youtube](https://www.youtube.com/watch?v=s8hAwP0JvE4))
- Blockchain security — Decred Fundamentals por @phoenixgreen ([youtube](https://www.youtube.com/watch?v=BsKV7fiWdqE))
- The cost of attack — Decred Fundamentals por @phoenixgreen ([youtube](https://www.youtube.com/watch?v=RXV8dGZ9HEk))
- Hybrid security — Decred Fundamentals por @phoenixgreen ([youtube](https://www.youtube.com/watch?v=QgInCQTbw4s))
- Decred Price Analysis — 1 de julio del 2021 por @Brave New Coin ([youtube](https://www.youtube.com/watch?v=rtpCGv63Tm8))
- A ragin’ geek speak with… Decred blockchain developer con Luke Powell — 07/05/2021 por Meredith Loughran of GeekInsider ([youtube](https://www.youtube.com/watch?v=VLZRriYx8qM), [periscope](https://www.pscp.tv/w/c7IKyDFQbUtxVmduRHpqb1l8MWt2SnBvb0FaZG9HRadTE0sJ4V5iChp6FerysRgxlLOi8yj07WsN_joUocji))
- Entrevista con @fst_nml en Decred in Depth (live): Decred and Thorchain integration por @elima_iii ([youtube](https://www.youtube.com/watch?v=vGjqqVN4qDs))
- Decred in Depth 39 — Dominic Frisby — Marketing + filmmaking + DAO por @elima_iii ([youtube](https://www.youtube.com/watch?v=WpMKGsQLxic))
- Decred in Depth 40 — Entrevista a Notsofast por @elima_iii ([youtube](https://www.youtube.com/watch?v=ryyJ25EXqKI))

Audio:

- Se han subido nuevos episodios de Decred in Depth a [Libsynn](https://decredindepth.libsyn.com/)

Arte y diversión:

- visualización de [modelos de gobernanza](https://twitter.com/OfficialCryptos/status/1410731577546477568) por @OfficialCryptos

Traducciones:

- Decred Journal de junio del 2021 se tradujo al árabe (@arij, @ abdulrahman4), chino (@Dominic) y español (@francov_). La edición de mayo en español también está disponible. Un cálido agradecimiento a todos los traductores por permanecer con nosotros durante tanto tiempo.

Si tiene traducciones que no conocemos compártalas en nuestro chat de [#traducciones](https://chat.decred.org/#/room/#translations:decred.org).

## Discusiones

Publicaciones seleccionadas de Reddit:

- ideas sobre cómo [atraer desarrolladores](https://www.reddit.com/r/decred/comments/ohcr5q/how_attact_developers_to_join_decred_community/) para que se unan a la comunidad Decred
- múltiples comentarios sobre la compra de [ASIC](https://www.reddit.com/r/decred/comments/occ45q/buy_decred_asic_where_when_what_do_you_think_guys/) y su rentabilidad.

Debates seleccionados de Twitter:

- El [hilo](https://twitter.com/lukebp_/status/1418216538193203200) de @ lukebp sobre el cambio de consenso de revocaciones automáticas de tickets destaca que el trabajo en el código de consenso de misión crítica realizado por desarrolladores fuera del equipo original es un paso importante en la descentralización del proyecto. El segundo punto a destacar es que este cambio demuestra la propuesta de valor fundamental de Decred: la capacidad de mejorar la UX de la capa base.
- @decredmemelord ha [resumido](https://twitter.com/decredmemelord/status/1420227949970685956) algunos de los logros clave del proyecto en el último año.

## Mercados

En julio, DCR cotizaba entre 91.70–158.46 USD/ BTC 0.00338–0.00381. La tarifa promedio diaria fue de $127.48.

## Noticias Relevantes

Thorchain ha sido golpeado por dos ataques este mes. Los [primeros](https://decrypt.co/76215/thorchain-tapping-treasury-repay-5m-ethereum-after-attack) proveedores de liquidez ETH afectados cuyos pools se agotaron por $5 millones serán compensados por la tesorería de Thorchain. El [segundo](https://www.coindesk.com/thorchain-8-million-exploit-bifrost) ataque reclamó $8 millones al engañar al protocolo Bifrost de la red para que recibiera activos falsos; aparentemente podría haber sido mucho peor si no fuera por las [aparentes](https://twitter.com/THORChain/status/1418360743523618825) tendencias de sombrero blanco del hacker. Sin embargo, las cosas pueden estar mejorando para Thorchain ya que el último atacante dejó [instrucciones](https://news.bitcoin.com/thorchain-trolled-by-hacker-after-two-successful-seven-figure-exploits/) sobre cómo pueden mejorar la seguridad.

Uniswap ha votado a favor de [financiar](https://www.coindesk.com/defi-gets-proactive-about-policy-thanks-to-a-20m-grant-from-the-uniswap-community) un "Fondo de Educación DeFi" con 1 millón de UNI (con un valor de alrededor de $20 millones) la mitad de los cuales se intercambiaron inmediatamente por USDC. Esta propuesta fue originalmente facturada como un "fondo de defensa política" para pagar a los representantes que pueden luchar en la esquina de DeFi con los reguladores. Ha habido algunas [críticas](https://decrypt.co/75841/uniswap-proposal-sparks-blowback-after-grantees-dump-10m-uni-tokens) sobre el papel que jugaron las ballenas de UNI asociadas con los proponentes en la aprobación de esta propuesta.

La organización ShapeShift está [cerrando](https://www.coindesk.com/shapeshift-to-shut-down-airdrop-fox-tokens-to-decentralize-itself-out-of-existence) sus puertas en un esfuerzo por “descentralizarse y dejar de existir”. Está lanzando tokens FOX a sus usuarios y usuarios de varios protocolos DeFi donde esos tokens se usarán para gobernar una DAO (que también está recibiendo una asignación de token). El airdrop es complejo ya que cubre una variedad de blockchains pero los usuarios solo tendrán 100 días para reclamar sus tokens FOX antes de que estos vuelvan a la DAO.

Eso es todo por julio. Comparta sus actualizaciones para el próximo número en nuestra sala de chat [#journal.](https://chat.decred.org/#/room/#journal:decred.org)

## Sobre esta edición

Esta es la edición #40 de la Revista Decred. Un índice de todas las ediciones, y traducciones están disponibles [aquí](https://xaur.github.io/decred-news/).

La mayoría de la información de terceros se transmite directamente desde la fuente después de un control de fiabilidad mínimo. Los autores de la Revista Decred no tienen la capacidad de verificar todas las reclamaciones. Tenga cuidado con las estafas y haga su propia investigación.

Créditos (por orden alfabético)

- Escritura y redacción: bee, degeri, l1ndseymm, richardred
- Revisión y comentarios: davecgh, karamble, lukebp, raedah
- Imagen de portada: saender
- Financiado por: Los stakeholders de Decred
