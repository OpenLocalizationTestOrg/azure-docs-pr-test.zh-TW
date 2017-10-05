---
title: "使用 Datadog 監視 Azure Kubernetes 叢集 | Microsoft Docs"
description: "使用 Datadog 監視 Azure Container Service 中的 Kubernetes 叢集"
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: 40b34457447a8f80d8cdf77579750e0c42df22d0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-datadog"></a><span data-ttu-id="b8e16-103">使用 DataDog 監視 Azure Container Service 叢集</span><span class="sxs-lookup"><span data-stu-id="b8e16-103">Monitor an Azure Container Service cluster with DataDog</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b8e16-104">必要條件</span><span class="sxs-lookup"><span data-stu-id="b8e16-104">Prerequisites</span></span>
<span data-ttu-id="b8e16-105">本逐步解說假設您已[使用 Azure Container Service 建立 Kubernetes 叢集](container-service-kubernetes-walkthrough.md)。</span><span class="sxs-lookup"><span data-stu-id="b8e16-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="b8e16-106">同時也假設您已經安裝 `az` Azure cli 和 `kubectl` 工具。</span><span class="sxs-lookup"><span data-stu-id="b8e16-106">It also assumes that you have the `az` Azure cli and `kubectl` tools installed.</span></span>

<span data-ttu-id="b8e16-107">您可以藉由執行下列操作來測試是否已安裝 `az` 工具：</span><span class="sxs-lookup"><span data-stu-id="b8e16-107">You can test if you have the `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="b8e16-108">如果您尚未安裝 `az` 工具，[這裡](https://github.com/azure/azure-cli#installation)有指示。</span><span class="sxs-lookup"><span data-stu-id="b8e16-108">If you don't have the `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="b8e16-109">您可以藉由執行下列操作來測試是否已安裝 `kubectl` 工具：</span><span class="sxs-lookup"><span data-stu-id="b8e16-109">You can test if you have the `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="b8e16-110">如果您尚未安裝 `kubectl`，可以執行︰</span><span class="sxs-lookup"><span data-stu-id="b8e16-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="datadog"></a><span data-ttu-id="b8e16-111">DataDog</span><span class="sxs-lookup"><span data-stu-id="b8e16-111">DataDog</span></span>
<span data-ttu-id="b8e16-112">Datadog 是一項監視服務，會從 Azure 容器服務叢集內的容器收集監視資料。</span><span class="sxs-lookup"><span data-stu-id="b8e16-112">Datadog is a monitoring service that gathers monitoring data from your containers within your Azure Container Service cluster.</span></span> <span data-ttu-id="b8e16-113">Datadog 有 Docker 整合儀表板，可供您查看容器內的特定度量。</span><span class="sxs-lookup"><span data-stu-id="b8e16-113">Datadog has a Docker Integration Dashboard where you can see specific metrics within your containers.</span></span> <span data-ttu-id="b8e16-114">從容器收集到的度量會依 CPU、記憶體、網路和 I/O 來加以整理。</span><span class="sxs-lookup"><span data-stu-id="b8e16-114">Metrics gathered from your containers are organized by CPU, Memory, Network and I/O.</span></span> <span data-ttu-id="b8e16-115">Datadog 會將度量分割成容器和映像。</span><span class="sxs-lookup"><span data-stu-id="b8e16-115">Datadog splits metrics into containers and images.</span></span>

<span data-ttu-id="b8e16-116">您必須先[建立帳戶 (英文)](https://www.datadoghq.com/lpg/)</span><span class="sxs-lookup"><span data-stu-id="b8e16-116">You first need to [create an account](https://www.datadoghq.com/lpg/)</span></span>

## <a name="installing-the-datadog-agent-with-a-daemonset"></a><span data-ttu-id="b8e16-117">使用 DaemonSet 安裝 Datadog Agent</span><span class="sxs-lookup"><span data-stu-id="b8e16-117">Installing the Datadog Agent with a DaemonSet</span></span>
<span data-ttu-id="b8e16-118">DaemonSet 是 Kubernetes 用來在叢集中每個主機上執行容器的單一執行個體。</span><span class="sxs-lookup"><span data-stu-id="b8e16-118">DaemonSets are used by Kubernetes to run a single instance of a container on each host in the cluster.</span></span>
<span data-ttu-id="b8e16-119">它們非常適合用來執行監視代理程式。</span><span class="sxs-lookup"><span data-stu-id="b8e16-119">They're perfect for running monitoring agents.</span></span>

<span data-ttu-id="b8e16-120">當您登入 Datadog 之後，您可以依照 [Datadog 指示 (英文)](https://app.datadoghq.com/account/settings#agent/kubernetes) 使用 DaemonSet 在您的叢集上安裝 Datadog Agent。</span><span class="sxs-lookup"><span data-stu-id="b8e16-120">Once you have logged into Datadog, you can follow the [Datadog instructions](https://app.datadoghq.com/account/settings#agent/kubernetes) to install Datadog agents on your cluster using a DaemonSet.</span></span>

## <a name="conclusion"></a><span data-ttu-id="b8e16-121">結論</span><span class="sxs-lookup"><span data-stu-id="b8e16-121">Conclusion</span></span>
<span data-ttu-id="b8e16-122">就這麼簡單！</span><span class="sxs-lookup"><span data-stu-id="b8e16-122">That's it!</span></span> <span data-ttu-id="b8e16-123">當代理程式啟動並執行之後，幾分鐘之內您應該會在主控台中看到資料。</span><span class="sxs-lookup"><span data-stu-id="b8e16-123">Once the agents are up and running you should see data in the console in a few minutes.</span></span> <span data-ttu-id="b8e16-124">您可以造訪這些整合式 [kubernetes 儀表板 (英文)](https://app.datadoghq.com/screen/integration/kubernetes) 以查看您的叢集摘要。</span><span class="sxs-lookup"><span data-stu-id="b8e16-124">You can visit the integrated [kubernetes dashboard](https://app.datadoghq.com/screen/integration/kubernetes) to see a summary of your cluster.</span></span>
