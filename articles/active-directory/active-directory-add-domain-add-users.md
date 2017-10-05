---
title: "將使用者指派給 Azure Active Directory 中的自訂網域 | Microsoft Docs"
description: "如何在 Azure Active Directory 中的自訂網域填入使用者帳戶。"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 717b5a7c-7bc3-4ab1-98b5-4740b53338fe
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 39cb54a6637088c35c6aef864a804c24803f48ba
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="assign-users-to-a-custom-domain"></a><span data-ttu-id="9fec2-103">將使用者指派至自訂網域</span><span class="sxs-lookup"><span data-stu-id="9fec2-103">Assign users to a custom domain</span></span>
<span data-ttu-id="9fec2-104">在您將您的自訂網域新增至 Azure Active Directory 之後，您必須加入此網域的使用者帳戶，以便開始驗證它們。</span><span class="sxs-lookup"><span data-stu-id="9fec2-104">After you have added your custom domain to Azure Active Directory, you must add the user accounts for this domain so that you can begin authenticating them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9fec2-105">Microsoft 建議您使用 Azure 入口網站中的 [Azure AD 系統管理中心](https://aad.portal.azure.com)來管理 Azure AD，而不要使用本文所提及的 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="9fec2-105">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> <span data-ttu-id="9fec2-106">如需如何在 Azure AD 系統管理中心管理網域名稱的相關資訊，請參閱[在 Azure Active Directory 中管理自訂網域名稱](active-directory-domains-manage-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="9fec2-106">For how to manage your domain names in the Azure AD admin center, see [Managing custom domain names in your Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span></span>

## <a name="users-synced-from-a-on-premises-directory"></a><span data-ttu-id="9fec2-107">從內部部署目錄同步處理的使用者</span><span class="sxs-lookup"><span data-stu-id="9fec2-107">Users synced from a on-premises directory</span></span>
<span data-ttu-id="9fec2-108">如果您已經設定內部部署 Active Directory 與 Azure Active Directory 之間的連線，同步處理可以填入帳戶。</span><span class="sxs-lookup"><span data-stu-id="9fec2-108">If you have already set up a connection between your on-premises Active Directory and Azure Active Directory, synchronization can populate the accounts.</span></span> <span data-ttu-id="9fec2-109">如需有關如何同步處理 Azure Active Directory 與內部部署 Active Directory 的詳細資訊，請參閱 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="9fec2-109">For more information on how to synchronize Azure Active Directory with your on-premises Active Directory, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

## <a name="users-added-and-managed-in-the-cloud"></a><span data-ttu-id="9fec2-110">新增和管理雲端中的使用者</span><span class="sxs-lookup"><span data-stu-id="9fec2-110">Users added and managed in the cloud</span></span>
<span data-ttu-id="9fec2-111">若要變更現有使用者帳戶的網域：</span><span class="sxs-lookup"><span data-stu-id="9fec2-111">To change the domain for an existing user account:</span></span>

1. <span data-ttu-id="9fec2-112">使用全域管理員或使用者管理員帳戶開啟 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="9fec2-112">Open the Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="9fec2-113">開啟您的目錄。</span><span class="sxs-lookup"><span data-stu-id="9fec2-113">Open your directory.</span></span>
3. <span data-ttu-id="9fec2-114">選取 [使用者]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="9fec2-114">Select the **Users** tab.</span></span>
4. <span data-ttu-id="9fec2-115">從清單中選取使用者。</span><span class="sxs-lookup"><span data-stu-id="9fec2-115">Select the user from the list.</span></span>
5. <span data-ttu-id="9fec2-116">變更使用者的網域，然後選取 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="9fec2-116">Change the domain for the user, and then select **Save**.</span></span>

<span data-ttu-id="9fec2-117">使用 [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) 或 [Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations) 也可以完成此操作。</span><span class="sxs-lookup"><span data-stu-id="9fec2-117">This can also be done using [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) or the [Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).</span></span>

## <a name="select-a-custom-domain-when-creating-a-new-user"></a><span data-ttu-id="9fec2-118">在建立新的使用者時選取自訂網域</span><span class="sxs-lookup"><span data-stu-id="9fec2-118">Select a custom domain when creating a new user</span></span>
1. <span data-ttu-id="9fec2-119">使用全域管理員或使用者管理員帳戶開啟 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="9fec2-119">Open the Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="9fec2-120">開啟您的目錄。</span><span class="sxs-lookup"><span data-stu-id="9fec2-120">Open your directory.</span></span>
3. <span data-ttu-id="9fec2-121">選取 [使用者]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="9fec2-121">Select the **Users** tab.</span></span>
4. <span data-ttu-id="9fec2-122">在命令列上選取 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="9fec2-122">In the command bar, select **Add**.</span></span>
5. <span data-ttu-id="9fec2-123">當您新增使用者名稱時，請從網域清單中選擇自訂網域。</span><span class="sxs-lookup"><span data-stu-id="9fec2-123">When you add the user name, choose the custom domain from the domain list.</span></span>
6. <span data-ttu-id="9fec2-124">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="9fec2-124">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9fec2-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9fec2-125">Next steps</span></span>
* [<span data-ttu-id="9fec2-126">使用自訂網域名稱，以簡化您的使用者的登入體驗</span><span class="sxs-lookup"><span data-stu-id="9fec2-126">Using custom domain names to simplify the sign-in experience for your users</span></span>](active-directory-add-domain.md)
* [<span data-ttu-id="9fec2-127">管理自訂網域名稱</span><span class="sxs-lookup"><span data-stu-id="9fec2-127">Manage custom domain names</span></span>](active-directory-add-manage-domain-names.md)
* [<span data-ttu-id="9fec2-128">了解 Azure AD 中的網域管理概念</span><span class="sxs-lookup"><span data-stu-id="9fec2-128">Learn about domain management concepts in Azure AD</span></span>](active-directory-add-domain-concepts.md)

