---
title: "將第一個應用程式部署到 Microsoft Azure 上的 Cloud Foundry | Microsoft Docs"
description: "將應用程式部署到 Azure 上的 Cloud Foundry"
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
ms.openlocfilehash: b617127fc0a3f8dcae293e356ea669edcfa5deff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-your-first-app-to-cloud-foundry-on-microsoft-azure"></a><span data-ttu-id="2dac2-103">將第一個應用程式部署到 Microsoft Azure 上的 Cloud Foundry</span><span class="sxs-lookup"><span data-stu-id="2dac2-103">Deploy your first app to Cloud Foundry on Microsoft Azure</span></span>

<span data-ttu-id="2dac2-104">[Cloud Foundry](http://cloudfoundry.org) 是 Microsoft Azure 上可用的熱門開放原始碼應用程式平台。</span><span class="sxs-lookup"><span data-stu-id="2dac2-104">[Cloud Foundry](http://cloudfoundry.org) is a popular open-source application platform available on Microsoft Azure.</span></span> <span data-ttu-id="2dac2-105">在本文中，我們會示範如何在 Azure 環境中部署和管理 Cloud Foundry 上的應用程式。</span><span class="sxs-lookup"><span data-stu-id="2dac2-105">In this article, we show how to deploy and manage an application on Cloud Foundry in an Azure environment.</span></span>

## <a name="create-a-cloud-foundry-environment"></a><span data-ttu-id="2dac2-106">建立 Cloud Foundry 環境</span><span class="sxs-lookup"><span data-stu-id="2dac2-106">Create a Cloud Foundry environment</span></span>

<span data-ttu-id="2dac2-107">有幾個選項可以用來在 Azure 上建立 Cloud Foundry 環境：</span><span class="sxs-lookup"><span data-stu-id="2dac2-107">There are several options for creating a Cloud Foundry environment on Azure:</span></span>

- <span data-ttu-id="2dac2-108">使用 Azure Marketplace 中的 [Pivotal Cloud Foundry 優惠][pcf-azuremarketplace]以建立標準環境，其中包含 PCF OPS Manager 和 Azure Service Broker。</span><span class="sxs-lookup"><span data-stu-id="2dac2-108">Use the [Pivotal Cloud Foundry offer][pcf-azuremarketplace] in the Azure Marketplace to create a standard environment that includes PCF Ops Manager and the Azure Service Broker.</span></span> <span data-ttu-id="2dac2-109">您可以在 Pivotal 文件中找到部署市集優惠的[完整指示][pcf-azuremarketplace-pivotaldocs]。</span><span class="sxs-lookup"><span data-stu-id="2dac2-109">You can find [complete instructions][pcf-azuremarketplace-pivotaldocs] for deploying the marketplace offer in the Pivotal documentation.</span></span>
- <span data-ttu-id="2dac2-110">建立自訂的環境，方法是[手動部署 Pivotal Cloud Foundry][pcf-custom]。</span><span class="sxs-lookup"><span data-stu-id="2dac2-110">Create a customized environment by [deploying Pivotal Cloud Foundry manually][pcf-custom].</span></span>
- <span data-ttu-id="2dac2-111">[直接部署開放原始碼 Cloud Foundry 套件][oss-cf-bosh]，方法是設定 [BOSH](http://bosh.io) 導向器，這是一個 VM，它會協調 Cloud Foundry 環境的部署。</span><span class="sxs-lookup"><span data-stu-id="2dac2-111">[Deploy the open-source Cloud Foundry packages directly][oss-cf-bosh] by setting up a [BOSH](http://bosh.io) director, a VM that coordinates the deployment of the Cloud Foundry environment.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="2dac2-112">如果您正在從 Azure Marketplace 部署 PCF，請記下存取 Pivotal Apps Manager 所需的 SYSTEMDOMAINURL 和管理員認證，這兩個項目都在市集部署指南中提及。</span><span class="sxs-lookup"><span data-stu-id="2dac2-112">If you are deploying PCF from the Azure Marketplace, make a note of the SYSTEMDOMAINURL and the admin credentials required to access the Pivotal Apps Manager, both of which are described in the marketplace deployment guide.</span></span> <span data-ttu-id="2dac2-113">需要這兩個項目才能完成本教學課程。</span><span class="sxs-lookup"><span data-stu-id="2dac2-113">They are needed to complete this tutorial.</span></span> <span data-ttu-id="2dac2-114">對於市集部署，SYSTEMDOMAINURL 在表單 https://system.*ip-address*.cf.pcfazure.com 中。</span><span class="sxs-lookup"><span data-stu-id="2dac2-114">For marketplace deployments, the SYSTEMDOMAINURL is in the form https://system.*ip-address*.cf.pcfazure.com.</span></span>

## <a name="connect-to-the-cloud-controller"></a><span data-ttu-id="2dac2-115">連線至 Cloud Controller</span><span class="sxs-lookup"><span data-stu-id="2dac2-115">Connect to the Cloud Controller</span></span>

<span data-ttu-id="2dac2-116">Cloud Controller 是到 Cloud Foundry 環境以部署和管理應用程式的主要進入點。</span><span class="sxs-lookup"><span data-stu-id="2dac2-116">The Cloud Controller is the primary entry point to a Cloud Foundry environment for deploying and managing applications.</span></span> <span data-ttu-id="2dac2-117">核心 Cloud Controller API (CCAPI) 是 REST API，但是可以透過各種工具存取。</span><span class="sxs-lookup"><span data-stu-id="2dac2-117">The core Cloud Controller API (CCAPI) is a REST API, but it is accessible through various tools.</span></span> <span data-ttu-id="2dac2-118">在此情況下，我們透過 [Cloud Foundry CLI][cf-cli] 與它互動。</span><span class="sxs-lookup"><span data-stu-id="2dac2-118">In this case, we interact with it through the [Cloud Foundry CLI][cf-cli].</span></span> <span data-ttu-id="2dac2-119">您可以在 Linux、MacOS 或 Windows 上安裝 CLI，但是如果您完全不想要安裝，它可以預先安裝在 [Azure Cloud Shell][cloudshell-docs]。</span><span class="sxs-lookup"><span data-stu-id="2dac2-119">You can install the CLI on Linux, MacOS, or Windows, but if you'd prefer not to install it at all, it is available pre-installed in the [Azure Cloud Shell][cloudshell-docs].</span></span>

<span data-ttu-id="2dac2-120">若要登入，請在您從市集部署取得的 SYSTEMDOMAINURL 前面加上 `api`。</span><span class="sxs-lookup"><span data-stu-id="2dac2-120">To log in, prepend `api` to the SYSTEMDOMAINURL that you obtained from the marketplace deployment.</span></span> <span data-ttu-id="2dac2-121">由於預設部署使用自我簽署憑證，您也應該包含 `skip-ssl-validation` 參數。</span><span class="sxs-lookup"><span data-stu-id="2dac2-121">Since the default deployment uses a self-signed certificate, you should also include the `skip-ssl-validation` switch.</span></span>

```bash
cf login -a https://api.SYSTEMDOMAINURL --skip-ssl-validation
```

<span data-ttu-id="2dac2-122">系統會提示您登入 Cloud Controller。</span><span class="sxs-lookup"><span data-stu-id="2dac2-122">You are prompted to log in to the Cloud Controller.</span></span> <span data-ttu-id="2dac2-123">使用您從市集部署步驟取得的管理員帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="2dac2-123">Use the admin account credentials that you acquired from the marketplace deployment steps.</span></span>

<span data-ttu-id="2dac2-124">Cloud Foundry 提供組織和空間 作為命名空間，以隔離共用部署內的小組和環境。</span><span class="sxs-lookup"><span data-stu-id="2dac2-124">Cloud Foundry provides *orgs* and *spaces* as namespaces to isolate the teams and environments within a shared deployment.</span></span> <span data-ttu-id="2dac2-125">PCF 市集部署包含預設系統組織和建立以包含基礎元件的一組空間，例如自動調整服務和 Azure Service Broker。</span><span class="sxs-lookup"><span data-stu-id="2dac2-125">The PCF marketplace deployment includes the default *system* org and a set of spaces created to contain the base components, like the autoscaling service and the Azure service broker.</span></span> <span data-ttu-id="2dac2-126">目前，選擇系統空間。</span><span class="sxs-lookup"><span data-stu-id="2dac2-126">For now, choose the *system* space.</span></span>


## <a name="create-an-org-and-space"></a><span data-ttu-id="2dac2-127">建立組織和空間</span><span class="sxs-lookup"><span data-stu-id="2dac2-127">Create an org and space</span></span>

<span data-ttu-id="2dac2-128">如果您輸入 `cf apps`，您會看到一組系統應用程式，已部署在系統組織內的系統空間。</span><span class="sxs-lookup"><span data-stu-id="2dac2-128">If you type `cf apps`, you see a set of system applications that have been deployed in the system space within the system org.</span></span> 

<span data-ttu-id="2dac2-129">您應該為系統應用程式保留系統組織，因此請建立組織和空間以容納我們的範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="2dac2-129">You should keep the *system* org reserved for system applications, so create an org and space to house our sample application.</span></span>

```bash
cf create-org myorg
cf create-space dev -o myorg
```

<span data-ttu-id="2dac2-130">使用目標命令以切換至新的組織和空間：</span><span class="sxs-lookup"><span data-stu-id="2dac2-130">Use the target command to switch to the new org and space:</span></span>

```bash
cf target -o testorg -s dev
```

<span data-ttu-id="2dac2-131">現在，當您部署應用程式時，會自動在新的組織和空間中建立。</span><span class="sxs-lookup"><span data-stu-id="2dac2-131">Now, when you deploy an application, it is automatically created in the new org and space.</span></span> <span data-ttu-id="2dac2-132">若要確認目前在新的組織/空間中沒有應用程式，請再次輸入 `cf apps`。</span><span class="sxs-lookup"><span data-stu-id="2dac2-132">To confirm that there are currently no apps in the new org/space, type `cf apps` again.</span></span>

> [!NOTE] 
> <span data-ttu-id="2dac2-133">如需組織和空間以及它們如何用於角色型存取控制 (RBAC) 的詳細資訊，請參閱[Cloud Foundry 文件][cf-orgs-spaces-docs]。</span><span class="sxs-lookup"><span data-stu-id="2dac2-133">For more information about orgs and spaces and how they can be used for role-based access control (RBAC), see the [Cloud Foundry documentation][cf-orgs-spaces-docs].</span></span>

## <a name="deploy-an-application"></a><span data-ttu-id="2dac2-134">部署應用程式</span><span class="sxs-lookup"><span data-stu-id="2dac2-134">Deploy an application</span></span>

<span data-ttu-id="2dac2-135">讓我們使用名為 Hello Spring Cloud 的範例 Cloud Foundry 應用程式，該應用程式是以 Java 撰寫，並且根據 [Spring Framework](http://spring.io) 和 [Spring Boot](http://projects.spring.io/spring-boot/)。</span><span class="sxs-lookup"><span data-stu-id="2dac2-135">Let's use a sample Cloud Foundry application called Hello Spring Cloud, which is written in Java and based on the [Spring Framework](http://spring.io) and [Spring Boot](http://projects.spring.io/spring-boot/).</span></span>

### <a name="clone-the-hello-spring-cloud-repository"></a><span data-ttu-id="2dac2-136">複製 Hello Spring Cloud 存放庫</span><span class="sxs-lookup"><span data-stu-id="2dac2-136">Clone the Hello Spring Cloud repository</span></span>

<span data-ttu-id="2dac2-137">Hello Spring Cloud 範例應用程式可以在 GitHub 上取得。</span><span class="sxs-lookup"><span data-stu-id="2dac2-137">The Hello Spring Cloud sample application is available on GitHub.</span></span> <span data-ttu-id="2dac2-138">將它複製到您的環境，並且變更到新的目錄：</span><span class="sxs-lookup"><span data-stu-id="2dac2-138">Clone it to your environment and change into the new directory:</span></span>

```bash
git clone https://github.com/cloudfoundry-samples/hello-spring-cloud
cd hello-spring-cloud
```

### <a name="build-the-application"></a><span data-ttu-id="2dac2-139">建置應用程式</span><span class="sxs-lookup"><span data-stu-id="2dac2-139">Build the application</span></span>

<span data-ttu-id="2dac2-140">使用 [Apache Maven](http://maven.apache.org) 建置應用程式。</span><span class="sxs-lookup"><span data-stu-id="2dac2-140">Build the app using [Apache Maven](http://maven.apache.org).</span></span>

```bash
mvn clean package
```

### <a name="deploy-the-application-with-cf-push"></a><span data-ttu-id="2dac2-141">使用 cf push 部署應用程式</span><span class="sxs-lookup"><span data-stu-id="2dac2-141">Deploy the application with cf push</span></span>

<span data-ttu-id="2dac2-142">您可以使用 `push` 命令，將大部分的應用程式部署到 Cloud Foundry：</span><span class="sxs-lookup"><span data-stu-id="2dac2-142">You can deploy most applications to Cloud Foundry using the `push` command:</span></span>

```bash
cf push
```

<span data-ttu-id="2dac2-143">當您發送應用程式時，Cloud Foundry 會偵測應用程式類型 (在此案例中為 Java 應用程式)，並且識別其相依性 (在此案例中為 Spring Framework)。</span><span class="sxs-lookup"><span data-stu-id="2dac2-143">When you *push* an application, Cloud Foundry detects the type of application (in this case, a Java app) and identifies its dependencies (in this case, the Spring framework).</span></span> <span data-ttu-id="2dac2-144">然後它會將執行程式碼所需的所有項目封裝至獨立容器映像，稱為 droplet。</span><span class="sxs-lookup"><span data-stu-id="2dac2-144">It then packages everything required to run your code into a standalone container image, known as a *droplet*.</span></span> <span data-ttu-id="2dac2-145">最後，Cloud Foundry 會在環境中其中一部可用的機器上排程應用程式，並且建立您可以在該位置取得它的 URL，該 URL 可以在命令的輸出中取得。</span><span class="sxs-lookup"><span data-stu-id="2dac2-145">Finally, Cloud Foundry schedules the application on one of the available machines in your environment and creates a URL where you can reach it, which is available in the output of the command.</span></span>

![cf push 命令的輸出][cf-push-output]

<span data-ttu-id="2dac2-147">若要查看 hello-spring-cloud 應用程式，請在瀏覽器中開啟提供的 URL：</span><span class="sxs-lookup"><span data-stu-id="2dac2-147">To see the hello-spring-cloud application, open the provided URL in your browser:</span></span>

![Hello Spring Cloud 的預設 UI][hello-spring-cloud-basic]

> [!NOTE] 
> <span data-ttu-id="2dac2-149">若要深入了解 `cf push` 期間會發生什麼狀況，請參閱 Cloud Foundry 文件中的[應用程式如何暫存][cf-push-docs]。</span><span class="sxs-lookup"><span data-stu-id="2dac2-149">To learn more about what happens during `cf push`, see [How Applications Are Staged][cf-push-docs] in the Cloud Foundry documentation.</span></span>

## <a name="view-application-logs"></a><span data-ttu-id="2dac2-150">檢視應用程式記錄</span><span class="sxs-lookup"><span data-stu-id="2dac2-150">View application logs</span></span>

<span data-ttu-id="2dac2-151">您可以使用 Cloud Foundry CLI 以根據應用程式的名稱檢視其記錄：</span><span class="sxs-lookup"><span data-stu-id="2dac2-151">You can use the Cloud Foundry CLI to view logs for an application by its name:</span></span>

```bash
cf logs hello-spring-cloud
```

<span data-ttu-id="2dac2-152">根據預設，記錄命令會使用 tail，在寫入之後顯示新的記錄。</span><span class="sxs-lookup"><span data-stu-id="2dac2-152">By default, the logs command uses *tail*, which shows new logs as they are written.</span></span> <span data-ttu-id="2dac2-153">若要查看出現的新記錄，請在瀏覽器中重新整理 hello-spring-cloud 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2dac2-153">To see new logs appear, refresh the hello-spring-cloud app in the browser.</span></span>

<span data-ttu-id="2dac2-154">若要檢視已寫入的記錄，請新增 `recent` 參數：</span><span class="sxs-lookup"><span data-stu-id="2dac2-154">To view logs that have already been written, add the `recent` switch:</span></span>

```bash
cf logs --recent hello-spring-cloud
```

## <a name="scale-the-application"></a><span data-ttu-id="2dac2-155">調整應用程式</span><span class="sxs-lookup"><span data-stu-id="2dac2-155">Scale the application</span></span>

<span data-ttu-id="2dac2-156">根據預設，`cf push` 只會建立應用程式的單一執行個體。</span><span class="sxs-lookup"><span data-stu-id="2dac2-156">By default, `cf push` only creates a single instance of your application.</span></span> <span data-ttu-id="2dac2-157">若要確保高可用性，並且啟用相應放大以獲得較高的輸送量，您通常要執行應用程式的多個執行個體。</span><span class="sxs-lookup"><span data-stu-id="2dac2-157">To ensure high availability and enable scale out for higher throughput, you generally want to run more than one instance of your applications.</span></span> <span data-ttu-id="2dac2-158">您可以使用 `scale` 命令，輕鬆地相應放大已部署的應用程式：</span><span class="sxs-lookup"><span data-stu-id="2dac2-158">You can easily scale out already deployed applications using the `scale` command:</span></span>

```bash
cf scale -i 2 hello-spring-cloud
```

<span data-ttu-id="2dac2-159">在應用程式上執行 `cf app` 命令，會顯示 Cloud Foundry 正在建立應用程式的另一個執行個體。</span><span class="sxs-lookup"><span data-stu-id="2dac2-159">Running the `cf app` command on the application shows that Cloud Foundry is creating another instance of the application.</span></span> <span data-ttu-id="2dac2-160">應用程式啟動之後，Cloud Foundry 會自動對它啟動負載平衡流量。</span><span class="sxs-lookup"><span data-stu-id="2dac2-160">Once the application has started, Cloud Foundry automatically starts load balancing traffic to it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="2dac2-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2dac2-161">Next steps</span></span>

- <span data-ttu-id="2dac2-162">[閱讀 Cloud Foundry 文件][cloudfoundry-docs]</span><span class="sxs-lookup"><span data-stu-id="2dac2-162">[Read the Cloud Foundry documentation][cloudfoundry-docs]</span></span>
- <span data-ttu-id="2dac2-163">[設定適用於 Cloud Foundry 的 Visual Studio Team Services 外掛程式][vsts-plugin]</span><span class="sxs-lookup"><span data-stu-id="2dac2-163">[Set up the Visual Studio Team Services plugin for Cloud Foundry][vsts-plugin]</span></span>
- <span data-ttu-id="2dac2-164">[設定適用於 Cloud Foundry 的 Microsoft Log Analytics Nozzle][loganalytics-nozzle]</span><span class="sxs-lookup"><span data-stu-id="2dac2-164">[Configure the Microsoft Log Analytics Nozzle for Cloud Foundry][loganalytics-nozzle]</span></span>

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