---
title: "aaaManage Azure 儲存體使用 Azure 自動化"
description: "深入了解如何 hello Azure 自動化服務可以使用在標尺 toomanage Azure 儲存體。"
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
ms.openlocfilehash: 5edfba1a9ce1f9c81b5bd0889de19099f3d86fc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-storage-using-azure-automation"></a><span data-ttu-id="4dec0-103">使用 Azure 自動化管理 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="4dec0-103">Managing Azure Storage using Azure Automation</span></span>
<span data-ttu-id="4dec0-104">本指南將介紹 toohello Azure 自動化服務，而且您可以如何使用的 toosimplify 管理 Azure 儲存體 blob、 資料表和佇列。</span><span class="sxs-lookup"><span data-stu-id="4dec0-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of your Azure Storage blobs, tables, and queues.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="4dec0-105">什麼是 Azure 自動化？</span><span class="sxs-lookup"><span data-stu-id="4dec0-105">What is Azure Automation?</span></span>
<span data-ttu-id="4dec0-106">[Azure 自動化](https://azure.microsoft.com/services/automation/) 是一項 Azure 服務，可經由程序自動化簡化雲端管理。</span><span class="sxs-lookup"><span data-stu-id="4dec0-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="4dec0-107">使用 Azure 自動化，長時間執行，手動容易發生錯誤，而且經常重複可以工作自動化的 tooincrease 穩定性和效率，並減少時間 toovalue 為您的組織。</span><span class="sxs-lookup"><span data-stu-id="4dec0-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability and efficiency, and reduce time toovalue for your organization.</span></span>

<span data-ttu-id="4dec0-108">Azure 自動化提供高度可靠、 高可用性的工作流程執行引擎隨著組織成長而擴充 toomeet 您的需求。</span><span class="sxs-lookup"><span data-stu-id="4dec0-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="4dec0-109">在 Azure 自動化中，程序可透過手動方式、經由協力廠商系統，或依照排程的間隔啟動，讓工作精準地在需要時執行。</span><span class="sxs-lookup"><span data-stu-id="4dec0-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="4dec0-110">降低操作費用並釋出 IT / DevOps 人員 toofocus 移動您的雲端管理工作 toobe 商務價值的工作自動執行的 Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="4dec0-110">Lower operational overhead and free up IT / DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-storage"></a><span data-ttu-id="4dec0-111">Azure 自動化為何有助於管理 Azure 儲存體？</span><span class="sxs-lookup"><span data-stu-id="4dec0-111">How can Azure Automation help manage Azure Storage?</span></span>
<span data-ttu-id="4dec0-112">Azure 儲存體可以使用提供的 hello PowerShell cmdlet 來管理 Azure 自動化中[Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4dec0-112">Azure Storage can be managed in Azure Automation by using hello PowerShell cmdlets that are available in [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="4dec0-113">讓您可以執行您的 blob、 資料表和佇列管理工作 hello 服務內的所有 azure 自動化出 hello 方塊中，有可以使用這些儲存體 PowerShell 指令程式。</span><span class="sxs-lookup"><span data-stu-id="4dec0-113">Azure Automation has these Storage PowerShell cmdlets available out of hello box, so that you can perform all of your blob, table, and queue management tasks within hello service.</span></span> <span data-ttu-id="4dec0-114">您也可以跨 Azure 服務和第 3 個合作對象系統配對這些 cmdlet 在 Azure 自動化中利用 hello 適用於其他 Azure 服務、 tooautomate 複雜工作的 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="4dec0-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="4dec0-115">hello [Azure 自動化 runbook 資源庫](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/)包含各種不同的產品團隊和社群 runbook tooget 啟動自動化的 Azure 儲存體、 其他 Azure 服務和第 3 個合作對象的系統管理。</span><span class="sxs-lookup"><span data-stu-id="4dec0-115">hello [Azure Automation runbook gallery](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contains a variety of product team and community runbooks tooget started automating management of Azure Storage, other Azure services, and 3rd party systems.</span></span> <span data-ttu-id="4dec0-116">資源庫 Runbook 包括：</span><span class="sxs-lookup"><span data-stu-id="4dec0-116">Gallery runbooks include:</span></span>

* [<span data-ttu-id="4dec0-117">使用自動化服務移除特定天數前的 Azure 儲存體 Blob</span><span class="sxs-lookup"><span data-stu-id="4dec0-117">Remove Azure Storage Blobs that are Certain Days Old Using Automation Service</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Remove-Storage-Blobs-that-aae4b761)
* [<span data-ttu-id="4dec0-118">從 Azure 儲存體下載 Blob</span><span class="sxs-lookup"><span data-stu-id="4dec0-118">Download a Blob from Azure Storage</span></span>](https://gallery.technet.microsoft.com/scriptcenter/a-Blob-from-Azure-Storage-6bc13745)
* [<span data-ttu-id="4dec0-119">備份單一 Azure VM 中的所有磁碟，或雲端服務中所有 VM 的所有磁碟</span><span class="sxs-lookup"><span data-stu-id="4dec0-119">Backup all disks for a single Azure VM or for all VMs in a Cloud Service</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Backup-all-disks-for-a-ede940d5)

## <a name="next-steps"></a><span data-ttu-id="4dec0-120">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4dec0-120">Next Steps</span></span>
<span data-ttu-id="4dec0-121">既然您已經學會 hello 的 Azure 自動化，方式可以使用的 toomanage Azure 儲存體 blob、 資料表和佇列的基本概念，請遵循這些連結 toolearn 深入了解 Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="4dec0-121">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure Storage blobs, tables, and queues, follow these links toolearn more about Azure Automation.</span></span>

<span data-ttu-id="4dec0-122">請參閱 hello Azure 自動化教學課程[建立或匯入 Azure 自動化中的 runbook](../../automation/automation-creating-importing-runbook.md)。</span><span class="sxs-lookup"><span data-stu-id="4dec0-122">See hello Azure Automation tutorial [Creating or importing a runbook in Azure Automation](../../automation/automation-creating-importing-runbook.md).</span></span>

