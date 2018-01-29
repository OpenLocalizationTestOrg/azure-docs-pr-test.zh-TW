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
ms.openlocfilehash: 86e19d5bb942937779665eb60d9dc0654c16747d
ms.sourcegitcommit: bc8d39fa83b3c4a66457fba007d215bccd8be985
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/10/2017
---
# <a name="configuring-python-with-azure-app-service-web-apps"></a>使用 Azure App Service Web Apps 設定 Python
本教學課程描述在 [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714)上編寫與設定基本的 Web 伺服器閘道介面 (WSGI) 相容之 Python 應用程式的選項。

它會說明 Git 部署的其他功能，例如虛擬環境和使用 requirements.txt 進行封裝安裝。

## <a name="bottle-django-or-flask"></a>Bottle、Django 或 Flask？
Azure Marketplace 包含 Bottle、Django 和 Flask 架構的範本。 如果您正在開發 Azure App Service 中的第一個 Web 應用程式，您可以從 Azure 入口網站快速地建立一個應用程式：

* [利用 Bottle 建立 Web 應用程式](https://portal.azure.com/#create/PTVS.Bottle)
* [利用 Django 建立 Web 應用程式](https://portal.azure.com/#create/PTVS.Django)
* [利用 Flask 建立 Web 應用程式](https://portal.azure.com/#create/PTVS.Flask)

## <a name="web-app-creation-on-azure-portal"></a>在 Azure 入口網站上建立 Web 應用程式
本教學課程假設有現有的 Azure 訂用帳戶，而且能夠存取 Azure 入口網站。

如果您還沒有 Web 應用程式，則可以從 [Azure 入口網站](https://portal.azure.com)建立。  按一下左上角的 [新增] 按鈕，然後按一下 [Web + 行動] > [Web 應用程式]。

## <a name="git-publishing"></a>Git 發行
依照 [本機 Git 部署至 Azure App Service](app-service-deploy-local-git.md)的指示，為您新建立的 Web 應用程式設定 Git 發佈功能。 本教學課程使用 Git 來建立、管理並將您的 Python Web 應用程式發佈至 Azure App Service。

Git 發佈設定完畢後，會建立一個 Git 存放庫並與您的 Web 應用程式產生關聯。 隨即顯示該存放庫的 URL，並且可用於將資料從本機開發環境推送到雲端。 若要透過 Git 發佈應用程式，請確保同時安裝了 Git 用戶端，並遵守提供的指示將您的 Web 應用程式內容推送到 Azure App Service。

## <a name="application-overview"></a>應用程式概觀
在後續章節中，會建立下列檔案。 它們應該放在 Git 儲存機制的根目錄中。

    app.py
    requirements.txt
    runtime.txt
    web.config
    ptvs_virtualenv_proxy.py


## <a name="wsgi-handler"></a>WSGI 處理常式
WSGI 是由 [PEP 3333](http://www.python.org/dev/peps/pep-3333/) 描述的一項 Python 標準，此標準定義了 Web 伺服器與 Python 之間的介面。 此標準為您提供標準化介面，方便您使用 Python 撰寫各種 Web 應用程式與架構。 今日熱門的 Python Web 架構都採用 WSGI。 Azure App Service Web Apps 針對此類任何架構提供支援，而進階使用者甚至可以撰寫自己的架構，但前提是自訂處理常式必須遵守 WSGI 規範指示。

以下是用於定義自訂處理常式的 `app.py` 範例：

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

您可以搭配 `python app.py` 在本機執行此應用程式，然後在您的網頁瀏覽器中瀏覽到 `http://localhost:5555`。

## <a name="virtual-environment"></a>虛擬環境
雖然上述範例應用程式不需要任何外部封裝，但您的應用程式可能需要。

為了協助管理外部的封裝相依性，Azure Git 部署支援虛擬環境的建立。

當 Azure 偵測到儲存機制根目錄中的 requirements.txt 時，會自動建立名為 `env`的虛擬環境。 這只會發生在第一次部署，或是選取之 Python 執行階段變更之後的任何部署期間。

您可能想要在本機建立虛擬環境以進行開發，但是請勿將它包含在 Git 存放庫中。

## <a name="package-management"></a>封裝管理
Requirements.txt 中所列的封裝會使用 pip 自動安裝於虛擬環境中。 這種情況會發生在每個部署，但是如果已安裝封裝，pip 會跳過安裝。

`requirements.txt`範例：

    azure==0.8.4


## <a name="python-version"></a>Python 版本
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

`runtime.txt`範例：

    python-2.7


## <a name="webconfig"></a>Web.config
您需要建立 web.config 檔來指定伺服器應該如何處理要求。

如果您在存放庫中有 web.x.y. 組態檔，其中 x.y 符合所選的 Python 執行階段，則 Azure 會自動複製適當的檔案，做為 web.config。

下列 web.config 範例仰賴虛擬環境 Proxy 指令碼，於下一節中說明。  其會使用上述範例 `app.py` 中所使用之 WSGI 處理常式。

Python 2.7 的 `web.config` 範例：

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


Python 3.4 的 `web.config` 範例：

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


靜態檔案交由 Web 伺服器直接處理，而不會通過 Python 程式碼，以改善效能。

在上述範例中，磁碟上靜態檔案的位置應該符合在 URL 中的位置。 這表示 `http://pythonapp.azurewebsites.net/static/site.css` 要求將於 `\static\site.css` 提供磁碟上的檔案。

`WSGI_ALT_VIRTUALENV_HANDLER` 是您指定 WSGI 處理常式的地方。 在上述範例中為 `app.wsgi_app`，因為處理常式是根資料夾中 `app.py` 內名為 `wsgi_app` 的函式。

`PYTHONPATH` 可自訂，但是如果您藉由在 requirements.txt 中指定相依性，將其全部安裝於虛擬環境中，您應該不需要變更。

## <a name="virtual-environment-proxy"></a>虛擬環境 Proxy
下列指令碼用來擷取 WSGI 處理常式，會啟動虛擬環境並記錄錯誤。 它已設計為 Generic，不需修改就可使用。

`ptvs_virtualenv_proxy.py`內容：

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


## <a name="customize-git-deployment"></a>自訂 Git 部署
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-deployment.md)]

## <a name="troubleshooting---package-installation"></a>疑難排解 - 封裝安裝
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a>疑難排解 - 虛擬環境
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a>後續步驟
如需詳細資訊，請參閱 [Python 開發人員中心](/develop/python/)。

> [!NOTE]
> 如果您想在註冊 Azure 帳戶前開始使用 Azure App Service，請移至 [試用 App Service](https://azure.microsoft.com/try/app-service/)，即可在 App Service 中立即建立短期入門 Web 應用程式。 不需要信用卡；沒有承諾。
> 
> 
