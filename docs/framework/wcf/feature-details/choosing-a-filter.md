---
title: "Ausw&#228;hlen eines Filters | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 67ab5af9-b9d9-4300-b3b1-41abb5a1fd10
caps.latest.revision: 8
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 8
---
# Ausw&#228;hlen eines Filters
Beim Konfigurieren des Routingdiensts ist es wichtig, richtige Nachrichtenfilter auszuwählen und so zu konfigurieren, dass Sie genaue Übereinstimmungen mit den Nachrichten erzielen können, die Sie empfangen.Falls die ausgewählten Filter in Bezug auf die Übereinstimmungen zu ungenau oder falsch konfiguriert sind, werden die Nachrichten nicht korrekt weitergeleitet.Wenn die Filter zu restriktiv sind, kann es sein, dass für einige Nachrichten keine gültigen Weiterleitungsrouten verfügbar sind.  
  
## Filtertypen  
 Beim Auswählen der vom Routingdienst verwendeten Filter ist es wichtig, dass Sie verstehen, wie die einzelnen Filter funktionieren. Außerdem sollten Sie wissen, welche Informationen in Verbindung mit den eingehenden Nachrichten verfügbar sind.Falls beispielsweise alle Nachrichten über den gleichen Endpunkt empfangen werden, sind die Adress\- und EndpointName\-Filter nicht hilfreich, weil alle Nachrichten Übereinstimmungen mit diesen Filtern aufweisen.  
  
### Action  
 Der Action\-Filter überprüft die <xref:System.ServiceModel.Channels.MessageHeaders.Action%2A>\-Eigenschaft.Falls der Inhalt des Action\-Headers in der Nachricht mit dem Filterdatenwert übereinstimmt, der in der Filterkonfiguration angegeben ist, gibt dieser Filter `true` zurück.Im folgenden Beispiel wird ein `FilterElement` definiert, das den Action\-Filter verwendet, um für Nachrichten mit einem Aktionsheader, der den Wert "http:\/\/namespace\/contract\/operation\/" enthält, nach Übereinstimmungen zu suchen.  
  
```xml  
<filter name="action1" filterType="Action" filterData="http://namespace/contract/operation/" />  
```  
  
```csharp  
ActionMessageFilter action1 = new ActionMessageFilter(new string[] { "http://namespace/contract/operation" });  
  
```  
  
 Dieser Filter sollte beim Weiterleiten von Nachrichten verwendet werden, die einen eindeutigen Action\-Header enthalten.  
  
### EndpointAddress  
 Der EndpointAddress\-Filter überprüft die EndpointAddress, über die die Nachricht empfangen wurde.Wenn die Adresse, über die die Nachricht eingeht, genau mit der in der Filterkonfiguration angegebenen Filteradresse übereinstimmt, gibt dieser Filter `true` zurück.Im folgenden Beispiel wird ein `FilterElement` definiert, dass den Address\-Filter verwendet, um Übereinstimmungen für alle Nachrichten zu ermitteln, die an "http:\/\/\<hostname\>\/vdir\/s.svc\/b" addressiert sind.  
  
```xml  
<filter name="address1" filterType="EndpointAddress" filterData="http://host/vdir/s.svc/b" />  
  
```  
  
```csharp  
EndpointAddressMessageFilter address1 = new EndpointAddressMessageFilter(new EndpointAddress("http://host/vdir/s.svc/b"), false);  
  
```  
  
> [!NOTE]
>  Beachten Sie dabei, dass sich der Hostnamenteil einer Adresse in Abhängigkeit davon unterscheiden kann, ob der Client den vollqualifizierten Domänennamen, den NetBIOS\-Namen, die IP\-Adresse oder einen anderen Namen verwendet.Da verschiedene Werte auf den gleichen Host verweisen können, besteht das Standardverhalten für diesen Vergleich nicht darin, beim Ermitteln von Übereinstimmungen den Hostnamenteil der Adresse zu verwenden.  
>   
>  Dieses Verhalten kann geändert werden, damit der Vergleich beim programmgesteuerten Konfigurieren des Routingdiensts den Hostnamen auswerten kann.  
  
 Dieser Filter sollte verwendet werden, wenn die eingehenden Nachrichten an eine eindeutige Adresse adressiert sind.  
  
### EndpointAddressPrefix  
 Der EndpointAddressPrefix\-Filter ähnelt dem EndpointAddress\-Filter.Der EndpointAddressPrefix\-Filter überprüft die EndpointAddress, über die die Nachricht empfangen wurde.Der EndpointAddressPrefix\-Filter fungiert jedoch als Platzhalter, indem er Übereinstimmungen für Adressen ermittelt, die mit dem in der Filterkonfiguration angegebenen Wert beginnen.Im folgenden Beispiel wird ein `FilterElement` definiert, dass den EndpointAddressPrefix\-Filter verwendet, um Übereinstimmungen für alle Nachrichten zu ermitteln, die an "http:\/\/\<hostname\>\/vdir\*" addressiert sind.  
  
```xml  
<filter name="prefix1" filterType="EndpointAddressPrefix" filterData="http://host/vdir" />  
  
```  
  
```csharp  
PrefixEndpointAddressMessageFilter prefix1 = new PrefixEndpointAddressMessageFilter(new EndpointAddress("http://host/vdir/s.svc/b"), false);  
  
```  
  
> [!NOTE]
>  Beachten Sie dabei, dass sich der Hostnamenteil einer Adresse in Abhängigkeit davon unterscheiden kann, ob der Client den vollqualifizierten Domänennamen, den NetBIOS\-Namen, die IP\-Adresse oder einen anderen Namen verwendet.Da verschiedene Werte auf den gleichen Host verweisen können, besteht das Standardverhalten für diesen Vergleich nicht darin, beim Ermitteln von Übereinstimmungen den Hostnamenteil der Adresse zu verwenden.  
  
 Dieser Filter sollte verwendet werden, wenn eingehende Nachrichten weitergeleitet werden, die über ein gemeinsames Adresspräfix verfügen.  
  
### AND  
 Der AND\-Filter filtert nicht direkt nach einem Wert innerhalb einer Nachricht, sondern ermöglicht Ihnen die Kombination von zwei anderen Filtern, um eine `AND`\-Bedingung zu erstellen. Dabei müssen beide Filter eine Übereinstimmung mit der Nachricht ergeben, bevor für den AND\-Filter `true` ausgewertet wird.Auf diese Weise können Sie komplexe Filter erstellen, die nur dann Übereinstimmungen ergeben, wenn alle Unterfilter zu Übereinstimmungen führen.Im folgenden Beispiel werden ein Adressfilter und ein Aktionsfilter definiert. Anschließend wird ein AND\-Filter definiert, der eine Nachricht sowohl für den Adressfilter als auch für den Aktionsfilter auswertet.Falls der Adressfilter und der Aktionsfilter zu Übereinstimmungen führen, gibt der AND\-Filter `true` zurück.  
  
```xml  
<filter name=”address1” filterType=”AddressPrefix” filterData=”http://host/vdir”/>  
<filter name=”action1” filterType=”Action” filterData=”http://namespace/contract/operation/”/>  
<filter name="and1" filterType="And" filter1="address1" filter2="action1" />  
  
```  
  
```csharp  
EndpointAddressMessageFilter address1 = new EndpointAddressMessageFilter(new EndpointAddress("http://host/vdir/s.svc/b"), false);  
ActionMessageFilter action1 = new ActionMessageFilter(new string[] { "http://namespace/contract/operation" });  
StrictAndMessageFilter and1=new StrictAndMessageFilter(address1, action1);  
  
```  
  
 Dieser Filter sollte verwendet werden, wenn Sie die Logik mehrerer Filter kombinieren müssen, um festzulegen, wann eine Übereinstimmung erzielt werden soll.Wenn Sie z. B. über mehrere Ziele verfügen, die nur bestimmte Kombinationen von Aktionen und Nachrichten unter bestimmten Adressen empfangen dürfen, können Sie die erforderlichen Aktions\- und Adressfilter mithilfe eines AND\-Filters kombinieren.  
  
### Benutzerdefiniert  
 Wenn Sie den Filtertyp "Benutzerdefiniert" auswählen, müssen Sie einen customType\-Wert mit dem Typ von Assembly bereitstellen, der die **MessageFilter**\-Implementierung enthält, die für diesen Filter verwendet werden soll.Außerdem muss "filterData" alle Werte enthalten, die der benutzerdefinierte Filter beim Auswerten der Nachrichten ggf. erfordert.Im folgenden Beispiel wird ein `FilterElement` definiert, dass die `CustomAssembly.MyCustomMsgFilter`\-MessageFilter\-Implementierung verwendet.  
  
```xml  
<filter name="custom1" filterType="Custom" customType="CustomAssembly.MyCustomMsgFilter, CustomAssembly" filterData="Custom Data" />  
  
```  
  
```csharp  
MyCustomMsgFilter custom1=new MyCustomMsgFilter(“Custom Data”);  
```  
  
 Wenn Sie die benutzerdefinierte Übereinstimmungslogik auf eine Nachricht anwenden müssen, die nicht von den unter [!INCLUDE[netfx_current_short](../../../../includes/netfx-current-short-md.md)] bereitgestellten Filtern abgedeckt wird, müssen Sie einen benutzerdefinierten Filter erstellen, der eine Implementierung der **MessageFilter**\-Klasse darstellt.Sie können z. B. einen benutzerdefinierten Filter erstellen, der ein Feld in der eingehenden Nachricht mit einer Liste bekannter Werte vergleicht, die dem Filter als Konfiguration vorliegen. Oder Sie können einen Filter erstellen, der den Hashwert für ein bestimmtes Nachrichtenelement generiert und diesen Wert dann untersucht und angibt, ob der Filter `true` oder `false` zurückgeben soll.  
  
### EndpointName  
 Der EndpointName\-Filter überprüft den Namen des Endpunkts, der die Nachricht empfangen hat.Im folgenden Beispiel wird ein `FilterElement` definiert, das den EndpointName\-Filter zum Weiterleiten von Nachrichten verwendet, die über "SvcEndpoint" empfangen wurden.  
  
```xml  
<filter name="name1" filterType="Endpoint" filterData="SvcEndpoint" />  
  
```  
  
```csharp  
EndpointNameMessageFilter name1 = new EndpointNameMessageFilter("SvcEndpoint");  
  
```  
  
 Dieser Filter ist nützlich, wenn der Routingdienst mehr als einen benannten Dienstendpunkt verfügbar macht.Sie können z. B. zwei Endpunkte verfügbar machen, die der Routingdienst zum Empfangen von Nachrichten verwendet. Einer wird von Prioritätskunden verwendet, die eine Echtzeitverarbeitung ihrer Nachrichten benötigen, während der andere Endpunkt Nachrichten empfängt, die nicht eilig sind.  
  
 Sie können zwar häufig die Übereinstimmungsprüfung für vollständige Adressen verwenden, um zu ermitteln, über welchen Endpunkt eine Nachricht empfangen wurde, aber die Verwendung des definierten Endpunktnamens stellt eine einfache Alternative dar, die oft weniger fehleranfällig ist. Dies gilt besonders beim Konfigurieren eines Routingdiensts mithilfe einer Konfigurationsdatei \(bei denen Endpunktnamen ein erforderliches Attribut darstellen\).  
  
### MatchAll  
 Der MatchAll\-Filter ergibt für alle empfangenen Nachrichten Übereinstimmungen.Dies ist nützlich, wenn Sie alle empfangenen Nachrichten immer an einen bestimmten Endpunkt weiterleiten müssen, z. B. bei einem Protokollierungsdienst, der eine Kopie jeder empfangenen Nachricht speichert.Im folgenden Beispiel wird ein `FilterElement` definiert, das den MatchAll\-Filter verwendet.  
  
```xml  
<filter name="matchAll1" filterType="MatchAll" />  
  
```  
  
```csharp  
MatchAllMessageFilter matchAll1 = new MatchAllMessageFilter();  
  
```  
  
### XPath  
 Mit dem XPath\-Filter können Sie eine XPath\-Abfrage angeben, die verwendet wird, um ein bestimmtes Element innerhalb der Nachricht zu überprüfen.Die XPath\-Filterung ist eine leistungsstarke Filteroption, mit der Sie jeden per XML\-Adressierung erreichbaren Eintrag in der Nachricht direkt untersuchen können. Dafür ist es jedoch erforderlich, dass Sie über genaue Kenntnisse der Struktur der Nachrichten verfügen, die Sie empfangen.Im folgenden Beispiel wird ein `FilterElement` definiert, das den XPath\-Filter zum Untersuchen der Nachricht für ein Element mit dem Namen "element" innerhalb des Namespace verwendet, auf den mit dem Namespacepräfix "ns" verwiesen wird.  
  
```xml  
<filter name="xpath1" filterType="XPath" filterData="//ns:element" />  
  
```  
  
```csharp  
XPathMessageFilter xpath1=new XPathMessageFilter(“//ns:element”);  
  
```  
  
 Dieser Filter ist nützlich, wenn Sie wissen, dass die empfangenen Nachrichten einen bestimmten Wert enthalten.Wenn Sie beispielsweise zwei Versionen des gleichen Diensts hosten und wissen, dass an die neuere Version des Diensts adressierte Nachrichten in einem benutzerdefinierten Header einen eindeutigen Wert enthalten, können Sie einen speziellen Filter erstellen. Der Filter verwendet XPath zum Navigieren zu diesem Header und vergleicht den im Header enthaltenen Wert mit einem anderen Wert in der Filterkonfiguration, um zu bestimmen, ob der Filter eine Übereinstimmung ergibt.  
  
 Da XPath\-Abfragen häufig eindeutige Namespaces enthalten, bei denen es sich oft um lange oder komplexe Zeichenfolgenwerte handelt, können Sie mit dem XPath\-Filter die Namespacetabelle zum Definieren eindeutiger Präfixe für die Namespaces verwenden.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] zur Namespacetabelle finden Sie unter [Nachrichtenfilter](../../../../docs/framework/wcf/feature-details/message-filters.md).  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] zum Entwerfen von XPath\-Abfragen finden Sie unter [XPath\-Syntax](http://go.microsoft.com/fwlink/?LinkId=164592) \(http:\/\/go.microsoft.com\/fwlink\/?LinkId\=164592\).  
  
## Siehe auch  
 [Nachrichtenfilter](../../../../docs/framework/wcf/feature-details/message-filters.md)   
 [Vorgehensweise: Verwenden von Filtern](../../../../docs/framework/wcf/feature-details/how-to-use-filters.md)