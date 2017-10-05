---
title: "Azure Container Service for Kubernetes 簡介 | Microsoft Docs"
description: "Azure Container Service for Kubernetes 可讓您輕鬆地部署和管理 Azure 上的容器型應用程式。"
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
ms.openlocfilehash: 92cdbe20e7a2974a734dfed5294c547866050290
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="introduction-to-azure-container-service-for-kubernetes"></a><span data-ttu-id="3538a-104">Azure Container Service for Kubernetes 簡介</span><span class="sxs-lookup"><span data-stu-id="3538a-104">Introduction to Azure Container Service for Kubernetes</span></span>
<span data-ttu-id="3538a-105">Azure Container Service for Kubernetes 可讓您輕鬆建立、設定及管理虛擬機器的叢集，這些虛擬機器預先設定為執行容器化應用程式。</span><span class="sxs-lookup"><span data-stu-id="3538a-105">Azure Container Service for Kubernetes makes it simple to create, configure, and manage a cluster of virtual machines that are preconfigured to run containerized applications.</span></span> <span data-ttu-id="3538a-106">這樣可讓您使用現有技能，或運用大量且不斷成長的社群專業知識，在 Microsoft Azure 上部署及管理容器應用程式。</span><span class="sxs-lookup"><span data-stu-id="3538a-106">This enables you to use your existing skills, or draw upon a large and growing body of community expertise, to deploy and manage container-based applications on Microsoft Azure.</span></span>

<span data-ttu-id="3538a-107">藉由使用 Azure Container Service，您可以充分利用 Azure 的企業級功能，同時仍可保有應用程式在 Kubernetes 內的可攜性和 Docker 映像格式。</span><span class="sxs-lookup"><span data-stu-id="3538a-107">By using Azure Container Service, you can take advantage of the enterprise-grade features of Azure, while still maintaining application portability through Kubernetes and the Docker image format.</span></span>

## <a name="using-azure-container-service-for-kubernetes"></a><span data-ttu-id="3538a-108">使用 Azure Container Service for Kubernetes</span><span class="sxs-lookup"><span data-stu-id="3538a-108">Using Azure Container Service for Kubernetes</span></span>
<span data-ttu-id="3538a-109">我們對於 Azure Container Service 的目標，是要使用現今頗受客戶歡迎的開放原始碼工具和技術，提供容器主控環境。</span><span class="sxs-lookup"><span data-stu-id="3538a-109">Our goal with Azure Container Service is to provide a container hosting environment by using open-source tools and technologies that are popular among our customers today.</span></span> <span data-ttu-id="3538a-110">為了這個目的，我們已公開標準 Kubernetes API 端點。</span><span class="sxs-lookup"><span data-stu-id="3538a-110">To this end, we expose the standard Kubernetes API endpoints.</span></span> <span data-ttu-id="3538a-111">透過這些標準端點，您可以利用任何能夠與 Kubernetes 叢集通訊的軟體。</span><span class="sxs-lookup"><span data-stu-id="3538a-111">By using these standard endpoints, you can leverage any software that is capable of talking to a Kubernetes cluster.</span></span> <span data-ttu-id="3538a-112">例如，您可能會選擇 [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/)、[helm](https://helm.sh/) 或 [draft](https://github.com/Azure/draft)。</span><span class="sxs-lookup"><span data-stu-id="3538a-112">For example, you might choose [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [helm](https://helm.sh/), or [draft](https://github.com/Azure/draft).</span></span>

## <a name="creating-a-kubernetes-cluster-using-azure-container-service"></a><span data-ttu-id="3538a-113">使用 Azure Container Service 建立 Kubernetes 叢集</span><span class="sxs-lookup"><span data-stu-id="3538a-113">Creating a Kubernetes cluster using Azure Container Service</span></span>
<span data-ttu-id="3538a-114">若要開始使用 Azure Container Service，請使用 [Azure CLI 2.0](container-service-kubernetes-walkthrough.md) 或透過入口網站 (在 Marketplace 內搜尋 **Azure Container Service**) 來部署 Azure Container Service 叢集。</span><span class="sxs-lookup"><span data-stu-id="3538a-114">To begin using Azure Container Service, deploy an Azure Container Service cluster with the [Azure CLI 2.0](container-service-kubernetes-walkthrough.md) or via the portal (search the Marketplace for **Azure Container Service**).</span></span> <span data-ttu-id="3538a-115">如果您是需要更充分控制 Azure Resource Manager 範本的進階使用者，您可以使用開放原始碼 [acs-engine](https://github.com/Azure/acs-engine) 專案來建立您自己的自訂 Kubernetes 叢集，並透過 `az` CLI 來部署它。</span><span class="sxs-lookup"><span data-stu-id="3538a-115">If you are an advanced user who needs more control over the Azure Resource Manager templates, you can use the open source [acs-engine](https://github.com/Azure/acs-engine) project to build your own custom Kubernetes cluster and deploy it via the `az` CLI.</span></span>

### <a name="using-kubernetes"></a><span data-ttu-id="3538a-116">使用 Kubernetes</span><span class="sxs-lookup"><span data-stu-id="3538a-116">Using Kubernetes</span></span>
<span data-ttu-id="3538a-117">Kubernetes 能自動化部署、調整和管理容器化應用程式。</span><span class="sxs-lookup"><span data-stu-id="3538a-117">Kubernetes automates deployment, scaling, and management of containerized applications.</span></span> <span data-ttu-id="3538a-118">它包含一組豐富的功能，包括︰</span><span class="sxs-lookup"><span data-stu-id="3538a-118">It has a rich set of features including:</span></span>
* <span data-ttu-id="3538a-119">自動 binpacking</span><span class="sxs-lookup"><span data-stu-id="3538a-119">Automatic binpacking</span></span>
* <span data-ttu-id="3538a-120">自我修復</span><span class="sxs-lookup"><span data-stu-id="3538a-120">Self-healing</span></span>
* <span data-ttu-id="3538a-121">水平調整</span><span class="sxs-lookup"><span data-stu-id="3538a-121">Horizontal scaling</span></span>
* <span data-ttu-id="3538a-122">服務探索和負載平衡</span><span class="sxs-lookup"><span data-stu-id="3538a-122">Service discovery and load balancing</span></span>
* <span data-ttu-id="3538a-123">自動化推出和復原</span><span class="sxs-lookup"><span data-stu-id="3538a-123">Automated rollouts and rollbacks</span></span>
* <span data-ttu-id="3538a-124">祕密和組態管理</span><span class="sxs-lookup"><span data-stu-id="3538a-124">Secret and configuration management</span></span>
* <span data-ttu-id="3538a-125">儲存體協調流程</span><span class="sxs-lookup"><span data-stu-id="3538a-125">Storage orchestration</span></span>
* <span data-ttu-id="3538a-126">批次執行</span><span class="sxs-lookup"><span data-stu-id="3538a-126">Batch execution</span></span>

<span data-ttu-id="3538a-127">透過 Container Service 部署的 Kubernetes 架構圖：</span><span class="sxs-lookup"><span data-stu-id="3538a-127">Architectural diagram of Kubernetes deployed via Azure Container Service:</span></span>

![Azure Container Service 設定為使用 Kubernetes。](media/acs-intro/kubernetes.png)

## <a name="videos"></a><span data-ttu-id="3538a-129">影片</span><span class="sxs-lookup"><span data-stu-id="3538a-129">Videos</span></span>

<span data-ttu-id="3538a-130">Azure Container Service 中的 Kubernetes 支援 (Azure Friday，2017 年 1 月)：</span><span class="sxs-lookup"><span data-stu-id="3538a-130">Kubernetes Support in Azure Container Services (Azure Friday, January 2017):</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Kubernetes-Support-in-Azure-Container-Services/player]
>
>

<span data-ttu-id="3538a-131">用於在 Kubernetes 開發及部署應用程式的工具 (Azure OpenDev，2017 年 6 月)：</span><span class="sxs-lookup"><span data-stu-id="3538a-131">Tools for Developing and Deploying Applications on Kubernetes (Azure OpenDev, June 2017):</span></span>

> [!VIDEO https://channel9.msdn.com/Events/AzureOpenDev/June2017/Tools-for-Developing-and-Deploying-Applications-on-Kubernetes/player]
>
>

## <a name="next-steps"></a><span data-ttu-id="3538a-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3538a-132">Next steps</span></span>

<span data-ttu-id="3538a-133">瀏覽 [Kubernetes 快速入門](container-service-kubernetes-walkthrough.md)，立即開始探索 Azure Container Service。</span><span class="sxs-lookup"><span data-stu-id="3538a-133">Explore the [Kubernetes Quickstart](container-service-kubernetes-walkthrough.md) to begin exploring Azure Container Service today.</span></span>