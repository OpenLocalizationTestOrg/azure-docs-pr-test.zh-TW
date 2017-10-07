---
title: "aaaHow tooperform 存取檢閱 |Microsoft 文件"
description: "了解如何檢閱的 tooperform hello Azure Privileged 的 Identity Management 的應用程式。"
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
ms.openlocfilehash: 301a5e9f97b68fedfbf4954e0bd7dadb7f0fc510
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="6235d-103">如何 tooperform 存取檢閱在 Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="6235d-103">How tooperform an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="6235d-104">Azure Active Directory (AD) 的權限身分管理可簡化企業如何管理 Azure AD 中的特殊權限的存取 tooresources 和 Office 365 或 Microsoft Intune 等其他 Microsoft online services。</span><span class="sxs-lookup"><span data-stu-id="6235d-104">Azure Active Directory (AD) Privileged Identity Management simplifies how enterprises manage privileged access tooresources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>  

<span data-ttu-id="6235d-105">如果您指派 tooan 系統管理角色，您組織的特殊權限的角色系統管理員可能會要求您 tooregularly 確認適用於您作業仍然需要該角色。</span><span class="sxs-lookup"><span data-stu-id="6235d-105">If you are assigned tooan administrative role, your organization's privileged role administrator may ask you tooregularly confirm that you still need that role for your job.</span></span> <span data-ttu-id="6235d-106">您可能會收到電子郵件，其中包含的連結，或者您可以移直線 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="6235d-106">You might get an email that includes a link, or you can go straight toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="6235d-107">請遵循自我檢閱您已指派的角色，此文章 tooperform hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="6235d-107">Follow hello steps in this article tooperform a self-review of your assigned roles.</span></span>

<span data-ttu-id="6235d-108">如果您想要存取檢閱的特殊權限的角色系統管理員，取得更多詳細資料，在[如何 toostart 存取檢閱](active-directory-privileged-identity-management-how-to-start-security-review.md)。</span><span class="sxs-lookup"><span data-stu-id="6235d-108">If you're a privileged role administrator interested in access reviews, get more details at [How toostart an access review](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span>

## <a name="add-hello-privileged-identity-management-application"></a><span data-ttu-id="6235d-109">新增 hello Privileged Identity Management 的應用程式</span><span class="sxs-lookup"><span data-stu-id="6235d-109">Add hello Privileged Identity Management application</span></span>
<span data-ttu-id="6235d-110">您可以使用 hello Azure AD Privileged Identity Management (PIM) 的應用程式中 hello [Azure 入口網站](https://portal.azure.com/)tooperform 您進行檢閱。</span><span class="sxs-lookup"><span data-stu-id="6235d-110">You can use hello Azure AD Privileged Identity Management (PIM) application in hello [Azure portal](https://portal.azure.com/) tooperform your review.</span></span>  <span data-ttu-id="6235d-111">如果您的入口網站上沒有 hello Azure AD Privileged Identity Management 的應用程式，請遵循啟動這些步驟 tooget。</span><span class="sxs-lookup"><span data-stu-id="6235d-111">If you don't have hello Azure AD Privileged Identity Management application on your portal, follow these steps tooget started.</span></span>

1. <span data-ttu-id="6235d-112">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="6235d-112">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="6235d-113">選取您在 hello 右上角的 hello Azure 入口網站，與您將您的選取 hello 目錄中的使用者名稱進行操作。</span><span class="sxs-lookup"><span data-stu-id="6235d-113">Select your username in hello upper right-hand corner of hello Azure portal, and select hello directory where you will you be operating.</span></span>
3. <span data-ttu-id="6235d-114">選取**更多服務**並用的 hello 篩選文字方塊中 toosearch **Azure AD Privileged Identity Management**。</span><span class="sxs-lookup"><span data-stu-id="6235d-114">Select **More services** and use hello Filter textbox toosearch for **Azure AD Privileged Identity Management**.</span></span>
4. <span data-ttu-id="6235d-115">請檢查**Pin toodashboard** ，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="6235d-115">Check **Pin toodashboard** and then click **Create**.</span></span> <span data-ttu-id="6235d-116">hello Privileged Identity Management 的應用程式將會開啟。</span><span class="sxs-lookup"><span data-stu-id="6235d-116">hello Privileged Identity Management application will open.</span></span>

## <a name="approve-or-deny-access"></a><span data-ttu-id="6235d-117">核准或拒絕存取</span><span class="sxs-lookup"><span data-stu-id="6235d-117">Approve or deny access</span></span>
<span data-ttu-id="6235d-118">當您核准或拒絕存取時，您只要告訴 hello 檢閱者您仍要使用此角色或不。</span><span class="sxs-lookup"><span data-stu-id="6235d-118">When you approve or deny access, you're just telling hello reviewer whether you still use this role or not.</span></span> <span data-ttu-id="6235d-119">選擇**核准**如果您想在 hello 角色 toostay 或**拒絕**如果您不需要再 hello 存取。</span><span class="sxs-lookup"><span data-stu-id="6235d-119">Choose **Approve** if you want toostay in hello role, or **Deny** if you don't need hello access anymore.</span></span> <span data-ttu-id="6235d-120">Hello 檢閱者套用 hello 結果之前，不會立即，變更您的狀態。</span><span class="sxs-lookup"><span data-stu-id="6235d-120">Your status won't change right away, until hello reviewer applies hello results.</span></span>
<span data-ttu-id="6235d-121">請依照這些步驟 toofind 並完成 hello 存取檢閱：</span><span class="sxs-lookup"><span data-stu-id="6235d-121">Follow these steps toofind and complete hello access review:</span></span>

1. <span data-ttu-id="6235d-122">在 hello PIM 應用程式中，選取 **檢閱特殊權限存取**。</span><span class="sxs-lookup"><span data-stu-id="6235d-122">In hello PIM application, select **Review privileged access**.</span></span> <span data-ttu-id="6235d-123">如果您有任何暫止存取檢閱，它們會出現在 hello Azure AD 存取檢閱 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="6235d-123">If you have any pending access reviews, they appear in hello Azure AD Access reviews blade.</span></span>
2. <span data-ttu-id="6235d-124">選取您想要 toocomplete hello 檢閱。</span><span class="sxs-lookup"><span data-stu-id="6235d-124">Select hello review you want toocomplete.</span></span>
3. <span data-ttu-id="6235d-125">除非您建立 hello 檢閱時，您可以顯示為 hello 只有 hello 檢閱中的使用者。</span><span class="sxs-lookup"><span data-stu-id="6235d-125">Unless you created hello review, you appear as hello only user in hello review.</span></span> <span data-ttu-id="6235d-126">選取 hello 核取記號和 tooyour 名稱下一步。</span><span class="sxs-lookup"><span data-stu-id="6235d-126">Select hello check mark next tooyour name.</span></span>
4. <span data-ttu-id="6235d-127">選擇 [核准] 或 [拒絕]。</span><span class="sxs-lookup"><span data-stu-id="6235d-127">Choose either **Approve** or **Deny**.</span></span> <span data-ttu-id="6235d-128">您可能需要在 hello 決策的原因 tooinclude**提供原因**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="6235d-128">You may need tooinclude a reason for your decision in hello **Provide a reason** text box.</span></span>  
5. <span data-ttu-id="6235d-129">關閉 hello**檢閱 Azure AD 角色**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="6235d-129">Close hello **Review Azure AD roles** blade.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="6235d-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6235d-130">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
