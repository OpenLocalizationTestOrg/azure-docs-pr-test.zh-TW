---
title: "Azure RemoteApp 使用 Azure 自動化 aaaManage |Microsoft 文件"
description: "深入了解如何 hello Azure 自動化服務可以使用的 toomanage Azure RemoteApp。"
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
ms.openlocfilehash: a4cb23e292c797256e971acb3b363b025f140f16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-remoteapp-using-azure-automation"></a><span data-ttu-id="f460c-103">使用 Azure 自動化管理 Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="f460c-103">Managing Azure RemoteApp using Azure Automation</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f460c-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="f460c-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="f460c-105">讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f460c-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="f460c-106">本指南將介紹 toohello Azure 自動化服務，而且您可以如何使用的 toosimplify 管理的 Azure RemoteApp。</span><span class="sxs-lookup"><span data-stu-id="f460c-106">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of Azure RemoteApp.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="f460c-107">什麼是 Azure 自動化？</span><span class="sxs-lookup"><span data-stu-id="f460c-107">What is Azure Automation?</span></span>
<span data-ttu-id="f460c-108">[Azure 自動化](../automation/automation-intro.md) 是一項 Azure 服務，可經由程序自動化簡化雲端管理。</span><span class="sxs-lookup"><span data-stu-id="f460c-108">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="f460c-109">使用 Azure 自動化，自動化的 tooincrease 可靠性、 效率與時間 toovalue 為您的組織可能會手動、 經常重複、 長時間執行及容易發生錯誤的工作。</span><span class="sxs-lookup"><span data-stu-id="f460c-109">Using Azure Automation, manual, frequently-repeated, long-running, and error-prone tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="f460c-110">Azure 自動化會提供您的需求調整 toomeet 的非常可靠、 高可用性的工作流程執行引擎。</span><span class="sxs-lookup"><span data-stu-id="f460c-110">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales toomeet your needs.</span></span> <span data-ttu-id="f460c-111">在 Azure 自動化中，程序可透過手動方式、經由協力廠商系統，或依照排程的間隔啟動，讓工作精準地在需要時執行。</span><span class="sxs-lookup"><span data-stu-id="f460c-111">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="f460c-112">降低操作費用並釋出 IT 和 DevOps 人員 toofocus 移動您的雲端管理工作 toobe 商務價值的工作自動執行的 Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="f460c-112">Reduce operational overhead and free up IT and DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-remoteapp"></a><span data-ttu-id="f460c-113">Azure 自動化為何有助於管理 Azure RemoteApp？</span><span class="sxs-lookup"><span data-stu-id="f460c-113">How can Azure Automation help manage Azure RemoteApp?</span></span>
<span data-ttu-id="f460c-114">可以使用 hello hello 中可用的 PowerShell cmdlet 在 Azure 自動化中管理 RemoteApp [Azure PowerShell 工具](https://msdn.microsoft.com/library/azure/jj156055.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f460c-114">RemoteApp can be managed in Azure Automation by using hello PowerShell cmdlets that are available in hello [Azure PowerShell tools](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="f460c-115">Azure 自動化會有這些可用的 RemoteApp PowerShell cmdlet hello 立即可用，以便您可以執行所有的 RemoteApp hello 服務中管理工作。</span><span class="sxs-lookup"><span data-stu-id="f460c-115">Azure Automation has these RemoteApp PowerShell cmdlets available out of hello box, so that you can perform all of your RemoteApp management tasks within hello service.</span></span> <span data-ttu-id="f460c-116">您也可以跨 Azure 服務和第 3 個合作對象系統配對這些 cmdlet 在 Azure 自動化中利用 hello 適用於其他 Azure 服務、 tooautomate 複雜工作的 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="f460c-116">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f460c-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f460c-117">Next steps</span></span>
<span data-ttu-id="f460c-118">現在，您學到的 Azure 自動化，而且可以如何使用的 toomanage Azure RemoteApp 的 hello 基本概念，請遵循這些連結 toolearn 深入了解 Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="f460c-118">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure RemoteApp, follow these links toolearn more about Azure Automation.</span></span>

* <span data-ttu-id="f460c-119">請參閱 hello Azure 自動化[入門教學課程](../automation/automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="f460c-119">See hello Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md)</span></span>

