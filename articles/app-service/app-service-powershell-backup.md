---
title: "使用 PowerShell 來備份及還原 App Service 應用程式"
description: "了解如何使用 PowerShell 來備份和還原 Azure App Service 中的應用程式"
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
ms.openlocfilehash: 34a7e1d025c301ca056753d964bb3c5f4f1a62d8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-powershell-to-back-up-and-restore-app-service-apps"></a><span data-ttu-id="c80a3-103">使用 PowerShell 來備份及還原 App Service 應用程式</span><span class="sxs-lookup"><span data-stu-id="c80a3-103">Use PowerShell to back up and restore App Service apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c80a3-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c80a3-104">PowerShell</span></span>](app-service-powershell-backup.md)
> * [<span data-ttu-id="c80a3-105">REST API</span><span class="sxs-lookup"><span data-stu-id="c80a3-105">REST API</span></span>](../app-service-web/websites-csm-backup.md)
> 
> 

<span data-ttu-id="c80a3-106">了解如何使用 Azure PowerShell 來備份及還原 [App Service 應用程式](https://azure.microsoft.com/services/app-service/web/)。</span><span class="sxs-lookup"><span data-stu-id="c80a3-106">Learn how to use Azure PowerShell to back up and restore [App Service apps](https://azure.microsoft.com/services/app-service/web/).</span></span> <span data-ttu-id="c80a3-107">如需有關 Web 應用程式備份的詳細資訊，包括需求和限制，請參閱 [在 Azure App Service 中備份 Web 應用程式](../app-service-web/web-sites-backup.md)。</span><span class="sxs-lookup"><span data-stu-id="c80a3-107">For more information about web app backups, including requirements and restrictions, see [Back up a web app in Azure App Service](../app-service-web/web-sites-backup.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c80a3-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="c80a3-108">Prerequisites</span></span>
<span data-ttu-id="c80a3-109">若要使用 PowerShell 來管理您的應用程式備份，您需要下列項目︰</span><span class="sxs-lookup"><span data-stu-id="c80a3-109">To use PowerShell to manage your app backups, you need the following:</span></span>

* <span data-ttu-id="c80a3-110">**SAS URL** ，提供 Azure 儲存體容器的讀取和寫入存取權。</span><span class="sxs-lookup"><span data-stu-id="c80a3-110">**A SAS URL** that allows read and write access to an Azure Storage container.</span></span> <span data-ttu-id="c80a3-111">如需 SAS URL 的說明，請參閱 [了解 SAS 模型](../storage/common/storage-dotnet-shared-access-signature-part-1.md) 。</span><span class="sxs-lookup"><span data-stu-id="c80a3-111">See [Understanding the SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) for an explanation of SAS URLs.</span></span> <span data-ttu-id="c80a3-112">如需使用 PowerShell 管理 Azure 儲存體的範例，請參閱 [搭配使用 Azure PowerShell 與 Azure 儲存體](../storage/common/storage-powershell-guide-full.md) 。</span><span class="sxs-lookup"><span data-stu-id="c80a3-112">See [Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) for examples of managing Azure Storage using PowerShell.</span></span>
* <span data-ttu-id="c80a3-113">**資料庫連接字串** ，如果您想要備份資料庫和 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c80a3-113">**A database connection string** if you want to back up a database along with your web app.</span></span>

### <a name="how-to-generate-a-sas-url-to-use-with-the-web-app-backup-cmdlets"></a><span data-ttu-id="c80a3-114">如何產生 SAS URL 以搭配 Web 應用程式備份 Cmdlet 使用</span><span class="sxs-lookup"><span data-stu-id="c80a3-114">How to generate a SAS URL to use with the web app backup cmdlets</span></span>
<span data-ttu-id="c80a3-115">您可以使用 PowerShell 產生 SAS URL。</span><span class="sxs-lookup"><span data-stu-id="c80a3-115">A SAS URL can be generated with PowerShell.</span></span> <span data-ttu-id="c80a3-116">以下是如何產生一個 SAS URL 以搭配本文所討論的 Cmdlet 使用的範例。</span><span class="sxs-lookup"><span data-stu-id="c80a3-116">Here is an example of how to generate one that can be used with the cmdlets discussed in this article.</span></span>

        $storageAccountName = "<your storage account's name>"
        $storageAccountRg = "<your storage account's resource group>"

        # This returns an array of keys for your storage account. Be sure to select the appropriate key. Here we select the first key as a default.
        $storageAccountKey = Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccountRg -Name $storageAccountName
        $context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey[0].Value

        $blobContainerName = "<name of blob container for app backups>"
        $sasUrl = New-AzureStorageContainerSASToken -Name $blobContainerName -Permission rwdl -Context $context -ExpiryTime (Get-Date).AddMonths(1) -FullUri

## <a name="install-azure-powershell-132-or-greater"></a><span data-ttu-id="c80a3-117">安裝 Azure PowerShell 1.3.2 或更新版本</span><span class="sxs-lookup"><span data-stu-id="c80a3-117">Install Azure PowerShell 1.3.2 or greater</span></span>
<span data-ttu-id="c80a3-118">如需安裝和使用 Azure PowerShell 的指示，請參閱 [搭配使用 Azure PowerShell 與 Azure Resource Manager](/powershell/azure/overview) 。</span><span class="sxs-lookup"><span data-stu-id="c80a3-118">See [Using Azure PowerShell with Azure Resource Manager](/powershell/azure/overview) for instructions on installing and using Azure PowerShell.</span></span>

## <a name="create-a-backup"></a><span data-ttu-id="c80a3-119">建立備份</span><span class="sxs-lookup"><span data-stu-id="c80a3-119">Create a backup</span></span>
<span data-ttu-id="c80a3-120">使用 New-AzureRmWebAppBackup Cmdlet 來建立 Web 應用程式的備份。</span><span class="sxs-lookup"><span data-stu-id="c80a3-120">Use the New-AzureRmWebAppBackup cmdlet to create a backup of a web app.</span></span>

        $sasUrl = "<your SAS URL>"
        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl

<span data-ttu-id="c80a3-121">這會以自動產生的名稱建立備份。</span><span class="sxs-lookup"><span data-stu-id="c80a3-121">This creates a backup with an automatically generated name.</span></span> <span data-ttu-id="c80a3-122">如果您要為您的備份提供名稱，請使用 BackupName 選用參數。</span><span class="sxs-lookup"><span data-stu-id="c80a3-122">If you would like to provide a name for your backup, use the BackupName optional parameter.</span></span>

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl -BackupName MyBackup

<span data-ttu-id="c80a3-123">若要將資料庫包含在備份中，請先使用 New-AzureRmWebAppDatabaseBackupSetting Cmdlet 建立資料庫備份設定，然後在 New-AzureRmWebAppBackup Cmdlet 的 Databases 參數中提供該設定。</span><span class="sxs-lookup"><span data-stu-id="c80a3-123">To include a database in the backup, first create a database backup setting using the New-AzureRmWebAppDatabaseBackupSetting cmdlet, then supply that setting in the Databases parameter of the New-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="c80a3-124">Databases 參數可接受資料庫設定陣列，讓您備份一個以上的資料庫。</span><span class="sxs-lookup"><span data-stu-id="c80a3-124">The Databases parameter accepts an array of database settings, allowing you to back up more than one database.</span></span>

        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbBackup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupName MyBackup -StorageAccountUrl $sasUrl -Databases $dbSetting1,$dbSetting2

## <a name="get-backups"></a><span data-ttu-id="c80a3-125">取得備份</span><span class="sxs-lookup"><span data-stu-id="c80a3-125">Get backups</span></span>
<span data-ttu-id="c80a3-126">Get-AzureRmWebAppBackupList Cmdlet 會傳回 Web 應用程式的所有備份陣列。</span><span class="sxs-lookup"><span data-stu-id="c80a3-126">The Get-AzureRmWebAppBackupList cmdlet returns an array of all backups for a web app.</span></span> <span data-ttu-id="c80a3-127">您必須提供 Web 應用程式與其資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="c80a3-127">You must supply the name of the web app and its resource group.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $backups = Get-AzureRmWebAppBackupList -Name $appName -ResourceGroupName $resourceGroupName

<span data-ttu-id="c80a3-128">若要取得特定備份，請使用 Get-AzureRmWebAppBackup Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="c80a3-128">To get a specific backup, use the Get-AzureRmWebAppBackup cmdlet.</span></span>

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102

<span data-ttu-id="c80a3-129">為了方便，您也可以使用管線將 Web 應用程式物件傳送至任何備份管理 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="c80a3-129">You can also pipe a web app object into any of the backup management cmdlets for convenience.</span></span>

        $app = Get-AzureRmWebApp -Name ContosoApp -ResourceGroupName Default-Web-WestUS
        $backupList = $app | Get-AzureRmWebAppBackupList
        $backup = $app | Get-AzureRmWebAppBackup -BackupId 10102

## <a name="schedule-automatic-backups"></a><span data-ttu-id="c80a3-130">排程自動備份</span><span class="sxs-lookup"><span data-stu-id="c80a3-130">Schedule automatic backups</span></span>
<span data-ttu-id="c80a3-131">您可以排程備份以在指定的間隔自動進行。</span><span class="sxs-lookup"><span data-stu-id="c80a3-131">You can schedule backups to happen automatically at a specified interval.</span></span> <span data-ttu-id="c80a3-132">若要設定備份排程，請使用 Edit-AzureRmWebAppBackupConfiguration Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="c80a3-132">To configure a backup schedule, use the Edit-AzureRmWebAppBackupConfiguration cmdlet.</span></span> <span data-ttu-id="c80a3-133">此 Cmdlet 會採用數個參數︰</span><span class="sxs-lookup"><span data-stu-id="c80a3-133">This cmdlet takes several parameters:</span></span>

* <span data-ttu-id="c80a3-134">**Name** - Web 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="c80a3-134">**Name** - The name of the web app.</span></span>
* <span data-ttu-id="c80a3-135">**ResourceGroupName** - 包含 Web 應用程式之資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="c80a3-135">**ResourceGroupName** - The name of the resource group containing the web app.</span></span>
* <span data-ttu-id="c80a3-136">**Slot** - 選用。</span><span class="sxs-lookup"><span data-stu-id="c80a3-136">**Slot** - Optional.</span></span> <span data-ttu-id="c80a3-137">Web 應用程式位置的名稱。</span><span class="sxs-lookup"><span data-stu-id="c80a3-137">The name of the web app slot.</span></span>
* <span data-ttu-id="c80a3-138">**StorageAccountUrl** - 用來儲存備份的 Azure 儲存體容器的 SAS URL。</span><span class="sxs-lookup"><span data-stu-id="c80a3-138">**StorageAccountUrl** - The SAS URL for the Azure Storage container used to store the backups.</span></span>
* <span data-ttu-id="c80a3-139">**FrequencyInterval** - 應多久進行一次備份的數值。</span><span class="sxs-lookup"><span data-stu-id="c80a3-139">**FrequencyInterval** - Numeric value for how often the backups should be made.</span></span> <span data-ttu-id="c80a3-140">必須是正整數。</span><span class="sxs-lookup"><span data-stu-id="c80a3-140">Must be a positive integer.</span></span>
* <span data-ttu-id="c80a3-141">**FrequencyUnit** - 應多久進行一次備份的時間單位。</span><span class="sxs-lookup"><span data-stu-id="c80a3-141">**FrequencyUnit** - Unit of time for how often the backups should be made.</span></span> <span data-ttu-id="c80a3-142">選項為 [小時] 和 [天]。</span><span class="sxs-lookup"><span data-stu-id="c80a3-142">Options are Hour and Day.</span></span>
* <span data-ttu-id="c80a3-143">**RetentionPeriodInDays** - 在自動刪除自動備份前所應儲存的天數。</span><span class="sxs-lookup"><span data-stu-id="c80a3-143">**RetentionPeriodInDays** - How many days the automatic backups should be saved before being automatically deleted.</span></span>
* <span data-ttu-id="c80a3-144">**StartTime** - 選用。</span><span class="sxs-lookup"><span data-stu-id="c80a3-144">**StartTime** - Optional.</span></span> <span data-ttu-id="c80a3-145">應開始自動備份的時間。</span><span class="sxs-lookup"><span data-stu-id="c80a3-145">The time when the automatic backups should begin.</span></span> <span data-ttu-id="c80a3-146">如果這是 null，將立即開始備份。</span><span class="sxs-lookup"><span data-stu-id="c80a3-146">Backups begin immediately if this is null.</span></span> <span data-ttu-id="c80a3-147">必須是 DateTime。</span><span class="sxs-lookup"><span data-stu-id="c80a3-147">Must be a DateTime.</span></span>
* <span data-ttu-id="c80a3-148">**Databases** - 選用。</span><span class="sxs-lookup"><span data-stu-id="c80a3-148">**Databases** - Optional.</span></span> <span data-ttu-id="c80a3-149">要備份資料庫的 DatabaseBackupSettings 陣列。</span><span class="sxs-lookup"><span data-stu-id="c80a3-149">An array of DatabaseBackupSettings for the databases to backup.</span></span>
* <span data-ttu-id="c80a3-150">**KeepAtLeastOneBackup** - 選擇性切換參數。</span><span class="sxs-lookup"><span data-stu-id="c80a3-150">**KeepAtLeastOneBackup** - Optional switched parameter.</span></span> <span data-ttu-id="c80a3-151">如有一個備份應該永遠留在儲存體帳戶中 (無論有多舊)，請提供此參數值。</span><span class="sxs-lookup"><span data-stu-id="c80a3-151">Supply this if one backup should always be kept in the storage account, regardless of how old it is.</span></span>

<span data-ttu-id="c80a3-152">以下是如何使用此 Cmdlet 的範例。</span><span class="sxs-lookup"><span data-stu-id="c80a3-152">Following is an example of how to use this cmdlet.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Edit-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName -Slot $slotName `
          -StorageAccountUrl "<your SAS URL>" -FrequencyInterval 6 -FrequencyUnit Hour -Databases $dbSetting1,$dbSetting2 `
          -KeepAtLeastOneBackup -StartTime (Get-Date).AddHours(1)

<span data-ttu-id="c80a3-153">若要取得目前的備份排程，請使用 Get-AzureRmWebAppBackupConfiguration Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="c80a3-153">To get the current backup schedule, use the Get-AzureRmWebAppBackupConfiguration cmdlet.</span></span> <span data-ttu-id="c80a3-154">這很適合用於修改已設定的排程。</span><span class="sxs-lookup"><span data-stu-id="c80a3-154">This can be useful for modifying a schedule that has already been configured.</span></span>

        $configuration = Get-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName

        # Modify the configuration slightly
        $configuration.FrequencyInterval = 2
        $configuration.FrequencyUnit = "Day"

        # Apply the new configuration by piping it into the Edit-AzureRmWebAppBackupConfiguration cmdlet
        $configuration | Edit-AzureRmWebAppBackupConfiguration

## <a name="restore-a-web-app-from-a-backup"></a><span data-ttu-id="c80a3-155">從備份還原 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="c80a3-155">Restore a web app from a backup</span></span>
<span data-ttu-id="c80a3-156">若要從備份中還原 Web 應用程式，請使用 Restore-AzureRmWebAppBackup Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="c80a3-156">To restore a web app from a backup, use the Restore-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="c80a3-157">使用這個 Cmdlet 的最簡單方式就是透過管線傳入從 Get-AzureRmWebAppBackup Cmdlet 或 Get-AzureRmWebAppBackupList Cmdlet 擷取的備份物件。</span><span class="sxs-lookup"><span data-stu-id="c80a3-157">The easiest way to use this cmdlet is to pipe in a backup object retrieved from the Get-AzureRmWebAppBackup cmdlet or Get-AzureRmWebAppBackupList cmdlet.</span></span>

<span data-ttu-id="c80a3-158">一旦有備份物件，即可透過管線將該物件送至 Restore-AzureRmWebAppBackup Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="c80a3-158">Once you have a backup object, you can pipe it into the Restore-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="c80a3-159">指定 Overwrite 切換參數，以指出您打算以備份的內容覆寫 Web 應用程式的內容。</span><span class="sxs-lookup"><span data-stu-id="c80a3-159">Specify the Overwrite switch parameter to indicate that you intend to overwrite the contents of your web app with the contents of the backup.</span></span> <span data-ttu-id="c80a3-160">如果備份包含資料庫，也將會還原這些資料庫。</span><span class="sxs-lookup"><span data-stu-id="c80a3-160">If the backup contains databases, those databases are restored as well.</span></span>

        $backup | Restore-AzureRmWebAppBackup -Overwrite

<span data-ttu-id="c80a3-161">以下是如何藉由指定所有參數來使用 Restore-AzureRmWebAppBackup 的範例。</span><span class="sxs-lookup"><span data-stu-id="c80a3-161">Following is an example of how to use the Restore-AzureRmWebAppBackup by specifying all the parameters.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $blobName = "ContosoBackup.zip"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Restore-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -Slot $slotName -StorageAccountUrl "<your SAS URL>" -BlobName $blobName -Databases $dbSetting1,$dbSetting2 -Overwrite

## <a name="delete-a-backup"></a><span data-ttu-id="c80a3-162">刪除備份</span><span class="sxs-lookup"><span data-stu-id="c80a3-162">Delete a backup</span></span>
<span data-ttu-id="c80a3-163">若要刪除備份，請使用 Remove-AzureRmWebAppBackup Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="c80a3-163">To delete a backup, use the Remove-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="c80a3-164">這會從您的儲存體帳戶移除備份。</span><span class="sxs-lookup"><span data-stu-id="c80a3-164">This removes the backup from your storage account.</span></span> <span data-ttu-id="c80a3-165">指定您的應用程式名稱、其資源群組和您想要刪除之備份的識別碼。</span><span class="sxs-lookup"><span data-stu-id="c80a3-165">Specify your app name, its resource group, and the ID of the backup you want to delete.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        Remove-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupId 10102

<span data-ttu-id="c80a3-166">您也可以透過管線將備份物件送至 Remove-AzureRmWebAppBackup Cmdlet 加以刪除。</span><span class="sxs-lookup"><span data-stu-id="c80a3-166">You can also pipe a backup object into the Remove-AzureRmWebAppBackup cmdlet to delete it.</span></span>

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102
        $backup | Remove-AzureRmWebAppBackup -Overwrite
