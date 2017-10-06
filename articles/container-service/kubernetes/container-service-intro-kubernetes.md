---
title: "aaaIntroduction tooAzure Kubernetes 的容器服務 |Microsoft 文件"
description: "Kubernetes azure 容器服務便可簡單 toodeploy 並管理容器應用程式在 Azure 上。"
services: container-service
documentationcenter: 
author: gabrtv
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Kubernetes, Docker, 容器, 微服務, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2017
ms.author: gamonroy
ms.custom: mvc
ms.openlocfilehash: bfc85a180bdf4a405c9047eb882d3eed01640dd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-container-service-for-kubernetes"></a><span data-ttu-id="34d16-104">簡介 tooAzure Kubernetes 的容器服務</span><span class="sxs-lookup"><span data-stu-id="34d16-104">Introduction tooAzure Container Service for Kubernetes</span></span>
<span data-ttu-id="34d16-105">使得簡單 toocreate Kubernetes azure 容器服務、 設定和管理所預先設定的 toorun 容器化應用程式的虛擬機器的叢集。</span><span class="sxs-lookup"><span data-stu-id="34d16-105">Azure Container Service for Kubernetes makes it simple toocreate, configure, and manage a cluster of virtual machines that are preconfigured toorun containerized applications.</span></span> <span data-ttu-id="34d16-106">這可讓您 toouse 您現有的技術，或運用社群專業知識，toodeploy 大量且不斷主體和管理容器應用程式在 Microsoft Azure 上。</span><span class="sxs-lookup"><span data-stu-id="34d16-106">This enables you toouse your existing skills, or draw upon a large and growing body of community expertise, toodeploy and manage container-based applications on Microsoft Azure.</span></span>

<span data-ttu-id="34d16-107">藉由使用 Azure 容器服務，您可以利用 hello 企業級功能的 Azure，同時仍維持 Kubernetes 透過應用程式可攜性和 hello Docker 映像格式。</span><span class="sxs-lookup"><span data-stu-id="34d16-107">By using Azure Container Service, you can take advantage of hello enterprise-grade features of Azure, while still maintaining application portability through Kubernetes and hello Docker image format.</span></span>

## <a name="using-azure-container-service-for-kubernetes"></a><span data-ttu-id="34d16-108">使用 Azure Container Service for Kubernetes</span><span class="sxs-lookup"><span data-stu-id="34d16-108">Using Azure Container Service for Kubernetes</span></span>
<span data-ttu-id="34d16-109">我們使用 Azure 容器服務的目標是使用開放原始碼工具和技術，現在都可以在我們的客戶之間的熱門 tooprovide 容器主機環境。</span><span class="sxs-lookup"><span data-stu-id="34d16-109">Our goal with Azure Container Service is tooprovide a container hosting environment by using open-source tools and technologies that are popular among our customers today.</span></span> <span data-ttu-id="34d16-110">toothis 結束時，我們展現 hello 標準 Kubernetes API 端點。</span><span class="sxs-lookup"><span data-stu-id="34d16-110">toothis end, we expose hello standard Kubernetes API endpoints.</span></span> <span data-ttu-id="34d16-111">藉由使用這些標準端點，您可以利用能夠進行交談 tooa Kubernetes 叢集的任何軟體。</span><span class="sxs-lookup"><span data-stu-id="34d16-111">By using these standard endpoints, you can leverage any software that is capable of talking tooa Kubernetes cluster.</span></span> <span data-ttu-id="34d16-112">例如，您可能會選擇 [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/)、[helm](https://helm.sh/) 或 [draft](https://github.com/Azure/draft)。</span><span class="sxs-lookup"><span data-stu-id="34d16-112">For example, you might choose [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [helm](https://helm.sh/), or [draft](https://github.com/Azure/draft).</span></span>

## <a name="creating-a-kubernetes-cluster-using-azure-container-service"></a><span data-ttu-id="34d16-113">使用 Azure Container Service 建立 Kubernetes 叢集</span><span class="sxs-lookup"><span data-stu-id="34d16-113">Creating a Kubernetes cluster using Azure Container Service</span></span>
<span data-ttu-id="34d16-114">使用 Azure 的容器服務 toobegin 部署 Azure 容器服務叢集以 hello [Azure CLI 2.0](container-service-kubernetes-walkthrough.md)或透過 hello 入口網站 (搜尋 hello Marketplace 的**Azure 容器服務**)。</span><span class="sxs-lookup"><span data-stu-id="34d16-114">toobegin using Azure Container Service, deploy an Azure Container Service cluster with hello [Azure CLI 2.0](container-service-kubernetes-walkthrough.md) or via hello portal (search hello Marketplace for **Azure Container Service**).</span></span> <span data-ttu-id="34d16-115">如果您需要更充分掌控 hello Azure Resource Manager 範本的進階的使用者，您可以使用 hello 開放原始碼[acs 引擎](https://github.com/Azure/acs-engine)專案 toobuild 您自己自訂的 Kubernetes 叢集，並將其部署透過 hello `az` CLI。</span><span class="sxs-lookup"><span data-stu-id="34d16-115">If you are an advanced user who needs more control over hello Azure Resource Manager templates, you can use hello open source [acs-engine](https://github.com/Azure/acs-engine) project toobuild your own custom Kubernetes cluster and deploy it via hello `az` CLI.</span></span>

### <a name="using-kubernetes"></a><span data-ttu-id="34d16-116">使用 Kubernetes</span><span class="sxs-lookup"><span data-stu-id="34d16-116">Using Kubernetes</span></span>
<span data-ttu-id="34d16-117">Kubernetes 能自動化部署、調整和管理容器化應用程式。</span><span class="sxs-lookup"><span data-stu-id="34d16-117">Kubernetes automates deployment, scaling, and management of containerized applications.</span></span> <span data-ttu-id="34d16-118">它包含一組豐富的功能，包括︰</span><span class="sxs-lookup"><span data-stu-id="34d16-118">It has a rich set of features including:</span></span>
* <span data-ttu-id="34d16-119">自動 binpacking</span><span class="sxs-lookup"><span data-stu-id="34d16-119">Automatic binpacking</span></span>
* <span data-ttu-id="34d16-120">自我修復</span><span class="sxs-lookup"><span data-stu-id="34d16-120">Self-healing</span></span>
* <span data-ttu-id="34d16-121">水平調整</span><span class="sxs-lookup"><span data-stu-id="34d16-121">Horizontal scaling</span></span>
* <span data-ttu-id="34d16-122">服務探索和負載平衡</span><span class="sxs-lookup"><span data-stu-id="34d16-122">Service discovery and load balancing</span></span>
* <span data-ttu-id="34d16-123">自動化推出和復原</span><span class="sxs-lookup"><span data-stu-id="34d16-123">Automated rollouts and rollbacks</span></span>
* <span data-ttu-id="34d16-124">祕密和組態管理</span><span class="sxs-lookup"><span data-stu-id="34d16-124">Secret and configuration management</span></span>
* <span data-ttu-id="34d16-125">儲存體協調流程</span><span class="sxs-lookup"><span data-stu-id="34d16-125">Storage orchestration</span></span>
* <span data-ttu-id="34d16-126">批次執行</span><span class="sxs-lookup"><span data-stu-id="34d16-126">Batch execution</span></span>

<span data-ttu-id="34d16-127">透過 Container Service 部署的 Kubernetes 架構圖：</span><span class="sxs-lookup"><span data-stu-id="34d16-127">Architectural diagram of Kubernetes deployed via Azure Container Service:</span></span>

![Azure 容器服務設定 toouse Kubernetes。](media/acs-intro/kubernetes.png)

## <a name="videos"></a><span data-ttu-id="34d16-129">影片</span><span class="sxs-lookup"><span data-stu-id="34d16-129">Videos</span></span>

<span data-ttu-id="34d16-130">Azure Container Service 中的 Kubernetes 支援 (Azure Friday，2017 年 1 月)：</span><span class="sxs-lookup"><span data-stu-id="34d16-130">Kubernetes Support in Azure Container Services (Azure Friday, January 2017):</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Kubernetes-Support-in-Azure-Container-Services/player]
>
>

<span data-ttu-id="34d16-131">用於在 Kubernetes 開發及部署應用程式的工具 (Azure OpenDev，2017 年 6 月)：</span><span class="sxs-lookup"><span data-stu-id="34d16-131">Tools for Developing and Deploying Applications on Kubernetes (Azure OpenDev, June 2017):</span></span>

> [!VIDEO https://channel9.msdn.com/Events/AzureOpenDev/June2017/Tools-for-Developing-and-Deploying-Applications-on-Kubernetes/player]
>
>

## <a name="next-steps"></a><span data-ttu-id="34d16-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="34d16-132">Next steps</span></span>

<span data-ttu-id="34d16-133">瀏覽 hello [Kubernetes 快速入門](container-service-kubernetes-walkthrough.md)toobegin 今天瀏覽 Azure 容器服務。</span><span class="sxs-lookup"><span data-stu-id="34d16-133">Explore hello [Kubernetes Quickstart](container-service-kubernetes-walkthrough.md) toobegin exploring Azure Container Service today.</span></span>
