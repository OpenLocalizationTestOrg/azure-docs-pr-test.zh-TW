---
title: "aaaConfiguring Python 與 Azure App Service Web 應用程式"
description: "本教學課程描述在 Azure App Service Web Apps 上編寫與設定基本的 Web 伺服器閘道介面 (WSGI) 相容之 Python 應用程式的選項。"
services: app-service
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: fd00dc91-9935-4331-b955-4bd71e66d518
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/26/2016
ms.author: huvalo
ms.openlocfilehash: 00d49fb01491e9adb4b6fededfb95669a8dbd485
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-python-with-azure-app-service-web-apps"></a><span data-ttu-id="a3953-103">使用 Azure App Service Web Apps 設定 Python</span><span class="sxs-lookup"><span data-stu-id="a3953-103">Configuring Python with Azure App Service Web Apps</span></span>
<span data-ttu-id="a3953-104">本教學課程描述在 [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714)上編寫與設定基本的 Web 伺服器閘道介面 (WSGI) 相容之 Python 應用程式的選項。</span><span class="sxs-lookup"><span data-stu-id="a3953-104">This tutorial describes options for authoring and configuring a basic Web Server Gateway Interface (WSGI) compliant Python application on [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="a3953-105">它會說明 Git 部署的其他功能，例如虛擬環境和使用 requirements.txt 進行封裝安裝。</span><span class="sxs-lookup"><span data-stu-id="a3953-105">It describes additional features of Git deployment, such as virtual environment and package installation using requirements.txt.</span></span>

## <a name="bottle-django-or-flask"></a><span data-ttu-id="a3953-106">Bottle、Django 或 Flask？</span><span class="sxs-lookup"><span data-stu-id="a3953-106">Bottle, Django or Flask?</span></span>
<span data-ttu-id="a3953-107">hello Azure Marketplace 包含 hello Bottle，如 Django 和酒瓶介面架構的範本。</span><span class="sxs-lookup"><span data-stu-id="a3953-107">hello Azure Marketplace contains templates for hello Bottle, Django and Flask frameworks.</span></span> <span data-ttu-id="a3953-108">如果您正在開發 Azure 應用程式服務中，第一個 web 應用程式，或您不熟悉 Git，我們建議您遵循這些教學課程包含逐步指示來建立工作中的應用程式使用 Git 部署的 hello 圖庫的其中一個從 Windows 或 Mac:</span><span class="sxs-lookup"><span data-stu-id="a3953-108">If you are developing your first web app in Azure App Service, or you are not familiar with Git, we recommend that you follow one of these tutorials, which include step-by-step instructions for building a working application from hello gallery using Git deployment from Windows or Mac:</span></span>

* [<span data-ttu-id="a3953-109">利用 Bottle 建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a3953-109">Creating web apps with Bottle</span></span>](web-sites-python-create-deploy-bottle-app.md)
* [<span data-ttu-id="a3953-110">利用 Django 建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a3953-110">Creating web apps with Django</span></span>](web-sites-python-create-deploy-django-app.md)
* [<span data-ttu-id="a3953-111">利用 Flask 建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a3953-111">Creating web apps with Flask</span></span>](web-sites-python-create-deploy-flask-app.md)

## <a name="web-app-creation-on-azure-portal"></a><span data-ttu-id="a3953-112">在 Azure 入口網站上建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a3953-112">Web app creation on Azure Portal</span></span>
<span data-ttu-id="a3953-113">本教學課程假設現有 Azure 訂用帳戶和存取 toohello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="a3953-113">This tutorial assumes an existing Azure subscription and access toohello Azure Portal.</span></span>

<span data-ttu-id="a3953-114">如果您沒有現有的 web 應用程式，您可以建立一個從 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="a3953-114">If you do not have an existing web app, you can create one from hello [Azure Portal](https://portal.azure.com).</span></span>  <span data-ttu-id="a3953-115">按一下 hello 新按鈕在 hello 左上角，然後按一下**Web + 行動** > **Web 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a3953-115">Click hello NEW button in hello top left corner, then click **Web + Mobile** > **Web app**.</span></span>

## <a name="git-publishing"></a><span data-ttu-id="a3953-116">Git 發行</span><span class="sxs-lookup"><span data-stu-id="a3953-116">Git Publishing</span></span>
<span data-ttu-id="a3953-117">設定 Git 發行功能，新建立的 web 應用程式在 hello 指示[應用程式服務的本機 Git 部署 tooAzure](app-service-deploy-local-git.md)。</span><span class="sxs-lookup"><span data-stu-id="a3953-117">Configure Git publishing for your newly created web app by following hello instructions at [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span> <span data-ttu-id="a3953-118">本教學課程使用 Git toocreate、 管理及發行我們 Python web 應用程式 tooAzure 應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="a3953-118">This tutorial uses Git toocreate, manage, and publish our Python web app tooAzure App Service.</span></span>

<span data-ttu-id="a3953-119">Git 發佈設定完畢後，會建立一個 Git 儲存機制並與您的 Web 應用程式產生關聯。</span><span class="sxs-lookup"><span data-stu-id="a3953-119">Once Git publishing is set up, a Git repository will be created and associated with your web app.</span></span> <span data-ttu-id="a3953-120">hello 儲存機制 URL 將會顯示，而且可以從此以後是使用的 toopush hello 本機開發環境 toohello 雲端的資料。</span><span class="sxs-lookup"><span data-stu-id="a3953-120">hello repository's URL will be displayed and can henceforth be used toopush data from hello local development environment toohello cloud.</span></span> <span data-ttu-id="a3953-121">toopublish 應用程式透過 Git，請確定也會安裝 Git 用戶端，且使用 hello 指示提供 toopush 您 web 應用程式內容 tooAzure 應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="a3953-121">toopublish applications via Git, make sure a Git client is also installed and use hello instructions provided toopush your web app content tooAzure App Service.</span></span>

## <a name="application-overview"></a><span data-ttu-id="a3953-122">應用程式概觀</span><span class="sxs-lookup"><span data-stu-id="a3953-122">Application Overview</span></span>
<span data-ttu-id="a3953-123">在 hello 下一步 區段中，會建立下列檔案的 hello。</span><span class="sxs-lookup"><span data-stu-id="a3953-123">In hello next sections, hello following files are created.</span></span> <span data-ttu-id="a3953-124">它們應該放在 hello hello Git 儲存機制根目錄中。</span><span class="sxs-lookup"><span data-stu-id="a3953-124">They should be placed in hello root of hello Git repository.</span></span>

    app.py
    requirements.txt
    runtime.txt
    web.config
    ptvs_virtualenv_proxy.py


## <a name="wsgi-handler"></a><span data-ttu-id="a3953-125">WSGI 處理常式</span><span class="sxs-lookup"><span data-stu-id="a3953-125">WSGI Handler</span></span>
<span data-ttu-id="a3953-126">WSGI 是所描述的 Python 標準[PEP 3333](http://www.python.org/dev/peps/pep-3333/)定義 hello web 伺服器，並將 Python 之間的介面。</span><span class="sxs-lookup"><span data-stu-id="a3953-126">WSGI is a Python standard described by [PEP 3333](http://www.python.org/dev/peps/pep-3333/) defining an interface between hello web server and Python.</span></span> <span data-ttu-id="a3953-127">此標準為您提供標準化介面，方便您使用 Python 撰寫各種 Web 應用程式與架構。</span><span class="sxs-lookup"><span data-stu-id="a3953-127">It provides a standardized interface for writing various web applications and frameworks using Python.</span></span> <span data-ttu-id="a3953-128">今日熱門的 Python Web 架構都採用 WSGI。</span><span class="sxs-lookup"><span data-stu-id="a3953-128">Popular Python web frameworks today use WSGI.</span></span> <span data-ttu-id="a3953-129">Azure App Service Web 應用程式可讓您支援之任何這類架構。此外，進階的使用者可以甚至編寫自己，只要 hello 自訂處理常式會遵循 hello WSGI 規格指導方針。</span><span class="sxs-lookup"><span data-stu-id="a3953-129">Azure App Service Web Apps gives you support for any such frameworks; in addition, advanced users can even author their own as long as hello custom handler follows hello WSGI specification guidelines.</span></span>

<span data-ttu-id="a3953-130">以下是用於定義自訂處理常式的 `app.py` 範例：</span><span class="sxs-lookup"><span data-stu-id="a3953-130">Here's an example of an `app.py` that defines a custom handler:</span></span>

    def wsgi_app(environ, start_response):
        status = '200 OK'
        response_headers = [('Content-type', 'text/plain')]
        start_response(status, response_headers)
        response_body = 'Hello World'
        yield response_body.encode()

    if __name__ == '__main__':
        from wsgiref.simple_server import make_server

        httpd = make_server('localhost', 5555, wsgi_app)
        httpd.serve_forever()

<span data-ttu-id="a3953-131">您可以執行此應用程式使用在本機`python app.py`，然後瀏覽過`http://localhost:5555`web 瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="a3953-131">You can run this application locally with `python app.py`, then browse too`http://localhost:5555` in your web browser.</span></span>

## <a name="virtual-environment"></a><span data-ttu-id="a3953-132">虛擬環境</span><span class="sxs-lookup"><span data-stu-id="a3953-132">Virtual Environment</span></span>
<span data-ttu-id="a3953-133">雖然上述的 hello 範例應用程式不需要任何外部的封裝，可能是應用程式所需的部分。</span><span class="sxs-lookup"><span data-stu-id="a3953-133">Although hello example app above doesn't require any external packages, it is likely that your application will require some.</span></span>

<span data-ttu-id="a3953-134">toohelp 管理的外部封裝相依性，Azure Git 部署支援虛擬環境的 hello 建立。</span><span class="sxs-lookup"><span data-stu-id="a3953-134">toohelp manage external package dependencies, Azure Git deployment supports hello creation of virtual environments.</span></span>

<span data-ttu-id="a3953-135">當 Azure 偵測 requirements.txt hello hello 儲存機制的根目錄中時，它會自動建立名為在虛擬環境`env`。</span><span class="sxs-lookup"><span data-stu-id="a3953-135">When Azure detects a requirements.txt in hello root of hello repository, it automatically creates a virtual environment named `env`.</span></span> <span data-ttu-id="a3953-136">這只會發生 hello 第一次部署，或在任何部署後 hello 期間所選的 Python 執行階段已變更。</span><span class="sxs-lookup"><span data-stu-id="a3953-136">This only occurs on hello first deployment, or during any deployment after hello selected Python runtime has changed.</span></span>

<span data-ttu-id="a3953-137">您可能會想 toocreate 虛擬環境在本機進行開發，但不將它加入您的 Git 儲存機制中。</span><span class="sxs-lookup"><span data-stu-id="a3953-137">You will probably want toocreate a virtual environment locally for development, but don't include it in your Git repository.</span></span>

## <a name="package-management"></a><span data-ttu-id="a3953-138">封裝管理</span><span class="sxs-lookup"><span data-stu-id="a3953-138">Package Management</span></span>
<span data-ttu-id="a3953-139">Requirements.txt 中列出的套件會使用 pip 的 hello 虛擬環境中自動安裝。</span><span class="sxs-lookup"><span data-stu-id="a3953-139">Packages listed in requirements.txt will be installed automatically in hello virtual environment using pip.</span></span> <span data-ttu-id="a3953-140">這種情況會發生在每個部署，但是如果已安裝封裝，pip 會跳過安裝。</span><span class="sxs-lookup"><span data-stu-id="a3953-140">This happens on every deployment, but pip will skip installation if a package is already installed.</span></span>

<span data-ttu-id="a3953-141">`requirements.txt`範例：</span><span class="sxs-lookup"><span data-stu-id="a3953-141">Example `requirements.txt`:</span></span>

    azure==0.8.4


## <a name="python-version"></a><span data-ttu-id="a3953-142">Python 版本</span><span class="sxs-lookup"><span data-stu-id="a3953-142">Python Version</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

<span data-ttu-id="a3953-143">`runtime.txt`範例：</span><span class="sxs-lookup"><span data-stu-id="a3953-143">Example `runtime.txt`:</span></span>

    python-2.7


## <a name="webconfig"></a><span data-ttu-id="a3953-144">Web.config</span><span class="sxs-lookup"><span data-stu-id="a3953-144">Web.config</span></span>
<span data-ttu-id="a3953-145">您將需要 toocreate web.config 檔案 toospecify hello 伺服器應該如何處理要求。</span><span class="sxs-lookup"><span data-stu-id="a3953-145">You'll need toocreate a web.config file toospecify how hello server should handle requests.</span></span>

<span data-ttu-id="a3953-146">請注意，是否您在您的儲存機制，以便符合 x.y web.x.y.config 檔案 hello 選取 Python 執行階段，則 Azure 會自動複製 hello 適當檔案儲存為 web.config。</span><span class="sxs-lookup"><span data-stu-id="a3953-146">Note that if you have a web.x.y.config file in your repository, where x.y matches hello selected Python runtime, then Azure will automatically copy hello appropriate file as web.config.</span></span>

<span data-ttu-id="a3953-147">hello 下列 web.config 範例依賴 hello 下一節所述的虛擬環境 proxy 指令碼。</span><span class="sxs-lookup"><span data-stu-id="a3953-147">hello following web.config examples rely on a virtual environment proxy script, which is described in hello next section.</span></span>  <span data-ttu-id="a3953-148">它們適用於 hello 範例 hello WSGI 處理常式的`app.py`上方。</span><span class="sxs-lookup"><span data-stu-id="a3953-148">They work with hello WSGI handler used in hello example `app.py` above.</span></span>

<span data-ttu-id="a3953-149">Python 2.7 的 `web.config` 範例：</span><span class="sxs-lookup"><span data-stu-id="a3953-149">Example `web.config` for Python 2.7:</span></span>

    <?xml version="1.0"?>
    <configuration>
      <appSettings>
        <add key="WSGI_ALT_VIRTUALENV_HANDLER" value="app.wsgi_app" />
        <add key="WSGI_ALT_VIRTUALENV_ACTIVATE_THIS"
             value="D:\home\site\wwwroot\env\Scripts\activate_this.py" />
        <add key="WSGI_HANDLER"
             value="ptvs_virtualenv_proxy.get_virtualenv_handler()" />
        <add key="PYTHONPATH" value="D:\home\site\wwwroot" />
      </appSettings>
      <system.web>
        <compilation debug="true" targetFramework="4.0" />
      </system.web>
      <system.webServer>
        <modules runAllManagedModulesForAllRequests="true" />
        <handlers>
          <remove name="Python27_via_FastCGI" />
          <remove name="Python34_via_FastCGI" />
          <add name="Python FastCGI"
               path="handler.fcgi"
               verb="*"
               modules="FastCgiModule"
               scriptProcessor="D:\Python27\python.exe|D:\Python27\Scripts\wfastcgi.py"
               resourceType="Unspecified"
               requireAccess="Script" />
        </handlers>
        <rewrite>
          <rules>
            <rule name="Static Files" stopProcessing="true">
              <conditions>
                <add input="true" pattern="false" />
              </conditions>
            </rule>
            <rule name="Configure Python" stopProcessing="true">
              <match url="(.*)" ignoreCase="false" />
              <conditions>
                <add input="{REQUEST_URI}" pattern="^/static/.*" ignoreCase="true" negate="true" />
              </conditions>
              <action type="Rewrite"
                      url="handler.fcgi/{R:1}"
                      appendQueryString="true" />
            </rule>
          </rules>
        </rewrite>
      </system.webServer>
    </configuration>


<span data-ttu-id="a3953-150">Python 3.4 的 `web.config` 範例：</span><span class="sxs-lookup"><span data-stu-id="a3953-150">Example `web.config` for Python 3.4:</span></span>

    <?xml version="1.0"?>
    <configuration>
      <appSettings>
        <add key="WSGI_ALT_VIRTUALENV_HANDLER" value="app.wsgi_app" />
        <add key="WSGI_ALT_VIRTUALENV_ACTIVATE_THIS"
             value="D:\home\site\wwwroot\env\Scripts\python.exe" />
        <add key="WSGI_HANDLER"
             value="ptvs_virtualenv_proxy.get_venv_handler()" />
        <add key="PYTHONPATH" value="D:\home\site\wwwroot" />
      </appSettings>
      <system.web>
        <compilation debug="true" targetFramework="4.0" />
      </system.web>
      <system.webServer>
        <modules runAllManagedModulesForAllRequests="true" />
        <handlers>
          <remove name="Python27_via_FastCGI" />
          <remove name="Python34_via_FastCGI" />
          <add name="Python FastCGI"
               path="handler.fcgi"
               verb="*"
               modules="FastCgiModule"
               scriptProcessor="D:\Python34\python.exe|D:\Python34\Scripts\wfastcgi.py"
               resourceType="Unspecified"
               requireAccess="Script" />
        </handlers>
        <rewrite>
          <rules>
            <rule name="Static Files" stopProcessing="true">
              <conditions>
                <add input="true" pattern="false" />
              </conditions>
            </rule>
            <rule name="Configure Python" stopProcessing="true">
              <match url="(.*)" ignoreCase="false" />
              <conditions>
                <add input="{REQUEST_URI}" pattern="^/static/.*" ignoreCase="true" negate="true" />
              </conditions>
              <action type="Rewrite" url="handler.fcgi/{R:1}" appendQueryString="true" />
            </rule>
          </rules>
        </rewrite>
      </system.webServer>
    </configuration>


<span data-ttu-id="a3953-151">靜態檔案處理 hello web 伺服器直接管理，而不需要透過 Python 程式碼，以改善效能。</span><span class="sxs-lookup"><span data-stu-id="a3953-151">Static files will be handled by hello web server directly, without going through Python code, for improved performance.</span></span>

<span data-ttu-id="a3953-152">在上述範例 hello，hello 磁碟上的靜態檔案的 hello 位置應符合 hello hello URL 中的位置。</span><span class="sxs-lookup"><span data-stu-id="a3953-152">In hello above examples, hello location of hello static files on disk should match hello location in hello URL.</span></span> <span data-ttu-id="a3953-153">這表示要求`http://pythonapp.azurewebsites.net/static/site.css`做 hello 檔案在磁碟上的`\static\site.css`。</span><span class="sxs-lookup"><span data-stu-id="a3953-153">This means that a request for `http://pythonapp.azurewebsites.net/static/site.css` will serve hello file on disk at `\static\site.css`.</span></span>

<span data-ttu-id="a3953-154">`WSGI_ALT_VIRTUALENV_HANDLER`是您用來指定 hello WSGI 處理常式。</span><span class="sxs-lookup"><span data-stu-id="a3953-154">`WSGI_ALT_VIRTUALENV_HANDLER` is where you specify hello WSGI handler.</span></span> <span data-ttu-id="a3953-155">在 hello 上述範例中，它有`app.wsgi_app`因為 hello 處理常式是名為函式`wsgi_app`中`app.py`hello 根資料夾中。</span><span class="sxs-lookup"><span data-stu-id="a3953-155">In hello above examples, it's `app.wsgi_app` because hello handler is a function named `wsgi_app` in `app.py` in hello root folder.</span></span>

<span data-ttu-id="a3953-156">`PYTHONPATH`您可以自訂，但如果您安裝所有相依性，您可以在 hello 虛擬環境中 requirements.txt 中指定它們，您應該不需要 toochange 它。</span><span class="sxs-lookup"><span data-stu-id="a3953-156">`PYTHONPATH` can be customized, but if you install all your dependencies in hello virtual environment by specifying them in requirements.txt, you shouldn't need toochange it.</span></span>

## <a name="virtual-environment-proxy"></a><span data-ttu-id="a3953-157">虛擬環境 Proxy</span><span class="sxs-lookup"><span data-stu-id="a3953-157">Virtual Environment Proxy</span></span>
<span data-ttu-id="a3953-158">下列指令碼的 hello 使用的 tooretrieve hello WSGI 處理常式，啟動 hello 虛擬環境並記錄錯誤。</span><span class="sxs-lookup"><span data-stu-id="a3953-158">hello following script is used tooretrieve hello WSGI handler, activate hello virtual environment and log errors.</span></span> <span data-ttu-id="a3953-159">設計的 toobe 泛型和已使用不需修改它。</span><span class="sxs-lookup"><span data-stu-id="a3953-159">It is designed toobe generic and used without modifications.</span></span>

<span data-ttu-id="a3953-160">`ptvs_virtualenv_proxy.py`內容：</span><span class="sxs-lookup"><span data-stu-id="a3953-160">Contents of `ptvs_virtualenv_proxy.py`:</span></span>

     # ############################################################################
     #
     # Copyright (c) Microsoft Corporation. 
     #
     # This source code is subject tooterms and conditions of hello Apache License, Version 2.0. A 
     # copy of hello license can be found in hello License.html file at hello root of this distribution. If 
     # you cannot locate hello Apache License, Version 2.0, please send an email too
     # vspython@microsoft.com. By using this source code in any fashion, you are agreeing toobe bound 
     # by hello terms of hello Apache License, Version 2.0.
     #
     # You must not remove this notice, or any other, from this software.
     #
     # ###########################################################################

    import datetime
    import os
    import sys
    import traceback

    if sys.version_info[0] == 3:
        def to_str(value):
            return value.decode(sys.getfilesystemencoding())

        def execfile(path, global_dict):
            """Execute a file"""
            with open(path, 'r') as f:
                code = f.read()
            code = code.replace('\r\n', '\n') + '\n'
            exec(code, global_dict)
    else:
        def to_str(value):
            return value.encode(sys.getfilesystemencoding())

    def log(txt):
        """Logs fatal errors tooa log file if WSGI_LOG env var is defined"""
        log_file = os.environ.get('WSGI_LOG')
        if log_file:
            f = open(log_file, 'a+')
            try:
                f.write('%s: %s' % (datetime.datetime.now(), txt))
            finally:
                f.close()

    ptvsd_secret = os.getenv('WSGI_PTVSD_SECRET')
    if ptvsd_secret:
        log('Enabling ptvsd ...\n')
        try:
            import ptvsd
            try:
                ptvsd.enable_attach(ptvsd_secret)
                log('ptvsd enabled.\n')
            except: 
                log('ptvsd.enable_attach failed\n')
        except ImportError:
            log('error importing ptvsd.\n')

    def get_wsgi_handler(handler_name):
        if not handler_name:
            raise Exception('WSGI_ALT_VIRTUALENV_HANDLER env var must be set')

        if not isinstance(handler_name, str):
            handler_name = to_str(handler_name)

        module_name, _, callable_name = handler_name.rpartition('.')
        should_call = callable_name.endswith('()')
        callable_name = callable_name[:-2] if should_call else callable_name
        name_list = [(callable_name, should_call)]
        handler = None
        last_tb = ''

        while module_name:
            try:
                handler = __import__(module_name, fromlist=[name_list[0][0]])
                last_tb = ''
                for name, should_call in name_list:
                    handler = getattr(handler, name)
                    if should_call:
                        handler = handler()
                break
            except ImportError:
                module_name, _, callable_name = module_name.rpartition('.')
                should_call = callable_name.endswith('()')
                callable_name = callable_name[:-2] if should_call else callable_name
                name_list.insert(0, (callable_name, should_call))
                handler = None
                last_tb = ': ' + traceback.format_exc()

        if handler is None:
            raise ValueError('"%s" could not be imported%s' % (handler_name, last_tb))

        return handler

    activate_this = os.getenv('WSGI_ALT_VIRTUALENV_ACTIVATE_THIS')
    if not activate_this:
        raise Exception('WSGI_ALT_VIRTUALENV_ACTIVATE_THIS is not set')

    def get_virtualenv_handler():
        log('Activating virtualenv with %s\n' % activate_this)
        execfile(activate_this, dict(__file__=activate_this))

        log('Getting handler %s\n' % os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        handler = get_wsgi_handler(os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        log('Got handler: %r\n' % handler)
        return handler

    def get_venv_handler():
        log('Activating venv with executable at %s\n' % activate_this)
        import site
        sys.executable = activate_this
        old_sys_path, sys.path = sys.path, []

        site.main()

        sys.path.insert(0, '')
        for item in old_sys_path:
            if item not in sys.path:
                sys.path.append(item)

        log('Getting handler %s\n' % os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        handler = get_wsgi_handler(os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        log('Got handler: %r\n' % handler)
        return handler


## <a name="customize-git-deployment"></a><span data-ttu-id="a3953-161">自訂 Git 部署</span><span class="sxs-lookup"><span data-stu-id="a3953-161">Customize Git deployment</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-deployment.md)]

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="a3953-162">疑難排解 - 封裝安裝</span><span class="sxs-lookup"><span data-stu-id="a3953-162">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="a3953-163">疑難排解 - 虛擬環境</span><span class="sxs-lookup"><span data-stu-id="a3953-163">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="a3953-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a3953-164">Next steps</span></span>
<span data-ttu-id="a3953-165">如需詳細資訊，請參閱 hello [Python 開發人員中心](/develop/python/)。</span><span class="sxs-lookup"><span data-stu-id="a3953-165">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

> [!NOTE]
> <span data-ttu-id="a3953-166">如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="a3953-166">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="a3953-167">不需要信用卡；沒有承諾。</span><span class="sxs-lookup"><span data-stu-id="a3953-167">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="a3953-168">變更的項目</span><span class="sxs-lookup"><span data-stu-id="a3953-168">What's changed</span></span>
* <span data-ttu-id="a3953-169">從網站 tooApp 服務變更如指南 toohello: [Azure 應用程式服務和其對影響現有的 Azure 服務](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="a3953-169">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

