---
title: "在 Azure 中的存取 aaaUnderstanding 資源 |Microsoft 文件"
description: "本主題說明在 hello 中使用訂用帳戶系統管理員 toocontrol 資源存取相關的概念完整 Azure 入口網站"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
ms.assetid: 174f1706-b959-4230-9a75-bf651227ebf6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 06b9c4166bdea849faae67cae3146c6c278deb97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-resource-access-in-azure"></a><span data-ttu-id="caf50-103">了解 Azure 中的資源存取</span><span class="sxs-lookup"><span data-stu-id="caf50-103">Understanding resource access in Azure</span></span>
> [!IMPORTANT]
> <span data-ttu-id="caf50-104">Microsoft 建議您管理 Azure AD 使用 hello [Azure AD 系統管理中心](https://aad.portal.azure.com)hello 在 Azure 入口網站，而不是使用 hello 這個文件中參考的 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="caf50-104">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> <span data-ttu-id="caf50-105">hello Azure 入口網站提供[角色型存取控制](role-based-access-control-configure.md)因此可以更精確地管理 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="caf50-105">hello Azure portal provides [role-based access control](role-based-access-control-configure.md) so Azure resources can be managed more precisely.</span></span>
> 
> 

<span data-ttu-id="caf50-106">2013 年 10 月 hello Azure 傳統入口網站和服務管理 Api 與整合 Azure Active Directory 中順序 toolay hello 奠定改善管理存取 tooAzure 資源 hello 使用者經驗。</span><span class="sxs-lookup"><span data-stu-id="caf50-106">In October 2013, hello Azure classic portal and Service Management APIs were integrated with Azure Active Directory in order toolay hello groundwork for improving hello user experience for managing access tooAzure resources.</span></span> <span data-ttu-id="caf50-107">Azure Active Directory 已提供絕佳功能，例如使用者管理、內部部署目錄同步、Multi-Factor Authentication 和應用程式存取控制。</span><span class="sxs-lookup"><span data-stu-id="caf50-107">Azure Active Directory already provides great capabilities such as user management, on-premises directory sync, multi-factor authentication, and application access control.</span></span> <span data-ttu-id="caf50-108">當然，這些也應該能夠用於全面管理 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="caf50-108">Naturally, these should also be made available for managing Azure resources across-the-board.</span></span>

<span data-ttu-id="caf50-109">在 Azure 中從計費觀點著手的存取控制。</span><span class="sxs-lookup"><span data-stu-id="caf50-109">Access control in Azure starts from a billing perspective.</span></span> <span data-ttu-id="caf50-110">hello 擁有者的 Azure 帳戶，供造訪 hello [Azure 帳戶中心](https://account.windowsazure.com/subscriptions)，為 hello 帳戶系統管理員 (AA)。</span><span class="sxs-lookup"><span data-stu-id="caf50-110">hello owner of an Azure account, accessed by visiting hello  [Azure Accounts Center](https://account.windowsazure.com/subscriptions), is hello Account Administrator (AA).</span></span> <span data-ttu-id="caf50-111">訂用帳戶是帳單的容器，但也可做為安全性界限： 每個訂閱都有一個服務系統管理員 (SA)，可以加入、 移除和修改該訂用帳戶中的 Azure 資源使用 hello [Azure 傳統入口網站](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="caf50-111">Subscriptions are a container for billing, but they also act as a security boundary: each subscription has a Service Administrator (SA) who can add, remove, and modify Azure resources in that subscription by using hello [Azure classic portal](https://manage.windowsazure.com/).</span></span> <span data-ttu-id="caf50-112">新的訂閱 hello 預設 SA 為 hello AA、 但是 hello AA 可以變更 hello Azure 帳戶中心中的 hello SA。</span><span class="sxs-lookup"><span data-stu-id="caf50-112">hello default SA of a new subscription is hello AA, but hello AA can change hello SA in hello Azure Accounts Center.</span></span>

<br><br>![Azure 帳戶][1]

<span data-ttu-id="caf50-114">訂用帳戶也會與目錄產生關聯。</span><span class="sxs-lookup"><span data-stu-id="caf50-114">Subscriptions also have an association with a directory.</span></span> <span data-ttu-id="caf50-115">hello 目錄定義一組使用者。</span><span class="sxs-lookup"><span data-stu-id="caf50-115">hello directory defines a set of users.</span></span> <span data-ttu-id="caf50-116">這些可以是從 hello 工作或學校中建立 hello 目錄的使用者，或者可以是外部使用者 （也就是 Microsoft 帳戶）。</span><span class="sxs-lookup"><span data-stu-id="caf50-116">These can be users from hello work or school that created hello directory or they can be external users (that is, Microsoft Accounts).</span></span> <span data-ttu-id="caf50-117">訂用帳戶都可以存取已獲指派為服務系統管理員 (SA) 或共同管理員 (CA); 這些目錄使用者子集hello 只例外狀況是，由於傳統原因，Microsoft 帳戶 (先前稱為 Windows Live ID) 可以指派為 SA 或 CA 不需要出現在 hello 目錄中。</span><span class="sxs-lookup"><span data-stu-id="caf50-117">Subscriptions are accessible by a subset of those directory users who have been assigned as either Service Administrator (SA) or Co-Administrator (CA); hello only exception is that, for legacy reasons, Microsoft Accounts (formerly Windows Live ID) can be assigned as SA or CA without being present in hello directory.</span></span>

<br><br>![Azure 中的存取控制][2]

<span data-ttu-id="caf50-119">Hello Azure 傳統入口網站中的功能可讓登入使用 Microsoft 帳戶 toochange hello 目錄使用 hello 訂用帳戶相關聯的 SAs**編輯目錄**命令 hello **訂閱**頁面**設定**。</span><span class="sxs-lookup"><span data-stu-id="caf50-119">Functionality within hello Azure classic portal enables SAs that are signed in using a Microsoft Account toochange hello directory that a subscription is associated with by using hello **Edit Directory** command on hello **Subscriptions** page in **Settings**.</span></span> <span data-ttu-id="caf50-120">請注意這項作業有 hello 該訂用帳戶的存取控制的影響。</span><span class="sxs-lookup"><span data-stu-id="caf50-120">Note that this operation has implications on hello access control of that subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="caf50-121">hello**編輯目錄**中 hello Azure 傳統入口網站不使用 toousers 登入使用工作或學校帳戶，因為這些帳戶可以登入只有 toohello 目錄 toowhich 其所屬的命令。</span><span class="sxs-lookup"><span data-stu-id="caf50-121">hello **Edit Directory** command in hello Azure classic portal is not available toousers who are signed in using a work or school account because those accounts can sign in only toohello directory toowhich they belong.</span></span>
> 
> 

<br><br>![簡單的使用者登入流程][3]

<span data-ttu-id="caf50-123">在 hello 簡單的情況下，組織 （例如 Contoso) 將會強制執行計費和 hello 相同的訂用帳戶設定存取控制。</span><span class="sxs-lookup"><span data-stu-id="caf50-123">In hello simple case, an organization (such as Contoso) will enforce billing and access control across hello same set of subscriptions.</span></span> <span data-ttu-id="caf50-124">也就是說，hello 目錄是由單一 Azure 帳戶所擁有的相關聯的 toosubscriptions。</span><span class="sxs-lookup"><span data-stu-id="caf50-124">That is, hello directory is associated toosubscriptions that are owned by a single Azure Account.</span></span> <span data-ttu-id="caf50-125">成功登入 toohello Azure 傳統入口網站，使用者可以看到兩個集合的資源 （橙色 hello 上圖中所示）：</span><span class="sxs-lookup"><span data-stu-id="caf50-125">Upon successful login toohello Azure classic portal, users see two collections of resources (depicted in orange in hello previous illustration):</span></span>

* <span data-ttu-id="caf50-126">其使用者帳戶所在的目錄 (來自或加入為外部主體)。</span><span class="sxs-lookup"><span data-stu-id="caf50-126">Directories where their user account exists (sourced or added as a foreign principal).</span></span> <span data-ttu-id="caf50-127">請注意，用來登入該 hello 目錄不相關的 toothis 計算，因此無論您登入的地方，一律顯示您的目錄。</span><span class="sxs-lookup"><span data-stu-id="caf50-127">Note that hello directory used for login isn’t relevant toothis computation, so your directories will always be shown regardless of where you logged in.</span></span>
* <span data-ttu-id="caf50-128">資源的訂用帳戶，會與用來登入的 hello 目錄相關聯，並且其中 hello 使用者屬於可存取 （當他們是 SA 或 CA）。</span><span class="sxs-lookup"><span data-stu-id="caf50-128">Resources that are part of subscriptions that are associated with hello directory used for login AND which hello user can access (where they are an SA or CA).</span></span>

<br><br>![具有多個訂用帳戶和目錄的使用者][4]

<span data-ttu-id="caf50-130">具有跨多個目錄的使用者具有 hello 能力 tooswitch hello 目前內容 hello Azure 傳統入口網站使用 hello 訂用帳戶篩選。</span><span class="sxs-lookup"><span data-stu-id="caf50-130">Users with subscriptions across multiple directories have hello ability tooswitch hello current context of hello Azure classic portal by using hello subscription filter.</span></span> <span data-ttu-id="caf50-131">在 hello 過程中，這會導致不同的登入 tooa 不同的目錄，但是這是透過單一登入 (SSO)。</span><span class="sxs-lookup"><span data-stu-id="caf50-131">Under hello covers, this results in a separate login tooa different directory, but this is accomplished seamlessly using single sign-on (SSO).</span></span>

<span data-ttu-id="caf50-132">在訂用帳戶之間移動資源等作業，可能會因為訂用帳戶的這個單一目錄檢視而變得更加困難。</span><span class="sxs-lookup"><span data-stu-id="caf50-132">Operations such as moving resources between subscriptions can be more difficult as a result of this single directory view of subscriptions.</span></span> <span data-ttu-id="caf50-133">tooperform hello 資源傳輸時，您可能需要 toofirst 使用 hello**編輯目錄**命令在 hello 訂閱] 頁面中**設定**tooassociate hello 訂閱 toohello 相同的目錄.</span><span class="sxs-lookup"><span data-stu-id="caf50-133">tooperform hello resource transfer, it may be necessary toofirst use hello **Edit Directory** command on hello Subscriptions page in **Settings** tooassociate hello subscriptions toohello same directory.</span></span>

## <a name="next-steps"></a><span data-ttu-id="caf50-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="caf50-134">Next Steps</span></span>
* <span data-ttu-id="caf50-135">toolearn 深入了解如何 toochange 管理員 Azure 訂用帳戶，請參閱[如何 tooadd 或變更的 Azure 系統管理員角色](../billing/billing-add-change-azure-subscription-administrator.md)</span><span class="sxs-lookup"><span data-stu-id="caf50-135">toolearn more about how toochange administrators for an Azure subscription, see [How tooadd or change Azure administrator roles](../billing/billing-add-change-azure-subscription-administrator.md)</span></span>
* <span data-ttu-id="caf50-136">如需有關 Azure Active Directory 與 tooyour Azure 訂用帳戶的關聯方式的詳細資訊，請參閱[都與 Azure Active Directory 相關聯 Azure 訂用帳戶](active-directory-how-subscriptions-associated-directory.md)</span><span class="sxs-lookup"><span data-stu-id="caf50-136">For more information on how Azure Active Directory relates tooyour Azure subscription, see [How Azure subscriptions are associated with Azure Active Directory](active-directory-how-subscriptions-associated-directory.md)</span></span>
* <span data-ttu-id="caf50-137">如需有關如何 tooassign 角色在 Azure AD 中，請參閱[指派 Azure Active Directory 中的系統管理員角色](active-directory-assign-admin-roles.md)</span><span class="sxs-lookup"><span data-stu-id="caf50-137">For more information on how tooassign roles in Azure AD, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md)</span></span>

<!--Image references-->
[1]: ./media/active-directory-understanding-resource-access/IC707931.png
[2]: ./media/active-directory-understanding-resource-access/IC707932.png
[3]: ./media/active-directory-understanding-resource-access/IC707933.png
[4]: ./media/active-directory-understanding-resource-access/IC707934.png
