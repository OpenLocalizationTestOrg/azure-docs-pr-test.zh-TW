---
title: "使用 Azure 自動化的 Vm aaaManage |Microsoft 文件"
description: "了解如何 hello Azure 自動化服務可以使用的 toomanage 大規模 Azure 虛擬機器。"
services: virtual-machines-windows, automation
documentationcenter: 
author: jodoglevy
manager: timlt
editor: 
ms.assetid: ce49f83a-f409-42ee-af74-a8ea2caa9ae8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2016
ms.author: timlt
ms.openlocfilehash: bfe7b3a51b6e82bd7cd5b0a83df7226476ed4f36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-virtual-machines-using-azure-automation"></a><span data-ttu-id="84ebe-103">使用 Azure 自動化管理 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="84ebe-103">Managing Azure Virtual Machines using Azure Automation</span></span>
<span data-ttu-id="84ebe-104">本指南會為您介紹 toohello Azure 自動化服務，以及如何使用它 toosimplify 管理 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="84ebe-104">This guide introduces you toohello Azure Automation service and how it can be used toosimplify managing your Azure virtual machines.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="84ebe-105">什麼是 Azure 自動化？</span><span class="sxs-lookup"><span data-stu-id="84ebe-105">What is Azure Automation?</span></span>
<span data-ttu-id="84ebe-106">[Azure 自動化](https://azure.microsoft.com/services/automation/) 是一項 Azure 服務，可經由程序自動化簡化雲端管理。</span><span class="sxs-lookup"><span data-stu-id="84ebe-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="84ebe-107">藉由使用 Azure 自動化，長時間執行、 手動、 容易發生錯誤，並經常重複的工作可以自動化的 tooincrease 可靠性、 效率與時間到值為您的組織。</span><span class="sxs-lookup"><span data-stu-id="84ebe-107">By using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability, efficiency, and time-to-value for your organization.</span></span>

<span data-ttu-id="84ebe-108">Azure 自動化提供高度可靠、 高可用性的工作流程執行引擎隨著組織成長而擴充 toomeet 您的需求。</span><span class="sxs-lookup"><span data-stu-id="84ebe-108">Azure Automation provides a highly reliable and highly available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="84ebe-109">在 Azure 自動化中，可利用手動方式、透過協力廠商系統或依排定的間隔開始執行程序，讓工作只發生在必要時刻。</span><span class="sxs-lookup"><span data-stu-id="84ebe-109">In Azure Automation, processes can be kicked off manually, by third-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="84ebe-110">您可以降低操作費用並釋出 IT 和 DevOps 人員 toofocus 於商務價值，將自動與 Azure 自動化執行您的雲端管理工作的工作。</span><span class="sxs-lookup"><span data-stu-id="84ebe-110">You can lower operational overhead and free up IT and DevOps staff toofocus on work that adds business value by running your cloud management tasks automatically with Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-virtual-machines"></a><span data-ttu-id="84ebe-111">Azure 自動化為何有助於管理 Azure 虛擬機器？</span><span class="sxs-lookup"><span data-stu-id="84ebe-111">How can Azure Automation help manage Azure virtual machines?</span></span>
<span data-ttu-id="84ebe-112">您可以在 Azure 自動化中使用 [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx)來管理虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="84ebe-112">Virtual machines can be managed in Azure Automation by using [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="84ebe-113">Azure 自動化包括 hello Azure PowerShell cmdlet，讓您可以執行所有的 hello 服務內虛擬機器管理工作。</span><span class="sxs-lookup"><span data-stu-id="84ebe-113">Azure Automation includes hello Azure PowerShell cmdlets, so you can perform all of your virtual machine management tasks within hello service.</span></span> <span data-ttu-id="84ebe-114">您也可以透過 Azure 服務和協力廠商系統配對在 Azure 自動化中的 hello cmdlet 與其他 Azure 服務、 tooautomate 複雜工作的 hello cmdlet。</span><span class="sxs-lookup"><span data-stu-id="84ebe-114">You can also pair hello cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and third-party systems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="84ebe-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="84ebe-115">Next steps</span></span>
<span data-ttu-id="84ebe-116">既然您已經學會 hello 基本概念的 Azure 自動化，而且可以如何使用的 toomanage Azure 虛擬機器，進一步了解：</span><span class="sxs-lookup"><span data-stu-id="84ebe-116">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure virtual machines, learn more:</span></span>

* [<span data-ttu-id="84ebe-117">Azure 自動化概觀</span><span class="sxs-lookup"><span data-stu-id="84ebe-117">Azure Automation Overview</span></span>](../../automation/automation-intro.md)
* [<span data-ttu-id="84ebe-118">我的第一個 Runbook</span><span class="sxs-lookup"><span data-stu-id="84ebe-118">My first runbook</span></span>](../../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="84ebe-119">Azure 自動化的學習地圖</span><span class="sxs-lookup"><span data-stu-id="84ebe-119">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)

