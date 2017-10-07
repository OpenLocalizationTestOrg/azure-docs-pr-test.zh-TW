---
title: "在 OMS 中的管理解決方案 aaaUpdate |Microsoft 文件"
description: "本文是預定的 toohelp 您了解如何 toouse 這個方案 toomanage 更新為 Windows 和 Linux 電腦。"
services: operations-management-suite
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: e33ce6f9-d9b0-4a03-b94e-8ddedcc595d2
ms.service: operations-management-suite
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/27/2017
ms.author: magoedte
ms.openlocfilehash: 2dd321913bf049ab1996fd60a2f74b8417084dcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="update-management-solution-in-oms"></a>OMS 中的更新管理方案

![更新管理符號](./media/oms-solution-update-management/update-management-symbol.png)

hello 在 OMS 中的更新管理解決方案可讓您 toomanage 作業系統安全性更新為 Windows 和 Linux 電腦部署在 Azure 中，內部部署環境或其他雲端提供者。  快速評估 hello 狀態的所有代理程式電腦上可用的更新和管理 hello 安裝伺服器所需的更新程序。


## <a name="solution-overview"></a>解決方案概觀
OMS 所管理的電腦使用執行評估和更新部署的 hello 下列：

* 適用於 Windows 或 Linux 的 OMS 代理程式
* 適用於 Linux 的 PowerShell 預期狀態組態 (DSC)
* 自動化 Hybrid Runbook Worker
* 適用於 Windows 電腦的 Microsoft Update 或 Windows Server Update Services

hello 下列圖表顯示以 hello 解決方案如何評估及套用安全性更新 tooall hello 行為和資料流程的概念檢視連接 Windows Server 和 Linux 電腦工作區中。    

#### <a name="windows-server"></a>Windows Server
![Windows Server 更新管理程序流程](media/oms-solution-update-management/update-mgmt-windows-updateworkflow.png)

#### <a name="linux"></a>Linux
![Linux 更新管理程序流程](media/oms-solution-update-management/update-mgmt-linux-updateworkflow.png)

Hello 電腦執行的更新相容性掃描之後，hello OMS 代理程式會將大量 tooOMS 中的 hello 資訊轉送。 視窗的電腦上，hello 相容性掃描是預設執行每隔 12 小時。  此外 hello Microsoft Monitoring Agent (MMA) 是否重新啟動、 先前 tooupdate 安裝 15 分鐘內，並在更新安裝之後，就會起始 toohello 掃描排程在內 hello 的更新相容性的掃描。  與 Linux 電腦，hello 相容性掃描會執行每 3 個小時預設值，而如果 hello MMA 代理程式重新啟動 15 分鐘內起始相容性掃描。  

hello 相容性資訊然後處理及彙總在 hello 儀表板包含在 hello 方案或可搜尋使用使用者定義或預先-定義之查詢。  hello 方案報告 hello 如何保持最新狀態根據哪些來源所使用的設定的 toosynchronize 電腦。  如果 hello Windows 的電腦是根據當 WSUS 上次同步處理與 Microsoft Update 的設定的 tooreport tooWSUS hello 結果可能會與 Microsoft 更新的示範中不同。  hello 與 Linux 電腦的相同設定 tooreport tooa 本機儲存機制與公用儲存機制。   

您可以部署，並在需要藉由建立排程的部署的 hello 更新的電腦上安裝軟體更新。  更新分類為*選擇性*不包含在 Windows 電腦的 hello 部署範圍只需要更新。  hello 排程的部署定義哪些目標電腦將會收到 hello 適用的更新，藉由明確指定的電腦，或選取[電腦群組](../log-analytics/log-analytics-computer-groups.md)，根據一組特定的記錄搜尋電腦。  您也指定排程 tooapprove，並指定一段時間時允許更新 toobe 內安裝。  在 Azure 自動化中，會由 Runbook 安裝更新。  您無法檢視這些 Runbook，而它們也不需要任何設定。  建立更新的部署時，它會建立指定的排程，開始在 hello 主機更新 runbook hello 包含電腦的時間。  這個主要 Runbook 會在每個代理程式上啟動子 Runbook，以安裝必要的更新。       

在 hello 指定日期和時間在 hello 更新部署，hello 目標電腦會以平行方式執行 hello 部署。  掃描正在第一次執行的 tooverify hello 更新是否仍需要並進行安裝。  請務必 toonote WSUS 用戶端電腦，如果 hello 更新未核准 WSUS，hello 更新部署中將會失敗。  hello 的 hello 套用更新的結果會被轉送 tooOMS toobe 處理，並摘要說明在 hello 儀表板或 hello 搜尋 hello 事件。     

## <a name="prerequisites"></a>必要條件
* hello 方案支援針對 Windows Server 2008 及更新版本，執行的更新評估，並更新部署針對 Windows Server 2008 R2 SP1 和更新版本。  不支援「伺服器核心」和「Nano 伺服器」安裝選項。

    > [!NOTE]
    > 支援部署更新 tooWindows Server 2008 R2 SP1 需要.NET Framework 4.5 及 WMF 5.0 或更新版本。
    >  
* 不支援 Windows 用戶端作業系統。  
* Windows 代理程式必須設定的 toocommunicate 與 Windows Server Update Services (WSUS) 伺服器，或具有存取 tooMicrosoft 更新。  

    > [!NOTE]
    > hello Windows 代理程式無法管理同時 System Center Configuration Manager。  
    >
* CentOS 6 (x86/x64) 和 7 (x64)  
* Red Hat Enterprise 6 (x86/x64) 和 7 (x64)  
* SUSE Linux Enterprise Server 11 (x86/x64) 和 12 (x64)  
* Ubuntu 12.04 LTS 和更新的 x86/x64   
    > [!NOTE]  
    > 在 Ubuntu，在維護期間以外所套用的 tooavoid 更新重新設定自動安裝升級套件 toodisable 自動更新。 如需詳細資訊 tooconfigure，請參閱[hello Ubuntu Server 指南中的自動更新主題](https://help.ubuntu.com/lts/serverguide/automatic-updates.html)。

* Linux 代理程式必須存取 tooan 更新存放庫。  

    > [!NOTE]
    > OMS Agent for Linux 設定 tooreport toomultiple OMS 工作區不支援使用此解決方案。  
    >

如需有關如何 tooinstall hello OMS Agent for Linux 及下載 hello 最新版本的詳細資訊，請參閱太[Operations Management Suite Agent for Linux](https://github.com/microsoft/oms-agent-for-linux)。  如需有關如何 tooinstall hello OMS Agent for Windows，詳細檢閱[Operations Management Suite 代理程式的 Windows](../log-analytics/log-analytics-windows-agents.md)。  

### <a name="permissions"></a>權限
順序 toocreate 中更新部署，您需要 toobe 授與您的自動化帳戶 」 和 「 記錄分析工作區中的 hello 參與者角色。  

## <a name="solution-components"></a>方案元件
這個解決方案包含 hello 遵循 tooyour 自動化帳戶與直接連接的代理程式或 Operations Manager 連線的管理群組所新增的資源。

### <a name="management-packs"></a>管理組件
如果您的 System Center Operations Manager 管理群組連線的 tooan OMS 工作區，hello 下列管理組件會安裝在 Operations Manager。  新增此解決方案之後，這些管理組件也會安裝在直接連線的 Windows 電腦上。 沒有任何 tooconfigure 或管理這些管理組件。

* Microsoft System Center Advisor 更新評估智慧套件 (Microsoft.IntelligencePacks.UpdateAssessment)
* Microsoft.IntelligencePack.UpdateAssessment.Configuration (Microsoft.IntelligencePack.UpdateAssessment.Configuration)
* 更新部署 MP

如需有關解決方案管理組件的更新方式的詳細資訊，請參閱[Operations Manager 連線 tooLog 分析](../log-analytics/log-analytics-om-agents.md)。

### <a name="hybrid-worker-groups"></a>混合式背景工作群組
啟用此解決方案之後，任何 Windows 電腦直接連線 OMS 工作區會自動設定為包含在此解決方案 Hybrid Runbook Worker toosupport hello runbook tooyour。  對於 hello 解決方案管理的每部 Windows 電腦，它會列在 hello 混合式 Runbook 背景工作群組刀鋒視窗中的 hello 遵循 hello 命名慣例的自動化帳戶*Hostname FQDN_GUID*。  您不能讓這些群組以您帳戶中的 Runbook 為目標，否則它們會失敗。 這些群組是僅預期的 toosupport hello 管理解決方案。   

不過，您可以在您的自動化帳戶 toosupport 自動化 runbook 加入 hello Windows 電腦 tooa 混合式 Runbook 背景工作群組，只要您使用相同帳戶執行 hello 解決方案和混合式 Runbook 背景工作群組成員資格的 hello。  這項功能已加入 tooversion 7.2.12024.0 的 hello Hybrid Runbook Worker。  

## <a name="configuration"></a>組態
執行下列步驟 tooadd hello 更新管理方案 tooyour OMS 工作區的 hello，並確認代理程式會報告。 Windows 代理程式已連接的 tooyour 工作區會自動新增，不需要額外組態。

您可以部署使用下列方法 hello hello 方案：

* 從 Azure Marketplace 中 hello 藉由選取 hello 自動化和控制供應項目或更新的管理解決方案的 Azure 入口網站
* 從您的 OMS 工作區中的 OMS 解決方案資源庫 hello

如果您沒有自動化帳戶和 OMS 工作區連結一起放在 hello 相同的資源群組和區域中，選取 自動化和控制會將驗證您的組態和只有 hello 方案安裝並設定這兩項服務中。  選取 Azure marketplace 的 hello 更新管理解決方案提供 hello 相同的行為。  如果您沒有部署您的訂用帳戶中的任一個服務，請依照下列 hello 中的 hello 步驟**建立新方案**刀鋒視窗，並確認您想 tooinstall hello 其他預先選取的建議的解決方案。  （選擇性） 您可以在其中加入 hello OMS 工作區中使用 hello 步驟所述的更新管理方案 tooyour[加入 OMS 解決方案](../log-analytics/log-analytics-add-solutions.md)從 hello 解決方案資源庫。  

### <a name="confirm-oms-agents-and-operations-manager-management-group-connected-toooms"></a>確認 OMS 代理程式和 Operations Manager 管理群組連線 tooOMS

tooconfirm 直接連線 OMS Agent for Linux 與 Windows 伺服器正在與 OMS 通訊幾分鐘後您可以執行下列記錄搜尋 hello:

* Linux - `Type=Heartbeat OSType=Linux | top 500000 | dedup SourceComputerId | Sort Computer | display Table`.  

* Windows - `Type=Heartbeat OSType=Windows | top 500000 | dedup SourceComputerId | Sort Computer | display Table`

Windows 電腦上，您可以檢閱下列 tooverify 與 OMS 的代理程式連線的 hello:

1.  開啟 Microsoft Monitoring Agent，在控制台中，並在 hello **Azure 記錄分析 (OMS)**索引標籤上，hello 代理程式會顯示訊息指出： **hello Microsoft Monitoring Agent 已成功連接 toohello MicrosoftOperations Management Suite 服務**。   
2.  開啟 hello Windows 事件記錄檔，瀏覽過**應用程式和服務 Logs\Operations 管理員**和來源服務連接器事件識別碼 3000 和 5002 搜尋。  這些事件指出 hello 電腦已註冊 hello OMS 工作區，而且接收組態。  

如果 hello 代理程式不能 toocommunicate 以 hello OMS 服務，而且它是以 hello 設定的 toocommunicate 網際網路透過防火牆或 proxy 伺服器，確認 hello 防火牆或 proxy 伺服器已正確設定，藉由檢閱[網路Windows 代理程式組態](../log-analytics/log-analytics-windows-agents.md#network)或[Linux 代理程式的網路組態](../log-analytics/log-analytics-agent-linux.md#network)。

> [!NOTE]
> 如果您的 Linux 系統設定與 proxy 或閘道 OMS toocommunicate 而且您登入此方案，請更新 hello *proxy.conf*權限 toogrant hello omiuser 群組 「 讀取 」 權限 hello 檔案執行下列命令的 hello:  
> `sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/proxy.conf`  
> `sudo chmod 644 /etc/opt/microsoft/omsagent/proxy.conf`


在執行評估之後，新增的 Linux 代理程式的狀態會顯示為 [已更新]。  此程序可能佔用 too6 小時。

tooconfirm Operations Manager 管理群組通訊的 OMS 時，請參閱[驗證 Operations Manager 整合與 OMS](../log-analytics/log-analytics-om-agents.md#validate-operations-manager-integration-with-oms)。

## <a name="data-collection"></a>資料收集
### <a name="supported-agents"></a>支援的代理程式
hello 下表描述此解決方案所支援的 hello 連接來源。

| 連接的來源 | 支援 | 說明 |
| --- | --- | --- |
| Windows 代理程式 |是 |hello 方案會從 Windows 代理程式收集系統更新的相關資訊，並起始安裝的必要更新。 |
| Linux 代理程式 |是 |hello 方案會從 Linux 代理程式收集系統更新的相關資訊，並起始上支援的散發版本的必要更新的安裝。 |
| Operations Manager 管理群組 |是 |hello 方案會從已連線的管理群組中代理程式收集系統更新的相關資訊。<br>從 hello Operations Manager 代理程式 tooLog 的直接連接分析不需要。 從 hello 管理群組 toohello OMS 儲存機制，就會轉送資料。 |
| Azure 儲存體帳戶 |否 |Azure 儲存體未包含系統更新的相關資訊。 |

### <a name="collection-frequency"></a>收集頻率
對於每部受管理的 Windows 電腦，每天會掃描兩次。 每隔 15 分鐘 hello Windows API 稱為 tooquery hello 上次更新時間 toodetermine 如果狀態已變更，而且如果這樣就會起始相容性掃描。  對於每部受管理的 Linux 電腦，每 3 個小時會掃描一次。

它可以需要 30 分鐘 too6 hello 儀表板 toodisplay 更新資料從受管理電腦的時數。   

## <a name="using-hello-solution"></a>使用 hello 解決方案
當您新增 hello 更新管理方案 tooyour OMS 工作區時，hello**更新管理**磚加入 tooyour OMS 儀表板。 此磚會顯示在您的環境和其更新相容性的計數與 hello 電腦數目的圖形表示。<br><br>
![更新管理摘要圖格](media/oms-solution-update-management/update-management-summary-tile.png)  


## <a name="viewing-update-assessments"></a>檢視更新評估
按一下 hello**更新管理**磚 tooopen hello**更新管理**儀表板。<br><br> ![更新管理摘要儀表板](./media/oms-solution-update-management/update-management-dashboard.png)<br>

此儀表板會提供依照作業系統類型和更新類別分類之更新狀態的詳細明細 - 嚴重、安全性或其他 (例如定義更新)。 此儀表板上的每個磚中的 hello 結果會反映核准部署，以根據 hello 電腦同步處理來源的更新。   hello**更新部署**磚選取時，將您重新導向 toohello 更新部署頁面，您可以在其中檢視排程、 部署目前正在執行，已完成的部署，或排定新的部署。  

您可以執行按一下 hello 特定磚或 toorun 特定類別目錄和預先定義的準則的查詢傳回的所有記錄的記錄搜尋，請選取 hello 清單 hello 底下可使用其中一個**一般更新查詢**資料行。    

## <a name="installing-updates"></a>安裝更新
一旦 hello Linux 和 Windows 電腦工作區中的所有已評估過更新，您可以有已安裝必要更新藉由建立*更新部署*。  更新部署會排定為一或多部電腦安裝必要的更新。  您指定 hello 日期和時間 hello 部署除了 tooa 電腦或群組的電腦應該包含在部署的 hello 範圍內。  toolearn 進一步了解電腦群組，請參閱[記錄分析中的電腦群組](../log-analytics/log-analytics-computer-groups.md)。  當您將更新部署的電腦群組時，群組 memnbership 是只評估一次的排程建立 hello 次。  不會反映後續變更 tooa 群組。  此 toowork 刪除 hello 排定更新部署，並重新建立它。

> [!NOTE]
> 從 hello Azure Marketplace，依預設會設 tooreceive 自動更新 Windows Update Service 部署的 Windows Vm。  加入這個方案或 Windows Vm tooyour 工作區之後不會變更此行為。  如果您使用此解決方案不會主動管理的更新，hello 預設行為 （自動套用更新） 會套用。  

針對從 hello 隨 Red Hat Enterprise Linux (RHEL) 提供的映像在 Azure Marketplace 中建立的虛擬機器，它們是已註冊的 tooaccess hello [Red Hat 更新基礎結構 (RHUI)](../virtual-machines/virtual-machines-linux-update-infrastructure-redhat.md)部署在 Azure 中。  其他 Linux 散發套件必須更新從 hello 散發版本線上的檔案儲存機制遵循支援的方法。  

### <a name="viewing-update-deployments"></a>檢視更新部署
按一下 hello**更新部署**並排 tooview hello 清單的現有更新部署。  其分組依據為狀態 – **已排程**、**執行中**和**已完成**。<br><br> ![更新部署排程頁面](./media/oms-solution-update-management/update-updatedeployment-schedule-page.png)<br>  

顯示每個更新部署的 hello 屬性詳述於下表中的 hello。

| 屬性 | 說明 |
| --- | --- |
| 名稱 |Hello 更新部署的名稱。 |
| 排程 |排程的類型。  可用的選項為 [一次性]、[每週週期性] 或 [每月週期性]。 |
| 開始時間 |日期和時間的 hello 更新部署是排程的 toostart。 |
| Duration |更新部署允許 toorun 分鐘 hello 的數目。  如果然後 hello 剩餘更新必須等到所有的更新不會在這段期間，安裝，hello 下一個更新部署。 |
| 伺服器 |更新部署的 hello 所影響的電腦數目。  |
| 狀態 |Hello 更新部署的目前狀態。<br><br>可能的值包括：<br>- 未啟動<br>- 執行中<br>- 已完成 |

選取 已完成更新部署 tooview hello 詳細資料螢幕包含 hello 下表中的 hello 資料行。  將更新部署的 hello 尚未填入這些資料行，尚未啟動。<br><br> ![更新部署結果的概觀](./media/oms-solution-update-management/update-management-deploymentresults-dashboard.png)

| 資料欄 | 說明 |
| --- | --- |
| **電腦檢視** | |
| Windows 電腦 |列出 hello hello 更新部署的狀態中的 Windows 電腦的數目。  按一下狀態 toorun 記錄搜尋，傳回所有與 hello 更新部署狀態更新記錄。 |
| Linux 電腦 |列出 hello hello 更新部署的狀態中的 Linux 電腦的數目。  按一下狀態 toorun 記錄搜尋，傳回所有與 hello 更新部署狀態更新記錄。 |
| 電腦安裝狀態 |列出相關的 hello 更新部署的 hello 電腦和 hello 百分比已成功安裝的更新。 按一下其中一個 hello 項目 toorun 記錄搜尋，傳回所有遺漏和重大更新。 |
| **更新檢視** | |
| Windows 更新 |列出包含在更新部署的 hello 和其安裝狀態，每個每個更新的 Windows 更新。  選取更新 toorun 傳回所有更新該特定更新的記錄，或按一下 hello 狀態 toorun 記錄搜尋，傳回所有更新 hello 部署記錄的記錄搜尋。 |
| Linux 更新 |列出 Linux 更新包含在更新部署的 hello 和其每個每個更新的安裝狀態。  選取更新 toorun 傳回所有更新該特定更新的記錄，或按一下 hello 狀態 toorun 記錄搜尋，傳回所有更新 hello 部署記錄的記錄搜尋。 |

### <a name="creating-an-update-deployment"></a>建立更新部署
Hello，即可建立新的更新部署**新增**按鈕上方的 hello 螢幕 tooopen hello hello**新的更新部署**頁面。  您必須提供的 hello 下表中的 hello 屬性的值。

| 屬性 | 說明 |
| --- | --- |
| 名稱 |唯一的名稱 tooidentify hello 更新部署。 |
| 時區 |Hello 開始時間的時區 toouse。 |
| 排程類型 | 排程的類型。  可用的選項為 [一次性]、[每週週期性] 或 [每月週期性]。  
| 開始時間 |日期和時間 toostart hello 更新部署。 **注意：** hello 最快過期可以執行部署為 30 分鐘內，從目前的時間，如果您需要立即 toodeploy。 |
| Duration |更新部署允許 toorun 分鐘 hello 的數目。  如果然後 hello 剩餘更新必須等到所有的更新不會在這段期間，安裝，hello 下一個更新部署。 |
| 電腦 |電腦或電腦群組 tooinclude 和 hello 更新部署中的目標的名稱。  從 [hello] 下拉式清單中選取一或多個項目。 |

<br><br> ![新增更新部署頁面](./media/oms-solution-update-management/update-newupdaterun-page.png)

### <a name="time-range"></a>時間範圍
根據預設，hello 分析 hello 更新管理解決方案中的 hello 資料範圍是從 hello 中過去 1 天所產生的所有已連線的管理群組。

hello 資料 toochange hello 時間範圍選取**資料根據**在 hello hello 儀表板的頂端。 您可以選擇建立或更新內 hello 過去 7 天 1 天或在 6 小時的記錄。 或者，也可以選取 [自訂]  ，再指定自訂日期範圍。

## <a name="log-analytics-records"></a>Log Analytics 記錄
更新管理解決方案 hello hello OMS 儲存機制中建立兩種類型的記錄。

### <a name="update-records"></a>更新記錄
每一部電腦上所安裝或需要的每個更新，都會建立類型為**更新**的記錄。 更新資料錄 hello 下表中都有 hello 屬性。

| 屬性 | 說明 |
| --- | --- |
| 類型 |更新 |
| SourceSystem |hello 核准 hello 更新安裝的來源。<br>可能的值包括：<br>- Microsoft Update<br>- Windows Update<br>- SCCM<br>- Linux 伺服器 (擷取自套件管理員) |
| 已核准 |指定是否已核准安裝 hello 更新。<br> 在 Linux 伺服器中，此屬性目前是選擇性的，因為其修補並非由 OMS 負責管理。 |
| Windows 的分類 |Hello 更新的分類。<br>可能的值包括：<br>- 應用程式<br>- 重大更新<br>- 定義更新<br>- 功能套件<br>- 安全性更新<br>- Service Pack<br>- 更新彙總套件<br>- 更新 |
| Linux 的分類 |Cassification hello 更新。<br>可能的值包括：<br>- 重大更新<br>- 安全性更新<br>- 其他更新 |
| 電腦 |Hello 電腦的名稱。 |
| InstallTimeAvailable |指定是否可從其他 hello 的安裝時間安裝的代理程式 hello 相同更新。 |
| InstallTimePredictionSeconds |估計的安裝時間，以秒為單位，根據其他安裝的代理程式 hello 相同的更新。 |
| KBID |描述 hello 更新 hello KB 文章的識別碼。 |
| ManagementGroupName |SCOM 代理程式 hello 管理群組名稱。  若為其他代理程式，此為 AOI-<workspace ID>。 |
| MSRCBulletinID |描述 hello 更新 hello Microsoft 安全性公告識別碼。 |
| MSRCSeverity |Hello Microsoft 資訊安全佈告欄的嚴重性。<br>可能的值包括：<br>- 重大<br>- 重要<br>- 中度 |
| 選用 |指定是否 hello 更新為選擇性。 |
| 產品 |Hello 產品 hello 更新的名稱是。  按一下**檢視**tooopen hello 發行項，在瀏覽器中的。 |
| PackageSeverity |hello 的 hello Linux distro 廠商所提供的報告，此更新中修正的 hello 漏洞的嚴重性。 |
| PublishDate |日期和時間 hello 更新已安裝。 |
| RebootBehavior |指定是否 hello 更新會強制重新開機。<br>可能的值包括：<br>- canrequestreboot<br>- neverreboots |
| RevisionNumber |Hello 更新的修訂編號。 |
| SourceComputerId |GUID toouniquely 識別 hello 的電腦。 |
| TimeGenerated |上次更新日期和 hello 記錄的時間。 |
| Title |Hello 更新的標題。 |
| UpdateID |GUID toouniquely 識別 hello 更新。 |
| UpdateState |指定是否已在此電腦上安裝 hello 更新。<br>可能的值包括：<br>安裝-hello 更新已安裝在這部電腦上。<br>-需要-hello 更新未安裝，而且需要在此電腦上。 |

當您執行任何傳回類型為記錄的記錄搜尋**更新**您可以選取 hello**更新**檢視可顯示一組圖格 hello hello 搜尋所傳回的更新彙總。 您可以在 hello hello 中的項目上按一下**遺失及套用的更新**和**必要和選擇性的更新**磚 tooscope hello 檢視 toothat 組的更新。 選取 hello**清單**或**資料表**檢視 tooreturn hello 個別記錄。<br>

![記錄類型為更新的記錄搜尋更新檢視](./media/oms-solution-update-management/update-la-view-updates.png)  

在 [hello**資料表**] 檢視中，您可以按一下 hello **KBID**的任何記錄 tooopen hello KB 文件的瀏覽器。 這可讓您 tooquickly 閱讀 hello hello 特定更新詳細資料。<br>

![具有記錄類型為更新之圖格的記錄搜尋資料表檢視](./media/oms-solution-update-management/update-la-view-table.png)

在 [hello**清單**] 檢視中，按一下 hello**檢視**連結 toohello KBID tooopen hello KB 文章。<br>

![具有記錄類型為更新之圖格的記錄搜尋清單檢視](./media/oms-solution-update-management/update-la-view-list.png)

### <a name="updatesummary-records"></a>UpdateSummary 記錄
每部 Windows 代理程式電腦都會建立類型為 **UpdateSummary** 的記錄。 此記錄會更新會掃描 hello 電腦每次更新。 **UpdateSummary** hello 下表中，將記錄都有 hello 屬性。

| 屬性 | 說明 |
| --- | --- |
| 類型 |UpdateSummary |
| SourceSystem |OpsManager |
| 電腦 |Hello 電腦的名稱。 |
| CriticalUpdatesMissing |Hello 電腦上遺失的重要更新的數目。 |
| ManagementGroupName |SCOM 代理程式 hello 管理群組名稱。 若為其他代理程式，此為 AOI-<workspace ID>。 |
| NETRuntimeVersion |Hello hello 電腦上安裝的.NET 執行階段版本。 |
| OldestMissingSecurityUpdateBucket |值區 toocategorize hello 時間 hello 最舊遺失安全性更新這部電腦上的已發行之後。<br>可能的值包括：<br>- 更久之前<br>- 180 天前<br>- 150 天前<br>- 120 天前<br>- 90 天前<br>- 60 天前<br>- 30 天前<br>- 最近 |
| OldestMissingSecurityUpdateInDays |Hello 最舊遺失安全性更新這部電腦上的已發行之後的日數。 |
| OsVersion |Hello 作業系統 hello 電腦上安裝的版本。 |
| OtherUpdatesMissing |其他 hello 電腦上缺少的更新數目。 |
| SecurityUpdatesMissing |遺失 hello 電腦上的安全性更新的數目。 |
| SourceComputerId |GUID toouniquely 識別 hello 的電腦。 |
| TimeGenerated |上次更新日期和 hello 記錄的時間。 |
| TotalUpdatesMissing |Hello 電腦上缺少的更新總數。 |
| WindowsUpdateAgentVersion |Hello hello 電腦上的 Windows Update 代理程式的版本號碼。 |
| WindowsUpdateSetting |Hello 電腦安裝重要更新的方式設定。<br>可能的值包括：<br>- 已停用<br>- 先通知再安裝<br>- 排程的安裝 |
| WSUSServer |URL 的 WSUS 伺服器 hello 電腦是否設定 toouse 其中一個。 |

## <a name="sample-log-searches"></a>記錄檔搜尋範例
下表中的 hello 提供範例記錄檔搜尋更新這個解決方案所收集的記錄。

| 查詢 | 說明 |
| --- | --- |
| Type:Update OSType!=Linux UpdateState=Needed Optional=false Approved!=false &#124; measure count() by Computer |以 Windows 為基礎且需要更新的伺服器電腦 |
| Type:Update OSType=Linux UpdateState!="Not needed" &#124; measure count() by Computer |需要更新的 Linux 伺服器 | 
| Type=Update UpdateState=Needed Optional=false &#124; select Computer,Title,KBID,Classification,UpdateSeverity,PublishedDate |遺漏更新的所有電腦 |
| Type=Update UpdateState=Needed Optional=false Computer="COMPUTER01.contoso.com" &#124; select Computer,Title,KBID,Product,UpdateSeverity,PublishedDate |特定電腦的遺漏更新 (以您自己的電腦名稱取代此值)|
| Type=Update UpdateState=Needed Optional=false (Classification="Security Updates" OR Classification="Critical Updates") |遺漏重大更新或安全性更新的所有電腦 | 
| Type=Update UpdateState=Needed Optional=false (Classification="Security Updates" OR Classification="Critical Updates") Computer IN {Type=UpdateSummary WindowsUpdateSetting=Manual &#124; Distinct Computer} &#124; Distinct KBID |機器所需的重大更新或安全性更新 (以手動方式套用的) |
| Type=Event EventLevelName=error Computer IN {Type=Update (Classification="Security Updates" OR Classification="Critical Updates") UpdateState=Needed Optional=false &#124; Distinct Computer} |遺漏必要重大更新或安全性更新之機器的錯誤事件 |
| Type=Update Optional=false Classification="Update Rollups" UpdateState=Needed &#124; select Computer,Title,KBID,Classification,UpdateSeverity,PublishedDate |遺漏更新彙總套件的所有電腦 | 
| Type=Update UpdateState=Needed Optional=false &#124; Distinct Title |所有電腦的不同遺漏更新 | 
| Type:UpdateRunProgress InstallationStatus=failed &#124; measure count() by Computer, Title, UpdateRunName |以 Windows 為基礎且在更新回合中更新失敗的伺服器電腦 | 
| Type:UpdateRunProgress InstallationStatus=failed &#124; measure count() by Computer, Product, UpdateRunName |在更新回合中更新失敗的 Linux 伺服器 | 
| Type=UpdateSummary &#124; measure count() by WSUSServer |WSUS 電腦成員資格 | 
| Type=UpdateSummary &#124; measure count() by WindowsUpdateSetting |自動更新組態 | 
| Type=UpdateSummary WindowsUpdateSetting=Manual |已停用自動更新的電腦 | 
| Type=Update and OSType=Linux and UpdateState!="Not needed" &#124; measure count() by Computer |具有可用的套件更新所有 hello Linux 機器的清單 | 
| Type=Update and OSType=Linux and UpdateState!="Not needed" and (Classification="Critical Updates" OR Classification="Security Updates") &#124; measure count() by Computer |有一個可用的套件更新所有 hello Linux 機器的清單會解決重大或安全性弱點 | 
| Type=Update and OSType=Linux and UpdateState!="Not needed" |有可用更新的所有套件清單 | 
| Type=Update  and OSType=Linux and UpdateState!="Not needed" and (Classification="Critical Updates" OR Classification="Security Updates") |有可以解決重大漏洞或安全性漏洞之可用更新的所有套件清單 | 
| Type:UpdateRunProgress &#124; measure Count() by UpdateRunName |列出哪些更新部署已修改過電腦 | 
| Type:UpdateRunProgress UpdateRunName="DeploymentName" &#124; measure Count() by Computer |在此更新回合中更新的電腦 (以您的更新部署名稱取代此值) | 
| Type=Update and OSType=Linux and OSName = Ubuntu &#124; measure count() by Computer |所有 hello"Ubuntu"機器任何可用的更新清單 | 

## <a name="troubleshooting"></a>疑難排解

本節提供 toohelp 疑難排解問題 hello 更新管理解決方案的資訊。  

### <a name="how-do-i-troubleshoot-onboarding-issues"></a>我該如何進行上架問題的疑難排解？
如果您嘗試 tooonboard hello 方案或虛擬機器時遇到問題，請檢查 hello**應用程式和服務 Logs\Operations 管理員**事件記錄檔的事件與事件識別碼位於 4502 和事件訊息包含**Microsoft.EnterpriseManagement.HealthService.AzureAutomation.HybridAgent**。  hello 下表會強調每個特定的錯誤訊息及可能的解決方式。  

| 訊息 | 原因 | 方案 |   
|----------|----------|----------|  
| 無法 tooRegister 修補程式管理的電腦<br>註冊失敗並發生例外狀況<br>System.InvalidOperationException：{"Message":"電腦已經<br>註冊 tooa 不同的帳戶。 "} | 已進行更新管理工作區中的 onboarded tooanother 機器。 | 對執行清除舊的成品[刪除 hello 混合式 runbook 群組](../automation/automation-hybrid-runbook-worker.md#remove-hybrid-worker-groups)|  
| 無法太註冊修補程式管理的電腦<br>註冊失敗並發生例外狀況<br>System.Net.Http.HttpRequestException： 傳送嗨要求時發生錯誤。 ---><br>System.Net.WebException: hello 基礎連接<br>已關閉：接收時發生<br>意外的錯誤。 ---> System.ComponentModel.Win32Exception：<br>hello 用戶端和伺服器無法通訊，<br>因為它們沒有共同的演算法 | Proxy/閘道/防火牆封鎖通訊 | [檢閱網路需求](../automation/automation-offering-get-started.md#network-planning)|  
| 無法 tooRegister 修補程式管理的電腦<br>註冊失敗並發生例外狀況<br>Newtonsoft.Json.JsonReaderException：剖析正無限值時發生錯誤。 | Proxy/閘道/防火牆封鎖通訊 | [檢閱網路需求](../automation/automation-offering-get-started.md#network-planning)| 
| 由 hello 服務所提供的 hello 憑證<wsid>。 oms.opinsights.azure.com<br>所提供的憑證不是由 Microsoft 服務所用的<br>憑證授權單位發出。 請連絡<br>您的網路系統管理員 toosee 一起執行會攔截的 proxy<br>Proxy。 |Proxy/閘道/防火牆封鎖通訊 | [檢閱網路需求](../automation/automation-offering-get-started.md#network-planning)|  
| 無法 tooRegister 修補程式管理的電腦<br>註冊失敗並發生例外狀況<br>AgentService.HybridRegistration。<br>PowerShell.Certificates.CertificateCreationException：<br>無法 toocreate 自我簽署憑證。 ---><br>System.UnauthorizedAccessException：存取遭到拒絕。 | 自我簽署的憑證產生失敗 | 確認系統帳戶具有<br>讀取權限 toofolder:<br>**C:\ProgramData\Microsoft\**<br>**Crypto\RSA**|  

### <a name="how-do-i-troubleshoot-update-deployments"></a>如何針對更新部署進行疑難排解？
您可以檢視 hello hello runbook 負責部署的 hello 作業刀鋒視窗，您的自動化帳戶連結到支援此解決方案的 hello OMS 工作區的 hello 排定更新部署中所包含的 hello 更新結果。  hello runbook**修補程式 MicrosoftOMSComputer**是特定的受管理的電腦，為目標之子系 runbook，並檢閱 hello 詳細資料流將會顯示該部署的詳細的資訊。  hello 輸出會顯示需要有適用的更新，請下載狀態、 安裝狀態，以及其他詳細資料。<br><br> ![更新部署作業狀態](media/oms-solution-update-management/update-la-patchrunbook-outputstream.png)<br>

如需進一步資訊，請參閱[自動化 Runbook 輸出和訊息](../automation/automation-runbook-output-and-messages.md)。   

## <a name="next-steps"></a>後續步驟
* 使用中的記錄搜尋[記錄分析](../log-analytics/log-analytics-log-searches.md)tooview 詳細的更新資料。
* [建立您自己的儀表板](../log-analytics/log-analytics-dashboards.md)，其中會顯示受管理電腦的更新相容性。
* 在偵測到電腦遺漏重大更新或電腦已停用自動更新時[建立警示](../log-analytics/log-analytics-alerts.md)。  
