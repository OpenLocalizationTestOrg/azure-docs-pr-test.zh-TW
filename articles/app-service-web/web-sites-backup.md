---
title: "備份您的應用程式在 Azure 中的 aaaBack"
description: "深入了解如何在 Azure App Service 中的應用程式的 toocreate 備份。"
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
ms.openlocfilehash: e41d93d322bbc48b45b28eeaa817928d83c2b9d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-your-app-in-azure"></a><span data-ttu-id="5f5c7-103">在 Azure 中備份應用程式</span><span class="sxs-lookup"><span data-stu-id="5f5c7-103">Back up your app in Azure</span></span>
<span data-ttu-id="5f5c7-104">hello 備份和還原功能[Azure App Service](../app-service/app-service-value-prop-what-is.md)可讓您輕鬆地建立應用程式備份，以手動方式或依據排程。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-104">hello Back up and Restore feature in [Azure App Service](../app-service/app-service-value-prop-what-is.md) lets you easily create app backups manually or on a schedule.</span></span> <span data-ttu-id="5f5c7-105">您可以覆寫 hello 現有應用程式或還原 tooanother 應用程式，以還原 hello 先前狀態的應用程式 tooa 快照集。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-105">You can restore hello app tooa snapshot of a previous state by overwriting hello existing app or restoring tooanother app.</span></span> 

<span data-ttu-id="5f5c7-106">如需從備份還原應用程式的相關資訊，請參閱 [在 Azure 中還原應用程式](web-sites-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-106">For information on restoring an app from backup, see [Restore an app in Azure](web-sites-restore.md).</span></span>

<a name="whatsbackedup"></a>

## <a name="what-gets-backed-up"></a><span data-ttu-id="5f5c7-107">備份什麼項目</span><span class="sxs-lookup"><span data-stu-id="5f5c7-107">What gets backed up</span></span>
<span data-ttu-id="5f5c7-108">應用程式服務可以備份 hello 下列資訊 tooan Azure 儲存體帳戶和設定應用程式 toouse 的容器。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-108">App Service can backup hello following information tooan Azure storage account and container that you have configured your app toouse.</span></span> 

* <span data-ttu-id="5f5c7-109">應用程式設定</span><span class="sxs-lookup"><span data-stu-id="5f5c7-109">App configuration</span></span>
* <span data-ttu-id="5f5c7-110">檔案內容</span><span class="sxs-lookup"><span data-stu-id="5f5c7-110">File content</span></span>
* <span data-ttu-id="5f5c7-111">資料庫連接的 tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="5f5c7-111">Database connected tooyour app</span></span>

<span data-ttu-id="5f5c7-112">備份功能支援下列資料庫方案的 hello:</span><span class="sxs-lookup"><span data-stu-id="5f5c7-112">hello following database solutions are supported with backup feature:</span></span> 
   - [<span data-ttu-id="5f5c7-113">SQL Database</span><span class="sxs-lookup"><span data-stu-id="5f5c7-113">SQL Database</span></span>](https://azure.microsoft.com/en-us/services/sql-database/)
   - [<span data-ttu-id="5f5c7-114">適用於 MySQL 的 Azure 資料庫 (預覽)</span><span class="sxs-lookup"><span data-stu-id="5f5c7-114">Azure Database for MySQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/mysql)
   - [<span data-ttu-id="5f5c7-115">適用於 PostgreSQL 的 Azure 資料庫 (預覽)</span><span class="sxs-lookup"><span data-stu-id="5f5c7-115">Azure Database for PostgreSQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/postgres)
   - [<span data-ttu-id="5f5c7-116">ClearDB MySQL</span><span class="sxs-lookup"><span data-stu-id="5f5c7-116">ClearDB MySQL</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
   - [<span data-ttu-id="5f5c7-117">應用程式內 MySQL</span><span class="sxs-lookup"><span data-stu-id="5f5c7-117">MySQL in-app</span></span>](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)
 

> [!NOTE]
>  <span data-ttu-id="5f5c7-118">每個備份都是應用程式的完整離線複本，而不是增量更新。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-118">Each backup is a complete offline copy of your app, not an incremental update.</span></span>
>  

<a name="requirements"></a>

## <a name="requirements-and-restrictions"></a><span data-ttu-id="5f5c7-119">需求和限制</span><span class="sxs-lookup"><span data-stu-id="5f5c7-119">Requirements and restrictions</span></span>
* <span data-ttu-id="5f5c7-120">hello 備份和還原功能需要 hello hello 中的應用程式服務計劃 toobe**標準**層或**Premium**層。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-120">hello Back up and Restore feature requires hello App Service plan toobe in hello **Standard** tier or **Premium** tier.</span></span> <span data-ttu-id="5f5c7-121">如需調整您的應用程式服務計劃 toouse 更高的層的詳細資訊，請參閱[在 Azure 中的應用程式向上延展](web-sites-scale.md)。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-121">For more information about scaling your App Service plan toouse a higher tier, see [Scale up an app in Azure](web-sites-scale.md).</span></span>  
  <span data-ttu-id="5f5c7-122">「進階」層所允許的每日備份數量比「標準」層多。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-122">**Premium** tier allows a greater number of daily back ups than **Standard** tier.</span></span>
* <span data-ttu-id="5f5c7-123">您需要 Azure 儲存體帳戶和容器在 hello hello 應用程式的 toobackup 相同訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-123">You need an Azure storage account and container in hello same subscription as hello app that you want toobackup.</span></span> <span data-ttu-id="5f5c7-124">如需有關 Azure 儲存體帳戶的詳細資訊，請參閱 hello[連結](#moreaboutstorage)hello 本文結尾處。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-124">For more information on Azure storage accounts, see hello [links](#moreaboutstorage) at hello end of this article.</span></span>
* <span data-ttu-id="5f5c7-125">備份可以是內容的 up too10 GB 的應用程式和資料庫。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-125">Backups can be up too10 GB of app and database content.</span></span> <span data-ttu-id="5f5c7-126">如果 hello 備份大小超過此限制，您會收到錯誤。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-126">If hello backup size exceeds this limit, you get an error .</span></span>

<a name="manualbackup"></a>

## <a name="create-a-manual-backup"></a><span data-ttu-id="5f5c7-127">建立手動備份</span><span class="sxs-lookup"><span data-stu-id="5f5c7-127">Create a manual backup</span></span>
1. <span data-ttu-id="5f5c7-128">在 hello [Azure 入口網站](https://portal.azure.com)、 瀏覽應用程式 tooyour 刀鋒視窗中，選取**備份**。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-128">In hello [Azure Portal](https://portal.azure.com), navigate tooyour app's blade, select **Backups**.</span></span> <span data-ttu-id="5f5c7-129">hello**備份**刀鋒視窗會顯示。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-129">hello **Backups** blade will be displayed.</span></span>
   
    ![Backups page][ChooseBackupsPage]
   
   > [!NOTE]
   > <span data-ttu-id="5f5c7-131">如果您看到以下的 hello 訊息，按一下的 tooupgrade 您的應用程式服務計劃之前您, 可以繼續進行備份。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-131">If you see hello message below, click it tooupgrade your App Service plan before you can proceed with backups.</span></span>
   > <span data-ttu-id="5f5c7-132">如需詳細資訊，請參閱 [在 Azure 中調整應用程式規模](web-sites-scale.md) 。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-132">See [Scale up an app in Azure](web-sites-scale.md) for more information.</span></span>  
   > <span data-ttu-id="5f5c7-133">![Choose storage account](./media/web-sites-backup/01UpgradePlan1.png)</span><span class="sxs-lookup"><span data-stu-id="5f5c7-133">![Choose storage account](./media/web-sites-backup/01UpgradePlan1.png)</span></span>
   > 
   > 

2. <span data-ttu-id="5f5c7-134">在 hello**備份**刀鋒視窗中，按一下**設定**
![按 [設定]](./media/web-sites-backup/ClickConfigure1.png)</span><span class="sxs-lookup"><span data-stu-id="5f5c7-134">In hello **Backup** blade, Click **Configure**
![Click Configure](./media/web-sites-backup/ClickConfigure1.png)</span></span>
3. <span data-ttu-id="5f5c7-135">在 hello**備份設定**刀鋒視窗中，按一下 **儲存體： 未設定**tooconfigure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-135">In hello **Backup Configuration** blade, click **Storage: Not configured** tooconfigure a storage account.</span></span>
   
    ![Choose storage account][ChooseStorageAccount]
4. <span data-ttu-id="5f5c7-137">選取 [儲存體帳戶] 和 [容器]，以選擇您的備份目的地。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-137">Choose your backup destination by selecting a **Storage Account** and **Container**.</span></span> <span data-ttu-id="5f5c7-138">hello 儲存體帳戶必須屬於 toohello hello 應用程式要 tooback 相同訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-138">hello storage account must belong toohello same subscription as hello app you want tooback up.</span></span> <span data-ttu-id="5f5c7-139">如果想要的話，您可以在 hello 個別刀鋒視窗中建立新的儲存體帳戶或新的容器。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-139">If you wish, you can create a new storage account or a new container in hello respective blades.</span></span> <span data-ttu-id="5f5c7-140">完成後，按一下 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-140">When you're done, click **Select**.</span></span>
   
    ![Choose storage account](./media/web-sites-backup/02ChooseStorageAccount1-1.png)
5. <span data-ttu-id="5f5c7-142">在 hello**備份設定**仍處於開啟狀態的刀鋒視窗，您可以設定**Backup Database**，然後選取 hello 資料庫 tooinclude hello 備份 （SQL database 或 MySQL），然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-142">In hello **Backup Configuration** blade that is still left open, you can configure **Backup Database**, then select hello databases you want tooinclude in hello backups (SQL database or MySQL), then click **OK**.</span></span>  
   
    ![Choose storage account](./media/web-sites-backup/03ConfigureDatabase1.png)
   
   > [!NOTE]
   > <span data-ttu-id="5f5c7-144">針對資料庫 tooappear 這份清單中，其連接字串必須存在於 hello**連接字串**區段 hello**應用程式設定**刀鋒視窗，您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-144">For a database tooappear in this list, its connection string must exist in hello **Connection strings** section of hello **Application settings** blade for your app.</span></span>
   > 
   > 
6. <span data-ttu-id="5f5c7-145">在 hello**備份設定**刀鋒視窗中，按一下 **儲存**。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-145">In hello **Backup Configuration** blade, click **Save**.</span></span>    
7. <span data-ttu-id="5f5c7-146">在 hello**備份**刀鋒視窗中，按一下 **備份**。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-146">In hello  **Backups** blade, click **Backup**.</span></span>
   
    ![BackUpNow button][BackUpNow]
   
    <span data-ttu-id="5f5c7-148">Hello 備份程序中看到進度訊息。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-148">You see a progress message during hello backup process.</span></span>

<span data-ttu-id="5f5c7-149">Hello 儲存體帳戶和容器設定之後您可以隨時起始手動備份。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-149">Once hello storage account and container is configured you can initiate a manual backup at any time.</span></span>  

<a name="automatedbackups"></a>

## <a name="configure-automated-backups"></a><span data-ttu-id="5f5c7-150">設定自動備份</span><span class="sxs-lookup"><span data-stu-id="5f5c7-150">Configure automated backups</span></span>
1. <span data-ttu-id="5f5c7-151">在 hello**備份設定**刀鋒視窗中，設定**已排程備份**太**上**。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-151">In hello **Backup Configuration** blade, set **Scheduled backup** too**On**.</span></span> 
   
    ![Choose storage account](./media/web-sites-backup/05ScheduleBackup1.png)
2. <span data-ttu-id="5f5c7-153">設定備份排程選項會顯示，**排定備份**太**上**，然後視需要設定 hello 備份排程，再按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-153">Backup schedule options will show up, set **Scheduled Backup** too**On**, then configure hello backup schedule as desired and click **OK**.</span></span>
   
    ![Enable automated backups][SetAutomatedBackupOn]

<a name="partialbackups"></a>

## <a name="configure-partial-backups"></a><span data-ttu-id="5f5c7-155">設定部分備份</span><span class="sxs-lookup"><span data-stu-id="5f5c7-155">Configure Partial Backups</span></span>
<span data-ttu-id="5f5c7-156">有時候您不想 toobackup 的所有項目在您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-156">Sometimes you don't want toobackup everything on your app.</span></span> <span data-ttu-id="5f5c7-157">以下是一些範例：</span><span class="sxs-lookup"><span data-stu-id="5f5c7-157">Here are a few examples:</span></span>

* <span data-ttu-id="5f5c7-158">您為包含永不變更的靜態內容 (例如舊部落格文章或影像) 的應用程式 [設定每週備份](web-sites-backup.md#configure-automated-backups) 。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-158">You [set up weekly backups](web-sites-backup.md#configure-automated-backups) of your app that contains static content that never changes, such as old blog posts or images.</span></span>
* <span data-ttu-id="5f5c7-159">您的應用程式具有超過 10 GB 的內容 （亦即 hello 最大數量，您可以備份一次）。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-159">Your app has over 10 GB of content (that's hello max amount you can backup at a time).</span></span>
* <span data-ttu-id="5f5c7-160">您不想 toobackup hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-160">You don't want toobackup hello log files.</span></span>

<span data-ttu-id="5f5c7-161">部分備份會讓您選擇正確的檔案，您想 toobackup。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-161">Partial backups allows you choose exactly which files you want toobackup.</span></span>

### <a name="exclude-files-from-your-backup"></a><span data-ttu-id="5f5c7-162">從備份中排除檔案</span><span class="sxs-lookup"><span data-stu-id="5f5c7-162">Exclude files from your backup</span></span>
<span data-ttu-id="5f5c7-163">假設您有應用程式，其中包含記錄檔和備份一次，而且不會成為 toochange 的靜態影像。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-163">Suppose you have an app that contains log files and static images that have been backup once and are not going toochange.</span></span> <span data-ttu-id="5f5c7-164">在這類情況下，您可以將這些資料夾和檔案排除，而不儲存在您未來的備份中。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-164">In such cases you can exclude those folders and files from being stored in your future backups.</span></span> <span data-ttu-id="5f5c7-165">tooexclude 檔案和資料夾從您的備份，建立`_backup.filter`檔案在 hello`D:\home\site\wwwroot`應用程式資料夾。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-165">tooexclude files and folders from your backups, create a `_backup.filter` file in hello `D:\home\site\wwwroot` folder of your app.</span></span> <span data-ttu-id="5f5c7-166">指定檔案和資料夾想 tooexclude 此檔案中的 hello 的清單。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-166">Specify hello list of files and folders you want tooexclude in this file.</span></span> 

<span data-ttu-id="5f5c7-167">您的檔案是 toouse Kudu 輕鬆 tooaccess。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-167">An easy way tooaccess your files is toouse Kudu .</span></span> <span data-ttu-id="5f5c7-168">按一下**進階工具]-> [移至**設定您的 web 應用程式 tooaccess Kudu。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-168">Click **Advanced Tools -> Go** setting for your web app tooaccess Kudu.</span></span>

![使用入口網站時的 Kuku][kudu-portal]

<span data-ttu-id="5f5c7-170">識別您想 tooexclude，從您的備份 hello 資料夾。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-170">Identify hello folders that you want tooexclude from your backups.</span></span>  <span data-ttu-id="5f5c7-171">例如，您會想 toofilter 出 hello 反白顯示的資料夾和檔案。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-171">For example , you want toofilter out hello highlighted folder and files.</span></span>

![Images 資料夾][ImagesFolder]

<span data-ttu-id="5f5c7-173">建立一個叫做檔案`_backup.filter`並將上述 hello 清單放入 hello 檔案，但移除`D:\home`。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-173">Create a file called `_backup.filter` and put hello list above in hello file, but remove `D:\home`.</span></span> <span data-ttu-id="5f5c7-174">一行列出一個目錄或檔案。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-174">List one directory or file per line.</span></span> <span data-ttu-id="5f5c7-175">因此 hello hello 檔案內容應該：</span><span class="sxs-lookup"><span data-stu-id="5f5c7-175">So hello content of hello file should be:</span></span>
 ```bash
    \site\wwwroot\Images\brand.png
    \site\wwwroot\Images\2014
    \site\wwwroot\Images\2013
```

<span data-ttu-id="5f5c7-176">上傳`_backup.filter`檔案 toohello`D:\home\site\wwwroot\`目錄的站台使用[ftp](web-sites-deploy.md#ftp)或任何其他方法。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-176">Upload `_backup.filter` file toohello `D:\home\site\wwwroot\` directory of your site using [ftp](web-sites-deploy.md#ftp) or any other method.</span></span> <span data-ttu-id="5f5c7-177">如果您希望，您可以建立 hello 檔案直接使用 Kudu`DebugConsole`並插入那里 hello 內容。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-177">If you wish, you can create hello file directly using Kudu  `DebugConsole` and insert hello content there.</span></span>

<span data-ttu-id="5f5c7-178">執行的備份 hello 相同方式，通常會進行，[手動](#create-a-manual-backup)或[自動](#configure-automated-backups)。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-178">Run backups hello same way you would normally do it, [manually](#create-a-manual-backup) or [automatically](#configure-automated-backups).</span></span> <span data-ttu-id="5f5c7-179">現在，任何的檔案和資料夾中所指定`_backup.filter`hello 未來的備份排程或手動起始已排除。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-179">Now, any files and folders that are specified in `_backup.filter` is excluded from hello future backups scheduled or manually initiated.</span></span> 

> [!NOTE]
> <span data-ttu-id="5f5c7-180">還原部分備份的站台 hello 一樣[還原定期備份](web-sites-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-180">You restore partial backups of your site hello same way you would [restore a regular backup](web-sites-restore.md).</span></span> <span data-ttu-id="5f5c7-181">hello 還原程序沒有 hello 正確的事。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-181">hello restore process does hello right thing.</span></span>
> 
> <span data-ttu-id="5f5c7-182">還原完整備份時，hello 站台上的所有內容會都取代任何處於 hello 備份。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-182">When a full backup is restored, all content on hello site is replaced with whatever is in hello backup.</span></span> <span data-ttu-id="5f5c7-183">如果檔案在 hello 站台，但不是在 hello 備份它被刪除。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-183">If a file is on hello site, but not in hello backup it gets deleted.</span></span> <span data-ttu-id="5f5c7-184">但是，還原部分備份時，位於其中一個 hello 列入黑名單中而目錄或任何列入封鎖清單的檔案中的任何內容保持原狀。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-184">But when a partial backup is restored, any content that is located in one of hello blacklisted directories, or any blacklisted file, is left as is.</span></span>
> 


<a name="aboutbackups"></a>

## <a name="how-backups-are-stored"></a><span data-ttu-id="5f5c7-185">備份的儲存方式</span><span class="sxs-lookup"><span data-stu-id="5f5c7-185">How backups are stored</span></span>
<span data-ttu-id="5f5c7-186">Hello 備份您的應用程式進行一個或多個備份之後，會顯示 hello**容器**刀鋒視窗中的儲存體帳戶和您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-186">After you have made one or more backups for your app, hello backups are visible on hello **Containers** blade of your storage account, and your app.</span></span> <span data-ttu-id="5f5c7-187">Hello 儲存體帳戶，在每個備份包含`.zip`包含 hello 備份資料檔案和`.xml`檔案，其中包含資訊清單的 hello`.zip`檔案內容。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-187">In hello storage account, each backup consists of a`.zip` file that contains hello backup data and an `.xml` file that contains a manifest of hello `.zip` file contents.</span></span> <span data-ttu-id="5f5c7-188">您可以解壓縮並瀏覽這些檔案，如果您想要 tooaccess 備份而不需實際執行應用程式還原。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-188">You can unzip and browse these files if you want tooaccess your backups without actually performing an app restore.</span></span>

<span data-ttu-id="5f5c7-189">hello hello 應用程式的資料庫備份會儲存在 hello the.zip 檔案根目錄中。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-189">hello database backup for hello app is stored in hello root of the.zip file.</span></span> <span data-ttu-id="5f5c7-190">若是 SQL 資料庫，這會是 BACPAC 檔案 (無副檔名)，而且可以匯入。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-190">For a SQL database, this is a BACPAC file (no file extension) and can be imported.</span></span> <span data-ttu-id="5f5c7-191">toocreate SQL database 根據 hello BACPAC 匯出，請參閱[匯入新的使用者資料庫的 BACPAC 檔案 tooCreate](http://technet.microsoft.com/library/hh710052.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-191">toocreate a SQL database based on hello BACPAC export, see [Import a BACPAC File tooCreate a New User Database](http://technet.microsoft.com/library/hh710052.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="5f5c7-192">改變任何 hello 檔案中您**websitebackups**容器可能會導致備份 hello toobecome 無效，因此非還原。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-192">Altering any of hello files in your **websitebackups** container can cause hello backup toobecome invalid and therefore non-restorable.</span></span>
> 
> 

<a name="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="5f5c7-193">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5f5c7-193">Next Steps</span></span>
<span data-ttu-id="5f5c7-194">如需從備份還原應用程式的相關資訊，請參閱 [在 Azure 中還原應用程式](web-sites-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-194">For information on restoring an app from a backup, see [Restore an app in Azure](web-sites-restore.md).</span></span> <span data-ttu-id="5f5c7-195">您也可以備份與還原 App Service 使用 REST API 的應用程式 (請參閱[使用 REST toobackup 與還原 App Service 應用程式](websites-csm-backup.md))。</span><span class="sxs-lookup"><span data-stu-id="5f5c7-195">You can also backup and restore App Service apps using REST API (see [Use REST toobackup and restore App Service apps](websites-csm-backup.md)).</span></span>


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

