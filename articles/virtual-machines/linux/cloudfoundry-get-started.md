---
title: "在 Microsoft Azure 上開始使用 Cloud Foundry | Microsoft Docs"
description: "在 Microsoft Azure 上執行 OSS 或 Pivotal Cloud Foundry"
services: virtual-machines-linux
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 2a15ffbf-9f86-41e4-b75b-eb44c1a2a7ab
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 01/19/2017
ms.author: seanmck
ms.openlocfilehash: 94fbde7707ea9a91076780fdefc3f5a827e0e7b2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="cloud-foundry-on-azure"></a><span data-ttu-id="ec177-103">Azure 上的 Cloud Foundry</span><span class="sxs-lookup"><span data-stu-id="ec177-103">Cloud Foundry on Azure</span></span>

<span data-ttu-id="ec177-104">Cloud Foundry 是開放原始碼的平台即服務 (PaaS)，可用於建置、部署和操作以各種不同語言和架構開發的 12-factor 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ec177-104">Cloud Foundry is an open-source platform-as-a-service (PaaS) for building, deploying, and operating 12-factor applications developed in various languages and frameworks.</span></span> <span data-ttu-id="ec177-105">本文件說明您可用來在 Azure 上執行 Cloud Foundry 的選項，以及應如何開始使用。</span><span class="sxs-lookup"><span data-stu-id="ec177-105">This document describes the options you have for running Cloud Foundry on Azure and how you can get started.</span></span>

## <a name="cloud-foundry-offerings"></a><span data-ttu-id="ec177-106">Cloud Foundry 供應項目</span><span class="sxs-lookup"><span data-stu-id="ec177-106">Cloud Foundry offerings</span></span>

<span data-ttu-id="ec177-107">有兩種形式的 Cloud Foundry 可在 Azure 上執行：開放原始碼的 Cloud Foundry (OSS CF) 和 Pivotal Cloud Foundry (PCF)。</span><span class="sxs-lookup"><span data-stu-id="ec177-107">There are two forms of Cloud Foundry available to run on Azure: open-source Cloud Foundry (OSS CF) and Pivotal Cloud Foundry (PCF).</span></span> <span data-ttu-id="ec177-108">OSS CF 是完全[開放原始碼](https://github.com/cloudfoundry)的 Cloud Foundry 版本，可透過 Cloud Foundry Foundation 來管理。</span><span class="sxs-lookup"><span data-stu-id="ec177-108">OSS CF is an entirely [open-source](https://github.com/cloudfoundry) version of Cloud Foundry managed by the Cloud Foundry Foundation.</span></span> <span data-ttu-id="ec177-109">Pivotal Cloud Foundry 是由 Pivotal Software Inc. 所提供的 Cloud Foundry 企業散發版本。我們將查看這兩個供應項目之間的差異。</span><span class="sxs-lookup"><span data-stu-id="ec177-109">Pivotal Cloud Foundry is an enterprise distribution of Cloud Foundry from Pivotal Software Inc. We look at some of the differences between the two offerings.</span></span>

### <a name="open-source-cloud-foundry"></a><span data-ttu-id="ec177-110">開放原始碼的 Cloud Foundry</span><span class="sxs-lookup"><span data-stu-id="ec177-110">Open-source Cloud Foundry</span></span>

<span data-ttu-id="ec177-111">您可以在 Azure 上部署 OSS Cloud Foundry，方法是使用 [GitHub 上提供的指示](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/blob/master/docs/guidance.md)，先部署 BOSH 導向器，然後再部署 Cloud Foundry。</span><span class="sxs-lookup"><span data-stu-id="ec177-111">You can deploy OSS Cloud Foundry on Azure by first deploying a BOSH director and then deploying Cloud Foundry, using the [instructions provided on GitHub](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/blob/master/docs/guidance.md).</span></span> <span data-ttu-id="ec177-112">若要深入了解如何使用 OSS CF，請參閱 Cloud Foundry Foundation 所提供的[文件](https://docs.cloudfoundry.org/)。</span><span class="sxs-lookup"><span data-stu-id="ec177-112">To learn more about using OSS CF, see the [documentation](https://docs.cloudfoundry.org/) provided by the Cloud Foundry Foundation.</span></span>

<span data-ttu-id="ec177-113">Microsoft 透過下列社群管道提供 OSS CF 的最佳支援：</span><span class="sxs-lookup"><span data-stu-id="ec177-113">Microsoft provides best-effort support for OSS CF through the following community channels:</span></span>

- #<a name="bosh-azure-cpi-channel-on-cloud-foundry-slackhttpsslackcloudfoundryorg"></a><span data-ttu-id="ec177-114">[Cloud Foundry Slack (英文)](https://slack.cloudfoundry.org/) 上的 bosh-azure-cpi 管道</span><span class="sxs-lookup"><span data-stu-id="ec177-114">bosh-azure-cpi channel on [Cloud Foundry Slack](https://slack.cloudfoundry.org/)</span></span>
- [<span data-ttu-id="ec177-115">cf-bosh 郵寄清單 (英文)</span><span class="sxs-lookup"><span data-stu-id="ec177-115">cf-bosh mailing list</span></span>](https://lists.cloudfoundry.org/pipermail/cf-bosh)
- <span data-ttu-id="ec177-116">GitHub 上關於 [CPI (英文)](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/issues) 和 [Service Broker (英文)](https://github.com/Azure/meta-azure-service-broker/issues) 的問題</span><span class="sxs-lookup"><span data-stu-id="ec177-116">GitHub issues for the [CPI](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/issues) and [service broker](https://github.com/Azure/meta-azure-service-broker/issues)</span></span>

>[!NOTE]
> <span data-ttu-id="ec177-117">對於您 Azure 資源 (例如，您執行 Cloud Foundry 的虛擬機器) 的支援層級是以您的 Azure 支援合約為根據。</span><span class="sxs-lookup"><span data-stu-id="ec177-117">The level of support for your Azure resources, such as the virtual machines where you run Cloud Foundry, is based on your Azure support agreement.</span></span> <span data-ttu-id="ec177-118">最佳的社群支援僅適用於 Cloud Foundry 特有的元件。</span><span class="sxs-lookup"><span data-stu-id="ec177-118">Best-effort community support only applies to the Cloud Foundry-specific components.</span></span>

### <a name="pivotal-cloud-foundry"></a><span data-ttu-id="ec177-119">Pivotal Cloud Foundry</span><span class="sxs-lookup"><span data-stu-id="ec177-119">Pivotal Cloud Foundry</span></span>

<span data-ttu-id="ec177-120">Pivotal Cloud Foundry 包含與 OSS 散發版本相同的核心平台，以及一組專屬的管理工具和企業支援。</span><span class="sxs-lookup"><span data-stu-id="ec177-120">Pivotal Cloud Foundry includes the same core platform as the OSS distribution, along with a set of proprietary management tools and enterprise support.</span></span> <span data-ttu-id="ec177-121">若要在 Azure 上執行 PCF，您必須取得 Pivotal 的授權。</span><span class="sxs-lookup"><span data-stu-id="ec177-121">To run PCF on Azure, you must acquire a license from Pivotal.</span></span> <span data-ttu-id="ec177-122">Azure Marketplace 提供的 PCF 優惠包括 90 天試用版授權。</span><span class="sxs-lookup"><span data-stu-id="ec177-122">The PCF offer from the Azure marketplace includes a 90-day trial license.</span></span>

<span data-ttu-id="ec177-123">這些工具包括 [Pivotal Operations Manager (英文)](http://docs.pivotal.io/pivotalcf/customizing/)、可簡化部署和管理 Cloud Foundry Foundation 的 Web 應用程式，以及 [Pivotal Apps Manager (英文)](https://docs.pivotal.io/pivotalcf/console/)，此為可用來管理使用者和應用程式的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ec177-123">The tools include [Pivotal Operations Manager](http://docs.pivotal.io/pivotalcf/customizing/), a web application that simplifies deployment and management of a Cloud Foundry foundation, and [Pivotal Apps Manager](https://docs.pivotal.io/pivotalcf/console/), a web application for managing users and applications.</span></span>

<span data-ttu-id="ec177-124">除了以上針對 OSS CF 列出的支援管道，PCF 授權還會賦與您連絡 Pivotal 以取得支援的權利。</span><span class="sxs-lookup"><span data-stu-id="ec177-124">In addition to the support channels listed for OSS CF above, a PCF license entitles you to contact Pivotal for support.</span></span> <span data-ttu-id="ec177-125">Microsoft 和 Pivotal 也已經啟用支援工作流程，可讓您連絡其中一方以取得協助，並讓您根據問題的所在位置適當地路由傳送查詢。</span><span class="sxs-lookup"><span data-stu-id="ec177-125">Microsoft and Pivotal have also enabled support workflows that allow you to contact either party for assistance and have your inquiry routed appropriately depending on where the issue lies.</span></span>

## <a name="azure-service-broker"></a><span data-ttu-id="ec177-126">Azure Service Broker</span><span class="sxs-lookup"><span data-stu-id="ec177-126">Azure Service Broker</span></span>

<span data-ttu-id="ec177-127">Cloud Foundry 鼓勵使用 ["twelve-factor app" (英文)](https://12factor.net/) 方法，明確區分無狀態應用程式程序和可設定狀態的備份服務。</span><span class="sxs-lookup"><span data-stu-id="ec177-127">Cloud Foundry encourages the ["twelve-factor app"](https://12factor.net/) methodology, which promotes a clean separation of stateless application processes and stateful backing services.</span></span> <span data-ttu-id="ec177-128">[Service Broker (英文)](https://docs.cloudfoundry.org/services/api.html) 提供一致的方式來佈建備份服務並繫結至應用程式。</span><span class="sxs-lookup"><span data-stu-id="ec177-128">[Service brokers](https://docs.cloudfoundry.org/services/api.html) offer a consistent way to provision and bind backing services to applications.</span></span> <span data-ttu-id="ec177-129">[Azure Service Broker (英文)](https://github.com/Azure/meta-azure-service-broker) 會透過此管道提供一些主要的 Azure 服務，包括 Azure 儲存體和 Azure SQL。</span><span class="sxs-lookup"><span data-stu-id="ec177-129">The [Azure service broker](https://github.com/Azure/meta-azure-service-broker) provides some of the key Azure services through this channel, including Azure storage and Azure SQL.</span></span>

<span data-ttu-id="ec177-130">如果您使用 Pivotal Cloud Foundry，您也可以從 Pivotal Network，[以圖格形式取得](https://docs.pivotal.io/azure-sb/installing.html)此 Service Broker。</span><span class="sxs-lookup"><span data-stu-id="ec177-130">If you are using Pivotal Cloud Foundry, the service broker is also [available as a tile](https://docs.pivotal.io/azure-sb/installing.html) from the Pivotal Network.</span></span>

## <a name="related-resources"></a><span data-ttu-id="ec177-131">相關資源</span><span class="sxs-lookup"><span data-stu-id="ec177-131">Related resources</span></span>

### <a name="visual-studio-team-services-plugin"></a><span data-ttu-id="ec177-132">Visual Studio Team Services 外掛程式</span><span class="sxs-lookup"><span data-stu-id="ec177-132">Visual Studio Team Services plugin</span></span>

<span data-ttu-id="ec177-133">Cloud Foundry 非常適合敏捷式軟體開發，包括使用持續整合 (CI) 和持續傳遞 (CD)。</span><span class="sxs-lookup"><span data-stu-id="ec177-133">Cloud Foundry is well suited to agile software development, including the use of continuous integration (CI) and continuous delivery (CD).</span></span> <span data-ttu-id="ec177-134">如果您使用 Visual Studio Team Services (VSTS) 來管理專案，並且想要設定目標為 Cloud Foundry 的 CI/CD 管線，則可使用 [VSTS Cloud Foundry 組建擴充功能 (英文)](https://marketplace.visualstudio.com/items?itemName=ms-vsts.cloud-foundry-build-extension)。</span><span class="sxs-lookup"><span data-stu-id="ec177-134">If you use Visual Studio Team Services (VSTS) to manage your projects and would like to set up a CI/CD pipeline targeting Cloud Foundry, you can use the [VSTS Cloud Foundry build extension](https://marketplace.visualstudio.com/items?itemName=ms-vsts.cloud-foundry-build-extension).</span></span> <span data-ttu-id="ec177-135">此外掛程式讓您能夠簡單地設定和自動化部署至 Cloud Foundry，而不論是在 Azure 或另一個環境中執行。</span><span class="sxs-lookup"><span data-stu-id="ec177-135">The plugin makes it simple to configure and automate deployments to Cloud Foundry, whether running in Azure or another environment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec177-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ec177-136">Next steps</span></span>

- [<span data-ttu-id="ec177-137">從 Azure Marketplace 部署 Pivotal Cloud Foundry (英文)</span><span class="sxs-lookup"><span data-stu-id="ec177-137">Deploy Pivotal Cloud Foundry from the Azure Marketplace</span></span>](https://azure.microsoft.com/en-us/marketplace/partners/pivotal/pivotal-cloud-foundryazure-pcf/)
- [<span data-ttu-id="ec177-138">在 Azure 將應用程式部署至 Cloud Foundry</span><span class="sxs-lookup"><span data-stu-id="ec177-138">Deploy an app to Cloud Foundry in Azure</span></span>](./cloudfoundry-deploy-your-first-app.md)