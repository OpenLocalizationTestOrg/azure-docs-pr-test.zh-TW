---
title: "使用 Windows PowerShell 指令碼來發佈至開發和測試環境 | Microsoft Docs"
description: "了解如何從 Visual Studio 使用 Windows PowerShell 指令碼來發佈至開發和測試環境。"
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
ms.openlocfilehash: d4c39eb7a8bc97a980061872ba0f32f375e6976f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="using-windows-powershell-scripts-to-publish-to-dev-and-test-environments"></a><span data-ttu-id="f927a-103">使用 Windows PowerShell 指令碼來發行至開發和測試環境</span><span class="sxs-lookup"><span data-stu-id="f927a-103">Using Windows PowerShell scripts to publish to dev and test environments</span></span>
<span data-ttu-id="f927a-104">當您在 Visual Studio 中建立 Web 應用程式時，您可以產生 Windows PowerShell 指令碼，以供稍後用來將網站自動發佈至 Azure 做為 Azure App Service 或虛擬機器中的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f927a-104">When you create a web application in Visual Studio, you can generate a Windows PowerShell script that you can use later to automate the publishing of your website to Azure as a Web App in Azure App Service or a virtual machine.</span></span> <span data-ttu-id="f927a-105">您可以在 Visual Studio 編輯器中編輯和擴充 Windows PowerShell 指令碼以符合需求，或將指令碼整合到現有組建、測試和發佈指令碼。</span><span class="sxs-lookup"><span data-stu-id="f927a-105">You can edit and extend the Windows PowerShell script in the Visual Studio editor to suit your requirements, or integrate the script with existing build, test, and publishing scripts.</span></span>

<span data-ttu-id="f927a-106">使用這些指令碼，您可以佈建網站的自訂版本 (也稱為開發和測試環境)，以做臨時使用。</span><span class="sxs-lookup"><span data-stu-id="f927a-106">Using these scripts, you can provision customized versions (also known as dev and test environments) of your site for temporary use.</span></span> <span data-ttu-id="f927a-107">例如，您可以在 Azure 虛擬機器上或網站的預備位置上設定網站的特定版本，以執行測試套件、重現錯誤、測試錯誤修正、試驗提議的變更，或設定用來進行示範或展示的自訂環境。</span><span class="sxs-lookup"><span data-stu-id="f927a-107">For example, you might set up a particular version of your website on an Azure virtual machine or on the staging slot on a website to run a test suite, reproduce a bug, test a bug fix, trial a proposed change, or set up a custom environment for a demo or presentation.</span></span> <span data-ttu-id="f927a-108">在建立用來發佈專案的指令碼後，您可以視需要重新執行指令碼來重建相同環境，或對 Web 應用程式的自有組建執行指令碼以建立用於測試的自訂環境。</span><span class="sxs-lookup"><span data-stu-id="f927a-108">After you've created a script that publishes your project, you can recreate identical environments by re-running the script as needed, or run the script with your own build of your web application to create a custom environment for testing.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f927a-109">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="f927a-109">What you need</span></span>
* <span data-ttu-id="f927a-110">Azure SDK 2.3 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="f927a-110">Azure SDK 2.3 or later.</span></span> <span data-ttu-id="f927a-111">如需詳細資訊，請參閱 [Visual Studio 下載](http://go.microsoft.com/fwlink/?LinkID=624384) 。</span><span class="sxs-lookup"><span data-stu-id="f927a-111">See [Visual Studio Downloads](http://go.microsoft.com/fwlink/?LinkID=624384) for more information.</span></span>

<span data-ttu-id="f927a-112">要產生 Web 專案的指令碼並不需要用到 Azure SDK。</span><span class="sxs-lookup"><span data-stu-id="f927a-112">You do not need the Azure SDK to generate the scripts for web projects.</span></span> <span data-ttu-id="f927a-113">這項功能是供 Web 專案使用，而非供雲端服務中的 Web 角色使用。</span><span class="sxs-lookup"><span data-stu-id="f927a-113">This feature is for web projects, not web roles in cloud services.</span></span>

* <span data-ttu-id="f927a-114">Azure PowerShell 0.7.4 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="f927a-114">Azure PowerShell 0.7.4 or later.</span></span> <span data-ttu-id="f927a-115">如需詳細資訊，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview) 。</span><span class="sxs-lookup"><span data-stu-id="f927a-115">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>
* <span data-ttu-id="f927a-116">[Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="f927a-116">[Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) or later.</span></span>

## <a name="additional-tools"></a><span data-ttu-id="f927a-117">其他工具</span><span class="sxs-lookup"><span data-stu-id="f927a-117">Additional tools</span></span>
<span data-ttu-id="f927a-118">我們有提供其他工具和資源，以供您在 Visual Studio 中使用 PowerShell 進行 Azure 開發。</span><span class="sxs-lookup"><span data-stu-id="f927a-118">Additional tools and resources for working with PowerShell in Visual Studio for Azure development are available.</span></span> <span data-ttu-id="f927a-119">請參閱 [PowerShell Tools for Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012)。</span><span class="sxs-lookup"><span data-stu-id="f927a-119">See [PowerShell Tools for Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).</span></span>

## <a name="generating-the-publish-scripts"></a><span data-ttu-id="f927a-120">產生發佈指令碼</span><span class="sxs-lookup"><span data-stu-id="f927a-120">Generating the publish scripts</span></span>
<span data-ttu-id="f927a-121">您可以遵循 [這些指示](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)，在建立新專案時產生裝載網站之虛擬機器的發佈指令碼。</span><span class="sxs-lookup"><span data-stu-id="f927a-121">You can generate the publish scripts for a virtual machine that hosts your website when you create a new project by following [these instructions](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="f927a-122">您也可以 [在 Azure App Service 中產生 Web 應用程式的發佈指令碼](app-service-web/app-service-web-get-started-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="f927a-122">You can also [generate publish scripts for web apps in Azure App Service](app-service-web/app-service-web-get-started-dotnet.md).</span></span>

## <a name="scripts-that-visual-studio-generates"></a><span data-ttu-id="f927a-123">Visual Studio 所產生的指令碼</span><span class="sxs-lookup"><span data-stu-id="f927a-123">Scripts that Visual Studio generates</span></span>
<span data-ttu-id="f927a-124">Visual Studio 會產生名為 **PublishScripts** 的方案層級資料夾，並內含兩個 Windows PowerShell 檔案，一個是用於虛擬機器或網站的發佈指令碼，一個是含有可在指令碼中使用之函式的模組。</span><span class="sxs-lookup"><span data-stu-id="f927a-124">Visual Studio generates a solution-level folder called **PublishScripts** that contains two Windows PowerShell files, a publish script for your virtual machine or website, and a module that contains functions that you can use in the scripts.</span></span> <span data-ttu-id="f927a-125">Visual Studio 也會產生 JSON 格式的檔案，以指定您要部署之專案的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f927a-125">Visual Studio also generates a file in the JSON format that specifies the details of the project you are deploying.</span></span>

### <a name="windows-powershell-publish-script"></a><span data-ttu-id="f927a-126">Windows PowerShell 發佈指令碼</span><span class="sxs-lookup"><span data-stu-id="f927a-126">Windows PowerShell publish script</span></span>
<span data-ttu-id="f927a-127">發佈指令碼含有部署至網站或虛擬機器的特定發佈步驟。</span><span class="sxs-lookup"><span data-stu-id="f927a-127">The publish script contains specific publish steps for deploying to a website or virtual machine.</span></span> <span data-ttu-id="f927a-128">Visual Studio 提供語法著色功能，可用來進行 Windows PowerShell 開發。</span><span class="sxs-lookup"><span data-stu-id="f927a-128">Visual Studio provides syntax coloring for Windows PowerShell development.</span></span> <span data-ttu-id="f927a-129">有提供函式說明，而且您可以自由編輯指令碼中的函式以符合您不斷變化的需求。</span><span class="sxs-lookup"><span data-stu-id="f927a-129">Help for the functions is available, and you can freely edit the functions in the script to suit your changing requirements.</span></span>

### <a name="windows-powershell-module"></a><span data-ttu-id="f927a-130">Windows PowerShell 模組</span><span class="sxs-lookup"><span data-stu-id="f927a-130">Windows PowerShell module</span></span>
<span data-ttu-id="f927a-131">Visual Studio 所產生的 Windows PowerShell 模組包含發佈指令碼所使用的函式。</span><span class="sxs-lookup"><span data-stu-id="f927a-131">The Windows PowerShell module that Visual Studio generates contains functions that the publish script uses.</span></span> <span data-ttu-id="f927a-132">這些都是 Azure PowerShell 函式，不可進行修改。</span><span class="sxs-lookup"><span data-stu-id="f927a-132">These are Azure PowerShell functions and are not intended to be modified.</span></span> <span data-ttu-id="f927a-133">如需詳細資訊，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview) 。</span><span class="sxs-lookup"><span data-stu-id="f927a-133">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>

### <a name="json-configuration-file"></a><span data-ttu-id="f927a-134">JSON 組態檔</span><span class="sxs-lookup"><span data-stu-id="f927a-134">JSON configuration file</span></span>
<span data-ttu-id="f927a-135">JSON 檔案建立在 [組態]  資料夾，其包含的組態資料可確切指定要部署至 Azure 的資源。</span><span class="sxs-lookup"><span data-stu-id="f927a-135">The JSON file is created in the **Configurations** folder and contains configuration data that specifies exactly which resources to deploy to Azure.</span></span> <span data-ttu-id="f927a-136">Visual Studio 所產生之檔案的名稱是 project-name-WAWS-dev.json (如果您建立網站) 或 project name-VM-dev.json (如果您建立虛擬機器)。</span><span class="sxs-lookup"><span data-stu-id="f927a-136">The name of the file that Visual Studio generates is project-name-WAWS-dev.json if you created a website, or project name-VM-dev.json if you created a virtual machine.</span></span> <span data-ttu-id="f927a-137">以下是建立網站時所產生之 JSON 組態檔的範例。</span><span class="sxs-lookup"><span data-stu-id="f927a-137">Here's an example of a JSON configuration file that's generated when you create a website.</span></span> <span data-ttu-id="f927a-138">其中大多數的值都簡單易懂。</span><span class="sxs-lookup"><span data-stu-id="f927a-138">Most of the values are self-explanatory.</span></span> <span data-ttu-id="f927a-139">網站名稱是由 Azure 產生，因此可能不符合您的專案名稱。</span><span class="sxs-lookup"><span data-stu-id="f927a-139">The website name is generated by Azure, so it might not match your project name.</span></span>

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
<span data-ttu-id="f927a-140">在建立虛擬機器時，JSON 組態檔看起來類似下面範例。</span><span class="sxs-lookup"><span data-stu-id="f927a-140">When you create a virtual machine, the JSON configuration file looks similar to the following.</span></span> <span data-ttu-id="f927a-141">請注意，雲端服務會建立為虛擬機器的容器。</span><span class="sxs-lookup"><span data-stu-id="f927a-141">Note that a cloud service is created as a container for the virtual machine.</span></span> <span data-ttu-id="f927a-142">虛擬機器包含用來透過 HTTP 和 HTTPS 進行 Web 存取的常用端點以及供 Web Deploy 使用的端點，後者可讓您從本機電腦、遠端桌面和 Windows PowerShell 發佈至網站。</span><span class="sxs-lookup"><span data-stu-id="f927a-142">The virtual machine contains the usual endpoints for web access through HTTP and HTTPS, as well as endpoints for Web Deploy, which lets you publish to the website from your local machine, Remote Desktop, and Windows PowerShell.</span></span>

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

<span data-ttu-id="f927a-143">您可以編輯 JSON 組態以變更執行發佈指令碼時會進行的作業。</span><span class="sxs-lookup"><span data-stu-id="f927a-143">You can edit the JSON configuration to change what happens when you run the publish scripts.</span></span> <span data-ttu-id="f927a-144">`cloudService` 和 `virtualMachine` 是必要區段，但如果您不需要 `databases` 區段，則可以將它刪除。</span><span class="sxs-lookup"><span data-stu-id="f927a-144">The `cloudService` and `virtualMachine` sections are required, but you can delete the `databases` section if you don't need it.</span></span> <span data-ttu-id="f927a-145">Visual Studio 所產生的預設組態檔中的空白屬性是選用屬性；預設組態檔中具有值的屬性則是必要屬性。</span><span class="sxs-lookup"><span data-stu-id="f927a-145">The properties that are empty in the default configuration file that Visual Studio generates are optional; those that have values in the default configuration file are required.</span></span>

<span data-ttu-id="f927a-146">如果您有內含多個部署環境 (稱為位置) 的網站而不是在 Azure 中的單一生產網站，您可以在 JSON 組態檔的網站名稱中加入位置名稱。</span><span class="sxs-lookup"><span data-stu-id="f927a-146">If you have a website that has multiple deployment environments (known as slots) instead of a single production site in Azure, you can include the slot name in the name of the website in the JSON configuration file.</span></span> <span data-ttu-id="f927a-147">例如，如果您擁有名為 **mysite** 的網站和名為 **test** 的位置，則 URI 是 mysite-test.cloudapp.net，但要在組態檔中使用的正確名稱是 mysite(test)。</span><span class="sxs-lookup"><span data-stu-id="f927a-147">For example, if you have a website that's named **mysite** and a slot for it named **test** then the URI is mysite-test.cloudapp.net, but the correct name to use in the configuration file is mysite(test).</span></span> <span data-ttu-id="f927a-148">只有在訂用帳戶中已存在網站和位置時才能這麼做。</span><span class="sxs-lookup"><span data-stu-id="f927a-148">You can only do this if the website and slots already exist in your subscription.</span></span> <span data-ttu-id="f927a-149">如果不存在，請執行指令碼 (不指定位置) 來建立網站，然後在 [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)中建立位置，之後再以修改過的網站名稱執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="f927a-149">If they don't exist, create the website by running the script without specifying the slot, then create the slot in the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), and thereafter run the script with the modified website name.</span></span> <span data-ttu-id="f927a-150">如需 Web 應用程式部署位置的詳細資訊，請參閱 [針對 Azure App Service 中的 Web 應用程式設定預備環境](app-service-web/web-sites-staged-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="f927a-150">For more information about deployment slots for web apps, see [Set up staging environments for web apps in Azure App Service](app-service-web/web-sites-staged-publishing.md).</span></span>

## <a name="how-to-run-the-publish-scripts"></a><span data-ttu-id="f927a-151">如何執行發佈指令碼</span><span class="sxs-lookup"><span data-stu-id="f927a-151">How to run the publish scripts</span></span>
<span data-ttu-id="f927a-152">如果您之前未曾執行過 Windows PowerShell 指令碼，您必須先設定執行原則以啟用要執行的指令碼。</span><span class="sxs-lookup"><span data-stu-id="f927a-152">If you have never run a Windows PowerShell script before, you must first set the execution policy to enable scripts to run.</span></span> <span data-ttu-id="f927a-153">如果 Windows PowerShell 指令碼容易受到涉及執行指令碼的惡意程式碼或病毒的威脅，這項安全性功能可防止使用者執行 Windows PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="f927a-153">This is a security feature to prevent users from running Windows PowerShell scripts if they're vulnerable to malware or viruses that involve executing scripts.</span></span>

### <a name="run-the-script"></a><span data-ttu-id="f927a-154">執行指令碼</span><span class="sxs-lookup"><span data-stu-id="f927a-154">Run the script</span></span>
1. <span data-ttu-id="f927a-155">建立專案的 Web Deploy 封裝。</span><span class="sxs-lookup"><span data-stu-id="f927a-155">Create the Web Deploy package for your project.</span></span> <span data-ttu-id="f927a-156">Web Deploy 封裝是經過壓縮的封存檔 (.zip 檔案)，內含您想要複製到網站或虛擬機器的檔案。</span><span class="sxs-lookup"><span data-stu-id="f927a-156">A Web Deploy package is a compressed archive (.zip file) that contain files that you want to copy to your website or virtual machine.</span></span> <span data-ttu-id="f927a-157">您可以在 Visual Studio 中為任何 Web 應用程式建立 Web Deploy 封裝。</span><span class="sxs-lookup"><span data-stu-id="f927a-157">You can create Web Deploy packages in Visual Studio for any web application.</span></span>

![建立 Web Deploy 封裝](./media/vs-azure-tools-publishing-using-powershell-scripts/IC767885.png)

<span data-ttu-id="f927a-159">如需詳細資訊，請參閱 [如何：在 Visual Studio 中建立 Web 部署封裝](https://msdn.microsoft.com/library/dd465323.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f927a-159">For more information, see [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span></span> <span data-ttu-id="f927a-160">您也可以自動建立 Web Deploy 封裝，如本主題稍後的＜自訂和擴充發佈指令碼＞  一節所述。</span><span class="sxs-lookup"><span data-stu-id="f927a-160">You can also automate the creation of your Web Deploy package, as described in the section **Customizing and extending the publish scripts** later in this topic.</span></span>

1. <span data-ttu-id="f927a-161">在 [方案總管] 中，開啟指令碼的內容功能表，然後選擇 [以 PowerShell ISE 開啟]。</span><span class="sxs-lookup"><span data-stu-id="f927a-161">In **Solution Explorer**, open the context menu for the script, and then choose **Open with PowerShell ISE**.</span></span>
2. <span data-ttu-id="f927a-162">如果這是您第一次在此電腦上執行 Windows PowerShell 指令碼，請以系統管理員權限開啟命令提示字元視窗，並輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="f927a-162">If this is the first time you've run Windows PowerShell scripts on this computer, open a command prompt window with Administrator privileges and type the following command:</span></span>

    ```powershell
    Set-ExecutionPolicy RemoteSigned
    ```

3. <span data-ttu-id="f927a-163">使用下列命令登入 Azure。</span><span class="sxs-lookup"><span data-stu-id="f927a-163">Sign in to Azure by using the following command.</span></span>

    ```powershell
    Add-AzureAccount
    ```

    <span data-ttu-id="f927a-164">出現提示時，提供您的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="f927a-164">When prompted, supply your username and password.</span></span>

    <span data-ttu-id="f927a-165">請注意，當您自動執行指令碼時，這個提供 Azure 認證的方法將沒有作用。</span><span class="sxs-lookup"><span data-stu-id="f927a-165">Note that when you automate the script, this method of providing Azure credentials won't work.</span></span> <span data-ttu-id="f927a-166">您應該改用 .publishsettings 檔案來提供認證。</span><span class="sxs-lookup"><span data-stu-id="f927a-166">Instead, you should use the .publishsettings file to provide credentials.</span></span> <span data-ttu-id="f927a-167">請使用 **Get-AzurePublishSettingsFile** 命令從 Azure 下載檔案，之後使用 **Import-AzurePublishSettingsFile** 匯入檔案 (此程序只需執行一次)。</span><span class="sxs-lookup"><span data-stu-id="f927a-167">One time only, you use the command **Get-AzurePublishSettingsFile** to download the file from Azure, and thereafter use **Import-AzurePublishSettingsFile** to import the file.</span></span> <span data-ttu-id="f927a-168">如需詳細指示，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="f927a-168">For detailed instructions, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

4. <span data-ttu-id="f927a-169">(選用) 如果您想要建立虛擬機器、資料庫和網站等 Azure 資源，而不要發佈 Web 應用程式，請使用 **Publish-WebApplication.ps1** 命令搭配設定為 JSON 組態檔的 **-Configuration** 引數。</span><span class="sxs-lookup"><span data-stu-id="f927a-169">(Optional) If you want to create Azure resources such as the virtual machine, database, and website without publishing your web application, use the **Publish-WebApplication.ps1** command with the **-Configuration** argument set to the JSON configuration file.</span></span> <span data-ttu-id="f927a-170">此命令列使用 JSON 組態檔來決定要建立哪些資源。</span><span class="sxs-lookup"><span data-stu-id="f927a-170">This command line uses the JSON configuration file to determine which resources to create.</span></span> <span data-ttu-id="f927a-171">因為它使用其他命令列引數的預設設定，所以會建立資源，但不會發佈 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f927a-171">Because it uses the default settings for other command-line arguments, it creates the resources, but doesn't publish your web application.</span></span> <span data-ttu-id="f927a-172">–Verbose 選項可讓您進一步了解會發生什麼事。</span><span class="sxs-lookup"><span data-stu-id="f927a-172">The –Verbose option gives you more information about what's happening.</span></span>

    ```powershell
    Publish-WebApplication.ps1 -Verbose –Configuration C:\Path\WebProject-WAWS-dev.json
    ```

5. <span data-ttu-id="f927a-173">如下列其中一個範例所示使用 **Publish-WebApplication.ps1** 命令叫用指令碼並發佈 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f927a-173">Use the **Publish-WebApplication.ps1** command as shown in one of the following examples to invoke the script and publish your web application.</span></span> <span data-ttu-id="f927a-174">如果您需要覆寫任何其他引數的預設設定，例如訂用帳戶名稱、發佈封裝名稱、虛擬機器認證或資料庫伺服器認證，可以指定這些參數。</span><span class="sxs-lookup"><span data-stu-id="f927a-174">If you need to override the default settings for any of the other arguments, such as the subscription name, publish package name, virtual machine credentials, or database server credentials, you can specify those parameters.</span></span> <span data-ttu-id="f927a-175">使用 **–Verbose** 選項可檢視發佈程序進度的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f927a-175">Use the **–Verbose** option to see more information about the progress of the publishing process.</span></span>

    ```powershell
    Publish-WebApplication.ps1 –Configuration C:\Path\WebProject-WAWS-dev-json `
    –SubscriptionName Contoso `
    -WebDeployPackage C:\Documents\Azure\ADWebApp.zip `
    -DatabaseServerPassword @{Name="dbServerName";Password="adminPassword"} `
    -Verbose
    ```

    <span data-ttu-id="f927a-176">如果您要建立虛擬機器，其命令如下所示。</span><span class="sxs-lookup"><span data-stu-id="f927a-176">If you're creating a virtual machine, the command looks like the following.</span></span> <span data-ttu-id="f927a-177">此範例也顯示如何指定多個資料庫的認證。</span><span class="sxs-lookup"><span data-stu-id="f927a-177">This example also shows how to specify the credentials for multiple databases.</span></span> <span data-ttu-id="f927a-178">針對這些指令碼所建立的虛擬機器，其 SSL 憑證不是來自受信任的根授權單位。</span><span class="sxs-lookup"><span data-stu-id="f927a-178">For the virtual machines that these scripts create, the SSL certificate is not from a trusted root authority.</span></span> <span data-ttu-id="f927a-179">因此，您需要使用 **–AllowUntrusted** 選項。</span><span class="sxs-lookup"><span data-stu-id="f927a-179">Therefore, you need to use the **–AllowUntrusted** option.</span></span>

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

    <span data-ttu-id="f927a-180">指令碼可以建立資料庫，但不會建立資料庫伺服器。</span><span class="sxs-lookup"><span data-stu-id="f927a-180">The script can create databases, but it doesn't create database servers.</span></span> <span data-ttu-id="f927a-181">如果您想要建立資料庫伺服器，您可以使用 Azure 模組中的 **New-AzureSqlDatabaseServer** 函式。</span><span class="sxs-lookup"><span data-stu-id="f927a-181">If you want to create a database server, you can use the **New-AzureSqlDatabaseServer** function in the Azure module.</span></span>

## <a name="customizing-and-extending-the-publish-scripts"></a><span data-ttu-id="f927a-182">自訂和擴充發佈指令碼</span><span class="sxs-lookup"><span data-stu-id="f927a-182">Customizing and extending the publish scripts</span></span>
<span data-ttu-id="f927a-183">您可以自訂發佈指令碼和 JSON 組態檔。</span><span class="sxs-lookup"><span data-stu-id="f927a-183">You can customize the publish script and JSON configuration file.</span></span> <span data-ttu-id="f927a-184">Windows PowerShell 模組 **AzureWebAppPublishModule.psm1** 中的函式不可進行修改。</span><span class="sxs-lookup"><span data-stu-id="f927a-184">The functions in the Windows PowerShell module **AzureWebAppPublishModule.psm1** are not intended to be modified.</span></span> <span data-ttu-id="f927a-185">如果您想要指定不同的資料庫或變更虛擬機器的某些屬性，請編輯 JSON 組態檔。</span><span class="sxs-lookup"><span data-stu-id="f927a-185">If you just want to specify a different database or change some of the properties of the virtual machine, edit the JSON configuration file.</span></span> <span data-ttu-id="f927a-186">如果您想要擴充指令碼的功能來自動建置和測試專案，您可以在 **Publish-WebApplication.ps1**中實作函式虛設常式。</span><span class="sxs-lookup"><span data-stu-id="f927a-186">If you want to extend the functionality of the script to automate building and testing your project, you can implement function stubs in **Publish-WebApplication.ps1**.</span></span>

<span data-ttu-id="f927a-187">若要自動建置專案，請將呼叫 MSBuild 的程式碼加入 `New-WebDeployPackage` ，如此程式碼範例所示。</span><span class="sxs-lookup"><span data-stu-id="f927a-187">To automate building your project, add code that calls MSBuild to `New-WebDeployPackage` as shown in this code example.</span></span> <span data-ttu-id="f927a-188">MSBuild 命令的路徑會因為您所安裝的 Visual Studio 版本而有所不同。</span><span class="sxs-lookup"><span data-stu-id="f927a-188">The path to the MSBuild command is different depending on the version of Visual Studio you have installed.</span></span> <span data-ttu-id="f927a-189">若要取得正確路徑，您可以使用函式 **Get-MSBuildCmd**，如此範例所示。</span><span class="sxs-lookup"><span data-stu-id="f927a-189">To get the correct path, you can use the function **Get-MSBuildCmd**, as shown in this example.</span></span>

### <a name="to-automate-building-your-project"></a><span data-ttu-id="f927a-190">自動建置專案</span><span class="sxs-lookup"><span data-stu-id="f927a-190">To automate building your project</span></span>
1. <span data-ttu-id="f927a-191">在全域參數區段新增 `$ProjectFile` 參數。</span><span class="sxs-lookup"><span data-stu-id="f927a-191">Add the `$ProjectFile` parameter in the global param section.</span></span>

    ```powershell
    [Parameter(Mandatory = $false)]
    [ValidateScript({Test-Path $_ -PathType Leaf})]
    [String]
    $ProjectFile,
    ```

2. <span data-ttu-id="f927a-192">將函式 `Get-MSBuildCmd` 複製到指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="f927a-192">Copy the function `Get-MSBuildCmd` into your script file.</span></span>

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

3. <span data-ttu-id="f927a-193">以下列程式碼取代 `New-WebDeployPackage`，並取代建構 `$msbuildCmd` 的程式行中的預留位置。</span><span class="sxs-lookup"><span data-stu-id="f927a-193">Replace `New-WebDeployPackage` with the following code and replace the placeholders in the line constructing `$msbuildCmd`.</span></span> <span data-ttu-id="f927a-194">此程式碼係用於 Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="f927a-194">This code is for Visual Studio 2015.</span></span> <span data-ttu-id="f927a-195">如果您使用的是 Visual Studio 2013，請將下面的 **VisualStudioVersion** 屬性變更為 `12.0`。</span><span class="sxs-lookup"><span data-stu-id="f927a-195">If you're using Visual Studio 2013, change the **VisualStudioVersion** property below to `12.0`.</span></span>

    ```powershell
    function New-WebDeployPackage
    {
        #Write a function to build and package your web application
    ```

    <span data-ttu-id="f927a-196">若要建置 Web 應用程式，使用 MsBuild.exe。</span><span class="sxs-lookup"><span data-stu-id="f927a-196">To build your web application, use MsBuild.exe.</span></span> <span data-ttu-id="f927a-197">如需協助，請參閱 MSBuild 命令列參考︰[http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)</span><span class="sxs-lookup"><span data-stu-id="f927a-197">For help, see MSBuild Command-Line Reference at: [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)</span></span>

    ```powershell
    Write-VerboseWithTime 'Build-WebDeployPackage: Start'

    $msbuildCmd = '"{0}" "{1}" /T:Rebuild;Package /P:VisualStudioVersion=14.0 /p:OutputPath="{2}\MSBuildOutputPath" /flp:logfile=msbuild.log,v=d' -f (Get-MSBuildCmd), $ProjectFile, $scriptDirectory

    Write-VerboseWithTime ('Build-WebDeployPackage: ' + $msbuildCmd)
    ```

### <a name="start-execution-of-the-build-command"></a><span data-ttu-id="f927a-198">開始執行建置命令</span><span class="sxs-lookup"><span data-stu-id="f927a-198">Start execution of the build command</span></span>

```powershell
$job = Start-Process cmd.exe -ArgumentList('/C "' + $msbuildCmd + '"') -WindowStyle Normal -Wait -PassThru

if ($job.ExitCode -ne 0) {
    throw('MsBuild exited with an error. ExitCode:' + $job.ExitCode)
}

#Obtain the project name
$projectName = (Get-Item $ProjectFile).BaseName

#Construct the path to web deploy zip package
$DeployPackageDir =  '.\MSBuildOutputPath\_PublishedWebsites\{0}_Package\{0}.zip' -f $projectName

#Get the full path for the web deploy zip package. This is required for MSDeploy to work
$WebDeployPackage = Resolve-Path –LiteralPath $DeployPackageDir

Write-VerboseWithTime 'Build-WebDeployPackage: End'

return $WebDeployPackage
}
```

1. <span data-ttu-id="f927a-199">在此程式行前呼叫 `New-WebDeployPackage` 函式：`$Config = Read-ConfigFile $Configuration` (若為 Web 應用程式) 或 `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` (若為虛擬機器)。</span><span class="sxs-lookup"><span data-stu-id="f927a-199">Call the `New-WebDeployPackage` function before this line: `$Config = Read-ConfigFile $Configuration` for web apps or `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` for virtual machines.</span></span>

    ```powershell
    if($ProjectFile)
    {
    $WebDeployPackage = New-WebDeployPackage
    }
    ```

2. <span data-ttu-id="f927a-200">從命令列使用傳遞 `$Project` 引數叫用自訂指令碼，如下列範例的命令列所示。</span><span class="sxs-lookup"><span data-stu-id="f927a-200">Invoke the customized script from command line using passing the `$Project` argument, as in the following example command line.</span></span>

    ```powershell
    .\Publish-WebApplicationVM.ps1 -Configuration .\Configurations\WebApplication5-VM-dev.json `
    -ProjectFile ..\WebApplication5\WebApplication5.csproj `
    -VMPassword @{Name="VMUser";Password="Test.123"} `
    -AllowUntrusted `
    -Verbose
    ```

    <span data-ttu-id="f927a-201">若要自動測試應用程式，請將程式碼加入 `Test-WebApplication`。</span><span class="sxs-lookup"><span data-stu-id="f927a-201">To automate testing of your application, add code to `Test-WebApplication`.</span></span> <span data-ttu-id="f927a-202">請務必要將 **Publish-WebApplication.ps1** 中呼叫這些函式的程式行取消註解。</span><span class="sxs-lookup"><span data-stu-id="f927a-202">Be sure to uncomment the lines in **Publish-WebApplication.ps1** where these functions are called.</span></span> <span data-ttu-id="f927a-203">如果您沒有提供實作，您可以使用 Visual Studio 手動建置專案，然後執行發佈指令碼以發佈至 Azure。</span><span class="sxs-lookup"><span data-stu-id="f927a-203">If you don't provide an implementation, you can manually build your project with Visual Studio, and then run the publish script to publish to Azure.</span></span>

## <a name="publishing-function-summary"></a><span data-ttu-id="f927a-204">發佈函式摘要</span><span class="sxs-lookup"><span data-stu-id="f927a-204">Publishing function summary</span></span>
<span data-ttu-id="f927a-205">若要取得可以在 Windows PowerShell 命令提示字元使用之函式的說明，請使用 `Get-Help function-name`命令。</span><span class="sxs-lookup"><span data-stu-id="f927a-205">To get help for functions you can use at the Windows PowerShell command prompt, use the command `Get-Help function-name`.</span></span> <span data-ttu-id="f927a-206">說明中會包括參數說明和範例。</span><span class="sxs-lookup"><span data-stu-id="f927a-206">The help includes parameter help and examples.</span></span> <span data-ttu-id="f927a-207">**AzureWebAppPublishModule.psm1** 和 **Publish-WebApplication.ps1** 指令碼原始程式檔中也有相同的說明文字 。</span><span class="sxs-lookup"><span data-stu-id="f927a-207">The same help text is also in the script source files, **AzureWebAppPublishModule.psm1** and **Publish-WebApplication.ps1**.</span></span> <span data-ttu-id="f927a-208">指令碼和說明都已當地語系化為 Visual Studio 所使用的語言。</span><span class="sxs-lookup"><span data-stu-id="f927a-208">The script and help are localized in your Visual Studio language.</span></span>

<span data-ttu-id="f927a-209">**AzureWebAppPublishModule**</span><span class="sxs-lookup"><span data-stu-id="f927a-209">**AzureWebAppPublishModule**</span></span>

| <span data-ttu-id="f927a-210">函式名稱</span><span class="sxs-lookup"><span data-stu-id="f927a-210">Function name</span></span> | <span data-ttu-id="f927a-211">說明</span><span class="sxs-lookup"><span data-stu-id="f927a-211">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f927a-212">Add-AzureSQLDatabase</span><span class="sxs-lookup"><span data-stu-id="f927a-212">Add-AzureSQLDatabase</span></span> |<span data-ttu-id="f927a-213">建立新的 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="f927a-213">Creates a new Azure SQL database.</span></span> |
| <span data-ttu-id="f927a-214">Add-AzureSQLDatabases</span><span class="sxs-lookup"><span data-stu-id="f927a-214">Add-AzureSQLDatabases</span></span> |<span data-ttu-id="f927a-215">從 Visual Studio 所產生的 JSON 組態檔中的值建立 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="f927a-215">Creates Azure SQL databases from the values in the JSON configuration file that Visual Studio generates.</span></span> |
| <span data-ttu-id="f927a-216">Add-AzureVM</span><span class="sxs-lookup"><span data-stu-id="f927a-216">Add-AzureVM</span></span> |<span data-ttu-id="f927a-217">建立 Azure 虛擬機器並傳回所部署 VM 的 URL。</span><span class="sxs-lookup"><span data-stu-id="f927a-217">Creates a Azure virtual machine and returns the URL of the deployed VM.</span></span> <span data-ttu-id="f927a-218">函式會設定必要條件，然後呼叫 **New-AzureVM** 函式 (Azure 模組) 以建立新的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f927a-218">The function sets up the prerequisites and then calls the **New-AzureVM** function (Azure module) to create a new virtual machine.</span></span> |
| <span data-ttu-id="f927a-219">Add-AzureVMEndpoints</span><span class="sxs-lookup"><span data-stu-id="f927a-219">Add-AzureVMEndpoints</span></span> |<span data-ttu-id="f927a-220">將新的輸入端點加入至虛擬機器，並傳回具有新端點的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f927a-220">Adds new input endpoints to a virtual machine and returns the virtual machine with the new endpoint.</span></span> |
| <span data-ttu-id="f927a-221">Add-AzureVMStorage</span><span class="sxs-lookup"><span data-stu-id="f927a-221">Add-AzureVMStorage</span></span> |<span data-ttu-id="f927a-222">在目前的訂用帳戶中建立新的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f927a-222">Creates a new Azure storage account in the current subscription.</span></span> <span data-ttu-id="f927a-223">帳戶名稱開頭是 "devtest"，後面接著唯一的英數字元字串。</span><span class="sxs-lookup"><span data-stu-id="f927a-223">The name of the account begins with "devtest" followed by a unique alphanumeric string.</span></span> <span data-ttu-id="f927a-224">此函式會傳回新儲存體帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="f927a-224">The function returns the name of the new storage account.</span></span> <span data-ttu-id="f927a-225">您必須指定新儲存體帳戶的位置或同質群組。</span><span class="sxs-lookup"><span data-stu-id="f927a-225">You must specify either a location or an affinity group for the new storage account.</span></span> |
| <span data-ttu-id="f927a-226">Add-AzureWebsite</span><span class="sxs-lookup"><span data-stu-id="f927a-226">Add-AzureWebsite</span></span> |<span data-ttu-id="f927a-227">使用指定的名稱和位置建立網站。</span><span class="sxs-lookup"><span data-stu-id="f927a-227">Creates a website with the specified name and location.</span></span> <span data-ttu-id="f927a-228">此函式會呼叫 Azure 模組中的 **New-AzureWebsite** 函式。</span><span class="sxs-lookup"><span data-stu-id="f927a-228">This function calls the **New-AzureWebsite** function in the Azure module.</span></span> <span data-ttu-id="f927a-229">如果訂用帳戶還沒有具有指定名稱的網站，此函式會建立該網站並傳回網站物件。</span><span class="sxs-lookup"><span data-stu-id="f927a-229">If the subscription doesn't already include a website with the specified name, this function creates the website and returns a website object.</span></span> <span data-ttu-id="f927a-230">否則，它會傳回 `$null`。</span><span class="sxs-lookup"><span data-stu-id="f927a-230">Otherwise, it returns `$null`.</span></span> |
| <span data-ttu-id="f927a-231">Backup-Subscription</span><span class="sxs-lookup"><span data-stu-id="f927a-231">Backup-Subscription</span></span> |<span data-ttu-id="f927a-232">在指令碼範圍的 `$Script:originalSubscription` 變數中儲存目前的 Azure 訂用帳戶。此函式會在指令碼範圍中，儲存目前的 Azure 訂用帳戶 (由 `Get-AzureSubscription -Current` 取得) 與其儲存體帳戶，以及此指令碼所變更的訂用帳戶 (儲存在 `$UserSpecifiedSubscription` 變數中) 與其儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f927a-232">Saves the current Azure subscription in the `$Script:originalSubscription` variable in script scope.This function saves the current Azure subscription (as obtained by `Get-AzureSubscription -Current`) and its storage account, and the subscription that is changed by this script (stored in the variable `$UserSpecifiedSubscription`) and its storage account, in script scope.</span></span> <span data-ttu-id="f927a-233">透過儲存這些值，您可以使用函式 (例如 `Restore-Subscription`) 將原始的目前訂用帳戶和儲存體帳戶還原為目前狀態 (如果目前狀態已變更)。</span><span class="sxs-lookup"><span data-stu-id="f927a-233">By saving the values, you can use a function, such as `Restore-Subscription`, to restore the original current subscription and storage account to current status if the current status has changed.</span></span> |
| <span data-ttu-id="f927a-234">Find-AzureVM</span><span class="sxs-lookup"><span data-stu-id="f927a-234">Find-AzureVM</span></span> |<span data-ttu-id="f927a-235">取得指定的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f927a-235">Gets the specified Azure virtual machine.</span></span> |
| <span data-ttu-id="f927a-236">Format-DevTestMessageWithTime</span><span class="sxs-lookup"><span data-stu-id="f927a-236">Format-DevTestMessageWithTime</span></span> |<span data-ttu-id="f927a-237">在訊息前面加上日期和時間。</span><span class="sxs-lookup"><span data-stu-id="f927a-237">Prepends the date and time to a message.</span></span> <span data-ttu-id="f927a-238">此函式是專為寫入 Error 和 Verbose 串流的訊息所設計。</span><span class="sxs-lookup"><span data-stu-id="f927a-238">This function is designed for messages written to the Error and Verbose streams.</span></span> |
| <span data-ttu-id="f927a-239">Get-AzureSQLDatabaseConnectionString</span><span class="sxs-lookup"><span data-stu-id="f927a-239">Get-AzureSQLDatabaseConnectionString</span></span> |<span data-ttu-id="f927a-240">組合連接字串來連線到 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="f927a-240">Assembles a connection string to connect to an Azure SQL database.</span></span> |
| <span data-ttu-id="f927a-241">Get-AzureVMStorage</span><span class="sxs-lookup"><span data-stu-id="f927a-241">Get-AzureVMStorage</span></span> |<span data-ttu-id="f927a-242">傳回指定位置或同質群組中具有 "devtest*" (不區分大小寫) 名稱模式的第一個儲存體帳戶的名稱。如果 "devtest*" 儲存體帳戶不符合位置或同質群組，此函式會忽略它。</span><span class="sxs-lookup"><span data-stu-id="f927a-242">Returns the name of the first storage account with the name pattern "devtest*" (case insensitive) in the specified location or affinity group. If the "devtest*" storage account doesn't match the location or affinity group, the function ignores it.</span></span> <span data-ttu-id="f927a-243">您必須指定位置或同質群組。</span><span class="sxs-lookup"><span data-stu-id="f927a-243">You must specify either a location or an affinity group.</span></span> |
| <span data-ttu-id="f927a-244">Get-MSDeployCmd</span><span class="sxs-lookup"><span data-stu-id="f927a-244">Get-MSDeployCmd</span></span> |<span data-ttu-id="f927a-245">傳回執行 MsDeploy.exe 工具的命令。</span><span class="sxs-lookup"><span data-stu-id="f927a-245">Returns a command to run the MsDeploy.exe tool.</span></span> |
| <span data-ttu-id="f927a-246">New-AzureVMEnvironment</span><span class="sxs-lookup"><span data-stu-id="f927a-246">New-AzureVMEnvironment</span></span> |<span data-ttu-id="f927a-247">在訂用帳戶中尋找或建立符合 JSON 組態檔中的值的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f927a-247">Finds or creates a virtual machine in the subscription that matches the values in the JSON configuration file.</span></span> |
| <span data-ttu-id="f927a-248">Publish-WebPackage</span><span class="sxs-lookup"><span data-stu-id="f927a-248">Publish-WebPackage</span></span> |<span data-ttu-id="f927a-249">使用 MsDeploy.exe 和 Web 發佈封裝 .Zip 檔案將資源部署至網站。</span><span class="sxs-lookup"><span data-stu-id="f927a-249">Uses MsDeploy.exe and a web publish package .Zip file to deploy resources to a website.</span></span> <span data-ttu-id="f927a-250">此函式不會產生任何輸出。</span><span class="sxs-lookup"><span data-stu-id="f927a-250">This function doesn't generate any output.</span></span> <span data-ttu-id="f927a-251">如果呼叫 MSDeploy.exe 失敗，此函式會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="f927a-251">If the call to MSDeploy.exe fails, the function throws an exception.</span></span> <span data-ttu-id="f927a-252">若要取得更詳細的輸出，請使用 **-Verbose** 選項。</span><span class="sxs-lookup"><span data-stu-id="f927a-252">To get more detailed output, use the **-Verbose** option.</span></span> |
| <span data-ttu-id="f927a-253">Publish-WebPackageToVM</span><span class="sxs-lookup"><span data-stu-id="f927a-253">Publish-WebPackageToVM</span></span> |<span data-ttu-id="f927a-254">驗證參數值，然後呼叫 **Publish-WebPackage** 函式。</span><span class="sxs-lookup"><span data-stu-id="f927a-254">Verifies the parameter values, and then calls the **Publish-WebPackage** function.</span></span> |
| <span data-ttu-id="f927a-255">Read-ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f927a-255">Read-ConfigFile</span></span> |<span data-ttu-id="f927a-256">驗證 JSON 組態檔並傳回所選值的雜湊資料表。</span><span class="sxs-lookup"><span data-stu-id="f927a-256">Validates the JSON configuration file and returns a hash table of selected values.</span></span> |
| <span data-ttu-id="f927a-257">Restore-Subscription</span><span class="sxs-lookup"><span data-stu-id="f927a-257">Restore-Subscription</span></span> |<span data-ttu-id="f927a-258">將目前的訂用帳戶重設為原始訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f927a-258">Resets the current subscription to the original subscription.</span></span> |
| <span data-ttu-id="f927a-259">Test-AzureModule</span><span class="sxs-lookup"><span data-stu-id="f927a-259">Test-AzureModule</span></span> |<span data-ttu-id="f927a-260">如果所安裝的 Azure 模組版本為 0.7.4 或更新版本，則傳回 `$true` 。</span><span class="sxs-lookup"><span data-stu-id="f927a-260">Returns `$true` if the installed Azure module version is 0.7.4 or later.</span></span> <span data-ttu-id="f927a-261">如果尚未安裝模組或模組為較舊的版本，則傳回 `$false` 。</span><span class="sxs-lookup"><span data-stu-id="f927a-261">Returns `$false` if the module isn't installed or is an earlier version.</span></span> <span data-ttu-id="f927a-262">此函式沒有參數。</span><span class="sxs-lookup"><span data-stu-id="f927a-262">This function has no parameters.</span></span> |
| <span data-ttu-id="f927a-263">Test-AzureModuleVersion</span><span class="sxs-lookup"><span data-stu-id="f927a-263">Test-AzureModuleVersion</span></span> |<span data-ttu-id="f927a-264">如果 Azure 模組的版本為 0.7.4 或更新版本，則傳回 `$true` 。</span><span class="sxs-lookup"><span data-stu-id="f927a-264">Returns `$true` if the version of the Azure module is 0.7.4 or later.</span></span> <span data-ttu-id="f927a-265">如果尚未安裝模組或模組為較舊的版本，則傳回 `$false` 。</span><span class="sxs-lookup"><span data-stu-id="f927a-265">Returns `$false` if the module isn't installed or is an earlier version.</span></span> <span data-ttu-id="f927a-266">此函式沒有參數。</span><span class="sxs-lookup"><span data-stu-id="f927a-266">This function has no parameters.</span></span> |
| <span data-ttu-id="f927a-267">Test-HttpsUrl</span><span class="sxs-lookup"><span data-stu-id="f927a-267">Test-HttpsUrl</span></span> |<span data-ttu-id="f927a-268">將輸入的 URL 轉換為 System.Uri 物件。</span><span class="sxs-lookup"><span data-stu-id="f927a-268">Converts the input URL to a System.Uri object.</span></span> <span data-ttu-id="f927a-269">如果 URL 為絕對值，而且其配置為 https，則傳回 `$True` 。</span><span class="sxs-lookup"><span data-stu-id="f927a-269">Returns `$True` if the URL is absolute and its scheme is https.</span></span> <span data-ttu-id="f927a-270">如果 URL 是相對值、其配置不是 HTTPS 或輸入的字串無法轉換成 URL，則傳回 `$false` 。</span><span class="sxs-lookup"><span data-stu-id="f927a-270">Returns `$false` if the URL is relative, its scheme isn't HTTPS, or the input string can't be converted to a URL.</span></span> |
| <span data-ttu-id="f927a-271">Test-Member</span><span class="sxs-lookup"><span data-stu-id="f927a-271">Test-Member</span></span> |<span data-ttu-id="f927a-272">如果屬性或方法是物件的成員，則傳回 `$true` 。</span><span class="sxs-lookup"><span data-stu-id="f927a-272">Returns `$true` if a property or method is a member of the object.</span></span> <span data-ttu-id="f927a-273">否則傳回 `$false`。</span><span class="sxs-lookup"><span data-stu-id="f927a-273">Otherwise, returns `$false`.</span></span> |
| <span data-ttu-id="f927a-274">Write-ErrorWithTime</span><span class="sxs-lookup"><span data-stu-id="f927a-274">Write-ErrorWithTime</span></span> |<span data-ttu-id="f927a-275">寫入前面會加上目前時間的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="f927a-275">Writes an error message prefixed with the current time.</span></span> <span data-ttu-id="f927a-276">此函式會呼叫 **Format-DevTestMessageWithTime** 函式，以在將訊息寫入 Error 串流之前在訊息前面加上時間。</span><span class="sxs-lookup"><span data-stu-id="f927a-276">This function calls the **Format-DevTestMessageWithTime** function to prepend the time before writing the message to the Error stream.</span></span> |
| <span data-ttu-id="f927a-277">Write-HostWithTime</span><span class="sxs-lookup"><span data-stu-id="f927a-277">Write-HostWithTime</span></span> |<span data-ttu-id="f927a-278">將前面會加上目前時間的訊息寫入主機程式 (**Write-Host**)。</span><span class="sxs-lookup"><span data-stu-id="f927a-278">Writes a message to the host program (**Write-Host**) prefixed with the current time.</span></span> <span data-ttu-id="f927a-279">寫入主機程式的效果並不一定。</span><span class="sxs-lookup"><span data-stu-id="f927a-279">The effect of writing to the host program varies.</span></span> <span data-ttu-id="f927a-280">大部分裝載 Windows PowerShell 的程式會將這些訊息寫入標準輸出。</span><span class="sxs-lookup"><span data-stu-id="f927a-280">Most programs that host Windows PowerShell write these messages to standard output.</span></span> |
| <span data-ttu-id="f927a-281">Write-VerboseWithTime</span><span class="sxs-lookup"><span data-stu-id="f927a-281">Write-VerboseWithTime</span></span> |<span data-ttu-id="f927a-282">寫入前面會加上目前時間的詳細資訊訊息。</span><span class="sxs-lookup"><span data-stu-id="f927a-282">Writes a verbose message prefixed with the current time.</span></span> <span data-ttu-id="f927a-283">它會呼叫 **Write-Verbose**，所以只有當指令碼搭配 **Verbose** 參數執行或當 [VerbosePreference] 喜好設定設為 [繼續] 時，才會顯示訊息。</span><span class="sxs-lookup"><span data-stu-id="f927a-283">Because it calls **Write-Verbose**, the message displays only when the script runs with the **Verbose** parameter or when the **VerbosePreference** preference is set to **Continue**.</span></span> |

<span data-ttu-id="f927a-284">**Publish-WebApplication**</span><span class="sxs-lookup"><span data-stu-id="f927a-284">**Publish-WebApplication**</span></span>

| <span data-ttu-id="f927a-285">函式名稱</span><span class="sxs-lookup"><span data-stu-id="f927a-285">Function name</span></span> | <span data-ttu-id="f927a-286">說明</span><span class="sxs-lookup"><span data-stu-id="f927a-286">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f927a-287">New-AzureWebApplicationEnvironment</span><span class="sxs-lookup"><span data-stu-id="f927a-287">New-AzureWebApplicationEnvironment</span></span> |<span data-ttu-id="f927a-288">建立 Azure 資源，例如網站或虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f927a-288">Creates Azure resources, such as a website or virtual machine.</span></span> |
| <span data-ttu-id="f927a-289">New-WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="f927a-289">New-WebDeployPackage</span></span> |<span data-ttu-id="f927a-290">此函式未實作。</span><span class="sxs-lookup"><span data-stu-id="f927a-290">This function isn't implemented.</span></span> <span data-ttu-id="f927a-291">您可以在此函式新增命令來建置專案。</span><span class="sxs-lookup"><span data-stu-id="f927a-291">You can add commands in this function to build your project.</span></span> |
| <span data-ttu-id="f927a-292">Publish-AzureWebApplication</span><span class="sxs-lookup"><span data-stu-id="f927a-292">Publish-AzureWebApplication</span></span> |<span data-ttu-id="f927a-293">將 Web 應用程式發佈至 Azure。</span><span class="sxs-lookup"><span data-stu-id="f927a-293">Publishes a web application to Azure.</span></span> |
| <span data-ttu-id="f927a-294">Publish-WebApplication</span><span class="sxs-lookup"><span data-stu-id="f927a-294">Publish-WebApplication</span></span> |<span data-ttu-id="f927a-295">建立並部署 Visual Studio Web 專案的 Web Apps、虛擬機器、SQL Database 和儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f927a-295">Creates and deploys Web Apps, virtual machines, SQL databases, and storage accounts for a Visual Studio web project.</span></span> |
| <span data-ttu-id="f927a-296">Test-WebApplication</span><span class="sxs-lookup"><span data-stu-id="f927a-296">Test-WebApplication</span></span> |<span data-ttu-id="f927a-297">此函式未實作。</span><span class="sxs-lookup"><span data-stu-id="f927a-297">This function isn't implemented.</span></span> <span data-ttu-id="f927a-298">您可以在此函式新增命令來測試應用程式。</span><span class="sxs-lookup"><span data-stu-id="f927a-298">You can add commands in this function to test your application.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f927a-299">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f927a-299">Next steps</span></span>
<span data-ttu-id="f927a-300">請參閱[使用 Windows PowerShell 撰寫指令碼](https://technet.microsoft.com/library/bb978526.aspx)來深入了解 PowerShell 指令碼，並參閱[指令碼中心](https://azure.microsoft.com/documentation/scripts/)內的其他 Azure PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="f927a-300">Learn more about PowerShell scripting by reading [Scripting with Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx) and see other Azure PowerShell scripts at the [Script Center](https://azure.microsoft.com/documentation/scripts/).</span></span>
