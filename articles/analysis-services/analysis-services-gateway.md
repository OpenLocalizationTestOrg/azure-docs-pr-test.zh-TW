---
title: "aaaOn 內部部署資料閘道 |Microsoft 文件"
description: "如果您在 Azure 中的 Analysis Services 伺服器將連線 tooon 內部部署資料來源，必須在內部部署閘道。"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: cd596155-b608-4a34-935e-e45c95d884a9
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/21/2017
ms.author: owend
ms.openlocfilehash: fc7b9c69e6f81b41deb7a5d6d963225593845d84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-tooon-premises-data-sources-with-azure-on-premises-data-gateway"></a>使用 Azure 的內部部署資料閘道連接 tooon 內部部署資料來源
hello 在內部部署資料閘道作為橋接器，提供在內部部署資料來源與 hello 雲端中的您 Azure Analysis Services 伺服器之間的安全資料傳輸。 在多個 Azure Analysis Services 中的伺服器 hello 加法 tooworking 相同的區域，hello hello 閘道最新版本也可以搭配 Azure 邏輯應用程式、 Power BI、 電源應用程式和 Microsoft Flow。 您可以將多個服務在 hello 與單一閘道相同的區域。 

 Azure Analysis Services 需要在 hello 閘道資源相同的區域。 例如，如果您有 Azure Analysis Services 伺服器 hello 美國東部 2 區域中，您會需要 hello 美國東部 2 區域中的閘道資源。 美國東部 2 中的多部伺服器可以使用 hello 相同閘道器。

讓安裝程式以 hello 閘道 hello 第一次是四部分的程序：

- **下載並執行安裝程式** - 這個步驟會在您組織中的電腦上安裝閘道服務。

- **註冊您的閘道**-在此步驟中，您指定的名稱和復原您的閘道金鑰，然後選取區域，以 hello 閘道器雲端服務中註冊您的閘道。

- **在 Azure 中建立閘道資源** - 在此步驟中，您會在您的 Azure 訂用帳戶中建立閘道資源。

- **連接您的伺服器 tooyour 閘道資源**-一旦您訂用帳戶中有閘道資源，您就可以開始連接伺服器 tooit。

訂用帳戶設定閘道資源之後，您可以連接多部伺服器和其他服務 tooit。 您只需要 tooinstall 不同的閘道，並建立其他閘道資源，如果您的伺服器或其他服務在不同的區域。

tooget 立即，請參閱[安裝和設定內部部署資料閘道](analysis-services-gateway-install.md)。

## <a name="how-it-works"> </a>運作方式
您的電腦安裝在組織中的 hello 閘道會當做 Windows 服務，來執行**在內部部署資料閘道**。 這個本機服務已向 hello 透過 Azure 服務匯流排閘道器雲端服務。 您接著可為您的 Azure 訂用帳戶建立閘道資源 (閘道雲端服務)。 您 Azure 的 Analysis Services 伺服器接著會連接 tooyour 閘道資源。 當您伺服器需要 tooconnect tooyour 模型內部的查詢或處理資料來源時，查詢和資料流量會周遊 hello 閘道資源時，Azure 服務匯流排，hello 本機內部部署資料閘道服務，以及您的資料來源。 

![運作方式](./media/analysis-services-gateway/aas-gateway-how-it-works.png)

查詢和資料流程：

1. Hello 雲端服務所使用的認證加密的 hello hello 在內部部署資料來源建立查詢。 然後已傳送嗨閘道 tooprocess tooa 佇列。
2. hello 閘道器雲端服務會分析 hello 查詢，並將推送 hello 要求 toohello [Azure 服務匯流排](https://azure.microsoft.com/documentation/services/service-bus/)。
3. hello 在內部部署資料閘道會輪詢 hello 適用於 Azure 服務匯流排擱置的要求。
4. hello 閘道取得 hello 查詢、 解密 hello 認證，並利用這些認證連接 toohello 資料來源。
5. hello 閘道會傳送 hello 查詢 toohello 資料來源執行。
6. hello 結果會傳送 hello 資料來源，回復 toohello 閘道，然後拖曳 hello 雲端服務和您的伺服器。

## <a name="windows-service-account"> </a>Windows 服務帳戶
hello 在內部部署資料閘道已設定的 toouse *NT SERVICE\PBIEgwService* hello Windows 服務登入認證。 根據預設，其具有作為服務; hello 登入的權限hello 在內容中您要安裝 hello 閘道的 hello 機器。 此認證不是 hello 相同的帳戶使用 tooconnect tooon 內部部署資料來源或您的 Azure 帳戶。  

如果您遇到的問題與您的 proxy 伺服器，因為 tooauthentication，您可能會想的 toochange hello Windows 服務帳戶 tooa 網域使用者或受管理服務帳戶。

## <a name="ports"></a>連接埠
hello 閘道建立服務匯流排的輸出連線 tooAzure。 閘道會與下列輸出連接埠進行通訊︰TCP 443 (預設)、5671、5672、9350 到 9354。  hello 閘道不需要輸入連接埠。

我們建議您在防火牆中的資料區域的白名單 hello IP 位址。 您可以下載 hello [Microsoft Azure Datacenter IP 清單](https://www.microsoft.com/download/details.aspx?id=41653)。 此清單每週更新。

> [!NOTE]
> hello hello Azure Datacenter IP 清單中列出的 IP 位址是以 CIDR 標記法。 例如，10.0.0.0/24 並非 10.0.0.0 到 10.0.0.24。 深入了解 hello [CIDR 標記法](http://whatismyipaddress.com/cidr)。
>
>

hello 如下 hello 閘道所使用的 hello 完整網域名稱。

| 網域名稱 | 輸出連接埠 | 說明 |
| --- | --- | --- |
| *.powerbi.com |80 |Toodownload hello 安裝程式會使用 HTTP。 |
| *.powerbi.com |443 |HTTPS |
| *.analysis.windows.net |443 |HTTPS |
| *.login.windows.net |443 |HTTPS |
| *.servicebus.windows.net |5671-5672 |進階訊息佇列通訊協定 (AMQP) |
| *.servicebus.windows.net |443、9350-9354 |透過 TCP 之服務匯流排轉送上的接聽程式 (需要 443 才能取得「存取控制」權杖) |
| *.frontend.clouddatahub.net |443 |HTTPS |
| *.core.windows.net |443 |HTTPS |
| login.microsoftonline.com |443 |HTTPS |
| *.msftncsi.com |443 |如果無法連到 hello Power BI 服務的 hello 閘道，請使用 tootest 網際網路連線。 |
| *.microsoftonline-p.com |443 |用於驗證 (視設定而定)。 |

### <a name="force-https"></a>強制使用 Azure 服務匯流排進行 HTTPS 通訊
您可以使用 HTTPS 而不是直接 TCP; 強制 hello 閘道 toocommunicate 搭配 Azure Service Bus不過，這樣做，可以大幅降低效能。 您可以修改 hello *Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config*藉由變更 hello 值從檔案`AutoDetect`太`Https`。 這個檔案通常位於 *C:\Program Files\On-premises data gateway*。

```
<setting name="ServiceBusSystemConnectivityModeString" serializeAs="String">
    <value>Https</value>
</setting>
```

## <a name="faq"></a>常見問題集

### <a name="general"></a>一般

**問：**： 我需要閘道 hello 雲端，例如 Azure SQL Database 中的資料來源嗎？ <br/>
**答**：否。 閘道正在連接只 tooon 內部部署資料來源。

**問：**: hello 閘道是否有 toobe hello 做 hello 資料來源相同電腦上安裝？ <br/>
**答**：否。 hello 閘道正在連接 toohello 資料來源使用所提供的 hello 連接資訊。 Hello 閘道視為用戶端應用程式，這方面。 hello 閘道只需要 hello 功能 tooconnect toohello 伺服器所提供名稱，通常在 hello 相同網路。

<a name="why-azure-work-school-account"></a>

**問：**： 為什麼需要 toouse 工作或學校帳戶 toosign 中的？ <br/>
**A**： 您只能使用 Azure 的工作或學校帳戶，當您安裝 hello 在內部部署資料閘道。 登入帳戶會儲存在由 Azure Active Directory (Azure AD) 所管理的租用戶中。 通常，您的 Azure AD 帳戶的使用者主要名稱 (UPN) 符合 hello 電子郵件地址。

**問**︰我的認證儲存在哪裡？ <br/>
**A**： 您輸入的資料來源的 hello 認證會加密並儲存在 hello 閘道器雲端服務。 hello 認證會在 hello 在內部部署資料閘道進行解密。

**問**︰網路頻寬是否有任何需求？ <br/>
**答**︰建議您的網路連線要有良好的輸送量。 每個環境都不同，並傳送資料的 hello 數量會影響 hello 的結果。 使用 ExpressRoute 有利於 tooguarantee 的內部部署與 hello Azure 資料中心之間的輸送量層級。
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
**A**: hello 閘道在服務中，呼叫在內部部署資料閘道服務。

**問：**： 可以 hello 使用 Azure Active Directory 帳戶來執行閘道 Windows 服務嗎？ <br/>
**答**：否。 hello Windows 服務必須有有效的 Windows 帳戶。 根據預設，hello 服務會以 hello 服務 SID NT SERVICE\PBIEgwService 執行。

### <a name="high-availability"></a>高可用性和災害復原

**問**︰災害復原有哪些選項？ <br/>
**A**： 您可以使用 hello 修復金鑰 toorestore 或移動閘道。 當您安裝 hello 閘道時，指定 hello 修復金鑰。

**問：**: hello hello 修復金鑰的優點為何？ <br/>
**A**: hello 修復金鑰提供方式 toomigrate 或損毀狀況之後復原您的閘道設定。

## <a name="troubleshooting"></a>疑難排解

**問：**： 如何查看哪些查詢會傳送 toohello 在內部部署資料來源嗎？ <br/>
**A**： 您可以啟用查詢追蹤，其中包括傳送嗨查詢。 請記住 toochange 查詢後追蹤 toohello 完成疑難排解後的原始值。 讓查詢追蹤保持開啟會產生較大的記錄。

您也可以查看資料來源具備的工具是否有追蹤查詢。 例如，您可以使用 SQL Server 和 Analysis Services 的擴充事件或 SQL Profiler。

**問：**： 所在 hello 閘道記錄檔？ <br/>
**答**：請參閱本主題稍後的「記錄」。

### <a name="update"></a>更新 toohello 最新版本

Hello 閘道器版本過期時，就會出現許多問題。 良好一般做法，請確定您使用 hello 最新版本。 如果您超過一個月或更久沒有更新 hello 閘道，您可能會考慮安裝 hello hello 閘道最新版本，並查看可否重現 hello 問題。

### <a name="error-failed-tooadd-user-toogroup--2147463168-pbiegwservice-performance-log-users"></a>錯誤： 無法 tooadd 使用者 toogroup。 (-2147463168 PBIEgwService Performance Log Users)

如果您嘗試 tooinstall hello 閘道不支援的網域控制站上，您可能會收到這個錯誤。 請確定您部署的 hello 閘道不是網域控制站的電腦上。

## <a name="logs"></a>記錄

進行疑難排解時，記錄檔是重要的資源。

#### <a name="enterprise-gateway-service-logs"></a>企業閘道服務記錄檔

`C:\Users\PBIEgwService\AppData\Local\Microsoft\On-premises data gateway\<yyyyymmdd>.<Number>.log`

#### <a name="configuration-logs"></a>組態記錄檔

`C:\Users\<username>\AppData\Local\Microsoft\On-premises data gateway\GatewayConfigurator.log`




#### <a name="event-logs"></a>事件記錄檔

您可以找到 hello 下的資料管理閘道器和 PowerBIGateway 記錄**Application and Services Logs**。


## <a name="telemetry"></a>遙測
遙測可應用在監視和疑難排解上。 依照預設

**tooturn 遙測**

1.  請檢查 hello 在內部部署資料閘道用戶端電腦上的目錄 hello。 此目錄通常是 **%systemdrive%\Program Files\內部部署資料閘道**。 或者，您可以開啟 [服務] 主控台，並檢查 hello 路徑 tooexecutable: hello 在內部部署資料閘道服務的屬性。
2.  在用戶端目錄中的 hello Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config 檔案。 變更 hello SendTelemetry 設定 tootrue。
        
    ```
        <setting name="SendTelemetry" serializeAs="String">
                    <value>true</value>
        </setting>
    ```

3.  儲存變更並重新啟動 hello Windows 服務： 在內部部署資料閘道服務。




## <a name="next-steps"></a>後續步驟
* [ Analysis Services](analysis-services-manage.md)
* [從 Azure Analysis Services 取得資料](analysis-services-connect.md)
