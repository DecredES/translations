# Revista Decred — Noviembre 2020

![portada](./assets/202011.png)
Imagen: Reestructuración II por @saender


Las mejores noticias de noviembre:

- Los candidatos a la versión v1.6 han sido probados por la comunidad y recibieron muchas correcciones de errores y mejoras en la experiencia del usuario. Los problemas son difíciles de encontrar ahora, por lo que generalmente significa que la graduación a una versión completa ocurrirá pronto.
- dcrdex lanzó una versión de parche con algunas correcciones de casos de borde y mejoras de interfaz de usuario y backend para la próxima versión.
- Se aprobó la financiación para el desarrollo continuo de las billeteras móviles y una nueva billetera de escritorio GoDCR, la financiación para GoDCR también incluye el patrocinio de la librería Gio que se utiliza para la interfaz.
- Los VSP se están incorporando a vspd y ya cuatro proveedores se han actualizado para admitir los nuevos tickets sin cuenta y opcionalmente mixtos que Decrediton ofrece en v1.6.

## Versión 1.6 versión candidata 4

Los candidatos a nuevas versiones tienen muchos errores corregidos en las cuatro partes de la próxima versión v1.6. Obtenga los últimos binarios de RC [aquí](https://github.com/decred/decred-binaries/releases) (haga clic en `Assets`) y asegúrese de [verificarlos](https://docs.decred.org/advanced/verifying-binaries/).

Gracias a todos por ayudar a probar las compilaciones y acercarse al lanzamiento de la épica v1.6.

## Desarrollo
A menos que se indique lo contrario, el trabajo que se informa aquí tiene el estado "fusionado con la rama master". Significa que el trabajo se completó, revisó e integró en el código fuente que los usuarios avanzados pueden construir y ejecutar, pero aún no está disponible en los binarios del lanzamiento en general.

[dcrd](https://github.com/decred/dcrd)

Las reglas de consenso para descentralizar al fondo de tesorería han sido [activadas](https://twitter.com/degeri_crypto/status/1329980732110819331) en la red de prueba sin algún problema o error.

Combinado en master (trabajo hacia v1.7) y portado a la rama de lanzamiento v1.6:
- Mempool limitado para no realizar un seguimiento de las estadísticas de demasiadas transacciones de [pasadas](https://github.com/decred/dcrd/pull/2458) ​​no confirmadas. Esto evita la posibilidad de una serie de ataques de complejidad y acelera la generación de plantillas de bloques para grandes cadenas de transacciones no confirmadas.
- [Manejo de estado](https://github.com/decred/dcrd/pull/2469) en el voto de tesorería en comandos RPC.
- Se agregaron nuevos campos a la salida de algunos comandos RPC para indicar el [monto en el fondo de la tesorería](https://github.com/decred/dcrd/pull/2470) y [sus entradas](https://github.com/decred/dcrd/pull/2472) (fondos provenientes de los nuevos bloques generados) y se actualizaron los documentos.
- Se corrigió un [problema menor de sincronización](https://github.com/decred/dcrd/pull/2474) en el código de tesorería descubierto en testnet.
- La curva predeterminada para generar certificados RPC cambió a P-256 porque Chromium (utilizado por Decrediton) [eliminó](https://security.stackexchange.com/questions/100991/why-is-secp521r1-no-longer-supported-in-chrome-others) el soporte para un P-521 más fuerte.

Otras fusiones:
- La herramienta gencerts obtuvo la capacidad de generar certificados firmados por un certificado y una clave de CA local, lo que ayuda a reducir la complejidad de la configuración. 
- Solucionados los problemas de concurrencia. 
- Más pruebas para [rpcserver](https://github.com/decred/dcrd/issues/2069).
- Lógica de la base de datos [refactorizada](https://github.com/decred/dcrd/pull/2457) para duplicar y agilizar la escritura de actualizaciones futuras.


[dcrwallet](https://github.com/decred/dcrwallet)

- Utilizar la [selección de monedas al azar](https://github.com/decred/dcrwallet/pull/1914) para todos los envíos regulares.
- Guardar las transacciones de las [tarifas del VSP](https://github.com/decred/dcrwallet/pull/1915) no publicadas para evitar los gastos dobles en los reinicios de la billetera.
- Enviar la [transacción principal](https://github.com/decred/dcrwallet/pull/1917) del ticket junto con la solicitud de la dirección de las tarifa del VSP (para registrar el ticket más rápido, el VSP debe estar al tanto de la salida que financia el ticket, que generalmente proviene de la "transacción dividida" extraída en el mismo bloque y no siempre visible inmediatamente por el VSP).
- Usar la [cuenta de cambio](https://github.com/decred/dcrwallet/pull/1919) correcta para pagar las tarifas del VSP cuando realice una compra de tickets mixtos, a fin de evitar que el cambio sin mezclar se use con una cuenta mixta (no hubo filtración de privacidad porque la participación mixta de VSP aún no se ha liberado y no hubo tal problema).
- Hacer [configurable](https://github.com/decred/dcrwallet/pull/1933) la tarifa máxima de VSP.
- Corrección de errores y actualizaciones de la documentación.

[Decrediton](https://github.com/decred/decrediton)

- Actualización del [firmware](https://github.com/decred/decrediton/pull/2932) de Trezor (un paso hacia el [soporte de staking en Trezor](https://github.com/decred/decrediton/issues/2681)).
- Página de [privacidad](https://github.com/decred/decrediton/pull/2987) rediseñada para simplificar, siguiendo el [diseño](https://github.com/decred/decrediton/issues/2965) actualizado.
- [La página de ayuda](https://github.com/decred/decrediton/pull/2885) que presenta las funciones de privacidad.
- Mostrar [registros](https://github.com/decred/decrediton/pull/2888) en la página de privacidad.
- Capacidad para permitir el envío de transacciones desde [cuentas que no sean cuentas mixtas](https://github.com/decred/decrediton/pull/2909).
- Filtro de visualización para transacciones [mixtas](https://github.com/decred/decrediton/pull/2926).
- Se corrigió el destino de [cambio](https://github.com/decred/decrediton/pull/2889) incorrecto para las billeteras de privacidad.
- [Filtrar](https://github.com/decred/decrediton/pull/2854) propuestas que terminaron de votar por su estado de aprobadas o rechazadas.
- No permitir [cerrar](https://github.com/decred/decrediton/pull/3005) Decrediton mientras se estén ejecutando determinadas operaciones.
- Empaquetado de [AppImage](https://github.com/decred/decrediton/pull/2864) donde Decrediton viene como un solo archivo ejecutable (como efecto secundario, esto permite a los usuarios de GNOME evitar tener que iniciarlo a través de la línea de comandos).
- Eliminar el[ límite máximo de billeteras](https://github.com/decred/decrediton/pull/2886).
- Traducción [china](https://github.com/decred/decrediton/pull/2927) actualizada.
- Se agregaron nuevas traducciones parciales al [árabe](https://github.com/decred/decrediton/pull/2974), italiano y polaco.
- Muchos ajustes de interfaz de usuario.

Se corrigieron alrededor de 60 errores en octubre y ~65 en noviembre. La creciente lista de características de Decrediton requiere más pruebas. ¡Muchas gracias a todos los probadores que ayudaron a mejorar Decrediton!

En progreso: 
- Migración a [grpc-js](https://github.com/decred/decrediton/pull/2936) para reducir significativamente el tiempo de compilación y el tamaño binario.
- Pruebas automatizadas para las páginas de [introducción](https://github.com/decred/decrediton/pull/2659) y [configuración](https://github.com/decred/decrediton/pull/2957).
- Compra de tickets en [Trezor](https://github.com/decred/decrediton/pull/2869) sobre la red de prueba.

[Politeia](https://github.com/decred/politeia)
- Verificación del código [TOTP](https://github.com/decred/politeia/pull/1212) al iniciar sesión (esos códigos de 6 dígitos para 2FA).
- [Imagenes](https://github.com/decred/politeiagui/pull/2201)adecuadas a los borradores.
- Numerosos arreglos de [diseño](https://github.com/decred/politeiagui/pull/2197).
- [Pruebas de IU](https://github.com/decred/politeiagui/pull/2151) automatizadas usando [cypress](https://www.cypress.io/).
- Corrección de errores.

CMS:
- Infraestructura para el seguimiento de las [estadísticas de actividad](https://github.com/decred/politeia/pull/1185) de GitHub que se utilizarán para garantizar que el progreso de los desarrolladores coincida con las horas facturadas.
- Estadísticas de facturas anteriores y contribuciones de GitHub en la página Factura para ayudar a los administradores con la revisión.
- Corrección de errores.

En progreso:
- Soporte frontend para el [inicio de sesión de TOTP](https://github.com/decred/politeiagui/pull/2127).

[vspd](https://github.com/decred/vspd)
- No rechazar los tickets con opciones de voto [inválido](https://github.com/decred/vspd/pull/199) (esto es deseable para no detener el registro de tickets cuando el cliente o el servidor no están actualizados, explicado [aquí](https://github.com/decred/vspd/issues/197#issuecomment-739478813)).
- Aceptar la [transacción principal](https://github.com/decred/vspd/pull/205) opcional en la solicitud de dirección de tarifa (consulte la sección anterior de dcrwallet).
- Corrección de errores y limpieza de código.

[dcrpool](https://github.com/decred/dcrpool)
- Completar la implementación de [Postgres](https://github.com/decred/dcrpool/pull/282). Todas las pruebas de la base de datos ahora se ejecutan tanto en Bolt como en Postgres. BoltDB solo permite implementar una única instancia de dcrpool, ya que es una base de datos de clave / valor incorporada. Con Postgres, se pueden implementar varias instancias de dcrpool en la misma base de datos de Postgres.
- Paquete de [errores](https://github.com/decred/dcrpool/pull/284) extraídos para admitir la extracción de la base de datos en su propio paquete
- Corrección de errores y limpieza de código.

[dcrlnd](https://github.com/decred/dcrlnd)
- Se agregó una función de [IPC](https://en.wikipedia.org/wiki/Inter-process_communication) para [permitir](https://github.com/decred/dcrlnd/pull/117) que los procesos principales (como Decrediton) controlen el proceso dcrlnd.

La [portabilidad](https://github.com/decred/dcrlnd/pull/103) de octubre de los cambios desde lnd [v0.11.1](https://github.com/lightningnetwork/lnd/releases/tag/v0.11.1-beta) incluyó correcciones de [dos](https://lists.linuxfoundation.org/pipermail/lightning-dev/2020-October/002858.html) [vulnerabilidades](https://lists.linuxfoundation.org/pipermail/lightning-dev/2020-October/002857.html) que pueden conducir potencialmente a la pérdida de fondos. Más antecedentes del descubridor están [aquí](https://lists.linuxfoundation.org/pipermail/lightning-dev/2020-October/002859.html) y [aquí](https://lists.linuxfoundation.org/pipermail/lightning-dev/2020-October/002855.html).

Se recomienda actualizar a la última [etiqueta](https://github.com/decred/dcrlnd/tags) o candidata de lanzamiento de dcrlnd.

[dcrdex](https://github.com/decred/dcrdex)

Se lanzó el parche [v0.1.3](https://github.com/decred/dcrdex/releases/tag/v0.1.3) solucionando un posible bloqueo del cliente y algunos problemas menores. Los binarios están disponibles como parte de [v1.6 RC4](https://github.com/decred/decred-binaries/releases/tag/v1.6.0-rc4).

Fusionado en la rama master (principal):
- [Botones de cierrre](https://github.com/decred/dcrdex/pull/800) en los modales.
- [Confirmaciónes](https://github.com/decred/dcrdex/pull/805) de la cuenta en la página de detalles de ordenes.
- Transacciones de [canje](https://github.com/decred/dcrdex/pull/797) por lotes para posiblemente ahorrar algunas monedas en las tarifas de tx.
- Notificación visible cuando se [revoca](https://github.com/decred/dcrdex/pull/798) una orden.
- Más [interactividad](https://github.com/decred/dcrdex/pull/837) en el gráfico (resaltar las órdenes flotantes en el gráfico de profundidad y más)
- TUI [eliminado](https://github.com/decred/dcrdex/pull/827) (:formas de vida terminales que caen pequeñas lágrimas:)
- No permitir el comercio mientras la blockchain se está [sincronizando](https://github.com/decred/dcrdex/pull/785).
- Ejecutar la auditoría de contratos de forma [asincrónica](https://github.com/decred/dcrdex/pull/819) para no bloquear los mensajes entrantes y otras actividades para el comercio.
- Secuencia de [apagado](https://github.com/decred/dcrdex/pull/787) mejorada.
- Evitar errores de billetera [bloqueada](https://github.com/decred/dcrdex/pull/817).
- Uso optimizado de la [memoria](https://github.com/decred/dcrdex/pull/794) de los libros de pedidos.
- [Límites de lote](https://github.com/decred/dcrdex/pull/815) configurables para nuevos usuarios y usuarios con buen historial de intercambio.
- Funciones de administración para recuperar [datos de mercado](https://github.com/decred/dcrdex/pull/771).
- [arneses de prueba](https://github.com/decred/dcrdex/pull/820) más rápidos.
- [Bot de prueba](https://github.com/decred/dcrdex/pull/717) de carga con "programas" personalizables para estresar el sistema.
- [Docker](https://github.com/decred/dcrdex/pull/836).
- Especificación para el [protocolo RPC](https://github.com/decred/dcrdex/pull/702) del cliente DEX para ayudar a programas distintos de dexctl (como Decrediton) a utilizar el cliente DEX.
- Arreglar varios casos de borde.

Se fusionaron un total de 37 PR de 6 colaboradores, agregando 7 000 y eliminando 4 000 líneas de código.

En progreso:
- Estimación de [orden máxima](https://github.com/decred/dcrdex/pull/842).
- [Reputación](https://github.com/decred/dcrdex/pull/848) del usuario.
- [Reanudar](https://github.com/decred/dcrdex/pull/856) los intercambios de la base de datos.
- [API enpoints](https://github.com/decred/dcrdex/pull/796) de datos del mercado para permitir que las partes externas y los sitios web extraigan datos del DEX.

[dcrandroid](https://github.com/planetdecred/dcrandroid)
Fusionado en la biblioteca compartida dcrlibwallet:
- Capacidad de enviar [entradas personalizadas](https://github.com/planetdecred/dcrlibwallet/pull/165) (para admitir funciones de [control de monedas](https://nopara73.medium.com/coin-control-is-must-learn-if-you-care-about-your-privacy-in-bitcoin-33b9a5f224a2)).
- Evitar que más de una billetera use la [misma semilla](https://github.com/planetdecred/dcrlibwallet/pull/138).

En progreso:
- Mostrar las [propuestas](https://github.com/planetdecred/dcrandroid/pull/503) en Politeia.
- Soporte al [vspd](https://github.com/planetdecred/dcrlibwallet/pull/163).

[dcrios](https://github.com/planetdecred/dcrios)
- Traducción al [francés](https://github.com/planetdecred/dcrios/pull/726).
- Correcciones de errores y ajustes de la interfaz de usuario 

En progreso: 
- [Propuestas](https://github.com/planetdecred/dcrios/pull/715) de politeia.
- Modo [privado](https://github.com/planetdecred/dcrios/pull/727).

[godcr](https://github.com/planetdecred/godcr)
- [Revisión de la interfaz de usuario](https://github.com/planetdecred/godcr/pull/262).

En progreso: 
- Soporte a [vspd](https://github.com/planetdecred/godcr/pull/263).
- [Propuestas](https://github.com/planetdecred/godcr/pull/254) de Politeia.

[dcrdata](https://github.com/decred/dcrdata)
- Correcciones de errores para la página Mercados.

[dcrros](https://github.com/decred/dcrros)
- Actualizado a la especificación Rosetta [v1.4.5](https://github.com/coinbase/rosetta-specifications/releases/tag/v1.4.5).
- Cobertura de [pruebas unitarias](https://github.com/decred/dcrros/pull/9) para cada llamada de servicio del backend y la mayoría de las rutas en el código.
- Manejo mejorado de la [conexión](https://github.com/decred/dcrros/pull/11) a dcrd.
- Devolver la [lista de pares](https://github.com/decred/dcrros/pull/12) y el estado de sincronización.
- Hacer que los métodos de la API de construcción se puedan usar en una instancia [fuera de línea](https://github.com/decred/dcrros/pull/13) como lo requiere la especificación.

[decred.org](https://github.com/decred/dcrweb)
- Comunicados de prensa convertidos a páginas [separadas](https://github.com/decred/dcrweb/pull/931).
- Actualizaciones de contenido.

Otros:
- La herramienta de [lanzamiento](https://github.com/decred/release) obtuvo un montón de actualizaciones para automatizar más pasos del proceso de lanzamiento.

## Comunidad
Damos bienvenida a los nuevos colaboradores con una fusión de código completada dentro de las ramas principales de desarrollo: @HlloWrld ([dcrweb](https://github.com/decred/dcrweb/commits?author=HlloWrld)).

Estadísticas de la comunidad a partir del 1 de diciembre:
Seguidores en:

- Twitter: 40 897 (+45)
- Suscriptores en Reddit: 9 982 (+45)
- Usuarios en la sala #general de Matrix: 253 (+31)
- Usuarios en Discord: 1 501
- Usuarios en Telegram: 2 339 (-55)
- Suscriptores en YouTube: 4 250 (+40), vistas: 162 000 (+3 000)
- Seguidores en LinkedIn: 932 (+8)
- Estrellas en el repositorio dcrd en GitHub: 567 (+1), forks: 246 (+0)

## Gobernanza
En noviembre, el [fondo de tesorería](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx) recibió 11 975 DCR y gastó 13 846 DCR. Con la tasa promedio diaria de DCR / USD en noviembre de $18.19, esto es $218 000 recibido y $252 000 gastado. A la tasa promedio diaria de octubre de $12.01, la cifra en USD facturada por el trabajo completado en ese mes es de $166 000. A partir del 4 de diciembre, el saldo del fondo de la tesorería es de 636 385 DCR (16.4 millones de dólares a $25.69).

En octubre se publicaron 4 propuestas, se aprobaron 3 y se abandonó 1.

- La propuesta de [GoDCR](https://proposals.decred.org/proposals/e5c8051) de @raedah solicitó un presupuesto de $60 000 para desarrollar otros 8 meses más, una billetera de escritorio nativa escrita en Go utilizando la librería [Gio](https://gioui.org/). Esta propuesta incluye un patrocinio de Gio de $1,000 al mes, volviendose un proyecto pionero. Aprobado con 92% de aprobación y 38% de participación.
- La [propuesta](https://proposals.decred.org/proposals/bc499c9) para las billeteras móviles de @raedah solicitó $44 000 para otros 8 meses de trabajo en las billeteras de Android e iOS. Tanto las billeteras móviles como GoDCR comparten el componente [dcrlibwallet](https://github.com/planetdecred/dcrlibwallet), que permite a las tres acceder a las nuevas funciones que se le agregan. Aprobado con 93% de aprobación y 38% de participación.
- la [propuesta](https://proposals.decred.org/proposals/3943bff) de @joegruff para desarrollar una aplicación de "Android Decred Address Scanner" solicitó $3 000 por el trabajo ya terminado  (la aplicación ha sido de código abierto y disponible en Google Play por una duración de un año) junto con un máximo de $6 000 para las actualizaciones necesarias y nuevas funciones. Por demanda popular en los comentarios, Joe acordó [agregar soporte de filtros compactos](https://proposals.decred.org/proposals/3943bff/comments/15) para mejorar la privacidad e incluso trabajar de forma voluntaria si se llegará a necesitar, (porque era demasiado tarde para editar la propuesta con esta función). La votación estuvo tensa ya que el apoyo se mantuvo por [debajo](https://explorer.dcrdata.org/proposal/decred-address-scanner) del 60% la mayor parte del tiempo, pero finalmente la propuesta fue aprobada con un 67% de aprobación y un 34% de participación.
- [La propuesta](https://proposals.decred.org/proposals/8a09324) de @paris_smithson para financiar la producción y el marketing de obras de arte para [WhyDecred.com](https://www.whydecred.com/) originalmente solicitó $16 800 para financiar 16 obras de arte, se editó para eliminar la solicitud en $10 000 (a $ 6 800), finalmente fue rechazada.

Consulte el [#39 de Politeia Digest](https://blockcommons.red/politeia-digest/issue039/) para obtener una revisión más detallada.

El repositorio de [decredcommunity/proposals](https://github.com/decredcommunity/proposals) se ha reorganizado para lograr una estructura más coherente. El repositorio contiene actualmente 52 actualizaciones para 13 propuestas. Envía tus actualizaciones, esto ayuda a que sean recopiladas en un solo lugar (para no estar buscando en los chats y en Reddit) y protegerse de pérdidas. (Envía mensaje a @bee en Matrix si no quieres enfrentarte a GitHub solo).

## Red
Hashrate: el [hashrate](https://explorer.dcrdata.org/charts?chart=hashrate&zoom=kgw9asu9-ki79jtll&scale=linear&bin=block&axis=time) de noviembre se abrió a ~ 226 Ph / s y cerró ~ 293 Ph / s, tocando fondo en 215 Ph / s y alcanzando un máximo de 566 Ph / s durante todo el mes. 

[Distribución de hashrate en los pools](https://miningpoolstats.stream/decred) a partir del 1 de diciembre: 

- UUPool 44%
- Poolin 35%
- easy2mine 13%
- Huobipool 2.6%
- Antpool 2%
- F2Pool 1.6%
- BTC.com 1.2%
- Luxor 1%
- CoinMine 0.02%.

Staking: [el precio medio del ticket a 30 días](https://dcrstats.com/) fue de 158.66 DCR (+6,96). El [precio](https://explorer.dcrdata.org/charts?chart=ticket-price&zoom=kgw9asu9-ki79jtll&bin=window&axis=time&visibility=true-false&mode=stepped) varió entre 139.3 y 188.9 DCR. El [monto bloqueado](https://explorer.dcrdata.org/charts?chart=ticket-pool-value&zoom=kgw9asu9-ki79jtll&scale=linear&bin=block&axis=time) por [participación](https://explorer.dcrdata.org/charts?chart=stake-participation&zoom=kgw9asu9-ki79jtll&scale=linear&bin=block&axis=time) fue de 6.09 a 6.61 millones de DCR, lo que correspondió al 49.88 al 53.64% del suministro disponible en PoS.

El precio del ticket volvió a alcanzar un nuevo máximo de 188.85 DCR, mientras que los tickets bloqueados alcanzó un máximo histórico del 53.6%.

Nodos: a lo largo de [noviembre](https://charts.dcr.farm/d/000000014/nodes?orgId=1&from=1604188800000&to=1606780800000) hubo un promedio de 114 nodos públicos y 166 nodos de dcr.farm.

Distribución de versiones promedio para noviembre: 

- 28% dcrd v1.5.2
- 20% dcrd v1.5.1 
- 13% dcrd v1.6 dev builds 
- 5% dcrd v1.5.0
- 3.4% dcrd v1.7 dev builds 
- 3% dcrd v1. 5 compilaciones de desarrollo y RC 
- 1.1% dcrd v1.4
- 12% dcrwallet v1.5.1
- 2.5% dcrwallet v1.6 compilaciones de desarrollo y RC
- 1.3% dcrwallet v1.5
- 0.8% dcrwallet v1.4
- 9% otros.

En otras noticias:

- ¡Decred network ha procesado [+500 000 bloques](https://twitter.com/decredproject/status/1324674240268898304)!
- Hay una nueva cuenta [@CoinShuffle_BOT](https://twitter.com/CoinShuffle_BOT) que tuitea las estadísticas diarias de los DCR mezclados.
- El [estudio de distribución de riqueza](https://coinmetrics.io/bitcoin-an-unprecedented-experiment-in-fair-distribution/) realizado por Coin Metrics ha encontrado que Decred es el segundo después de Bitcoin por su métrica de Factor de distribución de red (nota: NDF se basa en direcciones de billeteras y muchas direcciones pueden ser controladas por una misma persona, encuentre aquí la [discusión](https://www.reddit.com/r/decred/comments/jrsrbk/network_distribution_factor_ndf_btc_has_the/) de este tema).

## Integraciones
Bienvenido al nuevo servicio [vsp.decredcommunity.org](https://vsp.decredcommunity.org/) que se está ejecutando en la red principal del nuevo software vspd. Al momento de escribir, tiene ~ 70 tickets en vivo y ~ 30 tickets que han votado.

Los proveedores existentes de [decredbrasil.com](https://vspd.decredbrasil.com/), [99split.com](https://vspd.99split.com/) y [Stakeminer.com](https://vsp.stakeminer.com/) han lanzado instancias vspd además, sus servidores dcrstakepool figuran en [decred.org/vsp](https://decred.org/vsp/).

Al momento de escribir, tenemos un total de 5 servicios vspd de mainnet para elegir. Gracias a todos por apoyar [una forma más privada de hacer staking en DCR](https://medium.com/decred-es/una-forma-m%C3%A1s-privada-de-hacer-staking-en-dcr-36785ad54a47).

[Stakey.net](https://stakey.net/) VSP ahora publica actualizaciones de estado y soporte en [Mastodon](https://citadel.stakey.net/@support).

Staked [anunció](https://twitter.com/staked_us/status/1329173484598124546) el cierre de su VSP de Decred por falta de viabilidad económica. A partir del 8 de diciembre, Decred todavía aparece en el [sitio](https://staked.us/) y la página de [estadísticas](https://decred.staked.us/stats) de VSP donde muestra 133 usuarios activos, 308 usuarios en total y 31 tickets en vivo.

Hotbit Korea [anunció](https://twitter.com/Hotbit_Korea/status/1331412789416534017) que el 26 de noviembre se incluirían al mercado DCR / KRW.

Advertencia: los autores de la Revista Decred no tienen idea de la confiabilidad de alguno de los servicios anteriores. Haga su propia investigación antes de confiar su información personal o activos.

## Adopción
VotoLegal [utilizó](https://twitter.com/Decred_BR/status/1328848031832215553) dcrtime para registrar y marcar el tiempo de las donaciones para la campaña electoral de Brasil de 2020. Según [Geek Insider](https://geekinsider.com/decred-blockchain-for-brazil-municipal-elections/), se han rastreado más de 24 mil donaciones por un total de más de  600 mil al 19 de noviembre. ([discusión](https://www.reddit.com/r/decred/comments/jw4l9o/decred_blockchain_used_in_brazil_election/))

## Alcance
Para abordar el reto de [difundir contenido y noticias](https://www.reddit.com/r/decred/comments/jz0bq1/decred_skepticism_sunday_22_november_2020/gd9auhx/), @Exitus y otros han creado un Grupo de trabajo de marketing en Telegram para ayudar a coordinar:

> Hasta ahora, han demostrado ser una fuerza productiva y positiva. Si alguien quiere participar y agregar valor, por favor envíeme un DM.

El servidor Mastodon de Stakey.net VSP lanzó su propia cuenta de [soporte](https://citadel.stakey.net/@support) y está abierto a la comunidad Decred a través de este [enlace de invitación](https://citadel.stakey.net/invite/tZ2Cm5FX). [Mastodon](https://docs.joinmastodon.org/) es una alternativa de código abierto de microblogueo-autohospedado ante Twitter y es parte de [Fediverse](https://en.wikipedia.org/wiki/Fediverse).

Decred aparece como patrocinador en [gioui.org](https://gioui.org/).

Decred en español publicó su quinto [informe mensual de actividades](https://github.com/decredcommunity/proposals/blob/master/proposals/3c02b67/updates/20201120.md) y gastos de su segunda propuesta que finaliza en diciembre. Se publicó un [gran informe final](https://github.com/DecredES/Monthly_reports/blob/master/Final_Report_June_December_2020.md) de junio a diciembre junto con la [3ª propuesta](https://proposals.decred.org/proposals/350f64b) para continuar su gran esfuerzo.

Blockchain Learning Challenge (coorganizado por Decred en español y Talent Land Network) tuvo 6 proyectos que llegaron a la final. Los participantes publicaron el código fuente en GitHub y presentaron sus proyectos en breves presentaciones en video. 5 jueces han calificado cada proyecto en 5 áreas. El resumen de las finales con todas las calificaciones y enlaces está [aquí](https://github.com/DecredES/Challenge/blob/main/Proyectos-Finalistas.md), el video del premio final está [aquí](https://www.youtube.com/watch?v=CQTitBVUMMY).

@michae2xl publicó un [informe](https://github.com/decredcommunity/proposals/blob/master/proposals/bc20f98/updates/20201203.md) de sus actividades de noviembre para la propuesta de marketing de Brasil.

### Los logros de Monde PR en noviembre:

- Creó y presentó una idea de historia para las blogs financieros y de criptografía.
- Respondió a 3 solicitudes de comentarios.
- Aseguró 2 entrevistas en los medios correspondientes.

### Cobertura de noticias por parte de Monde PR:

- @richardred apareció en el [podcast](https://www.hitechies.com/richard-red-at-decred-talks-to-pramod-dhakal/) de Hitechies hablando sobre la descentralización y el futuro de DeFi.
- @jy-p apareció en el podcast de [Crypto Conversation](https://bravenewcoin.com/insights/podcasts/how-the-decred-dex-plans-to-disrupt-the-crypto-exchange-market) hablando sobre el lanzamiento del DCRDEX.
- Un artículo en [Crypto Briefing](https://cryptobriefing.com/politicians-brazil-use-decred-record-political-donations/) con comentarios de @jy-p sobre el uso de Decred en las elecciones de Brasil, distribuido a 6 medios de comunicación, incluido [Coin Market Cap](https://coinmarketcap.com/fr/headlines/news/politicians-brazil-use-decred-record-political-donations/).
- Un artículo en [Cryptonomist](https://en.cryptonomist.ch/2020/11/19/elections-in-brazil-donations-on-blockchain/) con comentarios de @jy-p sobre el uso de Decred en las elecciones de Brasil, distribuido a 3 medios de comunicación, incluido [Bitcoin Ethereum News](https://ms.bitcoinethereumnews.com/blockchain/elections-in-brazil-donations-on-blockchain-the-cryptonomist/).
- Un artículo en [Geek Insider](https://geekinsider.com/decred-blockchain-for-brazil-municipal-elections/) con comentarios de @jy-p sobre el uso de Decred en las elecciones de Brasil.
- Un artículo en [Blockchain Latino America](https://blockchainlatinoamerica.com/blockchain/blockchain-para-donaciones-transparentes/) con comentarios de @jy-p sobre el uso de Decred en las elecciones de Brasil.
- Un artículo en [Explica.co](https://www.explica.co/ripples-waves-and-xrp-ahead-on-weekly-top-with-more-than-50-hikes/) sobre el uso de Decred en las elecciones brasileñas.
- Un artículo en [Cointelegraph](https://cointelegraph.com/news/friendliest-of-them-all-these-could-be-the-best-countries-for-crypto) con comentarios de @jy-p sobre Estados Unidos como el país más amigable con las criptomonedas, distribuido a 33 medios de comunicación, incluidos [Cointelegraph Italia](https://it.cointelegraph.com/news/friendliest-of-them-all-these-could-be-the-best-countries-for-crypto) e [Investing.com](https://www.investing.com/news/cryptocurrency-news/friendliest-of-them-all-these-could-be-the-best-countries-for-crypto-2353744).
- Un artículo en [Master of Nodes](https://mastersofnodes.com/decred-blockchain-system-implemented-in-brazil-municipal-elections) con comentarios de @jy-p sobre el uso de Decred en las elecciones de Brasil.
- @lukebp apareció en el podcast de [Digital Cash Network](https://odysee.com/@DigitalCashNetwork:c/Decred:6) hablando sobre el modelo de gobierno de Decred.
- Un artículo en [Cointelegraph](https://cointelegraph.com/news/decred-co-founder-explains-rationale-behind-bitcoin-bull-and-bear-cycles) con comentarios de @jy-p sobre los ciclos alcistas y bajistas de Bitcoin, distribuido a 17 medios de comunicación, incluidos [Cointelegraph Alemania](https://de.cointelegraph.com/news/decred-co-founder-explains-rationale-behind-bitcoin-bull-and-bear-cycles), [Cointelegraph Brasil](https://cointelegraph.com.br/news/decred-co-founder-explains-rationale-behind-bitcoin-bull-and-bear-cycles) y [Cointelegraph Italia](https://it.cointelegraph.com/news/decred-co-founder-explains-rationale-behind-bitcoin-bull-and-bear-cycles).

## Eventos
Atendidos:

- 2 de noviembre - [Blockchain Summit Latam](https://www.blockchainsummit.la/) - Internet. @elian dio una charla de “Gobernanza en protocolos públicos” sobre las similitudes y diferencias entre varias cadenas de bloques públicas y cómo se destaca Decred. ([vídeo](https://www.youtube.com/watch?v=SiMoxHS8AAk&list=PLiJAJqCfjxwIR6q1W0bidE9W4369KMjzz))
- 5 de noviembre - [Hablemos Decred No.- 20](https://twitter.com/Decred_ES/status/1323671501212684288) - Internet. @elian y Fernando Quiros de Cointelegraph en español hablaron sobre los posibles casos de uso de la tecnología blockchain y las criptomonedas en el contexto del periodismo, la comunicación y la publicidad. ([vídeo](https://www.youtube.com/watch?v=V1tl600djBA))
- 9 de noviembre - [Talent Land Latinoamerica](https://talentland.talent-republic.tv/) - Internet. @adcade, @elian, @francov_ y @pablito hablaron sobre “Nuestro dinero, nuestras reglas: Dejando atrás las monedas nacionales”. ([vídeo](https://www.youtube.com/watch?v=B0tEYQ2l_RM))
- 12 de noviembre - [Hablemos Decred No.- 21](https://twitter.com/Decred_ES/status/1326279642169348096) - Internet. Se unió al invitado Cristóbal Pereira (CEO LatAmTech) para recapitular Blockchain Summit Latam y discutir las perspectivas para el ecosistema de Latam. ([vídeo](https://www.youtube.com/watch?v=sTaghDgY5k8))
- 19 de noviembre - [Hablemos Decred No.- 22](https://twitter.com/Decred_ES/status/1328819770876162049) - Internet. El invitado fue Joaquín Moreno para discutir el tema "Empresas que compran Bitcoin, ¿estás list@?". ([vídeo](https://www.youtube.com/watch?v=N2hxP8I6hbM))
- 19 de noviembre - [Universidad de El Salvador](https://twitter.com/addcade/status/1329605293081288709) - Internet. @adcade habló con estudiantes de la facultad de economía sobre criptomonedas, Decred, gobernanza y oportunidades de contribución. Fue una conferencia de 2 horas con 77 personas, extendida a +1 hora con ~ 45 personas.
- 27 de noviembre - [Hablemos Decred No.- 23](https://twitter.com/Decred_ES/status/1331372082354130946) - Internet. @caibarrad de Decred en español y el invitado Felipe Montoya discutieron las similitudes y diferencias entre "DLT" y cripto. ([vídeo](https://www.youtube.com/watch?v=tu5OqKQhSbk))
- 28 de noviembre - [Acuerdo de colaboración con OMJD](https://decredcommunity.github.io/events/index/20201128.1) - Casablanca, Marruecos. Luego de una reunión en línea con la Organización Marroquí de Jóvenes Decisores (OMJD) en julio, @arij firmó un acuerdo de 2 años con ellos para realizar reuniones, talleres y conferencias sobre Decred y la tecnología blockchain en beneficio de los jóvenes.

Tenga en cuenta que los eventos de Decred en español son anunciados por [Cointelegraph en español](https://es.cointelegraph.com/tags/decred).

Nuestro [repositorio de eventos](https://github.com/decredcommunity/events) que sirve como fuente para los datos de eventos anteriores se actualizó con una nueva "tecnología". Ahora la información clave sobre los eventos se guarda en [archivos YAML](https://github.com/decredcommunity/events/tree/master/index) (en su mayoría legibles por humanos) y requiere escribir menos prosa que los [informes completos](https://github.com/decredcommunity/events/tree/master/reports). Tal estructura nos permite generar un sitio web donde cada evento tiene un [enlace bonito con todo lo relacionado](https://decredcommunity.github.io/events/index/). Esto debería ayudar a informar y compartir. Para que su evento aparezca en la lista, [siga estos pasos](https://github.com/decredcommunity/events/blob/master/docs/submit-index.md).

## Media
Articulos seleccionados:  (Inglés)
- Polkadot governance overview por @richardred ([blockcommons.red](https://blockcommons.red/crypto-governance-research/overviews/polkadot/))
- Uniswap/SushiSwap governance overview por @richardred ([blockcommons.red](https://blockcommons.red/crypto-governance-research/overviews/uniswap/))

Videos: (Inglés)
- Decred bi-weekly news update — New 1.6 release is inbound & DEX is live! por @Exitus ([youtube](https://www.youtube.com/watch?v=mYfOr4e9MZ8))
- Decred bi-weekly news update — Development progress, staking participation all-time high — and more! por @Exitus ([youtube](https://www.youtube.com/watch?v=13YGyb27z5E))
- Decred — The hybrid blockchain por Decred Society ([youtube](https://www.youtube.com/watch?v=dszDzH0OlEo))
- Luke Powell on Decred governance, hybrid consensus, and new decentralized treasury on the Digital Cash Network ([youtube](https://www.youtube.com/watch?v=4_EafyDcJvk), [odysee.com](https://odysee.com/@DigitalCashNetwork:c/Decred:6), [anchor.fm](https://anchor.fm/digitalcashnetwork))
- Interview with Permabull Niño (@PermabullNino) por Staked Podcast ([youtube](https://www.youtube.com/watch?v=nRryWFk_l7k))
- Interview with Le_Hibou_ (@Frenchy_LeDegen) por Staked Podcast ([youtube](https://www.youtube.com/watch?v=N5BnEB6MDLs))
- Interview with L.O.L. DEFI (@loldefi) por Staked Podcast ([youtube](https://www.youtube.com/watch?v=eqpafR0E1SA))
- Crypto Convo — Eduardo Lima of the Staked Podcast junto DubDigital ([youtube](https://www.youtube.com/watch?v=ErezLZ-SG5o))

- La versión de "solo audio" de Staked Podcast está disponible en [anchor.fm](https://anchor.fm/staked-podcast). ¡Felicitaciones por alcanzar las [1,000 descargas / transmisiones!](https://twitter.com/stakedpodcast/status/1326856050465792008)

Audio:
- Hitechies Podcast — Richard Red y Pramod Dhakalrr hablan sobre los desafíos de DeFi, ETH, la industria bancaria, el futuro de los sistemas de pago y más. ([hitechies.com](https://www.hitechies.com/richard-red-at-decred-talks-to-pramod-dhakal/))
- Crypto Conversation 074 — Cómo Decred DEX planea interrumpir el mercado de intercambio de crypto con @jy-p ([bravenewcoin.com](https://bravenewcoin.com/insights/podcasts/how-the-decred-dex-plans-to-disrupt-the-crypto-exchange-market), [youtube](https://www.youtube.com/watch?v=i3LQza2sYNQ))
- Decred in Depth 33: Seth Simmons en DCR + privacidad de Monero ([libsyn](https://decredindepth.libsyn.com/seth-simmons-dcr-monero-privacy))
- Rough Consensus 12: Bitcoin ha entrado al mercado chino. Los muchachos de @ck_SNARKs, coanfitrión de @POVCryptoPod y Bitcoin Magazine, para discutir la adopción de Bitcoin, las lecciones de los ciclos de auge y caída de las altcoin, el papel del precio dentro del espacio de las criptomonedas y más. (libsyn)
- Rough Consensus 13: Autonomía y libertad digital. Spiderman se une a Frank Braun (@thefrankbraun) en una amplia conversación que cubre: sociedades digitales cypherpunk, privacidad y libertad en la era digital, el papel de BTC, DCR, Scrit y otros en un futuro más brillante. ([libsyn](https://roughconsensus.libsyn.com/episode-12-bitcoin-has-entered-the-china-shop-w-ck_snarks))

### Arte y Diversión
- Decred DAO space invitation [poster](https://twitter.com/exitusdcr/status/1324430999212744704) por @Exitus.
- [Swiss Army Knife](https://twitter.com/_Checkmatey_/status/1324835192100413441) of sound money por @Checkmate.
- [Hidden Hydra](https://twitter.com/New_Copernicus/status/1333518011861372928) teaser clip por @New_Copernicus.
- Echa un vistazo a los diseños de merchandising de OfficialCrypto en [Redbubble](https://officialcryptos.redbubble.com/) (¿sabías que el logotipo de Decred coincide perfectamente con el ["Real Defi"](https://twitter.com/OfficialCryptos/status/1325421754777526272))?

### Traducciones:
- Cómo aprendí a dejar de preocuparme y amar el DCRDEX— [en español](https://medium.com/decred-es/c%C3%B3mo-aprend%C3%AD-a-dejar-de-preocuparme-y-amar-el-dcrdex-74e4ecf7bf70) por @francov_
- Monero y Decred son el nuevo Bitcoin — [en español](https://github.com/DecredES/traducciones/blob/master/Monero-y-Decred-son-el-nuevo-Bitcoin.md) por @francov_
- La utilidad de los criptoactivos — [en español](https://github.com/DecredES/traducciones/blob/master/La-utilidad-de-los-criptoactivos.md) por @francov_
- La revista Decred octubre 2020 [fue traducida](https://xaur.github.io/decred-news/) al arabé (@arij, @abdulrahman4), Chino (@Dominic), español (@francov_) and vietnamita (@duyenemdo). Los lectores vietnamitas también pueden ponerse al día con los eventos de agosto. ¡Gracias a todos por su trabajo continuo!

- Si traduces contenido de Decred, ven a saludar a la sala de [#translations](https://chat.decred.org/#/room/#translations:decred.org).

## Discusiones en la comunidad
Reddit:

- [Forward Thinking - Sábado 14 de noviembre](https://www.reddit.com/r/decred/comments/jtx4y2/forward_thinkingsaturday_14_november/).
- Creando [direcciones multifirma](https://www.reddit.com/r/decred/comments/jvhxea/how_to_create_a_decred_multisig_wallet/)
- Una colección de [ideas de marketing](https://www.reddit.com/r/decred/comments/jx989d/tiny_marketing_ideas/) por parte de u / oiezz y otros.
- Por qué [ofuscar](https://www.reddit.com/r/decred/comments/k39r3v/not_showing_result_of_a_votation_before_it_ends/) los votos es una mala idea.
- Aplicabilidad de los [lenguajes de nivel superior](https://www.reddit.com/r/decred/comments/k3ioxi/how_feasible_is_to_implement_a_scripting_language/) como Miniscript, Minsc o RGB a Decred.

Twitter:

- El [diagrama de flujo de valor](https://twitter.com/PermabullNino/status/1323330573444632576) de @ PermabullNino en dcrdex muestra por qué no es necesario inyectar un token en el proceso comercial.
- El [hilo](https://twitter.com/withdecred/status/1325147231935098880) de Decred lleno de hechos por parte de @withdecred.

## Mercados
En noviembre, DCR cotizaba entre USD 11.71-24.78 / BTC 0.00086-0.00135. La tarifa diaria promedio fue de $18.19.

El TIE [ha demostrado una correlación](https://twitter.com/TheTIEIO/status/1334586246606319623) entre el DCR / USD en aumento y el volumen promedio de tweets de 30 días.

Se [observó](https://twitter.com/Mr_DEX89/status/1326602830053068802) en Binance un extraño aumento de pánico de hasta 0.00075 BTC.

El 12 de noviembre @jy-p [informó](https://matrix.to/#/!mlRZqBtfWHrcmgdTWB:decred.org/$ZPdL5sG-IwT034pc7FldzbijUOjAe3u0ja1OkcabU_g) que el DEX había negociado 191K DCR en total. Esto tiene un promedio de 10 BTC / día.

Aquellos que deseen echar un vistazo al DCRDEX sin instalar nada pueden consultar la [transmisión](https://www.youtube.com/channel/UCSxEsULY1DUBsjdkZTbkKRA) 24/7 en YouTube.


## Noticias Relevantes
Se [descubrió](https://www.reddit.com/r/bsv/comments/jq9jv3/and_its_gone_popular_bsv_multisig_provides_no/) que el reemplazo de P2SH en la billetera Electrum de BSV estaba "roto", lo que permitía a cualquiera gastar monedas guardadas en hashes multi-sig en la cadena BSV.

El protocolo Value DeFi fue [hackeado](https://rekt.ghost.io/value-defi-rekt/) por $7 millones, aunque el atacante devolvió $2 millones a la dirección del contrato por razones desconocidas. El exploit se ejecutó con un préstamo flash, que se produjo en menos de 24 horas después de que Value DeFi tuiteara (ahora eliminado) para presumir de una seguridad sólida con “prevención de ataques de préstamos flash”.

La moneda estable OUSD fue [hackeada](https://medium.com/originprotocol/urgent-ousd-has-hacked-and-there-has-been-a-loss-of-funds-7b8c4a7d534c) con un préstamo flash utilizado para realizar un ataque de reentrada, para imprimir y rebasar (degradar) OUSD equivalente a casi todo el suministro circulante, lo que permite al hacker extraer $ 7 millones en valor.

También se utilizó un flash loan para [explotar](https://decrypt.co/46575/group-uses-flash-loan-to-game-maker-protocol-governance) el sistema de gobierno de MakerDAO, pidiendo prestados tokens MKR por un valor de $7 millones, usándolos para votar antes de reembolsar inmediatamente el préstamo. La [respuesta de MakerDAO](https://forum.makerdao.com/t/urgent-flash-loans-and-securing-the-maker-protocol/4901) ha sido deshabilitar ciertas funciones ejecutivas en caso de que un atacante pueda acceder a ellas, y extender el período de reflexión durante el cual la comunidad puede responder a propuestas inesperadas. Tal debilidad no quedaría expuesta si los titulares de MKR tuvieran que bloquear los tokens durante algún tiempo para poder votar, o si la cantidad de MKR disponible para pedir prestado fuera menor que la cantidad legítimamente comprometida en el sistema de gobierno.

La implementación del fork ligero de las firmas Schnorr y Taproot [se fusionó](https://github.com/bitcoin/bitcoin/pull/19953) con Bitcoin Core en octubre, pero hasta el momento no hay algún acuerdo sobre el método para [activar](https://www.coindesk.com/taproot-ready-bitcoin-developers-debate-activation) el cambio en la red. También existe un [argumento](https://twitter.com/nikzh/status/1332246112196063232) de que Taproot empeorará la situación de privacidad de Bitcoin para los usuarios habituales al introducir otro esquema de direcciones. Taproot agregará un nuevo tipo de firma Schnorr, que permitirá una mayor flexibilidad con billeteras de múltiples firmas y que estas transacciones se vean igual a las transacciones regulares.

El contrato de depósito en cadena de balizas Ethereum 2.0 se [lanzó](https://www.coindesk.com/ethereum-2-0-contract-deposit-mainnet) a principios de noviembre y alcanzó el objetivo de 540 000 ETH depositados el 24 de noviembre, y los 150 000 ETH finales se entregaron a tan solo unas horas antes de la fecha límite establecida para el lanzamiento del 1 de diciembre. La cadena de balizas es la primera de las 4 fases del lanzamiento y la migración a Ethereum 2.0, en esta forma inicial, el único propósito de la cadena es garantizar que los validadores de PoS puedan permanecer en consenso.

La última bifurcación (Fork) dura de Bitcoin Cash [se produjo](https://www.coindesk.com/bitcoin-cash-has-split-into-two-new-blockchains-again) en noviembre, esta vez el foco de la disputa es la financiación para los desarrolladores de ABC. Esta guerra de hash tuvo un claro [ganador](https://abc.coin.dance/blocks/hashrate), con la cadena BCHN (sin fondos de desarrollo) atrayendo prácticamente todo el poder de la minería. Antes de la bifurcación (Fork), [se observó](https://twitter.com/philip_gradwell/status/1326452365004861440) que más de 1 millón de BCH se movían en intercambios.

El 11 de noviembre, la red de Ethereum experimentó una [interrupción](https://www.coindesk.com/ethereums-hard-fork-disruption). Una versión reciente del software del nodo Geth corrigió silenciosamente un error de consenso que estuvo inactivo durante más de un año. Dado que cambió el código de consenso, tenía el riesgo de un hard fork no deseado. Un proveedor descubrió el error de forma independiente y al notar que la mayoría de los nodos se habían actualizado, decidió probarlo [en producción](https://twitter.com/jinglanW/status/1326651349912719360) y ver qué pasaba. Para sorpresa de todos, entre la minoría de nodos que ejecutan software antiguo estaba Infura, un proveedor de servicios popular utilizado por "dapps" para sincronizar con la red Ethereum. La transacción que provocó errores detuvo a Infura y un montón de aplicaciones financieras "descentralizadas" que dependían de ella, incluidas Metamask, MakerDAO, Uniswap, Compound y otras. Binance y otros intercambios también han detenido el comercio después de notar historiales de transacciones en conflicto. Infura resolvió el problema en unas horas y publicó [un informe](https://blog.infura.io/infura-mainnet-outage-post-mortem-2020-11-11/) en la que explicaba por qué no se actualizaron y señalaba el peligro de las correcciones por consenso silencioso. El desarrollador de Ethereum también [publicó para Geth](https://gist.github.com/karalabe/e1891c8a99fdc16c4e60d9713c35401f), que explicaba que la corrección se realizó en silencio para no atraer atención no deseada de los atacantes. Entre otras cosas, el incidente nos enseña que implementar soluciones críticas es un desafío ya que es un compromiso entre informar a los buenos actores y no informar a los malos.

El proyecto Aragon está en [proceso](https://aragon.org/blog/lightweight-process) de desmantelar el token ANJ que se introdujo hace un año como token para usar con “Aragon Court”, un servicio de resolución de disputas para las DAO de Aragón. El token de ANJ ahora se ve como una barrera para el éxito de Aragon Court, y los forks de ANT lo comprarán emitiendo una inflación de ~ 1–5% a los forks de ANJ.

Las autoridades estadounidenses [incautaron](https://www.coindesk.com/u-s-seized-more-than-1b-in-silk-road-linked-bitcoin-seeks-forfeiture-bloomberg) 69 370 BTC (y bifurcaciones) por un valor de alrededor de mil millones de dólares, aparentemente con el consentimiento de un hacker informático anónimo que había robado los fondos de Silk Road en 2013.

## Sobre esta edición
Este es la edición #32 de la Revista Decred, un índice de todos los números originales y traducciones se encuentran disponibles [aquí](https://xaur.github.io/decred-news/).

La mayoría de la información de terceros se transmite directamente desde la fuente después de un control de fiabilidad mínimo. Los autores de la Revista Decred no tienen la capacidad de verificar todas las reclamaciones. Tenga cuidado con las estafas y haga su propia investigación.

Puedes enviar una historia [aquí](https://github.com/xaur/decred-news/labels/next%20release) para ser considerada para el próximo número. Los [comentarios](https://github.com/xaur/decred-news/blob/docs/contributing.md#feedback) y las [contribuciones](https://github.com/xaur/decred-news/blob/docs/contributing.md) siempre son bienvenidas.

Créditos:

- Redacción y edición: adcade, bee, degeri, elian, l1ndseymm, richardred.
- Revisión y comentarios: davecgh, dnldd, jholdstock, JoeGruff, lukebp.
- Imagen de portada: saender.
- Fondeado por: El fondo de tesorería de Decred.
