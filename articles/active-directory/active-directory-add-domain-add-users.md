---
title: "Azure Active Directory 中的 aaaAssign 使用者 tooa 自訂網域 |Microsoft 文件"
description: "如何 toopopulate 自訂網域使用者帳戶與 Azure Active Directory 中。"
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
ms.openlocfilehash: 23c338a361a90fddf42d4df90db94c9774305886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="assign-users-tooa-custom-domain"></a><span data-ttu-id="9c36e-103">指派使用者 tooa 自訂網域</span><span class="sxs-lookup"><span data-stu-id="9c36e-103">Assign users tooa custom domain</span></span>
<span data-ttu-id="9c36e-104">加入您的自訂網域 tooAzure Active Directory 之後，您必須新增 hello 這個網域的使用者帳戶，以便您可以開始驗證它們。</span><span class="sxs-lookup"><span data-stu-id="9c36e-104">After you have added your custom domain tooAzure Active Directory, you must add hello user accounts for this domain so that you can begin authenticating them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9c36e-105">Microsoft 建議您管理 Azure AD 使用 hello [Azure AD 系統管理中心](https://aad.portal.azure.com)hello 在 Azure 入口網站，而不是使用 hello 這個文件中參考的 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="9c36e-105">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> <span data-ttu-id="9c36e-106">如何 toomanage 您的網域名稱在 hello Azure AD 系統管理中心，請參閱[管理您的 Azure Active Directory 中的自訂網域名稱](active-directory-domains-manage-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="9c36e-106">For how toomanage your domain names in hello Azure AD admin center, see [Managing custom domain names in your Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span></span>

## <a name="users-synced-from-a-on-premises-directory"></a><span data-ttu-id="9c36e-107">從內部部署目錄同步處理的使用者</span><span class="sxs-lookup"><span data-stu-id="9c36e-107">Users synced from a on-premises directory</span></span>
<span data-ttu-id="9c36e-108">如果您有已設定連線之間您內部部署 Active Directory 與 Azure Active Directory，同步處理可以填入 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="9c36e-108">If you have already set up a connection between your on-premises Active Directory and Azure Active Directory, synchronization can populate hello accounts.</span></span> <span data-ttu-id="9c36e-109">如需有關如何 toosynchronize Azure Active Directory 與您的內部部署 Active Directory，請參閱[整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="9c36e-109">For more information on how toosynchronize Azure Active Directory with your on-premises Active Directory, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

## <a name="users-added-and-managed-in-hello-cloud"></a><span data-ttu-id="9c36e-110">新增和管理 hello 雲端中的使用者</span><span class="sxs-lookup"><span data-stu-id="9c36e-110">Users added and managed in hello cloud</span></span>
<span data-ttu-id="9c36e-111">現有的使用者帳戶的 toochange hello 網域：</span><span class="sxs-lookup"><span data-stu-id="9c36e-111">toochange hello domain for an existing user account:</span></span>

1. <span data-ttu-id="9c36e-112">開啟 hello Azure 傳統入口網站使用的帳戶，是全域管理員或使用者的系統管理員。</span><span class="sxs-lookup"><span data-stu-id="9c36e-112">Open hello Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="9c36e-113">開啟您的目錄。</span><span class="sxs-lookup"><span data-stu-id="9c36e-113">Open your directory.</span></span>
3. <span data-ttu-id="9c36e-114">選取 hello**使用者** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="9c36e-114">Select hello **Users** tab.</span></span>
4. <span data-ttu-id="9c36e-115">Hello 清單中選取 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="9c36e-115">Select hello user from hello list.</span></span>
5. <span data-ttu-id="9c36e-116">變更 hello hello 使用者的網域，然後選取**儲存**。</span><span class="sxs-lookup"><span data-stu-id="9c36e-116">Change hello domain for hello user, and then select **Save**.</span></span>

<span data-ttu-id="9c36e-117">這還可以使用[Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)或 hello [Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)。</span><span class="sxs-lookup"><span data-stu-id="9c36e-117">This can also be done using [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) or hello [Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).</span></span>

## <a name="select-a-custom-domain-when-creating-a-new-user"></a><span data-ttu-id="9c36e-118">在建立新的使用者時選取自訂網域</span><span class="sxs-lookup"><span data-stu-id="9c36e-118">Select a custom domain when creating a new user</span></span>
1. <span data-ttu-id="9c36e-119">開啟 hello Azure 傳統入口網站使用的帳戶，是全域管理員或使用者的系統管理員。</span><span class="sxs-lookup"><span data-stu-id="9c36e-119">Open hello Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="9c36e-120">開啟您的目錄。</span><span class="sxs-lookup"><span data-stu-id="9c36e-120">Open your directory.</span></span>
3. <span data-ttu-id="9c36e-121">選取 hello**使用者** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="9c36e-121">Select hello **Users** tab.</span></span>
4. <span data-ttu-id="9c36e-122">Hello 命令列中，選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="9c36e-122">In hello command bar, select **Add**.</span></span>
5. <span data-ttu-id="9c36e-123">當您新增 hello 使用者名稱時，請從 hello 網域清單中選擇 hello 自訂網域。</span><span class="sxs-lookup"><span data-stu-id="9c36e-123">When you add hello user name, choose hello custom domain from hello domain list.</span></span>
6. <span data-ttu-id="9c36e-124">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="9c36e-124">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c36e-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9c36e-125">Next steps</span></span>
* [<span data-ttu-id="9c36e-126">為您的使用者使用自訂網域名稱 toosimplify hello 登入體驗</span><span class="sxs-lookup"><span data-stu-id="9c36e-126">Using custom domain names toosimplify hello sign-in experience for your users</span></span>](active-directory-add-domain.md)
* [<span data-ttu-id="9c36e-127">管理自訂網域名稱</span><span class="sxs-lookup"><span data-stu-id="9c36e-127">Manage custom domain names</span></span>](active-directory-add-manage-domain-names.md)
* [<span data-ttu-id="9c36e-128">了解 Azure AD 中的網域管理概念</span><span class="sxs-lookup"><span data-stu-id="9c36e-128">Learn about domain management concepts in Azure AD</span></span>](active-directory-add-domain-concepts.md)

