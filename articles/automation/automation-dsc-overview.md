---
title: "Azure Automation DSC 概觀 | Microsoft Docs"
description: "Azure 自動化期望狀態組態 (DSC)、其條款和已知問題的概觀"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: "powershell dsc, 需要的狀態組態, powershell dsc azure"
ms.assetid: fd40cb68-c1a6-48c3-bba2-710b607d1555
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 06/15/2017
ms.author: eslesar
ms.openlocfilehash: 468321fa6863d78bc0d179fbe5c2ed6195040d50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-dsc-overview"></a><span data-ttu-id="98c70-104">Azure 自動化 DSC 概觀</span><span class="sxs-lookup"><span data-stu-id="98c70-104">Azure Automation DSC Overview</span></span>

<span data-ttu-id="98c70-105">Azure Automation DSC 是一種 Azure 服務，可讓您撰寫、管理和編譯 PowerShell Desired State Configuration (DSC) [設定](https://msdn.microsoft.com/powershell/dsc/configurations)、匯入 [DSC 資源](https://msdn.microsoft.com/powershell/dsc/resources)，以及將設定指派給目標節點，而這些作業都是在雲端中進行。</span><span class="sxs-lookup"><span data-stu-id="98c70-105">Azure Automation DSC is an Azure service that allows you to write, manage, and compile PowerShell Desired State Configuration (DSC) [configurations](https://msdn.microsoft.com/powershell/dsc/configurations), import [DSC Resources](https://msdn.microsoft.com/powershell/dsc/resources), and assign configurations to target nodes, all in the cloud.</span></span>

## <a name="why-use-azure-automation-dsc"></a><span data-ttu-id="98c70-106">為何使用 Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="98c70-106">Why use Azure Automation DSC</span></span>

<span data-ttu-id="98c70-107">Azure Automation DSC 提供在 Azure 外部使用 DSC 的數個優點。</span><span class="sxs-lookup"><span data-stu-id="98c70-107">Azure Automation DSC provides several advantages over using DSC outside of Azure.</span></span>

### <a name="built-in-pull-server"></a><span data-ttu-id="98c70-108">內建提取伺服器</span><span class="sxs-lookup"><span data-stu-id="98c70-108">Built-in pull server</span></span>

<span data-ttu-id="98c70-109">Azure 自動化提供 [DSC 提取伺服器](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver)，因此目標節點會自動接收設定、符合期望狀態，並回報其相容性。</span><span class="sxs-lookup"><span data-stu-id="98c70-109">Azure Automation provides a [DSC pull server](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) so that target nodes automatically receive configurations, conform to the desired state, and report back on their compliance.</span></span>
<span data-ttu-id="98c70-110">Azure 自動化中的內建提取伺服器可讓您不需要設定和維護自己的提取伺服器。</span><span class="sxs-lookup"><span data-stu-id="98c70-110">The built-in pull server in Azure Automation eliminates the need to set up and maintain your own pull server.</span></span>
<span data-ttu-id="98c70-111">Azure 自動化會以位於雲端或內部部署的虛擬或實體 Windows 或 Linux 機器為目標。</span><span class="sxs-lookup"><span data-stu-id="98c70-111">Azure Automation can target virtual or physical Windows or Linux machines, in the cloud or on-premises.</span></span>

### <a name="management-of-all-your-dsc-artifacts"></a><span data-ttu-id="98c70-112">所有 DSC 構件的管理</span><span class="sxs-lookup"><span data-stu-id="98c70-112">Management of all your DSC artifacts</span></span>

<span data-ttu-id="98c70-113">Azure Automation DSC 為 [PowerShell Desired State Configuration](https://msdn.microsoft.com/powershell/dsc/overview) 帶來與 Azure 自動化提供的 PowerShell 指令碼相同的管理層。</span><span class="sxs-lookup"><span data-stu-id="98c70-113">Azure Automation DSC brings the same management layer to [PowerShell Desired State Configuration](https://msdn.microsoft.com/powershell/dsc/overview) as Azure Automation offers for PowerShell scripting.</span></span>

<span data-ttu-id="98c70-114">從 Azure 入口網站或 PowerShell 中，您可以管理所有 DSC 設定、資源和目標節點。</span><span class="sxs-lookup"><span data-stu-id="98c70-114">From the Azure portal, or from PowerShell, you can manage all your DSC configurations, resources, and target nodes.</span></span>

![Azure 自動化刀鋒視窗的螢幕擷取畫面](./media/automation-dsc-overview/azure-automation-blade.png)

### <a name="import-reporting-data-into-log-analytics"></a><span data-ttu-id="98c70-116">將報告資料匯入至 Log Analytics</span><span class="sxs-lookup"><span data-stu-id="98c70-116">Import reporting data into Log Analytics</span></span>

<span data-ttu-id="98c70-117">使用 Azure Automation DSC 所管理的節點會將詳細報告狀態資料傳送至內建提取伺服器。</span><span class="sxs-lookup"><span data-stu-id="98c70-117">Nodes that are managed with Azure Automation DSC send detailed reporting status data to the built-in pull server.</span></span>
<span data-ttu-id="98c70-118">您可以設定 Azure Automation DSC，將此資料傳送至 Microsoft Operations Management Suite (OMS) Log Analytics 工作區。</span><span class="sxs-lookup"><span data-stu-id="98c70-118">You can configure Azure Automation DSC to send this data to your Microsoft Operations Management Suite (OMS) Log Analytics workspace.</span></span>
<span data-ttu-id="98c70-119">若要了解如何將 DSC 狀態資料傳送至 Log Analytics 工作區，請參閱[將 Azure Automation DSC 報告資料轉送到 OMS Log Analytics](automation-dsc-diagnostics.md)。</span><span class="sxs-lookup"><span data-stu-id="98c70-119">To learn how to send DSC status data to your Log Analytics workspace, see [Forward Azure Automation DSC reporting data to OMS Log Analytics](automation-dsc-diagnostics.md).</span></span>

## <a name="introduction-video"></a><span data-ttu-id="98c70-120">簡介影片</span><span class="sxs-lookup"><span data-stu-id="98c70-120">Introduction video</span></span>

<span data-ttu-id="98c70-121">寧可觀賞也不要閱讀？</span><span class="sxs-lookup"><span data-stu-id="98c70-121">Prefer watching to reading?</span></span> <span data-ttu-id="98c70-122">看看下列 2015 年 5 月 Azure 自動化 DSC 推出當時的影片。</span><span class="sxs-lookup"><span data-stu-id="98c70-122">Have a look at the following video from May 2015, when Azure Automation DSC was first announced.</span></span>

>[!NOTE]
><span data-ttu-id="98c70-123">雖然這段影片中所討論的概念和週期都是正確的，但是 Azure Automation DSC 自從錄製這段影片之後已經進步許多。</span><span class="sxs-lookup"><span data-stu-id="98c70-123">While the concepts and life cycle discussed in this video are correct, Azure Automation DSC has progressed a lot since this video was recorded.</span></span>
><span data-ttu-id="98c70-124">它現在已正式發行，在 Azure 入口網站中具有更豐富的 UI，並支援額外的功能。</span><span class="sxs-lookup"><span data-stu-id="98c70-124">It is now generally available, has a much more extensive UI in the Azure portal, and supports many additional capabilities.</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3467/player]

## <a name="next-steps"></a><span data-ttu-id="98c70-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="98c70-125">Next steps</span></span>

* <span data-ttu-id="98c70-126">若要了解如何將以 Azure Automation DSC 管理的節點上架，請參閱[上架由 Azure Automation DSC 管理的機器](automation-dsc-onboarding.md)。</span><span class="sxs-lookup"><span data-stu-id="98c70-126">To learn how to onboard nodes to be managed with Azure Automation DSC, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md)</span></span>
* <span data-ttu-id="98c70-127">若要開始使用 Azure Automation DSC，請參閱[開始使用 Azure Automation DSC](automation-dsc-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="98c70-127">To get started using Azure Automation DSC, see [Getting started with Azure Automation DSC](automation-dsc-getting-started.md)</span></span>
* <span data-ttu-id="98c70-128">若要了解如何編譯 DSC 設定，以將它們指派給目標節點，請參閱[編譯 Azure Automation DSC 中的設定](automation-dsc-compile.md)。</span><span class="sxs-lookup"><span data-stu-id="98c70-128">To learn about compiling DSC configurations so that you can assign them to target nodes, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md)</span></span>
* <span data-ttu-id="98c70-129">如需 Azure Automation DSC 的 PowerShell Cmdlet 參考，請參閱 [Azure Automation DSC Cmdlet](/powershell/module/azurerm.automation/#automation)。</span><span class="sxs-lookup"><span data-stu-id="98c70-129">For PowerShell cmdlet reference for Azure Automation DSC, see [Azure Automation DSC cmdlets](/powershell/module/azurerm.automation/#automation)</span></span>
* <span data-ttu-id="98c70-130">如需定價資訊，請參閱 [Azure Automation DSC 定價](https://azure.microsoft.com/pricing/details/automation/)。</span><span class="sxs-lookup"><span data-stu-id="98c70-130">For pricing information, see [Azure Automation DSC pricing](https://azure.microsoft.com/pricing/details/automation/)</span></span>
* <span data-ttu-id="98c70-131">若要查看 Azure 自動化 DSC 使用連續部署管線中的範例，請參閱[IaaS Vm 使用 Azure 自動化 DSC 和 Chocolatey 連續部署](automation-dsc-cd-chocolatey.md)</span><span class="sxs-lookup"><span data-stu-id="98c70-131">To see an example of using Azure Automation DSC in a continuous deployment pipeline, see  [Continuous Deployment to IaaS VMs Using Azure Automation DSC and Chocolatey](automation-dsc-cd-chocolatey.md)</span></span>