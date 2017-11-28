---
title: "aaaAzure 自動化 DSC 的概觀 |Microsoft 文件"
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
ms.openlocfilehash: 5b8e5104c7b5bed848c015ac26a8b7d1f5b24de9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-dsc-overview"></a><span data-ttu-id="882c2-104">Azure 自動化 DSC 概觀</span><span class="sxs-lookup"><span data-stu-id="882c2-104">Azure Automation DSC Overview</span></span>

<span data-ttu-id="882c2-105">Azure 自動化 DSC 是一項 Azure 服務，可讓您 toowrite、 管理及編譯 PowerShell 預期狀態設定 (DSC)[組態](https://msdn.microsoft.com/powershell/dsc/configurations)，匯入[DSC 資源](https://msdn.microsoft.com/powershell/dsc/resources)，並指派設定 tootarget 節點，所有 hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="882c2-105">Azure Automation DSC is an Azure service that allows you toowrite, manage, and compile PowerShell Desired State Configuration (DSC) [configurations](https://msdn.microsoft.com/powershell/dsc/configurations), import [DSC Resources](https://msdn.microsoft.com/powershell/dsc/resources), and assign configurations tootarget nodes, all in hello cloud.</span></span>

## <a name="why-use-azure-automation-dsc"></a><span data-ttu-id="882c2-106">為何使用 Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="882c2-106">Why use Azure Automation DSC</span></span>

<span data-ttu-id="882c2-107">Azure Automation DSC 提供在 Azure 外部使用 DSC 的數個優點。</span><span class="sxs-lookup"><span data-stu-id="882c2-107">Azure Automation DSC provides several advantages over using DSC outside of Azure.</span></span>

### <a name="built-in-pull-server"></a><span data-ttu-id="882c2-108">內建提取伺服器</span><span class="sxs-lookup"><span data-stu-id="882c2-108">Built-in pull server</span></span>

<span data-ttu-id="882c2-109">Azure 自動化提供[DSC 提取伺服器](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver)，目標節點會自動接收組態，符合 toohello 預期狀態，以及回報其相容性。</span><span class="sxs-lookup"><span data-stu-id="882c2-109">Azure Automation provides a [DSC pull server](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) so that target nodes automatically receive configurations, conform toohello desired state, and report back on their compliance.</span></span>
<span data-ttu-id="882c2-110">hello Azure 自動化中的內建的提取伺服器 hello 需要 tooset 排除設定和維護您自己的提取伺服器。</span><span class="sxs-lookup"><span data-stu-id="882c2-110">hello built-in pull server in Azure Automation eliminates hello need tooset up and maintain your own pull server.</span></span>
<span data-ttu-id="882c2-111">Azure 自動化可鎖定目標虛擬機器或實體 Windows 或 Linux 機器，hello 雲端或內部部署中。</span><span class="sxs-lookup"><span data-stu-id="882c2-111">Azure Automation can target virtual or physical Windows or Linux machines, in hello cloud or on-premises.</span></span>

### <a name="management-of-all-your-dsc-artifacts"></a><span data-ttu-id="882c2-112">所有 DSC 構件的管理</span><span class="sxs-lookup"><span data-stu-id="882c2-112">Management of all your DSC artifacts</span></span>

<span data-ttu-id="882c2-113">Azure Automation DSC 讓太 hello 相同的管理層[PowerShell Desired State Configuration](https://msdn.microsoft.com/powershell/dsc/overview) Azure 自動化提供 PowerShell 指令碼處理。</span><span class="sxs-lookup"><span data-stu-id="882c2-113">Azure Automation DSC brings hello same management layer too[PowerShell Desired State Configuration](https://msdn.microsoft.com/powershell/dsc/overview) as Azure Automation offers for PowerShell scripting.</span></span>

<span data-ttu-id="882c2-114">從 hello Azure 入口網站或 PowerShell，您可以管理所有您 DSC 設定、 資源和目標節點。</span><span class="sxs-lookup"><span data-stu-id="882c2-114">From hello Azure portal, or from PowerShell, you can manage all your DSC configurations, resources, and target nodes.</span></span>

![Hello Azure 自動化刀鋒視窗的螢幕擷取畫面](./media/automation-dsc-overview/azure-automation-blade.png)

### <a name="import-reporting-data-into-log-analytics"></a><span data-ttu-id="882c2-116">將報告資料匯入至 Log Analytics</span><span class="sxs-lookup"><span data-stu-id="882c2-116">Import reporting data into Log Analytics</span></span>

<span data-ttu-id="882c2-117">使用 Azure 自動化 DSC 傳送詳細報告狀態資料 toohello 內建的提取伺服器所管理的節點。</span><span class="sxs-lookup"><span data-stu-id="882c2-117">Nodes that are managed with Azure Automation DSC send detailed reporting status data toohello built-in pull server.</span></span>
<span data-ttu-id="882c2-118">您可以設定 Azure 自動化 DSC toosend 此資料 tooyour Microsoft Operations Management Suite (OMS) 的記錄分析工作區。</span><span class="sxs-lookup"><span data-stu-id="882c2-118">You can configure Azure Automation DSC toosend this data tooyour Microsoft Operations Management Suite (OMS) Log Analytics workspace.</span></span>
<span data-ttu-id="882c2-119">如何 toosend DSC 狀態資料 tooyour 記錄分析工作區中，請參閱的 toolearn[向前復原 Azure 自動化 DSC 報告資料 tooOMS 記錄分析](automation-dsc-diagnostics.md)。</span><span class="sxs-lookup"><span data-stu-id="882c2-119">toolearn how toosend DSC status data tooyour Log Analytics workspace, see [Forward Azure Automation DSC reporting data tooOMS Log Analytics](automation-dsc-diagnostics.md).</span></span>

## <a name="introduction-video"></a><span data-ttu-id="882c2-120">簡介影片</span><span class="sxs-lookup"><span data-stu-id="882c2-120">Introduction video</span></span>

<span data-ttu-id="882c2-121">偏好觀看 tooreading 嗎？</span><span class="sxs-lookup"><span data-stu-id="882c2-121">Prefer watching tooreading?</span></span> <span data-ttu-id="882c2-122">看看下列影片從 2015 年首次宣佈 Azure Automation DSC 的 hello。</span><span class="sxs-lookup"><span data-stu-id="882c2-122">Have a look at hello following video from May 2015, when Azure Automation DSC was first announced.</span></span>

>[!NOTE]
><span data-ttu-id="882c2-123">雖然正確 hello 概念和生命週期，這段影片中所述，Azure Automation DSC 已在這段影片錄製，因為許多前進。</span><span class="sxs-lookup"><span data-stu-id="882c2-123">While hello concepts and life cycle discussed in this video are correct, Azure Automation DSC has progressed a lot since this video was recorded.</span></span>
><span data-ttu-id="882c2-124">現在已上市，hello Azure 入口網站中具備更廣泛的 UI，而且支援許多其他功能。</span><span class="sxs-lookup"><span data-stu-id="882c2-124">It is now generally available, has a much more extensive UI in hello Azure portal, and supports many additional capabilities.</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3467/player]

## <a name="next-steps"></a><span data-ttu-id="882c2-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="882c2-125">Next steps</span></span>

* <span data-ttu-id="882c2-126">toolearn 如何 tooonboard 節點 toobe 所管理的 Azure 自動化 DSC，請參閱[供 Azure Automation DSC 來管理登入機器](automation-dsc-onboarding.md)</span><span class="sxs-lookup"><span data-stu-id="882c2-126">toolearn how tooonboard nodes toobe managed with Azure Automation DSC, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md)</span></span>
* <span data-ttu-id="882c2-127">請參閱 < 開始使用 Azure 自動化 DSC tooget[開始使用 Azure 自動化 DSC](automation-dsc-getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="882c2-127">tooget started using Azure Automation DSC, see [Getting started with Azure Automation DSC](automation-dsc-getting-started.md)</span></span>
* <span data-ttu-id="882c2-128">toolearn 需編譯 DSC 設定，以指派 tootarget 節點，請參閱[編譯在 Azure Automation DSC 設定](automation-dsc-compile.md)</span><span class="sxs-lookup"><span data-stu-id="882c2-128">toolearn about compiling DSC configurations so that you can assign them tootarget nodes, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md)</span></span>
* <span data-ttu-id="882c2-129">如需 Azure Automation DSC 的 PowerShell Cmdlet 參考，請參閱 [Azure Automation DSC Cmdlet](/powershell/module/azurerm.automation/#automation)。</span><span class="sxs-lookup"><span data-stu-id="882c2-129">For PowerShell cmdlet reference for Azure Automation DSC, see [Azure Automation DSC cmdlets](/powershell/module/azurerm.automation/#automation)</span></span>
* <span data-ttu-id="882c2-130">如需定價資訊，請參閱 [Azure Automation DSC 定價](https://azure.microsoft.com/pricing/details/automation/)。</span><span class="sxs-lookup"><span data-stu-id="882c2-130">For pricing information, see [Azure Automation DSC pricing](https://azure.microsoft.com/pricing/details/automation/)</span></span>
* <span data-ttu-id="882c2-131">toosee 示範如何使用 Azure 自動化 DSC 在連續部署管線中，請參閱[連續部署 tooIaaS Vm 使用 Azure 自動化 DSC 和 Chocolatey](automation-dsc-cd-chocolatey.md)</span><span class="sxs-lookup"><span data-stu-id="882c2-131">toosee an example of using Azure Automation DSC in a continuous deployment pipeline, see  [Continuous Deployment tooIaaS VMs Using Azure Automation DSC and Chocolatey](automation-dsc-cd-chocolatey.md)</span></span>
