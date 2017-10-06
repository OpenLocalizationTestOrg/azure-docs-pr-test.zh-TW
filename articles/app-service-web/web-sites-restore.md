---
title: "aaaRestore 在 Azure 中的應用程式"
description: "深入了解如何 toorestore 從備份應用程式。"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 4444dbf7-363c-47e2-b24a-dbd45cb08491
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: 4b54029a9197064f990f29a3c4558c8322668714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-app-in-azure"></a><span data-ttu-id="a07ee-103">在 Azure 中還原應用程式</span><span class="sxs-lookup"><span data-stu-id="a07ee-103">Restore an app in Azure</span></span>
<span data-ttu-id="a07ee-104">本文章將示範如何中的應用程式的 toorestore [Azure App Service](../app-service/app-service-value-prop-what-is.md)您先前已備份的 (請參閱[備份您的應用程式在 Azure 中](web-sites-backup.md))。</span><span class="sxs-lookup"><span data-stu-id="a07ee-104">This article shows you how toorestore an app in [Azure App Service](../app-service/app-service-value-prop-what-is.md) that you have previously backed up (see [Back up your app in Azure](web-sites-backup.md)).</span></span> <span data-ttu-id="a07ee-105">您可以還原成連結的資料庫隨 tooa 先前的狀態，您的應用程式，或建立新的應用程式，以其中一個原始應用程式的備份。</span><span class="sxs-lookup"><span data-stu-id="a07ee-105">You can restore your app with its linked databases on-demand tooa previous state, or create a new app based on one of your original app's backup.</span></span> <span data-ttu-id="a07ee-106">Azure App Service 支援下列用於備份和還原資料庫的 hello:</span><span class="sxs-lookup"><span data-stu-id="a07ee-106">Azure App Service supports hello following databases for backup and restore:</span></span>
- [<span data-ttu-id="a07ee-107">SQL Database</span><span class="sxs-lookup"><span data-stu-id="a07ee-107">SQL Database</span></span>](https://azure.microsoft.com/en-us/services/sql-database/)
- [<span data-ttu-id="a07ee-108">適用於 MySQL 的 Azure 資料庫 (預覽)</span><span class="sxs-lookup"><span data-stu-id="a07ee-108">Azure Database for MySQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/mysql)
- [<span data-ttu-id="a07ee-109">適用於 PostgreSQL 的 Azure 資料庫 (預覽)</span><span class="sxs-lookup"><span data-stu-id="a07ee-109">Azure Database for PostgreSQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/postgres)
- [<span data-ttu-id="a07ee-110">ClearDB MySQL</span><span class="sxs-lookup"><span data-stu-id="a07ee-110">ClearDB MySQL</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
- [<span data-ttu-id="a07ee-111">應用程式內 MySQL</span><span class="sxs-lookup"><span data-stu-id="a07ee-111">MySQL in-app</span></span>](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)

<span data-ttu-id="a07ee-112">從備份還原為執行的可用 tooapps**標準**和**Premium**層。</span><span class="sxs-lookup"><span data-stu-id="a07ee-112">Restoring from backups is available tooapps running in **Standard** and **Premium** tier.</span></span> <span data-ttu-id="a07ee-113">如需有關相應增加應用程式的詳細資訊，請參閱 [在 Azure 中調整應用程式規模](web-sites-scale.md)。</span><span class="sxs-lookup"><span data-stu-id="a07ee-113">For information about scaling up your app, see [Scale up an app in Azure](web-sites-scale.md).</span></span> <span data-ttu-id="a07ee-114">**Premium**層可讓更多超過執行每日備份 toobe**標準**層。</span><span class="sxs-lookup"><span data-stu-id="a07ee-114">**Premium** tier allows a greater number of daily backups toobe performed than **Standard** tier.</span></span>

<a name="PreviousBackup"></a>

## <a name="restore-an-app-from-an-existing-backup"></a><span data-ttu-id="a07ee-115">從現有備份還原應用程式</span><span class="sxs-lookup"><span data-stu-id="a07ee-115">Restore an app from an existing backup</span></span>
1. <span data-ttu-id="a07ee-116">在 hello**設定**刀鋒視窗中的 hello Azure 入口網站中的應用程式按一下**備份**toodisplay hello**備份**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="a07ee-116">On hello **Settings** blade of your app in hello Azure Portal, click **Backups** toodisplay hello **Backups** blade.</span></span> <span data-ttu-id="a07ee-117">然後按一下 [還原]。</span><span class="sxs-lookup"><span data-stu-id="a07ee-117">Then click **Restore**.</span></span>
   
    ![選擇立即還原][ChooseRestoreNow]
2. <span data-ttu-id="a07ee-119">在 hello**還原**刀鋒視窗中，第一個選取的 hello 備份來源。</span><span class="sxs-lookup"><span data-stu-id="a07ee-119">In hello **Restore** blade, first select hello backup source.</span></span>
   
    ![](./media/web-sites-restore/021ChooseSource1.png)
   
    <span data-ttu-id="a07ee-120">hello**應用程式備份**選項會顯示所有 hello hello 目前應用程式的現有備份，及您可以輕鬆地選取其中一個。</span><span class="sxs-lookup"><span data-stu-id="a07ee-120">hello **App backup** option shows you all hello existing backups of hello current app, and you can easily select one.</span></span>
    <span data-ttu-id="a07ee-121">hello**儲存體**選項可讓您選取從任何現有的 Azure 儲存體帳戶和訂用帳戶中的容器的任何備份 ZIP 檔案。</span><span class="sxs-lookup"><span data-stu-id="a07ee-121">hello **Storage** option lets you select any backup ZIP file from any existing Azure Storage account and container in your subscription.</span></span>
    <span data-ttu-id="a07ee-122">如果您想要 toorestore 另一個應用程式的備份，使用 hello**儲存體**選項。</span><span class="sxs-lookup"><span data-stu-id="a07ee-122">If you're trying toorestore a backup of another app, use hello **Storage** option.</span></span>
3. <span data-ttu-id="a07ee-123">然後，指定 hello 應用程式還原中的 hello 目的地**還原目的地**。</span><span class="sxs-lookup"><span data-stu-id="a07ee-123">Then, specify hello destination for hello app restore in **Restore destination**.</span></span>
   
    ![](./media/web-sites-restore/022ChooseDestination1.png)
   
   > [!WARNING]
   > <span data-ttu-id="a07ee-124">如果您選擇 [覆寫]，則目前應用程式中的所有現有資料都將被清除並覆寫。</span><span class="sxs-lookup"><span data-stu-id="a07ee-124">If you choose **Overwrite**, all existing data in your current app is erased and overwritten.</span></span> <span data-ttu-id="a07ee-125">在您按一下之前**確定**，請確定它是只想 toodo。</span><span class="sxs-lookup"><span data-stu-id="a07ee-125">Before you click **OK**, make sure that it is exactly what you want toodo.</span></span>
   > 
   > 
   
    <span data-ttu-id="a07ee-126">您可以選取**現有應用程式**toorestore hello 應用程式備份 tooanother 應用程式在 hello 相同資源群組。</span><span class="sxs-lookup"><span data-stu-id="a07ee-126">You can select **Existing App** toorestore hello app backup tooanother app in hello same resoure group.</span></span> <span data-ttu-id="a07ee-127">使用此選項之前，您應該已經建立另一個應用程式與鏡像資料庫組態 toohello hello 應用程式備份中所定義的其中一個資源群組中。</span><span class="sxs-lookup"><span data-stu-id="a07ee-127">Before you use this option, you should have already created another app in your resource group with mirroring database configuration toohello one defined in hello app backup.</span></span> <span data-ttu-id="a07ee-128">您也可以建立**新增**應用程式 toorestore 您的內容。</span><span class="sxs-lookup"><span data-stu-id="a07ee-128">You can also Create a **New** app toorestore your content to.</span></span>

4. <span data-ttu-id="a07ee-129">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="a07ee-129">Click **OK**.</span></span>

<a name="StorageAccount"></a>

## <a name="download-or-delete-a-backup-from-a-storage-account"></a><span data-ttu-id="a07ee-130">從儲存體帳戶下載或刪除備份</span><span class="sxs-lookup"><span data-stu-id="a07ee-130">Download or delete a backup from a storage account</span></span>
1. <span data-ttu-id="a07ee-131">從主要 hello**瀏覽**刀鋒視窗中的 hello Azure 入口網站，選取**儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="a07ee-131">From hello main **Browse** blade of hello Azure portal, select **Storage accounts**.</span></span> <span data-ttu-id="a07ee-132">隨即會顯示您現有的儲存體帳戶清單。</span><span class="sxs-lookup"><span data-stu-id="a07ee-132">A list of your existing storage accounts is displayed.</span></span>
2. <span data-ttu-id="a07ee-133">選取包含您想要 toodownload 或 delete.hello hello 儲存體帳戶的刀鋒視窗會顯示 hello 備份 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a07ee-133">Select hello storage account that contains hello backup that you want toodownload or delete.hello blade for hello storage account is displayed.</span></span>
3. <span data-ttu-id="a07ee-134">在 hello 儲存體帳戶 刀鋒視窗，選取您想要的 hello 容器</span><span class="sxs-lookup"><span data-stu-id="a07ee-134">In hello storage account blade, select hello container you want</span></span>
   
    ![檢視容器][ViewContainers]
4. <span data-ttu-id="a07ee-136">選取您想要 toodownload 或刪除的備份檔案。</span><span class="sxs-lookup"><span data-stu-id="a07ee-136">Select backup file you want toodownload or delete.</span></span>
   
    ![ViewContainers](./media/web-sites-restore/03ViewFiles.png)
5. <span data-ttu-id="a07ee-138">按一下**下載**或**刪除**根據您想要 toodo。</span><span class="sxs-lookup"><span data-stu-id="a07ee-138">Click **Download** or **Delete** depending on what you want toodo.</span></span>  

<a name="OperationLogs"></a>

## <a name="monitor-a-restore-operation"></a><span data-ttu-id="a07ee-139">監視還原作業</span><span class="sxs-lookup"><span data-stu-id="a07ee-139">Monitor a restore operation</span></span>
<span data-ttu-id="a07ee-140">toosee 詳細 hello 成功或失敗的 hello 應用程式還原作業，瀏覽 toohello**活動記錄檔**hello Azure 入口網站中的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="a07ee-140">toosee details about hello success or failure of hello app restore operation, navigate toohello **Activity Log** blade in hello Azure portal.</span></span>  
 

<span data-ttu-id="a07ee-141">向下捲動 toofind hello 需要還原作業，並按一下 tooselect 它。</span><span class="sxs-lookup"><span data-stu-id="a07ee-141">Scroll down toofind hello desired restore operation and click tooselect it.</span></span>

<span data-ttu-id="a07ee-142">hello 詳細資料 刀鋒視窗會顯示 hello 可用相關 toohello 還原作業。</span><span class="sxs-lookup"><span data-stu-id="a07ee-142">hello details blade displays hello available information related toohello restore operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a07ee-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a07ee-143">Next Steps</span></span>
<span data-ttu-id="a07ee-144">您可以備份與還原 App Service 使用 REST API 的應用程式 (請參閱[使用 REST tooback 及還原 App Service 應用程式](websites-csm-backup.md))。</span><span class="sxs-lookup"><span data-stu-id="a07ee-144">You can backup and restore App Service apps using REST API (see [Use REST tooback up and restore App Service apps](websites-csm-backup.md)).</span></span>


<!-- IMAGES -->
[ChooseRestoreNow]: ./media/web-sites-restore/02ChooseRestoreNow1.png
[ViewContainers]: ./media/web-sites-restore/03ViewContainers.png
[StorageAccountFile]: ./media/web-sites-restore/02StorageAccountFile.png
[BrowseCloudStorage]: ./media/web-sites-restore/03BrowseCloudStorage.png
[StorageAccountFileSelected]: ./media/web-sites-restore/04StorageAccountFileSelected.png
[ChooseRestoreSettings]: ./media/web-sites-restore/05ChooseRestoreSettings.png
[ChooseDBServer]: ./media/web-sites-restore/06ChooseDBServer.png
[RestoreToNewSQLDB]: ./media/web-sites-restore/07RestoreToNewSQLDB.png
[NewSQLDBConfig]: ./media/web-sites-restore/08NewSQLDBConfig.png
[RestoredContosoWebSite]: ./media/web-sites-restore/09RestoredContosoWebSite.png
[DashboardOperationLogsLink]: ./media/web-sites-restore/10DashboardOperationLogsLink.png
[ManagementServicesOperationLogsList]: ./media/web-sites-restore/11ManagementServicesOperationLogsList.png
[DetailsButton]: ./media/web-sites-restore/12DetailsButton.png
[OperationDetails]: ./media/web-sites-restore/13OperationDetails.png
