---
title: "使用 Azure 自動化管理 Azure RemoteApp | Microsoft Docs"
description: "了解如何使用 Azure 自動化服務管理 Azure RemoteApp。"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 589f01ef-f9c1-4e7b-a040-1b46862d3544
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: magoedte;csand
ms.openlocfilehash: 59ac11f153c0bd74a1106400dbbf5790968b657c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-remoteapp-using-azure-automation"></a><span data-ttu-id="bffd9-103">使用 Azure 自動化管理 Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="bffd9-103">Managing Azure RemoteApp using Azure Automation</span></span>
> [!IMPORTANT]
> <span data-ttu-id="bffd9-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="bffd9-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="bffd9-105">如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。</span><span class="sxs-lookup"><span data-stu-id="bffd9-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="bffd9-106">本指南將為您介紹 Azure 自動化服務，以及如何使用它來簡化 Azure RemoteApp 的管理。</span><span class="sxs-lookup"><span data-stu-id="bffd9-106">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of Azure RemoteApp.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="bffd9-107">什麼是 Azure 自動化？</span><span class="sxs-lookup"><span data-stu-id="bffd9-107">What is Azure Automation?</span></span>
<span data-ttu-id="bffd9-108">[Azure 自動化](../automation/automation-intro.md) 是一項 Azure 服務，可經由程序自動化簡化雲端管理。</span><span class="sxs-lookup"><span data-stu-id="bffd9-108">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="bffd9-109">使用 Azure 自動化，可以自動執行手動、經常重複、長時間執行及容易出錯的工作，以提高您的組織的可靠性、 效率和時間價值。</span><span class="sxs-lookup"><span data-stu-id="bffd9-109">Using Azure Automation, manual, frequently-repeated, long-running, and error-prone tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="bffd9-110">Azure 自動化提供高度可靠、高度可用的工作流程執行引擎，可加以調整以符合您的需求。</span><span class="sxs-lookup"><span data-stu-id="bffd9-110">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales to meet your needs.</span></span> <span data-ttu-id="bffd9-111">在 Azure 自動化中，可以手動方式、由協力廠商系統或依排定的間隔開始執行程序，讓工作只發生在必要時刻。</span><span class="sxs-lookup"><span data-stu-id="bffd9-111">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="bffd9-112">將您的雲端管理工作交由「Azure 自動化」自動執行，以減少營運負擔並釋出 IT 和開發維運人力，使其專注於能夠為企業創造價值的工作上。</span><span class="sxs-lookup"><span data-stu-id="bffd9-112">Reduce operational overhead and free up IT and DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-remoteapp"></a><span data-ttu-id="bffd9-113">Azure 自動化為何有助於管理 Azure RemoteApp？</span><span class="sxs-lookup"><span data-stu-id="bffd9-113">How can Azure Automation help manage Azure RemoteApp?</span></span>
<span data-ttu-id="bffd9-114">Azure RemoteApp 可透過 [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx)工具中提供的 PowerShell Cmdlet，在 Azure 自動化中受到管理。</span><span class="sxs-lookup"><span data-stu-id="bffd9-114">RemoteApp can be managed in Azure Automation by using the PowerShell cmdlets that are available in the [Azure PowerShell tools](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="bffd9-115">Azure 自動化的這些 RemoteApp PowerShell Cmdlet 都是內建的，以便您在服務內執行所有 RemoteApp 管理工作。</span><span class="sxs-lookup"><span data-stu-id="bffd9-115">Azure Automation has these RemoteApp PowerShell cmdlets available out of the box, so that you can perform all of your RemoteApp management tasks within the service.</span></span> <span data-ttu-id="bffd9-116">您也可以將 Azure 自動化中的這些 Cmdlet 與其他 Azure 服務的 Cmdlet 搭配，以透過 Azure 服務和協力廠商系統自動執行複雜的工作。</span><span class="sxs-lookup"><span data-stu-id="bffd9-116">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bffd9-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bffd9-117">Next steps</span></span>
<span data-ttu-id="bffd9-118">了解 Azure 自動化的基本概念以及如何用它來管理 Azure RemoteApp 之後，請參考下列連結，以深入了解 Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="bffd9-118">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure RemoteApp, follow these links to learn more about Azure Automation.</span></span>

* <span data-ttu-id="bffd9-119">請參閱 Azure 自動化 [入門指南](../automation/automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="bffd9-119">See the Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md)</span></span>

