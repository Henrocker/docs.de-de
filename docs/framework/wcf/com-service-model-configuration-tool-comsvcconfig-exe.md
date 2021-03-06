---
title: COM+ Service Model Configuration-Tool (ComSvcConfig.exe)
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Windows Communication Foundation, COM+ integration
- WCF, COM+ integration
ms.assetid: 7717c6c2-85fc-418b-a8ed-bad8e61cec5c
caps.latest.revision: "15"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 40e7644ade32f245772a8971cf0693683b980952
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="com-service-model-configuration-tool-comsvcconfigexe"></a>COM+ Service Model Configuration-Tool (ComSvcConfig.exe)
Das Befehlszeilentool COM+ Service Model Configuration (ComSvcConfig.exe) ermöglicht die Konfiguration von COM+-Schnittstellen, die als Webdienste verfügbar gemacht werden sollen.  
  
## <a name="syntax"></a>Syntax  
  
```  
ComSvcConfig.exe /install | /uninstall | /list [/application:<ApplicationID | ApplicationName>] [/contract:<ClassID | ProgID | *,InterfaceID | InterfaceName | *>] [/hosting:<complus | was>] [/webSite:<WebsiteName>] [/webDirectory:<WebDirectoryName>] [/mex] [/id] [/nologo] [/verbose] [/help] [/partial]  
```  
  
## <a name="remarks"></a>Hinweise  
  
> [!NOTE]
>  Sie müssen Administrator auf dem lokalen Computer sein, um ComSvcConfig.exe zu verwenden.  
  
 Das Tool befindet sich an folgendem Speicherort:  
  
 %SystemRoot%\Microsoft.Net\Framework\v3.0\Windows Communication Foundation\  
  
 Weitere Informationen zu ComSvcConfig.exe, finden Sie unter [Vorgehensweise: Verwenden Sie das COM+ Service Model Configuration-Tool](../../../docs/framework/wcf/feature-details/how-to-use-the-com-service-model-configuration-tool.md).  
  
 In der folgenden Tabelle werden die Modi beschrieben, die mit ComSvcConfig.exe verwendet werden können.  
  
|Option|Beschreibung|  
|------------|-----------------|  
|`install`|Installiert eine Konfiguration für eine COM+-Schnittstelle für die Service Model-Integration.<br /><br /> Kurzform: `/i`.|  
|`uninstall`|Deinstalliert eine Konfiguration für eine COM+-Schnittstelle aus der Service Model-Integration.<br /><br /> Kurzform: `/u`.|  
|`list`|Listet Informationen über COM+-Anwendungen und -Komponenten auf, die über Schnittstellen verfügen, die für die Service Model-Integration konfiguriert sind.<br /><br /> Kurzform: `/l`.|  
  
 In der folgenden Tabelle werden die Flags beschrieben, die mit ComSvcConfig.exe verwendet werden können.  
  
|Option|Beschreibung|  
|------------|-----------------|  
|`/application:`\< *ApplicationID* &#124; *Parameter "ApplicationName"*\>|Gibt die zu konfigurierende COM+-Anwendung an.<br /><br /> Kurzform: `/a`.|  
|`/contract:`\< *ClassID* &#124; *ProgID* &#124; \*,*InterfaceID* &#124; *Schnittstellenname* &#124;\*\>|Gibt die COM+-Komponente und -Schnittstelle an, die als Vertrag für den Dienst konfiguriert werden sollen.<br /><br /> Kurzform: `/c`.<br /><br /> Während Sie das Platzhalterzeichen (\*) kann verwendet werden, wenn Sie angeben, dass die Namen Komponenten- und Schnittstellennamen es wird empfohlen, dass Sie ihn nicht verwenden, da Sie Schnittstellen verfügbar, die Sie nicht zum beabsichtigten machen können.|  
|`/hosting:`\< *Complus* &#124; *wurde*\>|Gibt an, ob der COM+-Hostingmodus oder der Webhostingmodus verwendet werden soll.<br /><br /> Kurzform: `/h`.<br /><br /> Die Verwendung des COM+-Hostingmodus erfordert die explizite Aktivierung der COM+-Anwendung. Bei der Verwendung des Webhostingmodus wird die COM+-Anwendung automatisch aktiviert. Wenn die COM+-Anwendung eine Bibliotheksanwendung ist, wird sie im IIS-Prozess (Internetinformationsdienste) ausgeführt. Wenn die COM+-Anwendung eine Serveranwendung ist, wird sie im Dllhost.exe-Prozess ausgeführt.|  
|`/webSite:`\< *Angegebenen "Websitename"*\>|Gibt bei Verwendung des Webhostingmodus die Website für das Hosting an (siehe das `/hosting`-Flag).<br /><br /> Kurzform: `/w`.<br /><br /> Wenn keine Website angegeben wird, wird die Standardwebsite verwendet.|  
|`/webDirectory:`\< *WebDirectoryName*\>|Gibt bei Verwendung des Webhosting das virtuelle Hostingverzeichnis an (siehe das `/hosting`-Flag).<br /><br /> Kurzform: `/d`.|  
|`/mex`|Fügt der Standarddienstkonfiguration einen MEX-Dienstendpunkt (Metadata Exchange, Metadatenaustausch) hinzu, um Clients zu unterstützen, die eine Vertragsdefinition vom Dienst abrufen.<br /><br /> Kurzform: `/x`.|  
|`/id`|Zeigt die Anwendungs-, Komponenten- und Schnittstelleninformationen als IDs an.<br /><br /> Kurzform: `/k`.|  
|`/nologo`|Verhindert, dass ComSvcConfig.exe sein Logo anzeigt.<br /><br /> Kurzform: `/n`.|  
|`/verbose`|Gibt alle Warnungen oder Informationsmeldungen zusätzlich zu gefundenen Fehlern aus.<br /><br /> Kurzform: `/v`.|  
|`/help`|Zeigt die Syntaxmeldung an.<br /><br /> Kurzform: `/?`.|  
|`/partial`|Generiert eine Dienstkonfiguration, wenn die angegebene Schnittstelle ein oder mehr Methodensignaturen umfasst, die verfügbar gemacht werden können. Zum Zeitpunkt der Dienstinitialisierung werden kompatible Methoden als Vorgänge für den Dienstvertrag angezeigt, und nicht kompatible Methoden werden ignoriert und gelten als nicht vorhanden für den Dienstvertrag.<br /><br /> Fehlt das Flag, generiert das Tool keine Dienstkonfiguration, wenn die angegebene Schnittstelle ein oder mehr inkompatible Methoden umfasst.|  
  
## <a name="examples"></a>Beispiele  
  
### <a name="description"></a>Beschreibung  
 Im folgenden Beispiel wird die `IFinances`-Schnittstelle der `ItemOrders.IFinancial`-Komponente (aus der OnlineStore-COM+-Anwendung) mithilfe des COM+-Hostingmodus der Gruppe von Schnittstellen hinzugefügt, die als Webdienste verfügbar gemacht werden sollen. Alle Warnungen werden zusätzlich zu gefundenen Fehlern ausgegeben.  
  
### <a name="code"></a>Code  
  
```  
ComSvcConfig.exe /install /application:OnlineStore /contract:ItemOrders.Financial,IFinances /hosting:complus /verbose  
```  
  
### <a name="description"></a>Beschreibung  
 Im folgenden Beispiel wird die `IStockLevels`-Schnittstelle der `ItemInventory.Warehouse`-Komponente (aus der OnlineWarehouse-COM+-Anwendung) mithilfe des Webhostingmodus der Gruppe von Schnittstellen hinzugefügt, die als Webdienste verfügbar gemacht werden sollen. Der Webdienst wird im virtuellen IIS-Verzeichnis OnlineWarehouse gehostet.  
  
### <a name="code"></a>Code  
  
```  
ComSvcConfig.exe /install /application:OnlineWarehouse /contract:ItemInventory.Warehouse,IStockLevels /hosting:was /webDirectory:root/OnlineWarehouse  
```  
  
### <a name="description"></a>Beschreibung  
 Im folgenden Beispiel wird die `IFinances`-Schnittstelle der `ItemOrders.Financial`-Komponente (aus der OnlineStore-COM+-Anwendung) aus der Gruppe von Schnittstellen entfernt, die als Webdienste verfügbar gemacht werden.  
  
### <a name="code"></a>Code  
  
```  
ComSvcConfig.exe /uninstall /application:OnlineStore /interface:ItemOrders.Financial,IFinances /hosting:complus  
```  
  
### <a name="description"></a>Beschreibung  
 Im folgenden Beispiel werden die derzeit verfügbar gemachten COM+-gehosteten Schnittstellen zusammen mit den entsprechenden Adress- und Bindungsdetails für die OnlineStore-COM+-Anwendung auf dem lokalen Computer aufgelistet.  
  
### <a name="code"></a>Code  
  
```  
ComSvcConfig.exe /list /application:OnlineStore /hosting:complus  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Vorgehensweise: Verwenden des COM+-Dienstmodell-Konfigurationstools](../../../docs/framework/wcf/feature-details/how-to-use-the-com-service-model-configuration-tool.md)
