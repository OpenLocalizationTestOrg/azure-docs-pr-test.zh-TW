---
title: "aaaMonitor Azure DC/OS 叢集 Operations Management |Microsoft 文件"
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
ms.openlocfilehash: 0ebfa3ba3cef8f0205b15731b0e91f5b304bc8fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-operations-management-suite"></a><span data-ttu-id="f9358-103">使用 Operations Management Suite 監視 Azure Container Service DC/OS 叢集</span><span class="sxs-lookup"><span data-stu-id="f9358-103">Monitor an Azure Container Service DC/OS cluster with Operations Management Suite</span></span>

<span data-ttu-id="f9358-104">Microsoft Operations Management Suite (OMS) 是 Microsoft 的雲端型 IT 管理解決方案，可協助您管理並保護內部部署和雲端基礎結構。</span><span class="sxs-lookup"><span data-stu-id="f9358-104">Microsoft Operations Management Suite (OMS) is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="f9358-105">容器的解決方案是 OMS 記錄分析可協助您檢視 hello 容器清查、 效能和記錄檔中的單一位置中的解決方案。</span><span class="sxs-lookup"><span data-stu-id="f9358-105">Container Solution is a solution in OMS Log Analytics, which helps you view hello container inventory, performance, and logs in a single location.</span></span> <span data-ttu-id="f9358-106">您可以稽核、 疑難排解容器檢視 hello 記錄在集中式位置，並尋找雜訊耗用過多的容器主機上。</span><span class="sxs-lookup"><span data-stu-id="f9358-106">You can audit, troubleshoot containers by viewing hello logs in centralized location, and find noisy consuming excess container on a host.</span></span>

![](media/container-service-monitoring-oms/image1.png)

<span data-ttu-id="f9358-107">如需容器解決方案的詳細資訊，請參閱 toothe[容器方案記錄分析](../../log-analytics/log-analytics-containers.md)。</span><span class="sxs-lookup"><span data-stu-id="f9358-107">For more information about Container Solution, please refer toothe [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

## <a name="setting-up-oms-from-hello-dcos-universe"></a><span data-ttu-id="f9358-108">從 hello DC/OS universe 設定 OMS</span><span class="sxs-lookup"><span data-stu-id="f9358-108">Setting up OMS from hello DC/OS universe</span></span>


<span data-ttu-id="f9358-109">本文假設您已設定 DC/OS 和已部署的 hello 叢集上的簡單的 web 容器應用程式。</span><span class="sxs-lookup"><span data-stu-id="f9358-109">This article assumes that you have set up an DC/OS and have deployed simple web container applications on hello cluster.</span></span>

### <a name="pre-requisite"></a><span data-ttu-id="f9358-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="f9358-110">Pre-requisite</span></span>
- <span data-ttu-id="f9358-111">[Microsoft Azure 訂用帳戶](https://azure.microsoft.com/free/) - 您可以免費取得帳戶。</span><span class="sxs-lookup"><span data-stu-id="f9358-111">[Microsoft Azure Subscription](https://azure.microsoft.com/free/) - You can get this for free.</span></span>  
- <span data-ttu-id="f9358-112">Microsoft OMS 工作區設定 - 請參閱下方的「步驟 3」</span><span class="sxs-lookup"><span data-stu-id="f9358-112">Microsoft OMS Workspace Setup - see "Step 3" below</span></span>
- <span data-ttu-id="f9358-113">已安裝 [DC/OS CLI](https://dcos.io/docs/1.8/usage/cli/install/)。</span><span class="sxs-lookup"><span data-stu-id="f9358-113">[DC/OS CLI](https://dcos.io/docs/1.8/usage/cli/install/) installed.</span></span>

1. <span data-ttu-id="f9358-114">Hello DC/OS 儀表板中按一下 Universe，搜尋 'OMS' 如下所示。</span><span class="sxs-lookup"><span data-stu-id="f9358-114">In hello DC/OS dashboard, click on Universe and search for ‘OMS’ as shown below.</span></span>

![](media/container-service-monitoring-oms/image2.png)

2. <span data-ttu-id="f9358-115">按一下 [Install] 。</span><span class="sxs-lookup"><span data-stu-id="f9358-115">Click **Install**.</span></span> <span data-ttu-id="f9358-116">您會看到快顯向上 hello OMS 版本資訊和**安裝套件**或**進階安裝** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f9358-116">You will see a pop up with hello OMS version information and an **Install Package** or **Advanced Installation** button.</span></span> <span data-ttu-id="f9358-117">當您按一下**進階安裝**，這會導致 toohello **OMS 特定組態屬性**頁面。</span><span class="sxs-lookup"><span data-stu-id="f9358-117">When you click **Advanced Installation**, which leads you toohello **OMS specific configuration properties** page.</span></span>

![](media/container-service-monitoring-oms/image3.png)

![](media/container-service-monitoring-oms/image4.png)

3. <span data-ttu-id="f9358-118">在這裡，將會要求您 tooenter hello `wsid` (hello OMS 工作區識別碼) 和`wskey`（hello OMS 主索引鍵的 hello 工作區識別碼）。</span><span class="sxs-lookup"><span data-stu-id="f9358-118">Here, you will be asked tooenter hello `wsid` (hello OMS workspace ID) and `wskey` (hello OMS primary key for hello workspace id).</span></span> <span data-ttu-id="f9358-119">這兩個 tooget`wsid`和`wskey`OMS 帳戶在需要 toocreate <https://mms.microsoft.com>。請遵循 hello 步驟 toocreate 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f9358-119">tooget both `wsid` and `wskey` you need toocreate an OMS account at <https://mms.microsoft.com>. Please follow hello steps toocreate an account.</span></span> <span data-ttu-id="f9358-120">一旦您完成建立 hello 帳戶之後，您需要 tooobtain 您`wsid`和`wskey`按一下**設定**，然後**連線來源**，然後**Linux 伺服器**，如下所示。</span><span class="sxs-lookup"><span data-stu-id="f9358-120">Once you are done creating hello account, you need tooobtain your `wsid` and `wskey` by clicking **Settings**, then **Connected Sources**, and then **Linux Servers**, as shown below.</span></span>

 ![](media/container-service-monitoring-oms/image5.png)

4. <span data-ttu-id="f9358-121">選取 hello 數字您 OMS 執行個體，然後按一下 hello 「 檢閱和安裝 」 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f9358-121">Select hello number you OMS instances that you want and click hello ‘Review and Install’ button.</span></span> <span data-ttu-id="f9358-122">一般而言，您會想 toohave hello 數目 OMS 執行個體相等 toohello VM 的您在您代理程式的叢集數目。</span><span class="sxs-lookup"><span data-stu-id="f9358-122">Typically, you will want toohave hello number of OMS instances equal toohello number of VM’s you have in your agent cluster.</span></span> <span data-ttu-id="f9358-123">適用於 Linux 的 OMS 代理程式是安裝做為其想 toocollect 資訊來監視和記錄資訊的每個 VM 上的個別容器。</span><span class="sxs-lookup"><span data-stu-id="f9358-123">OMS Agent for Linux is installs as individual containers on each VM that it wants toocollect information for monitoring and logging information.</span></span>

## <a name="setting-up-a-simple-oms-dashboard"></a><span data-ttu-id="f9358-124">設定簡單的 OMS 儀表板</span><span class="sxs-lookup"><span data-stu-id="f9358-124">Setting up a simple OMS dashboard</span></span>

<span data-ttu-id="f9358-125">一旦您已經安裝 hello OMS Agent for Linux hello Vm 上下, 一個步驟是 tooset hello OMS 儀表板上。</span><span class="sxs-lookup"><span data-stu-id="f9358-125">Once you have installed hello OMS Agent for Linux on hello VMs, next step is tooset up hello OMS dashboard.</span></span> <span data-ttu-id="f9358-126">有兩種方式 toodo 這： OMS 入口網站或 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="f9358-126">There are two ways toodo this: OMS Portal or Azure Portal.</span></span>

### <a name="oms-portal"></a><span data-ttu-id="f9358-127">OMS 入口網站</span><span class="sxs-lookup"><span data-stu-id="f9358-127">OMS Portal</span></span> 

<span data-ttu-id="f9358-128">登入 toohello OMS 入口網站 (<https://mms.microsoft.com>)，並移 toohello**解決方案資源庫**。</span><span class="sxs-lookup"><span data-stu-id="f9358-128">Log in toohello OMS portal (<https://mms.microsoft.com>) and go toohello **Solution Gallery**.</span></span>

![](media/container-service-monitoring-oms/image6.png)

<span data-ttu-id="f9358-129">當您在 hello**解決方案資源庫**，選取**容器**。</span><span class="sxs-lookup"><span data-stu-id="f9358-129">Once you are in hello **Solution Gallery**, select **Containers**.</span></span>

![](media/container-service-monitoring-oms/image7.png)

<span data-ttu-id="f9358-130">一旦您已選取 hello 容器解決方案，您會看到 hello hello OMS 概觀儀表板頁面上的磚。</span><span class="sxs-lookup"><span data-stu-id="f9358-130">Once you’ve selected hello Container Solution, you will see hello tile on hello OMS Overview Dashboard page.</span></span> <span data-ttu-id="f9358-131">一旦 hello 內嵌的容器資料具有索引，您會看到 hello 磚填入解決方案檢視磚上的資訊。</span><span class="sxs-lookup"><span data-stu-id="f9358-131">Once hello ingested container data is indexed, you will see hello tile populated with information on the solution view tiles.</span></span>

![](media/container-service-monitoring-oms/image8.png)

### <a name="azure-portal"></a><span data-ttu-id="f9358-132">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="f9358-132">Azure Portal</span></span> 

<span data-ttu-id="f9358-133">登入 tooAzure 入口網站則位於<https://portal.microsoft.com/>。</span><span class="sxs-lookup"><span data-stu-id="f9358-133">Login tooAzure portal at <https://portal.microsoft.com/>.</span></span> <span data-ttu-id="f9358-134">移至 [Marketplace]，選取 [監視 + 管理]，然後按一下 [查看全部]。</span><span class="sxs-lookup"><span data-stu-id="f9358-134">Go to **Marketplace**, select **Monitoring + management** and click **See All**.</span></span> <span data-ttu-id="f9358-135">接著在搜尋中輸入 `containers` (容器)。</span><span class="sxs-lookup"><span data-stu-id="f9358-135">Then Type `containers` in search.</span></span> <span data-ttu-id="f9358-136">您會看到 [容器] hello 搜尋結果中。</span><span class="sxs-lookup"><span data-stu-id="f9358-136">You will see "containers" in hello search results.</span></span> <span data-ttu-id="f9358-137">選取 [Containers]\(容器)，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="f9358-137">Select **Containers** and click **Create**.</span></span>

![](media/container-service-monitoring-oms/image9.png)

<span data-ttu-id="f9358-138">按一下 [建立] 後，它會要求您提供您的工作區。</span><span class="sxs-lookup"><span data-stu-id="f9358-138">Once you click **Create**, it will ask you for your workspace.</span></span> <span data-ttu-id="f9358-139">選取您的工作區，或是如果您沒有工作區，請建立新的工作區。</span><span class="sxs-lookup"><span data-stu-id="f9358-139">Select your workspace or if you do not have one, create a new workspace.</span></span>

![](media/container-service-monitoring-oms/image10.PNG)

<span data-ttu-id="f9358-140">選取您的工作區後，按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="f9358-140">Once you’ve selected your workspace, click **Create**.</span></span>

![](media/container-service-monitoring-oms/image11.png)

<span data-ttu-id="f9358-141">如需有關 hello 容器項 OMS 解決方案的詳細資訊，請參閱 toothe[容器方案記錄分析](../../log-analytics/log-analytics-containers.md)。</span><span class="sxs-lookup"><span data-stu-id="f9358-141">For more information about hello OMS Container Solution, please refer toothe [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

### <a name="how-tooscale-oms-agent-with-acs-dcos"></a><span data-ttu-id="f9358-142">如何 tooscale OMS 代理程式與 ACS DC/OS 中</span><span class="sxs-lookup"><span data-stu-id="f9358-142">How tooscale OMS Agent with ACS DC/OS</span></span> 

<span data-ttu-id="f9358-143">如果您需要 toohave 安裝 OMS 代理程式，除非 hello 實際節點計數，或您會藉由新增更多 VM VMSS 向上擴充，您可以藉由調整 hello`msoms`服務。</span><span class="sxs-lookup"><span data-stu-id="f9358-143">In case you need toohave installed OMS agent short of hello actual node count or you are scaling up VMSS by adding more VM, you can do so by scaling hello `msoms` service.</span></span>

<span data-ttu-id="f9358-144">您可以移 tooMarathon 或 hello DC/OS UI 服務 索引標籤，並向上擴充節點計數。</span><span class="sxs-lookup"><span data-stu-id="f9358-144">You can either go tooMarathon or hello DC/OS UI Services tab and scale up your node count.</span></span>

![](media/container-service-monitoring-oms/image12.PNG)

<span data-ttu-id="f9358-145">這會將部署 tooother 節點尚未部署 hello OMS 代理程式。</span><span class="sxs-lookup"><span data-stu-id="f9358-145">This will deploy tooother nodes which have not yet deployed hello OMS agent.</span></span>

## <a name="uninstall-ms-oms"></a><span data-ttu-id="f9358-146">解除安裝 MS OMS</span><span class="sxs-lookup"><span data-stu-id="f9358-146">Uninstall MS OMS</span></span>

<span data-ttu-id="f9358-147">toouninstall MS OMS 輸入 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="f9358-147">toouninstall MS OMS enter hello following command:</span></span>

```bash
$ dcos package uninstall msoms
```

## <a name="let-us-know"></a><span data-ttu-id="f9358-148">請告訴我們！</span><span class="sxs-lookup"><span data-stu-id="f9358-148">Let us know!!!</span></span>
<span data-ttu-id="f9358-149">哪些資訊是有用的？</span><span class="sxs-lookup"><span data-stu-id="f9358-149">What works?</span></span> <span data-ttu-id="f9358-150">缺少哪些資訊？</span><span class="sxs-lookup"><span data-stu-id="f9358-150">What is missing?</span></span> <span data-ttu-id="f9358-151">還有什麼您需要此 toobe 有用了？</span><span class="sxs-lookup"><span data-stu-id="f9358-151">What else do you need for this toobe useful for you?</span></span> <span data-ttu-id="f9358-152">請透過 <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a> 告訴我們。</span><span class="sxs-lookup"><span data-stu-id="f9358-152">Let us know at <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9358-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f9358-153">Next steps</span></span>

 <span data-ttu-id="f9358-154">既然您已設定 OMS toomonitor 您容器[看到儀表板容器](../../log-analytics/log-analytics-containers.md)。</span><span class="sxs-lookup"><span data-stu-id="f9358-154">Now that you have set up OMS toomonitor your containers,[see your container dashboard](../../log-analytics/log-analytics-containers.md).</span></span>
