---
title: "使用 CoScale 監視 Azure Kubernetes 叢集 | Microsoft Docs"
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
ms.openlocfilehash: f894191baced710fc0f5a8c8692df98033341a48
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-with-coscale"></a><span data-ttu-id="51d59-103">使用 CoScale 監視 Azure Container Service Kubernetes 叢集</span><span class="sxs-lookup"><span data-stu-id="51d59-103">Monitor an Azure Container Service Kubernetes cluster with CoScale</span></span>

<span data-ttu-id="51d59-104">在本文中，我們會示範如何部署 [CoScale](https://www.coscale.com/) 代理程式，監視 Azure Container Service 中 Kubernetes 叢集的所有節點和容器。</span><span class="sxs-lookup"><span data-stu-id="51d59-104">In this article, we show you how to deploy the [CoScale](https://www.coscale.com/) agent to monitor all nodes and containers in your Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="51d59-105">您需要 CoScale 帳戶以進行這項設定。</span><span class="sxs-lookup"><span data-stu-id="51d59-105">You need an account with CoScale for this configuration.</span></span> 


## <a name="about-coscale"></a><span data-ttu-id="51d59-106">關於 CoScale</span><span class="sxs-lookup"><span data-stu-id="51d59-106">About CoScale</span></span> 

<span data-ttu-id="51d59-107">CoScale 是監視平台，收集數個協調流程平台上所有容器的計量和事件。</span><span class="sxs-lookup"><span data-stu-id="51d59-107">CoScale is a monitoring platform that gathers metrics and events from all containers in several orchestration platforms.</span></span> <span data-ttu-id="51d59-108">CoScale 提供 Kubernetes 環境的全方位監視。</span><span class="sxs-lookup"><span data-stu-id="51d59-108">CoScale offers full-stack monitoring for Kubernetes environments.</span></span> <span data-ttu-id="51d59-109">它提供堆疊中所有圖層的視覺效果和分析：作業系統、Kubernetes、Docker 和容器內執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="51d59-109">It provides visualizations and analytics for all layers in the stack: the OS, Kubernetes, Docker, and applications running inside your containers.</span></span> <span data-ttu-id="51d59-110">CoScale 提供數個內建的監視儀表板，而且具有內建的異常偵測，可讓操作人員和開發人員快速找出基礎結構和應用程式的問題。</span><span class="sxs-lookup"><span data-stu-id="51d59-110">CoScale offers several built-in monitoring dashboards, and it has built-in anomaly detection to allow operators and developers to find infrastructure and application issues fast.</span></span>

![CoScale UI](./media/container-service-kubernetes-coscale/coscale.png)

<span data-ttu-id="51d59-112">如本文所示，您可以在 Kubernetes 叢集上安裝代理程式，將 CoScale 當成 SaaS 解決方案執行。</span><span class="sxs-lookup"><span data-stu-id="51d59-112">As shown in this article, you can install agents on a Kubernetes cluster to run CoScale as a SaaS solution.</span></span> <span data-ttu-id="51d59-113">如果您想要在現場保留資料，CoScale 也提供內部部署安裝。</span><span class="sxs-lookup"><span data-stu-id="51d59-113">If you want to keep your data on-site, CoScale is also available for on-premises installation.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="51d59-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="51d59-114">Prerequisites</span></span>

<span data-ttu-id="51d59-115">您需要先[建立 CoScale 帳戶](https://www.coscale.com/free-trial)。</span><span class="sxs-lookup"><span data-stu-id="51d59-115">You first need to [create a CoScale account](https://www.coscale.com/free-trial).</span></span>

<span data-ttu-id="51d59-116">本逐步解說假設您已[使用 Azure Container Service 建立 Kubernetes 叢集](container-service-kubernetes-walkthrough.md)。</span><span class="sxs-lookup"><span data-stu-id="51d59-116">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="51d59-117">同時也假設您已經安裝 `az` Azure CLI 和 `kubectl` 工具。</span><span class="sxs-lookup"><span data-stu-id="51d59-117">It also assumes that you have the `az` Azure CLI and `kubectl` tools installed.</span></span>

<span data-ttu-id="51d59-118">您可以藉由執行下列操作來測試是否已安裝 `az` 工具：</span><span class="sxs-lookup"><span data-stu-id="51d59-118">You can test if you have the `az` tool installed by running:</span></span>

```azurecli
az --version
```

<span data-ttu-id="51d59-119">如果您尚未安裝 `az` 工具，[這裡](/cli/azure/install-azure-cli)有指示。</span><span class="sxs-lookup"><span data-stu-id="51d59-119">If you don't have the `az` tool installed, there are instructions [here](/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="51d59-120">您可以藉由執行下列操作來測試是否已安裝 `kubectl` 工具：</span><span class="sxs-lookup"><span data-stu-id="51d59-120">You can test if you have the `kubectl` tool installed by running:</span></span>

```bash
kubectl version
```

<span data-ttu-id="51d59-121">如果您尚未安裝 `kubectl`，可以執行︰</span><span class="sxs-lookup"><span data-stu-id="51d59-121">If you don't have `kubectl` installed, you can run:</span></span>

```azurecli
az acs kubernetes install-cli
```

## <a name="installing-the-coscale-agent-with-a-daemonset"></a><span data-ttu-id="51d59-122">使用 DaemonSet 安裝 CoScale 代理程式</span><span class="sxs-lookup"><span data-stu-id="51d59-122">Installing the CoScale agent with a DaemonSet</span></span>
<span data-ttu-id="51d59-123">[DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) 是 Kubernetes 用來在叢集中每個主機上執行容器的單一執行個體。</span><span class="sxs-lookup"><span data-stu-id="51d59-123">[DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) are used by Kubernetes to run a single instance of a container on each host in the cluster.</span></span>
<span data-ttu-id="51d59-124">它們非常適合執行監視代理程式，例如 CoScale 代理程式。</span><span class="sxs-lookup"><span data-stu-id="51d59-124">They're perfect for running monitoring agents such as the CoScale agent.</span></span>

<span data-ttu-id="51d59-125">登入 CoScale 之後，請移至[代理程式頁面](https://app.coscale.com/)使用 DaemonSet 在您的叢集上安裝 CoScale 代理程式。</span><span class="sxs-lookup"><span data-stu-id="51d59-125">After you log in to CoScale, go to the [agent page](https://app.coscale.com/) to install CoScale agents on your cluster using a DaemonSet.</span></span> <span data-ttu-id="51d59-126">CoScale UI 提供引導式設定步驟，讓您建立代理程式並開始監視完整的 Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="51d59-126">The CoScale UI provides guided configuration steps to create an agent and start monitoring your complete Kubernetes cluster.</span></span>

![CoScale 代理程式設定](./media/container-service-kubernetes-coscale/installation.png)

<span data-ttu-id="51d59-128">若要在叢集上啟動代理程式，請執行提供的命令：</span><span class="sxs-lookup"><span data-stu-id="51d59-128">To start the agent on the cluster, run the supplied command:</span></span>

![啟動 CoScale 代理程式](./media/container-service-kubernetes-coscale/agent_script.png)

<span data-ttu-id="51d59-130">就這麼簡單！</span><span class="sxs-lookup"><span data-stu-id="51d59-130">That's it!</span></span> <span data-ttu-id="51d59-131">當代理程式啟動並執行之後，幾分鐘之內您應該會在主控台中看到資料。</span><span class="sxs-lookup"><span data-stu-id="51d59-131">Once the agents are up and running, you should see data in the console in a few minutes.</span></span> <span data-ttu-id="51d59-132">請瀏覽[代理程式頁面](https://app.coscale.com/)查看叢集摘要，執行其他設定步驟並查看儀表板，例如 **Kubernetes 叢集概觀**。</span><span class="sxs-lookup"><span data-stu-id="51d59-132">Visit the [agent page](https://app.coscale.com/) to see a summary of your cluster, perform additional configuration steps, and see dashboards such as the **Kubernetes cluster overview**.</span></span>

![Kubernetes 叢集概觀](./media/container-service-kubernetes-coscale/dashboard_clusteroverview.png)

<span data-ttu-id="51d59-134">CoScale 代理程式會自動部署在叢集中的新機器上。</span><span class="sxs-lookup"><span data-stu-id="51d59-134">The CoScale agent is automatically deployed on new machines in the cluster.</span></span> <span data-ttu-id="51d59-135">新版本發行時，代理程式會自動更新。</span><span class="sxs-lookup"><span data-stu-id="51d59-135">The agent updates automatically when a new version is released.</span></span>


## <a name="next-steps"></a><span data-ttu-id="51d59-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="51d59-136">Next steps</span></span>

<span data-ttu-id="51d59-137">如需 CoScale 監視解決方案的詳細資訊，請參閱 [CoScale 文件](http://docs.coscale.com/)和[部落格](https://www.coscale.com/blog)。</span><span class="sxs-lookup"><span data-stu-id="51d59-137">See the [CoScale documentation](http://docs.coscale.com/) and [blog](https://www.coscale.com/blog) for more more information about CoScale monitoring solutions.</span></span> 

