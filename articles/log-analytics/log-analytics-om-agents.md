---
title: "aaaConnect Operations Manager tooLog 分析 |Microsoft 文件"
description: "toomaintain 您現有的投資，在 System Center Operations Manager，並使用擴充功能記錄分析，您可以整合 Operations Manager 與 OMS 工作區。"
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 245ef71e-15a2-4be8-81a1-60101ee2f6e6
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: magoedte
ms.openlocfilehash: b2841c7aa209fec7357dc4c8b1ff4325fdaa37ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-operations-manager-toolog-analytics"></a>連接 Operations Manager tooLog 分析
toomaintain 您現有的投資，在 System Center Operations Manager，並使用擴充功能記錄分析，您可以整合 Operations Manager 與 OMS 工作區。  這可讓您利用 OMS 的 hello 機會繼續 toouse Operations Manager 時要：

* 繼續監視您的 IT 服務，與 Operations Manager hello 健全狀況
* 維護與支援事件和問題管理之 ITSM 解決方案的整合
* 管理部署的代理程式 tooon 內部和公用雲端 IaaS 虛擬機器，您使用 Operations Manager 監視 hello 生命週期

整合 System Center Operations Manager 與使用 hello 速度與效率中收集、 儲存及分析資料的 Operations Manager OMS 新增值 tooyour 服務作業的策略。  OMS 協助建立相互關聯，並朝向識別 hello 錯誤的問題和面對日數，以支援您現有的問題管理程序的工作。   hello hello 搜尋引擎 tooexamine 效能、 事件和警示資料，與豐富的儀表板的彈性和報告功能 tooexpose 有意義的方式，此資料會示範 OMS 帶來 complimenting Operations Manager 中的 hello 強度。

hello 代理程式回報 toohello Operations Manager 管理群組會從您根據 hello 記錄分析資料來源 」 和 「 您已啟用您的 OMS 訂用帳戶中解決方案的伺服器收集資料。  根據您已啟用的 hello 解決方案，這些解決方案的資料是 toohello OMS web 服務，或因為 hello hello 代理程式管理系統上所收集的資料磁碟區會直接傳送訊息，請傳送直接從 Operations Manager 管理伺服器從 hello 代理程式 tooOMS web 服務。 hello 管理伺服器將轉寄 hello OMS 資料直接 toohello OMS web 服務。它永遠不會寫入 toohello OperationsManager 或 OperationsManagerDW 資料庫。  當管理伺服器失去連線能力與 hello OMS web 服務時，只有重新建立與 OMS 通訊之前，在本機快取 hello 資料。  如果 hello 管理伺服器已離線到期 tooplanned 維護或非計劃的中斷，hello 管理群組中的另一部管理伺服器會繼續與 OMS 的連線。  

hello 下列圖表描述 hello hello 管理伺服器與 System Center Operations Manager 管理群組和 OMS，包括 hello 方向和連接埠中的代理程式之間的連線。   

![oms-operations-manager-integration-diagram](./media/log-analytics-om-agents/oms-operations-manager-connection.png)

如果您的 IT 安全性原則不允許您的網路 tooconnect toohello 網際網路上的電腦，管理伺服器可以設定的 tooconnect toohello OMS 閘道 tooreceive 組態資訊並傳送收集的資料取決於 hello 方案已啟用。  如需詳細資訊和步驟上如何 tooconfigure OMS 閘道 toohello OMS 服務，透過您 Operations Manager 管理群組 toocommunicate 參閱[連接使用 hello OMS 閘道電腦 tooOMS](log-analytics-oms-gateway.md)。  

## <a name="system-requirements"></a>系統需求
開始之前，請檢閱下列符合必要條件的詳細資料 tooverify hello。

* OMS 僅支援 Operations Manager 2016、Operations Manager 2012 SP1 UR6 和更新版本，以及 Operations Manager 2012 R2 UR2 和更新版本。  Operations Manager 2012 SP1 UR7 和 Operations Manager 2012 R2 UR3 中已加入 Proxy 支援。
* 所有 Operations Manager 代理程式必須符合最低支援需求。 確定代理程式已在 hello 最小更新，否則 Windows 代理程式的流量可能會失敗並許多錯誤可能會填滿 hello Operations Manager 事件記錄檔。
* OMS 訂用帳戶。  如需進一步資訊，請檢閱 [開始使用 Log Analytics](log-analytics-get-started.md)。

### <a name="network"></a>網路
以下清單 hello proxy 和防火牆設定資訊所需的 hello Operations Manager 代理程式、 管理伺服器，以及與 OMS 的 Operations 主控台 toocommunicate hello 資訊。  從每個元件的流量是輸出從您的網路 toohello OMS 服務。     

|資源 | 連接埠號碼| 略過 HTTPS 檢查|  
|---------|------|-----------------------|  
|**代理程式**|||  
|\*.ods.opinsights.azure.com| 443 |是|  
|\*.oms.opinsights.azure.com| 443|是|  
|\*.blob.core.windows.net| 443|是|  
|\*.azure-automation.net| 443|是|  
|**管理伺服器**|||  
|\*.service.opinsights.azure.com| 443||  
|\*.blob.core.windows.net| 443| 是|  
|\*.ods.opinsights.azure.com| 443| 是|  
|*.azure-automation.net | 443| 是|  
|**Operations Manager 主控台 tooOMS**|||  
|service.systemcenteradvisor.com| 443||  
|\*.service.opinsights.azure.com| 443||  
|\*.live.com| 80 和 443||  
|\*.microsoft.com| 80 和 443||  
|\*.microsoftonline.com| 80 和 443||  
|\*.mms.microsoft.com| 80 和 443||  
|login.windows.net| 80 和 443||  


## <a name="connecting-operations-manager-toooms"></a>連接 Operations Manager tooOMS
執行一系列的步驟 tooconfigure 後 hello 您 Operations Manager 管理群組 tooconnect tooone 的 OMS 工作區。

1. 在 hello Operations Manager 主控台中，選取 hello**管理**工作區。
2. 展開 hello Operations Management Suite 節點，然後按一下**連接**。
3. 按一下 hello**註冊 tooOperations Management Suite**連結。
4. 在 hello **Operations Management Suite 登入精靈： 驗證**頁面上，輸入 hello 電子郵件地址或電話號碼和您的 OMS 訂用帳戶，與相關聯的 hello 系統管理員帳戶的密碼，然後按一下**登入**。
5. 您成功驗證，在 hello 之後**Operations Management Suite 登入精靈： 選取工作區**頁面上，會提示您 tooselect OMS 工作區。  如果您有多個工作區中，選取 hello 您想 tooregister hello 下拉式清單中，從 hello Operations Manager 管理群組，然後按一下工作區**下一步**。
   
   > [!NOTE]
   > Operations Manager 一次只支援一個 OMS 工作區。 hello 連接和已註冊的 tooOMS 與 hello 前一個工作區的 hello 電腦都會從 OMS 移除。
   > 
   > 
6. 在 hello **Operations Management Suite 登入精靈： 摘要**頁面上，確認您的設定都正確無誤，如果按**建立**。
7. 在 hello **Operations Management Suite 登入精靈： 完成**頁面上，按一下**關閉**。

### <a name="add-agent-managed-computers"></a>加入代理程式所管理的電腦
之後您可以設定整合的 OMS 工作區，這只會建立與 OMS 的連線，從 hello 代理程式回報 tooyour 管理群組收集任何資料。 除非您設定特定代理程式管理的哪些電腦會收集 Log Analytics 的資料，否則不會發生這種情況。 您可以個別選取 hello 電腦物件，或者您可以選取包含 Windows 電腦物件的群組。 您無法選取包含另一個類別之執行個體 (例如邏輯磁碟或 SQL 資料庫) 的群組。

1. 開啟 hello Operations Manager 主控台並選取 hello**管理**工作區。
2. 展開 hello Operations Management Suite 節點，然後按一下**連接**。
3. 按一下 hello**新增電腦/群組**底下 hello 動作連結上 hello 右邊 hello 窗格的標題。
4. 在 hello**電腦搜尋**對話方塊中，您可以搜尋由 Operations Manager 監視電腦或群組。 選取 電腦或群組 tooonboard tooOMS**新增**，然後按一下 **確定**。

您可以檢視電腦和群組設定中 hello hello 受管理的電腦節點下 Operations Management Suite toocollect 資料**管理**hello Operations 主控台 工作區。  您可以視需要在這裡新增或移除電腦和群組。

### <a name="configure-oms-proxy-settings-in-hello-operations-console"></a>在 hello Operations 主控台中設定 OMS 的 proxy 設定
執行下列步驟，如果內部 proxy 伺服器 hello 管理群組與 OMS web 服務之間的 hello。  這些設定都集中管理 hello 管理群組與 oms hello 領域 toocollect 資料中包含分散式的 tooagent 受管理的系統。  這是有幫助的某些解決方案當許可 hello 管理伺服器和傳送資料，直接 tooOMS web 服務。

1. 開啟 hello Operations Manager 主控台並選取 hello**管理**工作區。
2. 展開 Operations Management Suite，然後按一下連接 。
3. 在 hello OMS 連接 檢視中，按一下 **設定 Proxy 伺服器**。
4. 在**Operations Management Suite 精靈： Proxy 伺服器**頁面上，選取**使用 proxy 伺服器 tooaccess hello Operations Management Suite**，然後輸入 hello 與 hello 通訊埠編號，例如 http:// 的 URLcorpproxy:80，然後按一下**完成**。

如果您的 proxy 伺服器需要驗證，請執行 hello 下列步驟 tooconfigure 認證和需要 toopropagate toomanaged 電腦報告 tooOMS hello 管理群組中的設定。

1. 開啟 hello Operations Manager 主控台並選取 hello**管理**工作區。
2. 在 [RunAs 組態] 底下，選取 [設定檔]。
3. 開啟 hello **System Center Advisor 執行身分設定檔 Proxy**設定檔。
4. 在 hello 執行身分設定檔精靈 中，按一下 新增 toouse 的執行身分帳戶。 您可以建立[執行身分帳戶](https://technet.microsoft.com/library/hh321655.aspx)，或使用現有的帳戶。 此帳戶必須 toohave 足夠的權限 toopass 透過 hello proxy 伺服器。
5. tooset hello 帳戶 toomanage 中，選擇 **選取的類別、 群組或物件**，按一下 **選取...** 然後按一下群組… tooopen hello**群組搜尋**方塊。
6. 搜尋，然後選取 [Microsoft System Center Advisor 監控伺服器群組] 。  按一下**確定**選取 hello 群組 tooclose hello 之後**群組搜尋**方塊。
7. 按一下**確定**tooclose hello**新增執行身分帳戶**方塊。
8. 按一下**儲存**toocomplete hello 精靈並儲存變更。

建立 hello 連線，而且您設定的代理程式會收集和報告資料 tooOMS 之後，hello 下列組態會套用在 hello 管理群組中，不一定會依照順序：

* 執行身分帳戶 hello **Microsoft.SystemCenter.Advisor.RunAsAccount.Certificate**建立。  相關聯的執行身分設定檔 hello **Microsoft System Center Advisor 執行做為設定檔 Blob**和目標設定為兩個類別-**集合伺服器**和**Operations Manager 管理群組**.
* 會建立兩個連接器。  第一次命名 hello **Microsoft.SystemCenter.Advisor.DataConnector**並會自動設定轉寄 hello 管理群組 tooOMS 記錄檔中的所有類別的執行個體所產生的所有警示的訂閱分析。 hello 第二個連接器**Advisor 連接器**，這是負責與 OMS web 服務通訊以及共用資料。
* 代理程式和確定您已選取 toocollect 資料 hello 管理群組中的群組會加入 toohello **Microsoft System Center Advisor 監控伺服器群組**。

## <a name="management-pack-updates"></a>管理組件更新
設定完成之後，hello Operations Manager 管理群組會建立與 hello OMS 服務的連線。  hello 管理伺服器與 hello web 服務同步處理，並以您已啟用與 Operations Manager 整合的 hello 解決方案的管理組件的 hello 格式接收更新的組態資訊。   Operations Manager 會檢查這些管理組件的更新，如果有更新，就會自動下載並匯入。  有兩個規則特別可控制這個行為︰

* **Microsoft.SystemCenter.Advisor.MPUpdate** -hello 基底的 OMS 管理套件會更新。 預設會每 12 小時執行一次。
* **Microsoft.SystemCenter.Advisor.Core.GetIntelligencePacksRule** - 更新工作區中所啟用的解決方案管理組件。 預設會每五 (5) 分鐘執行一次。

您可以覆寫 tooeither 停用它們，以防止自動下載這兩個規則，或修改 hello 頻率 hello 管理同步處理伺服器與 OMS toodetermine 如果新的管理組件可用，且應下載的頻率。  請依照下列步驟 hello[如何 tooOverride 規則或監視](https://technet.microsoft.com/library/hh212869.aspx)toomodify hello**頻率**參數的值，以秒為單位 toochange hello 同步處理排程，或修改 hello**已啟用**參數 toodisable hello 規則。  目標 hello 會覆寫 tooall 類別物件的 Operations Manager 管理群組。

如果您想 toocontinue 遵循現有的變更控制程序來控制生產管理群組中的管理組件版本，您可以停用 hello 規則，並讓它們可在指定時間允許更新。 如果您環境中有開發或 QA 管理群組，而且它有連線能力 toohello 網際網路，您可以設定該管理群組與 OMS 工作區 toosupport 這種情況。  這可讓您 tooreview，並將其發佈至您的生產管理群組之前進行評估 hello 反覆 hello OMS 管理套件版本。

## <a name="switch-an-operations-manager-group-tooa-new-oms-workspace"></a>切換 Operations Manager 群組 tooa 新 OMS 工作區
1. 登入 tooyour OMS 訂用帳戶，並建立工作區中的[Microsoft Operations Management Suite](http://oms.microsoft.com/)。
2. 選取 hello hello Operations Manager 系統管理員角色的成員的帳戶開啟 hello Operations Manager 主控台**管理**工作區。
3. 展開 Operations Management Suite，選取 [連接] 。
4. 選取 hello**重新設定作業 Management Suite** hello 中介層 hello 窗格的一邊上的連結。
5. 請遵循 hello **Operations Management Suite 登入精靈**，然後輸入 hello 電子郵件地址或電話號碼和 hello 與新的 OMS 工作區相關聯的系統管理員帳戶的密碼。
   
   > [!NOTE]
   > hello **Operations Management Suite 登入精靈： 選取工作區**頁面會顯示使用中的 hello 現有工作區。
   > 
   > 

## <a name="validate-operations-manager-integration-with-oms"></a>驗證 Operations Manager 與 OMS 的整合
有幾個不同的方式，您可以確認您的 OMS tooOperations Manager 整合成功。

### <a name="tooconfirm-integration-from-hello-oms-portal"></a>tooconfirm 整合，從 hello OMS 入口網站
1. 在 hello OMS 入口網站中，按一下 hello**設定**磚
2. 選取 [連接的來源]。
3. 在 hello 資料表 hello System Center Operations Manager 一節，您應該會看到 hello hello 管理群組名稱的前次收到資料時，與 hello 數目的代理程式和一起列出。
   
   ![oms-settings-connectedsources](./media/log-analytics-om-agents/oms-settings-connectedsources.png)
4. 請注意 hello**工作區識別碼**下 hello 左方 hello 設定頁面的值。  以下您將根據 Operations Manager 管理群組來驗證此值。  

### <a name="tooconfirm-integration-from-hello-operations-console"></a>從 hello Operations 主控台 tooconfirm 整合
1. 開啟 hello Operations Manager 主控台並選取 hello**管理**工作區。
2. 選取**管理組件**在 hello**尋找：**文字方塊中輸入**Advisor**或**智慧**。
3. 根據您已啟用的 hello 解決方案，您會看到 hello 搜尋結果中列出的對應管理組件。  例如，如果您已啟用 hello 警示管理解決方案，hello 管理組件 Microsoft System Center Advisor 警示管理是 hello 清單中。
4. 從 hello**監視**檢視中，瀏覽 toohello **Operations 管理 Suite\Health 狀態**檢視。  選取管理伺服器在 hello **Management Server 狀態** 窗格中，在 hello**詳細資料檢視**窗格確認屬性的 hello 值**驗證服務 URI**符合 hello OMS 工作區識別碼。
   
   ![oms-opsmgr-mg-authsvcuri-property-ms](./media/log-analytics-om-agents/oms-opsmgr-mg-authsvcuri-property-ms.png)

## <a name="remove-integration-with-oms"></a>移除與 OMS 的整合
當您不再需要您的 Operations Manager 管理群組與 OMS 工作區之間的整合時，有數個必要步驟 tooproperly 移除 hello 連線和 hello 管理群組中的組態。 hello 下列程序，您已刪除的管理群組的 hello 參考更新您的 OMS 工作區，刪除 hello OMS 連接器，然後再刪除管理組件支援 OMS。   

您已啟用與 Operations Manager 整合的 hello 解決方案的管理組件和 hello 管理組件以 hello OMS 服務的必要的 toosupport 整合無法輕鬆地從 hello 管理群組刪除。  這是因為某些 hello OMS 管理套件的其他相關的管理組件相依性。  toodelete 管理組件，因為相依於其他管理組件中，下載 hello 指令碼[移除相依性的管理組件](https://gallery.technet.microsoft.com/scriptcenter/Script-to-remove-a-84f6873e)從 TechNet 指令碼中心。  

1. Hello Operations Manager 系統管理員角色的成員的帳戶開啟 Operations Manager 命令殼層 hello。
   
    > [!WARNING]
    > 請確認您沒有任何自訂的管理組件 hello word Advisor 或 IntelligencePack hello 名稱，再繼續進行，否則 hello 步驟 hello 管理群組中刪除它們。
    > 

2. Hello 命令殼層提示字元中輸入`Get-SCOMManagementPack -name "*Advisor*" | Remove-SCOMManagementPack -ErrorAction SilentlyContinue`
3. 接著輸入 `Get-SCOMManagementPack -name “*IntelligencePack*” | Remove-SCOMManagementPack -ErrorAction SilentlyContinue`
4. tooremove 任何管理組件，剩餘的有相依的其他 System Center Advisor 管理組件，請使用 hello 指令碼*RecursiveRemove.ps1*您從先前 hello TechNet 指令碼中心下載。  
 
    > [!NOTE]
    > 請勿刪除 hello Microsoft System Center Advisor 或 Microsoft System Center 內部 Advisor 管理組件。  
    >  

5. Hello Operations Manager 系統管理員角色成員的帳戶開啟 hello Operations Manager Operations 主控台。
6. 在下**管理**，選取 hello**管理組件**節點在 hello**尋找：**方塊中，輸入**Advisor**並確認 hello下列管理組件仍會匯入管理群組：
   
   * Microsoft System Center Advisor
   * Microsoft System Center Advisor Internal
7. 在 hello OMS 入口網站中，按一下 hello**設定**磚。
8. 選取 [連接的來源] 。
9. 在 System Center Operations Manager 區段 hello hello 資料表，您應該會看到 hello 名稱要 tooremove hello 工作區中的 hello 管理群組。  Hello] 欄下方**最後一筆資料**，按一下 [**移除**。  
   
    > [!NOTE]
    > hello**移除**連結將無法使用之前在 14 天後如果沒有偵測到從 hello 連線的管理群組的活動。  
    > 

10. 會出現一個視窗，詢問您想要移除 hello tooproceed tooconfirm。  按一下**是**tooproceed。 

toodelete hello 兩個連接器-Microsoft.SystemCenter.Advisor.DataConnector 和 Advisor 連接器、 儲存 hello tooyour 電腦以下的 PowerShell 指令碼及執行使用 hello 遵循範例：

```
    .\OM2012_DeleteConnector.ps1 “Advisor Connector” <ManagementServerName>
    .\OM2012_DeleteConnectors.ps1 “Microsoft.SytemCenter.Advisor.DataConnector” <ManagementServerName>
```

> [!NOTE]
> hello 電腦執行此指令碼，如果不是管理伺服器，應該根據 hello 版本的管理群組安裝 hello Operations Manager 命令殼層。
> 
> 

```
    `param(
    [String] $connectorName,
    [String] $msName="localhost"
    )
    $mg = new-object Microsoft.EnterpriseManagement.ManagementGroup $msName
    $admin = $mg.GetConnectorFrameworkAdministration()
    ##########################################################################################
    # Configures a connector with hello specified name.
    ##########################################################################################
    function New-Connector([String] $name)
    {
         $connectorForTest = $null;
         foreach($connector in $admin.GetMonitoringConnectors())
    {
    if($connectorName.Name -eq ${name})
    {
         $connectorForTest = Get-SCOMConnector -id $connector.id
    }
    }
    if ($connectorForTest -eq $null)
    {
         $testConnector = New-Object Microsoft.EnterpriseManagement.ConnectorFramework.ConnectorInfo
         $testConnector.Name = $name
         $testConnector.Description = "${name} Description"
         $testConnector.DiscoveryDataIsManaged = $false
         $connectorForTest = $admin.Setup($testConnector)
         $connectorForTest.Initialize();
    }
    return $connectorForTest
    }
    ##########################################################################################
    # Removes a connector with hello specified name.
    ##########################################################################################
    function Remove-Connector([String] $name)
    {
        $testConnector = $null
        foreach($connector in $admin.GetMonitoringConnectors())
       {
        if($connector.Name -eq ${name})
       {
         $testConnector = Get-SCOMConnector -id $connector.id
       }
      }
     if ($testConnector -ne $null)
     {
        if($testConnector.Initialized)
     {
     foreach($alert in $testConnector.GetMonitoringAlerts())
     {
       $alert.ConnectorId = $null;
       $alert.Update("Delete Connector");
     }
     $testConnector.Uninitialize()
     }
     $connectorIdForTest = $admin.Cleanup($testConnector)
     }
    }
    ##########################################################################################
    # Delete a connector's Subscription
    ##########################################################################################
    function Delete-Subscription([String] $name)
    {
      foreach($testconnector in $admin.GetMonitoringConnectors())
      {
      if($testconnector.Name -eq $name)
      {
        $connector = Get-SCOMConnector -id $testconnector.id
      }
    }
    $subs = $admin.GetConnectorSubscriptions()
    foreach($sub in $subs)
    {
      if($sub.MonitoringConnectorId -eq $connector.id)
      {
        $admin.DeleteConnectorSubscription($admin.GetConnectorSubscription($sub.Id))
      }
     }
    }
    #New-Connector $connectorName
    write-host "Delete-Subscription"
    Delete-Subscription $connectorName
    write-host "Remove-Connector"
    Remove-Connector $connectorName
```

在未來的 hello 如果您計劃重新連線管理群組 tooan OMS 工作區，您的需要 toore 匯入 hello `Microsoft.SystemCenter.Advisor.Resources.\<Language>\.mpb` hello 最新的更新彙總從管理組件檔案套用 tooyour 管理群組。  您可以找到此檔案在 hello`%ProgramFiles%\Microsoft System Center 2012`或 hello`System Center 2012 R2\Operations Manager\Server\Management Packs for Update Rollups`資料夾。

## <a name="next-steps"></a>後續步驟
tooadd 功能和收集資料，請參閱[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。


