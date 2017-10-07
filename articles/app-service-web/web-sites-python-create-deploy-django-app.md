---
title: "在 Azure 中的 Django aaaCreating web 應用程式"
description: "此教學課程為您介紹 toorunning Python web 應用程式在 Azure App Service Web 應用程式。"
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 9be1a05a-9460-49ae-94fb-9798f82c11cf
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2016
ms.author: huvalo
ms.openlocfilehash: 26a131da358748bd6fe4ee5c114d0a8f91b83cfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-django-in-azure"></a>在 Azure 中使用 Django 建立 Web 應用程式
這個教學課程描述如何 tooget 啟動上執行 Python [Azure App Service Web 應用程式](http://go.microsoft.com/fwlink/?LinkId=529714)。 Web Apps 提供有限的免費裝載和快速部署，而您可以使用 Python！ 當您的應用程式成長，您可以切換 toopaid 裝載，您也可以與所有的整合 hello 其他 Azure 服務。

您將建立使用 hello Django web 架構的應用程式 (請參閱本教學課程中的替代版本[酒瓶](web-sites-python-create-deploy-flask-app.md)和[Bottle](web-sites-python-create-deploy-bottle-app.md))。 您會建立從 hello Azure Marketplace 的 hello web 應用程式、 設定 Git 部署和複製本機 hello 儲存機制。 然後，您會在本機執行 hello 應用程式、 進行變更、 認可並推送它們 tooAzure。 hello 教學課程顯示如何 toodo 於 Windows 或 Mac/Linux。

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
* [Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - 注意：這是選擇性的

**注意**：Python 專案目前不支援 TFS 發佈。

### <a name="windows"></a>Windows
如果您還沒有安裝 Python 2.7 或 3.4 (32 位元)，建議您使用 Web Platform Installer 安裝 [Azure SDK for Python 2.7] 或 [Azure SDK for Python 3.4]。 這會安裝 hello 32 位元版本的 Python、 setuptools、 pip、 virtualenv 等 （32 位元 Python 是 hello Azure 主機機器上安裝的內容）。 或者，您可以從 [python.org]取得 Python。

針對 Git，建議您安裝 [Git for Windows] 或 [GitHub for Windows]。 如果您使用 Visual Studio，您可以使用整合的 hello Git 支援。

我們也建議您安裝 [Python Tools 2.2 for Visual Studio]。 這是選擇性的但如果您有[Visual Studio]，包括 hello 釋放 Visual Studio Community 2013 或 Visual Studio Express 2013 for Web，則這會提供絕佳的 Python IDE。

### <a name="maclinux"></a>Mac/Linux
您應該已經安裝 Python 與 Git，但請確定您擁有的是 Python 2.7 或 3.4。

## <a name="web-app-creation-on-portal"></a>在入口網站中建立 Web 應用程式
hello 第一個步驟中建立您的應用程式是 toocreate hello web 應用程式，透過 hello [Azure 入口網站](https://portal.azure.com)。

1. 登入 hello Azure 入口網站並按一下 hello**新增**hello 左下角中的按鈕。
2. 在 hello 搜尋方塊中輸入"python"。
3. 在 hello 搜尋結果中，選取  **Django** （發行 PTVS），然後按一下 **建立**。
4. 設定 hello 新 Django 應用程式，例如為它建立新的應用程式服務方案和新的資源群組。 然後按一下 [ **建立**]。
5. 設定 Git 發行功能，新建立的 web 應用程式在 hello 指示[應用程式服務的本機 Git 部署 tooAzure](app-service-deploy-local-git.md)。

## <a name="application-overview"></a>應用程式概觀
### <a name="git-repository-contents"></a>Git 儲存機制內容
以下是您會發現在 hello 初始 Git 儲存機制，我們將複製 hello 下一節中的 hello 檔案的概觀。

    \app\__init__.py
    \app\forms.py
    \app\models.py
    \app\tests.py
    \app\views.py
    \app\static\content\
    \app\static\fonts\
    \app\static\scripts\
    \app\templates\about.html
    \app\templates\contact.html
    \app\templates\index.html
    \app\templates\layout.html
    \app\templates\login.html
    \app\templates\loginpartial.html
    \DjangoWebProject\__init__.py
    \DjangoWebProject\settings.py
    \DjangoWebProject\urls.py
    \DjangoWebProject\wsgi.py

Hello 應用程式的主要來源。 包含 3 個主要的版面配置頁面 (index、about、contact)。 靜態內容和指令碼，包含啟動程序、jquery、modernizr 和回應。

    \manage.py

本機管理和開發伺服器支援。 在本機上使用此 toorun hello 應用程式，同步處理 hello 資料庫等等。

    \db.sqlite3

預設資料庫。 包含 hello hello 應用程式 toorun，針對必要的資料表，但不包含任何使用者 （同步處理 hello 資料庫 toocreate 使用者）。

    \DjangoWebProject.pyproj
    \DjangoWebProject.sln

搭配 [Python Tools for Visual Studio]使用的專案檔。

    \ptvs_virtualenv_proxy.py

虛擬環境和 PTVS 遠端偵錯支援的 IIS Proxy。

    \requirements.txt

此應用程式所需的外部封裝。 hello 部署指令碼將 pip 安裝 hello 封裝這個檔案中列出。

    \web.2.7.config
    \web.3.4.config

IIS 組態檔。 將使用 hello 適當 web.x.y.config hello 部署指令碼，並將它複製為 web.config。

### <a name="optional-files---customizing-deployment"></a>選用的檔案 - 自訂部署
[!INCLUDE [web-sites-python-django-customizing-deployment](../../includes/web-sites-python-django-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a>選用的檔案 - Python 執行階段
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a>在伺服器上的其他檔案
某些檔案存在於 hello 伺服器，但不是會新增 toohello git 儲存機制。 這些被建立 hello 部署指令碼。

    \web.config

IIS 組態檔。 從 web.x.y.config 建立於每個部署上。

    \env\

Python 虛擬環境。 如果相容的虛擬環境不存在 hello web 應用程式上，在部署期間建立。 封裝中 requirements.txt 列出 pip 安裝，但 pip 會略過安裝，如果已安裝 hello 封裝。

hello 接下來的 3 各節說明如何以 hello tooproceed web 3 不同環境下的應用程式開發：

* Windows，使用 Python Tools for Visual Studio
* Windows，使用命令列
* Mac/Linux，使用命令列

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a>Web 應用程式開發 - Windows - 適用於 Visual Studio 的 Python 工具
### <a name="clone-hello-repository"></a>複製 hello 儲存機制
首先，複製 hello 儲存機制使用 hello hello Azure 入口網站上所提供的 URL。 如需詳細資訊，請參閱[應用程式服務的本機 Git 部署 tooAzure](app-service-deploy-local-git.md)。

開啟包含 hello hello 儲存機制的根目錄中的 hello 方案檔 (.sln)。

![](./media/web-sites-python-create-deploy-django-app/ptvs-solution-django.png)

### <a name="create-virtual-environment"></a>建立虛擬環境
現在我們要建立本機開發的虛擬環境。 以滑鼠右鍵按一下 [Python 環境]，選取 [新增虛擬環境...]。

* 請確定 hello 環境的 hello 名稱`env`。
* 選取 hello 基底直譯器。 請確定 toouse hello 相同版本的 web 應用程式的已選取的 Python (runtime.txt 或 hello**應用程式設定**刀鋒視窗中的 hello Azure 入口網站中的 web 應用程式)。
* 請確定已核取 hello 選項 toodownload 和安裝封裝。

![](./media/web-sites-python-create-deploy-django-app/ptvs-add-virtual-env-27.png)

按一下 [建立] 。 將建立 hello 虛擬環境中，並安裝相依項目 requirements.txt 中列出。

### <a name="create-a-superuser"></a>建立超級使用者
hello hello 應用程式所包含的資料庫並沒有定義任何超級使用者。 在訂單 toouse hello 登入功能 hello 應用程式或 hello Django 管理介面中 (如果您決定 tooenable 它)，您將需要 toocreate 超級使用者。

這個 hello 從命令列從執行您的專案資料夾：

    env\scripts\python manage.py createsuperuser

請遵循 hello 提示 tooset hello 使用者名稱、 密碼等。

### <a name="run-using-development-server"></a>使用開發伺服器來執行
偵錯，請按 F5 toostart 和網頁瀏覽器會開啟自動在本機執行的 toohello 頁面。

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

您可以在 hello 來源、 使用 hello 監看式視窗和其他內容中設定中斷點。請參閱 hello [Python Tools for Visual Studio 文件]如需有關 hello 各種功能。

### <a name="make-changes"></a>進行變更
現在您可以嘗試藉由變更 toohello 應用程式來源及/或範本。

測試過您的變更之後，認可這些 toohello Git 儲存機制：

![](./media/web-sites-python-create-deploy-django-app/ptvs-commit-django.png)

### <a name="install-more-packages"></a>安裝更多封裝
您的應用程式可能會擁有 Python 和 Django 之外的相依性。

您可以使用 pip 安裝其他封裝。 tooinstall 封裝時，以滑鼠右鍵按一下 hello 虛擬環境，並選取**安裝 Python 封裝**。

例如，tooinstall hello Azure SDK for Python 可讓您存取 tooAzure 儲存體、 服務匯流排和其他 Azure 服務，輸入`azure`:

![](./media/web-sites-python-create-deploy-django-app/ptvs-install-package-dialog.png)

以滑鼠右鍵按一下 hello 虛擬環境，然後選取**產生 requirements.txt** tooupdate requirements.txt。

然後，認可 hello 變更 toorequirements.txt toohello Git 儲存機制。

### <a name="deploy-tooazure"></a>部署 tooAzure
tootrigger 部署中，按一下 **同步**或**推送**。 同步處理會推送和提取。

![](./media/web-sites-python-create-deploy-django-app/ptvs-git-push.png)

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

請確定 toouse hello 相同版本的 Python 選取 web 應用程式 （在 runtime.txt 或 hello 應用程式設定 刀鋒視窗的 hello Azure 入口網站中的 web 應用程式）。

針對 Python 2.7：

    c:\python27\python.exe -m virtualenv env

針對 Python 3.4：

    c:\python34\python.exe -m venv env

安裝應用程式所需的任何外部封裝。 您可以在虛擬環境中，根目錄 hello hello 儲存機制 tooinstall hello 封裝使用 hello requirements.txt 檔案：

    env\scripts\pip install -r requirements.txt

### <a name="create-a-superuser"></a>建立超級使用者
hello hello 應用程式所包含的資料庫並沒有定義任何超級使用者。 在訂單 toouse hello 登入功能 hello 應用程式或 hello Django 管理介面中 (如果您決定 tooenable 它)，您將需要 toocreate 超級使用者。

這個 hello 從命令列從執行您的專案資料夾：

    env\scripts\python manage.py createsuperuser

請遵循 hello 提示 tooset hello 使用者名稱、 密碼等。

### <a name="run-using-development-server"></a>使用開發伺服器來執行
您可以啟動 hello 應用程式開發伺服器底下，以 hello 下列命令：

    env\scripts\python manage.py runserver

hello 主控台就會顯示 hello URL，而且會接聽通訊埠 hello 伺服器：

![](./media/web-sites-python-create-deploy-django-app/windows-run-local-django.png)

然後，開啟您的 web 瀏覽器 toothat URL。

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

### <a name="make-changes"></a>進行變更
現在您可以嘗試藉由變更 toohello 應用程式來源及/或範本。

測試過您的變更之後，認可這些 toohello Git 儲存機制：

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a>安裝更多封裝
您的應用程式可能會擁有 Python 和 Django 之外的相依性。

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

或

    pyvenv env

安裝應用程式所需的任何外部封裝。 您可以在虛擬環境中，根目錄 hello hello 儲存機制 tooinstall hello 封裝使用 hello requirements.txt 檔案：

    env/bin/pip install -r requirements.txt

### <a name="create-a-superuser"></a>建立超級使用者
hello hello 應用程式所包含的資料庫並沒有定義任何超級使用者。 在訂單 toouse hello 登入功能 hello 應用程式或 hello Django 管理介面中 (如果您決定 tooenable 它)，您將需要 toocreate 超級使用者。

這個 hello 從命令列從執行您的專案資料夾：

    env/bin/python manage.py createsuperuser

請遵循 hello 提示 tooset hello 使用者名稱、 密碼等。

### <a name="run-using-development-server"></a>使用開發伺服器來執行
您可以啟動 hello 應用程式開發伺服器底下，以 hello 下列命令：

    env/bin/python manage.py runserver

hello 主控台就會顯示 hello URL，而且會接聽通訊埠 hello 伺服器：

![](./media/web-sites-python-create-deploy-django-app/mac-run-local-django.png)

然後，開啟您的 web 瀏覽器 toothat URL。

![](./media/web-sites-python-create-deploy-django-app/mac-browser-django.png)

### <a name="make-changes"></a>進行變更
現在您可以嘗試藉由變更 toohello 應用程式來源及/或範本。

測試過您的變更之後，認可這些 toohello Git 儲存機制：

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a>安裝更多封裝
您的應用程式可能會擁有 Python 和 Django 之外的相依性。

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

## <a name="troubleshooting---static-files"></a>疑難排解 - 靜態檔案
Django 並收集靜態檔案的 hello 概念。 這會從其原始位置中取得所有 hello 靜態檔案，並將其複製 tooa 單一資料夾。 此應用程式，將它們複製太`/static`。

這是因為靜態檔案可能來自不同的 Django「應用程式」。 比方說，hello Django 管理介面中的 hello 靜態檔案位於 hello 虛擬環境中如 Django 程式庫的子資料夾中。 此應用程式所定義的靜態檔案位於 `/app/static`。 當您使用多個 Django「應用程式」時 ，您必須擁有位於多個位置中的靜態檔案。

當偵錯模式執行 hello 應用程式，hello 應用程式服務的 hello 靜態檔案從其原始位置。

在發行模式中執行 hello 應用程式，hello 應用程式會執行**不**做 hello 靜態檔案。 負責 hello hello web 伺服器 tooserve hello 檔案。 此應用程式中，IIS 會提供 hello 靜態檔`/static`。

hello 靜態檔案的集合做為組件的 hello 部署指令碼中，清除先前收集的檔案會自動完成的。 這表示 hello 回收會針對每個部署，一個位元速度減緩部署，但是它確保過時的檔案，將無法使用，避免潛在的安全性問題。

如果您想 tooskip 靜態檔案的集合，如 Django 應用程式：

    \.skipDjango

然後您將在本機電腦上手動需要 toodo hello 集合：

    env\scripts\python manage.py collectstatic

然後移除 hello`\static`資料夾從`.gitignore`並將它加入 toohello Git 儲存機制。

## <a name="troubleshooting---settings"></a>疑難排解 - 設定
Hello 應用程式的各種設定可以變更在`DjangoWebProject/settings.py`。

為了開發人員方便起見，已啟用偵錯模式。 一個好所造成的副作用，是您在本機執行，而不需要 toocollect 靜態檔案時將會無法 toosee 映像，而且其他靜態內容。

toodisable 偵錯模式：

    DEBUG = False

停用偵錯時，hello 值`ALLOWED_HOSTS`需求 toobe 更新 tooinclude hello Azure 主機名稱。 例如：

    ALLOWED_HOSTS = (
        'pythonapp.azurewebsites.net',
    )

或 tooenable 任何：

    ALLOWED_HOSTS = (
        '*',
    )

在實務上，您可能想 toodo 更複雜的 toodeal 之間切換偵錯與發行模式中，並取得 hello 主機名稱的項目。

您可以設定環境變數，透過 Azure 入口網站 hello**設定** 頁面的 hello**應用程式設定**> 一節。  這可用於設定值，您可能不想 tooappear hello 來源 （連接字串、 密碼等），或您想 tooset Azure 與您的本機電腦之間的不同。 在`settings.py`，您可以查詢 hello 環境變數使用`os.getenv`。

## <a name="using-a-database"></a>使用資料庫
sqlite 資料庫 hello 資料庫所包含的 hello 應用程式。 這是方便且實用的預設資料庫 toouse 進行開發，因為它不需要的幾乎任何設定。 hello 資料庫會儲存在 hello 專案資料夾中的 hello db.sqlite3 檔案。

Azure 會提供資料庫服務，而這是簡單 toouse 從 Django 應用程式。 教學課程使用[SQL Database]和[MySQL]從 Django 應用程式顯示 hello 步驟需要 toocreate hello 資料庫服務，變更中的 hello 資料庫設定`DjangoWebProject/settings.py`，和 hello程式庫需要 tooinstall。

當然，如果您偏好 toomanage 您自己的資料庫伺服器，您可以使用在 Azure 上執行的 Windows 或 Linux 的虛擬機器。

## <a name="django-admin-interface"></a>Django 管理介面
一旦您開始建置您的模型，您會想 toopopulate hello 資料庫，某些資料。 Toodo 加入，以互動方式編輯內容的簡單方法是 toouse hello Django 管理介面。

hello hello 管理介面的程式碼會標記為註解中 hello 應用程式的來源，但明確標示讓您輕鬆地啟用它 （搜尋 'admin'）。

啟用之後，同步處理 hello 資料庫、 執行 hello 應用程式並瀏覽過`/admin`。

## <a name="next-steps"></a>後續步驟
請遵循這些連結 toolearn 更多關於如 Django 和 Python Tools for Visual Studio:

* [Django 說明文件]
* [Python Tools for Visual Studio 文件]

如需使用 SQL Database 和 MySQL 的資訊：

* [Azure 上使用 Python Tools for Visual Studio 的 Django 和 MySQL]
* [Azure 上使用 Python Tools for Visual Studio 的 Django 和 SQL Database]

如需詳細資訊，請參閱 hello [Python 開發人員中心](/develop/python/)。

## <a name="whats-changed"></a>變更的項目
* 從網站 tooApp 服務變更如指南 toohello: [Azure 應用程式服務和其對影響現有的 Azure 服務](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[Azure 上使用 Python Tools for Visual Studio 的 Django 和 MySQL]: web-sites-python-ptvs-django-mysql.md
[Azure 上使用 Python Tools for Visual Studio 的 Django 和 SQL Database]: web-sites-python-ptvs-django-sql.md
[SQL Database]: web-sites-python-ptvs-django-sql.md
[MySQL]: web-sites-python-ptvs-django-mysql.md

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
[Django 說明文件]: https://www.djangoproject.com/
