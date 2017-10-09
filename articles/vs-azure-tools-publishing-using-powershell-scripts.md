---
title: "aaaUsing Windows PowerShell 指令碼 tooPublish tooDev 和測試環境 |Microsoft 文件"
description: "了解如何 toouse Windows PowerShell 指令碼，從 Visual Studio toopublish toodevelopment 和測試環境。"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5fff1301-5469-4d97-be88-c85c30f837c1
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 491a058f96255576afa74f6156f20ae9559bb9f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-windows-powershell-scripts-toopublish-toodev-and-test-environments"></a><span data-ttu-id="e9385-103">使用 Windows PowerShell 指令碼 toopublish toodev 和測試環境</span><span class="sxs-lookup"><span data-stu-id="e9385-103">Using Windows PowerShell scripts toopublish toodev and test environments</span></span>
<span data-ttu-id="e9385-104">當您在 Visual Studio 中建立 web 應用程式時，您可以產生 Windows PowerShell 指令碼可讓您的網站 tooAzure 稍後 tooautomate hello 發佈為 Web 應用程式在 Azure 應用程式服務或虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e9385-104">When you create a web application in Visual Studio, you can generate a Windows PowerShell script that you can use later tooautomate hello publishing of your website tooAzure as a Web App in Azure App Service or a virtual machine.</span></span> <span data-ttu-id="e9385-105">您可以編輯和擴充 hello hello Visual Studio 編輯器 toosuit 中的 Windows PowerShell 指令碼程式的需求，或與現有的組建、 測試和發佈指令碼整合 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="e9385-105">You can edit and extend hello Windows PowerShell script in hello Visual Studio editor toosuit your requirements, or integrate hello script with existing build, test, and publishing scripts.</span></span>

<span data-ttu-id="e9385-106">使用這些指令碼，您可以佈建網站的自訂版本 (也稱為開發和測試環境)，以做臨時使用。</span><span class="sxs-lookup"><span data-stu-id="e9385-106">Using these scripts, you can provision customized versions (also known as dev and test environments) of your site for temporary use.</span></span> <span data-ttu-id="e9385-107">比方說，您可能會設定您的網站的特定版本 Azure 的虛擬機器上或在暫存位置上的網站 toorun hello 測試套件、 重現錯誤、 測試錯誤修正、 試驗提議的變更，或設定示範或展示的自訂環境。</span><span class="sxs-lookup"><span data-stu-id="e9385-107">For example, you might set up a particular version of your website on an Azure virtual machine or on hello staging slot on a website toorun a test suite, reproduce a bug, test a bug fix, trial a proposed change, or set up a custom environment for a demo or presentation.</span></span> <span data-ttu-id="e9385-108">您已建立的指令碼可用於發行專案之後，您可以重新執行 hello 指令碼，如有需要重新建立相同的環境，或執行您 web 應用程式 toocreate 的組建進行測試的自訂環境的 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="e9385-108">After you've created a script that publishes your project, you can recreate identical environments by re-running hello script as needed, or run hello script with your own build of your web application toocreate a custom environment for testing.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e9385-109">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="e9385-109">What you need</span></span>
* <span data-ttu-id="e9385-110">Azure SDK 2.3 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="e9385-110">Azure SDK 2.3 or later.</span></span> <span data-ttu-id="e9385-111">如需詳細資訊，請參閱 [Visual Studio 下載](http://go.microsoft.com/fwlink/?LinkID=624384) 。</span><span class="sxs-lookup"><span data-stu-id="e9385-111">See [Visual Studio Downloads](http://go.microsoft.com/fwlink/?LinkID=624384) for more information.</span></span>

<span data-ttu-id="e9385-112">您不需要 web 專案 hello Azure SDK toogenerate hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="e9385-112">You do not need hello Azure SDK toogenerate hello scripts for web projects.</span></span> <span data-ttu-id="e9385-113">這項功能是供 Web 專案使用，而非供雲端服務中的 Web 角色使用。</span><span class="sxs-lookup"><span data-stu-id="e9385-113">This feature is for web projects, not web roles in cloud services.</span></span>

* <span data-ttu-id="e9385-114">Azure PowerShell 0.7.4 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="e9385-114">Azure PowerShell 0.7.4 or later.</span></span> <span data-ttu-id="e9385-115">請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="e9385-115">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>
* <span data-ttu-id="e9385-116">[Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="e9385-116">[Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) or later.</span></span>

## <a name="additional-tools"></a><span data-ttu-id="e9385-117">其他工具</span><span class="sxs-lookup"><span data-stu-id="e9385-117">Additional tools</span></span>
<span data-ttu-id="e9385-118">我們有提供其他工具和資源，以供您在 Visual Studio 中使用 PowerShell 進行 Azure 開發。</span><span class="sxs-lookup"><span data-stu-id="e9385-118">Additional tools and resources for working with PowerShell in Visual Studio for Azure development are available.</span></span> <span data-ttu-id="e9385-119">請參閱 [PowerShell Tools for Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012)。</span><span class="sxs-lookup"><span data-stu-id="e9385-119">See [PowerShell Tools for Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).</span></span>

## <a name="generating-hello-publish-scripts"></a><span data-ttu-id="e9385-120">產生 hello 發行指令碼</span><span class="sxs-lookup"><span data-stu-id="e9385-120">Generating hello publish scripts</span></span>
<span data-ttu-id="e9385-121">您可以產生 hello 裝載您的網站，當您使用建立新專案的虛擬機器的發行指令碼[這些指示](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="e9385-121">You can generate hello publish scripts for a virtual machine that hosts your website when you create a new project by following [these instructions](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="e9385-122">您也可以 [在 Azure App Service 中產生 Web 應用程式的發佈指令碼](app-service-web/app-service-web-get-started-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="e9385-122">You can also [generate publish scripts for web apps in Azure App Service](app-service-web/app-service-web-get-started-dotnet.md).</span></span>

## <a name="scripts-that-visual-studio-generates"></a><span data-ttu-id="e9385-123">Visual Studio 所產生的指令碼</span><span class="sxs-lookup"><span data-stu-id="e9385-123">Scripts that Visual Studio generates</span></span>
<span data-ttu-id="e9385-124">Visual Studio 會產生名為方案層級資料夾**PublishScripts** ，其中包含兩個 Windows PowerShell 檔案，您的虛擬機器或網站，並含有可讓您在 hello 函式的模組的發行指令碼指令碼。</span><span class="sxs-lookup"><span data-stu-id="e9385-124">Visual Studio generates a solution-level folder called **PublishScripts** that contains two Windows PowerShell files, a publish script for your virtual machine or website, and a module that contains functions that you can use in hello scripts.</span></span> <span data-ttu-id="e9385-125">Visual Studio 也會產生以指定您要部署的 hello 專案 hello 詳細資料的 hello JSON 格式的檔案。</span><span class="sxs-lookup"><span data-stu-id="e9385-125">Visual Studio also generates a file in hello JSON format that specifies hello details of hello project you are deploying.</span></span>

### <a name="windows-powershell-publish-script"></a><span data-ttu-id="e9385-126">Windows PowerShell 發佈指令碼</span><span class="sxs-lookup"><span data-stu-id="e9385-126">Windows PowerShell publish script</span></span>
<span data-ttu-id="e9385-127">hello 發行指令碼包含特定發行步驟部署 tooa 網站或虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e9385-127">hello publish script contains specific publish steps for deploying tooa website or virtual machine.</span></span> <span data-ttu-id="e9385-128">Visual Studio 提供語法著色功能，可用來進行 Windows PowerShell 開發。</span><span class="sxs-lookup"><span data-stu-id="e9385-128">Visual Studio provides syntax coloring for Windows PowerShell development.</span></span> <span data-ttu-id="e9385-129">說明 hello 函式，而且您可以自由地編輯 hello 指令碼 toosuit 中的 hello 函式多變的需求。</span><span class="sxs-lookup"><span data-stu-id="e9385-129">Help for hello functions is available, and you can freely edit hello functions in hello script toosuit your changing requirements.</span></span>

### <a name="windows-powershell-module"></a><span data-ttu-id="e9385-130">Windows PowerShell 模組</span><span class="sxs-lookup"><span data-stu-id="e9385-130">Windows PowerShell module</span></span>
<span data-ttu-id="e9385-131">hello Visual Studio 會產生的模組包含 hello 函式的 Windows PowerShell 發行指令碼使用。</span><span class="sxs-lookup"><span data-stu-id="e9385-131">hello Windows PowerShell module that Visual Studio generates contains functions that hello publish script uses.</span></span> <span data-ttu-id="e9385-132">這些是 Azure PowerShell 函數，而且不想要修改的 toobe。</span><span class="sxs-lookup"><span data-stu-id="e9385-132">These are Azure PowerShell functions and are not intended toobe modified.</span></span> <span data-ttu-id="e9385-133">請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="e9385-133">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>

### <a name="json-configuration-file"></a><span data-ttu-id="e9385-134">JSON 組態檔</span><span class="sxs-lookup"><span data-stu-id="e9385-134">JSON configuration file</span></span>
<span data-ttu-id="e9385-135">hello JSON 檔案建立在 hello**組態**資料夾並包含指定完全哪些資源 toodeploy tooAzure 的組態資料。</span><span class="sxs-lookup"><span data-stu-id="e9385-135">hello JSON file is created in hello **Configurations** folder and contains configuration data that specifies exactly which resources toodeploy tooAzure.</span></span> <span data-ttu-id="e9385-136">hello hello Visual Studio 所產生名稱是檔案的專案的名稱-WAWS-DEV.JSON-稱為如果您建立網站或專案名稱 VM 稱為若已建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e9385-136">hello name of hello file that Visual Studio generates is project-name-WAWS-dev.json if you created a website, or project name-VM-dev.json if you created a virtual machine.</span></span> <span data-ttu-id="e9385-137">以下是建立網站時所產生之 JSON 組態檔的範例。</span><span class="sxs-lookup"><span data-stu-id="e9385-137">Here's an example of a JSON configuration file that's generated when you create a website.</span></span> <span data-ttu-id="e9385-138">大部分 hello 值都一目了然。</span><span class="sxs-lookup"><span data-stu-id="e9385-138">Most of hello values are self-explanatory.</span></span> <span data-ttu-id="e9385-139">hello 網站名稱是由 Azure 產生，所以可能不符合您的專案名稱。</span><span class="sxs-lookup"><span data-stu-id="e9385-139">hello website name is generated by Azure, so it might not match your project name.</span></span>

```json
{
    "environmentSettings": {
        "webSite": {
            "name": "WebApplication26632",
            "location": "West US"
        },
        "databases": [{
            "connectionStringName": "DefaultConnection",
            "databaseName": "WebApplication26632_db",
            "serverName": "YourDatabaseServerName",
            "user": "sqluser2",
            "password": "",
            "edition": "",
            "size": "",
            "collation": "",
            "location": "West US"
        }]
    }
}
```
<span data-ttu-id="e9385-140">當您建立虛擬機器時，hello JSON 組態檔看起來類似 toohello 下列。</span><span class="sxs-lookup"><span data-stu-id="e9385-140">When you create a virtual machine, hello JSON configuration file looks similar toohello following.</span></span> <span data-ttu-id="e9385-141">請注意，雲端服務會建立為 hello 虛擬機器的容器。</span><span class="sxs-lookup"><span data-stu-id="e9385-141">Note that a cloud service is created as a container for hello virtual machine.</span></span> <span data-ttu-id="e9385-142">hello 虛擬機器包含 hello 透過 HTTP 和 HTTPS 進行 web 存取的一般端點以及 Web deploy，它可讓您從本機電腦、 遠端桌面和 Windows PowerShell toohello 網站發行端點。</span><span class="sxs-lookup"><span data-stu-id="e9385-142">hello virtual machine contains hello usual endpoints for web access through HTTP and HTTPS, as well as endpoints for Web Deploy, which lets you publish toohello website from your local machine, Remote Desktop, and Windows PowerShell.</span></span>

```json
{
    "environmentSettings": {
        "cloudService": {
            "name": "myusernamevm1",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myusernamevm1",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Win2K8R2SP1-Datacenter-201403.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [{
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [{
            "connectionStringName": "",
            "databaseName": "",
            "serverName": "",
            "user": "",
            "password": ""
        }],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

<span data-ttu-id="e9385-143">您可以編輯 hello JSON 組態 toochange 執行 hello 時，會發生什麼事發行指令碼。</span><span class="sxs-lookup"><span data-stu-id="e9385-143">You can edit hello JSON configuration toochange what happens when you run hello publish scripts.</span></span> <span data-ttu-id="e9385-144">hello`cloudService`和`virtualMachine`區段都是必要的但您可以刪除 hello`databases`區段，如果您不需要它。</span><span class="sxs-lookup"><span data-stu-id="e9385-144">hello `cloudService` and `virtualMachine` sections are required, but you can delete hello `databases` section if you don't need it.</span></span> <span data-ttu-id="e9385-145">Visual Studio 會產生的 hello 預設組態檔中的 空白的 hello 屬性是選擇性的;具有值 hello 預設組態檔中的所需。</span><span class="sxs-lookup"><span data-stu-id="e9385-145">hello properties that are empty in hello default configuration file that Visual Studio generates are optional; those that have values in hello default configuration file are required.</span></span>

<span data-ttu-id="e9385-146">如果您的網站有多個部署環境 （又稱為位置），而不是在 Azure 中的單一生產網站，您可以在 hello hello JSON 組態檔中的 hello 網站名稱中包含 hello 位置名稱。</span><span class="sxs-lookup"><span data-stu-id="e9385-146">If you have a website that has multiple deployment environments (known as slots) instead of a single production site in Azure, you can include hello slot name in hello name of hello website in hello JSON configuration file.</span></span> <span data-ttu-id="e9385-147">例如，如果您有一個名為的網站**mysite**和名為位置**測試**然後 hello URI 為 mysite test.cloudapp.net，但 hello hello 組態檔中的正確名稱 toouse 為 mysite （test）.</span><span class="sxs-lookup"><span data-stu-id="e9385-147">For example, if you have a website that's named **mysite** and a slot for it named **test** then hello URI is mysite-test.cloudapp.net, but hello correct name toouse in hello configuration file is mysite(test).</span></span> <span data-ttu-id="e9385-148">您可以只這樣如果 hello 網站和位置存在於訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e9385-148">You can only do this if hello website and slots already exist in your subscription.</span></span> <span data-ttu-id="e9385-149">如果不存在，但不指定 hello 位置執行 hello 指令碼來建立 hello 網站，然後建立 hello 中的 hello 位置[Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)，以及此後 hello 修改後的網站名稱用來執行 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="e9385-149">If they don't exist, create hello website by running hello script without specifying hello slot, then create hello slot in hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), and thereafter run hello script with hello modified website name.</span></span> <span data-ttu-id="e9385-150">如需 Web 應用程式部署位置的詳細資訊，請參閱 [針對 Azure App Service 中的 Web 應用程式設定預備環境](app-service-web/web-sites-staged-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="e9385-150">For more information about deployment slots for web apps, see [Set up staging environments for web apps in Azure App Service](app-service-web/web-sites-staged-publishing.md).</span></span>

## <a name="how-toorun-hello-publish-scripts"></a><span data-ttu-id="e9385-151">Toorun hello 發行指令碼的方式</span><span class="sxs-lookup"><span data-stu-id="e9385-151">How toorun hello publish scripts</span></span>
<span data-ttu-id="e9385-152">如果您從未執行過 Windows PowerShell 指令碼之前，您必須先設定 hello 執行原則 tooenable 指令碼 toorun。</span><span class="sxs-lookup"><span data-stu-id="e9385-152">If you have never run a Windows PowerShell script before, you must first set hello execution policy tooenable scripts toorun.</span></span> <span data-ttu-id="e9385-153">這是從執行 Windows PowerShell 指令碼，很容易遭受 toomalware 或病毒威脅的執行指令碼時的安全性功能 tooprevent 使用者。</span><span class="sxs-lookup"><span data-stu-id="e9385-153">This is a security feature tooprevent users from running Windows PowerShell scripts if they're vulnerable toomalware or viruses that involve executing scripts.</span></span>

### <a name="run-hello-script"></a><span data-ttu-id="e9385-154">執行 hello 指令碼</span><span class="sxs-lookup"><span data-stu-id="e9385-154">Run hello script</span></span>
1. <span data-ttu-id="e9385-155">建立 hello Web Deploy 封裝您的專案。</span><span class="sxs-lookup"><span data-stu-id="e9385-155">Create hello Web Deploy package for your project.</span></span> <span data-ttu-id="e9385-156">Web Deploy 套件是經過壓縮的封存 （.zip 檔），其中包含您想 toocopy tooyour 網站或虛擬機器的檔案。</span><span class="sxs-lookup"><span data-stu-id="e9385-156">A Web Deploy package is a compressed archive (.zip file) that contain files that you want toocopy tooyour website or virtual machine.</span></span> <span data-ttu-id="e9385-157">您可以在 Visual Studio 中為任何 Web 應用程式建立 Web Deploy 封裝。</span><span class="sxs-lookup"><span data-stu-id="e9385-157">You can create Web Deploy packages in Visual Studio for any web application.</span></span>

![建立 Web Deploy 封裝](./media/vs-azure-tools-publishing-using-powershell-scripts/IC767885.png)

<span data-ttu-id="e9385-159">如需詳細資訊，請參閱 [如何：在 Visual Studio 中建立 Web 部署封裝](https://msdn.microsoft.com/library/dd465323.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e9385-159">For more information, see [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span></span> <span data-ttu-id="e9385-160">您也可以在 hello > 一節中所述自動化 hello 建立您的 Web Deploy 封裝，**自訂和擴充 hello 發行指令碼**本主題稍後。</span><span class="sxs-lookup"><span data-stu-id="e9385-160">You can also automate hello creation of your Web Deploy package, as described in hello section **Customizing and extending hello publish scripts** later in this topic.</span></span>

1. <span data-ttu-id="e9385-161">在**方案總管 中**，開啟 hello hello 指令碼的操作功能表，然後選擇**開啟 PowerShell ISE 與**。</span><span class="sxs-lookup"><span data-stu-id="e9385-161">In **Solution Explorer**, open hello context menu for hello script, and then choose **Open with PowerShell ISE**.</span></span>
2. <span data-ttu-id="e9385-162">如果這是 hello 您已在此電腦執行 Windows PowerShell 指令碼的第一次，開啟命令提示字元視窗使用系統管理員權限和型別 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="e9385-162">If this is hello first time you've run Windows PowerShell scripts on this computer, open a command prompt window with Administrator privileges and type hello following command:</span></span>

    ```powershell
    Set-ExecutionPolicy RemoteSigned
    ```

3. <span data-ttu-id="e9385-163">使用下列命令的 hello 登入 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="e9385-163">Sign in tooAzure by using hello following command.</span></span>

    ```powershell
    Add-AzureAccount
    ```

    <span data-ttu-id="e9385-164">出現提示時，提供您的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="e9385-164">When prompted, supply your username and password.</span></span>

    <span data-ttu-id="e9385-165">請注意當您自動執行 hello 指令碼，這個方法提供的 Azure 認證將無法運作。</span><span class="sxs-lookup"><span data-stu-id="e9385-165">Note that when you automate hello script, this method of providing Azure credentials won't work.</span></span> <span data-ttu-id="e9385-166">相反地，您應該使用 hello.publishsettings 檔案 tooprovide 認證。</span><span class="sxs-lookup"><span data-stu-id="e9385-166">Instead, you should use hello .publishsettings file tooprovide credentials.</span></span> <span data-ttu-id="e9385-167">一次您只能使用 hello 命令**Get-azurepublishsettingsfile** toodownload hello Azure 中，從檔案，之後使用**Import-azurepublishsettingsfile** tooimport hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="e9385-167">One time only, you use hello command **Get-AzurePublishSettingsFile** toodownload hello file from Azure, and thereafter use **Import-AzurePublishSettingsFile** tooimport hello file.</span></span> <span data-ttu-id="e9385-168">如需詳細指示，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="e9385-168">For detailed instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

4. <span data-ttu-id="e9385-169">（選擇性）如果您想 toocreate Azure 資源 hello 虛擬機器、 資料庫和網站，但不要發行 web 應用程式，例如使用 hello **Publish-webapplication.ps1**命令與 hello **-組態**引數設定 toohello JSON 組態檔。</span><span class="sxs-lookup"><span data-stu-id="e9385-169">(Optional) If you want toocreate Azure resources such as hello virtual machine, database, and website without publishing your web application, use hello **Publish-WebApplication.ps1** command with hello **-Configuration** argument set toohello JSON configuration file.</span></span> <span data-ttu-id="e9385-170">此命令列使用 hello JSON 組態檔 toodetermine 哪些資源 toocreate。</span><span class="sxs-lookup"><span data-stu-id="e9385-170">This command line uses hello JSON configuration file toodetermine which resources toocreate.</span></span> <span data-ttu-id="e9385-171">它會使用其他命令列引數的 hello 預設設定，因為它會建立 hello 資源，但不會發行 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e9385-171">Because it uses hello default settings for other command-line arguments, it creates hello resources, but doesn't publish your web application.</span></span> <span data-ttu-id="e9385-172">hello – Verbose 選項提供有關最新動態的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="e9385-172">hello –Verbose option gives you more information about what's happening.</span></span>

    ```powershell
    Publish-WebApplication.ps1 -Verbose –Configuration C:\Path\WebProject-WAWS-dev.json
    ```

5. <span data-ttu-id="e9385-173">使用 hello **Publish-webapplication.ps1**命令中其中一個 hello 遵循範例 tooinvoke hello 指令碼所示，並發行您的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e9385-173">Use hello **Publish-WebApplication.ps1** command as shown in one of hello following examples tooinvoke hello script and publish your web application.</span></span> <span data-ttu-id="e9385-174">如果您需要 toooverride hello 預設設定任何 hello 其他引數，例如 hello 訂用帳戶名稱、 發行套件名稱、 虛擬機器認證或資料庫伺服器認證，您可以指定這些參數。</span><span class="sxs-lookup"><span data-stu-id="e9385-174">If you need toooverride hello default settings for any of hello other arguments, such as hello subscription name, publish package name, virtual machine credentials, or database server credentials, you can specify those parameters.</span></span> <span data-ttu-id="e9385-175">使用 hello **– Verbose**選項 toosee hello 發行程序的 hello 進度的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="e9385-175">Use hello **–Verbose** option toosee more information about hello progress of hello publishing process.</span></span>

    ```powershell
    Publish-WebApplication.ps1 –Configuration C:\Path\WebProject-WAWS-dev-json `
    –SubscriptionName Contoso `
    -WebDeployPackage C:\Documents\Azure\ADWebApp.zip `
    -DatabaseServerPassword @{Name="dbServerName";Password="adminPassword"} `
    -Verbose
    ```

    <span data-ttu-id="e9385-176">如果您要建立虛擬機器，hello 命令看起來 hello 下列。</span><span class="sxs-lookup"><span data-stu-id="e9385-176">If you're creating a virtual machine, hello command looks like hello following.</span></span> <span data-ttu-id="e9385-177">此範例也顯示如何 toospecify hello 認證的多個資料庫。</span><span class="sxs-lookup"><span data-stu-id="e9385-177">This example also shows how toospecify hello credentials for multiple databases.</span></span> <span data-ttu-id="e9385-178">這些指令碼建立的 hello 虛擬機器，hello SSL 憑證不是來自受信任的根授權單位。</span><span class="sxs-lookup"><span data-stu-id="e9385-178">For hello virtual machines that these scripts create, hello SSL certificate is not from a trusted root authority.</span></span> <span data-ttu-id="e9385-179">因此，您需要 toouse hello **-AllowUntrusted**選項。</span><span class="sxs-lookup"><span data-stu-id="e9385-179">Therefore, you need toouse hello **–AllowUntrusted** option.</span></span>

    ```powershell
    Publish-WebApplication.ps1 `
    -Configuration C:\Path\ADVM-VM-test.json `
    -SubscriptionName Contoso `
    -WebDeployPackage C:\Path\ADVM.zip `
    -AllowUntrusted `
    -VMPassword @{name = "vmUserName"; password = "YourPasswordHere"} `
    -DatabaseServerPassword @{Name="server1";Password="adminPassword1"}, @{Name="server2";Password="adminPassword2"} `
    -Verbose
    ```

    <span data-ttu-id="e9385-180">hello 指令碼可以建立資料庫，但它不會建立資料庫伺服器。</span><span class="sxs-lookup"><span data-stu-id="e9385-180">hello script can create databases, but it doesn't create database servers.</span></span> <span data-ttu-id="e9385-181">如果您想 toocreate 資料庫伺服器，您可以使用 hello **New-azuresqldatabaseserver** hello Azure 模組中的函式。</span><span class="sxs-lookup"><span data-stu-id="e9385-181">If you want toocreate a database server, you can use hello **New-AzureSqlDatabaseServer** function in hello Azure module.</span></span>

## <a name="customizing-and-extending-hello-publish-scripts"></a><span data-ttu-id="e9385-182">自訂及擴充 hello 發行指令碼</span><span class="sxs-lookup"><span data-stu-id="e9385-182">Customizing and extending hello publish scripts</span></span>
<span data-ttu-id="e9385-183">您可以自訂 hello 發行指令碼和 JSON 組態檔。</span><span class="sxs-lookup"><span data-stu-id="e9385-183">You can customize hello publish script and JSON configuration file.</span></span> <span data-ttu-id="e9385-184">hello hello Windows PowerShell 模組中的函式**AzureWebAppPublishModule.psm1**不是預期的 toobe 修改。</span><span class="sxs-lookup"><span data-stu-id="e9385-184">hello functions in hello Windows PowerShell module **AzureWebAppPublishModule.psm1** are not intended toobe modified.</span></span> <span data-ttu-id="e9385-185">如果您只想 toospecify 不同的資料庫，或變更某些 hello hello 虛擬機器內容，編輯 hello JSON 組態檔。</span><span class="sxs-lookup"><span data-stu-id="e9385-185">If you just want toospecify a different database or change some of hello properties of hello virtual machine, edit hello JSON configuration file.</span></span> <span data-ttu-id="e9385-186">如果您想要的 hello 指令碼 tooautomate 建置和測試專案的 tooextend hello 功能，您可以實作中的函數虛設常式**Publish-webapplication.ps1**。</span><span class="sxs-lookup"><span data-stu-id="e9385-186">If you want tooextend hello functionality of hello script tooautomate building and testing your project, you can implement function stubs in **Publish-WebApplication.ps1**.</span></span>

<span data-ttu-id="e9385-187">tooautomate 建置您的專案，加入程式碼太呼叫 MSBuild 的`New-WebDeployPackage`這個程式碼範例所示。</span><span class="sxs-lookup"><span data-stu-id="e9385-187">tooautomate building your project, add code that calls MSBuild too`New-WebDeployPackage` as shown in this code example.</span></span> <span data-ttu-id="e9385-188">hello 路徑 toohello MSBuild 命令是 hello 您已安裝的 Visual Studio 版本而有所不同。</span><span class="sxs-lookup"><span data-stu-id="e9385-188">hello path toohello MSBuild command is different depending on hello version of Visual Studio you have installed.</span></span> <span data-ttu-id="e9385-189">tooget hello 正確的路徑，您可以使用 hello 函式**Get-msbuildcmd**，在此範例所示。</span><span class="sxs-lookup"><span data-stu-id="e9385-189">tooget hello correct path, you can use hello function **Get-MSBuildCmd**, as shown in this example.</span></span>

### <a name="tooautomate-building-your-project"></a><span data-ttu-id="e9385-190">tooautomate 建置專案</span><span class="sxs-lookup"><span data-stu-id="e9385-190">tooautomate building your project</span></span>
1. <span data-ttu-id="e9385-191">新增 hello `$ProjectFile` hello 全域 param 區段中的參數。</span><span class="sxs-lookup"><span data-stu-id="e9385-191">Add hello `$ProjectFile` parameter in hello global param section.</span></span>

    ```powershell
    [Parameter(Mandatory = $false)]
    [ValidateScript({Test-Path $_ -PathType Leaf})]
    [String]
    $ProjectFile,
    ```

2. <span data-ttu-id="e9385-192">Copy hello 函式`Get-MSBuildCmd`到指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="e9385-192">Copy hello function `Get-MSBuildCmd` into your script file.</span></span>

    ```powershell
    function Get-MSBuildCmd
    {
            process
    {

                $path =  Get-ChildItem "HKLM:\SOFTWARE\Microsoft\MSBuild\ToolsVersions\" |
                                    Sort-Object {[double]$_.PSChildName} -Descending |
                                    Select-Object -First 1 |
                                    Get-ItemProperty -Name MSBuildToolsPath |
                                    Select -ExpandProperty MSBuildToolsPath

                $path = (Join-Path -Path $path -ChildPath 'msbuild.exe')

            return Get-Item $path
        }
    }
    ```

3. <span data-ttu-id="e9385-193">取代`New-WebDeployPackage`以下列程式碼，並且在 hello 行建構 hello 預留位置取代的 hello `$msbuildCmd`。</span><span class="sxs-lookup"><span data-stu-id="e9385-193">Replace `New-WebDeployPackage` with hello following code and replace hello placeholders in hello line constructing `$msbuildCmd`.</span></span> <span data-ttu-id="e9385-194">此程式碼係用於 Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="e9385-194">This code is for Visual Studio 2015.</span></span> <span data-ttu-id="e9385-195">如果您使用 Visual Studio 2013，變更 hello **VisualStudioVersion**下面的屬性過`12.0`。</span><span class="sxs-lookup"><span data-stu-id="e9385-195">If you're using Visual Studio 2013, change hello **VisualStudioVersion** property below too`12.0`.</span></span>

    ```powershell
    function New-WebDeployPackage
    {
        #Write a function toobuild and package your web application
    ```

    <span data-ttu-id="e9385-196">toobuild 您 web 應用程式，請使用 MsBuild.exe。</span><span class="sxs-lookup"><span data-stu-id="e9385-196">toobuild your web application, use MsBuild.exe.</span></span> <span data-ttu-id="e9385-197">如需協助，請參閱 MSBuild 命令列參考︰[http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)</span><span class="sxs-lookup"><span data-stu-id="e9385-197">For help, see MSBuild Command-Line Reference at: [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)</span></span>

    ```powershell
    Write-VerboseWithTime 'Build-WebDeployPackage: Start'

    $msbuildCmd = '"{0}" "{1}" /T:Rebuild;Package /P:VisualStudioVersion=14.0 /p:OutputPath="{2}\MSBuildOutputPath" /flp:logfile=msbuild.log,v=d' -f (Get-MSBuildCmd), $ProjectFile, $scriptDirectory

    Write-VerboseWithTime ('Build-WebDeployPackage: ' + $msbuildCmd)
    ```

### <a name="start-execution-of-hello-build-command"></a><span data-ttu-id="e9385-198">開始執行 hello 建置命令</span><span class="sxs-lookup"><span data-stu-id="e9385-198">Start execution of hello build command</span></span>

```powershell
$job = Start-Process cmd.exe -ArgumentList('/C "' + $msbuildCmd + '"') -WindowStyle Normal -Wait -PassThru

if ($job.ExitCode -ne 0) {
    throw('MsBuild exited with an error. ExitCode:' + $job.ExitCode)
}

#Obtain hello project name
$projectName = (Get-Item $ProjectFile).BaseName

#Construct hello path tooweb deploy zip package
$DeployPackageDir =  '.\MSBuildOutputPath\_PublishedWebsites\{0}_Package\{0}.zip' -f $projectName

#Get hello full path for hello web deploy zip package. This is required for MSDeploy toowork
$WebDeployPackage = Resolve-Path –LiteralPath $DeployPackageDir

Write-VerboseWithTime 'Build-WebDeployPackage: End'

return $WebDeployPackage
}
```

1. <span data-ttu-id="e9385-199">呼叫 hello`New-WebDeployPackage`此行之前的函式： `$Config = Read-ConfigFile $Configuration` web 應用程式或`$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)`的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e9385-199">Call hello `New-WebDeployPackage` function before this line: `$Config = Read-ConfigFile $Configuration` for web apps or `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` for virtual machines.</span></span>

    ```powershell
    if($ProjectFile)
    {
    $WebDeployPackage = New-WebDeployPackage
    }
    ```

2. <span data-ttu-id="e9385-200">叫用自訂的 hello 指令碼，從命令列使用傳遞 hello`$Project`引數，如同下列範例命令列的 hello。</span><span class="sxs-lookup"><span data-stu-id="e9385-200">Invoke hello customized script from command line using passing hello `$Project` argument, as in hello following example command line.</span></span>

    ```powershell
    .\Publish-WebApplicationVM.ps1 -Configuration .\Configurations\WebApplication5-VM-dev.json `
    -ProjectFile ..\WebApplication5\WebApplication5.csproj `
    -VMPassword @{Name="VMUser";Password="Test.123"} `
    -AllowUntrusted `
    -Verbose
    ```

    <span data-ttu-id="e9385-201">tooautomate 測試應用程式加入程式碼太`Test-WebApplication`。</span><span class="sxs-lookup"><span data-stu-id="e9385-201">tooautomate testing of your application, add code too`Test-WebApplication`.</span></span> <span data-ttu-id="e9385-202">中的 hello 線條會確定 toouncomment **Publish-webapplication.ps1**呼叫這些函數。</span><span class="sxs-lookup"><span data-stu-id="e9385-202">Be sure toouncomment hello lines in **Publish-WebApplication.ps1** where these functions are called.</span></span> <span data-ttu-id="e9385-203">如果您沒有提供實作，您可以手動建立 Visual Studio 中，您的專案，然後執行的 hello 發行指令碼 toopublish tooAzure。</span><span class="sxs-lookup"><span data-stu-id="e9385-203">If you don't provide an implementation, you can manually build your project with Visual Studio, and then run hello publish script toopublish tooAzure.</span></span>

## <a name="publishing-function-summary"></a><span data-ttu-id="e9385-204">發佈函式摘要</span><span class="sxs-lookup"><span data-stu-id="e9385-204">Publishing function summary</span></span>
<span data-ttu-id="e9385-205">tooget 說明您可以在 hello Windows PowerShell 命令提示字元中使用的函式使用 hello 命令`Get-Help function-name`。</span><span class="sxs-lookup"><span data-stu-id="e9385-205">tooget help for functions you can use at hello Windows PowerShell command prompt, use hello command `Get-Help function-name`.</span></span> <span data-ttu-id="e9385-206">hello 說明包括參數說明和範例。</span><span class="sxs-lookup"><span data-stu-id="e9385-206">hello help includes parameter help and examples.</span></span> <span data-ttu-id="e9385-207">在 hello 指令碼來源檔案，也有相同的說明文字的 hello **AzureWebAppPublishModule.psm1**和**Publish-webapplication.ps1**。</span><span class="sxs-lookup"><span data-stu-id="e9385-207">hello same help text is also in hello script source files, **AzureWebAppPublishModule.psm1** and **Publish-WebApplication.ps1**.</span></span> <span data-ttu-id="e9385-208">hello 指令碼和說明都以您的 Visual Studio 語言進行當地語系化。</span><span class="sxs-lookup"><span data-stu-id="e9385-208">hello script and help are localized in your Visual Studio language.</span></span>

<span data-ttu-id="e9385-209">**AzureWebAppPublishModule**</span><span class="sxs-lookup"><span data-stu-id="e9385-209">**AzureWebAppPublishModule**</span></span>

| <span data-ttu-id="e9385-210">函式名稱</span><span class="sxs-lookup"><span data-stu-id="e9385-210">Function name</span></span> | <span data-ttu-id="e9385-211">說明</span><span class="sxs-lookup"><span data-stu-id="e9385-211">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e9385-212">Add-AzureSQLDatabase</span><span class="sxs-lookup"><span data-stu-id="e9385-212">Add-AzureSQLDatabase</span></span> |<span data-ttu-id="e9385-213">建立新的 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="e9385-213">Creates a new Azure SQL database.</span></span> |
| <span data-ttu-id="e9385-214">Add-AzureSQLDatabases</span><span class="sxs-lookup"><span data-stu-id="e9385-214">Add-AzureSQLDatabases</span></span> |<span data-ttu-id="e9385-215">從 Visual Studio 會產生的 hello JSON 組態檔中的 hello 值建立 Azure SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="e9385-215">Creates Azure SQL databases from hello values in hello JSON configuration file that Visual Studio generates.</span></span> |
| <span data-ttu-id="e9385-216">Add-AzureVM</span><span class="sxs-lookup"><span data-stu-id="e9385-216">Add-AzureVM</span></span> |<span data-ttu-id="e9385-217">建立 Azure 虛擬機器並傳回 hello hello URL 部署 VM。</span><span class="sxs-lookup"><span data-stu-id="e9385-217">Creates a Azure virtual machine and returns hello URL of hello deployed VM.</span></span> <span data-ttu-id="e9385-218">hello 函式中設定 hello 必要條件，然後呼叫 hello **New-azurevm**函式 （Azure 模組） toocreate 新的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e9385-218">hello function sets up hello prerequisites and then calls hello **New-AzureVM** function (Azure module) toocreate a new virtual machine.</span></span> |
| <span data-ttu-id="e9385-219">Add-AzureVMEndpoints</span><span class="sxs-lookup"><span data-stu-id="e9385-219">Add-AzureVMEndpoints</span></span> |<span data-ttu-id="e9385-220">加入新的輸入的端點 tooa 虛擬機器並傳回 hello 與 hello 新端點的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e9385-220">Adds new input endpoints tooa virtual machine and returns hello virtual machine with hello new endpoint.</span></span> |
| <span data-ttu-id="e9385-221">Add-AzureVMStorage</span><span class="sxs-lookup"><span data-stu-id="e9385-221">Add-AzureVMStorage</span></span> |<span data-ttu-id="e9385-222">Hello 目前訂用帳戶中建立新的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e9385-222">Creates a new Azure storage account in hello current subscription.</span></span> <span data-ttu-id="e9385-223">hello hello 帳戶名稱的開頭"devtest"後面接著唯一英數字串。</span><span class="sxs-lookup"><span data-stu-id="e9385-223">hello name of hello account begins with "devtest" followed by a unique alphanumeric string.</span></span> <span data-ttu-id="e9385-224">hello 函式會傳回 hello hello 新的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="e9385-224">hello function returns hello name of hello new storage account.</span></span> <span data-ttu-id="e9385-225">您必須指定位置或同質群組 hello 新儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e9385-225">You must specify either a location or an affinity group for hello new storage account.</span></span> |
| <span data-ttu-id="e9385-226">Add-AzureWebsite</span><span class="sxs-lookup"><span data-stu-id="e9385-226">Add-AzureWebsite</span></span> |<span data-ttu-id="e9385-227">具有 hello 指定的名稱和位置建立網站。</span><span class="sxs-lookup"><span data-stu-id="e9385-227">Creates a website with hello specified name and location.</span></span> <span data-ttu-id="e9385-228">此函式呼叫 hello **New-azurewebsite** hello Azure 模組中的函式。</span><span class="sxs-lookup"><span data-stu-id="e9385-228">This function calls hello **New-AzureWebsite** function in hello Azure module.</span></span> <span data-ttu-id="e9385-229">如果 hello 訂用帳戶已不包含具有指定名稱的 hello 的網站，此函式建立 hello 網站，並傳回網站物件。</span><span class="sxs-lookup"><span data-stu-id="e9385-229">If hello subscription doesn't already include a website with hello specified name, this function creates hello website and returns a website object.</span></span> <span data-ttu-id="e9385-230">否則，它會傳回 `$null`。</span><span class="sxs-lookup"><span data-stu-id="e9385-230">Otherwise, it returns `$null`.</span></span> |
| <span data-ttu-id="e9385-231">Backup-Subscription</span><span class="sxs-lookup"><span data-stu-id="e9385-231">Backup-Subscription</span></span> |<span data-ttu-id="e9385-232">儲存 hello 目前 Azure 訂用帳戶中 hello`$Script:originalSubscription`指令碼範圍的變數。此函式會將儲存 hello 目前的 Azure 訂用帳戶 (由`Get-AzureSubscription -Current`) 及其儲存體帳戶和 hello 訂用帳戶，此指令碼變更 (hello 變數中儲存`$UserSpecifiedSubscription`) 與其儲存體帳戶，指令碼範圍。</span><span class="sxs-lookup"><span data-stu-id="e9385-232">Saves hello current Azure subscription in hello `$Script:originalSubscription` variable in script scope.This function saves hello current Azure subscription (as obtained by `Get-AzureSubscription -Current`) and its storage account, and hello subscription that is changed by this script (stored in hello variable `$UserSpecifiedSubscription`) and its storage account, in script scope.</span></span> <span data-ttu-id="e9385-233">藉由儲存 hello 值，您可以使用函式，例如`Restore-Subscription`，toorestore hello 原始目前訂用帳戶和儲存體帳戶 toocurrent 狀態如果 hello 目前狀態已變更。</span><span class="sxs-lookup"><span data-stu-id="e9385-233">By saving hello values, you can use a function, such as `Restore-Subscription`, toorestore hello original current subscription and storage account toocurrent status if hello current status has changed.</span></span> |
| <span data-ttu-id="e9385-234">Find-AzureVM</span><span class="sxs-lookup"><span data-stu-id="e9385-234">Find-AzureVM</span></span> |<span data-ttu-id="e9385-235">取得 hello 指定 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e9385-235">Gets hello specified Azure virtual machine.</span></span> |
| <span data-ttu-id="e9385-236">Format-DevTestMessageWithTime</span><span class="sxs-lookup"><span data-stu-id="e9385-236">Format-DevTestMessageWithTime</span></span> |<span data-ttu-id="e9385-237">前面加上 hello tooa 訊息的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="e9385-237">Prepends hello date and time tooa message.</span></span> <span data-ttu-id="e9385-238">此函式可供寫入 toohello Error 和 Verbose 串流的訊息。</span><span class="sxs-lookup"><span data-stu-id="e9385-238">This function is designed for messages written toohello Error and Verbose streams.</span></span> |
| <span data-ttu-id="e9385-239">Get-AzureSQLDatabaseConnectionString</span><span class="sxs-lookup"><span data-stu-id="e9385-239">Get-AzureSQLDatabaseConnectionString</span></span> |<span data-ttu-id="e9385-240">組合連接字串 tooconnect tooan Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="e9385-240">Assembles a connection string tooconnect tooan Azure SQL database.</span></span> |
| <span data-ttu-id="e9385-241">Get-AzureVMStorage</span><span class="sxs-lookup"><span data-stu-id="e9385-241">Get-AzureVMStorage</span></span> |<span data-ttu-id="e9385-242">傳回 hello hello 名稱模式 hello 第一個儲存體帳戶名稱"devtest*"（不區分大小寫） hello 指定的位置或同質群組中。如果 hello"devtest*"hello 位置或同質群組，不符合儲存體帳戶、 hello 函式則會予以忽略。</span><span class="sxs-lookup"><span data-stu-id="e9385-242">Returns hello name of hello first storage account with hello name pattern "devtest*" (case insensitive) in hello specified location or affinity group. If hello "devtest*" storage account doesn't match hello location or affinity group, hello function ignores it.</span></span> <span data-ttu-id="e9385-243">您必須指定位置或同質群組。</span><span class="sxs-lookup"><span data-stu-id="e9385-243">You must specify either a location or an affinity group.</span></span> |
| <span data-ttu-id="e9385-244">Get-MSDeployCmd</span><span class="sxs-lookup"><span data-stu-id="e9385-244">Get-MSDeployCmd</span></span> |<span data-ttu-id="e9385-245">傳回命令 toorun hello MsDeploy.exe 工具。</span><span class="sxs-lookup"><span data-stu-id="e9385-245">Returns a command toorun hello MsDeploy.exe tool.</span></span> |
| <span data-ttu-id="e9385-246">New-AzureVMEnvironment</span><span class="sxs-lookup"><span data-stu-id="e9385-246">New-AzureVMEnvironment</span></span> |<span data-ttu-id="e9385-247">尋找或建立 hello 訂用帳戶符合 hello JSON 組態檔中的 hello 值中的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e9385-247">Finds or creates a virtual machine in hello subscription that matches hello values in hello JSON configuration file.</span></span> |
| <span data-ttu-id="e9385-248">Publish-WebPackage</span><span class="sxs-lookup"><span data-stu-id="e9385-248">Publish-WebPackage</span></span> |<span data-ttu-id="e9385-249">使用 MsDeploy.exe 和 web 發行套件。Zip 檔案 toodeploy 資源 tooa 網站。</span><span class="sxs-lookup"><span data-stu-id="e9385-249">Uses MsDeploy.exe and a web publish package .Zip file toodeploy resources tooa website.</span></span> <span data-ttu-id="e9385-250">此函式不會產生任何輸出。</span><span class="sxs-lookup"><span data-stu-id="e9385-250">This function doesn't generate any output.</span></span> <span data-ttu-id="e9385-251">如果 hello 呼叫 tooMSDeploy.exe，hello 函式會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="e9385-251">If hello call tooMSDeploy.exe fails, hello function throws an exception.</span></span> <span data-ttu-id="e9385-252">tooget 更多詳細的輸出，使用 hello **-Verbose**選項。</span><span class="sxs-lookup"><span data-stu-id="e9385-252">tooget more detailed output, use hello **-Verbose** option.</span></span> |
| <span data-ttu-id="e9385-253">Publish-WebPackageToVM</span><span class="sxs-lookup"><span data-stu-id="e9385-253">Publish-WebPackageToVM</span></span> |<span data-ttu-id="e9385-254">驗證 hello 參數值，然後呼叫 hello **Publish-webpackage**函式。</span><span class="sxs-lookup"><span data-stu-id="e9385-254">Verifies hello parameter values, and then calls hello **Publish-WebPackage** function.</span></span> |
| <span data-ttu-id="e9385-255">Read-ConfigFile</span><span class="sxs-lookup"><span data-stu-id="e9385-255">Read-ConfigFile</span></span> |<span data-ttu-id="e9385-256">驗證 hello JSON 組態檔並傳回所選值的雜湊資料表。</span><span class="sxs-lookup"><span data-stu-id="e9385-256">Validates hello JSON configuration file and returns a hash table of selected values.</span></span> |
| <span data-ttu-id="e9385-257">Restore-Subscription</span><span class="sxs-lookup"><span data-stu-id="e9385-257">Restore-Subscription</span></span> |<span data-ttu-id="e9385-258">重設 hello 目前訂用帳戶 toohello 原始訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e9385-258">Resets hello current subscription toohello original subscription.</span></span> |
| <span data-ttu-id="e9385-259">Test-AzureModule</span><span class="sxs-lookup"><span data-stu-id="e9385-259">Test-AzureModule</span></span> |<span data-ttu-id="e9385-260">傳回`$true`如果 hello 安裝的 Azure 模組版本為 0.7.4 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="e9385-260">Returns `$true` if hello installed Azure module version is 0.7.4 or later.</span></span> <span data-ttu-id="e9385-261">傳回`$false`如果 hello 模組尚未安裝，或是為舊的版本。</span><span class="sxs-lookup"><span data-stu-id="e9385-261">Returns `$false` if hello module isn't installed or is an earlier version.</span></span> <span data-ttu-id="e9385-262">此函式沒有參數。</span><span class="sxs-lookup"><span data-stu-id="e9385-262">This function has no parameters.</span></span> |
| <span data-ttu-id="e9385-263">Test-AzureModuleVersion</span><span class="sxs-lookup"><span data-stu-id="e9385-263">Test-AzureModuleVersion</span></span> |<span data-ttu-id="e9385-264">傳回`$true`如果 hello hello Azure 模組版本為 0.7.4 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="e9385-264">Returns `$true` if hello version of hello Azure module is 0.7.4 or later.</span></span> <span data-ttu-id="e9385-265">傳回`$false`如果 hello 模組尚未安裝，或是為舊的版本。</span><span class="sxs-lookup"><span data-stu-id="e9385-265">Returns `$false` if hello module isn't installed or is an earlier version.</span></span> <span data-ttu-id="e9385-266">此函式沒有參數。</span><span class="sxs-lookup"><span data-stu-id="e9385-266">This function has no parameters.</span></span> |
| <span data-ttu-id="e9385-267">Test-HttpsUrl</span><span class="sxs-lookup"><span data-stu-id="e9385-267">Test-HttpsUrl</span></span> |<span data-ttu-id="e9385-268">將轉換 hello 輸入的 URL tooa System.Uri 物件。</span><span class="sxs-lookup"><span data-stu-id="e9385-268">Converts hello input URL tooa System.Uri object.</span></span> <span data-ttu-id="e9385-269">傳回`$True`如果 hello URL 為絕對且其配置為 https。</span><span class="sxs-lookup"><span data-stu-id="e9385-269">Returns `$True` if hello URL is absolute and its scheme is https.</span></span> <span data-ttu-id="e9385-270">傳回`$false`如果 hello URL 是相對路徑、 其配置不是 HTTPS，或 hello 輸入的字串不能轉換的 tooa URL。</span><span class="sxs-lookup"><span data-stu-id="e9385-270">Returns `$false` if hello URL is relative, its scheme isn't HTTPS, or hello input string can't be converted tooa URL.</span></span> |
| <span data-ttu-id="e9385-271">Test-Member</span><span class="sxs-lookup"><span data-stu-id="e9385-271">Test-Member</span></span> |<span data-ttu-id="e9385-272">傳回`$true`如果屬性或方法是 hello 物件的成員。</span><span class="sxs-lookup"><span data-stu-id="e9385-272">Returns `$true` if a property or method is a member of hello object.</span></span> <span data-ttu-id="e9385-273">否則傳回 `$false`。</span><span class="sxs-lookup"><span data-stu-id="e9385-273">Otherwise, returns `$false`.</span></span> |
| <span data-ttu-id="e9385-274">Write-ErrorWithTime</span><span class="sxs-lookup"><span data-stu-id="e9385-274">Write-ErrorWithTime</span></span> |<span data-ttu-id="e9385-275">寫入前面會加上 hello 目前時間的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="e9385-275">Writes an error message prefixed with hello current time.</span></span> <span data-ttu-id="e9385-276">此函式呼叫 hello **Format-devtestmessagewithtime**寫入 hello 訊息 toohello 錯誤資料流之前的函式 tooprepend hello 時間。</span><span class="sxs-lookup"><span data-stu-id="e9385-276">This function calls hello **Format-DevTestMessageWithTime** function tooprepend hello time before writing hello message toohello Error stream.</span></span> |
| <span data-ttu-id="e9385-277">Write-HostWithTime</span><span class="sxs-lookup"><span data-stu-id="e9385-277">Write-HostWithTime</span></span> |<span data-ttu-id="e9385-278">寫入訊息 toohello 主機程式 (**Write-host**) 加上 hello 目前的時間。</span><span class="sxs-lookup"><span data-stu-id="e9385-278">Writes a message toohello host program (**Write-Host**) prefixed with hello current time.</span></span> <span data-ttu-id="e9385-279">撰寫 toohello 主機程式的 hello 效果各不相同。</span><span class="sxs-lookup"><span data-stu-id="e9385-279">hello effect of writing toohello host program varies.</span></span> <span data-ttu-id="e9385-280">大部分程式中主控 Windows PowerShell 的這些訊息 toostandard 將輸出寫入。</span><span class="sxs-lookup"><span data-stu-id="e9385-280">Most programs that host Windows PowerShell write these messages toostandard output.</span></span> |
| <span data-ttu-id="e9385-281">Write-VerboseWithTime</span><span class="sxs-lookup"><span data-stu-id="e9385-281">Write-VerboseWithTime</span></span> |<span data-ttu-id="e9385-282">寫入前面會加上 hello 目前時間的詳細資訊訊息。</span><span class="sxs-lookup"><span data-stu-id="e9385-282">Writes a verbose message prefixed with hello current time.</span></span> <span data-ttu-id="e9385-283">因為它會呼叫**Write-verbose**，hello 訊息會顯示只有 hello 指令碼執行時以 hello **Verbose**參數或當 hello **VerbosePreference**是喜好設定設定得**繼續**。</span><span class="sxs-lookup"><span data-stu-id="e9385-283">Because it calls **Write-Verbose**, hello message displays only when hello script runs with hello **Verbose** parameter or when hello **VerbosePreference** preference is set too**Continue**.</span></span> |

<span data-ttu-id="e9385-284">**Publish-WebApplication**</span><span class="sxs-lookup"><span data-stu-id="e9385-284">**Publish-WebApplication**</span></span>

| <span data-ttu-id="e9385-285">函式名稱</span><span class="sxs-lookup"><span data-stu-id="e9385-285">Function name</span></span> | <span data-ttu-id="e9385-286">說明</span><span class="sxs-lookup"><span data-stu-id="e9385-286">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e9385-287">New-AzureWebApplicationEnvironment</span><span class="sxs-lookup"><span data-stu-id="e9385-287">New-AzureWebApplicationEnvironment</span></span> |<span data-ttu-id="e9385-288">建立 Azure 資源，例如網站或虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e9385-288">Creates Azure resources, such as a website or virtual machine.</span></span> |
| <span data-ttu-id="e9385-289">New-WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="e9385-289">New-WebDeployPackage</span></span> |<span data-ttu-id="e9385-290">此函式未實作。</span><span class="sxs-lookup"><span data-stu-id="e9385-290">This function isn't implemented.</span></span> <span data-ttu-id="e9385-291">您可以在這個函式 toobuild 中新增命令，您的專案。</span><span class="sxs-lookup"><span data-stu-id="e9385-291">You can add commands in this function toobuild your project.</span></span> |
| <span data-ttu-id="e9385-292">Publish-AzureWebApplication</span><span class="sxs-lookup"><span data-stu-id="e9385-292">Publish-AzureWebApplication</span></span> |<span data-ttu-id="e9385-293">發行 web 應用程式 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="e9385-293">Publishes a web application tooAzure.</span></span> |
| <span data-ttu-id="e9385-294">Publish-WebApplication</span><span class="sxs-lookup"><span data-stu-id="e9385-294">Publish-WebApplication</span></span> |<span data-ttu-id="e9385-295">建立並部署 Visual Studio Web 專案的 Web Apps、虛擬機器、SQL Database 和儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e9385-295">Creates and deploys Web Apps, virtual machines, SQL databases, and storage accounts for a Visual Studio web project.</span></span> |
| <span data-ttu-id="e9385-296">Test-WebApplication</span><span class="sxs-lookup"><span data-stu-id="e9385-296">Test-WebApplication</span></span> |<span data-ttu-id="e9385-297">此函式未實作。</span><span class="sxs-lookup"><span data-stu-id="e9385-297">This function isn't implemented.</span></span> <span data-ttu-id="e9385-298">您可以在這個函式 tootest 中新增命令，您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="e9385-298">You can add commands in this function tootest your application.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e9385-299">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e9385-299">Next steps</span></span>
<span data-ttu-id="e9385-300">深入了解 PowerShell 的指令碼讀取[使用 Windows PowerShell 撰寫指令碼](https://technet.microsoft.com/library/bb978526.aspx)並查看其他的 Azure PowerShell 指令碼，於 hello[指令碼中心](https://azure.microsoft.com/documentation/scripts/)。</span><span class="sxs-lookup"><span data-stu-id="e9385-300">Learn more about PowerShell scripting by reading [Scripting with Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx) and see other Azure PowerShell scripts at hello [Script Center](https://azure.microsoft.com/documentation/scripts/).</span></span>
