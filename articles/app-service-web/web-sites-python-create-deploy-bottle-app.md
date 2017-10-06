---
title: "在 Azure 中的 Bottle aaaPython web 應用程式"
description: "此教學課程為您介紹 toorunning Python web 應用程式在 Azure App Service Web 應用程式。"
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 84f043b8-9d05-479f-a9d0-d0d9a32a0bb9
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2016
ms.author: huvalo
ms.openlocfilehash: 98acd7d8fcdbba326625121c20f9237d2663ea1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-bottle-in-azure"></a>在 Azure 中使用 Bottle 建立 Web 應用程式
本教學課程描述 tooget 啟動 Azure App Service Web 應用程式中執行 Python 的方式。 Web Apps 提供有限的免費裝載和快速部署，而您可以使用 Python！ 當您的應用程式成長，您可以切換 toopaid 裝載，您也可以與所有的整合 hello 其他 Azure 服務。

您將建立使用 hello Bottle web 架構的 web 應用程式 (請參閱本教學課程中的替代版本[Django](web-sites-python-create-deploy-django-app.md)和[酒瓶](web-sites-python-create-deploy-flask-app.md))。 您會建立從 hello Azure Marketplace 的 hello web 應用程式、 設定 Git 部署和複製本機 hello 儲存機制。 然後您會在本機執行 hello web 應用程式、 進行變更、 認可並推送它們太[Azure App Service Web 應用程式](http://go.microsoft.com/fwlink/?LinkId=529714)。 hello 教學課程顯示如何 toodo 於 Windows 或 Mac/Linux。

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> 如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。 不需要信用卡；沒有承諾。
> 
> 

## <a name="prerequisites"></a>必要條件
* Windows、Mac 或 Linux
* Python 2.7 或 3.4
* setuptools、pip、virtualenv (僅 Python 2.7)
* Git
* [Python Tools 2.2 for Visual Studio][Python Tools 2.2 for Visual Studio] (PTVS) - 注意：這是選擇性的

**注意**：Python 專案目前不支援 TFS 發佈。

### <a name="windows"></a>Windows
如果您還沒有安裝 Python 2.7 或 3.4 (32 位元)，建議您使用 Web Platform Installer 安裝 [Azure SDK for Python 2.7] 或 [Azure SDK for Python 3.4]。 這會安裝 hello 32 位元版本的 Python、 setuptools、 pip、 virtualenv 等 （32 位元 Python 是 hello Azure 主機機器上安裝的內容）。 或者，您可以從 [python.org]取得 Python。

針對 Git，建議您安裝 [Git for Windows] 或 [GitHub for Windows]。 如果您使用 Visual Studio，您可以使用整合的 hello Git 支援。

我們也建議您安裝 [Python Tools 2.2 for Visual Studio]。 這是選擇性的但如果您有[Visual Studio]，包括 hello 釋放 Visual Studio Community 2013 或 Visual Studio Express 2013 for Web，則這會提供絕佳的 Python IDE。

### <a name="maclinux"></a>Mac/Linux
您應該已經安裝 Python 與 Git，但請確定您擁有的是 Python 2.7 或 3.4。

## <a name="web-app-creation-on-hello-azure-portal"></a>在 hello Azure 入口網站上建立 web 應用程式
hello 第一個步驟中建立您的應用程式是 toocreate hello web 應用程式，透過 hello [Azure 入口網站](https://portal.azure.com)。  

1. 登入 hello Azure 入口網站並按一下 hello**新增**hello 左下角中的按鈕。 
2. 在 hello 搜尋方塊中輸入"python"。
3. 在 hello 搜尋結果中，選取  **Bottle**，然後按一下 **建立**。
4. 設定 hello 新 Bottle 應用程式，例如為它建立新的應用程式服務方案和新的資源群組。 然後按一下 [ **建立**]。
5. 設定 Git 發行功能，新建立的 web 應用程式在 hello 指示[應用程式服務的本機 Git 部署 tooAzure](app-service-deploy-local-git.md)。

## <a name="application-overview"></a>應用程式概觀
### <a name="git-repository-contents"></a>Git 儲存機制內容
以下是您會發現在 hello 初始 Git 儲存機制，我們將複製 hello 下一節中的 hello 檔案的概觀。

    \routes.py
    \static\content\
    \static\fonts\
    \static\scripts\
    \views\about.tpl
    \views\contact.tpl
    \views\index.tpl
    \views\layout.tpl

Hello 應用程式的主要來源。 包含 3 個主要的版面配置頁面 (index、about、contact)。  靜態內容和指令碼，包含啟動程序、jquery、modernizr 和回應。

    \app.py

本機開發伺服器支援。 在本機上使用此 toorun hello 應用程式。

    \BottleWebProject.pyproj
    \BottleWebProject.sln

搭配 [Python Tools for Visual Studio]使用的專案檔。

    \ptvs_virtualenv_proxy.py

虛擬環境和 PTVS 遠端偵錯支援的 IIS Proxy。

    \requirements.txt

此應用程式所需的外部封裝。 hello 部署指令碼將 pip 安裝 hello 封裝這個檔案中列出。

    \web.2.7.config
    \web.3.4.config

IIS 組態檔。 將使用 hello 適當 web.x.y.config hello 部署指令碼，並將它複製為 web.config。

### <a name="optional-files---customizing-deployment"></a>選用的檔案 - 自訂部署
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a>選用的檔案 - Python 執行階段
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a>在伺服器上的其他檔案
某些檔案存在於 hello 伺服器，但不是會新增 toohello git 儲存機制。 這些被建立 hello 部署指令碼。

    \web.config

IIS 組態檔。 從 web.x.y.config 建立於每個部署上。

    \env\

Python 虛擬環境。 如果相容的虛擬環境不存在 hello web 應用程式上，在部署期間建立。  封裝中 requirements.txt 列出 pip 安裝，但 pip 會略過安裝，如果已安裝 hello 封裝。

hello 接下來的 3 各節說明如何以 hello tooproceed web 3 不同環境下的應用程式開發：

* Windows，使用 Python Tools for Visual Studio
* Windows，使用命令列
* Mac/Linux，使用命令列

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a>Web 應用程式開發 - Windows - 適用於 Visual Studio 的 Python 工具
### <a name="clone-hello-repository"></a>複製 hello 儲存機制
首先，複製 hello 儲存機制使用 hello hello Azure 入口網站上所提供的 url。 如需詳細資訊，請參閱[應用程式服務的本機 Git 部署 tooAzure](app-service-deploy-local-git.md)。

開啟包含 hello hello 儲存機制的根目錄中的 hello 方案檔 (.sln)。

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-solution-bottle.png)

### <a name="create-virtual-environment"></a>建立虛擬環境
現在我們要建立本機開發的虛擬環境。 以滑鼠右鍵按一下 [Python 環境]，選取 [新增虛擬環境...]。

* 請確定 hello 環境的 hello 名稱`env`。
* 選取 hello 基底直譯器。 請確定 toouse hello 相同版本的 web 應用程式的已選取的 Python (runtime.txt 或 hello**應用程式設定**刀鋒視窗中的 hello Azure 入口網站中的 web 應用程式)。
* 請確定已核取 hello 選項 toodownload 和安裝封裝。

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-add-virtual-env-27.png)

按一下 [建立] 。 將建立 hello 虛擬環境中，並安裝相依項目 requirements.txt 中列出。

### <a name="run-using-development-server"></a>使用開發伺服器來執行
偵錯，請按 F5 toostart 和網頁瀏覽器會開啟自動在本機執行的 toohello 頁面。

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

您可以在 hello 來源、 使用 hello 監看式視窗和其他內容中設定中斷點。請參閱 hello [Python Tools for Visual Studio 文件]如需有關 hello 各種功能。

### <a name="make-changes"></a>進行變更
現在您可以嘗試藉由變更 toohello 應用程式來源及/或範本。

測試過您的變更之後，認可這些 toohello Git 儲存機制：

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-commit-bottle.png)

### <a name="install-more-packages"></a>安裝更多封裝
您的應用程式可能會擁有 Python 和 Bottle 之外的相依性。

您可以使用 pip 安裝其他封裝。 tooinstall 封裝時，以滑鼠右鍵按一下 hello 虛擬環境，並選取**安裝 Python 封裝**。

例如，tooinstall hello Azure SDK for Python 可讓您存取 tooAzure 儲存體、 服務匯流排和其他 Azure 服務，輸入`azure`:

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-install-package-dialog.png)

以滑鼠右鍵按一下 hello 虛擬環境，然後選取**產生 requirements.txt** tooupdate requirements.txt。

然後，認可 hello 變更 toorequirements.txt toohello Git 儲存機制。

### <a name="deploy-tooazure"></a>部署 tooAzure
tootrigger 部署中，按一下 **同步**或**推送**。 同步處理會推送和提取。

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-git-push.png)

hello 第一次部署將需要一些時間，因為它會建立虛擬環境、 安裝套件和其他內容。

Visual Studio 不會顯示 hello 部署的 hello 進度。 如果您想要 tooreview hello 輸出，請參閱 hello 章節[疑難排解-部署](#troubleshooting-deployment)。

瀏覽 toohello Azure URL tooview 您的變更。

## <a name="web-app-development---windows---command-line"></a>Web 應用程式開發 - Windows - 命令列
### <a name="clone-hello-repository"></a>複製 hello 儲存機制
首先，複製 hello 儲存機制使用 hello hello Azure 網站上所提供的 URL，並新增與遠端的 hello Azure 儲存機制。 如需詳細資訊，請參閱[應用程式服務的本機 Git 部署 tooAzure](app-service-deploy-local-git.md)。

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a>建立虛擬環境
我們將建立新的虛擬環境，供開發應用程式 （不要將它 toohello 儲存機制）。 Python 中的虛擬環境並不是可重置，因此處理 hello 應用程式開發人員會建立自己在本機。

請確定 toouse hello 相同的 web 應用程式 （在 runtime.txt 或 hello 應用程式設定 刀鋒視窗中 hello Azure 入口網站 web 應用程式） 選取的 Python 版本

針對 Python 2.7：

    c:\python27\python.exe -m virtualenv env

針對 Python 3.4：

    c:\python34\python.exe -m venv env

安裝應用程式所需的任何外部封裝。 您可以在虛擬環境中，根目錄 hello hello 儲存機制 tooinstall hello 封裝使用 hello requirements.txt 檔案：

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a>使用開發伺服器來執行
您可以啟動 hello 應用程式開發伺服器底下，以 hello 下列命令：

    env\scripts\python app.py

hello 主控台就會顯示 hello URL，而且會接聽通訊埠 hello 伺服器：

![](./media/web-sites-python-create-deploy-bottle-app/windows-run-local-bottle.png)

然後，開啟您的 web 瀏覽器 toothat URL。

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

### <a name="make-changes"></a>進行變更
現在您可以嘗試藉由變更 toohello 應用程式來源及/或範本。

測試過您的變更之後，認可這些 toohello Git 儲存機制：

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a>安裝更多封裝
您的應用程式可能會擁有 Python 和 Bottle 之外的相依性。

您可以使用 pip 安裝其他封裝。 例如，tooinstall hello Azure SDK for Python 可讓您存取 tooAzure 儲存體、 服務匯流排和其他 Azure 服務類型：

    env\scripts\pip install azure

請確定 tooupdate requirements.txt:

    env\scripts\pip freeze > requirements.txt

認可 hello 變更：

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a>部署 tooAzure
tootrigger 部署，推入 hello 變更 tooAzure:

    git push azure master

您會看到 hello 輸出 hello 部署指令碼，包括建立虛擬環境安裝封裝，建立 web.config。

瀏覽 toohello Azure URL tooview 您的變更。

## <a name="web-app-development---maclinux---command-line"></a>Web 應用程式開發 - Mac/Linux - 命令列
### <a name="clone-hello-repository"></a>複製 hello 儲存機制
首先，複製 hello 儲存機制使用 hello hello Azure 網站上所提供的 URL，並新增與遠端的 hello Azure 儲存機制。 如需詳細資訊，請參閱[應用程式服務的本機 Git 部署 tooAzure](app-service-deploy-local-git.md)。

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a>建立虛擬環境
我們將建立新的虛擬環境，供開發應用程式 （不要將它 toohello 儲存機制）。 Python 中的虛擬環境並不是可重置，因此處理 hello 應用程式開發人員會建立自己在本機。

請確定 toouse hello 相同版本的 Python 選取 web 應用程式 （在 runtime.txt 或 hello 應用程式設定 刀鋒視窗的 hello Azure 入口網站中的 web 應用程式）。

針對 Python 2.7：

    python -m virtualenv env

針對 Python 3.4：

    python -m venv env
或 pyvenv env

安裝應用程式所需的任何外部封裝。 您可以在虛擬環境中，根目錄 hello hello 儲存機制 tooinstall hello 封裝使用 hello requirements.txt 檔案：

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a>使用開發伺服器來執行
您可以啟動 hello 應用程式開發伺服器底下，以 hello 下列命令：

    env/bin/python app.py

hello 主控台就會顯示 hello URL，而且會接聽通訊埠 hello 伺服器：

![](./media/web-sites-python-create-deploy-bottle-app/mac-run-local-bottle.png)

然後，開啟您的 web 瀏覽器 toothat URL。

![](./media/web-sites-python-create-deploy-bottle-app/mac-browser-bottle.png)

### <a name="make-changes"></a>進行變更
現在您可以嘗試藉由變更 toohello 應用程式來源及/或範本。

測試過您的變更之後，認可這些 toohello Git 儲存機制：

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a>安裝更多封裝
您的應用程式可能會擁有 Python 和 Bottle 之外的相依性。

您可以使用 pip 安裝其他封裝。 例如，tooinstall hello Azure SDK for Python 可讓您存取 tooAzure 儲存體、 服務匯流排和其他 Azure 服務類型：

    env/bin/pip install azure

請確定 tooupdate requirements.txt:

    env/bin/pip freeze > requirements.txt

認可 hello 變更：

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a>部署 tooAzure
tootrigger 部署，推入 hello 變更 tooAzure:

    git push azure master

您會看到 hello 輸出 hello 部署指令碼，包括建立虛擬環境安裝封裝，建立 web.config。

瀏覽 toohello Azure URL tooview 您的變更。

## <a name="troubleshooting---package-installation"></a>疑難排解 - 封裝安裝
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a>疑難排解 - 虛擬環境
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a>後續步驟
請遵循這些連結 toolearn 更多關於 Bottle 和 Python Tools for Visual Studio: 

* [Bottle 說明文件]
* [Python Tools for Visual Studio 文件]

如需有關使用 Azure 資料表儲存體和 MongoDB 的資訊：

* [Azure 上使用 Python Tools for Visual Studio 的 Bottle 和 MongoDB]
* [Azure 上使用 Python Tools for Visual Studio 的 Bottle 和 Azure 資料表儲存體]

## <a name="whats-changed"></a>變更的項目
* 從網站 tooApp 服務變更如指南 toohello: [Azure 應用程式服務和其對影響現有的 Azure 服務](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[Azure 上使用 Python Tools for Visual Studio 的 Bottle 和 MongoDB]: web-sites-python-ptvs-bottle-table-storage.md
[Azure 上使用 Python Tools for Visual Studio 的 Bottle 和 Azure 資料表儲存體]: web-sites-python-ptvs-bottle-table-storage.md

<!--External Link references-->
[Azure SDK for Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281
[Azure SDK for Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990
[python.org]: http://www.python.org/
[Git for Windows]: http://msysgit.github.io/
[GitHub for Windows]: https://windows.github.com/
[Python Tools for Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Visual Studio]: http://www.visualstudio.com/
[Python Tools for Visual Studio 文件]: http://aka.ms/ptvsdocs 
[Bottle 說明文件]: http://bottlepy.org/docs/dev/index.html

