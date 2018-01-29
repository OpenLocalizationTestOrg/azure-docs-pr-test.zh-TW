---
title: "Azure App Service 混合式連線 | Microsoft Docs"
description: "如何建立和使用混合式連線以存取不同網路的資源"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: 66774bde-13f5-45d0-9a70-4e9536a4f619
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/20/2017
ms.author: ccompy
ms.openlocfilehash: 677642e4e97523ed71ff5857ae27263743dca535
ms.sourcegitcommit: cfd1ea99922329b3d5fab26b71ca2882df33f6c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/30/2017
---
# <a name="azure-app-service-hybrid-connections"></a>Azure App Service 混合式連線 #

混合式連線既是 Azure 服務，也是 Azure App Service 功能。 作為服務時，它具有 App Service 所利用之用途和功能以外的用途和功能。 若要深入了解混合式連線及其在 App Service 之外的使用方式，請參閱 [Azure 轉送混合式連線][HCService]。

在 App Service 中，「混合式連線」可用來存取其他網路中的應用程式資源。 它可讓您從應用程式存取應用程式端點。 它不會啟用替代功能來存取應用程式。 和在 App Service 中使用時相同，每個「混合式連線」都會與單一 TCP 主機和連接埠的組合相互關聯。 這意謂著「混合式連線」端點可以位於任何作業系統和任何應用程式上，只要您可以存取 TCP 接聽連接埠即可。 混合式連線不會知道 (或不在意) 應用程式通訊協定為何，或您要存取什麼資源。 它只負責提供網路存取。  


## <a name="how-it-works"></a>運作方式 ##
「混合式連線」功能是由對「Azure 服務匯流排轉送」發出的兩個輸出呼叫所組成。 在 App Service 中執行您應用程式的主機上，會從程式庫連線過來。 也會從 Microsoft Azure 混合式連線管理員連線到服務匯流排轉送。 HCM 是您在網路內部署的轉送服務，該網路裝載您要嘗試存取的資源。 

透過這個兩個聯結的連線，應用程式便會有一個可通往 HCM 另一端固定之「主機:連接埠」組合的 TCP 通道。 連線會使用 TLS 1.2 以求安全性，並使用共用存取簽章 (SAS) 金鑰來進行驗證和授權。    

![混合式連線概要流程圖表][1]

當應用程式提出的 DNS 要求與所設定的「混合式連線」端點相符時，系統就會透過「混合式連線」將輸出 TCP 流量重新導向。  

> [!NOTE]
> 這表示您應該嘗試一律對混合式連線使用 DNS 名稱。 如果端點改為使用 IP 位址，某些用戶端軟體不會執行 DNS 查閱。
>
>

「混合式連線」功能有兩種：分別是在「服務匯流排轉送」底下以服務形式提供的新式「混合式連線」，以及舊式的「Azure BizTalk 服務混合式連線」。 後者在入口網站中稱為「傳統混合式連線」。 本文稍後會提供這種連線的詳細資訊。

### <a name="app-service-hybrid-connection-benefits"></a>App Service 混合式連線優點 ###

「混合式連線」功能有一些優點，包括：

- 應用程式可以安全地存取內部部署系統和服務。
- 此功能不需要可存取網際網路的端點。
- 安裝速度快且過程簡單。 
- 每個「混合式連線」都會與單一的「主機:連接埠」組合對應，有助於提高安全性。
- 通常不需要在防火牆開洞。 連線全都是透過標準的 Web 連接埠輸出。
- 由於這是網路層級的功能，因此不會因為應用程式所使用的語言及端點所使用的技術而受到影響。
- 它可用來讓您從單一應用程式存取多個網路。 

### <a name="things-you-cannot-do-with-hybrid-connections"></a>混合式連線無法執行的作業 ###

有一些作業您無法透過「混合式連線」來執行，包括：

- 掛接磁碟機。
- 使用 UDP。
- 存取使用動態連接埠的 TCP 型服務 (例如「FTP 被動模式」或「延伸被動模式」)。
- 因為有時會需要 UDP，所以支援 LDAP。
- 支援 Active Directory。

## <a name="add-and-create-hybrid-connections-in-your-app"></a>在您的應用程式中新增和建立混合式連線 ##

您可以透過 Azure 入口網站中的 App Service 應用程式，或從 Azure 入口網站中的「Azure 轉送」，來建立「混合式連線」。 建議您透過要與「混合式連線」搭配使用的 App Service 應用程式，來建立「混合式連線」。 若要建立「混合式連線」，請移至 [Azure 入口網站][portal]，然後選取您的應用程式。 選取 [網路] > [設定您的混合式連接端點]。 您可以在這裡看到為您應用程式設定的「混合式連線」。  

![混合式連線清單的螢幕擷取畫面][2]

若要新增混合式連線，請選取 [新增混合式連線]。  您會看見已建立的混合式連線清單。 若要在應用程式中新增其中的一或多個混合式連線，請按一下您想要的混合式連線，然後選取 [新增選取的混合式連線]。  

![混合式連線入口網站的螢幕擷取畫面][3]

如果您想要建立新的「混合式連線」，請選取 [建立新的混合式連線]。 指定下列項目： 

- 端點名稱。
- 端點主機名稱。
- 端點連接埠。
- 您想要使用的「服務匯流排」命名空間。

![[建立新的混合式連線] 對話方塊螢幕擷取畫面][4]

每個「混合式連線」都會繫結至一個「服務匯流排」命名空間，而每個「服務匯流排」命名空間都位於 Azure 區域中。 請務必嘗試使用與應用程式位於相同區域的「服務匯流排」命名空間，以避免網路所引發的延遲。

如果您想要移除應用程式中的「混合式連線」，請對它按一下滑鼠右鍵，然後選取 [中斷連線]。  

將「混合式連線」新增至應用程式之後，您只要選取它就可以查看詳細資料。 

![混合式連線詳細資料的螢幕擷取畫面][5]

### <a name="create-a-hybrid-connection-in-the-azure-relay-portal"></a>在 Azure 轉送入口網站中建立混合式連線 ###

除了透過入口網站從您應用程式內進行的方式之外，您也可以從「Azure 轉送」入口網站內建立「混合式連線」。 若要讓 App Service 使用混合式連線，必須：

* 要求用戶端授權。
* 擁有一個以「主機:連接埠」組合作為值的中繼資料項目具名端點。

## <a name="hybrid-connections-and-app-service-plans"></a>混合式連線和 App Service 方案 ##

只有在「基本」、「標準」、「進階」及「隔離」定價 SKU 中，才有提供「混合式連線」功能。 定價方案會有相關聯的限制。  

> [!NOTE] 
> 您只能根據「Azure 轉送」來建立新的「混合式連線」。 您無法建立新的「BizTalk 混合式連線」。
>

| 定價方案 | 方案中可用的混合式連線數目 |
|----|----|
| 基本 | 5 |
| 標準 | 25 |
| 進階 | 200 |
| 隔離 | 200 |

請注意，App Service 方案會顯示您正在使用的混合式連線數目，以及由哪些應用程式使用。  

![App Service 方案屬性的螢幕擷取畫面][6]

請選取 [混合式連線] 以查看詳細資料。 您可以看到在應用程式檢視中所看到的所有資訊。 您也可以查看在相同的方案中，有多少其他的應用程式使用了該混合式連線。

可用於 App Service 方案的混合式連線端點數目有其上限。 不過，每個使用的混合式連線，則可用於方案中任何數目的應用程式上。 例如，一個在「App Service 方案」中 5 個個別應用程式上使用的「混合式連線」，只算 1 個「混合式連線」。

使用「混合式連線」需額外付費。 欲知詳情，請參閱[服務匯流排定價][sbpricing]。

## <a name="hybrid-connection-manager"></a>混合式連線管理員 ##

「混合式連線」功能需要在裝載「混合式連線」端點的網路中有轉送代理程式。 該轉送代理程式稱為混合式連線管理員 (HCM)。 若要下載 HCM，請在 [Azure 入口網站][portal] 中，從您的應用程式選取 [網路] > [設定您的混合式連接端點]。  

此工具可在 Windows Server 2012 和更新版本上執行。 安裝時，HCM 會根據所設定的端點，以連線到「服務匯流排轉送」的服務形式執行。 來自 HCM 的連線會透過連接埠 443 輸出到 Azure。    

在安裝 HCM 之後，您可以執行 HybridConnectionManagerUi.exe 來使用工具的 UI。 此檔案位於混合式連線管理員的安裝目錄下。 在 Windows 10 中，您也可以在搜尋方塊中搜尋「混合式連線管理員 UI」即可。  

![混合式連線管理員的螢幕擷取畫面][7]

啟動 HCM UI 時，您會先看到一個表格，當中會列出與這個 HCM 執行個體搭配設定的所有「混合式連線」。 如果您想要進行任何變更，請先向 Azure 進行驗證。 

若要在 HCM 中新增一或多個混合式連線︰

1. 啟動 HCM UI。
1. 選取 [設定另一個混合式連線]。
![設定新的混合式連線螢幕擷取畫面][8]

1. 使用您的 Azure 帳戶進行登入。
1. 選擇訂用帳戶。
1. 選取您要讓 HCM 轉送的「混合式連線」。
![混合式連線的螢幕擷取畫面][9]

1. 選取 [ **儲存**]。

現在可以看到您新增的「混合式連線」。 您也可以選取已設定的混合式連線，以查看詳細資料。

![混合式連線詳細資料的螢幕擷取畫面][10]

若要讓 HCM 能夠支援所設定與其搭配的「混合式連線」，它需要︰

- 對 Azure 的 TCP 存取權 (透過連接埠 80 和 443)。
- 對「混合式連線」端點的 TCP 存取權。
- 能夠對端點主機和「服務匯流排」命名空間執行 DNS 查閱。

HCM 同時支援「混合式連線」和「BizTalk 混合式連線」。

> [!NOTE]
> 「Azure 轉送」需倚賴「Web 通訊端」來取得連線能力。 此功能只有在 Windows Server 2012 或更新版本上才有提供。 因此，Windows Server 2012 以前的所有版本皆不支援 HCM。
>

### <a name="redundancy"></a>備援性 ###

每個 HCM 都可以支援多個「混合式連線」。 此外，任何指定的「混合式連線」也都可以受到多個 HCM 支援。 預設行為是在任何給定端點所設定的 HCM 之間路由傳送流量。 如果您想要讓來自您網路的「混合式連線」具有高可用性，請在不同電腦上執行多個 HCM。 

### <a name="manually-add-a-hybrid-connection"></a>手動新增混合式連線 ###

若要想讓訂用帳戶外的人員裝載指定「混合式連線」的 HCM 執行個體，您可以與他們共用「混合式連線」的閘道連接字串。 您可以在 [Azure 入口網站][portal]中，於「混合式連線」的屬性中看到此字串。 若要使用該字串，請在 HCM 中選取 [手動輸入]，然後貼上閘道連接字串。


## <a name="troubleshooting"></a>疑難排解 ##

「已連線」狀態意謂著該「混合式連線」至少有一個已設定的 HCM，並且能夠連線至 Azure。 如果「混合式連線」的狀態並未顯示「已連線」，則表示在所有可存取 Azure 的 HCM 上皆未設定該「混合式連線」。

用戶端無法連線至其端點的主要原因是，端點在指定時所使用的是 IP 位址而非 DNS 名稱。 如果您的應用程式無法連線到所要的端點，且您使用的是 IP 位址，請改為使用對 HCM 執行所在之主機有效的 DNS 名稱。 也請檢查 HCM 執行所在的主機已正確解析 DNS 名稱。 請確認 HCM 執行所在的主機可連線到「混合式連線」端點。  

App Service 中的 tcpping 工具，可從 [進階工具 (Kudu)] 主控台中叫用。 這個工具可以指出您是否能夠存取 TCP 端點，但不會指出您是否能夠存取「混合式連線」端點。 當您在主控台中對「混合式連線」端點使用此工具時，您只能確認該端點使用「主機:連接埠」組合。  

## <a name="biztalk-hybrid-connections"></a>BizTalk 混合式連線 ##

舊式「BizTalk 混合式連線」功能已關閉，以利發展新式「BizTalk 混合式連線」。 您可以繼續搭配應用程式使用現有的「BizTalk 混合式連線」，但應該將其移轉成使用「Azure 轉送」的新式「混合式連線」。 相較於 BizTalk 版本，新服務的好處包括︰

- 不需要額外的 BizTalk 帳戶。
- TLS 已從 1.0 版改為 1.2 版。
- 通訊是使用 DNS 名稱透過連接埠 80 和 443 來連線到 Azure，而非使用 IP 位址和其他連接埠範圍。  

若要在您的應用程式中新增現有的「BizTalk 混合式連線」，請在 [Azure 入口網站][portal] 中移至您的應用程式，然後 [網路] > [設定您的混合式連接端點]。 在 [傳統混合式連線] 表格中，按一下 [新增傳統混合式連線]。 接著您可以看到「BizTalk 混合式連線」的清單。  


<!--Image references-->
[1]: ./media/app-service-hybrid-connections/hybridconn-connectiondiagram.png
[2]: ./media/app-service-hybrid-connections/hybridconn-portal.png
[3]: ./media/app-service-hybrid-connections/hybridconn-addhc.png
[4]: ./media/app-service-hybrid-connections/hybridconn-createhc.png
[5]: ./media/app-service-hybrid-connections/hybridconn-properties.png
[6]: ./media/app-service-hybrid-connections/hybridconn-aspproperties.png
[7]: ./media/app-service-hybrid-connections/hybridconn-hcm.png
[8]: ./media/app-service-hybrid-connections/hybridconn-hcmadd.png
[9]: ./media/app-service-hybrid-connections/hybridconn-hcmadded.png
[10]: ./media/app-service-hybrid-connections/hybridconn-hcmdetails.png

<!--Links-->
[HCService]: http://docs.microsoft.com/azure/service-bus-relay/relay-hybrid-connections-protocol/
[portal]: http://portal.azure.com/
[oldhc]: http://docs.microsoft.com/azure/biztalk-services/integration-hybrid-connection-overview/
[sbpricing]: http://azure.microsoft.com/pricing/details/service-bus/
