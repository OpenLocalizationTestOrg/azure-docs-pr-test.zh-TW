---
title: "aaaWhat 是 Azure 堆疊？ | Microsoft Docs"
description: "Azure Stack 開發套件是一種用來評估 Azure Stack 功能和案例的環境。"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: d9e6aee1-4cba-4df5-b5a3-6f38da9627a3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: helaw
ms.custom: mvc
ms.openlocfilehash: 3f7c84f2302a6411f49a07de171501fbd72812e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-stack"></a><span data-ttu-id="03b39-104">什麼是 Azure Stack？</span><span class="sxs-lookup"><span data-stu-id="03b39-104">What is Azure Stack?</span></span>

<span data-ttu-id="03b39-105">Microsoft Azure Stack 是混合式雲端平台產品，可讓您組織的資料中心提供 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="03b39-105">Microsoft Azure Stack is a hybrid cloud platform that lets you deliver Azure services from your organization’s datacenter.</span></span>  <span data-ttu-id="03b39-106">Azure 堆疊是設計的 toohelp 您在索引鍵的情況下，像是符合安全性與相容性需求，或您需要 tooaccess 未連線到網際網路的 Azure 資源的位置。</span><span class="sxs-lookup"><span data-stu-id="03b39-106">Azure Stack is designed toohelp you in key scenarios, like meeting security and compliance requirements, or where you need tooaccess Azure resources without internet connectivity.</span></span>  

## <a name="azure-stack-development-kit"></a><span data-ttu-id="03b39-107">Azure Stack 開發套件</span><span class="sxs-lookup"><span data-stu-id="03b39-107">Azure Stack Development Kit</span></span>
<span data-ttu-id="03b39-108">Microsoft Azure 堆疊開發套件是單一節點版本的 Azure 堆疊，您可以使用 tooevaluate 並了解 Azure 堆疊。</span><span class="sxs-lookup"><span data-stu-id="03b39-108">Microsoft Azure Stack Development Kit is a single-node version of Azure Stack, which you can use tooevaluate and learn about Azure Stack.</span></span>  <span data-ttu-id="03b39-109">您也可以將 Azure Stack 開發套件作為開發人員環境，您可在其中使用一致的 API 和工具進行開發。</span><span class="sxs-lookup"><span data-stu-id="03b39-109">You can also use Azure Stack Development Kit as a developer environment, where you can develop using consistent APIs and tooling.</span></span>  

<span data-ttu-id="03b39-110">您應該留意下列 Azure Stack 開發套件事宜：</span><span class="sxs-lookup"><span data-stu-id="03b39-110">You should be aware of these points with Azure Stack Development Kit:</span></span>

* <span data-ttu-id="03b39-111">Azure Stack 開發套件不可用於生產環境，而應僅用於測試、評估和示範。</span><span class="sxs-lookup"><span data-stu-id="03b39-111">Azure Stack Development Kit must not be used as a production environment and should only be used for testing, evaluation, and demonstration.</span></span>  
* <span data-ttu-id="03b39-112">Azure Stack 的部署與單一 Azure Active Directory 或 Active Directory 同盟服務識別提供者相關聯。</span><span class="sxs-lookup"><span data-stu-id="03b39-112">Your deployment of Azure Stack is associated with a single Azure Active Directory or Active Directory Federation Services identity provider.</span></span> <span data-ttu-id="03b39-113">您可以在此目錄中建立多個使用者並指派訂閱 tooeach 使用者。</span><span class="sxs-lookup"><span data-stu-id="03b39-113">You can create multiple users in this directory and assign subscriptions tooeach user.</span></span>
* <span data-ttu-id="03b39-114">Hello 單一機器上部署的所有元件，有可用的實體資源有限的租用戶資源。</span><span class="sxs-lookup"><span data-stu-id="03b39-114">With all components deployed on hello single machine, there are limited physical resources available for tenant resources.</span></span> <span data-ttu-id="03b39-115">此設定不適合進行規模或效能評估。</span><span class="sxs-lookup"><span data-stu-id="03b39-115">This configuration is not intended for scale or performance evaluation.</span></span>
* <span data-ttu-id="03b39-116">網路狀況乃限制到期 toohello 單一的主機 NIC 的需求。</span><span class="sxs-lookup"><span data-stu-id="03b39-116">Networking scenarios are limited due toohello single host/NIC requirement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="03b39-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="03b39-117">Next steps</span></span>
[<span data-ttu-id="03b39-118">重要功能與概念</span><span class="sxs-lookup"><span data-stu-id="03b39-118">Key features and concepts</span></span>](azure-stack-key-features.md)

[<span data-ttu-id="03b39-119">使用 Azure 和 Azure Stack 的混合式應用程式創新 (pdf)</span><span class="sxs-lookup"><span data-stu-id="03b39-119">Hybrid Application innovation with Azure and Azure Stack (pdf)</span></span>](https://go.microsoft.com/fwlink/?LinkId=842846&clcid=0x409)

