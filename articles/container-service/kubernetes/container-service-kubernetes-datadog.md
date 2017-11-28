---
title: "aaaMonitor Datadog 叢集 Azure Kubernetes |Microsoft 文件"
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
ms.openlocfilehash: bccd8b59a048e0f791172fcfc4eeba6370dafcc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-datadog"></a><span data-ttu-id="b2f71-103">使用 DataDog 監視 Azure Container Service 叢集</span><span class="sxs-lookup"><span data-stu-id="b2f71-103">Monitor an Azure Container Service cluster with DataDog</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b2f71-104">必要條件</span><span class="sxs-lookup"><span data-stu-id="b2f71-104">Prerequisites</span></span>
<span data-ttu-id="b2f71-105">本逐步解說假設您已[使用 Azure Container Service 建立 Kubernetes 叢集](container-service-kubernetes-walkthrough.md)。</span><span class="sxs-lookup"><span data-stu-id="b2f71-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="b2f71-106">它也假設您擁有 hello `az` Azure cli 和`kubectl`安裝工具。</span><span class="sxs-lookup"><span data-stu-id="b2f71-106">It also assumes that you have hello `az` Azure cli and `kubectl` tools installed.</span></span>

<span data-ttu-id="b2f71-107">您可以測試是否有 hello`az`安裝執行工具：</span><span class="sxs-lookup"><span data-stu-id="b2f71-107">You can test if you have hello `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="b2f71-108">如果您沒有 hello`az`工具安裝，指示[這裡](https://github.com/azure/azure-cli#installation)。</span><span class="sxs-lookup"><span data-stu-id="b2f71-108">If you don't have hello `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="b2f71-109">您可以測試是否有 hello`kubectl`安裝執行工具：</span><span class="sxs-lookup"><span data-stu-id="b2f71-109">You can test if you have hello `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="b2f71-110">如果您尚未安裝 `kubectl`，可以執行︰</span><span class="sxs-lookup"><span data-stu-id="b2f71-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="datadog"></a><span data-ttu-id="b2f71-111">DataDog</span><span class="sxs-lookup"><span data-stu-id="b2f71-111">DataDog</span></span>
<span data-ttu-id="b2f71-112">Datadog 是一項監視服務，會從 Azure 容器服務叢集內的容器收集監視資料。</span><span class="sxs-lookup"><span data-stu-id="b2f71-112">Datadog is a monitoring service that gathers monitoring data from your containers within your Azure Container Service cluster.</span></span> <span data-ttu-id="b2f71-113">Datadog 有 Docker 整合儀表板，可供您查看容器內的特定度量。</span><span class="sxs-lookup"><span data-stu-id="b2f71-113">Datadog has a Docker Integration Dashboard where you can see specific metrics within your containers.</span></span> <span data-ttu-id="b2f71-114">從容器收集到的度量會依 CPU、記憶體、網路和 I/O 來加以整理。</span><span class="sxs-lookup"><span data-stu-id="b2f71-114">Metrics gathered from your containers are organized by CPU, Memory, Network and I/O.</span></span> <span data-ttu-id="b2f71-115">Datadog 會將度量分割成容器和映像。</span><span class="sxs-lookup"><span data-stu-id="b2f71-115">Datadog splits metrics into containers and images.</span></span>

<span data-ttu-id="b2f71-116">您必須先太[建立帳戶](https://www.datadoghq.com/lpg/)</span><span class="sxs-lookup"><span data-stu-id="b2f71-116">You first need too[create an account](https://www.datadoghq.com/lpg/)</span></span>

## <a name="installing-hello-datadog-agent-with-a-daemonset"></a><span data-ttu-id="b2f71-117">安裝 DaemonSet hello Datadog 代理程式</span><span class="sxs-lookup"><span data-stu-id="b2f71-117">Installing hello Datadog Agent with a DaemonSet</span></span>
<span data-ttu-id="b2f71-118">DaemonSets 所使用的 Kubernetes toorun hello 叢集中各主機上的容器的單一執行個體。</span><span class="sxs-lookup"><span data-stu-id="b2f71-118">DaemonSets are used by Kubernetes toorun a single instance of a container on each host in hello cluster.</span></span>
<span data-ttu-id="b2f71-119">它們非常適合用來執行監視代理程式。</span><span class="sxs-lookup"><span data-stu-id="b2f71-119">They're perfect for running monitoring agents.</span></span>

<span data-ttu-id="b2f71-120">一旦您登入 Datadog，您可以依照 hello [Datadog 指示](https://app.datadoghq.com/account/settings#agent/kubernetes)tooinstall Datadog 代理程式使用 DaemonSet 在叢集上的。</span><span class="sxs-lookup"><span data-stu-id="b2f71-120">Once you have logged into Datadog, you can follow hello [Datadog instructions](https://app.datadoghq.com/account/settings#agent/kubernetes) tooinstall Datadog agents on your cluster using a DaemonSet.</span></span>

## <a name="conclusion"></a><span data-ttu-id="b2f71-121">結論</span><span class="sxs-lookup"><span data-stu-id="b2f71-121">Conclusion</span></span>
<span data-ttu-id="b2f71-122">就這麼簡單！</span><span class="sxs-lookup"><span data-stu-id="b2f71-122">That's it!</span></span> <span data-ttu-id="b2f71-123">一旦 hello 代理程式已啟動並執行您應該會看到 hello 主控台中的資料在幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="b2f71-123">Once hello agents are up and running you should see data in hello console in a few minutes.</span></span> <span data-ttu-id="b2f71-124">您可以瀏覽 hello 整合[kubernetes 儀表板](https://app.datadoghq.com/screen/integration/kubernetes)toosee 叢集的摘要。</span><span class="sxs-lookup"><span data-stu-id="b2f71-124">You can visit hello integrated [kubernetes dashboard](https://app.datadoghq.com/screen/integration/kubernetes) toosee a summary of your cluster.</span></span>
