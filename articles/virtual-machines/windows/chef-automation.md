---
title: "使用 Chef 的 Azure 虛擬機器部署 | Microsoft Docs"
description: "了解如何使用 Chef 執行自動化的虛擬機器部署和設定 Microsoft Azure"
services: virtual-machines-windows
documentationcenter: 
author: diegoviso
manager: timlt
tags: azure-service-management,azure-resource-manager
editor: 
ms.assetid: 0b82ca70-89ed-496d-bb49-c04ae59b4523
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: diviso
ms.openlocfilehash: b6db0fbb4e0de896994954974ddcc39daad9c125
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="automating-azure-virtual-machine-deployment-with-chef"></a><span data-ttu-id="56e34-103">使用 Chef 自動化 Azure 虛擬機器部署</span><span class="sxs-lookup"><span data-stu-id="56e34-103">Automating Azure virtual machine deployment with Chef</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="56e34-104">Chef 是個很棒的工具，可提供自動化和所需狀態組態。</span><span class="sxs-lookup"><span data-stu-id="56e34-104">Chef is a great tool for delivering automation and desired state configurations.</span></span>

<span data-ttu-id="56e34-105">在我們最新的雲端應用程式開發介面版本中，Chef 提供與 Azure 的緊密整合，您可以透過單一命令佈建和部署組態狀態。</span><span class="sxs-lookup"><span data-stu-id="56e34-105">With our latest cloud-api release, Chef provides seamless integration with Azure, giving you the ability to provision and deploy configuration states through a single command.</span></span>

<span data-ttu-id="56e34-106">在本文中，您將了解如何設定可佈建 Azure 虛擬機器的 Chef 環境，並逐步指導您建立原則或 “CookBook”，然後將此操作手冊部署到 Azure 虛擬機器中。</span><span class="sxs-lookup"><span data-stu-id="56e34-106">In this article, I’ll show you how to set up your Chef environment to provision Azure virtual machines and walk you through creating a policy or “CookBook” and then deploying this cookbook to an Azure virtual machine.</span></span>

<span data-ttu-id="56e34-107">讓我們開始吧！</span><span class="sxs-lookup"><span data-stu-id="56e34-107">Let’s begin!</span></span>

## <a name="chef-basics"></a><span data-ttu-id="56e34-108">Chef 基本概念</span><span class="sxs-lookup"><span data-stu-id="56e34-108">Chef basics</span></span>
<span data-ttu-id="56e34-109">開始之前，建議您檢閱 Chef 的基本概念。</span><span class="sxs-lookup"><span data-stu-id="56e34-109">Before you begin, I suggest you review the basic concepts of Chef.</span></span> <span data-ttu-id="56e34-110">您可以在 <a href="http://www.chef.io/chef" target="_blank">這裡</a> 找到有用資訊，建議您在嘗試進行本逐步解說之前，先快速閱讀此內容。</span><span class="sxs-lookup"><span data-stu-id="56e34-110">There is great material <a href="http://www.chef.io/chef" target="_blank">here</a> and I recommend you have a quick read before you attempt this walkthrough.</span></span> <span data-ttu-id="56e34-111">不過，在開始之前，我會先複習一下基本概念。</span><span class="sxs-lookup"><span data-stu-id="56e34-111">I will however recap the basics before we get started.</span></span>

<span data-ttu-id="56e34-112">下圖說明高層級的 Chef 架構。</span><span class="sxs-lookup"><span data-stu-id="56e34-112">The following diagram depicts the high-level Chef architecture.</span></span>

![][2]

<span data-ttu-id="56e34-113">Chef 有三個主要的架構元件：Chef 伺服器、Chef 用戶端 (節點) 和 Chef 工作站。</span><span class="sxs-lookup"><span data-stu-id="56e34-113">Chef has three main architectural components: Chef Server, Chef Client (node), and Chef Workstation.</span></span>

<span data-ttu-id="56e34-114">Chef 伺服器是我們的管理重點，Chef 伺服器包含兩個選項：代管解決方案或內部部署解決方案。</span><span class="sxs-lookup"><span data-stu-id="56e34-114">The Chef Server is our management point and there are two options for the Chef Server: a hosted solution or an on-premises solution.</span></span> <span data-ttu-id="56e34-115">我們將使用代管解決方案。</span><span class="sxs-lookup"><span data-stu-id="56e34-115">We will be using a hosted solution.</span></span>

<span data-ttu-id="56e34-116">Chef 用戶端 (節點)是位於您所管理之伺服器上的代理程式。</span><span class="sxs-lookup"><span data-stu-id="56e34-116">The Chef Client (node) is the agent that sits on the servers you are managing.</span></span>

<span data-ttu-id="56e34-117">Chef 工作站是我們的系統管理工作站，我們可以在這裡建立原則並執行管理命令。</span><span class="sxs-lookup"><span data-stu-id="56e34-117">The Chef Workstation is our admin workstation where we create our policies and execute our management commands.</span></span> <span data-ttu-id="56e34-118">我們可以從 Chef 工作站執行管理基礎結構的 **knife** 命令。</span><span class="sxs-lookup"><span data-stu-id="56e34-118">We run the **knife** command from the Chef Workstation to manage our infrastructure.</span></span>

<span data-ttu-id="56e34-119">此外還有 “Cookbooks” 和 “Recipes” 的概念。</span><span class="sxs-lookup"><span data-stu-id="56e34-119">There is also the concept of “Cookbooks” and “Recipes”.</span></span> <span data-ttu-id="56e34-120">這些是我們有效定義並套用至服務的原則。</span><span class="sxs-lookup"><span data-stu-id="56e34-120">These are effectively the policies we define and apply to our servers.</span></span>

## <a name="preparing-the-workstation"></a><span data-ttu-id="56e34-121">準備工作站</span><span class="sxs-lookup"><span data-stu-id="56e34-121">Preparing the workstation</span></span>
<span data-ttu-id="56e34-122">首先準備工作站。</span><span class="sxs-lookup"><span data-stu-id="56e34-122">First, lets prep the workstation.</span></span> <span data-ttu-id="56e34-123">使用標準的 Windows 工作站。</span><span class="sxs-lookup"><span data-stu-id="56e34-123">I’m using a standard Windows workstation.</span></span> <span data-ttu-id="56e34-124">我們需要建立可儲存組態檔和 cookbook 的目錄。</span><span class="sxs-lookup"><span data-stu-id="56e34-124">We need to create a directory to store our config files and cookbooks.</span></span>

<span data-ttu-id="56e34-125">首先，建立名為 C:\chef 的目錄。</span><span class="sxs-lookup"><span data-stu-id="56e34-125">First create a directory called C:\chef.</span></span>

<span data-ttu-id="56e34-126">然後建立名為 c:\chef\cookbooks 的第二個目錄。</span><span class="sxs-lookup"><span data-stu-id="56e34-126">Then create a second directory called c:\chef\cookbooks.</span></span>

<span data-ttu-id="56e34-127">我們現在必須下載 Azure 設定檔，以便 Chef 與 Azure 訂閱進行通訊。</span><span class="sxs-lookup"><span data-stu-id="56e34-127">We now need to download our Azure settings file so Chef can communicate with our Azure subscription.</span></span>

<!--Download your publish settings from [here](https://manage.windowsazure.com/publishsettings/).-->
<span data-ttu-id="56e34-128">使用 PowerShell Azure [Get-AzurePublishSettingsFile](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0) 命令來下載您的發佈設定。</span><span class="sxs-lookup"><span data-stu-id="56e34-128">Download your publish settings using the PowerShell Azure [Get-AzurePublishSettingsFile](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0) command.</span></span> 

<span data-ttu-id="56e34-129">將發行設定檔儲存在 C:\chef 中。</span><span class="sxs-lookup"><span data-stu-id="56e34-129">Save the publish settings file in C:\chef.</span></span>

## <a name="creating-a-managed-chef-account"></a><span data-ttu-id="56e34-130">建立受管理的 Chef 帳戶</span><span class="sxs-lookup"><span data-stu-id="56e34-130">Creating a managed Chef account</span></span>
<span data-ttu-id="56e34-131">在 [這裡](https://manage.chef.io/signup)註冊代管的 Chef 帳戶。</span><span class="sxs-lookup"><span data-stu-id="56e34-131">Sign up for a hosted Chef account [here](https://manage.chef.io/signup).</span></span>

<span data-ttu-id="56e34-132">在註冊過程中，我們將要求您建立新的組織。</span><span class="sxs-lookup"><span data-stu-id="56e34-132">During the signup process, you will be asked to create a new organization.</span></span>

![][3]

<span data-ttu-id="56e34-133">建立組織後，請下載「入門套件」。</span><span class="sxs-lookup"><span data-stu-id="56e34-133">Once your organization is created, download the starter kit.</span></span>

![][4]

> [!NOTE]
> <span data-ttu-id="56e34-134">如果您收到提示，警告您將重新設定金鑰，您可以繼續作業，因為我們尚未設定任何基礎結構。</span><span class="sxs-lookup"><span data-stu-id="56e34-134">If you receive a prompt warning you that your keys will be reset, it’s ok to proceed as we have no existing infrastructure configured as yet.</span></span>
> 
> 

<span data-ttu-id="56e34-135">此入門套件 zip 檔案包含您的組織組態檔和金鑰。</span><span class="sxs-lookup"><span data-stu-id="56e34-135">This starter kit zip file contains your organization config files and keys.</span></span>

## <a name="configuring-the-chef-workstation"></a><span data-ttu-id="56e34-136">設定 Chef 工作站</span><span class="sxs-lookup"><span data-stu-id="56e34-136">Configuring the Chef workstation</span></span>
<span data-ttu-id="56e34-137">將 chef-starter.zip 的內容解壓縮到 C:\chef。</span><span class="sxs-lookup"><span data-stu-id="56e34-137">Extract the content of the chef-starter.zip to C:\chef.</span></span>

<span data-ttu-id="56e34-138">將 chef-starter\chef-repo\.chef 下的所有檔案複製到您的 c:\chef 目錄。</span><span class="sxs-lookup"><span data-stu-id="56e34-138">Copy all files under chef-starter\chef-repo\.chef to your c:\chef directory.</span></span>

<span data-ttu-id="56e34-139">您的目錄現在看起來應該類似以下範例。</span><span class="sxs-lookup"><span data-stu-id="56e34-139">Your directory should now look something like the following example.</span></span>

![][5]

<span data-ttu-id="56e34-140">您現在應該會有 4 個檔案，包括 c:\chef 根目錄中的 Azure 發行檔案。</span><span class="sxs-lookup"><span data-stu-id="56e34-140">You should now have four files including the Azure publishing file in the root of c:\chef.</span></span>

<span data-ttu-id="56e34-141">PEM 檔案包含可進行通訊的組織和管理員私密金鑰，而 knife.rb檔案則包含 knife 組態。</span><span class="sxs-lookup"><span data-stu-id="56e34-141">The PEM files contain your organization and admin private keys for communication while the knife.rb file contains your knife configuration.</span></span> <span data-ttu-id="56e34-142">我們將需要編輯 knife.rb 檔案。</span><span class="sxs-lookup"><span data-stu-id="56e34-142">We will need to edit the knife.rb file.</span></span>

<span data-ttu-id="56e34-143">在您選擇的編輯器中開啟此檔案，並修改 “cookbook_path” (移除其路徑中的 /../)，因此它會顯示如下所示。</span><span class="sxs-lookup"><span data-stu-id="56e34-143">Open the file in your editor of choice and modify the “cookbook_path” by removing the /../ from the path so it appears as shown next.</span></span>

    cookbook_path  ["#{current_dir}/cookbooks"]

<span data-ttu-id="56e34-144">並新增下列反映 Azure 發行設定檔名稱的程式碼行。</span><span class="sxs-lookup"><span data-stu-id="56e34-144">Also add the following line reflecting the name of your Azure publish settings file.</span></span>

    knife[:azure_publish_settings_file] = "yourfilename.publishsettings"

<span data-ttu-id="56e34-145">現在 knife.rb 檔案看起來應該會類似下列範例。</span><span class="sxs-lookup"><span data-stu-id="56e34-145">Your knife.rb file should now look similar to the following example.</span></span>

![][6]

<span data-ttu-id="56e34-146">這幾行程式碼可確保 Knife 會參考 c:\chef\cookbooks 底下的 cookbooks 目錄，並在 Azure 作業期間使用 Azure 發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="56e34-146">These lines will ensure that Knife references the cookbooks directory under c:\chef\cookbooks, and also uses our Azure Publish Settings file during Azure operations.</span></span>

## <a name="installing-the-chef-development-kit"></a><span data-ttu-id="56e34-147">安裝 Chef 開發套件</span><span class="sxs-lookup"><span data-stu-id="56e34-147">Installing the Chef Development Kit</span></span>
<span data-ttu-id="56e34-148">接下來 [下載並安裝](http://downloads.getchef.com/chef-dk/windows) ChefDK (Chef 開發套件) 以設定 Chef 工作站。</span><span class="sxs-lookup"><span data-stu-id="56e34-148">Next [download and install](http://downloads.getchef.com/chef-dk/windows) the ChefDK (Chef Development Kit) to set up your Chef Workstation.</span></span>

![][7]

<span data-ttu-id="56e34-149">安裝在 c:\opscode 預設位置。</span><span class="sxs-lookup"><span data-stu-id="56e34-149">Install in the default location of c:\opscode.</span></span> <span data-ttu-id="56e34-150">此安裝大約需要 10 分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="56e34-150">This install will take around 10 minutes.</span></span>

<span data-ttu-id="56e34-151">確認您的 PATH 變數包含 C:\opscode\chefdk\bin、C:\opscode\chefdk\embedded\bin、c:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin 等項目</span><span class="sxs-lookup"><span data-stu-id="56e34-151">Confirm your PATH variable contains entries for C:\opscode\chefdk\bin;C:\opscode\chefdk\embedded\bin;c:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin</span></span>

<span data-ttu-id="56e34-152">如果沒有，請確定您已加入這些路徑 ！</span><span class="sxs-lookup"><span data-stu-id="56e34-152">If they are not there, make sure you add these paths!</span></span>

<span data-ttu-id="56e34-153">*請注意，路徑的順序很重要！*</span><span class="sxs-lookup"><span data-stu-id="56e34-153">*NOTE THE ORDER OF THE PATH IS IMPORTANT!*</span></span> <span data-ttu-id="56e34-154">如果您的 opscode 路徑順序不正確，則會出現問題。</span><span class="sxs-lookup"><span data-stu-id="56e34-154">If your opscode paths are not in the correct order you will have issues.</span></span>

<span data-ttu-id="56e34-155">在繼續之前，請重新啟動您的工作站。</span><span class="sxs-lookup"><span data-stu-id="56e34-155">Reboot your workstation before you continue.</span></span>

<span data-ttu-id="56e34-156">接下來，我們將安裝 Knife Azure 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="56e34-156">Next, we will install the Knife Azure extension.</span></span> <span data-ttu-id="56e34-157">這會以「Azure 外掛程式」的形式提供 Knife。</span><span class="sxs-lookup"><span data-stu-id="56e34-157">This provides Knife with the “Azure Plugin”.</span></span>

<span data-ttu-id="56e34-158">執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="56e34-158">Run the following command.</span></span>

    chef gem install knife-azure ––pre

> [!NOTE]
> <span data-ttu-id="56e34-159">-pre 引數可確保您會收到最新的 RC 版本 Knife Azure 外掛程式，該版本可讓您存取最新的 API 組合。</span><span class="sxs-lookup"><span data-stu-id="56e34-159">The –pre argument ensures you are receiving the latest RC version of the Knife Azure Plugin which provides access to the latest set of APIs.</span></span>
> 
> 

<span data-ttu-id="56e34-160">同時也可能安裝多個相依性。</span><span class="sxs-lookup"><span data-stu-id="56e34-160">It’s likely that a number of dependencies will also be installed at the same time.</span></span>

![][8]

<span data-ttu-id="56e34-161">若要確保一切都已正確設定，請執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="56e34-161">To ensure everything is configured correctly, run the following command.</span></span>

    knife azure image list

<span data-ttu-id="56e34-162">如果一切都已正確設定，您會在捲動時看到可用的 Azure 映像清單。</span><span class="sxs-lookup"><span data-stu-id="56e34-162">If everything is configured correctly, you will see a list of available Azure images scroll through.</span></span>

<span data-ttu-id="56e34-163">恭喜！</span><span class="sxs-lookup"><span data-stu-id="56e34-163">Congratulations.</span></span> <span data-ttu-id="56e34-164">工作站已設定！</span><span class="sxs-lookup"><span data-stu-id="56e34-164">The workstation is set up!</span></span>

## <a name="creating-a-cookbook"></a><span data-ttu-id="56e34-165">建立 Cookbook</span><span class="sxs-lookup"><span data-stu-id="56e34-165">Creating a Cookbook</span></span>
<span data-ttu-id="56e34-166">Chef 會使用 Cookbook 來定義一組您想在受管理的用戶端上執行的命令。</span><span class="sxs-lookup"><span data-stu-id="56e34-166">A Cookbook is used by Chef to define a set of commands that you wish to execute on your managed client.</span></span> <span data-ttu-id="56e34-167">建立 Cookbook 非常簡單，我們可以使用 **chef generate cookbook** 命令來產生 Cookbook 範本。</span><span class="sxs-lookup"><span data-stu-id="56e34-167">Creating a Cookbook is straightforward and we use the **chef generate cookbook** command to generate our Cookbook template.</span></span> <span data-ttu-id="56e34-168">我將呼叫我的 Cookbook Web 伺服器，因為我需要可自動部署 IIS 的原則。</span><span class="sxs-lookup"><span data-stu-id="56e34-168">I will be calling my Cookbook web server as I would like a policy that automatically deploys IIS.</span></span>

<span data-ttu-id="56e34-169">在 C:\Chef 目錄下，執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="56e34-169">Under your C:\Chef directory run the following command.</span></span>

    chef generate cookbook webserver

<span data-ttu-id="56e34-170">這會在 C:\Chef\cookbooks\webserver 目錄下產生一組檔案。</span><span class="sxs-lookup"><span data-stu-id="56e34-170">This will generate a set of files under the directory C:\Chef\cookbooks\webserver.</span></span> <span data-ttu-id="56e34-171">我們現在需要定義一組需要 Chef 用戶端在受管理的虛擬機器上執行的命令。</span><span class="sxs-lookup"><span data-stu-id="56e34-171">We now need to define the set of commands we would like our Chef client to execute on our managed virtual machine.</span></span>

<span data-ttu-id="56e34-172">這些命令會儲存在 default.rb.</span><span class="sxs-lookup"><span data-stu-id="56e34-172">The commands are stored in the file default.rb.</span></span> <span data-ttu-id="56e34-173">檔案中在這個檔案中，請定義一組用來安裝 IIS、啟動 IIS 並將範本檔案複製到 wwwroot 資料夾的命令。</span><span class="sxs-lookup"><span data-stu-id="56e34-173">In this file, I’ll be defining a set of commands that installs IIS, starts IIS and copies a template file to the wwwroot folder.</span></span>

<span data-ttu-id="56e34-174">修改 C:\chef\cookbooks\webserver\recipes\default.rb 檔並加入下列幾行程式碼。</span><span class="sxs-lookup"><span data-stu-id="56e34-174">Modify the C:\chef\cookbooks\webserver\recipes\default.rb file and add the following lines.</span></span>

    powershell_script 'Install IIS' do
         action :run
         code 'add-windowsfeature Web-Server'
    end

    service 'w3svc' do
         action [ :enable, :start ]
    end

    template 'c:\inetpub\wwwroot\Default.htm' do
         source 'Default.htm.erb'
         rights :read, 'Everyone'
    end

<span data-ttu-id="56e34-175">完成後，請儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="56e34-175">Save the file once you are done.</span></span>

## <a name="creating-a-template"></a><span data-ttu-id="56e34-176">建立範本</span><span class="sxs-lookup"><span data-stu-id="56e34-176">Creating a template</span></span>
<span data-ttu-id="56e34-177">如先前所述，我們需要產生可作為 default.html 頁面的範本檔案。</span><span class="sxs-lookup"><span data-stu-id="56e34-177">As we mentioned previously, we need to generate a template file which will be used as our default.html page.</span></span>

<span data-ttu-id="56e34-178">執行下列命令以產生範本。</span><span class="sxs-lookup"><span data-stu-id="56e34-178">Run the following command to generate the template.</span></span>

    chef generate template webserver Default.htm

<span data-ttu-id="56e34-179">現在瀏覽至 C:\chef\cookbooks\webserver\templates\default\Default.htm.erb 檔案。</span><span class="sxs-lookup"><span data-stu-id="56e34-179">Now navigate to the C:\chef\cookbooks\webserver\templates\default\Default.htm.erb file.</span></span> <span data-ttu-id="56e34-180">加入一些簡單的 "Hello World" HTML 程式碼來編輯檔案，然後儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="56e34-180">Edit the file by adding some simple “Hello World” HTML code, and then save the file.</span></span>

## <a name="upload-the-cookbook-to-the-chef-server"></a><span data-ttu-id="56e34-181">將 Cookbook 上傳到 Chef 伺服器</span><span class="sxs-lookup"><span data-stu-id="56e34-181">Upload the Cookbook to the Chef Server</span></span>
<span data-ttu-id="56e34-182">在此步驟中，我們會將在本機電腦上建立的 Cookbook 複本，上傳到 Chef 代管伺服器。</span><span class="sxs-lookup"><span data-stu-id="56e34-182">In this step, we are taking a copy of the Cookbook that we have created on our local machine and uploading it to the Chef Hosted Server.</span></span> <span data-ttu-id="56e34-183">上傳後，Cookbook 便會出現在 [原則]  索引標籤底下。</span><span class="sxs-lookup"><span data-stu-id="56e34-183">Once uploaded, the Cookbook will appear under the **Policy** tab.</span></span>

    knife cookbook upload webserver

![][9]

## <a name="deploy-a-virtual-machine-with-knife-azure"></a><span data-ttu-id="56e34-184">使用 Knife Azure 部署虛擬機器</span><span class="sxs-lookup"><span data-stu-id="56e34-184">Deploy a virtual machine with Knife Azure</span></span>
<span data-ttu-id="56e34-185">我們現在要部署 Azure 虛擬機器，並套用 “Webserver” Cookbook，如此便會安裝 IIS Web 服務和預設網頁。</span><span class="sxs-lookup"><span data-stu-id="56e34-185">We will now deploy an Azure virtual machine and apply the “Webserver” Cookbook which will install our IIS web service and default web page.</span></span>

<span data-ttu-id="56e34-186">若要這樣做，請使用 **knife azure server create** 命令。</span><span class="sxs-lookup"><span data-stu-id="56e34-186">In order to do this, use the **knife azure server create** command.</span></span>

<span data-ttu-id="56e34-187">接下來會顯示此命令的範例。</span><span class="sxs-lookup"><span data-stu-id="56e34-187">Am example of the command appears next.</span></span>

    knife azure server create --azure-dns-name 'diegotest01' --azure-vm-name 'testserver01' --azure-vm-size 'Small' --azure-storage-account 'portalvhdsxxxx' --bootstrap-protocol 'cloud-api' --azure-source-image 'a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-Datacenter-201411.01-en.us-127GB.vhd' --azure-service-location 'Southeast Asia' --winrm-user azureuser --winrm-password 'myPassword123' --tcp-endpoints 80,3389 --r 'recipe[webserver]'

<span data-ttu-id="56e34-188">這些參數一看就懂。</span><span class="sxs-lookup"><span data-stu-id="56e34-188">The parameters are self-explanatory.</span></span> <span data-ttu-id="56e34-189">替換特定變數並執行。</span><span class="sxs-lookup"><span data-stu-id="56e34-189">Substitute your particular variables and run.</span></span>

> [!NOTE]
> <span data-ttu-id="56e34-190">透過命令列，我還打算使用 -tcp-endpoints 參數將端點網路篩選器規則自動化。</span><span class="sxs-lookup"><span data-stu-id="56e34-190">Through the the command line, I’m also automating my endpoint network filter rules by using the –tcp-endpoints parameter.</span></span> <span data-ttu-id="56e34-191">我已經開放連接埠 80 和 3389 以供網頁和 RDP 工作階段存取。</span><span class="sxs-lookup"><span data-stu-id="56e34-191">I’ve opened up ports 80 and 3389 to provide access to my web page and RDP session.</span></span>
> 
> 

<span data-ttu-id="56e34-192">執行命令後，前往 Azure 入口網站，您會看到已經開始佈建您的機器。</span><span class="sxs-lookup"><span data-stu-id="56e34-192">Once you run the command, go to the Azure portal and you will see your machine begin to provision.</span></span>

![][13]

<span data-ttu-id="56e34-193">命令提示字元會顯示下一步。</span><span class="sxs-lookup"><span data-stu-id="56e34-193">The command prompt appears next.</span></span>

![][10]

<span data-ttu-id="56e34-194">部署完成之後，我們應該能夠透過連接埠 80 連接到 Web 服務，因為我們使用 Knife Azure 命令佈建虛擬機器時已將此連接埠開啟。</span><span class="sxs-lookup"><span data-stu-id="56e34-194">Once the deployment is complete, we should be able to connect to the web service over port 80 as we had opened the port when we provisioned the virtual machine with the Knife Azure command.</span></span> <span data-ttu-id="56e34-195">由於此虛擬機器是我的雲端服務中唯一的虛擬機器，我要使用雲端服務 URL 來進行連接。</span><span class="sxs-lookup"><span data-stu-id="56e34-195">As this virtual machine is the only virtual machine in my cloud service, I’ll connect it with the cloud service url.</span></span>

![][11]

<span data-ttu-id="56e34-196">如您所見，我的 HTML 程式碼開始有點意思。</span><span class="sxs-lookup"><span data-stu-id="56e34-196">As you can see, I got creative with my HTML code.</span></span>

<span data-ttu-id="56e34-197">別忘了我們也可以透過連接埠 3389，從 Azure 入口網站的 RDP 工作階段進行連線。</span><span class="sxs-lookup"><span data-stu-id="56e34-197">Don’t forget we can also connect through an RDP session from the Azure portal via port 3389.</span></span>

<span data-ttu-id="56e34-198">我希望這對您有所幫助！</span><span class="sxs-lookup"><span data-stu-id="56e34-198">I hope this has been helpful!</span></span> <span data-ttu-id="56e34-199">現在就開始使用 Azure 來體驗基礎結構即程式碼！</span><span class="sxs-lookup"><span data-stu-id="56e34-199">Go  and start your infrastructure as code journey with Azure today!</span></span>

<!--Image references-->
[2]: media/chef-automation/2.png
[3]: media/chef-automation/3.png
[4]: media/chef-automation/4.png
[5]: media/chef-automation/5.png
[6]: media/chef-automation/6.png
[7]: media/chef-automation/7.png
[8]: media/chef-automation/8.png
[9]: media/chef-automation/9.png
[10]: media/chef-automation/10.png
[11]: media/chef-automation/11.png
[13]: media/chef-automation/13.png


<!--Link references-->
