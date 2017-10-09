---
title: "開始使用 Microsoft Azure 上的雲端 Foundry aaaGetting |Microsoft 文件"
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
ms.openlocfilehash: 56300d5a0a75b5a9f46145a49ed3f5daa774375a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-foundry-on-azure"></a><span data-ttu-id="9f817-103">Azure 上的 Cloud Foundry</span><span class="sxs-lookup"><span data-stu-id="9f817-103">Cloud Foundry on Azure</span></span>

<span data-ttu-id="9f817-104">Cloud Foundry 是開放原始碼的平台即服務 (PaaS)，可用於建置、部署和操作以各種不同語言和架構開發的 12-factor 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9f817-104">Cloud Foundry is an open-source platform-as-a-service (PaaS) for building, deploying, and operating 12-factor applications developed in various languages and frameworks.</span></span> <span data-ttu-id="9f817-105">本文件說明您的 Azure 和如何開始執行雲端 Foundry hello 選項。</span><span class="sxs-lookup"><span data-stu-id="9f817-105">This document describes hello options you have for running Cloud Foundry on Azure and how you can get started.</span></span>

## <a name="cloud-foundry-offerings"></a><span data-ttu-id="9f817-106">Cloud Foundry 供應項目</span><span class="sxs-lookup"><span data-stu-id="9f817-106">Cloud Foundry offerings</span></span>

<span data-ttu-id="9f817-107">有兩種形式的雲端 Foundry 在 Azure 上的可用 toorun： 開放原始碼雲端 Foundry (OSS CF) 和關鍵雲端 Foundry (PCF)。</span><span class="sxs-lookup"><span data-stu-id="9f817-107">There are two forms of Cloud Foundry available toorun on Azure: open-source Cloud Foundry (OSS CF) and Pivotal Cloud Foundry (PCF).</span></span> <span data-ttu-id="9f817-108">OS CF 是完全[開放原始碼](https://github.com/cloudfoundry)hello 雲端 Foundry Foundation 管理雲端 Foundry 的版本。</span><span class="sxs-lookup"><span data-stu-id="9f817-108">OSS CF is an entirely [open-source](https://github.com/cloudfoundry) version of Cloud Foundry managed by hello Cloud Foundry Foundation.</span></span> <span data-ttu-id="9f817-109">關鍵雲端 Foundry 是雲端 Foundry 關鍵軟體 inc.提供的企業分佈我們看看其中一些 hello hello 兩個供應項目之間的差異。</span><span class="sxs-lookup"><span data-stu-id="9f817-109">Pivotal Cloud Foundry is an enterprise distribution of Cloud Foundry from Pivotal Software Inc. We look at some of hello differences between hello two offerings.</span></span>

### <a name="open-source-cloud-foundry"></a><span data-ttu-id="9f817-110">開放原始碼的 Cloud Foundry</span><span class="sxs-lookup"><span data-stu-id="9f817-110">Open-source Cloud Foundry</span></span>

<span data-ttu-id="9f817-111">您可以部署在 Azure 上的 OSS 雲端 Foundry 第一次部署 BOSH 導向器，然後再部署雲端 Foundry，使用 hello [GitHub 上所提供的指示](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/blob/master/docs/guidance.md)。</span><span class="sxs-lookup"><span data-stu-id="9f817-111">You can deploy OSS Cloud Foundry on Azure by first deploying a BOSH director and then deploying Cloud Foundry, using hello [instructions provided on GitHub](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/blob/master/docs/guidance.md).</span></span> <span data-ttu-id="9f817-112">進一步了解使用 OS CF toolearn 看到 hello[文件](https://docs.cloudfoundry.org/)hello 雲端 Foundry Foundation 所提供。</span><span class="sxs-lookup"><span data-stu-id="9f817-112">toolearn more about using OSS CF, see hello [documentation](https://docs.cloudfoundry.org/) provided by hello Cloud Foundry Foundation.</span></span>

<span data-ttu-id="9f817-113">Microsoft 可透過下列社群管道 hello OSS CF 最佳方式支援：</span><span class="sxs-lookup"><span data-stu-id="9f817-113">Microsoft provides best-effort support for OSS CF through hello following community channels:</span></span>

- #<a name="bosh-azure-cpi-channel-on-cloud-foundry-slackhttpsslackcloudfoundryorg"></a><span data-ttu-id="9f817-114">[Cloud Foundry Slack (英文)](https://slack.cloudfoundry.org/) 上的 bosh-azure-cpi 管道</span><span class="sxs-lookup"><span data-stu-id="9f817-114">bosh-azure-cpi channel on [Cloud Foundry Slack](https://slack.cloudfoundry.org/)</span></span>
- [<span data-ttu-id="9f817-115">cf-bosh 郵寄清單 (英文)</span><span class="sxs-lookup"><span data-stu-id="9f817-115">cf-bosh mailing list</span></span>](https://lists.cloudfoundry.org/pipermail/cf-bosh)
- <span data-ttu-id="9f817-116">Hello 的 GitHub 問題[CPI](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/issues)和[service broker](https://github.com/Azure/meta-azure-service-broker/issues)</span><span class="sxs-lookup"><span data-stu-id="9f817-116">GitHub issues for hello [CPI](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/issues) and [service broker](https://github.com/Azure/meta-azure-service-broker/issues)</span></span>

>[!NOTE]
> <span data-ttu-id="9f817-117">hello Azure 資源，例如您用來執行雲端 Foundry hello 虛擬機器的支援層級根據您的 Azure 支援合約。</span><span class="sxs-lookup"><span data-stu-id="9f817-117">hello level of support for your Azure resources, such as hello virtual machines where you run Cloud Foundry, is based on your Azure support agreement.</span></span> <span data-ttu-id="9f817-118">最大速率社群支援只適用於 toohello 雲端 Foundry 特有的元件。</span><span class="sxs-lookup"><span data-stu-id="9f817-118">Best-effort community support only applies toohello Cloud Foundry-specific components.</span></span>

### <a name="pivotal-cloud-foundry"></a><span data-ttu-id="9f817-119">Pivotal Cloud Foundry</span><span class="sxs-lookup"><span data-stu-id="9f817-119">Pivotal Cloud Foundry</span></span>

<span data-ttu-id="9f817-120">關鍵雲端 Foundry 包含 hello hello OSS 分佈，以及一組專屬的管理工具和企業支援為相同的核心平台。</span><span class="sxs-lookup"><span data-stu-id="9f817-120">Pivotal Cloud Foundry includes hello same core platform as hello OSS distribution, along with a set of proprietary management tools and enterprise support.</span></span> <span data-ttu-id="9f817-121">toorun PCF 在 Azure 上，您必須取得授權的 Pivotal。</span><span class="sxs-lookup"><span data-stu-id="9f817-121">toorun PCF on Azure, you must acquire a license from Pivotal.</span></span> <span data-ttu-id="9f817-122">hello Azure marketplace hello PCF 提供項目包含的 90 天試用版授權。</span><span class="sxs-lookup"><span data-stu-id="9f817-122">hello PCF offer from hello Azure marketplace includes a 90-day trial license.</span></span>

<span data-ttu-id="9f817-123">hello 工具包括[關鍵的 Operations Manager](http://docs.pivotal.io/pivotalcf/customizing/)，web 應用程式，可簡化部署及管理的雲端 Foundry foundation 和[關鍵應用程式管理員](https://docs.pivotal.io/pivotalcf/console/)，來管理 web 應用程式使用者和應用程式。</span><span class="sxs-lookup"><span data-stu-id="9f817-123">hello tools include [Pivotal Operations Manager](http://docs.pivotal.io/pivotalcf/customizing/), a web application that simplifies deployment and management of a Cloud Foundry foundation, and [Pivotal Apps Manager](https://docs.pivotal.io/pivotalcf/console/), a web application for managing users and applications.</span></span>

<span data-ttu-id="9f817-124">除了上述的 OSS CF 列出 toohello 支援管道，PCF 授權允許您 toocontact Pivotal 支援。</span><span class="sxs-lookup"><span data-stu-id="9f817-124">In addition toohello support channels listed for OSS CF above, a PCF license entitles you toocontact Pivotal for support.</span></span> <span data-ttu-id="9f817-125">Microsoft Pivotal 也啟用了支援工作流程可讓您 toocontact 協助任一個合作對象和一定您正確路由，根據 hello 問題的所在位置的問題。</span><span class="sxs-lookup"><span data-stu-id="9f817-125">Microsoft and Pivotal have also enabled support workflows that allow you toocontact either party for assistance and have your inquiry routed appropriately depending on where hello issue lies.</span></span>

## <a name="azure-service-broker"></a><span data-ttu-id="9f817-126">Azure Service Broker</span><span class="sxs-lookup"><span data-stu-id="9f817-126">Azure Service Broker</span></span>

<span data-ttu-id="9f817-127">雲端 Foundry 鼓勵 hello ["12 個因素 app"](https://12factor.net/)升級清楚分隔無狀態應用程式處理序與備份服務的可設定狀態的方法。</span><span class="sxs-lookup"><span data-stu-id="9f817-127">Cloud Foundry encourages hello ["twelve-factor app"](https://12factor.net/) methodology, which promotes a clean separation of stateless application processes and stateful backing services.</span></span> <span data-ttu-id="9f817-128">[Service broker](https://docs.cloudfoundry.org/services/api.html)提供一致的方式 tooprovision 並繫結支援服務 tooapplications。</span><span class="sxs-lookup"><span data-stu-id="9f817-128">[Service brokers](https://docs.cloudfoundry.org/services/api.html) offer a consistent way tooprovision and bind backing services tooapplications.</span></span> <span data-ttu-id="9f817-129">hello [Azure 服務 broker](https://github.com/Azure/meta-azure-service-broker)提供了一些 hello 透過此通道，包括 Azure 儲存體和 Azure SQL 主要 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="9f817-129">hello [Azure service broker](https://github.com/Azure/meta-azure-service-broker) provides some of hello key Azure services through this channel, including Azure storage and Azure SQL.</span></span>

<span data-ttu-id="9f817-130">如果您使用關鍵雲端 Foundry，hello service broker 也會[可用為方塊](https://docs.pivotal.io/azure-sb/installing.html)從 hello 關鍵的網路。</span><span class="sxs-lookup"><span data-stu-id="9f817-130">If you are using Pivotal Cloud Foundry, hello service broker is also [available as a tile](https://docs.pivotal.io/azure-sb/installing.html) from hello Pivotal Network.</span></span>

## <a name="related-resources"></a><span data-ttu-id="9f817-131">相關資源</span><span class="sxs-lookup"><span data-stu-id="9f817-131">Related resources</span></span>

### <a name="visual-studio-team-services-plugin"></a><span data-ttu-id="9f817-132">Visual Studio Team Services 外掛程式</span><span class="sxs-lookup"><span data-stu-id="9f817-132">Visual Studio Team Services plugin</span></span>

<span data-ttu-id="9f817-133">雲端 Foundry 是很適合的 tooagile 軟體開發，包含 hello 使用持續整合 (CI) 和持續傳遞 (CD)。</span><span class="sxs-lookup"><span data-stu-id="9f817-133">Cloud Foundry is well suited tooagile software development, including hello use of continuous integration (CI) and continuous delivery (CD).</span></span> <span data-ttu-id="9f817-134">如果您使用 Visual Studio Team Services (VSTS) toomanage 您的專案，並希望 tooset 總目標雲端 Foundry CI/CD 管線，您可以使用 hello [VSTS 雲端 Foundry 建置延伸模組](https://marketplace.visualstudio.com/items?itemName=ms-vsts.cloud-foundry-build-extension)。</span><span class="sxs-lookup"><span data-stu-id="9f817-134">If you use Visual Studio Team Services (VSTS) toomanage your projects and would like tooset up a CI/CD pipeline targeting Cloud Foundry, you can use hello [VSTS Cloud Foundry build extension](https://marketplace.visualstudio.com/items?itemName=ms-vsts.cloud-foundry-build-extension).</span></span> <span data-ttu-id="9f817-135">hello 外掛程式可讓簡單 tooconfigure 並自動化部署 tooCloud Foundry，是否在 Azure 或另一個執行環境。</span><span class="sxs-lookup"><span data-stu-id="9f817-135">hello plugin makes it simple tooconfigure and automate deployments tooCloud Foundry, whether running in Azure or another environment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9f817-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9f817-136">Next steps</span></span>

- [<span data-ttu-id="9f817-137">從 hello Azure Marketplace 中部署關鍵雲端 Foundry</span><span class="sxs-lookup"><span data-stu-id="9f817-137">Deploy Pivotal Cloud Foundry from hello Azure Marketplace</span></span>](https://azure.microsoft.com/en-us/marketplace/partners/pivotal/pivotal-cloud-foundryazure-pcf/)
- [<span data-ttu-id="9f817-138">部署應用程式 tooCloud Foundry 在 Azure 中</span><span class="sxs-lookup"><span data-stu-id="9f817-138">Deploy an app tooCloud Foundry in Azure</span></span>](./cloudfoundry-deploy-your-first-app.md)
