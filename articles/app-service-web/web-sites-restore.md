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
# <a name="restore-an-app-in-azure"></a>在 Azure 中還原應用程式
本文章將示範如何中的應用程式的 toorestore [Azure App Service](../app-service/app-service-value-prop-what-is.md)您先前已備份的 (請參閱[備份您的應用程式在 Azure 中](web-sites-backup.md))。 您可以還原成連結的資料庫隨 tooa 先前的狀態，您的應用程式，或建立新的應用程式，以其中一個原始應用程式的備份。 Azure App Service 支援下列用於備份和還原資料庫的 hello:
- [SQL Database](https://azure.microsoft.com/en-us/services/sql-database/)
- [適用於 MySQL 的 Azure 資料庫 (預覽)](https://azure.microsoft.com/en-us/services/mysql)
- [適用於 PostgreSQL 的 Azure 資料庫 (預覽)](https://azure.microsoft.com/en-us/services/postgres)
- [ClearDB MySQL](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
- [應用程式內 MySQL](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)

從備份還原為執行的可用 tooapps**標準**和**Premium**層。 如需有關相應增加應用程式的詳細資訊，請參閱 [在 Azure 中調整應用程式規模](web-sites-scale.md)。 **Premium**層可讓更多超過執行每日備份 toobe**標準**層。

<a name="PreviousBackup"></a>

## <a name="restore-an-app-from-an-existing-backup"></a>從現有備份還原應用程式
1. 在 hello**設定**刀鋒視窗中的 hello Azure 入口網站中的應用程式按一下**備份**toodisplay hello**備份**刀鋒視窗。 然後按一下 [還原]。
   
    ![選擇立即還原][ChooseRestoreNow]
2. 在 hello**還原**刀鋒視窗中，第一個選取的 hello 備份來源。
   
    ![](./media/web-sites-restore/021ChooseSource1.png)
   
    hello**應用程式備份**選項會顯示所有 hello hello 目前應用程式的現有備份，及您可以輕鬆地選取其中一個。
    hello**儲存體**選項可讓您選取從任何現有的 Azure 儲存體帳戶和訂用帳戶中的容器的任何備份 ZIP 檔案。
    如果您想要 toorestore 另一個應用程式的備份，使用 hello**儲存體**選項。
3. 然後，指定 hello 應用程式還原中的 hello 目的地**還原目的地**。
   
    ![](./media/web-sites-restore/022ChooseDestination1.png)
   
   > [!WARNING]
   > 如果您選擇 [覆寫]，則目前應用程式中的所有現有資料都將被清除並覆寫。 在您按一下之前**確定**，請確定它是只想 toodo。
   > 
   > 
   
    您可以選取**現有應用程式**toorestore hello 應用程式備份 tooanother 應用程式在 hello 相同資源群組。 使用此選項之前，您應該已經建立另一個應用程式與鏡像資料庫組態 toohello hello 應用程式備份中所定義的其中一個資源群組中。 您也可以建立**新增**應用程式 toorestore 您的內容。

4. 按一下 [確定] 。

<a name="StorageAccount"></a>

## <a name="download-or-delete-a-backup-from-a-storage-account"></a>從儲存體帳戶下載或刪除備份
1. 從主要 hello**瀏覽**刀鋒視窗中的 hello Azure 入口網站，選取**儲存體帳戶**。 隨即會顯示您現有的儲存體帳戶清單。
2. 選取包含您想要 toodownload 或 delete.hello hello 儲存體帳戶的刀鋒視窗會顯示 hello 備份 hello 儲存體帳戶。
3. 在 hello 儲存體帳戶 刀鋒視窗，選取您想要的 hello 容器
   
    ![檢視容器][ViewContainers]
4. 選取您想要 toodownload 或刪除的備份檔案。
   
    ![ViewContainers](./media/web-sites-restore/03ViewFiles.png)
5. 按一下**下載**或**刪除**根據您想要 toodo。  

<a name="OperationLogs"></a>

## <a name="monitor-a-restore-operation"></a>監視還原作業
toosee 詳細 hello 成功或失敗的 hello 應用程式還原作業，瀏覽 toohello**活動記錄檔**hello Azure 入口網站中的刀鋒視窗。  
 

向下捲動 toofind hello 需要還原作業，並按一下 tooselect 它。

hello 詳細資料 刀鋒視窗會顯示 hello 可用相關 toohello 還原作業。

## <a name="next-steps"></a>後續步驟
您可以備份與還原 App Service 使用 REST API 的應用程式 (請參閱[使用 REST tooback 及還原 App Service 應用程式](websites-csm-backup.md))。


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
