---
title: "Azure 堆疊中最新消息 |Microsoft 文件"
description: "Azure 堆疊中最新消息"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: 872b0651-0a92-4d28-b2e6-07d0a4a9a25a
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/13/2017
ms.author: helaw
ms.openlocfilehash: 28cc736704a9700845a6d2f53f4fbd06b8a81201
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="whats-new-in-azure-stack"></a><span data-ttu-id="0ccc4-103">Azure 堆疊中最新消息</span><span class="sxs-lookup"><span data-stu-id="0ccc4-103">What's new in Azure Stack</span></span>
<span data-ttu-id="0ccc4-104">此版本提供租用戶和系統管理員的新功能。</span><span class="sxs-lookup"><span data-stu-id="0ccc4-104">This release provides new features for both tenants and administrators.</span></span>

## <a name="content-services-and-tools"></a><span data-ttu-id="0ccc4-105">內容、 服務和工具</span><span class="sxs-lookup"><span data-stu-id="0ccc4-105">Content, services, and tools</span></span>
* <span data-ttu-id="0ccc4-106">[Active Directory Federation Services (AD FS)](azure-stack-key-features.md#identity)支援服務都會提供的案例的網路連線受到限制或間歇性的 identity 選項。</span><span class="sxs-lookup"><span data-stu-id="0ccc4-106">[Active Directory Federation Services (AD FS)](azure-stack-key-features.md#identity) support provides identity options for scenarios where network connectivity is limited or intermittent.</span></span>
* <span data-ttu-id="0ccc4-107">您可以使用 Azure 虛擬機器擴展集以提供 managed 的向外延展和小數位數中的 IaaS VM 為基礎的工作負載。</span><span class="sxs-lookup"><span data-stu-id="0ccc4-107">You can use Azure Virtual Machine Scale Sets to provide managed scale-out and scale-in of IaaS VM-based workloads.</span></span> 
* <span data-ttu-id="0ccc4-108">使用 Azure D 系列 VM 大小，以增加的效能和一致性。</span><span class="sxs-lookup"><span data-stu-id="0ccc4-108">Use Azure D-Series VM sizes for increased performance and consistency.</span></span>
* <span data-ttu-id="0ccc4-109">部署和使用與 Azure 一致的暫存磁碟建立範本。</span><span class="sxs-lookup"><span data-stu-id="0ccc4-109">Deploy and create templates with Temp Disks that are consistent with Azure.</span></span>
* <span data-ttu-id="0ccc4-110">[Marketplace 新聞訂閱](azure-stack-download-azure-marketplace-item.md)可讓您從 Azure Marketplace 使用的內容，並在 Azure 堆疊中提供。</span><span class="sxs-lookup"><span data-stu-id="0ccc4-110">[Marketplace Syndication](azure-stack-download-azure-marketplace-item.md) allows you to use content from the Azure Marketplace and make available in Azure Stack.</span></span>

## <a name="infrastructure-and-operations"></a><span data-ttu-id="0ccc4-111">基礎結構和操作</span><span class="sxs-lookup"><span data-stu-id="0ccc4-111">Infrastructure and operations</span></span>
* <span data-ttu-id="0ccc4-112">系統管理員和使用者隔離[入口網站](azure-stack-manage-portals.md)和 Api 提供增強式的安全性。</span><span class="sxs-lookup"><span data-stu-id="0ccc4-112">Isolated administrator and user [portals](azure-stack-manage-portals.md) and APIs provide enhanced security.</span></span>
* <span data-ttu-id="0ccc4-113">使用增強的基礎結構的管理功能，例如改善警示。</span><span class="sxs-lookup"><span data-stu-id="0ccc4-113">Use enhanced infrastructure management functionality, such as improved alerting.</span></span>
* <span data-ttu-id="0ccc4-114">使用[Windows Azure Pack 連接器](azure-stack-manage-windows-azure-pack.md)，您可以檢視和管理裝載於 Windows Azure Pack 的 IaaS 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0ccc4-114">Using the [Windows Azure Pack Connector](azure-stack-manage-windows-azure-pack.md), you can view and manage IaaS virtual machines that are hosted on Windows Azure Pack.</span></span> <span data-ttu-id="0ccc4-115">此預覽版本，在此案例只有在測試環境 （Windows Azure Pack 和 Azure 堆疊） 中的再試一次。</span><span class="sxs-lookup"><span data-stu-id="0ccc4-115">For this preview release, try this scenario only in test environments (both Windows Azure Pack and Azure Stack).</span></span> <span data-ttu-id="0ccc4-116">需要額外的設定。</span><span class="sxs-lookup"><span data-stu-id="0ccc4-116">Additional configuration is required.</span></span>
* <span data-ttu-id="0ccc4-117">Azure 堆疊現在支援[多租用戶](azure-stack-enable-multitenancy.md)的案例中，您需要提供給您的 Azure Active Directory 網域以外之使用者 IaaS 和 paas 整合服務。</span><span class="sxs-lookup"><span data-stu-id="0ccc4-117">Azure Stack now supports [multi-tenancy](azure-stack-enable-multitenancy.md) for scenarios where you need to provide IaaS and PaaS services to users outside of your Azure Active Directory domain.</span></span>  <span data-ttu-id="0ccc4-118">例如，您可以提供 Azure 堆疊服務到夥伴公司使用其身分識別。</span><span class="sxs-lookup"><span data-stu-id="0ccc4-118">For example, you may want to provide Azure Stack services to a partner company using their identities.</span></span> <span data-ttu-id="0ccc4-119">您可以設定 Azure 堆疊信任其他組織的身分識別，並讓該組織從使用者註冊訂用帳戶，並使用服務。</span><span class="sxs-lookup"><span data-stu-id="0ccc4-119">You can configure Azure Stack to trust the other organization's identities, and enable users from that organization to sign up for subscriptions and consume services.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="0ccc4-120">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0ccc4-120">Next steps</span></span>
* [<span data-ttu-id="0ccc4-121">了解 Azure 堆疊 POC 架構</span><span class="sxs-lookup"><span data-stu-id="0ccc4-121">Understand Azure Stack POC architecture</span></span>](azure-stack-architecture.md)      
* [<span data-ttu-id="0ccc4-122">了解部署必要條件</span><span class="sxs-lookup"><span data-stu-id="0ccc4-122">Understand deployment prerequisites</span></span>](azure-stack-deploy.md)
* [<span data-ttu-id="0ccc4-123">部署 Azure Stack</span><span class="sxs-lookup"><span data-stu-id="0ccc4-123">Deploy Azure Stack</span></span>](azure-stack-run-powershell-script.md)

