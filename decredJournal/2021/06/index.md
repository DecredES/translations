# Revista Decred Junio 2021

![portada]('./assets/202006.png)
Core Lattice por @saender

Lo más destacado de junio:

- Se aprobó una próxima actualización de consenso en Politeia que haría que los cambios de consenso futuros sean más fáciles, más confiables y más seguros.
- Un error con los controles de los gastos de tesorería provocó la imposición de un límite demasiado bajo; esto requerirá una actualización por consenso para solucionarlo.
- Tres propuestas de Politeia aprobadas con una alta participación (~ 47%) y votos a favor (97–99%): Bug Bounty, Traducciones y la versión explícita de mejora en el cambio de consenso.
El hashrate de PoW ha experimentado una caída significativa, probablemente asociada con la represión de la minería en China.

Contenido

- [Nuevo bug en el fondo de tesorería]()
- [Desarrollo]()
- [Comunidad]()
- [Gobernanza]()
- [Red]()
- [Ecosistema]()
- [Alcance]()
- [Eventos]()
- [Media]()
- [Discusiones]()
- [Mercado]()
- [Relevantes externos]()
- [Sobre]()


## Nuevo bug en el fondo de tesorería

Los pagos del nuevo fondo de tesorería están bloqueados durante varios meses por un error en la implementación de la política de gastos. La transacción de gasto de tesorería de prueba extraída el [22 de mayo](https://explorer.dcrdata.org/tx/7507bcc72bfde895065034e12e6d462f2360163cd0c879f0db35514f9456b2c1) desencadenó una condición pasada por alto en el mecanismo de seguridad que protege de gastar demasiado DCR en un corto período de tiempo. Durante los próximos meses, solo se pueden gastar alrededor de 0.15 DCR de la nueva tesorería, que es demasiado bajo para pagar a los contratistas.

Si bien este es un retraso desafortunado en la migración a la tesorería descentralizada y trabajo adicional para corregir el error, el plan de migración se creó para manejar casos como este. Todos los fondos de la red están seguros y los pagos de los contratistas continuarán desde la tesorería anterior. Arreglar el algoritmo de seguridad requiere otro cambio de consenso que está [en desarrollo](https://github.com/decred/dcps/pull/20).

Leé la historia completa del error en la [publicación del blog](https://blog.decred.org/2021/06/25/Treasury-Expenditure-Policy-Bug/) y en los hilos de Twitter de [@matheusd](https://twitter.com/matheusd_tech/status/1409928455974699013) y [@lukebp](https://twitter.com/lukebp_/status/1409929016400822279).

> En una nota al margen, este incidente nos recuerda que incluso el código de consenso ampliamente [revisado](https://github.com/decred/dcrd/pull/2170) y probado no es inmune a los errores, pero son más fáciles de corregir cuando existe un proceso de actualización bien definido y no controvertido.

## Desarrollo

## Comunidad

¡Damos la bienvenida a los nuevos contribuidores con código fusionado en la rama principal:  @vibros68 ([politeiagui](https://github.com/decred/politeiagui/commits?author=vibros68)) y @x-walker-x ([politeiagui](https://github.com/decred/politeiagui/commits?author=x-walker-x))!

Estadísticas de la comunidad :

- Seguidores de [Twitter](https://twitter.com/decredproject): 46 919 (+1 195)
- Suscriptores de [Reddit](https://www.reddit.com/r/decred/): 11 322 (+132)
- Usuarios en la sala #general de [Matrix](https://chat.decred.org/): 501 (+34)
- Usuarios de [Discord](https://discord.com/invite/GJ2GXfz): 1 933 (+146)
- Usuarios de [Telegram](https://t.me/Decred): 2 733 (+28)
- Suscriptores de [Youtube](https://www.youtube.com/decredchannel): 4 570 (+30), views: 188K (+2K)
- Estrellas en el repo de [dcrd](https://github.com/decred/dcrd): 601 (+3), forks: 256 (+1)

El resumen de junio de la inusual dinámica de las redes sociales se puede encontrar [aquí](https://decredcommunity.github.io/social-media-stats/posts/20210711.1).

## Gobernanza

En junio, el [nuevo fondo de la tesorería](https://dcrdata.decred.org/treasury?chart=balance&zoom=knj8yxs0-kse64gw0&bin=month) recibió 10 510 DCR por un valor de 1.4 millones de dólares a la tasa promedio de mayo de 131.52 dólares. Se gastaron 1 460 DCR (de la dirección de tesorería heredada) para pagar a los contratistas, por un valor de $192 000 a la tasa de junio, o $253 000 a la tasa de facturación de mayo de $173.47. Al 2 de julio, el saldo combinado de la nueva tesorería [heredada](https://dcrdata.decred.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx?chart=balance&zoom=ijhhasg0-kr5vh280&bin=month) es de 692 988 DCR (91.4 millones de dólares a 131.88 dólares). 

La primera transacción real de la nueva tesorería no se extrajo debido al [bug](https://xaur.github.io/decred-news/journal/202106#new-treasury-bug) descrito anteriormente y los contratistas recibieron el pago de la antigua manera. A pesar de que no funcionó según lo [planeado](https://twitter.com/behindtext/status/1402628975676035078), esa transacción mostró un alto compromiso de los votantes en cadena y un alto apoyo de la administración actual de la tesorería: 11 943 tickets, 17 280 votaron Sí y cero votaron No, fue una participación del 69%. Este podría aumentar aún más cuando se implemente la votación TSPEND para los usuarios de VSP, que actualmente poseen alrededor del 20% de los tickets en vivo.

Se publicaron tres propuestas en Politeia y las tres han sido aprobadas con fuertes índices de aceptación.


- La propuesta de [cambio de consenso de actualizaciones de versión explícita](https://proposals.decred.org/record/3a98861) alcanzó un nuevo hito de aprobación con un 99.9% de votos a favor y solo 13 tickets votando en contra de la propuesta, entre el 47% de participación.

- La cuarta iteración de la [propuesta](https://proposals.decred.org/record/e1f104b) de Bug Bounty regresó con un calendario de pagos mejorado y fue aprobada con un 98.5% de votos a favor y una participación del 47%. Esto es + 0.5% de votos a favor y + 15% de participación en comparación con la [Fase 3](https://proposals-archive.decred.org/proposals/2170df6). @degeri [agradece](https://twitter.com/degeri_crypto/status/1409714139396591617) a los stakeholders por la creciente cantidad de fe y confianza.

- La segunda fase de la gran [propuesta](https://proposals.decred.org/record/af9942a) de traducción fue aprobada con un 97.3% de aprobación y una participación del 46%, un gran aumento en el apoyo del 75% Sí y el 28% de participación para la primera [propuesta](https://proposals-archive.decred.org/proposals/c093b8a).

Consulte el [issue #43](https://blockcommons.red/politeia-digest/issue043/) de Politeia Digest para obtener más detalles sobre las propuestas del mes.

## Red

Hashrate: el [hashrate](https://dcrdata.decred.org/charts?chart=hashrate&zoom=kpb32srm-kqn8vbkn&scale=linear&bin=block&axis=time) de junio se abrió a ~ 369 Ph / sy cerró ~ 73 Ph / s, tocando fondo en 61 Ph / sy alcanzando un máximo de 438 Ph / s durante todo el mes.

Como puede visualizar arriba, junio tuvo una gran caída en el hashrate debido a que los mineros se mudaron fuera de China debido a una [prohibición](https://www.coindesk.com/chinas-bitcoin-mining-crackdown-is-a-boon-for-miners-elsewhere) reciente. Esto es especialmente visible en monedas extraídas de ASIC como Decred y [Bitcoin](https://twitter.com/krugermacro/status/1409484360651317250).

Distribución del hashrate [reportada](https://miningpoolstats.stream/decred) en los pools el 1 de julio:

- Poolin 37%
- F2Pool 28%
- Antpool 8%
- Luxor 5%
- BTC.com 5%
- HuobiPool 1%
- UUPool 0.2%
- CoinMine 0.1%. 

La distribución de 1 000 bloques [realmente extraídos](https://miningpoolstats.stream/decred) casi coincide con el hashrate informado. Los bloques minados al 15% no identificados se dividen entre las mismas 4 direcciones mencionados con [anterioridad](https://xaur.github.io/decred-news/journal/202105).

Staking: el [precio de los tickets](https://dcrdata.decred.org/charts?chart=ticket-price&zoom=kpb32srm-kqn8vbkn&bin=window&axis=time&visibility=true-true) varió entre 168-208 DCR, con un [promedio](https://dcrstats.com/) de 30 días de 184.7 DCR (-1).

La [cantidad bloqueada](https://dcrdata.decred.org/charts?chart=ticket-pool-value&zoom=kpb32srm-kqn8vbkn&scale=linear&bin=block&axis=time) fue de 7.33 a 7.72 millones de DCR, lo que significa que entre el 56.1 y el 59% del suministro circulante [participó](https://dcrdata.decred.org/charts?chart=stake-participation&zoom=kpb32srm-kqn8vbkn&scale=linear&bin=block&axis=time) en el proof-of-stake.

VSP: El 1 de julio, los servidores vspd administraron ~ 8 000 (-200) tickets en vivo y los servidores dcrstakepool [enumerados](https://decred.org/vsp/) aproximadamente 600 (-500). En conjunto, los 12 VSP heredados y los 13 nuevos administraron el 20.9% del grupo de tickets, en comparación con el 22,7% del 1 de junio. Los VSP heredados excluidos de la lista que aún siguen activos administraron 26 tickets en vivo (-35).

Nodos: A lo largo de junio, hubo alrededor de 216 nodos accesibles según [dcrextdata](https://analytics.planetdecred.org/nodes).

Versiones de nodo a partir de la [instantánea](https://nodes.jholdstock.uk/user_agents) del 1 de julio (256 en total, solo dcrd): 

- v1.6.2–53%
- v1.6.0–19%
- v1.6.1–13%
- compilaciones de desarrollo v1.7 - 7%
- compilaciones de desarrollo v1.6 - 3%
- v1.5.1–2.8%
- v1.5.2–2%.


La proporción de [monedas mezcladas](https://dcrdata.decred.org/charts?chart=coin-supply&zoom=jzh4wow9-ks9hgjcu&bin=day&axis=time&visibility=true-true-true) varió entre el 43.7% y el 47% y alcanzó un nuevo máximo histórico.

La red [lightning network](https://ln-map.jholdstock.uk/) de Decred ha visto 34 nodos (+1), 60 canales (+7) con una capacidad total de 21.8 DCR (+4.7), al 1 de julio.

## Ecosistema

[Stakey.net](https://stakey.net/) ha [eliminado](https://citadel.stakey.net/@support/106416385081730641) la interfaz web de su instancia heredada de dcrstakepool. Las carteras de votación y la API se mantendrán hasta que los usuarios migren a vspd. A partir del 1 de julio, el VSP heredado de stakey.net gestionaba 63 tickets en vivo, frente a los 134 del 1 de junio. Su [instancia vspd](https://stakey.net/) se ha convertido en la más grande, con más de 2,200 tickets en vivo.

Para mantener la descentralización, se recomienda evitar proveedores que controlen demasiados tickets. Stakey.net se convierte en un "problema" aquí, ya que es el único VSP conocido que ofrece un servicio oculto Tor. ¡Otros proveedores son bienvenidos a la competencia!

dcr.farm ahora redirige su [instancia vspd](https://vsp.dcr.farm/), aún así @infertux [confirmó](https://github.com/decred/dcrwebapi/issues/146#issuecomment-865451784) que sus billeteras heredadas están activas y se mantendrán hasta que se voten todas las entradas (32 permanecieron activas hasta el 22 de junio). El estado de las carteras heredadas y vspd de dcr.farm se puede comprobar en una página de [estado dedicada](https://stats.uptimerobot.com/46PWkSrZD).

El VSP heredado de [YieldWallet](https://yieldwallet.io/) votó su último ticket y se cerró definitivamente. ¡Gracias por el servicio!

El nuevo VSP de crypto-synergy.net está disponible en [mainnet](https://vspd.synergy-crypto.net/) y [testnet](https://vspd-testnet.synergy-crypto.net/). La instancia de mainnet informa su primer ticket votado (un requisito para todos los nuevos VSP), pero debe pasar la [revisión](https://github.com/decred/dcrwebapi/pull/147) para aparecer en [decred.org/vsp](https://decred.org/vsp/).

En este punto, los VSP heredados tienen menos del 1.4% del grupo de tickets y se [recomienda](https://twitter.com/JamieHoldstock/status/1405069123453784065) actualizar a vspd para evitar el riesgo de tickets perdidos, p. Ej. en un escenario donde se active otra actualización de consenso mientras [dcrstakepool](https://github.com/decred/dcrstakepool) no está parcheado para seguir en la cadena.

Se recomienda a los usuarios de Ledger Live que se [actualicen](https://www.ledger.com/ledger-live) a la versión 2.29.0 o posterior cuando se hayan solucionado los [problemas](https://status.ledger.com/incidents/j1sypv88pgs6) de sincronización y envío de DCR. La interrupción entre las primeras [menciones](https://status.ledger.com/incidents/j1sypv88pgs6) del problema y el lanzamiento de [v2.29.0](https://github.com/LedgerHQ/ledger-live-desktop/releases/tag/v2.29.0) duraron alrededor de 22 días.

Indian [WazirX](https://wazirx.com/) ha [habilitado](https://twitter.com/WazirXIndia/status/1408022090750496776) el comercio DCR / INR y DCR / USDT. DCR fue parte del proceso de ["Listado Rápido"](https://blog.wazirx.com/rapid-listing-initiative-on-wazirx/) donde el comercio comienza antes, pero las opciones de depósito y retiro son limitadas hasta que se complete la integración. En el caso de esta lista, los depósitos y retiros entre billeteras entre WazirX y Binance están [disponibles](https://twitter.com/WazirXIndia/status/1407655011925073921) sin comisiones. WazirX fue [adquirido](https://www.binance.com/en/blog/404105749895733248/Binance-Acquires-Indias-Leading-Digital-Asset-Platform-WazirX-to-Launch-Multiple-FiattoCrypto-Gateways) por Binance en 2019.

Para aquellos que se lo perdieron, vale la pena destacar dos servicios menos conocidos en el ecosistema más amplio de Decred. Una es una alternativa de Twitter llamada stakey.net:

> Esta ciudadela Decred es una instancia de Mastodon modestamente rápida, segura y actualizada con disponibilidad de servidor monitoreada y copias de seguridad externas nocturnas. Abierto para toda la comunidad de Decred. (enlace de invitación [aquí](https://citadel.stakey.net/@support/105249104743040856))

Otra es la instancia de [PeerTube de @karamble](https://tube.decredcommunity.org/videos/recently-added) que refleja el contenido en video de Decred para aumentar la resiliencia y la descentralización.

Advertencia: los autores de la revista DEcred no tienen idea de la confiabilidad de ninguno de los servicios mencionados anteriormente. Haga su propia investigación antes de confiar su información personal o sus activos a cualquier entidad.

Únase a nuestro chat de [#services](https://chat.decred.org/#/room/#services:decred.org) para seguir las actualizaciones del ecosistema Decred.
