---
title: "aaaDjango 和使用 Python Tools 2.2 for Visual Studio 在 Azure 上的 MySQL"
description: "了解如何 toouse hello Python Tools for Visual Studio toocreate Django web 應用程式的 MySQL 資料庫執行個體中儲存資料，並將其部署 tooAzure App Service Web 應用程式。"
services: app-service\web
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: c60a50b5-8b5e-4818-a442-16362273dabb
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 1597c391d20c8e8ef629b4e4d05c9eb64c83bffc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="django-and-mysql-on-azure-with-python-tools-22-for-visual-studio"></a>Azure 上使用 Python Tools 2.2 for Visual Studio 的 Django 和 MySQL
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

在此教學課程中，您將使用[Python Tools for Visual Studio](https://www.visualstudio.com/vs/python) toocreate 簡單輪詢 web 應用程式使用其中一個 hello PTVS 範例範本。 您將學習如何 toouse MySQL 服務裝載在 Azure 上、 如何 tooconfigure hello web 應用程式 toouse MySQL，以及如何 toopublish hello web 應用程式太[Azure App Service Web 應用程式](http://go.microsoft.com/fwlink/?LinkId=529714)。

> [!NOTE]
> 在本教學課程所包含的 hello 資訊也會提供下列視訊 hello:
> 
> [PTVS 2.1：Django 應用程式與 MySQL][video]
> 
> 

請參閱 hello [Python 開發人員中心]涵蓋 Azure App Service Web 應用程式與使用 Bottle PTVS 開發的多個發行項，酒瓶和 Django web 架構，來使用 Azure 資料表儲存體、 MySQL 及 SQL Database 服務。 本文著重在應用程式服務，而開發時 hello 步驟均相似[Azure 雲端服務]。

## <a name="prerequisites"></a>必要條件
* Visual Studio 2015
* [Python 2.7 32 位元]或 [Python 3.4 32 位元]
* [Python Tools 2.2 for Visual Studio]
* [Python Tools 2.2 for Visual Studio 範例 VSIX]
* [Azure SDK Tools for VS 2015]
* Django 1.9 或更新版本

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<!-- This note should not render as part of hello hello previous include. -->

> [!NOTE]
> 如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。 不需要信用卡，無需承諾。
> 
> 

## <a name="create-hello-project"></a>建立 hello 專案
在這一節中，您將使用範例範本建立 Visual Studio 專案。 您將建立虛擬環境並安裝必要的套件。 您將使用 sqlite 建立本機資料庫。 然後您將在本機執行 hello 應用程式。

1. 在 Visual Studio 中，選取 [檔案]、[新增專案]。
2. hello 專案範本從 hello [Python Tools 2.2 for Visual Studio 範例 VSIX]底下可使用**Python**，**範例**。 選取**輪詢 Django Web 專案**然後按一下 [確定] toocreate hello 專案。
   
    ![New Project Dialog](./media/web-sites-python-ptvs-django-mysql/PollsDjangoNewProject.png)
3. 系統會提示的 tooinstall 外部的封裝。 選取 [安裝到虛擬環境] 。
   
    ![外部套件對話方塊](./media/web-sites-python-ptvs-django-mysql/PollsDjangoExternalPackages.png)
4. 選取**Python 2.7**或**Python 3.4**為 hello 基底直譯器。
   
    ![新增虛擬環境對話方塊](./media/web-sites-python-ptvs-django-mysql/PollsCommonAddVirtualEnv.png)
5. 在**方案總管 中**，hello 專案節點上按一下滑鼠右鍵，然後選取**Python**，然後選取**Django 移轉**。  然後選取 [Django 建立超級使用者] 。
6. 這會開啟 Django 管理主控台，並在 hello 專案資料夾中建立 sqlite 資料庫。 請遵循 hello 提示 toocreate 使用者。
7. 確認 hello 應用程式運作方式是按`F5`。
8. 按一下**登入**hello 導覽列頂端 hello。
   
    ![Django 導覽列](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalMenu.png)
9. Hello hello 資料庫進行同步處理時所建立的使用者輸入 hello 認證。
   
    ![登入表單](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalLogin.png)
10. 按一下 [Create Sample Polls] 。
    
     ![建立範例投票](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserNoPolls.png)
11. 按一下民調並進行投票。
    
     ![在範例投票中進行投票](./media/web-sites-python-ptvs-django-mysql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-mysql-database"></a>建立 MySQL Database
Hello 資料庫，您將在 Azure 上建立 ClearDB MySQL 裝載的資料庫。

或者，您可以為自己建立在 Azure 中執行的虛擬機器，然後自行安裝和管理 MySQL。

您可以依照下列步驟，透過免費計畫建立資料庫。

1. 登入 toohello [Azure 入口網站]。
2. 在 hello hello 瀏覽窗格的頂端，按一下**新增**，然後按一下**資料 + 儲存體**，然後按一下 **MySQL 資料庫**。
3. 藉由建立新的資源群組設定 hello 新的 MySQL 資料庫並選取 hello 為它的適當位置。
4. 一旦建立 hello MySQL 資料庫時，按一下 **屬性**hello 資料庫刀鋒視窗中。
5. 使用 hello 複製按鈕 tooput hello 值**連接字串**hello 剪貼簿上。

## <a name="configure-hello-project"></a>設定 hello 專案
在本節中，您需要設定 web 應用程式 toouse hello MySQL 資料庫剛剛建立。 您也會使用如 Django 安裝其他的 Python 封裝需要的 toouse MySQL 資料庫。 然後您將在本機執行 hello web 應用程式。

1. 在 Visual Studio 中開啟**settings.py**，從 hello *ProjectName*資料夾。 暫時貼上 hello 編輯器中的 hello 連接字串。 hello 連接字串是以下列格式：
   
        Database=<NAME>;Data Source=<HOST>;User Id=<USER>;Password=<PASSWORD>
   
    變更 hello 預設資料庫**引擎**toouse MySQL，以及組 hello 值**名稱**，**使用者**，**密碼**和**主機**從 hello **CONNECTIONSTRING**。
   
        DATABASES = {
            'default': {
                'ENGINE': 'django.db.backends.mysql',
                'NAME': '<Database>',
                'USER': '<User Id>',
                'PASSWORD': '<Password>',
                'HOST': '<Data Source>',
                'PORT': '',
            }
        }
2. 在 方案總管下**Python 環境**，以滑鼠右鍵按一下 hello 虛擬環境，然後選取**安裝 Python 封裝**。
3. 安裝套件 hello`mysqlclient`使用**pip**。
   
    ![安裝套件對話方塊](./media/web-sites-python-ptvs-django-mysql/PollsDjangoMySQLInstallPackage.png)
4. 在**方案總管 中**，hello 專案節點上按一下滑鼠右鍵，然後選取**Python**，然後選取**Django 移轉**。  然後選取 [Django 建立超級使用者] 。
   
    這會建立 hello hello 您 hello 前一節中所建立的 MySQL 資料庫的資料表。 請遵循 hello 提示 toocreate hello 的這篇文章的第一個區段中建立的 hello sqlite 資料庫中沒有 toomatch hello 使用者的使用者。
5. 執行與 hello 應用程式`F5`。 利用所建立的輪詢**建立範例輪詢**和送出的投票 hello 資料會序列化 hello MySQL 資料庫中。

## <a name="publish-hello-web-app-tooazure-app-service"></a>發行 hello web 應用程式 tooAzure 應用程式服務
hello Azure.NET SDK 提供簡單的方式 toodeploy 您 web 應用程式 tooAzure 應用程式服務。

1. 在**方案總管 中**，hello 專案節點上按一下滑鼠右鍵，然後選取**發行**。
   
    ![發行 Web 對話方塊](./media/web-sites-python-ptvs-django-mysql/PollsCommonPublishWebSiteDialog.png)
2. 按一下 [Microsoft Azure App Service] 。
3. 按一下**新增**toocreate 新的 web 應用程式。
4. 填寫下列欄位的 hello，並按一下**建立**:
   
   * **Web 應用程式名稱**
   * **App Service 計劃**
   * **資源群組**
   * **區域**
   * 保留**資料庫伺服器**設定得**沒有資料庫**
5. 接受所有其他預設值並按一下 [發佈] 。
6. 網頁瀏覽器會自動開啟 toohello 已發佈的 web 應用程式。 您應該看到 hello web 應用程式工作，如預期般，使用 hello **MySQL**裝載於 Azure 的資料庫。
   
    ![Web Browser](./media/web-sites-python-ptvs-django-mysql/PollsDjangoAzureBrowser.png)
   
    恭喜！ 您已成功發行您的 MySQL 為基礎的 web 應用程式 tooAzure。

## <a name="next-steps"></a>後續步驟
請遵循這些連結 toolearn 更多關於 Python Tools for Visual Studio，如 Django 和 MySQL。

* [Python Tools for Visual Studio 說明文件]
  * [Web 專案]
  * [雲端服務專案]
  * [在 Microsoft Azure 上進行遠端偵錯]
* [Django 說明文件]
* [MySQL]

如需詳細資訊，請參閱 hello [Python 開發人員中心](/develop/python/)。

<!--Link references-->

[Python 開發人員中心]: /develop/python/
[Azure 雲端服務]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->

[Azure 入口網站]: https://portal.azure.com
[Python Tools for Visual Studio]: https://www.visualstudio.com/vs/python/
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Python Tools 2.2 for Visual Studio 範例 VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 32 位元]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 32 位元]: http://go.microsoft.com/fwlink/?LinkId=517191
[Python Tools for Visual Studio 說明文件]: http://aka.ms/ptvsdocs
[在 Microsoft Azure 上進行遠端偵錯]: http://go.microsoft.com/fwlink/?LinkId=624026
[Web 專案]: http://go.microsoft.com/fwlink/?LinkId=624027
[雲端服務專案]: http://go.microsoft.com/fwlink/?LinkId=624028
[Django 說明文件]: https://www.djangoproject.com/
[MySQL]: http://www.mysql.com/
[video]: http://youtu.be/oKCApIrS0Lo
