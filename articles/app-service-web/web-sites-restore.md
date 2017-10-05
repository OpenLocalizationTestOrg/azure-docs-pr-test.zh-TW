---
title: "在 Azure 中還原應用程式"
description: "了解如何從備份還原您的應用程式。"
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
ms.openlocfilehash: 5fe74d992edb7028fa4a2500e427013d98ebc250
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="restore-an-app-in-azure"></a><span data-ttu-id="3d1aa-103">在 Azure 中還原應用程式</span><span class="sxs-lookup"><span data-stu-id="3d1aa-103">Restore an app in Azure</span></span>
<span data-ttu-id="3d1aa-104">本文說明如何在 [Azure App Service](../app-service/app-service-value-prop-what-is.md) 中還原您先前備份的應用程式 (請參閱[在 Azure 中備份應用程式](web-sites-backup.md))。</span><span class="sxs-lookup"><span data-stu-id="3d1aa-104">This article shows you how to restore an app in [Azure App Service](../app-service/app-service-value-prop-what-is.md) that you have previously backed up (see [Back up your app in Azure](web-sites-backup.md)).</span></span> <span data-ttu-id="3d1aa-105">您可以依需求將應用程式及其連結的資料庫還原到先前的狀態，或是根據您的其中一個原始應用程式備份來建立新的應用程式。</span><span class="sxs-lookup"><span data-stu-id="3d1aa-105">You can restore your app with its linked databases on-demand to a previous state, or create a new app based on one of your original app's backup.</span></span> <span data-ttu-id="3d1aa-106">Azure App Service 支援使用下列資料庫來進行備份與還原︰</span><span class="sxs-lookup"><span data-stu-id="3d1aa-106">Azure App Service supports the following databases for backup and restore:</span></span>
- [<span data-ttu-id="3d1aa-107">SQL Database</span><span class="sxs-lookup"><span data-stu-id="3d1aa-107">SQL Database</span></span>](https://azure.microsoft.com/en-us/services/sql-database/)
- [<span data-ttu-id="3d1aa-108">適用於 MySQL 的 Azure 資料庫 (預覽)</span><span class="sxs-lookup"><span data-stu-id="3d1aa-108">Azure Database for MySQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/mysql)
- [<span data-ttu-id="3d1aa-109">適用於 PostgreSQL 的 Azure 資料庫 (預覽)</span><span class="sxs-lookup"><span data-stu-id="3d1aa-109">Azure Database for PostgreSQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/postgres)
- [<span data-ttu-id="3d1aa-110">ClearDB MySQL</span><span class="sxs-lookup"><span data-stu-id="3d1aa-110">ClearDB MySQL</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
- [<span data-ttu-id="3d1aa-111">應用程式內 MySQL</span><span class="sxs-lookup"><span data-stu-id="3d1aa-111">MySQL in-app</span></span>](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)

<span data-ttu-id="3d1aa-112">從備份還原是提供給在**標準**和**進階**層中執行的應用程式使用。</span><span class="sxs-lookup"><span data-stu-id="3d1aa-112">Restoring from backups is available to apps running in **Standard** and **Premium** tier.</span></span> <span data-ttu-id="3d1aa-113">如需有關相應增加應用程式的詳細資訊，請參閱 [在 Azure 中調整應用程式規模](web-sites-scale.md)。</span><span class="sxs-lookup"><span data-stu-id="3d1aa-113">For information about scaling up your app, see [Scale up an app in Azure](web-sites-scale.md).</span></span> <span data-ttu-id="3d1aa-114">**進階**層所允許執行的每日備份數量比**標準**層多。</span><span class="sxs-lookup"><span data-stu-id="3d1aa-114">**Premium** tier allows a greater number of daily backups to be performed than **Standard** tier.</span></span>

<a name="PreviousBackup"></a>

## <a name="restore-an-app-from-an-existing-backup"></a><span data-ttu-id="3d1aa-115">從現有備份還原應用程式</span><span class="sxs-lookup"><span data-stu-id="3d1aa-115">Restore an app from an existing backup</span></span>
1. <span data-ttu-id="3d1aa-116">在「Azure 入口網站」中您應用程式的 [設定] 刀鋒視窗上，按一下 [備份] 以顯示 [備份] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="3d1aa-116">On the **Settings** blade of your app in the Azure Portal, click **Backups** to display the **Backups** blade.</span></span> <span data-ttu-id="3d1aa-117">然後按一下 [還原]。</span><span class="sxs-lookup"><span data-stu-id="3d1aa-117">Then click **Restore**.</span></span>
   
    ![選擇立即還原][ChooseRestoreNow]
2. <span data-ttu-id="3d1aa-119">在 [還原]  刀鋒視窗中，先選取備份來源。</span><span class="sxs-lookup"><span data-stu-id="3d1aa-119">In the **Restore** blade, first select the backup source.</span></span>
   
    ![](./media/web-sites-restore/021ChooseSource1.png)
   
    <span data-ttu-id="3d1aa-120">[應用程式備份]  選項會顯示目前應用程式的所有現有備份，您可以輕鬆地選取其中一個。</span><span class="sxs-lookup"><span data-stu-id="3d1aa-120">The **App backup** option shows you all the existing backups of the current app, and you can easily select one.</span></span>
    <span data-ttu-id="3d1aa-121">[儲存體]  選項可讓您從您訂用帳戶中任何現有 Azure 儲存體帳戶和容器中，選取任何備份 ZIP 檔案。</span><span class="sxs-lookup"><span data-stu-id="3d1aa-121">The **Storage** option lets you select any backup ZIP file from any existing Azure Storage account and container in your subscription.</span></span>
    <span data-ttu-id="3d1aa-122">如果您想要還原另一個應用程式的備份，請使用 [儲存體]  選項。</span><span class="sxs-lookup"><span data-stu-id="3d1aa-122">If you're trying to restore a backup of another app, use the **Storage** option.</span></span>
3. <span data-ttu-id="3d1aa-123">接著，在 [還原目的地] 中指定應用程式還原目的地。</span><span class="sxs-lookup"><span data-stu-id="3d1aa-123">Then, specify the destination for the app restore in **Restore destination**.</span></span>
   
    ![](./media/web-sites-restore/022ChooseDestination1.png)
   
   > [!WARNING]
   > <span data-ttu-id="3d1aa-124">如果您選擇 [覆寫]，則目前應用程式中的所有現有資料都將被清除並覆寫。</span><span class="sxs-lookup"><span data-stu-id="3d1aa-124">If you choose **Overwrite**, all existing data in your current app is erased and overwritten.</span></span> <span data-ttu-id="3d1aa-125">按一下 [確定] 之前，請確定這確實是您想要執行的動作。</span><span class="sxs-lookup"><span data-stu-id="3d1aa-125">Before you click **OK**, make sure that it is exactly what you want to do.</span></span>
   > 
   > 
   
    <span data-ttu-id="3d1aa-126">您可以選取 [現有應用程式]  ，將應用程式備份還原到相同資源群組中的另一個應用程式。</span><span class="sxs-lookup"><span data-stu-id="3d1aa-126">You can select **Existing App** to restore the app backup to another app in the same resoure group.</span></span> <span data-ttu-id="3d1aa-127">使用此選項之前，您應該已經在資源群組中，建立具有應用程式備份中所定義之資料庫組態的鏡像資料庫組態的另一個應用程式。</span><span class="sxs-lookup"><span data-stu-id="3d1aa-127">Before you use this option, you should have already created another app in your resource group with mirroring database configuration to the one defined in the app backup.</span></span> <span data-ttu-id="3d1aa-128">您也可以建立**新**應用程式作為還原內容的目標。</span><span class="sxs-lookup"><span data-stu-id="3d1aa-128">You can also Create a **New** app to restore your content to.</span></span>

4. <span data-ttu-id="3d1aa-129">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="3d1aa-129">Click **OK**.</span></span>

<a name="StorageAccount"></a>

## <a name="download-or-delete-a-backup-from-a-storage-account"></a><span data-ttu-id="3d1aa-130">從儲存體帳戶下載或刪除備份</span><span class="sxs-lookup"><span data-stu-id="3d1aa-130">Download or delete a backup from a storage account</span></span>
1. <span data-ttu-id="3d1aa-131">從 Azure 入口網站的主要 [瀏覽] 刀鋒視窗中，選取 [儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="3d1aa-131">From the main **Browse** blade of the Azure portal, select **Storage accounts**.</span></span> <span data-ttu-id="3d1aa-132">隨即會顯示您現有的儲存體帳戶清單。</span><span class="sxs-lookup"><span data-stu-id="3d1aa-132">A list of your existing storage accounts is displayed.</span></span>
2. <span data-ttu-id="3d1aa-133">選取包含您想要下載或刪除之備份的儲存體帳戶。隨即會顯示儲存體帳戶的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="3d1aa-133">Select the storage account that contains the backup that you want to download or delete.The blade for the storage account is displayed.</span></span>
3. <span data-ttu-id="3d1aa-134">在儲存體帳戶刀鋒視窗中，選取所需的容器</span><span class="sxs-lookup"><span data-stu-id="3d1aa-134">In the storage account blade, select the container you want</span></span>
   
    ![檢視容器][ViewContainers]
4. <span data-ttu-id="3d1aa-136">選取您想要下載或刪除的備份檔案。</span><span class="sxs-lookup"><span data-stu-id="3d1aa-136">Select backup file you want to download or delete.</span></span>
   
    ![ViewContainers](./media/web-sites-restore/03ViewFiles.png)
5. <span data-ttu-id="3d1aa-138">按一下 [下載] 或 [刪除]，視您要進行的作業而定。</span><span class="sxs-lookup"><span data-stu-id="3d1aa-138">Click **Download** or **Delete** depending on what you want to do.</span></span>  

<a name="OperationLogs"></a>

## <a name="monitor-a-restore-operation"></a><span data-ttu-id="3d1aa-139">監視還原作業</span><span class="sxs-lookup"><span data-stu-id="3d1aa-139">Monitor a restore operation</span></span>
<span data-ttu-id="3d1aa-140">若要查看有關應用程式還原作業成功或失敗的詳細資訊，請瀏覽至 Azure 入口網站中的 [活動記錄] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="3d1aa-140">To see details about the success or failure of the app restore operation, navigate to the **Activity Log** blade in the Azure portal.</span></span>  
 

<span data-ttu-id="3d1aa-141">向下捲動以尋找所要的還原作業，並按一下以選取它。</span><span class="sxs-lookup"><span data-stu-id="3d1aa-141">Scroll down to find the desired restore operation and click to select it.</span></span>

<span data-ttu-id="3d1aa-142">詳細資料刀鋒視窗會顯示與還原作業有關的可用資訊。</span><span class="sxs-lookup"><span data-stu-id="3d1aa-142">The details blade displays the available information related to the restore operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d1aa-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3d1aa-143">Next Steps</span></span>
<span data-ttu-id="3d1aa-144">您可以使用 REST API 來備份及還原 App Service 應用程式 (請參閱[使用 REST 來備份及還原 App Service 應用程式](websites-csm-backup.md))。</span><span class="sxs-lookup"><span data-stu-id="3d1aa-144">You can backup and restore App Service apps using REST API (see [Use REST to back up and restore App Service apps](websites-csm-backup.md)).</span></span>


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
