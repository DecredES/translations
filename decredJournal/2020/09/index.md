# Revista Decred — Septiembre 2020

![Estructuras](./assets/202009.png) 

Imagen: Estructuras ocultas en órbita cuadrática por @saender

Lo más destacado de Decred para septiembre:

- El PR para descentralizar el gasto del fondo de tesorería finalmente se fusionó, después de un proceso de revisión integral.
- El dcrdex está abordando muchos escenarios sofisticados de intercambio sin confianza descubiertos en las primeras pruebas, el primer intercambio de mainnet se realizó a principios de octubre y el MVP debería estar listo para el uso general pronto.
- La primera propuesta de RFP sobre Politeia, para cambiar los mensajes en decred.org, fue aprobada y recibió 4 propuestas candidatas. La votación comenzará pronto.
- El sitio de métricas en cadena dcronchain.com, aprobado por una propuesta en junio, ya se ha lanzado.
- El portal de incorporación withdecred.org tuvo su lanzamiento inicial y también se presentó una propuesta asociada para financiar los obsequios promocionales, aprobada a principios de octubre.

## Desarrollo

A menos que se indique lo contrario, el trabajo que se informa aquí tiene el estado "fusionado con la rama master". Significa que el trabajo se completó, revisó e integró en el código fuente que los usuarios avanzados pueden construir y ejecutar, pero aún no está disponible en los binarios del lanzamiento en general.

[dcrd](https://github.com/decred/dcrd):

El PR para descentralizar al fondo de tesorería obtuvo 576 comentarios de revisión, se cambió 115 archivos, se agregó 15 000 líneas de código y tomó ~ 5 meses desde que se publicó el primer borrador. Varios desarrolladores han sido retirados de otros proyectos para revisar y probar a fondo este código crítico para el consenso. ¡Gracias a todos por el arduo trabajo en este cambio épico!

DCP0006 [bajo revisión](https://github.com/decred/dcps/pull/17).

Seguimiento al PR para descentralizar al fondo de tesorería:

- [Migración unidireccional](https://github.com/decred/dcrd/pull/2336) de la base de datos para respaldar la nueva implementación del fondo de tesorería.
- [Registro](https://github.com/decred/dcrd/pull/2350) de la transacción tspend (gasto) en el mempool.
- Nuevos mensajes en los pares para [retransmitir](https://github.com/decred/dcrd/pull/2349) las transacciones tspend a medida que se inician los nodos (esto es para ayudar tanto a los nodos de minería como a las carteras de votación a descubrir los tspends de manera más oportuna).
- Nuevo comando RPC para [contar](https://github.com/decred/dcrd/pull/2351) los votos de las transacciones tspend (inicialmente solo se pueden consultar los tspends en el mempool o que se extrajeron).
- Se [eliminó](https://github.com/decred/dcrd/pull/2389) una parte del código para calcular los valores de la ventana de gasto.
- [Reescritura](https://github.com/decred/dcrd/pull/2394) en el paquete `standalone` y pruebas al 100%.

Más trabajo introducido:

- [Caché](https://github.com/decred/dcrd/pull/2358) de firmas optimizado.
- Lógica para [prohibición / lista blanca](https://github.com/decred/dcrd/pull/2363).
- [Privilegios](https://github.com/decred/dcrd/pull/2357) de servicio systemd más restrictivos.
- [Puntos de control actualizados](https://github.com/decred/dcrd/pull/2370) y [menor trabajo en cadena](https://github.com/decred/dcrd/pull/2371) para la próxima actualización.
- Actualizaciones en la dependencia para el siguiente lanzamiento.
- Mejoras menores en la cobertura de prueba, registro, manejo de errores, etc.

@matheusd desarrolló una [herramienta](https://github.com/matheusd/tspend) para generar las transacciones tspend que se pueden usar en configuraciones con espacios abiertos (sin requerir una conexión de red a una instancia de dcrd). Funciona en combinación con la herramienta [ss](https://github.com/jrick/ss) de @jrick para el cifrado de flujo y archivos post-cuánticos.

[dcrwallet](https://github.com/decred/dcrwallet):

- [Soporte](https://github.com/decred/dcrwallet/pull/1714) para el gasto del fondo de tesorería descentralizado, nueva herramienta para generar las claves en los operadores de la red.
- [Advertir](https://github.com/decred/dcrwallet/pull/1822) al descargar claves públicas extendidas (si el xpub se filtra en combinación con cualquier clave privada de la cuenta, esto revela todas las claves privadas de la cuenta).
- Manejar el [cambio](https://github.com/decred/dcrwallet/pull/1830) para la compra de tickets sin mezclar.
- Guardar transacciones [no publicadas](https://github.com/decred/dcrwallet/pull/1838) en la base de datos (necesario para evitar que algunas salidas de billeteras anteriores se gasten dos veces en los reinicios, o para persistir tx parcialmente firmado; esto será utilizado por los clientes vspd).
- Nueva bandera para agregar tickets [manualmente](https://github.com/decred/dcrwallet/pull/1833) y no descubrirlos a través de la sincronización de red (los administradores de vspd usarán esta bandera para evitar que sus usuarios obtengan votos gratis al reutilizar su dirección de votación. Con esta bandera configurada, los tickets se pueden agregar al vspd a través de la API adecuada).
- Agregar script para listar los P2SH [no gastados](https://github.com/decred/dcrwallet/pull/1842) (esto es para dcrdex).
- Cambios en soporte para el [vspd](https://github.com/decred/dcrwallet/pull/1840).
- Implementar el método [sendrawtransaction](https://github.com/decred/dcrwallet/pull/1846).
- Las pruebas exhaustivas realizadas por los clientes de vspd y dcrdex ayudaron a identificar y corregir numerosos errores.


[Decrediton](https://github.com/decred/decrediton):

- Reuso del componente [checkbox](https://github.com/decred/decrediton/pull/2663) en pi-ui.
- Refactorización continua a componentes funcionales y módulos CSS.
- Múltiples correcciones de errores

En progreso:

- Soporte de [vigilancia](https://github.com/decred/decrediton/pull/2638) en la red lighting.
- Mejoras de [UI / UX](https://github.com/decred/decrediton/pull/2641) en la red lighting.


[Politeia](https://github.com/decred/politeia):

- [Pruebas](https://github.com/decred/politeia/pull/1296) para la base de datos de usuarios.
- Uso optimizado de memoria con [paginación](https://github.com/decred/politeia/pull/1306).
- Comando admin de [reinicio](https://github.com/decred/politeia/pull/1298) TOTP.

CMS:

- [Búsqueda](https://github.com/decred/politeiagui/pull/2131) de usuario agregada.
- [Reemplazar](https://github.com/decred/politeia/pull/1300) el uso del caché restante para despejar el camino para la migración de tlog.
- Implementación de [LevelDB](https://github.com/decred/politeia/pull/1302) para la infraestructura de prueba.

En progreso:

- Inicio de sesión 2FA con [TOTP](https://github.com/decred/politeia/pull/1212) (códigos basados ​​en el tiempo).
- Consultar [las estadísticas del código](https://github.com/decred/politeia/pull/1185) del contratista para los administradores de CMS.
- Implementación de tlog en el [backend](https://github.com/decred/politeia/pull/1180) y la [GUI](https://github.com/decred/politeiagui/pull/2142).

Actualización de estado por parte de @lukebp:

> La mayor parte del desarrollo de politeia se centró en tlog el mes pasado. El trabajo de frontend y backend para que coincida con la funcionalidad politeia existente está completo. Las próximas semanas se centrarán en probar tlog, solucionar errores, escribir documentación y agregar cobertura de prueba al código. La única característica que aún no se ha implementado es la capacidad de recuperar la prueba de inclusión para una pieza específica de datos de politeia. El backend de politeiad actualmente admite esto, pero es necesario agregar las rutas de politeiawww correspondientes, así como una forma de mostrar / descargar las pruebas de inclusión en la GUI. Esta funcionalidad se agregará antes del lanzamiento.

[vspd](https://github.com/decred/vspd):

- Almacenar registros de hasta 10 [cambios](https://github.com/decred/vspd/pull/180) de elección de voto para cada ticket, para una responsabilidad bidireccional.
- Requerir que dcrwallet se ejecute en [modo de tickets manuales](https://github.com/decred/vspd/pull/187).

[dcrpool](https://github.com/decred/dcrpool):

- Actualizar la base de código a los [tipos de error](https://github.com/decred/dcrpool/pull/245) Go 1.13
- [Error](https://github.com/decred/dcrpool/pull/247) de reconexión fijo.

[dcrlnd](https://github.com/decred/dcrlnd):

- El PR para la [portabilidad](https://github.com/decred/dcrlnd/pull/103) se ha actualizado con todo el trabajo realizado hasta la versión v0.11.1-beta. Eso nos pondrá a la par con el último lanzamiento actual de lnd.

[dcrdex](https://github.com/decred/dcrdex):

- Implementar [vista del historial](https://github.com/decred/dcrdex/pull/644) de pedidos con filtros y desplazamiento infinito, y vista de detalles de pedidos con todas las coincidencias y relevantes.
- Mostrar [importes bloqueados](https://github.com/decred/dcrdex/pull/683) en contratos y actualizar saldos en más casos.
- Se agregaron rutas [`match_status`](https://github.com/decred/dcrdex/issues/643) y [`order_status`](https://github.com/decred/dcrdex/pull/687) para recuperarse de casos inusuales descubiertos en las pruebas, como la suspensión de computadoras portátiles o la conectividad deficiente que hace que los clientes pierdan el paso `revoke_match` (reiniciar el programa dexc lo soluciona, pero era un mal UX).
- [Manejo](https://github.com/decred/dcrdex/pull/663) mejorado de la reconexión.
- Manejo más robusto de coincidencias [perdidas](https://github.com/decred/dcrdex/pull/661).
- Devolver pedidos [activos](https://github.com/decred/dcrdex/pull/677) en respuesta de `conexión`.
- [Desbloquear](https://github.com/decred/dcrdex/pull/648) monedas en más casos cuando ya no sean necesarias ([lea](https://github.com/decred/dcrdex/pull/648#issuecomment-688585289) este comentario aleatorio para tener una idea de cuántos casos deben considerarse en un protocolo de intercambio sin confianza).
- [Notificar](https://github.com/decred/dcrdex/pull/649) al usuario de la penalización.
- Período de gracia para nuevos usuarios cuando no se aplica el umbral de la tasa de [cancelación](https://github.com/decred/dcrdex/pull/638).
- Mejor manejo de la [redención](https://github.com/decred/dcrdex/pull/513) cuando Maker se apaga después del intercambio de Taker.
- Múltiples correcciones de verificación de [inacción](https://github.com/decred/dcrdex/pull/680).
- Requerir [contraseña](https://github.com/decred/dcrdex/pull/621) para la cliente RPC.
- [Registro](https://github.com/decred/dcrdex/pull/654) de depuración opcional en la interfaz de usuario.
- Muchos cambios internos y correcciones de errores.

Se [fusionaron](https://github.com/decred/dcrdex/pulls?q=is%3Apr+merged%3A2020-09-01..2020-09-30+sort%3Aupdated-asc) un total de 35 RP de 4 colaboradores, agregando 9 000 y eliminando 2 600 líneas de código.

[La encuesta](https://twitter.com/chappjc/status/1302795835248439296) de Twitter mostró interés en el soporte de LTC en mainnet beta.

> Los primeros intercambios atómicos de la red principal DCR-BTC coordinados por #dcrdex se llevaron a cabo ayer. Las pruebas y el desarrollo continúan, pero la conversación se ha trasladado a la distribución de software y los tutoriales. Tiempos emocionantes para @decredproject. (@chappjc, [9 de octubre](https://twitter.com/chappjc/status/1314436781891301376))

[dcrandroid](https://github.com/planetdecred/dcrandroid):

- Traducción [china](https://github.com/planetdecred/dcrandroid/pull/515) actualizada.
- Corrección de errores.

En progreso:

- Mostrar propuestas de [Politeia](https://github.com/planetdecred/dcrandroid/pull/503).

[dcrios](https://github.com/planetdecred/dcrios):

- Corrección de errores.

En progreso:

- Mostrar [propuestas](https://github.com/planetdecred/dcrios/pull/715) de Politeia
- [Pruebas](https://github.com/planetdecred/dcrios/pull/707) de IU automatizadas.

[dcrros](https://github.com/decred/dcrros):

- [Actualizado](https://github.com/decred/dcrros/pull/6) a la v1.4.4 de las especificaciones de Rosetta que incluye la capacidad de construir, firmar y publicar transacciones. El conjunto de pruebas de verificación: construcción del correspondiente rosetta-cli para esta especificación está pasando en este PR.

Rosetta v1.4 lanzó la API de construcción (anteriormente API de Wallet) para construir transacciones en un formato estándar, que no se terminó cuando anunciamos la implementación de Rosetta de Decred en [junio](https://github.com/DecredES/traducciones/blob/master/revista-decred/2020/202006.md). Esta API es compatible con los últimos dcrros y se está trabajando para mantenerla al día con las especificaciones, así como con los próximos cambios en el consenso de Decred.

[docs](https://github.com/decred/dcrdocs):

- Reemplazar una [propuesta](https://github.com/decred/dcrdocs/pull/1127) de desarrollo de ejemplo con una de mayor escala.
- Reemplazar las secciones [plegables](https://github.com/decred/dcrdocs/pull/1129) específicas del sistema operativo con pestañas adecuadas.

[dev docs](https://github.com/decred/dcrdevdocs):

- [Mover](https://github.com/decred/dcrdocs/pull/1126) la página de [selección de tickets](https://devdocs.decred.org/developer-guides/ticket-selection/) de dcrdocs.
- [Agregar](https://github.com/decred/dcrdevdocs/pull/86) una [descripción general](https://devdocs.decred.org/developer-guides/transactions/txscript/overview/) y una [referencia de códigos de operación](https://devdocs.decred.org/developer-guides/transactions/txscript/opcodes/) para el sistema txscript usado en Decred (es un lenguaje de programación simple, basado en pila, similar a Forth).

[decred.org](https://github.com/decred/dcrweb):
- Contribuidores [Latam](https://github.com/decred/dcrweb/pull/909) agregados.
- Actualizaciones de backend.

Otros:
El programa Bug Bounty publicó una nueva [actualización](https://bounty.decred.org/2020/09/status-update/) y realizó [cambios](https://github.com/decred/dcrbounty/pull/71/files) en las reglas y el alcance según la experiencia con envíos recientes.

## Comunidad

Estadísticas de la comunidad a partir del 1 de octubre:

- Seguidores en Twitter: 40 790 (-26)
- Suscriptores en Reddit: 9 929 (+23)
- Usuarios en la sala #general de Matrix: 197 (+23)
- Usuarios en Discord: 1 396 (+2)
- Usuarios en Telegram: 2 434 (-34)
- Suscriptores en YouTube: 4 210 (+30), vistas: 156 000 (+1 700)
- Seguidores en Facebook: 3 655 (+0), me gustas: 3 305 (-6)
- Seguidores en LinkedIn: 891 (+16)
- Estrellas en el repositorio dcrd en GitHub: 563 (+6), forks: 248 (+2)

Los gráficos de estas estadísticas están disponibles en el [repositorio](https://github.com/decredcommunity/social-media-stats/blob/graphs/graphs/index.md) de estadísticas de redes sociales (más cuentas rastreadas) y en la instancia [dcrextdata](https://dcrextdata.planetdecred.org/community) de Planet Decred (gráficos dinámicos con alta resolución).

## Gobernanza

En septiembre, [el fondo de tesorería](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx) recibió 12 300 DCR y gastó 5 740 DCR. Con la tasa promedio diaria de DCR / USD en agosto de $13.6, esto es 163 000 USD recibidos y 76 000 USD gastados. A la tasa promedio diaria de agosto de $17.02, la cifra en USD facturada por el trabajo completado en ese mes es de 98 000 USD. A partir del 3 de octubre, el saldo del fondo de la tesorería es de 640,000 DCR (7.5 millones de dólares a $11.69).

- La [propuesta](https://proposals.decred.org/proposals/1e55a41) de @exitus para la producción de videos fue aprobada con un 94.6% a favor y una participación del 31%.
- La [propuesta](https://proposals.decred.org/proposals/2bf72e6) para promocionar el nuevo sitio web withdecred.org con regalos en DCR fue enviada en septiembre y aprobada a principios de octubre con 62% de votos a favor y una participación del 37%.
- La [propuesta](https://proposals.decred.org/proposals/f279ed5) para pagarle a @alexsolo por el trabajo realizado en 2016 al 2018 fue rechazada con un 8% a favor y una participación del 28%.
- Se aprobó una [propuesta](https://proposals.decred.org/proposals/91becea) de RFP para cambiar los mensajes en decred.org con un 85% de aprobación y un 29% de participación. Se presentaron 4 propuestas antes de la fecha límite del 28 de septiembre y, una vez que estén todas listas, comenzará la segunda votación. Solo se puede aprobar una de estas propuestas y aún debe cumplir con los requisitos habituales de aprobación y quórum.

Consulte el [#36](https://blockcommons.red/politeia-digest/issue036/) y el [#37](https://blockcommons.red/politeia-digest/issue037/) del Politeia Digest para obtener una revisión más detallada.

@bee publicó una [lista de verificación completa](https://github.com/decredcommunity/guidelines/blob/master/proposals.md) para las propuestas exitosas de Politeia basadas en la experiencia con propuestas anteriores.

Se han importado 4 actualizaciones en el [repositorio de propuestas](https://github.com/decredcommunity/proposals/tree/master/proposals). Todavía no hay un índice adecuado, pero los enlaces directos funcionan ([ejemplo](https://github.com/decredcommunity/proposals/blob/master/proposals/95cfb73/updates/20200902.md)). Envíe sus actualizaciones para ayudar a recopilarlas todas en un solo lugar.

## Red

Hashrate: el [hashrate](https://explorer.dcrdata.org/charts?chart=hashrate&zoom=kegbelov-kfrbnmg7&scale=linear&bin=block&axis=time) de septiembre abrió a ~ 460 Ph/s y cerró a ~ 450 Ph/s, tuvo un mínimo en 338 Ph/s y alcanzó un máximo de 609 Ph/s durante todo el mes.

[Distribución del hashrate en los pools](https://miningpoolstats.stream/decred) a partir del 1 de agosto (aproximado):

- UUPool 35%.
- Poolin 27%.
- Huobipool 11%.
- Easy2mine 10%.
- Antpool 9%.
- BTC.com 3%.
- Luxor 0.9%.
- F2Pool 0.5%.
- Okex 0.2%.
- CoinMine 0.02%.
- Otros ~ 3%.

Tenga en cuenta que hemos cambiado de [dcrstats.com/pow](https://dcrstats.com/pow) a [miningpoolstats.stream](https://miningpoolstats.stream/decred) porque identifica un ~20% más de hashrate.

Staking: el precio [promedio del ticket a 30 días](https://dcrstats.com/) fue de 148.6 DCR (-2.8). [El precio](https://explorer.dcrdata.org/charts?chart=ticket-price&zoom=kegbelov-kfrbnmg7&bin=window&axis=time&visibility=true-false) varió entre 144.7–152.5 DCR. [El monto bloqueado por participación](https://explorer.dcrdata.org/charts?chart=ticket-pool-value&zoom=kegbelov-kfrbnmg7&bin=block&axis=time) fue de 6.06–6.12 millones de DCR, que correspondió al 50.38%–51.04% del [suministro total en circulación](https://explorer.dcrdata.org/charts?chart=stake-participation&zoom=kegbelov-kfrbnmg7&bin=block&axis=time).

Nodos: en [septiembre](https://charts.dcr.farm/d/000000014/nodes?orgId=1&from=1598918400000&to=1601510400000) hubo un promedio de 108 nodos públicos y 133 nodos por parte de dcr.farm.

Distribución promedio por versión en septiembre:

- 26% dcrd v1.5.1.
- 22% dcrd v1.5.2.
- 7% dcrd v1.6 dev builds.
- 7% dcrd v1.5.0.
- 4% dcrd v1.5 dev and RC builds.
- 0.8% dcrd v1.4.
- 17% dcrwallet v1.5.1.
- 1.6% dcrwallet v1.5.
- 1.1% dcrwallet v1.4.
- 15% otras versiones.

[dcronchain.com](https://dcronchain.com/) se lanzó cuatro meses después que se aprobó su [propuesta](https://proposals.decred.org/proposals/0230918) en junio. La versión inicial incluye 5 gráficos interactivos derivados de los datos en cadena de Decred, basados ​​en la investigación de @Checkmate y @PermabullNino. El equipo agradece cualquier comentario en [Reddit](https://www.reddit.com/r/decred/comments/j3589s/release_dcronchaincom_onchain_researchgraphs_in/). El código fuente está disponible en [GitHub](https://github.com/Decred-Bulls/dcronchain). ¡Felicidades por el lanzamiento!

## Integraciones

La casa de cambio brasileña NovaDAX el cual [listó a DCR en junio](https://twitter.com/Decred_BR/status/1275190825060794377) ahora [agregó](https://twitter.com/Decred_BR/status/1305922555124035584) soporte para DCR en sus tarjetas de débito. Esto permitirá el acceso a más de 23.000 cajeros automáticos y terminales POS en todo el país.

> NovaDAX está entre los 3 primeros en el mercado BR. Con la nueva tarjeta de débito, es posible pagar cualquier factura en lugares que aceptan [Elo](https://en.wikipedia.org/wiki/Elo_(card_association)), que en Brasil tiene la misma adopción que Visa y Mastercard. Además, es posible realizar transferencias bancarias en BRL, deduciendo DCR de su cuenta y sin pagar comisiones de transferencia, algo que cobran todos los bancos de Brasil. También es posible intercambiar DCR por BRL en los cajeros automáticos de Banco24horas, con alrededor de 23 mil máquinas en Brasil. NovaDAX está abriendo una sucursal en Portugal y tiene la intención de hacer lo mismo en el mercado europeo. ([@emiliomann](https://matrix.to/#/!rLQWsgjPJFAClvskmU:decred.org/$QD-Fxk-3mm9wiuR3f1DQqJ-K4yQQcFFmoQYfx8r40jE)).

Se [añadió](https://github.com/decred/dcrweb/pull/907) la casa de cambio [Swyftx](https://swyftx.com.au/) a decred.org. Cuenta con [muchas características](https://swyftx.com.au/features/) y permite a los usuarios obtener DCR con AUD.

Advertencia: los autores de la Revista Decred no tienen idea de la confiabilidad de alguno de los servicios anteriores. Haga su propia investigación antes de confiar su información personal o activos.

## Alcance

La segunda [propuesta](https://proposals.decred.org/proposals/1e55a41) de @Exitus para hacer contenido de video por otros 6 meses fue aprobada con un gran apoyo. @Checkmate se unirá a la segunda fase para ayudar con los scripts y los comentarios. La propuesta compartió algunas estadísticas de los últimos 6 meses: 21 000 vistas ganadas con una tasa de me gusta del 98%, ~ 500 suscriptores ganados y ~ 250 perdidos, 170 comentarios recibidos. El video más popular fue [DCR 101 - How to Stake Decred 2020](https://www.youtube.com/watch?v=m5lcm6yttEk) con 1 600 vistas. Varios videos subidos a Twitter obtuvieron ~ 18 000 vistas.

@pavel, @pablito y @el_capitan [lanzaron](https://www.reddit.com/r/decred/comments/it9mkf/withdecredorg_new_portal_to_onboard_newcomers_to/) un nuevo sitio web [withdecred.org](https://withdecred.org/) para encontrar un nuevo enfoque escalable sobre cómo incorporar nuevos usuarios a la comunidad de Decred. El sitio web contiene una serie de artículos que forman un "embudo" estructurado que lleva a la persona a comprar algunos DCR. Siguió una [propuesta](https://proposals.decred.org/proposals/2bf72e6) para financiar las operaciones y una distribución de $5,000 en DCR para impulsar el lanzamiento inicial, aprobada a principios de octubre. Históricamente, algunos miembros de la comunidad se han mostrado escépticos sobre los regalos y este proyecto finalmente traerá algunos datos y evaluará el ROI de ese modelo. La cuenta de Twitter complementaria es [@withdecred](https://twitter.com/withdecred).

Algunos miembros de la comunidad se [organizaron](https://www.reddit.com/r/decred/comments/it0idm/decred_on_quora/) para responder varias preguntas sobre Decred en Quora.

@pavel comenzó a experimentar [contenido](https://www.publish0x.com/crypto-as-an-agent-for-change/monero-and-decred-are-the-new-bitcoin-xlldpze) de [Decred](https://www.publish0x.com/withdecred/why-we-need-decred-an-inclusive-approach-to-sound-money-xgdwkjl) en [Publish0x](https://github.com/Decred-Bulls/decred-marketing#why-to-invest-time-into-publish0xcom), ya que es un portal de cifrado prometedor.

@pablito y @caibarrad lanzaron el primer episodio del podcast de Decred en Español, disponible en [YouTube](https://twitter.com/Decred_ES/status/1310654270056923136) y [Spotify](https://twitter.com/Decred_ES/status/1310055071200292869).

@jazzah publicó un [concurso](https://www.reddit.com/r/decred/comments/ifyb03/contest/) con el tema “KYC vs Shuffle ++” en el que los participantes deben completar tareas no triviales al inspeccionar una imagen loca e hilarante. Se reclamó el premio n° 1, pero los premios 2-4 aún están abiertos para todos.

Los logros de Monde PR para septiembre:

- creó / presentó 2 historias en publicaciones financieras y criptográficas
- respondió a 3 solicitudes de comentarios
- respondió a 2 noticias sobre DCR

Cobertura de noticias por parte de Monde PR:

- Un artículo en la [revista Authority](https://medium.com/authority-magazine/meet-the-disruptors-how-jake-yocom-piatt-of-decred-aims-to-redefine-governance-with-blockchain-5c3724f20e74) con comentarios de @jy-p sobre cómo Decred pretende redefinir la gobernanza con la tecnología blockchain.
- Un artículo en [AMB Crypto](https://eng.ambcrypto.com/will-defi-crash-the-crypto-economy-the-same-way-cdos-did/) con comentarios de @richardred sobre la "burbuja DeFi", distribuido a 12 medios de comunicación, incluidos [Crypto Fund Report](https://www.cryptofundreport.com/articles/will-defi-crash-the-crypto-economy-the-same-way-cdos-did/) y [Coingenius.news](https://coingenius.news/will-defi-crash-the-crypto-economy-the-same-way).
- Un artículo en [The Daily Chain](https://thedailychain.com/decred-clarify-details-of-reported-vulnerability/) con comentarios de @davecgh que aclaran los detalles de una vulnerabilidad reportada.

## Eventos

Atendidos:

- 04 de septiembre — [Hablemos Decred 11](https://twitter.com/Decred_ES/status/1301583356644282368) — Internet. @elian y el invitado Jose Zarate de Stamping.io discutieron sobre el estampado en el tiempo en blockchain. ([video](https://www.youtube.com/watch?v=QwsWiJ8v5qE)) 
- 10 de septiembre — [Hablemos Decred 12](https://twitter.com/Decred_ES/status/1304153821631791104) — Intenet. @caibarrad y @elian invitaron a David Riascos de @cLabs para hablar sobre la importancia de la comunidad en el desarrollo de protocolos abiertos y los desafíos de la adopción en la industria. ([video](https://www.youtube.com/watch?v=QC5_1PqJb_4))
- 17 de septiembre — [Hablemos Decred 13](https://twitter.com/Decred_ES/status/1305595709257846785) — Internet. @adcade y @elian hablaron con la invitada Nancy Salazar de Platzi sobre como comenzar una carrera en tecnología y como resolver los desafíos en un área compleja como blockchain. ([video](https://www.youtube.com/watch?v=f_ppC-GVDk8))
- 25 de septiembre — [Hablemos Decred 14](https://twitter.com/Decred_ES/status/1308582624772927494) — Internet. @elian y la invitada Eloisa Cadenas de CryptoFintech exploraron el origen del [maximalismo](https://es.cointelegraph.com/news/wild-crypto-maximalism), el futuro de interoperabilidad blockchain y cuales son los desafíos para la adopción. El evento fue [anunciado](https://es.cointelegraph.com/news/virtual-talk-where-does-the-concept-of-maximalist-come-from) en Cointelegraph en español. ([video](https://www.youtube.com/watch?v=EGaMhQX3Wd4))

Próximos eventos:

- 15 de octubre — Hablemos Decred 17 — Internet. @elian y Gus Grilliesca van a explorar sobre el futuro del arte en las criptomonedas.
- 17 de octubre — [Introducción a la API de Decred](https://www.eventbrite.com/e/open-source-workshop-introduccion-a-blockchain-api-de-decred-dcrdata-tickets-124107662359) — Internet. Será un taller para explorer la blockchain de Decred con la API de dcrdata.
- 19 de octubre — [Open Source Software Summit](https://www.eventbrite.com.mx/e/cumbre-de-contribuidores-de-open-source-software-ccoss-2020-tickets-91491063233) — Internet. @adcade va a presentar a Decred con la plática titulada "El modelo de un contratista open source en la industria de criptomonedas".

## Media

Decred fue mencionado en un [reporte](https://medium.com/greenfield-one/the-state-of-blockchain-governance-governance-by-and-of-blockchains-f6418c46077) sobre la gobernanza en blockchain. Las 115 páginas completas se encuentran [aquí](https://65eocu3ftlpiygeym3g5kply6zy2dtdjyrhbm4m26cb6bt3msyla.arweave.net/90jhU2Wa3owYmGbN1T149nGhzGnEThZxmvCD4M9slhY). (Decred se menciona en las páginas 64-66)

Artículos seleccionados:

Inglés:

- Why I Decred por Decred Citizen. ([medium](https://medium.com/@decred.citizen/why-i-decred-8d83081b6fb8))
- Decred on-chain: DAO + Treasury accounting por @permabullnino. ([medium](https://medium.com/@permabullnino/decred-on-chain-dao-treasury-accounting-afb1ed989b0a))
- Blockchain governance — Part 2 por @mm. ([stakey.club](https://stakey.club/en/blockchain-gov-part2/))
- Meet the Disruptors: How Jake Yocom-Piatt of Decred aims to redefine governance, with blockchain technology por Tyler Gallagher. ([medium](https://medium.com/authority-magazine/meet-the-disruptors-how-jake-yocom-piatt-of-decred-aims-to-redefine-governance-with-blockchain-5c3724f20e74))
- Monero and Decred are the new Bitcoin por John Dennehy. ([medium](https://john-dennehy.medium.com/monero-and-decred-are-the-new-bitcoin-34a8c1fb2515))

> Dado que la descentralización es un principio fundamental del espacio criptográfico, recibe muchos comentarios, pero uno de los problemas más antiguos con el poder es que es extremadamente raro que una vez que alguien lo tenga, lo renuncie voluntariamente. Decred es una rara excepción y notable en el progreso que sus desarrolladores han hecho al convertir los recursos del proyecto en este sistema autónomo. Monero es otro caso atípico aquí, ya que su desarrollo está completamente financiado por donaciones de la comunidad.

Los medios criptográficos han detectado la vulnerabilidad [INVDoS](https://invdos.net/) divulgada el 9 de septiembre, lo que generó una prensa mixta para Decred. La publicación de [CoinDesk](https://www.coindesk.com/high-severity-bug-in-bitcoin-software-revealed-2-years-after-fix) fue la primera y no mencionó a Decred en absoluto. En particular, se publicó solo 45 minutos después de la última actualización del PDF en invdos.net y 28 minutos antes del correo electrónico en la lista de correo de [bitcoin-dev](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2020-September/018164.html). [ZDNet](https://www.zdnet.com/article/researcher-kept-a-major-bitcoin-bug-secret-for-two-years-to-prevent-attacks/) mencionó brevemente el programa de recompensas por errores de Decred. [Decrypt](https://decrypt.co/41685/developers-reveal-2018-bitcoin-bug-used-to-crash-entire-networks) ha exagerado el problema y ha publicado algunas inexactitudes. [The Daily Chain](https://thedailychain.com/bitcoin-engineers-identify-and-patch-vulnerability-in-decred-btcd-blockchains/) llegó a decir que "los ingenieros de Bitcoin parchearon la vulnerabilidad en Decred". Un patrón común es que estos medios no solicitaron comentarios de los expertos más familiarizados con el software (desarrolladores Decred). @l1ndseymm se puso en contacto con The Daily Chain y publicaron una [aclaración](https://thedailychain.com/decred-clarify-details-of-reported-vulnerability/) de seguimiento con un comentario de @davecgh. @degeri abordó la desinformación en un [hilo de tweets](https://twitter.com/degeri_crypto/status/1305591774698786821). Una descripción detallada de la cobertura de los medios, la desinformación, la cronología de los eventos y la reflexión está disponible [aquí](https://github.com/xaur/notes/blob/master/invdos.md).

Traducciones:

- Conozca a los disruptores: cómo Jake Yocom-Piatt de Decred apunta a redefinir la gobernanza, con tecnología blockchain, en [chino](https://github.com/Decred-CN/articles/blob/master/Meet%20The%20Disruptors.md) por @dominic.
- Politeia Digest #36 y #37 al [árabe](https://insaf01.github.io/politeia-digest-ar/) por @arij y @abdulrahman4
- Decred Journal de agosto de 2020 se [tradujo](https://xaur.github.io/decred-news/) al árabe (@arij, @ abdulrahman4), chino (@Dominic) y español (@francov_). ¡Gracias a todos por correr la voz!

[Aquí](https://github.com/decredcommunity/translations/blob/master/index.md) se ha compilado una lista de todas las traducciones conocidas de Decred.

Si traduce contenido, únase a la nueva sala de chat pública [#translations](https://chat.decred.org/#/room/#translations:decred.org) para coordinarse con otros.

Videos:

Inglés:

- The Cost of attacking Decred por Decred Society. ([youtube](https://www.youtube.com/watch?v=yv2wzRsK6zc))
- Security and coin supply por Decred Society. ([youtube](https://www.youtube.com/watch?v=M5HWV_a1gj8))
- Going down the Decred rabbit hole por Decred Society. ([youtube](https://www.youtube.com/watch?v=cI1jbIAe4YE))
- Decred price analysis — 6th September 2020 por Brave New Coin. ([youtube](https://www.youtube.com/watch?v=ABjp9RYnDrk))

Audio:

Inglés:

- Decred in Depth 30 con @eSizeDave y @zohand del equipo de Decred Australia hablando sobre sus experiencias al presentar Decred a varias audiencias: lo que funciona y lo que no. ([libsyn](https://decredindepth.libsyn.com/zohand-dave-decred-australia), [player.fm](https://player.fm/series/decred-in-depth/zohand-dave-decred-australia))
- Decred in Depth 31 con @l1ndseymm que le da su papel de relaciones públicas, su experiencia de trabajar con la comunidad de Decred y pasar por el proceso de propuesta, y las estrategias para elevar el perfil del proyecto. ([libsyn](https://decredindepth.libsyn.com/lindsey-mcconaghy-dcr-pr-marketing-2020), [anchor.fm](https://anchor.fm/staked-podcast/episodes/Staked-Podcast-Episode-0-0-3-ejq685/a-a38c12o))
- Podcast de Cyber ​​Hacker: Crypto-Security e innovaciones en blockchaincon con @ jy-p. ([player.fm](https://player.fm/series/cyber-hacker/crypto-security-and-block-chain-innovations), [apple](https://podcasts.apple.com/au/podcast/cyber-hacker/id1462830605?i=1000489977562))

El Decred dork ha estado ocupado este mes, con 4 episodios del nuevo Podcast Staked:

- Episodio 0.0.1 — History of Decred
- Episodio 0.0.2 — Decred Constitution
- Episodio podcast interview con @pavel.
- Episodio 0.0.3 — Decred investment thesis

Staked Podcast está disponible en [YouTube](https://www.youtube.com/channel/UCWoknbkENz-W4pg18p57rNA) (con video), [anchor.fm](https://anchor.fm/staked-podcast), [Spotify](https://open.spotify.com/show/4KWpxBXn26Ek4VVeNg8D3S) y [Google](https://podcasts.google.com/feed/aHR0cHM6Ly9hbmNob3IuZm0vcy8xNDY5ZjRlYy9wb2RjYXN0L3Jzcw==).

## Discusiones de la comunidad
Noticias en los medios de comunicación:

- El chat de #trading ahora está disponible a través de [Telegram](https://t.me/DecredTrading) y está conectado a Matrix y Discord

Post seleccionados en Reddit:

- El CEO de Wall Street favorito de todos, u / jamie-demon, ha estado ocupado publicando [dcrdocs](https://www.reddit.com/r/decred/comments/j1ia6k/dcrdocs_on_ipfs_and_zeronet/), [decredpower](https://www.reddit.com/r/decred/comments/iu9f31/decredpower_on_the_ipfs/) y [DCRComic](https://www.reddit.com/r/decred/comments/iw333o/dcr_comic_on_ipfs/) en las redes web distribuidas IPFS y ZeroNet.
- Una [publicación](https://www.reddit.com/r/decred/comments/iwu75w/bch_has_some_funding_and_governance_issues/) sobre gobernanza y financiación del BCH atrajo 45 comentarios, principalmente en respuesta a alguien quejándose de DCR.
- @pavel está organizando una entrevista de AMA y envió una [publicación](https://www.reddit.com/r/decred/comments/j2gz5f/ask_me_anything_ama_what_would_you_ask_decreds/) para recopilar preguntas al final del mes.
- [Discusión](https://www.reddit.com/r/decred/comments/i11tjv/porting_cloak_coins_enigma_protocol_and/g4psjpr/) en profundidad sobre los méritos del protocolo de privacidad Enigma de CloakCoin con uno de los desarrolladores de ese proyecto.

Discusiones en Twitter:

- @richardred [tuiteó](https://twitter.com/RichardRed0x/status/1310700935216271360) una imagen animada, titulada "Ticket Price All Time Highs Again".
- Últimas noticias sobre el desarrollo en Twitter de [@moo31337](https://twitter.com/marco_peereboom/status/1308125042149134336) (Descentralizar el gasto del fondo de tesorería) y [@chappjc](https://twitter.com/chappjc/status/1302798545439817730) (dcrdex).
- @jz afirma que Decred es un [#ChadCoin](https://twitter.com/jz_bz/status/1310639727477915648).

## Mercados

En septiembre, DCR cotizaba entre 11.03–17.30 USD / 0.00106–0.00148 BTC La tarifa diaria promedio fue de 13.26 USD.

## Noticias relevantes externas

La cartera Wasabi estaba sujeta a una [vulnerabilidad](https://blog.wasabiwallet.io/responsible-disclosure-v4-hard-fork/) DoS que habría permitido a un atacante detener el proceso CoinJoin para todos los participantes sin revelarse, corregido antes de que pudiera ser explotado.

Cain [resumió](https://read.cash/@Cain/the-current-bch-drama-for-outsiders-50b4dbb8) muy bien la situación actual de Bitcoin Cash. La cadena BCH (también conocida como BCH ABC) parece dispuesta a resolver una disputa sobre la financiación de los desarrolladores. Los desarrolladores de Bitcoin ABC están agregando una regla del 15 de noviembre de que el 8% de la recompensa del bloque debe ir a una dirección controlada por ellos, para financiar el desarrollo de infraestructura. Esta idea ha sido controvertida en la comunidad de BCH durante algún tiempo, y se planea una implementación alternativa de BCHN. Esto establece un escenario interesante de guerra de hash, donde los mineros de ABC no extraerán bloques de BCHN sin una recompensa de los desarrolladores, mientras que los mineros de BCHN minarán cualquier cosa: si la cadena BCHN no tiene una mayoría significativa de hashpower, los mineros de BCHN verían muchos bloques huérfanos. BCH tiene un sistema de puntos de control, que agrega algo más de intriga sobre la posibilidad de divisiones de cadenas y nuevos nodos que terminen en cadenas diferentes. Hasta ahora, alrededor del 50% de la potencia minera de PoW está indicando BCHN, y el resto no indica nada.

BitShares tiene un futuro [hardfork](https://finbold.com/binance-huobi-announces-support-for-upcoming-bitshares-hardfork/) que será apoyado por Binance y Huobi, luego de que la Asociación China de BitShares alegara que uno de los desarrolladores de BitShares había manipulado el código del sistema de votación sin la aprobación de la comunidad.

La saga SushiSwap proporcionó el máximo drama de DeFi en septiembre. SushiSwap es una "intercambio descentralizado" que se ejecuta en Ethereum y que copia los contratos inteligentes de código abierto de un intercambio descentralizado establecido (financiado por VC), UniSwap. Cuando el desarrollador de SushiSwap, Chef Nomi, anunció que SushiSwap haría un "lanzamiento justo" y otorgaría casi todos los tokens SUSHI a los proveedores de liquidez, SushiSwap comenzó a extraer mucha liquidez de UniSwap, y SUSHI ganó un valor considerable en poco tiempo. de tiempo. El 10% de todos los tokens SUSHI se destinan a un fondo de desarrollo, y cuando la exageración estaba en su punto máximo, el Chef Nomi [liquidó](https://www.coindesk.com/sushiswap-liquidation-weekend) el dev SUSHI (con un valor de más de $10 millones en ese momento) en ETH y anunció que no saldría de la estafa porque todavía estaría presente. para hacer desarrollo, pero había vendido todo el dev SUSHI. Esto no fue bien recibido por la comunidad SUSHI, que buscó reemplazar a Nomi en poco tiempo, y Nomi luego entregó las riendas (¿llaves?) A Sam Bankman-Fried del intercambio FTX. SushiSwap luego pasó a elegir un conjunto de gobernadores multi-sig con un voto simbólico. Posteriormente, el Chef Nomi [regresó](https://www.coindesk.com/sushiswap-creator-chef-nomi-returns-dev-fund) junto con el ETH que habían obtenido al vender dev SUSHI, ofreciendo que la comunidad determinara cuánto deberían ser recompensados ​​por su parte. Se especuló que la chef Nomi había sido efectivamente desenmascarado y no quería vivir con el estigma de su salida apresurada.

UniSwap [lanzó](https://uniswap.org/blog/uni/) su propio token, UNI, en respuesta al éxito de SUSHI y la cantidad de liquidez que estaba atrayendo. El 60% de los tokens de génesis (destinados a cubrir los primeros cuatro años) están disponibles para los proveedores de liquidez, y un 15% inicial se asigna a las personas que habían utilizado UniSwap antes del cierre de principios de septiembre. asignados a inversores y empleados.

Ethereum Classic Labs se [ha asociado](https://medium.com/etc-core/ethereum-classic-labs-teams-up-with-openrelay-and-chainsafe-8248d1182612) con Chainsafe y OpenRelay para desarrollar una solución que previene más ataques del 51%. 3 días después del anuncio de la formación de equipos, ya existe un plan integral de [MESS](https://medium.com/etc-core/agreeing-to-disagree-proposing-a-weakly-subjective-finality-solution-for-ethereum-classic-7daad47efc0e) para una finalidad débilmente subjetiva.

El intercambio KuCoin (que enumera DCR) fue hackeado y se [informó](https://www.coindesk.com/hackers-drain-kucoin-crypto-exchanges-funds) que se robaron $150 millones, que luego se [actualizaron](https://www.coindesk.com/kucoin-ceo-says-perpetrators-of-281m-hack-identified-authorities-on-the-case) a $281 millones, aunque posteriormente se [recuperaron](https://www.coindesk.com/kucoin-ceo-says-perpetrators-of-281m-hack-identified-authorities-on-the-case) $204 millones (con la ayuda de los operadores de monedas estables centralizadas) y KuCoin afirma haber identificado a los sospechosos. y los denunció a las autoridades.

Coinbase Pro [anunció](https://twitter.com/CoinbasePro/status/1306641678506360832) que las tarifas por los retiros de criptomonedas ahora se transferirían a los clientes (Coinbase los había cubierto anteriormente para proporcionar retiros "gratuitos").

La casa de préstamos bZxHQ DeFi fue sometida a otro [exploit](https://www.coindesk.com/defi-lender-bzx-third-attack), esta vez por $8 millones, que es más grande que los dos exploits anteriores a principios de este año. Tienen un fondo de seguro que cubre los daños. Según CoinDesk, “el error logró pasar desapercibido en dos extensas auditorías de código de las firmas de ciberseguridad Certik y Peckshield”.

Square [formó](https://www.coindesk.com/square-alliance-patents-crypto) la Cryptocurrency Open Patent Alliance (COPA), donde los miembros se comprometen a nunca hacer valer los derechos de patente con fines ofensivos y, a su vez, pueden usar las patentes de cualquier organización miembro a la defensiva si es necesario. Blockstream [tuiteó](https://twitter.com/Blockstream/status/1304529416131940352) sobre unirse a COPA como el siguiente paso en su estrategia defensiva de patentes.

La Tesorería de Polkadot recibió sus primeras [propuestas](https://polkadot.network/writing-history-the-first-teams-submit-their-proposal-to-the-polkadot-treasury-2/). El Tesoro de Polkadot se financia con tarifas de transacción, reduciendo y apostando ineficiencias, y cada 24 días, si estos fondos no se utilizan, se quema el 1% del saldo. Los fondos son administrados actualmente por el Consejo de Polkadot, y los primeros cuatro equipos que se financiarán.

Este [artículo](https://decrypt.co/41024/researchers-find-new-way-for-criminals-to-launder-money-using-bitcoin) sobre "minería privada", donde un usuario entrega su transacción a un minero específico, quien recolecta la recompensa asociada cada vez que lo extrae en un bloque, lo ve como una posible herramienta para el lavado de dinero y, en el futuro, potencialmente también fuente de ingresos de los mineros.

El Servicio de Impuestos Internos de los Estados Unidos [ofrece](https://cointelegraph.com/news/the-irs-offers-a-625-000-bounty-to-anyone-who-can-break-monero-and-lightning) una recompensa de $625,000 a cualquier persona que pueda proporcionar un prototipo funcional de tecnología para rastrear transacciones de Monero o Lightning Network. La fecha límite era el 16 de septiembre, por lo que, desafortunadamente, ahora es demasiado tarde para sacar provecho de ese prototipo que rompe la privacidad, si tiene uno a mano.

Los fanáticos de la sección de noticias relevantes externas probablemente disfrutarán de la cuenta de Twitter [@Scams_alarms](https://twitter.com/Scams_alarms) para ver historias más horribles.

## Sobre esta edición

Este es la edición #30 de la Revista Decred, un índice de todos los números originales y traducciones se encuentran disponibles [aquí](https://xaur.github.io/decred-news/).

La mayoría de la información de terceros se transmite directamente desde la fuente después de un control de fiabilidad mínimo. Los autores de la Revista Decred no tienen la capacidad de verificar todas las reclamaciones. Tenga cuidado con las estafas y haga su propia investigación.

Puede enviar una historia [aquí](https://github.com/xaur/decred-news/labels/next%20release) para ser considerada para el próximo número. Los [comentarios](https://github.com/xaur/decred-news/blob/docs/contributing.md#feedback) y las [contribuciones](https://github.com/xaur/decred-news/blob/docs/contributing.md) siempre son bienvenidos.

Créditos:
Redacción y edición: bee, degeri, elian, l1ndseymm, lukebp, matheusd, richardred.
Revisión y comentarios: Checkmate, davecgh, jazzah, jholdstock, pavel.
Imagen de portada: saender.
