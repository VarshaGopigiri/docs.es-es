---
title: "Firmar procedimientos almacenados en SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: eeed752c-0084-48e5-9dca-381353007a0d
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# Firmar procedimientos almacenados en SQL Server
Puede firmar un procedimiento almacenado con un certificado o una clave asimétrica.  Esto está diseñado para los casos en los que no se pueden heredar permisos mediante encadenamiento de propiedad o cuando la cadena de propiedad está rota, como en SQL dinámico.  Entonces, se crea un usuario asignado al certificado, el cual concede permisos de usuario en los objetos a los que el procedimiento almacenado necesita tener acceso.  
  
 Cuando se ejecuta el procedimiento almacenado, SQL Server combina los permisos del usuario del certificado con los del llamador.  A diferencia de la cláusula EXECUTE AS, aquí no cambia el contexto de ejecución del procedimiento.  La funciones integradas que devuelven nombres de usuario e inicio de sesión devuelven el nombre del llamador, no el nombre de usuario del certificado.  
  
 Una firma digital es un resumen de datos cifrados con una clave privada del firmante.  La clave privada garantiza que la firma digital sea única para su portador o propietario.  Se pueden firmar procedimientos almacenados, funciones o desencadenadores.  
  
> [!NOTE]
>  Se puede crear un certificado en la base de datos maestra para conceder permisos a nivel de servidor.  
  
## Crear certificados  
 Al firmar un procedimiento almacenado con un certificado, se crea mediante la clave privada un resumen de datos que consta de hash cifrado de código del procedimiento almacenado.  En tiempo de ejecución, el resumen de datos se descifra con la clave pública y se compara con el valor hash del procedimiento almacenado.  La modificación del procedimiento almacenado invalida el valor hash, de manera que la firma digital ya no coincide.  Con ello, se evita que alguien que no tenga acceso a la clave privada pueda cambiar el código del procedimiento almacenado.  Por lo tanto, deberá volver a firmar el procedimiento almacenado cada vez que lo modifique.  
  
 Son cuatro los pasos que implica la firma de un módulo:  
  
1.  Crear un certificado mediante la instrucción Transact\-SQL `CREATE CERTIFICATE [certificateName]`.  Esta instrucción tiene varias opciones para establecer una fecha de inicio y finalización, así como una contraseña.  La fecha de expiración predeterminada es un año  
  
2.  Crear una base de datos asociada a un certificado utilizando la instrucción Transact\-SQL `CREATE USER [userName] FROM CERTIFICATE [certificateName]`.  Este usuario existe únicamente en la base de datos y no está asociado a un inicio de sesión.  
  
3.  Conceder al usuario del certificado los permisos necesarios en los objetos de la base de datos.  
  
> [!NOTE]
>  Un certificado no puede conceder permisos a un usuario que tiene permisos revocados con la instrucción DENY.  DENY siempre tiene prioridad sobre GRANT, lo que evita que el llamador herede permisos concedidos al usuario del certificado.  
  
1.  Firmar el procedimiento con el certificado utilizando la instrucción Transact\-SQL `ADD SIGNATURE TO [procedureName] BY CERTIFICATE [certificateName]`.  
  
## Recursos externos  
 Para obtener más información, vea los siguientes recursos.  
  
|Recurso|Descripción|  
|-------------|-----------------|  
|[Firma de módulos \(Motor de base de datos\)](http://go.microsoft.com/fwlink/?LinkId=98590) en los Libros en pantalla de SQL Server.|Describe la firma de módulos, con un caso de ejemplo, y proporciona vínculos a los temas importantes de Transact\-SQL.|  
|[Tutorial: Firmar procedimientos almacenados con un certificado](http://msdn.microsoft.com/library/bb283630.aspx) en los Libros en pantalla de SQL Server.|Proporciona un tutorial sobre la firma de procedimientos almacenados con un certificado.|  
  
## Vea también  
 [Proteger aplicaciones de ADO.NET](../../../../../docs/framework/data/adonet/securing-ado-net-applications.md)   
 [Información general sobre seguridad de SQL Server](../../../../../docs/framework/data/adonet/sql/overview-of-sql-server-security.md)   
 [Escenarios de seguridad de aplicaciones en SQL Server](../../../../../docs/framework/data/adonet/sql/application-security-scenarios-in-sql-server.md)   
 [Administrar permisos con procedimientos almacenados en SQL Server](../../../../../docs/framework/data/adonet/sql/managing-permissions-with-stored-procedures-in-sql-server.md)   
 [Escribir SQL dinámico seguro en SQL Server](../../../../../docs/framework/data/adonet/sql/writing-secure-dynamic-sql-in-sql-server.md)   
 [Personalizar permisos con suplantación en SQL Server](../../../../../docs/framework/data/adonet/sql/customizing-permissions-with-impersonation-in-sql-server.md)   
 [Modificar datos con procedimientos almacenados](../../../../../docs/framework/data/adonet/modifying-data-with-stored-procedures.md)   
 [Proveedores administrados de ADO.NET y centro de desarrolladores de conjuntos de datos](http://go.microsoft.com/fwlink/?LinkId=217917)