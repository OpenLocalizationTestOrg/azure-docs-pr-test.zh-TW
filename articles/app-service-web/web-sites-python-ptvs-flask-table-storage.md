---
title: "aaaFlask 和使用 Python Tools 2.2 for Visual Studio 在 Azure 上的 Azure 資料表儲存體"
description: "了解如何 toouse hello Python Tools for Visual Studio toocreate 酒瓶 web 應用程式在 Azure 資料表儲存體中儲存資料，並將其部署 tooAzure App Service Web 應用程式。"
services: app-service\web
tags: python
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: d8e70a29-aca1-4010-95f5-cfe769e3be06
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 1a09d4cc78078a00492ba4fe7e2075df96fb0380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="flask-and-azure-table-storage-on-azure-with-python-tools-22-for-visual-studio"></a>Azure 上使用 Python Tools 2.2 for Visual Studio 的 Flask 和 Azure 資料表儲存體
在此教學課程中，我們將使用[Python Tools for Visual Studio] toocreate 簡單輪詢 web 應用程式使用其中一個 hello PTVS 範例範本。 本教學課程也提供 [教學影片](https://www.youtube.com/watch?v=qUtZWtPwbTk)。

hello 輪詢 web 應用程式定義它的儲存機制的抽象概念，因此您可以輕鬆切換不同類型的儲存機制 (記憶體中，Azure 資料表儲存體，MongoDB) 之間。

我們也將學習如何 toocreate Azure 儲存體帳戶，tooconfigure hello web 應用程式 toouse Azure 資料表儲存體，以及如何 toopublish hello web 應用程式太[Azure App Service Web 應用程式](http://go.microsoft.com/fwlink/?LinkId=529714)。

請參閱 hello [Python 開發人員中心]涵蓋 Azure App Service Web 應用程式與使用 Bottle PTVS 開發的多個發行項，酒瓶和 Django web 架構，來使用 MongoDB、 Azure 資料表儲存體、 MySQL 及 SQL Database 的服務。 本文著重在應用程式服務，而開發時 hello 步驟均相似[Azure 雲端服務]。

## <a name="prerequisites"></a>必要條件
* Visual Studio 2015
* [Python Tools 2.2 for Visual Studio]
* [Python Tools 2.2 for Visual Studio 範例 VSIX]
* [Azure SDK Tools for VS 2015]
* [Python 2.7 32 位元]或 [Python 3.4 32 位元]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> 如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。 不需要信用卡；沒有承諾。
> 
> 

## <a name="create-hello-project"></a>建立 hello 專案
在這一節中，我們將使用範例範本建立 Visual Studio 專案。 我們將建立虛擬環境並安裝必要的套件。 然後我們將執行 hello 應用程式在本機使用 hello 預設記憶體中儲存機制。

1. 在 Visual Studio 中，選取 [檔案]、[新增專案]。
2. hello 專案範本從 hello [Python Tools 2.2 for Visual Studio 範例 VSIX]底下可使用**Python**，**範例**。 選取**輪詢酒瓶 Web 專案**然後按一下 [確定] toocreate hello 專案。
   
     ![New Project Dialog](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskNewProject.png)
3. 系統會提示的 tooinstall 外部的封裝。 選取 [安裝到虛擬環境] 。
   
     ![外部套件對話方塊](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskExternalPackages.png)
4. 選取**Python 2.7**或**Python 3.4**為 hello 基底直譯器。
   
     ![新增虛擬環境對話方塊](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAddVirtualEnv.png)
5. 確認 hello 應用程式運作方式是按`F5`。 根據預設，hello 應用程式會使用記憶體中儲存機制並不需要任何設定。 Hello web 伺服器停止時，所有資料都都會遺失。
6. 按一下 [Create Sample Polls] ，然後按一下某項民調並投票。
   
     ![Web Browser](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskInMemoryBrowser.png)

## <a name="create-an-azure-storage-account"></a>建立 Azure 儲存體帳戶
toouse 儲存作業，您需要 Azure 儲存體帳戶。 您可以依照下列步驟來建立儲存體帳戶。

1. 登入 hello [Azure 入口網站](https://portal.azure.com/)。
2. 按一下 hello**新增**hello 上方的圖示左邊 hello 入口網站，請按一下 **資料 + 儲存體** > **儲存體帳戶**。 按一下**建立**，然後提供 hello 儲存體帳戶的唯一名稱，並建立新[資源群組](../azure-resource-manager/resource-group-overview.md)它。
   
      ![Quick Create](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAzureStorageCreate.png)
   
    Hello 儲存體帳戶建立後，hello**通知** 按鈕會閃爍綠色**成功**且 hello 儲存體帳戶的刀鋒視窗已開啟 tooshow 其所屬 toohello 新資源群組建立。
3. 按一下 hello**便捷鍵**hello 儲存體帳戶的刀鋒視窗的一部分。 請注意 hello 帳戶名稱和 hello key1。
   
      ![之間的信任](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAzureStorageKeys.png)
   
    我們需要此資訊 tooconfigure hello 下一節中的專案。

## <a name="configure-hello-project"></a>設定 hello 專案
在本節中，我們稍後會設定剛才所建立我們應用程式 toouse hello 儲存體帳戶。 我們會看到如何從 tooobtain 連線設定 hello Azure 入口網站。 然後我們將在本機執行 hello 應用程式。

1. 在 Visual Studio 的 [方案總管] 中，在您的專案節點上按一下滑鼠右鍵，然後選取 [屬性] 。 按一下 hello**偵錯** 索引標籤。
   
     ![專案偵錯設定](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureTableStorageProjectDebugSettings.png)
2. 設定環境變數中的 hello 應用程式所需的 hello 值**偵錯伺服器指令**，**環境**。
   
       REPOSITORY_NAME=azuretablestorage
       STORAGE_NAME=<storage account name>
       STORAGE_KEY=<primary access key>
   
   這會將 hello 環境變數時您**開始偵錯**。 如果您想要 hello 變數 toobe 設定時您**啟動但不偵錯**，集 hello 相同值的下**執行伺服器命令**以及。
   
   或者，您可以定義使用 hello Windows 控制台中的環境變數。 如果您想要將認證儲存在原始程式碼中 tooavoid / 專案檔，這會是較好的選擇。 請注意，您將需要 Visual Studio toorestart hello 新環境值 toobe 可用 toohello 應用程式。
3. 實作 hello Azure 資料表儲存體儲存機制的 hello 程式碼位於**models/azuretablestorage.py**。 請參閱 hello[文件]如需有關如何 toouse 來自 Python 的表格服務。
4. 執行與 hello 應用程式`F5`。 利用所建立的輪詢**建立範例輪詢**和送出的投票 hello 資料會序列化 Azure 資料表儲存體中。
   
   > [!NOTE]
   > hello Python 2.7 虛擬環境，可能會在 Visual Studio 中導致例外狀況中斷。  按`F5`toocontinue 載入 hello web 專案。
   > 
   > 
5. 瀏覽 toohello**有關**hello 應用程式的頁面 tooverify 使用 hello **Azure 資料表儲存體**儲存機制。
   
     ![Web Browser](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureTableStorageAbout.png)

## <a name="explore-hello-azure-table-storage"></a>瀏覽 hello Azure 資料表儲存體
它是簡單 tooview 並編輯使用 Cloud Explorer Visual Studio 中的儲存體資料表。 本節中，我們會使用伺服器總管 tooview hello 資料表內容的 hello 輪詢應用程式。

> [!NOTE]
> 這需要安裝，Microsoft Azure Tools toobe 所提供的 hello 一部分[Azure SDK for.NET]。
> 
> 

1. 開啟 [雲端總管] 。 依序展開 [儲存體帳戶]、您的儲存體帳戶和 [資料表]。
   
     ![雲端總管](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorer.png)
2. 按兩下 hello**輪詢**或**選擇**資料表 tooview hello hello 資料表文件視窗中，以及加入/移除/編輯實體內容。
   
     ![資料表查詢結果](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorerTable.png)

## <a name="publish-hello-web-app-tooazure-app-service"></a>發行 hello web 應用程式 tooAzure 應用程式服務
hello Azure.NET SDK 提供簡單的方式 toodeploy 您 web 應用程式 tooAzure 應用程式服務。

1. 在**方案總管 中**，hello 專案節點上按一下滑鼠右鍵，然後選取**發行**。
   
     ![發行 Web 對話方塊](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonPublishWebSiteDialog.png)
2. 按一下 [Microsoft Azure Web Apps] 。
3. 按一下**新增**toocreate 新的 web 應用程式。
4. 填寫下列欄位的 hello，並按一下**建立**。
   
   * **Web 應用程式名稱**
   * **App Service 計劃**
   * **資源群組**
   * **區域**
   * 保留**資料庫伺服器**設定得**沒有資料庫**
5. 接受所有其他預設值並按一下 [發佈] 。
6. 網頁瀏覽器會自動開啟 toohello 已發佈的 web 應用程式。 如果您瀏覽 toohello 有關頁面，您會看到它會使用 hello **In-memory**儲存機制、 不 hello **Azure 資料表儲存體**儲存機制。
   
   這是因為 hello 環境變數上未設定 hello Web 應用程式的執行個體在 Azure 應用程式服務中，因此它會使用 hello 中指定的預設值**settings.py**。

## <a name="configure-hello-web-apps-instance"></a>設定 hello Web 應用程式執行個體
在本節中，我們會將設定環境變數 hello Web 應用程式執行個體。

1. 在[Azure 入口網站](https://portal.azure.com)，開啟 hello web 應用程式的刀鋒視窗中，依序按一下**瀏覽** > **應用程式服務**> web 應用程式名稱。
2. 在您的 Web 應用程式刀鋒視窗中，按一下 [所有設定] > [應用程式設定]。
3. 捲動 toohello**應用程式設定**區段，並設定 hello 值**儲存機制\_名稱**，**儲存體\_名稱**和**儲存體\_金鑰**hello 中所述**設定 hello 專案**上一節。
   
     ![應用程式設定](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonWebSiteConfigureSettingsTableStorage.png)
4. 按一下 [儲存] 。 收到 hello 變更已套用的 hello 通知之後，請按一下**瀏覽**hello Web 應用程式主要刀鋒視窗。
5. 您應該看到 hello web 應用程式工作，如預期般，使用 hello **Azure 資料表儲存體**儲存機制。
   
   恭喜！
   
     ![Web Browser](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureBrowser.png)

## <a name="next-steps"></a>後續步驟
遵循這些連結 toolearn 更多關於 Python Tools for Visual Studio、 酒瓶和 Azure 資料表儲存體。

* [Python Tools for Visual Studio 說明文件]
  * [Web 專案]
  * [雲端服務專案]
  * [在 Microsoft Azure 上進行遠端偵錯]
* [Flask 說明文件 (英文)]
* [Azure 儲存體]
* [Azure SDK for Python]
* [如何 tooUse hello 來自 Python 的資料表儲存體服務]

## <a name="whats-changed"></a>變更的項目
* 從網站 tooApp 服務變更如指南 toohello: [Azure 應用程式服務和其對影響現有的 Azure 服務](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[Python 開發人員中心]: /develop/python/
[Azure 雲端服務]: ../cloud-services/cloud-services-python-ptvs.md
[文件]:../cosmos-db/table-storage-how-to-use-python.md
[如何 tooUse hello 來自 Python 的資料表儲存體服務]:../cosmos-db/table-storage-how-to-use-python.md

<!--External Link references-->
[Azure Portal]: https://portal.azure.com
[Azure SDK for.NET]: http://azure.microsoft.com/downloads/
[Python Tools for Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Python Tools 2.2 for Visual Studio 範例 VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?linkid=518003
[Python 2.7 32 位元]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 32 位元]: http://go.microsoft.com/fwlink/?LinkId=517191
[Python Tools for Visual Studio 說明文件]: http://aka.ms/ptvsdocs
[Flask 說明文件 (英文)]: http://flask.pocoo.org/
[在 Microsoft Azure 上進行遠端偵錯]: http://go.microsoft.com/fwlink/?LinkId=624026
[Web 專案]: http://go.microsoft.com/fwlink/?LinkId=624027
[雲端服務專案]: http://go.microsoft.com/fwlink/?LinkId=624028
[Azure 儲存體]: http://azure.microsoft.com/documentation/services/storage/
[Azure SDK for Python]: https://github.com/Azure/azure-sdk-for-python
