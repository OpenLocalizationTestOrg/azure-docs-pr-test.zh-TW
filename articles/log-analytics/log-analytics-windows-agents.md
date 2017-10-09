---
title: "aaaConnect Windows 電腦 tooAzure 記錄分析 |Microsoft 文件"
description: "本文將說明在您的內部部署基礎結構 toohello 記錄分析服務 hello 步驟 tooconnect hello Windows 電腦使用 hello Microsoft Monitoring Agent (MMA) 的自訂的版本。"
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 932f7b8c-485c-40c1-98e3-7d4c560876d2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7e15f9eeb0440bd2f6557d7215df701526e4f9aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-windows-computers-toohello-log-analytics-service-in-azure"></a>連接 Windows Azure 中的電腦 toohello 記錄分析服務

本文示範 hello 步驟 tooconnect Windows 電腦在內部部署基礎結構 tooOMS 工作區中使用自訂的 hello Microsoft Monitoring Agent (MMA) 的版本。 您需要 tooinstall，並連線 toosend 資料 toohello 記錄分析服務，且 tooview 和在該資料上的運作，想要使其 tooonboard hello 電腦的所有代理程式。 每個代理程式可以報告 toomultiple 工作區。

您可以使用安裝程式、命令列、或 Azure 自動化中的期望狀態設定 (DSC) 來安裝代理程式。  

>[!NOTE]
在 Azure 中執行的虛擬機器，您可以使用來簡化安裝 hello[虛擬機器擴充功能](log-analytics-azure-vm-extension.md)。

在電腦上透過網際網路連線，hello 代理程式會使用 hello 連接 toohello 網際網路 toosend 資料 tooOMS。 對於沒有網際網路連線的電腦，您可以使用 proxy 或 hello [OMS 閘道](log-analytics-oms-gateway.md)。

連接您的 Windows 電腦 tooOMS 是直接使用三個簡單步驟：

1. 從 hello OMS 入口網站下載 hello 代理程式安裝檔案
2. 安裝 hello 代理程式使用您所選擇的 hello 方法
3. 設定 hello 代理程式，或視需要新增額外的工作區

hello 下列圖表顯示 hello 您 Windows 電腦和 OMS 之間的關聯性之後，您已安裝並設定代理程式。

![oms-direct-agent-diagram](./media/log-analytics-windows-agents/oms-direct-agent-diagram.png)

如果您的 IT 安全性原則不允許您的網路 tooconnect toohello 網際網路上的電腦，您可以設定您的電腦 tooconnect toohello OMS 閘道。 如需詳細資訊以及有關如何 tooconfigure 您的伺服器 toocommunicate 透過 OMS 閘道 toohello OMS 服務，請參閱步驟[連接使用 hello OMS 閘道電腦 tooOMS](log-analytics-oms-gateway.md)。

## <a name="system-requirements-and-required-configuration"></a>系統需求和所需的設定
您安裝或部署代理程式之前，請檢閱下列符合 hello 需求的詳細資料 tooensure hello。

- 您只能在執行 Windows Server 2008 SP 1 或更新版本的電腦或 Windows 7 SP1 上安裝 OMS MMA hello 或更新版本。
- 您需要 Azure 訂用帳戶。  如需詳細資訊，請參閱[開始使用 Log Analytics](log-analytics-get-started.md)。
- 每一部 Windows 電腦必須能夠 tooconnect toohello 網際網路使用 HTTPS 或 toohello OMS 閘道。 此連接可以是直接透過 proxy，或透過 hello OMS 閘道。
- 您可以在獨立電腦、 伺服器和虛擬機器上安裝 OMS MMA hello。 如果您想 tooconnect Azure 託管的虛擬機器 tooOMS，請參閱[連接 Azure 虛擬機器 tooLog 分析](log-analytics-azure-vm-extension.md)。
- hello 代理程式需要的各種資源建立 toouse TCP 連接埠 443。

### <a name="network"></a>網路

Windows 代理程式 tooconnect tooand 向 hello OMS 服務，它們必須存取 toonetwork 資源，包括 hello 連接埠號碼和網域 Url。

- Proxy 伺服器，您需要 hello 資源在代理程式設定中設定適當的 proxy 伺服器的 tooensure。
- 限制存取 toohello 網際網路的防火牆，您的網路工程師必須 tooconfigure 您防火牆 toopermit 存取 tooOMS。 您不需要在代理程式設定中進行任何動作。

hello 下表會顯示通訊所需的資源。

>[!NOTE]
>有部分的下列資源的 hello 提及 Operational Insights，這是供記錄分析先前的名稱。

| 代理程式資源 | 連接埠 | 略過 HTTPS 檢查 |
|---|---|---|
| *.ods.opinsights.azure.com | 443 | 是 |
| *.oms.opinsights.azure.com | 443 | 是 |
| *.blob.core.windows.net | 443 | 是 |
| *.azure-automation.net | 443 | 是 |



## <a name="download-hello-agent-setup-file-from-oms"></a>從 OMS 下載 hello 代理程式安裝檔案
1. 在 hello OMS 入口網站上 hello**概觀**頁面上，按一下 hello**設定**磚。  按一下 hello**連線來源**hello 頂端的索引標籤。  
    ![連接的來源索引標籤](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)
2. 按一下**Windows 伺服器**，然後按一下**下載 Windows 代理程式**適用 tooyour 電腦處理器類型 toodownload hello 設定檔。
3. 在右邊的 hello**工作區識別碼**，按一下 hello 複製圖示，然後貼入 [記事本] 中的 hello 識別碼。
4. 在右邊的 hello**主索引鍵**，按一下 hello 複製圖示，然後貼入 [記事本] 中的 hello 索引鍵。     

## <a name="install-hello-agent-using-setup"></a>Hello 使用安裝代理程式安裝程式
1. 您想 toomanage 的電腦上執行安裝程式 tooinstall hello 代理程式。
2. 在 hello  褖畫惎 頁面上，按一下 **下一步**。
3. 在 hello 授權條款 頁面上，讀取 hello 授權，然後按一下**我同意**。
4. 在 hello 目的地資料夾 頁面上，變更或保留 hello 預設安裝資料夾，然後按一下**下一步**。
5. 在 hello 代理程式安裝選項 頁面上，您可以選擇 tooconnect hello 代理程式 tooAzure 記錄分析 (OMS)，Operations Manager 中，或者可以 hello 選項保留為空白如果您稍後想 tooconfigure hello 代理程式。 按一下 [下一步] 。   
    - 如果您選擇 tooconnect tooAzure 記錄分析 (OMS)，貼上 hello**工作區識別碼**和**（主索引鍵） 的工作區金鑰**hello 前一個程序中複製到 [記事本]，然後再按一下**下一步**。  
        ![貼上工作區識別碼和主索引鍵](./media/log-analytics-windows-agents/connect-workspace.png)
    - 如果您選擇 tooconnect tooOperations 管理員，請輸入 hello**管理群組名稱**，**管理伺服器**名稱，和**管理伺服器連接埠**，然後按一下 **下一步**。 在 hello 代理程式動作帳戶] 頁面上，選擇 [hello 本機系統帳戶或本機網域帳戶，然後按一下**下一步**。  
        ![管理群組設定](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![代理程式動作帳戶](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)

6. 在 hello 準備 tooInstall 頁面上，檢閱您的選擇，然後按一下**安裝**。
7. 在 [hello 組態已順利完成] 頁面上，按一下**完成**。
8. 完成時，hello **Microsoft Monitoring Agent**會出現在**控制台**。 您可以檢閱您的設定，並確認該 hello 代理程式連接的 tooOperational Insights (OMS)。 當連接的 tooOMS hello 代理程式會顯示訊息指出： **hello Microsoft Monitoring Agent 已成功連接 toohello Microsoft Operations Management Suite 服務。**

## <a name="configure-proxy-settings"></a>進行 Proxy 設定

您可以使用下列程序 tooconfigure hello 使用控制台中的 Microsoft Monitoring Agent 的 proxy 設定的 hello。 您需要 toouse 此程序的每一部伺服器。 如果您有許多您需要 tooconfigure 的伺服器，您可能會發現它更容易 toouse 指令碼 tooautomate 此程序。 若是如此，請參閱下一個程序 hello [tooconfigure hello 使用指令碼的 Microsoft Monitoring Agent 的 proxy 設定](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script)。

### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-control-panel"></a>tooconfigure hello 使用控制台中的 Microsoft Monitoring Agent 的 proxy 設定
1. 開啟 [ **控制台**]。
2. 開啟 [ **Microsoft Monitoring Agent**].
3. 按一下 hello **Proxy 設定** 索引標籤。  
    ![[Proxy 設定] 索引標籤](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)
4. 選取**使用 proxy 伺服器**輸入 hello URL 和連接埠號碼，如有需要，類似 toohello 範例所示。 如果您的 proxy 伺服器需要驗證，請輸入 hello 使用者名稱和密碼 tooaccess hello proxy 伺服器。


### <a name="verify-agent-connectivity-toooms"></a>確認代理程式連線能力 tooOMS

您可以輕鬆地確認您的代理程式是否會與使用下列程序的 hello 的 OMS 的通訊：

1.  在 hello hello Windows 代理程式電腦，開啟控制台。
2.  開啟 [Microsoft Monitoring Agent]。
3.  按一下 hello Azure 記錄分析 (OMS) 索引標籤。
4.  在 hello 狀態 資料行，您應該會看到該 hello 代理程式已成功連接 toohello Operations Management Suite 服務。

![代理程式已連線](./media/log-analytics-windows-agents/mma-connected.png)


### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-a-script"></a>tooconfigure hello 使用指令碼的 Microsoft Monitoring Agent 的 proxy 設定
複製下列範例，資訊特定 tooyour 環境以更新、 儲存 PS1 副檔名為檔案名稱，然後再執行 hello 指令碼直接連接 toohello OMS 服務的每一部電腦上的 hello。

    param($ProxyDomainName="http://proxy.contoso.com:80", $cred=(Get-Credential))

    # First we get hello Health Service configuration object.  We need toodetermine if we
    #have hello right update rollup with hello API we need.  If not, no need toorun hello rest of hello script.
    $healthServiceSettings = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'

    $proxyMethod = $healthServiceSettings | Get-Member -Name 'SetProxyInfo'

    if (!$proxyMethod)
    {
         Write-Output 'Health Service proxy API not present, will not update settings.'
         return
    }

    Write-Output "Clearing proxy settings."
    $healthServiceSettings.SetProxyInfo('', '', '')

    $ProxyUserName = $cred.username

    Write-Output "Setting proxy too$ProxyDomainName with proxy username $ProxyUserName."
    $healthServiceSettings.SetProxyInfo($ProxyDomainName, $ProxyUserName, $cred.GetNetworkCredential().password)



## <a name="install-hello-agent-using-hello-command-line"></a>Hello 使用安裝代理程式 hello 命令列
- 修改，然後使用 hello 遵循範例 tooinstall hello 代理程式使用 hello 命令列。 hello 範例會執行完全無訊息安裝。

    >[!NOTE]
    如果您想 tooupgrade 代理程式，您需要 toouse hello 記錄分析指令碼應用程式開發介面。 請參閱下一個區段 tooupgrade hello 代理程式。

    ```dos
    MMASetup-AMD64.exe /Q:A /R:N /C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1"
    ```

hello 代理程式是使用 IExpress 做為其自我解壓縮程式使用 hello`/c`命令。 您可以看到在 hello 命令列參數[IExpress 的命令列參數](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages)，然後更新會 hello 範例 toosuit 您的需求。

|MMA 專屬選項                   |注意事項         |
|---------------------------------------|--------------|
|ADD_OPINSIGHTS_WORKSPACE               | 1 = 設定 hello 代理程式 tooreport tooa 工作區                |
|OPINSIGHTS_WORKSPACE_ID                | Hello 工作區 tooadd 的工作區識別碼 (guid)                    |
|OPINSIGHTS_WORKSPACE_KEY               | 工作區的索引鍵使用的 tooinitially 向 hello 工作區 |
|OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE  | 指定 hello hello 工作區所在位置的雲端環境 <br> 0 = Azure 商業雲端 (預設值) <br> 1 = Azure Government |
|OPINSIGHTS_PROXY_URL               | Hello proxy toouse URI |
|OPINSIGHTS_PROXY_USERNAME               | 使用者名稱 tooaccess 驗證的 proxy |
|OPINSIGHTS_PROXY_PASSWORD               | 密碼 tooaccess 驗證的 proxy |

>[!NOTE]
IExpress 的 tooavoid 達到 hello 命令列的長度限制 hello 代理程式安裝與設定任何工作區，然後再使用 hello 工作區的 指令碼 tooset 組態。

>[!NOTE]
如果您收到`Command line option syntax error.`時使用 hello`OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE`參數，您可以使用下列因應措施的 hello:
```dos
MMASetup-AMD64.exe /C /T:.\MMAExtract
cd .\MMAExtract
setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1
```

## <a name="add-a-workspace-using-a-script"></a>使用指令碼來新增工作區
加入工作區中以 hello 下列範例使用 hello 記錄分析代理程式的指令碼 API:

```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey)
$mma.ReloadConfiguration()
```

tooadd 美國政府，下列指令碼範例使用 hello 的 Azure 中的工作區：
```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey, 1)
$mma.ReloadConfiguration()
```

>[!NOTE]
如果您曾經使用 hello 命令列或指令碼先前 tooinstall 或設定 hello 代理程式，`EnableAzureOperationalInsights`取代為`AddCloudWorkspace`。

## <a name="install-hello-agent-using-dsc-in-azure-automation"></a>安裝在 Azure 自動化中使用 DSC 的 hello 代理程式

您可以使用下列指令碼範例 tooinstall hello 代理程式在 Azure 自動化中使用 DSC 的 hello。 hello 範例安裝 hello 64 位元代理程式，由 hello`URI`值。 您也可以使用 hello 32 位元版本來取代 hello URI 值。 這兩個版本的 hello Uri 是：

- Windows 64 位元代理程式 - https://go.microsoft.com/fwlink/?LinkId=828603
- Windows 32 位元代理程式 - https://go.microsoft.com/fwlink/?LinkId=828604


>[!NOTE]
此程序和指令碼範例不會升級現有的代理程式。

1. 匯入 hello xPSDesiredStateConfiguration DSC 模組從[http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration)至 Azure 自動化。  
2.  建立 Azure 自動化的 *OPSINSIGHTS_WS_ID* 和 *OPSINSIGHTS_WS_KEY* 變數資產。 設定*OPSINSIGHTS_WS_ID* tooyour OMS 記錄分析工作區識別碼和設定*OPSINSIGHTS_WS_KEY* toohello 工作區的主索引鍵。
3.  使用下列指令碼，並將它儲存為 MMAgent.ps1 hello
4.  修改，然後使用下列範例 tooinstall hello 代理程式在 Azure 自動化中使用 DSC 的 hello。 匯入 MMAgent.ps1 Azure 自動化使用 hello Azure 自動化介面或指令程式。
5.  請指派節點 toohello 設定。 15 分鐘內，hello 節點會檢查其組態和 hello MMA 推入 toohello 節點。

```PowerShell
Configuration MMAgent
{
    $OIPackageLocalPath = "C:\MMASetup-AMD64.exe"
    $OPSINSIGHTS_WS_ID = Get-AutomationVariable -Name "OPSINSIGHTS_WS_ID"
    $OPSINSIGHTS_WS_KEY = Get-AutomationVariable -Name "OPSINSIGHTS_WS_KEY"


    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    Node OMSnode {
        Service OIService
        {
            Name = "HealthService"
            State = "Running"
            DependsOn = "[Package]OI"
        }

        xRemoteFile OIPackage {
            Uri = "https://go.microsoft.com/fwlink/?LinkId=828603"
            DestinationPath = $OIPackageLocalPath
        }

        Package OI {
            Ensure = "Present"
            Path  = $OIPackageLocalPath
            Name = "Microsoft Monitoring Agent"
            ProductId = "8A7F2C51-4C7D-4BFD-9014-91D11F24AAE2"
            Arguments = '/C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=' + $OPSINSIGHTS_WS_ID + ' OPINSIGHTS_WORKSPACE_KEY=' + $OPSINSIGHTS_WS_KEY + ' AcceptEndUserLicenseAgreement=1"'
            DependsOn = "[xRemoteFile]OIPackage"
        }
    }
}


```

### <a name="get-hello-latest-productid-value"></a>取得最新 ProductId 值 hello

hello`ProductId value`在 hello MMAgent.ps1 指令碼是唯一的 tooeach 代理程式版本。 每個代理程式的更新的版本發行時，變更 hello ProductId 值。 因此，當 hello ProductId 變更 hello 未來時，您可以找到 hello 代理程式版本使用簡單的指令碼。 您擁有 hello 測試伺服器上安裝最新的代理程式版本之後，您可以使用下列指令碼 tooget hello 安裝 ProductId 值 hello。 您可以使用 hello 最新的產品識別碼值，更新 hello MMAgent.ps1 指令碼中的 hello 值。

```PowerShell
$InstalledApplications  = Get-ChildItem hklm:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall


foreach ($Application in $InstalledApplications)

{

     $Key = Get-ItemProperty $Application.PSPath

     if ($Key.DisplayName -eq "Microsoft Monitoring Agent")

     {

        $Key.DisplayName

        Write-Output ("Product ID is: " + $Key.PSChildName.Substring(1,$Key.PSChildName.Length -2))

     }

}  
```

## <a name="configure-an-agent-manually-or-add-additional-workspaces"></a>手動設定代理程式，或新增額外的工作區
如果您已安裝的代理程式但未設定或者您想 hello 代理程式 tooreport toomultiple 工作區，您可以使用下列資訊 tooenable 代理程式的 hello 或重新設定它。 設定 hello 代理程式之後，它會註冊 hello 代理程式服務，並將獲得所需的組態資訊及包含解決方案資訊的管理組件。

1. 您已安裝 Microsoft Monitoring Agent hello 之後，請開啟**控制台**。
2. 開啟**Microsoft Monitoring Agent**然後按一下hello **Azure 記錄分析 (OMS)**  索引標籤。   
3. 按一下**新增**tooopen hello**新增記錄分析工作區**方塊。
4. 貼上 hello**工作區識別碼**和**（主索引鍵） 的工作區金鑰**您在先前的程序，您想 tooadd，然後按一下 「 hello 」 工作區中複製到 [記事本]**確定**.  
    ![設定 Operational Insights](./media/log-analytics-windows-agents/add-workspace.png)

從 hello 代理程式所監視的電腦收集資料之後，hello OMS 監視的電腦數目會出現在 hello OMS 入口網站上 hello**連線來源**索引標籤中**設定**為**伺服器連接**。


## <a name="toodisable-an-agent"></a>toodisable 代理程式
1. 安裝之後 hello 代理程式，開啟**控制台**。
2. 開啟 Microsoft Monitoring Agent，然後按一下hello **Azure 記錄分析 (OMS)**  索引標籤。
3. 選取工作區，然後按一下移除 。 對其他所有工作區重複此步驟。


## <a name="optionally-configure-agents-tooreport-tooan-operations-manager-management-group"></a>（選擇性） 設定代理程式 tooreport tooan Operations Manager 管理群組

如果您使用 Operations Manager 在您的 IT 基礎結構，您也可以使用 hello MMA 代理程式與 Operations Manager 代理程式。

### <a name="tooconfigure-mma-agents-tooreport-tooan-operations-manager-management-group"></a>tooconfigure MMA 代理程式 tooreport tooan Operations Manager 管理群組
1.  Hello hello 代理程式安裝所在的電腦，開啟**控制台**。  
2.  開啟**Microsoft Monitoring Agent**然後按一下hello **Operations Manager**  索引標籤。  
    ![Microsoft 監視代理程式 Operations Manager 索引標籤](./media/log-analytics-windows-agents/om-mg01.png)
3.  如果 Operations Manager 伺服器已與 Active Directory 整合，請按一下 [自動更新來自 AD DS 的管理群組指派] 。
4.  按一下**新增**tooopen hello**新增管理群組** 對話方塊。  
    ![Microsoft 監視代理程式新增管理群組](./media/log-analytics-windows-agents/oms-mma-om02.png)
5.  在**管理群組名稱** 方塊中，輸入 hello 名稱的管理群組。
6.  在 [hello**主要管理伺服器**] 方塊中，輸入 hello 電腦名稱的 hello 主要管理伺服器。
7.  在 hello**管理伺服器連接埠**方塊中，型別 hello TCP 通訊埠編號。
8.  在下**代理程式動作帳戶**，選擇 hello 本機系統帳戶或本機網域帳戶。
9.  按一下**確定**tooclose hello**新增管理群組**對話方塊，然後按一下**確定**tooclose hello **Microsoft Monitoring Agent 內容** 對話方塊。


## <a name="next-steps"></a>後續步驟

- [新增記錄分析解決方案從 hello 解決方案資源庫](log-analytics-add-solutions.md)tooadd 功能和收集資料。
