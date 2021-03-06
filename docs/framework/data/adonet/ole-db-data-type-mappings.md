---
title: "Asignar tipos de datos OLE DB | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 04bcb259-59d3-4fd7-894d-4f0dd0c68069
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Asignar tipos de datos OLE DB
En la siguiente tabla se muestra el tipo [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] deducido de los tipos de datos del proveedor de datos .NET Framework para ADO y OLE DB \(<xref:System.Data.OleDb>\).  También se incluyen los métodos de los descriptores de acceso con tipo de <xref:System.Data.OleDb.OleDbDataReader>.  
  
|Tipo de ADO|Tipo de OLE DB|Tipo de [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]|Descriptor de acceso con tipo de [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]|  
|-----------------|--------------------|-------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------|  
|adBigInt|DBTYPE\_I8|Int64|GetInt64\(\)|  
|adBinary|DBTYPE\_BYTES|Byte\[\]|GetBytes\(\)|  
|adBoolean|DBTYPE\_BOOL|Boolean|GetBoolean\(\)|  
|adBSTR|DBTYPE\_BSTR|String|GetString\(\)|  
|adChapter|DBTYPE\_HCHAPTER|Compatible con `DataReader`.  Consulta [Recuperar datos mediante DataReader](../../../../docs/framework/data/adonet/retrieving-data-using-a-datareader.md).|GetValue\(\)|  
|adChar|DBTYPE\_STR|String|GetString\(\)|  
|adCurrency|DBTYPE\_CY|Decimal|GetDecimal\(\)|  
|adDate|DBTYPE\_DATE|DateTime|GetDateTime\(\)|  
|adDBDate|DBTYPE\_DBDATE|DateTime|GetDateTime\(\)|  
|adDBTime|DBTYPE\_DBTIME|DateTime|GetDateTime\(\)|  
|adDBTimeStamp|DBTYPE\_DBTIMESTAMP|DateTime|GetDateTime\(\)|  
|adDecimal|DBTYPE\_DECIMAL|Decimal|GetDecimal\(\)|  
|adDouble|DBTYPE\_R8|Double|GetDouble\(\)|  
|adError|DBTYPE\_ERROR|ExternalException|GetValue\(\)|  
|adFileTime|DBTYPE\_FILETIME|DateTime|GetDateTime\(\)|  
|adGUID|DBTYPE\_GUID|Guid|GetGuid\(\)|  
|adIDispatch|DBTYPE\_IDISPATCH \*|Objeto|GetValue\(\)|  
|adInteger|DBTYPE\_I4|Int32|GetInt32\(\)|  
|adIUnknown|DBTYPE\_IUNKNOWN \*|Objeto|GetValue\(\)|  
|adNumeric|DBTYPE\_NUMERIC|Decimal|GetDecimal\(\)|  
|adPropVariant|DBTYPE\_PROPVARIANT|Objeto|GetValue\(\)|  
|adSingle|DBTYPE\_R4|Single|GetFloat\(\)|  
|adSmallInt|DBTYPE\_I2|Int16|GetInt16\(\)|  
|adTinyInt|DBTYPE\_I1|Byte|GetByte\(\)|  
|adUnsignedBigInt|DBTYPE\_UI8|UInt64|GetValue\(\)|  
|adUnsignedInt|DBTYPE\_UI4|UInt32|GetValue\(\)|  
|adUnsignedSmallInt|DBTYPE\_UI2|UInt16|GetValue\(\)|  
|adUnsignedTinyInt|DBTYPE\_UI1|Byte|GetByte\(\)|  
|adVariant|DBTYPE\_VARIANT|Objeto|GetValue\(\)|  
|adWChar|DBTYPE\_WSTR|String|GetString\(\)|  
|adUserDefined|DBTYPE\_UDT|no admitido||  
|adVarNumeric|DBTYPE\_VARNUMERIC|no admitido||  
  
 \* En el caso de los tipos OLE DB `DBTYPE_IUNKNOWN` y `DBTYPE_IDISPATCH`, la referencia del objeto es una representación del puntero con referencias calculadas.  
  
## Vea también  
 [Recuperación y modificación de datos en ADO.NET](../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)   
 [Proveedores administrados de ADO.NET y centro de desarrolladores de conjuntos de datos](http://go.microsoft.com/fwlink/?LinkId=217917)