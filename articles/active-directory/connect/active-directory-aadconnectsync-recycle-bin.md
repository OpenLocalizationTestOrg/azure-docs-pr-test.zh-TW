---
title: "Azure AD Connect 同步處理︰啟用 AD 資源回收筒 | Microsoft Docs"
description: "本主題建議 hello 使用 Azure AD Connect 與 AD 資源回收筒功能。"
services: active-directory
keywords: "AD 資源回收筒, 意外刪除, 來源錨點"
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: afec4207-74f7-4cdd-b13a-574af5223a90
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 2bb4827d677ccecfd8d2861f2a2fcf73b8cc2d95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-enable-ad-recycle-bin"></a><span data-ttu-id="49565-104">Azure AD Connect 同步處理︰啟用 AD 資源回收筒</span><span class="sxs-lookup"><span data-stu-id="49565-104">Azure AD Connect sync: Enable AD recycle bin</span></span>
<span data-ttu-id="49565-105">建議您針對在內部部署 Active 目錄，也就是已同步處理的 tooAzure AD 啟用 hello AD 資源回收筒功能。</span><span class="sxs-lookup"><span data-stu-id="49565-105">It is recommended that you enable hello AD Recycle Bin feature for your on-premises Active Directories, which are synchronized tooAzure AD.</span></span> 

<span data-ttu-id="49565-106">如果您不小心刪除了內部部署 AD 使用者物件與它使用 hello 功能，Azure AD 會還原 hello 對應的 Azure AD 使用者物件的還原。</span><span class="sxs-lookup"><span data-stu-id="49565-106">If you accidentally deleted an on-premises AD user object and restore it using hello feature, Azure AD restores hello corresponding Azure AD user object.</span></span>  <span data-ttu-id="49565-107">Hello AD 資源回收筒功能的相關資訊，請參閱 tooarticle[還原刪除的 Active Directory 物件的案例概觀](https://technet.microsoft.com/library/dd379542.aspx)。</span><span class="sxs-lookup"><span data-stu-id="49565-107">For information about hello AD Recycle Bin feature, refer tooarticle [Scenario Overview for Restoring Deleted Active Directory Objects](https://technet.microsoft.com/library/dd379542.aspx).</span></span>

## <a name="benefits-of-enabling-hello-ad-recycle-bin"></a><span data-ttu-id="49565-108">優點啟用 hello AD 資源回收筒</span><span class="sxs-lookup"><span data-stu-id="49565-108">Benefits of enabling hello AD recycle bin</span></span>
<span data-ttu-id="49565-109">這項功能可協助執行 hello 下列還原 Azure AD 使用者物件：</span><span class="sxs-lookup"><span data-stu-id="49565-109">This feature helps with restoring Azure AD user objects by doing hello following:</span></span>

* <span data-ttu-id="49565-110">如果您不小心刪除了內部部署 AD 使用者物件、 hello 對應的 Azure AD 使用者物件將會在刪除 hello 下一個同步處理循環。</span><span class="sxs-lookup"><span data-stu-id="49565-110">If you accidentally deleted an on-premises AD user object, hello corresponding Azure AD user object will be deleted in hello next sync cycle.</span></span> <span data-ttu-id="49565-111">根據預設，Azure AD 會保留 hello 刪除 Azure AD 使用者物件，處於虛刪除狀態 30 天的時間。</span><span class="sxs-lookup"><span data-stu-id="49565-111">By default, Azure AD keeps hello deleted Azure AD user object in soft-deleted state for 30 days.</span></span>

* <span data-ttu-id="49565-112">如果您有內部啟用的 AD 資源回收筒功能，您可以還原已刪除的 hello 內部部署 AD 使用者物件而不需要變更其來源錨點值。</span><span class="sxs-lookup"><span data-stu-id="49565-112">If you have on-premises AD Recycle Bin feature enabled, you can restore hello deleted on-premises AD user object without changing its Source Anchor value.</span></span> <span data-ttu-id="49565-113">當 hello 復原在內部部署同步處理 AD 使用者物件 tooAzure AD，Azure AD 將會還原 hello 對應虛刪除 Azure AD 使用者物件。</span><span class="sxs-lookup"><span data-stu-id="49565-113">When hello recovered on-premises AD user object is synchronized tooAzure AD, Azure AD will restore hello corresponding soft-deleted Azure AD user object.</span></span> <span data-ttu-id="49565-114">來源錨點屬性的相關資訊，請參閱 tooarticle [Azure AD Connect： 設計概念](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor)。</span><span class="sxs-lookup"><span data-stu-id="49565-114">For information about Source Anchor attribute, refer tooarticle [Azure AD Connect: Design concepts](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).</span></span>

* <span data-ttu-id="49565-115">如果您不需要在內部部署 AD 資源回收筒功能已啟用，您可能需要的 toocreate 的 AD 使用者物件 tooreplace hello 已刪除物件。</span><span class="sxs-lookup"><span data-stu-id="49565-115">If you do not have on-premises AD Recycle Bin feature enabled, you may be required toocreate an AD user object tooreplace hello deleted object.</span></span> <span data-ttu-id="49565-116">如果 Azure AD Connect 同步處理服務設定的 toouse 系統產生 AD 屬性 （例如 ObjectGuid) hello 來源錨點屬性，hello 新建立的 AD 使用者物件將不具有 hello 相同的來源錨點值為 hello 刪除 AD 使用者物件。</span><span class="sxs-lookup"><span data-stu-id="49565-116">If Azure AD Connect Synchronization Service is configured toouse system-generated AD attribute (such as ObjectGuid) for hello Source Anchor attribute, hello newly created AD user object will not have hello same Source Anchor value as hello deleted AD user object.</span></span> <span data-ttu-id="49565-117">當 hello 新建立的 AD 使用者物件同步處理的 tooAzure AD，Azure AD 會建立新的 Azure AD 使用者物件，而不是還原 hello 虛刪除 Azure AD 使用者物件。</span><span class="sxs-lookup"><span data-stu-id="49565-117">When hello newly created AD user object is synchronized tooAzure AD, Azure AD creates a new Azure AD user object instead of restoring hello soft-deleted Azure AD user object.</span></span>

> [!NOTE]
> <span data-ttu-id="49565-118">根據預設，Azure AD 會讓已刪除的 Azure AD 使用者物件保持 30 天的虛刪除狀態，再將其永久刪除。</span><span class="sxs-lookup"><span data-stu-id="49565-118">By default, Azure AD keeps deleted Azure AD user objects in soft-deleted state for 30 days before they are permanently deleted.</span></span> <span data-ttu-id="49565-119">不過，系統管理員可以加速 hello 刪除這類物件。</span><span class="sxs-lookup"><span data-stu-id="49565-119">However, administrators can accelerate hello deletion of such objects.</span></span> <span data-ttu-id="49565-120">一旦 hello 物件會永久刪除，就無法再復原，即使在內部部署 AD 資源回收筒功能已啟用。</span><span class="sxs-lookup"><span data-stu-id="49565-120">Once hello objects are permanently deleted, they can no longer be recovered, even if on-premises AD Recycle Bin feature is enabled.</span></span>



## <a name="next-steps"></a><span data-ttu-id="49565-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="49565-121">Next steps</span></span>
<span data-ttu-id="49565-122">**概觀主題**</span><span class="sxs-lookup"><span data-stu-id="49565-122">**Overview topics**</span></span>

* [<span data-ttu-id="49565-123">Azure AD Connect 同步處理：了解及自訂同步處理</span><span class="sxs-lookup"><span data-stu-id="49565-123">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="49565-124">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="49565-124">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
