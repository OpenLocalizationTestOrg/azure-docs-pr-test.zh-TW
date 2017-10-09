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
# <a name="django-hello-world-web-app-on-a-windows-server-vm"></a><span data-ttu-id="01679-103">Windows Server VM 上的 Django Hello World Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="01679-103">Django Hello World web app on a Windows Server VM</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="01679-104">Azure 有用於建立和使用資源的兩個不同的部署模型： [Azure 資源管理員和 hello 傳統部署模型](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="01679-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and hello classic deployment model](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="01679-105">本文說明 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="01679-105">This article describes hello classic deployment model.</span></span> <span data-ttu-id="01679-106">建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="01679-106">We recommend that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="01679-107">本教學課程示範如何 toohost Django 為基礎的網站在 Azure 虛擬機器中的 Windows Server 中。</span><span class="sxs-lookup"><span data-stu-id="01679-107">This tutorial shows you how toohost a Django-based website in Windows Server in Azure Virtual Machines.</span></span> <span data-ttu-id="01679-108">在 hello 教學課程中，我們會假設沒有與 Azure 的使用經驗。</span><span class="sxs-lookup"><span data-stu-id="01679-108">In hello tutorial, we assume no prior experience with Azure.</span></span> <span data-ttu-id="01679-109">當您完成 hello 教學課程時，您可以如 Django 架構應用程式註冊以及 hello 雲端中執行。</span><span class="sxs-lookup"><span data-stu-id="01679-109">When you finish hello tutorial, you can have a Django-based application up and running in hello cloud.</span></span>

<span data-ttu-id="01679-110">了解如何：</span><span class="sxs-lookup"><span data-stu-id="01679-110">Learn how to:</span></span>

* <span data-ttu-id="01679-111">設定 Azure 虛擬機器 toohost Django。</span><span class="sxs-lookup"><span data-stu-id="01679-111">Set up an Azure virtual machine toohost Django.</span></span> <span data-ttu-id="01679-112">雖然本教學課程說明如何 toodo 此作業對於**Windows Server**，您可以在 Azure 中裝載的 Linux VM 的 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="01679-112">Although this tutorial explains how toodo this for **Windows Server**, you can do hello same for a Linux VM hosted in Azure.</span></span>
* <span data-ttu-id="01679-113">在 Windows 中建立新的 Django 應用程式。</span><span class="sxs-lookup"><span data-stu-id="01679-113">Create a new Django application in Windows.</span></span>

<span data-ttu-id="01679-114">hello 教學課程會示範如何 toobuild 基本的 Hello World web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="01679-114">hello tutorial shows you how toobuild a basic Hello World web application.</span></span> <span data-ttu-id="01679-115">hello 應用程式裝載於 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="01679-115">hello application is hosted in an Azure virtual machine.</span></span>

<span data-ttu-id="01679-116">下列螢幕擷取畫面的 hello 顯示 hello 完成應用程式：</span><span class="sxs-lookup"><span data-stu-id="01679-116">hello following screenshot shows hello completed application:</span></span>

![在瀏覽器視窗會顯示在 Azure 中的 hello hello world 網頁][1]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a><span data-ttu-id="01679-118">建立並設定 Azure 虛擬機器 toohost Django</span><span class="sxs-lookup"><span data-stu-id="01679-118">Create and set up an Azure virtual machine toohost Django</span></span>

1. <span data-ttu-id="01679-119">toocreate Azure 虛擬機器以 hello Windows Server 2012 R2 Datacenter 分佈，請參閱[建立執行 Windows hello Azure 入口網站中的虛擬機器](tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="01679-119">toocreate an Azure virtual machine with hello Windows Server 2012 R2 Datacenter distribution, see [Create a virtual machine running Windows in hello Azure portal](tutorial.md).</span></span>
2. <span data-ttu-id="01679-120">從 hello web tooport 80 hello 虛擬機器上設定 Azure toodirect 連接埠 80 的流量：</span><span class="sxs-lookup"><span data-stu-id="01679-120">Set Azure toodirect port 80 traffic from hello web tooport 80 on hello virtual machine:</span></span>
   
   1. <span data-ttu-id="01679-121">在 hello Azure 入口網站，移 toohello 儀表板，然後選取您新建立的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="01679-121">In hello Azure portal, go toohello dashboard and select your newly created virtual machine.</span></span>
   2. <span data-ttu-id="01679-122">選取 端點，然後按一下新增。</span><span class="sxs-lookup"><span data-stu-id="01679-122">Click **Endpoints**, and then click **Add**.</span></span>

     ![新增端點。](./media/python-django-web-app/django-helloworld-add-endpoint-new-portal.png)

   3. <span data-ttu-id="01679-124">在 hello**加入端點** 頁面上，針對**名稱**，輸入**HTTP**。</span><span class="sxs-lookup"><span data-stu-id="01679-124">On hello **Add endpoint** page, for **Name**, enter **HTTP**.</span></span> <span data-ttu-id="01679-125">設定 hello 公用和私人 TCP 連接埠太**80**。</span><span class="sxs-lookup"><span data-stu-id="01679-125">Set hello public and private TCP ports too**80**.</span></span>

     ![輸入名稱並設定公用和私人連接埠](./media/python-django-web-app/django-helloworld-add-endpoint-set-ports-new-portal.png)

   4. <span data-ttu-id="01679-127">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="01679-127">Click **OK**.</span></span>
     
3. <span data-ttu-id="01679-128">Hello 儀表板 中，選取您的 VM。</span><span class="sxs-lookup"><span data-stu-id="01679-128">In hello dashboard, select your VM.</span></span> <span data-ttu-id="01679-129">按一下 toouse 遠端桌面通訊協定 (RDP) tooremotely 登入新建立的 Azure 虛擬機器，toohello**連接**。</span><span class="sxs-lookup"><span data-stu-id="01679-129">toouse Remote Desktop Protocol (RDP) tooremotely sign in toohello newly created Azure virtual machine, click **Connect**.</span></span>  

> [!IMPORTANT] 
> <span data-ttu-id="01679-130">hello 下列指示假設您正確簽署 toohello 虛擬機器中。</span><span class="sxs-lookup"><span data-stu-id="01679-130">hello following instructions assume that you signed in toohello virtual machine correctly.</span></span> <span data-ttu-id="01679-131">它們也假設您要發出 hello 虛擬機器中，而不是在本機電腦的命令。</span><span class="sxs-lookup"><span data-stu-id="01679-131">They also assume that you are issuing commands in hello virtual machine and not on your local computer.</span></span>

## <span data-ttu-id="01679-132"><a id="setup"> </a>安裝 Python、Django 和 WFastCGI</span><span class="sxs-lookup"><span data-stu-id="01679-132"><a id="setup"> </a>Install Python, Django, and WFastCGI</span></span>
> [!NOTE]
> <span data-ttu-id="01679-133">使用 Internet Explorer toodownload，您可能必須 tooconfigure Internet Explorer**增強式安全性設定**設定。</span><span class="sxs-lookup"><span data-stu-id="01679-133">toodownload by using Internet Explorer, you might have tooconfigure Internet Explorer **Enhanced Security Configuration** settings.</span></span> <span data-ttu-id="01679-134">toodo 此，依序按一下**啟動** > **系統管理工具** > **伺服器管理員** > **本機伺服器**.</span><span class="sxs-lookup"><span data-stu-id="01679-134">toodo this, click **Start** > **Administrative Tools** > **Server Manager** > **Local Server**.</span></span> <span data-ttu-id="01679-135">按一下 [IE 增強式安全性設定]，然後選取 [關閉]。</span><span class="sxs-lookup"><span data-stu-id="01679-135">Click **IE Enhanced Security Configuration**, and then select **Off**.</span></span>

1. <span data-ttu-id="01679-136">安裝 hello 最新版本的 Python 2.7 或從 Python 3.4 [python.org][python.org]。</span><span class="sxs-lookup"><span data-stu-id="01679-136">Install hello latest versions of Python 2.7 or Python 3.4 from [python.org][python.org].</span></span>
2. <span data-ttu-id="01679-137">安裝使用 pip 的 hello wfastcgi 和 django 封裝。</span><span class="sxs-lookup"><span data-stu-id="01679-137">Install hello wfastcgi and django packages using pip.</span></span>
   
    <span data-ttu-id="01679-138">使用 Python 2.7 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="01679-138">For Python 2.7, use hello following command:</span></span>
   
        c:\python27\scripts\pip install wfastcgi
        c:\python27\scripts\pip install django
   
    <span data-ttu-id="01679-139">使用 Python 3.4 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="01679-139">For Python 3.4, use hello following command:</span></span>
   
        c:\python34\scripts\pip install wfastcgi
        c:\python34\scripts\pip install django

## <a name="install-iis-with-fastcgi"></a><span data-ttu-id="01679-140">安裝含 FastCGI 的 IIS</span><span class="sxs-lookup"><span data-stu-id="01679-140">Install IIS with FastCGI</span></span>
* <span data-ttu-id="01679-141">使用 FastCGI 支援安裝 Internet Information Services (IIS)。</span><span class="sxs-lookup"><span data-stu-id="01679-141">Install Internet Information Services (IIS) with FastCGI support.</span></span> <span data-ttu-id="01679-142">這可能需要幾分鐘的時間 tooexecute。</span><span class="sxs-lookup"><span data-stu-id="01679-142">This might take several minutes tooexecute.</span></span>
   
        start /wait %windir%\System32\PkgMgr.exe /iu:IIS-WebServerRole;IIS-WebServer;IIS-CommonHttpFeatures;IIS-StaticContent;IIS-DefaultDocument;IIS-DirectoryBrowsing;IIS-HttpErrors;IIS-HealthAndDiagnostics;IIS-HttpLogging;IIS-LoggingLibraries;IIS-RequestMonitor;IIS-Security;IIS-RequestFiltering;IIS-HttpCompressionStatic;IIS-WebServerManagementTools;IIS-ManagementConsole;WAS-WindowsActivationService;WAS-ProcessModel;WAS-NetFxEnvironment;WAS-ConfigurationAPI;IIS-CGI

## <a name="create-a-new-django-application"></a><span data-ttu-id="01679-143">建立新的 Django 應用程式</span><span class="sxs-lookup"><span data-stu-id="01679-143">Create a new Django application</span></span>
1. <span data-ttu-id="01679-144">在 C:\inetpub\wwwroot，toocreate 新 Django 專案中，輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="01679-144">In C:\inetpub\wwwroot, toocreate a new Django project, enter hello following command:</span></span>
   
   <span data-ttu-id="01679-145">使用 Python 2.7 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="01679-145">For Python 2.7, use hello following command:</span></span>
   
       C:\Python27\Scripts\django-admin.exe startproject helloworld
   
   <span data-ttu-id="01679-146">使用 Python 3.4 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="01679-146">For Python 3.4, use hello following command:</span></span>
   
       C:\Python34\Scripts\django-admin.exe startproject helloworld
   
   ![hello hello 新 AzureService 命令結果](./media/python-django-web-app/django-helloworld-cmd-new-azure-service.png)
2. <span data-ttu-id="01679-148">hello`django-admin`命令會產生如 Django 架構網站的基本結構：</span><span class="sxs-lookup"><span data-stu-id="01679-148">hello `django-admin` command generates a basic structure for Django-based websites:</span></span>
   
   * <span data-ttu-id="01679-149">`helloworld\manage.py` 可協助您開始裝載及停止裝載以 Django 作為基礎的網站。</span><span class="sxs-lookup"><span data-stu-id="01679-149">`helloworld\manage.py` helps you start hosting and stop hosting your Django-based website.</span></span>
   * <span data-ttu-id="01679-150">`helloworld\helloworld\settings.py` 具有您應用程式的 Django 設定。</span><span class="sxs-lookup"><span data-stu-id="01679-150">`helloworld\helloworld\settings.py` has Django settings for your application.</span></span>
   * <span data-ttu-id="01679-151">`helloworld\helloworld\urls.py`具有 hello 每個 URL 和它的檢視之間的對應程式碼。</span><span class="sxs-lookup"><span data-stu-id="01679-151">`helloworld\helloworld\urls.py` has hello mapping code between each URL and its view.</span></span>
3. <span data-ttu-id="01679-152">在 hello C:\inetpub\wwwroot\helloworld\helloworld 目錄中，建立名為 views.py 新檔案。</span><span class="sxs-lookup"><span data-stu-id="01679-152">In hello C:\inetpub\wwwroot\helloworld\helloworld directory, create a new file named views.py.</span></span> <span data-ttu-id="01679-153">此檔案具有 hello 檢視呈現 hello"hello world"的頁面。</span><span class="sxs-lookup"><span data-stu-id="01679-153">This file has hello view that renders hello "hello world" page.</span></span> <span data-ttu-id="01679-154">在程式碼編輯器中，輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="01679-154">In your code editor, enter hello following commands:</span></span>
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. <span data-ttu-id="01679-155">取代下列命令的 hello hello hello urls.py 檔案內容：</span><span class="sxs-lookup"><span data-stu-id="01679-155">Replace hello contents of hello urls.py file with hello following commands:</span></span>
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-iis"></a><span data-ttu-id="01679-156">設定 IIS</span><span class="sxs-lookup"><span data-stu-id="01679-156">Set up IIS</span></span>
1. <span data-ttu-id="01679-157">在 hello 全域 applicationhost.config 檔案中，解除鎖定 hello 處理常式區段。</span><span class="sxs-lookup"><span data-stu-id="01679-157">In hello global applicationhost.config file, unlock hello handlers section.</span></span>  <span data-ttu-id="01679-158">這可讓您 web.config 檔案 toouse hello Python 的處理常式。</span><span class="sxs-lookup"><span data-stu-id="01679-158">This allows your web.config file toouse hello Python handler.</span></span> <span data-ttu-id="01679-159">新增這個命令：</span><span class="sxs-lookup"><span data-stu-id="01679-159">Add this command:</span></span>
   
        %windir%\system32\inetsrv\appcmd unlock config -section:system.webServer/handlers
2. <span data-ttu-id="01679-160">啟動 WFastCGI。</span><span class="sxs-lookup"><span data-stu-id="01679-160">Activate WFastCGI.</span></span> <span data-ttu-id="01679-161">這樣會加入應用程式 toohello 全域 applicationhost.config 檔，它會參考 tooyour Python 解譯器可執行檔和 hello wfastcgi.py 指令碼。</span><span class="sxs-lookup"><span data-stu-id="01679-161">This adds an application toohello global applicationhost.config file, which refers tooyour Python interpreter executable and hello wfastcgi.py script.</span></span>
   
    <span data-ttu-id="01679-162">在 Python 2.7 中：</span><span class="sxs-lookup"><span data-stu-id="01679-162">In Python 2.7:</span></span>
   
        C:\python27\scripts\wfastcgi-enable
   
    <span data-ttu-id="01679-163">在 Python 3.4 中：</span><span class="sxs-lookup"><span data-stu-id="01679-163">In Python 3.4:</span></span>
   
        C:\python34\scripts\wfastcgi-enable
3. <span data-ttu-id="01679-164">在 C:\inetpub\wwwroot\helloworld 中建立 web.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="01679-164">In C:\inetpub\wwwroot\helloworld, create a web.config file.</span></span> <span data-ttu-id="01679-165">hello 值 hello`scriptProcessor`屬性應該符合 hello hello 前面步驟的輸出。</span><span class="sxs-lookup"><span data-stu-id="01679-165">hello value of hello `scriptProcessor` attribute should match hello output from hello preceding step.</span></span> <span data-ttu-id="01679-166">如需 hello wfastcgi 設定的詳細資訊，請參閱[pypi wfastcgi][wfastcgi]。</span><span class="sxs-lookup"><span data-stu-id="01679-166">For more information about hello wfastcgi setting, see [pypi wfastcgi][wfastcgi].</span></span>
   
   <span data-ttu-id="01679-167">在 Python 2.7 中：</span><span class="sxs-lookup"><span data-stu-id="01679-167">In  Python 2.7:</span></span>
   
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
   
   <span data-ttu-id="01679-168">在 Python 3.4 中：</span><span class="sxs-lookup"><span data-stu-id="01679-168">In  Python 3.4:</span></span>
   
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
4. <span data-ttu-id="01679-169">更新 hello hello IIS 預設網站 toopoint toohello Django 專案資料夾的位置：</span><span class="sxs-lookup"><span data-stu-id="01679-169">Update hello location of hello IIS default website toopoint toohello Django project folder:</span></span>
   
        %windir%\system32\inetsrv\appcmd set vdir "Default Web Site/" -physicalPath:"C:\inetpub\wwwroot\helloworld"
5. <span data-ttu-id="01679-170">載入 hello 網頁瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="01679-170">Load hello webpage in your browser.</span></span>

![在瀏覽器視窗會顯示在 Azure 上的 hello hello world 網頁][1]

## <a name="shut-down-your-azure-virtual-machine"></a><span data-ttu-id="01679-172">關閉 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="01679-172">Shut down your Azure virtual machine</span></span>
<span data-ttu-id="01679-173">當您完成本教學課程中時，我們建議您關閉或移除 hello hello 教學課程中建立的 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="01679-173">When you're done with this tutorial, we recommend that you shut down or remove hello Azure VM you created for hello tutorial.</span></span> <span data-ttu-id="01679-174">這樣可為其他教學課程釋放資源，您也可以避免產生 Azure 使用量費用。</span><span class="sxs-lookup"><span data-stu-id="01679-174">This frees up resources for other tutorials, and you can avoid incurring Azure usage charges.</span></span>

[1]: ./media/python-django-web-app/django-helloworld-browser-azure.png

[port80]: ./media/python-django-web-app/django-helloworld-port80.png

[Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[python.org]: https://www.python.org/downloads/
[wfastcgi]: https://pypi.python.org/pypi/wfastcgi
