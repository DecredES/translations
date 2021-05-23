# Revista Decred – Enero 2020

![abstract art](./assets/202001.png)

_Imagen: Event Horizon by @saender_

Lo más destacado de Enero:

- Se lanzó la versión 1.5.1 del software de Decred en el nodo y la cartera, incorporando algunas correcciones de errores y nuevas características.
- Politeia tuvo su mes más activo en mucho tiempo, con 6 nuevas propuestas presentadas, 5 de ellas ya terminaron su etapa de votación.
- El voto de cambio en la regla de consenso para DCP0005 está en camino de completarse y el soporte es > 99%.
- La cadena global de eventos y reuniones comunitarias se está desarrollando para conmemorar el 4to aniversario del bloque génesis de Decred  el 8 de febrero. Algunos grupos celebraron el 6 de febrero. Las bolsas de Stakey están empacadas para una gira mundial vertiginosa.

## ¡Emite tus votos!

El voto de cambio de consenso para habilitar los commits de encabezado del bloque como se define en [DCP0005](https://github.com/decred/dcps/blob/master/dcp-0005/dcp-0005.mediawiki) está [progresando](https://explorer.dcrdata.org/agenda/headercommitments) constantemente. Del 61% de los votos de Sí / No activos, el 99.94% son Sí, mientras que el 39% restante son Abstenciones.

Todavía queda alrededor de 1 semana. Si tiene alguna preferencia, [configúrela](https://docs.decred.org/governance/consensus-rule-voting/how-to-vote/) en su cartera de votación individual y / o VSP.

## Lanzamiento v1.5.1

La versión v1.5.1 corrige los errores encontrados en la anterior versión (1.5.1) y agrega algunas características.

dcrd: reducción de la memoria menor fija con clientes RPC WebSocket autenticados en conexiones intermitentes. Esto es especialmente relevante para configuraciones que involucran carteras con una gran cantidad de direcciones.

dcrwallet: error de reutilización en la dirección fija que podría activarse al reiniciar la sincronización de la red (por ejemplo, al perder el enlace a dcrd), un error en el comprador del ticket que podría enviar el cambio a una cuenta incorrecta y algunos otros errores. Las nuevas características incluyen el comando auditreuse y la capacidad de usar createrawtransaction en el modo de sincronización SPV (es decir, sin la necesidad de ejecutar dcrd).

Decrediton: se corrigió la visualización incorrecta de los tickets activos, el agotamiento de brechas durante la generación de cambios y varios problemas en la UI. Los códigos QR han sido diseñados con el logotipo Decred azul / verde en el centro.

En cuentra las notas y descargas completas en la [página de lanzamiento](https://github.com/decred/decred-binaries/releases/tag/v1.5.1). Como siempre, [verifique los binarios](https://docs.decred.org/advanced/verifying-binaries/) antes de la instalación.

## Desarrollo

[dcrd](https://github.com/decred/dcrd): Se [agregó](https://github.com/decred/dcrd/pull/2030) un script de servicio para OpenBSD rc.d además de las configuraciones [existentes](https://github.com/decred/dcrd/tree/master/release/services) Se agregó compatibilidad con sembradora HTTP a [dcrseeder](https://github.com/decred/dcrseeder/pull/25) y a [dcrd](https://github.com/decred/dcrd/pull/2017). El paquete `chainec` se [eliminó](https://github.com/decred/dcrd/pull/2039) debido a los problemas prácticos encontrados con esta API criptográfica genérica 

La generación del Nonce se [mejoró y optimizó](https://github.com/decred/dcrd/pull/2044) al especializar la implementación específicamente para el módulo secp256k1 y modificarla de tal manera que la firma ya no pueda fallar en el caso extremadamente improbable de que un nonce devuelto dé como resultado una firma no válida.

[dcrwallet](https://github.com/decred/dcrwallet): Múltiples correcciones de errores para la versión 1.5.1.

[Decrediton](https://github.com/decred/decrediton): Muchas correcciones de errores y mejoras en la interfaz de usuario para la versión 1.5.1.

El trabajo continúa para lograr un [inicio refactorizado](https://github.com/decred/decrediton/issues/2121) y utilizar una máquina de estados jerárquica.

[Politeia](https://github.com/decred/politeia): El Decred Contractor Clearance (DCC) del CMS lanzó y comenzó a procesar las emisiones de DCC. El CMS recibió un montón de correcciones y mejoras en la interfaz de usuario.

El trabajo continúa en la interfaz de usuario del CMS, [Rediseñando](https://github.com/decred/politeiagui/pull/1625) y agregando el modo oscuro a Politeia.

[dcrstakepool](https://github.com/decred/dcrstakepool): La v1.5.0 fue lanzada. Esta versión contiene todo el trabajo de desarrollo completado desde la v1.2.0 (septiembre de 2019). Desde entonces, 7 contribuyentes han producido y fusionado 37 pull request. Los cambios incluyen mejoras menores de la GUI, registro de las solicitudes HTTP mejorado, racionalización del código existente y varias correcciones de errores. Para ver la lista completa de cambios y la ruta de actualización, consulte el [Notas del lanzamiento](https://github.com/decred/dcrstakepool/blob/master/docs/release-note-1.5.0.md).

Un nuevo diseño de alto nivel fue [propuesto](https://github.com/decred/dcrstakepool/issues/574) para eliminar cuentas de VSP que también eliminan tarifas de las transacciones de los tickets del VSP, lo que hace posible que tanto los apostadores individuales como los del VSP compren tickets mixtos en el mismo conjunto de anonimato.

[dcrpool](https://github.com/decred/dcrpool): Refactorización grande [completada](https://github.com/decred/dcrpool/pull/143) para desacoplar los componentes y facilitar el aumento de la cobertura de prueba.

[dcrlnd](https://github.com/decred/dcrlnd): Corrección de errores y mejoras en la documentación.Los ejemplos del [Docker](https://github.com/decred/dcrlnd/pull/66) que automatizan la implementación de los entornos simnet con docker-compose han sido terminados. Una guía para principiantes para probar el Decred LN fue [publicado](https://medium.com/decred/beginner-guide-to-the-decred-dcr-lightning-network-917f8ad304aa) en Medium.

El trabajo continúa para [los cambios en el puerto de upstream](https://github.com/decred/dcrlnd/pull/74) hasta el recientemente lanzamiento de la versión [v0.9.0-beta](https://github.com/lightningnetwork/lnd/releases/tag/v0.9.0-beta). El conjunto de cambios del puerto incluye 503 confirmaciones que agregan 37K y eliminan 11K líneas de código.

[cspp](https://github.com/decred/cspp): Corrección de errores y mantenimiento de código. Se [eliminó](https://github.com/decred/cspp/pull/38) una copia del paquete chacha20 interno de Go a favor de la API pública recientemente lanzada.

[dcrdex](https://github.com/decred/dcrdex): Más bloques de construcción completados. Destacados: cliente de la [cartera](https://github.com/decred/dcrdex/pull/92) para el DCR Exchange, cliente para la [base de datos](https://github.com/decred/dcrdex/pull/99) basada en bbolt, cliente para el [servidor web](https://github.com/decred/dcrdex/pull/103) para habilitar el acceso del cliente a través del navegador, cliente para la aplicación [inicial principal](https://github.com/decred/dcrdex/pull/120), [esqueleto](https://github.com/decred/dcrdex/pull/100) del cliente de la aplicación, cliente para el registro de una [cuenta en el DEX](https://github.com/decred/dcrdex/pull/140) a través de la interfaz web, configuración de la aplicación del servidor y [sistema](https://github.com/decred/dcrdex/pull/81) de controladores de activos, implementación del [Mersenne Twister PRNG](https://github.com/decred/dcrdex/pull/137) de 64 bits.

Fue otro mes de desarrollo ocupado: un total de 27 pull request se fusionaron agregando 22K y 4K eliminando líneas.

[dcrandroid](https://github.com/decred/dcrandroid): El diseño en la página para restaurar la cartera fué [mejorado](https://github.com/decred/dcrandroid/pull/422).

La biblioteca móvil de dcrlibwallet compartida entre las aplicaciones de Android e iOS recibió un montón de correcciones de errores y se [actualizó](https://github.com/raedahgroup/dcrlibwallet/pull/93) a la versión v1.5.0 de dcrd y dcrwallet.

[dcrios](https://github.com/raedahgroup/dcrios): Mejoras de la interfaz de usuario y optimizaciones de rendimiento. [Mejoras](https://github.com/raedahgroup/dcrios/pull/566) de sincronización y limpieza de la interfaz de usuario en la página de descripción general, [optimizaciones](https://github.com/raedahgroup/dcrios/pull/572) en multi-wallet, [migración](https://github.com/raedahgroup/dcrios/pull/558) preliminar a la función de multi-wallet de dcrlibwallet, cambio al [almacenamiento de configuración](https://github.com/raedahgroup/dcrios/pull/576) de dcrlibwallet. Se implementó una nueva interfaz de usuario para la configuración de [password/PIN](https://github.com/raedahgroup/dcrios/pull/551), las caracteristicas de [copia de seguridad de las semillas](https://github.com/raedahgroup/dcrios/pull/530) y de [restaura desde la semilla](https://github.com/raedahgroup/dcrios/pull/527) fueron agregadas.

[dcrdata](https://github.com/decred/dcrdata): Pequeñas correcciones y mejoras en la interfaz de usuario.

[tinydecred](https://github.com/decred/tinydecred): El cliente RPC se [agregó](https://github.com/decred/tinydecred/issues/45) en la mayoría de los comandos implementados por ahora. Se agregó un botón para [revocar](https://github.com/decred/tinydecred/pull/30) tickets perdidos y vencidos. La base de datos fué [rediseñada](https://github.com/decred/tinydecred/pull/42) para soportar codificación personalizada, inserción batch, namespaces, y más. [Prueba de Cobertura](https://github.com/decred/tinydecred/pull/47) mejorada hasta en un ~ 73%. Se reestructuró el proyecto para que sea [empaquetable](https://github.com/decred/tinydecred/pull/59).

[docs](https://github.com/decred/dcrdocs): Los comandos y argumentos del [dcrlnd](https://docs.decred.org/wallets/lightning/) para el CLI han sido [documentados](https://github.com/decred/dcrdocs/pull/1055). Fueron [añadidas](https://github.com/decred/dcrdocs/pull/1062) intrucciones para configurar el [Trezor](https://docs.decred.org/wallets/decrediton/trezor/) en Decrediton. La [Reading list](https://docs.decred.org/getting-started/reading-list/) fué [añadida](https://github.com/decred/dcrdocs/pull/1043) a la sección de Getting Started y contiene una selección de artículos, podcasts, videos y otros materiales (basado en el repositorio de recursos educativos de Ditto). La página del [BLAKE-256](https://docs.decred.org/research/blake-256-hash-function/) se ha [ampliado](https://github.com/decred/dcrdocs/pull/1034) significativamente para explicar por qué se eligió esta función. Se [agregaron](https://github.com/decred/dcrdocs/pull/1057) dos nuevas definiciones al [Glosario](https://docs.decred.org/glossary/) (Tipo de moneda y Cartera HD).

[decred.org](https://github.com/decred/dcrweb): Se actualizó y se limpió la página de [contribuyentes](https://github.com/decred/dcrweb/pull/774).

Estadísticas de actividad de desarrollo para el mes de enero: 246 PR activos, 210 confirmaciones al master, 58,000 líneas agregadas y 25,000 líneas eliminadas distribuidas en 17 repositorios. Las contribuciones vinieron de 3 a 6 desarrolladores por repositorio.

## Comunidad

Bienvenido a los nuevos contribuyentes: @termoose ([dcrlnd](https://github.com/decred/dcrlnd/commits?author=termoose)) and @pablito ([dcrweb](https://github.com/decred/dcrweb/commits?author=pLabarta)).

Congratulations to first contractors granted the Decred Contractor Clearance via the new CMS process: [@bgptr](https://github.com/bgptr) (development), [@teknico](https://github.com/teknico) (development) and [@decreddragon](https://twitter.com/DecredDragon) (marketing).

Las siguientes personas fueron eliminadas de la lista [lista de contribuyentes activos](https://decred.org/contributors/): Leslie Ankney, Elizabeth Bagot, Margaret Huang, Milvian Prieto, Denys Zayets, Tim Hebel, Phillip Conrad, Justin Santoro, Bill Xing. ¡Gracias por todo el buen trabajo y no duden en pasar por aquí!

La página de [contribuyentes](https://decred.org/contributors/) se actualiza regularmente para enumerar las personas que actualmente están creando Decred. La consecuencia de esto es que cuando se eliminan los contribuyentes inactivos, no queda ningún registro en el sitio web de que hayan trabajado para el proyecto. Para abordar esto, se ha propuesto crear una lista de [contribuyentes pasados](https://github.com/decred/dcrweb/issues/744) y/o [salón de la fama.](https://github.com/decredcommunity/issues/issues/52).

Estadísticas de la comunidad:

- Seguidores en Twitter: 40,860 (-37)
- Suscriptores de Reddit: 9,723 (+15)
- Usuarios de matrix: 533 (+29)
- Usuarios slack: 6.880 (-1)
- Usuarios de Discord: 2,670 (+42), verificado para publicar: 433 (+26)
- Usuarios de Telegram: 2,728 (-110)
- Suscriptores de YouTube: 3.950 (-10)
- Seguidores en Facebook: 3,563 (+11), Me gusta: 3,234 (+11)
- Seguidores de LinkedIn: 689 (+15)
- GitHub dcrd stars: 533 (+5), forks: 1,476 (+18)

Los gráficos históricos de las estadísticas de Twitter, YouTube, Reddit y GitHub ahora están disponibles en [dcrextdata](http://dcrextdata.planetdecred.org/community).

## Gobernanza

En enero, la [tesorería](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx) recibió 14,121 DCR y gastó 15, 560 DCR. Usando la tasa promedio diaria de DCR / USD de enero de $ 18.00, esto es $ 254K recibido y $ 280K gastado. A la tasa promedio diaria de diciembre de $ 18.32, la cifra en USD facturada por el trabajo completado en ese mes es de $ 285K. A partir del 1 de febrero, el saldo de la tesorería es de 642,082 DCR (12.2 millones de dólares a $ 18.96).

Hubo 6 propuestas presentadas en enero, 5 ya han sido votadas y 1 todavía está en discusión.

- La propuesta de Relaciones Públicas de [Monde](https://proposals.decred.org/proposals/bdd02d82547bd78fc95939c1e2b3df21ebec6e8d31444df5bea3c133b0199f05) fue aprobada con un 72% de aprobación y una participación del 25%.
- La propuesta de [Ditto](https://proposals.decred.org/proposals/012b4e335f25704e28ef196d650316dca421f730225d39e37b31b3c646eb8497) PR fue rechazada con un 17% de aprobación y una participación del 35%.
- La [fase 3](https://proposals.decred.org/proposals/e3675649075a2f92269d8cdc2e1dfd71b16796477df31de7d2868cccfcffb13f) del programa de Decred Open Source Research fue aprobada con un 82% de aprobación y una participación del 29%.
- Se aprobó una [propuesta](https://proposals.decred.org/proposals/063e38270b475ad680e98c12d1a48e322f4e8defe40b265272ea60c6d2202b13) de @dezryth para administrar la cuenta de Facebook del proyecto y representar a Decred en los eventos con un 76% de votos afirmativos y una participación del 21%.
- Se rechazó una propuesta de [stickers](https://proposals.decred.org/proposals/4acb95564d36488a7ee64683a84dd7954982b2f4743e2f7a15477231f863442f) con un 5% de votos a favor y una participación del 21%.
- Se está discutiendo una [propuesta](https://proposals.decred.org/proposals/95cfb73254a032b2c199c37bb499d6f172d044b1f38016279c5bbca6572251f0) de @Exitus para producir contenido de video para Decred.

[El número 26](https://blockcommons.red/politeia-digest/issue026/) del Politeia Digest tiene más detalles sobre todas las propuestas y la auditoría del Market Maker. Se han desarrollado herramientas de auditoría que procesan el historial de apertura / cierre de pedidos de i2 para calcular el tiempo de actividad en porcentaje. Si el tiempo de actividad es inferior al 90% citado en la propuesta de i2, sus tarifas para el mes se reducirán proporcionalmente.

En enero, CoinDesk publicó un [artículo](https://www.coindesk.com/is-bitcoin-in-2020-really-like-the-early-internet) ue hacía referencia a las cifras de gasto en la Tesorería de Decred. Se calcularon algunas cifras adicionales para el artículo en ese momento (finales de noviembre de 2019). La tesorería había pagado el equivalente a $6.55 millones, con un 54.7% pagado a los desarrolladores. Desde que Politeia se lanzó en octubre de 2018, más del 10% del gasto de la Tesoreria se ha destinado a proyectos propuestos y aprobados a través de Politeia. Por región geográfica, el 30% de los desarrolladores de Decred se encuentran en América Central / del Sur, el 25% en los EE. UU., El 20% en Europa, el 15% en África y el 10% en Asia.

## Red

Hashrate: el hashrate de enero abrió a ~ 396 Ph/s y cerró en ~ 435 Ph/s, tocó fondo a 315 Ph/s y alcanzó un máximo de 528 Ph/s durante todo el mes. Distribución de hashrate del pool al 1 de febrero: Poolin 26%, UUPool 18%, lab.antpool.com 10%, F2Pool 2%, Luxor 1.78%, BTC.com 1.46%, BeePool 0.08%, CoinMine 0.07%, suprnova 0.01%, y otros ~ 40% por [dcrstats.com](https://dcrstats.com/pow). Los números de distribución del pool son aproximados y no se pueden determinar con precisión.

Staking: el precio promedio del boleto de 30 días fue 138.3 DCR (+0.8) por dcrstats.com. El precio varió entre 128.1–150.4 DCR. El monto bloqueado fue de 5.55–5.71 millones de DCR, que correspondió al 50.83–51.96% del suministro disponible.

Nodos: a lo largo de [enero](https://charts.dcr.farm/d/000000014/nodes?orgId=1&from=1577836800000&to=1580515200000) hubo un promedio de 137 nodos de públicos y 323 nodos normales por dcr.farm. Distribución promedio de versiones para enero: 50.8% usa dcrd v1.4, 21.1% usa dcrd v1.5, 9.0% usa dcrd v1.5 dev y RC builds, 3.1% usa dcrd v1.6 dev builds, 2.2% usa dcrd v1. 5.1, 5.6% usa dcrwallet v1.4, 3.4% usa dcrwallet v1.5, 0.6% usa dcrwallet v1.5.1.

[dcrextdata](http://dcrextdata.planetdecred.org/) obtuvo un diseño actualizado y habilitó el mempool y los cuadros de propagación de bloques. Algunos de ellos son un poco lentos pero ya muestran información interesante. Los comentarios son bienvenidos en el [rastreador de problemas](https://github.com/raedahgroup/dcrextdata) o en la sala de [#planetdecred](https://matrix.to/#/!gruHpujXftcsHcghjx:planetdecred.org).

Los datos de un nodo que se ha estado ejecutando desde el bloque 0 [muestran](https://matrix.to/#/!vGasNHFXqjoEWUBTIi:decred.org/$15792934191332SWDSY:decred.org) que la cadena en la red principal de Decred ha tenido 2517 reagrupaciones de profundidad 1,25 reorganizaciones de profundidad 2,3 reorganizaciones de profundidad 3 y 0 reorganizaciones de profundidad mayores que 3.

[El mapa de Decred mainnet LN](https://ln-map.jamieholdstock.com/) muestra 14 nodos y 31 canales con una capacidad total de 6 DCR, a partir del 6 de febrero.

## Integraciones

Noticias del VSP:

- Nuevo VSP lanzado por el proveedor de participación como servicio YieldWallet, disponible en [decred.yieldwallet.io](https://decred.yieldwallet.io/). La tarifa de servicio es del 2%.
- El VSP [decredvoting.com](https://decredvoting.com/) [anunció](https://www.reddit.com/r/decred/comments/euqd4h/introducing_split_ticket_dashboard_on/) un nuevo panel de tickets divididos que "brinda a los usuarios de tickets divididos una vista resumida y completa de todos sus tickets junto con datos analíticos personalizados".
- Los siguientes VSP se eliminaron de la [lista](https://decred.org/vsp/) por su bajo rendimiento: [d1pool.com](https://github.com/decred/dcrwebapi/pull/63), [dcr.grassfed.network](https://github.com/decred/dcrwebapi/pull/70) y [dcr.pos.fans](https://github.com/decred/dcrwebapi/pull/79).

Resulta que el VSP [dcr.farm](https://dcr.farm/) ejecuta una serie de servicios útiles sin la debida publicidad:

- [seed.dcr.farm](https://seed.dcr.farm/) es un nodo semilla dcrd con un ancho de banda dedicado, ubicado en Francia.
- [explorer.dcr.farm](https://explorer.dcr.farm/) es un explorador alternativo para Decred blockchain.
- [Panel de estado](https://status.dcr.farm/) sofisticado para todos los servicios, incluidas las 6 carteras de votación.
- DJ lo usa activamente, pero mencionando que está completo: [charts.dcr.farm](https://charts.dcr.farm/) tiene [~16 paneles](https://charts.dcr.farm/dashboards) con algunos gráficos únicos como [Nodos](https://charts.dcr.farm/d/000000014/nodes) (versiones de nodo a lo largo del tiempo), [VSPs](https://charts.dcr.farm/d/000000016/proof-of-stake-pools) (estadísticas de VSP a lo largo del tiempo) y [tarifas de transacción](https://charts.dcr.farm/d/000000013/transaction-fees) (tarifas irregulares altas y bajas) .

Exchanges:

- Vimos algunos informes de que las carteras de [Bittrex](https://twitter.com/Cjfan23/status/1218727480854446081) y [Binance](https://www.reddit.com/r/decred/comments/ew1vyc/binance_dcr_withdrawls_disabled/) estaban en modo de mantenimiento por un tiempo. Al momento de escribir ambos están funcionando.

Advertencia: la redacción de la Revista Decred no puede asegurar los servicios prestados por terceros. Recuerda siempre hacer tu propia investigación antes de confiar.

## Alcance

El 8 de febrero, Decred cumplió cuatro años y la comunidad celebró el evento con el hashtag [#DecredGlobalMeetup](https://twitter.com/hashtag/DecredGlobalMeetup). Los eventos tuvieron lugar en al menos una [docena de ciudades](https://twitter.com/decredproject/status/1225440495108841475) de todo el mundo para celebrar la comunidad y la tecnología que Decred ha construido.

En enero, las nuevas subpáginas del sitio web se completaron y se enviaron para su traducción, y se espera que todos los idiomas se publiquen de inmediato en febrero. Esto ofrece una actualización visual del sitio y se alinea con el [mensaje](https://github.com/decredcommunity/pr/blob/release/foundational-messaging.md) actual del proyecto. El sitio web se ha simplificado, y todas las actualizaciones futuras se podrán lograr en no más de tres meses, de principio a fin.

Se han presentado varias propuestas de marketing y relaciones públicas, y hay más en camino, así como un informe que detalla un resumen de los esfuerzos y gastos de 2019, y un llamado a la acción para 2020 para descentralizar, romper la burbuja, educar y aprovechar el potencial individual.

El podcast Decred in Depth lanzó dos episodios: @matheusd en Decred's Lightning Network y @permabullnino en "Block Subsidies + Ticket Pool VWAP + HODLer Conversion Rates". No olvides suscribirte y calificar el podcast.

## Eventos

Asistidos:

- 7 de enero- [Digital Money Forum](https://thedigitalmoneyforum.com/) - Las Vegas, USA. @akinsawyerr abogó por redes descentralizadas y soberanía individual en el panel [The Libra Effect](https://thedigitalmoneyforum.com/Sessions/the-problem-with-old-money-a-great-debate/) panel, que apareció en [CoinDesk](https://www.coindesk.com/libra-association-exec-world-needs-us-because-bitcoin-is-not-a-means-of-payment), y también habló con varios periodistas. ([reporte](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$157859800075195pLJde:decred.org), [fotos](https://twitter.com/AkinSawyerr/status/1214614201517232128))
- 14 de enero - [Cryptopia Documentary Premiere](https://www.meetup.com/en-AU/BC-Aus/events/267242503/) - Melbourne, Australia.Australia. Decred fue invitado a ser patrocinador del evento y socio de lanzamiento de Cryptopia Film, un documental sobre los temas clave dentro de la criptomoneda, que incluye regulación, privacidad, servicios financieros, gobernanza, marketing y desarrollo. Todo el teatro se reservó con más de 140 invitados de la comunidad de criptografía y blockchain. @eSizeDave y @zohand hablaron de Decred en un panel de discusión y fueron citados en el comunicado de [prensa oficial](https://prwire.com.au/r/87706). ([reporte](https://github.com/decredcommunity/events/blob/master/reports/20200114-cryptopiafilm-world-premiere-melbourne-australia.md))
- 14 de enero - [GoCracow #7](https://www.meetup.com/en-AU/GoCracow/events/265765051/) - Kraków, Polonia. @kozel presentó a~ 30 Go devs a las criptomonedas y Decred. La audiencia estuvo atenta en general, pero los participantes más activos fueron los que se describieron como familiares o entusiastas de la criptografía. ([reporte](https://github.com/decredcommunity/events/blob/master/reports/20200114-gocracow7-meetup-krakow-poland.md))
- 24 de enero - Blockchain Technology and Use Cases - Casablanca, Morocco. @arij fue invitada a hablar en el evento coorganizado por el Ministerio de la Juventud de Marruecos con el tema "El papel de las nuevas tecnologías en la promoción del desarrollo positivo de los jóvenes". @arij habló sobre blockchains, presentó a Politeia y LN a la audiencia de alrededor de 50 personas de diferentes orígenes, en su mayoría jóvenes. ([fotos](https://twitter.com/DecredArabia/status/1220819101586685952))
- 29-31 de enero - [Crypto 101 Online Summit](https://www.crypto2020summit.com/) - Internet. @lukebp describió los planes de Decred para 2020, la presentación se cargará en YouTube cuando esté lista.

Próximos eventos:

- Feb 8 - [Blockchain and AI](https://www.eventbrite.com/e/blockchain-and-ai-best-tools-for-the-development-of-nations-tickets-91389994935) - Casablanca, Morocco. @arij hablará sobre los logros de Decred durante sus 4 años. Una pequeña fiesta al final marcará el aniversario de Decred.
- 8 de febrero - [Decred Crypto Hangouts](https://www.eventbrite.com/e/decred-crypto-hangout-learn-about-career-opportunities-in-the-industry-tickets-91830803405) - Ikeja, Lagos. Huobi, Yellowcard y Telos4Africa estarán presentes.
- 8 de febrero - [Decred Global Meetup](https://www.meetup.com/pt-BR/DecredBrasil/events/268496816/) - Salvador, Brasil.
- 12-13 de febrero - [Blockchain Summit Latam](https://www.blockchainsummit.la) - Panama City, Panama. Decred será un patrocinador de plata.
- 18 de marzo - [Campus Party Amazonia](https://brasil.campus-party.org/campus-party-amazonia-2020/) - Manaus, Brasil. Decred tendrá 2 charlas y varias otras actividades.
- 20 de marzo - [BlockchainUA](https://blockchainua.com/en/) - Kyiv, Ucrania. Los oradores quieren representar a Decred en el evento más grande de Europa del Este. Póngase en contacto con @cryptotexty en la sala de [#events](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org) para obtener más información.
- 20-21 de marzo - [CIBTC Blockchain Summit](http://cibtc.es/) - Motril, España. Decred será patrocinador de oro. El evento es parte de una gran gira de Decred en español en España donde @elian organizará reuniones y un taller con comunidades locales en Madrid, Barcelona, Bilbao, Valencia, Vigo y Motril.
- 30-31 de marzo - [Bitconf](https://www.bitconf.com.br/portal/) - São Paulo, Brasil. Decred tendrá múltiples charlas sobre diversos temas.

## Media

[Decred Drive](https://medium.com/@decreddrive), un nuevo boletín semanal, fue [lanzado](https://twitter.com/DecredDragon/status/1215309738293985280) por @decreddragon el 9 de enero y publicó 5 números hasta el momento.

Decred apareció en el nuevo boletín semanal Our Network, números [#2](https://ournetwork.substack.com/p/our-network-issue-2) y [#6](https://ournetwork.substack.com/p/our-network-issue-6), con @Checkmate proporcionando gráficos e información sobre los datos en cadena de Decred y @richardred proporcionando un gráfico sobre Politeia. Cada semana, el boletín incluye 5 gráficos y comentarios para varios proyectos diferentes de blockchain.

Checkmate hizo el caso del oso para Ethereum como parte de un "[ruido criptográfico](https://bankless.substack.com/p/why-eth-wont-sustain-a-monetary-premium)" previsto en el boletín de Bankless. Vitalik Buterin [respondió](https://www.reddit.com/r/ethereum/comments/ewb9as/why_eth_wont_sustain_a_monetary_premium/fg2x4oz/) a algunos comentarios sobre la redacción en Reddit, y ahora hay 3 [respuestas](https://bankless.substack.com/p/why-eth-will-sustain-a-monetary-premium) en el subgrupo Bankless de destacados miembros de la comunidad Ethereum.

Decrypt ha [cubierto](https://decrypt.co/17371/we-found-the-no-coiner-troll-guarding-wikipedia) parte de la [experiencia](https://github.com/decredcommunity/issues/issues/79) de Decred con Wikipedia, que desencadenó en un [intercambio](https://twitter.com/decryptmedia/status/1220069033405485057) inteligente de Twitter con uno de los expertos en criptografía de WP.

Artículos seleccionados:

- Building a Transparent Future with the Decred Blockchain por @ammarooni ([medium](https://medium.com/decred/building-a-transparent-future-with-the-decred-blockchain-e77471d28059))
- Decred On-Chain: HODLer Conversion Rates por @permabullnino ([medium](https://medium.com/@permabullnino/decred-on-chain-hodler-conversion-rates-87e16a4c78cd))
- 2019 Review: Distributed Governance ([Smith and Crown](https://sci.smithandcrown.com/research/2019-governance-review)) - esta descripción completa del gobierno de blockchain en 2019 presenta muchas observaciones precisas sobre Decred, con una nota especial sobre las tasas de participación de Politeia.
- The Future of Digital Currencies in Africa? Meet Decred the Autonomous Digital Currency ([appsafrica.com](https://www.appsafrica.com/the-future-of-digital-currencies-in-africa-meet-decred-the-autonomous-digital-currency/))
- Is Bitcoin Really Like the Early Internet? por Leigh Cuen ([coindesk.com](https://www.coindesk.com/is-bitcoin-in-2020-really-like-the-early-internet)) - esta pieza de reflexión sobre las similitudes entre Bitcoin y los principios del internet, presenta entrevistas con @ moo31337 y Zooko Wilcox de Zcash. El artículo también tiene algunas cifras relacionadas con el gasto del Tesoro de Decred, como se señaló en la sección de Gobierno.

> ¡Estamos igualmente emocionados de ver el compromiso provocado por el [artículo](https://www.coindesk.com/is-bitcoin-in-2020-really-like-the-early-internet) de CoinDesk el fin de semana pasado! Ciertamente fue interesante ver varios proyectos discutiendo quién terminó siendo mencionado en el artículo, con solo Decred y un puñado de otros haciendo el corte. Este tipo de cobertura es el resultado de meses de comunicación con los periodistas: educación, respuestas oportunas, entrevistas, suministro de información y estadísticas, etc. Historias como esta no suceden de la noche a la mañana o por sí mismas, y el viejo adagio "fuera de la vista", fuera de la mente "se aplica a los medios de comunicación.([@liz_bagot](https://proposals.decred.org/proposals/012b4e335f25704e28ef196d650316dca421f730225d39e37b31b3c646eb8497/comments/71))

Traducciones:

- Beginner guide to the Decred Lightning Network - [en Árabe](https://insaf01.github.io/decred-arabic/articles/beginner-guide-to-the-decred-lightning-network.html) by @arij, [en Español](https://medium.com/decred-es/gu%C3%ADa-para-probar-el-lightning-network-de-decred-dcr-344cad6be20e) by @francov\_.
- Decred Journal diciembre de 2019 traducido al árabe (@arij), chino (@Dominic) y español (@francov_). ¡Gracias por su duro trabajo!

Videos:

- Is a Public Relations Firm in Crypto Worth It? Decred Stakeholders Vote and Decide Using Politeia por @Exitus ([youtube](https://www.youtube.com/watch?v=uzhc2CKI2wk))
- Decred's Akin Sawyerr Says Blockchain Is Part of Africa's Political Future ([coindesk.com](https://www.coindesk.com/decreds-akin-sawyerr-says-blockchain-is-part-of-africas-political-future), [youtube](https://www.youtube.com/watch?v=8w7uCSVuuVw))
- The Libra Effect at CES2020: Highlights of @akinsawyerr por @Exitus ([youtube](https://www.youtube.com/watch?v=5Zi5wYZhEDE)) - the full panel can be found [here](https://www.youtube.com/watch?v=prz6ILpLNLE) (@akinsawyerr starts around [17 min](https://www.youtube.com/watch?v=prz6ILpLNLE&t=17m00s))

Audio:

- @akinsawyerr appeared on Tom Shaugnessy's Chain Reaction podcast to talk about Governance Reimagined. ([podbean](https://fiftyonepercent.podbean.com/e/decred/))
- Crypto 101 Ep. 302 - Governing the Masses w/ Decred, por @lukebp. ([podbean](https://www.podbean.com/media/share/dir-j5baa-7c90e87), [soundcloud](https://soundcloud.com/crypto101podcast/ep-302-governing-the-masses-w-decred))
- Decred in Depth Ep. 16 - @permabullnino discute el proceso de propuesta de Politeia y su trabajo en curso analizando los movimientos de los tickets en la cadena Decred, presentando conceptos como las tasas de conversión de TVWAP y Hodler. ([libsyn](https://decredindepth.libsyn.com/permabull-nino-block-subsidies-ticket-pool-vwap-hodler-conversion-rates), [soundcloud](https://soundcloud.com/decredindepth/ep-16-permabull-nino-block-subsidies-ticket-pool-vwap-hodler-conversion-rates))
- Decred in Depth Ep. 17 - @ammarooni habla sobre la rica historia de criptografía de Toronto, los tokenomics de DCR, BTC y ETH, y considera a Decred como un proveedor de infraestructura, activo productivo y avance económico. ([libsyn](http://decredindepth.libsyn.com/ammar-nasier-decred-an-economic-breakthrough))

@AGNFAB1 publicó dos nuevas obras de arte: [Politeia pirate](https://www.reddit.com/r/decred/comments/end3lc/d_e_c_r_e_d/) (título no oficial), [DCR is Water BTC is Fire](https://twitter.com/AGNFAB1/status/1220091425737580544).

## Discusiones de la comunidad

Sistemas:

¡Slack está bajando, el puente está siendo quemado, huye a [Matrix](https://decred.org/matrix/) mientras puedas!

Reddit:

- [Actualización](https://www.reddit.com/r/decred/comments/eo3tje/decred_dex_progress_the_client_and_server_are/) sobre el dcrdex, comercio atómico de testnet próximo.
- [Cómo](https://www.reddit.com/r/decred/comments/ervlvw/how_to_runstartmove_decrd_to_the_background_i_can/) mover dcrd a segundo plano: una pregunta común para los nuevos usuarios de CLI.
- ¿Decred está [muerto](https://www.reddit.com/r/decred/comments/ekhi2l/is_decred_dead_hash_rate_has_stagnated_and/)? Nope.
- Discusión interesante sobre la [publicación](https://www.reddit.com/r/ethereum/comments/ewb9as/why_eth_wont_sustain_a_monetary_premium/fg1q9q7/) del caso de osos Ethereum de @Checkmate en / r / ethereum, incluida alguna discusión con Vitalik Buterin.

Twitter:

- Stakey les recuerda a todos que controlen sus [llaves](https://twitter.com/DCRComic/status/1212754642481881088).
- Primero en el mercado vs adaptable, un [ejemplo](https://twitter.com/BarnardTheBear/status/1213893268351672320) histórico.
- Por qué Decred es [Aburrido](https://twitter.com/marco_peereboom/status/1218178834786324480).
- ¿Con qué frecuencia su CEO / [líder del proyecto](https://twitter.com/marco_peereboom/status/1212849047456927744) le dice que lo elimine del proyecto?
- @DCRComic: cómic [Atomic Swaps](https://twitter.com/DCRComic/status/1222874521507717121), una [versión](https://twitter.com/DCRComic/status/1220367582479425537) de la historia de financiamiento para el desarrollo de BCH, un hilo sobre [dcrdata](https://twitter.com/DCRComic/status/1218189767759859713).
- Una [actualización](https://twitter.com/chappjc/status/1222004371199864834) en dcrdex de @chappjc, "esta primavera".
- @richardred [abrió](https://twitter.com/RichardRed0x/status/1219381114768429057) las puertas de la bahía de pod para votar por el programa de investigación de código abierto.
- @lukebp [tuitea](https://twitter.com/lukebp_/status/1217871970420711424) sobre los beneficios de poder modificar las reglas de consenso para mejorar la seguridad de la red y la experiencia de usuario.
- Las propuestas de relaciones públicas de Ditto y Monde llamaron la atención de los periodistas en el espacio, incluido The blocks of [Frank Chaparro](https://twitter.com/fintechfrank/status/1215704016564428802).
- @Dustorf en el [colectivo](https://twitter.com/lefebvre_dustin/status/1220397690602901504) digital de contratistas Decred.
- @degeri señala que los sitios web de la mayoría de los principales proyectos de blockchain están [suministrando](https://twitter.com/degeri_crypto/status/1217372695483965441) información a Google.
- Concurso [#DrawStakey](https://twitter.com/DCRComic/status/1220732376088809477).

## Mercado

En enero, DCR cotizaba entre los USD 16.24–22.44 / BTC 0.00195–0.00257. La tarifa diaria promedio fue de $18.00.

El movimiento de precios de Bitcoin desde ~ 6500 hasta el rango de ~ 9000 estimuló el aumento de precios de varias [altcoins](https://cointelegraph.com/news/dash-price-up-70-bsv-gains-200-is-a-price-correction-imminent) incluidas Dash, Zcash y varios forks de Bitcoin.

## Noticias externas relevantes

Bitcoin celebró su 11° aniversario. Desde el 3 de enero de 2009, la red Bitcoin ha operado con [99.9848% de tiempo de actividad](http://bitcoinuptime.com/).

El informe de minería de diciembre de CoinShares señala un aumento del 80% del hashrate de Bitcoin desde junio de 2019, de ~ 50 a ~ 90 Eh / s (Exahashes por segundo). Se especula que el 70% de los ~ 40 Eh / s adicionales provienen de China, mientras que la participación de China en el hashrate total se estima en un 65%. Los precios de "equilibrio" y "capitulación minera" se estiman en ~ $ 6,100 y ~ $ 3,900, respectivamente. Consulte los [puntos destacados](https://medium.com/coinshares/bitcoins-hash-rate-grew-more-than-80-since-june-mostly-within-china-7444b20b2c89) y el informe completo vinculado para obtener más números interesantes.

El [estado de la red Año 2019](https://coinmetrics.substack.com/p/state-of-the-network-2019-year-in) en revisión por Coin Metrics comparó el rendimiento de los 18 criptoactivos más grandes (incluido DCR) en un conjunto de métricas de mercado y cadena.

Monero anunció [RPC-Pay](https://www.monerooutreach.org/stories/RPC-Pay.html), Un nuevo esquema para microtransacciones instantáneas y privadas donde los clientes pagan con hash de minería por usar un servidor compatible, como un nodo Monero. "El servidor utiliza los hashes recibidos como pago para obtener ingresos, y gracias a RandomX de Monero, los hashes de minería se pueden calcular de manera eficiente utilizando las CPU más populares. Pagar con solo hashes en lugar de Monero significa que RPC-Pay no carga la red de Monero ni deja un registro. Con RPC-Pay, los hashes mineros se convierten en una nueva unidad de pago sigilosa más pequeña en el universo Monero ". El proyecto Primo es la primera aplicación externa del concepto para implementar la entrega de contenido de sitios web pagos.

[Nakamoto](https://nakamoto.com/), una nueva criptomoneda con mucho por que hablar, lanzada en el 11 ° aniversario del bloque de génesis de Bitcoin con una selección de artículos de destacadas personalidades de blockchain. La revista se describe a sí misma (y a sus colaboradores) como "pro-Bitcoin", pero esto causó bastante [controversia](https://cryptoslate.com/nakamowho-blog-by-pro-bitcoin-technologists-bashed-by-btc-maximalists/) con algunos maximalistas de Bitcoin que hicieron excepciones a los artículos que trataban sobre proyectos de criptomonedas distintos de Bitcoin. Muchas personas que figuran como contribuyentes aún no [publicaban](https://modernconsensus.com/cryptocurrencies/bitcoin/bitcoin-journal-nakamotos-rocky-start/) artículos en la revista, pero enumerar nombres como Roger Ver y Brendan Blumer (CEO de Block.one) parece haber sido suficiente para tener otros colaboradores como Tuur Demeester [quiten](https://twitter.com/TuurDemeester/status/1213939900476743680) sus nombres.

DigixDAO se liquidará después de una [votación](https://www.coindesk.com/digixdao-votes-to-liquidate-64m-treasury) en la que 58 partes interesadas votaron [abrumadoramente](https://community.digix.global/#/proposals/0xe7d5d8aefc5f73c4c8bbc716f0c3c2dd52d5282d18217db331da4435b8e6966e) (97%) para liquidar su fondo de financiación y reclamar su ETH. DigixDAO se formó para admitir un ecosistema alrededor del token de oro Digix (DGX) y promoverlo. Digix [realizó](https://www.coindesk.com/digixdao-votes-to-liquidate-64m-treasury) una ICO en 2016 y recaudó 466,648 ETH, con un valor de $7 millones en ese momento, y actualmente posee 380,000 ETH (con un valor de $71 millones a precios de enero de 2019). Después de que la plataforma DAO se lanzó en marzo de 2019 para administrar el fondo, los fundadores comenzaron a escuchar la insatisfacción de los miembros de  la DAO y las solicitudes de disolución. Introdujeron el [Proyecto Ragnarok](https://community.digix.global/#/proposals/0xe7d5d8aefc5f73c4c8bbc716f0c3c2dd52d5282d18217db331da4435b8e6966e) como una opción para disolver el DAO y permitir a los miembros reclamar su ETH, y los miembros tomaron esa opción. Del suministro circulante del token DAO (DGD) de 2 millones, se apostó 1 millón para participar en el gobierno de DAO. La inspección informal de las propuestas en el [sitio](https://community.digix.global/#/) de la comunidad DigixDAO sugiere que la participación en los votos de las propuestas fue regularmente inferior al 10% de la DGD representada, con alrededor de 20-30 votantes en la mayoría de las propuestas. La propuesta de liquidación tuvo una participación mucho mayor, con el 66% de los votos circulantes de DGD para cerrar todo. Este [artículo](https://blog.coinfund.io/digixdao-divorce-story-6ed74b00e2bd) tiene más detalles, incluido el papel fundamental desempeñado por 4 ballenas DGD que se cree que fueron los fundadores del proyecto.

Otro proyecto de ICO para reducir y devolver fondos no gastados este mes fue [TruStory](https://medium.com/trustory-app/why-trustory-is-shutting-down-6d50175628eb).

Decentraland está volviendo a usar su plataforma de gobernanza Agora con [dos](https://decentraland.org/blog/announcements/back-to-the-polls-two-new-agora-votes/) votos más para determinar los parámetros del ecosistema. Los titulares de MANA votaron sobre cuál debería ser la [tarifa](https://agora.decentraland.org/polls/1d955723-5158-4403-b026-32e974e2fae9) del mercado (las tarifas se cobran en MANA y se queman), con una votación del 90% para aumentar la tarifa del 1% al 2.5% (las otras opciones eran para aumentos mayores). Los titulares de MANA también votaron sobre cuánto peso otorgar a [LAND](https://agora.decentraland.org/polls/0387cebc-31a3-4e12-a7b4-e9926dd5b392) la propiedad de la gobernanza, habiendo [votado](https://agora.decentraland.org/polls/8c4fdc25-1876-4ca5-a2ac-809c13ab840c) previamente para indicar que los propietarios de LAND también deberían poder votar, en esta encuesta los titulares de MANA votaron para otorgar a cada LAND el poder de voto equivalente a 2K MANA (la opción más baja disponible). La participación en estas encuestas de gobernanza fue de alrededor del 3.5-4% del suministro circulante de MANA y alrededor de 50 direcciones individuales.

La saga de financiación para el desarrollo de Zcash parece estar finalmente [terminada](https://electriccoin.co/blog/dev-fund-poll-shows-consensus/), para esta época. Sin embargo, no antes de tener que resolver algunos desacuerdos finales. El primero de ellos fue sobre si los fondos de ECC deberían estar limitados en términos de USD (lo que limita la exposición de ECC al alza de ZEC). El ECC realizó una [publicación](https://electriccoin.co/blog/dev-funds-should-be-in-zcash-not-united-states-dollars/) sobre la importancia de los paquetes de incentivos denominados en ZEC para atraer y retener a los trabajadores talentosos, con un cronograma de adjudicación de 4 años para fomentar un servicio prolongado. La publicación argumentaba en contra de un límite denominado fiduciario en las ganancias de ECC, ya que rompería esta alineación de incentivos al reducir la exposición de ECC a ZEC.

Esta fue una de las preguntas formuladas a los miembros del foro de larga data en una [encuesta](https://www.zfnd.org/blog/zip-1014-poll-results/) en [Helios](https://vote.heliosvoting.org/faq) plataforma de votación, cuyos [resultados](https://vote.heliosvoting.org/helios/elections/43b9bec8-39a1-11ea-914c-b6e34ffa859a/view) de los cuales indicaron que 56 no querían una gorra mientras que 18 lo hicieron. Los votantes también optaron por limitar la participación de ECC en las recompensas al 35%, la más pequeña de las opciones presentadas. Todo lo que queda es que la Fundación Zcash y ECC finalicen los detalles del acuerdo, y el 20% de las recompensas de ZEC irán a ECC (35%), Fundación Zcash (25%) y subvenciones importantes (según lo decidido por un panel seleccionado por la Fundación, 40%) - hasta la próxima época de la mitad, cuando el baile comienza de nuevo.

Un desacuerdo relacionado como parte de esta ronda final de encuestas fue sobre la importancia de tener un voto para los titulares de monedas. Esto involucró [dos](https://forum.zcashcommunity.com/t/staked-poll-on-zcash-dev-fund-debate/34846/121) [integrales](https://forum.zcashcommunity.com/t/community-sentiment-polling-results-nu4-and-draft-zip-1014/35560/375) discusiones en el foro ZEC (es bueno ver Decred [mencionado](https://forum.zcashcommunity.com/t/staked-poll-on-zcash-dev-fund-debate/34846/210), parece que hay un contingente de la comunidad ZEC que quisiera pasar a un enfoque de estilo Decred). Al final, el voto de la moneda se convirtió en más de una discusión, como se puede ver en este tablero (advertencia: Google Drive [enlace](https://docs.google.com/spreadsheets/d/e/2PACX-1vSlHXhA_NoJy0RW3Gc6YY3bmYcKT_YF8oS_BrSkBnvEGGaJ56WYo7iL_9shuoh-z_DZMYojA6FpLoJv/pubhtml)).

La ronda 4 del experimento de Financiación Cuadrática de Gitcoin ocurrió, y esta [redacción](https://vitalik.ca/general/2020/01/28/round4.html) de Vitalik Buterin da una cuenta de cómo fue. Esta ronda agregó un flujo de subvenciones de medios, con un presupuesto equivalente más pequeño ($75,000) que el flujo principal de subvenciones de tecnología ($125,000). En las primeras etapas, @antiprosynth, una prominente personalidad de Ethereum en Twitter, estaba en línea para recibir $20,000 en fondos de contrapartida, pero después de algunas campañas sobre estas otras iniciativas recibió más donaciones y la proporción de fondos de contrapartida para esta cuenta de Twitter se redujo a $11,393. Hubo más [controversia](https://twitter.com/TrustlessState/status/1217894717909848067) en la categoría de subvenciones de Medios ya que uno de los proyectos involucraba a un grupo privado que obtendría acceso privilegiado a los resultados. El principal beneficiario en la categoría de subsidios tecnológicos fue Tornado.cash, un mezclador ETH basado en contratos inteligentes.

Jiang Zhuoer reveló un [plan](https://medium.com/@jiangzhuoer/infrastructure-funding-plan-for-bitcoin-cash-131fdcd2412e) para financiar el desarrollo del software Bitcoin Cash con el 12.5% de la recompensa del bloque de BCH. Esto se aplicaría a todos los mineros por una mayoría de la energía minera, y en su forma inicial habría canalizado todos los fondos a una compañía específica. Después de recibir el rechazo de algunas personas en la comunidad BCH, se publicó una [versión](https://read.cash/@Jiang_Zhuoer_BTC.TOP_CEO/bch-miner-donation-plan-update-a45daad6) revisada  del plan. En esta nueva versión, los mineros elegirán a cuál de un conjunto de proyectos de desarrollo preaprobados para donar el 12.5% de sus recompensas en bloque. Si a un minero no le gustan las opciones disponibles, puede elegir quemar esa parte de sus recompensas en lugar de donar. La publicación también parece sugerir reducir la tasa de donación del 12.5% al 2-3%, y deja en claro que los detalles del plan aún están abiertos a discusión. Habrá una ronda de votación de hashrate antes de la implementación, y una Fundación interina para recibir donaciones de mineros y otros, que tendrán votos en proporción a sus fondos donados.

Después de años de demoras en Dash Evolution (un conjunto de cambios de usabilidad como nombres de usuario y libretas de direcciones), una versión de esto ahora llamada Dash Platform se [lanzó](https://dashnews.org/long-awaited-dash-evolution-platform-released-on-testnet-with-developer-documentation-hub/) en un testnet público. Esta será la primera de muchas versiones de testnet antes de cualquier versión del mainnet.

Después [fallar](https://www.reddit.com/r/dashpay/comments/egl6eu/dash_force_news_defunded_by_masternodes/) en obtener fondos del Tesoro de Dash en 3 años, Dash Force ha optado por [disolver](https://app.dashnexus.org/proposals/dash-force-q1-2020/overview) sus operaciones después de las [críticas](https://www.reddit.com/r/dashpay/comments/esaf38/lets_talk_about_dash_force_news/) de la comunidad.

Un [documento de trabajo](https://www.ecb.europa.eu/pub/pdf/scpwps/ecb.wp2351~c8c18bbd60.en.pdf?9bd63a4ddea2300dca05f2ccaa08c0e0) del Banco Central Europeo ha indicado que el BCE necesitaría controlar el volumen utilizado de cualquier moneda digital del Banco Central (CBDC). Un [análisis](https://cointelegraph.com/news/europe-central-bank-proposes-unattractive-rates-for-digital-currency) del documento sugirió que se establecerían tasas poco atractivas para grandes participaciones para desalentar el uso intensivo de la moneda digital. Una preocupación sobre el uso intensivo de un CBDC sería que los titulares podrían mover sus fondos fuera de la jurisdicción del BCE con mayor facilidad en tiempos de crisis.

Los perpetradores de la estafa PlusToken [todavía](https://blog.chainalysis.com/reports/plustoken-scam-bitcoin-price) están batiendo y vendiendo los 180,000 BTC obtenidos de su esquema Ponzi. Aunque 6 personas han sido arrestadas en relación con PlusToken, los fondos todavía se están moviendo y vendiendo a través de intercambios OTC en Huobi, [aparentemente](https://blog.chainalysis.com/reports/plustoken-scam-bitcoin-price), posiblemente afectando el precio de BTC. Los tokens de los estafadores están siendo rastreados a pesar de su uso de mezclas y 24,000 transacciones que involucran 71,000 direcciones para tratar de dificultar esto, porque reutilizaron una dirección. Si bien se ha vendido un valor estimado de $185 millones del BTC, 790K ETH de un total de 800K permanece intacto.

El proveedor custodio de la cartera de bitcoin Bottle Pay [cerró](https://www.coindesk.com/bitcoin-app-bottle-pay-shuts-down-over-impending-eu-money-laundering-laws) en diciembre, citando la regulación AMLD5 de la UE que entró en vigencia el 10 de enero de 2020. Desde el [anuncio](https://bottlepay.helpscoutdocs.com/article/40-official-announcement-on-the-shutdown-of-bottle-pay): “La cantidad y el tipo de información personal adicional que se nos requeriría recopilar de nuestros usuarios alteraría La experiencia actual del usuario y es tan radical y tan negativa que no estamos dispuestos a forzar esto en nuestra comunidad”. Respetar los principios y cerrar es lo contrario de hacer lo que sea necesario para [mantener](https://thenextweb.com/hardfork/2018/09/05/shapeshift-cryptocurrency-exchange-kyc/) el negocio a flote. El caso puede servir como una señal más para centrar los esfuerzos en mejorar el software criptográfico de custodia propia.

Kraken Security Labs [reveló](https://blog.kraken.com/post/3662/kraken-identifies-critical-flaw-in-trezor-hardware-wallets/) una fálla de seguridad crítica tanto en Trezor One como en Trezor Model T que permite extraer la semilla dentro de los 15 minutos posteriores al acceso físico al dispositivo. “El ataque aprovecha las fallas inherentes dentro del microcontrolador utilizado en las carteras Trezor. Desafortunadamente, esto significa que es difícil para el equipo de Trezor hacer algo sobre esta vulnerabilidad sin un rediseño de hardware". Las protecciones recomendadas son no permitir que nadie acceda físicamente al dispositivo y habilitar la función Frase de contraseña en el software Trezor Client.

$500 mil millones que la Fed bombea al mercado nocturno de dinero (repos) ha llamado la atención de Colin Harper de la revista Bitcoin, en un buen [artículo](https://bitcoinmagazine.com/articles/the-fed-has-pumped-500-billion-into-the-repo-market-where-does-it-end) que presenta el tema y pregunta qué está pasando.

## Sobre esta edición

Este es el número 22 de Decred Journal. El índice de todos los problemas y traducciones está disponible [aquí](https://xaur.github.io/decred-news/).

La mayoría de la información de terceros se transmite directamente desde la fuente después de un control mínimo. Los autores de Decred Journal no tienen la capacidad de verificar todas las reclamaciones. Tenga cuidado con las estafas y haga su propia investigación.

Sus [comentarios](https://github.com/xaur/decred-news/blob/docs/contributing.md#feedback) y [contribuciones](https://github.com/xaur/decred-news/blob/docs/contributing.md) son siempre bienvenidos.

Créditos (orden alfabético):

- Escritura y edición: bee, degeri, Dustorf, kozel, richardred, s_ben
- Revisiones y comentarios: ammarooni, buck54321, davecgh, dnldd, emiliomann, jholdstock, lukebp, matheusd
- Imagen de título: saender
- Traducción al Español: @Francov_
