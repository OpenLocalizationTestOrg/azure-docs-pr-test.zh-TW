---
title: "aaaDeploy 第一個應用程式 tooCloud Microsoft Azure 上 Foundry |Microsoft 文件"
description: "部署應用程式 tooCloud Foundry 在 Azure 上"
services: virtual-machines-linux
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 8fa04a58-56ad-4e6c-bef4-d02c80d4b60f
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/14/2017
ms.author: seanmck
ms.openlocfilehash: 878da38f6eabe32a339f02aa0ead811d6e5af9a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-first-app-toocloud-foundry-on-microsoft-azure"></a><span data-ttu-id="d6ffc-103">部署第一個應用程式 tooCloud Foundry Microsoft Azure 上</span><span class="sxs-lookup"><span data-stu-id="d6ffc-103">Deploy your first app tooCloud Foundry on Microsoft Azure</span></span>

<span data-ttu-id="d6ffc-104">[Cloud Foundry](http://cloudfoundry.org) 是 Microsoft Azure 上可用的熱門開放原始碼應用程式平台。</span><span class="sxs-lookup"><span data-stu-id="d6ffc-104">[Cloud Foundry](http://cloudfoundry.org) is a popular open-source application platform available on Microsoft Azure.</span></span> <span data-ttu-id="d6ffc-105">在本文中，我們會示範如何 toodeploy 及管理雲端 Foundry Azure 環境中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d6ffc-105">In this article, we show how toodeploy and manage an application on Cloud Foundry in an Azure environment.</span></span>

## <a name="create-a-cloud-foundry-environment"></a><span data-ttu-id="d6ffc-106">建立 Cloud Foundry 環境</span><span class="sxs-lookup"><span data-stu-id="d6ffc-106">Create a Cloud Foundry environment</span></span>

<span data-ttu-id="d6ffc-107">有幾個選項可以用來在 Azure 上建立 Cloud Foundry 環境：</span><span class="sxs-lookup"><span data-stu-id="d6ffc-107">There are several options for creating a Cloud Foundry environment on Azure:</span></span>

- <span data-ttu-id="d6ffc-108">使用 hello[關鍵雲端 Foundry 優惠][ pcf-azuremarketplace] hello Azure Marketplace toocreate 包含 PCF Ops Manager 和 hello Azure Service Broker 的標準環境中。</span><span class="sxs-lookup"><span data-stu-id="d6ffc-108">Use hello [Pivotal Cloud Foundry offer][pcf-azuremarketplace] in hello Azure Marketplace toocreate a standard environment that includes PCF Ops Manager and hello Azure Service Broker.</span></span> <span data-ttu-id="d6ffc-109">您可以找到[完成指示][ pcf-azuremarketplace-pivotaldocs]部署 hello marketplace 提供 hello 關鍵的文件中。</span><span class="sxs-lookup"><span data-stu-id="d6ffc-109">You can find [complete instructions][pcf-azuremarketplace-pivotaldocs] for deploying hello marketplace offer in hello Pivotal documentation.</span></span>
- <span data-ttu-id="d6ffc-110">建立自訂的環境，方法是[手動部署 Pivotal Cloud Foundry][pcf-custom]。</span><span class="sxs-lookup"><span data-stu-id="d6ffc-110">Create a customized environment by [deploying Pivotal Cloud Foundry manually][pcf-custom].</span></span>
- <span data-ttu-id="d6ffc-111">[直接部署 hello 開放原始碼雲端 Foundry 封裝][ oss-cf-bosh]藉由設定[BOSH](http://bosh.io)導向器，協調 hello Foundry 雲端環境的 hello 部署的 VM。</span><span class="sxs-lookup"><span data-stu-id="d6ffc-111">[Deploy hello open-source Cloud Foundry packages directly][oss-cf-bosh] by setting up a [BOSH](http://bosh.io) director, a VM that coordinates hello deployment of hello Cloud Foundry environment.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="d6ffc-112">如果您要部署 PCF hello Azure Marketplace 中，記下 hello SYSTEMDOMAINURL 和 tooaccess hello 關鍵應用程式管理員 中，這兩種指南所述 hello marketplace 部署所需的 hello 系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="d6ffc-112">If you are deploying PCF from hello Azure Marketplace, make a note of hello SYSTEMDOMAINURL and hello admin credentials required tooaccess hello Pivotal Apps Manager, both of which are described in hello marketplace deployment guide.</span></span> <span data-ttu-id="d6ffc-113">它們是本教學課程所需的 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="d6ffc-113">They are needed toocomplete this tutorial.</span></span> <span data-ttu-id="d6ffc-114">Marketplace 部署的 hello SYSTEMDOMAINURL 處於 hello 表單 https://system。*ip 位址*。 cf.pcfazure.com。</span><span class="sxs-lookup"><span data-stu-id="d6ffc-114">For marketplace deployments, hello SYSTEMDOMAINURL is in hello form https://system.*ip-address*.cf.pcfazure.com.</span></span>

## <a name="connect-toohello-cloud-controller"></a><span data-ttu-id="d6ffc-115">連接 toohello 雲端控制器</span><span class="sxs-lookup"><span data-stu-id="d6ffc-115">Connect toohello Cloud Controller</span></span>

<span data-ttu-id="d6ffc-116">hello 雲端控制站是 hello 主要進入點 tooa 雲端 Foundry 環境來部署和管理應用程式。</span><span class="sxs-lookup"><span data-stu-id="d6ffc-116">hello Cloud Controller is hello primary entry point tooa Cloud Foundry environment for deploying and managing applications.</span></span> <span data-ttu-id="d6ffc-117">hello 核心雲端控制站應用程式開發介面 (CCAPI) 是 REST API，但可透過各種工具存取。</span><span class="sxs-lookup"><span data-stu-id="d6ffc-117">hello core Cloud Controller API (CCAPI) is a REST API, but it is accessible through various tools.</span></span> <span data-ttu-id="d6ffc-118">在此情況下，我們藉此與其互動透過 hello[雲端 Foundry CLI][cf-cli]。</span><span class="sxs-lookup"><span data-stu-id="d6ffc-118">In this case, we interact with it through hello [Cloud Foundry CLI][cf-cli].</span></span> <span data-ttu-id="d6ffc-119">您可以安裝 hello CLI Linux、 MacOS、 或 Windows，但如果您想使用 tooinstall 它，並使用預先安裝在 hello [Azure 雲端殼層][cloudshell-docs]。</span><span class="sxs-lookup"><span data-stu-id="d6ffc-119">You can install hello CLI on Linux, MacOS, or Windows, but if you'd prefer not tooinstall it at all, it is available pre-installed in hello [Azure Cloud Shell][cloudshell-docs].</span></span>

<span data-ttu-id="d6ffc-120">在中，toolog 前面加上`api`toohello SYSTEMDOMAINURL 您從 hello marketplace 部署取得。</span><span class="sxs-lookup"><span data-stu-id="d6ffc-120">toolog in, prepend `api` toohello SYSTEMDOMAINURL that you obtained from hello marketplace deployment.</span></span> <span data-ttu-id="d6ffc-121">因為 hello 預設部署伺服器使用自我簽署的憑證，您也應該包括 hello`skip-ssl-validation`切換。</span><span class="sxs-lookup"><span data-stu-id="d6ffc-121">Since hello default deployment uses a self-signed certificate, you should also include hello `skip-ssl-validation` switch.</span></span>

```bash
cf login -a https://api.SYSTEMDOMAINURL --skip-ssl-validation
```

<span data-ttu-id="d6ffc-122">您必須提示的 toolog toohello 雲端控制站中。</span><span class="sxs-lookup"><span data-stu-id="d6ffc-122">You are prompted toolog in toohello Cloud Controller.</span></span> <span data-ttu-id="d6ffc-123">使用貴用戶取得 hello marketplace 部署步驟中的 hello 系統管理員帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="d6ffc-123">Use hello admin account credentials that you acquired from hello marketplace deployment steps.</span></span>

<span data-ttu-id="d6ffc-124">提供雲端 Foundry*入*和*空格*做為命名空間 tooisolate hello 小組和環境中共用的部署。</span><span class="sxs-lookup"><span data-stu-id="d6ffc-124">Cloud Foundry provides *orgs* and *spaces* as namespaces tooisolate hello teams and environments within a shared deployment.</span></span> <span data-ttu-id="d6ffc-125">hello PCF marketplace 部署包含 hello 預設*系統*組織一組的空間建立和 toocontain hello 基礎元件，例如 hello 自動調整服務和 hello Azure 的 service broker。</span><span class="sxs-lookup"><span data-stu-id="d6ffc-125">hello PCF marketplace deployment includes hello default *system* org and a set of spaces created toocontain hello base components, like hello autoscaling service and hello Azure service broker.</span></span> <span data-ttu-id="d6ffc-126">現在請選擇 hello*系統*空間。</span><span class="sxs-lookup"><span data-stu-id="d6ffc-126">For now, choose hello *system* space.</span></span>


## <a name="create-an-org-and-space"></a><span data-ttu-id="d6ffc-127">建立組織和空間</span><span class="sxs-lookup"><span data-stu-id="d6ffc-127">Create an org and space</span></span>

<span data-ttu-id="d6ffc-128">如果您輸入`cf apps`，您會看到一組內 hello 系統 my.app hello 系統空間中已部署的系統應用程式</span><span class="sxs-lookup"><span data-stu-id="d6ffc-128">If you type `cf apps`, you see a set of system applications that have been deployed in hello system space within hello system org.</span></span> 

<span data-ttu-id="d6ffc-129">您應該保留 hello*系統*組織保留給系統應用程式，因此建立組織及空間 toohouse 我們的範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="d6ffc-129">You should keep hello *system* org reserved for system applications, so create an org and space toohouse our sample application.</span></span>

```bash
cf create-org myorg
cf create-space dev -o myorg
```

<span data-ttu-id="d6ffc-130">使用 hello 目標命令 tooswitch toohello 新組織和空間：</span><span class="sxs-lookup"><span data-stu-id="d6ffc-130">Use hello target command tooswitch toohello new org and space:</span></span>

```bash
cf target -o testorg -s dev
```

<span data-ttu-id="d6ffc-131">現在，當您部署應用程式時，它會自動建立在 hello 新組織及空間。</span><span class="sxs-lookup"><span data-stu-id="d6ffc-131">Now, when you deploy an application, it is automatically created in hello new org and space.</span></span> <span data-ttu-id="d6ffc-132">目前沒有的 tooconfirm hello 新組織/在空間中，沒有應用程式輸入`cf apps`一次。</span><span class="sxs-lookup"><span data-stu-id="d6ffc-132">tooconfirm that there are currently no apps in hello new org/space, type `cf apps` again.</span></span>

> [!NOTE] 
> <span data-ttu-id="d6ffc-133">如需入空格及如何使用它們以角色為基礎的存取控制 (RBAC) 的詳細資訊，請參閱 hello[雲端 Foundry 文件][cf-orgs-spaces-docs]。</span><span class="sxs-lookup"><span data-stu-id="d6ffc-133">For more information about orgs and spaces and how they can be used for role-based access control (RBAC), see hello [Cloud Foundry documentation][cf-orgs-spaces-docs].</span></span>

## <a name="deploy-an-application"></a><span data-ttu-id="d6ffc-134">部署應用程式</span><span class="sxs-lookup"><span data-stu-id="d6ffc-134">Deploy an application</span></span>

<span data-ttu-id="d6ffc-135">讓我們使用範例雲端 Foundry 應用程式呼叫 Hello Spring 雲端，這是以 Java 撰寫，且根據 hello [Spring 架構](http://spring.io)和[Spring 開機](http://projects.spring.io/spring-boot/)。</span><span class="sxs-lookup"><span data-stu-id="d6ffc-135">Let's use a sample Cloud Foundry application called Hello Spring Cloud, which is written in Java and based on hello [Spring Framework](http://spring.io) and [Spring Boot](http://projects.spring.io/spring-boot/).</span></span>

### <a name="clone-hello-hello-spring-cloud-repository"></a><span data-ttu-id="d6ffc-136">複製 hello Hello Spring 雲端儲存機制</span><span class="sxs-lookup"><span data-stu-id="d6ffc-136">Clone hello Hello Spring Cloud repository</span></span>

<span data-ttu-id="d6ffc-137">GitHub 上使用 hello Hello Spring 雲端範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="d6ffc-137">hello Hello Spring Cloud sample application is available on GitHub.</span></span> <span data-ttu-id="d6ffc-138">複製它 tooyour 環境，並變更到新目錄中 hello:</span><span class="sxs-lookup"><span data-stu-id="d6ffc-138">Clone it tooyour environment and change into hello new directory:</span></span>

```bash
git clone https://github.com/cloudfoundry-samples/hello-spring-cloud
cd hello-spring-cloud
```

### <a name="build-hello-application"></a><span data-ttu-id="d6ffc-139">建置 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="d6ffc-139">Build hello application</span></span>

<span data-ttu-id="d6ffc-140">組建 hello 應用程式使用[Apache Maven](http://maven.apache.org)。</span><span class="sxs-lookup"><span data-stu-id="d6ffc-140">Build hello app using [Apache Maven](http://maven.apache.org).</span></span>

```bash
mvn clean package
```

### <a name="deploy-hello-application-with-cf-push"></a><span data-ttu-id="d6ffc-141">部署 hello 與 cf 推入的應用程式</span><span class="sxs-lookup"><span data-stu-id="d6ffc-141">Deploy hello application with cf push</span></span>

<span data-ttu-id="d6ffc-142">您可以部署大部分的應用程式 tooCloud Foundry 使用 hello`push`命令：</span><span class="sxs-lookup"><span data-stu-id="d6ffc-142">You can deploy most applications tooCloud Foundry using hello `push` command:</span></span>

```bash
cf push
```

<span data-ttu-id="d6ffc-143">當您*發送*應用程式時，雲端 Foundry 會偵測 hello （在這個情況下，Java 應用程式） 的應用程式類型，並識別其相依性 （在此案例中的 hello Spring 架構）。</span><span class="sxs-lookup"><span data-stu-id="d6ffc-143">When you *push* an application, Cloud Foundry detects hello type of application (in this case, a Java app) and identifies its dependencies (in this case, hello Spring framework).</span></span> <span data-ttu-id="d6ffc-144">封裝的所有項目所需 toorun 您的程式碼的獨立容器映像，又稱為*droplet*。</span><span class="sxs-lookup"><span data-stu-id="d6ffc-144">It then packages everything required toorun your code into a standalone container image, known as a *droplet*.</span></span> <span data-ttu-id="d6ffc-145">最後，雲端 Foundry 排程 hello 其中一個環境中的 hello 可用電腦上的應用程式，並建立，您可能會達到，hello hello 命令輸出中所提供的 URL。</span><span class="sxs-lookup"><span data-stu-id="d6ffc-145">Finally, Cloud Foundry schedules hello application on one of hello available machines in your environment and creates a URL where you can reach it, which is available in hello output of hello command.</span></span>

![cf push 命令的輸出][cf-push-output]

<span data-ttu-id="d6ffc-147">toosee hello hello spring 雲端應用程式，您的瀏覽器中開啟 hello 提供 URL:</span><span class="sxs-lookup"><span data-stu-id="d6ffc-147">toosee hello hello-spring-cloud application, open hello provided URL in your browser:</span></span>

![Hello Spring Cloud 的預設 UI][hello-spring-cloud-basic]

> [!NOTE] 
> <span data-ttu-id="d6ffc-149">深入了解時會發生什麼事 toolearn `cf push`，請參閱[暫存應用程式如何][ cf-push-docs] hello 雲端 Foundry 文件中。</span><span class="sxs-lookup"><span data-stu-id="d6ffc-149">toolearn more about what happens during `cf push`, see [How Applications Are Staged][cf-push-docs] in hello Cloud Foundry documentation.</span></span>

## <a name="view-application-logs"></a><span data-ttu-id="d6ffc-150">檢視應用程式記錄</span><span class="sxs-lookup"><span data-stu-id="d6ffc-150">View application logs</span></span>

<span data-ttu-id="d6ffc-151">您可以使用應用程式的 hello 雲端 Foundry CLI tooview 記錄檔的名稱：</span><span class="sxs-lookup"><span data-stu-id="d6ffc-151">You can use hello Cloud Foundry CLI tooview logs for an application by its name:</span></span>

```bash
cf logs hello-spring-cloud
```

<span data-ttu-id="d6ffc-152">根據預設，hello 記錄命令使用*結尾*，其中會顯示新的記錄檔，當它們被寫入。</span><span class="sxs-lookup"><span data-stu-id="d6ffc-152">By default, hello logs command uses *tail*, which shows new logs as they are written.</span></span> <span data-ttu-id="d6ffc-153">toosee 新記錄檔都會出現，請重新整理 hello 瀏覽器中的 hello hello spring 雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="d6ffc-153">toosee new logs appear, refresh hello hello-spring-cloud app in hello browser.</span></span>

<span data-ttu-id="d6ffc-154">tooview 記錄已經寫入、 新增 hello`recent`切換：</span><span class="sxs-lookup"><span data-stu-id="d6ffc-154">tooview logs that have already been written, add hello `recent` switch:</span></span>

```bash
cf logs --recent hello-spring-cloud
```

## <a name="scale-hello-application"></a><span data-ttu-id="d6ffc-155">標尺 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="d6ffc-155">Scale hello application</span></span>

<span data-ttu-id="d6ffc-156">根據預設，`cf push` 只會建立應用程式的單一執行個體。</span><span class="sxs-lookup"><span data-stu-id="d6ffc-156">By default, `cf push` only creates a single instance of your application.</span></span> <span data-ttu-id="d6ffc-157">tooensure 高可用性和啟用向外延展的較高的輸送量，您通常想 toorun 多個應用程式的一個執行個體。</span><span class="sxs-lookup"><span data-stu-id="d6ffc-157">tooensure high availability and enable scale out for higher throughput, you generally want toorun more than one instance of your applications.</span></span> <span data-ttu-id="d6ffc-158">您可以輕鬆地向外擴充已部署的應用程式使用 hello`scale`命令：</span><span class="sxs-lookup"><span data-stu-id="d6ffc-158">You can easily scale out already deployed applications using hello `scale` command:</span></span>

```bash
cf scale -i 2 hello-spring-cloud
```

<span data-ttu-id="d6ffc-159">執行 hello `cf app` hello 應用程式上的命令會顯示雲端 Foundry 建立 hello 應用程式的另一個執行個體。</span><span class="sxs-lookup"><span data-stu-id="d6ffc-159">Running hello `cf app` command on hello application shows that Cloud Foundry is creating another instance of hello application.</span></span> <span data-ttu-id="d6ffc-160">Hello 應用程式啟動之後，雲端 Foundry 會負載平衡流量 tooit 自動啟動。</span><span class="sxs-lookup"><span data-stu-id="d6ffc-160">Once hello application has started, Cloud Foundry automatically starts load balancing traffic tooit.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d6ffc-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d6ffc-161">Next steps</span></span>

- <span data-ttu-id="d6ffc-162">[讀取 hello 雲端 Foundry 文件][cloudfoundry-docs]</span><span class="sxs-lookup"><span data-stu-id="d6ffc-162">[Read hello Cloud Foundry documentation][cloudfoundry-docs]</span></span>
- <span data-ttu-id="d6ffc-163">[設定雲端 Foundry hello Visual Studio Team Services 外掛程式][vsts-plugin]</span><span class="sxs-lookup"><span data-stu-id="d6ffc-163">[Set up hello Visual Studio Team Services plugin for Cloud Foundry][vsts-plugin]</span></span>
- <span data-ttu-id="d6ffc-164">[設定雲端 Foundry hello Microsoft 記錄分析噴嘴][loganalytics-nozzle]</span><span class="sxs-lookup"><span data-stu-id="d6ffc-164">[Configure hello Microsoft Log Analytics Nozzle for Cloud Foundry][loganalytics-nozzle]</span></span>

<!-- LINKS -->

[pcf-azuremarketplace]: https://azuremarketplace.microsoft.com/marketplace/apps/pivotal.pivotal-cloud-foundry
[pcf-custom]: https://docs.pivotal.io/pivotalcf/1-10/customizing/azure.html
[oss-cf-bosh]: https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/tree/master/docs
[pcf-azuremarketplace-pivotaldocs]: https://docs.pivotal.io/pivotalcf/customizing/pcf_azure.html
[cf-cli]: https://github.com/cloudfoundry/cli
[cloudshell-docs]: https://docs.microsoft.com/azure/cloud-shell/overview
[cf-orgs-spaces-docs]: https://docs.cloudfoundry.org/concepts/roles.html
[spring-boot]: https://projects.spring.io/spring-boot/
[spring-framework]: http://spring.io
[cf-push-docs]: https://docs.cloudfoundry.org/concepts/how-applications-are-staged.html
[cloudfoundry-docs]: https://docs.cloudfoundry.org
[vsts-plugin]: https://github.com/Microsoft/vsts-cloudfoundry
[loganalytics-nozzle]: https://github.com/Azure/oms-log-analytics-firehose-nozzle

<!-- IMAGES -->
[cf-push-output]: ./media/cloudfoundry-deploy-your-first-app/cf-push-output.png
[hello-spring-cloud-basic]: ./media/cloudfoundry-deploy-your-first-app/hello-spring-cloud-basic.png