---
title: "aaaInstall 在內部部署資料閘道 Azure 邏輯應用程式 |Microsoft 文件"
description: "您存取在內部部署資料來源之前，安裝 hello 在內部部署資料閘道進行快速的資料傳輸和在內部部署資料來源與邏輯應用程式之間的加密"
keywords: "存取資料, 內部部署, 資料傳輸, 加密, 資料來源"
services: logic-apps
documentationcenter: 
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 47e3024e-88a0-4017-8484-8f392faec89d
ms.service: logic-apps
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/13/2017
ms.author: LADocs; dimazaid; estfan
ms.openlocfilehash: 01386a904d856ff545f2eca8eb1b008dcdc08574
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-on-premises-data-gateway-for-azure-logic-apps"></a>Azure 邏輯應用程式安裝 hello 在內部部署資料閘道

您的 logic apps 可以存取在內部部署資料來源之前，您必須安裝並設定 hello 在內部部署資料閘道。 hello 閘道作為橋接器，提供快速的資料傳輸和內部部署系統與應用程式邏輯之間的加密。 hello 閘道轉送上 hello Azure Service Bus 透過加密通道在內部部署來源的資料。 所有流量都來自為 hello 閘道代理程式的安全輸出流量。 深入了解[hello 資料閘道的運作方式](#gateway-cloud-service)。

hello 閘道支援連線 toothese 資料來源，在內部部署：

*   BizTalk Server 2016
*   DB2  
*   檔案系統
*   Informix
*   MQ
*   MySQL
*   Oracle 資料庫
*   PostgreSQL
*   SAP 應用程式伺服器 
*   SAP 訊息伺服器
*   SharePoint
*   SQL Server
*   Teradata

這些步驟顯示如何 toofirst 安裝 hello 內部部署資料閘道，才能[hello 閘道和您的 logic apps 之間的連接設定](./logic-apps-gateway-connection.md)。 如需所支援連接器的詳細資訊，請參閱 [Azure Logic Apps 的連接器](https://docs.microsoft.com/azure/connectors/apis-list)。 

如需如何 toouse hello 閘道與其他服務資訊，請參閱下列文章：

*   [Microsoft Power BI 內部部署資料閘道](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [Azure Analysis Services 內部部署資料閘道](../analysis-services/analysis-services-gateway.md)
*   [Microsoft Flow 內部部署資料閘道](https://flow.microsoft.com/documentation/gateway-manage/)
*   [Microsoft PowerApps 內部部署資料閘道](https://powerapps.microsoft.com/tutorials/gateway-management/)

<a name="requirements"></a>
## <a name="requirements"></a>需求

**最低**：

* .NET 4.5 Framework
* 64 位元版本的 Windows 7 或 Windows Server 2008 R2 (或更新版本)

**建議**：

* 8 核心 CPU
* 8 GB 記憶體
* 64 位元版本的 Windows 2012 R2 (或更新版本)

**重要考量**︰

* 只能在本機電腦上安裝 hello 在內部部署資料閘道。
您無法在網域控制站上安裝 hello 閘道。

   > [!TIP]
   > 您沒有在 hello tooinstall hello 閘道做為資料來源的同一部電腦。 toominimize 延遲，您可以安裝接近以可能 tooyour 資料來源，或在 hello 上相同的 hello 閘道電腦，假設您有權限。

* 請勿關閉、 toosleep，或並不會因為 hello 閘道器無法在這些情況下執行時連接 toohello 網際網路的電腦上安裝 hello 閘道。 此外，透過無線網路的閘道效能可能會受到影響。

* 在安裝期間，您必須登入[公司或學校帳戶](https://docs.microsoft.com/azure/active-directory/sign-up-organization)，該帳戶是由 Azure Active Directory (Azure AD) 所管理，而非 Microsoft 帳戶。 

  您有 toouse hello 相同的工作或學校帳戶稍後在 hello Azure 入口網站，當您建立並關聯閘道安裝閘道資源。 當您建立 hello 連線之間邏輯應用程式與 hello 在內部部署資料來源，然後選取此閘道資源。 [為何必須使用公司或學校的 Azure AD 帳戶？](#why-azure-work-school-account)

  > [!TIP]
  > 如果您註冊 Office 365 供應項目，但是未提供實際的公司電子郵件，您的登入位址看起來可能會像 jeff@contoso.onmicrosoft.com。 

* 如果您有現有的閘道設定與之前版本 14.16.6317.4 的安裝程式，您無法變更您的閘道執行 hello 最新的安裝程式的位置。 不過，您可以使用 hello 最新安裝程式 tooset 註冊新的閘道與 hello 改為您想要的位置。
  
  如果您有閘道安裝程式之前版本 14.16.6317.4，但您尚未安裝您的閘道，您可以下載並使用 hello 最新的安裝程式。

<a name="install-gateway"></a>

## <a name="install-hello-data-gateway"></a>安裝 hello 部署資料閘道

1.  [下載並在本機電腦上執行 hello 閘道安裝程式](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409)。

2. 檢閱並接受 hello 使用條款和隱私權聲明。

3. 指定您想要 tooinstall hello 閘道在本機電腦上的 hello 路徑。

4. 在系統提示時，使用公司或學校的 Azure 帳戶而非 Microsoft 帳戶來登入。

   ![使用 Azure 公司或學校帳戶登入](./media/logic-apps-gateway-install/sign-in-gateway-install.png)

5. 現在您已安裝的閘道註冊 hello[閘道器雲端服務](#gateway-cloud-service)。 選擇**在這部電腦上註冊新的閘道**。

   hello 閘道器雲端服務會加密，並將您的資料來源認證和閘道器詳細資料。 
   hello 服務也會將查詢和它們的結果，應用程式邏輯、 hello 在內部部署資料閘道和您的資料來源之間路由在內部部署。

6. 為閘道安裝提供名稱。 建立復原金鑰，然後確認復原金鑰。 

   > [!IMPORTANT] 
   > 修復金鑰必須至少包含 8 個字元。 請確定您儲存，並將 hello 金鑰保存在安全的地方。 您也需要此金鑰，當您想 toomigrate，還原或取代現有的閘道。

   1. hello 閘道器雲端服務和您的閘道安裝所使用的 Azure 服務匯流排 toochange hello 預設區域選擇**變更區域**。

      ![變更區域](./media/logic-apps-gateway-install/change-region-gateway-install.png)

      hello 預設區域是與 Azure AD 租用戶相關聯的 hello 區域。

   2. 在 hello 下一步] 窗格中，開啟 [hello**選取地區**太選擇不同的區域。

      ![選取其他區域](./media/logic-apps-gateway-install/select-region-gateway-install.png)

      例如，您可能會選取 hello 與應用程式邏輯，相同的區域，或選取 hello 區域最接近 tooyour 在內部部署資料來源，以便您可以減少延遲。 閘道資源和邏輯應用程式可位於不同位置。

      > [!IMPORTANT]
      > 安裝完成後就無法變更此區域。 這個區域也會決定，並限制 hello 位置，您可以在其中建立閘道 hello Azure 資源。 因此當您在 Azure 中建立閘道資源，請確定 hello 資源位置符合您在閘道安裝期間選取的 hello 區域。
      > 
      > 如果您想 toouse 不同的區域閘道之後，您必須設定新的閘道。

   3. 準備就緒時，請選擇 [完成]。

7. 現在遵循 hello Azure 入口網站中的這些步驟，這樣您就可以[建立閘道的 Azure 資源](../logic-apps/logic-apps-gateway-connection.md)。 

深入了解[hello 資料閘道的運作方式](#gateway-cloud-service)。

## <a name="migrate-restore-or-take-over-an-existing-gateway"></a>移轉、還原或取代現有閘道

tooperform 這些工作，您必須擁有 hello hello 閘道已安裝時所指定的修復金鑰。

1. 在電腦的 [開始] 功能表中，選擇 [內部部署資料閘道]。

2. Hello 安裝程式隨即開啟，來登入之後 hello 相同 Azure 工作或學校帳戶，先前已使用 tooinstall hello 閘道。

3. 選擇**移轉、還原或取代現有閘道**。

4. 提供您想透過 toomigrate、 還原或接受的 hello 閘道的 hello 名稱及修復金鑰。

<a name="restart-gateway"></a>
## <a name="restart-hello-gateway"></a>重新啟動 hello 閘道

hello 閘道會當做 Windows 服務來執行。 與其他任何 Windows 服務，您可以啟動和停止 hello 服務有多個。 比方說，您可以 hello hello 閘道執行所在的電腦上提高權限開啟命令提示字元並執行下列任一命令：

* toostop hello 服務，執行下列命令：
  
    `net stop PBIEgwService`

* toostart hello 服務，執行下列命令：
  
    `net start PBIEgwService`

### <a name="windows-service-account"></a>Windows 服務帳戶

hello 在內部部署資料閘道設定 toouse `NT SERVICE\PBIEgwService` hello windows 服務的登入認證。 根據預設，hello 閘道具有 hello hello 機器的 「 以服務方式登入 」 權限 hello 閘道的安裝位置。

> [!NOTE]
> hello Windows 服務帳戶與從 hello 帳戶用來連線 tooon 內部部署資料來源，以及從 hello Azure 工作或學校帳戶用於 toosign toocloud 服務中。

## <a name="configure-a-firewall-or-proxy"></a>設定防火牆或 Proxy

hello 閘道建立輸出連線太[Azure 服務匯流排](https://azure.microsoft.com/services/service-bus/)。 您的閘道的 tooprovide proxy 資訊，請參閱[設定 proxy 設定](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/)。

toocheck 是否您防火牆或 proxy 時，可能會封鎖連線，確認您的電腦是否可以實際連線 toohello 網際網路和 hello [Azure 服務匯流排](https://azure.microsoft.com/services/service-bus/)。 從 PowerShell 命令提示字元中，執行此命令︰

`Test-NetConnection -ComputerName watchdog.servicebus.windows.net -Port 9350`

> [!NOTE]
> 此命令只會測試網路連線和連線 toohello Azure 服務匯流排。 因此 hello 命令不會動用 toodo hello 閘道或 hello 閘道器雲端服務加密並儲存您的認證和閘道器詳細資料。 
>
> 此外，這個命令僅適用於 Windows Server 2012 R2 或更新版本，以及 Windows 8.1 或更新版本。 在舊的 OS 版本中，您可以使用 Telnet 太測試連線。 深入了解 [Azure 服務匯流排和混合式解決方案](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)。

您的結果應該看起來類似 toothis 範例：

```text
ComputerName           : watchdog.servicebus.windows.net
RemoteAddress          : 70.37.104.240
RemotePort             : 5672
InterfaceAlias         : vEthernet (Broadcom NetXtreme Gigabit Ethernet - Virtual Switch)
SourceAddress          : 10.120.60.105
PingSucceeded          : False
PingReplyDetails (RTT) : 0 ms
TcpTestSucceeded       : True
```

如果**TcpTestSucceeded**未設定太**True**，您可能會被防火牆封鎖。 如果您想 toobe 完整，以取代 hello **ComputerName**和**連接埠**底下所列的值與 hello 值[設定連接埠](#configure-ports)本主題中。

hello 防火牆也可能會封鎖連接該 hello Azure 服務匯流排可讓 toohello Azure 資料中心。 如果發生這種情況下，請核准 （解除封鎖） 所有 hello 這些資料中心區域中的 IP 位址。 為 IP 位址， [get hello Azure IP 位址清單這裡](https://www.microsoft.com/download/details.aspx?id=41653)。

## <a name="configure-ports"></a>設定連接埠

hello 閘道建立輸出連線太[Azure 服務匯流排](https://azure.microsoft.com/services/service-bus/)並在輸出連接埠與通訊： TCP 443 （預設）、 5671、 5672、 9350 到 9354。 hello 閘道不需要輸入連接埠。 深入了解 [Azure 服務匯流排和混合式解決方案](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)。

| 網域名稱 | 輸出連接埠 | 描述 |
| --- | --- | --- |
| *.analysis.windows.net | 443 | HTTPS | 
| *.login.windows.net | 443 | HTTPS | 
| *.servicebus.windows.net | 5671-5672 | 進階訊息佇列通訊協定 (AMQP) | 
| *.servicebus.windows.net | 443、9350-9354 | 透過 TCP 之服務匯流排轉送上的接聽程式 (需要 443 才能取得「存取控制」權杖) | 
| *.frontend.clouddatahub.net | 443 | HTTPS | 
| *.core.windows.net | 443 | HTTPS | 
| login.microsoftonline.com | 443 | HTTPS | 
| *.msftncsi.com | 443 | 無法連到 hello Power BI 服務的 hello 閘道時，請使用 tootest 網際網路連線。 | 

如果您有 tooapprove IP 位址而非 hello 定義域時，您可以下載並使用 hello [Microsoft Azure Datacenter IP 範圍清單](https://www.microsoft.com/download/details.aspx?id=41653)。 在某些情況下，hello Azure 服務匯流排連線的 IP 位址，而不是完整的網域名稱。

<a name="gateway-cloud-service"></a>
## <a name="how-does-hello-data-gateway-work"></a>Hello 資料閘道的運作方式為何？

hello 資料閘道，協助應用程式邏輯、 hello 閘道器雲端服務和內部部署資料來源之間快速且安全的通訊。 

![diagram-for-on-premises-data-gateway-flow](./media/logic-apps-gateway-install/how-on-premises-data-gateway-works-flow-diagram.png)

因此 hello 雲端中的 hello 使用者互動的項目，已連線 tooyour 內部部署資料來源：

1. hello 閘道器雲端服務建立查詢，以及加密 hello 認證 hello 資料來源，並傳送嗨閘道 tooprocess hello 查詢 toohello 佇列。

2. hello 閘道器雲端服務會分析 hello 查詢，並將推送 hello 要求 toohello Azure 服務匯流排。

3. hello 在內部部署資料閘道會輪詢 hello 適用於 Azure 服務匯流排擱置的要求。

4. hello 閘道取得 hello 查詢、 解密 hello 認證，並利用這些認證連接 toohello 資料來源。

5. hello 閘道會傳送 hello 查詢 toohello 資料來源執行。

6. hello 結果會傳送 hello 資料來源、 回復 toohello 閘道和 toohello 閘道器雲端服務。 hello 閘道器雲端服務接著會使用 hello 結果。

<a name="faq"></a>
## <a name="frequently-asked-questions"></a>常見問題集

### <a name="general"></a>一般

**問：**： 我需要閘道 hello 雲端，例如 SQL Azure 中的資料來源嗎？ <br/>
**答**：否。 閘道正在連接只 tooon 內部部署資料來源。

**問：**: hello 閘道是否有 toobe hello 做 hello 資料來源相同電腦上安裝？ <br/>
**答**：否。 hello 閘道正在連接 toohello 資料來源使用所提供的 hello 連接資訊。 Hello 閘道視為用戶端應用程式，這方面。 hello 閘道只需要 hello 功能 tooconnect toohello 伺服器所提供名稱。

<a name="why-azure-work-school-account"></a>

**問：**： 為什麼必須使用 Azure 的工作或學校帳戶 toosign 中的？ <br/>
**A**： 您只能使用 Azure 的工作或學校帳戶，當您安裝 hello 在內部部署資料閘道。 登入帳戶會儲存在由 Azure Active Directory (Azure AD) 所管理的租用戶中。 通常，您的 Azure AD 帳戶的使用者主要名稱 (UPN) 符合 hello 電子郵件地址。

**問**︰我的認證儲存在哪裡？ <br/>
**A**： 您輸入的資料來源的 hello 認證會加密並儲存在 hello 閘道器雲端服務。 hello 認證會在 hello 在內部部署資料閘道進行解密。

**問**︰網路頻寬是否有任何需求？ <br/>
**答**︰我們的建議是，您的網路連線要有良好的輸送量。 每個環境都不同，並傳送資料的 hello 數量會影響 hello 的結果。 使用 ExpressRoute 有利於 tooguarantee 的內部部署與 hello Azure 資料中心之間的輸送量層級。
您可以使用您的輸送量 hello 協力廠商工具 Azure Speed Test 應用程式 toohelp 量測計。

**問：**: hello 延遲執行查詢 tooa 資料來源，從 hello 閘道是什麼？ Hello 最佳架構為何？ <br/>
**A**: tooreduce 網路延遲，安裝 hello 閘道為盡可能關閉 toohello 資料來源。 您可以安裝 hello 閘道 hello 實際的資料來源上，如果此相近延遲降至最低 hello 導入。 太考慮 hello 資料中心。 例如，如果您的服務會使用 hello 美國西部的資料中心，而且您的 Azure VM 中裝載 SQL Server，Azure VM 應該在 hello 美國西部太。 此接近延遲降至最低，並避免 hello Azure VM 的輸出流量費用。

**問：**： 的結果傳送後 toohello 雲端方式？ <br/>
**A**: hello Azure Service Bus 透過傳送結果。

**問：**： 是否有任何輸入的連線 toohello 閘道在 hello 雲端？ <br/>
**答**：否。 hello 閘道會使用輸出連線 tooAzure Service Bus。

**問**︰如果我封鎖輸出連線會如何？ 怎麼我需要 tooopen？ <br/>
**A**: hello 連接埠和主控件以 hello 閘道使用，請參閱。

**問：**: hello 實際的 Windows 服務稱為？<br/>
**A**: hello 閘道呼叫 Power BI Enterprise Gateway 服務在 [服務]。

**問：**： 可以 hello 使用 Azure Active Directory 帳戶來執行閘道 Windows 服務嗎？ <br/>
**答**：否。 hello Windows 服務必須有有效的 Windows 帳戶。 根據預設，hello 服務會以 hello 服務 SID NT SERVICE\PBIEgwService 執行。

### <a name="high-availability-and-disaster-recovery"></a>高可用性和災害復原

**問**︰災害復原有哪些選項？ <br/>
**A**： 您可以使用 hello 修復金鑰 toorestore 或移動閘道。 當您安裝 hello 閘道時，指定 hello 修復金鑰。

**問：**: hello hello 修復金鑰的優點為何？ <br/>
**A**: hello 修復金鑰提供方式 toomigrate 或損毀狀況之後復原您的閘道設定。

**問：**： 是否有任何的計劃，以啟用高可用性案例的 hello 閘道？ <br/>
**A**： 這些案例在 hello 藍圖上，但我們尚未時間軸。

## <a name="troubleshooting"></a>疑難排解

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

**問：**： 如何查看哪些查詢會傳送 toohello 在內部部署資料來源嗎？ <br/>
**A**： 您可以啟用查詢追蹤，其中包括傳送嗨查詢。 請記住 toochange 查詢後追蹤 toohello 完成疑難排解後的原始值。 讓查詢追蹤保持開啟會產生較大的記錄。

您也可以查看資料來源具備的工具是否有追蹤查詢。 例如，您可以使用 SQL Server 和 Analysis Services 的擴充事件或 SQL Profiler。

**問：**： 所在 hello 閘道記錄檔？ <br/>
**答**：請參閱本主題稍後的「工具」。

### <a name="update-toohello-latest-version"></a>更新 toohello 最新版本

Hello 閘道器版本過期時，就會出現許多問題。 良好一般做法，請確定您使用 hello 最新版本。 如果您超過一個月或更久沒有更新 hello 閘道，您可能會考慮安裝 hello hello 閘道最新版本，並查看可否重現 hello 問題。

### <a name="error-failed-tooadd-user-toogroup--2147463168-pbiegwservice-performance-log-users"></a>錯誤： 無法 tooadd 使用者 toogroup。 (-2147463168 PBIEgwService Performance Log Users)

如果您嘗試 tooinstall hello 閘道不支援的網域控制站上，您可能會收到這個錯誤。 請確定您部署的 hello 閘道不是網域控制站的電腦上。

## <a name="tools"></a>工具

### <a name="collect-logs-from-hello-gateway-configurer"></a>從 hello 閘道 configurer 收集記錄檔

您可以收集 hello 閘道的數個記錄檔。 一律與 hello 記錄檔開始 ！

#### <a name="installer-logs"></a>安裝程式記錄檔

`%localappdata%\Temp\Power_BI_Gateway_–Enterprise.log`

#### <a name="configuration-logs"></a>組態記錄檔

`%localappdata%\Microsoft\Power BI Enterprise Gateway\GatewayConfigurator.log`

#### <a name="enterprise-gateway-service-logs"></a>企業閘道服務記錄檔

`C:\Users\PBIEgwService\AppData\Local\Microsoft\Power BI Enterprise Gateway\EnterpriseGateway.log`

#### <a name="event-logs"></a>事件記錄檔

您可以找到 hello 下的資料管理閘道器和 PowerBIGateway 記錄**Application and Services Logs**。

### <a name="fiddler-trace"></a>Fiddler 追蹤

[Fiddler](http://www.telerik.com/fiddler) 是一個 Telerik 公司開發，用來監視 HTTP 流量的免費工具。 您可以看到這個流量以 hello hello 用戶端電腦從 Power BI 服務。 此服務可能會顯示錯誤和其他相關資訊。

## <a name="next-steps"></a>後續步驟
    
* [邏輯應用程式從連接 tooon 內部部署資料](../logic-apps/logic-apps-gateway-connection.md)
* [企業整合功能](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [適用於 Azure Logic Apps 的連接器](../connectors/apis-list.md)
