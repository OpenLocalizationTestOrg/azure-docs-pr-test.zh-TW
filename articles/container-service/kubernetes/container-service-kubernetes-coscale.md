---
title: "aaaMonitor Azure Kubernetes 叢集 CoScale |Microsoft 文件"
description: "使用 CoScale 監視 Azure Container Service 中的 Kubernetes 叢集"
services: container-service
documentationcenter: 
author: fryckbos
manager: 
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: f835e82d2be3afe1d85070bd0bf69649cc6dd2ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-with-coscale"></a><span data-ttu-id="61efe-103">使用 CoScale 監視 Azure Container Service Kubernetes 叢集</span><span class="sxs-lookup"><span data-stu-id="61efe-103">Monitor an Azure Container Service Kubernetes cluster with CoScale</span></span>

<span data-ttu-id="61efe-104">在本文中，我們會示範如何 toodeploy hello [CoScale](https://www.coscale.com/)代理程式 toomonitor Azure 容器服務中的所有節點和容器，在您 Kubernetes 都叢集。</span><span class="sxs-lookup"><span data-stu-id="61efe-104">In this article, we show you how toodeploy hello [CoScale](https://www.coscale.com/) agent toomonitor all nodes and containers in your Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="61efe-105">您需要 CoScale 帳戶以進行這項設定。</span><span class="sxs-lookup"><span data-stu-id="61efe-105">You need an account with CoScale for this configuration.</span></span> 


## <a name="about-coscale"></a><span data-ttu-id="61efe-106">關於 CoScale</span><span class="sxs-lookup"><span data-stu-id="61efe-106">About CoScale</span></span> 

<span data-ttu-id="61efe-107">CoScale 是監視平台，收集數個協調流程平台上所有容器的計量和事件。</span><span class="sxs-lookup"><span data-stu-id="61efe-107">CoScale is a monitoring platform that gathers metrics and events from all containers in several orchestration platforms.</span></span> <span data-ttu-id="61efe-108">CoScale 提供 Kubernetes 環境的全方位監視。</span><span class="sxs-lookup"><span data-stu-id="61efe-108">CoScale offers full-stack monitoring for Kubernetes environments.</span></span> <span data-ttu-id="61efe-109">它提供視覺效果和分析 hello 堆疊中的所有圖層： hello OS、 Kubernetes、 Docker 和在您的容器內執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="61efe-109">It provides visualizations and analytics for all layers in hello stack: hello OS, Kubernetes, Docker, and applications running inside your containers.</span></span> <span data-ttu-id="61efe-110">CoScale 提供數個內建監視儀表板，它有內建的異常偵測 tooallow 運算子和快速開發人員 toofind 基礎結構和應用程式問題。</span><span class="sxs-lookup"><span data-stu-id="61efe-110">CoScale offers several built-in monitoring dashboards, and it has built-in anomaly detection tooallow operators and developers toofind infrastructure and application issues fast.</span></span>

![CoScale UI](./media/container-service-kubernetes-coscale/coscale.png)

<span data-ttu-id="61efe-112">本文所示，您可以安裝代理程式上 Kubernetes 叢集 toorun CoScale 做為 SaaS 解決方案。</span><span class="sxs-lookup"><span data-stu-id="61efe-112">As shown in this article, you can install agents on a Kubernetes cluster toorun CoScale as a SaaS solution.</span></span> <span data-ttu-id="61efe-113">如果您希望 tookeep 資料公司，CoScale 也是可在內部部署安裝。</span><span class="sxs-lookup"><span data-stu-id="61efe-113">If you want tookeep your data on-site, CoScale is also available for on-premises installation.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="61efe-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="61efe-114">Prerequisites</span></span>

<span data-ttu-id="61efe-115">您必須先太[建立 CoScale 帳戶](https://www.coscale.com/free-trial)。</span><span class="sxs-lookup"><span data-stu-id="61efe-115">You first need too[create a CoScale account](https://www.coscale.com/free-trial).</span></span>

<span data-ttu-id="61efe-116">本逐步解說假設您已[使用 Azure Container Service 建立 Kubernetes 叢集](container-service-kubernetes-walkthrough.md)。</span><span class="sxs-lookup"><span data-stu-id="61efe-116">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="61efe-117">它也假設您擁有 hello `az` Azure CLI 和`kubectl`安裝工具。</span><span class="sxs-lookup"><span data-stu-id="61efe-117">It also assumes that you have hello `az` Azure CLI and `kubectl` tools installed.</span></span>

<span data-ttu-id="61efe-118">您可以測試是否有 hello`az`安裝執行工具：</span><span class="sxs-lookup"><span data-stu-id="61efe-118">You can test if you have hello `az` tool installed by running:</span></span>

```azurecli
az --version
```

<span data-ttu-id="61efe-119">如果您沒有 hello`az`工具安裝，指示[這裡](/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="61efe-119">If you don't have hello `az` tool installed, there are instructions [here](/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="61efe-120">您可以測試是否有 hello`kubectl`安裝執行工具：</span><span class="sxs-lookup"><span data-stu-id="61efe-120">You can test if you have hello `kubectl` tool installed by running:</span></span>

```bash
kubectl version
```

<span data-ttu-id="61efe-121">如果您尚未安裝 `kubectl`，可以執行︰</span><span class="sxs-lookup"><span data-stu-id="61efe-121">If you don't have `kubectl` installed, you can run:</span></span>

```azurecli
az acs kubernetes install-cli
```

## <a name="installing-hello-coscale-agent-with-a-daemonset"></a><span data-ttu-id="61efe-122">安裝 DaemonSet hello CoScale 代理程式</span><span class="sxs-lookup"><span data-stu-id="61efe-122">Installing hello CoScale agent with a DaemonSet</span></span>
<span data-ttu-id="61efe-123">[DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/)是 Kubernetes toorun 容器的單一執行個體上使用 hello 叢集中各主機。</span><span class="sxs-lookup"><span data-stu-id="61efe-123">[DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) are used by Kubernetes toorun a single instance of a container on each host in hello cluster.</span></span>
<span data-ttu-id="61efe-124">它們很適合執行例如 hello CoScale 代理程式監視代理程式。</span><span class="sxs-lookup"><span data-stu-id="61efe-124">They're perfect for running monitoring agents such as hello CoScale agent.</span></span>

<span data-ttu-id="61efe-125">在您登入 tooCoScale 之後，請繼續 toohello[代理程式 頁面](https://app.coscale.com/)tooinstall CoScale 代理程式使用 DaemonSet 在叢集上的。</span><span class="sxs-lookup"><span data-stu-id="61efe-125">After you log in tooCoScale, go toohello [agent page](https://app.coscale.com/) tooinstall CoScale agents on your cluster using a DaemonSet.</span></span> <span data-ttu-id="61efe-126">hello CoScale UI 提供引導式的組態步驟 toocreate 代理程式，並開始監視完整的 Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="61efe-126">hello CoScale UI provides guided configuration steps toocreate an agent and start monitoring your complete Kubernetes cluster.</span></span>

![CoScale 代理程式設定](./media/container-service-kubernetes-coscale/installation.png)

<span data-ttu-id="61efe-128">hello 在叢集上，執行命令提供的 hello toostart hello 代理程式：</span><span class="sxs-lookup"><span data-stu-id="61efe-128">toostart hello agent on hello cluster, run hello supplied command:</span></span>

![啟動 hello CoScale 代理程式](./media/container-service-kubernetes-coscale/agent_script.png)

<span data-ttu-id="61efe-130">就這麼簡單！</span><span class="sxs-lookup"><span data-stu-id="61efe-130">That's it!</span></span> <span data-ttu-id="61efe-131">一旦 hello 代理程式正在執行，您應該在幾分鐘內看到 hello 主控台中的資料。</span><span class="sxs-lookup"><span data-stu-id="61efe-131">Once hello agents are up and running, you should see data in hello console in a few minutes.</span></span> <span data-ttu-id="61efe-132">請瀏覽 hello[代理程式 頁面](https://app.coscale.com/)toosee 叢集的摘要執行其他設定步驟，並查看儀表板例如 hello **Kubernetes 叢集概觀**。</span><span class="sxs-lookup"><span data-stu-id="61efe-132">Visit hello [agent page](https://app.coscale.com/) toosee a summary of your cluster, perform additional configuration steps, and see dashboards such as hello **Kubernetes cluster overview**.</span></span>

![Kubernetes 叢集概觀](./media/container-service-kubernetes-coscale/dashboard_clusteroverview.png)

<span data-ttu-id="61efe-134">hello CoScale 代理程式會自動部署 hello 叢集中的新電腦上。</span><span class="sxs-lookup"><span data-stu-id="61efe-134">hello CoScale agent is automatically deployed on new machines in hello cluster.</span></span> <span data-ttu-id="61efe-135">hello 代理程式更新的新版本時自動釋放。</span><span class="sxs-lookup"><span data-stu-id="61efe-135">hello agent updates automatically when a new version is released.</span></span>


## <a name="next-steps"></a><span data-ttu-id="61efe-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="61efe-136">Next steps</span></span>

<span data-ttu-id="61efe-137">請參閱 hello [CoScale 文件](http://docs.coscale.com/)和[部落格](https://www.coscale.com/blog)如需 CoScale 監視解決方案，更詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="61efe-137">See hello [CoScale documentation](http://docs.coscale.com/) and [blog](https://www.coscale.com/blog) for more more information about CoScale monitoring solutions.</span></span> 

