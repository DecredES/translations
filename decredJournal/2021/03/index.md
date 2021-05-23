# Revista Decred Marzo 2021

![portadamarzo2021](./assets/202103.png)

## Lo más destacado de marzo:
- El voto de consenso para habilitar el nuevo sistema del fondo de tesorería ha sido aprobado y debería activarse el día 7 de mayo, momento en el que los nodos que ejecutan software anterior a la v1.6 se bifurcarán fuera de la red.
- v1.6.2 se lanzó a principios de abril, donde se soluciona una serie de problemas con la mezcla y los tickets VSP, además de mejorar la estabilidad de los nodos SPV, entre otras mejoras.
- ¡La migración épica de Politeia a un nuevo back-end de almacenamiento más flexible y escalable, que ha estado en progreso durante más de un año, finalmente se ha completado!

- La comunidad de Decred se ha decidido por un animal espiritual para el proyecto, ¡el majestuoso Bison!

### Contenido:

- [Se acerca la bifurcación](https://github.com/DecredES/traducciones/blob/master/revista-decred/2021/202103.md#se-acerca-la-bifurcaci%C3%B3n)
- Desarrollo
- Comunidad
- Gobernanza
- Red
- Integraciones
- Alcance
- Eventos
- Medios
- Discusiones de la comunidad 
- Mercados
- Noticias Relevantes
- Sobre esta edición

## Se acerca la bifurcación
La votación de consenso para habilitar el nuevo sistema del fondo de la tesorería ha [pasado](https://explorer.dcrdata.org/agenda/treasury) y las nuevas reglas se activarán alrededor del 7 de mayo. Los nodos anteriores a la v1.6 dejarán de sincronizarse, así que actualiza tu nodo para permanecer en la red. Puedes realizar un seguimiento de los días que quedan [aquí](https://voting.decred.org/).
La última versión v1.6.2 tiene correcciones para varios errores con el staking y la mezcla de VSP, así como una operación del SPV mejorada. Ve las notas de la versión completas y las descargalas [aquí](https://github.com/decred/decred-binaries/releases/tag/v1.6.2), y no olvides [verificarlas](https://docs.decred.org/advanced/verifying-binaries/) antes de instalar.

## Desarrollo
El trabajo que se informa a continuación tiene el estado "fusionado con el maestro" a menos que se indique lo contrario. Significa que el trabajo se completa, revisa e integra en el código fuente para que los usuarios avanzados puedan construir y correr, pero aún no está disponible en binarios para usuarios regulares.

#### dcrd
Combinado en master y la versión v1.6.2:
- solo envíe anuncios de bloqueo rápido a pares de nodos completos y no los envíe a clientes livianos que no pueden manejarlos correctamente. Esto mejora la estabilidad de la conexión SPV y, como resultado, las billeteras SPV deberían necesitar menos escaneos.

La principal adición del mes es el nuevo paquete para manejar direcciones estándar que es más fácil de seguir y usar que el código que reemplaza. También es más genérico, lo que permite agregar nuevos tipos de direcciones en el futuro. Si alguna vez se ha preguntado cómo se relacionan los "scripts" y las "direcciones", o en qué se diferencia "estándar" de "consenso", consulte el nuevo y brillante `README` del paquete o siga los ejemplos y las pruebas completas para comprender completamente cómo funciona. Gracias a todos los revisores y bienvenidos a los recién llegados. ¡Siempre es bueno tener un par de ojos nuevos!

El nuevo paquete de direcciones, junto con los otros cambios combinados relacionados con las direcciones, son parte de la creación de una infraestructura y un trabajo preliminar para futuras votaciones de consenso.

Otro trabajo fusionado:
- opción para no imprimir timestamps en los registros.
- detección más precisa de la propia dirección IP para corregir algunas configuraciones UPnP.
- mayor cobertura en los test para `rpcserver` y la nueva caché UTXO.

#### dcrwallet
Combinado en master y la versión v1.6.2:

- evitar envíos de bajo costo al servidor de mezcla, que ahora están siendo rechazados.
- se corrigió el manejo de UTXO para evitar errores confusos de "saldo insuficiente" cuando el saldo restante es suficiente para comprar un ticket más.
- actualice las opciones de voto para los tickets vspd usando el comando `setvotechoices`, si el VSP está configurado en dcrwallet settings.
- nueva comando `accountunlocked` que informa el cifrado de la cuenta y el estado de bloqueo (necesario para DCRDEX pero también útil en general).
- bandera de configuración para deshabilitar el registro en archivos.

#### Decrediton
La versión de patch v1.6.2 ha corregido varios errores y ha actualizado la biblioteca trezor-connect parcheada por Decred.

Fusionado en maestro:

- use el nuevo componente deslizante de la biblioteca pi-ui.
- resumen de saldos reorganizados.
- vista de lista de UTXO convertida a modal.
- diseño mejorado de modales relacionados con Trezor.
- proyecto actualizado a los últimos Electron 12 y Webpack 5.
- ~ 25 solicitudes de extracción concluyeron la búsqueda de 1 año para migrar la base de código a un estilo de programación React moderno con componentes funcionales, ganchos (hooks) y módulos en CSS.
- mayor cobertura de pruebas de IU.
- ~ 11 correcciones de errores.
Se fusionaron un total de 53 RP de 5 contribuyentes, cambiando 504 archivos, agregando 14 500 y eliminando 14 700 líneas de código. Sin demasiados cambios tangibles para el usuario, estos grandes números básicamente significan muchas actualizaciones de infraestructura "entre bastidores" para facilitar el desarrollo futuro.

En curso: integración de DCRDEX y actualizaciones de diseño.

#### Politeia

Una migración épica a un backend de almacenamiento más escalable y flexible se fusiona después de casi 1 año de desarrollo. A alto nivel nos trae lo siguiente:
- escalabilidad: ya no está restringido al sistema de archivos de una sola instancia.
- los timestamp y los datos están separados, lo que permite censurar (y eliminar) los datos sin concesiones incómodas. Tenga en cuenta que la censura solo elimina los datos, pero no el registro que prueba que el servidor lo ha visto, es decir, la "pista de auditoría" es inmutable.
- capacidad para recuperar una prueba criptográfica con sello de tiempo para cualquier dato, p. ej. un solo comentario. No había una manera fácil de hacer esto en el backend de Git.
- una arquitectura de complementos adecuada en la que se pueden extender los "registros" genéricos con timestamp con funcionalidad adicional, como comentarios o votación de tickets. Los complementos se pueden activar y desactivar en un archivo de configuración sin escribir código.
- API `politeiad` simplificada.
- `politeiawww` API reescrito para ser genérico e independiente de la aplicación, mientras que los complementos manejan rutas especializadas.
- consulte la solicitud de extracción para obtener más detalles.

Los cambios de backend y frontend reescribieron gran parte del código base de Politeia como se puede ver en las estadísticas: 51 000 líneas agregadas, 42 000 eliminadas y 474 archivos modificados.

Para los desarrolladores, la etiqueta v0.2.0 marca la última confirmación que admite el backend politeiad Git, la API politeiad v1 y gran parte de las API politeiawww `www / v1` y `www / v2`.

Todos son bienvenidos a unirse a la fiesta de prueba de la nueva versión en test-proposals2.decred.org.

Otros cambios:

El modo de goteo de la herramienta de línea de comandos politeiavoter se hizo verdaderamente aleatorio en lugar de utilizar duraciones de depósito aleatorias.

> A corto plazo, nos centraremos en el desarrollo de funciones que quedó en segundo plano durante estas actualizaciones de arquitectura. Cosas como actualizaciones de propuestas del autor, lanzar un foro similar a Reddit para la comunidad que se ejecuta en Politeia, agregar encuestas informales a las partes interesadas, etc.
A largo plazo, la idea es que Politeia se convierta en un almacén de datos configurable con timestamp que pueda servir como base para todo tipo de casos de uso. (@lukebp)

#### dcrpool
La versión candidata 2 para la próxima v1.2.0 está disponible para pruebas. Consulte las notas de la versión para obtener una lista completa de correcciones de errores, mejoras y un par de cambios importantes.

Fusionado en maestro:
- ahorro fijo de pagos archivados
- deshabilitar la interfaz de usuario de búsqueda de cuenta en grupos individuales donde no está disponible
- `--Homedir` config flag renombrado a `--appdata` para ser consistente con otro software

#### dcrlnd
@matheusd descubrió un truco interesante que permite implementar PTLC con muy pocos cambios en el código LN existente creado para HTLC.

Los PTLC (contratos puntuales bloqueados por tiempo) son un desarrollo emocionante en Lightning Network por su potencial para abordar las limitaciones de los HTLC (contratos bloqueados por tiempo hash) que se utilizan actualmente y para los nuevos casos de uso que son posibles.

El truco para habilitar PTLC fue de hecho tan simple para @matheusd que también pudo codificar una construcción interesante llamada Multi-Redeemer Transaction Tree (MRTTREE) con él, y un prototipo de donación / pago LN fuera de línea además de eso. El sistema está hecho de un dcrlnd parcheado, un servidor PoC para coordinar MRTTREEs y un Decrediton parcheado. Las matemáticas se explican en un correo electrónico a la lista de correo de Lightning-Dev y un video de presentación (la demostración de pagos LN sin conexión comienza alrededor de los 15 minutos).

El truco es experimental y necesita una investigación criptográfica seria para asegurarse de que sea seguro. Sin embargo, este trabajo es interesante en el contexto de tickets de múltiples propietarios con tecnología LN (una mejor forma de división de tickets), así como otros casos de uso habilitados por MRTTREE como donaciones fuera de la cadena y crowdfunding. A diferencia de la construcción de MRTTREE basada en HTLC mencionada en la publicación del blog original, la basada en PTLC no necesita un nuevo código de operación: el código de operación de verificación de Schnorr existente (o cualquier otro nuevo que se agregue eventualmente) es suficiente para habilitarlo.

Puede obtener más información sobre el LN de Decred en el reciente Decred in Depth con @matheusd, a partir de la marca de 28 minutos.

#### cspp
- recuento mínimo de pares configurable para servidores que desean aumentarlo para proporcionar mezclas de mayor calidad
- admite LOGFLAGS para un registro más flexible

#### DCRDEX
- capacidad para restablecer y cambiar la contraseña
- capacidad para deshabilitar la cuenta
- permitir ordenar la tabla de pedidos
- indicar estado desconectado
- admite el cifrado y el bloqueo basados en cuentas para billeteras DCR (esto será utilizado por Decrediton para bloquear solo la cuenta comercial, pero no otras)
- permitir múltiples sesiones autenticadas (para iniciar sesión en diferentes navegadores al mismo tiempo)
- enviar la estimación de tarifas más reciente al cliente para ayudar a los clientes de SPV, mejorar las estimaciones de pedidos y reforzar la seguridad
- enviar datos de transacciones sin procesar para acomodar a los clientes de SPV que no tienen un mempool y están en la oscuridad hasta que se extrae el tx de un contrato (esto también hace que el proceso sea más sólido contra la propagación deficiente de tx en la red)
- Arnés de simnet de Ethereum para pruebas durante el desarrollo
- fundamentos para el soporte de Bitcoin Cash
- Se agregaron versiones de la base de datos y se generaron datos comerciales históricos (volúmenes, máximos y mínimos, etc.)
- actualizado para usar Webpack 5 y otros módulos más nuevos
- dex.decred.org actualizado con nuevas imágenes geniales por @ 30000fps

Se fusionaron un total de 25 RP de 6 contribuyentes, agregando 22 000 y eliminando 9 000 líneas de código.

En progreso: soporte de Ethereum, un nuevo protocolo de registro (más robusto + admite pagos de tarifas en activos arbitrarios), integración de Electron de demostración y muchas otras mejoras.

Se agradecen enormemente los comentarios de los expertos de Ethereum sobre los swap contracts utilizados.

Consulte los hitos v0.2 y v0.3 para realizar un seguimiento del progreso de las próximas versiones.

#### dcrios
En curso:
- mostrando propuestas de Politeia
- implementación de mezcla
- actualización de dcrlibwallet a los últimos módulos Decred y solucion a problemas de sincronización

#### godcr
- nueva interfaz de usuario para la página Enviar
- interfaz de usuario actualizada para las páginas de descripción general y cuenta
- agregada página "Acerca de"
- agregado staking y otra información a la página de detalles de la cuenta
- entradas de texto modificadas
- página de depuración con registros
- iniciar la sincronización al iniciar la aplicación después de ingresar la frase de contraseña
- solicitar una frase de contraseña al sincronizar una billetera restaurada para permitir la generación de direcciones
- limpieza de código y corrección de errores

En curso: página de propuestas de Politeia y más trabajo en la interfaz de usuario.

#### dcrdata
- limitar la cantidad de direcciones permitidas en las solicitudes POST

#### dcrdevdocs
- La página de extensiones de script se movió de dcrdocs

#### decred.org
- enumerar las instancias de vspd en la página de VSP
- página de intercambios actualizada

#### Escáner de direcciones decred
- repositorio de código movido a organización decred
- licencia cambiada a ISC para cumplir con los requisitos de F-Droid
Además de Google Play y la descarga directa de APK, ¡la aplicación ahora también está disponible en F-Droid!

#### Decred Mapper
@jholdstock ha lanzado un sitio web con un mapa mundial de nodos y recuentos de cada agente de usuario. El código fuente está disponible aquí. La versión de Testnet del sitio está aquí. Los barbas grises de Unix disfrutarán del tema 386.

#### Ticket Splitting
@bee ha compilado un documento completo con todo el conocimiento reciente sobre división de tickets y software v1.6. Conclusiones clave:
- la solución de división de tickets existente funcionará con el software v1.5.2 hasta el 7 de mayo de 2021, cuando dejará de sincronizarse.
- todo el mundo está de acuerdo en que es bueno tener tickets splitting, pero actualmente no hay recursos de sobra para asignar, dada la baja demanda (81 split tickets - por mes es aproximadamente el 0.2% de todos los tickets)
- la fruta? más baja es parchear el cliente para admitir la nueva autenticación en dcrwallet v1.6
- esta es una buena oportunidad para que los nuevos desarrolladores se familiaricen con Decred y, al mismo tiempo, hacer que Decred staking sea más asequible

#### Otro:
- decredpower.com recibió un montón de nuevos enlaces y ajustes de diseño
- El programa Bug Bounty informó que ha procesado un total de 157 envíos y 15 eran elegibles para un pago. ¡Felicidades a @proabiral que ha sido incluido en el Salón de la Fama!

![salóndelafama](./assets/famous.png)

## Comunidad
Damos la bienvenida a los nuevos colaboradores con código fusionado de la rama principal ¡@tuhalang ([godcr](https://github.com/planetdecred/godcr/commits?author=tuhalang))!
Estadísticas de la comunidad a partir del 2 de abril:
- [Twitter](https://twitter.com/decredproject): 43 628 (+706)
- Suscriptores en [Reddit](https://www.reddit.com/r/decred/): 10 797 (+238)
- Usuarios en la sala #general de [Matrix](https://chat.decred.org/): 407 (+25)
- Usuarios en [Discord](https://discord.com/invite/GJ2GXfz): 1 409 (-35)
- Usuarios en [Telegram](https://t.me/Decred): 2 594 (+76)
- Suscriptores en [YouTube](https://www.youtube.com/channel/UCJ2bYDaPYHpSmJPh_M5dNSg): 4 460 (+40), visualizaciones: 179 000 (+4 000)
- Estrellas en el repositorio [dcrd](https://github.com/decred/dcrd) en GitHub: 589 (+5), forks: 255 (+3)

Cambios inusuales detectados entre un[ ~ 90 de cuentas](https://github.com/decredcommunity/social-media-stats) rastreadas:

- Twitter, Reddit y Telegram tuvieron otro mes de buen crecimiento
- [CoinGecko](https://www.coingecko.com/en/coins/decred) obtuvo +409 me gusta (hasta 9 516) desde mediados de marzo cuando comenzamos a rastrearlo
- La cuenta de [@decredproject](https://gab.com/decredproject) en Gab tiene 11 meses, pero todavía tiene 7 seguidores. Cualquier esfuerzo de divulgación es bienvenido para ayudarlo a crecer.
- [@Checkmate](https://twitter.com/_Checkmatey_), también conocido como "The Machine", ganó +1 816 seguidores (+ 35% a 7 042), publicando otros 1000 tweets a ~ 34 tweets por día.
- [@PermabullNino](https://twitter.com/PermabullNino) ganó +398 seguidores (+ 13% a 3 391)
- [@ConsensusRough](https://twitter.com/ConsensusRough) obtuvo un sorprendente aumento del 34% de seguidores (a 580)
- [@decredbr](https://t.me/decredbr) TG obtuvo un aumento del 6% de usuarios (a 384)
- [@Decred_ES](https://twitter.com/Decred_ES) TW obtuvo un aumento del 5% de seguidores (a 1365)
- [DECRED BRasil](https://web.facebook.com/groups/decredbrasil/?_rdc=1&_rdr) FB tuvo una caída notable en las publicaciones de 30 días de ~ 50 a 19

Los puntos anteriores son los aspectos más destacados, pero puede ver los informes completos de [marzo](https://decredcommunity.github.io/social-media-stats/posts/20210407.1) y [febrero](https://decredcommunity.github.io/social-media-stats/posts/20210306.1) en un nuevo lugar dedicado (*donde por fin estan * todos * mis números: @bee*).

¡Gracias a los embajadores de Decred en todas las plataformas por dar a conocer el proyecto!

## Gobernanza

En marzo, el fondo de la [tesorería](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx) recibió 11 531 DCR y gastó 4 196 DCR sin embargo, 3 010 de esto se retrasaron en el pago de las facturas de enero, por lo que el monto pagado por las facturas de febrero fue de solo 1 184 DCR.. Utilizando la tasa promedio diaria DCR/USD en marzo de $161.01, esto es $1.86 millones recibidos y $676 000 gastados . A la tasa diaria promedio de febrero son $135 000 para febrero (a $ 113,76) y pagos retrasados de $163 000 para enero (a $54,25). A partir del 4 de abril el balance del fondo de tesorería es de 663 658 DCR (124 millones de dólares a 187.04 dólares)

En marzo se publicaron tres propuestas: 
- La [propuesta](https://proposals.decred.org/proposals/e1cda44) de Moderación 2021 estimó un presupuesto de $8,800 (máximo $16,500) para el año, y fue aprobada con un apoyo del 93,4% y una participación del 36%.
- La [propuesta](https://proposals.decred.org/proposals/76eba5a) de Diseño para cubrir el resto de 2021 solicita un máximo de $58.850, y reportó un gasto insuficiente en la propuesta anterior, de modo que solo se utilizó el 60% de su presupuesto. La mayor parte de la infrautilización está asociada con los subdominios de identidad y comunicación visual. El informe del registro de trabajo de la propuesta anterior se publicó [aquí](https://github.com/decred/dcrdesign/issues/252).
- La [propuesta](https://proposals.decred.org/proposals/95a1409) de contenido de video (fase 3) está pendiente de renovación con un presupuesto máximo de $18,800 por otros 6 meses y 2 nuevos contribuyentes (@karamble y @DecredSociety). Durante la fase anterior solo se utilizó el 41% del presupuesto.

@bee publicó una lista de todas las propuestas [aprobadas activas](https://decredcommunity.github.io/proposals/approved) para rastrear las que vencen pronto.

El [Issue 41](https://blockcommons.red/politeia-digest/issue041/) de Politeia Digest tiene más detalles sobre las propuestas del mes.

## Red
Hashrate: el [hashrate](https://explorer.dcrdata.org/charts?chart=hashrate&zoom=kln9bt1o-kn255ihw&scale=linear&bin=block&axis=time) de marzo se abrió a ~410 Ph/s y cerró ~ 496 Ph/s, tocando fondo en 228 Ph/s alcanzando un máximo de 620 Ph/s durante todo el mes.
Distribución del hashrate [reportada](https://miningpoolstats.stream/decred) en los pools a partir del 1 de abril:
- Antpool 37%
- Poolin 29%
- F2Pool 10%
- Easy2Mine 8%
- Luxor 1.3%
- BTC.com 1.3%
- Coinmine 0.04%
- UUPool 0.04% 
- otros 13%.

Distribución de 1 000 bloques [minados](https://miningpoolstats.stream/decred) antes del 1 de abril:
- Poolin 30%
- Antpool 27%
- F2Pool 8%
- Easy2Mine 4%
- Luxor 2%
- BTC.com 1.6%
- Coinmine 0.1%
- otros 27%.

El hashrate informado de UUPool ha caído desde el punto superior al inferior y parece que sus mineros han migrado a Antpool y F2Pool. 

### Staking: 
el [precio del ticket](https://explorer.dcrdata.org/charts?chart=ticket-price&zoom=kln9bt1o-kn255ihw&bin=window&axis=time&visibility=true-true) varió entre 154.3 y 221.5 DCR, con un precio [medio](https://dcrstats.com/) del ticket a 30 días de 178.0 DCR (-3.7).En los primeros 3 meses del 2021, el precio del ticket tuvo la oscilación más alta desde que el algoritmo de precios cambió en 2017, oscilando entre ~ 150 y ~ 220.

El [monto bloqueado](https://explorer.dcrdata.org/charts?chart=ticket-pool-value&zoom=kln9bt1o-kn255ihw&scale=linear&bin=block&axis=time) por [participación](https://explorer.dcrdata.org/charts?chart=stake-participation&zoom=kln9bt1o-kn255ihw&scale=linear&bin=block&axis=time) fue de 7.10 a 7.46 millones de DCR, lo que correspondió al 56.0% a 58.7% del suministro disponible en PoS. -nuevamente se batió máximos históricos.

### VSP:
El 1 de abril, los servidores vspd tenían 6.6 mil tickets en vivo y los servidores antiguos de dcrstakepool, 4 mil. En comparación con el 1 de marzo, más de 2 200 tickets se han migrado al nuevo sistema vspd. Los VSP antiguos han informado de 11 mil usuarios activos y 22 mil usuarios en total. Todos los VSP juntos (17 antiguos, 11 nuevos) tenían el 26% del grupo de tickets.

Nodos: a lo largo de marzo hubo alrededor de 215 nodos accesibles según [dcrextdata](https://dcrextdata.planetdecred.org/nodes).

Versiones de nodos a partir de [snapshot](https://nodes.jholdstock.uk/user_agents) del 1 de abril (247 en total, solo dcrd):
- 32% v1.6.1 
- 32% v1.6.0 
- 10% v1.5.1 
- 8% v1.5.2 
- 8% v1.7 dev builds 
- 6% v1.6 dev builds 
- 2.4% v1.5.0
- 1.2% v1.6.2

La proporción de [monedas mixtas](https://explorer.dcrdata.org/charts?chart=coin-supply&zoom=kln9bt1o-kn255ihw&bin=day&axis=time&visibility=true-true-true) ha crecido del 39% a 44%. La [cantidad de mezcla](https://explorer.dcrdata.org/charts?chart=privacy-participation&zoom=jzuht6o0-knjjoqo0&bin=day&axis=time&visibility=true-false) diaria varió entre 200 000 y 350 000 DCR.

El [Lightning Network](https://ln-map.jholdstock.uk/) de Decred ha visto 34 nodos (+4), 60 canales (+4) con una capacidad total de 20 DCR (+3.2), al 1 de abril.

@Checkmate compartió gráficos que muestran un aumento en los volúmenes de [transacciones](https://twitter.com/_Checkmatey_/status/1372684156908437508) (el volumen de 2021 se ve aún más dramático cuando se [ajusta](https://twitter.com/_Checkmatey_/status/1369787880776691712) para el suministro circulante) y cómo el staking de las [tarifas](https://twitter.com/_Checkmatey_/status/1375608621417996288) en la recompensa total del bloque pasó del 0.01% al 0.12% desde octubre de 2020.

@matheusd [compartió](https://www.reddit.com/r/decred/comments/m547to/not_focusing_on_split_tickets_will_affect_us/gr0in3e/) unos gráficos sobre las compras de los tickets splits [por mes](https://github.com/decredcommunity/wiki/blob/files/files/20210315.1.png) (80 en promedio, con un máximo de 127 en marzo del 2020) y por el número de [participantes](https://github.com/decredcommunity/wiki/blob/files/files/20210315.2.png) (el 4 es el más común).

## Integraciones

El VSP [decred.raqamiya.net](https://decred.raqamiya.net/) anunció que cerrará. Alrededor del 5 de abril, tenía 128 usuarios activos y 284 usuarios en total, 52 tickets en vivo y más de 20 000 tickets votados desde 2017. El VSP presentaba una interfaz de usuario personalizada, notificaciones por correo electrónico sobre tickets votados y 4 servidores de votación en 3 continentes. [La página de inicio](https://decred.raqamiya.net/) solicita no comprar tickets nuevos, pero los tickets en vivo serán compatibles hasta que se llamen todas. ¡Gracias por tu servicio!

El exchange [CexZ](https://www.cexz.ca/) [anunció](https://twitter.com/_cexz_/status/1366501324536299523) la lista de un par DCR / BTC y vino a visitar r / decred.

Advertencia: los autores de la Revista Decred no tienen idea de la confiabilidad de alguno de los servicios anteriores. Haga su propia investigación antes de confiar su información personal o activos.

## Alcance
Un nuevo [tema](https://twitter.com/BisonContent/status/1370827335973416960) de bisontes (bison) explotó en marzo, que culminó con el hecho de que las especies de DCR Bison obtengan su propia cuenta de Twitter especializada en [@BisonContent](https://twitter.com/BisonContent). La mayor parte de las investigaciones sobre bisontes se realizaron en [#trading](https://chat.decred.org/#/room/#trading:decred.org) (casi 400 menciones). Las [primeras menciones](https://matrix.to/#/!hxDOGQVaUlvoqMMcOB:decred.org/$CWpMA7avAE_gWjVVwGglZPIAxxEO-QJ1WwqfT4JfIrw) se remontan a los chats de 2019 sobre Bison Trails, una empresa de infraestructura blockchain de la ciudad de Nueva York (¡que ofrece [servicios Decred](https://bisontrails.co/decred/) ahora!). Pero la exageración realmente despegó cuando @Void y @karamble encontraron un vínculo más fuerte con Decred en un [artículo](https://www.researchgate.net/publication/281933407_Collective_decision_making_during_group_movements_in_European_bison_Bison_bonasus) de 2015 titulado “Toma de decisiones colectivas durante los movimientos grupales del bisonte europeo, Bison bonasus”.

> La coordinación del grupo y la sincronización de actividades son esenciales para mantener la cohesión del grupo durante los movimientos colectivos. Las decisiones colectivas que surgen de esta sincronización están influenciadas por factores tanto ecológicos como sociodemográficos. (…) Era más probable que se siguiera al iniciador si iba en la dirección indicada por la mayoría de las personas, *sugiriendo un proceso de votación.*

El canal de Telegram [@DCRann](https://t.me/DCRann) se creó para reflejar anuncios importantes y reducir la dependencia de Twitter.

@pavel ha compartido más [información](https://github.com/decredcommunity/proposals/blob/master/proposals/2bf72e/updates/20210313.md) sobre la ejecución de la propuesta [withDecred.org](https://proposals.decred.org/proposals/2bf72e6). En total, 11.6 DCR se distribuyeron en 5 rondas. La gente estaba bastante comprometida en Twitter incluso sin ser recompensada. Sin embargo, lograr que la gente visitara el [sitio web](https://withdecred.org/) fue un desafío, incluso con tweets patrocinados. Es más común que los usuarios de Twitter consuman rápidamente y den me gusta / retuiteen si les gusta el contenido. Con eso en mente, el contenido del sitio se redujo a una gran [lluvia de tweets](https://twitter.com/withdecred/status/1325147231935098880) en el perfil de Twitter.

Se agradecen los informes de experimentos de divulgación como el anterior, ya que ayudan a la comunidad a aprender qué funciona y qué no, y a mejorar la difusión de nuestro mensaje.

Logros obtenidos por parte de Monde PR en marzo:
- creó y lanzó 2 artículos para blogs financieros y criptográficos
- respondió comentarios para 1 artículo
- atendió 1 entrevista con los medios.

Cobertura de noticias por parte de Monde PR:
- @ jy-p apareció en el podcast de [Finance Magnates](https://www.financemagnates.com/cryptocurrency/interview/decreds-jake-yocom-piatt-on-bitcoin-blockchain-governance-dcr-more/) hablando sobre Bitcoin, la gobernanza de blockchain y DCR, difundido a 4 medios de comunicación, incluido [Tech Centry](https://techfans.co.uk/decreds-jake-yocom-piatt-on-bitcoin-blockchain-governance-dcr-more/).

Un recordatorio para todos, si tienen un tweet o contenido increíble para compartir, no duden en dejarlo caer en el chat de [#media](https://chat.decred.org/#/room/#media:decred.org) y solicitar un retweet a través de @decredproject.

![bisontes](./assets/hooves.jpg)

## Eventos
Asistidos:

- 12-14 de marzo - [Hackathon Nayarit 2021](https://decredcommunity.github.io/events/index/20210312.1) - Internet. Decred en español patrocinó el hackathon organizado por el Ministerio de Educación de Nayarit. Para preparar a los participantes, el equipo español organizó la semana de capacitación sobre Blockchain Education, que consta de 5 seminarios web. La bolsa de premios del Hackathon de $1,000 se dividió de la siguiente manera: $500 para el primer lugar, $300 para el segundo lugar y $200 divididos entre el resto de los 20 participantes que presentaron los proyectos finales. Después del hackathon se realizó una sesión de aprendizaje para que los ganadores aprendieran cómo usar Decrediton, billeteras móviles y una información general sobre cómo almacenar y usar cripto. Duró 3 horas y los ganadores tuvieron la oportunidad de hacer preguntas mientras recibían sus premios. Más detalles [aquí](https://decredcommunity.github.io/events/index/20210312.1).

- 15 de marzo - [Estado de la adopción de criptomonedas en Marruecos](https://decredcommunity.github.io/events/index/20210315.1) - Internet. @arij fue invitada a una entrevista con Tony Obiajuru de #InsideBlockchain en CryptoTvplus, donde habló sobre el estado de la adopción de criptomonedas en Marruecos y sobre Decred y su trabajo con el proyecto.

## Media

Artículos seleccionados:

- @arij de la “empresa de criptomonedas Decred” comentó a [CoinDesk](https://www.coindesk.com/crypto-is-banned-in-morocco-but-bitcoin-purchases-are-soaring) sobre el estado de la adopción de criptomonedas en Marruecos. El artículo fue traducido a más de 4 idiomas y se volvió un poco viral en las noticias electrónicas marroquíes. El gobernador del banco central de Marruecos [comentó](https://www.youtube.com/watch?v=yWLNOlKbhtc) sobre el artículo, diciendo que han reunido un comité para estudiar las criptomonedas y las monedas digitales del banco central para mantenerse al día con la innovación, que Bitcoin no es dinero porque es especulativo y no está regulado, sino en el No se puede impedir que las personas lo utilicen. Como seguimiento, el banco ha lanzado un [video](https://www.youtube.com/watch?v=38N24GrUTxY) que desalienta el uso de Bitcoin porque es demasiado arriesgado.
- La versión v1.6.1 de Decred y el "Hardfork activada por el usuario" para descentralizar el fondo de la tesorería se han mencionado en las ediciones quincenales de PoW Round-Up de f2pool en el issue de [marzo 09](https://f2pool.io/mining/pow-round-up/20210309-pow-round-up/) y de [marzo 23](https://f2pool.io/mining/pow-round-up/20210323-pow-round-up/).
- ¿Qué es Decred? por Samuel Sherwood ([exodus.com](https://www.exodus.com/blog/what-is-decred/))
### Videos:
- Entrevista a Matheus Degiovani Decred in Depth (en vivo) por @elima_iii ([youtube](https://www.youtube.com/watch?v=O6oIrRsZnMQ)) - nueva tesorería, códigos de operación, LN y más
- Tutorial de staking en Decred - [2021 actualizado] por @Salirus ([youtube](https://www.youtube.com/watch?v=olWfTqw16OQ))
- Explorando Decred y el análisis en cadena de Real Vision ([realvision.com](https://www.realvision.com/shows/the-interview-crypto/videos/exploring-decred-and-on-chain-analysis)): una entrevista con @Checkmate, puede ver una muestra gratuita en [YouTube](https://www.youtube.com/watch?v=SLr-XTqPL4s) (menciona la reducción sin precedentes de la liquidez en BTC) o el episodio completo registrándose en el sitio.
- PTLC, MRTREE y pagos LN fuera de línea por @matheusd ([youtube](https://www.youtube.com/watch?v=m1sQGHUKU7I))
- Actualización de Decred News: descentralización de la tesorería de $110 millones, votación de gobernanza en cadena, ATH de red y más por @Salirus (youtube)
- Análisis de precios de Decred - 24 de marzo de 2021 por Josh Olszewicz de Brave New Coin ([youtube](https://www.youtube.com/watch?v=5UyRni0rjHc)) - ¡Rebanadas y dados de Decred!
### Audio:
- Jake Yocom-Piatt de Decred sobre Bitcoin, gobierno de blockchain, DCR y más por Rachel McIntosh ([youtube](https://www.youtube.com/watch?v=SOoCbr51sus), versión de texto editado en [financemagnates.com](https://www.financemagnates.com/cryptocurrency/interview/decreds-jake-yocom-piatt-on-bitcoin-blockchain-governance-dcr-more/))
### Traducciones:
Se agregaron subtítulos en español a algunos de los videos del [canal](https://www.youtube.com/channel/UCJ2bYDaPYHpSmJPh_M5dNSg) más vistos: [Tutorial de cómo hacer stake](https://www.youtube.com/watch?v=m5lcm6yttEk), [Nodo completo y Tor en Raspberry Pi](https://www.youtube.com/watch?v=B-5O_GBcbV0), [Tutorial de gobernanza](https://www.youtube.com/watch?v=1QiC0btcf7E) con @Checkmate, [Decred Assembly 15 en Decred y ASIC](https://www.youtube.com/watch?v=7K2sDhyjQys), [Actualización de noticias del 14 de febrero](https://www.youtube.com/watch?v=cZx4azGOvqQ) y el reciente [Decred in Depth](https://www.youtube.com/watch?v=O6oIrRsZnMQ) con @matheusd
- La Revista Decred de febrero de 2021 se [tradujo](https://xaur.github.io/decred-news/) al árabe (@arij, @ abdulrahman4), chino (@Dominic) y español (@francov_). ¡Gracias a todos por difundir las novedades de Decred!

## Discusiones de la comunidad

Publicaciones seleccionadas de Reddit:
- [patrones extraños](https://www.reddit.com/r/decred/comments/lzr2w8/decredbitcoin_chart/) en el gráfico de precios
- una compilación de [problemas al hacer staking](https://www.reddit.com/r/decred/comments/m3k31o/161_things_ive_learned/) mixto con Decrediton v1.6.1 y cómo solucionarlas
- invitación al [torneo](https://www.reddit.com/r/decred/comments/m618sa/decred_is_in_the_2021_ultimate_crypto_tournament/) de encuestas de Twitter (y la ironía de presentarlo a una comunidad obsesionada con la tecnología de votación sólida)
- notas sobre la resistencia [cuántica](https://www.reddit.com/r/decred/comments/m6w2ue/q_re_quantum_resistance/)
- [generar](https://www.reddit.com/r/decred/comments/marjaa/generating_media_for_upcoming_consensus_vote/) contenido para la última votación de consenso (y los desafíos de correr la voz)
- La última [charla sobre precios](https://www.reddit.com/r/decred/comments/mg5hhj/has_anybody_noticed_that_decred_has_finally/) de marzo volvió a ser bastante inteligente y comparó a Decred con Python

Debates seleccionados de Twitter:
- @jy-p avanza en la dirección [opuesta](https://twitter.com/behindtext/status/1368655110449094657) al crear un sistema financiero opt-in más justo
- @ammarooni [sugiere](https://twitter.com/Ammarooni/status/1367655623698096128) hablar más sobre el valor en USD bloqueado en los tickets, porque superar los mil millones es todo un logro.
- @bochinchero ha [vinculado](https://twitter.com/TheBochinchero/status/1375072938106445824) el repunte de precios con el aumento de la participación en staking, la participación de votantes y la actividad de monedas mixtas, y señaló que la fungibilidad es fuerte cuando es masiva:

> Más del 43% del suministro de $DCR disponible ahora se mezcla y no se gasta. Algunos argumentan que optar por la privacidad o un libro de contabilidad transparente nunca pueden ser realmente fungibles ... Honestamente, no puedo pensar en un actor racional que acepte voluntariamente una moneda, pero rechace la mitad de las monedas en circulación. ([@TheBochinchero](https://twitter.com/TheBochinchero/status/1375072954493636608))

## Mercado

En marzo, DCR cotizaba entre 140.16 y 180.60 USD / 0.00275 a 0.00310 BTC. La tarifa diaria promedio fue de $161.01.

@PermabullNino [publicó](https://twitter.com/PermabullNino/status/1366915444355964932) que los datos en cadena de Decred están en modo bestia, habiendo establecido 4 veces más unidades nativas que Bitcoin en febrero.

@Checkmate ha actualizado su cuadro de [comparación](https://twitter.com/_Checkmatey_/status/1369769392884436992) de "Lindy Coins" vs Bitcoin, ya que se ha recuperado de $10 000 a $58 000. DCR sigue destacando.

## Noticias Relevantes
El gran DeFi Dumpster Fire de marzo fue PAID, que fue sometido a un [ataque](https://cointelegraph.com/news/paid-network-exploiter-nets-3-million-in-infinite-mint-attack) de acuñación infinita que vio al atacante emitirse $180 millones de PAID a sí mismos, pero aparentemente solo pudieron capturar $3 millones del valor convirtiéndolo en algo más que devaluar rápidamente ( hasta un 85% en una etapa) tokens PAID. En un [postmortem](https://paidnetwork.medium.com/paid-network-attack-postmortem-march-7-2021-9e4c0fef0e07) se explicó que el atacante obtuvo acceso a la clave privada para el implementador del contrato original y la usó para "actualizar" los contratos para que pudieran acuñar nuevos tokens. Se utilizará una instantánea para "restablecer" el token PAID para eliminar los tokens del atacante que no pudieron vender antes de ser descubiertos.

SushiSwap ha estado lidiando con un gran [dilema](https://decrypt.co/62522/defi-exchange-sushiswap-faces-an-880-million-dilemma) sobre cómo distribuir los tokens que debe a los proveedores de liquidez desde octubre del 2020, los tokens tenían un "período de adquisición" de 6 meses y la cuestión de cómo distribuirlos se planteó en enero del 2021. Ya votaron en contra de un airdrop directo de los tokens y optaron por un mecanismo de reclamo que costará las tarifas de los reclamantes, pero luego se supo que el código del smartcontract se había editado para que los usuarios que interactuaran con él ya no pudieran reclamarlo a través de terceros. Los contratos inteligentes de partes (como Harvest.finance, a cuyos usuarios se les debe entre el 5% y el 6% de estos tokens). La razón dada por los desarrolladores que implementaron esta actualización es la preocupación de que las "granjas parásitas" descarguen sus asignaciones de tokens. La última es que estas granjas pueden enviar propuestas sobre cómo distribuir sus asignaciones, para que las revise la comunidad de Sushiswap.

El protocolo de "comunicación entre cadenas de bloques (IBC)" de Cosmos ha sido [aprobado](https://www.coindesk.com/cosmos-vote-approve-inter-blockchain-communication) por los votantes de Cosmos por una gran mayoría de 112 millones a setenta y cinco, y promete permitir una comunicación segura entre cadenas de bloques que satisfagan ciertos criterios. Como Cosmos es la única cadena de bloques que admite este estándar IBC, actualmente no es muy útil, pero es probable que otras cadenas de bloques basadas en Tendermint también agreguen soporte pronto.

El EIP 1559 de Ethereum se ha incluido en el próximo hard fork de Londres, como se decidió en la [convocatoria](https://www.youtube.com/watch?v=xWfR-WxjmYg) de Core Developers el 5 de marzo. EIP 1559 cambiará fundamentalmente la forma en que se calculan y pagan las tarifas de transacción, ganando el apoyo de la mayoría de los usuarios y desarrolladores al prometer mejorar significativamente la experiencia del usuario. Sin embargo, los mineros han [manifestado](https://twitter.com/_Checkmatey_/status/1366831390424068098) su [oposición](https://www.coindesk.com/ethereum-improvement-proposal-1559-london-hard-fork) a este cambio, con más del 60% oponiéndose a él, ya que interferirá con una fuente de ingresos para ellos. El [análisis](https://insights.deribit.com/market-research/miners-will-accept-eip-1559-here-is-why/) de Hasu sugiere que los mineros lo aceptarán de todos modos, ya que aún pueden obtener una buena ganancia de las recompensas en bloque y el valor extraíble del minero (MEV), mientras que la alternativa puede interpretarse como un ataque a la red y es probable que dañe el ETH. precio (por lo tanto, el resultado final de los mineros).

La autoridad fiscal del Reino Unido ha [actualizado](https://www.coindesk.com/uk-tax-authority-updates-treatment-of-crypto-assets-to-incorporate-staking) su guía para el tratamiento de los criptoactivos para cubrir la participación por primera vez; esto debe tratarse de la misma manera que se tratan actualmente los ingresos mineros, pero puede abrir la puerta para un tratamiento diferenciado futuro.

El defensor de la privacidad @6102bitcoin [recibió](https://twitter.com/6102bitcoin/status/1367376460214853632) un informe de que Bitstamp Europe le pidió a su usuario que explicara una transacción de CoinJoin realizada con la billetera Wasabi poco después del retiro, y esa solicitud se realizó meses después de la actividad. 

Una [respuesta](https://twitter.com/thibm_/status/1367613186950766603) señaló que los operadores están presionados por los gobiernos que imponen estas reglas, como la autorización francesa DASP que solicita inspeccionar los lúpulos en cadena en ambos sentidos (entrantes y salientes).

Anteriormente, Bitstamp fue [noticia](https://cointelegraph.com/news/bitstamp-crypto-exchange-users-bemoan-additional-kyc-requirements) por pedirle a un cliente holandés que compartiera una cantidad inusual de información personal, incluido el patrimonio neto y los ingresos anuales, prueba de residencia y los orígenes de los fondos fiduciarios y criptográficos.

La cuenta de YouTube de CoinDesk se [suspendió](https://www.coindesk.com/youtube-suspends-coindesk) durante 1 día, después de lo que aparentemente fue una eliminación errónea de su canal.

Un nuevo método para cobrar criptomonedas aparentemente se ha popularizado en Rusia, el "[tesoro](https://www.nasdaq.com/articles/russias-darknet-criminals-have-novel-crypto-cash-out-system%3A-buried-treasure-2021-03-22) enterrado" o las gotas muertas de efectivo en coordenadas específicas.

## Sobre esta edición
Este es la edición #36 de la Revista Decred, un índice de todos los números originales y traducciones se encuentran disponibles [aquí](https://xaur.github.io/decred-news/).

La mayoría de la información de terceros se transmite directamente desde la fuente después de un control de fiabilidad mínimo. Los autores de la Revista Decred no tienen la capacidad de verificar todas las reclamaciones. Tenga cuidado con las estafas y haga su propia investigación.

Puedes enviar una historia [aquí](https://github.com/xaur/decred-news/labels/next%20release) para ser considerada para el próximo número. Los [comentarios](https://github.com/xaur/decred-news/blob/docs/contributing.md#feedback) y las [contribuciones](https://github.com/xaur/decred-news/blob/docs/contributing.md) siempre son bienvenidas.

Créditos (por orden alfabético)

- Redacción y edición: bee, degeri, l1ndseymm, richardred
- Revisión y comentarios: arij, davecgh, dnldd, jholdstock, JoeGruff, lukebp, matheusd
- Imagen de portada: saender
- Fondeado por: los stakeholders de Decred.

