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
# <a name="use-powershell-tooback-up-and-restore-app-service-apps"></a>使用 PowerShell tooback] 和 [還原 App Service 應用程式
> [!div class="op_single_selector"]
> * [PowerShell](app-service-powershell-backup.md)
> * [REST API](../app-service-web/websites-csm-backup.md)
> 
> 

深入了解如何 toouse Azure PowerShell tooback 及還原[App Service 應用程式](https://azure.microsoft.com/services/app-service/web/)。 如需有關 Web 應用程式備份的詳細資訊，包括需求和限制，請參閱 [在 Azure App Service 中備份 Web 應用程式](../app-service-web/web-sites-backup.md)。

## <a name="prerequisites"></a>必要條件
toouse PowerShell toomanage 您應用程式的備份，您需要遵循的 hello:

* **SAS URL** ，可讓讀取和寫入權限 tooan Azure 儲存體容器。 請參閱[了解 hello SAS 模型](../storage/common/storage-dotnet-shared-access-signature-part-1.md)取得 SAS Url 的說明。 如需使用 PowerShell 管理 Azure 儲存體的範例，請參閱 [搭配使用 Azure PowerShell 與 Azure 儲存體](../storage/common/storage-powershell-guide-full.md) 。
* **資料庫連接字串**如果您想將資料庫 tooback 您 web 應用程式。

### <a name="how-toogenerate-a-sas-url-toouse-with-hello-web-app-backup-cmdlets"></a>Toogenerate SAS URL toouse hello web 應用程式與如何備份 cmdlet
您可以使用 PowerShell 產生 SAS URL。 以下是如何 toogenerate 可以搭配 hello cmdlet 的其中一個本文所討論的範例。

        $storageAccountName = "<your storage account's name>"
        $storageAccountRg = "<your storage account's resource group>"

        # This returns an array of keys for your storage account. Be sure tooselect hello appropriate key. Here we select hello first key as a default.
        $storageAccountKey = Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccountRg -Name $storageAccountName
        $context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey[0].Value

        $blobContainerName = "<name of blob container for app backups>"
        $sasUrl = New-AzureStorageContainerSASToken -Name $blobContainerName -Permission rwdl -Context $context -ExpiryTime (Get-Date).AddMonths(1) -FullUri

## <a name="install-azure-powershell-132-or-greater"></a>安裝 Azure PowerShell 1.3.2 或更新版本
如需安裝和使用 Azure PowerShell 的指示，請參閱 [搭配使用 Azure PowerShell 與 Azure Resource Manager](/powershell/azure/overview) 。

## <a name="create-a-backup"></a>建立備份
使用 hello 新增 AzureRmWebAppBackup cmdlet toocreate web 應用程式的備份。

        $sasUrl = "<your SAS URL>"
        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl

這會以自動產生的名稱建立備份。 如果您想要 tooprovide 您備份的名稱，使用 hello BackupName 選擇性參數。

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl -BackupName MyBackup

tooinclude hello 備份中的資料庫第一次建立資料庫的備份設定，使用 hello 新增 AzureRmWebAppDatabaseBackupSetting cmdlet，然後提供該設定在 hello hello 新增 AzureRmWebAppBackup cmdlet 資料庫參數。 hello 資料庫參數接受允許您 tooback 多個資料庫的資料庫設定的陣列。

        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbBackup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupName MyBackup -StorageAccountUrl $sasUrl -Databases $dbSetting1,$dbSetting2

## <a name="get-backups"></a>取得備份
hello Get AzureRmWebAppBackupList cmdlet 會傳回陣列的 web 應用程式中的所有備份。 您必須提供 hello hello web 應用程式名稱和其資源群組。

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $backups = Get-AzureRmWebAppBackupList -Name $appName -ResourceGroupName $resourceGroupName

tooget 特定備份，使用 hello Get AzureRmWebAppBackup 指令程式。

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102

您也可以將 web 應用程式物件傳送至任一個 hello 備份管理 cmdlet，為了方便起見。

        $app = Get-AzureRmWebApp -Name ContosoApp -ResourceGroupName Default-Web-WestUS
        $backupList = $app | Get-AzureRmWebAppBackupList
        $backup = $app | Get-AzureRmWebAppBackup -BackupId 10102

## <a name="schedule-automatic-backups"></a>排程自動備份
您可以依指定的間隔自動排程備份 toohappen。 tooconfigure 備份排程，使用 hello 編輯 AzureRmWebAppBackupConfiguration 指令程式。 此 Cmdlet 會採用數個參數︰

* **名稱**-hello hello web 應用程式的名稱。
* **ResourceGroupName** -hello hello 資源群組包含 hello web 應用程式的名稱。
* **Slot** - 選用。 hello hello web 應用程式位置名稱。
* **StorageAccountUrl** -hello Azure 儲存體容器使用 toostore hello 備份 hello SAS URL。
* **FrequencyInterval** -頻率 hello 備份應該設定成數值。 必須是正整數。
* **FrequencyUnit** -的頻率 hello 應該備份來進行時間單位。 選項為 [小時] 和 [天]。
* **RetentionPeriodInDays** -hello 自動備份應該儲存之前不會自動刪除的天數。
* **StartTime** - 選用。 hello hello 自動備份應開始的時間。 如果這是 null，將立即開始備份。 必須是 DateTime。
* **Databases** - 選用。 Hello 資料庫 toobackup DatabaseBackupSettings 的陣列。
* **KeepAtLeastOneBackup** - 選擇性切換參數。 這如果一個備份應該永遠保持 hello 儲存體帳戶，無論它是舊的供應器。

以下是如何的範例 toouse 這個指令程式。

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Edit-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName -Slot $slotName `
          -StorageAccountUrl "<your SAS URL>" -FrequencyInterval 6 -FrequencyUnit Hour -Databases $dbSetting1,$dbSetting2 `
          -KeepAtLeastOneBackup -StartTime (Get-Date).AddHours(1)

tooget hello 目前的備份排程，使用 hello Get AzureRmWebAppBackupConfiguration 指令程式。 這很適合用於修改已設定的排程。

        $configuration = Get-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName

        # Modify hello configuration slightly
        $configuration.FrequencyInterval = 2
        $configuration.FrequencyUnit = "Day"

        # Apply hello new configuration by piping it into hello Edit-AzureRmWebAppBackupConfiguration cmdlet
        $configuration | Edit-AzureRmWebAppBackupConfiguration

## <a name="restore-a-web-app-from-a-backup"></a>從備份還原 Web 應用程式
toorestore web 應用程式，從備份使用 hello 還原 AzureRmWebAppBackup 指令程式。 最簡單方式 toouse hello 這個指令程式是 toopipe 備份物件擷取自 hello Get AzureRmWebAppBackup cmdlet 或 Get AzureRmWebAppBackupList cmdlet 中。

備份的物件之後，您可以將其傳送到 hello 還原 AzureRmWebAppBackup cmdlet。 指定您想 toooverwrite hello 的內容，您的 web 應用程式的 hello 備份的 hello 內容 hello 覆寫參數參數 tooindicate。 如果 hello 備份包含資料庫，這些資料庫也會一併還原。

        $backup | Restore-AzureRmWebAppBackup -Overwrite

以下是範例 toouse hello 還原 AzureRmWebAppBackup 藉由指定所有 hello 參數的方式。

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $blobName = "ContosoBackup.zip"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Restore-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -Slot $slotName -StorageAccountUrl "<your SAS URL>" -BlobName $blobName -Databases $dbSetting1,$dbSetting2 -Overwrite

## <a name="delete-a-backup"></a>刪除備份
toodelete 備份時，使用 hello 移除 AzureRmWebAppBackup 指令程式。 這會移除 hello 備份從儲存體帳戶。 指定您的應用程式名稱，其資源群組，然後 hello 識別碼 hello 備份您想要 toodelete。

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        Remove-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupId 10102

您也可以將備份的物件傳送至 hello 移除 AzureRmWebAppBackup cmdlet toodelete 它。

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102
        $backup | Remove-AzureRmWebAppBackup -Overwrite
