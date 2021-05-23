# Revista Decred - Enero 2021

![portada](./assets/202101.png)

Imagen: Disipación de desbordamiento por @saender

¡Feliz cumpleaños Decred!

Destrás quedan cinco años de desarrollo continuo y cumpliento la promesa de descentralización, un paso pragmático a la vez. Enero no fue diferente:

- La v1.6 ya está disponible, consulta la sección de “Hydra ya está aquí” a continuación para que obtengas los detalles del lanzamiento.
- El precio de los tickets y la participación en PoS siguieron aumentando hasta alcanzar nuevos máximos.
- El récord de participación dentro de una propuesta en Politeia se rompió en enero, y nuevamente ya en febrero, ¡llegando hasta el 70% de participación!
- El financiamiento continuo del DCRDEX fue aprobado casi por unanimidad, Decred in Depth y el equipo de Decred Arabia también recibieron algunas propuestas aprobadas.
- La Revista Decred por fin tiene su propia propuesta en Politeia (compartida con el socio menor Politeia Digest) que vería asegurada la financiación para 2021, y ya se está votando.

## El Hidden Hydra ya está aquí

¡La tan esperada v1.6 también conocida como Hidden Hydra finalmente está aquí! Esta es probablemente la mayor actualización en la historia de Decred con varias actualizaciones importantes y numerosas actualizaciones más pequeñas en todos los proyectos de software. Todos los cambios se enumeran en las notas de la versión detalladas, por lo que aquí solo destacaremos los más importantes:

- **Las transacciones privadas** ahora son accesibles a través de la interfaz gráfica del usuario de Decrediton. Funciona mezclando monedas y haciendo que sea extremadamente difícil rastrearlas y espiar su saldo o actividad. Esta función es fundamental para proteger la privacidad de los usuarios habituales y especialmente de los votantes, cuya privacidad mejora la seguridad de toda la red. También protege el principio de fungibilidad en la [Constitución](https://docs.decred.org/governance/decred-constitution/) de Decred. La implementación elegida (StakeShuffle) tiene las hermosas propiedades de mantener el suministro de monedas auditable en todo momento, confiando en una criptografía simple y logrando una alta privacidad gracias a la integración inteligente con el sistema de participación y un gran volumen de mezcla.
- **La nueva arquitectura del VSP** mejora enormemente la experiencia de uso de proveedores de servicios de votación, que son utilizados por aproximadamente la mitad de todos los votantes que no utilizan carteras de votación las 24 horas del día, los 7 días de la semana. Sin cuentas para crear y recordar, sin canjear scripts para respaldar, sin correo electrónico para compartir, sin direcciones reutilizadas y soporte de mezcla opcional, todo hace que las apuestas sean más fáciles y privadas.
- **El control de la tesorería descentralizada** transferirá la facultad de aprobar o rechazar el gasto de la tesorería a manos de las partes interesadas de Decred. Los cambios de consenso necesarios se votarán en los próximos meses y se activarán si se aprueban.
- **DCRDEX** brinda un intercambio seguro, privado y justo, donde controlas las claves en todo momento y el intercambio nunca tiene monedas. La información privada está protegida de la mejor manera posible, al no recopilarla. La combinación de coincidencia de órdenes pseudoaleatorias dentro de las épocas, que requiere fondos en cadena y límites de tasas, evita el mal comportamiento, como operaciones de alta frecuencia, ejecución inicial, falsificación de órdenes y falsificación del volumen de operaciones. Y el intercambio no cobra comisiones comerciales.

Y estos son los pasos de alto nivel para actualizar:

- Consulte la [página](https://decred.org/release/) de la nueva versión para obtener una descripción general de las nuevas funciones y los enlaces de descarga, o vea la [descripción general](https://www.youtube.com/watch?v=3AxBa-EE8RM) del video (las funciones de la v1.6 comienzan en 21:00).
- [Verifica las descargas](https://docs.decred.org/advanced/verifying-binaries/) (la rutina no es divertida, ¡pero garantiza que los archivos no hayan sido manipulados!).
- Lee las [notas de la versión](https://github.com/decred/decred-binaries/releases/tag/v1.6.0) y presta atención a las advertencias de degradación: no será posible utilizar versiones anteriores después de que se hayan actualizado los archivos de blockchain y billetera.
- Aprender a mezclar con el tutorial en [video](https://www.youtube.com/watch?v=QC65PBNwAK4) de @Salirus.
- Compra tickets desde el vspd en Decrediton eligiendo un VSP en el menú desplegable y la cantidad de tickets, y déjelo abierto hasta que se mida la transacción y se pague la tarifa del VSP (puede demorar hasta 20 minutos). Si ve un "Error" en los tickets, vuelva a sincronizarlo, que se encuentra en la pestaña de estado del ticket.
- Establece tu [elección](https://docs.decred.org/governance/consensus-rule-voting/how-to-vote/) para la próxima votación de cambio de regla de consenso para habilitar la tesorería descentralizada. Para saber cómo funciona, lea la [propuesta](https://proposals.decred.org/proposals/c96290a) de un concepto general y el [DCP](https://github.com/decred/dcps/blob/master/dcp-0006/dcp-0006.mediawiki) para obtener los últimos detalles técnicos. Si es nuevo en la gobernanza de Decred, vea el [video tutorial](https://www.youtube.com/watch?v=1QiC0btcf7E) de gobernanza rápida de @Checkmate.
- Observa el progreso de la votación por consenso y la actualización de la red [aquí](https://voting.decred.org/) o [aquí](https://explorer.dcrdata.org/agenda/treasury).
- Actualmente, el uso de DCRDEX requiere algunas habilidades técnicas, pero esto se simplificará en las próximas versiones. Mientras tanto, puede seguir esta [guía](https://medium.com/decred/how-to-get-on-dcrdex-mvp-816d713ec5c0) de @richardred.

Hay algunos [problemas conocidos](https://www.reddit.com/r/decred/comments/lebx71/error_when_trying_to_purchase_tickets_with/) con la compra de tickets en Decrediton v1.6.0 que se solucionarán en el próximo lanzamiento de parche.

## Desarrollo

A menos que se indique lo contrario, el trabajo que se informa aquí tiene el estado "fusionado con la rama master". Significa que el trabajo se completó, revisó e integró en el código fuente que los usuarios avanzados pueden construir y ejecutar, pero aún no está disponible en los binarios del lanzamiento en general.

Las actualizaciones de enero en dcrd son un buen ejemplo de lo que los usuarios que compilan desde [el código fuente](https://medium.com/@artikozel/the-decred-node-back-to-the-source-part-one-27d4576e7e1c) pueden obtener hoy sin tener que esperar a la próxima versión.

[**dcrd**](https://github.com/decred/dcrd)

El principal esfuerzo del mes fue preparar, revisar a fondo y probar varios cambios épicos hacia la descarga de bloques de [múltiples pares](https://github.com/decred/dcrd/issues/1145), aunque los cambios son generalmente útiles para simplificar el código y desbloquear futuras optimizaciones:

- Procesamiento e indexación de bloques completamente [rediseñado](https://github.com/decred/dcrd/pull/2518) para usar semántica de encabezados y soporte para procesamiento desordenado de datos de bloque.
- Manejo de UTXO reelaborado para que funcione [por punto de salida](https://github.com/decred/dcrd/pull/2540) en lugar de a nivel de transacción.
- [Modelo de sincronización](https://github.com/decred/dcrd/pull/2555) reelaborado para utilizar el encabezado. Los pequeños [encabezados](https://devdocs.decred.org/developer-guides/block-header-specifications/) de 180 bytes se descargarán antes de cualquier dato de bloque, y luego solo se descargarán los bloques necesarios. Esto optimiza el tráfico, elimina el concepto de “bloques huérfanos” y abre la puerta a futuras mejoras.
Preparativos para implementar la caché UTXO.

Otros cambios:

- Documento [DCP-0006](https://github.com/decred/dcps/blob/master/dcp-0006/dcp-0006.mediawiki) finalizado que describe los detalles técnicos del próximo cambio de consenso del fondo de la tesorería descentralizada.
- Se agregaron 3 nuevas [generadoras de semilla](https://github.com/decred/dcrd/pull/2532) HTTPS para reducir la dependencia del dominio decred.org.
- Los cfilters de la versión 1 obsoleta se [eliminaron](https://github.com/decred/dcrd/pull/2525) a favor de la v2 más eficiente (los "filtros compactos" potencian la increíble tecnología [SPV](https://docs.decred.org/wallets/spv/) de Decred para clientes ligeros).
- [Autenticación](https://github.com/decred/dcrd/pull/2482) de cliente TLS agregada mediante certificados de cliente (más flexible que usuario + contraseña).
- Se agregó soporte de clave [RSA](https://github.com/decred/dcrd/pull/2551) de 4096 bits a la herramienta Gencerts.
- Nuevos comandos para [invalidar](https://github.com/decred/dcrd/pull/2536) bloques arbitrarios y reconsiderar bloques arbitrarios para la validación (permite pruebas más fáciles y actualizaciones más fluidas en el futuro).
- Evitar conexiones pendientes [duplicadas](https://github.com/decred/dcrd/pull/2563) a la misma dirección IP y puerto.
- Actualizaciones diversas para probar el código, el registro, los documentos, las dependencias, las correcciones menores, etc.

Se [**fusionaron**](https://github.com/decred/dcrd/pulls?q=is%3Apr+merged%3A2021-01-01..2021-01-31+sort%3Aupdated-asc) un total de 47 PR de 10 contribuyentes, agregando 12 000 y eliminando 7 000 líneas de código.

En progreso:

- Introducir [filtros Bloom con particiones por tiempo-edad](https://github.com/decred/dcrd/pull/2579) para reducir significativamente la memoria utilizada para rastrear qué datos se sabe que tienen otros pares.

[**dcrwallet**](https://github.com/decred/dcrwallet)

- El cliente VSP se [reescribió](https://github.com/decred/dcrwallet/pull/1956) para mejorar el procesamiento en segundo plano y respaldar la recuperación de la información de pago de tarifas después de la restauración de semillas.
- [Reglas](https://github.com/decred/dcrwallet/pull/1961) restringidas de lo que se considera un posible CoinJoin (utilizado al detectar la cuenta mixta de la billetera durante la recuperación de la semilla)

Los cambios anteriores también se portaron a la versión v1.6.

[**Decrediton**](https://github.com/decred/decrediton)

- Nueva página que muestra una lista de salidas [no gastadas](https://github.com/decred/decrediton/pull/3098) (UTXO).
- Mostrar VSP en orden [aleatorio](https://github.com/decred/decrediton/pull/3114).
- Actualizar el [estado del ticket](https://github.com/decred/decrediton/pull/3121) en inicios, reinicios y restauraciones de semillas.
- Eliminar el uso de tokens [CSRF](https://github.com/decred/decrediton/pull/3133) al comunicarse con Politeia, para evitar fugas de privacidad.
- [Autodetectar](https://github.com/decred/decrediton/pull/3033) si la billetera usó mezcla en el pasado.
- Sugerencias de interfaz de usuario para propuestas y presentaciones de [RFP](https://github.com/decred/decrediton/pull/3118).
- Traducciones actualizadas.
- Algunas actualizaciones del soporte de Trezor.
- Pruebas de IU más automatizadas.
- ~ 24 correcciones de errores y 3 ajustes de [interfaz de usuario](https://github.com/decred/decrediton/pull/2659).

La mayoría de los cambios anteriores se incluyeron en la versión v1.6 y el resto tendrán lugar en la versión del parche v1.6.1.

[**Politeia**](https://github.com/decred/politeia)

- Interfaz de usuario para configurar y verificar códigos [TOTP](https://github.com/decred/politeiagui/pull/2127) para 2FA.
- Mostrar las [reglas básicas de la propuesta](https://github.com/decred/politeiagui/pull/2290) antes del botón Enviar.
- Eliminar las llamadas a [dcrdata](https://github.com/decred/politeia/pull/1360) desde la herramienta de línea de comandos politeiavoter.

CMS:

- Resumen de [facturación](https://github.com/decred/politeiagui/pull/2275) de propuesta mejorado.
- Visualización mejorada de [estadísticas de código](https://github.com/decred/politeiagui/pull/2279).
- Corrección de errores.

[**vspd**](https://github.com/decred/vspd)

- El envío de la transacción [principal](https://github.com/decred/vspd/pull/218) del ticket se hizo obligatorio, ya que reduce en gran medida la posibilidad de errores de transmisión del ticket
- Dependencias actualizadas

vspd [versión 1.0.0](https://github.com/decred/vspd/releases/tag/release-v1.0.0) ahora está etiquetado y todos los operadores de VSP deben actualizar su implementación de red principal.

v1.0.0 marca el comienzo de un proceso de lanzamiento adecuado, en el que los operadores de VSP solo deberían ejecutar lanzamientos etiquetados en producción (hasta ahora, vspd todavía estaba en desarrollo y los operadores acababan de implementar el último maestro).

[**dcrpool**](https://github.com/decred/dcrpool)

- Varias mejoras para el manejo de configuraciones, errores y redireccionamientos HTTP.

En progreso:

- Soporte para implementaciones de [proxy inverso](https://github.com/decred/dcrpool/pull/301)
  Soporte NiceHash.

[**dcrlnd**](https://github.com/decred/dcrlnd)

- Arreglos de apagado y actualizaciones de dependencia.

[**dcrdex**](https://github.com/decred/dcrdex)

Tres temas clave en enero fueron solucionar los problemas restantes para el parche v0.1.4 (que era parte del lanzamiento de v1.6), continuar el desarrollo hacia el próximo hito v0.2 y administrar la propuesta para la siguiente fase de desarrollo.

Trabajo fusionado:

- Permitir al usuario [exportar e importar](https://github.com/decred/dcrdex/pull/885) datos de la cuenta (principalmente claves privadas).
- Admitir el [cambio](https://github.com/decred/dcrdex/pull/901) de billetera BTC sin cifrar a cifrada.
- [Límites](https://github.com/decred/dcrdex/pull/874) de tasas de tarifa del lado del cliente.
- Archivos de [configuración](https://github.com/decred/dcrdex/pull/927) de muestra.
- Validar [la tarifa máxima](https://github.com/decred/dcrdex/pull/898) en el momento del emparejamiento de orden para evitar parcialmente que el servidor asigne maliciosamente una tarifa demasiado alta.
- Se corrigieron varios problemas con la validación de la dirección, el bloqueo de la billetera, el inicio de sesión, etc., y los transfirieron a la versión v0.1.4.

Se [fusionaron](https://github.com/decred/dcrdex/pulls?q=is%3Apr+merged%3A2021-01-01..2021-01-31+sort%3Aupdated-asc) un total de 32 PR de 7 contribuyentes, agregando 3 000 y eliminando 1 000 líneas de código.

Consulta la [segunda propuesta](https://proposals.decred.org/proposals/d462ac3) para ver un plan general de lo que vendrá en los próximos 9 meses. Además, este [tweet](https://twitter.com/behindtext/status/1355478387721187328) insinuó una posible integración de la privacidad en el lado del trading en DCR.

¡Felicitaciones al equipo de DCRDEX con el impresionante 98% de votos a favor!

[**dcrandroid**](https://github.com/planetdecred/dcrandroid)

- Soporte inicial de [StakeShuffle](https://github.com/planetdecred/dcrandroid/pull/520): cuando está habilitado, la generación de direcciones de recepción para la cuenta mixta y el envío de fondos desde la cuenta de cambio están deshabilitados.
- Páginas de la [interfaz de usuario](https://github.com/planetdecred/dcrandroid/pull/529) de privacidad: introducción, ventana emergente de ayuda, visualización del saldo sin mezclar, detalles del servidor CSPP, progreso del mix, etc.
- Soporte de [propuestas](https://github.com/planetdecred/dcrandroid/pull/503) de Politeia: ver una lista de propuestas y su estado de votación, abrir una propuesta específica y recibir notificaciones sobre nuevas propuestas, inicio y finalización de la votación
- Página de depuración para ver detalles sobre [pares](https://github.com/planetdecred/dcrandroid/pull/501) conectados.
- Opción para crear una billetera [watch-only](https://github.com/planetdecred/dcrandroid/pull/530) desde la pantalla de inicio.
- Notificaciones más específicas para las transacciones de votación y revocación de [tickets](https://github.com/planetdecred/dcrandroid/pull/531).

Para habilitar las características anteriores, se agregaron mezclas y compatibilidad con Politeia a la librería base de [dcrlibwallet](https://github.com/planetdecred/dcrlibwallet) y ahora pueden ser reutilizadas por dcrios y godcr.

[**dcrios**](https://github.com/planetdecred/dcrios)

- Notificaciones para [cfilters](https://github.com/planetdecred/dcrios/pull/728) que recuperan el progreso.

[**godcr**](https://github.com/planetdecred/godcr)

- [Interfaz de usuario](https://github.com/planetdecred/godcr/pull/293) implementada y configuración para la mezcla de StakeShuffle.
- Agregadas [páginas de configuración de la aplicación](https://github.com/planetdecred/godcr/pull/305) y [configuración de billetera](https://github.com/planetdecred/godcr/pull/298).
- Nueva interfaz de usuario para las páginas de mensaje de [firma](https://github.com/planetdecred/godcr/pull/288) y [verificación](https://github.com/planetdecred/godcr/pull/286).
- Encabezados actualizados en las páginas para una mejor UX
- La API para superponer widgets se agregó a la librería de [Gio](https://gioui.org/) y se usó para lograr el diseño y el comportamiento de la interfaz de usuario previstos en la página de Wallets.

[**dcrdata**](https://github.com/decred/dcrdata)

- Una codificación de transmisión más eficiente de las [exportaciones CSV](https://github.com/decred/dcrdata/pull/1800).
- [Módulos](https://github.com/decred/dcrdata/pull/1796) reorganizados para el ciclo de desarrollo v6.
- Mostrar etiquetas de Swap Contract y Swap Redemption para transacciones de [swap atómico](https://github.com/decred/dcrdata/pull/1733).

[**dcrros**](https://github.com/decred/dcrros)

- actualizado para que coincida con la especificación Rosetta [v1.4.8](https://github.com/decred/dcrros/pull/15), que requiere realizar un seguimiento de las monedas no gastadas por cuenta.

[**docs**](https://github.com/decred/dcrdocs)

- [Eliminar](https://github.com/decred/dcrdocs/pull/1144) la necesidad de ejecutar JavaScript del lado del cliente para representar valores matemáticos y fórmulas, cambió para representarlos con HTML y CSS sin formato, y eliminar 9 MB de material MathJax (gracias @jholdstock ❤).
- Actualización parcial para la versión [v1.6](https://github.com/decred/dcrdocs/pull/1142) (Privacy y LN próximamente).

[**decred.org**](https://github.com/decred/dcrweb)

- Agregar una nueva página elegante dedicada a la [versión v1.6](https://decred.org/release/).
- Actualizaciones de contenido.

[**Decred Address Scanner**](https://github.com/JoeGruffins/dcraddrscanner)

La versión 1.06 ha sido lanzada con una nueva estructura de base de datos y capacidades de observación de tickets. Está disponible en [Google Play](https://play.google.com/store/apps/details?id=com.joegruff.decredaddressscanner) y como descarga directa de APK en [GitHub](https://github.com/JoeGruffins/dcraddrscanner/releases).

Estado a la actualización del [20 de enero](https://github.com/decredcommunity/proposals/blob/master/proposals/3943bff/updates/20210120.md):

- La [integración](https://github.com/decred/decrediton/pull/3112) de Decrediton está pendiente de revisión, hará que los tickets sean más fáciles de cargar en la aplicación.
- Se están investigando las compilaciones de [F-Droid](https://github.com/JoeGruffins/dcraddrscanner/issues/6).
- Se eligió la licencia de [Blue Oak](https://blueoakcouncil.org/license/1.0.0), pero esta puede cambiar para adaptarse a los [requisitos](https://github.com/JoeGruffins/dcraddrscanner/issues/6) de F-Droid.
- El soporte de filtro compacto está en progreso pero necesita mucho trabajo (esta es la forma que más preserva la privacidad de obtener información de dirección, la misma que usan las billeteras SPV).

Otros desarrollos:

- [dcrseeder](https://github.com/decred/dcrseeder) recibió correcciones para el seguimiento de [pares](https://github.com/decred/dcrseeder/pull/43) y el [apagado](https://github.com/decred/dcrseeder/pull/41).
- [La herramienta de lanzamiento](https://github.com/decred/release) se actualizó a v1.6 y fue utilizada por varios desarrolladores para reproducir compilaciones de lanzamiento.
- El programa Bug Bounty [informó](https://bounty.decred.org/2021/01/status-update/) que ha procesado un total de 150 envíos y 14 eran elegibles para pago.
- La ayuda para el desarrollo es [bienvenida](https://www.reddit.com/r/decred/comments/l3pj90/dcronchain_status/gki371x/) para [dcronchain.com](https://dcronchain.com/): la aplicación [se basa](https://github.com/Decred-Bulls/dcronchain) en Nuxt.js (derivado de Vue.js)


## Comunidad 
Damos la bienvenida a los nuevos colaboradores con código fusionado en la rama master @lolandhold ([dcrd](https://github.com/decred/dcrd/commits?author=lolandhold])), @brunaazambuja ([pi-ui](https://github.com/decred/pi-ui/commits?author=brunaazambuja)), @hamurabiaraujo ([pi-ui](https://github.com/decred/pi-ui/commits?author=hamurabiaraujo))

Estadísticas de la comunidad a partir del 1 de febrero
Seguidores en:

- [Twitter](https://twitter.com/decredproject): 41 801 (+481)
- Suscriptores en [Reddit](https://www.reddit.com/r/decred/): 10 201 (+150)
- Usuarios en la sala #general de [Matrix](https://chat.decred.org/): 344 (+57)
- Usuarios en [Discord](https://discord.com/invite/GJ2GXfz): 1 917 (+194)
- Usuarios en [Telegram](https://t.me/Decred): 2 428 (+90)
- Suscriptores en [YouTube](https://www.youtube.com/decredchannel): 4 320 (+20), vistas: 169 000 (+4 000)
- Seguidores en [LinkedIn](https://www.linkedin.com/company/decredproject/): 962 (+18)
- Estrellas en el repositorio [dcrd](https://github.com/decred/dcrd) en GitHub: 575 (+5), forks: 249 (+2)

Cambios inusuales detectados entre las cuentas [rastreadas](https://github.com/decredcommunity/social-media-stats):
- La cuenta de twitter [@decredproject](https://twitter.com/decredproject) tuvo una segunda afluencia de casi +500 seguidores después de los +400 anteriores (después de 1,5 años de casi ningún cambio)
- Los chats de Matrix obtuvieron un aumento del 20% y Discord de un 11% de usuarios
- Telegram revirtió después de 6 meses de declive ganando un aumento del 4% de usuarios
- En telegram el canal de [DecredTrading](https://t.me/DecredTrading) obtuvo otro aumento del 26%
- La página del proyecto [CoinMarketCap](https://coinmarketcap.com/currencies/decred/) de alguna manera agregó más de 8 000 observadores (+ 45%)
- [@Checkmate](https://twitter.com/_Checkmatey_) obtuvo otro aumento del 13% de seguidores (a 4 000) y publicó mil tweets (~ 34 / día) por tercer mes consecutivo
- La [página rusa de VK](https://vk.com/decred_project) está publicando actualizaciones nuevamente después de un largo período de inactividad.

## Gobernanza
En enero, el [fondo de tesorería](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx) recibió 11 878 DCR y gastó 6 750 DCR. Utilizando la tasa promedio diaria DCR/USD en enero de $54.25, esto es $644 000 recibido y $366 000 gastado. A la tasa diaria promedio de diciembre 31.07 dólares, la cifra en dólares facturada por trabajos anteriores es de $210 000. A partir del 10 de febrero el balance del fondo de tesorería es de 647 942 DCR (64.3 millones de dólares a $99.26).

Cuatro propuestas fueron publicadas en enero, según la publicación de la Revista Decred todas habían terminado de votar a principios de febrero:

- [La propuesta](https://proposals.decred.org/proposals/d462ac3) de desarrollo de la Fase 2 de DCRDEX estableció nuevos récords en términos de apoyo del grupo de tickets, ¡con el 53% de los tickets elegibles que votaron casi por unanimidad que sí (98.2%)! Esta propuesta aprobó un presupuesto de $245 000 para desarrollar un conjunto de características que incluyen soporte para billeteras SPV, comercio de tokens ETH y ERC-20, más bifurcaciones de Bitcoin e integración de Decrediton.
- El podcast Decred in Depth estará bajo una nueva administración, y hacerlo en vivo, después de que se aprobara una [propuesta](https://proposals.decred.org/proposals/391108e) de @elima_iii con un 86,3% de aprobación y un 28% de participación; esto cubre entre 24 y 36 episodios a $ 500 por episodio.
- Una nueva propuesta de investigación de @ammarooni solicitó $ 17,500 para escribir y publicar un libro, [Créditos descentralizados: la digitalización del dinero y el estado](https://proposals.decred.org/proposals/9e1d644): esta propuesta fue rechazada por poco a principios de febrero, con una aprobación del 57% y una participación récord del 70%.
- El equipo de Decred Arabia [solicitó](https://proposals.decred.org/proposals/d0c32d5) 6.200 dólares para seis meses de financiación. Esta propuesta fue aprobada a principios de febrero con un 96% de apoyo y una participación del 55%, lo que la convierte en la propuesta con la segunda participación más alta (por delante de la propuesta de la fase 2 de DCRDEX, que pasó del nuevo récord al tercero en unas pocas semanas ).
Parece que el aumento en el precio de los tickets y la participación de PoS también ha resultado en un mayor nivel de participación de Politeia por parte de las personas que participan en el staking.

Se enviaron otras dos propuestas a principios de febrero, para la [Revista Decred 2021](https://proposals.decred.org/proposals/1d74b88) (presupuesto máximo $39 000) y [Open Source Research 2021](https://proposals.decred.org/proposals/020b8b0) (presupuesto máximo $40 000). La propuesta de la Revista Decred ofrece la oportunidad de dejar comentarios más formales e inmutables de lo habitual, y también puede (si tiene ticketss) votar para continuar financiando la Revista.

@buck54321 redactó una [propuesta previa](https://gist.github.com/buck54321/4c67c5f5e16fadd076673f2b245ca92b) para Decred Eco, un administrador de aplicaciones GUI para instalar, configurar y actualizar una lista cada vez mayor de software relacionado con Decred sin tocar la línea de comandos (piense en lo que hace Steam para los juegos).

@Checkmate y @pavel han [aclarado](https://www.reddit.com/r/decred/comments/l3pj90/dcronchain_status/) el estado de la propuesta de dcronchain.com: el proyecto está vivo, el desarrollo continúa cuando hay tiempo disponible y no está siendo reemplazado por [checkonchain.com](https://checkonchain.com/). Todas las actualizaciones de propuestas conocidas se han recopilado [aquí](https://github.com/decredcommunity/proposals/tree/master/proposals/0230918/updates).

Politeia Digest regresó con el [issue 40](https://blockcommons.red/politeia-digest/issue040/) de actualización que también cubría las propuestas de diciembre.

## Red
Hashrate: el [hashrate](https://explorer.dcrdata.org/charts?chart=hashrate&zoom=kjc6iems-kkn6rfe4&scale=linear&bin=block&axis=time) de enero se abrió a ~348 Ph/s y cerró ~ 406 Ph/s, tocando fondo en 283 Ph/s alcanzando un máximo de 545 Ph/s durante todo el mes.

[Distribución](https://miningpoolstats.stream/decred) del hashrate en los pools a partir del 1 de febrero:
- UUPool 33%
- Poolin 29%
- easy2mine 9.4%
- F2Pool 5.2%
- Antpool 18%
- Huobipool 1.9%
- BTC.com 2%
- Luxor 1.1%
- CoinMine 0.04%

Staking: el precio medio del ticket a [30 días](https://dcrstats.com/) fue de 173.23 DCR (+9.3). El precio varió entre 149.9 y 212.3 DCR. [El monto bloqueado](https://explorer.dcrdata.org/charts?chart=ticket-pool-value&zoom=kjc6iems-kkn6rfe4&scale=linear&bin=block&axis=time) por [participación](https://explorer.dcrdata.org/charts?chart=stake-participation&zoom=kjc6iems-kkn6rfe4&scale=linear&bin=block&axis=time) fue de 6.55 a 7.12 millones de DCR, lo que correspondió al 52.53 a 56.71%% del suministro disponible en PoS.

Una vez más, tuvimos cifras récord este mes tanto en términos de precio del ticket por 212.28 DCR (con un nuevo [USD ATH](https://twitter.com/TheBochinchero/status/1347934876054532096)) como también participación de stake del ¡56.71%!

Nodos: a lo largo de [enero](https://charts.dcr.farm/d/000000014/nodes?orgId=1&from=1609459200000&to=1612137600000) hubo un promedio de 116 nodos públicos y 235 nodos de dcr.farm.

Distribución de versiones promedio para enero:
- 22% dcrd v1.5.2
- 14% dcrd v1.6.0
- 13% dcrd v1.6 dev y RC builds
- 13% dcrd v1.5.1 
- 4% dcrd v1.7 dev builds 
- 3.6% dcrd v1.5.0 
- 2.3% dcrd v1.5 dev y RC builds
- 0.4% dcrd v1.4
- 10% dcrwallet v1.5.1
- 7% dcrwallet v1.6.0
- 1% dcrwallet v1.6 dev y RC builds
- 1% dcrwallet v1.5
- 0.6% dcrwallet v1.4
- 8% otros.

A partir del 10 de febrero, se alcanzó el [umbral de actualización](https://voting.decred.org/) de PoS para el [cambio](https://github.com/decred/dcps/blob/master/dcp-0006/dcp-0006.mediawiki) de consenso del fondo de tesorería descentralizada, mientras que el PoW se está poniendo al día al 50%.

Lightning Network de Decred tenía 28 nodos (+4), 47 canales (+5) con una capacidad total de 8.3 DCR (-0.4), al 1 de febrero. El mapa de la red de @jholdstock se ha trasladado a un [nuevo dominio](https://ln-map.jholdstock.uk/). La capacidad de LN es cada vez más importante a medida que se exponen más funciones de LN a los usuarios finales a través de la GUI de Decrediton. ¡Gracias a todos los operadores de LN por [ejecutar los nodos](https://docs.decred.org/lightning-network/overview/)!

En su segundo [reporte](https://blockcommons.red/post/dcr-on-chain-2/) de análisis de blockchain, @richardred continúo cómo las monedas recién extraídas fluyen a través de los grupos de minería, sus mineros y finalmente llegan a las direcciones de intercambio. El informe se actualiza sobre el progreso del desarrollo de las herramientas y comparte visualizaciones de grupos de direcciones / transacciones y el flujo de fondos. El enfoque principal del informe está en los 5 clústeres que recibieron la mayor cantidad de DCR de [Coinbase](https://docs.decred.org/glossary/#coinbase-transaction) en 2019-2020, y los 5 que recibieron la mayor cantidad de DCR de estas transacciones. Se pensaba que estos grupos representaban grupos de minería y sus usuarios, pero el examen de cómo están estructurados indicó variabilidad en la función, y algunos parecen pertenecer a individuos. Se puede tomar un total de 4,852 grupos distintos (con más de 1 dirección cada uno) como una estimación aproximada del número de personas / billeteras diferentes que extrajeron DCR en este período.

## Integraciones

dcr.farm agregó soporte para vspd en un nuevo subdominio [vsp.dcr.farm](https://vsp.dcr.farm/). A principios de febrero, [decredvoting.com](https://decredvoting.com/) y [dcrpool.ibitlin.com](https://dcrpool.ibitlin.com/) también se actualizaron para admitir el vspd. Este último ofrece un [bot de Telegram](https://t.me/DcrTicketNotificationBot) adicional para ver los tickets.

Los VSP que no respondieron [decred.everstake.one](https://decred.everstake.one/) y [dcrpos.megapool.info](https://dcrpos.megapool.info/) se eliminaron de la lista.

Al momento de escribir, [10 de 17 VSP](https://github.com/decred/vspd/issues/231#issuecomment-774877129) se han actualizado al [vspd](https://github.com/decred/vspd). Los operadores de VSP deben tener en cuenta que los usuarios de Decrediton v1.6 verán la lista de nuevas instancias de vspd como una opción recomendada, lo que significa que los VSP que se actualizan antes pueden robar algunos usuarios a los más lentos.

Brazilian [Monnos](https://monnos.com/) anunció la [incorporación](https://twitter.com/MonnosGlobal/status/1351212798739669004) de DCR a su cartera. La plataforma permite intercambiar criptomonedas por dinero fiduciario BRL, copiar estrategias de otros comerciantes ("comercio social") y planes para emitir tarjetas de pago criptográficas. Al momento de escribir, los depósitos DCR [no están disponibles](https://monnos.com/en/fees-and-limits/), pero la compra, el comercio y el retiro pueden funcionar.

Nigerian [First Kudi](https://firstkudi.com/) [anunció](https://twitter.com/firstkudiapp/status/1353729854697582598) que DCR se agregó a su nueva plataforma [First Kudi Pro](https://first-kudi.medium.com/introducing-first-kudi-pro-2b8d30f85d08) que permite intercambiar criptomonedas con monedas fiduciarias NGN y monedas estables USDT / GUSD.

Binance tenía los depósitos y retiros DCR desactivados durante [más de 30 horas](https://twitter.com/behindtext/status/1354389277870845959) a partir de aproximadamente 12 horas después del lanzamiento de la v1.6.

> Advertencia: los autores de la Revista Decred no tienen idea de la confiabilidad de alguno de los servicios anteriores. Haga su propia investigación antes de confiar su información personal o activos.

## Adopción

La empresa de riesgo [Inflection](https://www.inflection.xyz/) que se encuentra en etapa inicial cerró su [segundo fondo](https://twitter.com/alexlangevc/status/1346409341004509184) con DCR como uno de los activos. Su página de inicio define a Decred como una “Nación de internet y plataforma de gobierno”.

## Alcance

Logros de Monde PR en enero:
- creó / lanzó 2 historias para publicaciones financieras y criptográficas.
- respondió a 3 solicitudes de comentarios.
- consiguió 3 entrevistas con los medios de comunicación.

Cobertura de noticias por parte de Monde PR:

- un artículo en [Cointelegraph](https://cointelegraph.com/news/decred-co-founder-explains-the-possible-effects-of-a-cbdc-takeover) con comentarios de @ jy-p sobre los efectos de una adquisición de CBDC (sindicado a 25 medios de comunicación, incluidos [Investing.com](https://www.investing.com/news/cryptocurrency-news/decred-cofounder-explains-the-possible-effects-of-a-cbdc-takeover-2391956) y [Cointelegraph Brasil](https://cointelegraph.com.br/news/decred-co-founder-explains-the-possible-effects-of-a-cbdc-takeover)). Los comentarios también se utilizaron en 3 noticias posteriores, en [Cointelegraph](https://cointelegraph.com/news/horizen-labs-co-founder-says-cbdcs-could-raise-bitcoin-awareness) (sindicado a 9 medios de comunicación), [World Stock Market](https://www.worldstockmarket.net/co-founder-of-decred-digital-currencies-of-the-central-bank-are-not-an-obstacle-to-cryptocurrencies/) y [Etherdesk](https://www.etherdesk.com/cbdcs-impact-on-bitcoin-adoption-expalined/).
- el lanzamiento de Decred v1.6 fue cubierto por [Bitcoin Exchange Guide](https://bitcoinexchangeguide.com/decred-launches-private-transactions-integrates-lightning-network-decentralizes-treasury/), [Crypto Mode](https://cryptomode.com/decreds-position-as-money-evolved-further-cemented-by-three-new-features/) (sindicado a [Crypto News BTC](https://cryptonewsbtc.org/2021/01/27/decreds-position-as-money-evolved-further-cemented-by-three-new-features-cryptomode/)), [8btc](https://www.8btc.com/article/6589360), [Explica](https://www.explica.co/decred-updates-its-code-and-integrates-the-lightning-network/), [Crypto Briefing](https://cryptobriefing.com/decred-launches-lightning-support-voting-and-mixing/) (sindicado a 6 medios de comunicación, incluido [Techtelegraph](https://www.techtelegraph.co.uk/decred-launches-lightning-support-voting-and-mixing/)) e [Invezz](https://invezz.com/news/2021/01/28/decred-dcr-update-brought-ln-support-voting-and-a-new-privacy-system/) (sindicado a 4 medios de comunicación, incluido [CCNC](https://www.cryptocurrencynewscast.online/2021/01/decred-dcr-update-brought-ln-support.html)).
- Un artículo en [Modern Consensus](https://modernconsensus.com/commentary/opinion/gamestop-is-defis-golden-moment/) con comentarios de @jy-p sobre el incidente de GameStop / Robinhood.

## Eventos
- 22 de enero - [Gate.io AMA](https://decredcommunity.github.io/events/index/20210122.1) - Internet. @elian respondió preguntas sobre Decred de la comunidad española Gate.io en su canal de [Telegram](https://t.me/Gateio_Espanol). Alrededor de 25 personas participaron en las preguntas y respuestas y tuvieron la oportunidad de ganar $10 en DCR (total $ 50).

## Media

@kyleFirethought y EETER convirtieron a Decred en el [principal colaborador](https://twitter.com/firethought/status/1346855997281882112) de LottieFiles por subir [203 animaciones](https://lottiefiles.com/decred) en 2020. [Lottie](https://lottiefiles.com/what-is-lottie) es un sistema de animación utilizado por los diseñadores de Decred.

Artículos seleccionados:

- Análisis de Decred blockchain - Parte 2 PoW wow por @richardred ([blockcommons.red](https://blockcommons.red/post/dcr-on-chain-2/))
- Revisión de Crypto Commons 2020 y registro de cambios v1.0 por @richardred ([blockcommons.red](https://blockcommons.red/post/ppcc-changelog-2020/))

El libro [cryptocommons.cc](https://cryptocommons.cc/) recibió una actualización importante que cubre desarrollos seleccionados de 2020, y estos también se escribieron como una publicación de blog independiente en el estilo de una revisión anual. La idea es que las personas que ya leyeron Peer Production en Crypto Commons puedan obtener la actualización sin volver a leerlo todo. Si bien la publicación completa tiene 18 000 palabras, también hay una versión en [hilo de tweets](https://twitter.com/RichardRed0x/status/1346160647923511297) que es mucho más corta. Los lectores habituales de la sección de Noticias Relevantes reconocerán muchas de las mismas historias. Uno de los temas principales de la actualización es la divergencia del "movimiento de código abierto", con la desilusión aparentemente creciendo entre las personas que trabajan en proyectos dominados por más corporaciones. Esto contrasta con el espacio criptográfico donde la cantidad de proyectos de código abierto y los mecanismos de financiación para estos están creciendo en escala y diversidad. Si bien el mercado bajista fue difícil para muchos proyectos y sus esfuerzos se redujeron, otros pudieron continuar sin preocuparse, y todavía hay un flujo constante de nuevas iniciativas de financiamiento que se están probando.

videos:

- Actualización de Decred News, 24 de enero de 2021–1.6 inminente, Decred Eco, máximos métricos, propuestas, ¡nuevo contenido! por @Salirus ([youtube](https://www.youtube.com/watch?v=hRvGHhGx-Fg))
- Podcast Staked - Entrevista con Crypto N Culture, también conocido como Your Bitcoin Baby Daddy ([youtube](https://www.youtube.com/watch?v=TzHhXWMhAow))
- Podcast Staked - Entrevista con Emaad Pervez ([youtube](https://www.youtube.com/watch?v=YJ7Pyo4W2rs)) - este utilizó un enfoque más profesional y ayudó a [convencer](https://proposals.decred.org/proposals/391108e/comments/19) un comentarista de propuestas.
- Análisis de monedas - Luz al final del túnel; ¡Hidra escondida! por DubDigital ([youtube](https://www.youtube.com/watch?v=E9VdHxpIr_I))
- Decred DEX: ¿un mejor diseño DEX? con Jake Yocom-Piatt y Nick Gregory para Coinscrum ([youtube](https://www.youtube.com/watch?v=uqhaz55dFRQ)), la versión un poco más corta se volvió a [cargar](https://www.youtube.com/watch?v=dTjw-Ff-CgI) en febrero)
- Tutorial de gobierno de Decred feat. Jaque mate analista en cadena ([youtube](https://www.youtube.com/watch?v=1QiC0btcf7E]))

Arte y diversión:
- [El tweet](https://twitter.com/decredproject/status/1353736208065638401) de lanzamiento v1.6 vino con una nueva animación de calidad.
- Se hizo otra animación de lanzamiento con [menos bits](https://twitter.com/decredproject/status/1353780294013353986) para la audiencia mayor.
- ¿[Qué haces por Decred DAO](https://twitter.com/exitusdcr/status/1348385341338742784)?

Traducciones:

- [Iterando la privacidad](https://blog.decred.org/2019/08/28/Iterating-Privacy/) - [en español](https://medium.com/decred-es/privacidad-iterativa-d4ecef46a9e9) por @francov_
- [La estructura Decred](https://stakey.club/en/the-decred-structure/) - [en español](https://medium.com/decred-es/la-estructura-de-decred-ad6e56794815) por @francov_
- Decred Journal de diciembre de 2020 se [tradujo](https://xaur.github.io/decred-news/) al árabe (@arij, @ abdulrahman4), chino (@Dominic) y español (@francov_). ¡Gracias a todos por su perseverancia!

Otro contenido que no está en inglés:

- La versión v1.6 se cubrió en Cointelegraph en [español](https://es.cointelegraph.com/news/decred-launches-version-16-with-focus-on-sovereignty-privacy-and-lightning-network).

## Discusiones de la comunidad 

Noticias de sistemas de comunicación:
- La aplicación Element (cliente de Android para el protocolo de chat Matrix utilizado por la comunidad Decred) se [eliminó temporalmente](https://twitter.com/element_hq/status/1355290296947499013) de Google Play Store. La versión [F-Droid](https://f-droid.org/en/packages/im.vector.app/) es menos vulnerable a este tipo de incidentes.
- Los usuarios de Signal pueden demostrar su [amor](https://twitter.com/decredproject/status/1348382377127665665) por Stakey instalando un [paquete de stickers](https://signal.art/addstickers/#pack_id=ba8c921e5bf3d132e77ddf53419ea3c1&pack_key=a0e0deb45d65777d21dd8e98af09b946241073210fba562e55f574f14b790838) especial.

Post seleccionados en Reddit:
- Decred fue mencionado en un informe sobre monedas estables emitidas por el banco central publicado por una gran corporación de cartera [MetLife](https://www.reddit.com/r/decred/comments/kxssw5/m%C3%A1rcio_siqueira_on_twitter_a_651_billion/)
- Cómo se [comparan](https://www.reddit.com/r/decred/comments/l61ggx/dash_treasury_a_glimpse_at_greatness_or_a/) los gastos de marketing de Dash con los de Decred.
- "Si pudieras cambiar [una cosa](https://www.reddit.com/r/decred/comments/kx201g/if_you_could_change_one_thing_in_how_decred_was/) en la forma en que se hizo Decred, ¿cuál sería?"
- Cómo podría ser el [futuro](https://www.reddit.com/r/decred/comments/kpzieu/any_good_threadslinks_on_what_the_future_of/) de Politeia
- Qué [lenguajes](https://www.reddit.com/r/decred/comments/kogozc/what_programming_languages_to_learn_to_work_for/) de programación se utilizan en Decred
- [De nuevo](https://github.com/decredcommunity/wiki/blob/master/wiki/misconceptions.md#coin-holders-cannot-make-good-decisions) "¿no es peligroso que alguien pueda votar sobre cambios de código?" [esta pregunta](https://www.reddit.com/r/decred/comments/ktei89/isnt_it_kinda_dangerous_that_anyone_can_vote_on/) reunió muchas respuestas completas
- Han surgido algunos otros temas recurrentes: convertir Decred en [DeFi](https://www.reddit.com/r/decred/comments/kqqwje/dcrdex_is_impressive/), nombrar [unidades](https://www.reddit.com/r/decred/comments/kq0uh2/names_of_the_units_of_decred/) sub-DCR, y la idea favorita de todos de [cambiar el nombre](https://www.reddit.com/r/decred/comments/kpjte8/change_decred_name_to_another_without_any/) de Decred a algo menos negativo se convirtió inevitablemente en el hilo más comentado del mes.

Discusiones seleccionadas en Twitter:
- @geostone [señaló](https://twitter.com/KingSolomonMine/status/1347581022850846727) que Decred no pertenece a ningún "token de características" pero tiene muchas de sus características.
- @ammarooni [señala](https://twitter.com/Ammarooni/status/1354961779256864779) que los [últimos pensamientos](https://www.bridgewater.com/research-and-insights/ray-dalio-what-i-think-of-bitcoin) de Ray Dalio reconocen la falta de adaptabilidad de Bitcoin.

La gente que ama DCR, realmente lo ama :) DCRDEX un gran catalizador fundamental y de estructura de mercado, después de un venta (oso) brutal. La capa de privacidad DCR es ahora uno de los lugares más soberanos para intercambiar monedas.

Ahora la gente simplemente apila tickets y apila satélites a través de DCR. ([@cburniske](https://twitter.com/cburniske/status/1355406801731108866))

## Mercados

En enero, DCR cotizaba entre 39.80 y 69,00 USD / 0.0013-0.0020 BTC. El promedio de tarifa diaria fue de $54.25.

Un gráfico [colorido](https://twitter.com/_Checkmatey_/status/1347662655830441984) de @Checkmate mostró cómo DCR no ha seguido a 5 monedas más grandes en su declive frente a BTC e incluso ha logrado algunas ganancias.

La actualización decred en el [issue 56](https://ournetwork.substack.com/p/our-network-issue-56) del boletín Our Network por @Checkmate y @PermabullNino [destaca](https://twitter.com/_Checkmatey_/status/1355296688026447873) la entrada más alta de DCR en los tickets que respaldaron la duplicación del precio de DCR / BTC. El indicador del precio al que se aplicó DCR muestra que solo el 17% de todas las apuestas se realizaron por encima de $40, lo que sugiere que los apostantes tienen una ganancia razonable en términos de USD. El nivel de equilibrio de DCR / BTC para los participantes se estima en alrededor de 0.004 BTC, por encima del cual ~ 60% de todos los participantes obtendrán ganancias.

[checkonchain.com](https://checkonchain.com/dcronchain/unrealisedpnl_oscillator_usd/unrealisedpnl_oscillator_usd_light.html) [agregó](https://twitter.com/_Checkmatey_/status/1347035560687202307) un oscilador de Pérdidas y Ganancias No Realizadas que mide la diferencia entre el precio al contado y el precio realizado como una medida de "sentimiento" sobre cuántas ganancias hay en el sistema. @PermabullNino se [unió](https://twitter.com/PermabullNino/status/1351571649548599297) para mejorar el sitio y publicó un recorrido rápido de algunos gráficos interesantes. Por ejemplo, USD Lifetime Ticket Price ha actuado como una línea histórica alcista / bajista que se eliminó en enero.

[DCRDEX](https://dex.decred.org/) ha negociado un total de 1 300 000 DCR y 1 900 BTC durante casi 4 meses desde su lanzamiento. En promedio, eso es aproximadamente 12 000 DCR / 17 BTC por 24 horas.

## Noticias Relevantes

Bitcoin Core [0.21.0](https://bitcoincore.org/en/releases/0.21.0/) se ha lanzado con grandes aspectos destacados, incluidas las reglas de consenso de [Taproot](https://bitcoinmagazine.com/articles/taproot-coming-what-it-and-how-it-will-benefit-bitcoin) (permite contratos inteligentes más flexibles y una mejor privacidad) implementadas como una bifurcación suave y soporte para servir filtros compactos BIP157. Este último se [propuso](https://github.com/bitcoin/bips/blob/master/bip-0157.mediawiki) en mayo de 2017 y ofreció una gran mejora en la seguridad y privacidad de las billeteras ligeras, en comparación con las populares Electrum y las billeteras que se basan en servidores centrales para obtener datos sin validar la blockchain completa. En diciembre de 2018, el riesgo del middleware Electrum se materializó y los hackers informáticos [robaron](https://blog.malwarebytes.com/cybercrime/2019/04/electrum-bitcoin-wallets-under-siege/) alrededor de $4 millones en BTC. Un problema menos obvio es la recopilación de direcciones privadas y datos de transacciones por ~90 [servidores](https://1209k.com/bitcoin-eye/ele.php?chain=btc) Electrum que continúa hasta el día de hoy.

Las billeteras ligeras basadas en filtros compactos se comunican con nodos completos sin intermediarios y [no tienen](https://docs.decred.org/wallets/spv/#how-is-this-different-from-a-light-wallet) estos riesgos. Decred agregó su soporte inicial en [septiembre del 2018](https://github.com/decred/decred-binaries/releases/tag/v1.3.0) y estuvo expuesto a todos los usuarios en [febrero del 2019](https://github.com/decred/decred-binaries/releases/tag/v1.4.0). La segunda generación de esta tecnología se agregó en [mayo del 2020](https://docs.decred.org/governance/consensus-rule-voting/consensus-vote-archive/#v7) a nivel de consenso y se integró en las billeteras en [enero del 2021](https://github.com/decred/decred-binaries/releases/tag/v1.6.0#dcrwallet-v160).

La minera estadounidense Marathon Patent Group se unió a DMG Blockchain Solutions para [crear](https://www.marathonpg.com/news/press-releases/detail/1220/marathon-patent-group-and-dmg-blockchain-solutions-to-form) un "grupo de minería cooperativa". Para beneficiar a la industria, el grupo incluirá tecnología patentada de "minería de bloques limpios" que "omitirá específicamente cualquier transacción que Walletscore considere riesgosa y que no cumpla con los estándares de la OFAC". r / Bitcoin [discutió](https://www.reddit.com/r/Bitcoin/comments/kqyg0l/a_2nd_american_miner_marathon_patent_group_is/) posibles contramedidas y afirmaciones hechas por las empresas.

Firo (anteriormente Zcoin) sufrió un [ataque](https://twitter.com/firoorg/status/1351703001849757697) del 51% en el que el atacante depositó 866 000 FIRO en Binance, los vendió por otras monedas que retiraron y luego transmitió aproximadamente 1 día de bloques que borraron los depósitos del atacante. Los desarrolladores de Firo respondieron activando un interruptor "Lelantus" que impedía que el atacante anonimizara su FIRO (que fue útilmente almacenado en una dirección), y lanzaron una actualización que incluyó la dirección del atacante en la lista negra y agregó una nueva regla que limita la profundidad máxima de reorganización a 5 Mientras que la red actualizaba al atacante y los mineros honestos involucrados en una [guerra de hash](https://www.coindesk.com/privacy-coin-firo-currently-experiencing-51-attack), el atacante trataba de extraer suficientes bloques para mantenerse a la vanguardia para poder gastar sus ganancias mal habidas.

BitMEX Research causó revuelo cuando [tuitearon](https://twitter.com/BitMEXResearch/status/1351855414103715842) que Bitcoin había experimentado un pequeño gasto doble. [Hasu](https://insights.deribit.com/market-research/was-there-a-bitcoin-double-spend-on-jan-20-2021/) y otros aclararon amablemente que este no era un ataque malicioso de doble gasto, sino un evento benigno en el que un usuario estaba aumentando la tarifa de su transacción cuando se producía un bloqueo obsoleto y la transacción original se eliminó de la cadena de bloques.

Yearn Finance [votó](https://snapshot.page/#/yearn/proposal/QmX8oYTSkaXSARYZn7RuQzUufW9bVVQtwJ3zxurWrquS9a) a favor de [inflar](https://www.coindesk.com/yearn-finance-votes-to-inflate-yfi-token-supply-by-20) la oferta de YFI en un 20% para financiar el desarrollo futuro. YFI ha sido elogiado por su "lanzamiento justo" que puso todos los tokens en manos de los mineros de liquidez, pero ahora han votado para dedicar el 20% al desarrollo algunos meses después. Como parte del período previo a la votación, el desarrollador líder de Yearn Finance, Andre Cronje, [escribió](https://andrecronje.medium.com/building-in-defi-sucks-part-2-75df9ee7871b) sobre cómo la construcción en DeFi apesta.

Tether ha [impreso](https://www.coindesk.com/tether-mints-record-2b-usdt-in-one-week) un número récord de USDT. El suministro total de monedas estables está [explotando](https://twitter.com/PermabullNino/status/1354545678437912579) y los patrones de emisión se [correlacionan](https://twitter.com/PermabullNino/status/1352278182288793607) con los precios de las criptomonedas.

Reddit subreddit r / wallstreetbets irrumpió en la [corriente principal](https://www.bloomberg.com/news/articles/2021-02-01/gamestop-short-interest-plummets-in-a-sign-traders-are-covering) con un pequeño apretón de manos minoristas que atrajo la cobertura de la prensa mundial y costó a los fondos de cobertura que fueron capturados $20 mil millones, antes de que Robinhood y las otras plataformas que lo habían habilitado [tiraran de la alfombra](https://www.cnbc.com/2021/01/28/robinhood-interactive-brokers-restrict-trading-in-gamestop-s.html) al evitar que los usuarios abrienan nuevos puestos.

A Elon Musk se le [atribuyó](https://www.coindesk.com/bitcoin-price-falls-retraces-elon-musk-twitter) el aumento del precio de BTC después de que tuiteó el apoyo a Bitcoin, y luego [repitió](https://twitter.com/elonmusk/status/1357231313376456708) el mismo truco con Dogecoin, presumiblemente para su propia diversión.

El servicio de microblogging Parler ha probado un nuevo nivel de censura en enero. La eliminación de aplicaciones de las tiendas de Google y Apple no fue nada nuevo, pero una rápida eliminación por parte de 2FA, proveedores de identidad, bases de datos y, en última instancia, Amazon Web Services, mostró prácticamente todo lo que puede salir mal cuando las soluciones centralizadas se utilizan ingenuamente para construir un entorno menos censurado. Con suerte, los desarrolladores y operadores de nodos aprenderán de esto y se prepararán para tales eventos con anticipación.

Google [suspendió](https://twitter.com/element_hq/status/1355290296947499013) la aplicación Element sin previo aviso. Tras una solicitud de aclaración, su representante [explicó](https://twitter.com/element_hq/status/1355663753380032512) que “la suspensión fue provocada por un informe de contenido extremadamente abusivo accesible en el servidor de matrix.org”. Como es habitual en tales casos, no se hizo referencia a la instancia exacta del contenido para que el público verificara que la huelga fue justa. La aplicación se restauró aproximadamente 1 hora después. Una interpretación más positiva es que este fue un recordatorio suave para reducir la dependencia del efímero Google Play y cambiar a [F-Droid](https://f-droid.org/en/packages/im.vector.app/) o [APK autohospedados](https://twitter.com/element_hq/status/1355331704781742082).

Buenas noticias para los combatientes de la censura, el repositorio de [youtube-dl](https://github.com/ytdl-org/youtube-dl9) que se eliminó a través de la solicitud de la RIAA, se restauró después de un [retroceso](https://torrentfreak.com/riaas-youtube-dl-takedown-ticks-of-developers-and-githubs-ceo-201027/) impresionante que involucraba formas creativas de compartir código censurado.

## Sobre esta edición

Este es la edición #34 de la Revista Decred, un índice de todos los números originales y traducciones se encuentran disponibles [aquí](https://xaur.github.io/decred-news/).

> La mayoría de la información de terceros se transmite directamente desde la fuente después de un control de fiabilidad mínimo. Los autores de la Revista Decred no tienen la capacidad de verificar todas las reclamaciones. Tenga cuidado con las estafas y haga su propia investigación.

Puedes enviar una historia [aquí](https://github.com/xaur/decred-news/labels/next%20release) para ser considerada para el próximo número. Los [comentarios](https://github.com/xaur/decred-news/blob/docs/contributing.md#feedback) y las [contribuciones](https://github.com/xaur/decred-news/blob/docs/contributing.md) siempre son bienvenidas.

Créditos:

- Redacción y edición: bee, degeri, jholdstock, l1ndseymm, richardred.
- Revisión y comentarios: davecgh, dnldd, elian, Exitus, oshorefueled.
- Imagen de portada: saender.
- Fondeado por: la tesorería de Decred.

ACTUALIZACIÓN 2021–02–11 para corregir cómo funciona DCRDEX y utilizar el término StakeShuffle en lugar de CoinShuffle++ (este último es solo una parte del sistema). Puede encontrar los cambios exactos [aquí](https://github.com/xaur/decred-news/commits/master).
