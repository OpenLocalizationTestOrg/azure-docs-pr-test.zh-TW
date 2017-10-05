---
title: "使用 Azure 自動化管理 Azure Web 應用程式 | Microsoft Docs"
description: "了解如何使用 Azure 自動化服務管理 Web 應用程式。"
services: app-service\web, automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: c960a44f-f941-401d-afba-a4bc0f0394eb
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: magoedte
ms.openlocfilehash: a96332346747114620ee6ebd2a2d0c4417d4a213
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="managing-azure-web-app-using-azure-automation"></a><span data-ttu-id="a6186-103">使用 Azure 自動化管理 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a6186-103">Managing Azure Web App using Azure Automation</span></span>
<span data-ttu-id="a6186-104">本指南將為您介紹 Azure 自動化服務，以及如何使用它來簡化 Web 應用程式管理。</span><span class="sxs-lookup"><span data-stu-id="a6186-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of Azure Web App.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="a6186-105">什麼是 Azure 自動化？</span><span class="sxs-lookup"><span data-stu-id="a6186-105">What is Azure Automation?</span></span>
<span data-ttu-id="a6186-106">[Azure 自動化](../automation/automation-intro.md) 是一項 Azure 服務，可經由程序自動化簡化雲端管理。</span><span class="sxs-lookup"><span data-stu-id="a6186-106">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="a6186-107">使用 Azure 自動化，可以自動執行手動、重複、長時間執行及容易出錯的工作，以提高您的組織的可靠性、效率和時間價值。</span><span class="sxs-lookup"><span data-stu-id="a6186-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="a6186-108">Azure 自動化提供高度可靠、高度可用的工作流程執行引擎，可加以調整以符合您的需求。</span><span class="sxs-lookup"><span data-stu-id="a6186-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales to meet your needs.</span></span> <span data-ttu-id="a6186-109">在 Azure 自動化中，可以手動方式、由協力廠商系統或依排定的間隔開始執行程序，讓工作只發生在必要時刻。</span><span class="sxs-lookup"><span data-stu-id="a6186-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="a6186-110">將您的雲端管理工作交由「Azure 自動化」自動執行，以減少營運負擔並釋出 IT 和開發維運人力，使其專注於能夠為企業創造價值的工作上。</span><span class="sxs-lookup"><span data-stu-id="a6186-110">Reduce operational overhead and free up IT and DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-web-app"></a><span data-ttu-id="a6186-111">Azure 自動化為何有助於管理 Azure Web 應用程式？</span><span class="sxs-lookup"><span data-stu-id="a6186-111">How can Azure Automation help manage Azure Web App?</span></span>
<span data-ttu-id="a6186-112">Web 應用程式可透過 [Azure PowerShell 模組](/powershell/azureps-cmdlets-docs)中提供的 PowerShell Cmdlet，在 Azure 自動化中受到管理。</span><span class="sxs-lookup"><span data-stu-id="a6186-112">Web App can be managed in Azure Automation by using the PowerShell cmdlets that are available in the [Azure PowerShell modules](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="a6186-113">您可以 [在 Azure 自動化中安裝這些 Web 應用程式 PowerShell Cmdlet](https://azure.microsoft.com/blog/announcing-azure-resource-manager-support-azure-automation-runbooks/)，以便您能夠在服務內執行所有 Web 應用程式管理工作。</span><span class="sxs-lookup"><span data-stu-id="a6186-113">You can [install these Web App PowerShell cmdlets in Azure Automation](https://azure.microsoft.com/blog/announcing-azure-resource-manager-support-azure-automation-runbooks/), so that you can perform all of your Web App management tasks within the service.</span></span> <span data-ttu-id="a6186-114">您也可以在 Azure 自動化中將這些 Cmdlet 與其他 Azure 服務的 Cmdlet 配對，將跨 Azure 服務和協力廠商系統的複雜工作自動化。</span><span class="sxs-lookup"><span data-stu-id="a6186-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="a6186-115">以下是使用自動化來管理應用程式服務的一些範例 ︰</span><span class="sxs-lookup"><span data-stu-id="a6186-115">Here are some examples of managing App Services with Automation:</span></span>

* [<span data-ttu-id="a6186-116">用來管理 Web Apps 的指令碼</span><span class="sxs-lookup"><span data-stu-id="a6186-116">Scripts for managing Web Apps</span></span>](https://azure.microsoft.com/documentation/scripts/)

## <a name="next-steps"></a><span data-ttu-id="a6186-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a6186-117">Next steps</span></span>
<span data-ttu-id="a6186-118">了解 Azure 自動化的基本概念以及如何用它來管理 Azure Web 應用程式之後，請參考下列連結，以深入了解 Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="a6186-118">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure Web App, follow these links to learn more about Azure Automation.</span></span>

* <span data-ttu-id="a6186-119">請參閱 Azure 自動化 [入門指南](../automation/automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="a6186-119">See the Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md)</span></span>

