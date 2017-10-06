---
title: "aaaCreate 和管理混合式連線 |Microsoft 文件"
description: "了解 toocreate 混合連線，管理 hello 連接和安裝 hello 混合式連線管理員的方式。 MABS，WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: erikre
editor: 
ms.assetid: aac0546b-3bae-41e0-b874-583491a395ea
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: ccompy
ms.openlocfilehash: 561d8f3dd97318130a05c3bb2874ee8022e7f417
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-hybrid-connections"></a>建立和管理混合式連線

> [!IMPORTANT]
> BizTalk 混合式連線已停用，並以 App Service 混合式連線取代。 如需詳細資訊，包括如何 toomanage 現有 BizTalk 混合式連線，請參閱[Azure 應用程式服務的混合式連線](../app-service/app-service-hybrid-connections.md)。


## <a name="overview-of-hello-steps"></a>Hello 步驟的概觀
1. 建立混合式連接輸入 hello**主機名稱**或**FQDN**的私人網路中的 hello 在內部部署資源。
2. 連結您的 Azure web 應用程式或 Azure 的行動裝置應用程式 toohello 混合式連接。
3. 在內部部署資源上安裝 hello 混合式連線管理員，而且連接 toohello 特定混合式連接。 提供按一下體驗 tooinstall hello Azure 入口網站，並連接。
4. 管理混合式連線及其連接金鑰。

本主題將列出這些步驟。 

> [!IMPORTANT]
> 很可能 tooset 混合式連接端點 tooan IP 位址。 如果您使用的 IP 位址，您可能會或可能無法到達 hello 在內部部署資源，根據您的用戶端。 hello 混合式連接取決於 hello 用戶端執行 DNS 查閱。 在大部分情況下，hello**用戶端**是應用程式程式碼。 如果 hello 用戶端不會執行 DNS 查閱、 （它不會嘗試 tooresolve hello IP 位址就好像是網域名稱 (x.x.x.x)），則流量不會傳送到 hello 混合式連接。
> 
> 例如 (虛擬程式碼)，您會定義 **10.4.5.6** 做為內部部署主機︰
> 
> **下列案例中運作的 hello:**  
> `Application code -> GetHostByName("10.4.5.6") -> Resolves too127.0.0.3 -> Connect("127.0.0.3") -> Hybrid Connection -> on-prem host`
> 
> **不適用於下列案例中的 hello:**  
> `Application code -> Connect("10.4.5.6") -> ?? -> No route toohost`
> 
> 

## <a name="CreateHybridConnection"></a>建立混合式連線
混合式連接中可建立 hello 使用 Web 應用程式的 Azure 入口網站**或**使用 BizTalk 服務。 

**toocreate 使用 Web 應用程式的混合式連線**，請參閱[連接 Azure Web Apps tooan 在內部部署資源](../app-service-web/web-sites-hybrid-connection-get-started.md)。 您也可以從您的 web 應用程式，這是慣用的 hello 方法安裝 hello 混合式連線管理員 (HCM)。 

**在 BizTalk 服務中的混合式連線 toocreate**:

1. 登入 toohello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/p/?LinkID=213885)。
2. 在 hello 左側瀏覽窗格中，選取**BizTalk 服務**，然後選取 BizTalk 服務。 
   
    如果您沒有現有的 BizTalk 服務，您可以 [建立 BizTalk 服務](biztalk-provision-services.md)。
3. 選取 hello**混合式連線** 索引標籤：  
   ![混合式連線索引標籤][HybridConnectionTab]
4. 選取**建立混合式連接**或選取 hello**新增**hello 工作列中的按鈕。 輸入 hello 下列：
   
   | 屬性 | 說明 |
   | --- | --- |
   | 名稱 |hello 混合式連接名稱必須是唯一的而且不能 hello 相同命名為 hello BizTalk 服務。 您可以輸入任何名稱，但要能夠具體表示用途。 範例包括：<br/><br/>Payroll*SQLServer*<br/>SupplyList*SharepointServer*<br/>Customers*OracleServer* |
   | 主機名稱 |輸入 hello 完整的主機名稱，只有 hello 主機名稱，或是 hello hello 在內部部署資源的 IPv4 位址。 範例包括：<br/><br/>mySQLServer<br/>*mySQLServer*.*Domain*.corp.*yourCompany*.com<br/>*myHTTPSharePointServer*<br/>*myHTTPSharePointServer*.*yourCompany*.com<br/>10.100.10.10<br/><br/>如果您使用 hello IPv4 位址，請注意您的用戶端或應用程式程式碼可能無法解析 hello IP 位址。 請參閱 hello 重要附註在 hello 本主題的頂端。 |
   | Port |輸入 hello hello 在內部部署資源連接埠號碼。 例如，如果您使用 Web Apps，請輸入連接埠 80 或 443。 如果您使用 SQL Server，請輸入連接埠 1433。 |
5. 選取 hello 核取記號 toocomplete hello 安裝程式。 

#### <a name="additional"></a>其他
* 可建立多個混合式連線。 請參閱 hello [BizTalk 服務： 版本圖表](biztalk-editions-feature-chart.md)hello 允許連線的數目。 
* 每個「混合式連線」都是由一對連接字串建立而成：分別是負責「傳送」的應用程式金鑰，以及負責「接聽」的內部部署金鑰。 每一對都有「主要」和「次要」金鑰。 

## <a name="LinkWebSite"></a>連結 Azure App Service Web 應用程式或行動應用程式
選取 toolink Web 應用程式或行動裝置應用程式中現有的混合式連接的 Azure App Service tooan**使用現有的混合式連接**hello 混合式連線刀鋒視窗中。 請參閱[在 Azure App Service 中使用混合式連線存取內部部署資源](../app-service-web/web-sites-hybrid-connection-get-started.md)。

## <a name="InstallHCM"></a>安裝 hello 混合式連線管理員內部部署
建立混合式連接之後，安裝 hello 混合式連線管理員上 hello 在內部部署資源。 可從 Azure Web Apps 或 BizTalk 服務下載此程式。 BizTalk 服務步驟： 

1. 登入 toohello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/p/?LinkID=213885)。
2. 在 hello 左側瀏覽窗格中，選取**BizTalk 服務**，然後選取 BizTalk 服務。 
3. 選取 hello**混合式連線** 索引標籤：  
   ![混合式連線索引標籤][HybridConnectionTab]
4. 在 hello 工作列上，選取 **在內部部署安裝**:  
   ![內部部署設定][HCOnPremSetup]
5. 選取**安裝及設定**toorun 或下載 hello 混合式連線管理員上 hello 內部部署系統。 
6. 選取 hello 核取記號 toostart hello 安裝。 

<!--
You can also download hello Hybrid Connection Manager MSI file and copy hello file tooyour on-premises resource. Specific steps:

1. Copy hello on-premises primary Connection String. See [Manage Hybrid Connections](#ManageHybridConnection) in this topic for hello specific steps.
2. Download hello Hybrid Connection Manager MSI file. 
3. On hello on-premises resource, install hello Hybrid Connection Manager from hello MSI file. 
4. Using Windows PowerShell, type: 
> Add-HybridConnection -ConnectionString “*Your On-Premises Connection String that you copied*” 
--> 

#### <a name="additional"></a>其他
* 混合式連線管理員可以安裝在下列作業系統的 hello:
  
  * Windows Server 2008 R2 (須有 .NET Framework 4.5+ 和 Windows Management Framework 4.0+)
  * Windows Server 2012 (須有 Windows Management Framework 4.0+)
  * Windows Server 2012 R2
* 安裝 hello 混合式連接管理員之後，hello 會發生下列情況： 
  
  * hello 裝載於 Azure 的混合式連線會自動設定的 toouse hello 主應用程式連接字串。 
  * hello 在內部部署資源為自動設定的 toouse hello 主要內部部署連接字串。
* hello 混合式連線管理員必須使用有效的內部部署連接字串進行授權。 hello Azure Web 應用程式或行動應用程式必須使用有效的應用程式連接字串進行授權。
* 您可以在另一部伺服器上安裝另一個執行個體的 hello 混合式連線管理員調整混合式連線。 設定 hello 在內部部署接聽程式 toouse hello 相同位址為 hello 第一個在內部部署接聽程式。 在此情況下，hello 已流量隨機分配 （循環配置資源） 之間 hello 作用中的內部部署接聽程式。 

## <a name="ManageHybridConnection"></a>管理混合式連線
toomanage 混合式連線，您可以：

* 使用 hello Azure 入口網站，並移 tooyour BizTalk 服務。 
* 使用 [REST API](http://msdn.microsoft.com/library/azure/dn232347.aspx)。

#### <a name="copyregenerate-hello-hybrid-connection-strings"></a>複製/重新產生 hello 混合式連接字串
1. 登入 toohello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/p/?LinkID=213885)。
2. 在 hello 左側瀏覽窗格中，選取**BizTalk 服務**，然後選取 BizTalk 服務。 
3. 選取 hello**混合式連線** 索引標籤：  
   ![混合式連線索引標籤][HybridConnectionTab]
4. 選取 hello 混合式連接。 在 hello 工作列上，選取 **管理連接**:  
   ![管理選項][HCManageConnection]
   
    **管理連線**清單 hello 應用程式和內部部署連接字串。 您可以複製連接字串 hello 或重新產生存取金鑰 hello 連接字串中所使用的 hello。 
   
    **如果您選取重新產生**，hello 的 hello 則變更連接字串內使用共用存取金鑰。 請勿 hello 遵循：
   
   * 在 hello Azure 傳統入口網站，選取 **同步金鑰**hello Azure 應用程式中。
   * 重新執行 hello**在內部部署安裝**。 當您重新執行 hello 在內部部署安裝程式，在內部部署資源，則會自動 hello 設定 toouse hello 更新主要連接字串。

#### <a name="use-group-policy-toocontrol-hello-on-premises-resources-used-by-a-hybrid-connection"></a>使用群組原則 toocontrol hello 內部部署混合式連接所使用的資源
1. 下載 hello[混合式連線管理員系統管理範本](http://www.microsoft.com/download/details.aspx?id=42963)。
2. Hello 檔案解壓縮。
3. Hello 在電腦上修改群組原則，請勿 hello 遵循：  
   
   * 將複製 hello。ADMX 檔案 toohello *%WINROOT%\PolicyDefinitions*資料夾。
   * 將複製 hello。ADML 檔案 toohello *%WINROOT%\PolicyDefinitions\en-us*資料夾。

複製後，您可以使用群組原則編輯器 toochange hello 原則。

## <a name="next"></a>下一步
[連接 Azure Web Apps tooan 在內部部署資源](../app-service-web/web-sites-hybrid-connection-get-started.md)  
[從 Azure Web 應用程式連接 tooon 內部部署 SQL Server](../app-service-web/web-sites-hybrid-connection-connect-on-premises-sql-server.md)   
[混合式連線概觀](integration-hybrid-connection-overview.md)

## <a name="see-also"></a>另請參閱
[用於管理 Microsoft Azure 上之 BizTalk 服務的 REST API](http://msdn.microsoft.com/library/azure/dn232347.aspx)  
[BizTalk 服務：版本圖表](biztalk-editions-feature-chart.md)  
[使用 Azure 傳統入口網站建立「BizTalk 服務」](biztalk-provision-services.md)  
[BizTalk 服務：儀表板、監視和調整索引標籤](biztalk-dashboard-monitor-scale-tabs.md)

[HybridConnectionTab]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionTab.png
[HCOnPremSetup]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionOnPremSetup.png
[HCManageConnection]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionManageConn.png 
