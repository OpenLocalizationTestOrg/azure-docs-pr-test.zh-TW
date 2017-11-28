---
title: "aaaB2B 共同作業的使用者宣告的 Azure Active Directory 中的對應 |Microsoft 文件"
description: "Azure Active Directory B2B 共同作業的宣告對應參考資料"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 03/15/2017
ms.author: sasubram
ms.openlocfilehash: 9e26085e91a6004b2f11286ae9c1df133bd47341
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="b2b-collaboration-user-claims-mapping-in-azure-active-directory"></a><span data-ttu-id="6bf35-103">Azure Active Directory 中的 B2B 共同作業使用者宣告對應</span><span class="sxs-lookup"><span data-stu-id="6bf35-103">B2B collaboration user claims mapping in Azure Active Directory</span></span>

<span data-ttu-id="6bf35-104">Azure Active Directory (Azure AD) 支援自訂 hello hello B2B 共同作業的使用者的 SAML 權杖中發出的宣告。</span><span class="sxs-lookup"><span data-stu-id="6bf35-104">Azure Active Directory (Azure AD) supports customizing hello claims issued in hello SAML token for B2B collaboration users.</span></span> <span data-ttu-id="6bf35-105">當使用者驗證 toohello 應用程式時，Azure AD 會發出 hello 使用者可唯一識別它們的相關資訊 （或宣告） 包含的 SAML 權杖 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6bf35-105">When a user authenticates toohello application, Azure AD issues a SAML token toohello app that contains information (or claims) about hello user that uniquely identifies them.</span></span> <span data-ttu-id="6bf35-106">根據預設，這包括 hello 使用者的使用者名稱、 電子郵件地址、 名字和姓氏。</span><span class="sxs-lookup"><span data-stu-id="6bf35-106">By default, this includes hello user's user name, email address, first name, and last name.</span></span> <span data-ttu-id="6bf35-107">您可以檢視或編輯傳送嗨 hello 屬性] 索引標籤下的 SAML 權杖 toohello 應用程式中的 hello 宣告。</span><span class="sxs-lookup"><span data-stu-id="6bf35-107">You can view or edit hello claims sent in hello SAML token toohello application under hello Attributes tab.</span></span>

<span data-ttu-id="6bf35-108">有兩個可能的原因為何，您可能需要在 hello SAML 權杖中發出的 tooedit hello 宣告。</span><span class="sxs-lookup"><span data-stu-id="6bf35-108">There are two possible reasons why you might need tooedit hello claims issued in hello SAML token.</span></span>

1. <span data-ttu-id="6bf35-109">已寫入 hello 應用程式 toorequire 用不同的宣告的 Uri 設定，或宣告值</span><span class="sxs-lookup"><span data-stu-id="6bf35-109">hello application has been written toorequire a different set of claim URIs or claim values</span></span>

2. <span data-ttu-id="6bf35-110">您的應用程式需要 hello NameIdentifier 宣告 toobe hello 使用者主體名稱儲存在 Azure Active Directory 以外的項目。</span><span class="sxs-lookup"><span data-stu-id="6bf35-110">Your application requires hello NameIdentifier claim toobe something other than hello user principal name stored in Azure Active Directory.</span></span>

  ![檢視 SAML 權杖中的宣告](media/active-directory-b2b-claims-mapping/view-claims-in-saml-token.png)

<span data-ttu-id="6bf35-112">如 tooadd 和編輯的宣告資訊，請參閱這篇文章上宣告自訂[自訂預先整合的應用程式在 Azure Active Directory 中的 hello SAML 權杖中發出的宣告](develop/active-directory-saml-claims-customization.md)。</span><span class="sxs-lookup"><span data-stu-id="6bf35-112">For information on how tooadd and edit claims, check out this article on claims customization, [Customizing claims issued in hello SAML token for pre-integrated apps in Azure Active Directory](develop/active-directory-saml-claims-customization.md).</span></span> <span data-ttu-id="6bf35-113">對於 B2B 共同作業使用者，基於安全性原因，系統會防止對應 NameID 與 UPN 跨租用戶。</span><span class="sxs-lookup"><span data-stu-id="6bf35-113">For B2B collaboration users, mapping NameID and UPN cross-tenant are prevented for security reasons.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6bf35-114">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6bf35-114">Next steps</span></span>

<span data-ttu-id="6bf35-115">請瀏覽有關 Azure AD B2B 共同作業的其他文章：</span><span class="sxs-lookup"><span data-stu-id="6bf35-115">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="6bf35-116">何謂 Azure AD B2B 共同作業？</span><span class="sxs-lookup"><span data-stu-id="6bf35-116">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="6bf35-117">B2B 共同作業使用者屬性</span><span class="sxs-lookup"><span data-stu-id="6bf35-117">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="6bf35-118">新增 B2B 共同作業使用者 tooa 角色</span><span class="sxs-lookup"><span data-stu-id="6bf35-118">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="6bf35-119">委派 B2B 共同作業邀請</span><span class="sxs-lookup"><span data-stu-id="6bf35-119">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="6bf35-120">動態群組與 B2B 共同作業</span><span class="sxs-lookup"><span data-stu-id="6bf35-120">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="6bf35-121">B2B 共同作業程式碼與 PowerShell 範例</span><span class="sxs-lookup"><span data-stu-id="6bf35-121">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="6bf35-122">設定適用於 B2B 共同作業的 SaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="6bf35-122">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="6bf35-123">Office 365 外部共用</span><span class="sxs-lookup"><span data-stu-id="6bf35-123">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="6bf35-124">B2B 共同作業使用者權杖</span><span class="sxs-lookup"><span data-stu-id="6bf35-124">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="6bf35-125">B2B 共同作業目前的限制</span><span class="sxs-lookup"><span data-stu-id="6bf35-125">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
