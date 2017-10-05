---
title: "使用 Azure App Service Web Apps 設定 Python"
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
ms.openlocfilehash: 9683a1af13eeff364d3c4714f0b791324fd82659
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-python-with-azure-app-service-web-apps"></a><span data-ttu-id="6f01c-103">使用 Azure App Service Web Apps 設定 Python</span><span class="sxs-lookup"><span data-stu-id="6f01c-103">Configuring Python with Azure App Service Web Apps</span></span>
<span data-ttu-id="6f01c-104">本教學課程描述在 [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714)上編寫與設定基本的 Web 伺服器閘道介面 (WSGI) 相容之 Python 應用程式的選項。</span><span class="sxs-lookup"><span data-stu-id="6f01c-104">This tutorial describes options for authoring and configuring a basic Web Server Gateway Interface (WSGI) compliant Python application on [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="6f01c-105">它會說明 Git 部署的其他功能，例如虛擬環境和使用 requirements.txt 進行封裝安裝。</span><span class="sxs-lookup"><span data-stu-id="6f01c-105">It describes additional features of Git deployment, such as virtual environment and package installation using requirements.txt.</span></span>

## <a name="bottle-django-or-flask"></a><span data-ttu-id="6f01c-106">Bottle、Django 或 Flask？</span><span class="sxs-lookup"><span data-stu-id="6f01c-106">Bottle, Django or Flask?</span></span>
<span data-ttu-id="6f01c-107">Azure Marketplace 包含 Bottle、Django 和 Flask 架構的範本。</span><span class="sxs-lookup"><span data-stu-id="6f01c-107">The Azure Marketplace contains templates for the Bottle, Django and Flask frameworks.</span></span> <span data-ttu-id="6f01c-108">如果您在 Azure App Service 中開發您的第一個 Web 應用程式，或是您不熟悉 Git，我們建議您遵循這些教學課程，其中包括了在 Windows 或 Mac 使用 Git 部署，從資源庫建置工作應用程式的逐步指示：</span><span class="sxs-lookup"><span data-stu-id="6f01c-108">If you are developing your first web app in Azure App Service, or you are not familiar with Git, we recommend that you follow one of these tutorials, which include step-by-step instructions for building a working application from the gallery using Git deployment from Windows or Mac:</span></span>

* [<span data-ttu-id="6f01c-109">利用 Bottle 建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="6f01c-109">Creating web apps with Bottle</span></span>](web-sites-python-create-deploy-bottle-app.md)
* [<span data-ttu-id="6f01c-110">利用 Django 建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="6f01c-110">Creating web apps with Django</span></span>](web-sites-python-create-deploy-django-app.md)
* [<span data-ttu-id="6f01c-111">利用 Flask 建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="6f01c-111">Creating web apps with Flask</span></span>](web-sites-python-create-deploy-flask-app.md)

## <a name="web-app-creation-on-azure-portal"></a><span data-ttu-id="6f01c-112">在 Azure 入口網站上建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="6f01c-112">Web app creation on Azure Portal</span></span>
<span data-ttu-id="6f01c-113">本教學課程假設定有現有的 Azure 訂用帳戶，而且能夠存取 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="6f01c-113">This tutorial assumes an existing Azure subscription and access to the Azure Portal.</span></span>

<span data-ttu-id="6f01c-114">如果您還沒有 Web 應用程式，則可以從 [Azure 入口網站](https://portal.azure.com)建立。</span><span class="sxs-lookup"><span data-stu-id="6f01c-114">If you do not have an existing web app, you can create one from the [Azure Portal](https://portal.azure.com).</span></span>  <span data-ttu-id="6f01c-115">按一下左上角的 [新增] 按鈕，然後按一下 [Web + 行動] > [Web 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="6f01c-115">Click the NEW button in the top left corner, then click **Web + Mobile** > **Web app**.</span></span>

## <a name="git-publishing"></a><span data-ttu-id="6f01c-116">Git 發行</span><span class="sxs-lookup"><span data-stu-id="6f01c-116">Git Publishing</span></span>
<span data-ttu-id="6f01c-117">依照 [本機 Git 部署至 Azure App Service](app-service-deploy-local-git.md)的指示，為您新建立的 Web 應用程式設定 Git 發佈功能。</span><span class="sxs-lookup"><span data-stu-id="6f01c-117">Configure Git publishing for your newly created web app by following the instructions at [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span> <span data-ttu-id="6f01c-118">本教學課程將使用 Git 來建立、管理並將您的 Python Web 應用程式發佈至 Azure App Service。</span><span class="sxs-lookup"><span data-stu-id="6f01c-118">This tutorial uses Git to create, manage, and publish our Python web app to Azure App Service.</span></span>

<span data-ttu-id="6f01c-119">Git 發佈設定完畢後，會建立一個 Git 儲存機制並與您的 Web 應用程式產生關聯。</span><span class="sxs-lookup"><span data-stu-id="6f01c-119">Once Git publishing is set up, a Git repository will be created and associated with your web app.</span></span> <span data-ttu-id="6f01c-120">該儲存機制的 URL 會加以顯示，方便您將資料從本機開發環境推送到雲端。</span><span class="sxs-lookup"><span data-stu-id="6f01c-120">The repository's URL will be displayed and can henceforth be used to push data from the local development environment to the cloud.</span></span> <span data-ttu-id="6f01c-121">若要透過 Git 發佈應用程式，請確保同時安裝了 Git 用戶端，並遵守提供的指示將您的 Web 應用程式內容推送到 Azure App Service。</span><span class="sxs-lookup"><span data-stu-id="6f01c-121">To publish applications via Git, make sure a Git client is also installed and use the instructions provided to push your web app content to Azure App Service.</span></span>

## <a name="application-overview"></a><span data-ttu-id="6f01c-122">應用程式概觀</span><span class="sxs-lookup"><span data-stu-id="6f01c-122">Application Overview</span></span>
<span data-ttu-id="6f01c-123">在後續章節中，會建立下列檔案。</span><span class="sxs-lookup"><span data-stu-id="6f01c-123">In the next sections, the following files are created.</span></span> <span data-ttu-id="6f01c-124">它們應該放在 Git 儲存機制的根目錄中。</span><span class="sxs-lookup"><span data-stu-id="6f01c-124">They should be placed in the root of the Git repository.</span></span>

    app.py
    requirements.txt
    runtime.txt
    web.config
    ptvs_virtualenv_proxy.py


## <a name="wsgi-handler"></a><span data-ttu-id="6f01c-125">WSGI 處理常式</span><span class="sxs-lookup"><span data-stu-id="6f01c-125">WSGI Handler</span></span>
<span data-ttu-id="6f01c-126">WSGI 是由 [PEP 3333](http://www.python.org/dev/peps/pep-3333/) 描述的一項 Python 標準，此標準定義了 Web 伺服器與 Python 之間的介面。</span><span class="sxs-lookup"><span data-stu-id="6f01c-126">WSGI is a Python standard described by [PEP 3333](http://www.python.org/dev/peps/pep-3333/) defining an interface between the web server and Python.</span></span> <span data-ttu-id="6f01c-127">此標準為您提供標準化介面，方便您使用 Python 撰寫各種 Web 應用程式與架構。</span><span class="sxs-lookup"><span data-stu-id="6f01c-127">It provides a standardized interface for writing various web applications and frameworks using Python.</span></span> <span data-ttu-id="6f01c-128">今日熱門的 Python Web 架構都採用 WSGI。</span><span class="sxs-lookup"><span data-stu-id="6f01c-128">Popular Python web frameworks today use WSGI.</span></span> <span data-ttu-id="6f01c-129">Azure App Service Web Apps 針對此類任何架構提供支援，而進階使用者甚至可以撰寫自己的架構，但前提是自訂處理常式必須遵守 WSGI 規範指示。</span><span class="sxs-lookup"><span data-stu-id="6f01c-129">Azure App Service Web Apps gives you support for any such frameworks; in addition, advanced users can even author their own as long as the custom handler follows the WSGI specification guidelines.</span></span>

<span data-ttu-id="6f01c-130">以下是用於定義自訂處理常式的 `app.py` 範例：</span><span class="sxs-lookup"><span data-stu-id="6f01c-130">Here's an example of an `app.py` that defines a custom handler:</span></span>

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

<span data-ttu-id="6f01c-131">您可以搭配 `python app.py` 在本機執行此應用程式，然後在您的網頁瀏覽器中瀏覽到 `http://localhost:5555`。</span><span class="sxs-lookup"><span data-stu-id="6f01c-131">You can run this application locally with `python app.py`, then browse to `http://localhost:5555` in your web browser.</span></span>

## <a name="virtual-environment"></a><span data-ttu-id="6f01c-132">虛擬環境</span><span class="sxs-lookup"><span data-stu-id="6f01c-132">Virtual Environment</span></span>
<span data-ttu-id="6f01c-133">雖然上述範例應用程式不需要任何外部的封裝，但您的應用程式可能需要。</span><span class="sxs-lookup"><span data-stu-id="6f01c-133">Although the example app above doesn't require any external packages, it is likely that your application will require some.</span></span>

<span data-ttu-id="6f01c-134">為了協助管理外部的封裝相依性，Azure Git 部署支援虛擬環境的建立。</span><span class="sxs-lookup"><span data-stu-id="6f01c-134">To help manage external package dependencies, Azure Git deployment supports the creation of virtual environments.</span></span>

<span data-ttu-id="6f01c-135">當 Azure 偵測到儲存機制根目錄中的 requirements.txt 時，會自動建立名為 `env`的虛擬環境。</span><span class="sxs-lookup"><span data-stu-id="6f01c-135">When Azure detects a requirements.txt in the root of the repository, it automatically creates a virtual environment named `env`.</span></span> <span data-ttu-id="6f01c-136">這只會發生在第一次部署，或是選取之 Python 執行階段變更之後的任何部署期間。</span><span class="sxs-lookup"><span data-stu-id="6f01c-136">This only occurs on the first deployment, or during any deployment after the selected Python runtime has changed.</span></span>

<span data-ttu-id="6f01c-137">您可能想要在本機建立虛擬環境以進行開發，但是請勿將它包含在 Git 儲存機制中。</span><span class="sxs-lookup"><span data-stu-id="6f01c-137">You will probably want to create a virtual environment locally for development, but don't include it in your Git repository.</span></span>

## <a name="package-management"></a><span data-ttu-id="6f01c-138">封裝管理</span><span class="sxs-lookup"><span data-stu-id="6f01c-138">Package Management</span></span>
<span data-ttu-id="6f01c-139">Requirements.txt 中所列封裝，將會使用 pip 自動安裝於虛擬環境中。</span><span class="sxs-lookup"><span data-stu-id="6f01c-139">Packages listed in requirements.txt will be installed automatically in the virtual environment using pip.</span></span> <span data-ttu-id="6f01c-140">這種情況會發生在每個部署，但是如果已安裝封裝，pip 會跳過安裝。</span><span class="sxs-lookup"><span data-stu-id="6f01c-140">This happens on every deployment, but pip will skip installation if a package is already installed.</span></span>

<span data-ttu-id="6f01c-141">`requirements.txt`範例：</span><span class="sxs-lookup"><span data-stu-id="6f01c-141">Example `requirements.txt`:</span></span>

    azure==0.8.4


## <a name="python-version"></a><span data-ttu-id="6f01c-142">Python 版本</span><span class="sxs-lookup"><span data-stu-id="6f01c-142">Python Version</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

<span data-ttu-id="6f01c-143">`runtime.txt`範例：</span><span class="sxs-lookup"><span data-stu-id="6f01c-143">Example `runtime.txt`:</span></span>

    python-2.7


## <a name="webconfig"></a><span data-ttu-id="6f01c-144">Web.config</span><span class="sxs-lookup"><span data-stu-id="6f01c-144">Web.config</span></span>
<span data-ttu-id="6f01c-145">您需要建立 web.config 檔來指定伺服器應該如何處理要求。</span><span class="sxs-lookup"><span data-stu-id="6f01c-145">You'll need to create a web.config file to specify how the server should handle requests.</span></span>

<span data-ttu-id="6f01c-146">請注意，如果您在儲存機制中有 web.x.y. 組態檔，其中 x.y 符合所選的 Python 執行階段，則 Azure 會自動複製適當的檔案，做為 web.config。</span><span class="sxs-lookup"><span data-stu-id="6f01c-146">Note that if you have a web.x.y.config file in your repository, where x.y matches the selected Python runtime, then Azure will automatically copy the appropriate file as web.config.</span></span>

<span data-ttu-id="6f01c-147">下列 web.config 範例仰賴虛擬環境 Proxy 指令碼，於下一節中說明。</span><span class="sxs-lookup"><span data-stu-id="6f01c-147">The following web.config examples rely on a virtual environment proxy script, which is described in the next section.</span></span>  <span data-ttu-id="6f01c-148">其會使用上述範例 `app.py` 中所使用之 WSGI 處理常式。</span><span class="sxs-lookup"><span data-stu-id="6f01c-148">They work with the WSGI handler used in the example `app.py` above.</span></span>

<span data-ttu-id="6f01c-149">Python 2.7 的 `web.config` 範例：</span><span class="sxs-lookup"><span data-stu-id="6f01c-149">Example `web.config` for Python 2.7:</span></span>

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


<span data-ttu-id="6f01c-150">Python 3.4 的 `web.config` 範例：</span><span class="sxs-lookup"><span data-stu-id="6f01c-150">Example `web.config` for Python 3.4:</span></span>

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


<span data-ttu-id="6f01c-151">靜態檔案交由 Web 伺服器直接處理，而不會通過 Python 程式碼，以改善效能。</span><span class="sxs-lookup"><span data-stu-id="6f01c-151">Static files will be handled by the web server directly, without going through Python code, for improved performance.</span></span>

<span data-ttu-id="6f01c-152">在上述範例中，磁碟上靜態檔案的位置應該符合在 URL 中的位置。</span><span class="sxs-lookup"><span data-stu-id="6f01c-152">In the above examples, the location of the static files on disk should match the location in the URL.</span></span> <span data-ttu-id="6f01c-153">這表示 `http://pythonapp.azurewebsites.net/static/site.css` 要求將於 `\static\site.css` 提供磁碟上的檔案。</span><span class="sxs-lookup"><span data-stu-id="6f01c-153">This means that a request for `http://pythonapp.azurewebsites.net/static/site.css` will serve the file on disk at `\static\site.css`.</span></span>

<span data-ttu-id="6f01c-154">`WSGI_ALT_VIRTUALENV_HANDLER` 是您指定 WSGI 處理常式的地方。</span><span class="sxs-lookup"><span data-stu-id="6f01c-154">`WSGI_ALT_VIRTUALENV_HANDLER` is where you specify the WSGI handler.</span></span> <span data-ttu-id="6f01c-155">在上述範例中，為 `app.wsgi_app` 因為處理常式是根資料夾中 `app.py` 內名為 `wsgi_app` 的函式。</span><span class="sxs-lookup"><span data-stu-id="6f01c-155">In the above examples, it's `app.wsgi_app` because the handler is a function named `wsgi_app` in `app.py` in the root folder.</span></span>

<span data-ttu-id="6f01c-156">`PYTHONPATH` 可自訂，但是如果您藉由在 requirements.txt 中指定相依性，將其全部安裝於虛擬環境中，您應該不需要變更。</span><span class="sxs-lookup"><span data-stu-id="6f01c-156">`PYTHONPATH` can be customized, but if you install all your dependencies in the virtual environment by specifying them in requirements.txt, you shouldn't need to change it.</span></span>

## <a name="virtual-environment-proxy"></a><span data-ttu-id="6f01c-157">虛擬環境 Proxy</span><span class="sxs-lookup"><span data-stu-id="6f01c-157">Virtual Environment Proxy</span></span>
<span data-ttu-id="6f01c-158">下列指令碼用來擷取 WSGI 處理常式，會啟動虛擬環境並記錄錯誤。</span><span class="sxs-lookup"><span data-stu-id="6f01c-158">The following script is used to retrieve the WSGI handler, activate the virtual environment and log errors.</span></span> <span data-ttu-id="6f01c-159">它已設計為 Generic，不需修改就可使用。</span><span class="sxs-lookup"><span data-stu-id="6f01c-159">It is designed to be generic and used without modifications.</span></span>

<span data-ttu-id="6f01c-160">`ptvs_virtualenv_proxy.py`內容：</span><span class="sxs-lookup"><span data-stu-id="6f01c-160">Contents of `ptvs_virtualenv_proxy.py`:</span></span>

     # ############################################################################
     #
     # Copyright (c) Microsoft Corporation. 
     #
     # This source code is subject to terms and conditions of the Apache License, Version 2.0. A 
     # copy of the license can be found in the License.html file at the root of this distribution. If 
     # you cannot locate the Apache License, Version 2.0, please send an email to 
     # vspython@microsoft.com. By using this source code in any fashion, you are agreeing to be bound 
     # by the terms of the Apache License, Version 2.0.
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
        """Logs fatal errors to a log file if WSGI_LOG env var is defined"""
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


## <a name="customize-git-deployment"></a><span data-ttu-id="6f01c-161">自訂 Git 部署</span><span class="sxs-lookup"><span data-stu-id="6f01c-161">Customize Git deployment</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-deployment.md)]

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="6f01c-162">疑難排解 - 封裝安裝</span><span class="sxs-lookup"><span data-stu-id="6f01c-162">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="6f01c-163">疑難排解 - 虛擬環境</span><span class="sxs-lookup"><span data-stu-id="6f01c-163">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="6f01c-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6f01c-164">Next steps</span></span>
<span data-ttu-id="6f01c-165">如需詳細資訊，請參閱 [Python 開發人員中心](/develop/python/)。</span><span class="sxs-lookup"><span data-stu-id="6f01c-165">For more information, see the [Python Developer Center](/develop/python/).</span></span>

> [!NOTE]
> <span data-ttu-id="6f01c-166">如果您想在註冊 Azure 帳戶前開始使用 Azure App Service，請移至 [試用 App Service](https://azure.microsoft.com/try/app-service/)，即可在 App Service 中立即建立短期入門 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6f01c-166">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="6f01c-167">不需要信用卡；沒有承諾。</span><span class="sxs-lookup"><span data-stu-id="6f01c-167">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="6f01c-168">變更的項目</span><span class="sxs-lookup"><span data-stu-id="6f01c-168">What's changed</span></span>
* <span data-ttu-id="6f01c-169">如需從網站變更為 App Service 的指南，請參閱： [Azure App Service 及其對現有 Azure 服務的影響](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="6f01c-169">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

