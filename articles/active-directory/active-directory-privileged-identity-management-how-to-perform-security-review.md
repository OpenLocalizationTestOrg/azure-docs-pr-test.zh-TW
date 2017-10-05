---
title: "如何執行存取權檢閱 | Microsoft Docs"
description: "了解如何使用 Azure Privileged Identity Management 應用程式來執行檢閱。"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 49ee2feb-7d2e-4acf-82c1-40ff23062862
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: a98ed60221eeba1d9c92df846aeae2deafb8ae60
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-perform-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="d6998-103">如何在 Azure AD Privileged Identity Management 中執行存取權檢閱</span><span class="sxs-lookup"><span data-stu-id="d6998-103">How to perform an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="d6998-104">Azure Active Directory (AD) Privileged Identity Management 簡化了企業管理以特殊權限身分存取 Azure AD 中的資源和其他 Microsoft 線上服務 (如 Office 365 或 Microsoft Intune) 的方式。</span><span class="sxs-lookup"><span data-stu-id="d6998-104">Azure Active Directory (AD) Privileged Identity Management simplifies how enterprises manage privileged access to resources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>  

<span data-ttu-id="d6998-105">如果您已被指派系統管理角色，貴組織的特殊權限角色管理員可能會要求您定期確認您仍需要該角色來執行作業。</span><span class="sxs-lookup"><span data-stu-id="d6998-105">If you are assigned to an administrative role, your organization's privileged role administrator may ask you to regularly confirm that you still need that role for your job.</span></span> <span data-ttu-id="d6998-106">您可能會收到包含連結的電子郵件，或請直接移至 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="d6998-106">You might get an email that includes a link, or you can go straight to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="d6998-107">請遵循本文中的步驟，執行獲指派角色的自我檢閱。</span><span class="sxs-lookup"><span data-stu-id="d6998-107">Follow the steps in this article to perform a self-review of your assigned roles.</span></span>

<span data-ttu-id="d6998-108">如果您是對存取權檢閱感興趣的特殊權限角色管理員，請在 [如何開始存取權檢閱](active-directory-privileged-identity-management-how-to-start-security-review.md)中取得更多詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="d6998-108">If you're a privileged role administrator interested in access reviews, get more details at [How to start an access review](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span>

## <a name="add-the-privileged-identity-management-application"></a><span data-ttu-id="d6998-109">加入 Privileged Identity Management 應用程式</span><span class="sxs-lookup"><span data-stu-id="d6998-109">Add the Privileged Identity Management application</span></span>
<span data-ttu-id="d6998-110">您可以使用 [Azure 入口網站](https://portal.azure.com/) 中的 Azure AD Privileged Identity Management (PIM) 應用程式來執行檢閱。</span><span class="sxs-lookup"><span data-stu-id="d6998-110">You can use the Azure AD Privileged Identity Management (PIM) application in the [Azure portal](https://portal.azure.com/) to perform your review.</span></span>  <span data-ttu-id="d6998-111">如果入口網站中沒有 Azure AD Privileged Identity Management 應用程式，請遵循這些步驟操作。</span><span class="sxs-lookup"><span data-stu-id="d6998-111">If you don't have the Azure AD Privileged Identity Management application on your portal, follow these steps to get started.</span></span>

1. <span data-ttu-id="d6998-112">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="d6998-112">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d6998-113">選取 Azure 入口網站右上角的使用者名稱，然後選取您要操作的目錄。</span><span class="sxs-lookup"><span data-stu-id="d6998-113">Select your username in the upper right-hand corner of the Azure portal, and select the directory where you will you be operating.</span></span>
3. <span data-ttu-id="d6998-114">選取 [更多服務] 並使用 [篩選器] 文字方塊來搜尋 [Azure AD Privileged Identity Management]。</span><span class="sxs-lookup"><span data-stu-id="d6998-114">Select **More services** and use the Filter textbox to search for **Azure AD Privileged Identity Management**.</span></span>
4. <span data-ttu-id="d6998-115">選取 [釘選到儀表板]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="d6998-115">Check **Pin to dashboard** and then click **Create**.</span></span> <span data-ttu-id="d6998-116">Privileged Identity Management 應用程式隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="d6998-116">The Privileged Identity Management application will open.</span></span>

## <a name="approve-or-deny-access"></a><span data-ttu-id="d6998-117">核准或拒絕存取</span><span class="sxs-lookup"><span data-stu-id="d6998-117">Approve or deny access</span></span>
<span data-ttu-id="d6998-118">當您核准或拒絕存取權時，只是在告訴檢閱者您是否仍然使用此角色。</span><span class="sxs-lookup"><span data-stu-id="d6998-118">When you approve or deny access, you're just telling the reviewer whether you still use this role or not.</span></span> <span data-ttu-id="d6998-119">如果您想要繼續擔任此角色，請選擇 [核准]，如果您不再需要此存取權，則請選擇 [拒絕]。</span><span class="sxs-lookup"><span data-stu-id="d6998-119">Choose **Approve** if you want to stay in the role, or **Deny** if you don't need the access anymore.</span></span> <span data-ttu-id="d6998-120">您的狀態不會立即變更，必須等到檢閱者套用結果之後才會變更。</span><span class="sxs-lookup"><span data-stu-id="d6998-120">Your status won't change right away, until the reviewer applies the results.</span></span>
<span data-ttu-id="d6998-121">請依照下列步驟來尋找並完成存取權檢閱︰</span><span class="sxs-lookup"><span data-stu-id="d6998-121">Follow these steps to find and complete the access review:</span></span>

1. <span data-ttu-id="d6998-122">在 PIM 應用程式中，選取 [檢閱特殊存取權限] 。</span><span class="sxs-lookup"><span data-stu-id="d6998-122">In the PIM application, select **Review privileged access**.</span></span> <span data-ttu-id="d6998-123">如果您有任何擱置中的存取權檢閱時，它們會顯示在 Azure AD 的 [存取權檢閱] 刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="d6998-123">If you have any pending access reviews, they appear in the Azure AD Access reviews blade.</span></span>
2. <span data-ttu-id="d6998-124">選取您想要完成的檢閱。</span><span class="sxs-lookup"><span data-stu-id="d6998-124">Select the review you want to complete.</span></span>
3. <span data-ttu-id="d6998-125">除非該檢閱是您所建立，否則您會顯示為該檢閱中的唯一使用者。</span><span class="sxs-lookup"><span data-stu-id="d6998-125">Unless you created the review, you appear as the only user in the review.</span></span> <span data-ttu-id="d6998-126">選取您名稱旁邊的核取記號。</span><span class="sxs-lookup"><span data-stu-id="d6998-126">Select the check mark next to your name.</span></span>
4. <span data-ttu-id="d6998-127">選擇 [核准] 或 [拒絕]。</span><span class="sxs-lookup"><span data-stu-id="d6998-127">Choose either **Approve** or **Deny**.</span></span> <span data-ttu-id="d6998-128">您可能需要在 [提供原因]  文字方塊中提供您的決定原因。</span><span class="sxs-lookup"><span data-stu-id="d6998-128">You may need to include a reason for your decision in the **Provide a reason** text box.</span></span>  
5. <span data-ttu-id="d6998-129">關閉 [檢閱 Azure AD 角色]  刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d6998-129">Close the **Review Azure AD roles** blade.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="d6998-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d6998-130">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
