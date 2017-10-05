---
title: "在 Azure 中備份應用程式"
description: "了解如何在 Azure App Service 中建立應用程式的備份。"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 6223b6bd-84ec-48df-943f-461d84605694
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: 77e983afaaba8e944ab1f337e1c28ced83b63205
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="back-up-your-app-in-azure"></a><span data-ttu-id="ccaeb-103">在 Azure 中備份應用程式</span><span class="sxs-lookup"><span data-stu-id="ccaeb-103">Back up your app in Azure</span></span>
<span data-ttu-id="ccaeb-104">[Azure App Service](../app-service/app-service-value-prop-what-is.md) 中的「備份與還原」功能可讓您以手動或透過排程方式輕鬆建立應用程式備份。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-104">The Back up and Restore feature in [Azure App Service](../app-service/app-service-value-prop-what-is.md) lets you easily create app backups manually or on a schedule.</span></span> <span data-ttu-id="ccaeb-105">您可以透過覆寫現有的應用程式或還原到另一個應用程式，將應用程式還原到先前狀態的快照。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-105">You can restore the app to a snapshot of a previous state by overwriting the existing app or restoring to another app.</span></span> 

<span data-ttu-id="ccaeb-106">如需從備份還原應用程式的相關資訊，請參閱 [在 Azure 中還原應用程式](web-sites-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-106">For information on restoring an app from backup, see [Restore an app in Azure](web-sites-restore.md).</span></span>

<a name="whatsbackedup"></a>

## <a name="what-gets-backed-up"></a><span data-ttu-id="ccaeb-107">備份什麼項目</span><span class="sxs-lookup"><span data-stu-id="ccaeb-107">What gets backed up</span></span>
<span data-ttu-id="ccaeb-108">App Service 可以將下列資訊備份到您已設定讓應用程式使用的 Azure 儲存體帳戶和容器。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-108">App Service can backup the following information to an Azure storage account and container that you have configured your app to use.</span></span> 

* <span data-ttu-id="ccaeb-109">應用程式設定</span><span class="sxs-lookup"><span data-stu-id="ccaeb-109">App configuration</span></span>
* <span data-ttu-id="ccaeb-110">檔案內容</span><span class="sxs-lookup"><span data-stu-id="ccaeb-110">File content</span></span>
* <span data-ttu-id="ccaeb-111">已連線到您應用程式的資料庫</span><span class="sxs-lookup"><span data-stu-id="ccaeb-111">Database connected to your app</span></span>

<span data-ttu-id="ccaeb-112">備份功能支援下列資料庫解決方案：</span><span class="sxs-lookup"><span data-stu-id="ccaeb-112">The following database solutions are supported with backup feature:</span></span> 
   - [<span data-ttu-id="ccaeb-113">SQL Database</span><span class="sxs-lookup"><span data-stu-id="ccaeb-113">SQL Database</span></span>](https://azure.microsoft.com/en-us/services/sql-database/)
   - [<span data-ttu-id="ccaeb-114">適用於 MySQL 的 Azure 資料庫 (預覽)</span><span class="sxs-lookup"><span data-stu-id="ccaeb-114">Azure Database for MySQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/mysql)
   - [<span data-ttu-id="ccaeb-115">適用於 PostgreSQL 的 Azure 資料庫 (預覽)</span><span class="sxs-lookup"><span data-stu-id="ccaeb-115">Azure Database for PostgreSQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/postgres)
   - [<span data-ttu-id="ccaeb-116">ClearDB MySQL</span><span class="sxs-lookup"><span data-stu-id="ccaeb-116">ClearDB MySQL</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
   - [<span data-ttu-id="ccaeb-117">應用程式內 MySQL</span><span class="sxs-lookup"><span data-stu-id="ccaeb-117">MySQL in-app</span></span>](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)
 

> [!NOTE]
>  <span data-ttu-id="ccaeb-118">每個備份都是應用程式的完整離線複本，而不是增量更新。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-118">Each backup is a complete offline copy of your app, not an incremental update.</span></span>
>  

<a name="requirements"></a>

## <a name="requirements-and-restrictions"></a><span data-ttu-id="ccaeb-119">需求和限制</span><span class="sxs-lookup"><span data-stu-id="ccaeb-119">Requirements and restrictions</span></span>
* <span data-ttu-id="ccaeb-120">若要使用「備份與還原」功能，App Service 方案必須屬於「標準」層或「進階」層。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-120">The Back up and Restore feature requires the App Service plan to be in the **Standard** tier or **Premium** tier.</span></span> <span data-ttu-id="ccaeb-121">如需有關調整 App Service 方案以使用更高階層的詳細資訊，請參閱 [在 Azure 中調整應用程式規模](web-sites-scale.md)。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-121">For more information about scaling your App Service plan to use a higher tier, see [Scale up an app in Azure](web-sites-scale.md).</span></span>  
  <span data-ttu-id="ccaeb-122">「進階」層所允許的每日備份數量比「標準」層多。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-122">**Premium** tier allows a greater number of daily back ups than **Standard** tier.</span></span>
* <span data-ttu-id="ccaeb-123">您的 Azure 儲存體帳戶和容器必須與所要備份之應用程式位於相同的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-123">You need an Azure storage account and container in the same subscription as the app that you want to backup.</span></span> <span data-ttu-id="ccaeb-124">如需 Azure 儲存體帳戶的詳細資訊，請參閱本文結尾處的 [連結](#moreaboutstorage) 。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-124">For more information on Azure storage accounts, see the [links](#moreaboutstorage) at the end of this article.</span></span>
* <span data-ttu-id="ccaeb-125">備份上限是 10 GB 的應用程式和資料庫內容。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-125">Backups can be up to 10 GB of app and database content.</span></span> <span data-ttu-id="ccaeb-126">如果備份大小超出此限制，您就會收到錯誤。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-126">If the backup size exceeds this limit, you get an error .</span></span>

<a name="manualbackup"></a>

## <a name="create-a-manual-backup"></a><span data-ttu-id="ccaeb-127">建立手動備份</span><span class="sxs-lookup"><span data-stu-id="ccaeb-127">Create a manual backup</span></span>
1. <span data-ttu-id="ccaeb-128">在 [Azure 入口網站](https://portal.azure.com)中，瀏覽至您應用程式的刀鋒視窗，並選取 [備份]。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-128">In the [Azure Portal](https://portal.azure.com), navigate to your app's blade, select **Backups**.</span></span> <span data-ttu-id="ccaeb-129">[備份]  刀鋒視窗隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-129">The **Backups** blade will be displayed.</span></span>
   
    ![Backups page][ChooseBackupsPage]
   
   > [!NOTE]
   > <span data-ttu-id="ccaeb-131">如果您看到下列訊息，請按一下訊息升級您的 App Service 方案，才可以繼續進行備份。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-131">If you see the message below, click it to upgrade your App Service plan before you can proceed with backups.</span></span>
   > <span data-ttu-id="ccaeb-132">如需詳細資訊，請參閱 [在 Azure 中調整應用程式規模](web-sites-scale.md) 。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-132">See [Scale up an app in Azure](web-sites-scale.md) for more information.</span></span>  
   > <span data-ttu-id="ccaeb-133">![Choose storage account](./media/web-sites-backup/01UpgradePlan1.png)</span><span class="sxs-lookup"><span data-stu-id="ccaeb-133">![Choose storage account](./media/web-sites-backup/01UpgradePlan1.png)</span></span>
   > 
   > 

2. <span data-ttu-id="ccaeb-134">在 [備份] 刀鋒視窗中，按一下 [設定]
![按一下 [設定]](./media/web-sites-backup/ClickConfigure1.png)</span><span class="sxs-lookup"><span data-stu-id="ccaeb-134">In the **Backup** blade, Click **Configure**
![Click Configure](./media/web-sites-backup/ClickConfigure1.png)</span></span>
3. <span data-ttu-id="ccaeb-135">在 [備份設定] 刀鋒視窗中，按一下 [儲存體: 未設定] 以設定儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-135">In the **Backup Configuration** blade, click **Storage: Not configured** to configure a storage account.</span></span>
   
    ![Choose storage account][ChooseStorageAccount]
4. <span data-ttu-id="ccaeb-137">選取 [儲存體帳戶] 和 [容器]，以選擇您的備份目的地。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-137">Choose your backup destination by selecting a **Storage Account** and **Container**.</span></span> <span data-ttu-id="ccaeb-138">此儲存體帳戶必須與您要備份之應用程式隸屬於相同的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-138">The storage account must belong to the same subscription as the app you want to back up.</span></span> <span data-ttu-id="ccaeb-139">如果您希望的話，也可以在個別的刀鋒視窗中，建立新的儲存體帳戶或新的容器。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-139">If you wish, you can create a new storage account or a new container in the respective blades.</span></span> <span data-ttu-id="ccaeb-140">完成後，按一下 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-140">When you're done, click **Select**.</span></span>
   
    ![Choose storage account](./media/web-sites-backup/02ChooseStorageAccount1-1.png)
5. <span data-ttu-id="ccaeb-142">在仍處於開啟狀態的 [備份設定] 刀鋒視窗中，您可以設定 [備份資料庫]，然後選取您想要包含在備份中的資料庫 (SQL Database 或 MySQL)，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-142">In the **Backup Configuration** blade that is still left open, you can configure **Backup Database**, then select the databases you want to include in the backups (SQL database or MySQL), then click **OK**.</span></span>  
   
    ![Choose storage account](./media/web-sites-backup/03ConfigureDatabase1.png)
   
   > [!NOTE]
   > <span data-ttu-id="ccaeb-144">若要讓資料庫出現在此清單中，其連接字串必須存在於您的應用程式之 [應用程式設定] 刀鋒視窗的 [連接字串] 區段中。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-144">For a database to appear in this list, its connection string must exist in the **Connection strings** section of the **Application settings** blade for your app.</span></span>
   > 
   > 
6. <span data-ttu-id="ccaeb-145">在 [備份設定] 刀鋒視窗中，按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-145">In the **Backup Configuration** blade, click **Save**.</span></span>    
7. <span data-ttu-id="ccaeb-146">在 [備份] 刀鋒視窗中，按一下 [備份]。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-146">In the  **Backups** blade, click **Backup**.</span></span>
   
    ![BackUpNow button][BackUpNow]
   
    <span data-ttu-id="ccaeb-148">在備份過程中，您會看見進度訊息。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-148">You see a progress message during the backup process.</span></span>

<span data-ttu-id="ccaeb-149">設定儲存體帳戶和容器之後，您隨時可以起始手動備份。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-149">Once the storage account and container is configured you can initiate a manual backup at any time.</span></span>  

<a name="automatedbackups"></a>

## <a name="configure-automated-backups"></a><span data-ttu-id="ccaeb-150">設定自動備份</span><span class="sxs-lookup"><span data-stu-id="ccaeb-150">Configure automated backups</span></span>
1. <span data-ttu-id="ccaeb-151">在 [備份設定] 刀鋒視窗中，將 [排定的備份] 設定為 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-151">In the **Backup Configuration** blade, set **Scheduled backup** to **On**.</span></span> 
   
    ![Choose storage account](./media/web-sites-backup/05ScheduleBackup1.png)
2. <span data-ttu-id="ccaeb-153">將會顯示備份排程選項，請將 [排定的備份] 設定為 [開啟]，然後視需要設定備份排程，並按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-153">Backup schedule options will show up, set **Scheduled Backup** to **On**, then configure the backup schedule as desired and click **OK**.</span></span>
   
    ![Enable automated backups][SetAutomatedBackupOn]

<a name="partialbackups"></a>

## <a name="configure-partial-backups"></a><span data-ttu-id="ccaeb-155">設定部分備份</span><span class="sxs-lookup"><span data-stu-id="ccaeb-155">Configure Partial Backups</span></span>
<span data-ttu-id="ccaeb-156">您有時不想要備份應用程式上的所有項目。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-156">Sometimes you don't want to backup everything on your app.</span></span> <span data-ttu-id="ccaeb-157">以下是一些範例：</span><span class="sxs-lookup"><span data-stu-id="ccaeb-157">Here are a few examples:</span></span>

* <span data-ttu-id="ccaeb-158">您為包含永不變更的靜態內容 (例如舊部落格文章或影像) 的應用程式 [設定每週備份](web-sites-backup.md#configure-automated-backups) 。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-158">You [set up weekly backups](web-sites-backup.md#configure-automated-backups) of your app that contains static content that never changes, such as old blog posts or images.</span></span>
* <span data-ttu-id="ccaeb-159">您應用程式的內容超過 10 GB (這是一次可備份的數量上限)。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-159">Your app has over 10 GB of content (that's the max amount you can backup at a time).</span></span>
* <span data-ttu-id="ccaeb-160">您不想要備份記錄檔。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-160">You don't want to backup the log files.</span></span>

<span data-ttu-id="ccaeb-161">部分備份可讓您精確選擇想要備份的檔案。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-161">Partial backups allows you choose exactly which files you want to backup.</span></span>

### <a name="exclude-files-from-your-backup"></a><span data-ttu-id="ccaeb-162">從備份中排除檔案</span><span class="sxs-lookup"><span data-stu-id="ccaeb-162">Exclude files from your backup</span></span>
<span data-ttu-id="ccaeb-163">假設您有一個應用程式，其中包含已經備份過一次且不會再變更的記錄檔和靜態映像。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-163">Suppose you have an app that contains log files and static images that have been backup once and are not going to change.</span></span> <span data-ttu-id="ccaeb-164">在這類情況下，您可以將這些資料夾和檔案排除，而不儲存在您未來的備份中。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-164">In such cases you can exclude those folders and files from being stored in your future backups.</span></span> <span data-ttu-id="ccaeb-165">若要將檔案和資料夾從您的備份中排除，請在應用程式的 `D:\home\site\wwwroot` 資料夾中建立 `_backup.filter` 檔案。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-165">To exclude files and folders from your backups, create a `_backup.filter` file in the `D:\home\site\wwwroot` folder of your app.</span></span> <span data-ttu-id="ccaeb-166">請在此檔案中指定您想要排除的檔案和資料夾清單。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-166">Specify the list of files and folders you want to exclude in this file.</span></span> 

<span data-ttu-id="ccaeb-167">有一個可輕鬆存取您檔案的方式，就是使用 Kudu。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-167">An easy way to access your files is to use Kudu .</span></span> <span data-ttu-id="ccaeb-168">請按一下您 Web 應用程式的 [進階工具] > [執行] 設定來存取 Kudu。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-168">Click **Advanced Tools -> Go** setting for your web app to access Kudu.</span></span>

![使用入口網站時的 Kuku][kudu-portal]

<span data-ttu-id="ccaeb-170">識別您想要從備份中排除的資料夾。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-170">Identify the folders that you want to exclude from your backups.</span></span>  <span data-ttu-id="ccaeb-171">例如，您想要篩選出醒目提示的資料夾和檔案。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-171">For example , you want to filter out the highlighted folder and files.</span></span>

![Images 資料夾][ImagesFolder]

<span data-ttu-id="ccaeb-173">建立名為 `_backup.filter` 的檔案並將上述清單放入此檔案中，但請移除 `D:\home`。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-173">Create a file called `_backup.filter` and put the list above in the file, but remove `D:\home`.</span></span> <span data-ttu-id="ccaeb-174">一行列出一個目錄或檔案。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-174">List one directory or file per line.</span></span> <span data-ttu-id="ccaeb-175">因此，檔案的內容應該如下：</span><span class="sxs-lookup"><span data-stu-id="ccaeb-175">So the content of the file should be:</span></span>
 ```bash
    \site\wwwroot\Images\brand.png
    \site\wwwroot\Images\2014
    \site\wwwroot\Images\2013
```

<span data-ttu-id="ccaeb-176">使用 [ftp](web-sites-deploy.md#ftp) 或任何其他方法，將 `_backup.filter` 檔案上傳到您站台的 `D:\home\site\wwwroot\` 目錄。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-176">Upload `_backup.filter` file to the `D:\home\site\wwwroot\` directory of your site using [ftp](web-sites-deploy.md#ftp) or any other method.</span></span> <span data-ttu-id="ccaeb-177">如果您希望的話，也可以使用 Kudu `DebugConsole` 直接建立該檔案，然後在該處插入內容。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-177">If you wish, you can create the file directly using Kudu  `DebugConsole` and insert the content there.</span></span>

<span data-ttu-id="ccaeb-178">以平常執行備份的相同方式執行備份：[手動](#create-a-manual-backup)或[自動](#configure-automated-backups)。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-178">Run backups the same way you would normally do it, [manually](#create-a-manual-backup) or [automatically](#configure-automated-backups).</span></span> <span data-ttu-id="ccaeb-179">現在，會將 `_backup.filter` 中指定的所有檔案和資料夾，從所排定或手動起始的未來備份中排除。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-179">Now, any files and folders that are specified in `_backup.filter` is excluded from the future backups scheduled or manually initiated.</span></span> 

> [!NOTE]
> <span data-ttu-id="ccaeb-180">您還原站台部分備份的方式會與[還原一般備份](web-sites-restore.md)的方式相同。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-180">You restore partial backups of your site the same way you would [restore a regular backup](web-sites-restore.md).</span></span> <span data-ttu-id="ccaeb-181">還原程序會執行正確的作業。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-181">The restore process does the right thing.</span></span>
> 
> <span data-ttu-id="ccaeb-182">還原完整備份時，網站上的所有內容都會取代為備份中的內容。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-182">When a full backup is restored, all content on the site is replaced with whatever is in the backup.</span></span> <span data-ttu-id="ccaeb-183">如果檔案在網站上，而不在備份中，系統就會將它刪除。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-183">If a file is on the site, but not in the backup it gets deleted.</span></span> <span data-ttu-id="ccaeb-184">但是，還原部分備份時，位於其中一個黑名單目錄或任何黑名單檔案中的任何內容都會保持原狀。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-184">But when a partial backup is restored, any content that is located in one of the blacklisted directories, or any blacklisted file, is left as is.</span></span>
> 


<a name="aboutbackups"></a>

## <a name="how-backups-are-stored"></a><span data-ttu-id="ccaeb-185">備份的儲存方式</span><span class="sxs-lookup"><span data-stu-id="ccaeb-185">How backups are stored</span></span>
<span data-ttu-id="ccaeb-186">在您為應用程式建立一或多個備份之後，這些備份就會顯示在您儲存體帳戶及應用程式的 [容器] 刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-186">After you have made one or more backups for your app, the backups are visible on the **Containers** blade of your storage account, and your app.</span></span> <span data-ttu-id="ccaeb-187">在儲存體帳戶中，每個備份都是由一個 `.zip` 檔案 (包含備份資料) 和一個 `.xml` 檔案 (包含 `.zip` 檔案內容的資訊清單) 所組成。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-187">In the storage account, each backup consists of a`.zip` file that contains the backup data and an `.xml` file that contains a manifest of the `.zip` file contents.</span></span> <span data-ttu-id="ccaeb-188">如果您要存取備份而不實際執行應用程式還原，則可以將這些檔案解壓縮並加以瀏覽。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-188">You can unzip and browse these files if you want to access your backups without actually performing an app restore.</span></span>

<span data-ttu-id="ccaeb-189">應用程式的資料庫備份則是儲存在 .zip 檔案的根目錄中。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-189">The database backup for the app is stored in the root of the.zip file.</span></span> <span data-ttu-id="ccaeb-190">若是 SQL 資料庫，這會是 BACPAC 檔案 (無副檔名)，而且可以匯入。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-190">For a SQL database, this is a BACPAC file (no file extension) and can be imported.</span></span> <span data-ttu-id="ccaeb-191">若要根據 BACPAC 匯出內容建立的 SQL Database，請參閱[匯入 BACPAC 檔案以建立新的使用者資料庫](http://technet.microsoft.com/library/hh710052.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-191">To create a SQL database based on the BACPAC export, see [Import a BACPAC File to Create a New User Database](http://technet.microsoft.com/library/hh710052.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="ccaeb-192">對 **websitebackups** 容器中的檔案進行任何變更，都可能導致備份失效，進而無法還原。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-192">Altering any of the files in your **websitebackups** container can cause the backup to become invalid and therefore non-restorable.</span></span>
> 
> 

<a name="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="ccaeb-193">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ccaeb-193">Next Steps</span></span>
<span data-ttu-id="ccaeb-194">如需從備份還原應用程式的相關資訊，請參閱 [在 Azure 中還原應用程式](web-sites-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-194">For information on restoring an app from a backup, see [Restore an app in Azure](web-sites-restore.md).</span></span> <span data-ttu-id="ccaeb-195">您也可以使用 REST API 來備份及還原 App Service 應用程式 (請參閱 [使用 REST 來備份及還原 App Service 應用程式](websites-csm-backup.md))。</span><span class="sxs-lookup"><span data-stu-id="ccaeb-195">You can also backup and restore App Service apps using REST API (see [Use REST to backup and restore App Service apps](websites-csm-backup.md)).</span></span>


<!-- IMAGES -->
[ChooseBackupsPage]: ./media/web-sites-backup/01ChooseBackupsPage1.png
[ChooseStorageAccount]: ./media/web-sites-backup/02ChooseStorageAccount-1.png
[IncludedDatabases]: ./media/web-sites-backup/03IncludedDatabases.png
[BackUpNow]: ./media/web-sites-backup/04BackUpNow1.png
[BackupProgress]: ./media/web-sites-backup/05BackupProgress.png
[SetAutomatedBackupOn]: ./media/web-sites-backup/06SetAutomatedBackupOn1.png
[Frequency]: ./media/web-sites-backup/07Frequency.png
[StartDate]: ./media/web-sites-backup/08StartDate.png
[StartTime]: ./media/web-sites-backup/09StartTime.png
[SaveIcon]: ./media/web-sites-backup/10SaveIcon.png
[ImagesFolder]: ./media/web-sites-backup/11Images.png
[LogsFolder]: ./media/web-sites-backup/12Logs.png
[GhostUpgradeWarning]: ./media/web-sites-backup/13GhostUpgradeWarning.png
[kudu-portal]:./media/web-sites-backup/kudu-portal.PNG

