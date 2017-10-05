---
title: "在 Linux VM 上裝載 Ruby on Rails 網站 | Microsoft 文件"
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
ms.openlocfilehash: 0518519da6c5e62a863a47d6743ab7b7c5923acf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="ruby-on-rails-web-application-on-an-azure-vm"></a><span data-ttu-id="39f6c-103">Azure VM 上的 Ruby on Rails Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="39f6c-103">Ruby on Rails Web application on an Azure VM</span></span>
<span data-ttu-id="39f6c-104">此教學課程說明如何在 Azure 上使用 Linux 虛擬機器，於 Rails 網站裝載 Ruby。</span><span class="sxs-lookup"><span data-stu-id="39f6c-104">This tutorial shows how to host a Ruby on Rails website on Azure using a Linux virtual machine.</span></span>  

<span data-ttu-id="39f6c-105">此教學課程使用 Ubuntu Server 14.04 LTS 通過驗證。</span><span class="sxs-lookup"><span data-stu-id="39f6c-105">This tutorial was validated using Ubuntu Server 14.04 LTS.</span></span> <span data-ttu-id="39f6c-106">若使用不同的 Linux 發行版本，您可能需要修改這些步驟以安裝 Rails。</span><span class="sxs-lookup"><span data-stu-id="39f6c-106">If you use a different Linux distribution, you might need to modify the steps to install Rails.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="39f6c-107">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../../../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="39f6c-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="39f6c-108">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="39f6c-108">This article covers using the classic deployment model.</span></span> <span data-ttu-id="39f6c-109">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="39f6c-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>
>
>

## <a name="create-an-azure-vm"></a><span data-ttu-id="39f6c-110">建立 Azure VM</span><span class="sxs-lookup"><span data-stu-id="39f6c-110">Create an Azure VM</span></span>
<span data-ttu-id="39f6c-111">開始使用 Linux 映像建立 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="39f6c-111">Start by creating an Azure VM with a Linux image.</span></span>

<span data-ttu-id="39f6c-112">若要建立 VM，您可以使用 Azure 入口網站或 Azure 命令列介面 (CLI)。</span><span class="sxs-lookup"><span data-stu-id="39f6c-112">To create the VM, you can use the Azure portal or the Azure Command-Line Interface (CLI).</span></span>

### <a name="azure-portal"></a><span data-ttu-id="39f6c-113">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="39f6c-113">Azure portal</span></span>
1. <span data-ttu-id="39f6c-114">登入 [Azure 入口網站](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="39f6c-114">Sign into the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="39f6c-115">按一下 [新增]，然後在搜尋方塊中輸入 "Ubuntu Server 14.04"。</span><span class="sxs-lookup"><span data-stu-id="39f6c-115">Click **New**, then type "Ubuntu Server 14.04" in the search box.</span></span> <span data-ttu-id="39f6c-116">按一下由搜尋傳回的項目。</span><span class="sxs-lookup"><span data-stu-id="39f6c-116">Click the entry returned by the search.</span></span> <span data-ttu-id="39f6c-117">針對部署模型，選取 [傳統]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="39f6c-117">For the deployment model, select **Classic**, then click "Create".</span></span>
3. <span data-ttu-id="39f6c-118">在 [基本] 刀鋒視窗中，提供必要欄位的值：名稱 (適用於 VM)、使用者名稱、驗證類型和對應的認證、Azure 訂用帳戶、資源群組及位置。</span><span class="sxs-lookup"><span data-stu-id="39f6c-118">In the Basics blade, supply values for the required fields: Name (for the VM), User name, Authentication type and the corresponding credentials, Azure subscription, Resource group, and Location.</span></span>

   ![Create a new Ubuntu Image](./media/virtual-machines-linux-classic-ruby-rails-web-app/createvm.png)

4. <span data-ttu-id="39f6c-120">佈建 VM 之後，按一下 VM 名稱，然後按一下 [設定] 分類中的 [端點]。</span><span class="sxs-lookup"><span data-stu-id="39f6c-120">After the VM is provisioned, click on the VM name, and click **Endpoints** in the **Settings** category.</span></span> <span data-ttu-id="39f6c-121">尋找列在 [獨立] 下方的 SSH 端點。</span><span class="sxs-lookup"><span data-stu-id="39f6c-121">Find the SSH endpoint, listed under **Standalone**.</span></span>

   ![預設端點](./media/virtual-machines-linux-classic-ruby-rails-web-app/endpointsnewportal.png)

### <a name="azure-cli"></a><span data-ttu-id="39f6c-123">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="39f6c-123">Azure CLI</span></span>
<span data-ttu-id="39f6c-124">請依照[建立執行 Linux 的虛擬機器][vm-instructions]中的步驟執行。</span><span class="sxs-lookup"><span data-stu-id="39f6c-124">Follow the steps in [Create a Virtual Machine Running Linux][vm-instructions].</span></span>

<span data-ttu-id="39f6c-125">佈建 VM 之後，您可以透過執行下列命令來取得 SSH 端點：</span><span class="sxs-lookup"><span data-stu-id="39f6c-125">After the VM is provisioned, you can get the SSH endpoint by running the following command:</span></span>

    azure vm endpoint list <vm-name>  

## <a name="install-ruby-on-rails"></a><span data-ttu-id="39f6c-126">安裝 Ruby on Rails</span><span class="sxs-lookup"><span data-stu-id="39f6c-126">Install Ruby on Rails</span></span>
1. <span data-ttu-id="39f6c-127">使用 SSH 連線到 VM。</span><span class="sxs-lookup"><span data-stu-id="39f6c-127">Use SSH to connect to the VM.</span></span>
2. <span data-ttu-id="39f6c-128">從 SSH 工作階段中，使用下列命令在 VM 上安裝 Ruby：</span><span class="sxs-lookup"><span data-stu-id="39f6c-128">From the SSH session, use the following commands to install Ruby on the VM:</span></span>

        sudo apt-get update -y
        sudo apt-get upgrade -y

        sudo apt-add-repository ppa:brightbox/ruby-ng
        sudo apt-get update
        sudo apt-get install ruby2.4

        > [!TIP]
        > The brightbox repository contains the current Ruby distribution.

    <span data-ttu-id="39f6c-129">安裝可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="39f6c-129">The installation may take a few minutes.</span></span> <span data-ttu-id="39f6c-130">完成時，請使用下列命令來確認 Ruby 是否已安裝：</span><span class="sxs-lookup"><span data-stu-id="39f6c-130">When it completes, use the following command to verify that Ruby is installed:</span></span>

        ruby -v

3. <span data-ttu-id="39f6c-131">使用下列命令來安裝 Rails：</span><span class="sxs-lookup"><span data-stu-id="39f6c-131">Use the following command to install Rails:</span></span>

        sudo gem install rails --no-rdoc --no-ri -V

    <span data-ttu-id="39f6c-132">使用 --no-rdoc 與 --no-ri 旗標來略過安裝文件，這樣安裝速度會比較快。</span><span class="sxs-lookup"><span data-stu-id="39f6c-132">Use the --no-rdoc and --no-ri flags to skip installing the documentation, which is faster.</span></span>
    <span data-ttu-id="39f6c-133">此命令的執行可能需要很長的時間，所以新增 -V 會顯示安裝進度的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="39f6c-133">This command will likely take a long time to execute, so adding the -V will display information about the installation progress.</span></span>

## <a name="create-and-run-an-app"></a><span data-ttu-id="39f6c-134">建立及執行應用程式</span><span class="sxs-lookup"><span data-stu-id="39f6c-134">Create and run an app</span></span>
<span data-ttu-id="39f6c-135">在仍透過 SSH 登入的情況下，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="39f6c-135">While still logged in via SSH, run the following commands:</span></span>

    rails new myapp
    cd myapp
    rails server -b 0.0.0.0 -p 3000

<span data-ttu-id="39f6c-136">[new](http://guides.rubyonrails.org/command_line.html#rails-new) 命令會建立新的 Rails 應用程式。</span><span class="sxs-lookup"><span data-stu-id="39f6c-136">The [new](http://guides.rubyonrails.org/command_line.html#rails-new) command creates a new Rails app.</span></span> <span data-ttu-id="39f6c-137">[server](http://guides.rubyonrails.org/command_line.html#rails-server) 命令會啟動 Rails 隨附的 WEBrick Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="39f6c-137">The [server](http://guides.rubyonrails.org/command_line.html#rails-server) command starts the WEBrick web server that comes with Rails.</span></span> <span data-ttu-id="39f6c-138">(對於實際執行環境用途，您可能想要使用不同的伺服器，例如 Unicorn 或 Passenger)。</span><span class="sxs-lookup"><span data-stu-id="39f6c-138">(For production use, you would probably want to use a different server, such as Unicorn or Passenger.)</span></span>

<span data-ttu-id="39f6c-139">您應該會看到如下所示的輸出。</span><span class="sxs-lookup"><span data-stu-id="39f6c-139">You should see output similar to the following.</span></span>

    => Booting WEBrick
    => Rails 4.2.1 application starting in development on http://0.0.0.0:3000
    => Run `rails server -h` for more startup options
    => Ctrl-C to shutdown server
    [2015-06-09 23:34:23] INFO  WEBrick 1.3.1
    [2015-06-09 23:34:23] INFO  ruby 1.9.3 (2013-11-22) [x86_64-linux]
    [2015-06-09 23:34:23] INFO  WEBrick::HTTPServer#start: pid=27766 port=3000

## <a name="add-an-endpoint"></a><span data-ttu-id="39f6c-140">新增端點。</span><span class="sxs-lookup"><span data-stu-id="39f6c-140">Add an endpoint</span></span>
1. <span data-ttu-id="39f6c-141">移至 [Azure 入口網站][https://portal.azure.com] 並選取您的 VM。</span><span class="sxs-lookup"><span data-stu-id="39f6c-141">Go to the [Azure portal][https://portal.azure.com] and select your VM.</span></span>

2. <span data-ttu-id="39f6c-142">在頁面左邊，選取 [設定] 中的 [端點]。</span><span class="sxs-lookup"><span data-stu-id="39f6c-142">Select **ENDPOINTS** in the **Settings** along the left edge the page.</span></span>

3. <span data-ttu-id="39f6c-143">按一下頁面頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="39f6c-143">Click **ADD** at the top of the page.</span></span>

4. <span data-ttu-id="39f6c-144">在 [新增端點] 對話方塊頁面中，輸入下列資訊：</span><span class="sxs-lookup"><span data-stu-id="39f6c-144">In the **Add endpoint** dialog page, enter the following information:</span></span>

   * <span data-ttu-id="39f6c-145">**名稱**：HTTP</span><span class="sxs-lookup"><span data-stu-id="39f6c-145">**Name**: HTTP</span></span>
   * <span data-ttu-id="39f6c-146">**通訊協定**：TCP</span><span class="sxs-lookup"><span data-stu-id="39f6c-146">**Protocol**: TCP</span></span>
   * <span data-ttu-id="39f6c-147">**公用連接埠**：80</span><span class="sxs-lookup"><span data-stu-id="39f6c-147">**Public port**: 80</span></span>
   * <span data-ttu-id="39f6c-148">**私用連接埠**：3000</span><span class="sxs-lookup"><span data-stu-id="39f6c-148">**Private port**: 3000</span></span>
   * <span data-ttu-id="39f6c-149">**浮動 IP 位址**：已停用</span><span class="sxs-lookup"><span data-stu-id="39f6c-149">**Floating PI address**: Disabled</span></span>
   * <span data-ttu-id="39f6c-150">**存取控制清單 - 順序**：1001，或另一個設定此存取規則之優先順序的值。</span><span class="sxs-lookup"><span data-stu-id="39f6c-150">**Access control list - Order**: 1001, or another value that sets the priority of this access rule.</span></span>
   * <span data-ttu-id="39f6c-151">**存取控制清單 - 名稱**：allowHTTP</span><span class="sxs-lookup"><span data-stu-id="39f6c-151">**Access control list - Name**: allowHTTP</span></span>
   * <span data-ttu-id="39f6c-152">**存取控制清單 - 動作**：允許</span><span class="sxs-lookup"><span data-stu-id="39f6c-152">**Access control list - Action**: permit</span></span>
   * <span data-ttu-id="39f6c-153">**存取控制清單 - 遠端子網路**：1.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="39f6c-153">**Access control list - Remote subnet**: 1.0.0.0/16</span></span>

     <span data-ttu-id="39f6c-154">此端點具有公用連接埠 80，其會將流量路由傳送至 Rails 伺服器所接聽的私用連接埠 3000。</span><span class="sxs-lookup"><span data-stu-id="39f6c-154">This endpoint  has a public port of 80 that will route traffic to the private port of 3000, where the Rails server is listening.</span></span> <span data-ttu-id="39f6c-155">存取控制清單規則允許連接埠 80 上的公用流量。</span><span class="sxs-lookup"><span data-stu-id="39f6c-155">The access control list rule allows public traffic on port 80.</span></span>

     ![new-endpoint](./media/virtual-machines-linux-classic-ruby-rails-web-app/createendpoint.png)

5. <span data-ttu-id="39f6c-157">按一下 [確定] 以儲存端點。</span><span class="sxs-lookup"><span data-stu-id="39f6c-157">Click OK to save the endpoint.</span></span>

6. <span data-ttu-id="39f6c-158">此時應會出現一則訊息，指出「正在儲存虛擬機器端點」。</span><span class="sxs-lookup"><span data-stu-id="39f6c-158">A message should appear that states **Saving virtual machine endpoint**.</span></span> <span data-ttu-id="39f6c-159">這個訊息消失後，端點便在作用中。</span><span class="sxs-lookup"><span data-stu-id="39f6c-159">Once this message disappears, the endpoint is active.</span></span> <span data-ttu-id="39f6c-160">您現在可以瀏覽至虛擬機器的 DNS 名稱，測試您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="39f6c-160">You may now test your application by navigating to the DNS name of your virtual machine.</span></span> <span data-ttu-id="39f6c-161">網站應如下所示：</span><span class="sxs-lookup"><span data-stu-id="39f6c-161">The website should appear similar to the following:</span></span>

    ![預設 rails 頁面][default-rails-cloud]

## <a name="next-steps"></a><span data-ttu-id="39f6c-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="39f6c-163">Next steps</span></span>
<span data-ttu-id="39f6c-164">在此教學課程中，您必須手動執行大部分的步驟。</span><span class="sxs-lookup"><span data-stu-id="39f6c-164">In this tutorial, you did most of the steps manually.</span></span> <span data-ttu-id="39f6c-165">在生產環境中，您會在開發電腦上撰寫應用程式，並將它部署至 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="39f6c-165">In a production environment, you would write your app on a development machine and deploy it to the Azure VM.</span></span> <span data-ttu-id="39f6c-166">另外，大部分生產環境均代管 Rails 應用程式以及 Apache 或 NginX 之類的其他伺服器程序，處理傳送至多個 Rails 應用程式及執行個體並提供靜態資源的要求。</span><span class="sxs-lookup"><span data-stu-id="39f6c-166">Also, most production environments host the Rails application in conjunction with another server process such as Apache or NginX, which handles request routing to multiple instances of the Rails application and serving static resources.</span></span> <span data-ttu-id="39f6c-167">如需詳細資訊，請參閱 http://rubyonrails.org/deploy/。</span><span class="sxs-lookup"><span data-stu-id="39f6c-167">For more information, see http://rubyonrails.org/deploy/.</span></span>

<span data-ttu-id="39f6c-168">若要深入了解 Ruby on Rails，請瀏覽 [Ruby on Rails 指南 (英文)][rails-guides]。</span><span class="sxs-lookup"><span data-stu-id="39f6c-168">To learn more about Ruby on Rails, visit the [Ruby on Rails Guides][rails-guides].</span></span>

<span data-ttu-id="39f6c-169">若要從您的 Ruby 應用程式 使用 Azure 服務，請參閱：</span><span class="sxs-lookup"><span data-stu-id="39f6c-169">To use Azure services from your Ruby application, see:</span></span>

* <span data-ttu-id="39f6c-170">[使用 Blob 儲存非結構化資料][blobs]</span><span class="sxs-lookup"><span data-stu-id="39f6c-170">[Store unstructured data using blobs][blobs]</span></span>
* <span data-ttu-id="39f6c-171">[使用資料表儲存機碼/值組][tables]</span><span class="sxs-lookup"><span data-stu-id="39f6c-171">[Store key/value pairs using tables][tables]</span></span>
* <span data-ttu-id="39f6c-172">[使用內容傳遞網路提供高頻寬內容][cdn-howto]</span><span class="sxs-lookup"><span data-stu-id="39f6c-172">[Serve high bandwidth content with the Content Delivery Network][cdn-howto]</span></span>

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
