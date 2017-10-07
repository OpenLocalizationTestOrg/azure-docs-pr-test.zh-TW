---
title: "aaaHost 滑軌 Linux VM 上的網站上的 Ruby |Microsoft 文件"
description: "在使用 Linux 虛擬機器的 Azure 上設定及裝載 Ruby on Rails 型網站。"
services: virtual-machines-linux
documentationcenter: ruby
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: aad32685-3550-4bff-9c73-beb8d70b3291
ms.service: virtual-machines-linux
ms.workload: web
ms.tgt_pltfrm: vm-linux
ms.devlang: ruby
ms.topic: article
ms.date: 06/27/2017
ms.author: robmcm
ms.openlocfilehash: c545c24fc6c89497854bbe55a6d0d1d0b072c386
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="ruby-on-rails-web-application-on-an-azure-vm"></a><span data-ttu-id="13aaf-103">Azure VM 上的 Ruby on Rails Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="13aaf-103">Ruby on Rails Web application on an Azure VM</span></span>
<span data-ttu-id="13aaf-104">本教學課程示範如何 toohost Ruby 滑軌網站上使用 Linux 虛擬機器的 Azure 上。</span><span class="sxs-lookup"><span data-stu-id="13aaf-104">This tutorial shows how toohost a Ruby on Rails website on Azure using a Linux virtual machine.</span></span>  

<span data-ttu-id="13aaf-105">此教學課程使用 Ubuntu Server 14.04 LTS 通過驗證。</span><span class="sxs-lookup"><span data-stu-id="13aaf-105">This tutorial was validated using Ubuntu Server 14.04 LTS.</span></span> <span data-ttu-id="13aaf-106">如果您使用不同的 Linux 散發套件，您可能需要 toomodify hello 步驟 tooinstall 滑軌。</span><span class="sxs-lookup"><span data-stu-id="13aaf-106">If you use a different Linux distribution, you might need toomodify hello steps tooinstall Rails.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="13aaf-107">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../../../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="13aaf-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="13aaf-108">本文說明如何使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="13aaf-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="13aaf-109">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="13aaf-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
>
>

## <a name="create-an-azure-vm"></a><span data-ttu-id="13aaf-110">建立 Azure VM</span><span class="sxs-lookup"><span data-stu-id="13aaf-110">Create an Azure VM</span></span>
<span data-ttu-id="13aaf-111">開始使用 Linux 映像建立 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="13aaf-111">Start by creating an Azure VM with a Linux image.</span></span>

<span data-ttu-id="13aaf-112">toocreate hello VM，您可以使用 hello Azure 入口網站或 hello Azure 命令列介面 (CLI)。</span><span class="sxs-lookup"><span data-stu-id="13aaf-112">toocreate hello VM, you can use hello Azure portal or hello Azure Command-Line Interface (CLI).</span></span>

### <a name="azure-portal"></a><span data-ttu-id="13aaf-113">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="13aaf-113">Azure portal</span></span>
1. <span data-ttu-id="13aaf-114">登入 hello [Azure 入口網站](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="13aaf-114">Sign into hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="13aaf-115">按一下**新增**，然後輸入 hello [搜尋] 方塊中的 < Ubuntu Server 14.04 >。</span><span class="sxs-lookup"><span data-stu-id="13aaf-115">Click **New**, then type "Ubuntu Server 14.04" in hello search box.</span></span> <span data-ttu-id="13aaf-116">按一下 hello hello 搜尋所傳回的項目。</span><span class="sxs-lookup"><span data-stu-id="13aaf-116">Click hello entry returned by hello search.</span></span> <span data-ttu-id="13aaf-117">Hello 部署模型中，選取**傳統**，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="13aaf-117">For hello deployment model, select **Classic**, then click "Create".</span></span>
3. <span data-ttu-id="13aaf-118">在 hello 基本概念刀鋒視窗中，提供所需的 hello 欄位的值: （適用於 hello VM) 的名稱、 使用者名稱、 驗證類型以及 hello 對應的認證、 Azure 訂用帳戶、 資源群組和位置。</span><span class="sxs-lookup"><span data-stu-id="13aaf-118">In hello Basics blade, supply values for hello required fields: Name (for hello VM), User name, Authentication type and hello corresponding credentials, Azure subscription, Resource group, and Location.</span></span>

   ![Create a new Ubuntu Image](./media/virtual-machines-linux-classic-ruby-rails-web-app/createvm.png)

4. <span data-ttu-id="13aaf-120">Hello VM 已佈建之後，按一下 hello VM 名稱，然後按一下**端點**在 hello**設定**類別目錄。</span><span class="sxs-lookup"><span data-stu-id="13aaf-120">After hello VM is provisioned, click on hello VM name, and click **Endpoints** in hello **Settings** category.</span></span> <span data-ttu-id="13aaf-121">找不到 hello SSH 端點，底下所列**獨立**。</span><span class="sxs-lookup"><span data-stu-id="13aaf-121">Find hello SSH endpoint, listed under **Standalone**.</span></span>

   ![預設端點](./media/virtual-machines-linux-classic-ruby-rails-web-app/endpointsnewportal.png)

### <a name="azure-cli"></a><span data-ttu-id="13aaf-123">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="13aaf-123">Azure CLI</span></span>
<span data-ttu-id="13aaf-124">中的 hello 步驟[建立執行 Linux 之虛擬機器][vm-instructions]。</span><span class="sxs-lookup"><span data-stu-id="13aaf-124">Follow hello steps in [Create a Virtual Machine Running Linux][vm-instructions].</span></span>

<span data-ttu-id="13aaf-125">Hello VM 已佈建之後，您可以藉由執行下列命令的 hello 取得 hello SSH 的端點：</span><span class="sxs-lookup"><span data-stu-id="13aaf-125">After hello VM is provisioned, you can get hello SSH endpoint by running hello following command:</span></span>

    azure vm endpoint list <vm-name>  

## <a name="install-ruby-on-rails"></a><span data-ttu-id="13aaf-126">安裝 Ruby on Rails</span><span class="sxs-lookup"><span data-stu-id="13aaf-126">Install Ruby on Rails</span></span>
1. <span data-ttu-id="13aaf-127">使用 SSH tooconnect toohello VM。</span><span class="sxs-lookup"><span data-stu-id="13aaf-127">Use SSH tooconnect toohello VM.</span></span>
2. <span data-ttu-id="13aaf-128">從 hello SSH 工作階段，使用下列命令 tooinstall Ruby hello VM 上的 hello:</span><span class="sxs-lookup"><span data-stu-id="13aaf-128">From hello SSH session, use hello following commands tooinstall Ruby on hello VM:</span></span>

        sudo apt-get update -y
        sudo apt-get upgrade -y

        sudo apt-add-repository ppa:brightbox/ruby-ng
        sudo apt-get update
        sudo apt-get install ruby2.4

        > [!TIP]
        > hello brightbox repository contains hello current Ruby distribution.

    <span data-ttu-id="13aaf-129">hello 安裝可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="13aaf-129">hello installation may take a few minutes.</span></span> <span data-ttu-id="13aaf-130">完成之後，使用下列命令 tooverify Ruby 已安裝的 hello:</span><span class="sxs-lookup"><span data-stu-id="13aaf-130">When it completes, use hello following command tooverify that Ruby is installed:</span></span>

        ruby -v

3. <span data-ttu-id="13aaf-131">使用 hello 下列命令 tooinstall 滑軌：</span><span class="sxs-lookup"><span data-stu-id="13aaf-131">Use hello following command tooinstall Rails:</span></span>

        sudo gem install rails --no-rdoc --no-ri -V

    <span data-ttu-id="13aaf-132">使用 hello-否 rdoc 和--無 ri 旗標 tooskip 安裝 hello 文件集，這種方式快。</span><span class="sxs-lookup"><span data-stu-id="13aaf-132">Use hello --no-rdoc and --no-ri flags tooskip installing hello documentation, which is faster.</span></span>
    <span data-ttu-id="13aaf-133">此命令很可能會很長的時間 tooexecute，因此加入 hello-V 會顯示 hello 安裝進度的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="13aaf-133">This command will likely take a long time tooexecute, so adding hello -V will display information about hello installation progress.</span></span>

## <a name="create-and-run-an-app"></a><span data-ttu-id="13aaf-134">建立及執行應用程式</span><span class="sxs-lookup"><span data-stu-id="13aaf-134">Create and run an app</span></span>
<span data-ttu-id="13aaf-135">仍透過 SSH 登入，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="13aaf-135">While still logged in via SSH, run hello following commands:</span></span>

    rails new myapp
    cd myapp
    rails server -b 0.0.0.0 -p 3000

<span data-ttu-id="13aaf-136">hello[新](http://guides.rubyonrails.org/command_line.html#rails-new)命令會建立新的滑軌應用程式。</span><span class="sxs-lookup"><span data-stu-id="13aaf-136">hello [new](http://guides.rubyonrails.org/command_line.html#rails-new) command creates a new Rails app.</span></span> <span data-ttu-id="13aaf-137">hello[伺服器](http://guides.rubyonrails.org/command_line.html#rails-server)啟動 hello WEBrick 滑軌所隨附的 web 伺服器的命令。</span><span class="sxs-lookup"><span data-stu-id="13aaf-137">hello [server](http://guides.rubyonrails.org/command_line.html#rails-server) command starts hello WEBrick web server that comes with Rails.</span></span> <span data-ttu-id="13aaf-138">（用於實際執行環境，您可能會想 toouse 不同的伺服器，例如獨角獸或旅客。）</span><span class="sxs-lookup"><span data-stu-id="13aaf-138">(For production use, you would probably want toouse a different server, such as Unicorn or Passenger.)</span></span>

<span data-ttu-id="13aaf-139">您應該會看到類似 toohello 下列輸出。</span><span class="sxs-lookup"><span data-stu-id="13aaf-139">You should see output similar toohello following.</span></span>

    => Booting WEBrick
    => Rails 4.2.1 application starting in development on http://0.0.0.0:3000
    => Run `rails server -h` for more startup options
    => Ctrl-C tooshutdown server
    [2015-06-09 23:34:23] INFO  WEBrick 1.3.1
    [2015-06-09 23:34:23] INFO  ruby 1.9.3 (2013-11-22) [x86_64-linux]
    [2015-06-09 23:34:23] INFO  WEBrick::HTTPServer#start: pid=27766 port=3000

## <a name="add-an-endpoint"></a><span data-ttu-id="13aaf-140">新增端點。</span><span class="sxs-lookup"><span data-stu-id="13aaf-140">Add an endpoint</span></span>
1. <span data-ttu-id="13aaf-141">前往 [Azure 入口網站] toohello [https://portal.azure.com] 並選取您的 VM。</span><span class="sxs-lookup"><span data-stu-id="13aaf-141">Go toohello [Azure portal][https://portal.azure.com] and select your VM.</span></span>

2. <span data-ttu-id="13aaf-142">選取**端點**在 hello**設定**沿著 hello 左邊的緣 hello 頁面。</span><span class="sxs-lookup"><span data-stu-id="13aaf-142">Select **ENDPOINTS** in hello **Settings** along hello left edge hello page.</span></span>

3. <span data-ttu-id="13aaf-143">按一下**新增**hello 頁面頂端的 hello。</span><span class="sxs-lookup"><span data-stu-id="13aaf-143">Click **ADD** at hello top of hello page.</span></span>

4. <span data-ttu-id="13aaf-144">在 hello**加入端點**對話方塊頁面上，輸入下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="13aaf-144">In hello **Add endpoint** dialog page, enter hello following information:</span></span>

   * <span data-ttu-id="13aaf-145">**名稱**：HTTP</span><span class="sxs-lookup"><span data-stu-id="13aaf-145">**Name**: HTTP</span></span>
   * <span data-ttu-id="13aaf-146">**通訊協定**：TCP</span><span class="sxs-lookup"><span data-stu-id="13aaf-146">**Protocol**: TCP</span></span>
   * <span data-ttu-id="13aaf-147">**公用連接埠**：80</span><span class="sxs-lookup"><span data-stu-id="13aaf-147">**Public port**: 80</span></span>
   * <span data-ttu-id="13aaf-148">**私用連接埠**：3000</span><span class="sxs-lookup"><span data-stu-id="13aaf-148">**Private port**: 3000</span></span>
   * <span data-ttu-id="13aaf-149">**浮動 IP 位址**：已停用</span><span class="sxs-lookup"><span data-stu-id="13aaf-149">**Floating PI address**: Disabled</span></span>
   * <span data-ttu-id="13aaf-150">**存取控制清單順序**: 1001，或另一個值，此存取規則 hello 優先權設定。</span><span class="sxs-lookup"><span data-stu-id="13aaf-150">**Access control list - Order**: 1001, or another value that sets hello priority of this access rule.</span></span>
   * <span data-ttu-id="13aaf-151">**存取控制清單 - 名稱**：allowHTTP</span><span class="sxs-lookup"><span data-stu-id="13aaf-151">**Access control list - Name**: allowHTTP</span></span>
   * <span data-ttu-id="13aaf-152">**存取控制清單 - 動作**：允許</span><span class="sxs-lookup"><span data-stu-id="13aaf-152">**Access control list - Action**: permit</span></span>
   * <span data-ttu-id="13aaf-153">**存取控制清單 - 遠端子網路**：1.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="13aaf-153">**Access control list - Remote subnet**: 1.0.0.0/16</span></span>

     <span data-ttu-id="13aaf-154">此端點都有會路由傳送流量 toohello 私用連接埠 3000、 hello 滑軌伺服器正在接聽所在的 80 的公用連接埠。</span><span class="sxs-lookup"><span data-stu-id="13aaf-154">This endpoint  has a public port of 80 that will route traffic toohello private port of 3000, where hello Rails server is listening.</span></span> <span data-ttu-id="13aaf-155">hello 存取控制清單規則可讓公用連接埠 80 上的流量。</span><span class="sxs-lookup"><span data-stu-id="13aaf-155">hello access control list rule allows public traffic on port 80.</span></span>

     ![new-endpoint](./media/virtual-machines-linux-classic-ruby-rails-web-app/createendpoint.png)

5. <span data-ttu-id="13aaf-157">按一下 [確定] toosave hello 端點。</span><span class="sxs-lookup"><span data-stu-id="13aaf-157">Click OK toosave hello endpoint.</span></span>

6. <span data-ttu-id="13aaf-158">此時應會出現一則訊息，指出「正在儲存虛擬機器端點」。</span><span class="sxs-lookup"><span data-stu-id="13aaf-158">A message should appear that states **Saving virtual machine endpoint**.</span></span> <span data-ttu-id="13aaf-159">此訊息會消失，一旦 hello 端點為作用中。</span><span class="sxs-lookup"><span data-stu-id="13aaf-159">Once this message disappears, hello endpoint is active.</span></span> <span data-ttu-id="13aaf-160">現在，您可能會測試您的應用程式瀏覽您的虛擬機器 toohello DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="13aaf-160">You may now test your application by navigating toohello DNS name of your virtual machine.</span></span> <span data-ttu-id="13aaf-161">hello 網站應該會出現類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="13aaf-161">hello website should appear similar toohello following:</span></span>

    ![預設 rails 頁面][default-rails-cloud]

## <a name="next-steps"></a><span data-ttu-id="13aaf-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="13aaf-163">Next steps</span></span>
<span data-ttu-id="13aaf-164">在本教學課程中，您所執行大部分的 hello 步驟手動。</span><span class="sxs-lookup"><span data-stu-id="13aaf-164">In this tutorial, you did most of hello steps manually.</span></span> <span data-ttu-id="13aaf-165">在實際執行環境中，您會在開發電腦上撰寫應用程式，並將其部署 toohello Azure VM。</span><span class="sxs-lookup"><span data-stu-id="13aaf-165">In a production environment, you would write your app on a development machine and deploy it toohello Azure VM.</span></span> <span data-ttu-id="13aaf-166">此外，大部分的實際執行環境裝載 hello 滑軌應用程式搭配另一個伺服器處理序，例如 Apache 或 NginX，以處理要求的 hello 滑軌應用程式和服務靜態資源的路由 toomultiple 執行個體。</span><span class="sxs-lookup"><span data-stu-id="13aaf-166">Also, most production environments host hello Rails application in conjunction with another server process such as Apache or NginX, which handles request routing toomultiple instances of hello Rails application and serving static resources.</span></span> <span data-ttu-id="13aaf-167">如需詳細資訊，請參閱 http://rubyonrails.org/deploy/。</span><span class="sxs-lookup"><span data-stu-id="13aaf-167">For more information, see http://rubyonrails.org/deploy/.</span></span>

<span data-ttu-id="13aaf-168">toolearn 深入了解 Ruby 上滑軌中，瀏覽 hello[拼音滑軌輔助線][rails-guides]。</span><span class="sxs-lookup"><span data-stu-id="13aaf-168">toolearn more about Ruby on Rails, visit hello [Ruby on Rails Guides][rails-guides].</span></span>

<span data-ttu-id="13aaf-169">toouse 從 Ruby 應用程式的 Azure 服務，請參閱：</span><span class="sxs-lookup"><span data-stu-id="13aaf-169">toouse Azure services from your Ruby application, see:</span></span>

* <span data-ttu-id="13aaf-170">[使用 Blob 儲存非結構化資料][blobs]</span><span class="sxs-lookup"><span data-stu-id="13aaf-170">[Store unstructured data using blobs][blobs]</span></span>
* <span data-ttu-id="13aaf-171">[使用資料表儲存機碼/值組][tables]</span><span class="sxs-lookup"><span data-stu-id="13aaf-171">[Store key/value pairs using tables][tables]</span></span>
* <span data-ttu-id="13aaf-172">[提供高頻寬內容以 hello 內容傳遞網路][cdn-howto]</span><span class="sxs-lookup"><span data-stu-id="13aaf-172">[Serve high bandwidth content with hello Content Delivery Network][cdn-howto]</span></span>

<!-- WA.com links -->
[blobs]:../../../storage/blobs/storage-ruby-how-to-use-blob-storage.md
[cdn-howto]:https://azure.microsoft.com/develop/ruby/app-services/
[tables]:../../../cosmos-db/table-storage-how-to-use-ruby.md
[vm-instructions]:createportal.md

<!-- External Links -->
[rails-guides]:http://guides.rubyonrails.org/
[sqlite3]:http://www.sqlite.org/

<!-- Images -->

[default-rails-cloud]:./media/virtual-machines-linux-classic-ruby-rails-web-app/basicrailscloud.png
[vmlist]:./media/virtual-machines-linux-classic-ruby-rails-web-app/vmlist.png
[endpoints]:./media/virtual-machines-linux-classic-ruby-rails-web-app/endpoints.png
[new-endpoint]:./media/virtual-machines-linux-classic-ruby-rails-web-app/newendpoint.png
[new-endpoint1]:./media/virtual-machines-linux-classic-ruby-rails-web-app/newendpoint1.png
