---
title: "aaaDjango 和使用 Python Tools 2.2 for Visual Studio 在 Azure 上的 SQL Database"
description: "了解如何 toouse hello Python Tools for Visual Studio toocreate Django web 應用程式將資料儲存在 SQL 資料庫執行個體中，並將其部署 tooAzure App Service Web 應用程式。"
services: app-service\web
tags: python
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 3a677e64-b5a9-4d43-b9c0-66246368b483
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: b5b2ef4f3292e7df85007465c5394c8660a7d231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="django-and-sql-database-on-azure-with-python-tools-22-for-visual-studio"></a>Azure 上使用 Python Tools 2.2 for Visual Studio 的 Django 和 SQL Database
在此教學課程中，我們將使用[Python Tools for Visual Studio] toocreate 簡單輪詢 web 應用程式使用其中一個 hello PTVS 範例範本。 本教學課程也提供 [教學影片](https://www.youtube.com/watch?v=ZwcoGcIeHF4)。

我們會了解如何 toouse SQL 資料庫裝載在 Azure 上、 如何 tooconfigure 會 hello web 應用程式 toouse SQL 資料庫，以及如何 toopublish hello web 應用程式太[Azure App Service Web 應用程式](http://go.microsoft.com/fwlink/?LinkId=529714)。

請參閱 hello [Python 開發人員中心]涵蓋 Azure App Service Web 應用程式與使用 Bottle PTVS 開發的多個發行項，酒瓶和 Django web 架構，來使用 Azure 資料表儲存體、 MySQL 及 SQL Database 服務。 本文著重在應用程式服務，而開發時 hello 步驟均相似[Azure 雲端服務]。

## <a name="prerequisites"></a>必要條件
* Visual Studio 2015
* [Python 2.7 (32 位元)]
* [Python Tools 2.2 for Visual Studio]
* [Python Tools 2.2 for Visual Studio 範例 VSIX]
* [Azure SDK Tools for VS 2015]
* Django 1.9 或更新版本

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> 如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。 不需要信用卡；沒有承諾。
>
>

## <a name="create-hello-project"></a>建立 hello 專案
在這一節中，我們將使用範例範本建立 Visual Studio 專案。 我們將建立虛擬環境並安裝必要的套件。 我們將使用 sqlite 建立本機資料庫。 然後我們將在本機執行 hello web 應用程式。

1. 在 Visual Studio 中，選取 [檔案]、[新增專案]。
2. hello 專案範本從 hello [Python Tools 2.2 for Visual Studio 範例 VSIX]底下可使用**Python**，**範例**。 選取**輪詢 Django Web 專案**然後按一下 [確定] toocreate hello 專案。

     ![New Project Dialog](./media/web-sites-python-ptvs-django-sql/PollsDjangoNewProject.png)
3. 系統會提示的 tooinstall 外部的封裝。 選取 [安裝到虛擬環境] 。

     ![外部套件對話方塊](./media/web-sites-python-ptvs-django-sql/PollsDjangoExternalPackages.png)
4. 選取**Python 2.7**為 hello 基底直譯器。

     ![新增虛擬環境對話方塊](./media/web-sites-python-ptvs-django-sql/PollsCommonAddVirtualEnv.png)
5. 在**方案總管 中**，hello 專案節點上按一下滑鼠右鍵，然後選取**Python**，然後選取**Django 移轉**。  然後選取 [Django 建立超級使用者] 。
6. 這會開啟 Django 管理主控台，並在 hello 專案資料夾中建立 sqlite 資料庫。 請遵循 hello 提示 toocreate 使用者。
7. 確認 hello 應用程式運作方式是按<kbd>F5</kbd>。
8. 按一下**登入**hello 導覽列頂端 hello。

     ![Web Browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalMenu.png)
9. Hello hello 資料庫進行同步處理時所建立的使用者輸入 hello 認證。

     ![Web Browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalLogin.png)
10. 按一下 [Create Sample Polls] 。

      ![Web Browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserNoPolls.png)
11. 按一下民調並進行投票。

      ![Web Browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-sql-database"></a>建立 SQL Database
Hello 資料庫，我們將建立 Azure SQL database。

您可以依照下列步驟來建立資料庫。

1. 登入 hello [Azure 入口網站]。
2. 在 hello hello 瀏覽窗格底部，按一下 **新增**。 接著，按一下 [資料 + 儲存體] > [Azure Marketplace]。
3. 設定新的 SQL Database hello 藉由建立新的資源群組和選取 hello 為它的適當位置。
4. Hello SQL 資料庫建立之後，按一下**Visual Studio 中開啟**hello 資料庫刀鋒視窗中。
5. 按一下 [設定防火牆] 。
6. 在 hello**防火牆設定**刀鋒視窗中，新增的防火牆規則**起始 IP**和**結束 IP** toohello 公用 IP 位址在開發電腦的設定。 按一下 [儲存] 。

   這可讓您在開發電腦的連線 toohello 資料庫伺服器。
7. 在 hello 資料庫刀鋒視窗中，按一下 **屬性**，然後按一下 **顯示資料庫的連接字串**。
8. 使用 hello 複製按鈕 tooput hello 值**ADO.NET** hello 剪貼簿上。

## <a name="configure-hello-project"></a>設定 hello 專案
在本節中，我們會將設定我們 web 應用程式 toouse hello SQL database 剛才所建立。 我們也會使用如 Django 安裝其他的 Python 封裝需要的 toouse SQL 資料庫。 然後我們將在本機執行 hello web 應用程式。

1. 在 Visual Studio 中開啟**settings.py**，從 hello *ProjectName*資料夾。 暫時貼上 hello 編輯器中的 hello 連接字串。 hello 連接字串是以下列格式：

       Server=<ServerName>,<ServerPort>;Database=<DatabaseName>;User ID=<UserName>;Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;

編輯的 hello 定義`DATABASES`toouse hello 上述的值。

        DATABASES = {
            'default': {
                'ENGINE': 'sql_server.pyodbc',
                'NAME': '<DatabaseName>',
                'USER': '<UserName>',
                'PASSWORD': '{your_password_here}',
                'HOST': '<ServerName>',
                'PORT': '<ServerPort>',
                'OPTIONS': {
                    'driver': 'SQL Server Native Client 11.0',
                    'MARS_Connection': 'True',
                }
            }
        }

1. 在 方案總管下**Python 環境**，以滑鼠右鍵按一下 hello 虛擬環境，然後選取**安裝 Python 封裝**。
2. 安裝套件 hello`pyodbc`使用**pip**。

     ![安裝 Python 封裝對話方塊](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackagePyodbc.png)
3. 安裝套件 hello`django-pyodbc-azure`使用**pip**。

     ![安裝 Python 封裝對話方塊](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackageDjangoPyodbcAzure.png)
4. 在**方案總管 中**，hello 專案節點上按一下滑鼠右鍵，然後選取**Python**，然後選取**Django 移轉**。  然後選取 [Django 建立超級使用者] 。

   這會建立 hello hello hello 上一節中建立的 SQL database 的資料表。 請遵循 hello 提示 toocreate 建立 hello 第一個區段中的 hello sqlite 資料庫中沒有 toomatch hello 使用者的使用者。
5. 執行與 hello 應用程式`F5`。 利用所建立的輪詢**建立範例輪詢**和送出的投票 hello 資料會序列化 hello SQL 資料庫中。

## <a name="publish-hello-web-app-tooazure-app-service"></a>發行 hello web 應用程式 tooAzure 應用程式服務
hello Azure.NET SDK 提供簡單的方式 toodeploy 您 web web 應用程式 tooAzure App Service Web 應用程式。

1. 在**方案總管 中**，hello 專案節點上按一下滑鼠右鍵，然後選取**發行**。

     ![發行 Web 對話方塊](./media/web-sites-python-ptvs-django-sql/PollsCommonPublishWebSiteDialog.png)
2. 按一下 [Microsoft Azure Web Apps] 。
3. 按一下**新增**toocreate 新的 web 應用程式。
4. 填寫下列欄位的 hello，並按一下**建立**。

   * **Web 應用程式名稱**
   * **App Service 計劃**
   * **資源群組**
   * **區域**
   * 保留**資料庫伺服器**設定得**沒有資料庫**
5. 接受所有其他預設值並按一下 [發佈] 。
6. 網頁瀏覽器會自動開啟 toohello 已發佈的 web 應用程式。 您應該看到 hello web 應用程式工作，如預期般，使用 hello **SQL**裝載於 Azure 的資料庫。

   恭喜！

     ![Web Browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoAzureBrowser.png)

## <a name="next-steps"></a>後續步驟
遵循這些連結 toolearn 更多關於 Python Tools for Visual Studio，如 Django 和 SQL Database。

* [Python Tools for Visual Studio 說明文件]
  * [Web 專案]
  * [雲端服務專案]
  * [在 Microsoft Azure 上進行遠端偵錯]
* [Django 說明文件]
* [SQL Database]

## <a name="whats-changed"></a>變更的項目
* 從網站 tooApp 服務變更如指南 toohello: [Azure 應用程式服務和其對影響現有的 Azure 服務](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[Python 開發人員中心]: /develop/python/
[Azure 雲端服務]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->
[Azure 入口網站]: https://portal.azure.com
[Python Tools for Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Python Tools 2.2 for Visual Studio 範例 VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 (32 位元)]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python Tools for Visual Studio 說明文件]: http://aka.ms/ptvsdocs
[在 Microsoft Azure 上進行遠端偵錯]: http://go.microsoft.com/fwlink/?LinkId=624026
[Web 專案]: http://go.microsoft.com/fwlink/?LinkId=624027
[雲端服務專案]: http://go.microsoft.com/fwlink/?LinkId=624028
[Django 說明文件]: https://www.djangoproject.com/
[SQL Database]: /documentation/services/sql-database/
