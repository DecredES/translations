# Revista Decred – Febrero 2020

![Segundo Pastel de Decred](./assets/202002.jpg)

_Imagen: Segundo pastel de Decred en Morocco por @arij_

- ¡El cuarto aniversario del bloque Génesis de Decred se llevó acabo el 8 de febrero y se celebró en todo el mundo, los asistentes de al menos 11 ciudades participaron en el primer #DecredGlobalMeetup!
- @Dustorf publicó un informe sobre los esfuerzos de mercadotecnia del proyecto en 2019, dando detalles de lo que se hizo, cómo se gastó el recurso (DCR), qué salió bien y qué no, junto con ideas sobre cómo avanzar en 2020.
- Progreso sólido en todos los principales repositorios de software de Decred, con optimizaciones para dcrd, un gran lote de componentes sobre el DEX fueron completados, las aplicaciones móviles listas para beneficiarse de las nuevas reglas de consenso y un SPV más eficiente.
- El nuevo sitio decred.org se lanzó a principios de marzo, enfocándose en los mensajes clave según lo determinado por la comunidad en 2019, y presentándolos de una manera accesible y estéticamente agradable.

## Aviso de Actualización

El voto de consenso para habilitar DCP-0005 ha ocurrido y se espera sea [activado](https://voting.decred.org/) alrededor del 13 de marzo. Por favor toma tu tiempo para [actualizar](https://decred.org/wallets/) tu software y mantenerte conectado a la red.

## Desarrollo

[dcrd](https://github.com/decred/dcrd): Mucho trabajo en febrero se centró en reelaborar el paquete secp256k1 para introducir optimizaciones especializadas:

- Los paquetes internos de secp256k1 [fueron](https://github.com/decred/dcrd/pull/2056) independientes de las API criptográficas de la biblioteca estándar Go para eliminar muchas conversiones innecesarias y costosas permitiendo más optimizaciones en el futuro
- La verificación de firma fué [implementada](https://github.com/decred/dcrd/pull/2058) directamente en lugar de depender de una biblioteca estándar que permitirá optimizaciones específicas para la curva secp256k1
- Se introdujo código especializado para [mejorar la precision](https://github.com/decred/dcrd/pull/2060) en aritmética que es significativamente más rápido que la precision arbitraria de numeros enteros grandes de la biblioteca estándar y también es constante en el tiempo
- Se agrego optimizaciones en [square root](https://github.com/decred/dcrd/pull/2088) en el campo de cálculo, que es aproximadamente dos veces más rápido que usar numeros enteros grandes

Debido a que algunas optimizaciones son más difíciles de revisar, se tuvo mucho cuidado al introducirlas en pasos y documentar minuciosamente todas las técnicas utilizadas. Si te encantan las matemáticas y la computación rápida a nivel de donde se unen los bits , esta debería ser una lectura encantadora.

En general, los principales beneficios de la revisión en el paquete secp256k1 son la mejora de la velocidad y el uso de la memoria, que juegan un papel importante en el rendimiento general del software, ya que la verificación de firmas es la operación principal. Otro beneficio importante es que una vez que esto se complete, las operaciones de los paquetes secp256k1 serán de tiempo constante, lo que mejora la resistencia a los ataques de canal lateral. Esta es una propiedad importante para los protocolos multiparte que realizan muchas firmas, los protocolos Schnorr multigrado son un ejemplo.

Otras mejoras:

- el código de consenso [se hizo](https://github.com/decred/dcrd/pull/2031) un poco más robusto al ser explícito sobre los formularios de script que requieren en vez de [depender](https://github.com/decred/dcrd/pull/2036#issuecomment-583782693) de un código de política de estandarización (p.ej. lo que está permitido al ingresar al mempool y transmitirse a través de la red), que puede cambiar sin un voto de consenso
- Se permitió el rango de voto [ajustado](https://github.com/decred/dcrd/pull/2047) para prevenir en la red principal un improbable ataque vector DoS
- los tickets con entradas no aprobadas ahora se reastrean por [separado](https://github.com/decred/dcrd/pull/1852) para que la generación de plantillas de bloques y la estimación de tarifas sean más eficientes
- se añadió parámetros de tiempo para las [conexiones TCP](https://github.com/decred/dcrd/pull/2068) y los [pares inactivos](https://github.com/decred/dcrd/pull/2067)
- el rpcserver [se hizo](https://github.com/decred/dcrd/pull/2066) explícito sobre las unidades que acepta (atoms vs coins) en el código, se ayudó en los mensajes y en la documentación de las APIs
- se [definió](https://github.com/decred/dcrd/pull/2055) tipos de errores wire, trabajando en conjunto para [banear a los pares](https://github.com/decred/dcrd/issues/350) que no siguen el protocolo wire

[dcrwallet](https://github.com/decred/dcrwallet):

- se agregó un comando para crear un [ticket sin firma](https://github.com/decred/dcrwallet/pull/1281) para facilitar el staking fuera de línea y soportar el staking de Trezor en el futuro (El firmware de Trezor aún debe modificarse para admitir el staking de Decred)
- se agregó un comando para [crear una firma](https://github.com/decred/dcrwallet/pull/1611) de script para entrada de transacción 
- se agregó el comando [discoverusage](https://github.com/decred/dcrwallet/pull/1643) para activar manualmente el descubrimiento de la dirección y / o el uso de la cuenta sin reiniciar la cartera
- se añadió el RPC para iniciar el proceso de [servicio de mezcla](https://github.com/decred/dcrwallet/pull/1635) de cuentas que Decrediton utilizará
- la estrucura del módulo se [simplificó](https://github.com/decred/dcrwallet/pull/1642) para reducir la carga de mantenimiento
- se agregó un [paquete](https://github.com/decred/dcrwallet/pull/1664) para generar números pseudoaleatorios criptográficamente uniformes y seguros
- se modificó la distribución de los pares para utilizar la [API HTTPS](https://github.com/decred/dcrwallet/pull/1661)
- múltiples limpiezas de código

[Decrediton](https://github.com/decred/decrediton):

- se agregó el generador [BIP-0021](https://github.com/decred/decrediton/pull/2418) de links para los pagos de DCR
- se agregó una [advertencia](https://github.com/decred/decrediton/pull/2413) para hacer una copia de seguridad en los redeem scripts
- la base del código se actualizó a [Electron 8](https://github.com/decred/decrediton/pull/2208)
- se arregló errores y ajustes en la UI
- La gran refactorización de la lógica de inicio se [fusionó](https://github.com/decred/decrediton/pull/2425) después de muchos meses de trabajo

[Politeia](https://github.com/decred/politeia): cambios en el backend:

- las sesiones se [movieron](https://github.com/decred/politeia/pull/1113) hacia userdb para permitir la invalidación manual de sesiones y también como un paso para ejecutar múltiples instancias de politeiawww (para escalabilidad y tolerancia a fallas)
- lo [metadatos](https://github.com/decred/politeia/pull/1110) de propuestas necesarios para propuestas RFP se agregaron al cache
- StartVote v2 [fusionado](https://github.com/decred/politeia/pull/1088) (se describió en [diciembre](201912.md#development))
- se agregó una ruta de backend para recuperar propuestas utilizando un [token corto](https://github.com/decred/politeia/pull/1116) (esto permitirá URL más cortas en la GUI)
- el CMS recibió soporte preliminar en el [temporal del contractor](https://github.com/decred/politeia/pull/1132) y algunas correcciones más pequeñas

Cambios en el frontend:

- se agregó un modo [plano](https://github.com/decred/politeiagui/pull/1781) para ayudar a detectar nuevos comentarios sin buscarlos en el conjunto de árbol
- ajustes en la IU y optimizaciones de rendimiento

[dcrpool](https://github.com/decred/dcrpool):

- la mayoría del nuevo [diseño de la UI](https://github.com/decred/dcrpool/pull/149) fue implementado. La versión inicial fue un paso difícil hecho por los desarrolladores para obtener algo
  en movimiento, mientras que la nueva versión fue realizada correctamente por los diseñadores para que coincida con el resto de la apariencia Decred
- se agregó [unidades de tiempo](https://github.com/decred/dcrpool/pull/151) human-friendly en la configuración
- correcciones de errores y ajustes en la UI

[dcrlnd](https://github.com/decred/dcrlnd): Se ha[completado](https://github.com/decred/dcrlnd/pull/74)el enorme esfuerzo de portabilidad de los cambios ascendentes hasta la versión [v0.9.0-beta](https://github.com/lightningnetwork/lnd/releases/tag/v0.9.0-beta).

[cspp](https://github.com/decred/cspp): Correcciones múltiples y manejo mejorado de errores.

[dcrdex](https://github.com/decred/dcrdex): Aspectos más destacados del desarrollo:

- se agregó el cliente [del servidor RPC](https://github.com/decred/dcrdex/pull/133) para la línea de comando / cliente de control en script
- se basó en contraseña el paquete de la [llave de crifrado](https://github.com/decred/dcrdex/pull/155) para un almacenamiento secreto
- se agregó una [cola de pedidos queue](https://github.com/decred/dcrdex/pull/143) en el lado del servidor y validación aleatoria
- se agregó un cliente de [ingreso](https://github.com/decred/dcrdex/pull/153) y que conecta las funcionalidades, usando una contraseña para toda la aplicación
- se [implementó](https://github.com/decred/dcrdex/pull/145)  una coincidencia de orden determinista menos jugable en el [algoritmo](https://github.com/decred/dcrdex/issues/67) donde la cola de pedidos queue se baraja en función de los compromisos criptográficos del cliente, con preimágenes reveladas al motor correspondiente (los cambios de las especificaciones los puedes ver [aquí](https://github.com/decred/dcrdex/pull/83))
- se añadió una página de [carteras](https://github.com/decred/dcrdex/pull/176) en la GUI del cliente basado en el navegador que permite crear y controlar carteras de intercambio
- se realizó un [respaldo](https://github.com/decred/dcrdex/pull/183) en la base de datos del cliente
- se guardó todos los datos de coincidencias/swap en la [base de datos](https://github.com/decred/dcrdex/pull/177) para permitir que el servidor pruebe la recepción de mensajes de clientes relacionados con el swap
- compilación actualizada e [instrucciones](https://github.com/decred/dcrdex/pull/175) de contribución

Un total de 25 pull requests fusionados de 7 contribuyentes añadieron 12K líneas y borraron otras 3K (resumen de los commit [aquí](https://github.com/decred/dcrdex/compare/15d3021da853110baa02b24311b03e457b61be4a...94310f66c06fdf5ca31eeb80c9f6af7aecf4c31d)).

[dcrandroid](https://github.com/decred/dcrandroid): La versión 1.0.1 lanzada en Google Play corrige varios errores e incluye módulos v1.5 para admitir las nuevas reglas de consenso.


En desarrollo: migración implementada a un formato [multi-cartera](https://github.com/decred/dcrandroid/pull/426).

[dcrios](https://github.com/raedahgroup/dcrios): La versión 1.0.1 lanzada en App Store corrige un error e incluye módulos v1.5 para admitir las nuevas reglas de consenso.

En desarrollo:

- nueva implementación en la UI de las [Carteras](https://github.com/raedahgroup/dcrios/pull/567), [Transacciones](https://github.com/raedahgroup/dcrios/pull/569) y [Recibido](https://github.com/raedahgroup/dcrios/pull/583)
- se muestra el progreso de sincronización en las [multiples carteras](https://github.com/raedahgroup/dcrios/pull/579)
- se desbloqueó un resumen de la característica de [restauración](https://github.com/raedahgroup/dcrios/pull/577)

[dcrdata](https://github.com/decred/dcrdata):

- la página de estimación de costo por ataque finalmente fué [incorporada](https://github.com/decred/dcrdata/pull/1664). El trabajo empezó 6 meses atrás por Raedah Group con una contribución principal de @ademuanthony y @dmigwi usando [investigaciones](https://medium.com/decred/decreds-hybrid-protocol-a-superior-deterrent-to-majority-attacks-9421bf486292) de @zubair (que se basa en el modelo del documento de Proof-of-Activity ajustado por @jy-p, también tomó como referencia este [documento](https://github.com/buck54321/dcr-research/blob/master/paper/Attack-cost%20estimation.pdf) por @buck54321). La página está disponible para pruebas públicas [aquí](https://alpha.dcrdata.org/attack-cost).
- se agregó nuevos [gráficos](https://github.com/decred/dcrdata/pull/1640) para las [monedas mezcladas](https://alpha.dcrdata.org/charts?chart=coin-supply&bin=day&axis=time&visibility=true%2Ctrue%2Ctrue) y la [participación de privacidad](https://alpha.dcrdata.org/charts?chart=privacy-participation)
- se activó un modo [smooth](https://github.com/decred/dcrdata/pull/1678) para los gráficos de tickets
- correcciones de errores y ajustes de la UI

[tinydecred](https://github.com/decred/tinydecred):

- el código de prueba se simplificó y obtuvo mayor cobertura de prueba
- el cliente RPC fué [terminado](https://github.com/decred/tinydecred/pull/73)
- se realizó un manejo [simplificado de errores](https://github.com/decred/tinydecred/pull/81)

[docs](https://github.com/decred/dcrdocs):

- se agregó [nuevas](https://github.com/decred/dcrdocs/pull/1040) páginas para CoinShuffle++ de [descripción general](https://docs.decred.org/privacy/cspp/overview/) y [de como se usa](https://docs.decred.org/privacy/cspp/how-to-cspp/)
- se agregó [consejos adicionales](https://github.com/decred/dcrdocs/pull/1068) sobre cómo ejecutar dcrd y dcrwallet como servicios del sistema
- se [pulió](https://github.com/decred/dcrdocs/pull/1064) documentos de la red lightning

[decred.org](https://github.com/decred/dcrweb): Las menciones en Slack fueron [removidas](https://github.com/decred/dcrweb/pull/780), gran diseño y actualización de contenido (consulte la sección Alcance a continuación).

Otro:

- El programa Bug Bounty publicó una [actualización](https://bounty.decred.org/2020/02/status-update/): 97 envíos procesados hasta el momento (+14 desde la actualización de octubre), con 11 elegibles para un pago (+1).
- Los desarrolladores que buscan cómo comenzar a contribuir pueden seguir la cuenta de Twitter [@dcrgoodfirst](https://twitter.com/dcrgoodfirst).

Las estadísticas de actividad de los desarrolladores para febrero: 309 PRs activas, 274 confirmaciones en master, 52K líneas agregadas y 28K líneas eliminadas distribuidas en 20 repositorios. Las contribuciones vinieron de 2 a 6 desarrolladores por repositorio.

## Comunidad

Bienvenidos por primera vez a los nuevos contribuyentes con código fusionado en la rama master: @mkingori ([dcrdata](https://github.com/decred/dcrdata/commits?author=mkingori)).

Felicitaciones a los nuevos contratistas a los que se les otorgó la Autorización de Contratista Decred a través del nuevo proceso de CMS: [@dezryth](https://scottrchristian.com/) (marketing), [@guisso](https://github.com/fguisso) (desarrollo).

Felicitaciones a los nuevos [contribuyentes](https://decred.org/contributors/) que figuran en decred.org: Mike Winslow (@Exitus, Media Production).

Estadísticas de la comunidad:

- Seguidores en Twitter: 40,901 (+41)
- Suscriptores de Reddit: 9,738 (+15)
- Usuarios de matrix: 565 (+32)
- Usuarios de Discord: 1,087 (-1,583), verified to post: 450 (+17) (see Community Discussions about the purge)
- Usuarios de Telegram: 2,678 (-50)
- Suscriptores de YouTube: 3,990 (+40)
- Seguidores en Facebook: 3,580 (+17), likes: 3,249 (+15)
- Seguidores de LinkedIn: 719 (+30)
- Estrellas en el Github de dcrd: 535 (+2), forks: 1,496 (+20)

## Gobernanza

En febrero [la Tesorería](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx) recibió 13,018 DCR y gastó 12,622 DCR. Usando la tasa diaria promedio de DCR / USD de febrero de $20.48, esto es $267K recibido y $258K gastado. A una tasa diaria promedio de $18.00 en enero, la cifra en USD facturada por el trabajo completado en ese mes es de $227K. A partir del 2 de marzo, el saldo de la tesorería es de 643,179 DCR ($11.6 millones de dólares a $18).

[El número 6](https://ournetwork.substack.com/p/our-network-issue-6) de our network incluía un cuadro útil con entradas y salidas de la tesorería. Al 30 de enero, la Tesorería recibió un total de 939K DCR y gastó 299K DCR.

En febrero se presentaron 4 nuevas [propuestas](https://dcrdata.decred.org/proposals) y 5 se comenzaron a votar.

- La propuesta de producción de video de @Exitus que solicitó hasta $2,400 por mes fue aprobada con una aprobación del 92.5% y una participación de los votantes del 24.8%.
- La segunda propuesta de investigación de @Checkmate se aprobó con una tasa de aprobación del 81% y una participación de los votantes del 21,5%. Solicitó un presupuesto de $17,500 para continuar la investigación de @Checkmate y otras actividades, incluida la ayuda para obtener algunos gráficos del trabajo de él y @permabullnino en dcrdata.
- La propuesta de marketing y eventos europeos de @Haon y apoyada por @jholdstock, @kozel, @jazzah, @mm y @karamble inicialmente solicitó $75,000 pero redujo el presupuesto a $49,000 y eliminó el evento Web Summit en respuesta a los comentarios. La propuesta fue rechazada el 3 de marzo, obteniendo solo el 38% de apoyo, con una participación de los votantes del 25%.
- La propuesta de producción de video rusa fue rechazada con un 21% de aprobación y un 20% de participación.
- La propuesta de Economía Creativa para Decred de oscargamboae fue rechazada con un 3% de aprobación y se convirtió en la primera propuesta en no cumplir con el requisito del quórum del 20%, con solo el 15% de los boletos elegibles para votar.

Para obtener más detalles sobre la actividad mensual de Politeia, consulte la edición [27](https://blockcommons.red/politeia-digest/issue027/) y [28](https://blockcommons.red/politeia-digest/issue028/) de Politea Digest.

## Red

Hashrate: El hashrate de febrero abrió a ~ 427 Ph/s y cerró ~ 356 Ph/s, tocó fondo de 263 Ph/s y alcanzó un máximo de 578 Ph/s durante todo el mes. La distribución del hashrate del Pool a partir del 1 de marzo fué: Poolin 32%, UUPool 27%, lab.antpool.com 12%, BTC.com 1.7%, F2Pool 1.5%, Luxor 1.3%, BeePool 0.1%, CoinMine 0.02% y otros ~ 24% por [dcrstats.com](https://dcrstats.com/pow). Las estadísticas de distribución del Pool son aproximados y no se pueden determinar con precisión.

Staking: El precio promedio de los tickets de 30 días fue 132.1 DCR (-6.2) por dcrstats.com a partir del 5 de marzo. El precio varió entre 119.8–157.9 DCR. La cantidad bloqueada fue de 5.40–5.65 millones de DCR, que correspondió al 48.49–51.19% del suministro circulante.

Desde finales de enero, la cantidad de [DCR en stake](https://explorer.dcrdata.org/charts?chart=ticket-pool-value&zoom=k38z10xk-k7kaa0dk&bin=block&axis=time) experimentó una disminución de ~ 30 días desde aprox. 5.65M a 5.40M, o 51.5% a 48.5% (-3%) del suministro circulante, seguido de una recuperación de ~ 50%. El precio del ticket bajó a 119.8 DCR, pero luego se disparó rápidamente a niveles más altos de lo que ha alcanzado en años.

Nodos: A lo largo de [febrero](https://charts.dcr.farm/d/000000014/nodes?orgId=1&from=1580515200000&to=1583020800000) hubo un promedio de 165 nodos listening públicos y 341 nodos totales por dcr.farm. Distribución promedio de la versión para febrero: 40.8% usa dcrd v1.4, 18.2% usa dcrd v1.5, 9.1% usa dcrd v1.5 dev y RC builds, 12.3% usa dcrd v1.5.1, 4.1% usa dcrd v1.6 dev construcciones, 4.7% usa dcrwallet v1.4, 2.6% usa dcrwallet v1.5, 2.1% usa dcrwallet v1.5.1.

La cantidad de monedas mezcladas (conjunto de anonimato) alcanzó el 20% del suministro de DCR circulante. Las transacciones de CoinJoin se mezclan entre 50-100K DCR diariamente y el 22 de febrero se alcanzó un [nuevo máximo histórico](https://twitter.com/_Checkmatey_/status/1232746951294308356) de 154K DCR, equivalente a más de $3 millones. Estas y otras métricas fueron publicadas por @Checkmate en Our Network [edición 10](https://ournetwork.substack.com/p/our-network-issue-10) ([tweet](https://twitter.com/spencernoon/status/1233450761566244865)). Para los números actuales, dcrdata alpha ha desplegado gráficos de [porcentaje](https://alpha.dcrdata.org/charts?chart=coin-supply&bin=day&axis=time&visibility=true%2Ctrue%2Ctrue) de monedas mezcladas y la [cantidad de DCR](https://alpha.dcrdata.org/charts?chart=privacy-participation) mezclada por día y por bloque.

[Attack Cost Calculator](https://alpha.dcrdata.org/attack-cost) es una nueva herramienta web que permite estimar el costo de atacar la red en función de una serie de variables, actualmente disponibles en dcrdata alpha.

## Integraciones

Ha habido un [reporte](https://matrix.to/#/!MgQoetFiyjrHAywokv:decred.org/$158343614832392oTHUs:decred.org) de un titular de DCR estafado por una extensión de Chrome para la cartera de Ledger que solicitó las semillas de su cartera. Según los comentarios, parece que Google la eliminó de la tienda, pero solo después de que se quemaron algunas personas. ¡Presta mucha atención a qué software confías tus semillas!

OKCoin decidió [suspender](https://blog.okcoin.com/scheduled-token-suspensions/) las operaciones de DCR debido al bajo volumen de operaciones, a pesar de estar entusiasmado con Decred al principio e incluso organizar varios eventos en conjunto.

KuCoin [anunció](https://www.kucoin.com/news/en-decred-soft-staking-official-rules) el 17 de febrero que iba a comenzar a colocar en modo Hold los DCR de sus depositantes, dos días después, el 19 de febrero. Los usuarios de KuCoin que tienen DCR en el intercambio fueron informados de que estaban siendo suscritos automáticamente, y se les ordenó retirar sus fondos de inmediato. si deseaban optar por no participar.

> KuCoin ajustará la proporción de participación de Decred cada día en el calendario y calculará los ingresos diarios de los usuarios (…) Los usuarios deben tener en cuenta que debido a la participación del programa, habrá un riesgo potencial de que un usuario no pueda retirar su DCR designado de manera oportuna o según lo esperado, aunque KuCoin hará todo lo posible para evitar tal demora inevitable.

Los DCR en stake tendrán un límite de tiempo, la capacidad de KuCoin para proporcionarla a los depositantes dependerá de la votación suficiente de sus tickets, para liberar los DCR depositados y así puedan procesar los retiros.

> Un proyecto separado: el Servicio proporcionado por KuCoin en el presente solo afectará el retiro de DCR, y no afectará directa o indirectamente: (1) el comercio de activos DCR en nuestra plataforma; y (2) el comercio o retiro de cualquier otro activo digital en nuestra plataforma. Como tal, en el caso de que cualquier usuario sea reacio a seguir la secuencia de retiro pero ya esté alineado en la cola de retiro, dicho usuario puede optar por intercambiar DCR con otros tokens y retirar los tokens intercambiados inmediatamente.

Esto indica que, en un escenario en el que se está apostando demasiado DCR de KuCoin para poder satisfacer la demanda de retiro, los usuarios aún podrán comercializar ese DCR en el mercado, p. a cambio de BTC. Es probable que cualquier retraso prolongado en el procesamiento de los retiros disminuya el precio de DCR en KuCoin, si se sabe ampliamente que no pueden cumplir con las solicitudes de retiro de manera oportuna.

El anuncio no especifica ninguna tarifa que KuCoin cobre por la prestación de este servicio. Queda por ver si esto significa que no están tomando una comisión, o si el porcentaje de la comisión simplemente no está establecido.

Advertencia: la redacción de la Revista Decred no puede asegurar los servicios prestados por terceros. Recuerda siempre hacer tu propia investigación antes de confiar.

## Alcance

El 8 de febrero, Decred cumplió cuatro años y la comunidad celebró el evento con el [#DecredGlobalMeetup](https://twitter.com/hashtag/DecredGlobalMeetup). Los eventos tuvieron lugar en al menos una docena de ciudades de todo el mundo para celebrar la comunidad y la tecnología que Decred ha construido. @Dustorf escribió un [blog](https://medium.com/@dlefebvr/on-saturday-february-8th-the-decred-blockchain-will-have-been-adding-blocks-for-4-years-17fe3038f3bf) y un hilo de [twitter](https://twitter.com/lefebvre_dustin/status/1225462426503696384) que resumen el progreso de Decred hasta la fecha.

@Dustorf publicó un [Reporte de marketing](https://blog.decred.org/2020/02/26/Decred-2019-Marketing-Report/) que detalla todos los gastos relacionados con la mercadotecnia del proyecto en 2019. El informe incluye un resumen de lo que funcionó y lo que no funcionó, así como las recetas para el próximo año. Las tres recomendaciones de alto nivel incluyen: imaginar lo que se puede lograr socialmente usando tecnología Decred, rompa la burbuja para expandir Decred más allá de los que están actualmente en criptografía y aproveche el poder de cada individuo dentro de la comunidad. El reporte pide una descentralización de los esfuerzos de marketing por geografía. Con ese fin, América Latina ya aprobó una propuesta. La propuesta europea se hizo, pero fue rechazada. Se espera que las propuestas para Brasil, Estados Unidos, Canadá y Australia se hagan en marzo. Dado que el marketing de Decred siempre ha sido objeto de debates, cualquiera que esté interesado en este dominio puede estudiar el reporte y compartir sus ideas en  el hilo correspondiente de [Reddit](https://www.reddit.com/r/decred/comments/fa70c3/decred_2019_marketing_report/).

La renovación del sitio web [decred.org](https://decred.org/) se implementó a principios de marzo, con una nueva estética visual, un nuevo video explicativo y nuevas subpáginas que presentan la historia de Decred y sus tres principios: seguro, adaptable y sustentable. El sitio web refleja mensajes acordados que posicionan a Decred como una reserva de valor superior basada en esos tres principios.

Decred in Depth lanzó dos episodios en febrero, [Decred, an Economic Breakthrough](https://decredindepth.libsyn.com/ammar-nasier-decred-an-economic-breakthrough) con @ammarooni y [DCR in LATAM](https://decredindepth.libsyn.com/elian-huesca-dcr-in-latam) con @elian. Además, @mr.black trabajó con @Checkmate y @permabullnino para lanzar un nuevo podcast centrado en el comercio titulado [Rough Consensus](https://roughconsensus.libsyn.com/rough-consensus-1-rough-start).

DCR Comic lanzó el sitio web [dcrcomic.org](https://dcrcomic.org/) que aloja todo el trabajo producido por el equipo, del cual el último cómic explica la Red [Lightning](https://twitter.com/DCRComic/status/1229792848188444672).

@Checkmate publicó una pieza extremadamente interesante sobre el debate [ProgPoW](https://medium.com/@_Checkmatey_/observing-ethereum-governance-during-the-progpow-debate-9bf1aec724ad) en Ethereum que describe las deficiencias del sistema de gobernanza de Ethereum y cómo las herramientas y metodologías de Decred pueden emplearse para resolverlas. Es un excelente ejemplo de inserción de los puntos de diferenciación de Decred en conversaciones más amplias, y fue bien recibido por muchos en la comunidad Ethereum, incluido [David Hoffman](https://twitter.com/TrustlessState/status/1234653059424358400), coanfitrión del podcast POV Crypto.

@dezryth publicó la primera [actualización](https://scottrchristian.com/2020/02/15/dezryth-proposal-updates/) de su propuesta de Facebook y Eventos para el mes de enero.

Monde PR se unió y [estableció ](https://github.com/decredcommunity/pr/pull/7) rápidamente los objetivos de relaciones públicas del proyecto, audiencias objetivo, mensajes clave, puntos de credibilidad, temas clave documentados, realizó un [análisis de la competencia](https://github.com/decredcommunity/pr/blob/release/competitor-analysis.csv), documentó a todos los portavoces, creó historias clave para lanzar e incluso comenzó la divulgación, produciendo un número de ubicaciones valiosas:

- Un [artículo](https://cointelegraph.com/news/the-state-of-blockchain-experts-weigh-in-on-adoption-around-the-world) en Cointelegraph con comentarios de @elian y @akinsawyerr sobre la adopción de blockchain en todo el mundo.
- Un [artículo](https://www.financemagnates.com/cryptocurrency/news/does-china-control-bitcoin-and-ethereum/) en Finance Magnates que presenta los comentarios de @jy-p sobre la centralización de la minería de Bitcoin y los modelos de consenso.
- Un [artículo](https://eng.ambcrypto.com/bitcoin-building-a-nation-on-the-foundation-of-maximalism/) en AMB Crypto con comentarios de @richardred sobre Bitcoin construyendo una nación.

## Eventos

![#DecredGlobalMeetup in Mexico](./assets/decredglobalmeetup-mexico-384.jpg)

_Imagen: #DecredGlobalMeetup en México_

Asistidos:

- 4-6 de febrero - [África Tech Summit](https://www.africatechsummit.com/kigali/) - Kigali, Rwanda. @akinsawyerr y @beansgum asistieron a este evento de más de 600 visitantes y Akin compartió su experiencia de conectarse con reguladores, startups y VCs en un [reporte completo](https://github.com/decredcommunity/events/blob/master/reports/20200204-africa-tech-summit-kigali-rwanda.md). ""Cuando Decred esté listo para buscar activamente casos de uso que se desarrollen, habrá muchas manos abiertas y capaces disponibles para interactuar".
- 6 de febrero - [Decred Global Meetup](https://www.meetup.com/Chicago-Decred-Meetup/events/267784883/) - Chicago, USA. ([notas](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$158109310014665NneQF:decred.org))
- 6 de febrero - [Decred Global Meetup](https://www.meetup.com/DecredBrasil/events/268457863/) - Belo Horizonte - Brazil. ([fotos](https://twitter.com/Jackson_Duarte/status/1225722800972890112))
- 6 de febrero - [Decred Global Meetup](https://www.eventbrite.com/e/decredglobalmeetup-en-buenos-aires-tickets-90817259869) - Buenos Aires, Argentina. Alojado por @EspacioBitcoin. ([fotos](https://twitter.com/cryptorc_tech/status/1225879454158901248))
- 6 de febrero - [Decred Global Meetup](https://www.eventbrite.com/e/decredglobalmeetup-ciudad-de-mexico-en-bitcoin-embassy-bar-tickets-90619377999) - Ciudad de México, México. Alojado por el Bitcoin Embassy Bar. ([fotos](https://twitter.com/bitcoinemb/status/1228091984906113025), [video](https://twitter.com/Decred_ES/status/1225656932431626241))
- 6 de febrero - [Decred Global Meetup](https://www.meetup.com/DecredBrasil/events/268449660/) - Natal, Brazil. @guisso: una parte divertida de las camisetas es que al principio se mostraban en la mesa de entrada y nadie mostró interés, pero al final del evento, cuando conocieron el proyecto, todos querían participar". ([foto](https://twitter.com/_fguisso/status/1225620169654927360))
- 6 de febrero - [Decred Global Meetup](https://www.meetup.com/DecredBrasil/events/268455983/) - Rio de Janeiro, Brazil. No había escasez de cerveza. ([foto](https://matrix.to/#/!MgQoetFiyjrHAywokv:decred.org/$158119750815292FWqOn:decred.org))
- 6 de febrero - [Decred Global Meetup](https://www.meetup.com/DecredBrasil/events/268456316/) - São Paulo, Brazil. ([foto](https://twitter.com/Decred_ES/status/1225574822928928768))
- 6 de febrero - [Discover Decred](https://www.meetup.com/DecredCanada/events/268147731/) - Toronto, Canadá. ([foto](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$158104000314467WqrCH:decred.org))
- 6 de febrero - [Decred Global Meetup](https://www.meetup.com/DecredBrasil/events/268496816/) - Salvador, Brazil. ([fotos](https://matrix.to/#/!MgQoetFiyjrHAywokv:decred.org/$158119740315283cQkoQ:decred.org))
- 8 de febrero - [Blockchain and AI](https://www.eventbrite.com/e/blockchain-and-ai-best-tools-for-the-development-of-nations-tickets-91389994935) - Casablanca, Morocco. Este evento contó con el segundo Decred Cake conocido públicamente. (fotos: [twitter](https://twitter.com/DecredArabia/status/1226266689492410368), [matrix](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$158119875815325RomyP:decred.org))
- 8 de febrero - [Decred Crypto Hangout](https://www.eventbrite.com/e/decred-crypto-hangout-learn-about-career-opportunities-in-the-industry-tickets-91830803405) - Lagos, Nigeria. Los contribuyentes de Five Decred compartieron conocimientos sobre varios aspectos de Decred. Al evento asistieron más de 25 personas y representantes de @yellowcardio, @HuobiAfrica y @Telos4africa. ([reporte](https://github.com/decredcommunity/events/blob/master/reports/20200208-decred-crypto-hangout-lagos-nigeria.md))
- 27 de febrero - [3er After UX Crypto](https://www.eventbrite.com.ar/e/3er-after-ux-crypto-sponsor-decred-tickets-95737271757) - Santa Fe, Argentina. Decred fue un patrocinador. ([fotos](https://twitter.com/Decred_ES/status/1233159907194605572))
- 27 de febrero - Decred and Stamping.io Meetup - Lima, Perú. @victorarubin presentó Decred a Stamping.io y Life Community Leadership en Lima, asistieron alrededor de 60 personas. ([video](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$1582953585375340iScnJ:matrix.org))

Próximos eventos:

- 12 de marzo - Women in Blockchain - Ciudad de México, México. Alojado por el Bitcoin Embassy Bar.
- 12 de marzo - Decred Meetup - Montevideo, Uruguay.
- 12-13 de marzo - [Blockchain Summit Latam](https://www.blockchainsummit.la) - Ciudad de Panamá, Panamá. Decred va a ser patrocinador bronce.
- 17 de marzo - Decred Meetup - Bilbao, España.
- 18 de marzo - Decred Meetup - Barcelona, España.
- 18 de marzo - [Campus Party Amazonia](https://brasil.campus-party.org/campus-party-amazonia-2020/) - Manaus, Brazil. Decred tendrá 2 charlas y varias otras actividades.
- 20 de marzo - [BlockchainUA](https://blockchainua.com/en/) - Kyiv, Ucrania. Los oradores quieren representar a Decred en el evento más grande de Europa del Este. Póngase en contacto con @cryptotexty en la sala de [#events](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org) para más detalles.
- 20-21 de marzo - [CIBTC Blockchain Summit](http://cibtc.es/) - Motril, España. Decred será una patrocinadora de oro.
- 24 de marzo - Decred Meetup - Santiago, Chile.
- 24 de marzo - Decred Meetup - Madrid, España.
- 26 de marzo - Decred Meetup - Vigo, España.
- 27 de marzo - Decred Meetup - Valencia, España.
- 28 de marzo - [DevOpsDays](https://devopsdays.org/events/2020-natal/welcome/) - Natal, Brazil. @guisso presentará lo que se necesitó para implementar un entorno de prueba para dcrlnd con docker-compose.
- 5 de abril - [Toronto Blockchain Week](https://www.eventbrite.ca/e/discover-decred-an-autonomous-digital-currency-toronto-blockchain-week-tickets-91562362491) - Toronto, Canadá. @ammarooni, @michae2xl y probablemente también @zubair planean estar allí.
- 9 de abril - Bitcoin Road Trip - Buenos Aires, Argentina.
- 13-17 de abril - [Talent Land en Jalisco](https://www.talent-land.mx/en/home/) - Guadalajara, México. Decred es un patrocinador de bronce.
- 24 de abril - Decred Meetup - La Paz, Bolivia.
- 6 de mayo - [Bitcoinference](https://www.eventbrite.com/e/bitcoinference-where-the-blockchain-meets-you-tickets-94598812595) - Cancún, México.
- 30-31 de mayo - [Bitconf](https://www.bitconf.com.br/portal/) - São Paulo, Brazil. Decred tendrá múltiples charlas sobre diversos temas.

## Media

Artículos seleccionados:

- El reporte de marketing de 2019 aprobado por @Dustorf da cuenta del esfuerzo de marketing de 2019, en el que se gastaron 785K USD (similar al año anterior). El informe también tiene reflexiones sobre cómo evolucionar y descentralizar el esfuerzo de marketing del proyecto ([blog.decred.org](https://blog.decred.org/2020/02/26/Decred-2019-Marketing-Report/))
- Decred On-Chain: Ticket Funding Rates por @permabullnino ([medium](https://medium.com/@permabullnino/decred-on-chain-ticket-funding-rates-4e7233c7b64f))
- Decred On-Chain: Macro + Micro Outlook por @permabullnino ([medium](https://medium.com/@permabullnino/decred-on-chain-macro-micro-outlook-12a26930623e))
- Decred, The Resilient Stronghold por @Checkmate, errando la serie de 3 partes mirando Bitcoin y Decred en términos de resiliencia, psicología agregada y adopción de usuarios ([medium](https://medium.com/decred/decred-the-resilient-stronghold-4038dc64dd2a))
- Nueva edición de [Decred Drive](https://medium.com/@decreddrive) continuó apareciendo todos los jueves por cortesía de @DecredDragon - gracias también por sus amables palabras sobre el Journal, del equipo.
- CryptoEQ le otorgó a Decred una calificación de Bronce, citando preocupaciones con un alto costo en dólares para comprar un ticket, una inflación relativamente alta en comparación con otras monedas SoV y el costo de un ticket cada vez más volátil. ([cryptoeq.io](https://cryptoeq.io/coreReports/decred-abridged))
- The State of Blockchain: Los expertos analizan la adopción en todo el mundo por Joseph Birch - presentando a @elian en LATAM y @akinsawyerr en áfrica ([cointelegraph.com](https://cointelegraph.com/news/the-state-of-blockchain-experts-weigh-in-on-adoption-around-the-world))
- After Four Years, is Decred Better than Bitcoin Yet? por Liam Kelly ([cryptobriefing.com](https://cryptobriefing.com/after-four-years-is-decred-better-bitcoin-yet/))

Traducciones:

- El Decred Journal de enero del 2020 se tradujo al árabe (@arij), chino (@Dominic) y español (@francov_). ¡Gracias a todos por correr la voz!

Videos:

- "Why DEX", En pocas palabras, cita ilustrada de @ moo31337 sobre las diferentes motivaciones de los banqueros y desarrolladores de software libre, producida por @Exitus ([youtube](https://www.youtube.com/watch?v=TNcmLrSPMRc))
- Decred Bi-Weekly News Update - 25 de Febrero, 2020 por @Exitus, esta es la primera actualización quincenal que se entrega como parte de la propuesta aprobada ([youtube](https://www.youtube.com/watch?v=RMqrIZcR-Iw))
- @ivandecredfan ha seguido haciendo videos educativos de Decred en ruso incluso después de que su propuesta fallara ([youtube](https://www.youtube.com/channel/UCFjXbEDeyhhj2bH2t_eGKGA))

Audios:

- Decred in Depth Ep. 18. @elian habla sobre la vida en el camino que representa a Decred en todo LATAM, diferentes casos de uso en diferentes lugares y una estrategia para acentuar el contingente tropical de la comunidad global de Decred. ([libsyn](https://decredindepth.libsyn.com/elian-huesca-dcr-in-latam), [soundcloud](https://soundcloud.com/decredindepth/elian-huesca-dcr-in-latam))
- Rough Consensus Ep. 1. @Checkmate y @permabullnino abren un nuevo programa, hablando sobre derivados, alt season y la dinámica de blockchain. ([libsyn](https://roughconsensus.libsyn.com/rough-consensus-1-rough-start))
- Decred in Depth Roundup Ep. 1 (o Ep. 20 de Decred in Depth). Únase a @Checmkate, @permabullnino y @mr.black para una discusión sobre la financiación y la seguridad de blockchain, el ataque del 51% y sus últimos proyectos. ([soundcloud](https://soundcloud.com/decredindepth/dcr-round-up-with-checkmate))

## Discusiones de la comunidad

Noticias de sistemas de comunicación:

- El puente Slack a Matrix y Discord fue dado de baja el 28 de febrero y la mayoría de los canales se cerraron. Los problemas que llevaron a esta decisión incluyen el cierre disruptivo de las invitaciones automáticas en 2018, los DM y otros antecedentes que desaparecen después de aproximadamente una semana, y la migración de la mayoría de los moderadores activos a Matrix. Aquellos que deseaban continuar siguiendo y participando en los chats se mudaron a Matrix y Discord, al resto les decimos una cariñosa despedida.
- @Exitus purgó las cuentas inactivas de Discord, consolidando su férreo control del poder entre los habitantes de Decred en Discord. La poda eliminó las cuentas que no fueron verificadas y que no habían iniciado sesión en más de 30 días. Cualquier cuenta eliminada es libre de volver a unirse y pasar por el proceso de verificación.
- El equipo de DCRComic agregó un paquete de calcomanías en Telegram, que se pueden agregar siguiendo este [enlace](https://t.me/addstickers/DCRComic) o haciendo clic en una calcomanía publicada por otra persona en el chat. ¡Los usuarios de Telegram ahora tienen la opción de dos paquetes de pegatinas temáticas de Stakey! El nuevo conjunto complementa el [conjunto existente](https://t.me/addstickers/dcrstakey) de pegatinas Stakey producidas por @lustosa. ¡Parece que fue una buena decisión no gastar $ 1,400 en un conjunto adicional de calcomanías de Telegram de esa [propuesta](https://proposals.decred.org/proposals/4acb95564d36488a7ee64683a84dd7954982b2f4743e2f7a15477231f863442f) hace 2 meses!

Publicaciones seleccionadas de Reddit:

- @Checkmate compartió su [lista de deseos](https://www.reddit.com/r/decred/comments/f4i870/decred_wishlist/) para Decred, y otros respondieron con sus pensamientos sobre las sugerencias de @Checkmate, y algunas sugerencias propias.
- El reporte de marketing de Decred vio [15 comentarios](https://www.reddit.com/r/decred/comments/fa70c3/decred_2019_marketing_report/), algunos celebrándolo, otros discutiendo aspectos de él.

Debates seleccionados en Twitter:

- @Exitus identificó y extrajo un [clip](https://twitter.com/coveryfire7777/status/1229517588138528768) e un video de Ark Invest, donde Cathie Wood menciona a Decred como "prometedor".
- @degeri [compartió](https://twitter.com/degeri_crypto/status/1233658256737918976) una captura de pantalla de Altered Carbon Temporada 2 Episodio 5, donde los precios se cotizan en la pantalla en una variedad de criptomonedas, incluido Decred. DCR es la única moneda que se muestra con dos números, y esto generó especulaciones sobre lo que eso significó para la interpretación de la predicción de precios de 2400 para DCR de este año.
- @jy-p está de vuelta en Twitter después de un largo paréntesis, y se [pregunta](https://twitter.com/behindtext/status/1232381271252271104) qué están haciendo las personas que trabajan en proyectos de cc y que no están desarrollando activamente oráculos.
- el [hilo](https://twitter.com/RichardRed0x/status/1231223498787508224) de @richardred sobre la DAO de Decred, impulsado por una [respuesta](https://medium.com/@rzs/im-continually-amazed-at-the-lack-of-attention-decred-gets-4a40679246ba) de @rzs en Medium preguntando por qué Decred no apareció una [actualización](https://medium.com/@rebeccarachmany/dao-falloff-and-revival-2cf74f3c18c1) de la DAO.
- [DCR Time](https://twitter.com/DCRComic/status/1232714622819602432) obra de arte por DCR Comic.
- Chris Burniske con una linda [cita](https://twitter.com/cburniske/status/1227617853211336704) de Joel Monegro de su documento Sovereign Cryptonetworks, sobre Decred establecido para la soberanía a largo plazo gracias a sus principios de gobierno descentralizados.
- @Checkmate resume [el Fondo de Tesorería](https://twitter.com/_Checkmatey_/status/1224764330878603266) como el corazón del proyecto Decred.

## Mercados

En febrero, DCR cotizaba entre USD 16.71–24.75 / BTC 0.0019–0.0024. La tarifa diaria promedio fue de $20.48

## Noticias relevantes externas

El debate de Ethereum ProgPoW se volvió a encender con estilo cuando se aprobó entrar en una bifurcación dura en la llamada de los desarrolladores principales, lo que resultó en un desconcierto entre muchos en la comunidad más amplia de Ethereum, donde ProgPoW no tiene tanto apoyo. Este [post](https://hudsonjameson.com/2020-03-02-progpow-the-ethereum-community-speaks/) de Hudson Jameson da una cuenta de la historia de ProgPoW y llega a la conclusión de que mientras el cambio probablemente sea bueno, las amenazas para mantener una bifurcación contenciosa deben tomarse en serio y no vale la pena bifurcar la red. La comunidad Ethereum está utilizando una variedad de mecanismos de señalización, incluidos Twitter [encuestas](https://twitter.com/crypt0snews/status/1231288498474209280) y EIP [cartas abiertas](https://github.com/MidnightOnMars/EIPs/blob/master/EIPS/eip-2538.md) con campañas de hashtag. Como detalla la publicación de Hudson, ya se han realizado grandes esfuerzos para medir el sentimiento de la comunidad de Ethereum sobre ProgPoW, y tanto el voto de una moneda como el voto de los mineros estaban firmemente a favor de ProgPoW. Se han utilizado una variedad de otros métodos para recopilar señales de la comunidad, incluido [Kialo](https://www.kialo.com/ethereum-and-programmatic-proof-of-work-progpow-30878) y probablemente un número de publicaciones de Reddit. @Checkmate se ha unido al debate con algunas [observaciones](https://medium.com/@_Checkmatey_/observing-ethereum-governance-during-the-progpow-debate-9bf1aec724ad) sobre cómo se maneja esto, informado por su experiencia con el enfoque de Decred. El problema con la gobernanza informal es que, independientemente de la cantidad de recopilación de señales que tenga lugar y si todos tienen la oportunidad de hablar, inevitablemente habrá algunas personas que tendrán que hacer un juicio y avanzar para trazar una línea debajo de ella. Es un proceso desordenado y al final muy pocas personas se sienten satisfechas con el resultado.

Hay indicios de importantes [conflictos](https://decrypt.co/19769/zaki-manian-cosmos-number-two-resigns) en Tendermint, la compañía detrás de la cadena de bloques Cosmos, con el número dos Zaki Manian renunciando de Tendermint a formar su propia compañía centrada en Cosmos, diciendo que el CEO (Jae Kwon) está dificultando el progreso al subcontratar el desarrollo y enfocarse en un nuevo proyecto (Virgo) y Twitter (@jaesustein). Esta [actualización](https://gist.github.com/jaekwon/8861452eea20def46b89dfcc79c9212e#file-zaki_and_ref_god-md) de Jae ilustra el grado inusual en que el concepto de piedad ha entrado en juego en la disputa. Cosmos recaudó $17 millones en una ICO 2017, con un valor de unos $mil millones, unos meses después, en marzo de 2019 el proyecto recaudó otros $9 millones cuando se lanzó la primera iteración de la red, pero las señales ahora son que el progreso hacia un centro de blockchain en funcionamiento ha sido limitado desde entonces.

El CEO de Block.one, Brendan Blumer [despertó](https://twitter.com/BrendanBlumer/status/1232318319061061632) para descubrir que las reglas de la red EOS habían cambiado de la noche a la mañana, con 15 BP proponiendo y aprobando el cambio para reducir la emisión del 5% al 1%. Lo que sucedió no es exactamente una sorpresa, porque en ningún momento se ha realizado un esfuerzo significativo para desarrollar el "Sistema de Propuesta de Trabajador" planificado descrito en el documento técnico. El 4% no utilizado se ha acumulado en una dirección no utilizada, y el EOS acumulado ya se ha quemado una vez. Por qué el fondo WPF finalmente se cerró en esta noche en particular 18 meses después es un misterio al que solo los 15 EOS BP involucrados saben la respuesta. ¡Nadie le dio aviso a Brendan! Sin embargo, está bien con eso, las reglas que cambian de la noche a la mañana es cómo funciona la gobernanza descentralizada cuando solo hay 15 partes involucradas.

Los desarrolladores de Bitcoin ABC han [lanzado](https://www.bitcoinabc.org/2020-02-15-miner-fund/) detalles de su plan para implementar una variante del financiamiento de recompensa en bloque propuesto por Jiang Zhuoer de BTC. PARTE SUPERIOR. Esta implementación alterará los siguientes detalles del plan: cantidad reducida al 5%, los fondos pueden ir a cualquier proyecto incluido en la lista blanca y el plan solo entrará en vigencia si los mineros lo activan a través de BIP9. Queda una considerable [oposición](https://twitter.com/PeterRizun/status/1228787028734574592) a la idea de que cualquier desarrollador reciba fondos del bloque BCH.

Binance ha estado involucrado en una [disputa](https://cointelegraph.com/news/binance-returns-frozen-btc-after-user-promises-not-to-use-coinjoin) con uno de sus usuarios que había usado la billetera Wasabi para mezcla sus transacciones en CoinJoin y mejorar su privacidad. La actividad de mezcla elevó el puntaje de riesgo del usuario y sus fondos se congelaron mientras Binance investigaba. Finalmente, el usuario acordó retirar sus fondos, lo que no fue bien recibido por Binance, quien hizo referencia al cumplimiento de la ley de Singapur para explicar sus acciones. ¡El usuario tenía que prometer no mezclar más sus monedas antes de que Binance las devolviera! Hasta ahora no ha habido informes de mezcladores DCR marcados de esta manera.

Tim Copeland consideró las implicaciones de privacidad de los dominios de Ethereum Name Service (.ens) en un [artículo](https://decrypt.co/19423/we-tracked-133000-ethereum-names-and-exposed-their-secrets) en descifrar. Aunque muchos usuarios sabían que podían dañar su privacidad al vincular su dirección de dominio con sus otras direcciones, la transacción que solían pagar por sus .ens también se podía utilizar para vincularlos a sus fondos.

Blockstream está ingresando a la banca, siendo nombrado socio tecnológico estratégico de Avanti Financial Group, un [nuevo](https://avantibank.com/) banco estadounidense dedicado a activos digitales - [cubierto](https://coinspice.io/news/blockstream-bank-to-service-instituciones-clientes-planes-principios-2021-apertura/) por CoinSpice(con ilustraciones). Los términos no fueron revelados.

Casa está liquidando [down](https://www.coindesk.com/bitcoin-startup-casa-names-new-ceo-as-node-service-goes-open-source) su producto de hardware de nodo, del cual tiene vendió 2,000 unidades, y también [open](https://blog.keys.casa/open-sourcing-the-casa-node/) obteniendo su código. Casa se centrará en su servicio de suscripción de $10/mes para la gestión de claves.

Justin Sun de Tron tuvo un mes ocupado, [comprando](https://news.bitcoin.com/steemit-for-sale-tron/) el sitio web de contenido steemit.com que se basa (y el uso principal de) Steem blockchain e inmediatamente anunció que steemit.com se mudaría a la cadena de bloques Tron. Esto llevó a los testigos de Steem (productores de bloques) a promulgar un [fork suave](https://www.coindesk.com/justin-sun-bought-steemit-steem-moved-to-limit-his-power) que se congelaría la "participación minada ninja Steemit Inc", una gran cantidad desconocida de STEEM mantenida en varias cuentas por la compañía. El 1 de marzo, Justin [golpeó](https://www.coindesk.com/steem-community-mobilizes-popular-vote-in-battle-with-justin-sun) de nuevo reclutando intercambios (Binance y Huobi) para votar para un conjunto de testigos bajo su control que revertiría el fork suave y liberaría el STEEM. Después de la reacción de los usuarios, parecía que tanto [Binance](https://twitter.com/cz_binance/status/1234676941111742467) como [Huobi](https://medium.com/huobi-global/community-counts-a-letter-to-la-comunidad-steem-340881448ea7) iban a desarmar su STEEM y retirarse de cualquier acuerdo que tuvieran con Sun.

También ha habido alguna [sugerencia](https://bitcoinexchangeguide.com/did-justin-sun-rig-super-rep-election-two-tron-dapps-received-votes-from-zion-account/) de que Justin Sun usó los votos de la cuenta "Zion" para interferir con la votación comunitaria de Tron Apps, que él [apareció](https://twitter.com/justinsuntron/status/1230215220884201472) para confirmar, declarando que era temporal hasta que los 3 súper representantes actualizaran su software para "evitar que dañen la red".

El coordinador de IOTA fue apagado, [pautando con](https://bitcoinist.com/iota-trinity-wallet-vulnerability-1-6-million-stolen/) la red, el 13 de febrero, para investigar las reclamaciones de los robos de billeteras Trinity $1.6 millones. IOTA entró en un estado de calamidad elevada cuando, después de varios días de inactividad con el coordinador, fue [revelado](https://blog.iota.org/trinity-attack-incident-part-1-summary-y-next-steps-8c7ccc4d81e8) que todas las claves privadas de todos los usuarios del cliente Trinity de escritorio (mantenidas por la Fundación IOTA) se vieron comprometidas. Se han robado 8,55 Ti de IOTA, por un valor de aproximadamente $2.3 millones en ese momento. Trinity se vio comprometido por el código malicioso insertado en una dependencia de terceros del servicio MoonPay que permitió a los usuarios comprar tokens IOTA directamente dentro de Trinity. El [último reporte](https://cointelegraph.com/news/iota-prepares-to-relaunch-network-in-one-week) indica que hay una versión fija de Trinity y una herramienta de migración de semillas y los titulares de IOTA tienen 7 días para someterse al procedimiento de transferencia antes de que la fundación reinicie la red entre el 7 y el 10 de marzo. IOTA ha perdido el 30% de su valor en términos de USD al momento de la escritura (5 de marzo), pero los usuarios que poseen su propio IOTA han sido incapaces de moverlos ya que la red estaba en pausa.

El tribunal de Aragón se ha [lanzado](https://blog.aragon.org/launching-aragon-court/), con el objetivo de proporcionar una jurisdicción digital para que los DAO operen. 247 miembros del jurado se inscribieron para el lanzamiento mediante la participación colectiva de 1 millón de ANT (por un valor de ~ $1.3 millones). Para comenzar, los miembros del jurado están completando una "[campaña de precedencia](https://blog.aragon.org/precedence-campaign-primer/)" (ejercicio de capacitación del jurado) con [simulacro](https://twitter.com/Yazanator/status/1228752714873462784) disputas.

La versión beta pública de Colony se ha [abierto](https://blog.colony.io/the-colony-public-beta-is-live/). Colony es una plataforma para crear DAOs en Ethereum. Las colonias individuales no se enumeran públicamente, por lo que no está claro cuántas hay hasta el momento o para qué se utilizan. Colony planea convertirse en una empresa pública autosuficiente, gobernada a través de una "Metacolonia", que tendrá sus propios tokens CLNY en el futuro. Como precursor de eso, se lanzó ["Betacolony](https://colony.io/colony/beta)" este mes y financiado con 10,000 DAI - los contribuyentes pueden ganar tokens DAI y BLNY completando tareas, que van desde arreglar el soporte de la cartera de hardware hasta bloguear o tuitear sobre Colony. No hay signos de herramientas de toma de decisiones en la Betacolonia, en cambio, los administradores pueden crear tareas que luego son completadas por los miembros y validadas por los administradores, que procesan los pagos de recompensas.

El proyecto DeFi bZx ha estado en el centro de varias [historias](https://www.coindesk.com/everything-you-ever-wanted-to-know-about-the-defi-flash-loan-attack) sobre exploits este mes, con su nueva función de "préstamo flash" que se utiliza de manera creativa para establecer una serie de transacciones que manipularon oráculos de precios e inmediatamente se beneficiaron de ellos. El aspecto novedoso de estos exploits es que todas las transacciones se procesan en el mismo bloque, ya sea que haya un beneficio para el atacante o que la transacción no sea válida, lo que hace que el atacante tenga un riesgo muy bajo ya que no se les exige que proporcionen garantías. Después del exploit, la clave maestra se usó para editar los contratos inteligentes para que no pudieran ser explotados de la misma manera por más tiempo.

Otro grupo se [adelantó](https://medium.com/@1inch.exchange/yes-we-hacked-bzx-fulcrum-but-one-month-ago-3f7e5c437ee3) para decir que habían advertido a bZx sobre el tema un mes antes y no quedaron impresionados con su respuesta, incluida la negativa a pagar una recompensa razonable basada en un tecnicismo.

12 intercambios fueron pirateados en 2019 por un daño total de casi $300 millones y 510,000 inicios de sesión de usuarios, según un [informe de enero](https://cointelegraph.com/news/most-significant-hacks-of-2019-new-record-de-doce-en-un-año) por Cointelegraph. Esto sirve como un recordatorio para tener cuidado al seleccionar un intercambio para enviar monedas o documentos confidenciales.

## Sobre esta edición

Este es el journal de Decred número 23. Un índice completo, y de todas las traducciones, se encuentra [aquí](https://xaur.github.io/decred-news/).

La mayoría de la información de terceros se transmite directamente desde la fuente después de un control mínimo. Los autores de Decred Journal no tienen la capacidad de verificar todos los reclamos. Tenga cuidado con las estafas y haga su propia investigación.

Sus [comentarios](https://github.com/xaur/decred-news/blob/docs/contributing.md#feedback) y [contribuciones](https://github.com/xaur/decred-news/blob/docs/contributing.md) son siempre bienvenidos.

Créditos (orden alfabético):

- escritura y edición: bee, degeri, Dustorf, francov\_, guisso, l1ndseymm, richardred
- revisiones y comentarios: ay-p, chappjc, davecgh, dnldd, emiliomann, jholdstock, lukebp, matheusd, raedah
- traducción al español: @Francov_
