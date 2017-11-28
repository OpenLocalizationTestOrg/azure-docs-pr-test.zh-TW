---
title: "Azure backup aaaConfigure 報表"
description: "本文說明如何使用復原服務保存庫針對 Azure 備份設定 Power BI 報告。"
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 86e465f1-8996-4a40-b582-ccf75c58ab87
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/24/2017
ms.author: pajosh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 503a240b36ea999e0fea434b6a50d26ddf7677bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-backup-reports"></a><span data-ttu-id="51f41-103">設定 Azure 備份報告</span><span class="sxs-lookup"><span data-stu-id="51f41-103">Configure Azure Backup reports</span></span>
<span data-ttu-id="51f41-104">這篇文章參步驟 tooconfigure 報表使用 復原服務保存庫和 tooaccess Azure backup 使用 Power BI 報表。</span><span class="sxs-lookup"><span data-stu-id="51f41-104">This article talks about steps tooconfigure reports for Azure Backup using Recovery Services vault, and  tooaccess these reports using Power BI.</span></span> <span data-ttu-id="51f41-105">執行這些步驟之後，您可以直接前往 tooPower BI tooview hello 的所有報表、 自訂及建立報表。</span><span class="sxs-lookup"><span data-stu-id="51f41-105">After performing these steps, you can directly go tooPower BI tooview all hello reports, customize and create reports.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="51f41-106">支援的案例</span><span class="sxs-lookup"><span data-stu-id="51f41-106">Supported scenarios</span></span>
1. <span data-ttu-id="51f41-107">Azure 虛擬機器備份和檔案/資料夾備份 toocloud 使用 Azure 復原服務代理程式支援 azure Backup 的報表。</span><span class="sxs-lookup"><span data-stu-id="51f41-107">Azure Backup reports are supported for Azure virtual machine backup and file/folder backup toocloud using Azure Recovery Services Agent.</span></span>
2. <span data-ttu-id="51f41-108">目前不支援針對 Azure SQL、DPM 和 Azure 備份伺服器的報告功能。</span><span class="sxs-lookup"><span data-stu-id="51f41-108">Reports for Azure SQL, DPM and Azure Backup Server are not supported at this time.</span></span>
3. <span data-ttu-id="51f41-109">您可以檢視報告跨保存庫，以及跨訂用帳戶，如果相同的儲存體帳戶設定為每個 hello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="51f41-109">You can view reports across vaults and across subscriptions, if same storage account is configured for each of hello vaults.</span></span> <span data-ttu-id="51f41-110">選取的儲存體帳戶應在 hello 相同區域復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="51f41-110">Storage account selected should be in hello same region as recovery services vault.</span></span>
4. <span data-ttu-id="51f41-111">hello 的 hello 報表排程重新整理頻率是 Power BI 中的 24 小時。</span><span class="sxs-lookup"><span data-stu-id="51f41-111">hello frequency of scheduled refresh for hello reports is 24 hours in Power BI.</span></span> <span data-ttu-id="51f41-112">您也可以執行特定的重新整理 hello 報表在 Power BI 中案例的最新資料，客戶儲存體帳戶中用於轉譯報表。</span><span class="sxs-lookup"><span data-stu-id="51f41-112">You can also perform an ad-hoc refresh of hello reports in Power BI, in which case latest data in customer storage account is used for rendering reports.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="51f41-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="51f41-113">Prerequisites</span></span>
1. <span data-ttu-id="51f41-114">建立[Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)tooconfigure 它的報告。</span><span class="sxs-lookup"><span data-stu-id="51f41-114">Create an [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) tooconfigure it for reports.</span></span> <span data-ttu-id="51f41-115">這個儲存體帳戶是用來儲存與報告相關的資料。</span><span class="sxs-lookup"><span data-stu-id="51f41-115">This storage account is used for storing reports related data.</span></span>
2. <span data-ttu-id="51f41-116">[建立 Power BI 帳戶](https://powerbi.microsoft.com/landing/signin/)tooview，自訂和建立您自己的報表使用 Power BI 入口網站。</span><span class="sxs-lookup"><span data-stu-id="51f41-116">[Create a Power BI account](https://powerbi.microsoft.com/landing/signin/) tooview, customize, and create your own reports using Power BI portal.</span></span>
3. <span data-ttu-id="51f41-117">註冊 hello 資源提供者**Microsoft.insights**如果沒有已登錄，與 hello 訂用帳戶的儲存體帳戶和與 hello 訂用帳戶的 復原服務保存庫 tooenable 報告資料 tooflow toohello儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="51f41-117">Register hello resource provider **Microsoft.insights** if not registered already, with hello subscription of storage account and also with hello subscription of Recovery Services vault tooenable reporting data tooflow toohello storage account.</span></span> <span data-ttu-id="51f41-118">toodo hello 相同，您必須移 tooAzure 入口網站 > 訂用帳戶 > 資源提供者並檢查此提供者 tooregister 它。</span><span class="sxs-lookup"><span data-stu-id="51f41-118">toodo hello same, you must go tooAzure portal > Subscription > Resource providers and check for this provider tooregister it.</span></span> 

## <a name="configure-storage-account-for-reports"></a><span data-ttu-id="51f41-119">針對報告設定儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="51f41-119">Configure storage account for reports</span></span>
<span data-ttu-id="51f41-120">使用下列步驟 tooconfigure hello 儲存體帳戶使用 Azure 入口網站的復原服務保存庫的 hello。</span><span class="sxs-lookup"><span data-stu-id="51f41-120">Use hello following steps tooconfigure hello storage account for recovery services vault using Azure portal.</span></span> <span data-ttu-id="51f41-121">這是一次性的組態和儲存體帳戶設定之後，您可以移 tooPower BI 直接 tooview 內容套件，並利用報告。</span><span class="sxs-lookup"><span data-stu-id="51f41-121">This is a one-time configuration and once storage account is configured, you can go tooPower BI directly tooview content pack and leverage reports.</span></span>
1. <span data-ttu-id="51f41-122">如果您已經開啟的復原服務保存庫，請繼續執行 toonext 步驟。</span><span class="sxs-lookup"><span data-stu-id="51f41-122">If you already have a Recovery Services vault open, proceed toonext step.</span></span> <span data-ttu-id="51f41-123">如果您不需要復原服務保存庫開啟之後，但在 hello hello 中樞功能表中，在 Azure 入口網站中按一下**瀏覽**。</span><span class="sxs-lookup"><span data-stu-id="51f41-123">If you do not have a Recovery Services vault open, but are in hello Azure portal, on hello Hub menu, click **Browse**.</span></span>

   * <span data-ttu-id="51f41-124">在 [hello] 清單中的資源，輸入**復原服務**。</span><span class="sxs-lookup"><span data-stu-id="51f41-124">In hello list of resources, type **Recovery Services**.</span></span>
   * <span data-ttu-id="51f41-125">當您開始輸入 hello 清單會篩選根據您的輸入。</span><span class="sxs-lookup"><span data-stu-id="51f41-125">As you begin typing, hello list filters based on your input.</span></span> <span data-ttu-id="51f41-126">當您看到 [復原服務保存庫] 時，請按一下它。</span><span class="sxs-lookup"><span data-stu-id="51f41-126">When you see **Recovery Services vaults**, click it.</span></span>

      ![建立復原服務保存庫的步驟 1](./media/backup-azure-vms-encryption/browse-to-rs-vaults.png) <br/>

     <span data-ttu-id="51f41-128">復原服務保存庫 hello 清單隨即出現。</span><span class="sxs-lookup"><span data-stu-id="51f41-128">hello list of Recovery Services vaults appears.</span></span> <span data-ttu-id="51f41-129">從 hello 清單的 復原服務保存庫中，選取保存庫。</span><span class="sxs-lookup"><span data-stu-id="51f41-129">From hello list of Recovery Services vaults, select a vault.</span></span>

     <span data-ttu-id="51f41-130">hello 選取保存庫儀表板隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="51f41-130">hello selected vault dashboard opens.</span></span>
2. <span data-ttu-id="51f41-131">從 hello 的項目清單會出現在保存庫下，按一下 **備份報告**監視與報表區段 tooconfigure hello 儲存體帳戶的報表。</span><span class="sxs-lookup"><span data-stu-id="51f41-131">From hello list of items that appears under vault, click **Backup Reports** under Monitoring and Reports section tooconfigure hello storage account for reports.</span></span>

      ![選取備份報告功能表項目步驟 2](./media/backup-azure-configure-reports/backup-reports-settings.PNG)
3. <span data-ttu-id="51f41-133">在 hello 備份報告刀鋒視窗中，按一下 **設定** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="51f41-133">On hello Backup Reports blade, click **Configure** button.</span></span> <span data-ttu-id="51f41-134">這會開啟 hello Azure Application Insights 刀鋒視窗中，可用來將推送資料 toocustomer 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="51f41-134">This opens hello Azure Application Insights blade which is used for pushing data toocustomer storage account.</span></span>

      ![設定儲存體帳戶步驟 3](./media/backup-azure-configure-reports/configure-storage-account.PNG)
4. <span data-ttu-id="51f41-136">設定得 hello 狀態切換按鈕**上**選取**封存儲存體帳戶 tooa**核取方塊，以便資料可以開始送 toohello 儲存體帳戶中的報告。</span><span class="sxs-lookup"><span data-stu-id="51f41-136">Set hello Status toggle button too**On** and select **Archive tooa Storage Account** check box so that reporting data can start flowing in toohello storage account.</span></span>

      ![啟用診斷步驟 4](./media/backup-azure-configure-reports/set-status-on.png)
5. <span data-ttu-id="51f41-138">按一下 儲存體帳戶選擇器和選取 hello 儲存體帳戶，從 hello 清單，以儲存報告的資料以及按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="51f41-138">Click Storage Account picker and select hello storage account from hello list for storing reporting data and click **OK**.</span></span>

      ![選取儲存體帳戶步驟 5](./media/backup-azure-configure-reports/select-storage-account.png)
6. <span data-ttu-id="51f41-140">選取**AzureBackupReport**核取方塊，也會移動這個 hello 滑桿 tooselect 保留期限報告資料。</span><span class="sxs-lookup"><span data-stu-id="51f41-140">Select **AzureBackupReport** check box and also move hello slider tooselect retention period for this reporting data.</span></span> <span data-ttu-id="51f41-141">報告 hello 儲存體帳戶中的資料會保留選取 使用此滑桿 hello 週期。</span><span class="sxs-lookup"><span data-stu-id="51f41-141">Reporting data in hello storage account is kept for hello period selected using this slider.</span></span>

      ![選取儲存體帳戶步驟 6](./media/backup-azure-configure-reports/save-configuration.png)
7. <span data-ttu-id="51f41-143">檢閱所有 hello 變更，然後按一下**儲存**按鈕上方，hello 上圖所示。</span><span class="sxs-lookup"><span data-stu-id="51f41-143">Review all hello changes and click **Save** button on top, as shown in hello figure above.</span></span> <span data-ttu-id="51f41-144">此動作可確保所有變更都會儲存，且儲存體帳戶已針對儲存報告資料進行設定。</span><span class="sxs-lookup"><span data-stu-id="51f41-144">This action ensures that all your changes are saved and storage account is now configured for storing reporting data.</span></span>

> [!NOTE]
> <span data-ttu-id="51f41-145">一旦您藉由儲存儲存體帳戶設定的報表，您應該**等待 24 小時**的初始資料推入 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="51f41-145">Once you configure reports by saving storage account, you should **wait for 24 hours** for initial data push toocomplete.</span></span> <span data-ttu-id="51f41-146">只有在該時間之後，您才需要將 Power BI 中的 Azure 備份內容套件匯入。</span><span class="sxs-lookup"><span data-stu-id="51f41-146">You should import Azure Backup content pack in Power BI only after that time.</span></span> <span data-ttu-id="51f41-147">如需進一步的詳細資料，請參閱[常見問題集一節](#frequently-asked-questions)。</span><span class="sxs-lookup"><span data-stu-id="51f41-147">Refer [FAQ section](#frequently-asked-questions) for futher details.</span></span> 
>
>

## <a name="view-reports-in-power-bi"></a><span data-ttu-id="51f41-148">在 Power BI 中檢視報告</span><span class="sxs-lookup"><span data-stu-id="51f41-148">View reports in Power BI</span></span> 
<span data-ttu-id="51f41-149">使用 復原服務保存庫設定儲存體帳戶的報告之後，它會報告中傳送的資料 toostart 大約 24 小時。</span><span class="sxs-lookup"><span data-stu-id="51f41-149">After configuring storage account for reports using recovery services vault, it takes around 24 hours for reporting data toostart flowing in.</span></span> <span data-ttu-id="51f41-150">24 小時之後設定儲存體帳戶，使用 hello 下列步驟會在 Power BI 中的 tooview 報表：</span><span class="sxs-lookup"><span data-stu-id="51f41-150">After 24 hours of setting up storage account, use hello following steps tooview reports in Power BI:</span></span>
1. <span data-ttu-id="51f41-151">[登入](https://powerbi.microsoft.com/landing/signin/)tooPower BI。</span><span class="sxs-lookup"><span data-stu-id="51f41-151">[Sign in](https://powerbi.microsoft.com/landing/signin/) tooPower BI.</span></span>
2. <span data-ttu-id="51f41-152">按一下 [取得資料]，然後在內容套件庫中的 [服務] 底下，按一下 [取得]。</span><span class="sxs-lookup"><span data-stu-id="51f41-152">Click **Get Data** and click Get under **Services** in Content Pack Library.</span></span> <span data-ttu-id="51f41-153">使用中所述的步驟[Power BI 文件 tooaccess 內容套件](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-packs-services/)。</span><span class="sxs-lookup"><span data-stu-id="51f41-153">Use steps mentioned in [Power BI documentation tooaccess content pack](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-packs-services/).</span></span>

     ![匯入內容套件](./media/backup-azure-configure-reports/content-pack-import.png)
3. <span data-ttu-id="51f41-155">在搜尋列中輸入 **Azure Backup**，並按一下 [立即取得]。</span><span class="sxs-lookup"><span data-stu-id="51f41-155">Type **Azure Backup** in Search bar and click **Get it now**.</span></span>

      ![取得內容套件](./media/backup-azure-configure-reports/content-pack-get.png)
4. <span data-ttu-id="51f41-157">輸入 hello 上述步驟 5 中設定的儲存體帳戶名稱，然後按一下**下一步** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="51f41-157">Enter hello storage account name configured in step 5 above and click **Next** button.</span></span>

    ![輸入儲存體帳戶名稱](./media/backup-azure-configure-reports/content-pack-storage-account-name.png)    
5. <span data-ttu-id="51f41-159">輸入 hello 這個儲存體帳戶的儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="51f41-159">Enter hello storage account key for this storage account.</span></span> <span data-ttu-id="51f41-160">您可以[檢視和複製儲存體存取金鑰](../storage/common/storage-create-storage-account.md#manage-your-storage-account)瀏覽 tooyour Azure 入口網站中的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="51f41-160">You can [view and copy storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account) by navigating tooyour storage account in Azure portal.</span></span> 

     ![輸入儲存體帳戶](./media/backup-azure-configure-reports/content-pack-storage-account-key.png) <br/>
     
6. <span data-ttu-id="51f41-162">按一下 [登入] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="51f41-162">Click **Sign in** button.</span></span> <span data-ttu-id="51f41-163">登入成功後，您會收到「匯入資料」的通知。</span><span class="sxs-lookup"><span data-stu-id="51f41-163">After sign-in is successful, you get **Importing data** notification.</span></span>

    ![匯入內容套件](./media/backup-azure-configure-reports/content-pack-importing-data.png) <br/>
    
    <span data-ttu-id="51f41-165">取得一段時間後**成功**hello 匯入完成後的通知。</span><span class="sxs-lookup"><span data-stu-id="51f41-165">After some time, you get **Success** notification after hello import is complete.</span></span> <span data-ttu-id="51f41-166">如果有大量的 hello 儲存體帳戶中的資料可能需要很少長 tooimport hello 內容套件。</span><span class="sxs-lookup"><span data-stu-id="51f41-166">It might take little longer tooimport hello content pack, if there is a lot of data in hello storage account.</span></span>
    
    ![成功匯入內容套件](./media/backup-azure-configure-reports/content-pack-import-success.png) <br/>
    
7. <span data-ttu-id="51f41-168">成功時，匯入資料之後**Azure Backup**內容套件會顯示在**應用程式**hello 瀏覽窗格中。</span><span class="sxs-lookup"><span data-stu-id="51f41-168">Once data is imported successfully, **Azure Backup** content pack is visible in **Apps** in hello navigation pane.</span></span> <span data-ttu-id="51f41-169">hello 清單現在會顯示 Azure Backup 儀表板、 報表和資料集以黃色星號表示新匯入的報表。</span><span class="sxs-lookup"><span data-stu-id="51f41-169">hello list now shows Azure Backup dashboard, reports, and dataset with a yellow star indicating newly imported reports.</span></span> 

     ![Azure 備份內容套件](./media/backup-azure-configure-reports/content-pack-azure-backup.png) <br/>
     
8. <span data-ttu-id="51f41-171">按一下 [儀表板] 底下的 [Azure 備份]，這會顯示一組已釘選的重要資訊報告。</span><span class="sxs-lookup"><span data-stu-id="51f41-171">Click **Azure Backup** under Dashboards, which shows a set of pinned key reports.</span></span>

      ![Azure 備份儀表板](./media/backup-azure-configure-reports/azure-backup-dashboard.png) <br/>
9. <span data-ttu-id="51f41-173">tooview hello 整組報表，按一下 hello 儀表板中的任何報表。</span><span class="sxs-lookup"><span data-stu-id="51f41-173">tooview hello complete set of reports, click any report in hello dashboard.</span></span>

      ![Azure 備份作業健康情況](./media/backup-azure-configure-reports/azure-backup-job-health.png) <br/>
10. <span data-ttu-id="51f41-175">按一下該區域中的 hello 報表 tooview 報表中的每個索引標籤。</span><span class="sxs-lookup"><span data-stu-id="51f41-175">Click each tab in hello reports tooview reports in that area.</span></span>

      ![Azure 備份報告索引標籤](./media/backup-azure-configure-reports/reports-tab-view.png)


## <a name="frequently-asked-questions"></a><span data-ttu-id="51f41-177">常見問題集</span><span class="sxs-lookup"><span data-stu-id="51f41-177">Frequently asked questions</span></span>
1. <span data-ttu-id="51f41-178">**如何檢查如果報告資料後啟動流動 toostorage 帳戶中？**</span><span class="sxs-lookup"><span data-stu-id="51f41-178">**How do I check if reporting data has started flowing in toostorage account?**</span></span>
    
    <span data-ttu-id="51f41-179">您可以移 toohello 儲存體帳戶設定和選取的容器。</span><span class="sxs-lookup"><span data-stu-id="51f41-179">You can go toohello storage account configured and select containers.</span></span> <span data-ttu-id="51f41-180">如果 hello 容器擁有 insights-記錄檔-azurebackupreport 的項目，就表示，報告資料以啟動的流動。</span><span class="sxs-lookup"><span data-stu-id="51f41-180">If hello container has an entry for insights-logs-azurebackupreport, it indicates that reporting data has started flowing in.</span></span>

2. <span data-ttu-id="51f41-181">**什麼是資料推入 toostorage 帳戶和 Azure 備份的內容套件在 Power BI 中的 hello 頻率？**</span><span class="sxs-lookup"><span data-stu-id="51f41-181">**What is hello frequency of data push toostorage account and Azure Backup content pack in Power BI?**</span></span>

   <span data-ttu-id="51f41-182">對於第 0 天的使用者，將花費大約 24 小時 toopush 資料 toostorage 帳戶。</span><span class="sxs-lookup"><span data-stu-id="51f41-182">For Day 0 users, it would take around 24 hours toopush data toostorage account.</span></span> <span data-ttu-id="51f41-183">一旦此初始推送 compelete，hello 遵循 hello 圖所示的頻率重新整理資料。</span><span class="sxs-lookup"><span data-stu-id="51f41-183">Once this initial push is compelete, data is refreshed with hello following frequency shown in hello figure below.</span></span> 
      * <span data-ttu-id="51f41-184">資料太相關**作業、 警示、 備份的項目、 保存庫、 受保護的伺服器和原則**推 toocustomer 儲存體帳戶，並在登入。</span><span class="sxs-lookup"><span data-stu-id="51f41-184">Data related too**Jobs, Alerts, Backup Items, Vaults, Protected Servers and Policies** is pushed toocustomer storage account as and when it is logged.</span></span>
      * <span data-ttu-id="51f41-185">資料太相關**儲存體**會每隔 24 小時推送 toocustomer 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="51f41-185">Data related too**Storage** is pushed toocustomer storage account every 24 hours.</span></span>
   
    ![Azure 備份報表資料推送頻率](./media/backup-azure-configure-reports/reports-data-refresh-cycle.png)

  <span data-ttu-id="51f41-187">Power BI 具有[一天一次的排程重新整理](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/#what-can-be-refreshed)。</span><span class="sxs-lookup"><span data-stu-id="51f41-187">Power BI has a [scheduled refresh once a day](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/#what-can-be-refreshed).</span></span> <span data-ttu-id="51f41-188">您可以執行在 Power BI 中的手動資料重新整理的 hello hello 內容套件。</span><span class="sxs-lookup"><span data-stu-id="51f41-188">You can perform a manual refresh of hello data in Power BI for hello content pack.</span></span>

3. <span data-ttu-id="51f41-189">**時間長度可以保留 hello 報表？**</span><span class="sxs-lookup"><span data-stu-id="51f41-189">**How long can I retain hello reports?**</span></span> 

   <span data-ttu-id="51f41-190">在設定儲存體帳戶時，您可以選取報告資料的保留的期限 hello 儲存體帳戶 （使用上述的報表區段的設定儲存體帳戶中的步驟 6） 中。</span><span class="sxs-lookup"><span data-stu-id="51f41-190">While configuring storage account, you can select retention period of reporting data in hello storage account (using step 6 in Configure storage account for reports section above).</span></span> <span data-ttu-id="51f41-191">除此之外，您可以根據需求[在 Excel 中分析報告](https://powerbi.microsoft.com/documentation/powerbi-service-analyze-in-excel/)並儲存它們，以延長保留期間。</span><span class="sxs-lookup"><span data-stu-id="51f41-191">Besides that, you can [Analyze reports in excel](https://powerbi.microsoft.com/documentation/powerbi-service-analyze-in-excel/) and save them for a longer retention period, as per your needs.</span></span> 

4. <span data-ttu-id="51f41-192">**會看到我的所有資料在報表中之後設定 hello 儲存體帳戶？**</span><span class="sxs-lookup"><span data-stu-id="51f41-192">**Will I see all my data in reports after configuring hello storage account?**</span></span>

   <span data-ttu-id="51f41-193">所有 hello 之後產生的資料**」 設定儲存體帳戶"**推入 toohello 儲存體帳戶，而且會出現在報表中。</span><span class="sxs-lookup"><span data-stu-id="51f41-193">All hello data generated after **"configuring storage account"** will be pushed toohello storage account and will be available in reports.</span></span> <span data-ttu-id="51f41-194">不過，「進行中的作業」將不會針對報告進行推送。</span><span class="sxs-lookup"><span data-stu-id="51f41-194">However, **In Progress Jobs are not pushed** for Reporting.</span></span> <span data-ttu-id="51f41-195">一旦 hello 工作完成或失敗，它會傳送 tooreports。</span><span class="sxs-lookup"><span data-stu-id="51f41-195">Once hello job completes or fails, it is sent tooreports.</span></span>

5. <span data-ttu-id="51f41-196">**如果我已經設定 hello 存放裝置帳戶 tooview 報告，可以變更 hello 組態 toouse 另一個儲存體帳戶？**</span><span class="sxs-lookup"><span data-stu-id="51f41-196">**If I have already configured hello storage account tooview reports, can I change hello configuration toouse another storage account?**</span></span> 

   <span data-ttu-id="51f41-197">是，您可以變更 hello 組態 toopoint tooa 不同儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="51f41-197">Yes, you can change hello configuration toopoint tooa different storage account.</span></span> <span data-ttu-id="51f41-198">連線 tooAzure 備份內容套件時，您應該使用新設定的 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="51f41-198">You should use hello newly configured storage account while connecting tooAzure Backup content pack.</span></span> <span data-ttu-id="51f41-199">此外，在設定不同的儲存體帳戶之後，新的資料將會流入這個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="51f41-199">Also, once a different storage account is configured, new data would flow in this storage account.</span></span> <span data-ttu-id="51f41-200">但是較舊的資料 （然後再變更 hello 組態） 仍會保留在 hello 較舊的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="51f41-200">But older data (before changing hello configuration) would still remain in hello older storage account.</span></span>

6. <span data-ttu-id="51f41-201">**我是否可以檢視跨保存庫及跨訂用帳戶的報告？**</span><span class="sxs-lookup"><span data-stu-id="51f41-201">**Can I view reports across vaults and across subscriptions?**</span></span> 

   <span data-ttu-id="51f41-202">是，您可以設定 hello 跨不同的相同儲存體帳戶的保存庫 tooview 跨保存庫的報表。</span><span class="sxs-lookup"><span data-stu-id="51f41-202">Yes, you can configure hello same storage account across various vaults tooview cross-vault reports.</span></span> <span data-ttu-id="51f41-203">此外，您可以設定 hello 跨訂用帳戶的保存庫相同的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="51f41-203">Also, you can configure hello same storage account for vaults across subscriptions.</span></span> <span data-ttu-id="51f41-204">您接著可以使用這個儲存體帳戶連線 tooAzure 備份內容套件在 Power BI tooview hello 報表中的時。</span><span class="sxs-lookup"><span data-stu-id="51f41-204">You can then use this storage account while connecting tooAzure Backup content pack in Power BI tooview hello reports.</span></span> <span data-ttu-id="51f41-205">不過，在 hello 應該選取 hello 儲存體帳戶相同的區域復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="51f41-205">However, hello storage account selected should be in hello same region as recovery services vault.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="51f41-206">後續步驟</span><span class="sxs-lookup"><span data-stu-id="51f41-206">Next steps</span></span>
<span data-ttu-id="51f41-207">既然您已經設定 hello 儲存體帳戶和匯入的 Azure 備份內容套件、 hello 下一個步驟是 toocustomize，這些報表和使用報告資料模型 toocreate 報表。</span><span class="sxs-lookup"><span data-stu-id="51f41-207">Now that you have configured hello storage account and imported Azure Backup content pack, hello next step is toocustomize these reports and use reporting data model toocreate reports.</span></span> <span data-ttu-id="51f41-208">Hello 下列發行項，如需詳細資訊，請參閱。</span><span class="sxs-lookup"><span data-stu-id="51f41-208">Refer hello following articles for more details.</span></span>

* [<span data-ttu-id="51f41-209">使用 Azure 備份報告資料模型</span><span class="sxs-lookup"><span data-stu-id="51f41-209">Using Azure Backup reporting data model</span></span>](backup-azure-reports-data-model.md)
* [<span data-ttu-id="51f41-210">在 Power BI 中篩選報告</span><span class="sxs-lookup"><span data-stu-id="51f41-210">Filtering reports in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-service-about-filters-and-highlighting-in-reports/)
* [<span data-ttu-id="51f41-211">在 Power BI 中建立報告</span><span class="sxs-lookup"><span data-stu-id="51f41-211">Creating reports in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-service-create-a-new-report/)

