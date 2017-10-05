---
title: "了解 Azure 中的資源存取 | Microsoft Docs"
description: "本主題說明有關使用訂用帳戶管理員來控制整個 Azure 入口網站中資源存取的概念"
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
ms.openlocfilehash: f1fda3c4192d0dae4fa60788f4d88fb72ddba4ad
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="understanding-resource-access-in-azure"></a><span data-ttu-id="ec1d6-103">了解 Azure 中的資源存取</span><span class="sxs-lookup"><span data-stu-id="ec1d6-103">Understanding resource access in Azure</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ec1d6-104">Microsoft 建議您使用 Azure 入口網站中的 [Azure AD 系統管理中心](https://aad.portal.azure.com)來管理 Azure AD，而不要使用本文所提及的 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="ec1d6-104">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> <span data-ttu-id="ec1d6-105">Azure 入口網站提供[角色型存取控制](role-based-access-control-configure.md)，因此可以更精確地管理 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="ec1d6-105">The Azure portal provides [role-based access control](role-based-access-control-configure.md) so Azure resources can be managed more precisely.</span></span>
> 
> 

<span data-ttu-id="ec1d6-106">為了針對改進使用者的 Azure 資源存取管理體驗奠下基礎，Azure 傳統入口網站和「服務管理」API 已在 2013 年 10 月與 Azure Active Directory 進行整合。</span><span class="sxs-lookup"><span data-stu-id="ec1d6-106">In October 2013, the Azure classic portal and Service Management APIs were integrated with Azure Active Directory in order to lay the groundwork for improving the user experience for managing access to Azure resources.</span></span> <span data-ttu-id="ec1d6-107">Azure Active Directory 已提供絕佳功能，例如使用者管理、內部部署目錄同步、Multi-Factor Authentication 和應用程式存取控制。</span><span class="sxs-lookup"><span data-stu-id="ec1d6-107">Azure Active Directory already provides great capabilities such as user management, on-premises directory sync, multi-factor authentication, and application access control.</span></span> <span data-ttu-id="ec1d6-108">當然，這些也應該能夠用於全面管理 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="ec1d6-108">Naturally, these should also be made available for managing Azure resources across-the-board.</span></span>

<span data-ttu-id="ec1d6-109">在 Azure 中從計費觀點著手的存取控制。</span><span class="sxs-lookup"><span data-stu-id="ec1d6-109">Access control in Azure starts from a billing perspective.</span></span> <span data-ttu-id="ec1d6-110">Azure 帳戶的擁有者 (藉由造訪 [Azure 帳戶中心](https://account.windowsazure.com/subscriptions)來存取) 為帳戶管理員 (AA)。</span><span class="sxs-lookup"><span data-stu-id="ec1d6-110">The owner of an Azure account, accessed by visiting the  [Azure Accounts Center](https://account.windowsazure.com/subscriptions), is the Account Administrator (AA).</span></span> <span data-ttu-id="ec1d6-111">訂用帳戶是計費容器，但它們也可做為安全性界限：每個訂用帳戶都有一個服務管理員 (SA)，此管理員可以使用 [Azure 傳統入口網站](https://manage.windowsazure.com/)來新增、移除及修改該訂用帳戶中的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="ec1d6-111">Subscriptions are a container for billing, but they also act as a security boundary: each subscription has a Service Administrator (SA) who can add, remove, and modify Azure resources in that subscription by using the [Azure classic portal](https://manage.windowsazure.com/).</span></span> <span data-ttu-id="ec1d6-112">新訂用帳戶的預設 SA 為 AA，但 AA 可以在 Azure 帳戶中心變更 SA。</span><span class="sxs-lookup"><span data-stu-id="ec1d6-112">The default SA of a new subscription is the AA, but the AA can change the SA in the Azure Accounts Center.</span></span>

<br><br>![Azure 帳戶][1]

<span data-ttu-id="ec1d6-114">訂用帳戶也會與目錄產生關聯。</span><span class="sxs-lookup"><span data-stu-id="ec1d6-114">Subscriptions also have an association with a directory.</span></span> <span data-ttu-id="ec1d6-115">目錄會定義一組使用者。</span><span class="sxs-lookup"><span data-stu-id="ec1d6-115">The directory defines a set of users.</span></span> <span data-ttu-id="ec1d6-116">他們可以是公司或學校中建立目錄的使用者，也可以是外部使用者 (也就是 Microsoft 帳戶)。</span><span class="sxs-lookup"><span data-stu-id="ec1d6-116">These can be users from the work or school that created the directory or they can be external users (that is, Microsoft Accounts).</span></span> <span data-ttu-id="ec1d6-117">訂用帳戶可供已被指派為服務管理員 (SA) 或共同管理員 (CA) 的某些目錄使用者存取；唯一的例外就是，由於舊版原因，Microsoft 帳戶 (先前稱為 Windows Live ID) 不需存在目錄中，即可被指派為 SA 或 CA。</span><span class="sxs-lookup"><span data-stu-id="ec1d6-117">Subscriptions are accessible by a subset of those directory users who have been assigned as either Service Administrator (SA) or Co-Administrator (CA); the only exception is that, for legacy reasons, Microsoft Accounts (formerly Windows Live ID) can be assigned as SA or CA without being present in the directory.</span></span>

<br><br>![Azure 中的存取控制][2]

<span data-ttu-id="ec1d6-119">Azure 傳統入口網站內的功能可讓使用 Microsoft 帳戶登入的 SA 變更訂用帳戶相關聯的目錄，方法是使用 [設定] 中的 [訂用帳戶] 頁面上的 [編輯目錄] 命令。</span><span class="sxs-lookup"><span data-stu-id="ec1d6-119">Functionality within the Azure classic portal enables SAs that are signed in using a Microsoft Account to change the directory that a subscription is associated with by using the **Edit Directory** command on the **Subscriptions** page in **Settings**.</span></span> <span data-ttu-id="ec1d6-120">請注意，此作業會影響該訂用帳戶的存取控制。</span><span class="sxs-lookup"><span data-stu-id="ec1d6-120">Note that this operation has implications on the access control of that subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="ec1d6-121">Azure 傳統入口網站中的 [編輯目錄] 命令不適用於使用公司或學校帳戶登入的使用者，因為這些帳戶只可以登入其所屬的目錄。</span><span class="sxs-lookup"><span data-stu-id="ec1d6-121">The **Edit Directory** command in the Azure classic portal is not available to users who are signed in using a work or school account because those accounts can sign in only to the directory to which they belong.</span></span>
> 
> 

<br><br>![簡單的使用者登入流程][3]

<span data-ttu-id="ec1d6-123">簡而言之，組織 (例如 Contoso) 將會強制執行同一組訂用帳戶的計費和存取控制。</span><span class="sxs-lookup"><span data-stu-id="ec1d6-123">In the simple case, an organization (such as Contoso) will enforce billing and access control across the same set of subscriptions.</span></span> <span data-ttu-id="ec1d6-124">也就是說，此目錄會與單一 Azure 帳戶所擁有的訂用帳戶相關聯。</span><span class="sxs-lookup"><span data-stu-id="ec1d6-124">That is, the directory is associated to subscriptions that are owned by a single Azure Account.</span></span> <span data-ttu-id="ec1d6-125">成功登入 Azure 傳統入口網站之後，使用者會看到兩個資源集合 (在上圖中以橘色表示)：</span><span class="sxs-lookup"><span data-stu-id="ec1d6-125">Upon successful login to the Azure classic portal, users see two collections of resources (depicted in orange in the previous illustration):</span></span>

* <span data-ttu-id="ec1d6-126">其使用者帳戶所在的目錄 (來自或加入為外部主體)。</span><span class="sxs-lookup"><span data-stu-id="ec1d6-126">Directories where their user account exists (sourced or added as a foreign principal).</span></span> <span data-ttu-id="ec1d6-127">請注意，用於登入的目錄與此計算無關，所以不論您在哪裡登入，一律會顯示您的目錄。</span><span class="sxs-lookup"><span data-stu-id="ec1d6-127">Note that the directory used for login isn’t relevant to this computation, so your directories will always be shown regardless of where you logged in.</span></span>
* <span data-ttu-id="ec1d6-128">屬於訂用帳戶的資源，而這些訂用帳戶會與用來登入且使用者可以存取的目錄 (他們是 SA 或 CA) 相關聯。</span><span class="sxs-lookup"><span data-stu-id="ec1d6-128">Resources that are part of subscriptions that are associated with the directory used for login AND which the user can access (where they are an SA or CA).</span></span>

<br><br>![具有多個訂用帳戶和目錄的使用者][4]

<span data-ttu-id="ec1d6-130">具有跨多個目錄之訂用帳戶的使用者能夠使用訂用帳戶篩選，來切換 Azure 傳統入口網站的目前內容。</span><span class="sxs-lookup"><span data-stu-id="ec1d6-130">Users with subscriptions across multiple directories have the ability to switch the current context of the Azure classic portal by using the subscription filter.</span></span> <span data-ttu-id="ec1d6-131">實際上，這會導致個別登入到不同的目錄，但卻是使用單一登入 (SSO) 順利完成的。</span><span class="sxs-lookup"><span data-stu-id="ec1d6-131">Under the covers, this results in a separate login to a different directory, but this is accomplished seamlessly using single sign-on (SSO).</span></span>

<span data-ttu-id="ec1d6-132">在訂用帳戶之間移動資源等作業，可能會因為訂用帳戶的這個單一目錄檢視而變得更加困難。</span><span class="sxs-lookup"><span data-stu-id="ec1d6-132">Operations such as moving resources between subscriptions can be more difficult as a result of this single directory view of subscriptions.</span></span> <span data-ttu-id="ec1d6-133">若要執行資源移轉，可能需要先在 [設定] 中的 [訂用帳戶] 頁面使用 [編輯目錄] 命令，將訂用帳戶關聯到相同的目錄。</span><span class="sxs-lookup"><span data-stu-id="ec1d6-133">To perform the resource transfer, it may be necessary to first use the **Edit Directory** command on the Subscriptions page in **Settings** to associate the subscriptions to the same directory.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec1d6-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ec1d6-134">Next Steps</span></span>
* <span data-ttu-id="ec1d6-135">若要深入了解如何變更 Azure 訂用帳戶的管理員，請參閱 [如何新增或變更 Azure 管理員角色](../billing/billing-add-change-azure-subscription-administrator.md)</span><span class="sxs-lookup"><span data-stu-id="ec1d6-135">To learn more about how to change administrators for an Azure subscription, see [How to add or change Azure administrator roles](../billing/billing-add-change-azure-subscription-administrator.md)</span></span>
* <span data-ttu-id="ec1d6-136">如需有關 Azure Active Directory 與您的 Azure 訂用帳戶產生關聯之方式的詳細資訊，請參閱 [Azure 訂用帳戶如何與 Azure Active Directory 產生關聯](active-directory-how-subscriptions-associated-directory.md)</span><span class="sxs-lookup"><span data-stu-id="ec1d6-136">For more information on how Azure Active Directory relates to your Azure subscription, see [How Azure subscriptions are associated with Azure Active Directory](active-directory-how-subscriptions-associated-directory.md)</span></span>
* <span data-ttu-id="ec1d6-137">如需有關如何在 Azure AD 中指派角色的詳細資訊，請參閱 [在 Azure Active Directory 中指派系統管理員角色](active-directory-assign-admin-roles.md)</span><span class="sxs-lookup"><span data-stu-id="ec1d6-137">For more information on how to assign roles in Azure AD, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md)</span></span>

<!--Image references-->
[1]: ./media/active-directory-understanding-resource-access/IC707931.png
[2]: ./media/active-directory-understanding-resource-access/IC707932.png
[3]: ./media/active-directory-understanding-resource-access/IC707933.png
[4]: ./media/active-directory-understanding-resource-access/IC707934.png
