---
title: "aaaGet 啟動 Azure 記錄檔的整合 |Microsoft 文件"
description: "了解如何 tooinstall hello Azure 記錄整合服務，以及整合從 Azure 儲存體、 Azure 稽核記錄檔和 Azure 資訊安全中心警示記錄檔。"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 53f67a7c-7e17-4c19-ac5c-a43fabff70e1
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 07/26/2017
ms.author: TomSh
ms.custom: azlog
ms.openlocfilehash: 26c19070d76ff73b1bdbd32ba77fb04978af387e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-with-azure-diagnostics-logging-and-windows-event-forwarding"></a>使用 Azure 診斷記錄和 Windows 事件轉送進行 Azure 記錄整合
Azure 記錄檔整合 (AzLog) 可讓您從您的 Azure 資源 toointegrate 未經處理的記錄檔到內部部署安全性資訊和事件管理 (SIEM) 系統。 這項整合可讓可能 toohave 統一的安全性儀表板為您所有的資產、 在內部部署或 hello 雲端中，以便您可以彙總，相互關聯、 分析和與您的應用程式相關聯的安全性事件的警示。
>[!NOTE]
如需有關 Azure 記錄檔整合的詳細資訊，您可以檢閱 hello [Azure 記錄檔整合概觀](https://docs.microsoft.com/azure/security/security-azure-log-integration-overview)。

本文將協助您開始使用 Azure 記錄檔整合將焦點放在 hello hello Azlog 服務安裝和使用 Azure 診斷整合 hello 服務。 hello Azure 記錄檔整合服務，如此便能 toocollect hello Windows 安全性事件通道在 Azure IaaS 中部署的虛擬機器從 Windows 事件記錄檔資訊。 這是非常類似太 「 事件轉送 」，您可能已經使用內部部署。

>[!NOTE]
>SIEM hello SIEM 本身所提供的 Azure 記錄檔整合中 toohello hello 能力 toobring hello 輸出。 請參閱 hello 文章[整合 Azure 記錄檔整合與您在內部部署的 SIEM](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/)如需詳細資訊。

toobe 的非常清楚-hello Azure 記錄檔整合服務執行使用 hello Windows Server 2008 R2 的實體或虛擬電腦上或以上的作業系統 （Windows Server 2012 R2 或 Windows Server 2016 是慣用）。

hello 實體電腦可以執行內部 （或主機服務提供者站台上）。 如果您選擇 toorun hello Azure 記錄檔整合服務的虛擬機器上，確認虛擬機器可以是位在內部或公用雲端，例如 Microsoft Azure 中。

hello 實體或虛擬機器執行 hello Azure 記錄檔整合服務需要網路連線 toohello Azure 公用雲端。 本文章中的步驟提供 hello 設定詳細資料。

## <a name="prerequisites"></a>必要條件
最少 AzLog hello 安裝需要下列項目 hello:
* **Azure 訂用帳戶**。 如果您沒有訂用帳戶，您可以註冊 [免費帳戶](https://azure.microsoft.com/free/)。
* A**儲存體帳戶**，可用於 Windows Azure 診斷記錄 （您可以使用預先設定的儲存體帳戶，或建立新的-我們將示範如何 tooconfigure hello 本文中稍後的儲存體帳戶）
  >[!NOTE]
  根據您的情況，可能不需要儲存體帳戶。 Hello 需要本文章涵蓋 Azure 診斷案例。
* **兩個系統**： 將執行 hello Azure 記錄檔整合服務的電腦和電腦將會受到監視，且其傳送 toohello Azlog 服務電腦的記錄資訊。
   * 這是 VM，以執行您想 toomonitor – 電腦[Azure 虛擬機器](../virtual-machines/virtual-machines-windows-overview.md)
   * 將執行 hello Azure 記錄檔整合服務的電腦此機器將會收集所有稍後將會匯入您的 SIEM 的 hello 記錄資訊。
    * 這個系統可以是內部部署上或在 Microsoft Azure 中。  
    * 它需要 toobe 執行 x64 版本的 Windows server 2008 R2 SP1 或更高版本，而且有.NET 4.5.1 的安裝。 您可以決定下列標題為 「 hello 文件所安裝的 hello.NET 版本[How to： 判斷安裝的.NET Framework 版本是](https://msdn.microsoft.com/library/hh925568)  
    您必須先使用 Azure 診斷記錄連線 toohello Azure 儲存體帳戶。 我們稍後在本文將提供確認連線方式的指示。

如需快速示範 hello 程序，建立使用 hello Azure 入口網站在虛擬機器的看看 hello 視訊下方。

> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Create-a-Virtual-Machine/player]



## <a name="deployment-considerations"></a>部署考量
當您要測試 Azure 記錄檔整合時，您可以使用任何符合 hello 最低作業系統需求的系統。 不過，實際執行環境 hello 負載可能需要 tooplan 的相應增加或放大。

如果大量事件很高，您可以執行 hello Azure 記錄檔整合服務 （實體或虛擬機器每一個執行個體） 的多個執行個體。 此外，您可以負載的平衡 Windows (WAD) 和 hello 訂閱 tooprovide toohello 執行個體數目的 Azure 診斷儲存體帳戶應根據您的容量。
>[!NOTE]
這次我們不需要針對 tooscale 出 Azure 的執行個體時記錄 integration 機器 （亦即，執行的機器 hello Azure 記錄檔整合服務），或儲存體帳戶或訂用帳戶的特定建議。 應根據您在每個區域中的效能觀察調整決策。

您也可以 hello 選項 tooscale 向上 hello Azure 記錄檔整合服務 toohelp 改善效能。 下列效能度量的 hello 可協助您調整您選擇 toorun hello Azure 記錄檔整合服務的 hello 機器：
* 在 8 個處理器 (核心) 的電腦上，單一的 Azlog 整合器每日可以處理大約 2400 萬個事件 (~1 百萬個/小時)。

* 在 4 個處理器 (核心) 的電腦上，單一的 Azlog 整合器每日可以處理大約 1500 萬個事件 (~6 萬 2 千 5 百個/小時)。

## <a name="install-azure-log-integration"></a>安裝 Azure 記錄檔整合
tooinstall Azure 記錄檔整合，您需要 toodownload hello [Azure 記錄檔整合](https://www.microsoft.com/download/details.aspx?id=53324)安裝檔案。 執行透過 hello 安裝常式，並決定您是否想 tooprovide 遙測資訊 tooMicrosoft。  

![勾選遙測方塊的安裝畫面](./media/security-azure-log-integration-get-started/telemetry.png)

*
> [!NOTE]
> 我們建議您允許 Microsoft toocollect 遙測資料。 您可以取消核取此選項，以關閉遙測資料的收集。
>


hello Azure 記錄檔整合服務會從其安裝所在的 hello 機器收集遙測資料。  

所收集的遙測資料是︰

* Azure 記錄檔整合的執行期間所發生的例外狀況
* 大約 hello 數目的查詢和處理事件的度量
* 正在使用哪些 Azlog.exe 命令列選項的相關統計資料

hello 視訊底下涵蓋 hello 安裝程序。
> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Install-Azure-Log-Integration/player]



## <a name="post-installation-and-validation-steps"></a>張貼安裝和驗證步驟
完成之後 hello 基本安裝常式，您可以準備步驟 tooperform 文章的安裝和驗證步驟：
1. 開啟提升權限的 PowerShell 視窗並瀏覽過**c:\Program Files\Microsoft Azure 記錄檔整合**
2. 您需要 tootake hello 第一個步驟是 tooget hello AzLog Cmdlet 匯入。 您可以執行此動作執行 hello 指令碼**LoadAzlogModule.ps1** (請注意 hello"。 \"hello，下列命令中)。 輸入 **.\LoadAzlogModule.ps1** 後按 [ENTER]。  
您應該會看到類似在 hello 圖中顯示的內容。 </br></br>勾選遙測方塊的安裝畫面 
![](./media/security-azure-log-integration-get-started/loaded-modules.png) </br></br>
3. 現在您需要 tooconfigure AzLog toouse 特定 Azure 環境。 「 Azure 環境 」 是 hello 「 類型 」 想 toowork 與 Azure 雲端資料中心。 此時有數種 Azure 環境，hello 目前相關的選項都是**AzureCloud**或**AzureUSGovernment**。   在提高權限的 PowerShell 環境，請確定您是在 **c:\program files\Microsoft Azure Log Integration\** </br></br>
    一次，執行 hello 命令： </br>
    ``Set-AzlogAzureEnvironment -Name AzureCloud`` (適用於 Azure 商業)

      >[!NOTE]
      Hello 命令成功時，不會收到任何意見反應。  如果您想 toouse hello 美國政府 Azure 雲端，您會使用**AzureUSGovernment** (如 hello-名稱變數) hello 美國政府雲端。 目前不支援其他 Azure 雲端。  
4. 您可以監視系統之前，您需要 hello 名稱使用中的 hello 儲存體帳戶的 Azure 診斷。  在 hello Azure 入口網站瀏覽過**虛擬機器**並尋找您要監視的 hello 虛擬機器。 在 hello**屬性**區段中，選擇**診斷設定**。  按一下**代理程式**並記下指定 hello 儲存體帳戶名稱。 您需要此帳戶的名稱以進行後續步驟。
![Azure 診斷設定](./media/security-azure-log-integration-get-started/storage-account-large.png) </br></br>

      ![Azure 診斷設定](./media/security-azure-log-integration-get-started/azure-monitoring-not-enabled-large.png)
      >[!NOTE]
      如果監視未啟用虛擬機器建立期間您會獲得 hello 選項 tooenable 它如上所示。
5. 現在我們將切換我們注意後 toohello Azure 記錄檔整合機器。 我們需要 tooverify 您擁有連線 toohello 儲存體帳戶 hello 系統從 Azure 記錄檔整合的安裝位置。 hello 實體電腦或虛擬機器執行 hello Azure 記錄檔整合服務需要存取 Azure 診斷所記錄的所設定的每個 hello toohello 儲存體帳戶 tooretrieve 資訊監視系統。  
  1. 您可以從[這裡](http://storageexplorer.com/)下載 Azure 儲存體總管。
  2. 執行 hello 安裝常式
  3. Hello 安裝完成時按一下**下一步**保留 hello 核取方塊和**啟動 Microsoft Azure 儲存體總管**檢查。  
  4. 登入 tooAzure。
  5. 請確認您可以看到您設定 Azure 診斷的 hello 儲存體帳戶。  
![儲存體帳戶](./media/security-azure-log-integration-get-started/storage-account.jpg) </br></br>
   6. 請注意，儲存體帳戶之下有幾個選項。 其中一個是**資料表**。 在**資料表**下您應該會看到 **WADWindowsEventLogsTable** 。 </br></br>
   ![儲存體帳戶](./media/security-azure-log-integration-get-started/storage-explorer.png) </br>

## <a name="integrate-azure-diagnostic-logging"></a>整合 Azure 診斷記錄
在此步驟中，您將設定執行 hello Azure 記錄檔整合服務 tooconnect toohello 包含儲存體帳戶 hello 記錄檔的 hello 機器。
toocomplete 此步驟中，我們必須事先幾件事。  
* **FriendlyNameForSource:**這是您可以套用您已設定來自 Azure 診斷的 hello 虛擬機器 toostore 資訊 toohello 儲存體帳戶的易記名稱
* **StorageAccountName:**這是您指定當您設定 Azure diagnotics hello 儲存體帳戶 hello 名稱。  
* **StorageKey:**這是一個 hello hello 儲存體帳戶的儲存體金鑰 hello Azure 診斷資訊會儲存此虛擬機器。  

執行下列步驟 tooobtain hello 儲存體金鑰的 hello:
 1. 瀏覽 toohello [Azure 入口網站](http://portal.azure.com)。
 2. 主控台中的 hello Azure hello 瀏覽窗格中，捲動 toohello 下方，按一下 **更多服務。**

 ![更多服務](./media/security-azure-log-integration-get-started/more-services.png)
 3. 輸入**儲存體**在 hello**篩選**文字方塊。 按一下 [儲存體帳戶] \(這會在您輸入**儲存體**之後顯示)

   ![篩選方塊](./media/security-azure-log-integration-get-started/filter.png)
 4. 儲存體帳戶的清單隨即出現，按兩下您指派 tooLog 儲存體的 hello 帳戶。

   ![儲存體帳戶清單](./media/security-azure-log-integration-get-started/storage-accounts.png)
 5. 按一下**存取金鑰**在 hello**設定**> 一節。

  ![access keys](./media/security-azure-log-integration-get-started/storage-account-access-keys.png)
 6. 複製**key1**並將其放置在安全的位置，您可以存取以供 hello 下一個步驟。

   ![二個存取金鑰](./media/security-azure-log-integration-get-started/storage-account-access-keys.png)
 7. Hello 在伺服器上已安裝 Azure 記錄檔整合，開啟提升權限的命令提示字元 （請注意，我們在這裡使用提升權限的命令提示字元視窗，無法提高權限的 PowerShell 主控台）。
 8. 瀏覽過**c:\Program Files\Microsoft Azure 記錄檔整合**
 9. 執行 ``Azlog source add <FriendlyNameForTheSource> WAD <StorageAccountName> <StorageKey> `` </br> 例如``Azlog source add Azlogtest WAD Azlog9414 fxxxFxxxxxxxxywoEJK2xxxxxxxxxixxxJ+xVJx6m/X5SQDYc4Wpjpli9S9Mm+vXS2RVYtp1mes0t9H5cuqXEw==``如果您想要設定的 hello 訂用帳戶 ID tooshow hello 事件 XML 中，附加 hello 訂用帳戶 ID toohello 易記名稱：``Azlog source add <FriendlyNameForTheSource>.<SubscriptionID> WAD <StorageAccountName> <StorageKey>``或例如，``Azlog source add Azlogtest.YourSubscriptionID WAD Azlog9414 fxxxFxxxxxxxxywoEJK2xxxxxxxxxixxxJ+xVJx6m/X5SQDYc4Wpjpli9S9Mm+vXS2RVYtp1mes0t9H5cuqXEw==``

>[!NOTE]  
在等候 too60 分鐘，然後檢視取自 hello 儲存體帳戶的 hello 事件。 開啟 tooview**事件檢視器 > Windows 記錄檔 > 轉送事件**hello Azlog 整合器上。

您可以查看視訊通過 hello 步驟涵蓋上方。
> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Enable-Diagnostics-and-Storage/player]


## <a name="what-if-data-is-not-showing-up-in-hello-forwarded-events-folder"></a>如果資料未顯示在 hello 轉送的事件 資料夾嗎？
如果在一小時後資料沒有顯示在 hello**轉送事件**資料夾，然後：

1. 請檢查 hello 機器執行 hello Azure 記錄檔整合服務，並確認它可以存取 Azure。 tootest 連線，再試一次 tooopen hello [Azure 入口網站](http://portal.azure.com)從 hello 瀏覽器。
2. 請確定 hello 使用者帳戶**Azlog** hello 資料夾上具有寫入權限**users\Azlog**。
  <ol type="a">
   <li>開啟 [Windows 檔案總管] </li>
  <li> 瀏覽過**c:\users** </li>
  <li> 以滑鼠右鍵按一下 [c:\users\Azlog] </li>
  <li> 按一下 [安全性]  </li>
  <li> 按一下**NT Service\Azlog**和檢查 hello hello 帳戶的權限。 如果 hello 帳戶缺少此索引標籤，或 hello 適當的權限目前未顯示您可以授與此索引標籤中的 hello 帳戶權限。</li>
  </ol>
3.請確定 hello 儲存體帳戶 hello 命令中新增**Azlog 來源加入**列出當您執行 hello 命令**Azlog 來源清單**。
4. 跳過**事件檢視器 > Windows 記錄檔 > 應用程式**從 hello Azure 記錄檔整合報告 toosee 如果有任何錯誤。


如果 hello 安裝和設定期間遇到任何問題，請開啟[支援要求](../azure-supportability/how-to-create-azure-support-request.md)，選取**記錄 Integration**為 hello 服務您要求支援。

其他支援選項為 hello [Azure 記錄檔整合 MSDN 論壇](https://social.msdn.microsoft.com/Forums/home?forum=AzureLogIntegration)。 這裡 hello 社群可支援彼此與問題、 解答、 秘訣和訣竅 tooget hello 最的 Azure 記錄檔整合。 此外，hello Azure 記錄檔整合小組會監視此論壇，並將說明當我們可以。

## <a name="next-steps"></a>後續步驟
toolearn 進一步了解 Azure 記錄檔整合，請參閱下列文件的 hello:

* [Azure 記錄檔的 Microsoft Azure 記錄整合](https://www.microsoft.com/download/details.aspx?id=53324) – Azure 記錄整合詳細資料、系統需求和安裝指示的下載中心。
* [簡介 tooAzure 記錄 integration](security-azure-log-integration-overview.md) – 這份文件會為您介紹 tooAzure 記錄整合、 其重要功能，和它的運作方式。
* [夥伴的設定步驟](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/)– 此部落格文章會示範 tooconfigure Azure 與協力廠商解決方案 Splunk、 HP 討論 ArcSight 和 IBM QRadar 所記錄的整合 toowork。 這是我們目前指引 tooconfigure hello SIEM 元件的方式。 如需其他詳細資料，請先洽詢您的 SIEM 廠商。
* [Azure 記錄整合常見問題集 (FAQ)](security-azure-log-integration-faq.md) - 此常見問題集會回答有關 Azure 記錄整合的問題。
* [整合的資訊安全中心與 Azure 的警示記錄 Integration](../security-center/security-center-integrating-alerts-with-log-integration.md) – 本文件說明如何 toosync 資訊安全中心發出警示通知，以及虛擬機器的安全性事件收集 Azure 診斷和 Azure 活動記錄檔，記錄分析或 SIEM 解決方案。
* [Azure 診斷和 Azure 稽核記錄檔的新功能](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/)– 此部落格文章向您介紹 tooAzure 稽核記錄檔和其他功能，可協助您深入了解您的 Azure 資源的 hello 作業。
