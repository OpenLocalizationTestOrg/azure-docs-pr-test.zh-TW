---
title: "使用 Azure 自動化管理 Azure API 管理"
description: "了解如何使用 Azure 自動化服務來管理 Azure API 管理。"
services: api-management, automation
documentationcenter: 
author: csand-msft
manager: eamono
editor: 
ms.assetid: 2e53c9af-f738-47f8-b1b6-593050a7c51b
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 73a1135482b88ea7c228bc8b228d47c57b2e70a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-api-management-using-azure-automation"></a><span data-ttu-id="e4a12-103">使用 Azure 自動化管理 Azure API 管理</span><span class="sxs-lookup"><span data-stu-id="e4a12-103">Managing Azure API Management using Azure Automation</span></span>
<span data-ttu-id="e4a12-104">本指南將為您介紹 Azure 自動化服務，以及如何使用它來簡化 Azure API 管理。</span><span class="sxs-lookup"><span data-stu-id="e4a12-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of Azure API Management.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="e4a12-105">什麼是 Azure 自動化？</span><span class="sxs-lookup"><span data-stu-id="e4a12-105">What is Azure Automation?</span></span>
<span data-ttu-id="e4a12-106">[Azure 自動化](https://azure.microsoft.com/services/automation/) 是一項 Azure 服務，可經由程序自動化簡化雲端管理。</span><span class="sxs-lookup"><span data-stu-id="e4a12-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="e4a12-107">使用 Azure 自動化，可以自動執行手動、重複、長時間執行及容易出錯的工作，以提高您的組織的可靠性、效率和時間價值。</span><span class="sxs-lookup"><span data-stu-id="e4a12-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="e4a12-108">Azure 自動化提供高度可靠、高度可用的工作流程執行引擎，可加以調整以符合您的需求。</span><span class="sxs-lookup"><span data-stu-id="e4a12-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales to meet your needs.</span></span> <span data-ttu-id="e4a12-109">在 Azure 自動化中，可以手動方式、由協力廠商系統或依排定的間隔開始執行程序，讓工作只發生在必要時刻。</span><span class="sxs-lookup"><span data-stu-id="e4a12-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="e4a12-110">將您的雲端管理工作交由「Azure 自動化」自動執行，以減少營運負擔並釋出 IT 和開發維運人力，使其專注於能夠為企業創造價值的工作上。</span><span class="sxs-lookup"><span data-stu-id="e4a12-110">Reduce operational overhead and free up IT and DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-api-management"></a><span data-ttu-id="e4a12-111">Azure 自動化如何協助管理 Azure API 管理？</span><span class="sxs-lookup"><span data-stu-id="e4a12-111">How can Azure Automation help manage Azure API Management?</span></span>
<span data-ttu-id="e4a12-112">您可以在 Azure 自動化中利用 [適用於 API 管理 API 的 Windows PowerShell Cmdlet](https://azure.microsoft.com/updates/full-set-of-windows-powershell-cmdlets-for-azure-api-management-api/)來管理「API 管理」。</span><span class="sxs-lookup"><span data-stu-id="e4a12-112">API Management can be managed in Azure Automation by using the [Windows PowerShell cmdlets for Azure API Management API](https://azure.microsoft.com/updates/full-set-of-windows-powershell-cmdlets-for-azure-api-management-api/).</span></span> <span data-ttu-id="e4a12-113">在 Azure 自動化內，您可以利用 Cmdlet 撰寫 PowerShell 工作流程指令碼，以執行許多 API 管理工作。</span><span class="sxs-lookup"><span data-stu-id="e4a12-113">Within Azure Automation you can write PowerShell workflow scripts to perform many of your API Management tasks using the cmdlets.</span></span> <span data-ttu-id="e4a12-114">您也可以將 Azure 自動化中的這些 Cmdlet 與其他 Azure 服務的 Cmdlet 搭配，以透過 Azure 服務和協力廠商系統自動執行複雜的工作。</span><span class="sxs-lookup"><span data-stu-id="e4a12-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="e4a12-115">以下是幾個使用 API 管理搭配自動化的範例︰</span><span class="sxs-lookup"><span data-stu-id="e4a12-115">Here are some examples of using API Management with Automation:</span></span>

* [<span data-ttu-id="e4a12-116">Azure API 管理 – 使用 PowerShell 進行備份和還原</span><span class="sxs-lookup"><span data-stu-id="e4a12-116">Azure API Management – Using PowerShell for backup and restore</span></span>](https://blogs.msdn.microsoft.com/katriend/2015/10/02/azure-api-management-using-powershell-for-backup-and-restore/)

## <a name="next-steps"></a><span data-ttu-id="e4a12-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e4a12-117">Next Steps</span></span>
<span data-ttu-id="e4a12-118">了解 Azure 自動化的基本概念以及如何用它來管理 Azure API 管理之後，請參考下列連結以深入了解。</span><span class="sxs-lookup"><span data-stu-id="e4a12-118">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure API Management, follow these links to learn more.</span></span>

* <span data-ttu-id="e4a12-119">請參閱 Azure 自動化 [快速入門教學課程](../automation/automation-first-runbook-graphical.md)。</span><span class="sxs-lookup"><span data-stu-id="e4a12-119">See the Azure Automation [getting started tutorial](../automation/automation-first-runbook-graphical.md).</span></span>

