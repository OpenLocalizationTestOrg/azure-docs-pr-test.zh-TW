---
title: "aaaDeploy 和瀏覽 hello 多租用戶 Wingtip SaaS 應用程式使用 Azure SQL Database |Microsoft 文件"
description: "部署及瀏覽 hello Wingtip SaaS 多租用戶應用程式，示範使用 Azure SQL Database 的 SaaS 模式。"
keywords: SQL Database Azure
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: sstein
ms.openlocfilehash: 7c528ee19472d3b8c7a285b2f86013945e8f4bf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-explore-a-multi-tenant-application-that-uses-azure-sql-database---wingtip-saas"></a>部署及探索使用 Azure SQL Database 的多租用戶應用程式 - Wingtip SaaS

在本教學課程中，您可以部署，並瀏覽 hello Wingtip SaaS 應用程式。 hello 應用程式會使用資料庫的各個租用戶，SaaS 應用程式模式 tooservice 多個租用戶。 hello 應用程式是簡化啟用 SaaS 案例的設計的 tooshowcase 功能的 Azure SQL Database。

五分鐘後按一下 hello*部署 tooAzure*下方的按鈕，您有多租用戶 SaaS 應用程式中，最多使用 SQL Database 和 hello 雲端中執行。 hello 應用程式會使用三個範例租用戶，各有其專屬資料庫到 SQL 彈性集區已部署的所有部署。 hello 應用程式是部署的 tooyour Azure 訂用帳戶，讓您完整存取 tooexplore 及處理 hello 個別應用程式元件。 hello 應用程式來源的程式碼和管理指令碼可用於 hello WingtipSaaS GitHub 儲存機制。


您會在本教學課程中學到：

> [!div class="checklist"]

> * 如何 toodeploy hello Wingtip SaaS 應用程式
> * 其中 tooget hello 應用程式的原始程式碼，並管理指令碼
> * 關於 hello、 集區的伺服器和資料庫組成 hello 應用程式
> * 租用戶的方式對應 tootheir 資料以 hello*類別目錄*
> * 如何 tooprovision 新的租用戶
> * 如何 toomonitor 租用戶 hello 應用程式中的活動

tooexplore 各種 SaaS 設計和管理模式[相關教學課程系列](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)可用，是根據此初始的部署。 時經過 hello 教學課程，深入了解 hello 提供指令碼，並檢查 hello SaaS 模式不同的實作方式。 逐步執行每個教學課程 toogain 深入了解如何 tooimplement hello 許多 SQL Database 功能可讓您簡化開發 SaaS 應用程式中的 hello 指令碼。

## <a name="prerequisites"></a>必要條件

toocomplete 完成本教學課程，請確定 hello 下列必要條件：

* 已安裝 Azure PowerShell。 如需詳細資料，請參閱[開始使用 Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)

## <a name="deploy-hello-wingtip-saas-application"></a>部署 hello Wingtip SaaS 應用程式

部署 hello Wingtip SaaS 應用程式：

1. 按一下 hello**部署 tooAzure**按鈕會開啟 hello Azure 入口網站 toohello Wingtip SaaS 部署範本。 hello 範本需要兩個參數值。新的資源群組名稱和使用者名稱，可區別此部署中的其他部署的 hello Wingtip SaaS 應用程式。 hello 下一個步驟將詳細說明如何設定這些值。

   請確定 toonote hello 確切值，您使用，因為您將的 tooenter 其組態檔更新版本。

   <a href="http://aka.ms/deploywtpapp" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a>

1. 輸入 hello 部署必要的參數值：

    > [!IMPORTANT]
    > 為了示範的目的，已刻意將某些驗證和伺服器防火牆設為不安全。 **建立新的資源群組**，而不要使用現有資源群組、伺服器或集區。 請不要將此應用程式或任何它所建立的資源用於生產環境。 刪除此資源群組，當您完成 hello 應用程式 toostop 相關計費。

    * **資源群組**-選取**建立新**並提供**名稱**hello 資源群組。 選取**位置**hello 下拉式清單中。
    * **使用者** - 部分資源需要全域唯一的名稱。 tooensure 唯一性，每次部署 hello 應用程式提供的值 toodifferentiate 所建立的資源，從任何其他部署的 hello Wingtip 應用程式所建立的資源。 建議 toouse 簡短**使用者**名稱，例如您的首字母加上數字 (例如， *bg1*)，然後 hello 資源群組名稱中使用，(比方說， *wingtip bg1*). [使用者] 參數只能包含字母、數字和連字號 (無空格)。 hello 第一個和最後一個字元必須是字母或數字 （建議使用所有小寫）。


1. **部署的應用程式 hello**。

    * 按一下 tooagree toohello 條款和條件。
    * 按一下 [購買]。

1. 監視部署狀態，依序按一下**通知**（hello hello 搜尋 方塊右邊的鈴鐺圖示）。 部署的 hello Wingtip SaaS 應用程式會大約五分鐘。

   ![部署成功](media/sql-database-saas-tutorial/succeeded.png)

## <a name="download-and-unblock-hello-wingtip-saas-scripts"></a>下載並解除封鎖 hello Wingtip SaaS 指令碼

雖然 hello 應用程式正在部署，下載 hello 來源的程式碼和管理指令碼。

> [!IMPORTANT]
> 從外部來源下載 zip 檔案並進行解壓縮時，Windows 可能會封鎖可執行的內容 (指令碼、dll)。 當從 zip 檔案解壓縮 hello 指令碼，請遵循 hello 步驟下方 toounblock hello.zip 檔案，然後才能擷取。 這可確保會允許 toorun hello 指令碼。

1. 瀏覽過[hello Wingtip SaaS github 儲存機制](https://github.com/Microsoft/WingtipSaaS)。
1. 按一下 [複製或下載]。
1. 按一下**Download ZIP**儲存 hello 檔案。
1. 以滑鼠右鍵按一下 hello **WingtipSaaS master.zip**檔案，然後選取**屬性**。
1. 在 hello**一般**索引標籤上，選取**解除封鎖**，然後按一下**套用**。
1. 按一下 [確定] 。
1. Hello 檔案解壓縮。

指令碼位於 hello *...\\WingtipSaaS master\\學習模組*資料夾。

## <a name="update-hello-configuration-file-for-this-deployment"></a>更新此部署的 hello 設定檔

再執行任何指令碼，設定 hello*資源群組*和*使用者*值**UserConfig.psm1**。 設定這些變數 toohello 您在部署期間設定的值。

1. 開啟...\\學習模組\\*UserConfig.psm1*在 hello *PowerShell ISE*
1. 更新*ResourceGroupName*和*名稱*（位於行 10 和 11 只） 部署的 hello 特定值。
1. 儲存 hello 變更 ！

這裡將此設定，只可防止您在每個指令碼中具有 tooupdate 這些部署專屬的值。

## <a name="run-hello-application"></a>執行 hello 應用程式

hello 應用程式示範管道，例如搭配放逐，爵士梅花、 運動梅花裝載的事件。 管道註冊為 hello Wingtip 平台，針對簡單的方式 toolist 事件客戶 （或租用戶），並銷售票券。 每個地點取得個人化的 web 應用程式 toomanage 及列出其事件並銷售票券，獨立且從其他租用戶隔離。 在 hello 過程中，每個租用戶會取得 SQL 資料庫部署到 SQL 彈性集區。

中央**事件中樞**Url 特定 tooyour 部署提供租用戶的清單。

1. 開啟 hello_事件中樞_網頁瀏覽器： http://events.wtp。&lt;使用者&gt;。 trafficmanager.net （取代為您的部署使用者名稱）：

    ![事件中樞](media/sql-database-saas-tutorial/events-hub.png)

1. 按一下 [Events Hub (活動中心)] 中的 [Fabrikam Jazz Club (Fabrikam 爵士俱樂部)]。

   ![事件](./media/sql-database-saas-tutorial/fabrikam.png)


toocontrol hello 發佈的連入要求，hello 應用程式會使用[ *Azure Traffic Manager*](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview)。 hello 事件頁面，也就是租用戶專屬，需要確定 hello Url 中包含租用戶名稱。 所有 hello 租用戶 Url 包含您的特定*使用者*值，並遵循以下格式： http://events.wtp。&lt;使用者&gt;.trafficmanager.net/*fabrikamjazzclub*。 hello 事件應用程式剖析從 hello URL hello 租用戶名稱，並使用它 toocreate 類別目錄，使用金鑰 tooaccess [*分區對應管理*](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-scale-shard-map-management)。 hello 目錄對應 hello 金鑰 toohello 租用戶的資料庫位置。 hello**事件中樞**Url 的每個資料庫 tooprovide hello 清單相關聯的 hello 目錄 tooretrieve hello 租用戶的名稱中使用擴充的中繼資料。

在實際執行環境中，您通常會建立一筆 CNAME DNS 記錄[*點將公司網際網路網域*](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-point-internet-domain) hello 流量管理員設定檔。

## <a name="start-generating-load-on-hello-tenant-databases"></a>開始產生 hello 租用戶資料庫的負載

既然 hello 的應用程式部署，讓我們將其放 toowork ！ hello*示範 LoadGenerator* PowerShell 指令碼會啟動所有租用戶資料庫上執行的工作負載。 許多 SaaS 應用程式的 hello 真實世界負載通常是偶發和無法預期。 toosimulate 這種類型的負載，hello 產生器會產生負載分散到所有租用戶，隨機暴增上發生隨機的間隔在每個租用戶。 因為這個緣故花幾分鐘的時間 hello 負載模式 tooemerge，因此，最佳的 toolet hello 產生器，至少三個執行或四分鐘後再監視 hello 負載。

1. 在 hello *PowerShell ISE*，開啟 hello...\\學習模組\\公用程式\\*示範 LoadGenerator.ps1*指令碼。
1. 按**F5**執行 hello 指令碼，並啟動 hello 負載產生器 （保持 hello 預設參數值現在）。

> [!IMPORTANT]
> toorun 其他指令碼中，開啟新的 PowerShell ISE 視窗。 hello 負載產生器以一系列的工作執行，本機 PowerShell 工作階段中。 hello*示範 LoadGenerator.ps1* hello 實際負載產生器指令碼，以便為前景工作加上背景負載產生工作的一系列執行指令碼就會啟動。 負載產生器工作叫用 hello 目錄中註冊每個資料庫。 hello 工作執行本機的 PowerShell 工作階段中，所以正在關閉 hello PowerShell 工作階段停止所有工作。 如果您暫停電腦，則負載產生會暫停並在您喚醒電腦時繼續。

一旦 hello 負載產生器中，會叫用的工作負載產生每個租用戶，hello 前景工作仍會留在作業叫用的狀態，它會額外的背景工作啟動後續將佈建任何新租用戶。 您可以使用*CTRL-C*或按 hello*停止*按鈕 toostop hello 前景工作，但現有的背景作業會繼續產生每個資料庫上的負載。 如果您需要 toomonitor 並控制 hello 背景工作，請使用*Get-job*， *Receive-job*和*Stop-job*。 Hello 前景工作執行時您不能使用 hello 相同的 PowerShell 工作階段 tooexecute 其他指令碼。 toorun 其他指令碼中，開啟新的 PowerShell ISE 視窗。

如果您想 toorestart hello 負載產生器工作階段，例如使用不同的參數，您可以停止 hello 前景工作，然後重新執行 hello*示範 LoadGenerator.ps1*指令碼。 重新執行*示範 LoadGenerator.ps1*先停止任何目前正在執行工作，然後再重新啟動 hello 產生器，就會啟動一組新的作業使用 hello 目前參數。

現在請將保留在 hello 作業叫用的狀態下執行的 hello 負載產生器。


## <a name="provision-a-new-tenant"></a>佈建新租用戶

hello 初始部署會建立三個範例租用戶，但我們來建立另一個租用戶 toosee 如何影響部署的 hello 應用程式。 hello Wingtip SaaS 佈建租用工作流程會詳細說明 hello[佈建和類別目錄的教學課程](sql-database-saas-tutorial-provision-and-catalog.md)。 在此步驟中，您會快速建立新的租用戶。

1. 開啟...\\學習 Modules\Provision 和類別目錄\\*示範 ProvisionAndCatalog.ps1*在 hello *PowerShell ISE*。
1. 按**F5**執行 hello 指令碼 （保持 hello 預設值現在）。

   > [!NOTE]
   > 許多 Wingtip SaaS 指令碼會使用*$PSScriptRoot* tooallow 瀏覽其他指令碼中的資料夾 toocall 函式。 此變數只會評估 hello 指令碼執行按下時**F5**。  醒目提示並執行選取項目 (**F8**) 可能會導致錯誤，因此請在執行指令碼時按 **F5**。

hello 新租用戶資料庫是 SQL 彈性集區中建立、 初始化和註冊 hello 目錄中。 成功佈建之後，新租用戶 hello 的票證銷售*事件*網站會出現在您的瀏覽器：

![新租用戶](./media/sql-database-saas-tutorial/red-maple-racing.png)

重新整理 hello*事件中樞*且 hello 新的租用戶現在會顯示 hello 清單中。


## <a name="explore-hello-servers-pools-and-tenant-databases"></a>瀏覽 hello 伺服器集區和租用戶資料庫

既然您已啟動的租用戶的 hello 集合上執行負載，讓我們看看一些已部署的 hello 資源：

1. 在[Azure 入口網站](http://portal.azure.com)，瀏覽 SQL server 的 tooyour 清單並開啟**目錄-&lt;使用者&gt;**伺服器。 hello 類別目錄伺服器包含兩個資料庫。 hello **tenantcatalog**，和 hello **basetenantdb** (空*黃金*或範本資料庫複製 toocreate 新租用戶)。

   ![資料庫](./media/sql-database-saas-tutorial/databases.png)

1. 返回 SQL server 的 tooyour 清單並開啟 hello **tenants1-&lt;使用者&gt;**持有 hello 租用戶資料庫伺服器。 每個租用戶資料庫都是 50 eDTU 標準集區中的「彈性標準」資料庫。 同時也請注意沒有_紅色楓樹賽_資料庫，您先前佈建的 hello 租用戶資料庫。

   ![伺服器](./media/sql-database-saas-tutorial/server.png)

## <a name="monitor-hello-pool"></a>監視 hello 集區

如果 hello 負載產生器已執行幾分鐘的時間，足夠的資料應該可用 toostart 查看一些 hello 監視集區和資料庫內建功能。

1. 瀏覽 toohello 伺服器**tenants1-&lt;使用者&gt;**，然後按一下**Pool1**來檢視資源使用率 hello 集區 （執行 hello 下列圖表中的一小時的 hello 負載產生器）:

   ![監視集區](./media/sql-database-saas-tutorial/monitor-pool.png)

這兩個圖表清楚說明：彈性集區和 SQL Database 非常適合 SaaS 應用程式工作負載。 為每個 invalidreportparameterexception tooas 一樣 40 Edtu 輕鬆 50 eDTU 集區中所支援的四個資料庫。 如果它們已佈建為獨立資料庫，它們就是每個需要 toobe S2 (50 的 DTU) toosupport hello 暴增。 hello 成本的 4 獨立 S2 資料庫是 hello 集區中，幾乎 3 次 hello 價格和 hello 集區仍有大量的許多的多個資料庫的空間。 在真實世界的情況下，SQL Database 客戶目前正在 too500 200 eDTU 集區中的資料庫。 如需詳細資訊，請參閱 hello[效能監視教學課程](sql-database-saas-tutorial-performance-monitoring.md)。


## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解：

> [!div class="checklist"]

> * 如何 toodeploy hello Wingtip SaaS 應用程式
> * 關於 hello、 集區的伺服器和資料庫組成 hello 應用程式
> * 租用戶不對應的 tootheir 資料以 hello*類別目錄*
> * 如何 tooprovision 新租用戶
> * 如何 tooview 集區使用量 toomonitor 租用戶活動
> * Toodelete 範例資源 toostop 相關性計費

現在，請嘗試 hello[佈建和類別目錄的教學課程](sql-database-saas-tutorial-provision-and-catalog.md)



## <a name="additional-resources"></a>其他資源

* 其他[建置的教學課程 hello Wingtip SaaS 應用程式](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* toolearn 有關彈性集區，請參閱[*什麼是 Azure SQL 彈性集區*](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool)
* toolearn 關於彈性的工作，請參閱[*管理向外延展雲端資料庫*](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-jobs-overview)
* toolearn 有關多租用戶 SaaS 應用程式，請參閱[*設計模式為多租用戶 SaaS 應用程式*](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)
