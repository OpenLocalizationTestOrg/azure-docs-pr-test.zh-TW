---
title: "針對 Azure 備份設定報告"
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
ms.openlocfilehash: 4629665e6fbe26c26eb45af7509de338367c4e18
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="configure-azure-backup-reports"></a><span data-ttu-id="45626-103">設定 Azure 備份報告</span><span class="sxs-lookup"><span data-stu-id="45626-103">Configure Azure Backup reports</span></span>
<span data-ttu-id="45626-104">本文說明使用復原服務保存庫針對 Azure 備份設定報告，以及使用 Power BI 存取這些報告的步驟。</span><span class="sxs-lookup"><span data-stu-id="45626-104">This article talks about steps to configure reports for Azure Backup using Recovery Services vault, and  to access these reports using Power BI.</span></span> <span data-ttu-id="45626-105">執行這些步驟後，您可以直接移至 Power BI 以檢閱所有報告，以及自訂和建立報告。</span><span class="sxs-lookup"><span data-stu-id="45626-105">After performing these steps, you can directly go to Power BI to view all the reports, customize and create reports.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="45626-106">支援的案例</span><span class="sxs-lookup"><span data-stu-id="45626-106">Supported scenarios</span></span>
1. <span data-ttu-id="45626-107">Azure 備份報告支援使用 Azure 復原服務代理程式進行 Azure 虛擬機器備份，以及將檔案/資料夾備份到雲端。</span><span class="sxs-lookup"><span data-stu-id="45626-107">Azure Backup reports are supported for Azure virtual machine backup and file/folder backup to cloud using Azure Recovery Services Agent.</span></span>
2. <span data-ttu-id="45626-108">目前不支援針對 Azure SQL、DPM 和 Azure 備份伺服器的報告功能。</span><span class="sxs-lookup"><span data-stu-id="45626-108">Reports for Azure SQL, DPM and Azure Backup Server are not supported at this time.</span></span>
3. <span data-ttu-id="45626-109">如果針對每個保存庫皆設定相同的儲存體帳戶，則可以檢閱跨保存庫和跨訂用帳戶的報告。</span><span class="sxs-lookup"><span data-stu-id="45626-109">You can view reports across vaults and across subscriptions, if same storage account is configured for each of the vaults.</span></span> <span data-ttu-id="45626-110">選取的儲存體帳戶應與復原服務保存庫位於相同的區域。</span><span class="sxs-lookup"><span data-stu-id="45626-110">Storage account selected should be in the same region as recovery services vault.</span></span>
4. <span data-ttu-id="45626-111">Power BI 中報告的排程重新整理頻率為 24 小時。</span><span class="sxs-lookup"><span data-stu-id="45626-111">The frequency of scheduled refresh for the reports is 24 hours in Power BI.</span></span> <span data-ttu-id="45626-112">您也可以在 Power BI 中執行報告的臨機操作重新整理，這會使用客戶儲存體帳戶中的最新資料來轉譯報告。</span><span class="sxs-lookup"><span data-stu-id="45626-112">You can also perform an ad-hoc refresh of the reports in Power BI, in which case latest data in customer storage account is used for rendering reports.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="45626-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="45626-113">Prerequisites</span></span>
1. <span data-ttu-id="45626-114">建立 [Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)以針對報告進行設定。</span><span class="sxs-lookup"><span data-stu-id="45626-114">Create an [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) to configure it for reports.</span></span> <span data-ttu-id="45626-115">這個儲存體帳戶是用來儲存與報告相關的資料。</span><span class="sxs-lookup"><span data-stu-id="45626-115">This storage account is used for storing reports related data.</span></span>
2. <span data-ttu-id="45626-116">[建立 Power BI 帳戶](https://powerbi.microsoft.com/landing/signin/)，以使用 Power BI 入口網站檢視、自訂和建立您自己的報告。</span><span class="sxs-lookup"><span data-stu-id="45626-116">[Create a Power BI account](https://powerbi.microsoft.com/landing/signin/) to view, customize, and create your own reports using Power BI portal.</span></span>
3. <span data-ttu-id="45626-117">如果尚未註冊，請註冊資源提供者 **Microsoft.insights**，並搭配儲存體帳戶及復原服務保存庫的訂用帳戶，來使報告資料能流入儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="45626-117">Register the resource provider **Microsoft.insights** if not registered already, with the subscription of storage account and also with the subscription of Recovery Services vault to enable reporting data to flow to the storage account.</span></span> <span data-ttu-id="45626-118">若要這麼做，您必須前往 Azure 入口網站 > [訂用帳戶] > [資源提供者]，並查看此提供者以註冊它。</span><span class="sxs-lookup"><span data-stu-id="45626-118">To do the same, you must go to Azure portal > Subscription > Resource providers and check for this provider to register it.</span></span> 

## <a name="configure-storage-account-for-reports"></a><span data-ttu-id="45626-119">針對報告設定儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="45626-119">Configure storage account for reports</span></span>
<span data-ttu-id="45626-120">使用下列步驟，以使用 Azure 入口網站針對復原服務保存庫設定儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="45626-120">Use the following steps to configure the storage account for recovery services vault using Azure portal.</span></span> <span data-ttu-id="45626-121">這是一次性設定，一旦設定好儲存體帳戶之後，您可以直接移至 Power BI 檢視內容套件並運用報告。</span><span class="sxs-lookup"><span data-stu-id="45626-121">This is a one-time configuration and once storage account is configured, you can go to Power BI directly to view content pack and leverage reports.</span></span>
1. <span data-ttu-id="45626-122">如果您已開啟復原服務保存庫，請繼續下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="45626-122">If you already have a Recovery Services vault open, proceed to next step.</span></span> <span data-ttu-id="45626-123">如果您並未開啟復原服務保存庫，但位於 Azure 入口網站中，請在 [中樞] 功能表上按一下 [瀏覽] 。</span><span class="sxs-lookup"><span data-stu-id="45626-123">If you do not have a Recovery Services vault open, but are in the Azure portal, on the Hub menu, click **Browse**.</span></span>

   * <span data-ttu-id="45626-124">在資源清單中輸入 **復原服務**。</span><span class="sxs-lookup"><span data-stu-id="45626-124">In the list of resources, type **Recovery Services**.</span></span>
   * <span data-ttu-id="45626-125">當您開始輸入時，清單會根據您輸入的文字進行篩選。</span><span class="sxs-lookup"><span data-stu-id="45626-125">As you begin typing, the list filters based on your input.</span></span> <span data-ttu-id="45626-126">當您看到 [復原服務保存庫] 時，請按一下它。</span><span class="sxs-lookup"><span data-stu-id="45626-126">When you see **Recovery Services vaults**, click it.</span></span>

      ![建立復原服務保存庫的步驟 1](./media/backup-azure-vms-encryption/browse-to-rs-vaults.png) <br/>

     <span data-ttu-id="45626-128">隨即會出現 [復原服務保存庫] 清單。</span><span class="sxs-lookup"><span data-stu-id="45626-128">The list of Recovery Services vaults appears.</span></span> <span data-ttu-id="45626-129">在 [復原服務保存庫] 清單中選取保存庫。</span><span class="sxs-lookup"><span data-stu-id="45626-129">From the list of Recovery Services vaults, select a vault.</span></span>

     <span data-ttu-id="45626-130">選取的保存庫儀表板隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="45626-130">The selected vault dashboard opens.</span></span>
2. <span data-ttu-id="45626-131">從保存庫下的項目清單中，按一下 [監視和報告] 區段下的 [備份報告]，以針對報告設定儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="45626-131">From the list of items that appears under vault, click **Backup Reports** under Monitoring and Reports section to configure the storage account for reports.</span></span>

      ![選取備份報告功能表項目步驟 2](./media/backup-azure-configure-reports/backup-reports-settings.PNG)
3. <span data-ttu-id="45626-133">在 [備份報告] 刀鋒視窗上，按一下 [設定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="45626-133">On the Backup Reports blade, click **Configure** button.</span></span> <span data-ttu-id="45626-134">這會開啟 [Azure Application Insights] 刀鋒視窗，可用來將資料推送到客戶儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="45626-134">This opens the Azure Application Insights blade which is used for pushing data to customer storage account.</span></span>

      ![設定儲存體帳戶步驟 3](./media/backup-azure-configure-reports/configure-storage-account.PNG)
4. <span data-ttu-id="45626-136">將 [狀態] 切換按鈕設定為[開啟] 並選取 [封存至儲存體帳戶] 核取方塊，讓報告資料可以開始流入儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="45626-136">Set the Status toggle button to **On** and select **Archive to a Storage Account** check box so that reporting data can start flowing in to the storage account.</span></span>

      ![啟用診斷步驟 4](./media/backup-azure-configure-reports/set-status-on.png)
5. <span data-ttu-id="45626-138">按一下 [儲存體帳戶] 選擇器，並從儲存報告資料的清單中選取儲存體帳戶，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="45626-138">Click Storage Account picker and select the storage account from the list for storing reporting data and click **OK**.</span></span>

      ![選取儲存體帳戶步驟 5](./media/backup-azure-configure-reports/select-storage-account.png)
6. <span data-ttu-id="45626-140">選取 [AzureBackupReport] 核取方塊，並移動滑桿以選取此報告資料的保留期限。</span><span class="sxs-lookup"><span data-stu-id="45626-140">Select **AzureBackupReport** check box and also move the slider to select retention period for this reporting data.</span></span> <span data-ttu-id="45626-141">儲存體帳戶中的報告資料會在使用此滑桿選取的期限內保留。</span><span class="sxs-lookup"><span data-stu-id="45626-141">Reporting data in the storage account is kept for the period selected using this slider.</span></span>

      ![選取儲存體帳戶步驟 6](./media/backup-azure-configure-reports/save-configuration.png)
7. <span data-ttu-id="45626-143">檢閱所有變更，然後按一下頂端的 [儲存] 按鈕，如上圖所示。</span><span class="sxs-lookup"><span data-stu-id="45626-143">Review all the changes and click **Save** button on top, as shown in the figure above.</span></span> <span data-ttu-id="45626-144">此動作可確保所有變更都會儲存，且儲存體帳戶已針對儲存報告資料進行設定。</span><span class="sxs-lookup"><span data-stu-id="45626-144">This action ensures that all your changes are saved and storage account is now configured for storing reporting data.</span></span>

> [!NOTE]
> <span data-ttu-id="45626-145">一旦您將儲存體帳戶儲存從而設定報告後，應該**等待 24 小時**，初始資料推送才會完成。</span><span class="sxs-lookup"><span data-stu-id="45626-145">Once you configure reports by saving storage account, you should **wait for 24 hours** for initial data push to complete.</span></span> <span data-ttu-id="45626-146">只有在該時間之後，您才需要將 Power BI 中的 Azure 備份內容套件匯入。</span><span class="sxs-lookup"><span data-stu-id="45626-146">You should import Azure Backup content pack in Power BI only after that time.</span></span> <span data-ttu-id="45626-147">如需進一步的詳細資料，請參閱[常見問題集一節](#frequently-asked-questions)。</span><span class="sxs-lookup"><span data-stu-id="45626-147">Refer [FAQ section](#frequently-asked-questions) for futher details.</span></span> 
>
>

## <a name="view-reports-in-power-bi"></a><span data-ttu-id="45626-148">在 Power BI 中檢視報告</span><span class="sxs-lookup"><span data-stu-id="45626-148">View reports in Power BI</span></span> 
<span data-ttu-id="45626-149">使用復原服務保存庫針對報告設定儲存體帳戶之後，報告資料大約需要 24 小時的時間才會開始流入。</span><span class="sxs-lookup"><span data-stu-id="45626-149">After configuring storage account for reports using recovery services vault, it takes around 24 hours for reporting data to start flowing in.</span></span> <span data-ttu-id="45626-150">在設定儲存體帳戶的 24 小時後，請使用下列步驟以在 Power BI 中檢視報告：</span><span class="sxs-lookup"><span data-stu-id="45626-150">After 24 hours of setting up storage account, use the following steps to view reports in Power BI:</span></span>
1. <span data-ttu-id="45626-151">[登入](https://powerbi.microsoft.com/landing/signin/) Power BI。</span><span class="sxs-lookup"><span data-stu-id="45626-151">[Sign in](https://powerbi.microsoft.com/landing/signin/) to Power BI.</span></span>
2. <span data-ttu-id="45626-152">按一下 [取得資料]，然後在內容套件庫中的 [服務] 底下，按一下 [取得]。</span><span class="sxs-lookup"><span data-stu-id="45626-152">Click **Get Data** and click Get under **Services** in Content Pack Library.</span></span> <span data-ttu-id="45626-153">使用[針對存取內容套件的 Power BI 文件](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-packs-services/)中所述的步驟。</span><span class="sxs-lookup"><span data-stu-id="45626-153">Use steps mentioned in [Power BI documentation to access content pack](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-packs-services/).</span></span>

     ![匯入內容套件](./media/backup-azure-configure-reports/content-pack-import.png)
3. <span data-ttu-id="45626-155">在搜尋列中輸入 **Azure Backup**，並按一下 [立即取得]。</span><span class="sxs-lookup"><span data-stu-id="45626-155">Type **Azure Backup** in Search bar and click **Get it now**.</span></span>

      ![取得內容套件](./media/backup-azure-configure-reports/content-pack-get.png)
4. <span data-ttu-id="45626-157">輸入上述步驟 5 中所設定的儲存體帳戶名稱，然後按一下 [下一步] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="45626-157">Enter the storage account name configured in step 5 above and click **Next** button.</span></span>

    ![輸入儲存體帳戶名稱](./media/backup-azure-configure-reports/content-pack-storage-account-name.png)    
5. <span data-ttu-id="45626-159">輸入此儲存體帳戶的儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="45626-159">Enter the storage account key for this storage account.</span></span> <span data-ttu-id="45626-160">您可以透過瀏覽至 Azure 入口網站中的儲存體帳戶，來[檢視並複製儲存體存取金鑰](../storage/common/storage-create-storage-account.md#manage-your-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="45626-160">You can [view and copy storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account) by navigating to your storage account in Azure portal.</span></span> 

     ![輸入儲存體帳戶](./media/backup-azure-configure-reports/content-pack-storage-account-key.png) <br/>
     
6. <span data-ttu-id="45626-162">按一下 [登入] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="45626-162">Click **Sign in** button.</span></span> <span data-ttu-id="45626-163">登入成功後，您會收到「匯入資料」的通知。</span><span class="sxs-lookup"><span data-stu-id="45626-163">After sign-in is successful, you get **Importing data** notification.</span></span>

    ![匯入內容套件](./media/backup-azure-configure-reports/content-pack-importing-data.png) <br/>
    
    <span data-ttu-id="45626-165">當匯入於一段時間後完成時，您會收到「成功」的通知。</span><span class="sxs-lookup"><span data-stu-id="45626-165">After some time, you get **Success** notification after the import is complete.</span></span> <span data-ttu-id="45626-166">如果儲存體帳戶中有大量資料，匯入內容套件可能需要較長時間。</span><span class="sxs-lookup"><span data-stu-id="45626-166">It might take little longer to import the content pack, if there is a lot of data in the storage account.</span></span>
    
    ![成功匯入內容套件](./media/backup-azure-configure-reports/content-pack-import-success.png) <br/>
    
7. <span data-ttu-id="45626-168">一旦成功匯入資料，[Azure 備份] 內容套件就可以在 [瀏覽] 窗格的 [應用程式] 中看到。</span><span class="sxs-lookup"><span data-stu-id="45626-168">Once data is imported successfully, **Azure Backup** content pack is visible in **Apps** in the navigation pane.</span></span> <span data-ttu-id="45626-169">現在該清單會顯示以黃色星號表示為新匯入報告的 Azure 備份儀表板、報告和資料集。</span><span class="sxs-lookup"><span data-stu-id="45626-169">The list now shows Azure Backup dashboard, reports, and dataset with a yellow star indicating newly imported reports.</span></span> 

     ![Azure 備份內容套件](./media/backup-azure-configure-reports/content-pack-azure-backup.png) <br/>
     
8. <span data-ttu-id="45626-171">按一下 [儀表板] 底下的 [Azure 備份]，這會顯示一組已釘選的重要資訊報告。</span><span class="sxs-lookup"><span data-stu-id="45626-171">Click **Azure Backup** under Dashboards, which shows a set of pinned key reports.</span></span>

      ![Azure 備份儀表板](./media/backup-azure-configure-reports/azure-backup-dashboard.png) <br/>
9. <span data-ttu-id="45626-173">若要檢視完整的報告組合，請按一下儀表板中的任何報告。</span><span class="sxs-lookup"><span data-stu-id="45626-173">To view the complete set of reports, click any report in the dashboard.</span></span>

      ![Azure 備份作業健康情況](./media/backup-azure-configure-reports/azure-backup-job-health.png) <br/>
10. <span data-ttu-id="45626-175">按一下報告中的每個索引標籤，以檢視該區域中的報告。</span><span class="sxs-lookup"><span data-stu-id="45626-175">Click each tab in the reports to view reports in that area.</span></span>

      ![Azure 備份報告索引標籤](./media/backup-azure-configure-reports/reports-tab-view.png)


## <a name="frequently-asked-questions"></a><span data-ttu-id="45626-177">常見問題集</span><span class="sxs-lookup"><span data-stu-id="45626-177">Frequently asked questions</span></span>
1. <span data-ttu-id="45626-178">**我該如何確認報告資料是否已開始流入儲存體帳戶？**</span><span class="sxs-lookup"><span data-stu-id="45626-178">**How do I check if reporting data has started flowing in to storage account?**</span></span>
    
    <span data-ttu-id="45626-179">您可以前往已設定的儲存體帳戶，然後選取容器。</span><span class="sxs-lookup"><span data-stu-id="45626-179">You can go to the storage account configured and select containers.</span></span> <span data-ttu-id="45626-180">如果容器有 insights-logs-azurebackupreport 的項目，則表示報告資料已經開始流入。</span><span class="sxs-lookup"><span data-stu-id="45626-180">If the container has an entry for insights-logs-azurebackupreport, it indicates that reporting data has started flowing in.</span></span>

2. <span data-ttu-id="45626-181">**將資料推送到儲存體帳戶和 Power BI 中 Azure 備份內容套件的頻率為何？**</span><span class="sxs-lookup"><span data-stu-id="45626-181">**What is the frequency of data push to storage account and Azure Backup content pack in Power BI?**</span></span>

   <span data-ttu-id="45626-182">針對使用時間尚未達一天的使用者，將資料推送到儲存體帳戶需要大約 24 小時。</span><span class="sxs-lookup"><span data-stu-id="45626-182">For Day 0 users, it would take around 24 hours to push data to storage account.</span></span> <span data-ttu-id="45626-183">完成此初始推送後，資料會以下圖所示的頻率重新整理。</span><span class="sxs-lookup"><span data-stu-id="45626-183">Once this initial push is compelete, data is refreshed with the following frequency shown in the figure below.</span></span> 
      * <span data-ttu-id="45626-184">與「作業、警示、備份項目、保存庫、受保護的伺服器，以及原則」相關的資料，將會在記錄資料的同時推送到客戶儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="45626-184">Data related to **Jobs, Alerts, Backup Items, Vaults, Protected Servers and Policies** is pushed to customer storage account as and when it is logged.</span></span>
      * <span data-ttu-id="45626-185">與「儲存體」相關的資料，將會每 24 小時推送到客戶儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="45626-185">Data related to **Storage** is pushed to customer storage account every 24 hours.</span></span>
   
    ![Azure 備份報表資料推送頻率](./media/backup-azure-configure-reports/reports-data-refresh-cycle.png)

  <span data-ttu-id="45626-187">Power BI 具有[一天一次的排程重新整理](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/#what-can-be-refreshed)。</span><span class="sxs-lookup"><span data-stu-id="45626-187">Power BI has a [scheduled refresh once a day](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/#what-can-be-refreshed).</span></span> <span data-ttu-id="45626-188">您可以手動重新整理 Power BI 中內容套件的資料。</span><span class="sxs-lookup"><span data-stu-id="45626-188">You can perform a manual refresh of the data in Power BI for the content pack.</span></span>

3. <span data-ttu-id="45626-189">**報告可以保留多久？**</span><span class="sxs-lookup"><span data-stu-id="45626-189">**How long can I retain the reports?**</span></span> 

   <span data-ttu-id="45626-190">在設定儲存體帳戶時，您可以選取儲存體帳戶中報告資料的保留期限 (使用上述＜針對報告設定儲存體帳戶＞一節中的步驟 6)。</span><span class="sxs-lookup"><span data-stu-id="45626-190">While configuring storage account, you can select retention period of reporting data in the storage account (using step 6 in Configure storage account for reports section above).</span></span> <span data-ttu-id="45626-191">除此之外，您可以根據需求[在 Excel 中分析報告](https://powerbi.microsoft.com/documentation/powerbi-service-analyze-in-excel/)並儲存它們，以延長保留期間。</span><span class="sxs-lookup"><span data-stu-id="45626-191">Besides that, you can [Analyze reports in excel](https://powerbi.microsoft.com/documentation/powerbi-service-analyze-in-excel/) and save them for a longer retention period, as per your needs.</span></span> 

4. <span data-ttu-id="45626-192">**我在設定儲存體帳戶後，是否能在報告中看到所有的資料？**</span><span class="sxs-lookup"><span data-stu-id="45626-192">**Will I see all my data in reports after configuring the storage account?**</span></span>

   <span data-ttu-id="45626-193">在「設定儲存體帳戶」後所產生的所有資料都會被推送到儲存體帳戶，並會出現在報告中。</span><span class="sxs-lookup"><span data-stu-id="45626-193">All the data generated after **"configuring storage account"** will be pushed to the storage account and will be available in reports.</span></span> <span data-ttu-id="45626-194">不過，「進行中的作業」將不會針對報告進行推送。</span><span class="sxs-lookup"><span data-stu-id="45626-194">However, **In Progress Jobs are not pushed** for Reporting.</span></span> <span data-ttu-id="45626-195">當作業完成或失敗之後，便會被傳送至報告。</span><span class="sxs-lookup"><span data-stu-id="45626-195">Once the job completes or fails, it is sent to reports.</span></span>

5. <span data-ttu-id="45626-196">**如果我已經設定儲存體帳戶以檢視報告，我是否可以變更設定以使用其他儲存體帳戶？**</span><span class="sxs-lookup"><span data-stu-id="45626-196">**If I have already configured the storage account to view reports, can I change the configuration to use another storage account?**</span></span> 

   <span data-ttu-id="45626-197">是。您可以變更設定以指向不同的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="45626-197">Yes, you can change the configuration to point to a different storage account.</span></span> <span data-ttu-id="45626-198">在連線到 Azure 備份內容套件時，您應該使用新設定的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="45626-198">You should use the newly configured storage account while connecting to Azure Backup content pack.</span></span> <span data-ttu-id="45626-199">此外，在設定不同的儲存體帳戶之後，新的資料將會流入這個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="45626-199">Also, once a different storage account is configured, new data would flow in this storage account.</span></span> <span data-ttu-id="45626-200">但是較舊的資料 (變更設定之前的資料) 仍會保留在較舊的儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="45626-200">But older data (before changing the configuration) would still remain in the older storage account.</span></span>

6. <span data-ttu-id="45626-201">**我是否可以檢視跨保存庫及跨訂用帳戶的報告？**</span><span class="sxs-lookup"><span data-stu-id="45626-201">**Can I view reports across vaults and across subscriptions?**</span></span> 

   <span data-ttu-id="45626-202">是。您可以在不同的保存庫上設定相同的儲存體帳戶，以檢視跨保存庫的報告。</span><span class="sxs-lookup"><span data-stu-id="45626-202">Yes, you can configure the same storage account across various vaults to view cross-vault reports.</span></span> <span data-ttu-id="45626-203">您也可以針對跨訂用帳戶的保存庫設定相同的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="45626-203">Also, you can configure the same storage account for vaults across subscriptions.</span></span> <span data-ttu-id="45626-204">您接著可以在連線至 Power BI 中的 Azure 備份內容套件時，使用這個儲存體帳戶來檢視報告。</span><span class="sxs-lookup"><span data-stu-id="45626-204">You can then use this storage account while connecting to Azure Backup content pack in Power BI to view the reports.</span></span> <span data-ttu-id="45626-205">不過，選取的儲存體帳戶應與復原服務保存庫位於相同的區域。</span><span class="sxs-lookup"><span data-stu-id="45626-205">However, the storage account selected should be in the same region as recovery services vault.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="45626-206">後續步驟</span><span class="sxs-lookup"><span data-stu-id="45626-206">Next steps</span></span>
<span data-ttu-id="45626-207">現在您已經設定好儲存體帳戶並匯入 Azure 備份內容套件，下一個步驟是自訂這些報告，並使用報告資料模型建立報告。</span><span class="sxs-lookup"><span data-stu-id="45626-207">Now that you have configured the storage account and imported Azure Backup content pack, the next step is to customize these reports and use reporting data model to create reports.</span></span> <span data-ttu-id="45626-208">如需詳細資料，請參閱下列文章。</span><span class="sxs-lookup"><span data-stu-id="45626-208">Refer the following articles for more details.</span></span>

* [<span data-ttu-id="45626-209">使用 Azure 備份報告資料模型</span><span class="sxs-lookup"><span data-stu-id="45626-209">Using Azure Backup reporting data model</span></span>](backup-azure-reports-data-model.md)
* [<span data-ttu-id="45626-210">在 Power BI 中篩選報告</span><span class="sxs-lookup"><span data-stu-id="45626-210">Filtering reports in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-service-about-filters-and-highlighting-in-reports/)
* [<span data-ttu-id="45626-211">在 Power BI 中建立報告</span><span class="sxs-lookup"><span data-stu-id="45626-211">Creating reports in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-service-create-a-new-report/)

