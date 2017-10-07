---
title: "aaaHybrid 連接概觀 |Microsoft 文件"
description: "了解混合式連線、安全性、TCP 連接埠和支援的組態。 MABS，WABS。"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: erikre
editor: 
ms.assetid: 216e4927-6863-46e7-aa7c-77fec575c8a6
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/18/2016
ms.author: ccompy
ms.openlocfilehash: f092c6019aae761e1e73f13d1af8446a896515c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-connections-overview"></a>混合式連線概觀

> [!IMPORTANT]
> BizTalk 混合式連線已停用，並以 App Service 混合式連線取代。 如需詳細資訊，包括如何 toomanage 現有 BizTalk 混合式連線，請參閱[Azure 應用程式服務的混合式連線](../app-service/app-service-hybrid-connections.md)。

簡介 tooHybrid 連線，列出支援 hello 組態，並列出 hello 必要的 TCP 連接埠。

## <a name="what-is-a-hybrid-connection"></a>什麼是混合式連線
混合式連線是 Azure BizTalk 服務的功能。 混合式連線可提供 Azure 應用程式服務 （先前稱為網站） 的簡單、 方便的方式 tooconnect hello Web 應用程式功能和防火牆後方的 Azure 應用程式服務 (先前稱為 Mobile Services) tooon 內部部署資源中的 hello 行動應用程式功能。

![混合式連線][HCImage]

混合式連線的優點包括：

* Web Apps 和 Mobile Apps 可以安全地存取現有的內部部署資料和服務。
* 多個 Web 應用程式或行動應用程式可以共用的混合式連接 tooaccess 在內部部署資源。
* 最小的 TCP 連接埠是必要的 tooaccess 您的網路。
* 使用混合式連接的應用程式存取只 hello 特定的內部部署資源發行透過 hello 混合式連接。
* 可以使用靜態 TCP 連接埠，例如 SQL Server、 MySQL、 HTTP 的 Web Api，以及大部份的自訂 Web 服務的 tooany 在內部部署資源的連接。
  
  > [!NOTE]
  > 目前不支援使用動態連接埠的 TCP 服務 (例如 FTP 被動模式或延伸被動模式)。 也不支援 LDAP。 LDAP 使用靜態 TCP 連接埠，但它也可以使用 UDP。 因此不受支援。
  > 
  > 
* 可以與 Web Apps (.NET、PHP、Java、Python、Node.js) 和 Mobile Apps (Node.js、.NET) 支援的所有架構搭配使用。
* Web 應用程式和行動應用程式可以存取內部資源，完全 hello 中的相同的方式就如同 hello Web 或行動裝置應用程式位於您本機網路上。 例如，hello 相同的連接字串使用內部部署也可用在 Azure。

混合式連線也會提供企業系統管理員控制和可見性 hello 公司資源存取的混合式應用程式，包括：

* 使用 「 群組原則設定，系統管理員可以在 hello 網路上允許混合式連線，並也指定混合式應用程式可以存取的資源。
* Hello 公司網路上的事件和稽核記錄檔提供存取的混合式連線的 hello 資源可視性。

## <a name="example-scenarios"></a>範例案例
混合式連線支援 hello 遵循 framework 和應用程式的組合：

* .NET framework 存取 tooSQL 伺服器
* .NET framework 存取 tooHTTP/HTTPS 服務使用 WebClient
* PHP 存取 tooSQL 伺服器 MySQL
* Java 存取 tooSQL Server、 MySQL 和 Oracle
* Java 存取 tooHTTP/HTTPS 服務

當使用混合式連線 tooaccess 內部部署 SQL Server 時，請考慮下列 hello:

* SQL Express 具名執行個體必須設定的 toouse 靜態連接埠。 依預設，SQL Express 具名執行個體是使用動態連接埠。
* SQL Express 預設執行個體使用靜態連接埠，但必須啟用 TCP。 預設不會啟用 TCP。
* 使用群集或可用性群組時，hello`MultiSubnetFailover=true`模式目前不支援。
* hello`ApplicationIntent=ReadOnly`目前不支援。
* SQL 驗證可能需要為 hello hello Azure 應用程式和 hello 在內部部署 SQL server 所支援的端對端授權方法。

## <a name="security-and-ports"></a>安全性和連接埠
混合式連線會使用共用存取簽章 (SAS) 授權 toosecure hello 連線從 hello Azure 應用程式和 hello 內部部署混合式連線管理員 toohello 混合式連接。 個別連接索引鍵會針對 hello 應用程式和建立 hello 內部部署混合式連線管理員。 這些連線金鑰可以個別地更換和撤銷。

混合式連線提供順暢且安全的分佈的 hello 金鑰 toohello 應用程式，然後 hello 內部部署混合式連線管理員。

請參閱 [建立和管理混合式連線](integration-hybrid-connection-create-manage.md)(英文)。

*應用程式的授權是分開 hello 混合式連接*。 任何適當的授權方法都可使用。 hello 授權方法取決於 hello 端對端授權方法，支援跨 hello Azure 雲端和 hello 內部元件。 例如，您的 Azure 應用程式存取內部部署 SQL Server。 在此案例中，SQL 授權可能會支援的端對端的 hello 授權方法。

#### <a name="tcp-ports"></a>TCP 連接埠
混合式連線只需要您私人網路的輸出 TCP 或 HTTP 連線。 您不需要任何防火牆連接埠 tooopen 或變更您的網路周邊組態 tooallow 任何輸入的連線到您的網路。

混合式連線會使用下列 TCP 連接埠的 hello:

| Port | 您為何需要它 |
| --- | --- |
| 9350 - 9354 |這些連接埠用於資料傳輸。 hello Service Bus 轉送管理員探查連接埠 9350 toodetermine TCP 連線是否可用。 如果可用的話，則會假設連接埠 9352 也是可用。 資料流量會經過連接埠 9352。 <br/><br/>允許輸出連線 toothese 連接埠。 |
| 5671 |使用連接埠則為 9352 時的資料流量而言，hello 控制通道為使用連接埠 5671。 <br/><br/>允許輸出連線 toothis 連接埠。 |
| 80、443 |這些連接埠會用於某些資料要求 tooAzure。 也，則不會使用連接埠則為 9352 和 5671*然後*的連接埠 80 和 443 會 hello 後援用於資料傳輸和 hello 控制通道。<br/><br/>允許輸出連線 toothese 連接埠。 <br/><br/>**請注意**不建議 toouse 這些因為 hello hello 取代後援連接埠的其他 TCP 通訊埠。 hello HTTP/WebSocket 作為 hello 通訊協定，而不是原生 TCP 資料通道。 這可能會導致效能變低。 |

## <a name="next-steps"></a>後續步驟
[Create and manage Hybrid Connections](integration-hybrid-connection-create-manage.md)<br/>
[連接 Azure Web Apps tooan 在內部部署資源](../app-service-web/web-sites-hybrid-connection-get-started.md)<br/>
[從 Azure web 應用程式連接 tooon 內部部署 SQL Server](../app-service-web/web-sites-hybrid-connection-connect-on-premises-sql-server.md)<br/>

## <a name="see-also"></a>另請參閱
[用於管理 Microsoft Azure 上之 BizTalk 服務的 REST API](http://msdn.microsoft.com/library/azure/dn232347.aspx)
[BizTalk 服務：版本圖表](biztalk-editions-feature-chart.md)<br/>
[使用 Azure 入口網站建立 BizTalk 服務](biztalk-provision-services.md)<br/>
[BizTalk 服務：儀表板、監視和調整索引標籤](biztalk-dashboard-monitor-scale-tabs.md)<br/>

[HCImage]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionImage.png
[HybridConnectionTab]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionTab.png
[HCOnPremSetup]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionOnPremSetup.png
[HCManageConnection]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionManageConn.png
