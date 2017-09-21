---
title: Novedades de Cloud App Security | Microsoft Docs
description: "Este tema se actualiza con frecuencia para informarle de las novedades de la versión más reciente de Cloud App Security."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 9/3/2017
ms.topic: article
ms.prod: 
ms.service: cloud-app-security
ms.technology: 
ms.assetid: d418ef3d-76ee-45d5-b5ae-21346e5239a3
ms.reviewer: reutam
ms.suite: ems
ms.openlocfilehash: bacc5264d36e0948b0e802b2fbb9e04d9a058af9
ms.sourcegitcommit: de133f251ceab10d9c2306dd76e75a68db206743
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/03/2017
---
# <a name="whats-new-with-cloud-app-security"></a>Novedades de Cloud App Security


## <a name="cloud-app-security-release-104"></a>Notas de la versión 104 de Cloud App Security 
Fecha de publicación: 27 de agosto de 2017

-   Ahora puede agregar intervalos de direcciones IP de forma masiva creando un script mediante la [API de intervalos de direcciones IP](https://portal.cloudappsecurity.com/api-docs/). 
-   Cloud Discovery ahora ofrece una visibilidad mejorada de las transacciones bloqueadas. Para ello, presenta tanto las transacciones totales como las bloqueadas.
-   Ahora puede filtrar aplicaciones en la nube según si tiene la certificación **ISO 27017** o no. Este nuevo factor de riesgo del catálogo de aplicaciones en la nube determina si el proveedor de la aplicación tiene esta certificación, que establece los controles y las directrices comúnmente aceptados para el procesamiento y la protección de la información de los usuarios en un entorno público de computación en la nube.
- Para ayudarle a prepararse para el cumplimiento de RGPD, hemos recopilado las instrucciones de preparación de RGPD desde las aplicaciones en la nube del catálogo de aplicaciones en la nube. Aún no afecta a la puntuación de riesgo de la aplicación, pero ofrece un vínculo a la página de preparación de RGPD del editor de la aplicación, cuando se proporciona. Microsoft no ha comprobado el contenido y no es responsable de su validez.


## <a name="cloud-app-security-release-103"></a>Notas de la versión 103 de Cloud App Security 
Publicado el 13 de agosto de 2017

- Cloud App Security ahora incluye compatibilidad de protección nativa de Azure Information Protection con los siguientes archivos de Office: .docm, .docx, .dotm, .dotx, .xlam, .xlsb, .xlsm, .xlsx, .xltx, .xps, .potm, .potx, .ppsx, .ppsm, .pptm, .pptx, .thmx, .vsdx, .vsdm, .vssx, .vssm, .vstx, .vstm (en lugar de protección genérica).

- A cualquier administrador de cumplimiento de Azure Active Directory se le otorgarán automáticamente permisos similares en Cloud App Security, incluida la capacidad de solo lectura y de administrar alertas, crear y modificar directivas de archivo, permitir acciones de control de archivos y ver todos los informes integrados en Administración de datos. 

- Se ha ampliado el contexto de infracción de DLP de 40 a 100 caracteres para ayudarle a entender mejor el contexto de la infracción.

- Se incluyen mensajes de error detallados en la herramienta de carga de registros personalizados de Cloud Discovery para permitirle solucionar fácilmente los errores en la carga de registros.

- El script del bloque de Cloud Discovery se ha ampliado para admitir el formato de Zscaler.

- Nuevo factor de riesgo del Catálogo de aplicaciones en la nube: retención de datos después de la finalización de la cuenta. Esto le permite asegurarse de que los datos se quitan completamente una vez que finaliza una cuenta dentro de una aplicación en la nube.


## <a name="cloud-app-security-release-102"></a>Versión 102 de Cloud App Security 
Publicada el 30 de julio de 2017
 
-   Debido a que la información de dirección IP es fundamental para casi todas las investigaciones, ahora puede ver información detallada sobre las direcciones IP en el cajón de actividades. Desde una actividad específica, ahora puede hacer clic en la pestaña de dirección IP para ver los datos consolidados sobre la dirección IP, incluido el número de alertas abiertas para la dirección IP específica, un gráfico de tendencias de la actividad reciente y un mapa de ubicación. Esto permite explorar en profundidad; por ejemplo, cuando se investigan alertas de viajes imposibles, puede comprender fácilmente dónde se usó la dirección IP y si participó o no en actividades sospechosas. También puede realizar acciones directamente en el cajón de direcciones IP que le permiten etiquetar una dirección IP como riesgosa, VPN o corporativa para facilitar una investigación futura y la creación de directivas. Para más información, consulte el artículo sobre [información de dirección IP](activity-filters.md#ip-address-insights)

-   En Cloud Discovery, ahora puede usar [formatos de registros personalizados](custom-log-parser.md) también para [cargas de registros automatizadas](discovery-docker.md). Esto le permite automatizar fácilmente la carga de registros desde SIEM como servidores Splunk o cualquier otro formato no compatible. 
 
-   Las nuevas acciones de investigación de usuario permiten un nivel agregado de exploración en las investigaciones de usuario. En las páginas **Investigación**, ahora puede hacer clic con el botón derecho de una actividad, usuario o cuenta y aplicar uno de los siguientes filtros nuevos para una investigación y filtración avanzadas: **Ver actividad relacionada**, **Ver gobierno relacionado**, **Ver alertas relacionadas**, **Ver archivos con propietario**, **Ver archivos compartidos con este usuario**.

-   El Catálogo de aplicaciones en la nube ahora contiene un campo nuevo de retención de datos después de la terminación de la cuenta. El factor de riesgo le permite asegurarse de que los datos se quitan completamente una vez que da término a una cuenta dentro de una aplicación de nube.

-   Cloud App Security ahora cuenta con mayor visibilidad de las actividades relativas a objetos de Salesforce, como clientes potenciales, cuentas, campañas, oportunidades, perfiles y casos. Por ejemplo, la visibilidad sobre el acceso de las páginas de cuentas le permite configurar una directiva que le envía una alerta si un usuario ve una cantidad inusualmente grande de páginas de cuentas. Esto está disponible a través del conector de aplicaciones de Salesforce si tiene habilitada la supervisión de eventos de Salesforce en Salesforce (parte de Salesforce Shield).

- No realizar seguimiento ahora está disponible para los clientes de la versión preliminar privada. Ahora puede controlar qué datos de actividad de los usuarios se procesan. Esto le permite establecer grupos específicos de Cloud App Security como "No realizar seguimiento". Por ejemplo, ahora puede decidir no procesar ningún dato de actividad de usuarios ubicados en Alemania ni ningún país que no esté sometido a ninguna ley de cumplimiento específica. Esto se puede implementar en todas las aplicaciones en Cloud App Security para una aplicación específica e, incluso, para una subaplicación específica. Además, esta característica se puede usar para facilitar la implementación gradual de Cloud App Security. Para más información sobre la versión preliminar privada de esta característica o para unirse a ella, póngase en contacto con el soporte técnico o con su representante de cuenta. 



## <a name="cloud-app-security-release-100"></a>Notas de la versión 100 de Cloud App Security 
Publicado el 3 de julio de 2017
 

### <a name="new-features"></a>Nuevas características
-   **Extensiones de seguridad:** se trata de un nuevo panel para la administración centralizada de todas las extensiones de seguridad de Cloud App Security, incluida la administración de tokens de API, agentes SIEM y conectores de DLP externa. El nuevo panel está disponible en Cloud App Security en "Configuración". 
    - Tokens de API: genere y administre sus propios [tokens de API](api-tokens.md) para integrar Cloud App Security con software de terceros mediante nuestras API de RESTful. 
    - Agentes SIEM: antes la [integración SIEM](siem.md) se encontraba en "Configuración", pero ahora está disponible como una pestaña en Extensiones de seguridad.
    - DLP externa (versión preliminar): Cloud App Security permite [aprovechar las inversiones existentes en sistemas de clasificación de terceros](icap-stunnel.md), como soluciones de prevención de pérdida de datos (DLP), y permite examinar el contenido de aplicaciones en la nube mediante las implementaciones que se ejecutan en el entorno. Póngase en contacto con el administrador de cuentas para tomar parte en la versión preliminar. 
-   **Autorizar o no autorizar automáticamente:** las nuevas directivas de detección de aplicaciones permiten que Cloud Discovery aplique automáticamente a las aplicaciones la etiqueta Autorizada/No autorizada. De este modo, puede identificar automáticamente las aplicaciones que infringen la directiva y la normativa de la organización y agregarlas al script de bloqueo generado.
-   **Etiquetas de archivo de Cloud App Security:** actualmente se pueden aplicar etiquetas de archivo de Cloud App Security para proporcionar más información sobre los archivos que se examinan. Ahora ya puede saber si se ha impedido que la DLP de Cloud App Security inspeccione los archivos porque estaban dañados o cifrados. Por ejemplo, puede configurar directivas para que le alerten y pongan en cuarentena archivos protegidos con contraseña que se comparten externamente. Esta característica está disponible para los archivos examinados después del 3 de julio de 2017.

    Puede filtrar estos archivos mediante el filtro **Etiquetas de clasificación** > **Cloud App Security**: 
    - **Cifrado con Azure RMS**: archivos cuyo contenido no se ha inspeccionado porque tienen establecido un cifrado de Azure RMS.
    - **Cifrado con contraseña**: archivos cuyo contenido no se ha inspeccionado porque el usuario los ha protegido con una contraseña.
    - **Archivo dañado**: archivos cuyo contenido no se ha inspeccionado porque no se ha podido leer.
-   **Información de usuario**: la experiencia de investigación se ha mejorado para que incluya información predeterminada sobre el usuario activo. Con un solo clic, ahora puede ver una descripción detallada de los usuarios desde el cajón de actividades, incluida la ubicación desde la que se han conectado, con cuántas alertas abiertas están relacionados e información sobre sus metadatos.
-   **Información del conector de aplicaciones:** en **Conectores de aplicaciones**, cada aplicación conectada incluye ahora un cajón de aplicaciones en la tabla para explorar más fácilmente su estado. Entre los detalles que se proporcionan se incluyen cuándo se ha conectado el conector de aplicaciones y cuándo se ha realizado la última comprobación de estado del conector. También puede supervisar el estado del examen de DLP en cada aplicación, es decir, el número total de archivos inspeccionados por DLP, así como el estado de los exámenes en tiempo real (exámenes solicitados frente a exámenes reales). Podrá saber si el porcentaje de archivos examinados por Cloud App Security en tiempo real es inferior al número solicitado, y si el inquilino excede su capacidad y experimenta un retraso en los resultados de DLP.
-   **Personalización del Catálogo de aplicaciones en la nube:** 
    - **Etiquetas de aplicación**: ahora puede crear etiquetas personalizadas para las aplicaciones. Estas etiquetas pueden usarse como filtros para profundizar un poco más en los tipos de aplicaciones específicos que quiere investigar. Por ejemplo, lista de supervisión personalizada, asignación a una unidad de negocio específica o aprobaciones personalizadas (por ejemplo, "aprobado por el departamento legal").
    - **Notas personalizadas**: ahora, a medida que revise y evalúe las diferentes aplicaciones detectadas en el entorno, puede guardar las conclusiones y la información en notas.
    - **Puntuación de riesgo personalizada**: ahora puede reemplazar la puntuación de riesgo de una aplicación. Por ejemplo, si la puntuación de riesgo de una aplicación es 8 y es una aplicación autorizada en la organización, puede cambiar la puntuación de riesgo a 10 para la organización. También puede agregar notas para que el motivo de este cambio le quede claro a los usuarios que revisen la aplicación.
-   **Nuevo modo de implementación del recopilador de registros:** hemos empezado a aplicar un nuevo modo de implementación para el recopilador de registros. Además de la implementación actual basada en el dispositivo virtual, el nuevo recopilador de registros basado en Docker (contenedor) puede instalarse como un paquete en equipos Windows y Ubuntu locales y en Azure. Cuando se usa Docker, el cliente es el propietario del equipo host y puede aplicarle revisiones y supervisarlo libremente.

### <a name="announcements"></a>Anuncios: 
-   El Catálogo de aplicaciones en la nube ahora admite más de 15 000 aplicaciones reconocibles
-   Cumplimiento: Cloud App Security cuenta oficialmente con la certificación SOC1/2/3 de Azure. Si desea consultar la lista completa de certificaciones, consulte [Ofertas de Compliance](https://www.microsoft.com/trustcenter/compliance/complianceofferings) y filtre los resultados para ver Cloud App Security.

### <a name="other-improvements"></a>Otras mejoras: 
-   **Análisis mejorado:** se ha mejorado el mecanismo de análisis de registros de Cloud Discovery. Es mucho menos probable que se produzcan errores internos.
-   **Formatos de registro esperados:** ahora, el formato de registro esperado para los registros de Cloud Discovery proporciona ejemplos del formato Syslog y del formato FTP.
-   **Estado de carga del recopilador de registros:** ahora puede ver el estado del recopilador de registros en el portal y solucionar los errores más rápidamente gracias a las notificaciones de estado en el portal y las alertas del sistema.


## <a name="cloud-app-security-release-99"></a>Notas de la versión 99 de Cloud App Security 
Publicado el 18 de junio de 2017

### <a name="new-features"></a>Nuevas características

-   Ahora puede requerir a los usuarios que inicien sesión de nuevo en todas las aplicaciones de Office 365 y Azure AD como una solución rápida y eficaz en el caso de alertas de actividad sospechosa del usuario y cuentas en peligro. Encontrará la nueva acción de gobierno en la configuración de directiva y las páginas de alertas, junto a la opción Suspender usuario.
-   Ahora puede filtrar las actividades para **agregar asignación de roles de suplantación** en el registro de actividades. Esta actividad permite detectar si un administrador ha concedido un rol de **suplantación de aplicación** a una cuenta de usuario o del sistema, mediante el cmdlet **New-ManagementRoleAssignment**. Este rol permite al suplantador realizar operaciones con los permisos asociados a la cuenta suplantada, en lugar de con los permisos asociados a la cuenta del suplantador.
Mejoras de Cloud Discovery:
-   Ahora es posible mejorar los datos de Cloud Discovery con datos de nombre de usuario de Azure Active Directory. Cuando se habilita esta característica, el nombre de usuario que se recibe en los registros de tráfico de detección se hace coincidir con el nombre de usuario de Azure AD y se reemplaza por este, con lo que se habilitan las siguientes características nuevas:
  - Puede investigar el uso de Shadow IT por parte del usuario de Azure Active Directory.
  - Puede correlacionar el uso de las aplicaciones en la nube detectadas con las actividades de API recopiladas.
  - Después, puede crear registros personalizados en función de los grupos de usuarios de Azure AD. Por ejemplo, un informe de Shadow IT para un departamento de marketing específico.
-   Se han realizado mejoras en el analizador de Syslog de Juniper. Ahora admite los formatos welf y sd-syslog.
-   Se han realizado mejoras en el analizador de Palo Alto para optimizar la detección de aplicaciones.
-   Para comprobar que los registros se están cargando correctamente, ahora puede ver el estado de los recopiladores de registros en el portal de Cloud App Security. 

### <a name="general-improvements"></a>Mejoras generales:
-   Las etiquetas de dirección IP integradas y las etiquetas IP personalizadas ahora se consideran de forma jerárquica, y las etiquetas IP personalizadas tienen prioridad sobre las etiquetas IP integradas. Por ejemplo, si una dirección IP se etiqueta como **De riesgo** en función de la información disponible sobre las amenazas pero hay una etiqueta IP personalizada que la identifica como **Corporativa**, la categoría y las etiquetas personalizadas tendrán prioridad.


## <a name="cloud-app-security-release-98"></a>Notas de la versión 98 de Cloud App Security 
Publicado el 4 de junio de 2017
 
Actualizaciones de Cloud Discovery:
-   Ahora los usuarios pueden realizar un filtrado avanzado de las aplicaciones detectadas, lo que le permite realizar una investigación en profundidad, por ejemplo, filtrar las aplicaciones según su uso para saber cuánto tráfico de carga procede de las aplicaciones detectadas de ciertos tipos o cuántos usuarios han usado determinadas categorías de aplicaciones detectadas. También puede seleccionar al mismo tiempo varias categorías en el panel izquierdo. 
-   Se ha iniciado la implementación de nuevas plantillas para Cloud Discovery basadas en búsquedas frecuentes, por ejemplo, "aplicación de almacenamiento en la nube no compatible". Estos filtros básicos se pueden usar como plantillas para realizar el análisis de las aplicaciones detectadas.
-   Para facilitar el uso, ahora puede realizar determinadas acciones como autorizar y no autorizar varias aplicaciones de una sola vez.
-   Estamos implementando la capacidad de crear informes de detección personalizados en función de los grupos de usuarios de Azure Active Directory. Por ejemplo, si quiere ver el uso de la nube por parte del departamento de marketing, puede importar el grupo de marketing mediante la característica para importar grupos de usuarios y, después, crear un informe personalizado para este grupo.

Nuevas características:
-   Se ha completado la implementación de RBAC para los lectores de seguridad. Esta característica permite administrar los permisos concedidos a los administradores dentro de la consola de Cloud App Security. De forma predeterminada, todos los administradores globales y administradores de seguridad de Azure Active Directory y Office 365 tienen permisos completos en el portal, y todos los lectores de seguridad de Azure Active Directory y Office 365 tienen acceso de solo lectura en Cloud App Security. Puede agregar más administradores o reemplazar los permisos mediante la opción "Administrar acceso". Para obtener más información, consulte [Managing admin access](manage-admins.md) (Administración de permisos de administración).
-   Estamos implementando informes detallados de amenazas para las direcciones IP de riesgo detectadas por el gráfico de seguridad inteligente de Microsoft. Cuando una red de robots (botnet) realice una actividad, verá el nombre de la botnet (si está disponible) con un vínculo a un informe detallado sobre la botnet específica.
 
## <a name="cloud-app-security-release-97"></a>Notas de la versión 97 de Cloud App Security
Publicado el 24 de mayo de 2017

### <a name="new-features"></a>Nuevas características
-   Al investigar archivos e infracciones de directivas, ahora puede ver todas las coincidencias de directivas en la página Archivos. Además, se ha mejorado la página Alertas de archivo para que incluya una pestaña independiente con el historial del archivo específico, lo que le permite explorar en profundidad el historial de infracciones de todas las directivas del archivo específico. Cada evento del historial incluye una instantánea del archivo en el momento de la alerta e indica si el archivo se ha eliminado o se ha puesto en cuarentena.
-   Ya está disponible la [cuarentena de administrador](use-case-admin-quarantine.md) para archivos de Office 365 SharePoint y OneDrive para la Empresa, en versión preliminar privada. Esta característica permite poner en cuarentena los archivos que coincidan con las directivas o establecer una acción automatizada para ponerlos en cuarentena, con lo que se eliminan del directorio de SharePoint del usuario y se realiza una copia del archivo original en la ubicación de cuarentena del administrador de su elección.
        
### <a name="cloud-discovery-improvements"></a>Mejoras de Cloud Discovery

-   Se ha mejorado la compatibilidad de Cloud Discovery con los registros de Cisco Meraki.
-   La opción para proponer una mejora de Cloud Discovery permite sugerir un nuevo factor de riesgo.
-   Se ha mejorado el analizador de registros personalizado para que admita formatos de registro mediante la separación de la configuración de fecha y hora y para ofrecer la opción de establecer una marca de tiempo.
-   Se ha empezado a implementar la capacidad de crear informes de detección personalizados en función de los grupos de usuarios de Azure Active Directory. Por ejemplo, si quiere ver el uso de la nube por parte del departamento de marketing, puede importar el grupo de marketing mediante la característica para importar grupos de usuarios y, después, crear un informe personalizado para este grupo.

**Otras actualizaciones**

-   Cloud App Security ahora incluye compatibilidad con las actividades de Microsoft Power BI que se admiten en el registro de auditoría de Office 365. Esta característica se está implantando gradualmente. Tenga en cuenta que debe habilitar [esta funcionalidad en el portal de Power BI](https://powerbi.microsoft.com/documentation/powerbi-admin-auditing/).
-   En las directivas de actividad, ahora puede establecer que se realicen acciones para enviar notificaciones y suspender al usuario en todas las aplicaciones conectadas. Por ejemplo, puede establecer una directiva para notificar siempre al administrador del usuario y suspender al usuario de inmediato si este tiene varios inicios de sesión erróneos en una aplicación conectada.
 
## <a name="oob-release"></a>Lanzamiento de OOM
-   En respuesta a los ataques de ransomware que se están constatando en todo el mundo, el equipo de Cloud App Security agregó el domingo en el portal una nueva plantilla de [directiva de detección de posible actividad de ransomware](use-case-ransomware.md) que incluye la extensión de firma de WannaCrypt. Le recomendamos que establezca esta directiva hoy mismo.

## <a name="cloud-app-security-release-96"></a>Notas de la versión 96 de Cloud App Security
Fecha de publicación: 8 de mayo de 2017

Nuevas características:

-   Continuación de la implementación gradual del permiso de Lector de seguridad que le permite administrar los permisos que concede a los administradores dentro de la consola de Cloud App Security. De forma predeterminada, todos los administradores globales y administradores de seguridad de Azure Active Directory y Office 365 tendrán permisos completos en el portal, y todos los lectores de seguridad de Azure Active Directory y Office 365 tendrán acceso de solo lectura en Cloud App Security. Para obtener más información, consulte [Managing admin access](manage-admins.md) (Administración de permisos de administración).
-   Implementación completada de Cloud Discovery para analizadores de registros definidos por el usuario para registros basados en CSV. Cloud App Security le permite configurar un analizador para los dispositivos que antes no eran compatibles, proporcionándole las herramientas para delinear las columnas que se correlacionan con datos específicos. Para obtener más información, consulte [Uso del analizador de registros personalizado](custom-log-parser.md).

Mejoras:

-   Cloud Discovery ahora admite dispositivos Juniper SSG.
-   Se ha mejorado la compatibilidad de Cloud Discovery para los registros de Cisco ASA para una mejor visibilidad.
-   Ahora puede ejecutar más fácilmente acciones masivas y seleccionar varios registros en las tablas del portal de Cloud App Security: la longitud de la página se ha aumentado para mejorar las operaciones masivas.
-   Los informes integrados **Uso compartido externo por dominio** y **Propietarios de archivos compartidos** ahora se pueden ejecutar para datos de Salesforce.
-   Estamos comenzando el lanzamiento de actividades de Salesforce adicionales que le permiten realizar un seguimiento de la información interesante extraída de los datos de actividad. Estas actividades incluyen ver y editar cuentas, clientes potenciales, oportunidades y otros objetos de Salesforce interesantes.
-   Se han agregado nuevas actividades de Exchange para permitirle supervisar los permisos que se concedieron para buzones o carpetas de buzones. Estas actividades incluyen:
    -   Agregar permisos de destinatario
    -   Quitar permisos de destinatario
    -   Agregar permisos de carpeta de buzón
    -   Quitar permisos de carpeta de buzón
    -   Establecer permisos de carpeta de buzón

    Por ejemplo, ahora puede comprobar a qué usuarios se concedió el permiso **SendAs** sobre los buzones de otros usuarios y, como consecuencia, ahora pueden enviar mensajes de correo electrónico en su nombre.


## <a name="cloud-app-security-release-95"></a>Notas de la versión 95 de Cloud App Security
Publicado el 24 de abril de 2017

**Actualizaciones**
- La página **Cuentas** se ha actualizado con mejoras que facilitan la detección de riesgos. Ahora se pueden filtrar más fácilmente las cuentas internas y externas, ver de un vistazo si un usuario tiene permisos de administrador y realizar acciones en cada cuenta individualmente por cada aplicación (como quitar permisos, quitar colaboraciones de usuario o suspender a un usuario). Además, se muestran los [grupos de usuarios](user-groups.md) importados de cada cuenta. 

- En el caso de las cuentas Microsoft profesionales (Office 365 y Azure Active Directory), Cloud App Security agrupa distintos identificadores de usuario como direcciones proxy, alias, SID, etc. en una sola cuenta. Todos los alias relacionados con una cuenta aparecen en la dirección de correo electrónico principal. Basándose en la lista de identificadores de usuario, en las actividades cuyo actor sea un identificador de usuario, dicho actor se mostrará como UPN (nombre principal de usuario). Se asignarán los grupos y se aplicarán las directivas de acuerdo con el UPN. Esto mejorará la investigación de actividades y fusionará todas las relacionadas con la misma sesión para detectar anomalías y directivas basadas en grupos. Esta característica se implementará de forma gradual durante el próximo mes.

- Se ha agregado la etiqueta Robot como un posible factor de riesgo en el informe integrado de uso del explorador. Ahora, además de etiquetar como obsoleto el uso del explorador, puede ver si ha sido un robot el que ha usado el explorador. Obtenga más información sobre los [informes integrados](built-in-report-reference.md).

- Al crear una directiva de archivo de inspección de contenido, ahora puede establecer el filtro para incluir solo los archivos con un mínimo de 50 coincidencias.



## <a name="cloud-app-security-release-94"></a>Versión 94 de Cloud App Security
Publicada el 2 de abril de 2017

**Nuevas características**
-   Cloud App Security ahora se integra con Azure RMS. Puede proteger archivos en Office 365 OneDrive y Sharepoint Online con Microsoft Rights Management directamente desde el portal de Cloud App Security. Esto puede realizarse desde la página **Archivos**. Para más información, consulte [Integración de Azure Information Protection](azip-integration.md). En versiones futuras se proporcionará compatibilidad con aplicaciones adicionales.
-   Hasta ahora, cuando las actividades de robot y rastreador (crawler) tienen lugar en la red, era especialmente difícil de identificar porque dichas actividades no las realizaba un usuario de la red. Sin su conocimiento, los robots y rastreadores pueden ejecutar herramientas malintencionados en los equipos. Ahora, Cloud App Security proporciona las herramientas para ver cuándo los robots y los rastreadores están realizando actividades en la red. Puede usar la nueva etiqueta de agente de usuario para filtrar actividades en el registro de actividades. La etiqueta de agente de usuario le permite filtrar todas las actividades que realizan por robots y usarlo para crear una directiva que le avise cada vez que se detecte este tipo de actividad. El usuario se actualizará cuando las versiones futuras incluyan esta actividad de riesgo como insertada en las alertas de detección de anomalías. 
-   La nueva página de permisos de aplicación unificada permite investigar más fácilmente los permisos que se han concedido a los usuarios a aplicaciones de terceros. Haciendo clic en **Investigar** > **Permisos de aplicación**, ahora puede ver una lista de todos los permisos que se les concedió a los usuarios a aplicaciones de terceros con una página de permisos de aplicación por aplicación conectada que le permite comparar mejor entre las distintas aplicaciones y los permisos concedidos.  Para más información, vea [Administrar permisos de aplicación](manage-app-permissions.md).
-   Puede filtrar los datos desde el cajón de tablas para una investigación más sencilla.
En el **Registro de actividades**, la tabla **Archivos** y las páginas **Permisos de aplicación** ahora se han mejorado con nuevas acciones contextuales, lo que facilita bastante los giros en el proceso de investigación. También agregamos vínculos rápidos a páginas de configuración y la capacidad de copiar los datos con un solo clic. Para más información, consulte la información sobre el [trabajo con los cajones de archivos y actividades](file-filters.md).
-   Se ha completado el soporte para Microsoft Teams para la implementación de registros y alertas de actividad de Office 365.
 



## <a name="cloud-app-security-release-93"></a>Notas de la versión 93 de Cloud App Security
Fecha de publicación: 20 de marzo de 2017

**Nuevas características**
-   Ahora puede aplicar directivas para incluir o excluir grupos de usuarios importados. 
-   Anonimización de datos de Cloud Discovery ahora le permite configurar una clave de cifrado personalizada. Para más información, vea [Cloud Discovery Anonymization](cloud-discovery-anonymizer.md) (Anonimización de Cloud Discovery).
-   Para tener más control sobre la administración de cuentas y de usuario, ahora tiene acceso directo a la configuración de la cuenta de Azure AD para cada usuario y cuenta desde dentro de la página **Cuenta** haciendo clic en el engranaje junto a cada usuario. Esto permite facilitar el acceso a la administración del grupo de características de administración de usuario avanzado, la configuración de MFA, los detalles acerca de los inicios de sesión de usuario y la capacidad de bloquear el inicio de sesión. 
-   Ahora puede exportar un script de bloqueo para las aplicaciones sin aprobación a través de la API de Cloud App Security. Obtenga más información acerca de las API en el portal de Cloud App Security haciendo clic en el signo de interrogación en la barra de menús, seguido por **Documentación de la API**.
-   El conector de la aplicación de Cloud App Security para ServiceNow se ha expandido para incluir compatibilidad con tokens de OAuth (tal como se presenta en Ginebra, Helsinki y Estambul). Esto proporciona una conexión más sólida de la API con ServiceNow, que no se basa en el usuario de implementación. Para más información, vea [Conectar ServiceNow con Microsoft Cloud App Security](connect-servicenow-to-microsoft-cloud-app-security.md). Los clientes existentes pueden actualizar su configuración en la página del conector de ServiceNow App.
-   Si configura escáneres DLP adicionales de terceros, el estado del examen DLP ahora mostrará el estado de cada conector de forma independiente para mejorar la visibilidad.
-   Cloud App Security ahora incluye compatibilidad para las actividades de Microsoft Teams que se admiten en el registro de auditoría de Office 365. Esta característica se está implantando gradualmente.
-   Para los eventos de suplantación Exchange Online, ahora puede filtrar por nivel de permiso: usado-delegado, administrador o administrador delegado. Puede buscar eventos que muestran el nivel de suplantación que le interese en el  **registro de actividad** buscando **Elemento de** > **objetos de actividad**.
-   En el cajón de aplicaciones de la pestaña **Permisos de la aplicación** de aplicaciones Office 365, ahora puede ver el **publicador** de cada aplicación. También puede utilizar el publicador como un filtro para la investigación de las aplicaciones adicionales del mismo publicador.
-   Las direcciones IP de riesgo aparecen ahora como un factor de riesgo independiente en lugar de ponderado en el factor de riesgo de la **ubicación** general. 
-   Cuando las etiquetas de Azure Information Protection están deshabilitadas en un archivo, las etiquetas deshabilitadas aparecerán como deshabilitadas en Cloud App Security. No se mostrarán las etiquetas eliminadas.
 
**Compatibilidad adicional de Salesforce:**
-   Ahora puede suspender y quitar la suspensión de los usuarios de Salesforce en Cloud App Security. Esto puede realizarse en la ficha **Cuentas** del conector de Salesforce haciendo clic en el engranaje al final de la fila de un usuario específico y seleccionando **Suspender** o **Anular suspensión**, y también se puede aplicar como una acción de control como parte de una directiva. Todas las actividades de suspensión y de anulación de la suspensión realizadas en Cloud App Security se almacenarán en el [registro de control](governance-actions.md). 
-   Visibilidad mejorada para el uso compartido de contenido de Salesforce: ahora puede ver qué archivos se comparten con quién, incluidos los archivos compartidos públicamente, compartidos con grupos de archivos y compartidos con todo el dominio de Salesforce. La visibilidad mejorada se extenderá retroactivamente a aplicaciones de Salesforce conectadas nuevas y actuales. Puede que tarde en actualizarse la primera vez.
-   Mejoramos la cobertura de los siguientes eventos de Salesforce y los separamos de la actividad **Administrar usuarios**: 
    - Editar permisos
    - Crear usuario
    - Cambiar rol
    - Restablecer contraseña

## <a name="cloud-app-security-release-90-91-92"></a>Notas de la versión 90, 91 y 92 de Cloud App Security
Publicado en febrero de 2017

**Anuncio especial**

Cloud App Security ahora está certificada oficialmente con Microsoft Compliance para ISO, HIPAA, CSA STAR y cláusulas de modelo EU, entre otros. Para ver la lista completa de certificaciones, vaya a [Ofertas de Microsoft Compliance](https://www.microsoft.com/trustcenter/compliance/complianceofferings) y seleccione Cloud App Security.

**Nuevas características**

-  **Importar grupos de usuarios (versión preliminar)**   Al conectar aplicaciones mediante conectores de API, Cloud App Security ahora permite importar grupos de usuarios de Office 365 y Azure Active Directory. Puede aprovechar la existencia de grupos de usuarios importados para investigar qué documentos consulta el departamento de Recursos Humanos, para comprobar si sucede algo inusual en el grupo ejecutivo o para verificar si un miembro del grupo de administración ha llevado a cabo alguna actividad fuera del país. Para obtener más información e instrucciones, vea [Importar grupos de usuarios](user-groups.md).

-  En el registro de actividad, ahora puede filtrar los usuarios y los usuarios de grupos para mostrar las actividades realizadas por y en un usuario específico. Por ejemplo, puede investigar las actividades en las que el usuario ha suplantado a otras personas, así como las actividades en las que otras personas han suplantado a este usuario. Para obtener más información, vea [Actividades](activity-filters.md).

- Al investigar un archivo en la página **Archivos**, si explora en profundidad los **Colaboradores** de un archivo específico, ahora puede consultar más información sobre los colaboradores, incluido si son internos o externos, autores o lectores (permisos de archivo) y, cuando se comparte un archivo con un grupo, ahora puede ver todos los usuarios que son miembros del grupo. Esto le permite ver si los miembros del grupo son usuarios externos.

-  Ahora hay compatibilidad con IPv6 disponible para todos los dispositivos.

-   Cloud Discovery ahora admite dispositivos Barracuda.

-   Las alertas del sistema de Cloud App Security ahora incluyen errores de conectividad SIEM. Para obtener más información, vea [Integración de SIEM](siem.md).

-   Cloud App Security ahora es compatible con las actividades siguientes:

     **Office 365, SharePoint/OneDrive**: actualizar la configuración de aplicaciones, quitar el propietario del grupo, eliminar sitio, crear carpeta.

     **Dropbox**: agregar un miembro a un grupo, quitar un miembro de un grupo, crear grupo, cambiar el nombre de grupo, cambiar el nombre de un miembro de un equipo.

     **Box**: quitar un elemento de un grupo, actualizar un recurso compartido de elemento, agregar un usuario a un grupo, eliminar un usuario de un grupo.


## <a name="cloud-app-security-release-89"></a>Notas de la versión 89 de Cloud App Security
Publicado el 22 de enero de 2017

**Nuevas características**
-   Estamos empezando a implementar la capacidad de ver los eventos de DLP del Centro de seguridad y cumplimiento de Office 365 en Cloud App Security. Si configuró directivas DLP en el Centro de seguridad y cumplimiento de Office 365, cuando se detecten coincidencias de directiva, podrá verlas en el registro de actividades de Cloud App Security. La información del registro de actividades incluirá el archivo o el correo electrónico que desencadenó la coincidencia y la directiva o la alerta con la que coincide. La actividad **Evento de seguridad** permite ver las coincidencias de la directiva DLP de Office 365 en el registro de actividades de Cloud App Security. Con esta característica, puede hacer lo siguiente:
    -   Vea todas las coincidencias de DLP que proceden del motor DLP de Office 365.
    -   Alertar sobre las coincidencias de la directiva DLP de Office 365 para un archivo específico, un sitio de SharePoint o una directiva.
    -   Investigar las coincidencias de DLP con un contexto más amplio, por ejemplo, los usuarios externos que han obtenido acceso a un archivo o que han descargado un archivo que desencadenó una coincidencia de la directiva DLP.
 
-   Se han mejorado las descripciones de las actividades para una mayor claridad y coherencia. Ahora, cada actividad incluye un botón de comentarios, por lo que si no entiende algo o tiene una pregunta, puede hacérnoslo saber. 
 
**Mejoras**  
-   Se ha agregado una nueva acción de gobierno para Office 365 que permite quitar todos los usuarios externos de un archivo. Por ejemplo, esto permite implementar directivas que **quitan recursos compartidos externos de los archivos que tienen una clasificación solo interna**.
-   Se ha mejorado la identificación de los usuarios externos en SharePoint Online. Cuando se filtra el grupo de "usuarios externos", no se muestra la cuenta del sistema app@sharepoint.



## <a name="cloud-app-security-release-88"></a>Notas de la versión 88 de Cloud App Security
Publicado el 8 de enero de 2017
 
**Nuevas características**
- Conecte su SIEM con Cloud App Security. Ahora puede enviar alertas y actividades automáticamente al SIEM de su elección mediante la configuración de agentes de SIEM. Ahora está disponible como versión preliminar pública.  Para obtener documentación completa y detalles, consulte la información relativa a la integración con SIEM.
- Ahora, Cloud Discovery es compatible con IPv6. Hemos incluido compatibilidad con Palo Alto y Juniper y en versiones futuras se incluirán más dispositivos.
 
**Mejoras**
- Hay un nuevo factor de riesgo en el catálogo de aplicaciones de nube. Ahora puede valorar una aplicación en función de si requiere autenticación de usuario. Las aplicaciones que exijan la autenticación y que no permitan el uso anónimo recibirán una mejor puntuación de riesgo.
- Estamos implementando nuevas descripciones de actividades para que sean más fáciles de usar y coherentes. La búsqueda de actividades no se verá afectada.
- Hemos incluido una identificación mejorada del dispositivo de usuario al permitir que Cloud App Security enriquezca más eventos con información del dispositivo.
 
## <a name="cloud-app-security-release-87"></a>Notas de la versión 87 de Cloud App Security
Fecha de publicación 25 de diciembre de 2016

**Nuevas características**
-   Estamos en proceso de lanzar la [anonimización de los datos](cloud-discovery-anonymizer.md) para que pueda disfrutar de Cloud Discovery a la vez que se protege la privacidad de los usuarios. La anonimización de los datos se realiza mediante el cifrado de la información del nombre de usuario.
-   Estamos en proceso de lanzar la capacidad de exportar un script de bloqueo desde Cloud App Security a dispositivos adicionales. El script le permitirá reducir fácilmente Shadow IT mediante el bloqueo del tráfico a aplicaciones no autorizadas. Esta opción ya está disponible para: 
    -   BlueCoat ProxySG
    -   Cisco ASA
    -   Fortinet
    -   Juniper SRX
    -   Palo Alto
    -   Websense
-   Se ha agregado una nueva acción de control de archivos que le permite forzar a un archivo heredar permisos del elemento principal, eliminando así los permisos únicos que se hayan configurado para el archivo o carpeta. Esta acción de control de archivos le permite cambiar los permisos de la carpeta o el archivo para que se hereden de la carpeta principal. 
-   Se ha agregado un nuevo grupo de usuarios con el nombre Externos. Es un grupo de usuarios predeterminado configurado previamente por Cloud App Security para incluir todos los usuarios que no forman parte de los dominios internos. Puede usar este grupo como filtro; por ejemplo, puede buscar actividades realizadas por los usuarios externos.
-   La característica Cloud Discovery ahora admite dispositivos Sophos Cyberoam.
 
**Correcciones de errores**
-   Los archivos de SharePoint Online y OneDrive para la Empresa se mostraban en el informe de directiva de archivo y en la página de archivos como para uso interno en lugar de privado. Esto se ha corregido.
 


## <a name="cloud-app-security-release-86"></a>Notas de la versión 86 de Cloud App Security
Fecha de publicación: 13 de diciembre de 2016

**Nuevas características**
- Todas las licencias independientes de Cloud App Security proporcionan la capacidad de habilitar el análisis de Azure Information Protection desde la configuración general (sin necesidad de crear una directiva). 
 
**Mejoras**
- Ahora puede usar "o" en el filtro de archivos para el nombre de archivo y en el filtro de tipo MIME para los archivos y directivas. Esto habilita escenarios como escribir la palabra "pasaporte" O "controlador" al crear una directiva con PII y coincidirá con cualquier archivo que contenga "pasaporte" o "controlador" en el nombre de archivo. 
- De forma predeterminada, cuando se ejecuta una directiva DLP de inspección de contenido, los datos de las infracciones resultantes se enmascaran. Ahora puede mostrar los últimos cuatro caracteres de la infracción. 

**Mejoras menores**
- Nuevos eventos relacionados con el buzón de Office 365 (Exchange) que tienen que ver con las reglas de reenvío y con agregar y quitar permisos de buzón delegados.
- Nuevo evento que audita la concesión de consentimiento para nuevas aplicaciones en Azure Active Directory. 




## <a name="cloud-app-security-release-85"></a>Notas de la versión 85 de Cloud App Security
Publicado el 27 de noviembre de 2016

**Nuevas características**
- Se ha creado una distinción entre las aplicaciones conectadas y las aplicaciones autorizadas. La autorización y la desautorización de aplicaciones funcionan ahora como etiquetas, de modo que se pueden aplicar a las aplicaciones detectadas o a cualquier aplicación del catálogo. Las aplicaciones conectadas son aplicaciones que ha conectado con el conector de la API para supervisarlas y controlarlas con mayor profundidad. Ahora puede etiquetar aplicaciones como autorizadas o no autorizadas, así como conectarlas mediante el conector de aplicaciones, en caso de que esté disponible. 
 
- Como parte de este cambio, se ha sustituido la página de aplicaciones autorizadas por la página **Aplicaciones conectadas**, que se ha rediseñado. Esta página externaliza los datos de estado de los conectores. 
 
- Se puede acceder más fácilmente a los recopiladores de registros desde el menú **Configuración**, en **Orígenes**. 
- Al crear un filtro de directiva de actividad, puede reducir el número de falsos positivos seleccionando la opción para ignorar las actividades repetidas cuando un mismo usuario las realiza de forma repetida en el mismo objeto. Este es el caso, por ejemplo, cuando una misma persona intenta descargar el mismo archivo varias veces, de modo que no se generará ninguna alerta. 
- Se han realizado mejoras en el cajón de actividades. Ahora, al hacer clic en un objeto de actividad, puede explorarlo en profundidad para obtener más información.

**Mejoras**
- Se han realizado mejoras en el motor de detección de anomalías, incluidas las alertas de desplazamiento imposible. Ahora, la información sobre la IP para este tipo de alertas está disponible en su descripción.
- También se han realizado mejoras en los filtros complejos, de modo que permitan agregar el mismo filtro más de una vez para ajustar los resultados que se filtran. 
- Se han separado las actividades de archivos y carpetas de Dropbox del resto para que se puedan consultar con mayor facilidad. 
  
**Correcciones de errores**
- Se ha corregido un error en el mecanismo del sistema de alertas que creaba falsos positivos.

## <a name="cloud-app-security-release-84"></a>Notas de la versión 84 de Cloud App Security
Publicado el 13 de noviembre de 2016

**Nuevas características**
-   Cloud App Security ahora admite Microsoft Azure Information Protection, que incluye una integración mejorada y autoaprovisionamiento. Puede filtrar los archivos y establecer directivas de archivo mediante la clasificación segura de etiquetas y, después, establecer la etiqueta de clasificación que quiere ver. Las etiquetas también indican si la clasificación la estableció alguien de su organización o un usuario de otro inquilino (externo). También puede establecer directivas de actividad, en función de las etiquetas de clasificación de Azure Information Protection y habilitar la detección automática de etiquetas de clasificación en Office 365. Para obtener más información acerca de cómo sacar partido a esta nueva característica increíble, consulte [Integración con Azure Information Protection](azip-integration.md).
 
**Mejoras**
-   Se realizaron mejoras en el registro de actividad de Cloud App Security: 
   -    Los eventos de Office 365 del Centro de seguridad y cumplimiento de Office 365 ahora se integran con Cloud App Security y se ven en el **Registro de actividades**.
   -    Toda la actividad de Cloud App Security se registra en el registro de actividades de Cloud App Security como actividad administrativa.
-   Para ayudarle a investigar alertas relacionadas con archivos, en cada alerta derivada de una directiva de archivo, ahora puede ver la lista de actividades que se realizaron en el archivo coincidente.
-   El algoritmo de viaje imposible del motor de detección de anomalías se ha mejorado para proporcionar una mayor compatibilidad para inquilinos pequeños. 
 
**Mejoras menores**
-   El **Activity export limit** (Límite de exportación de actividades) se elevó a 10 000. 
-   Al crear un **Informe de instantáneas** en el proceso de carga del registro manual de Cloud Discovery, ahora recibirá una estimación precisa de cuánto tardará el procesamiento del registro. 
-   En una directiva de archivo, la acción de gobierno **Remove collaborator** (Quitar colaborador) ahora funciona en grupos.
-   Se realizaron mejoras menores en la página **Permisos de la aplicación**. 
-   Si había más de 10 000 usuarios que disponían de permisos para una aplicación que se conectaba a Office 365, la lista se cargaba lentamente. Esto se ha solucionado.
-   Se han agregado atributos adicionales al **Catálogo de aplicaciones** con relación al sector de tarjetas de pago.


## <a name="cloud-app-security-release-83"></a>Notas de la versión 83 de Cloud App Security
Publicado el 30 de octubre de 2016

**Nuevas características**
-   Para simplificar el filtrado en el [registro de actividad](activity-filters.md) y en el [registro de archivo](file-filters.md), se han consolidado filtros similares. Utilice los filtros de actividad: Objeto de actividad, Dirección IP y Usuario. Utilice el filtro de archivos Colaboradores para encontrar exactamente lo que necesita.
-   Desde el cajón del registro de actividades, bajo **Origen**, puede hacer clic en el vínculo de **ver los datos sin procesar** para descargar los datos sin procesar usados para generar el registro de actividades, para explorar en profundidad en los eventos de la aplicación. 
-   Compatibilidad agregada para las actividades de inicio de sesión adicionales en Okta. [Versión preliminar privada]
-   Compatibilidad agregada para las actividades de inicio de sesión adicionales en Salesforce. 

**Mejoras**
-   Facilidad de uso mejorada para informes y solución de problemas de instantáneas de Cloud Discovery.
-   Visibilidad mejorada en la lista de alertas de varias aplicaciones.
-   Facilidad de uso mejorada al crear nuevos informes continuos de Cloud Discovery.
-   Facilidad de uso mejorada en el registro de gobierno.



## <a name="cloud-app-security-release-82"></a>Notas de la versión 82 de Cloud App Security
Publicado el 9 de octubre de 2016

**Mejoras**

- Las actividades **Cambiar correo electrónico** y **Cambiar contraseña** ahora son independientes de la actividad genérica **Administrar usuarios** en Salesforce.
- Se ha agregado una aclaración sobre el límite de alertas diarias por SMS. Se envía un máximo de 10 mensajes por número de teléfono y por día (UTC).
- Se ha agregado un nuevo certificado a los atributos de Cloud Discovery para Privacy Shield que reemplaza Safe Harbor (relevante solo para proveedores de EE. UU.).
- Se ha agregado un proceso de solución de problemas a los mensajes de error del conector de API para que sea más fácil solucionar los problemas.
- Mejora de la frecuencia de actualización del examen de aplicaciones de terceros de Office 365.
- Mejoras en el panel de Cloud Discovery.
- Se ha mejorado el analizador de Syslog de punto de control.
- Mejoras en el registro de gobierno para prohibir aplicaciones de terceros y para eliminar la prohibición.
 
**Correcciones de errores**
 
- Mejora del proceso para cargar un logotipo.
 
## <a name="cloud-app-security-release-81"></a>Notas de la versión 81 de Cloud App Security
Publicado el 18 de septiembre de 2016

**Mejoras**
- Cloud App Security ya es una aplicación de origen en Office 365. De ahora en adelante, puede conectar Office 365 con Cloud App Security con un solo clic.

- Nuevo aspecto del registro de gobierno: se ha actualizado para que tenga el mismo aspecto útil que el registro de actividad y la tabla de archivos. Use los nuevos filtros para encontrar fácilmente lo que necesita y supervisar las acciones de gobierno. 
- Se han realizado mejoras en el motor de detección de anomalías en lo que respecta a varios inicios de sesión erróneos y otros factores de riesgo.
- Se han realizado mejoras en los informes de instantáneas de Cloud Discovery.
- Se han realizado mejoras en las actividades administrativas del registro de actividades. Ahora, en Cambiar contraseña, Actualizar usuario y Restablecer contraseña se muestra si la actividad se realizó como una actividad administrativa.
- Se han mejorado los filtros de alerta para las alertas del sistema. 
- Ahora, la etiqueta de la directiva de una alerta contiene un vínculo al informe de directiva.
- Si no hay ningún propietario especificado para un archivo de Dropbox, los mensajes de correo electrónico de notificación se envían al destinatario que establezca. 
- Cloud App Security admite 24 idiomas más, con lo que la compatibilidad se amplía a un total de 41 idiomas.  


## <a name="cloud-app-security-release-80"></a>Notas de la versión 80 de Cloud App Security
Publicado el 4 de septiembre de 2016 

**Mejoras**
- Cuando se produce un error en el examen de DLP, ahora se proporciona una explicación de por qué Cloud App Security no pudo examinar el archivo. Para obtener más información, consulte [Content Inspection](https://aka.ms/aka.ms/cas-contentinspection) (Inspección de contenido).
- Se han realizado mejoras en los motores de detección de anomalías, incluido en las alertas de viaje imposible.
- Se han realizado mejoras en la experiencia para descartar alertas. También se pueden agregar comentarios para que el equipo de Cloud App Security sepa si la alerta era interesante y por qué razón, de modo que la información se pueda usar para mejorar las detecciones de Cloud App Security.
- Se han mejorado los analizadores de Cloud Discovery de Cisco ASA.
- Ahora recibirá una notificación por correo electrónico cuando se complete la carga manual de registros de Cloud Discovery.
   



## <a name="cloud-app-security-release-79"></a>Notas de la versión 79 de Cloud App Security
Publicado el 21 de agosto de 2016 

**Nuevas características**

- **Nuevo panel de Cloud Discovery**  
Ahora hay disponible un nuevo panel de Cloud Discovery, diseñado para proporcionar más información sobre cómo se usan las aplicaciones de nube en la organización. Proporciona una visión general a simple vista sobre los tipos de aplicaciones que se usan, las alertas abiertas y los niveles de riesgo de las aplicaciones de la organización. También permite saber quiénes son los usuarios de la organización que más usan las aplicaciones y proporciona un mapa de ubicación de la sede central de la aplicación.
El nuevo panel tiene más opciones para filtrar los datos, de modo que pueda generar vistas específicas en función de lo que más le interese y gráficos fáciles de entender para que se haga una idea general de un vistazo.

- **Nuevos informes de Cloud Discovery** Para ver los resultados de Cloud Discovery, ahora puede generar dos tipos de informes: informes de instantáneas e informes continuos.
Los informes de instantáneas proporcionan visibilidad ad hoc de un conjunto de registros de tráfico que puede cargar manualmente desde los firewalls y los servidores proxy. Los informes continuos muestran los resultados de todos los registros que se reenvían desde la red mediante los recopiladores de registros de Cloud App Security. Estos nuevos informes proporcionan una mejor visibilidad de todos los datos, la identificación automática de un uso anómalo según lo defina el motor de detección de anomalías de aprendizaje automático de Cloud App Security y la identificación de un uso anómalo según lo defina usted mediante el motor de directivas pormenorizadas y sólidas. Para obtener más información, consulte [Set up Cloud Discovery](set-up-cloud-discovery.md) (Configurar Cloud Discovery).
 
**Mejoras**
- Mejoras generales en la facilidad de uso de las páginas siguientes: páginas de directivas, configuración general y configuración de correo electrónico.
- En la tabla de alertas, es más fácil distinguir las alertas leídas de las no leídas. Las alertas leídas tienen una línea azul a la izquierda y aparecen atenuadas para indicar que ya se han leído.
- Se han actualizado los parámetros de **Actividad repetida** de la directiva de actividad. 
- En la página de cuentas, se ha agregado la columna **Tipo** de usuario, por lo que ahora puede ver qué tipo de cuenta de usuario tiene cada usuario. Los tipos de usuario son específicos de la aplicación. 
- Se ha agregado soporte prácticamente en tiempo real para las actividades relacionadas con archivos en OneDrive y SharePoint. Cuando un archivo cambia, Cloud App Security desencadena un examen casi de inmediato.


## <a name="cloud-app-security-release-78"></a>Notas de la versión 78 de Cloud App Security
Publicado el 7 de agosto de 2016

**Mejoras**
- Ahora puede hacer clic con el botón derecho en un archivo específico y **Buscar relacionados**. En el registro de actividades, puede usar el filtro del objeto de destino y seleccionar el archivo específico.

- Se han mejorado los analizadores de archivos de registro de Cloud Discovery, incluida la adición de Juniper y Cisco ASA.
- Cloud App Security ahora permite proporcionar comentarios para la mejora de las alertas cuando se descarta una alerta. Puede ayudar a mejorar la calidad de la característica de alertas de Cloud App Security. Para ello, infórmenos del motivo por el que descarta la alerta, por ejemplo: no es interesante, ha recibido demasiadas alertas similares, la gravedad real debe ser inferior o la alerta no es precisa.
-En la vista de la directiva de archivo o al ver un archivo, cuando se abre el cajón de archivos, se ha agregado un vínculo nuevo a las directivas coincidentes. Al hacer clic en él, puede ver todas las coincidencias y ahora puede descartarlas todas. 
- Ahora se ha agregado en todas las alertas correspondientes la unidad organizativa a la que pertenece un usuario.
- Ahora se envía una notificación por correo electrónico para informarle de que se ha completado el procesamiento de los registros cargados manualmente.


## <a name="cloud-app-security-release-77"></a>Notas de la versión 77 de Cloud App Security
Publicado el 24 de julio de 2016

**Mejoras**
- El icono del botón Exportar de Cloud Discovery se ha mejorado para una mayor facilidad de uso.
- Al investigar una actividad, si no se ha analizado el agente de usuario, ahora se pueden ver los datos sin procesar.
- Se han agregado dos nuevos factores de riesgo al motor de detección de anomalías: 
    - Cloud App Security ahora usa las etiquetas de direcciones IP que están asociadas a una red de robots (botnet) y direcciones IP anónimas como parte del cálculo de riesgo. 
    - La actividad de Office 365 ahora se supervisa para detectar frecuencias de descarga alta. Si la frecuencia de descarga de Office 365 es mucho mayor que la frecuencia de descarga normal de la organización o de un usuario específico, se desencadenará una alerta de detección de anomalías. 
- Ahora Cloud App Security es compatible con la nueva API de [función de uso compartido seguro](https://blogs.dropbox.com/dropbox/2016/06/new-dropbox-productivity-tools/) de Dropbox. 
- Se han realizado mejoras para agregar detalles en los errores de análisis de registro de Discovery, por ejemplo, para indicar que no hay transacciones relacionadas con la nube, todos los eventos están obsoletos, el archivo está dañado o el formato del registro no coincide.
- Se ha mejorado el filtro de fecha del registro de actividad y ahora incluye la capacidad de filtrar por hora.
- La página de intervalos de direcciones IP se ha mejorado para una mayor facilidad de uso.
- Ahora Cloud App Security incluye compatibilidad con Microsoft Azure Information Protection (versión preliminar). Puede filtrar los archivos y establecer directivas de archivo mediante la clasificación segura de etiquetas y, después, establecer el nivel de la etiqueta de clasificación que quiere ver. Las etiquetas también indicarán si la clasificación la estableció alguien de su organización o un usuario de otro inquilino (externo). 



## <a name="cloud-app-security-release-76"></a>Notas de la versión 76 de Cloud App Security
Publicado el 10 de julio de 2016

**Mejoras**

- Ahora se pueden exportar listas con los usuarios de los informes integrados.
- Se ha mejorado la facilidad de uso de la directiva de actividad agregada.
- Se ha mejorado la compatibilidad con el analizador de mensajes de registro de firewall de W3C de TMG.
- Se ha mejorado la facilidad de uso del menú desplegable de la acción de gobierno de archivos, que ahora se divide en acciones de colaboración, seguridad e investigación.
- Se ha mejorado la detección de viaje imposible de la actividad Enviar correo de Exchange Online.
- Se ha agregado una nueva lista de títulos (rutas de navegación) en la parte superior de las páginas de alertas y de directiva para facilitar la navegación.

**Correcciones de errores**
- La expresión preestablecida para la tarjeta de crédito de la configuración de DLP para las directivas de archivo se ha cambiado a Todos: Finanzas: Número de tarjeta de crédito.


## <a name="cloud-app-security-release-75"></a>Notas de la versión 75 de Cloud App Security
Publicado el 27 de junio de 2016


**Nuevas características**
* Se han agregado nuevos elementos a nuestra lista creciente de eventos compatibles con Salesforce, incluidos eventos que proporcionan información sobre informes, vínculos compartidos, distribución de contenido, inicio de sesión suplantado y mucho más.
* Los iconos de las aplicaciones conectadas del panel de Cloud App Security se han alineado con el estado de las aplicaciones tal como se muestra en el panel para reflejar los últimos 30 días.
* Compatibilidad con pantallas de ancho completo.


**Correcciones de errores**
* Los números de teléfono de alerta por SMS ahora se validan tras la inserción.

## <a name="cloud-app-security-release-74"></a>Notas de la versión 74 de Cloud App Security
Fecha de publicación: 13 de junio de 2016
* Se ha actualizado la pantalla Alerta para proporcionar más información de un vistazo, lo que incluye la posibilidad de ver todas las actividades del usuario con una sola mirada, un mapa de actividades, registros de gobierno de usuarios relacionados, una descripción del motivo por el que se ha desencadenado la alerta y gráficos adicionales y mapas de la página del usuario. 
* Los eventos generados por Cloud App Security ahora incluyen el tipo de evento, el formato, grupos de directivas, objetos relacionados y una descripción.
* Se han agregado nuevas etiquetas de direcciones IP para Office 365 ProPlus, OneNote, Office Online y Exchange Online Protection.
* Ahora tiene la opción de cargar registros desde el menú de detección principal.
* Se ha mejorado el filtro de categoría de direcciones IP. La categoría de dirección IP Nula ahora se denomina Sin categoría y se ha agregado una nueva categoría denominada Sin valor para incluir todas las actividades que no tienen datos de dirección IP.
* Los grupos de seguridad de Cloud App Security ahora se denominan grupos de usuarios para evitar la confusión con los grupos de seguridad de Active Directory.
* Ahora es posible filtrar por dirección IP y dejar fuera los eventos sin una dirección IP. 
* Se han realizado cambios en la configuración de los correos electrónicos de notificación cuando se detectan coincidencias en las directivas de actividad y de archivo. Ahora se pueden agregar direcciones de correo electrónico de destinatarios a CC con la notificación.


## <a name="cloud-app-security-release-73"></a>Notas de la versión 73 de Cloud App Security
Fecha de publicación: 29 de mayo de 2016

* Funciones de alerta actualizadas: ahora las alertas por directiva se pueden configurar para enviarse por correo o como mensaje de texto.
* Página de alertas: diseño mejorado para habilitar opciones de resolución avanzadas y la administración de incidentes.
* Ajuste de directiva: ahora es posible desplazarse desde las opciones de resolución de alertas directamente a la página de configuración de directiva y, así, permitir un mejor ajuste basado en alertas.
* Mejoras en el cálculo de la puntuación de riesgo de detección de anomalías y un menor índice de falsos positivos gracias a los comentarios de los clientes.
* Ahora la exportación del registro de actividades incluye el identificador de evento, la categoría de evento y el nombre del tipo de evento.
* Mejor apariencia y facilidad de uso de las acciones de gobierno de creación de directivas.
* Investigación y control simplificados para Office 365: con la selección de Office 365 se seleccionan automáticamente todas las aplicaciones que forman parte del conjunto de aplicaciones de Office 365.
* Ahora las notificaciones se envían a la dirección de correo configurada en la aplicación conectada. 
* Tras un error de conexión, ahora la aplicación de nube proporciona una descripción detallada de ese error.
* Cuando un archivo coincide con una directiva, ahora el cajón de archivos proporciona una dirección URL para tener acceso a ese archivo.
* Cuando se desencadena una alerta a raíz de una directiva de actividad o de una directiva de detección de anomalías, se envía una nueva notificación detallada que proporciona información sobre la coincidencia. 
* Cuando un conector de aplicaciones se desconecta, se desencadena una alerta del sistema automatizada.
* Ahora puede descartar y resolver una sola alerta o una selección masiva de alertas desde la página de alertas.

## <a name="cloud-app-security-release-72"></a>Notas de la versión 72 de Cloud App Security
Fecha de publicación: 15 de mayo de 2016

*  Mejoras generales en la infraestructura y apariencia:
    * Nuevo diagrama que proporciona más ayuda en el proceso de carga de registro manual de Cloud Discovery.
    * Proceso mejorado de actualización de archivos de registro no reconocidos (“Otros”), incluido un mensaje emergente que le avisa de que el archivo requiere revisión adicional y se le notificará cuando los datos estén disponibles.
    * Se destacan más infracciones de actividad y de archivo al investigar un registro de actividad y de archivo en busca de sistemas operativos y exploradores obsoletos.
* Mejores analizadores de archivos de registro de Cloud Discovery, incluida la adición de Cisco ASA, Cisco FWSM, Cisco Meraki y W3C.
* Mejoras en los problemas conocidos de Cloud Discovery.
* Nuevos filtros de actividad agregados para la afiliación interna/externa y de dominio del propietario.
* Se agregó un nuevo filtro que permite buscar cualquier objeto de Office 365 (archivos, carpetas, direcciones URL).
* Se agregó la capacidad de configurar una puntuación de riesgo mínima para las directivas de detección de anomalías.
* Al configurar una alerta para que se envíe cuando se infrinja una directiva, ahora se puede establecer un nivel de gravedad mínimo a partir del cual se recibirán las alertas. Puede elegir usar la configuración predeterminada de la organización para esto o establecer una configuración de alerta específica como valor predeterminado de la organización.

## <a name="see-also"></a>Consulte también  
[Para obtener soporte técnico, visite la página de soporte técnico asistido de Cloud App Security.](http://support.microsoft.com/oas/default.aspx?prid=16031)   
[Los clientes Premier también pueden elegir Cloud App Security directamente desde el Portal Premier.](https://premier.microsoft.com/)  
  
  
