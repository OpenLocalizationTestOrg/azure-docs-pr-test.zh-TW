---
title: "監視 Azure DC/OS 叢集 - Operations Management | Microsoft Docs"
description: "使用 Microsoft Operations Management Suite 監視 Azure Container Service DC/OS 叢集。"
services: container-service
documentationcenter: 
author: keikhara
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 11/17/2016
ms.author: keikhara
ms.custom: mvc
ms.openlocfilehash: 9b8f96b34b53982c469273a3df9751ceb7930d60
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-operations-management-suite"></a><span data-ttu-id="15d27-103">使用 Operations Management Suite 監視 Azure Container Service DC/OS 叢集</span><span class="sxs-lookup"><span data-stu-id="15d27-103">Monitor an Azure Container Service DC/OS cluster with Operations Management Suite</span></span>

<span data-ttu-id="15d27-104">Microsoft Operations Management Suite (OMS) 是 Microsoft 的雲端型 IT 管理解決方案，可協助您管理並保護內部部署和雲端基礎結構。</span><span class="sxs-lookup"><span data-stu-id="15d27-104">Microsoft Operations Management Suite (OMS) is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="15d27-105">容器解決方案是 OMS Log Analytics 中的解決方案，可協助您在單一位置檢視容器詳細目錄、效能和記錄檔。</span><span class="sxs-lookup"><span data-stu-id="15d27-105">Container Solution is a solution in OMS Log Analytics, which helps you view the container inventory, performance, and logs in a single location.</span></span> <span data-ttu-id="15d27-106">您可以在集中式位置檢視記錄檔以稽核、對容器進行疑難排解，並尋找壟斷及佔用過量主機資源的容器。</span><span class="sxs-lookup"><span data-stu-id="15d27-106">You can audit, troubleshoot containers by viewing the logs in centralized location, and find noisy consuming excess container on a host.</span></span>

![](media/container-service-monitoring-oms/image1.png)

<span data-ttu-id="15d27-107">如需容器解決方案的詳細資訊，請參閱[容器解決方案 Log Analytics](../../log-analytics/log-analytics-containers.md)。</span><span class="sxs-lookup"><span data-stu-id="15d27-107">For more information about Container Solution, please refer to the [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

## <a name="setting-up-oms-from-the-dcos-universe"></a><span data-ttu-id="15d27-108">從 DC/OS Universe 設定 OMS</span><span class="sxs-lookup"><span data-stu-id="15d27-108">Setting up OMS from the DC/OS universe</span></span>


<span data-ttu-id="15d27-109">本文假設您已在叢集上設定 DC/OS，並已部署簡單的 Web 容器應用程式。</span><span class="sxs-lookup"><span data-stu-id="15d27-109">This article assumes that you have set up an DC/OS and have deployed simple web container applications on the cluster.</span></span>

### <a name="pre-requisite"></a><span data-ttu-id="15d27-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="15d27-110">Pre-requisite</span></span>
- <span data-ttu-id="15d27-111">[Microsoft Azure 訂用帳戶](https://azure.microsoft.com/free/) - 您可以免費取得帳戶。</span><span class="sxs-lookup"><span data-stu-id="15d27-111">[Microsoft Azure Subscription](https://azure.microsoft.com/free/) - You can get this for free.</span></span>  
- <span data-ttu-id="15d27-112">Microsoft OMS 工作區設定 - 請參閱下方的「步驟 3」</span><span class="sxs-lookup"><span data-stu-id="15d27-112">Microsoft OMS Workspace Setup - see "Step 3" below</span></span>
- <span data-ttu-id="15d27-113">已安裝 [DC/OS CLI](https://dcos.io/docs/1.8/usage/cli/install/)。</span><span class="sxs-lookup"><span data-stu-id="15d27-113">[DC/OS CLI](https://dcos.io/docs/1.8/usage/cli/install/) installed.</span></span>

1. <span data-ttu-id="15d27-114">在 DC/OS 儀表板中，按一下 [Universe] 並搜尋 'OMS'，如下所示。</span><span class="sxs-lookup"><span data-stu-id="15d27-114">In the DC/OS dashboard, click on Universe and search for ‘OMS’ as shown below.</span></span>

![](media/container-service-monitoring-oms/image2.png)

2. <span data-ttu-id="15d27-115">按一下 [Install] 。</span><span class="sxs-lookup"><span data-stu-id="15d27-115">Click **Install**.</span></span> <span data-ttu-id="15d27-116">您會看到含有 OMS 版本資訊和一個 [Install Package]\(安裝套件) 或 [Advanced Installation]\(進階安裝) 按鈕的快顯。</span><span class="sxs-lookup"><span data-stu-id="15d27-116">You will see a pop up with the OMS version information and an **Install Package** or **Advanced Installation** button.</span></span> <span data-ttu-id="15d27-117">按一下 [Advanced Installation]\(進階安裝)，就會跳轉至 [OMS specific configuration properties]\(OMS 特定組態屬性) 頁面。</span><span class="sxs-lookup"><span data-stu-id="15d27-117">When you click **Advanced Installation**, which leads you to the **OMS specific configuration properties** page.</span></span>

![](media/container-service-monitoring-oms/image3.png)

![](media/container-service-monitoring-oms/image4.png)

3. <span data-ttu-id="15d27-118">這裡將要求您輸入 `wsid` (OMS 工作區識別碼) 和 `wskey` (工作區識別碼的 OMS 主索引鍵)。</span><span class="sxs-lookup"><span data-stu-id="15d27-118">Here, you will be asked to enter the `wsid` (the OMS workspace ID) and `wskey` (the OMS primary key for the workspace id).</span></span> <span data-ttu-id="15d27-119">若要取得 `wsid` 和 `wskey`，您必須建立在 <https://mms.microsoft.com> 建立一個 OMS 帳戶。請依步驟指示建立帳戶。</span><span class="sxs-lookup"><span data-stu-id="15d27-119">To get both `wsid` and `wskey` you need to create an OMS account at <https://mms.microsoft.com>. Please follow the steps to create an account.</span></span> <span data-ttu-id="15d27-120">建立帳戶之後，您必須依序按一下 [Settings]\(設定)、[Connected Sources]\(連接的來源)、[Linux Servers]\(Linux 伺服器)，以取得您的 `wsid` 和 `wskey`，如下所示。</span><span class="sxs-lookup"><span data-stu-id="15d27-120">Once you are done creating the account, you need to obtain your `wsid` and `wskey` by clicking **Settings**, then **Connected Sources**, and then **Linux Servers**, as shown below.</span></span>

 ![](media/container-service-monitoring-oms/image5.png)

4. <span data-ttu-id="15d27-121">選取您想要的 OMS 執行個體數目，然後按一下 [Review and Install]\(檢閱並安裝) 按鈕。</span><span class="sxs-lookup"><span data-stu-id="15d27-121">Select the number you OMS instances that you want and click the ‘Review and Install’ button.</span></span> <span data-ttu-id="15d27-122">一般而言，OMS 執行個體數目應等於您代理程式叢集中的 VM 數目。</span><span class="sxs-lookup"><span data-stu-id="15d27-122">Typically, you will want to have the number of OMS instances equal to the number of VM’s you have in your agent cluster.</span></span> <span data-ttu-id="15d27-123">適用於 Linux 的 OMS 代理程式會在其想要收集資訊的個別 VM 上安裝為獨立容器，以監視和記錄資訊。</span><span class="sxs-lookup"><span data-stu-id="15d27-123">OMS Agent for Linux is installs as individual containers on each VM that it wants to collect information for monitoring and logging information.</span></span>

## <a name="setting-up-a-simple-oms-dashboard"></a><span data-ttu-id="15d27-124">設定簡單的 OMS 儀表板</span><span class="sxs-lookup"><span data-stu-id="15d27-124">Setting up a simple OMS dashboard</span></span>

<span data-ttu-id="15d27-125">在 VM 上安裝適用於 Linux 的 OMS 代理程式後，下一步是設定 OMS 儀表板。</span><span class="sxs-lookup"><span data-stu-id="15d27-125">Once you have installed the OMS Agent for Linux on the VMs, next step is to set up the OMS dashboard.</span></span> <span data-ttu-id="15d27-126">有兩種設定方式︰OMS 入口網站或 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="15d27-126">There are two ways to do this: OMS Portal or Azure Portal.</span></span>

### <a name="oms-portal"></a><span data-ttu-id="15d27-127">OMS 入口網站</span><span class="sxs-lookup"><span data-stu-id="15d27-127">OMS Portal</span></span> 

<span data-ttu-id="15d27-128">登入 OMS 入口網站 (<https://mms.microsoft.com>)，並移至 [Solution Gallery]\(方案庫)。</span><span class="sxs-lookup"><span data-stu-id="15d27-128">Log in to the OMS portal (<https://mms.microsoft.com>) and go to the **Solution Gallery**.</span></span>

![](media/container-service-monitoring-oms/image6.png)

<span data-ttu-id="15d27-129">在 [Solution Gallery]\(方案庫) 中，選取 [Containers]\(容器)。</span><span class="sxs-lookup"><span data-stu-id="15d27-129">Once you are in the **Solution Gallery**, select **Containers**.</span></span>

![](media/container-service-monitoring-oms/image7.png)

<span data-ttu-id="15d27-130">選取容器解決方案後，您會在 [OMS 概觀儀表板] 頁面上看見圖格。</span><span class="sxs-lookup"><span data-stu-id="15d27-130">Once you’ve selected the Container Solution, you will see the tile on the OMS Overview Dashboard page.</span></span> <span data-ttu-id="15d27-131">擷取的容器資料建立索引後，您會在解決方案檢視圖格上看到已填入資訊的圖格。</span><span class="sxs-lookup"><span data-stu-id="15d27-131">Once the ingested container data is indexed, you will see the tile populated with information on the solution view tiles.</span></span>

![](media/container-service-monitoring-oms/image8.png)

### <a name="azure-portal"></a><span data-ttu-id="15d27-132">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="15d27-132">Azure Portal</span></span> 

<span data-ttu-id="15d27-133">登入 Azure 入口網站，位址是 <https://portal.microsoft.com/>。</span><span class="sxs-lookup"><span data-stu-id="15d27-133">Login to Azure portal at <https://portal.microsoft.com/>.</span></span> <span data-ttu-id="15d27-134">移至 [Marketplace]，選取 [監視 + 管理]，然後按一下 [查看全部]。</span><span class="sxs-lookup"><span data-stu-id="15d27-134">Go to **Marketplace**, select **Monitoring + management** and click **See All**.</span></span> <span data-ttu-id="15d27-135">接著在搜尋中輸入 `containers` (容器)。</span><span class="sxs-lookup"><span data-stu-id="15d27-135">Then Type `containers` in search.</span></span> <span data-ttu-id="15d27-136">您會在搜尋結果中看到 "containers" (容器)。</span><span class="sxs-lookup"><span data-stu-id="15d27-136">You will see "containers" in the search results.</span></span> <span data-ttu-id="15d27-137">選取 [Containers]\(容器)，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="15d27-137">Select **Containers** and click **Create**.</span></span>

![](media/container-service-monitoring-oms/image9.png)

<span data-ttu-id="15d27-138">按一下 [建立] 後，它會要求您提供您的工作區。</span><span class="sxs-lookup"><span data-stu-id="15d27-138">Once you click **Create**, it will ask you for your workspace.</span></span> <span data-ttu-id="15d27-139">選取您的工作區，或是如果您沒有工作區，請建立新的工作區。</span><span class="sxs-lookup"><span data-stu-id="15d27-139">Select your workspace or if you do not have one, create a new workspace.</span></span>

![](media/container-service-monitoring-oms/image10.PNG)

<span data-ttu-id="15d27-140">選取您的工作區後，按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="15d27-140">Once you’ve selected your workspace, click **Create**.</span></span>

![](media/container-service-monitoring-oms/image11.png)

<span data-ttu-id="15d27-141">如需 OMS 容器解決方案的詳細資訊，請參閱[容器解決方案 Log Analytics](../../log-analytics/log-analytics-containers.md)。</span><span class="sxs-lookup"><span data-stu-id="15d27-141">For more information about the OMS Container Solution, please refer to the [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

### <a name="how-to-scale-oms-agent-with-acs-dcos"></a><span data-ttu-id="15d27-142">如何以 ACS DC/OS 擴充 OMS 代理程式</span><span class="sxs-lookup"><span data-stu-id="15d27-142">How to scale OMS Agent with ACS DC/OS</span></span> 

<span data-ttu-id="15d27-143">如果您需要的已安裝 OMS 代理程式少於實際的節點數，或是您正透過新增更多 VM 來擴充 VMSS，您可以透過擴充 `msoms` 服務來達成。</span><span class="sxs-lookup"><span data-stu-id="15d27-143">In case you need to have installed OMS agent short of the actual node count or you are scaling up VMSS by adding more VM, you can do so by scaling the `msoms` service.</span></span>

<span data-ttu-id="15d27-144">您可以移至 [Marathon] 或 [DC/OS UI Services]\(DC/OS UI 服務) 索引標籤來擴充節點數。</span><span class="sxs-lookup"><span data-stu-id="15d27-144">You can either go to Marathon or the DC/OS UI Services tab and scale up your node count.</span></span>

![](media/container-service-monitoring-oms/image12.PNG)

<span data-ttu-id="15d27-145">這樣會部署到尚未部署 OMS 代理程式的其他節點。</span><span class="sxs-lookup"><span data-stu-id="15d27-145">This will deploy to other nodes which have not yet deployed the OMS agent.</span></span>

## <a name="uninstall-ms-oms"></a><span data-ttu-id="15d27-146">解除安裝 MS OMS</span><span class="sxs-lookup"><span data-stu-id="15d27-146">Uninstall MS OMS</span></span>

<span data-ttu-id="15d27-147">若要解除安裝 MS OMS，請輸入以下命令：</span><span class="sxs-lookup"><span data-stu-id="15d27-147">To uninstall MS OMS enter the following command:</span></span>

```bash
$ dcos package uninstall msoms
```

## <a name="let-us-know"></a><span data-ttu-id="15d27-148">請告訴我們！</span><span class="sxs-lookup"><span data-stu-id="15d27-148">Let us know!!!</span></span>
<span data-ttu-id="15d27-149">哪些資訊是有用的？</span><span class="sxs-lookup"><span data-stu-id="15d27-149">What works?</span></span> <span data-ttu-id="15d27-150">缺少哪些資訊？</span><span class="sxs-lookup"><span data-stu-id="15d27-150">What is missing?</span></span> <span data-ttu-id="15d27-151">我們還能提供您什麼樣的實用資訊？</span><span class="sxs-lookup"><span data-stu-id="15d27-151">What else do you need for this to be useful for you?</span></span> <span data-ttu-id="15d27-152">請透過 <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a> 告訴我們。</span><span class="sxs-lookup"><span data-stu-id="15d27-152">Let us know at <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15d27-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="15d27-153">Next steps</span></span>

 <span data-ttu-id="15d27-154">由於您已設定 OMS 來監視您的容器，[請檢視您的容器儀表板](../../log-analytics/log-analytics-containers.md)。</span><span class="sxs-lookup"><span data-stu-id="15d27-154">Now that you have set up OMS to monitor your containers,[see your container dashboard](../../log-analytics/log-analytics-containers.md).</span></span>
