---
title: "Azure Web 應用程式使用 Azure 自動化 aaaManage |Microsoft 文件"
description: "深入了解如何 hello Azure 自動化服務可以使用的 toomanage Azure Web 應用程式。"
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
ms.openlocfilehash: 6d80351a2927f26753cfbaead6e1c0c3c94e86e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-web-app-using-azure-automation"></a><span data-ttu-id="62dba-103">使用 Azure 自動化管理 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="62dba-103">Managing Azure Web App using Azure Automation</span></span>
<span data-ttu-id="62dba-104">本指南將介紹 toohello Azure 自動化服務，而且您可以如何使用的 toosimplify 管理的 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="62dba-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of Azure Web App.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="62dba-105">什麼是 Azure 自動化？</span><span class="sxs-lookup"><span data-stu-id="62dba-105">What is Azure Automation?</span></span>
<span data-ttu-id="62dba-106">[Azure 自動化](../automation/automation-intro.md) 是一項 Azure 服務，可經由程序自動化簡化雲端管理。</span><span class="sxs-lookup"><span data-stu-id="62dba-106">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="62dba-107">使用 Azure 自動化，自動化的 tooincrease 可靠性、 效率與時間 toovalue 為您的組織可能會手動、 重複、 長時間執行，而且容易產生錯誤的工作。</span><span class="sxs-lookup"><span data-stu-id="62dba-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="62dba-108">Azure 自動化會提供您的需求調整 toomeet 的非常可靠、 高可用性的工作流程執行引擎。</span><span class="sxs-lookup"><span data-stu-id="62dba-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales toomeet your needs.</span></span> <span data-ttu-id="62dba-109">在 Azure 自動化中，程序可透過手動方式、經由協力廠商系統，或依照排程的間隔啟動，讓工作精準地在需要時執行。</span><span class="sxs-lookup"><span data-stu-id="62dba-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="62dba-110">降低操作費用並釋出 IT 和 DevOps 人員 toofocus 移動您的雲端管理工作 toobe 商務價值的工作自動執行的 Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="62dba-110">Reduce operational overhead and free up IT and DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-web-app"></a><span data-ttu-id="62dba-111">Azure 自動化為何有助於管理 Azure Web 應用程式？</span><span class="sxs-lookup"><span data-stu-id="62dba-111">How can Azure Automation help manage Azure Web App?</span></span>
<span data-ttu-id="62dba-112">Web 應用程式可以使用 hello 中可用的 hello PowerShell cmdlet 來管理 Azure 自動化中[Azure PowerShell 模組](/powershell/azureps-cmdlets-docs)。</span><span class="sxs-lookup"><span data-stu-id="62dba-112">Web App can be managed in Azure Automation by using hello PowerShell cmdlets that are available in hello [Azure PowerShell modules](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="62dba-113">您可以[安裝這些 Web 應用程式的 PowerShell cmdlet 在 Azure 自動化中](https://azure.microsoft.com/blog/announcing-azure-resource-manager-support-azure-automation-runbooks/)，如此一來，您可以執行所有的 hello 服務內的 Web 應用程式管理工作。</span><span class="sxs-lookup"><span data-stu-id="62dba-113">You can [install these Web App PowerShell cmdlets in Azure Automation](https://azure.microsoft.com/blog/announcing-azure-resource-manager-support-azure-automation-runbooks/), so that you can perform all of your Web App management tasks within hello service.</span></span> <span data-ttu-id="62dba-114">您也可以跨 Azure 服務和第 3 個合作對象系統配對在 Azure 自動化中這些 cmdlet 與其他 Azure 服務 tooautomate 複雜工作的 hello cmdlet。</span><span class="sxs-lookup"><span data-stu-id="62dba-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="62dba-115">以下是使用自動化來管理應用程式服務的一些範例 ︰</span><span class="sxs-lookup"><span data-stu-id="62dba-115">Here are some examples of managing App Services with Automation:</span></span>

* [<span data-ttu-id="62dba-116">用來管理 Web Apps 的指令碼</span><span class="sxs-lookup"><span data-stu-id="62dba-116">Scripts for managing Web Apps</span></span>](https://azure.microsoft.com/documentation/scripts/)

## <a name="next-steps"></a><span data-ttu-id="62dba-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="62dba-117">Next steps</span></span>
<span data-ttu-id="62dba-118">既然您已經學會 hello 的 Azure 自動化，而且可以如何使用的 toomanage Azure Web 應用程式的基本概念，請遵循這些連結 toolearn 深入了解 Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="62dba-118">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure Web App, follow these links toolearn more about Azure Automation.</span></span>

* <span data-ttu-id="62dba-119">請參閱 hello Azure 自動化[入門教學課程](../automation/automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="62dba-119">See hello Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md)</span></span>

