---
title: "Windows Server 的 Azure VM 上 aaaDjango web 應用程式 |Microsoft 文件"
description: "深入了解如何 toohost Django 為基礎的網站與 hello 傳統部署模型中使用 Windows Server 2012 R2 Datacenter VM 在 Azure 中。"
services: virtual-machines-windows
documentationcenter: python
author: huguesv
manager: wpickett
editor: 
tags: azure-service-management
ms.assetid: e36484d1-afbf-47f5-b755-5e65397dc1c3
ms.service: virtual-machines-windows
ms.workload: web
ms.tgt_pltfrm: vm-windows
ms.devlang: python
ms.topic: article
ms.date: 05/31/2017
ms.author: huvalo
ms.openlocfilehash: 55847e3c6d6769965be29077e8d4eeebad914637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="django-hello-world-web-app-on-a-windows-server-vm"></a>Windows Server VM 上的 Django Hello World Web 應用程式

> [!IMPORTANT] 
> Azure 有用於建立和使用資源的兩個不同的部署模型： [Azure 資源管理員和 hello 傳統部署模型](../../../resource-manager-deployment-model.md)。 本文說明 hello 傳統部署模型。 建議最新的部署使用 hello 資源管理員的模型。

本教學課程示範如何 toohost Django 為基礎的網站在 Azure 虛擬機器中的 Windows Server 中。 在 hello 教學課程中，我們會假設沒有與 Azure 的使用經驗。 當您完成 hello 教學課程時，您可以如 Django 架構應用程式註冊以及 hello 雲端中執行。

了解如何：

* 設定 Azure 虛擬機器 toohost Django。 雖然本教學課程說明如何 toodo 此作業對於**Windows Server**，您可以在 Azure 中裝載的 Linux VM 的 hello 相同。
* 在 Windows 中建立新的 Django 應用程式。

hello 教學課程會示範如何 toobuild 基本的 Hello World web 應用程式。 hello 應用程式裝載於 Azure 虛擬機器。

下列螢幕擷取畫面的 hello 顯示 hello 完成應用程式：

![在瀏覽器視窗會顯示在 Azure 中的 hello hello world 網頁][1]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a>建立並設定 Azure 虛擬機器 toohost Django

1. toocreate Azure 虛擬機器以 hello Windows Server 2012 R2 Datacenter 分佈，請參閱[建立執行 Windows hello Azure 入口網站中的虛擬機器](tutorial.md)。
2. 從 hello web tooport 80 hello 虛擬機器上設定 Azure toodirect 連接埠 80 的流量：
   
   1. 在 hello Azure 入口網站，移 toohello 儀表板，然後選取您新建立的虛擬機器。
   2. 選取 端點，然後按一下新增。

     ![新增端點。](./media/python-django-web-app/django-helloworld-add-endpoint-new-portal.png)

   3. 在 hello**加入端點** 頁面上，針對**名稱**，輸入**HTTP**。 設定 hello 公用和私人 TCP 連接埠太**80**。

     ![輸入名稱並設定公用和私人連接埠](./media/python-django-web-app/django-helloworld-add-endpoint-set-ports-new-portal.png)

   4. 按一下 [確定] 。
     
3. Hello 儀表板 中，選取您的 VM。 按一下 toouse 遠端桌面通訊協定 (RDP) tooremotely 登入新建立的 Azure 虛擬機器，toohello**連接**。  

> [!IMPORTANT] 
> hello 下列指示假設您正確簽署 toohello 虛擬機器中。 它們也假設您要發出 hello 虛擬機器中，而不是在本機電腦的命令。

## <a id="setup"> </a>安裝 Python、Django 和 WFastCGI
> [!NOTE]
> 使用 Internet Explorer toodownload，您可能必須 tooconfigure Internet Explorer**增強式安全性設定**設定。 toodo 此，依序按一下**啟動** > **系統管理工具** > **伺服器管理員** > **本機伺服器**. 按一下 [IE 增強式安全性設定]，然後選取 [關閉]。

1. 安裝 hello 最新版本的 Python 2.7 或從 Python 3.4 [python.org][python.org]。
2. 安裝使用 pip 的 hello wfastcgi 和 django 封裝。
   
    使用 Python 2.7 hello 下列命令：
   
        c:\python27\scripts\pip install wfastcgi
        c:\python27\scripts\pip install django
   
    使用 Python 3.4 hello 下列命令：
   
        c:\python34\scripts\pip install wfastcgi
        c:\python34\scripts\pip install django

## <a name="install-iis-with-fastcgi"></a>安裝含 FastCGI 的 IIS
* 使用 FastCGI 支援安裝 Internet Information Services (IIS)。 這可能需要幾分鐘的時間 tooexecute。
   
        start /wait %windir%\System32\PkgMgr.exe /iu:IIS-WebServerRole;IIS-WebServer;IIS-CommonHttpFeatures;IIS-StaticContent;IIS-DefaultDocument;IIS-DirectoryBrowsing;IIS-HttpErrors;IIS-HealthAndDiagnostics;IIS-HttpLogging;IIS-LoggingLibraries;IIS-RequestMonitor;IIS-Security;IIS-RequestFiltering;IIS-HttpCompressionStatic;IIS-WebServerManagementTools;IIS-ManagementConsole;WAS-WindowsActivationService;WAS-ProcessModel;WAS-NetFxEnvironment;WAS-ConfigurationAPI;IIS-CGI

## <a name="create-a-new-django-application"></a>建立新的 Django 應用程式
1. 在 C:\inetpub\wwwroot，toocreate 新 Django 專案中，輸入下列命令的 hello:
   
   使用 Python 2.7 hello 下列命令：
   
       C:\Python27\Scripts\django-admin.exe startproject helloworld
   
   使用 Python 3.4 hello 下列命令：
   
       C:\Python34\Scripts\django-admin.exe startproject helloworld
   
   ![hello hello 新 AzureService 命令結果](./media/python-django-web-app/django-helloworld-cmd-new-azure-service.png)
2. hello`django-admin`命令會產生如 Django 架構網站的基本結構：
   
   * `helloworld\manage.py` 可協助您開始裝載及停止裝載以 Django 作為基礎的網站。
   * `helloworld\helloworld\settings.py` 具有您應用程式的 Django 設定。
   * `helloworld\helloworld\urls.py`具有 hello 每個 URL 和它的檢視之間的對應程式碼。
3. 在 hello C:\inetpub\wwwroot\helloworld\helloworld 目錄中，建立名為 views.py 新檔案。 此檔案具有 hello 檢視呈現 hello"hello world"的頁面。 在程式碼編輯器中，輸入下列命令的 hello:
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. 取代下列命令的 hello hello hello urls.py 檔案內容：
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-iis"></a>設定 IIS
1. 在 hello 全域 applicationhost.config 檔案中，解除鎖定 hello 處理常式區段。  這可讓您 web.config 檔案 toouse hello Python 的處理常式。 新增這個命令：
   
        %windir%\system32\inetsrv\appcmd unlock config -section:system.webServer/handlers
2. 啟動 WFastCGI。 這樣會加入應用程式 toohello 全域 applicationhost.config 檔，它會參考 tooyour Python 解譯器可執行檔和 hello wfastcgi.py 指令碼。
   
    在 Python 2.7 中：
   
        C:\python27\scripts\wfastcgi-enable
   
    在 Python 3.4 中：
   
        C:\python34\scripts\wfastcgi-enable
3. 在 C:\inetpub\wwwroot\helloworld 中建立 web.config 檔案。 hello 值 hello`scriptProcessor`屬性應該符合 hello hello 前面步驟的輸出。 如需 hello wfastcgi 設定的詳細資訊，請參閱[pypi wfastcgi][wfastcgi]。
   
   在 Python 2.7 中：
   
        <configuration>
          <appSettings>
            <add key="WSGI_HANDLER" value="django.core.handlers.wsgi.WSGIHandler()" />
            <add key="PYTHONPATH" value="C:\inetpub\wwwroot\helloworld" />
            <add key="DJANGO_SETTINGS_MODULE" value="helloworld.settings" />
          </appSettings>
          <system.webServer>
            <handlers>
                <add name="Python FastCGI" path="*" verb="*" modules="FastCgiModule" scriptProcessor="C:\Python27\python.exe|C:\Python27\Lib\site-packages\wfastcgi.pyc" resourceType="Unspecified" />
            </handlers>
          </system.webServer>
        </configuration>
   
   在 Python 3.4 中：
   
        <configuration>
          <appSettings>
            <add key="WSGI_HANDLER" value="django.core.handlers.wsgi.WSGIHandler()" />
            <add key="PYTHONPATH" value="C:\inetpub\wwwroot\helloworld" />
            <add key="DJANGO_SETTINGS_MODULE" value="helloworld.settings" />
          </appSettings>
          <system.webServer>
            <handlers>
                <add name="Python FastCGI" path="*" verb="*" modules="FastCgiModule" scriptProcessor="C:\Python34\python.exe|C:\Python34\Lib\site-packages\wfastcgi.py" resourceType="Unspecified" />
            </handlers>
          </system.webServer>
        </configuration>
4. 更新 hello hello IIS 預設網站 toopoint toohello Django 專案資料夾的位置：
   
        %windir%\system32\inetsrv\appcmd set vdir "Default Web Site/" -physicalPath:"C:\inetpub\wwwroot\helloworld"
5. 載入 hello 網頁瀏覽器中。

![在瀏覽器視窗會顯示在 Azure 上的 hello hello world 網頁][1]

## <a name="shut-down-your-azure-virtual-machine"></a>關閉 Azure 虛擬機器
當您完成本教學課程中時，我們建議您關閉或移除 hello hello 教學課程中建立的 Azure VM。 這樣可為其他教學課程釋放資源，您也可以避免產生 Azure 使用量費用。

[1]: ./media/python-django-web-app/django-helloworld-browser-azure.png

[port80]: ./media/python-django-web-app/django-helloworld-port80.png

[Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[python.org]: https://www.python.org/downloads/
[wfastcgi]: https://pypi.python.org/pypi/wfastcgi
