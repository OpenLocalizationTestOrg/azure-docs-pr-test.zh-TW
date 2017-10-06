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
# <a name="back-up-your-app-in-azure"></a>在 Azure 中備份應用程式
hello 備份和還原功能[Azure App Service](../app-service/app-service-value-prop-what-is.md)可讓您輕鬆地建立應用程式備份，以手動方式或依據排程。 您可以覆寫 hello 現有應用程式或還原 tooanother 應用程式，以還原 hello 先前狀態的應用程式 tooa 快照集。 

如需從備份還原應用程式的相關資訊，請參閱 [在 Azure 中還原應用程式](web-sites-restore.md)。

<a name="whatsbackedup"></a>

## <a name="what-gets-backed-up"></a>備份什麼項目
應用程式服務可以備份 hello 下列資訊 tooan Azure 儲存體帳戶和設定應用程式 toouse 的容器。 

* 應用程式設定
* 檔案內容
* 資料庫連接的 tooyour 應用程式

備份功能支援下列資料庫方案的 hello: 
   - [SQL Database](https://azure.microsoft.com/en-us/services/sql-database/)
   - [適用於 MySQL 的 Azure 資料庫 (預覽)](https://azure.microsoft.com/en-us/services/mysql)
   - [適用於 PostgreSQL 的 Azure 資料庫 (預覽)](https://azure.microsoft.com/en-us/services/postgres)
   - [ClearDB MySQL](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
   - [應用程式內 MySQL](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)
 

> [!NOTE]
>  每個備份都是應用程式的完整離線複本，而不是增量更新。
>  

<a name="requirements"></a>

## <a name="requirements-and-restrictions"></a>需求和限制
* hello 備份和還原功能需要 hello hello 中的應用程式服務計劃 toobe**標準**層或**Premium**層。 如需調整您的應用程式服務計劃 toouse 更高的層的詳細資訊，請參閱[在 Azure 中的應用程式向上延展](web-sites-scale.md)。  
  「進階」層所允許的每日備份數量比「標準」層多。
* 您需要 Azure 儲存體帳戶和容器在 hello hello 應用程式的 toobackup 相同訂用帳戶。 如需有關 Azure 儲存體帳戶的詳細資訊，請參閱 hello[連結](#moreaboutstorage)hello 本文結尾處。
* 備份可以是內容的 up too10 GB 的應用程式和資料庫。 如果 hello 備份大小超過此限制，您會收到錯誤。

<a name="manualbackup"></a>

## <a name="create-a-manual-backup"></a>建立手動備份
1. 在 hello [Azure 入口網站](https://portal.azure.com)、 瀏覽應用程式 tooyour 刀鋒視窗中，選取**備份**。 hello**備份**刀鋒視窗會顯示。
   
    ![Backups page][ChooseBackupsPage]
   
   > [!NOTE]
   > 如果您看到以下的 hello 訊息，按一下的 tooupgrade 您的應用程式服務計劃之前您, 可以繼續進行備份。
   > 如需詳細資訊，請參閱 [在 Azure 中調整應用程式規模](web-sites-scale.md) 。  
   > ![Choose storage account](./media/web-sites-backup/01UpgradePlan1.png)
   > 
   > 

2. 在 hello**備份**刀鋒視窗中，按一下**設定**
![按 [設定]](./media/web-sites-backup/ClickConfigure1.png)
3. 在 hello**備份設定**刀鋒視窗中，按一下 **儲存體： 未設定**tooconfigure 儲存體帳戶。
   
    ![Choose storage account][ChooseStorageAccount]
4. 選取 [儲存體帳戶] 和 [容器]，以選擇您的備份目的地。 hello 儲存體帳戶必須屬於 toohello hello 應用程式要 tooback 相同訂用帳戶。 如果想要的話，您可以在 hello 個別刀鋒視窗中建立新的儲存體帳戶或新的容器。 完成後，按一下 [選取] 。
   
    ![Choose storage account](./media/web-sites-backup/02ChooseStorageAccount1-1.png)
5. 在 hello**備份設定**仍處於開啟狀態的刀鋒視窗，您可以設定**Backup Database**，然後選取 hello 資料庫 tooinclude hello 備份 （SQL database 或 MySQL），然後按一下**確定**。  
   
    ![Choose storage account](./media/web-sites-backup/03ConfigureDatabase1.png)
   
   > [!NOTE]
   > 針對資料庫 tooappear 這份清單中，其連接字串必須存在於 hello**連接字串**區段 hello**應用程式設定**刀鋒視窗，您的應用程式。
   > 
   > 
6. 在 hello**備份設定**刀鋒視窗中，按一下 **儲存**。    
7. 在 hello**備份**刀鋒視窗中，按一下 **備份**。
   
    ![BackUpNow button][BackUpNow]
   
    Hello 備份程序中看到進度訊息。

Hello 儲存體帳戶和容器設定之後您可以隨時起始手動備份。  

<a name="automatedbackups"></a>

## <a name="configure-automated-backups"></a>設定自動備份
1. 在 hello**備份設定**刀鋒視窗中，設定**已排程備份**太**上**。 
   
    ![Choose storage account](./media/web-sites-backup/05ScheduleBackup1.png)
2. 設定備份排程選項會顯示，**排定備份**太**上**，然後視需要設定 hello 備份排程，再按一下**確定**。
   
    ![Enable automated backups][SetAutomatedBackupOn]

<a name="partialbackups"></a>

## <a name="configure-partial-backups"></a>設定部分備份
有時候您不想 toobackup 的所有項目在您的應用程式。 以下是一些範例：

* 您為包含永不變更的靜態內容 (例如舊部落格文章或影像) 的應用程式 [設定每週備份](web-sites-backup.md#configure-automated-backups) 。
* 您的應用程式具有超過 10 GB 的內容 （亦即 hello 最大數量，您可以備份一次）。
* 您不想 toobackup hello 記錄檔。

部分備份會讓您選擇正確的檔案，您想 toobackup。

### <a name="exclude-files-from-your-backup"></a>從備份中排除檔案
假設您有應用程式，其中包含記錄檔和備份一次，而且不會成為 toochange 的靜態影像。 在這類情況下，您可以將這些資料夾和檔案排除，而不儲存在您未來的備份中。 tooexclude 檔案和資料夾從您的備份，建立`_backup.filter`檔案在 hello`D:\home\site\wwwroot`應用程式資料夾。 指定檔案和資料夾想 tooexclude 此檔案中的 hello 的清單。 

您的檔案是 toouse Kudu 輕鬆 tooaccess。 按一下**進階工具]-> [移至**設定您的 web 應用程式 tooaccess Kudu。

![使用入口網站時的 Kuku][kudu-portal]

識別您想 tooexclude，從您的備份 hello 資料夾。  例如，您會想 toofilter 出 hello 反白顯示的資料夾和檔案。

![Images 資料夾][ImagesFolder]

建立一個叫做檔案`_backup.filter`並將上述 hello 清單放入 hello 檔案，但移除`D:\home`。 一行列出一個目錄或檔案。 因此 hello hello 檔案內容應該：
 ```bash
    \site\wwwroot\Images\brand.png
    \site\wwwroot\Images\2014
    \site\wwwroot\Images\2013
```

上傳`_backup.filter`檔案 toohello`D:\home\site\wwwroot\`目錄的站台使用[ftp](web-sites-deploy.md#ftp)或任何其他方法。 如果您希望，您可以建立 hello 檔案直接使用 Kudu`DebugConsole`並插入那里 hello 內容。

執行的備份 hello 相同方式，通常會進行，[手動](#create-a-manual-backup)或[自動](#configure-automated-backups)。 現在，任何的檔案和資料夾中所指定`_backup.filter`hello 未來的備份排程或手動起始已排除。 

> [!NOTE]
> 還原部分備份的站台 hello 一樣[還原定期備份](web-sites-restore.md)。 hello 還原程序沒有 hello 正確的事。
> 
> 還原完整備份時，hello 站台上的所有內容會都取代任何處於 hello 備份。 如果檔案在 hello 站台，但不是在 hello 備份它被刪除。 但是，還原部分備份時，位於其中一個 hello 列入黑名單中而目錄或任何列入封鎖清單的檔案中的任何內容保持原狀。
> 


<a name="aboutbackups"></a>

## <a name="how-backups-are-stored"></a>備份的儲存方式
Hello 備份您的應用程式進行一個或多個備份之後，會顯示 hello**容器**刀鋒視窗中的儲存體帳戶和您的應用程式。 Hello 儲存體帳戶，在每個備份包含`.zip`包含 hello 備份資料檔案和`.xml`檔案，其中包含資訊清單的 hello`.zip`檔案內容。 您可以解壓縮並瀏覽這些檔案，如果您想要 tooaccess 備份而不需實際執行應用程式還原。

hello hello 應用程式的資料庫備份會儲存在 hello the.zip 檔案根目錄中。 若是 SQL 資料庫，這會是 BACPAC 檔案 (無副檔名)，而且可以匯入。 toocreate SQL database 根據 hello BACPAC 匯出，請參閱[匯入新的使用者資料庫的 BACPAC 檔案 tooCreate](http://technet.microsoft.com/library/hh710052.aspx)。

> [!WARNING]
> 改變任何 hello 檔案中您**websitebackups**容器可能會導致備份 hello toobecome 無效，因此非還原。
> 
> 

<a name="nextsteps"></a>

## <a name="next-steps"></a>後續步驟
如需從備份還原應用程式的相關資訊，請參閱 [在 Azure 中還原應用程式](web-sites-restore.md)。 您也可以備份與還原 App Service 使用 REST API 的應用程式 (請參閱[使用 REST toobackup 與還原 App Service 應用程式](websites-csm-backup.md))。


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

