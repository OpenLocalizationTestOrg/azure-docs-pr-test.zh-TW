---
title: "Active Directory PoC 腳本食材 aaaAzure |Microsoft 文件"
description: "探索並快速實作身分識別和存取管理案例"
services: active-directory
keywords: "azure active directory, 腳本, 概念證明, PoC"
documentationcenter: 
author: dstefanMSFT
manager: asuthar
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/12/2017
ms.author: dstefan
ms.openlocfilehash: 0a7f5cd659b9d62ac86e3c27e5727294d481f4a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-ingredients"></a><span data-ttu-id="3d102-104">Azure Active Directory 概念證明腳本組成要素</span><span class="sxs-lookup"><span data-stu-id="3d102-104">Azure Active Directory Proof of Concept Playbook Ingredients</span></span> 

## <a name="theme"></a><span data-ttu-id="3d102-105">佈景主題</span><span class="sxs-lookup"><span data-stu-id="3d102-105">Theme</span></span>
<span data-ttu-id="3d102-106">Azure AD 提供身分識別和存取解決方案，跨 hello 企業中的多個區域。</span><span class="sxs-lookup"><span data-stu-id="3d102-106">Azure AD provides identity and access solutions across multiple areas in hello enterprise.</span></span> <span data-ttu-id="3d102-107">我們分類 hello 下列區域中的 hello 案例：</span><span class="sxs-lookup"><span data-stu-id="3d102-107">We classify hello scenarios in hello following areas:</span></span> 

* [<span data-ttu-id="3d102-108">許多應用程式、一個身分識別</span><span class="sxs-lookup"><span data-stu-id="3d102-108">Lots of apps, one identity</span></span>](active-directory-playbook-implementation.md#theme---lots-of-apps-one-identity) 
* [<span data-ttu-id="3d102-109">增加您的安全性</span><span class="sxs-lookup"><span data-stu-id="3d102-109">Increase your security</span></span>](active-directory-playbook-implementation.md#theme---increase-your-security) 
* [<span data-ttu-id="3d102-110">使用自助式縮放比例</span><span class="sxs-lookup"><span data-stu-id="3d102-110">Scale with Self Service</span></span>](active-directory-playbook-implementation.md#theme---scale-with-self-service) 

<span data-ttu-id="3d102-111">這定義佈景主題 tooframe hello PoC 有助於 toofocus hello 努力建立業務目標與共鳴，有時候是概念證明 hello 第一個位置中的 hello 感興趣的 hello 觸發程序。</span><span class="sxs-lookup"><span data-stu-id="3d102-111">Defining a theme tooframe hello PoC helps toofocus hello efforts that resonates with business goals, which oftentimes are hello triggers of hello interest in a proof of concept in hello first place.</span></span> 

## <a name="environment"></a><span data-ttu-id="3d102-112">Environment</span><span class="sxs-lookup"><span data-stu-id="3d102-112">Environment</span></span>

<span data-ttu-id="3d102-113">它是您將在其中傳送 hello PoC hello 環境的重要 toodetermine hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3d102-113">It is important toodetermine hello details of hello environment where you will deliver hello PoC.</span></span> <span data-ttu-id="3d102-114">在理想情況下可以建置它之後 hello PoC 完成。</span><span class="sxs-lookup"><span data-stu-id="3d102-114">Ideally you can build upon it after hello PoC is completed.</span></span> <span data-ttu-id="3d102-115">hello 目標環境很重要，而且您應該找到 hello 之間進行它為實際盡可能與條件約束或額外的考量 hello 成本的正確平衡。</span><span class="sxs-lookup"><span data-stu-id="3d102-115">hello target environment is crucial and you should find hello right balance between making it as real as possible and hello overhead of constraints or extra considerations.</span></span> <span data-ttu-id="3d102-116">hello PoCs 一般環境是：</span><span class="sxs-lookup"><span data-stu-id="3d102-116">hello typical environments for PoCs are:</span></span>
* <span data-ttu-id="3d102-117">**生產環境：** hello 案例會實作即時環境中和已部署 Microsoft 雲端服務 （生產 AD、 Office 365、 Azure AD 租用戶/SSO 解決方案）。</span><span class="sxs-lookup"><span data-stu-id="3d102-117">**Production:** hello scenarios will be implemented in your live environment and already deployed Microsoft Cloud services (production AD, Office 365, Azure AD tenant/SSO solution).</span></span> 
* <span data-ttu-id="3d102-118">**使用者接受度測試 (UAT)/開發環境︰**您擁有測試基礎結構 (平行 AD，並可能有 Azure AD 租用戶/SSO 解決方案) 與類似生產環境的測試資料。</span><span class="sxs-lookup"><span data-stu-id="3d102-118">**User Acceptance Test (UAT)/Dev environment:** You have test infrastructure (parallel AD and potentially Azure AD tenant/SSO solution) with test data that resembles production.</span></span> <span data-ttu-id="3d102-119">一般而言，hello 測試環境是跨多個專案共用 hello 企業中。</span><span class="sxs-lookup"><span data-stu-id="3d102-119">Typically, hello test environment is shared across multiple projects in hello enterprise.</span></span>

<span data-ttu-id="3d102-120">本指南中的大部分案例皆具有附加特質。</span><span class="sxs-lookup"><span data-stu-id="3d102-120">Most scenarios in this guide are additive in nature.</span></span> <span data-ttu-id="3d102-121">如此一來，他們可以部署在 hello 生產租用戶中而不會影響 hello PoC 外的使用者。</span><span class="sxs-lookup"><span data-stu-id="3d102-121">As a result, they can be deployed in hello production tenant without affecting users outside hello PoC.</span></span> <span data-ttu-id="3d102-122">在整份文件中，我們會指出哪些案例會對整個租用戶造成影響。</span><span class="sxs-lookup"><span data-stu-id="3d102-122">Throughout this document, we will be calling out which scenarios would have tenant-wide effect.</span></span> <span data-ttu-id="3d102-123">在這些情況下，您可能想 tooconsider 非生產環境。</span><span class="sxs-lookup"><span data-stu-id="3d102-123">In those cases, you might want tooconsider a non-production environment.</span></span> 


## <a name="target-users"></a><span data-ttu-id="3d102-124">目標使用者</span><span class="sxs-lookup"><span data-stu-id="3d102-124">Target Users</span></span>

<span data-ttu-id="3d102-125">它是使用者將要執行 hello 案例，尤其是當 hello 環境時，生產或測試重要 toodetermine hello 目標組。</span><span class="sxs-lookup"><span data-stu-id="3d102-125">It is important toodetermine hello target set of users that will exercise hello scenarios, especially when hello environment is production or test.</span></span> <span data-ttu-id="3d102-126">hello PoC 的目標使用者類別如下：</span><span class="sxs-lookup"><span data-stu-id="3d102-126">hello categories of target users for PoC are:</span></span>
* <span data-ttu-id="3d102-127">**試驗使用者：** hello 環境，將它們用於其天 tooday hello 帳戶搭配使用 hello 方案中的實際使用者的工作函式</span><span class="sxs-lookup"><span data-stu-id="3d102-127">**Pilot Users:** Real users in hello environment that will be using hello solution with hello account they use for their day tooday job functions</span></span>
* <span data-ttu-id="3d102-128">**測試使用者：**測試 hello 環境中建立的帳戶</span><span class="sxs-lookup"><span data-stu-id="3d102-128">**Test Users:** Test accounts created in hello environment</span></span> 

<span data-ttu-id="3d102-129">本指南中的大部分案例均可供試驗使用者進行練習。</span><span class="sxs-lookup"><span data-stu-id="3d102-129">Most scenarios in this guide can be exercised by pilot users.</span></span> <span data-ttu-id="3d102-130">在整份文件中，我們會視需要指出目標使用者的考量事項。</span><span class="sxs-lookup"><span data-stu-id="3d102-130">Throughout this document, we will be calling out target user considerations if needed.</span></span>


[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]