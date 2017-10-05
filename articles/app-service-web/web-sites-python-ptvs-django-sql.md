---
title: "Azure 上使用 Python Tools 2.2 for Visual Studio 的 Django 和 SQL Database"
description: "了解如何使用 Python Tools for Visual Studio 建立 Django Web 應用程式，藉此將資料儲存在 SQL Database 執行個體中，並部署到 Azure App Service Web Apps。"
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
ms.openlocfilehash: 65b59dee2b7bddca77d31c692dab713c68d67e24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="django-and-sql-database-on-azure-with-python-tools-22-for-visual-studio"></a>Azure 上使用 Python Tools 2.2 for Visual Studio 的 Django 和 SQL Database
在此教學課程中，我們將使用 [Python Tools for Visual Studio] ，並使用其中一個 PTVS 範例範本來建立簡單的民調 Web 應用程式。 本教學課程也提供 [教學影片](https://www.youtube.com/watch?v=ZwcoGcIeHF4)。

我們將學習如何使用 Azure 上裝載的 SQL Database、如何設定 Web 應用程式來使用 SQL Database，以及如何將 Web 應用程式發佈至 [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714)。

如需更多相關文章 (說明透過使用 Bottle、Flask 和 Django 架構的 PTVS、透過 Azure 資料表儲存體、MySQL 和 SQL Database 服務進行 Azure App Service Web Apps 開發)，請參閱 [Python 開發人員中心] 。 雖然本文著重於 App Service，但其開發步驟類似於開發 [Azure 雲端服務]。

## <a name="prerequisites"></a>必要條件
* Visual Studio 2015
* [Python 2.7 (32 位元)]
* [Python Tools 2.2 for Visual Studio]
* [Python Tools 2.2 for Visual Studio 範例 VSIX]
* [Azure SDK Tools for VS 2015]
* Django 1.9 或更新版本

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> 如果您想在註冊 Azure 帳戶前開始使用 Azure App Service，請移至 [試用 App Service](https://azure.microsoft.com/try/app-service/)，即可在 App Service 中立即建立短期入門 Web 應用程式。 不需要信用卡；無需承諾。
>
>

## <a name="create-the-project"></a>建立專案
在這一節中，我們將使用範例範本建立 Visual Studio 專案。 我們將建立虛擬環境並安裝必要的套件。 我們將使用 sqlite 建立本機資料庫。 接著，在本機執行 Web 應用程式。

1. 在 Visual Studio 中，選取 [檔案]、[新增專案]。
2. 在 [Python]、[範例] 之下可取得 [Python Tools 2.2 for Visual Studio 範例 VSIX] 中的專案範本。 選取 [Polls Django Web Project]  ，然後按一下 [確定] 以建立專案。

     ![New Project Dialog](./media/web-sites-python-ptvs-django-sql/PollsDjangoNewProject.png)
3. 系統會提示您安裝外部套件。 選取 [安裝到虛擬環境] 。

     ![外部套件對話方塊](./media/web-sites-python-ptvs-django-sql/PollsDjangoExternalPackages.png)
4. 選取 **Python 2.7** 作為基礎解譯器。

     ![新增虛擬環境對話方塊](./media/web-sites-python-ptvs-django-sql/PollsCommonAddVirtualEnv.png)
5. 在 [方案總管] 中，以滑鼠右鍵按一下專案節點並選取 [Python]，然後選取 [Django 移轉]。  然後選取 [Django 建立超級使用者] 。
6. 這樣會開啟 Django 管理主控台，並在專案資料夾中建立 sqlite 資料庫。 依照提示建立使用者。
7. 按 <kbd>F5</kbd> 確認應用程式可運作。
8. 按一下頂端導覽列中的 [登入]  。

     ![Web Browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalMenu.png)
9. 為您在同步處理資料庫時建立的使用者輸入認證。

     ![Web Browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalLogin.png)
10. 按一下 [Create Sample Polls] 。

      ![Web Browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserNoPolls.png)
11. 按一下民調並進行投票。

      ![Web Browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-sql-database"></a>建立 SQL Database
對於資料庫，我們將建立 Azure SQL 資料庫。

您可以依照下列步驟來建立資料庫。

1. 登入 [Azure 入口網站]。
2. 在導覽窗格的底端，按一下 [新增]。 接著，按一下 [資料 + 儲存體] > [Azure Marketplace]。
3. 設定新的 SQL Database，做法是建立新的資源群組，然後為其選取一個適當的位置。
4. 建立 SQL Database 後，請按一下資料庫刀鋒視窗中的 [在 Visual Studio 中開啟]  。
5. 按一下 [設定防火牆] 。
6. 在 [防火牆設定] 刀鋒視窗中新增下列防火牆規則：**START IP** 與 **END IP** 設為您開發電腦上的公用 IP 位址。 按一下 [儲存] 。

   這樣可讓您從開發電腦連線至資料庫伺服器。
7. 在資料庫刀鋒視窗中，按一下 [屬性]，然後按一下 [顯示資料庫連接字串]。
8. 使用 [複製] 按鈕將 **ADO.NET** 的值複製到剪貼簿上。

## <a name="configure-the-project"></a>設定專案
在這一節中，我們會將 Web 應用程式設定為使用我們剛才建立的 SQL Database。 我們也將安裝搭配使用 SQL 資料庫與 Django 所需的其他 Python 套件。 接著，在本機執行 Web 應用程式。

1. 在 Visual Studio 中，從 **ProjectName**資料夾開啟 *settings.py* 。 暫時在編輯器中貼上連接字串。 連接字串的格式如下：

       Server=<ServerName>,<ServerPort>;Database=<DatabaseName>;User ID=<UserName>;Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;

使用上述值編輯 `DATABASES` 的定義。

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

1. 在 [方案總管] 的 [Python 環境] 之下，在虛擬環境上按一下滑鼠右鍵並選取 [安裝 Python 封裝]。
2. 使用 **pip** 安裝 `pyodbc` 封裝。

     ![安裝 Python 封裝對話方塊](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackagePyodbc.png)
3. 使用 **pip** 安裝 `django-pyodbc-azure` 封裝。

     ![安裝 Python 封裝對話方塊](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackageDjangoPyodbcAzure.png)
4. 在 [方案總管] 中，以滑鼠右鍵按一下專案節點並選取 [Python]，然後選取 [Django 移轉]。  然後選取 [Django 建立超級使用者] 。

   此舉會為我們在上一節中建立的 SQL Database 建立資料表。 依照提示建立使用者，該使用者不需符合在第一節中建立之 sqlite 資料庫中的使用者。
5. 使用 `F5`執行應用程式。 使用 [Create Sample Polls]  建立的民調以及投票所提交的資料將會在 SQL Database 中序列化。

## <a name="publish-the-web-app-to-azure-app-service"></a>將 Web 應用程式發佈至 Azure App Service
Azure .NET SDK 提供簡單的方法將 Web 應用程式部署至 Azure App Service Web Apps。

1. 在 [方案總管] 中，以滑鼠右鍵按一下專案節點並選取 [發佈]。

     ![發行 Web 對話方塊](./media/web-sites-python-ptvs-django-sql/PollsCommonPublishWebSiteDialog.png)
2. 按一下 [Microsoft Azure Web Apps] 。
3. 按一下 [新增]  以建立新的 Web 應用程式。
4. 填寫下列欄位，然後按一下 [建立] 。

   * **Web 應用程式名稱**
   * **App Service 計劃**
   * **資源群組**
   * **區域**
   * 讓「資料庫伺服器」維持設定為「沒有資料庫」
5. 接受所有其他預設值並按一下 [發佈] 。
6. 您的 Web 瀏覽器將會自動開啟到已發佈的 Web 應用程式。 您應該會看到 Web 應用程式如預期般運作，並使用 Azure 上裝載的 **SQL** 資料庫。

   恭喜！

     ![Web Browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoAzureBrowser.png)

## <a name="next-steps"></a>後續步驟
請遵循下列連結以深入了解 Python Tools for Visual Studio、Django 和 SQL Database。

* [Python Tools for Visual Studio 說明文件]
  * [Web 專案]
  * [雲端服務專案]
  * [在 Microsoft Azure 上進行遠端偵錯]
* [Django 說明文件]
* [SQL Database]

## <a name="whats-changed"></a>變更的項目
* 如需從網站變更為 App Service 的指南，請參閱： [Azure App Service 及其對現有 Azure 服務的影響](http://go.microsoft.com/fwlink/?LinkId=529714)

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
