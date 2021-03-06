# Revista Decred Septiembre 2021
![portada](./assets/DJsep.png)

Lo más destacado de septiembre:

-   Se ha completado el trabajo sobre los cambios de consenso de DCP-8 y DCP-9, están listos para ser presentados para una votación en cadena para ratificarlos.
-   Politeia se ha actualizado a v1.2, agregando características como actualizaciones de propuestas y la capacidad de hacer comparaciones entre dos versiones de una propuesta.
-   Las billetera móviles de Android e iOS vieron nuevos lanzamientos en sus respectivas tiendas de aplicaciones.
-   GoDCR alcanzó su primera construcción de red de prueba funcional, lo que demuestra lo que se ha logrado con ese proyecto hasta ahora, ya que se publicó y discutió la propuesta para la financiación continua de GoDCR.

Contenido:

- [Desarrollo](https://github.com/DecredES/translations/blob/master/decredJournal/2021/09/index.md#desarrollo)

- [Comunidad](https://github.com/DecredES/translations/blob/master/decredJournal/2021/09/index.md#comunidad)

- [Gobernanza](https://github.com/DecredES/translations/blob/master/decredJournal/2021/09/index.md#gobernanza)

- [Red](https://github.com/DecredES/translations/blob/master/decredJournal/2021/09/index.md#red)

- [Ecosistema](https://github.com/DecredES/translations/blob/master/decredJournal/2021/09/index.md#ecosistema)

- [Alcance](https://github.com/DecredES/translations/blob/master/decredJournal/2021/09/index.md#alcance)

- [Medios](https://github.com/DecredES/translations/blob/master/decredJournal/2021/09/index.md#medios)

- [Mercados](https://github.com/DecredES/translations/blob/master/decredJournal/2021/09/index.md#mercados)

- [Noticias Relevantes](https://github.com/DecredES/translations/blob/master/decredJournal/2021/09/index.md#noticias-relevantes)


**Desarrollo**
--------------

El trabajo que se informa a continuación tiene el estado "fusionado con el maestro" al menos que se indique lo contrario. Significa que el trabajo se completa, se revisa e integra en el código fuente para que los usuarios avanzados puedan [crear y ejecutar](https://medium.com/@artikozel/the-decred-node-back-to-the-source-part-one-27d4576e7e1c) pero aún no está disponible en la versión de binarios para los usuarios habituales.

### [dcrd](https://github.com/decred/dcrd)

*dcrd es una implementación de nodo completo que impulsa la red peer-to-peer de Decred en todo el mundo.*

Cambio de consenso de actualizaciones de versión explícita ([DCP-8](https://github.com/decred/dcps/blob/master/dcp-0008/dcp-0008.mediawiki)):

-   Se han [implementado](https://github.com/decred/dcrd/pull/2716) nuevas reglas de consenso. Una vez activadas, las transacciones desconocidas y las versiones de script se rechazarán hasta que se hayan habilitado explícitamente mediante otro cambio de consenso. Las monedas que se podían gastar antes de la activación seguirán siendo gastables. Este cambio proporcionará una mayor seguridad en la red y permitirá a los desarrolladores escribir más código a prueba de errores, cómo se explica en los comentarios de la [propuesta](https://proposals.decred.org/record/3a98861) [DCP-8](https://github.com/decred/dcps/blob/master/dcp-0008/dcp-0008.mediawiki) y una [discusión](https://github.com/decred/dcrd/pull/2719#issuecomment-909535320) reciente de los desarrolladores.
-   @davecgh publicó una [propuesta de actualización](https://proposals.decred.org/record/3a98861/comments/21) del trabajo completo del desarrollo de dcrd.

Cambio de consenso de revocaciones automáticas de los tickets ([DCP-9](https://github.com/decred/dcps/blob/master/dcp-0009/dcp-0009.mediawiki)):

-   [Preparativos](https://github.com/decred/dcrd/pull/2718): pruebas añadidas, definiciones de agenda añadidas, código reorganizado para adaptarse a los próximos cambios. Se introdujo una nueva prioridad de transacción para garantizar que siempre se creen revocaciones automáticas. La lista completa de prioridades se convierte en: votos (más alto)> revocaciones automáticas> tickets> transacciones regulares y revocaciones (más bajo).
-   [Implementación](https://github.com/decred/dcrd/pull/2720) en el cambio de consenso real. Una vez activados, se requerirá que los bloques contengan revocaciones para todos los tickets que se perdieron o caducaron a partir de ese bloque. Las nuevas reglas también permitirán desbloquear algunos [~ 200 mil DCR](https://github.com/decredcommunity/proposals/blob/master/proposals/e2d7b7d/docs/unrevoked-missed-tickets.md) que se atascaron en tickets perdidos no revocados.
-   @rstaudt2 publicó una [actualización de la propuesta](https://proposals.decred.org/record/e2d7b7d/comments/19) del trabajo completo de desarrollo de dcrd.

Otro trabajo fusionado:

-   Se implementó la [poda](https://github.com/decred/dcrd/pull/2641) del diario de gastos que retrasaba la eliminación de los tickets que se usaban hasta su máximo de uso (esto es necesario para la [indexación asincrónica](https://github.com/decred/dcrd/issues/1470) que acelerará la validación de bloques).
-   Se agregó más pruebas para el administrador de direcciones y el [desacopló](https://github.com/decred/dcrd/pull/2596) del paquete de cables, en preparación para los próximos cambios en el protocolo de cables.
-   Se ancló imágenes de [Docker](https://github.com/decred/dcrd/pull/2735) y [Acciones de GitHub](https://github.com/decred/dcrd/pull/2736) con hash en lugar de etiquetas para una mejor seguridad para la cadena de suministro.
-   Se modificó la compatibilidad con [Docker](https://github.com/decred/dcrd/pull/2740) para proporcionar una imagen con un fuerte enfoque en la seguridad. Solo incluye binarios específicos de Decred ("distroless") y los ejecuta como un usuario sin privilegios. La nueva imagen final es de alrededor de 10 MB, en comparación con ~ 1 GB de la versión anterior.
-   Código actualizado para usar las funciones de [Go 1.16](https://github.com/decred/dcrd/pull/2722).
-   Actualización del los módulos del gráfico de [jerarquía](https://github.com/decred/dcrd/pull/2744).

> Se está preparando un gran lanzamiento de dcrd ... que incluye 3 votos de consenso, sincronización de un 30% más rápida y mucho más. ([@rstaudt2](https://twitter.com/rstaudt2/status/1443668800679858181))

### [dcrwallet](https://github.com/decred/dcrwallet)

*dcrwallet es un servidor de billetera utilizado por aplicaciones de billetera gráfica y líneas de comandos.*

-   Se permite el procesamiento de [tarifas de VSP](https://github.com/decred/dcrwallet/pull/2058) para tickets comprados cuando el comprador de tickets (ticketbuyer) se encuentre apagado.

-   Se cambió el [límite](https://github.com/decred/dcrwallet/pull/2086) predeterminado de `ticketbuyer` a 1 ticket máximo por bloque.

-   Se permite [inhabilitar](https://github.com/decred/dcrwallet/pull/2088) el descubrimiento de cuentas (permitiendo optimizar los clientes que no lo necesitan, como dcrlnd).

-   Opción de configuración agergada para el [tamaño máximo](https://github.com/decred/dcrwallet/pull/2077) de registro antes de que se cambié.

-   Código [Go 1.16](https://github.com/decred/dcrwallet/pull/2085) actualizado junto con los últimos módulos de [dcrd](https://github.com/decred/dcrwallet/pull/2087).

-   Se corrigieron algunos problemas con el procesamiento y la confirmación de los [pagos de tarifas](https://github.com/decred/dcrwallet/pull/2083) para los tickets administrados por VSP.

-   Se puede [calcular la tarifa](https://github.com/decred/dcrwallet/pull/2057) fija para transacciones multifirma.

-   Se corrigió un posible issue de [carrera](https://github.com/decred/dcrwallet/pull/2089) en el modo SPV.

### [Decrediton](https://github.com/decred/decrediton)

*Decrediton es una aplicación de billetera para escritorio con todas las funciones que cuentan con votación integrada, mezcla de StakeShuffle, Lightning Network, comercio DEX y más. Funciona con o sin una blockchain completa (modo SPV).*

-   Se implementó un nuevo diseño de interfaz de usuario para la pestaña de los [Canales LN](https://github.com/decred/decrediton/pull/3543).
-   Se actualizó todas las frases [contraseñas](https://github.com/decred/decrediton/pull/3546) de las cuentas en el cambio de frase de contraseña privada.
-   Se corrigieron algunos problemas con la sincronización del [estado de pago](https://github.com/decred/decrediton/pull/3545) de la tarifa de VSP.
-   Se corrigieron 3 errores cuando se [crea](https://github.com/decred/decrediton/pull/3554) una billetera.
-   Se corrigieron los [errores](https://github.com/decred/decrediton/pull/3561) de VSP heredados que se muestran en el nuevo modo VSP.
-   Enlaces de [navegación](https://github.com/decred/decrediton/pull/3558) faltantes arreglados.
-   Se corrigió el [desenfoque](https://github.com/decred/decrediton/pull/3555) al restaurar una billetera Trezor.
-   Se arregló los [bloqueos](https://github.com/decred/decrediton/pull/3548) fijos causados por el procesamiento de transacciones muy grandes.
-   Se [cambió](https://github.com/decred/decrediton/pull/3553) los enviós fijos mixtos cuando estos se llevan a cabo en una dirección incorrecta.

![LN](./assets/LN.png)

### [Politeia](https://github.com/decred/politeia)

*Politeia es el sistema de propuestas de Decred. Se utiliza para solicitar financiación a la tesorería de Decred.*

¡Otra versión de función y corrección de errores ha [aterrizado](https://twitter.com/lukebp/status/1442540461244043264) en el sitio web de [Politeia](https://proposals.decred.org/)! Aspectos destacados de v1.2.0:

-   Actualizaciones del autor de la propuesta para las que sean aprobadas.
-   Comparar dos versiones de una propuesta.
-   Botón para insertar imagenes.
-   Actualizaciones optimistas de votos instantáneos para comentarios.
-   Servidor: estado de facturación de la propuesta, para formalizar si la facturación está permitida o no.
-   Servidor: estado de la propuesta unificada para simplificar los clientes.
-   Servidor: mayor seguridad y estabilidad.

Para obtener más detalles, consulte las notas de la versión en los repositorios [politeia](https://github.com/decred/politeia/releases/tag/v1.2.0) y [politeiagui](https://github.com/decred/politeiagui/releases/tag/v1.2.0).

Los cambios orientados al usuario se fusionaron en septiembre:

-   Nuevo [estado](https://github.com/decred/politeiagui/pull/2609) de propuesta integrado y capacidad de administrador para establecer el estado de facturación.
-   UX mejorada de [incrustación de imágenes](https://github.com/decred/politeiagui/pull/2567).
-   Muestre el modo de inicio de sesión cuando [expira](https://github.com/decred/politeiagui/pull/2541) la sesión del usuario.
-   Se agregaron [metaetiquetas de SEO](https://github.com/decred/politeiagui/pull/2614) para mejorar la ubicación en los resultados de búsqueda y permitir vistas previas agradables en Twitter y Facebook.
-   Diseño de [alternancia](https://github.com/decred/politeiagui/pull/2588) de modo oscuro actualizado.
-   ~ 18 correcciones de errores de GUI y ~ 3 mejoras.

Cambios en el backend, internos y en la línea de comandos:

-   Se agregó un [estado de propuesta](https://github.com/decred/politeia/pull/1515) unificado que sirve como una fuente única para los metadatos de la propuesta de diferentes complementos, lo que elimina la complejidad de los clientes y también reduce la carga en el servidor. El nuevo estado se puede consultar con el comando `pictl proposummaries`.
-   Se agregaron interfaces de alto nivel para las [comprobaciones del sistema de archivos](https://github.com/decred/politeia/pull/1512) para verificar la integridad de los datos y reconstruir las cachés al inicio. Las [implementaciones](https://github.com/decred/politeia/issues/1511) para componentes individuales se realizarán por separado.
-   Se implementó la reconstrucción de caché para el [inventario de registros](https://github.com/decred/politeia/pull/1520) cuando la verificación del sistema de archivos este habilitada con `--fsck`.
-   Se agregó una opción para guardar la salida de los resultados de la votación de `pictl` como [CSV](https://github.com/decred/politeia/pull/1478).
-   Se agregaron [tiempos](https://github.com/decred/politeia/pull/1505) de espera de lectura y escritura para los servidores `politeiad` y `politeiawww.`
-   Middleware refactorizado en servidores [`politeiad`](<https://github.com/decred/politeia/pull/1507>) y [`politeiawww`](<https://github.com/decred/politeia/pull/1506>) y límites de lectura agregados para solicitudes de clientes y mensajes WebSocket.
-   Se agregaron [tamaños de página](https://github.com/decred/politeia/pull/1518) a las respuestas de la política.
-   Documentación agregada: documentos [API exportados](https://github.com/decred/politeia/pull/1497), descripción general del sistema de [pluggin](https://github.com/decred/politeia/pull/1519) y escritura de [pruebas E2E](https://github.com/decred/politeiagui/pull/2591).
-   Se solucionó una [fuga](https://github.com/decred/politeia/pull/1500) de memoria.
-   ~ 4 otras correcciones de errores de backend.
-   Mayor cobertura de pruebas de IU de backend y de un extremo a otro.

![LD](./assets/LD.png)

### [vspd](https://github.com/decred/vspd)

*vspd es un servidor de software para ejecutar un proveedor de servicios de votación. Un VSP vota en nombre de sus usuarios las 24 horas del día, los 7 días de la semana y no puede robar fondos.*

-   [Diagrama](https://github.com/decred/vspd/pull/296) de arquitectura agregado a la [Guía de implementación](https://github.com/decred/vspd/blob/master/docs/deployment.md).
-   Manejo actualizado de los [errores](https://github.com/decred/vspd/pull/295) de dcrd.
-   [Comparación](https://github.com/decred/vspd/pull/294) de valores más fiable en las pruebas.

### [dcrpool](https://github.com/decred/dcrpool)

*dcrpool es un software de servidor para ejecutar un grupo de minería.*

-   Fue actualizado para usar las funciones de [Go 1.16](https://github.com/decred/dcrpool/pull/335).
-   Manejo fijo de bloques que se [reordenaron](https://github.com/decred/dcrpool/pull/336) fuera de la cadena.

### [dcrlnd](https://github.com/decred/dcrlnd)

*dcrlnd es el software de nodo Lightning Network de Decred. LN permite transacciones instantáneas y de bajo costo.*

-   Se agregó un interruptor para guardar [perfiles de memoria](https://github.com/decred/dcrlnd/pull/144).

### [DCRDEX](https://github.com/decred/dcrdex)

*DCRDEX es un exchange sin custodia para el trading sin confianza, impulsado por atomic swaps.*

Orientado al usuario:

-   Gráfico de [velas históricas](https://github.com/decred/dcrdex/pull/1208) añadido.
-   Reconocimiento en el parámetro de configuración [`rpcconnect`](https://github.com/decred/dcrdex/pull/1206) Bitcoin.

![adn](./assets/ADN.png)


Cambios internos y de backend:

-   Infraestructura agregada para pagar la tarifa de registro en [activos](https://github.com/decred/dcrdex/pull/1202) que no sean DCR, tarifas de registro implementadas en BTC.
-   Refactorización para la preparación del soporte de [Bitcoin SPV](https://github.com/decred/dcrdex/pull/1089).
-   [Limitación de velocidad](https://github.com/decred/dcrdex/pull/1192) más detallada para proteger contra ataques a la red.
-   Cuenta de [restauración](https://github.com/decred/dcrdex/pull/1183) optimizada desde semilla.
-   Simplificación sobre el procedimiento de cambio de [tamaño de lote](https://github.com/decred/dcrdex/pull/1212) (la cantidad mínima de trade).
-   Se puede descubrir cuentas [antes](https://github.com/decred/dcrdex/pull/1201) en el flujo (para soportar tarifas de activos múltiples).
-   Verificación simplificada de la [propiedad](https://github.com/decred/dcrdex/pull/1193) de la billetera al cambiar la configuración de la billetera.
-   Aplicación de línea de comandos de [`usermatches`](https://github.com/decred/dcrdex/pull/1213) agregada para recuperar datos de coincidencias y guardarlos como CSV.

Trabajar hacia la internacionalización:

-   Se [agregó](https://github.com/decred/dcrdex/pull/1127) soporte de traducción a la interfaz de usuario del cliente web.
-   Sistema mejorado para traducir [notificaciones](https://github.com/decred/dcrdex/pull/1197).
-   Se agregó un interruptor `dexc` para volver a traducir las plantillas sobre la marcha (permite una iteración más rápida).
-   Se añadió traducciones al [portugués](https://github.com/decred/dcrdex/pull/1185) y [chino](https://github.com/decred/dcrdex/pull/1207).

![chino](./assets/chino.png)

Cambios internos hacia el soporte de Ethereum:

-   Se agregó una herramienta para [verificar](https://github.com/decred/dcrdex/pull/1203) el contract de intercambio implementado en la red de Ethereum (se puede usar para detectar un cambio inesperado del contract).
-   Decodificación y validación agregadas de [transacciones](https://github.com/decred/dcrdex/pull/1215) mientras están en el mempool (permite fallar rápidamente antes de que se extraiga un tx mal formado).
-   Estimación implementada del [pedido máximo](https://github.com/decred/dcrdex/pull/1184) que se puede colocar en la billetera

### [Decred Wallet (Android)](https://github.com/planetdecred/dcrandroid)

¡Decred Wallet v1.6.1 ha sido lanzado en [Google Play Store](https://play.google.com/store/apps/details?id=com.decred.dcrandroid.mainnet)!

Los usuarios con mentalidad de privacidad ahora también pueden obtener el APK firmado directamente desde la [versión de GitHub](https://github.com/planetdecred/dcrandroid/releases/tag/v1.6.1).

Fusionado en septiembre:

-   Opción de configuración agregada para elegir el [tema](https://github.com/planetdecred/dcrandroid/pull/582) de la aplicación.
-   Se permite intentos de desbloqueo de billetera con una frase de contraseña [vacía](https://github.com/planetdecred/dcrandroid/pull/585).

Combinación de la biblioteca [dcrlibwallet](https://github.com/planetdecred/dcrlibwallet) (compartida por las carteras de Android / iOS y GoDCR):

-   Se agregaron varias consultas de datos para admitir la descripción general del [staking](https://github.com/planetdecred/dcrlibwallet/pull/206) de múltiples billeteras.

Consulta la nueva [propuesta](https://proposals.decred.org/record/6db3c4e) de las billeteras móviles para conocer la hoja de ruta de desarrollo para 2021--2022.

### [Decred Wallet (iOS)](https://github.com/planetdecred/dcrios)

¡Decred Wallet v1.6.1 ha sido lanzado en [App Store](https://apps.apple.com/us/app/decred-wallet/id1462247643)!

Fusionado en septiembre:

-   Implementación del [modo oscuro](https://github.com/planetdecred/dcrios/pull/812).
-   [Notificación](https://github.com/planetdecred/dcrios/pull/853) para los usuarios en donde sus cuentas no se pueden eliminar una vez creadas.
-   Se permite intentos de desbloqueo de billetera con una frase de contraseña [vacía](https://github.com/planetdecred/dcrios/pull/827).
-   ~ 5 correcciones de errores y ~ 2 ajustes de UI.

![wallet](./assets/wallet.png)

### [GoDCR](https://github.com/planetdecred/godcr)

*GoDCR es una aplicación de billetera para escritorio liviana con staking integrado, privacidad y navegación en Politeia.*

¡La primera compilación de testnet está [disponible](https://twitter.com/planetdecred/status/1441164793470087187) para vista previa! Descárguelo de la [versión de GitHub](https://github.com/planetdecred/godcr/releases) y verifique las firmas. Si planea buscar errores, se recomienda compilar a partir de la última [fuente](https://github.com/planetdecred/godcr) para tener todas las correcciones de errores recientes.

Se fusionaron los cambios orientados al usuario:

-   División de la restauración de las frases semillas en [pasos](https://github.com/planetdecred/godcr/pull/587).
-   Se agregó el enlace "[Modo avanzado](https://github.com/planetdecred/godcr/pull/614)" a la página Enviar que permite seleccionar manualmente las monedas para gastar en la transacción (esta característica de privacidad también se [conoce](https://en.bitcoin.it/wiki/Privacy#Coin_control) como "[control de monedas](https://bitcoin.design/guide/payments/send/coin-selection/#manual-coin-selection-aka-coin-control) (coin control)".
-   Se agregaron efectos de [desplazamiento](https://github.com/planetdecred/godcr/pull/586) a numerosos [widgets](https://github.com/planetdecred/godcr/pull/624).
-   Se muestra el progreso de la [reexploración](https://github.com/planetdecred/godcr/pull/629) en la descripción general.
-   UX mejorada para [crear](https://github.com/planetdecred/godcr/pull/622) billeteras y cuentas.
-   Se permite el cierre de menús [desplegables](https://github.com/planetdecred/godcr/pull/616) haciendo clic fuera.
-   Representación mejorada de [tablas](https://github.com/planetdecred/godcr/pull/529) de Markdown.
-   Búsqueda y visualización de [tickets](https://github.com/planetdecred/godcr/pull/567) refactorizados.
-   UX optimizado de los [modales](https://github.com/planetdecred/godcr/pull/626) de selección de idioma y moneda.
-   Se añadió traducción al [español](https://github.com/planetdecred/godcr/pull/521).
-   Se corrigieron los iconos [borrosos](https://github.com/planetdecred/godcr/pull/618) en resoluciones más altas.
-   ~ 7 otros ajustes de UX y ~ 17 correcciones de errores

Cambios internos y del desarrollador:

-   Edificio fijo en [FreeBSD](https://github.com/planetdecred/godcr/pull/627).
-   [Makefile](https://github.com/planetdecred/godcr/pull/628) agregado para administrar las compilaciones del sistema operativo construido.
-   Activos [incrustados](https://github.com/planetdecred/godcr/pull/620) en el binario de la aplicación.

![2511](./assets/2511.png)

En progreso:

-   Integración en el [DEX](https://github.com/planetdecred/godcr/pull/637) (basada en el [soporte](https://github.com/planetdecred/dcrlibwallet/pull/210) base en dcrlibwallet).

Consulta la segunda [propuesta de GoDCR](https://proposals.decred.org/record/f7d9fc8) para obtener una actualización de estado y la hoja de ruta 2021-2022.

### [dcrdata](https://github.com/decred/dcrdata)

*dcrdata es un explorador blockchain de Decred y datos fuera de la cadena como propuestas, mercados y más de Politeia.*

Cambios de interfaz de usuario:

-   Se implementó el gráfico de [velas](https://github.com/decred/dcrdata/pull/1854) DCRDEX en la página del [mercado](https://explorer.dcrdata.org/market?chart=candlestick&xc=dcrdex&bin=1d).
-   Se muestra las [versiones](https://github.com/decred/dcrdata/pull/1863) de la transacción y del script en la página tx.
-   Soporte agregado para el [tipo de dirección](https://devdocs.decred.org/developer-guides/addresses/) [Pay-to-Pubkey](https://github.com/decred/dcrdata/pull/1871) (P2PK).
-   [Notificaciones](https://github.com/decred/dcrdata/pull/1866) de escritorio restauradas.
-   Se agregaron [metaetiquetas de SEO](https://github.com/decred/dcrdata/pull/1870) para obtener resultados de búsqueda más bonitos y vistas previas en las redes sociales.
-   ~ 2 correcciones de errores.

Cambios internos:

-   Se cambió a una nueva implementación de [trylock](https://github.com/decred/dcrdata/pull/1868).
-   Menor [dependencia](https://github.com/decred/dcrdata/pull/1855) de los paquetes RPC de dcrd.
-   Quedo actualizado a la última versión de [dcrd](https://github.com/decred/dcrdata/pull/1849).
-   Se eliminó la dependencia de [notify.js](https://github.com/decred/dcrdata/pull/1867) abandonada.

Consejo: se puede acceder a la versión de desarrollo de vanguardia de dcrdata en [tip.dcrdata.org](http://tip.dcrdata.org/).

### [dcrdevdocs](https://github.com/decred/dcrdevdocs)

*dcrdevdocs es un código fuente para la [documentación para desarrolladores](https://devdocs.decred.org/) de Decred.*

-   Se añadido [modo oscuro](https://github.com/decred/dcrdevdocs/pull/97) (por supuesto).
-   HTML en [línea eliminado](https://github.com/decred/dcrdevdocs/pull/98) (ayuda a detectar enlaces rotos).
-   [Versiones](https://github.com/decred/dcrdevdocs/pull/99) actualizadas de MkDocs y Python.

Otro:

-   El programa [Bug Bounty](https://bounty.decred.org/) obtuvo dos actualizaciones [de alcance](https://github.com/decred/dcrbounty/pull/83): reemplazó dcrstakepool con vspd, eliminó dcrdocs y se aclararon las reglas para atomicswap.

## Comunidad

¡Bienvenido al nuevo contribuyente con código fusionado en la rama master: @naveensrinivasan ([dcrd)](https://github.com/decred/dcrd/commits?author=naveensrinivasan)!

Estadísticas de la comunidad a partir del 2 de octubre:

-   Seguidores de [Twitter](https://twitter.com/decredproject): 48 673 (+512)
-   Suscriptores de [Reddit](https://www.reddit.com/r/decred/): 11 954 (+357)
-   Usuarios en la sala #general de [Matrix](https://chat.decred.org/): 535 (+13)
-   Usuarios de [Discord](https://discord.com/invite/GJ2GXfz): 2 077 (-47)
-   Usuarios de [Telegram](https://t.me/Decred): 2 909 (+63)
-   Suscriptores de [Youtube](https://www.youtube.com/decredchannel): 4 610 (+0) views: 196 000 (+2 000)

**Gobernanza**
--------------

En septiembre, el nuevo fondo de la [tesorería](https://dcrdata.decred.org/treasury?chart=balance&zoom=knj8yxs0-ktmgrvk0&bin=month) recibió 10 274 DCR por un valor de 1.4 millones de dólares a la tasa promedio de septiembre de 139.56 dólares. Se gastaron 590 DCR para pagar a los contratistas por un valor de $82 000 a la tasa de septiembre o bien $95 000 a la tasa de facturación de agosto de $161.24. Al 2 de octubre el saldo combinado de la nueva tesorería [heredada](https://dcrdata.decred.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx?chart=balance&zoom=ijhhasg0-kse64gw0&bin=month) es de 723,528 DCR (83.5 millones de dólares a 115.45 dólares).

Se presentaron dos nuevas propuestas, ambas por @raedah, solicitando fondos renovados para [GoDCR](https://proposals.decred.org/record/f7d9fc8) y las [billeteras para móvil](https://proposals.decred.org/record/6db3c4e).

La participación de los votantes alcanzó nuevas alturas y ambos votos de este mes registraron una participación por encima del nivel récord anterior.

-   La [propuesta](https://proposals.decred.org/record/58d9f46) de Monde PR fue aprobada con 97.5% de aprobación y una participación del 75%.
-   La [propuesta](https://proposals.decred.org/record/150cf81) de financiar una serie de videos educativos para el mercado de India, de @ finstreet21 fue rechazada con un 45% de aprobación y una participación del 77%.

La característica de [actualizaciones por parte del autor de propuestas](https://github.com/decred/politeia/issues/1473) tan esperada ahora está disponible en Politeia y ya ha sido utilizada por dos [propuestas de desarrollo](https://proposals.decred.org/record/3a98861) para informar el progreso.

Consulte el [issue 46](https://blockcommons.red/politeia-digest/issue046/) y el [issue 47](https://medium.com/decred-es/politeia-digest-47-septiembre-4-octubre-3-2021-3cb3bb3e6c01) de Politeia Digest para obtener más detalles sobre las propuestas del mes.

**Red**
-------

**Hashrate:** el [hashrate](https://dcrdata.decred.org/charts?chart=hashrate&zoom=krrqjgnz-kt1oo9gz&scale=linear&bin=block&axis=time) de septiembre se abrió a ~355 Ph / s y cerró ~228 Ph / s, tocando fondo en 190 Ph / s alcanzando un máximo de 449 Ph / s durante todo el mes.

Distribución del hashrate [reportada](https://miningpoolstats.stream/decred) en los pools el 1 de octubre:

-   Poolin 36%
-   F2Pool 25%
-   AntPool 22%
-   BTC.com 5%
-   ViaBTC 5%
-   Luxor 3%
-   HuobiPool 1%
-   CoinMine 0.15%
-   OKEx 0.13%.

La distribución de 1 000 bloques [minados](https://miningpoolstats.stream/decred) antes del 1 de octubre coincidió estrechamente con el hashrate informado.

**Staking:** el [precio de los tickets](https://dcrdata.decred.org/charts?chart=ticket-price&zoom=krrqjgnz-kt1oo9gz&bin=window&axis=time&visibility=true-true) varió entre 192.8--210.8 DCR con un [promedio](https://dcrstats.com/) de 30 días de 199.4 DCR (+5.6).

La [cantidad bloqueada](https://dcrdata.decred.org/charts?chart=ticket-pool-value&zoom=krrqjgnz-kt1oo9gz&scale=linear&bin=block&axis=time) fue de 7.69--8.16 millones DCR lo que significa que entre el 57.7 y 61.1% del suministro circulante [participó](https://dcrdata.decred.org/charts?chart=stake-participation&zoom=krrqjgnz-kt1oo9gz&scale=linear&bin=block&axis=time) en el proof-of-stake.

Los precios de los tickets parecen haber alcanzado una estabilización relativa entre dos extremos.

**VSP:** El 1 de octubre los servidores vspd [administraron](https://decred.org/vsp/) ~7,600 (-500) tickets en vivo y los servidores dcrstakepool enumerados aproximadamente ~220 (-30). En conjunto, los 8 VSP heredados y los 15 nuevos administraron el 219% (-2%) del grupo de tickets. Los VSP heredados excluidos de la lista que aún siguen activos administraron 29 (-11) tickets en vivo.

**Nodos:** a lo largo de septiembre hubo alrededor de 204 nodos accesibles según [dcrextdata](https://analytics.planetdecred.org/).

Versiones de nodo a partir del [snapshot](https://nodes.jholdstock.uk/user_agents) del 1 de octubre (257 dcrd nodos):

-   v1.6.2--55%
-   v1.6.0--13%
-   v1.6.1--12%
-   v1.7 dev builds --- 14%
-   v1.6 dev builds --- 2.7%
-   v1.5.2--2%
-   v1.5.1--1.2%.

La proporción de [monedas mezcladas](https://dcrdata.decred.org/charts?chart=coin-supply&zoom=jyefppu5-kub1inpe&bin=day&axis=time&visibility=true-true-true) varió entre el 50.3% y 52.2% y estableció un nuevo récord histórico, mientras que la suma de monedas mixtas no gastadas superó la marca de los 7 millones.

La [cantidad diaria mezclada](https://dcrdata.decred.org/charts?chart=privacy-participation&zoom=jzuht6o0-kv1lwqo0&bin=day&axis=time&visibility=true-false) varió entre 240-550 mil DCR.

**Ecosistema**
--------------

Se recomienda a los usuarios de Matrix que actualicen a sus clientes (especialmente Element) para parchear la [vulnerabilidad](https://matrix.org/blog/2021/09/13/vulnerability-disclosure-key-sharing) de seguridad divulgada el 13 de septiembre. Si la cuenta de un usuario se ve comprometida (ya sea por un compromiso directo de las credenciales de la cuenta o por un servidor doméstico comprometido) en ciertas circunstancias puede que sea posible leer los mensajes cifrados enviados a dicha cuenta desde sus contactos vulnerables. La divulgación señaló: "El mayor riesgo es para los usuarios que se encuentran en salas encriptadas que contienen servidores maliciosos. Los administradores de servidores maliciosos podrían intentar hacerse pasar por los dispositivos de sus usuarios para espiar los mensajes enviados por clientes vulnerables en esa sala ". Como medida de seguridad adicional, puede revisar las sesiones activas y eliminar las obsoletas o sospechosas.

El legado [decredvoting.com](http://decredvoting.com/) se eliminó de la [lista VSP](https://decred.org/vsp/) para facilitar la migración de usuarios al nuevo [sistema vspd](https://blog.decred.org/2020/06/02/A-More-Private-Way-to-Stake/). Las billeteras de votación todavía están en línea para votar los tickets restantes (9 tickets a partir del 1 de octubre). Decred Voting ha prestado [servicios desde 2018](https://www.reddit.com/r/decred/comments/9c6s3l/new_voting_service_provider_aka_stake_pool_is_now/) y es conocido por desarrollar funciones avanzadas como [notificaciones](https://www.reddit.com/r/decred/comments/9oepq6/decredvotingcom_now_supporting_automatic_email/) por correo electrónico en tickets ya votados y un [panel](https://www.reddit.com/r/decred/comments/hbofz4/tired_of_keeping_track_of_your_staking_activities/) de análisis de tickets personalizados y también por ayudar a los pequeños propietarios con [educación](https://medium.com/decred/dcr-ticket-splitting-all-you-need-to-know-b8edc6b65db3) sobre la división de tickets y [funciones](https://www.reddit.com/r/decred/comments/euqd4h/introducing_split_ticket_dashboard_on/) para facilitar su uso.

Para cualquier persona que todavía use VSP heredado, se recomienda cambiar a [proveedores de vspd](https://decred.org/vsp/) para evitar el riesgo de perdida, p. Ej. en caso de que el VSP heredado se apague o deje de funcionar con las próximas actualizaciones de consenso. A partir del 1 de octubre, todos los VSP heredados administraron menos de 250 tickets o el 0.6% del grupo de tickets.

u / daryledesilva [compartió](https://www.reddit.com/r/decred/comments/pp8uu4/decred_dcr_dollar_cost_averaging_dca_calculator/) una [calculadora](https://dcacryptocalculator.com/decred) de promedio de costos en dólares para Decred.

*Advertencia: los autores de la revista Decred no tienen idea de la confiabilidad de ninguno de los servicios mencionados anteriormente. Haga su propia investigación antes de confiar su información personal o sus activos a cualquier entidad.*

Únase a nuestro chat [#services](https://chat.decred.org/#/room/#services:decred.org) para seguir las actualizaciones del ecosistema Decred.

**Alcance**
-----------

Se actualizó la publicación fijada de r / decred para recién llegados: [Bienvenido a Decred: Money Evolved.](https://www.reddit.com/r/decred/comments/pqsmgf/welcome_to_decred_money_evolved/)

@davecgh nos dió un nuevo y fantástico [discurso de Decred](https://www.reddit.com/r/decred/comments/ppmkdm/opinions_on_long_term_value_of_decred_not_asking/hd5kvp0/) que responde cómo Decred es valioso a largo plazo. Versión de Twitter [aquí](https://twitter.com/rstaudt2/status/1443257842920734727).

Logros de Monde PR para septiembre:

-   [Propuesta](https://proposals.decred.org/record/58d9f46) de relaciones públicas aprobada el 14 de septiembre.
-   Actualizó el calendario de relaciones públicas para incluir los próximos anuncios y la actividad de relaciones públicas.
-   Lanzó para Decred dos oportunidades de relaciones públicas.
-   Aseguró dos entrevistas con los medios para Decred.

Se aseguro el siguiente artículo de noticias:

-   @lukebp fue entrevistado por [Cigars and Crypto Podcast](https://www.cigarsandcrypto.com/episode-175-luke-powell-of-the-decred-project/) cubriendo todo lo relacionado con Decred.

## Medios

**Artículos seleccionados:**

- Decred Blockchain Analysis - Part 3 por @richardred ([blockcommons.red](https://blockcommons.red/post/dcr-on-chain-3/)) - explora cuál es la información que se puede encontrar aplicando agrupación de direcciones de todos los tickets en los pools en alturas de bloques específicas. Nota: quedan algunos problemas por solucionar con los resultados.
- Decred address clustering deep dive por @richardred ([blockcommons.red](https://blockcommons.red/publication/clustering-deep-dive/)): un informe  especializado en los desafíos de la agrupación en clústeres, incluye muchos gráficos que muestran el comportamiento de votación de diferentes pools (usuarios) y cómo se ve cuando algo anda mal con uno de ellos.
- A deep dive into how the top 10 DAOs work por Andrey Sergeenkov ([coinmarketcap.com](https://coinmarketcap.com/alexandria/article/a-deep-dive-into-how-the-top-daos-work))

**Videos:**

- Being fork resistant - Decred Fundamentals por @phoenixgreen ([youtube](https://www.youtube.com/watch?v=P2LrIcF_8qw)).
- How is Decred fork resistant? - Fundamentos de Decred @phoenixgreen ([youtube](https://www.youtube.com/watch?v=pmQiU3zycU0))
- Decred in Depth Ep. 43 - Chris Dannen + pensamiento de diseño + futuro de Decred por @elima_iii ([youtube](https://www.youtube.com/watch?v=Cj6PmMza9RQ))
- Decred Price Analysis - 15 de septiembre del 2021 por Brave New Coin ([youtube](https://www.youtube.com/watch?v=qOpLpdBCMI4))

**Audio:**

- Cigars and Crypto 175 - Luke Powell del Proyecto Decred ([cigarsandcrypto.com](https://www.cigarsandcrypto.com/episode-175-luke-powell-of-the-decred-project/))
- Decred Society series de @phoenixgreen se ha publicado en [Apple Podcasts](https://podcasts.apple.com/us/podcast/decred-society/id1586826872).

**Traducciones:**

- [Decred News August](https://www.youtube.com/watch?v=6ifueUAWy_c) - en chino (@Dominic) publicado en plataformas de video chinas como [Bilibili](https://www.bilibili.com/video/BV1QA411c77W), [Weibo](https://passport.weibo.com/visitor/visitor?entry=miniblog&a=enter&url=https%3A%2F%2Fweibo.com%2F6824123103%2FKvXMCaDEW&domain=.weibo.com&sudaref=https%3A%2F%2Fmedium.com%2F&ua=php-sso_sdk_client-0.6.36&_rand=1635107778.4762) y [WeChat](https://mp.weixin.qq.com/s/l1RO1Mkb9LNQK2Z2x1mkyw).
- La Revista Decred de agosto del 2021 se [tradujo](https://xaur.github.io/decred-news/) al árabe (@arij, @ abdulrahman4), chino (@Dominic) y español (@francov_). ¡Gracias a todos los traductores por quedarse!

Comparta sus traducciones en nuestra sala de chat [#translations](https://chat.decred.org/#/room/#translations:decred.org).

![bufalo](./assets/bufalo.jpeg)

**Mercados**
--------

En septiembre, DCR cotizaba entre 96.14--185.79 USD/ BTC 0.0023--0.0038. La tarifa promedio diaria fue de $139.56.

![mercado](./assets/exchange.png)

**Noticias Relevantes**
-----------------------

La aplicación de Sushi's Miso fue [utilizado](https://www.coindesk.com/business/2021/09/17/3m-in-ether-stolen-from-sushiswaps-miso-launchpad/) para robar las ganancias de una caída de NFT ($ 3 millones para Kia Sedonas de Jay Pegs Auto Mart). El atacante fue [identificado](https://www.coindesk.com/tech/2021/09/17/3m-was-stolen-but-the-real-steal-is-these-kia-sedonas-say-anonymous-developers/) (mediante el uso del dominio ENS) como un desarrollador de Sushi, que había insertado un código en la interfaz en donde envió los fondos a su propia dirección. Posteriormente los fondos fueron devueltos a sus respectivas cuentas.

La aplicación Compound DeFi implementó nuevos smarts contracts en donde [entregaron](https://www.coindesk.com/tech/2021/09/30/defi-money-market-compound-overpays-15m-in-comp-rewards-in-possible-exploit/) tokens COMP por un valor de 80 millones de dólares de formas no deseadas. El fundador, Robert Leshner, pidió a los destinatarios que devolvieran los tokens y lo describió como un [dilema](https://www.coindesk.com/tech/2021/10/01/compound-founder-says-80m-bug-presents-moral-dilemma-for-defi-users/) moral, después de insinuar inicialmente que las personas que no devuelvan los tokens podrían pasar sus datos a las autoridades de recaudación de impuestos. Un aspecto interesante de la historia es que el problema se identificó con bastante rapidez, pero debido a que cambiar los contracts requiere un proceso de gobernanza, no había forma de implementar una solución rápida y todos los fondos vulnerables se agotaron.

Los usuarios de Coinbase han sido [atacados](https://www.zdnet.com/article/coinbase-sends-out-breach-notification-letters-after-6000-accounts-had-funds-stolen/), parece que alrededor de 6 000 usuarios cuyos datos de inicio de sesión se habían visto comprometidos en otros lugares sufrieron pérdidas en sus cuentas de Coinbase después de que los atacantes explotaran una falla en el proceso de recuperación de dos factores de SMS de Coinbase para eludir esta protección y retirar los fondos de sus víctimas. En una [carta](https://oag.ca.gov/system/files/09-24-2021%20Customer%20Notification.pdf) de notificación a los clientes, Coinbase dijo que la falla se ha solucionado y que todos los clientes afectados serán reembolsados. Esto se debe a un [descontento](https://www.zdnet.com/article/coinbase-sends-out-breach-notification-letters-after-6000-accounts-had-funds-stolen/) más general con el servicio al cliente de Coinbase en el verano.

La Ley de Estructura del Mercado de Activos Digitales y Protección al Inversionista, que se [presentó](https://beyer.house.gov/news/documentsingle.aspx?DocumentID=5307) en julio, continúa recibiendo [cobertura](https://www.jdsupra.com/legalnews/new-us-digital-assets-bill-casts-wide-5957884/) y discusión, lo que indica que recibirá una seria consideración por parte de los legisladores. La Ley propuesta es una de las leyes más amplias para abordar los activos digitales y aclararía cómo los diferentes tipos de activos caerían dentro del ámbito de las diferentes agencias de aplicación. La definición propuesta de un valor se centraría en la equidad o los derechos de voto en la entidad emisora (corporativa) excluyendo la votación sobre asuntos de blockchain como la creación de bloques. También hay un aspecto por el cual la venta de tokens para un producto sin terminar cuya producción será financiada por la venta de tokens (es decir, el modelo ICO) se consideraría valores. Las monedas estables no se podrían crear ni usar sin la aprobación del Secretario del Tesoro y la Reserva Federal recibiría la autoridad para emitir una moneda digital del banco central de EE. UU.

Eso es todo por septiembre. Comparta sus actualizaciones para el próximo número en nuestra sala de chat [#journal](https://chat.decred.org/#/room/#journal:decred.org).

**Sobre esta edición**
======================

Esta es la edición #42 de la Revista Decred. Un índice de todas las ediciones, y traducciones están disponibles [aquí](https://xaur.github.io/decred-news/).

*La mayoría de la información de terceros se transmite directamente desde la fuente después de un control de fiabilidad mínimo. Los autores de la Revista Decred no tienen la capacidad de verificar todas las reclamaciones. Tenga cuidado con las estafas y haga su propia investigación.*

Créditos (por orden alfabético):

-   Escritura y redacción: bee, degeri, l1ndseymm, richardred
-   Revisión y comentarios: davecgh, lukebp
-   Imagen de portada: saender
-   Financiado por: Los stakeholders de Decred

