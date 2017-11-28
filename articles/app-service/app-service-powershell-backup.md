---
title: "aaaUse PowerShell tooback 及還原 App Service 應用程式"
description: "深入了解如何 toouse PowerShell tooback 及還原 Azure App Service 中的應用程式"
services: app-service
documentationcenter: 
author: NKing92
manager: erikre
editor: 
ms.assetid: 7ea8661e-aefb-4823-9626-6bff980cdebf
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2016
ms.author: nicking
ms.openlocfilehash: 4042166f6c650841926f010056d6c80ab2de57e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooback-up-and-restore-app-service-apps"></a><span data-ttu-id="c34bd-103">使用 PowerShell tooback] 和 [還原 App Service 應用程式</span><span class="sxs-lookup"><span data-stu-id="c34bd-103">Use PowerShell tooback up and restore App Service apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c34bd-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c34bd-104">PowerShell</span></span>](app-service-powershell-backup.md)
> * [<span data-ttu-id="c34bd-105">REST API</span><span class="sxs-lookup"><span data-stu-id="c34bd-105">REST API</span></span>](../app-service-web/websites-csm-backup.md)
> 
> 

<span data-ttu-id="c34bd-106">深入了解如何 toouse Azure PowerShell tooback 及還原[App Service 應用程式](https://azure.microsoft.com/services/app-service/web/)。</span><span class="sxs-lookup"><span data-stu-id="c34bd-106">Learn how toouse Azure PowerShell tooback up and restore [App Service apps](https://azure.microsoft.com/services/app-service/web/).</span></span> <span data-ttu-id="c34bd-107">如需有關 Web 應用程式備份的詳細資訊，包括需求和限制，請參閱 [在 Azure App Service 中備份 Web 應用程式](../app-service-web/web-sites-backup.md)。</span><span class="sxs-lookup"><span data-stu-id="c34bd-107">For more information about web app backups, including requirements and restrictions, see [Back up a web app in Azure App Service](../app-service-web/web-sites-backup.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c34bd-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="c34bd-108">Prerequisites</span></span>
<span data-ttu-id="c34bd-109">toouse PowerShell toomanage 您應用程式的備份，您需要遵循的 hello:</span><span class="sxs-lookup"><span data-stu-id="c34bd-109">toouse PowerShell toomanage your app backups, you need hello following:</span></span>

* <span data-ttu-id="c34bd-110">**SAS URL** ，可讓讀取和寫入權限 tooan Azure 儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="c34bd-110">**A SAS URL** that allows read and write access tooan Azure Storage container.</span></span> <span data-ttu-id="c34bd-111">請參閱[了解 hello SAS 模型](../storage/common/storage-dotnet-shared-access-signature-part-1.md)取得 SAS Url 的說明。</span><span class="sxs-lookup"><span data-stu-id="c34bd-111">See [Understanding hello SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) for an explanation of SAS URLs.</span></span> <span data-ttu-id="c34bd-112">如需使用 PowerShell 管理 Azure 儲存體的範例，請參閱 [搭配使用 Azure PowerShell 與 Azure 儲存體](../storage/common/storage-powershell-guide-full.md) 。</span><span class="sxs-lookup"><span data-stu-id="c34bd-112">See [Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) for examples of managing Azure Storage using PowerShell.</span></span>
* <span data-ttu-id="c34bd-113">**資料庫連接字串**如果您想將資料庫 tooback 您 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c34bd-113">**A database connection string** if you want tooback up a database along with your web app.</span></span>

### <a name="how-toogenerate-a-sas-url-toouse-with-hello-web-app-backup-cmdlets"></a><span data-ttu-id="c34bd-114">Toogenerate SAS URL toouse hello web 應用程式與如何備份 cmdlet</span><span class="sxs-lookup"><span data-stu-id="c34bd-114">How toogenerate a SAS URL toouse with hello web app backup cmdlets</span></span>
<span data-ttu-id="c34bd-115">您可以使用 PowerShell 產生 SAS URL。</span><span class="sxs-lookup"><span data-stu-id="c34bd-115">A SAS URL can be generated with PowerShell.</span></span> <span data-ttu-id="c34bd-116">以下是如何 toogenerate 可以搭配 hello cmdlet 的其中一個本文所討論的範例。</span><span class="sxs-lookup"><span data-stu-id="c34bd-116">Here is an example of how toogenerate one that can be used with hello cmdlets discussed in this article.</span></span>

        $storageAccountName = "<your storage account's name>"
        $storageAccountRg = "<your storage account's resource group>"

        # This returns an array of keys for your storage account. Be sure tooselect hello appropriate key. Here we select hello first key as a default.
        $storageAccountKey = Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccountRg -Name $storageAccountName
        $context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey[0].Value

        $blobContainerName = "<name of blob container for app backups>"
        $sasUrl = New-AzureStorageContainerSASToken -Name $blobContainerName -Permission rwdl -Context $context -ExpiryTime (Get-Date).AddMonths(1) -FullUri

## <a name="install-azure-powershell-132-or-greater"></a><span data-ttu-id="c34bd-117">安裝 Azure PowerShell 1.3.2 或更新版本</span><span class="sxs-lookup"><span data-stu-id="c34bd-117">Install Azure PowerShell 1.3.2 or greater</span></span>
<span data-ttu-id="c34bd-118">如需安裝和使用 Azure PowerShell 的指示，請參閱 [搭配使用 Azure PowerShell 與 Azure Resource Manager](/powershell/azure/overview) 。</span><span class="sxs-lookup"><span data-stu-id="c34bd-118">See [Using Azure PowerShell with Azure Resource Manager](/powershell/azure/overview) for instructions on installing and using Azure PowerShell.</span></span>

## <a name="create-a-backup"></a><span data-ttu-id="c34bd-119">建立備份</span><span class="sxs-lookup"><span data-stu-id="c34bd-119">Create a backup</span></span>
<span data-ttu-id="c34bd-120">使用 hello 新增 AzureRmWebAppBackup cmdlet toocreate web 應用程式的備份。</span><span class="sxs-lookup"><span data-stu-id="c34bd-120">Use hello New-AzureRmWebAppBackup cmdlet toocreate a backup of a web app.</span></span>

        $sasUrl = "<your SAS URL>"
        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl

<span data-ttu-id="c34bd-121">這會以自動產生的名稱建立備份。</span><span class="sxs-lookup"><span data-stu-id="c34bd-121">This creates a backup with an automatically generated name.</span></span> <span data-ttu-id="c34bd-122">如果您想要 tooprovide 您備份的名稱，使用 hello BackupName 選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="c34bd-122">If you would like tooprovide a name for your backup, use hello BackupName optional parameter.</span></span>

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl -BackupName MyBackup

<span data-ttu-id="c34bd-123">tooinclude hello 備份中的資料庫第一次建立資料庫的備份設定，使用 hello 新增 AzureRmWebAppDatabaseBackupSetting cmdlet，然後提供該設定在 hello hello 新增 AzureRmWebAppBackup cmdlet 資料庫參數。</span><span class="sxs-lookup"><span data-stu-id="c34bd-123">tooinclude a database in hello backup, first create a database backup setting using hello New-AzureRmWebAppDatabaseBackupSetting cmdlet, then supply that setting in hello Databases parameter of hello New-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="c34bd-124">hello 資料庫參數接受允許您 tooback 多個資料庫的資料庫設定的陣列。</span><span class="sxs-lookup"><span data-stu-id="c34bd-124">hello Databases parameter accepts an array of database settings, allowing you tooback up more than one database.</span></span>

        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbBackup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupName MyBackup -StorageAccountUrl $sasUrl -Databases $dbSetting1,$dbSetting2

## <a name="get-backups"></a><span data-ttu-id="c34bd-125">取得備份</span><span class="sxs-lookup"><span data-stu-id="c34bd-125">Get backups</span></span>
<span data-ttu-id="c34bd-126">hello Get AzureRmWebAppBackupList cmdlet 會傳回陣列的 web 應用程式中的所有備份。</span><span class="sxs-lookup"><span data-stu-id="c34bd-126">hello Get-AzureRmWebAppBackupList cmdlet returns an array of all backups for a web app.</span></span> <span data-ttu-id="c34bd-127">您必須提供 hello hello web 應用程式名稱和其資源群組。</span><span class="sxs-lookup"><span data-stu-id="c34bd-127">You must supply hello name of hello web app and its resource group.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $backups = Get-AzureRmWebAppBackupList -Name $appName -ResourceGroupName $resourceGroupName

<span data-ttu-id="c34bd-128">tooget 特定備份，使用 hello Get AzureRmWebAppBackup 指令程式。</span><span class="sxs-lookup"><span data-stu-id="c34bd-128">tooget a specific backup, use hello Get-AzureRmWebAppBackup cmdlet.</span></span>

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102

<span data-ttu-id="c34bd-129">您也可以將 web 應用程式物件傳送至任一個 hello 備份管理 cmdlet，為了方便起見。</span><span class="sxs-lookup"><span data-stu-id="c34bd-129">You can also pipe a web app object into any of hello backup management cmdlets for convenience.</span></span>

        $app = Get-AzureRmWebApp -Name ContosoApp -ResourceGroupName Default-Web-WestUS
        $backupList = $app | Get-AzureRmWebAppBackupList
        $backup = $app | Get-AzureRmWebAppBackup -BackupId 10102

## <a name="schedule-automatic-backups"></a><span data-ttu-id="c34bd-130">排程自動備份</span><span class="sxs-lookup"><span data-stu-id="c34bd-130">Schedule automatic backups</span></span>
<span data-ttu-id="c34bd-131">您可以依指定的間隔自動排程備份 toohappen。</span><span class="sxs-lookup"><span data-stu-id="c34bd-131">You can schedule backups toohappen automatically at a specified interval.</span></span> <span data-ttu-id="c34bd-132">tooconfigure 備份排程，使用 hello 編輯 AzureRmWebAppBackupConfiguration 指令程式。</span><span class="sxs-lookup"><span data-stu-id="c34bd-132">tooconfigure a backup schedule, use hello Edit-AzureRmWebAppBackupConfiguration cmdlet.</span></span> <span data-ttu-id="c34bd-133">此 Cmdlet 會採用數個參數︰</span><span class="sxs-lookup"><span data-stu-id="c34bd-133">This cmdlet takes several parameters:</span></span>

* <span data-ttu-id="c34bd-134">**名稱**-hello hello web 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="c34bd-134">**Name** - hello name of hello web app.</span></span>
* <span data-ttu-id="c34bd-135">**ResourceGroupName** -hello hello 資源群組包含 hello web 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="c34bd-135">**ResourceGroupName** - hello name of hello resource group containing hello web app.</span></span>
* <span data-ttu-id="c34bd-136">**Slot** - 選用。</span><span class="sxs-lookup"><span data-stu-id="c34bd-136">**Slot** - Optional.</span></span> <span data-ttu-id="c34bd-137">hello hello web 應用程式位置名稱。</span><span class="sxs-lookup"><span data-stu-id="c34bd-137">hello name of hello web app slot.</span></span>
* <span data-ttu-id="c34bd-138">**StorageAccountUrl** -hello Azure 儲存體容器使用 toostore hello 備份 hello SAS URL。</span><span class="sxs-lookup"><span data-stu-id="c34bd-138">**StorageAccountUrl** - hello SAS URL for hello Azure Storage container used toostore hello backups.</span></span>
* <span data-ttu-id="c34bd-139">**FrequencyInterval** -頻率 hello 備份應該設定成數值。</span><span class="sxs-lookup"><span data-stu-id="c34bd-139">**FrequencyInterval** - Numeric value for how often hello backups should be made.</span></span> <span data-ttu-id="c34bd-140">必須是正整數。</span><span class="sxs-lookup"><span data-stu-id="c34bd-140">Must be a positive integer.</span></span>
* <span data-ttu-id="c34bd-141">**FrequencyUnit** -的頻率 hello 應該備份來進行時間單位。</span><span class="sxs-lookup"><span data-stu-id="c34bd-141">**FrequencyUnit** - Unit of time for how often hello backups should be made.</span></span> <span data-ttu-id="c34bd-142">選項為 [小時] 和 [天]。</span><span class="sxs-lookup"><span data-stu-id="c34bd-142">Options are Hour and Day.</span></span>
* <span data-ttu-id="c34bd-143">**RetentionPeriodInDays** -hello 自動備份應該儲存之前不會自動刪除的天數。</span><span class="sxs-lookup"><span data-stu-id="c34bd-143">**RetentionPeriodInDays** - How many days hello automatic backups should be saved before being automatically deleted.</span></span>
* <span data-ttu-id="c34bd-144">**StartTime** - 選用。</span><span class="sxs-lookup"><span data-stu-id="c34bd-144">**StartTime** - Optional.</span></span> <span data-ttu-id="c34bd-145">hello hello 自動備份應開始的時間。</span><span class="sxs-lookup"><span data-stu-id="c34bd-145">hello time when hello automatic backups should begin.</span></span> <span data-ttu-id="c34bd-146">如果這是 null，將立即開始備份。</span><span class="sxs-lookup"><span data-stu-id="c34bd-146">Backups begin immediately if this is null.</span></span> <span data-ttu-id="c34bd-147">必須是 DateTime。</span><span class="sxs-lookup"><span data-stu-id="c34bd-147">Must be a DateTime.</span></span>
* <span data-ttu-id="c34bd-148">**Databases** - 選用。</span><span class="sxs-lookup"><span data-stu-id="c34bd-148">**Databases** - Optional.</span></span> <span data-ttu-id="c34bd-149">Hello 資料庫 toobackup DatabaseBackupSettings 的陣列。</span><span class="sxs-lookup"><span data-stu-id="c34bd-149">An array of DatabaseBackupSettings for hello databases toobackup.</span></span>
* <span data-ttu-id="c34bd-150">**KeepAtLeastOneBackup** - 選擇性切換參數。</span><span class="sxs-lookup"><span data-stu-id="c34bd-150">**KeepAtLeastOneBackup** - Optional switched parameter.</span></span> <span data-ttu-id="c34bd-151">這如果一個備份應該永遠保持 hello 儲存體帳戶，無論它是舊的供應器。</span><span class="sxs-lookup"><span data-stu-id="c34bd-151">Supply this if one backup should always be kept in hello storage account, regardless of how old it is.</span></span>

<span data-ttu-id="c34bd-152">以下是如何的範例 toouse 這個指令程式。</span><span class="sxs-lookup"><span data-stu-id="c34bd-152">Following is an example of how toouse this cmdlet.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Edit-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName -Slot $slotName `
          -StorageAccountUrl "<your SAS URL>" -FrequencyInterval 6 -FrequencyUnit Hour -Databases $dbSetting1,$dbSetting2 `
          -KeepAtLeastOneBackup -StartTime (Get-Date).AddHours(1)

<span data-ttu-id="c34bd-153">tooget hello 目前的備份排程，使用 hello Get AzureRmWebAppBackupConfiguration 指令程式。</span><span class="sxs-lookup"><span data-stu-id="c34bd-153">tooget hello current backup schedule, use hello Get-AzureRmWebAppBackupConfiguration cmdlet.</span></span> <span data-ttu-id="c34bd-154">這很適合用於修改已設定的排程。</span><span class="sxs-lookup"><span data-stu-id="c34bd-154">This can be useful for modifying a schedule that has already been configured.</span></span>

        $configuration = Get-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName

        # Modify hello configuration slightly
        $configuration.FrequencyInterval = 2
        $configuration.FrequencyUnit = "Day"

        # Apply hello new configuration by piping it into hello Edit-AzureRmWebAppBackupConfiguration cmdlet
        $configuration | Edit-AzureRmWebAppBackupConfiguration

## <a name="restore-a-web-app-from-a-backup"></a><span data-ttu-id="c34bd-155">從備份還原 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="c34bd-155">Restore a web app from a backup</span></span>
<span data-ttu-id="c34bd-156">toorestore web 應用程式，從備份使用 hello 還原 AzureRmWebAppBackup 指令程式。</span><span class="sxs-lookup"><span data-stu-id="c34bd-156">toorestore a web app from a backup, use hello Restore-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="c34bd-157">最簡單方式 toouse hello 這個指令程式是 toopipe 備份物件擷取自 hello Get AzureRmWebAppBackup cmdlet 或 Get AzureRmWebAppBackupList cmdlet 中。</span><span class="sxs-lookup"><span data-stu-id="c34bd-157">hello easiest way toouse this cmdlet is toopipe in a backup object retrieved from hello Get-AzureRmWebAppBackup cmdlet or Get-AzureRmWebAppBackupList cmdlet.</span></span>

<span data-ttu-id="c34bd-158">備份的物件之後，您可以將其傳送到 hello 還原 AzureRmWebAppBackup cmdlet。</span><span class="sxs-lookup"><span data-stu-id="c34bd-158">Once you have a backup object, you can pipe it into hello Restore-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="c34bd-159">指定您想 toooverwrite hello 的內容，您的 web 應用程式的 hello 備份的 hello 內容 hello 覆寫參數參數 tooindicate。</span><span class="sxs-lookup"><span data-stu-id="c34bd-159">Specify hello Overwrite switch parameter tooindicate that you intend toooverwrite hello contents of your web app with hello contents of hello backup.</span></span> <span data-ttu-id="c34bd-160">如果 hello 備份包含資料庫，這些資料庫也會一併還原。</span><span class="sxs-lookup"><span data-stu-id="c34bd-160">If hello backup contains databases, those databases are restored as well.</span></span>

        $backup | Restore-AzureRmWebAppBackup -Overwrite

<span data-ttu-id="c34bd-161">以下是範例 toouse hello 還原 AzureRmWebAppBackup 藉由指定所有 hello 參數的方式。</span><span class="sxs-lookup"><span data-stu-id="c34bd-161">Following is an example of how toouse hello Restore-AzureRmWebAppBackup by specifying all hello parameters.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $blobName = "ContosoBackup.zip"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Restore-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -Slot $slotName -StorageAccountUrl "<your SAS URL>" -BlobName $blobName -Databases $dbSetting1,$dbSetting2 -Overwrite

## <a name="delete-a-backup"></a><span data-ttu-id="c34bd-162">刪除備份</span><span class="sxs-lookup"><span data-stu-id="c34bd-162">Delete a backup</span></span>
<span data-ttu-id="c34bd-163">toodelete 備份時，使用 hello 移除 AzureRmWebAppBackup 指令程式。</span><span class="sxs-lookup"><span data-stu-id="c34bd-163">toodelete a backup, use hello Remove-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="c34bd-164">這會移除 hello 備份從儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c34bd-164">This removes hello backup from your storage account.</span></span> <span data-ttu-id="c34bd-165">指定您的應用程式名稱，其資源群組，然後 hello 識別碼 hello 備份您想要 toodelete。</span><span class="sxs-lookup"><span data-stu-id="c34bd-165">Specify your app name, its resource group, and hello ID of hello backup you want toodelete.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        Remove-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupId 10102

<span data-ttu-id="c34bd-166">您也可以將備份的物件傳送至 hello 移除 AzureRmWebAppBackup cmdlet toodelete 它。</span><span class="sxs-lookup"><span data-stu-id="c34bd-166">You can also pipe a backup object into hello Remove-AzureRmWebAppBackup cmdlet toodelete it.</span></span>

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102
        $backup | Remove-AzureRmWebAppBackup -Overwrite
