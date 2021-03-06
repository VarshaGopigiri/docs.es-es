---
title: "C&#243;mo: Depurar servicios y aplicaciones con reconocimiento de notificaciones usando traza WIF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3d51ba59-3adb-4ca4-bd33-5027531af687
caps.latest.revision: 7
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 7
---
# C&#243;mo: Depurar servicios y aplicaciones con reconocimiento de notificaciones usando traza WIF
## Se aplica a  
  
-   Microsoft® Windows® Identity Foundation \(WIF\)  
  
-   Herramienta del visor de seguimiento de servicio \(SvcTraceViewer.exe\)  
  
-   Solución de problemas y depuración de aplicaciones de WIF  
  
## Resumen  
 En este procedimiento se describen los pasos necesarios para configurar el seguimiento de WIF, recopilar registros de seguimiento y analizar los registros de seguimiento con la herramienta Visor de seguimiento.  Proporciona una correspondencia entre las entradas de seguimiento y las acciones necesarias para solucionar los problemas relacionados con WIF.  
  
## Contenido  
  
-   Objetivos  
  
-   Resumen de pasos  
  
-   Paso 1: configurar el seguimiento de WIF mediante el archivo de configuración de Web.config  
  
-   Paso 2: analizar los archivos de seguimiento de WIF mediante la herramienta Visor de seguimiento  
  
-   Paso 3: identificar soluciones para corregir los problemas relacionados con WIF  
  
-   Elementos relacionados  
  
## Objetivos  
  
-   Configurar el seguimiento de WIF.  
  
-   Ver los registros de seguimiento en la herramienta Visor de seguimiento.  
  
-   Identificar los problemas relacionados con WIF en los registros de seguimiento.  
  
-   Aplicar acciones correctivas a los problemas relacionados con WIF encontrados en los registros de seguimiento.  
  
## Resumen de pasos  
  
-   Paso 1: configurar el seguimiento de WIF mediante el archivo de configuración Web.config  
  
-   Paso 2: analizar los archivos de seguimiento de WIF mediante la herramienta Visor de seguimiento  
  
-   Paso 3: identificar soluciones para corregir los problemas relacionados con WIF  
  
## Paso 1: configurar el seguimiento de WIF mediante el archivo de configuración Web.config  
 En este paso, realizará cambios en las secciones de configuración del archivo *Web.config* que permite a WIF realizar un seguimiento de sus eventos y almacenarlos en un registro de seguimiento.  
  
#### Para configurar el seguimiento de WIF mediante el archivo de configuración Web.config  
  
1.  Abra el archivo de configuración raíz **Web.config** o **App.config** en el editor de Visual Studio haciendo doble clic en él en el **Explorador de soluciones**.  Si su solución no tiene un archivo de configuración **Web.config** o **App.config**, agréguelo; para ello, haga clic en la solución en el **Explorador de soluciones**, haga clic en **Agregar** y, después, haga clic en **Nuevo elemento...** En el cuadro de diálogo **Nuevo elemento**, seleccione **Archivo de configuración de la aplicación** para **App.config** o **Archivo de configuración web** para **Web.config** en la lista y haga clic en **Aceptar**.  
  
2.  Agregue las entradas de configuración similares a las siguientes al archivo de configuración, en el nodo **\<configuration\>** al final del archivo de configuración:  
  
    ```xml  
    <system.diagnostics>  
        <sources>  
            <source name="System.IdentityModel" switchValue="Verbose">  
                <listeners>  
                    <add name="xml" type="System.Diagnostics.XmlWriterTraceListener" initializeData="WIFTrace.e2e"/>  
                </listeners>  
            </source>  
        </sources>  
        <trace autoflush="true"/>  
    </system.diagnostics>  
    ```  
  
3.  La configuración anterior indica a WIF que genere eventos de seguimiento detallados y los registre en el archivo *WIFTrace.e2e*.  Para obtener una lista completa de los valores del modificador **switchValue**, consulte la tabla Nivel de seguimiento que se encuentra en el siguiente tema: [Configurar el seguimiento](http://msdn.microsoft.com/library/ms733025.aspx).  
  
## Paso 2: analizar los archivos de seguimiento de WIF mediante la herramienta Visor de seguimiento  
 En este paso, usará la herramienta Visor de seguimiento \(SvcTraceViewer.exe\) para analizar los registros de seguimiento de WIF.  
  
#### Para analizar los registros de seguimiento de WIF con la herramienta Visor de seguimiento \(SvcTraceViewer.exe\)  
  
1.  La herramienta Visor de seguimiento \(SvcTraceViewer.exe\) se incluye como parte de Windows SDK.  Si no ha instalado Windows SDK, puede descargarlo aquí: [Windows SDK](http://www.microsoft.com/download/en/details.aspx?id=8279).  
  
2.  Ejecute la herramienta Visor de seguimiento \(SvcTraceViewer.exe\)  Normalmente está disponible en la carpeta **Bin** de la ruta de instalación.  
  
3.  Para abrir el archivo de registro de seguimiento de WIF, por ejemplo, WIFTrace.e2e, seleccione la opción **Archivo**, **Abrir...** en el menú o use el acceso directo **CTRL\+O**.  Se abre el archivo de registro de seguimiento en la herramienta Visor de seguimiento.  
  
4.  Consulte las entradas de la pestaña **Actividad**.  Cada entrada debe contener un número de actividad, el número de seguimientos que se registraron, la duración de la actividad y sus marcas de tiempo de inicio y finalización.  
  
5.  Haga clic en la pestaña **Actividad**.  Verá las entradas de seguimiento detalladas en el área principal de la herramienta.  Use la lista desplegable **Nivel** del menú para filtrar por nivel específico de seguimiento, por ejemplo: **Todo**, **Advertencia**, **Errores**, **Información**, etc.  
  
6.  Haga clic en entradas de seguimiento específicas para revisar los detalles en el área inferior de la herramienta.  Elija las pestañas **Formato** o **XML** para ver los detalles en la vista correspondiente.  
  
## Paso 3: identificar soluciones para corregir los problemas relacionados con WIF  
 En este paso, puede encontrar soluciones a problemas relacionados con WIF identificados con la herramienta Visor de seguimiento y el registro de seguimiento de WIF.  Realiza una correspondencia general entre las excepciones de WIF y sus posibles soluciones o las acciones necesarias para solucionar el problema.  
  
#### Para identificar soluciones para corregir los problemas relacionados con WIF  
  
1.  Revise la siguiente tabla de excepciones de WIF y las acciones necesarias para corregir los problemas.  
  
||||  
|-|-|-|  
|**Identificador del error:**|**Mensaje de error**|**Acción necesaria para corregir el error**|  
|ID4175|IssuerNameRegistry no reconoció el emisor del token de seguridad.  Para aceptar los tokens de seguridad de este emisor, configure IssuerNameRegistry para devolver un nombre válido para este emisor.|Este error se puede producir cuando se copia una huella digital desde el complemento MMC y se pega en el archivo *Web.config*.  En concreto, puede obtener un carácter adicional no imprimible en la cadena de texto cuando se copia desde la ventana de propiedades del certificado.  Este carácter adicional produce un error de coincidencia de la huella digital. Aquí encontrará el procedimiento para copiar correctamente la huella digital: [http:\/\/msdn.microsoft.com\/library\/ff359102.aspx](http://msdn.microsoft.com/library/ff359102.aspx)|  
  
## Elementos relacionados  
  
-   [Uso del visor de seguimiento de servicios para ver seguimientos asociados y para la solución de problemas](http://msdn.microsoft.com/library/aa751795.aspx)