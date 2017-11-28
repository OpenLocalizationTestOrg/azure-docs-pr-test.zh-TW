---
title: "chef aaaAzure 虛擬機器部署 |Microsoft 文件"
description: "了解 Chef toodo toouse 自動化虛擬機器部署和設定 Microsoft Azure 上的方式"
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
ms.openlocfilehash: c5ea98c673b2ee75dd4cedf27e50330af05230d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automating-azure-virtual-machine-deployment-with-chef"></a><span data-ttu-id="da006-103">使用 Chef 自動化 Azure 虛擬機器部署</span><span class="sxs-lookup"><span data-stu-id="da006-103">Automating Azure virtual machine deployment with Chef</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="da006-104">Chef 是個很棒的工具，可提供自動化和所需狀態組態。</span><span class="sxs-lookup"><span data-stu-id="da006-104">Chef is a great tool for delivering automation and desired state configurations.</span></span>

<span data-ttu-id="da006-105">我們最新的雲端應用程式開發介面版本中，Chef 提供 Azure 與緊密整合，讓您 hello 能力 tooprovision 及部署的組態狀態，透過單一命令。</span><span class="sxs-lookup"><span data-stu-id="da006-105">With our latest cloud-api release, Chef provides seamless integration with Azure, giving you hello ability tooprovision and deploy configuration states through a single command.</span></span>

<span data-ttu-id="da006-106">在本文中，我們將示範如何 tooset 註冊您的 Chef 環境 tooprovision Azure 虛擬機器，並會逐步引導您建立原則或 「 操作手冊"，然後再部署這個操作手冊 tooan Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="da006-106">In this article, I’ll show you how tooset up your Chef environment tooprovision Azure virtual machines and walk you through creating a policy or “CookBook” and then deploying this cookbook tooan Azure virtual machine.</span></span>

<span data-ttu-id="da006-107">讓我們開始吧！</span><span class="sxs-lookup"><span data-stu-id="da006-107">Let’s begin!</span></span>

## <a name="chef-basics"></a><span data-ttu-id="da006-108">Chef 基本概念</span><span class="sxs-lookup"><span data-stu-id="da006-108">Chef basics</span></span>
<span data-ttu-id="da006-109">在開始之前，建議您檢閱的 Chef hello 基本概念。</span><span class="sxs-lookup"><span data-stu-id="da006-109">Before you begin, I suggest you review hello basic concepts of Chef.</span></span> <span data-ttu-id="da006-110">您可以在 <a href="http://www.chef.io/chef" target="_blank">這裡</a> 找到有用資訊，建議您在嘗試進行本逐步解說之前，先快速閱讀此內容。</span><span class="sxs-lookup"><span data-stu-id="da006-110">There is great material <a href="http://www.chef.io/chef" target="_blank">here</a> and I recommend you have a quick read before you attempt this walkthrough.</span></span> <span data-ttu-id="da006-111">我將在我們開始之前，不過複習 hello 基本概念。</span><span class="sxs-lookup"><span data-stu-id="da006-111">I will however recap hello basics before we get started.</span></span>

<span data-ttu-id="da006-112">hello 下列圖表描述 hello 高階 Chef 架構。</span><span class="sxs-lookup"><span data-stu-id="da006-112">hello following diagram depicts hello high-level Chef architecture.</span></span>

![][2]

<span data-ttu-id="da006-113">Chef 有三個主要的架構元件：Chef 伺服器、Chef 用戶端 (節點) 和 Chef 工作站。</span><span class="sxs-lookup"><span data-stu-id="da006-113">Chef has three main architectural components: Chef Server, Chef Client (node), and Chef Workstation.</span></span>

<span data-ttu-id="da006-114">hello Chef Server 是我們的管理點，而且有兩個選項的 hello Chef Server： 託管的解決方案或內部部署方案。</span><span class="sxs-lookup"><span data-stu-id="da006-114">hello Chef Server is our management point and there are two options for hello Chef Server: a hosted solution or an on-premises solution.</span></span> <span data-ttu-id="da006-115">我們將使用代管解決方案。</span><span class="sxs-lookup"><span data-stu-id="da006-115">We will be using a hosted solution.</span></span>

<span data-ttu-id="da006-116">hello Chef 用戶端 （節點） 是位於您所管理的 hello 伺服器 hello 代理程式。</span><span class="sxs-lookup"><span data-stu-id="da006-116">hello Chef Client (node) is hello agent that sits on hello servers you are managing.</span></span>

<span data-ttu-id="da006-117">hello Chef 工作站是我們的系統管理工作站，我們建立我們的原則和執行我們的管理命令。</span><span class="sxs-lookup"><span data-stu-id="da006-117">hello Chef Workstation is our admin workstation where we create our policies and execute our management commands.</span></span> <span data-ttu-id="da006-118">我們要執行 hello **knife**命令 hello Chef 工作站 toomanage 從我們的基礎結構。</span><span class="sxs-lookup"><span data-stu-id="da006-118">We run hello **knife** command from hello Chef Workstation toomanage our infrastructure.</span></span>

<span data-ttu-id="da006-119">另外還有 hello 概念"食譜 」 與 「 食譜 」。</span><span class="sxs-lookup"><span data-stu-id="da006-119">There is also hello concept of “Cookbooks” and “Recipes”.</span></span> <span data-ttu-id="da006-120">這些都是有效我們定義及套用 tooour 伺服器 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="da006-120">These are effectively hello policies we define and apply tooour servers.</span></span>

## <a name="preparing-hello-workstation"></a><span data-ttu-id="da006-121">正在準備 hello 工作站</span><span class="sxs-lookup"><span data-stu-id="da006-121">Preparing hello workstation</span></span>
<span data-ttu-id="da006-122">首先，可讓準備 hello 工作站。</span><span class="sxs-lookup"><span data-stu-id="da006-122">First, lets prep hello workstation.</span></span> <span data-ttu-id="da006-123">使用標準的 Windows 工作站。</span><span class="sxs-lookup"><span data-stu-id="da006-123">I’m using a standard Windows workstation.</span></span> <span data-ttu-id="da006-124">我們的組態檔和操作手冊，我們需要 toocreate 目錄 toostore。</span><span class="sxs-lookup"><span data-stu-id="da006-124">We need toocreate a directory toostore our config files and cookbooks.</span></span>

<span data-ttu-id="da006-125">首先，建立名為 C:\chef 的目錄。</span><span class="sxs-lookup"><span data-stu-id="da006-125">First create a directory called C:\chef.</span></span>

<span data-ttu-id="da006-126">然後建立名為 c:\chef\cookbooks 的第二個目錄。</span><span class="sxs-lookup"><span data-stu-id="da006-126">Then create a second directory called c:\chef\cookbooks.</span></span>

<span data-ttu-id="da006-127">我們現在需要 toodownload 我們的 Azure 設定檔，Chef 可以與我們的 Azure 訂用帳戶進行通訊。</span><span class="sxs-lookup"><span data-stu-id="da006-127">We now need toodownload our Azure settings file so Chef can communicate with our Azure subscription.</span></span>

<!--Download your publish settings from [here](https://manage.windowsazure.com/publishsettings/).-->
<span data-ttu-id="da006-128">下載您發行設定使用 PowerShell Azure hello [Get-azurepublishsettingsfile](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0)命令。</span><span class="sxs-lookup"><span data-stu-id="da006-128">Download your publish settings using hello PowerShell Azure [Get-AzurePublishSettingsFile](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0) command.</span></span> 

<span data-ttu-id="da006-129">儲存 hello C:\chef 中的發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="da006-129">Save hello publish settings file in C:\chef.</span></span>

## <a name="creating-a-managed-chef-account"></a><span data-ttu-id="da006-130">建立受管理的 Chef 帳戶</span><span class="sxs-lookup"><span data-stu-id="da006-130">Creating a managed Chef account</span></span>
<span data-ttu-id="da006-131">在 [這裡](https://manage.chef.io/signup)註冊代管的 Chef 帳戶。</span><span class="sxs-lookup"><span data-stu-id="da006-131">Sign up for a hosted Chef account [here](https://manage.chef.io/signup).</span></span>

<span data-ttu-id="da006-132">在 hello 註冊過程中，您將會詢問 toocreate 新的組織。</span><span class="sxs-lookup"><span data-stu-id="da006-132">During hello signup process, you will be asked toocreate a new organization.</span></span>

![][3]

<span data-ttu-id="da006-133">一旦建立您的組織，下載 hello 入門套件。</span><span class="sxs-lookup"><span data-stu-id="da006-133">Once your organization is created, download hello starter kit.</span></span>

![][4]

> [!NOTE]
> <span data-ttu-id="da006-134">如果您收到提示，警告您，將會重設您的金鑰，因為我們不有尚未設定任何現有基礎結構，所以 tooproceed [確定]。</span><span class="sxs-lookup"><span data-stu-id="da006-134">If you receive a prompt warning you that your keys will be reset, it’s ok tooproceed as we have no existing infrastructure configured as yet.</span></span>
> 
> 

<span data-ttu-id="da006-135">此入門套件 zip 檔案包含您的組織組態檔和金鑰。</span><span class="sxs-lookup"><span data-stu-id="da006-135">This starter kit zip file contains your organization config files and keys.</span></span>

## <a name="configuring-hello-chef-workstation"></a><span data-ttu-id="da006-136">設定 hello Chef 工作站</span><span class="sxs-lookup"><span data-stu-id="da006-136">Configuring hello Chef workstation</span></span>
<span data-ttu-id="da006-137">擷取 hello chef starter.zip tooC:\chef hello 內容。</span><span class="sxs-lookup"><span data-stu-id="da006-137">Extract hello content of hello chef-starter.zip tooC:\chef.</span></span>

<span data-ttu-id="da006-138">複製儲存 starter\chef chef 機制底下的所有檔案\.chef tooyour c:\chef 目錄。</span><span class="sxs-lookup"><span data-stu-id="da006-138">Copy all files under chef-starter\chef-repo\.chef tooyour c:\chef directory.</span></span>

<span data-ttu-id="da006-139">您的目錄現在應該看起來類似下列範例中的 hello。</span><span class="sxs-lookup"><span data-stu-id="da006-139">Your directory should now look something like hello following example.</span></span>

![][5]

<span data-ttu-id="da006-140">您現在應該有四個檔案，包括 c:\chef hello 根目錄中的 hello Azure 發行檔案。</span><span class="sxs-lookup"><span data-stu-id="da006-140">You should now have four files including hello Azure publishing file in hello root of c:\chef.</span></span>

<span data-ttu-id="da006-141">hello PEM 檔案包含您的組織和管理私密金鑰進行通訊，而 hello knife.rb 檔案包含 knife 組態。</span><span class="sxs-lookup"><span data-stu-id="da006-141">hello PEM files contain your organization and admin private keys for communication while hello knife.rb file contains your knife configuration.</span></span> <span data-ttu-id="da006-142">我們需要 tooedit hello knife.rb 檔案。</span><span class="sxs-lookup"><span data-stu-id="da006-142">We will need tooedit hello knife.rb file.</span></span>

<span data-ttu-id="da006-143">在您選擇的編輯器中開啟 hello 檔案，並藉由移除 hello 修改 hello"cookbook_path"/...從中 hello 路徑，讓它出現如下所示。</span><span class="sxs-lookup"><span data-stu-id="da006-143">Open hello file in your editor of choice and modify hello “cookbook_path” by removing hello /../ from hello path so it appears as shown next.</span></span>

    cookbook_path  ["#{current_dir}/cookbooks"]

<span data-ttu-id="da006-144">也新增 hello 下列程式行會將 hello 名稱反映您的 Azure 發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="da006-144">Also add hello following line reflecting hello name of your Azure publish settings file.</span></span>

    knife[:azure_publish_settings_file] = "yourfilename.publishsettings"

<span data-ttu-id="da006-145">Knife.rb 檔現在看起來應該類似下列範例的 toohello。</span><span class="sxs-lookup"><span data-stu-id="da006-145">Your knife.rb file should now look similar toohello following example.</span></span>

![][6]

<span data-ttu-id="da006-146">Knife 參考 hello 下 c:\chef\cookbooks 的操作手冊目錄，而且也會使用我們的 Azure 發佈設定檔的 Azure 作業期間，可確保這些線條。</span><span class="sxs-lookup"><span data-stu-id="da006-146">These lines will ensure that Knife references hello cookbooks directory under c:\chef\cookbooks, and also uses our Azure Publish Settings file during Azure operations.</span></span>

## <a name="installing-hello-chef-development-kit"></a><span data-ttu-id="da006-147">安裝 hello Chef 開發套件</span><span class="sxs-lookup"><span data-stu-id="da006-147">Installing hello Chef Development Kit</span></span>
<span data-ttu-id="da006-148">下一步[下載並安裝](http://downloads.getchef.com/chef-dk/windows)hello ChefDK （Chef 開發套件） tooset Chef 工作站。</span><span class="sxs-lookup"><span data-stu-id="da006-148">Next [download and install](http://downloads.getchef.com/chef-dk/windows) hello ChefDK (Chef Development Kit) tooset up your Chef Workstation.</span></span>

![][7]

<span data-ttu-id="da006-149">安裝 c:\opscode hello 預設位置中。</span><span class="sxs-lookup"><span data-stu-id="da006-149">Install in hello default location of c:\opscode.</span></span> <span data-ttu-id="da006-150">此安裝大約需要 10 分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="da006-150">This install will take around 10 minutes.</span></span>

<span data-ttu-id="da006-151">確認您的 PATH 變數包含 C:\opscode\chefdk\bin、C:\opscode\chefdk\embedded\bin、c:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin 等項目</span><span class="sxs-lookup"><span data-stu-id="da006-151">Confirm your PATH variable contains entries for C:\opscode\chefdk\bin;C:\opscode\chefdk\embedded\bin;c:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin</span></span>

<span data-ttu-id="da006-152">如果沒有，請確定您已加入這些路徑 ！</span><span class="sxs-lookup"><span data-stu-id="da006-152">If they are not there, make sure you add these paths!</span></span>

<span data-ttu-id="da006-153">*請注意 hello 順序的 hello 路徑重要 ！*</span><span class="sxs-lookup"><span data-stu-id="da006-153">*NOTE hello ORDER OF hello PATH IS IMPORTANT!*</span></span> <span data-ttu-id="da006-154">如果 opscode 路徑不正確的順序 hello 會出現問題。</span><span class="sxs-lookup"><span data-stu-id="da006-154">If your opscode paths are not in hello correct order you will have issues.</span></span>

<span data-ttu-id="da006-155">在繼續之前，請重新啟動您的工作站。</span><span class="sxs-lookup"><span data-stu-id="da006-155">Reboot your workstation before you continue.</span></span>

<span data-ttu-id="da006-156">接下來，我們將會安裝 hello Knife Azure 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="da006-156">Next, we will install hello Knife Azure extension.</span></span> <span data-ttu-id="da006-157">這提供 Knife hello"Azure Plugin"。</span><span class="sxs-lookup"><span data-stu-id="da006-157">This provides Knife with hello “Azure Plugin”.</span></span>

<span data-ttu-id="da006-158">執行下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="da006-158">Run hello following command.</span></span>

    chef gem install knife-azure ––pre

> [!NOTE]
> <span data-ttu-id="da006-159">hello – 前置引數可確保您收到 hello RC 新版 hello Knife Azure 外掛程式可提供存取 toohello 一組最新的 Api。</span><span class="sxs-lookup"><span data-stu-id="da006-159">hello –pre argument ensures you are receiving hello latest RC version of hello Knife Azure Plugin which provides access toohello latest set of APIs.</span></span>
> 
> 

<span data-ttu-id="da006-160">很少的相依性也會安裝在 hello 相同的時間。</span><span class="sxs-lookup"><span data-stu-id="da006-160">It’s likely that a number of dependencies will also be installed at hello same time.</span></span>

![][8]

<span data-ttu-id="da006-161">tooensure 一切都已正確設定，執行下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="da006-161">tooensure everything is configured correctly, run hello following command.</span></span>

    knife azure image list

<span data-ttu-id="da006-162">如果一切都已正確設定，您會在捲動時看到可用的 Azure 映像清單。</span><span class="sxs-lookup"><span data-stu-id="da006-162">If everything is configured correctly, you will see a list of available Azure images scroll through.</span></span>

<span data-ttu-id="da006-163">恭喜！</span><span class="sxs-lookup"><span data-stu-id="da006-163">Congratulations.</span></span> <span data-ttu-id="da006-164">設定工作站 hello ！</span><span class="sxs-lookup"><span data-stu-id="da006-164">hello workstation is set up!</span></span>

## <a name="creating-a-cookbook"></a><span data-ttu-id="da006-165">建立 Cookbook</span><span class="sxs-lookup"><span data-stu-id="da006-165">Creating a Cookbook</span></span>
<span data-ttu-id="da006-166">使用 Chef toodefine 操作手冊的一組命令，您會希望 tooexecute 您受管理的用戶端上。</span><span class="sxs-lookup"><span data-stu-id="da006-166">A Cookbook is used by Chef toodefine a set of commands that you wish tooexecute on your managed client.</span></span> <span data-ttu-id="da006-167">建立操作手冊很簡單，我們 hello **chef 產生 cookbook**命令 toogenerate 我們 Cookbook 的範本。</span><span class="sxs-lookup"><span data-stu-id="da006-167">Creating a Cookbook is straightforward and we use hello **chef generate cookbook** command toogenerate our Cookbook template.</span></span> <span data-ttu-id="da006-168">我將呼叫我的 Cookbook Web 伺服器，因為我需要可自動部署 IIS 的原則。</span><span class="sxs-lookup"><span data-stu-id="da006-168">I will be calling my Cookbook web server as I would like a policy that automatically deploys IIS.</span></span>

<span data-ttu-id="da006-169">C:\Chef 目錄執行下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="da006-169">Under your C:\Chef directory run hello following command.</span></span>

    chef generate cookbook webserver

<span data-ttu-id="da006-170">這會產生一組 hello 目錄 C:\Chef\cookbooks\webserver 下的檔案。</span><span class="sxs-lookup"><span data-stu-id="da006-170">This will generate a set of files under hello directory C:\Chef\cookbooks\webserver.</span></span> <span data-ttu-id="da006-171">我們現在需要 toodefine hello 組我們受管理的虛擬機器上，我們都希望我們 Chef 用戶端 tooexecute 命令。</span><span class="sxs-lookup"><span data-stu-id="da006-171">We now need toodefine hello set of commands we would like our Chef client tooexecute on our managed virtual machine.</span></span>

<span data-ttu-id="da006-172">hello 命令會儲存在 hello 檔案 default.rb。</span><span class="sxs-lookup"><span data-stu-id="da006-172">hello commands are stored in hello file default.rb.</span></span> <span data-ttu-id="da006-173">在此檔案中，我會定義一組命令來安裝 IIS，啟動 IIS，並將範本檔案 toohello wwwroot 資料夾複製到。</span><span class="sxs-lookup"><span data-stu-id="da006-173">In this file, I’ll be defining a set of commands that installs IIS, starts IIS and copies a template file toohello wwwroot folder.</span></span>

<span data-ttu-id="da006-174">修改 hello C:\chef\cookbooks\webserver\recipes\default.rb 檔案，並新增下列幾行 hello。</span><span class="sxs-lookup"><span data-stu-id="da006-174">Modify hello C:\chef\cookbooks\webserver\recipes\default.rb file and add hello following lines.</span></span>

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

<span data-ttu-id="da006-175">完成後，請儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="da006-175">Save hello file once you are done.</span></span>

## <a name="creating-a-template"></a><span data-ttu-id="da006-176">建立範本</span><span class="sxs-lookup"><span data-stu-id="da006-176">Creating a template</span></span>
<span data-ttu-id="da006-177">如先前所述，我們需要 toogenerate 用作我們 default.html 頁面的範本檔案。</span><span class="sxs-lookup"><span data-stu-id="da006-177">As we mentioned previously, we need toogenerate a template file which will be used as our default.html page.</span></span>

<span data-ttu-id="da006-178">執行下列命令 toogenerate hello 範本 hello。</span><span class="sxs-lookup"><span data-stu-id="da006-178">Run hello following command toogenerate hello template.</span></span>

    chef generate template webserver Default.htm

<span data-ttu-id="da006-179">現在您可以瀏覽 toohello C:\chef\cookbooks\webserver\templates\default\Default.htm.erb 檔案。</span><span class="sxs-lookup"><span data-stu-id="da006-179">Now navigate toohello C:\chef\cookbooks\webserver\templates\default\Default.htm.erb file.</span></span> <span data-ttu-id="da006-180">編輯 hello 檔案加入一些簡單的"Hello World"HTML 程式碼，並儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="da006-180">Edit hello file by adding some simple “Hello World” HTML code, and then save hello file.</span></span>

## <a name="upload-hello-cookbook-toohello-chef-server"></a><span data-ttu-id="da006-181">上傳 hello Cookbook toohello Chef Server</span><span class="sxs-lookup"><span data-stu-id="da006-181">Upload hello Cookbook toohello Chef Server</span></span>
<span data-ttu-id="da006-182">在此步驟中，我們會 hello 我們建立了我們在本機電腦的操作手冊的複製，並將它上傳 toohello Chef 託管伺服器。</span><span class="sxs-lookup"><span data-stu-id="da006-182">In this step, we are taking a copy of hello Cookbook that we have created on our local machine and uploading it toohello Chef Hosted Server.</span></span> <span data-ttu-id="da006-183">Hello 操作手冊上傳之後，會出現在 hello**原則** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="da006-183">Once uploaded, hello Cookbook will appear under hello **Policy** tab.</span></span>

    knife cookbook upload webserver

![][9]

## <a name="deploy-a-virtual-machine-with-knife-azure"></a><span data-ttu-id="da006-184">使用 Knife Azure 部署虛擬機器</span><span class="sxs-lookup"><span data-stu-id="da006-184">Deploy a virtual machine with Knife Azure</span></span>
<span data-ttu-id="da006-185">我們現在將會部署 Azure 虛擬機器，並套用 hello 」 網頁伺服器 」 操作手冊，如此可安裝我們 IIS web 服務和預設 web 網頁。</span><span class="sxs-lookup"><span data-stu-id="da006-185">We will now deploy an Azure virtual machine and apply hello “Webserver” Cookbook which will install our IIS web service and default web page.</span></span>

<span data-ttu-id="da006-186">在此順序 toodo，使用 hello **knife azure 伺服器建立**命令。</span><span class="sxs-lookup"><span data-stu-id="da006-186">In order toodo this, use hello **knife azure server create** command.</span></span>

<span data-ttu-id="da006-187">在 [hello 命令的範例則顯示下一步]。</span><span class="sxs-lookup"><span data-stu-id="da006-187">Am example of hello command appears next.</span></span>

    knife azure server create --azure-dns-name 'diegotest01' --azure-vm-name 'testserver01' --azure-vm-size 'Small' --azure-storage-account 'portalvhdsxxxx' --bootstrap-protocol 'cloud-api' --azure-source-image 'a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-Datacenter-201411.01-en.us-127GB.vhd' --azure-service-location 'Southeast Asia' --winrm-user azureuser --winrm-password 'myPassword123' --tcp-endpoints 80,3389 --r 'recipe[webserver]'

<span data-ttu-id="da006-188">hello 參數都一目了然。</span><span class="sxs-lookup"><span data-stu-id="da006-188">hello parameters are self-explanatory.</span></span> <span data-ttu-id="da006-189">替換特定變數並執行。</span><span class="sxs-lookup"><span data-stu-id="da006-189">Substitute your particular variables and run.</span></span>

> [!NOTE]
> <span data-ttu-id="da006-190">透過 hello hello 命令列，我也使用 hello – tcp 端點參數自動化端點網路篩選規則。</span><span class="sxs-lookup"><span data-stu-id="da006-190">Through hello hello command line, I’m also automating my endpoint network filter rules by using hello –tcp-endpoints parameter.</span></span> <span data-ttu-id="da006-191">我已經開啟通訊埠 80 與 3389 tooprovide 存取 toomy 網頁以及 RDP 工作階段。</span><span class="sxs-lookup"><span data-stu-id="da006-191">I’ve opened up ports 80 and 3389 tooprovide access toomy web page and RDP session.</span></span>
> 
> 

<span data-ttu-id="da006-192">一旦您執行 hello 命令，請移 toohello Azure 入口網站，您會看到您的電腦開始 tooprovision。</span><span class="sxs-lookup"><span data-stu-id="da006-192">Once you run hello command, go toohello Azure portal and you will see your machine begin tooprovision.</span></span>

![][13]

<span data-ttu-id="da006-193">hello 命令提示字元會顯示下一步。</span><span class="sxs-lookup"><span data-stu-id="da006-193">hello command prompt appears next.</span></span>

![][10]

<span data-ttu-id="da006-194">Hello 部署完成之後，我們應該是可以 tooconnect toohello web 服務透過連接埠 80 我們佈建以 hello Knife Azure 指令 hello 虛擬機器時，我們已開啟 hello 連接埠。</span><span class="sxs-lookup"><span data-stu-id="da006-194">Once hello deployment is complete, we should be able tooconnect toohello web service over port 80 as we had opened hello port when we provisioned hello virtual machine with hello Knife Azure command.</span></span> <span data-ttu-id="da006-195">因為此虛擬機器 hello 只有虛擬機器在我的雲端服務，我會將與 hello 雲端服務 url 來進行連接。</span><span class="sxs-lookup"><span data-stu-id="da006-195">As this virtual machine is hello only virtual machine in my cloud service, I’ll connect it with hello cloud service url.</span></span>

![][11]

<span data-ttu-id="da006-196">如您所見，我的 HTML 程式碼開始有點意思。</span><span class="sxs-lookup"><span data-stu-id="da006-196">As you can see, I got creative with my HTML code.</span></span>

<span data-ttu-id="da006-197">別忘了我們也可以透過從 hello Azure 入口網站連接埠 3389 透過 RDP 工作階段連接。</span><span class="sxs-lookup"><span data-stu-id="da006-197">Don’t forget we can also connect through an RDP session from hello Azure portal via port 3389.</span></span>

<span data-ttu-id="da006-198">我希望這對您有所幫助！</span><span class="sxs-lookup"><span data-stu-id="da006-198">I hope this has been helpful!</span></span> <span data-ttu-id="da006-199">現在就開始使用 Azure 來體驗基礎結構即程式碼！</span><span class="sxs-lookup"><span data-stu-id="da006-199">Go  and start your infrastructure as code journey with Azure today!</span></span>

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
