---
title: "aaaWhat 的新 Azure 堆疊中 |Microsoft 文件"
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
ms.openlocfilehash: 32b4bd7deebb12a92e4abbdaacdbcebaa5125e11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="whats-new-in-azure-stack"></a><span data-ttu-id="32b4c-103">Azure 堆疊中最新消息</span><span class="sxs-lookup"><span data-stu-id="32b4c-103">What's new in Azure Stack</span></span>
<span data-ttu-id="32b4c-104">此版本提供租用戶和系統管理員的新功能。</span><span class="sxs-lookup"><span data-stu-id="32b4c-104">This release provides new features for both tenants and administrators.</span></span>

## <a name="content-services-and-tools"></a><span data-ttu-id="32b4c-105">內容、 服務和工具</span><span class="sxs-lookup"><span data-stu-id="32b4c-105">Content, services, and tools</span></span>
* <span data-ttu-id="32b4c-106">[Active Directory Federation Services (AD FS)](azure-stack-key-features.md#identity)支援服務都會提供的案例的網路連線受到限制或間歇性的 identity 選項。</span><span class="sxs-lookup"><span data-stu-id="32b4c-106">[Active Directory Federation Services (AD FS)](azure-stack-key-features.md#identity) support provides identity options for scenarios where network connectivity is limited or intermittent.</span></span>
* <span data-ttu-id="32b4c-107">您可以使用 Azure 虛擬機器擴展集 tooprovide 管理向外延展及向單元 IaaS VM 為基礎的工作負載。</span><span class="sxs-lookup"><span data-stu-id="32b4c-107">You can use Azure Virtual Machine Scale Sets tooprovide managed scale-out and scale-in of IaaS VM-based workloads.</span></span> 
* <span data-ttu-id="32b4c-108">使用 Azure D 系列 VM 大小，以增加的效能和一致性。</span><span class="sxs-lookup"><span data-stu-id="32b4c-108">Use Azure D-Series VM sizes for increased performance and consistency.</span></span>
* <span data-ttu-id="32b4c-109">部署和使用與 Azure 一致的暫存磁碟建立範本。</span><span class="sxs-lookup"><span data-stu-id="32b4c-109">Deploy and create templates with Temp Disks that are consistent with Azure.</span></span>
* <span data-ttu-id="32b4c-110">[Marketplace 新聞訂閱](azure-stack-download-azure-marketplace-item.md)可讓您從 hello Azure Marketplace toouse 內容，並提供 Azure 堆疊中。</span><span class="sxs-lookup"><span data-stu-id="32b4c-110">[Marketplace Syndication](azure-stack-download-azure-marketplace-item.md) allows you toouse content from hello Azure Marketplace and make available in Azure Stack.</span></span>

## <a name="infrastructure-and-operations"></a><span data-ttu-id="32b4c-111">基礎結構和操作</span><span class="sxs-lookup"><span data-stu-id="32b4c-111">Infrastructure and operations</span></span>
* <span data-ttu-id="32b4c-112">系統管理員和使用者隔離[入口網站](azure-stack-manage-portals.md)和 Api 提供增強式的安全性。</span><span class="sxs-lookup"><span data-stu-id="32b4c-112">Isolated administrator and user [portals](azure-stack-manage-portals.md) and APIs provide enhanced security.</span></span>
* <span data-ttu-id="32b4c-113">使用增強的基礎結構的管理功能，例如改善警示。</span><span class="sxs-lookup"><span data-stu-id="32b4c-113">Use enhanced infrastructure management functionality, such as improved alerting.</span></span>
* <span data-ttu-id="32b4c-114">使用 hello [Windows Azure Pack 連接器](azure-stack-manage-windows-azure-pack.md)，您可以檢視和管理裝載於 Windows Azure Pack 的 IaaS 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="32b4c-114">Using hello [Windows Azure Pack Connector](azure-stack-manage-windows-azure-pack.md), you can view and manage IaaS virtual machines that are hosted on Windows Azure Pack.</span></span> <span data-ttu-id="32b4c-115">此預覽版本，在此案例只有在測試環境 （Windows Azure Pack 和 Azure 堆疊） 中的再試一次。</span><span class="sxs-lookup"><span data-stu-id="32b4c-115">For this preview release, try this scenario only in test environments (both Windows Azure Pack and Azure Stack).</span></span> <span data-ttu-id="32b4c-116">需要額外的設定。</span><span class="sxs-lookup"><span data-stu-id="32b4c-116">Additional configuration is required.</span></span>
* <span data-ttu-id="32b4c-117">Azure 堆疊現在支援[多租用戶](azure-stack-enable-multitenancy.md)案例，其中需要 tooprovide IaaS 和 PaaS 服務 toousers Azure Active Directory 網域之外。</span><span class="sxs-lookup"><span data-stu-id="32b4c-117">Azure Stack now supports [multi-tenancy](azure-stack-enable-multitenancy.md) for scenarios where you need tooprovide IaaS and PaaS services toousers outside of your Azure Active Directory domain.</span></span>  <span data-ttu-id="32b4c-118">比方說，您可能想 tooprovide Azure 堆疊服務 tooa 合作夥伴公司使用其身分識別。</span><span class="sxs-lookup"><span data-stu-id="32b4c-118">For example, you may want tooprovide Azure Stack services tooa partner company using their identities.</span></span> <span data-ttu-id="32b4c-119">您可以設定 Azure 堆疊 tootrust hello 其他組織的身分識別，並讓使用者從訂用帳戶註冊該組織 toosign 取用服務。</span><span class="sxs-lookup"><span data-stu-id="32b4c-119">You can configure Azure Stack tootrust hello other organization's identities, and enable users from that organization toosign up for subscriptions and consume services.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="32b4c-120">後續步驟</span><span class="sxs-lookup"><span data-stu-id="32b4c-120">Next steps</span></span>
* [<span data-ttu-id="32b4c-121">了解 Azure 堆疊 POC 架構</span><span class="sxs-lookup"><span data-stu-id="32b4c-121">Understand Azure Stack POC architecture</span></span>](azure-stack-architecture.md)      
* [<span data-ttu-id="32b4c-122">了解部署必要條件</span><span class="sxs-lookup"><span data-stu-id="32b4c-122">Understand deployment prerequisites</span></span>](azure-stack-deploy.md)
* [<span data-ttu-id="32b4c-123">部署 Azure Stack</span><span class="sxs-lookup"><span data-stu-id="32b4c-123">Deploy Azure Stack</span></span>](azure-stack-run-powershell-script.md)

