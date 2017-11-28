---
title: "aaaManage 使用 Azure 自動化的 Azure API 管理"
description: "深入了解如何 hello Azure 自動化服務可以使用的 toomanage Azure API 管理。"
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
ms.openlocfilehash: 05b8e3cad786fa701feb88f7b6d9629f16686d15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-api-management-using-azure-automation"></a><span data-ttu-id="3ac16-103">使用 Azure 自動化管理 Azure API 管理</span><span class="sxs-lookup"><span data-stu-id="3ac16-103">Managing Azure API Management using Azure Automation</span></span>
<span data-ttu-id="3ac16-104">本指南將介紹 toohello Azure 自動化服務，而且您可以如何使用的 toosimplify 管理的 Azure API 管理。</span><span class="sxs-lookup"><span data-stu-id="3ac16-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of Azure API Management.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="3ac16-105">什麼是 Azure 自動化？</span><span class="sxs-lookup"><span data-stu-id="3ac16-105">What is Azure Automation?</span></span>
<span data-ttu-id="3ac16-106">[Azure 自動化](https://azure.microsoft.com/services/automation/) 是一項 Azure 服務，可經由程序自動化簡化雲端管理。</span><span class="sxs-lookup"><span data-stu-id="3ac16-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="3ac16-107">使用 Azure 自動化，自動化的 tooincrease 可靠性、 效率與時間 toovalue 為您的組織可能會手動、 重複、 長時間執行，而且容易產生錯誤的工作。</span><span class="sxs-lookup"><span data-stu-id="3ac16-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="3ac16-108">Azure 自動化會提供您的需求調整 toomeet 的非常可靠、 高可用性的工作流程執行引擎。</span><span class="sxs-lookup"><span data-stu-id="3ac16-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales toomeet your needs.</span></span> <span data-ttu-id="3ac16-109">在 Azure 自動化中，程序可透過手動方式、經由協力廠商系統，或依照排程的間隔啟動，讓工作精準地在需要時執行。</span><span class="sxs-lookup"><span data-stu-id="3ac16-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="3ac16-110">降低操作費用並釋出 IT 和 DevOps 人員 toofocus 移動您的雲端管理工作 toobe 商務價值的工作自動執行的 Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="3ac16-110">Reduce operational overhead and free up IT and DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-api-management"></a><span data-ttu-id="3ac16-111">Azure 自動化如何協助管理 Azure API 管理？</span><span class="sxs-lookup"><span data-stu-id="3ac16-111">How can Azure Automation help manage Azure API Management?</span></span>
<span data-ttu-id="3ac16-112">應用程式開發介面可管理 Azure 自動化中使用 hello [Azure API 管理 API 的 Windows PowerShell cmdlet](https://azure.microsoft.com/updates/full-set-of-windows-powershell-cmdlets-for-azure-api-management-api/)。</span><span class="sxs-lookup"><span data-stu-id="3ac16-112">API Management can be managed in Azure Automation by using hello [Windows PowerShell cmdlets for Azure API Management API](https://azure.microsoft.com/updates/full-set-of-windows-powershell-cmdlets-for-azure-api-management-api/).</span></span> <span data-ttu-id="3ac16-113">Azure 自動化中您可以撰寫 PowerShell 工作流程指令碼 tooperform 許多您使用 hello 指令程式的 API 管理工作。</span><span class="sxs-lookup"><span data-stu-id="3ac16-113">Within Azure Automation you can write PowerShell workflow scripts tooperform many of your API Management tasks using hello cmdlets.</span></span> <span data-ttu-id="3ac16-114">您也可以跨 Azure 服務和第 3 個合作對象系統配對這些 cmdlet 在 Azure 自動化中利用 hello 適用於其他 Azure 服務、 tooautomate 複雜工作的 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="3ac16-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="3ac16-115">以下是幾個使用 API 管理搭配自動化的範例︰</span><span class="sxs-lookup"><span data-stu-id="3ac16-115">Here are some examples of using API Management with Automation:</span></span>

* [<span data-ttu-id="3ac16-116">Azure API 管理 – 使用 PowerShell 進行備份和還原</span><span class="sxs-lookup"><span data-stu-id="3ac16-116">Azure API Management – Using PowerShell for backup and restore</span></span>](https://blogs.msdn.microsoft.com/katriend/2015/10/02/azure-api-management-using-powershell-for-backup-and-restore/)

## <a name="next-steps"></a><span data-ttu-id="3ac16-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3ac16-117">Next Steps</span></span>
<span data-ttu-id="3ac16-118">既然您已經學會 hello 的 Azure 自動化，而且可以如何使用的 toomanage Azure API 管理的基本概念，請遵循這些連結 toolearn 更多。</span><span class="sxs-lookup"><span data-stu-id="3ac16-118">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure API Management, follow these links toolearn more.</span></span>

* <span data-ttu-id="3ac16-119">請參閱 hello Azure 自動化[快速入門教學課程](../automation/automation-first-runbook-graphical.md)。</span><span class="sxs-lookup"><span data-stu-id="3ac16-119">See hello Azure Automation [getting started tutorial](../automation/automation-first-runbook-graphical.md).</span></span>

