---
title: "aaaAzure 自動化 Hybrid Runbook Worker |Microsoft 文件"
description: "本文章提供有關安裝和使用這是一項功能可讓您 toorun runbook 在電腦本機資料中心或雲端提供者中的 Azure 自動化 Hybrid Runbook Worker 的資訊。"
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 06227cda-f3d1-47fe-b3f8-436d2b9d81ee
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: magoedte;bwren
ms.openlocfilehash: ccee35e8324149a79ff692a867e5ce7801299bcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automate-resources-in-your-data-center-or-cloud-with-hybrid-runbook-worker"></a>使用混合式 Runbook 背景工作角色將資料中心內或雲端的資源自動化
在 Azure 自動化 Runbook 無法存取在其他雲端或內部部署環境中的資源，因為其在 hello Azure 雲端中執行。  hello Azure 自動化 Hybrid Runbook Worker 功能可讓您 toorun runbook 直接在 hello 裝載 hello 角色的電腦上也可以根據 hello 環境 toomanage 中的資源的本機資源。 Runbook 會儲存和管理 Azure 自動化中，然後傳遞 tooone 或其他指定的電腦。  

下列映像的 hello 這項功能如下所示：<br>  

![混合式 Runbook 背景工作概觀](media/automation-offering-get-started/automation-infradiagram-networkcomms.png)

Hello 混合式 Runbook 背景工作角色和部署考量的技術概觀，請參閱[自動化架構概觀](automation-offering-get-started.md#automation-architecture-overview)。    

## <a name="hybrid-runbook-worker-groups"></a>混合式 Runbook 背景工作群組
每個混合式 Runbook 背景工作是您指定當您安裝 hello 代理程式的混合式 Runbook 背景工作群組的成員。  群組可包含單一代理程式，但您可以在群組中安裝多個代理程式以獲得高可用性。

當您在 Hybrid Runbook Worker 上啟動 runbook 時，您會指定其執行所在的 hello 群組。  hello 群組成員的 hello 判斷哪一個背景工作 services hello 要求。  您無法指定特定的背景工作。

## <a name="relationship-tooservice-management-automation"></a>關聯性 tooService Management Automation
[服務管理自動化 (SMA)](https://technet.microsoft.com/library/dn469260.aspx)可讓您 toorun hello Azure 自動化中您的本機資料中心所支援的相同 runbook。 SMA 通常與 Windows Azure Pack 一同部署，因為 Windows Azure Pack 包含 SMA 管理的圖形化介面。 不同於 Azure 自動化中，SMA 需要本機安裝，包括 web 伺服器 toohost hello API、 資料庫 toocontain runbook 和 SMA 設定和 Runbook Worker tooexecute runbook 工作。 Azure 自動化會提供這些 hello 雲端中的服務，並只會要求您在本機環境 toomaintain hello Hybrid Runbook Worker。

如果您是現有 SMA 使用者時，您可以移動您有任何變更，使用與混合式 Runbook 背景工作的 runbook tooAzure 自動化 toobe 假設他們中所述執行自己的驗證 tooresources[混合式 Runbook 上執行的 runbook背景工作](automation-hrw-run-runbooks.md)。  Hello hello 可能會提供驗證的 hello runbook hello 背景工作伺服器上的服務帳戶內容中執行的 SMA 中的 Runbook。

您可以使用下列準則 toodetermine 是否為更適合您需求的 Azure 自動化 Hybrid Runbook Worker 或 Service Management Automation 的 hello。

* SMA 需要其基礎的元件是否需要圖形化管理介面所連接的 tooWindows Azure Pack 的本機安裝。 相較於 Azure 自動化，這需要更多的本機資源和更高的維護成本；Azure 自動化只需要在本機 Runbook 背景工作角色上安裝代理程式。 hello 代理程式受 Operations Management Suite，進一步減少維護成本。
* Azure 自動化 hello 雲端中儲存其 runbook，並傳遞 tooon 內部部署混合式 Runbook 背景工作。 如果您的安全性原則不允許這種行為，您應該使用 SMA。
* SMA 隨附於 System Center，因此需要 System Center 2012 R2 授權。 Azure 自動化是採用分層式的訂用帳戶模型。
* Azure 自動化具備 SMA 中並未提供的圖形 Runbook 等進階功能。

## <a name="installing-hello-windows-hybrid-runbook-worker"></a>安裝 hello Windows Hybrid Runbook Worker 

tooinstall 和設定 Windows 混合式 Runbook 背景工作，，有兩種方法。  hello 建議的方法使用的自動化 runbook toocompletely 自動化所需的 hello 程序 tooconfigure Windows 電腦。  hello 第二種方法是下列逐步程序 toomanually 安裝，並設定 hello 角色。  

> [!NOTE]
> toomanage hello 伺服器支援 hello 混合式 Runbook 背景工作角色的預期狀態設定 (DSC) 設定，您需要 tooadd 它們成為 DSC 節點。  如需有關讓它們上線以透過 DSC 進行管理的詳細資訊，請參閱[讓機器上線以透過 Azure 自動化 DSC 進行管理](automation-dsc-onboarding.md)。           
><br>
>如果您啟用 hello[更新管理解決方案](../operations-management-suite/oms-solution-update-management.md)，任何 Windows 電腦連接的 tooyour OMS 工作區會自動設定為包含在此解決方案 Hybrid Runbook Worker toosupport runbook。  不過，它不會向您已在自動化帳戶中定義的任何 Hybrid Worker 群組註冊。  hello 電腦可新增 tooa Hybrid Runbook Worker 群組您的自動化帳戶 toosupport 自動化 runbook 中，只要您使用相同帳戶執行 hello 解決方案和混合式 Runbook 背景工作群組成員資格的 hello。  這項功能已加入 tooversion 7.2.12024.0 的 hello Hybrid Runbook Worker。  

檢閱下列有關 hello 資訊的 hello[硬體和軟體需求](automation-offering-get-started.md#hybrid-runbook-worker)和[準備您的網路所需的資訊](automation-offering-get-started.md#network-planning)在開始部署 Hybrid Runbook Worker 之前。  您已成功部署 runbook worker 後，請檢閱[混合式 Runbook 背景工作上執行的 runbook](automation-hrw-run-runbooks.md) toolearn 如何 tooconfigure runbook tooautomate 處理您的內部部署資料中心或其他雲端環境中。  
 
### <a name="automated-deployment"></a>自動化部署

執行 hello 下列步驟 tooautomate hello 安裝和設定 hello Windows 混合式背景工作角色。  

1. 下載 hello*新增 OnPremiseHybridWorker.ps1*指令碼從 hello [PowerShell 資源庫](https://www.powershellgallery.com/packages/New-OnPremiseHybridWorker/1.0/DisplayScript)直接從 hello 執行 hello 混合式 Runbook 背景工作角色的電腦或另一部電腦，在您環境並將它複製 toohello 背景工作。  

    hello*新增 OnPremiseHybridWorker.ps1*指令碼需要下列參數執行期間的 hello:

  * *AutomationAccountName* （必要）-hello 您的自動化帳戶名稱。  
  * *ResourceGroupName* （必要）-hello hello 與您的自動化帳戶相關聯的資源群組名稱。  
  * *HybridGroupName* （必要）-您指定為目標，以支援此案例中的 hello runbook 的混合式 Runbook 背景工作群組 hello 名稱。 
  *  *SubscriptionID* （必要）-hello 中為您的自動化帳戶的 Azure 訂用帳戶 Id。
  *  *WorkspaceName* （選用）-hello OMS 工作區名稱。  如果您沒有 OMS 工作區，hello 指令碼建立，並設定其中一個。  

     > [!NOTE]
     > 目前是 hello 與 OMS 整合的支援只有自動化區域-**澳洲東南部**，**美國東部 2**，**東南亞**，和**西歐洲**。  如果您的自動化帳戶不在其中一個這些區域中，hello 指令碼會建立 OMS 工作區，但是它會警告您，它不能將它們連結在一起。
     > 
2. 在您的電腦上啟動**Windows PowerShell**從 hello**啟動**畫面以系統管理員模式。  
3. 從 hello PowerShell 命令列殼層，瀏覽 toohello 資料夾，其中包含您下載並執行變更 hello 參數的值 「 hello 」 指令碼*-AutomationAccountName*， *-ResourceGroupName*， *-HybridGroupName*， *-SubscriptionId*，和*-WorkspaceName*。

     > [!NOTE] 
     > 您是提示的 tooauthenticate 與 Azure，在您執行 hello 指令碼。  您**必須**hello 訂用帳戶系統管理員角色的成員且 hello 訂用帳戶的共同管理員的帳戶登入。  
     >  
    
        .\New-OnPremiseHybridWorker.ps1 -AutomationAccountName <NameofAutomationAccount> `
        -ResourceGroupName <NameofOResourceGroup> -HybridGroupName <NameofHRWGroup> `
        -SubscriptionId <AzureSubscriptionId> -WorkspaceName <NameOfOMSWorkspace>

4. 會提示的 tooagree tooinstall **NuGet** ，而且提示的 tooauthenticate 與您的 Azure 認證。<br><br> ![Execution of New-OnPremiseHybridWorker script](media/automation-hybrid-runbook-worker/new-onpremisehybridworker-scriptoutput.png)

5. Hello 指令碼完成後，hello 混合式背景工作群組 刀鋒視窗會顯示 hello 新的群組和成員的數目，或如果現有的群組，就會遞增 hello 成員數目。  您可以從 hello hello 清單中選取 hello 群組**Hybrid Worker 群組**刀鋒視窗，然後選取 hello **Hybrid Worker**磚。  在 hello **Hybrid Worker**刀鋒視窗中，您會看到列出的 hello 群組的每個成員。  

### <a name="manual-deployment"></a>手動部署 
為您的自動化環境一次執行 hello 前兩個步驟，然後重複 hello 剩餘的每個背景工作電腦的步驟。

#### <a name="1-create-operations-management-suite-workspace"></a>1.建立 Operations Management Suite 工作區
如果您還沒有 Operations Management Suite 工作區，請使用[管理您的工作區](../log-analytics/log-analytics-manage-access.md)中的指示建立工作區。 如果您已經有工作區，可以使用現有的工作區。

#### <a name="2-add-automation-solution-toooperations-management-suite-workspace"></a>2.加入自動化方案 tooOperations Management Suite 工作區
解決方案會將功能 tooOperations Management Suite 的資訊。  hello 自動化解決方案新增功能，包括支援 Hybrid Runbook Worker Azure 自動化。  當您新增 hello 方案 tooyour 工作區時，它會自動將推入關閉 worker 元件 toohello 代理程式電腦 hello 下一個步驟中，您將安裝的。

請遵循指示 hello [tooadd 方案使用 hello 解決方案資源庫](../log-analytics/log-analytics-add-solutions.md)tooadd hello**自動化**方案 tooyour Operations Management Suite 工作區。

#### <a name="3-install-hello-microsoft-monitoring-agent"></a>3.安裝 Microsoft Monitoring Agent hello
Microsoft Monitoring Agent hello 連接電腦 tooOperations Management Suite 的資訊。  當您在內部部署電腦上安裝 hello 代理程式，並連接 tooyour 工作區時，它將會自動下載所需的 Hybrid Runbook Worker 的 hello 元件。

請遵循指示 hello[連接的 Windows 電腦 tooLog 分析](../log-analytics/log-analytics-windows-agents.md)tooinstall hello hello 在內部部署電腦上的代理程式 」。  您可以重複此程序的多個電腦 tooadd 多個工作者 tooyour 環境。

當 hello 代理程式已成功連接 tooOperations Management Suite 的資訊時，它就會列在 hello**連線來源**hello Operations Management Suite 索引標籤**設定**窗格。  您可以確認它具有名為的資料夾時，該 hello 代理程式已正確下載 hello 自動化解決方案**AzureAutomationFiles** C:\Program Files\Microsoft Monitoring Agent\Agent 中。  tooconfirm hello 版的 hello Hybrid Runbook Worker，您可以瀏覽 tooC:\Program Files\Microsoft 監視 Agent\Agent\AzureAutomation\ 並註記 hello \\*版本*子資料夾。   

#### <a name="4-install-hello-runbook-environment-and-connect-tooazure-automation"></a>4.安裝 hello runbook 環境，而且連接 tooAzure 自動化
當您將代理程式 tooOperations Management Suite 時，hello 自動化解決方案將 hello **HybridRegistration** PowerShell 模組，其中包含 hello **Add-hybridrunbookworker** cmdlet。  您在 hello 電腦上使用這個指令程式 tooinstall hello runbook 環境，並向 Azure 自動化。

系統管理員模式開啟的 PowerShell 工作階段，並執行下列命令 tooimport hello 模組 hello。

    cd "C:\Program Files\Microsoft Monitoring Agent\Agent\AzureAutomation\<version>\HybridRegistration"
    Import-Module HybridRegistration.psd1

然後執行 hello **Add-hybridrunbookworker** cmdlet 使用 hello，請使用下列語法：

    Add-HybridRunbookWorker –GroupName <String> -EndPoint <Url> -Token <String>

您可以取得從 hello 這個指令程式所需的 hello 資訊**管理金鑰**hello Azure 入口網站中的刀鋒視窗。  開啟此刀鋒視窗選取 hello**金鑰**選項從 hello**設定**刀鋒視窗，在您的自動化帳戶。

![混合式 Runbook 背景工作概觀](media/automation-hybrid-runbook-worker/elements-panel-keys.png)

* **GroupName** hello hello 混合式 Runbook 背景工作群組名稱。 如果此群組已經存在 hello 自動化帳戶中，hello 目前的電腦會加入 tooit。  如果尚不存在，則會加入。
* **端點**為 hello **URL**欄位 hello**管理金鑰**刀鋒視窗。
* **語彙基元**為 hello**主要存取金鑰**在 hello**管理金鑰**刀鋒視窗。  

使用 hello **-Verbose**參數搭配**Add-hybridrunbookworker** tooreceive 詳細 hello 安裝的相關資訊。

#### <a name="5-install-powershell-modules"></a>5.安裝 PowerShell 模組
Runbook 可以使用任何 hello 活動與 hello Azure 自動化環境中安裝的模組中定義的 cmdlet。  這些模組不會自動 tooon 內部部署的電腦，因此您必須手動安裝。  hello 例外狀況為 hello Azure 模組，提供 Azure 自動化所有 Azure 服務和活動存取 toocmdlets 預設會安裝。

Hello hello Hybrid Runbook Worker 功能主要用途是 toomanage 本機資源，因為您很可能會需要 tooinstall hello 模組可支援這些資源。  您可以使用參照太[安裝模組](http://msdn.microsoft.com/library/dd878350.aspx)如需有關安裝 Windows PowerShell 模組。  安裝的模組必須在 PSModulePath 環境變數所參考，以便自動匯入的 hello 混合式背景工作的位置。  如需詳細資訊，請參閱[修改 hello PSModulePath 安裝路徑](https://msdn.microsoft.com/library/dd878326%28v=vs.85%29.aspx)。 

## <a name="removing-hybrid-runbook-worker"></a>移除 Hybrid Runbook Worker 
您可以從群組中移除一或多個混合式 Runbook 背景工作，或您可以移除 hello 群組，根據您的需求。  tooremove Hybrid Runbook Worker 在內部部署電腦上，執行下列步驟的 hello。

1. 在 hello Azure 入口網站，瀏覽 tooyour 自動化帳戶。  
2. 從 hello**設定**刀鋒視窗中，選取**金鑰**並記下 hello 欄位值為**URL**和**主要存取金鑰**。  Hello 下一個步驟中需要這項資訊。
3. 以系統管理員模式開啟的 PowerShell 工作階段，然後執行 hello 下列命令- `Remove-HybridRunbookWorker -url <URL> -key <PrimaryAccessKey>`。  使用 hello **-Verbose**切換 hello 移除程序的詳細資訊記錄。

> [!NOTE]
> 這不會移除 Microsoft Monitoring Agent hello hello 電腦，只有 hello 功能和 hello 混合式 Runbook 背景工作角色的組態。  

## <a name="remove-hybrid-worker-groups"></a>移除混合式背景工作角色群組
tooremove 群組，您必須先從使用 hello 程序之前，顯示 hello 群組成員的每部電腦的 tooremove hello Hybrid Runbook Worker，則執行下列步驟 tooremove hello 群組 hello。  

1. 開啟 hello 自動化帳戶中的 hello Azure 入口網站。
2. 選取 hello **Hybrid Worker 群組**磚在 hello **Hybrid Worker 群組**刀鋒視窗中，您想 toodelete 選取 hello 群組。  選取 hello 特定群組之後, hello **Hybrid worker 群組**屬性刀鋒視窗會顯示。<br> ![Hybrid Runbook 背景工作角色群組刀鋒視窗](media/automation-hybrid-runbook-worker/automation-hybrid-runbook-worker-group-properties.png)   
3. 在 hello 屬性刀鋒視窗中的 hello 選取的群組，按一下 **刪除**。  會顯示訊息詢問您 tooconfirm 此動作，選取**是**您是否確定要 tooproceed。<br> ![建立群組確認對話方塊](media/automation-hybrid-runbook-worker/automation-hybrid-runbook-worker-confirm-delete.png)<br> 此程序可能需要幾秒 toocomplete，而且您可以追蹤在其進度**通知**hello 功能表。  

## <a name="troubleshooting"></a>疑難排解 
hello Hybrid Runbook Worker 取決於 hello 與自動化帳戶 tooregister hello 工作者的 Microsoft Monitoring Agent toocommunicate、 接收 runbook 作業，以及報告狀態。 如果註冊的 hello 背景工作失敗，以下是 hello 錯誤的一些可能的原因：  

1. hello 混合式背景工作會在 proxy 或防火牆後面。  
    確認 hello 電腦具有對外存取 too*.azure automation.net 連接埠 443。  

2. hello 電腦 hello 混合式背景工作上執行小於比 hello 最低硬體[需求](automation-offering-get-started.md#hybrid-runbook-worker)。  
    執行的 hello 應該符合 Hybrid Runbook Worker 的電腦 hello 最低硬體需求，再指定它 toohost 這項功能。 否則，根據 hello 資源使用的其他背景處理序和執行期間，runbook 所造成的競爭情形，hello 電腦會變得過度使用，並會造成 runbook 作業延遲或逾時。
   請確認指定 toorun hello Hybrid Runbook Worker 功能 hello 電腦符合 hello 最低硬體需求。  若是如此，監視 CPU 和記憶體使用率 toodetermine Windows hello 的混合式 Runbook 背景工作處理序的效能之間的任何相互關聯。  如果沒有記憶體或 CPU 不足的壓力，這可能表示 hello 需要 tooupgrade 或加入額外的處理器或增加記憶體 tooaddress hello 資源瓶頸並解決 hello 錯誤。 或者，選取不同的計算資源可支援 hello 最小需求並縮放工作負載需求指出是必要的增加時。
    
3. hello Microsoft Monitoring Agent 服務未執行。  
    如果 hello Microsoft 監視代理程式 Windows 服務未執行，這可防止 hello Hybrid Runbook Worker Azure 自動化與通訊。  確認 hello 代理程式正在執行輸入下列命令在 PowerShell 中的 hello: `get-service healthservice`。  如果 hello 服務已停止，請輸入下列命令在 PowerShell toostart hello 服務中的 hello: `start-service healthservice`。  

4. 在 hello**應用程式和服務 Logs\Operations 管理員**事件記錄檔，您會看到事件位於 4502 和 EventMessage 包含**Microsoft.EnterpriseManagement.HealthService.AzureAutomation.HybridAgent**以下列說明 hello: *hello 服務所提供的 hello 憑證<wsid>。 oms.opinsights.azure.com 並非由 Microsoft 服務所使用的憑證授權單位發行。請如果在執行任何會攔截 TLS/SSL 通訊的 proxy，連絡您的網路系統管理員 toosee。hello 文章 kb3126513 內另提供的連線問題的其他疑難排解資訊。*
    這可能被因您 proxy 或網路防火牆 blockking 通訊 tooMicrosoft Azure。  確認 hello 電腦具有對外存取 too*.azure automation.net 連接埠 443。

記錄檔儲存每一個混合式背景工作角色本機的 C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes 中。  您可以檢查是否有任何警告或錯誤事件寫入 toohello**應用程式和服務 Logs\Microsoft SMA\Operations**和**應用程式和服務 Logs\Operations 管理員**事件記錄檔表示連線或其他問題影響的 hello 角色 tooAzure 自動化或問題的上架到執行正常作業時。  

## <a name="next-steps"></a>後續步驟
檢閱[混合式 Runbook 背景工作上執行的 runbook](automation-hrw-run-runbooks.md) toolearn 如何 tooconfigure runbook tooautomate 處理您的內部部署資料中心或其他雲端環境中。
