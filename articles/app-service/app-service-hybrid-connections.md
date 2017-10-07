---
title: "aaa\"Azure App Service 混合式連線 |Microsoft 文件 」"
description: "如何在不同的網路中的 toocreate 和使用混合式連線 tooaccess 資源"
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
ms.date: 04/22/2017
ms.author: ccompy
ms.openlocfilehash: 61d58068ab0a7c803019e3f0e92bde4273d1a053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-hybrid-connections"></a>Azure App Service 混合式連線 #

## <a name="overview"></a>概觀 ##

混合式連線是 Azure 中的服務以及 hello Azure App Service 中的功能。  為服務，它有使用和之外，可利用 hello Azure App Service 中的功能。  深入了解混合式連線和外部 hello Azure 應用程式服務，您可以從這裡開始，其用法 toolearn [Azure 轉送混合式連線][HCService]

Hello Azure 應用程式服務，在混合式連線可以使用的 tooaccess 應用程式的其他網路資源。 它可從您的應用程式 tooan 應用程式端點的存取。  不會啟用其他功能 tooaccess 您的應用程式。  使用 hello App Service 中，每個混合式連接相互關聯 tooa 單一 TCP 主機和連接埠組合。  這表示該 hello 混合式連接端點可以在任何作業系統和任何應用程式提供到達 TCP 接聽連接埠。 混合式連線不知道或在意 hello 應用程式的通訊協定時，或是您要存取。  它只負責提供網路存取。  


## <a name="how-it-works"></a>運作方式 ##
hello 混合式連線 」 功能是由兩個輸出呼叫 tooService 匯流排轉送所組成。  沒有來自其中 hello app service 中執行您的應用程式，而且沒有從 hello 混合式連線 Manager(HCM) tooService 匯流排轉送連線 hello 主機上的程式庫的連接。  hello HCM 是您部署內 hello 網路裝載的轉送服務 

Hello 透過兩個聯結的連接，應用程式有 TCP 通道 tooa 固定的主機： 連接埠組合上 hello hello HCM 另一端。  hello 連接使用 TLS 1.2 安全性與驗證/授權的 SAS 金鑰。    

![][1]

當您的應用程式發出 DNS 要求符合設定混合式連接端點，然後 hello 輸出 TCP 流量會被重新導向向 hello 混合式連接。  

> [!NOTE]
> 這表示您應該嘗試 tooalways 使用混合式連接的 DNS 名稱。  某些用戶端軟體不會進行 DNS 查閱 hello 端點改為使用 IP 位址。
>
>

有兩種類型的混合式連線，hello 新混合式連線會提供給當作 Azure 轉送服務，hello 舊版 BizTalk 混合式連線。  hello 舊版 BizTalk 混合式連線會在 hello 入口網站的參照的 tooas 傳統的混合式連線。  本文稍後會提供這種連線的詳細資訊。

### <a name="app-service-hybrid-connection-benefits"></a>App Service 混合式連線的好處 ###

有許多優點 toohello 混合式連線功能，其中包括

- 應用程式可以安全地存取內部部署系統和服務
- hello 功能不需要網際網路存取端點
- 它是快速和輕鬆 tooset 向上  
- 每個混合式連接符合 tooa 單一主機： 連接埠組合，它會是很好的安全性層面
- 它通常不需要防火牆漏洞 hello 連線是透過標準的 web 連接埠所有輸出
- 因為 hello 功能也表示它是由您的應用程式與 hello 技術 hello 端點所使用的無從驗證 toohello 語言的網路層級
- 它可以從單一應用程式的多個網路中使用 tooprovide 存取 

### <a name="things-you-cannot-do-with-hybrid-connections"></a>混合式連線無法執行的作業 ###

您無法透過混合式連線來執行的一些作業如下：

- 掛接磁碟機
- 使用 UDP
- 存取使用動態連接埠的 TCP 型服務 (例如，FTP 被動模式或延伸被動模式)
- LDAP 支援，因為它有時需要 UDP
- Active Directory 支援

## <a name="adding-and-creating-a-hybrid-connection-in-your-app"></a>在應用程式中新增和建立混合式連線 ##

您可以建立混合式連線，透過 hello 應用程式入口網站或從 hello 混合式連接服務入口網站。  強烈建議您先使用 hello 應用程式入口網站 toocreate hello 想 toouse 與您的應用程式的混合式連線。  toocreate 混合式連接到 toohello [Azure 入口網站][ portal]而進入 hello UI 應用程式。  選取 [網路] > [設定混合式連線端點]。  從這裡您可以看到與您的應用程式設定的 hello 混合式連線  

![][2]

tooadd 新的混合式連接，按一下 新增混合式連接。  hello UI 開啟列出您已建立的 hello 混合式連線。  一或多個這些 tooadd tooyour 應用程式中，按一下 hello 的並叫用**新增選取的混合式連接**。  

![][3]

如果您想 toocreate 新的混合式連接，請按一下**建立新的混合式連接**。  您可以在這裡指定： 

- 端點名稱
- 端點主機名稱
- 端點連接埠
- 您想 toouse 服務匯流排命名空間

![][4]

每個混合式連接繫結的 tooa 服務匯流排命名空間且每個服務匯流排命名空間中的 Azure 區域。  請務必 tootry 和使用服務匯流排命名空間中的 hello 與您的應用程式相同的區域，以 tooavoid 引起的網路延遲。

如果您想 tooremove 混合式連線從您的應用程式，以滑鼠右鍵按一下它，然後選取**中斷連線**。  

一旦混合式連線新增 tooyour web 應用程式，您可以在其上查看詳細資料，只需按一下項目。  

![][5]

## <a name="hybrid-connections-and-app-service-plans"></a>混合式連線和 App Service 方案 ##

現在您可以做出 hello 唯一的混合式連線會 hello 新混合式連線。  基本、標準、進階和隔離的定價 SKU 才能使用混合式連線。  有繫結限制 toohello 定價計劃。  

| 定價方案 | Hello 計劃中可用的混合式連線的數目 |
|----|----|
| 基本 | 5 |
| 標準 | 25 |
| 進階 | 200 |
| 隔離 | 200 |

因為有 App Service 方案的限制，另外還有 UI hello App Service 方案，其中顯示您正在使用多少的混合式連線中以及哪些應用程式。  

![][6]

就像 hello 應用程式檢視，您可以看到詳細資料上混合式連接上它即可。  您可以看到您在 hello 應用程式檢視所有 hello 資訊，但也可以都查看在 hello 多少其他應用程式如下所示的 hello 屬性相同應用程式服務方案正在使用該混合式連接。

![][7]

Hello 可以用於應用程式服務方案的混合式連接端點數目上限時，可以使用每個混合式連線，跨任意數目的 App Service 方案中的應用程式。  這是 toosay 如果選項 1 我 5 不同的應用程式中使用我的應用程式服務計劃中的混合式連接的是 1 還是混合式連接。

沒有額外的成本 toohybrid 連線正在只可用於 Basic、 Standard、 Premium 或隔離的 SKU。  如需混合式連線定價的詳細資訊，請前往這裡︰[服務匯流排定價][sbpricing]。

## <a name="hybrid-connection-manager"></a>混合式連線管理員 ##

為了讓混合式連線 toowork 必須裝載您的混合式連接端點的 hello 網路中的轉送代理程式。  該轉送代理程式稱為 hello 混合式連線管理員 (HCM)。  此工具可以下載從 hello**網路 > 設定您的混合式連接端點**UI 可從您的應用程式在 hello [Azure 入口網站][portal]。  

此工具會在 Windows Server 2008 R2 和更新版本的 Windows 上執行。  安裝完成後 hello HCM 執行為服務。  此服務會連接 tooAzure hello 設定端點為基礎的服務匯流排轉送。  從 hello HCM hello 連線是輸出 tooports 80 和 443。    

hello HCM 具有 UI tooconfigure 它。  Hello HCM 安裝之後您可以藉由執行 hello HybridConnectionManagerUi.exe 位於 hello 混合式連線管理員的安裝目錄中叫出 hello UI。  在 Windows 10 上，您也可以在搜尋方塊中輸入「混合式連線管理員 UI」來輕鬆取得該 UI。  

Hello HCM UI 啟動時，首先 hello 您，請參閱時列出的所有設定與這個執行個體的 hello HCM hello 混合式連接的資料表。  如果您想 toomake 您必須使用 Azure tooauthenticate 任何變更。 

tooadd 其中一個或多個混合式連線 tooyour HCM:

1. 啟動 hello HCM UI
1. 按一下 [設定另一個混合式連線] ![][8]

1. 使用 Azure 帳戶進行登入
1. 選擇訂用帳戶
1. 按一下您要此 HCM toorelay hello 混合式連線![][9]

1. 按一下 [Save] \(儲存)。

此時，您會看到您加入的 hello 混合式連線。  您也可以按一下 hello 設定混合式連接，然後查看 hello 連線詳細資料。

![][10]

HCM toobe 無法 toosupport hello 混合式連線的設定，它需要：

- 透過連接埠 80 和 443 TCP 存取 tooAzure
- TCP 存取 toohello 混合式連接端點
- 能力 toodo DNS 查詢 ups hello 端點上的裝載和 hello azure 服務匯流排命名空間

hello HCM 支援新的混合式連線以及 hello 舊版 BizTalk 混合式連線。

### <a name="redundancy"></a>備援性 ###

每個 HCM 都可以支援多個混合式連線。  此外，任何給定的混合式連線也可由多個 HCM 來支援。  hello 預設行為是 tooround 循環配置資源流量，跨 hello HCMs 針對任何指定的端點。  如果您想讓網路的混合式連線具有高可用性，只需在不同機器上具現化多個 HCM。 

### <a name="manually-adding-a-hybrid-connection"></a>手動新增混合式連線 ###

如果您想有人之外訂用帳戶 toohost HCM 給定的混合式連接的執行個體，您可以在與他們共用 hello hello 混合式連接的閘道連接字串。  您可以在混合式連線在 hello hello 屬性看到[Azure 入口網站][portal]。 字串，toouse 按一下 hello**手動設定**hello HCM 按鈕，並貼上 hello 閘道連接字串中。


## <a name="troubleshooting"></a>疑難排解 ##

當您混合式連接以執行應用程式設定並沒有至少一個已設定，該混合式連接的 HCM 然後 hello 狀態會顯示**Connected** hello 入口網站中。  如果不是顯示**Connected**則表示可能是您的應用程式已關閉，或是您 HCM 無法 out tooAzure 連接埠 80 或 443 連線。  

用戶端無法連線 tootheir 端點的 hello 主要原因是因為 hello 端點指定使用的 IP 位址，而不 DNS 名稱。  如果您的應用程式無法連線到所需的 hello 端點使用的 IP 位址，切換 toousing hello hello HCM 執行所在的主機有效的 DNS 名稱。  其他事項 toocheck 是該 hello DNS 名稱正確解析其中 hello HCM 正在執行，而且沒有從 hello 執行的主控件 hello HCM toohello 混合式連接端點連線的 hello 主機上。  

Hello 可以叫用呼叫 tcpping hello 主控台從應用程式服務中沒有一項工具。  此工具可以告訴您，是否您具有存取 tooa TCP 端點，但不會告訴您是否您有存取 tooa 混合式連接端點。  針對混合式連接端點的 hello 主控台中使用時，成功 ping 會只告訴您有混合式連線為使用該主機： port 組合的應用程式設定。  

## <a name="biztalk-hybrid-connections"></a>BizTalk 混合式連線 ##

關閉 toofurther BizTalk 混合式連接建立 hello 舊版 BizTalk 混合式連線功能已關閉。  您可以繼續使用您預先存在的 BizTalk 混合式連線您的應用程式，但應該移轉 toohello 新的服務。  Hello hello hello BizTalk 版本透過新的服務中的優點包括：

- 不需要其他 BizTalk 帳戶
- TLS 是 1.2，而非 BizTalk 混合式連線所使用的 1.0
- 通訊是透過連接埠 80 和 443 使用 DNS 名稱 tooreach Azure 而不是 IP 位址和其他各種其他連接埠。  

tooadd BizTalk 混合式連線 tooyour 應用程式，應用程式移 tooyour hello [Azure 入口網站][ portal]按一下**網路 > 設定您的混合式連接端點**。  Hello 傳統混合式連接的資料表中按一下**加入傳統的混合式連接**。  您可以在這裡看到 BizTalk 混合式連線的清單。  


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

