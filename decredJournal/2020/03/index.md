# Revista Decred – Marzo 2020

![Imagen abstracta](./assets/202003.png)

_Imagen: Expand Vector por @saender_

Lo mas destacado de Marzo:

- El cambio DCP-0005 está activado, lo que se puede decir es que es la implementación SPV más segura y que preserva la privacidad para clientes ligeros en la red Decred. Todos los nodos v1.4 que aún se estaban ejecutando se han bifurcado la red.
- El primer intercambio del Atomic Swap fue coordinado por el DEX en el testnet.
- Hubo un progreso espectacular en casi todos los repositorios de software.
- Se aprobaron presupuestos anuales para el alcance de EE. UU. y Brasil por un total de $286K, incluido algunos fondos para continuar la producción de la revista.
- ¡Este es el número 24 de la Revista Decred y marca dos años de la cobertura mensual ininterrumpida del proyecto Decred!

## Desarrollo

A menos que se indique lo contrario, el trabajo que se informa aquí tiene el estado de "fusionado". Significa que el trabajo se completó, revisó y se integró en el código fuente en el que los usuarios avanzados pueden construir y ejecutar, pero aún no está disponible en los binarios del lanzamiento para usuarios normales.

[dcrd](https://github.com/decred/dcrd):

- las firmas ECDSA se [desacoplaron](https://github.com/decred/dcrd/pull/2139) del paquete secp256k1 para dejar en claro que el ECDSA es solo un algoritmo de firma digital, y para permitir que las firmas Schnorr se conviertan en habitantes de primera clase de la base de código.
- el tipo de [valor de campo](https://github.com/decred/dcrd/pull/2134) se exportó para permitir que los llamadores externos realicen cálculos matemáticos de campo optimizados.
- la verificación de firma fue optimizada al minimizar operaciones costosas.
- se agregó un método para [borrar](https://github.com/decred/dcrd/pull/2117) la clave privada de la memoria y se [redujo](https://github.com/decred/dcrd/pull/2131) el número de copias internas de las claves privadas para mejorar la seguridad contra el raspado de memoria.
- los grandes enteros se [eliminaron](https://github.com/decred/dcrd/pull/2107) por completo de las operaciones de firma, análisis y firma a favor del código y poder escalar de modo especializado.
- las pruebas de verificación de Schnorr fueron [reelaboradas](https://github.com/decred/dcrd/pull/2128) para resolver múltiples problemas.
- se evitó el mal uso de código no utilizado eliminando código en varias áreas.

Se [reveló](https://bounty.decred.org/2020/03/status-update/) una vulnerabilidad que permitía un posible ataque de agotamiento de memoria de varios días que podría provocar un bloqueo de nodos en dcrd v1.4.0. El 13 de marzo, la red se bifurcó a las nuevas reglas de consenso implementadas en dcrd v1.5.0, lo que significa que todos los nodos de la red deben ejecutarla como una versión mínima. Como esta y las versiones posteriores contienen una solución para la vulnerabilidad, ahora está mitigada.

dcrd tiene menos del 16% de superposición de código con btcd, lo que significa que 84% es el nuevo trabajo de desarrollo, según un [análisis](https://coincode.sh/c/dcr/) de CoinCode.sh. @davecgh [confirmó](https://matrix.to/#/!HEeJkbPRpAqgAwhXWO:decred.org/$15862843869377LGlSK:decred.org) que los números parecen plausibles dada la cantidad de código nuevo que se ha escrito y señaló que la divergencia es aún más pronunciada en dcrwallet (que no se analizó).

[dcrwallet](https://github.com/decred/dcrwallet):

- se [implementó](https://github.com/decred/dcrwallet/pull/1706) el comando `fundrawtransaction` que agrega entradas sin firmar y cambia la salida a una transacción sin procesar.
- las operaciones de la cartera se [cambiaron](https://github.com/decred/dcrwallet/pull/1648) para usar filtros comprometidos de la versión 2 (los filtros v1 están en desuso pero la red todavía los sirve y dcrwallet los usa, la próxima versión usará filtros v2).
- el comando `getaddressesbyaccount` fue [corregido](https://github.com/decred/dcrwallet/pull/1695) para devolver también direcciones importadas para la cuenta `imported`
- los scripts de canje P2SH no encriptados se [movieron](https://github.com/decred/dcrwallet/pull/1688) al almacenamiento del administrador de direcciones (esto simplifica el almacenamiento y elimina el requisito de desbloquear la cartera para ver o almacenar los scripts).
- mejoras internas a la eficiencia y la semántica.
- limpieza para eliminar el código obsoleto y no utilizado.

[Decrediton](https://github.com/decred/decrediton):

- se agregó soporte para el [staking en frío](https://github.com/decred/decrediton/pull/2424) (también se requiere para carteras de hardware)
- se agregó soporte para la [importación de scripts](https://github.com/decred/decrediton/pull/2423) en carteras de vista únicamente
- se puede recuperar [agendas](https://github.com/decred/decrediton/pull/2442) desde dcrdata
- ahora se puede checar las [nuevas propuestas](https://github.com/decred/decrediton/pull/2420) en la tabla de Gobernanza
- vista responsive en las [vistas de propuestas](https://github.com/decred/decrediton/pull/2444), [direcciones](https://github.com/decred/decrediton/pull/2416), vista general, transacciones, y otros ajustes de  las interfaz de usuario

En desarrollo:

- soporte para [CoinShuffle++](https://github.com/decred/decrediton/pull/2452)

[Politeia](https://github.com/decred/politeia):

- se [invalidaron](https://github.com/decred/politeia/pull/1159) los cambios de sesión o de contraseñas
- se hicieron pruebas y se resolvieron algunos errores

La integración de tlog ha comenzado y se [prevé](https://github.com/decred/politeia/issues/1112#issuecomment-606147106) que tarde 2 meses. En [julio de 2019](https://github.com/xaur/decred-news/blob/master/journal/201907.md#development), informamos incorrectamente el inicio de la integración de tlog, pero ese trabajo fue en realidad una implementación de referencia para servir como prueba de concepto y demostrar que el almacén de datos [Trillian](https://github.com/google/trillian) de Google puede reemplazar el backend Git existente. Se [fusionó](https://github.com/decred/politeia/pull/951) en agosto y contenía un [cliente / servidor](https://github.com/decred/politeia/tree/master/tlog) con funcionalidad básica para almacenar documentos. Esta experiencia dio suficiente información para saber que funcionará. El siguiente paso es escribir un backend de Politeia que use Trillian.

La principal ventaja del backend de tlog es que hará que Politeia sea más escalable y permitirá censurar el contenido después de que se haga público, al tiempo que se mantiene el seguimiento de auditoría de todos los datos enviados. También permitirá una corrección adecuada del error de comentarios duplicados.

CMS:

- se añadío la capacidad de asignar [la propiedad](https://github.com/decred/politeia/pull/1135) de la propuesta, que se utilizará en los próximos cambios para permitir que los propietarios de la propuesta vean lo que se factura contra su propuesta
- se añadío la capacidad de [desactivar](https://github.com/decred/politeia/pull/1154) la cuenta de un contratista temporal en la factura pagada y requerir la aprobación del administrador para permitir otra factura
- El trabajo de rediseño iniciado en octubre finalmente se [fusionó](https://github.com/decred/politeiagui/pull/1828). Este gran cambio agrega 9K y elimina 24K líneas de código.

Detrás de las actualizaciones visuales, el rediseño del CMS concluye el [proceso](https://matrix.to/#/!VFRvyndKpzcLrVslQD:decred.org/$158644942810878cUwaw:decred.org) de migración del código politeiagui de la biblioteca [snew-classic-ui](https://github.com/decred/snew-classic-ui) a [pi-ui](https://github.com/decred/pi-ui). 

En 2018, se permitió que Politeia saliera rápidamente con la apariencia y estilo de Reddit, pero rápidamente se volvió difícil de desarrollar. Construir el pi-ui y cambiarlo mejoró la modularización del código y le dio flexibilidad para componer y diseñar los componentes de la interfaz de usuario de la manera en que se requería que coincidiera con las especificaciones de diseño, así como con las ganancias de rendimiento.

[dcrstakepool](https://github.com/decred/dcrstakepool):

- mantenimiento de código para mejorar el manejo y la cancelación de errores, documentación adicional, dependencias mejoradas y pruebas adicionales

[dcrpool](https://github.com/decred/dcrpool):

- soporte para [Obelisk DCR1](https://github.com/decred/dcrpool/issues/110)
- la base de datos del pool se [respalda](https://github.com/decred/dcrpool/pull/164) antes del apagado
- se agregó una [paginación](https://github.com/decred/dcrpool/pull/163) para los bloques minados
- el código de conexión fué [refactorizado](https://github.com/decred/dcrpool/pull/171) para simplificar las pruebas
- se agregó una mayor cobertura de prueba
- se hicieron pequeñas mejoras en el UX, configuración y algunas correcciones de errores
- el trabajo es una preparación para una próxima versión 1.1.0

[dcrlnd](https://github.com/decred/dcrlnd):

- construcciones de [mejoras](https://github.com/decred/dcrlnd/pull/84) en el sistema

En desarrollo:

- se añadió un nuevo paquete de [escaneo de cadenas](https://github.com/decred/dcrlnd/pull/83) que utiliza filtros comprometidos para detectar transacciones relevantes para el nodo del LN de manera más eficiente y que también puede operar en modo SPV
- se añadieron [implementaciones](https://github.com/decred/dcrlnd/pull/92) para el paquete chainntnfs que usan dcrwallet integrado y remoto como fuente de eventos en cadena. Esto permite desacoplar aún más dcrlnd de un dcrd subyacente, que es un requisito para tener una instancia de dcrlnd ejecutándose en el modo SPV.
- basándose en lo anterior, habilite y pruebe el [modo SPV](https://github.com/decred/dcrlnd/pull/95) para carteras remotas ("cartera remota" es el modo de conexión donde dcrlnd se conecta a una instancia de dcrwallet que ya se está ejecutando, es decir, no necesita su propia cartera integrada con una semilla separada)

> El modo SPV es un requisito para las carteras móviles LN. Es probable que SPV sea el modo de sincronización dominante incluso en las carteras de escritorio, por lo que es esencial que dcrlnd admita el modo SPV. También es el último elemento de la sección de "trabajo inmediato" de mi tipo de "hoja de ruta" que describí en el [post](https://matheusd.com/post/announcing-dcrlnd/) de anuncio de LN, por lo que esto concluye la mayor parte del esfuerzo de transferencia de lnd a dcrlnd. Concluir el SPV significa que podemos comenzar a explorar cambios más exóticos que están disponibles en Decred (como los [PTLC](https://suredbits.com/payment-points-monotone-access-structures/) que dependen del trabajo de Schnorr que @davecgh también está concluyendo). ([@matheusd](https://matrix.to/#/!HEeJkbPRpAqgAwhXWO:decred.org/$1586258547807544APZNe:matrix.org))

[dcrdex](https://github.com/decred/dcrdex):

- se agregó una aplicación de [control](https://github.com/decred/dcrdex/pull/181) de línea de comandos para el cliente DEX
- se añadió la capacidad de [colocar órdenes](https://github.com/decred/dcrdex/pull/195) a través de la GUI del cliente en el navegador
- se agregó una [copia de seguridad](https://github.com/decred/dcrdex/pull/210) y restauración de claves de cliente y otros datos de la cuenta (una copia de seguridad anterior [#183](https://github.com/decred/dcrdex/pull/183) agregada de los datos del pedido del cliente)
- seguimiento del cliente de las [órdenes por época](https://github.com/decred/dcrdex/pull/188) y [verificación de la combinación y arrastramiento](https://github.com/decred/dcrdex/pull/189) de órdenes realizada al final de cada época
- se agregó un [cálculo del índice](https://github.com/decred/dcrdex/pull/206) que permite al servidor rastrear de manera confiable las órdenes completadas y canceladas del usuario, con la capacidad de reconstruir el historial de órdenes recientes de cualquier usuario de la base de datos. Esta es una parte importante de la aplicación de la conducta comunitaria.
- se realizaron refactorizaciones y limpieza en las bases de código

Un hito importante es la finalización de la [negociación de coincidencias](https://github.com/decred/dcrdex/pull/213). Esta es la última gran pieza del cliente que finalmente le permite ejecutar un intercambio. El RP específicamente hace que el cliente pase por todo el proceso de intercambio (negociación de coincidencias), se comunica con el servidor, realiza la auditoría necesaria de las transacciones de contraparte, crea y difunde el propio contrato del cliente y canjea las transacciones según lo requiera el proceso de intercambio.

Un total de 19 solicitudes de PR se fusionaron de 6 colaboradores que agregaron 11K y eliminaron 3K líneas de código (el resumen de confirmación está [aquí](https://github.com/decred/dcrdex/compare/94310f66c06fdf5ca31eeb80c9f6af7aecf4c31d...d3bd07f822200041092bdc85f5c1b752b3c9ee24)).

¡Felicitaciones al equipo de dcrdex por [coordinar](https://twitter.com/chappjc/status/1245075450625511425) el primer intercambio atómico impulsado en la red testnet!

[dcrandroid](https://github.com/decred/dcrandroid):

- se agregó una página de [estadísticas](https://github.com/decred/dcrandroid/pull/440)
- ajustes en la UI y correciones

La próxima versión del Testnet está disponible [aquí](https://play.google.com/apps/testing/com.decred.dcrandroid.testnet).

[dcrios](https://github.com/raedahgroup/dcrios):

- fué renovada la página de [Send](https://github.com/raedahgroup/dcrios/pull/557)
- nueva UI para el menú [More](https://github.com/raedahgroup/dcrios/pull/559)
- un nuevo widget selector fué añadido en la [Cartera](https://github.com/raedahgroup/dcrios/pull/600) para la página de transacciones
- se agregó la propiedad de leer los montos de DCR en los [códigos QR](https://github.com/raedahgroup/dcrios/pull/581)
- múltiples correcciones de errores y ajustes en la UI

La próxima versión del Testnet está disponible [aquí](https://testflight.apple.com/join/7KL4VnB2).

[dcrdata](https://github.com/decred/dcrdata):


- se agregó una URL comúnmente solicitada para los datos de gráficos [JSON sin procesar](https://github.com/decred/dcrdata/pull/1716) a las páginas de gráficos
- se realizaron pequeños ajustes y correcciones de errores

[tinydecred](https://github.com/decred/tinydecred):

- se agregó la [vista de staking](https://github.com/decred/tinydecred/pull/53) 
- la vista de staking muestra tickets gastados, no gastados y en vivo
- se añadió una vista simple del [resumen de la cuenta](https://github.com/decred/tinydecred/pull/94)
- se añadió una [vista](https://github.com/decred/tinydecred/pull/125) al crear una cuenta y enviar DCR
- [descubrimiento de cuenta](https://github.com/decred/tinydecred/pull/124)
- sea agregó un cambio en las pruebas al usar las bases de datos [dentro de la memoria](https://github.com/decred/tinydecred/pull/116)
- se aumentó la cobertura de prueba general al [98%](https://github.com/decred/tinydecred/issues/70#issuecomment-606669036) y se solucionó algunos errores descubiertos en el proceso, todos los archivos ahora tienen al menos un 94% de cobertura

Con un total de 56 PR fusionados de 3 contribuidores añadiendo 11K y borrando 6K líneas de código (El resúmen de los commits están [aquí](https://github.com/decred/tinydecred/compare/fa081e7f17d303f0eea31e9f07499db4e0acc53a...e1ef1ff72cb924d27098f9df151f6805d5db3e90)).

[docs](https://github.com/decred/dcrdocs):

- los documentos de [dcrlnd](https://docs.decred.org/lightning-network/overview/) fuerón [actualizados](https://github.com/decred/dcrdocs/pull/1083) para la última versión 0.2.1, y los comandos fueron agrupados en categorías
- la [guía](https://docs.decred.org/getting-started/joining-matrix-channels/) sobre como ingresar a Matrix [fué añadida](https://github.com/decred/dcrdocs/pull/1081)
- se ha cambiado el [nombre](https://github.com/decred/dcrdocs/issues/1074) de la página de inflación a [Emisión](https://docs.decred.org/advanced/issuance/) para eliminar la ambigüedad.
- se agregó a la [documentación](https://github.com/decred/dcrdocs/pull/1073) como acceder al servidor CoinShuffle++ como un servicio oculto de [Tor](https://docs.decred.org/privacy/cspp/how-to-cspp/#tor-hidden-service)

[decred.org](https://github.com/decred/dcrweb):

- se realizó una gran limpieza que soluciona problemas menores con el nuevo sitio web
- copia VSP [actualizada](https://github.com/decred/dcrweb/pull/853)
- la página de reclutamiento se eliminó y decred.org/recruiting ahora redirige a la página de [Contribución](https://docs.decred.org/contributing/overview/)
- la página de roadmap fué [removida](https://github.com/decred/dcrweb/pull/857)

Otros:

- la mayoría de los proyectos se actualizaron para compilar con Go v1.14 y dejaron de admitir Go v1.12
- @mm lanzó DigiSign Oracle, una aplicación web gratuita y de código abierto que ayuda a los usuarios finales a verificar las firmas digitales. Fue creado para ayudar a los usuarios de Decred a verificar las firmas de los paquetes sin tener que usar programas de línea de comandos complicados. Puede acceder a él en [stakey.club](https://stakey.club/digisign-oracle/) o descargar el [código fuente](https://github.com/mmartins000/digisign-oracle) a su computadora y abrirlo con un navegador web.

## Planes para v1.6

> El plan aproximado es que se publique v1.6 al final del segundo trimestre. Estamos planeando incluir: cambio de consenso descentralizado del Fondo de Tesorería, soporte CSPP de Staking y no Staking de Decrediton, soporte VSP basado en tickets y un sin fin de mejoras de dcrds. (@jy-p on [2020-03-20](https://matrix.to/#/!MgQoetFiyjrHAywokv:decred.org/$15855719584400kpyNr:decred.org))

## Comunidad

Bienvenido @unimere ([decrediton](https://github.com/decred/decrediton/commits?author=unimere)), felicidades por tu primer commit exitoso.

Estadísticas de la Comunidad:

- Seguidores de Twitter: 40,694 (-207)
- Suscriptores de Reddit: 9,760 (+22)
- Usuarios de Matrix: 601 (+36)
- Usuarios de Discord: 1,160 (+73), verified to post: 479 (+29)
- Usuarios de Telegram: 2,607 (-71)
- Suscriptores de Youtube: 3,980 (-10)
- Seguidores de Facebook: 3,606 (+26), likes: 3,273 (+24)
- Seguidores de LinkedIn: 744 (+25)
- Estrellas en el GitHub de dcrd: 536 (+1), forks: 1,507 (+11)

## Gobernanza

En Marzo el Fondo de [Tesorería](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx) recibió 13.713 DCR y gastó 17.153 DCR. Usando la tasa promedio diaria de DCR / USD de marzo de $ 13.40, esto es $ 184K recibidos y $ 230K gastados. A la tasa promedio diaria de febrero de $ 20.48, la cifra en USD facturada por el trabajo completado en ese mes es de $ 281K. A partir del 3 de abril, el saldo del Fondo de Tesorería es de 640K DCR (7.41 millones de dólares a $ 11.58).

En este mes se publicaron 4 nuevas propuestas.

La nueva [propuesta](https://proposals.decred.org/proposals/2f08f8518bc7672069a10ac6461fd9ab341d4a9e4c343fd4a7ec426250f3896f) del equipo de DCRComic solicitó un aumento del presupuesto de $ 16,200 para 12 cómics añadiendo actividades extra, con un adicional de $ 150 por cómic por el tiempo adicional dedicado a adaptar los activos para el uso de las redes sociales. La propuesta se puso en [suspensión](https://twitter.com/DCRComic/status/1243197581104041984) para reformular el elenco de personajes, después de algunas críticas de que Stakey estaba siendo usado en exceso para representar muchos roles diferentes en el ecosistema Decred. El 6 de abril, la propuesta fue editada para agregar nuevos [personajes](https://github.com/pLabarta/dcrwebcomic/blob/master/Proposal2/NewChars.md) que se unirán a la alineación junto a Stakey, el 9 de abril se abrió la votación. 

La [propuesta](https://proposals.decred.org/proposals/c830ea5afea45a0aabf4092d1bea51fb10b8bfa2d8474aac03224f0f94d3d1af) de Marketing de EE. UU. después de ser editada a $ 177,800 para eliminar la organización comunitaria de eventos a la luz de COVID-19, fue aprobada con un 74% de apoyo y una participación electoral del 31%.

La [propuesta](https://proposals.decred.org/proposals/bc20f986c3ea2fed2ea074c377a89f1a4b956ea0d527a8b6c099a5a8f175beb5) de Marketing Brasileño, que solicitó $ 108K para el resto del año también fue aprobada, con un 65% de soporte y participación. Esta propuesta fue editada para decir que los eventos no se organizarán ni se facturarán mientras persista la situación COVID-19, pero el elemento no se eliminó del presupuesto y parte de esta actividad puede tener lugar más adelante en el año.

Se presentaron dos propuestas más y están en plena discusión. Una [propuesta](https://proposals.decred.org/proposals/d3b16861a7e555db2fdd25b589123f4b6c4289c857fbdff329a4ffb1cb60c4d9) de PolisPay App busca $ 5,000 para soportar a DCR en su plataforma. 

También hay una [propuesta](https://proposals.decred.org/proposals/7d42c6f4bf3059b64789185af615c1df97cb61a379425933be5ff01d074ed4d5) para financiar la [cuenta](https://twitter.com/Decred_Daily) de Twitter Decred Daily durante 6 meses y un sitio web (presupuesto total de $5,280). La propuesta de Decred Daily se comenzó a votar el 9 de abril.

Poco antes de la publicación del 9 de abril, se publicó otra propuesta, solicitando $ 24,450 para la creación de una [Campaña de Marketing](https://proposals.decred.org/proposals/bce7bf3cd1f74d571d23ac8a330ddf29a14a547ed0cc9c995f1a97dce733d1e1).

La propuesta del creador de mercado i2 Trading está llegando al final de sus seis meses de actividad, esto comenzó a finales de octubre de 2019 y finalizará a fines de abril de 2020. Los registros de operaciones de i2 continúan siendo auditados mensualmente por Company 0 y se ha encontrado que el rendimiento es satisfactorio. i2 planea presentar una propuesta para continuar la creación de mercado para Decred, pero se reducirá para reflejar las condiciones actuales del mercado.

Para ver más detalles sobre la actividad de Politeia en el mes, vea la [Edición 29](https://blockcommons.red/politeia-digest/issue029/) de Politeia Digest.

## Red

Hashrate: El [Hashrate de Marzo](https://explorer.dcrdata.org/charts?chart=hashrate&zoom=k73pwcch-k8jayo3s&bin=block&axis=time) abrió a ~ 359 Ph/s y cerró ~ 309 Ph/s, tocó fondo a 274 Ph/s y alcanzó un máximo de 556 Ph / s durante todo el mes. Pool [distribución del hashrate](https://dcrstats.com/pow) a partir del 1 de abril: UUPool 55%, Poolin 18%, lab.antpool.com 17%, Luxor 2.5%, BTC.com 2.2%, F2Pool 1.5%, BeePool 0.13%, CoinMine 0.08%, Suprnova 0.02% y otros ~ 3.8 % Los números de distribución del Pool son aproximados y no se pueden determinar con precisión.

Staking: El precio del Ticket fue 141.9 DCR (+9.8) en el [promedio a 30 días](https://dcrstats.com/). La [cantidad bloqueada](https://explorer.dcrdata.org/charts?chart=ticket-pool-value&zoom=k73pwcch-k8jayo3s&bin=block&axis=time) fue de 5.50-5.75 millones de DCR, que correspondieron al 49.05-51.27% del suministro disponible [participando](https://explorer.dcrdata.org/charts?chart=stake-participation&zoom=k73pwcch-k8jayo3s&bin=block&axis=time) en PoS.

El precio del Ticket llegó a 166.82 DCR, que vuelve a ser un nuevo máximo desde el cambio del algoritmo de dificultad de apuesta.

Tamaño de bloque: este mes, el tamaño de blockchain creció en 129 MB. Los bloques tenían un [tamaño](https://explorer.dcrdata.org/charts?chart=block-size&zoom=k73pwcch-k8jayo3s&bin=block&axis=time) promedio de 14.5 KB. El bloque más pequeño tenía un tamaño de 1.62 KB y el más grande, 374.98 KB. Hasta ahora, la principal fuente de bloques casi completos en la Tesorería: este mes, los pagos crearon un rango de 9 bloques completos el [16 de marzo](https://explorer.dcrdata.org/blocks?height=432590&rows=20).

Transacciones: en marzo, los usuarios de Decred realizaron 49,078 transacciones regulares y compraron 44,149 Tickets. 43.791 Tickets fueron recompensados por votar y 728 fueron revocados. En promedio, hubo 1,583 transacciones regulares de DCR y 1,424 Tickets nuevos por día.

Nodos: a lo largo de [marzo](https://charts.dcr.farm/d/000000014/nodes?orgId=1&from=1583020800000&to=1585699200000) hubo un promedio de 146 nodos de escucha públicos y 246 nodos totales por dcr.farm. Distribución promedio de versiones para marzo: 28% dcrd v1.5.1, 20% dcrd v1.4, 15% dcrd v1.5, 8% dcrd v1.5 dev y RC builds, 5% dcrd v1.6 dev builds, 5% dcrwallet v1.5.1, 5% dcrwallet v1.4, 2% dcrwallet v1.5. El 13 de marzo se activaron las nuevas reglas de consenso y después de eso dcrd v1.4 ya no puede seguir en la cadena.

## Integraciones

Probit agregó [soporte](https://twitter.com/ProBit_Exchange/status/1235450770100649986) para los pares DCR/KRW y DCR/USDT a su exchange.

Exmo.com tuvo una [interrupción](https://twitter.com/Exmo_Com/status/1240255377507303431) repentina de DCR unos días después de la bifurcación del 13 de marzo, los servicios se [reanudaron](https://twitter.com/Exmo_Com/status/1240627750005870592) al día siguiente. Actualmente, Exmo es la única integración [financiada](https://proposals.decred.org/proposals/950e8149e594b01c010c1199233ab11e82c9da39174ba375d286dc72bb0a54d7) por las partes interesadas.

El procesador de pagos [NOWPayments](https://nowpayments.io/) que se lanzó en 2019 por ChangeNOW admite DCR entre más de [40 activos](https://nowpayments.io/supported-coins/).

ChainRift [anunció](https://twitter.com/ChainRift/status/1228010062163202049) en febrero que cerrarán las operaciones de intercambio y se dirigirán a una empresa de desarrollo de software.

DCR fue [agregado](https://twitter.com/Checkmatey/status/1244030247558729729) al contrato futuro del índice FTX PRIV-PERP que rastrea 9 monedas de privacidad. El cálculo del índice se puede encontrar [aquí](https://help.ftx.com/hc/en-us/articles/360027668812-Index-Calculation).

El usuario AGspearo no pudo acceder a sus [fondos](https://www.reddit.com/r/decred/comments/fim5j2/stakepool_failure_caused_me_to_lose_all_my/) debido a que el VSP d1pool.com se cerró sin previo aviso y no tuvo acceso a su script de canje. AGspearo dedicó mucho tiempo al soporte tratando de resolver este problema, pero finalmente no pudieron obtener sus fondos. @davecgh desglosó el problema como un [comentario](https://www.reddit.com/r/decred/comments/fim5j2/stakepool_failure_caused_me_to_lose_all_my/fkiac45) y también dijo que un posible cambio de consenso podría resolver estos [problemas](https://www.reddit.com/r/decred/comments/fim5j2/stakepool_failure_caused_me_to_lose_all_my/fkku35k). Si está leyendo esto y no tiene una [copia de seguridad](https://docs.decred.org/wallets/decrediton/using-decrediton/#backup-redeem-script) de sus scripts de canje, tome esta advertencia y haga una copia de seguridad y almacénela junto con su semilla.

Se [notificó](https://github.com/decred/dcrwebapi/pulls?q=is%3Apr+author%3Ajholdstock+created%3A2020-03-01..2020-03-31) a algunos VSP que tenían páginas de registro rotas / desactualizadas / errores de devolución que se eliminarán de la [lista](https://decred.org/vsp/). Algunos de ellos han respondido y solucionado los problemas. raqamiya.net, tokensmart.io y dcrpos.idcray.com se han eliminado porque no respondieron.

Advertencia: los autores de la revista Decred no tienen idea de la confiabilidad de alguno de los servicios anteriores. Haga su propia investigación antes de confiar su información personal o activos a cualquier entidad.

## Alcance

[Decred in Depth](https://decredindepth.libsyn.com) lanzó dos nuevos episodios en marzo y uno a principios de abril, mientras que [Rough Consensus](https://roughconsensus.libsyn.com/) también lanzó 2 episodios (Ver abajo en [Media](#media)).

@Dustorf [publicó](https://proposals.decred.org/proposals/c830ea5afea45a0aabf4092d1bea51fb10b8bfa2d8474aac03224f0f94d3d1af/comments/56) que estará operando en una capacidad reducida durante los próximos dos meses y que el costo de la propuesta se reducirá en consecuencia. Las ejecuciones afectadas incluyen: boletín informativo, generación de contenido original, Decred Assembly, Relaciones Públicas, coordinación de lanzamientos y trabajo de actualización. Esto significa específicamente que la versión DEX tendrá que ser administrada por los desarrolladores y la comunidad en general.

@dezryth [publicó](https://scottrchristian.com/2020/03/15/dezryth-proposal-updates/) una segunda actualización sobre su operación de la cuenta de Facebook de Decred para el mes de febrero. Este es más detallado e incluye estadísticas para cada publicación, comparación con los competidores y comparte algunas ideas sobre los próximos pasos. @dezryth reconoce que las estadísticas actuales no son excelentes y que el seguimiento orgánico es difícil de construir, pero en el lado positivo, la publicación activa trajo un aumento del 30% en las vistas diarias.

@bee [comentó](https://www.reddit.com/r/decred/comments/fa70c3/decred_2019_marketing_report/) bastante (de verdad) en el Informe de marketing 2019 y compartió su visión para seguir adelante.

Se agregó una recopilación completa de las [ideas erróneas comunes](https://github.com/decredcommunity/wiki/blob/master/wiki/misconceptions.md) y las críticas a Decred en Decred Community Wiki, junto con las respuestas a ellas. Comentarios / contribuciones de bienvenida, la discusión la puede seguir [aquí](https://www.reddit.com/r/decred/comments/frqkt0/your_favorite_misconceptions_about_decred_in_one/).

Los logros de Monde PR para marzo:

- Divulgación e introducciones para atacar a periodistas.
- Comentarios reactivos lanzados a las noticias actuales.
- Envió comentarios de portavoces de Decred a 7 noticias.
- Lanzó Decred a 3 próximas funciones.
- Envió una pieza de liderazgo de pensamiento escrita por @richardred a ValueWalk.
- Aseguró 2 entrevistas con los medios.

Cobertura de noticias asegurada por Monde PR:

- Un [artículo](https://cointelegraph.com/news/proof-of-stake-vs-proof-of-work-which-one-is-fairer) en Cointelegraph con comentarios de @jy-p sobre modelos de consenso.
- Un [artículo](https://www.financemagnates.com/cryptocurrency/news/fintech-experts-share-tips-for-remote-work-during-coronavirus-quarantine/) en Finance Magnates con comentarios de @richardred en trabajo remoto.
- Un [artículo](https://www.coindesk.com/remote-working-proves-unexpected-hero-as-half-of-us-economy-shifts-to-home-offices) en CoinDesk con comentarios de @jy-p sobre escalado rápido que también fue sindicado a Yahoo Finance.

## Eventos

Asistidos:

- 4 de marzo - [Decred Meetup](https://www.eventbrite.com/e/decred-meetup-la-plata-tickets-95666770887) - La Plata, Argentina. Fue una introducción al proyecto Decred en el que @camilolwi, @tomee y @pablito hablaron sobre los fundamentos de Decred, su modelo de consenso, gobernanza, votación y cómo convertirse en un contratista para el proyecto. Hubo alrededor de 20 asistentes a la reunión y una sesión de networking. ([fotos](https://twitter.com/cryptorc_tech/status/1238180910513733634))
- 4 de marzo - [Decred Meetup](https://www.eventbrite.com/e/decred-en-uninet-business-school-caracas-venezuela-tickets-97157792573) - Caracas, Venezuela. La reunión fue organizada conjuntamente por Uninet Business School e Innova Consultants. Hubo 15 asistentes a la reunión, hubo una introducción a Decred, su modelo de seguridad, privacidad, cómo contribuir, seguido de una sesión de preguntas y respuestas y networking. ([fotos](https://twitter.com/Decred_ES/status/1235324847338795009))
- 4 de marzo - [Crypto and Blockchain 2020 and Beyond](https://www.meetup.com/BC-Aus/events/268793182/) - Melbourne, Australia. Este evento de más de 80 personas dirigió las ventas de las entradas a Crypto Fire Alliance para ayudar con la emergencia de incendios forestales (el evento recaudó $ 1K mientras que el programa completo [recaudó](https://www.finder.com.au/crypto-bushfire-fundraiser) $ 27K en cripto). @eSizeDave se unió a un panel de discusión de una hora de duración, [señalando](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$158381267934685XUpiS:decred.org): "la audiencia me hizo más preguntas que nadie" y obtuve muchas reuniones siguientes como resultado ". ([informe](https://github.com/decredcommunity/events/blob/master/reports/20200304-crypto-and-blockchain-2020-and-beyond-melbourne-australia.md), [video](https://twitter.com/DecredAustralia/status/1235390840307978245))
- 5 de marzo - [Decred Meetup](https://www.eventbrite.com/e/decred-meetup-en-valencia-venezuela-tickets-97804334397) - Valencia, Venezuela. Co-organizado por ClicTechNova y CoWorking Lab. La reunión fue una introducción al ecosistema Decred, blockchain híbrido, mecanismo de gobierno, privacidad y elementos que hacen de Decred una DAO. Hubo ~ 50 asistentes que hicieron preguntas interesantes sobre los ataques sociales en la red, como es la distribución y el modelo de incentivos de DCR. ([fotos](https://twitter.com/Decred_ES/status/1236079742643773440), [video](https://twitter.com/Decred_ES/status/1236080559752916998))
- 6 de marzo - [Impact Hub](https://www.eventbrite.com/e/decred-meetup-impact-hub-caracas-venezuela-tickets-97159680219) - Caracas, Venezuela. Co-organizado por El Dorado y Cointigo. La reunión fue una introducción al ecosistema Decred, su estructura de gobierno y lo que lo convierte en una criptomoneda diferente del resto. Asistieron alrededor de 30 personas, varios empresarios y desarrolladores, pero también varios nuevos usuarios de criptomonedas que buscan más información sobre la tecnología y las oportunidades de inversión. ([fotos](https://twitter.com/Decred_ES/status/1236337867095343104), [video](https://twitter.com/Decred_ES/status/1236340242698752001))
- 8 de marzo - [Día Internacional de la Mujer](https://www.meetup.com/GDGCasablanca/events/268661463/) - Casablanca, Marruecos. El evento se realizó en ENSAM, una Universidad de Ciencias. La mayoría de los 70 asistentes eran estudiantes y desarrolladores de ciencias en datos. @arij dio una charla de 1 hora sobre blockchains -- Decred y un taller "Lo que aprendí de mis experiencias hablando y explicando la tecnología blockchain y Decred, es que la gente está más interesada cuando les muestras cómo funcionan realmente las cosas". ([notas](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$158374584733992NOIMZ:decred.org), [fotos](https://www.flickr.com/photos/187387360@N04/albums/72157713440754483))
- 12 de marzo - [Bitcoin Woman to Woman](https://twitter.com/bitcoinemb/status/1233500964566523911) - Ciudad de México, México. Organizado conjuntamente por Bitcoin Embassy Bar, la reunión de ~ 30 personas fue para discutir la participación de las mujeres en la industria de las criptomonedas y cómo empoderar a las mujeres para que usen las criptomonedas. @francov \ _ hizo una presentación sobre cómo contribuir al proyecto Decred y su experiencia trabajando en la industria. "Lo más destacado de la charla fue expresar que no necesitamos un título, género, nacionalidad, edad, ni siquiera su nombre real, solo necesitamos su talento y su aspiración para ayudar al crecimiento del ecosistema Decred". La reunión fue seguida por una sesión de networking. ([informe](https://github.com/decredcommunity/events/blob/master/reports/20200312-bitcoin-woman-to-woman-mexico-city-mexico.md))
- 12 de marzo - [Decred Meetup](https://www.meetup.com/es-ES/BitcoinBlockchainUruguay/events/269160706/) - Montevideo, Uruguay. Alrededor de 25 personas asistieron a la reunión. @tomee presentó una introducción a Decred y su seguridad, adaptabilidad y sostenibilidad, Politeia, gobernanza y cómo contribuir. La reunión también fue una sesión de networking y algunas de las personas conocieron el proyecto de Labitconf. (fotos: [1](https://twitter.com/ivarese/status/1238628854379536389), [2](https://twitter.com/cryptorc_tech/status/1241081659669315585))
- 12 de marzo - [Blockchain Summit Latam](https://twitter.com/Decred_ES/status/1237552322596593665) - Ciudad de Panamá, Panamá. El evento se reprogramó para el 15 y 16 de octubre, pero este cambio ocurrió 24 horas antes del evento cuando algunos oradores ya estaban en el área (~ 35 personas). El personal del evento aprovechó la oportunidad y organizó una pequeña reunión donde los presentadores tuvieron la oportunidad de establecer contactos y conocer de cerca los proyectos. @adcade y @elian conversaron con algunos representantes y obtuvieron una [entrevista](https://es.cointelegraph.com/news/decred-how-does-your-development-continue-during-the-bear-market) para Cointelegraph en español. ([informe](https://github.com/decredcommunity/events/blob/master/reports/20200312-blockchain-summit-latam-meetup-panama-city-panama.md))
- 12 de marzo - [Hablemos Decred 01](https://twitter.com/Decred_ES/status/1238242352306614273) - Internet. "Hablemos Decred", la primera reunión en línea en español utilizó el servidor Discord de Decred. La mayoría de las preguntas fueron sobre el sistema de votación PoS de Decred. Los que tenían algún conocimiento previo de la criptografía preguntaron cómo hacer stake, y los que no, querían saber más sobre los derechos de voto y qué pueden hacer las partes interesadas con sus tickets. Alrededor de un tercio de ~ 15 personas eran nuevas en el proyecto. ([informe](https://github.com/decredcommunity/events/blob/master/reports/20200312-hablemosdecred-01-internet.md))
- 18 de marzo - [Intercambios en LATAM](https://twitter.com/Decred_ES/status/1240428280756310018) - Internet. @elian habló sobre intercambios centralizados y descentralizados en una reunión virtual con personas de [@AvaLatam](https://twitter.com/AvaLatam), [@blockchain_land](https://twitter.com/blockchain_land) y virica.io Mexico Asistieron alrededor de 16 personas y una de las lecciones aprendidas fue que las conversaciones en línea deberían ser de 30 minutos o menos.
- 24 de marzo - [Webinar Decred](https://www.meetup.com/es-ES/blockacademycl/events/269108758/) - Internet. @tomee y @camilolwi hablaron de todo sobre Decred y los desafíos de la gobernanza descentralizada de blockchain en un seminario web coorganizado con Blockchain Academy Chile. ([video](https://www.youtube.com/watch?v=U07ZL_qFAQM))
- 27 de marzo - [Hablemos Decred 02](https://twitter.com/Decred_ES/status/1243214184793485314) - Internet. La segunda reunión en línea en español exploró a Jitsi para conectar a 13 participantes de Argentina, México, Bolivia, Chile, de los cuales 7 eran nuevos en el proyecto. Esta vez, la llamada comenzó con una charla introductoria sobre Decred, una demostración de Decrediton y un micrófono abierto para preguntas y comentarios. ([informe](https://github.com/decredcommunity/events/blob/master/reports/20200327-hablemosdecred-02-internet.md))
- 29 de marzo - [Binance AMA](https://twitter.com/Decred_ES/status/1244360357843533825) - Internet. El evento fue organizado en el grupo Binance Spanish Telegram con más de 8,000 miembros y recibió un alto nivel de compromiso. @adcade, @elian y @pablito obtuvieron 155 preguntas de 73 participantes y otorgaron 0.333 DCR a las mejores preguntas. Se recopiló una buena cantidad de conocimiento que puede indicar dónde los posibles usuarios de Decred carecen de información. Esta fue la segunda AMA Decred con la comunidad española de Binance y la AMA más larga que tuvieron hasta ahora (~ 2.5 horas). ([informe](https://github.com/decredcommunity/events/blob/master/reports/20200329-decred-ama-binance-spanish-community-internet.md))
- 30 de marzo - [Meetup virtual Decred and Sound Money](https://www.meetup.com/Decred-Australia/events/269640276/) - Internet. El evento fue organizado por @eSizeDave y @zohand y se unió a @Checkmate para discutir temas clave como el dinero sólido, el entorno macroeconómico, el oro y Decred. Los participantes quedaron bastante impresionados por la calidad y dejaron buenos comentarios, uno de ellos disfrutó de que era "mentalmente estimulante". ([informe](https://github.com/decredcommunity/events/blob/master/reports/20200330-decred-and-sound-money-internet.md))

Cancelados:

- 5 de abril - [Toronto Blockchain Week](https://www.eventbrite.ca/e/discover-decred-an-autonomous-digital-currency-toronto-blockchain-week-tickets-91562362491) - Toronto, Canadá.

Eventos próximos:

- 13-17 de abril - [Jalisco Talent Land @ Home](https://www.talent-land.tv/) - Internet. En un panel llamado "Decred, cripto y el futuro del dinero", el equipo Decred LATAM dará un resumen sobre Decred y explorará cómo el ecosistema cripto transformará el trabajo remoto y nuestra interacción con el dinero. El panel se transmitirá en [talent-land.tv](https://www.talent-land.tv/) el 15 de abril, 21:00 (CST, UTC-5).
- 16 de abril - [Seminario web Decred](https://twitter.com/Decred_ES/status/1245452957417684992) - Internet. El tema será "Hablemos de las criptomonedas y el futuro del dinero", un seminario web organizado por la Universidad Iberoamericana para analizar las criptomonedas y dar una visión general de Decred.
- 14 de mayo - [BlockConf](https://blockconf.digital/) - Internet. El equipo de Decred LATAM ejecutará un stand virtual para que Decred responda las preguntas de los asistentes. Si alguien quiere ayudar a mantener el stand activo en varias zonas horarias durante el evento de 48 horas, comuníquese con @elian.
- 30-31 de mayo - [Bitconf](https://www.bitconf.com.br/portal/) - São Paulo, Brasil. Decred tendrá múltiples charlas sobre diversos temas.
- Junio a más tarde - [Campus Party Amazonia](https://brasil.campus-party.org/campus-party-amazonia-2020/) - Manaus, Brasil. Movido desde marzo.
- Junio a más tarde - [Jalisco Talent Land](https://www.talent-land.mx/en/home/) - Guadalajara, México. Movido desde abril.
- Finales de 2020 - [DevOpsDays](https://devopsdays.org/events/2020-natal/welcome/) - Natal, Brasil. Movido desde marzo.

Pospuesto hasta nuevo aviso:

- [CIBTC Blockchain Summit](http://cibtc.es/) - Motril, España.
- Decred Meetup - La Paz, Bolivia.
- [Bitcoinference](https://www.eventbrite.com/e/bitcoinference-where-the-blockchain-meets-you-tickets-94598812595) - Cancún, México.

## Media

[decredpower.info](https://decredpower.info/) es un nuevo directorio para explorar todas las cosas de Decred. Las sugerencias son bienvenidas [aquí](https://github.com/raedahgroup/decredpower/issues).

- Observing Ethereum governance during the ProgPoW debate por @Checkmate ([medium](https://medium.com/@_Checkmatey_/observing-ethereum-governance-during-the-progpow-debate-9bf1aec724ad))
- Crypto risk is not what you think por @Dustorf ([medium](https://medium.com/@dlefebvr/crypto-risk-is-not-what-you-think-8a2662840b70))
- Theory of three pillars in the cypherpunk social contract por @Cato_io ([medium](https://medium.com/@cato_io/threepillarstheory-cd6b57c5d88a))
- Public service, pandemics and crypto networks por @mrbulb ([medium](https://medium.com/@decentpartners/public-service-pandemics-and-crypto-networks-379dce1594d1))
- Decred: ¿Cómo continúa su desarrollo durante el bear market? por @adcade ([es.cointelegraph.com](https://es.cointelegraph.com/news/decred-how-does-your-development-continue-during-the-bear-market))

La [propuesta](https://proposals.decred.org/proposals/bc20f986c3ea2fed2ea074c377a89f1a4b956ea0d527a8b6c099a5a8f175beb5) de Brazil Marketing y Eventos se cubrió en los medios desde una interesante perspectiva de "inversión en Brasil" (en portugués):

- "La comunidad de Decred permite que se inviertan más de 500,000 BRL en Brasil" ([criptofacil.com](https://www.criptofacil.com/comunidade-decred-permite-que-mais-r-500-mil-sejam-investidos-brasil/))
- "La criptomoneda invertirá más de medio millón en Brasil" ([livecoins.com.br](https://livecoins.com.br/criptomoeda-vai-investir-mais-meio-milhao-brasil/))
- "'Las ballenas' aprueban y Decred puede invertir más de 500,000 BRL para promover la criptomoneda en Brasil" ([cointelegraph.com.br](https://cointelegraph.com.br/news/decred-pode-investir-ate-us-500-mil-para-promover-criptomoeda-no-brasil)) - este está mal escrito y se basa en otra entrevista (@emiliomann)
- "Las criptomonedas que más invierten en Brasil" ([cointimes.com.br](https://cointimes.com.br/as-criptomoedas-que-mais-investem-no-brasil/))

Traducciones

- Teoría de los tres pilares en el contrato social cypherpunk - [en español](https://medium.com/decred-es/teor%C3%ADa-de-los-tres-pilares-en-el-contrato-social-del-cypherpunk-40f569836b6a) por @francov \ _
- Decred Technical Brief - [en árabe](https://insaf01.github.io/decred-arabic/articles/decred-technical-brief-ar.html) por @arij
- Revista Decred, febrero de 2020, se tradujo al árabe (@arij), chino (@Dominic) y español (@francov \ _). Los tres se almacenan [en Git](https://github.com/xaur/decred-news/blob/docs/guidelines.md#why-git) que ayuda a preservar el trabajo a largo plazo y protegerlo de la censura. ¡Gracias a todos por correr la voz!

Videos:

- Decred's 2020 marketing and publishing proposals for the USA & Brazil breakdown por @Exitus ([youtube](https://www.youtube.com/watch?v=Liol1lLCinQ))
- Decred bi-Weekly news update - 12 de Marzo del 2020 por @Exitus ([youtube](https://www.youtube.com/watch?v=N4U1FwYUaKA))
- Decred bi-Weekly news update - 31 de Marzo del 2020 por @Exitus ([youtube](https://www.youtube.com/watch?v=MBi7d263HvE))
- Top 5 staking coins in 2020 por Coin Bureau ([youtube](https://www.youtube.com/watch?v=znx7H7JWtfg))


Audio:

- Decred in Depth Ep. 19 - Leo Zhang, de Iterative Capital, habla sobre la prueba detrabajo, da una explicación de primera mano de la economía minera y considera los beneficios de un componente de PoS híbrido y la toma de decisiones formales de las partes interesadas. ([libsyn](https://decredindepth.libsyn.com/leo-zhang-dcr-mining), [youtube](https://www.youtube.com/watch?v=iWi3nK0HIHE), [soundcloud](https://soundcloud.com/decredindepth/leo-zhang-dcr-mining))
- Decred in Depth Ep. 21 - @Exitus habla sobre la producción de contenido de video para la DAO de Decred, como convertirse en un contratista y los desafíos que enfrenta el marketing durante el mercado bajista. ([libsyn](https://decredindepth.libsyn.com/-exitus-dcr-community-managment-media), [youtube](https://www.youtube.com/watch?v=oGi3NA14CZU))
- Rough Consensus Ep. 2 - Consenso distribuido. @ mr.black, @Checkmate y @permabullnino discuten el concepto de contabilidad de entrada triple y cómo proporciona un marco para analizar los mecanismos de consenso. La teoría es que PoW, PoS y los sistemas de seguridad híbridos proporcionan diferentes garantías de seguridad y contabilidad. ([libsyn](https://roughconsensus.libsyn.com/rough-consensus-2-distributed-consensus))
- Rough Consensus Ep. 3 - El largo camino por delante. @ mr.black, @Checkmate y @permabullnino discuten el último cambio macro desencadenado por COVID-19, el estallido del mercado alcista de acciones más largo de la historia y cómo las criptomonedas pueden desempeñar un papel en el futuro. ([libsyn](https://roughconsensus.libsyn.com/rough-consensus-3-the-long-road-ahead))
- POV Crypto Podcast Ep. 127 - Dinero difícil en tiempos de brrrr con @permabullnino ([libsyn](https://povcryptopod.libsyn.com/127-hard-money-in-the-time-of-brrr-with-permabullnino), Decred es mencionado alrededor de la marca de 30 minutos)
- ¿Qué es Decred? por @elian ([criptotendencias.com](https://www.criptotendencias.com/podcast/episodio-30-que-es-decred-entrevista-con-elian-huesca-community-builder-business-dev-del-proyecto/))
- Decred Brief por @elian ([Territorio Bitcoin](https://www.ivoox.com/episodio-111-especial-comunidad-blockchain-cuarentena-audios-mp3_rf_49382826_1.html))

## Discusiones de Comunidad

Noticias en el sistema de comunicación:

- Se publicó una guía sobre cómo unirse a la comunidad en Matrix en [docs.decred.org](https://docs.decred.org/getting-started/joining-matrix-channels/). Si prefiere que Stakey lo guíe, hay una versión ligeramente diferente disponible en [dcrcomic.org](https://dcrcomic.org/guide-enter-the-matrix.html).
- Para su información, puede ver el [r / feed de comentarios](https://www.reddit.com/r/decred/comments/) para nunca perderse un nuevo comentario.

Publicaciones seleccionadas de Reddit:

- u / oiezz sugirió utilizar las publicaciones mensuales del Diario como espacios de discusión, y la [publicación](https://www.reddit.com/r/decred/comments/fgo0p4/decred_journal_february_2020/) del mes pasado acumuló 18 comentarios.
- Una [publicación](https://www.reddit.com/r/decred/comments/fhrsqn/austerity_mindset/fkd6nrn/) de u / Corp-Por preguntando si Decred debería adoptar una mentalidad de austeridad con fondos de la Tesorería, tuvo 22 comentarios y un puntaje de 7. La mayoría de los comentaristas no estaban tan interesados como el OP para hacer cambios drásticos, citando las amplias reservas y la capacidad de la Tesorería para mantener el financiamiento a las tasas actuales durante 5 años.
- Una [publicación](https://www.reddit.com/r/decred/comments/frb863/next_privacy_iteration_how_private_and_fungible/) preguntando sobre la próxima iteración de privacidad de Decred hizo que @ jy-p respondiera que el enfoque es elegir lo más bajo. colgando fruta (soporte de Decrediton, seguridad post-cuántica), continúe aumentando la absorción de la mezcla, luego revise las preguntas sobre cómo mejorar aún más la privacidad.
- @davecgh [respondió](https://www.reddit.com/r/decred/comments/fim5j2/stakepool_failure_caused_me_to_lose_all_my/) a la desafortunada historia de un interesado Decred que ha perdido el acceso a su DCR estacado porque el VSP que estaban usando se desconectó, su máquina Decrediton fue destruida y no habían guardado el script de canje (ver detalles [aquí](https://docs.decred.org/wallets/decrediton/using-decrediton/#backup-redeem-script)) . @davecgh explicó que el script de canje se comparte con el VSP como una firma múltiple donde el usuario o VSP pueden canjear DCR bloqueado y revocar tickets. A medida que los scripts de canje se reutilizan y se revelan cuando se canjea el primer boleto, este escenario de DCR bloqueado solo puede ocurrir cuando la billetera del usuario o VSP nunca ha estado en línea para canjear ninguno de los boletos que lo usaron. Una vez que esa combinación de billetera / VSP ha canjeado un solo boleto, el script se almacena efectivamente en la cadena de bloques.
- @bee [piensa](https://www.reddit.com/r/decred/comments/frqvmc/checkmate_on_twitter_ftx_has_finally_listed_dcr/flxb7s0/) que los derivados son malos y espera informarse sobre su beneficio para el público.
- @bee hizo un [punto](https://www.reddit.com/r/decred/comments/frqkt0/your_favorite_misconceptions_about_decred_in_one/fm1jrmc/?context=3) de que no todos los cambios de consenso son tan indeseables como los cambios frecuentes del algoritmo PoW necesarios para mantener la resistencia ASIC.

Debates seleccionados en Twitter:

- @swack tuiteó este [hilo](https://twitter.com/swack0/status/1239674494526111747) sobre Decred como el único criptoactivo no Bitcoin que merece consideración como SoV y alternativa fiat, citando adaptabilidad, sostenibilidad, y la falta de productos financieros apalancados asociados.
- DCP-0006 Social Media Governance, [anunciado](https://twitter.com/decredproject/status/1245399765489254400?s=20) al 1 de abril, está en duda con una proporción inesperadamente grande de encuestados (66%) en Twitter votación electoral para darle a Twitter una mayor ponderación: esto plantea serias preguntas sobre la metodología de muestreo.
- @chappjc [tweets](https://twitter.com/chappjc/status/1245075450625511425) sobre la coordinación del primer intercambio atómico impulsado por órdenes de dcrdex.
- @davecgh sale de la jubilación de Twitter con un popular [tweet](https://twitter.com/davecgh/status/1238309416270790658?s=20) sobre la activación de los Compromisos de encabezado de bloque DCP0005.

## Mercados

En marzo, DCR cotizaba entre USD 8,68-19,78 / BTC 0,0017-0,0021. La tarifa diaria promedio fue de $ 13.40.

El 7 de marzo, BTC / USD comenzó su disminución de $ 9,100 a $ 7,800 el 11 de marzo. El 12 de marzo se unió al pánico global de COVID-19 y se desplomó por debajo de ~ $ 4,500 e ([incluso más bajo](https://twitter.com/HsakaTrades/status/1239227306863820801) en algunos mercados). La mayoría de los criptoactivos perdieron alrededor del 40% ese día, lo que demuestra sus niveles de precios en su mayoría especulativos y su dependencia persistente de BTC. Este volcado llevó a DCR / USD a ~ $ 8.

Fred Wilson [señaló](https://avc.com/2020/03/correlation-and-market-meltdowns/) que "en pánico, todos los activos están correlacionados", pero cuando se asiente el pánico, los fundamentos de la criptomoneda podrían comenzar a entrar en acción.

## Noticias relevantes externas

Los mercados en todas partes tuvieron un [mal momento](https://www.bloomberg.com/news/articles/2020-03-08/yen-slides-as-oil-price-war-adds-to-global-worries-markets-wrap) cuando la gravedad de la situación de COVID-19 se hizo evidente y las naciones comenzaron a cerrarse. Los precios de las criptomonedas disminuyeron tanto o más que la mayoría de los otros activos, todas las reuniones y eventos de Decred se cancelan o se mueven en de fecha, y algunos contribuyentes tienen más cuidado de niños que antes, pero esos parecen ser los únicos cambios que son directamente relevantes para Decred. Sin embargo, la situación obviamente tiene un efecto en todos nosotros y en el entorno macroeconómico y las perspectivas más amplias. Mantente a salvo.

Fue un mes desafiante para los proyectos DeFi, ya que una fuerte caída en el precio de ETH tensó la estabilidad de la moneda estable DAI. Cuando el precio de ETH se mueve demasiado, algunos préstamos DAI se liquidarán en subastas si sus titulares no agregan más ETH para alcanzar la garantía requerida, pero en esta ocasión, el precio parece haberse movido demasiado rápido para que las subastas de liquidación se mantengan. Este [artículo](https://medium.com/@whiterabbit_hq/black-thursday-for-makerdao-8-32-million-was-liquidated-for-0-dai-36b83cac56b6) explica cómo se liquidaron $8,32 millones en DAI por $0, ya que las condiciones imprevistas en el proceso de subasta (incluida la congestión de la cadena ETH) dieron como resultado que el 36% de todas las subastas de liquidación fueran al mejor postor a $ 0.00. "La Bóveda más grande ha perdido ~ 35,000 ETH, mientras que el liquidador más exitoso ha tenido una ganancia de 30,000 ETH". Esto dejó a la Fundación Maker y a la comunidad en una [posición difícil](https://www.coindesk.com/defi-leader-makerdao-weighs-emergency-shutdown-following-eth-price-drop), considerando cambiar las reglas sobre la marcha o provocar un cierre de emergencia. La Fundación [decidió](https://www.coindesk.com/makerdao-debts-grow-as-defi-leader-moves-to-stabilize-protocol) no usar su poder para intervenir directamente desencadenando un cierre, y se movió para presentar propuestas que modificaran los parámetros de riesgo y organizar una subasta de tokens MKR recién impresos para pagar la deuda del protocolo y "reembolsar los CDP que perdieron fondos".

El conflicto Steem-Sun comenzó el mes pasado cuando la compañía Steemit (y sus tokens STEEM "minados por ninjas") fue adquirida por Justin Sun - Los testigos de Steem (DPoS) adoptaron un hard fork para anular esos tokens, luego Sun movilizó el apoyo de intercambio para expulsar lo establecido por los testigos y los reemplazaron con títeres que no adoptarían el fork, conservando sus fichas STEEM. En marzo, la estrategia de la comunidad Steem cambió, ya que un grupo influyente decidió [migrar](https://www.coindesk.com/steem-will-hard-fork-in-just-hours-over-community-fears-de-justin-sun-power-grab) lejos de la cadena de bloques Steem a una nueva llamada Hive. Se dice que los intercambios Binance y Huobi apoyan este movimiento, en un cambio notable de sus acciones el mes pasado cuando votaron con Sun. Los miembros prominentes de la comunidad Steem agradecieron a los miembros de la comunidad por retirar su STEEM de los intercambios, para presionar a los intercambios y dar marcha atrás en el apoyo a los testigos impulsados por Sun. Parece que los operadores de intercambio también se equivocaron sobre la importancia de sus votos en ese contexto, creyendo que estaban votando por una actualización regular del protocolo.

Hive es lo mismo que Steem en la mayoría de los aspectos, con 1 STEEM intercambiable por 1 HIVE: la principal diferencia es que los tokens Steemit STEEM de Sun no serán canjeables en la cadena de HIVE, cortándolos efectivamente del ecosistema. Cuando se escribió esta [historia](https://www.coindesk.com/splinter-cryptocurrency-hive-outperforms-justin-suns-steem-after-one-week-trading) el precio de HIVE era casi el doble que el de STEEM , pero a partir del 4 de abril, los dos tokens se negocian por precios similares. Este caso debería ser de interés para aquellos que dicen que votar con monedas es plutócrata, ya que muestra lo que puede suceder cuando las ballenas intentan usar sus monedas para imponer su voluntad en una comunidad poco dispuesta.

Ha sido un buen mes para las personas a las que les gusta comprar, mantener o vender criptomonedas sin ser consideradas delincuentes. Los gobiernos en [Corea del Sur](https://thenews.asia/amendment-to-special-reporting-act-passes-cryptocurrency-trading-now-legal-in-south-korea/) y la corte suprema en [India](https://news.bitcoin.com/bitcoin-legal-india-supreme-court-verdict-cryptocurrency/) hizo movimientos para anular las restricciones impuestas previamente sobre el comercio de criptomonedas.

Desde el 18 de marzo, Tether ha emitido más de $ 400 millones de USDT en lotes de $ 60 millones y superó la marca [$ 6 mil millones](https://beincrypto.com/tether-usdt-quietly-surpasses-the-6-billion-mark/). El 25 de marzo, el USDT mantenido en las exchanges ha establecido un nuevo ATH de [$ 1.2 mil millones](https://twitter.com/glassnodealerts/status/1242849119456157699). El momento es interesante, ya que llega rápidamente después del colapso del mercado del 12 de marzo. Use el USDT con precaución, porque incluso su cofundador cree ["realmente no importa"](https://beincrypto.com/tether-co-Fundador-no-realmente-importa-si-usdt-respaldado-por-igual-cantidad-de-dólares/) si está respaldado por una cantidad igual de dólares.

El gobierno de los Estados Unidos aprobó un plan de "estímulo" excepcionalmente grande [$ 2 billones](https://www.zerohedge.com/economics/anatomy-2-trillion-covid-19-stimulus-bill) atribuido a COVID-19. La discusión sobre la fuente de fondos aún es poco frecuente en los medios. Un político [argumentó](https://twitter.com/RepThomasMassie/status/1243565651391897603) que el proyecto de ley crea aún más secreto en torno a la Reserva Federal que ya no es auditable.

La Fed de EE. UU. Realizó múltiples movimientos sin precedentes atribuidos a COVID-19, de manera sucinta [resumida](https://www.bloomberg.com/news/articles/2020-03-25/fed-unbound-all-the-u-s-central-bank-s-corona-related-moves) por Bloomberg. La mayor parte de eso significa [crear dinero](https://seekingalpha.com/article/4335693-inflation-alert-money-supply-expanding-26x-rate-of-qe1) de la nada sin trabajo, y luego prestar distribuya ese dinero a personas y empresas que necesitarán _trabajar_ para devolverlo. Entre las medidas se encuentran las líneas de intercambio creadas para "impulsar USD en todo el mundo para facilitar el acceso a la moneda más importante del mundo".

El presidente de uno de los 12 bancos de la Reserva Federal admitió abiertamente en una [entrevista](https://www.zerohedge.com/markets/kashkari-says-fed-has-infinite-amount-cash-we-create-it-electronically ) que "hay una cantidad infinita de efectivo en la Reserva Federal".

BCE [anunciado](https://www.ecb.europa.eu/press/pr/date/2020/html/ecb.pr200318_1~3949d6f266.en.html) un "Programa de compra de emergencia pandémica" de 750 mil millones de euros y [anotado](https://twitter.com/Lagarde/status/1240414918966480896) "No hay límites para nuestro compromiso con el euro. Estamos decididos a utilizar todo el potencial de nuestras herramientas, dentro de nuestro mandato". El banco está listo para aumentar aún más el tamaño de los programas de compra de activos y revisar los límites autoimpuestos.

## ¡Feliz cumpleaños DJ!

El número 24 marca el segundo aniversario de Decred Journal.

Retrospectiva y un poco de trivia de @bee:

- El equipo de DJ ha crecido de 2 a ~ 5 colaboradores estables, ~ 3-8 traductores y ~ 7-11 personas revisando y compartiendo comentarios.
- El tamaño de bytes de un problema ha aumentado de 20 KB a ~ 50 KB. El mayor problema fue [64.5 K](https://xaur.github.io/decred-news/journal/201908.html) (7.5K palabras).
- Nuestro proceso de producción ha evolucionado significativamente y ahora está ampliamente [documentado](https://github.com/xaur/decred-news/blob/docs/guidelines.md).
- Es posible que haya notado que el [pastel](https://xaur.github.io/decred-news/journal/202002.html) de [Decred](https://xaur.github.io/decred-news/journal/201805.html) tiene un significado especial para mí.
- Para publicar la [primera](https://xaur.github.io/decred-news/journal/201804.html) edición necesitábamos un título. Entre los candidatos considerados se encontraban "Sesión mensual de entretenimiento para los interesados" y "Deep in Decred". Este primero fue rechazado por sus connotaciones sexuales.
- En marzo de 2019 me cansé un poco y [anuncié](https://xaur.github.io/decred-news/journal/201903.html#psa-decred-journal-takes-a-break) que la producción del futuro los problemas son inciertos. Afortunadamente, algunas personas más han [intervenido](https://github.com/xaur/decred-news/issues/65) y continuamos.
- Problema del primer año: al comenzar cada número, me preocupaba no reunir suficiente contenido y que se vería pobre en comparación con los meses anteriores que tenían tanto. Me equivoqué cada vez. Problema del segundo año: al terminar cada número, me preocupaba que fuera demasiado grande y que fuera difícil seguir todo lo que estaba sucediendo.
- ¡No podía imaginar cómo sería el [índice](https://xaur.github.io/decred-news/) de todos los números y traducciones en 2 años!
- Después de ser pionero en el uso de Git y GitHub para DJ, comencé a molestar a casi todos en la comunidad para que hicieran lo mismo con otros documentos. Creo que la preservación del conocimiento es [importante](https://github.com/xaur/decred-news/blob/docs/guidelines.md#why-git) y los seguiré molestando. Gracias por su paciencia.
- Apróximadamente 6 meses después de comenzar a trabajar con DJ, me molestó el rechazo de los votos a favor en Reddit. Luego hablé con la gente y aprendí dos cosas. Primero, las personas que han estado aquí durante años dicen que es común: los humanos se vuelven menos sensibles a cualquier estímulo con el tiempo, incluso uno bueno. En segundo lugar, tomé los votos en serio sin siquiera saber quién está detrás de esos números. Pero las personas que conozco, con las que hablo todos los días, personas de la más alta inteligencia y sabiduría que son la razón por la que todavía estoy aquí, siguen diciéndome que estoy haciendo un buen trabajo. Y siguen haciendo un trabajo increíble durante años sin perseguir los gustos. Entonces me pregunté, ¿por qué me importan más estos números de lo que me importa lo que piensen las mejores personas a mi alrededor? ¡No tiene sentido! Así que dejé de preocuparme por eso. (Sin ofender a nuestros queridos lectores, valoramos mucho sus comentarios, ¡pero no la cantidad de clics! Estoy compartiendo esto para cualquiera que se enfoque demasiado en las estadísticas).
- Gracias a las partes interesadas de Decred por financiar este trabajo y ayudarnos a entregar la escala y la calidad de esta producción.
- Recibimos muchos [comentarios](https://xaur.github.io/decred-news/testimonials.html) positivos durante estos dos años. Alabar no es el objetivo, pero las palabras amables nos hacen saber que todavía estamos en el camino correcto. ¡Gracias por todo el apoyo!

## Sobre esta edición

Esta es la Revista Decred número 24. El índice completo, y de todas las traducciones se encuentran [aquí](https://xaur.github.io/decred-news/).

La mayoría de la información de terceros se transmite directamente desde la fuente después de un control mínimo. Los autores de la Revista Decred no tienen la capacidad de verificar todas las reclamaciones. Tenga cuidado con las estafas y haga su propia investigación.

Sus [comentarios](https://github.com/xaur/decred-news/blob/docs/contributing.md#feedback) y [contribuciones](https://github.com/xaur/decred-news/blob/docs/contributing.md) son siempre bienvenidos.

Créditos (orden alfabético):

- Escritura y edición: bee, elian, degeri, l1ndseymm, kozel, pablito, richardred, s \ _ben
- Revisiones y comentarios: adcade, ammarooni, chappjc, davecgh, emiliomann, guisso, jholdstock, jrick, lukebp, matheusd, michae2xl, raedah
- Imagen del título: saender
- Traducción al Español: francov_
