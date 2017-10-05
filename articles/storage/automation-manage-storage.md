---
title: "使用 Azure 自動化管理 Azure 儲存體"
description: "了解如何使用 Azure 自動化服務大規模地管理 Azure 儲存體。"
services: storage, automation
documentationcenter: 
author: jodoglevy
manager: eamono
editor: 
ms.assetid: bac41c39-1d95-46aa-a481-ec17bbb21b40
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: eamono
ms.openlocfilehash: fbf1cd9e73615f8d991f348cb705aa9df8b55b4e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-storage-using-azure-automation"></a><span data-ttu-id="44894-103">使用 Azure 自動化管理 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="44894-103">Managing Azure Storage using Azure Automation</span></span>
<span data-ttu-id="44894-104">本指南將為您介紹 Azure 自動化服務，以及如何使用它來簡化 Azure 儲存體 Blob、資料表及佇列的管理。</span><span class="sxs-lookup"><span data-stu-id="44894-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of your Azure Storage blobs, tables, and queues.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="44894-105">什麼是 Azure 自動化？</span><span class="sxs-lookup"><span data-stu-id="44894-105">What is Azure Automation?</span></span>
<span data-ttu-id="44894-106">[Azure 自動化](https://azure.microsoft.com/services/automation/) 是一項 Azure 服務，可經由程序自動化簡化雲端管理。</span><span class="sxs-lookup"><span data-stu-id="44894-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="44894-107">透過 Azure 自動化，長時間執行、手動、容易發生錯誤和經常重複的工作都可以自動化，以提高可靠性、效率，並為您的組織縮短創造價值時程。</span><span class="sxs-lookup"><span data-stu-id="44894-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated to increase reliability and efficiency, and reduce time to value for your organization.</span></span>

<span data-ttu-id="44894-108">Azure 自動化提供非常可靠且高度可用的工作流程執行引擎，可隨著組織的成長根據您的需求進行調整。</span><span class="sxs-lookup"><span data-stu-id="44894-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales to meet your needs as your organization grows.</span></span> <span data-ttu-id="44894-109">在 Azure 自動化中，程序可透過手動方式、經由協力廠商系統，或依照排程的間隔啟動，讓工作精準地在需要時執行。</span><span class="sxs-lookup"><span data-stu-id="44894-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="44894-110">將您的雲端管理工作交由「Azure 自動化」自動執行，以降低營運負擔並釋出 IT/開發維運人力，使其專注於能夠為企業創造價值的工作上。</span><span class="sxs-lookup"><span data-stu-id="44894-110">Lower operational overhead and free up IT / DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-storage"></a><span data-ttu-id="44894-111">Azure 自動化為何有助於管理 Azure 儲存體？</span><span class="sxs-lookup"><span data-stu-id="44894-111">How can Azure Automation help manage Azure Storage?</span></span>
<span data-ttu-id="44894-112">您可以透過使用 [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx)中提供的 PowerShell Cmdlet，於 Azure 自動化中管理 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="44894-112">Azure Storage can be managed in Azure Automation by using the PowerShell cmdlets that are available in [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="44894-113">Azure 自動化的這些 儲存體 PowerShell Cmdlet 都是內建的，以便您在服務內執行所有 Blob、資料表及佇列管理工作。</span><span class="sxs-lookup"><span data-stu-id="44894-113">Azure Automation has these Storage PowerShell cmdlets available out of the box, so that you can perform all of your blob, table, and queue management tasks within the service.</span></span> <span data-ttu-id="44894-114">您也可以將 Azure 自動化中的這些 Cmdlet 與其他 Azure 服務的 Cmdlet 搭配，以透過 Azure 服務和協力廠商系統自動執行複雜的工作。</span><span class="sxs-lookup"><span data-stu-id="44894-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="44894-115">[Azure 自動化 Runbook 資源庫](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) 含有多種產品團隊和社群 Runbook，可供您開始針對 Azure 儲存體、其他 Azure 服務及協力廠商系統進行自動化管理。</span><span class="sxs-lookup"><span data-stu-id="44894-115">The [Azure Automation runbook gallery](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contains a variety of product team and community runbooks to get started automating management of Azure Storage, other Azure services, and 3rd party systems.</span></span> <span data-ttu-id="44894-116">資源庫 Runbook 包括：</span><span class="sxs-lookup"><span data-stu-id="44894-116">Gallery runbooks include:</span></span>

* [<span data-ttu-id="44894-117">使用自動化服務移除特定天數前的 Azure 儲存體 Blob</span><span class="sxs-lookup"><span data-stu-id="44894-117">Remove Azure Storage Blobs that are Certain Days Old Using Automation Service</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Remove-Storage-Blobs-that-aae4b761)
* [<span data-ttu-id="44894-118">從 Azure 儲存體下載 Blob</span><span class="sxs-lookup"><span data-stu-id="44894-118">Download a Blob from Azure Storage</span></span>](https://gallery.technet.microsoft.com/scriptcenter/a-Blob-from-Azure-Storage-6bc13745)
* [<span data-ttu-id="44894-119">備份單一 Azure VM 中的所有磁碟，或雲端服務中所有 VM 的所有磁碟</span><span class="sxs-lookup"><span data-stu-id="44894-119">Backup all disks for a single Azure VM or for all VMs in a Cloud Service</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Backup-all-disks-for-a-ede940d5)

## <a name="next-steps"></a><span data-ttu-id="44894-120">後續步驟</span><span class="sxs-lookup"><span data-stu-id="44894-120">Next Steps</span></span>
<span data-ttu-id="44894-121">了解 Azure 自動化的基本概念以及如何用它來管理 Azure 儲存體 Blob、資料表及佇列之後，請參考下列連結，以深入了解 Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="44894-121">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure Storage blobs, tables, and queues, follow these links to learn more about Azure Automation.</span></span>

<span data-ttu-id="44894-122">請參閱 Azure 自動化教學課程： [在 Azure 自動化中建立或匯入 Runbook](../automation/automation-creating-importing-runbook.md)。</span><span class="sxs-lookup"><span data-stu-id="44894-122">See the Azure Automation tutorial [Creating or importing a runbook in Azure Automation](../automation/automation-creating-importing-runbook.md).</span></span>

