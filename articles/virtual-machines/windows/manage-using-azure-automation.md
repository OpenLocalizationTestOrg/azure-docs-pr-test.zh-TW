---
title: "使用 Azure 自動化管理 VM | Microsoft Docs"
description: "了解如何使用 Azure 自動化服務大規模地管理 Azure 虛擬機器。"
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
ms.openlocfilehash: 15653c5d653ae538bdb66eaf0daee12c35858b45
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-virtual-machines-using-azure-automation"></a><span data-ttu-id="7458a-103">使用 Azure 自動化管理 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="7458a-103">Managing Azure Virtual Machines using Azure Automation</span></span>
<span data-ttu-id="7458a-104">本指南將為您介紹 Azure 自動化服務，以及如何使用它來簡化您的 Azure 虛擬機器管理。</span><span class="sxs-lookup"><span data-stu-id="7458a-104">This guide introduces you to the Azure Automation service and how it can be used to simplify managing your Azure virtual machines.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="7458a-105">什麼是 Azure 自動化？</span><span class="sxs-lookup"><span data-stu-id="7458a-105">What is Azure Automation?</span></span>
<span data-ttu-id="7458a-106">[Azure 自動化](https://azure.microsoft.com/services/automation/) 是一項 Azure 服務，可經由程序自動化簡化雲端管理。</span><span class="sxs-lookup"><span data-stu-id="7458a-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="7458a-107">透過 Azure 自動化，長時間執行、手動、容易發生錯誤和經常重複的工作都可以自動化，以提高可靠性、效率，並為您的組織縮短創造價值時程。</span><span class="sxs-lookup"><span data-stu-id="7458a-107">By using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated to increase reliability, efficiency, and time-to-value for your organization.</span></span>

<span data-ttu-id="7458a-108">Azure 自動化提供非常可靠且高度可用的工作流程執行引擎，可隨著組織的成長根據您的需求進行調整。</span><span class="sxs-lookup"><span data-stu-id="7458a-108">Azure Automation provides a highly reliable and highly available workflow execution engine that scales to meet your needs as your organization grows.</span></span> <span data-ttu-id="7458a-109">在 Azure 自動化中，可利用手動方式、透過協力廠商系統或依排定的間隔開始執行程序，讓工作只發生在必要時刻。</span><span class="sxs-lookup"><span data-stu-id="7458a-109">In Azure Automation, processes can be kicked off manually, by third-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="7458a-110">您可以透過 Azure 自動化來自動執行雲端管理工作，以減少營運負擔並釋出 IT 和 DevOps 人力，使其專注於能夠為企業創造價值的工作上。</span><span class="sxs-lookup"><span data-stu-id="7458a-110">You can lower operational overhead and free up IT and DevOps staff to focus on work that adds business value by running your cloud management tasks automatically with Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-virtual-machines"></a><span data-ttu-id="7458a-111">Azure 自動化為何有助於管理 Azure 虛擬機器？</span><span class="sxs-lookup"><span data-stu-id="7458a-111">How can Azure Automation help manage Azure virtual machines?</span></span>
<span data-ttu-id="7458a-112">您可以在 Azure 自動化中使用 [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx)來管理虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="7458a-112">Virtual machines can be managed in Azure Automation by using [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="7458a-113">Azure 自動化包含 Azure PowerShell Cmdlet，因此您可以在此服務內執行所有的虛擬機器管理工作。</span><span class="sxs-lookup"><span data-stu-id="7458a-113">Azure Automation includes the Azure PowerShell cmdlets, so you can perform all of your virtual machine management tasks within the service.</span></span> <span data-ttu-id="7458a-114">您也可以將 Azure 自動化中的 Cmdlet 與其他 Azure 服務的 Cmdlet 搭配，以便在 Azure 服務和協力廠商系統上自動執行複雜的工作。</span><span class="sxs-lookup"><span data-stu-id="7458a-114">You can also pair the cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and third-party systems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7458a-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7458a-115">Next steps</span></span>
<span data-ttu-id="7458a-116">了解 Azure 自動化的基本概念以及如何用它來管理 Azure 虛擬機器之後，深入了解：</span><span class="sxs-lookup"><span data-stu-id="7458a-116">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure virtual machines, learn more:</span></span>

* [<span data-ttu-id="7458a-117">Azure 自動化概觀</span><span class="sxs-lookup"><span data-stu-id="7458a-117">Azure Automation Overview</span></span>](../../automation/automation-intro.md)
* [<span data-ttu-id="7458a-118">我的第一個 Runbook</span><span class="sxs-lookup"><span data-stu-id="7458a-118">My first runbook</span></span>](../../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="7458a-119">Azure 自動化的學習地圖</span><span class="sxs-lookup"><span data-stu-id="7458a-119">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)

