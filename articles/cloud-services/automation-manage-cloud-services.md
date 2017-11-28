---
title: "Azure 雲端服務使用 Azure 自動化 aaaManage |Microsoft 文件"
description: "深入了解如何 hello Azure 自動化服務可以使用的 toomanage 大規模的 Azure 雲端服務。"
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
ms.openlocfilehash: 8e920fb94955466bfec71cc332444f5f0ee497a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-cloud-services-using-azure-automation"></a><span data-ttu-id="a86df-103">使用 Azure 自動化管理 Azure 雲端服務</span><span class="sxs-lookup"><span data-stu-id="a86df-103">Managing Azure Cloud Services using Azure Automation</span></span>
<span data-ttu-id="a86df-104">本指南將介紹 toohello Azure 自動化服務，而且您可以如何使用的 toosimplify 管理您的 Azure 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="a86df-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of your Azure cloud services.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="a86df-105">什麼是 Azure 自動化？</span><span class="sxs-lookup"><span data-stu-id="a86df-105">What is Azure Automation?</span></span>
<span data-ttu-id="a86df-106">[Azure 自動化](https://azure.microsoft.com/services/automation/) 是一項 Azure 服務，可經由程序自動化簡化雲端管理。</span><span class="sxs-lookup"><span data-stu-id="a86df-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="a86df-107">使用 Azure 自動化，長時間執行、 手動、 容易發生錯誤，並經常重複的工作可以自動化的 tooincrease 可靠性、 效率與時間 toovalue 為您的組織。</span><span class="sxs-lookup"><span data-stu-id="a86df-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="a86df-108">Azure 自動化提供高度可靠、 高可用性的工作流程執行引擎隨著組織成長而擴充 toomeet 您的需求。</span><span class="sxs-lookup"><span data-stu-id="a86df-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="a86df-109">在 Azure 自動化中，程序可透過手動方式、經由協力廠商系統，或依照排程的間隔啟動，讓工作精準地在需要時執行。</span><span class="sxs-lookup"><span data-stu-id="a86df-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="a86df-110">降低操作費用並釋出 IT / DevOps 人員 toofocus 移動您的雲端管理工作 toobe 商務價值的工作自動執行的 Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="a86df-110">Lower operational overhead and free up IT / DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-cloud-services"></a><span data-ttu-id="a86df-111">Azure 自動化為何有助於管理 Azure 雲端服務？</span><span class="sxs-lookup"><span data-stu-id="a86df-111">How can Azure Automation help manage Azure cloud services?</span></span>
<span data-ttu-id="a86df-112">Azure 雲端服務可以使用 hello 中可用的 hello PowerShell cmdlet 來管理 Azure 自動化中[Azure PowerShell 工具](https://msdn.microsoft.com/library/azure/jj156055.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a86df-112">Azure cloud services can be managed in Azure Automation by using hello PowerShell cmdlets that are available in hello [Azure PowerShell tools](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="a86df-113">Azure 自動化有超出 hello 方塊中，這些雲端服務 PowerShell cmdlet 可用，以便您可以執行您的雲端服務管理工作，hello 服務內的所有。</span><span class="sxs-lookup"><span data-stu-id="a86df-113">Azure Automation has these cloud service PowerShell cmdlets available out of hello box, so that you can perform all of your cloud service management tasks within hello service.</span></span> <span data-ttu-id="a86df-114">您也可以跨 Azure 服務和第 3 個合作對象系統配對這些 cmdlet 在 Azure 自動化中利用 hello 適用於其他 Azure 服務、 tooautomate 複雜工作的 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a86df-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="a86df-115">某些範例使用的 Azure 自動化 toomanage Azure 雲端服務包括：</span><span class="sxs-lookup"><span data-stu-id="a86df-115">Some example uses of Azure Automation toomanage Azure Cloud Services include:</span></span>

* [<span data-ttu-id="a86df-116">每當 Azure Blob 儲存體中更新 cscfg 或 cspkg 時，即連續部署雲端服務</span><span class="sxs-lookup"><span data-stu-id="a86df-116">Continous deployment of a Cloud Service whenever cscfg or cspkg is updated in Azure Blob storage</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Continuous-Deployment-of-A-eeebf3a6)
* [<span data-ttu-id="a86df-117">以平行方式重新啟動雲端服務執行個體，一次升級一個網域</span><span class="sxs-lookup"><span data-stu-id="a86df-117">Rebooting Cloud Service instances in parallel, one upgrade domain at a time</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Reboot-Cloud-Service-PaaS-b337a06d)

## <a name="next-steps"></a><span data-ttu-id="a86df-118">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a86df-118">Next Steps</span></span>
<span data-ttu-id="a86df-119">既然您已經學會 hello 的 Azure 自動化，而且可以如何使用的 toomanage Azure 雲端服務的基本概念，請遵循這些連結 toolearn 深入了解 Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="a86df-119">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure cloud services, follow these links toolearn more about Azure Automation.</span></span>

* [<span data-ttu-id="a86df-120">Azure 自動化概觀</span><span class="sxs-lookup"><span data-stu-id="a86df-120">Azure Automation Overview</span></span>](../automation/automation-intro.md)
* [<span data-ttu-id="a86df-121">我的第一個 Runbook</span><span class="sxs-lookup"><span data-stu-id="a86df-121">My first runbook</span></span>](../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="a86df-122">Azure 自動化的學習地圖</span><span class="sxs-lookup"><span data-stu-id="a86df-122">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)
