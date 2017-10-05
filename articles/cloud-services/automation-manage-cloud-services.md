---
title: "使用 Azure 自動化管理 Azure 雲端服務 | Microsoft Docs"
description: "了解如何使用 Azure 自動化服務大規模地管理 Azure 雲端服務。"
services: cloud-services, automation
documentationcenter: 
author: jodoglevy
manager: timlt
editor: 
ms.assetid: 3789810a-2892-4eef-bf29-c781c1b5af48
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2016
ms.author: timlt
ms.openlocfilehash: 6b5acac1b8647c324988c316cd5602b3dba98a1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-cloud-services-using-azure-automation"></a><span data-ttu-id="2b260-103">使用 Azure 自動化管理 Azure 雲端服務</span><span class="sxs-lookup"><span data-stu-id="2b260-103">Managing Azure Cloud Services using Azure Automation</span></span>
<span data-ttu-id="2b260-104">本指南將為您介紹 Azure 自動化服務，以及如何使用它來簡化您的 Azure 雲端服務管理。</span><span class="sxs-lookup"><span data-stu-id="2b260-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of your Azure cloud services.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="2b260-105">什麼是 Azure 自動化？</span><span class="sxs-lookup"><span data-stu-id="2b260-105">What is Azure Automation?</span></span>
<span data-ttu-id="2b260-106">[Azure 自動化](https://azure.microsoft.com/services/automation/) 是一項 Azure 服務，可經由程序自動化簡化雲端管理。</span><span class="sxs-lookup"><span data-stu-id="2b260-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="2b260-107">透過 Azure 自動化，長時間執行、手動、容易發生錯誤和經常重複的工作都可以自動化，以提高可靠性、效率，並為您的組織縮短創造價值時程。</span><span class="sxs-lookup"><span data-stu-id="2b260-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="2b260-108">Azure 自動化提供非常可靠且高度可用的工作流程執行引擎，可隨著組織的成長根據您的需求進行調整。</span><span class="sxs-lookup"><span data-stu-id="2b260-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales to meet your needs as your organization grows.</span></span> <span data-ttu-id="2b260-109">在 Azure 自動化中，程序可透過手動方式、經由協力廠商系統，或依照排程的間隔啟動，讓工作精準地在需要時執行。</span><span class="sxs-lookup"><span data-stu-id="2b260-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="2b260-110">將您的雲端管理工作交由「Azure 自動化」自動執行，以降低營運負擔並釋出 IT/開發維運人力，使其專注於能夠為企業創造價值的工作上。</span><span class="sxs-lookup"><span data-stu-id="2b260-110">Lower operational overhead and free up IT / DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-cloud-services"></a><span data-ttu-id="2b260-111">Azure 自動化為何有助於管理 Azure 雲端服務？</span><span class="sxs-lookup"><span data-stu-id="2b260-111">How can Azure Automation help manage Azure cloud services?</span></span>
<span data-ttu-id="2b260-112">Azure 雲端服務可透過 [Azure PowerShell 工具](https://msdn.microsoft.com/library/azure/jj156055.aspx)中提供的 PowerShell Cmdlet，在 Azure 自動化中受到管理。</span><span class="sxs-lookup"><span data-stu-id="2b260-112">Azure cloud services can be managed in Azure Automation by using the PowerShell cmdlets that are available in the [Azure PowerShell tools](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="2b260-113">Azure 自動化的這些雲端服務 PowerShell Cmdlet 都是內建的，以便您在服務內執行所有雲端服務管理工作。</span><span class="sxs-lookup"><span data-stu-id="2b260-113">Azure Automation has these cloud service PowerShell cmdlets available out of the box, so that you can perform all of your cloud service management tasks within the service.</span></span> <span data-ttu-id="2b260-114">您也可以將 Azure 自動化中的這些 Cmdlet 與其他 Azure 服務的 Cmdlet 搭配，以透過 Azure 服務和協力廠商系統自動執行複雜的工作。</span><span class="sxs-lookup"><span data-stu-id="2b260-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="2b260-115">某些範例使用 Azure 自動化來管理 Azure 雲端服務，包括︰</span><span class="sxs-lookup"><span data-stu-id="2b260-115">Some example uses of Azure Automation to manage Azure Cloud Services include:</span></span>

* [<span data-ttu-id="2b260-116">每當 Azure Blob 儲存體中更新 cscfg 或 cspkg 時，即連續部署雲端服務</span><span class="sxs-lookup"><span data-stu-id="2b260-116">Continous deployment of a Cloud Service whenever cscfg or cspkg is updated in Azure Blob storage</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Continuous-Deployment-of-A-eeebf3a6)
* [<span data-ttu-id="2b260-117">以平行方式重新啟動雲端服務執行個體，一次升級一個網域</span><span class="sxs-lookup"><span data-stu-id="2b260-117">Rebooting Cloud Service instances in parallel, one upgrade domain at a time</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Reboot-Cloud-Service-PaaS-b337a06d)

## <a name="next-steps"></a><span data-ttu-id="2b260-118">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2b260-118">Next Steps</span></span>
<span data-ttu-id="2b260-119">了解 Azure 自動化的基本概念以及如何用它來管理 Azure 雲端服務之後，請參考下列連結，以深入了解 Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="2b260-119">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure cloud services, follow these links to learn more about Azure Automation.</span></span>

* [<span data-ttu-id="2b260-120">Azure 自動化概觀</span><span class="sxs-lookup"><span data-stu-id="2b260-120">Azure Automation Overview</span></span>](../automation/automation-intro.md)
* [<span data-ttu-id="2b260-121">我的第一個 Runbook</span><span class="sxs-lookup"><span data-stu-id="2b260-121">My first runbook</span></span>](../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="2b260-122">Azure 自動化的學習地圖</span><span class="sxs-lookup"><span data-stu-id="2b260-122">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)
