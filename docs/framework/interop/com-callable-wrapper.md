---
title: "COM Callable Wrapper | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "CCW"
  - "COM interop, COM wrappers"
  - "COM wrappers"
  - "callable wrappers"
  - "interoperation with unmanaged code, COM wrappers"
  - "COM callable wrappers"
ms.assetid: d04be3b5-27b9-4f5b-8469-a44149fabf78
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# COM Callable Wrapper
Cuando un cliente COM llama a un objeto .NET, Common Language Runtime crea el objeto administrado y un contenedor CCW \(COM callable wrapper\) para el objeto.  Como no pueden hacer referencia a los objetos .NET directamente, los clientes COM usan el CCW como un proxy del objeto administrado.  
  
 El motor en tiempo de ejecución crea exactamente un CCW para un objeto administrado, independientemente del número de clientes COM que soliciten sus servicios.  Como se muestra en la siguiente ilustración, varios clientes COM pueden guardar una referencia al CCW que expone la interfaz INew.  A su vez, el CCW contiene una única referencia al objeto administrado que implementa la interfaz y se recolectan los elementos no utilizados.  Los clientes COM y .NET pueden hacer solicitudes en un objeto administrado simultáneamente.  
  
 ![Contenedor CCW &#40;COM callable wrapper&#41;](../../../docs/framework/interop/media/ccw.gif "ccw")  
Acceso a los objetos .NET mediante el contenedor CCW  
  
 Los contenedores CCW no están visibles para otras clases en ejecución en .NET Framework.  Su objetivo principal es calcular las referencias de llamadas entre código administrado y no administrado; sin embargo, los CCW también pueden administrar la identidad y la duración de los objetos administrados que contienen.  
  
## Identidad de objetos  
 El motor en tiempo de ejecución asigna memoria para el objeto .NET desde su montón tras haber eliminado la memoria no utilizada, lo que permite que el motor en tiempo de ejecución mueva el objeto en la memoria como sea necesario.  En contraposición, el motor en tiempo de ejecución asigna al CCW memoria de un montón en el que no se ha eliminado la memoria no utilizada, con lo que los clientes COM pueden hacer referencia al contenedor directamente.  
  
## Duración de objetos  
 A diferencia del cliente .NET que contiene, las referencias del CCW se cuentan siguiendo la manera habitual de COM.  Cuando el número de referencias del CCW llega a cero, el contenedor libera su referencia en el objeto administrado.  Los objetos administrados a los que ya no quedan referencias se recogen en el siguiente ciclo de recolección de memoria no utilizada.  
  
## Simulación de interfaces COM  
 El [contenedor CCW](../../../docs/framework/interop/com-callable-wrapper.md) \(CCW\) expone todos los tipos de datos, interfaces visibles para COM públicas y valores devueltos a los clientes COM de manera coherente con los requisitos de COM de interacción basada en la interfaz.  Para un cliente COM, la invocación de métodos en un objeto .NET Framework es idéntica a la invocación de métodos en un objeto COM.  
  
 Para crear este enfoque uniforme, el CCW produce interfaces COM tradicionales como **IUnknown** e **IDispatch**.  Como se muestra en la siguiente ilustración, el CCW mantiene una sola referencia en el objeto .NET que encapsula.  El cliente COM y el objeto .NET interactúan entre sí a través de la construcción de proxy y código auxiliar del CCW.  
  
 ![Interfaces COM](../../../docs/framework/interop/media/ccwwithinterfaces.gif "ccwwithinterfaces")  
Interfaces COM y CCW  
  
 Además de exponer las interfaces implementadas explícitamente por una clase en el entorno administrado, .NET Framework proporciona implementaciones de las interfaces COM enumeradas en la tabla siguiente en nombre del objeto.  Una clase .NET puede proporcionar su propia implementación de estas interfaces para invalidar el comportamiento predeterminado.  Sin embargo, el runtime proporciona siempre la implementación de las interfaces **IUnknown** e **IDispatch**.  
  
|Interfaz|Descripción|  
|--------------|-----------------|  
|**Idispatch**|Proporciona un mecanismo para el enlace en tiempo de ejecución al tipo.|  
|**IerrorInfo**|Proporciona una descripción textual del error, su origen, un archivo de ayuda, contexto de ayuda y el GUID de la interfaz que definió el error \(siempre **GUID\_NULL** para las clases. NET\).|  
|**IprovideClassInfo**|Permite que los clientes COM tengan acceso a la interfaz **ITypeInfo** implementada por una clase administrada.|  
|**IsupportErrorInfo**|Permite a un cliente COM determinar si el objeto administrado es compatible con la interfaz **IErrorInfo**.  Si es así, permite al cliente obtener un puntero al objeto de excepción más reciente.  Todos los tipos administrados son compatibles con la interfaz **IErrorInfo**.|  
|**ItypeInfo**|Proporciona información de tipos para una clase que es exactamente igual que la información de tipos producida Tlbexp.exe.|  
|**Iunknown**|Proporciona la implementación estándar de la interfaz **IUnknown** con la que el cliente COM administra la duración del CCW y proporciona coerción de tipos.|  
  
 Una clase administrada también puede proporcionar las interfaces COM que se describe en la tabla siguiente.  
  
|Interfaz|Descripción|  
|--------------|-----------------|  
|Interfaz de clase \(\_*classname*\)|Interfaz, expuesta por el runtime y no definida explícitamente, que expone todas las interfaces públicas, métodos, propiedades y campos que se exponen explícitamente en un objeto administrado.|  
|**IConnectionPoint** e **IconnectionPointContainer**|Interfaz para objetos que son origen de eventos basados en delegados \(interfaz para registrar suscriptores de eventos\).|  
|**IdispatchEx**|Interfaz proporcionada por el runtime si la clase implementa **IExpando**.  La interfaz **IDispatchEx** es una extensión de la interfaz **IDispatch** que, a diferencia de **IDispatch**, permite la enumeración, adición, eliminación y llamada de miembros con distinción de mayúsculas y minúsculas.|  
|**IEnumVARIANT**|Interfaz para clases de tipo colección que enumera los objetos de la colección si la clase implementa **IEnumerable**.|  
  
## Presentar la interfaz de clase  
 La interfaz de clase, que no se define explícitamente en el código administrado, es una interfaz que expone todos los métodos, propiedades, campos y eventos públicos que se exponen explícitamente en el objeto .NET.  Puede ser una interfaz dual o sólo de envío.  La interfaz de clase recibe el nombre de la propia clase .NET, precedida por un carácter de subrayado.  Por ejemplo, para la clase Mammal, la interfaz de clase es \_Mammal.  
  
 Para las clases derivadas, la interfaz de clase también expone todos los métodos, propiedades y campos públicos de la clase base.  La clase derivada también expone una interfaz de clase para cada clase base.  Por ejemplo, si la clase Mammal extiende la clase MammalSuperclass, que a su vez extiende System.Object, el objeto .NET expone a los clientes COM tres interfaces de clase llamadas \_Mammal, \_MammalSuperclass y \_Object.  
  
 Por ejemplo, observe la siguiente clase .NET:  
  
```vb  
' Applies the ClassInterfaceAttribute to set the interface to dual.  
<ClassInterface(ClassInterfaceType.AutoDual)> _  
' Implicitly extends System.Object.  
Public Class Mammal  
    Sub Eat()  
    Sub Breathe()  
    Sub Sleep()  
End Class  
  
```  
  
```csharp  
// Applies the ClassInterfaceAttribute to set the interface to dual.  
[ClassInterface(ClassInterfaceType.AutoDual)]  
// Implicitly extends System.Object.  
public class Mammal  
{  
    void  Eat();  
    void  Breathe():  
    void  Sleep();  
}  
```  
  
 El cliente COM puede obtener un puntero a una interfaz de clase denominada `_Mammal`, que se describe en la biblioteca de tipos que genera la herramienta [Exportador de la biblioteca de tipos \(Tlbexp.exe\)](../../../docs/framework/tools/tlbexp-exe-type-library-exporter.md).  Si la clase `Mammal` implementó una o más interfaces, estas aparecerán bajo la coclase.  
  
```  
[odl, uuid(…), hidden, dual, nonextensible, oleautomation]  
interface _Mammal : IDispatch  
{  
    [id(0x00000000), propget] HRESULT ToString([out, retval] BSTR*  
        pRetVal);  
    [id(0x60020001)] HRESULT Equals([in] VARIANT obj, [out, retval]  
        VARIANT_BOOL* pRetVal);  
    [id(0x60020002)] HRESULT GetHashCode([out, retval] short* pRetVal);  
    [id(0x60020003)] HRESULT GetType([out, retval] _Type** pRetVal);  
    [id(0x6002000d)] HRESULT Eat();  
    [id(0x6002000e)] HRESULT Breathe();  
    [id(0x6002000f)] HRESULT Sleep();  
}  
[uuid(…)]  
coclass Mammal   
{  
    [default] interface _Mammal;  
}  
```  
  
 Generar la interfaz de clase es una acción opcional.  De manera predeterminada, la interoperabilidad COM genera una interfaz solo de envío para cada clase que se exporta a una biblioteca de tipos.  La creación automática de esta interfaz se puede impedir o modificar aplicando <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> a la clase.   Si bien la interfaz de clase puede facilitar la tarea de exponer clases administradas a COM, sus usos son limitados.  
  
> [!CAUTION]
>  Si se usa la interfaz de clase en lugar de definir una interfaz propia de manera explícita, el control de las futuras versiones de la clase administrada puede ser más complicado.  Antes de usar la interfaz de clase lea las instrucciones siguientes.  
  
### Defina una interfaz explícita para que la usen los clientes COM en lugar de generar la interfaz de clase.  
 Dado que la interoperabilidad COM genera automáticamente una interfaz de clase, los cambios en versiones posteriores de la clase pueden modificar el diseño de la interfaz de clase expuesta por Common Language Runtime.  Puesto que los clientes COM no están preparados normalmente para controlar cambios en el diseño de una interfaz, se interrumpen si se cambia el diseño de miembro de la clase.  
  
 Esta instrucción enfatiza la idea de que las interfaces expuestas a los clientes COM no se deben modificar.  Para reducir el riesgo de que los clientes COM se interrumpan por volver a ordenar involuntariamente el diseño de interfaz, aísle del diseño de interfaz todos los cambios que se hagan en la clase definiendo las interfaces de manera explícita.  
  
 Use **ClassInterfaceAttribute** para desactivar la generación automática de la interfaz de clase e implemente una interfaz explícita para la clase, como muestra el fragmento de código siguiente:  
  
```vb  
<ClassInterface(ClassInterfaceType.None)>Public Class LoanApp  
    Implements IExplicit  
    Sub M() Implements IExplicit.M  
…  
End Class  
  
```  
  
```csharp  
[ClassInterface(ClassInterfaceType.None)]  
public class LoanApp : IExplicit {  
    void M();  
}  
```  
  
 El valor **ClassInterfaceType.None** impide que la interfaz de clase se genere cuando los metadatos de la clase se exportan a una biblioteca de tipos.  En el ejemplo anterior, los clientes COM tan solo pueden tener acceso a la clase `LoanApp` a través de la interfaz `IExplicit`.  
  
### Evite el almacenamiento en caché de identificadores de envío \(DISPID\).  
 El uso de la interfaz de clase es una opción aceptable para los clientes con scripts, los clientes de Microsoft Visual Basic 6.0 o cualquier cliente enlazado en tiempo de ejecución que no almacene en caché los identificadores DispId de los miembros de la interfaz.  Los identificadores DispId identifican los miembros de la interfaz para admitir enlaces en tiempo de ejecución.  
  
 Para la interfaz de clase, la generación de identificadores DispId se basa en la posición del miembro en la interfaz.  Si cambia el orden del miembro y exporta la clase a una biblioteca de tipos, modificará los identificadores DispId generados en la interfaz de clase.  
  
 Para evitar que los clientes COM enlazados en tiempo de ejecución se interrumpan al usar la interfaz de clase, aplique **ClassInterfaceAttribute** con el valor **ClassInterfaceType.AutoDispatch**.  Este valor implementa una interfaz de clase de solo envío, pero omite la descripción de la interfaz de la biblioteca de tipos.  Sin una descripción de la interfaz, los clientes no pueden almacenar en caché los identificadores DispId en tiempo de compilación.  Aunque este es el tipo predeterminado de la interfaz de clase, se puede aplicar el valor del atributo de forma explícita.  
  
```vb  
<ClassInterface(ClassInterfaceType.AutoDispatch)> Public Class LoanApp  
    Implements IAnother  
    Sub M() Implements IAnother.M  
…  
End Class  
  
```  
  
```csharp  
[ClassInterface(ClassInterfaceType.AutoDispatch]  
public class LoanApp : IAnother {  
    void M();  
}  
```  
  
 Para obtener el DispId de un miembro de interfaz en tiempo de ejecución, los clientes COM pueden llamar a **IDispatch.GetIdsOfNames**.  Para invocar un método en la interfaz, pase el DispId devuelto como argumento a **IDispatch.Invoke**.  
  
### Restrinja el uso de la opción de interfaz dual en la interfaz de clase.  
 Las interfaces duales permiten el enlace en tiempo de diseño y en tiempo de ejecución de los clientes COM con los miembros de interfaz.  El establecimiento de la interfaz de clase en dual puede ser útil en tiempo de diseño y durante las pruebas.  Esta opción también es aceptable para una clase administrada \(y sus clases base\) que no se va a modificar nunca.  En todos los demás casos, no es necesario establecer la interfaz de clase en dual.  
  
 Una interfaz dual generada automáticamente puede ser apropiada en algunos casos, pero a menudo genera complicaciones de control de versiones.  Por ejemplo, los clientes COM que usen la interfaz de clase de una clase derivada se pueden interrumpir con facilidad si se hacen cambios en la clase base.  Si la clase base es de terceros, el usuario no tiene control sobre el diseño de la interfaz de clase.  Además, a diferencia de una interfaz de solo envío, una interfaz dual \(**ClassInterface.AutoDual**\) proporciona una descripción de la interfaz de clase en la biblioteca de tipos exportada.  Dicha descripción hace que los clientes enlazados en tiempo de ejecución almacenen en caché los identificadores DispId en tiempo de ejecución.  
  
## Vea también  
 <xref:System.Runtime.InteropServices.ClassInterfaceAttribute>   
 [COM Callable Wrapper](../../../docs/framework/interop/com-callable-wrapper.md)   
 [COM Wrappers](../../../docs/framework/interop/com-wrappers.md)   
 [Exposing .NET Framework Components to COM](../../../docs/framework/interop/exposing-dotnet-components-to-com.md)   
 [Simulating COM Interfaces](http://msdn.microsoft.com/es-es/ad2ab959-e2be-411b-aaff-275c3fba606c)   
 [Qualifying .NET Types for Interoperation](../../../docs/framework/interop/qualifying-net-types-for-interoperation.md)   
 [Runtime Callable Wrapper](../../../docs/framework/interop/runtime-callable-wrapper.md)