---
title: "aaaCompare B2B 共同作業和在 Azure Active Directory B2C |Microsoft 文件"
description: "Hello Azure Active Directory B2B 共同作業和 Azure AD B2C 之間的差異為何？"
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
ms.openlocfilehash: 34d88b9a7d023e077568e8df3d5e1610ae05b361
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="compare-b2b-collaboration-and-b2c-in-azure-active-directory"></a><span data-ttu-id="55416-103">比較 Azure Active Directory 的 B2B 共同作業和 B2C</span><span class="sxs-lookup"><span data-stu-id="55416-103">Compare B2B collaboration and B2C in Azure Active Directory</span></span>

<span data-ttu-id="55416-104">Azure Active Directory (Azure AD) B2B 共同作業和 Azure AD B2C 可讓您與外部使用者 toowork 在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="55416-104">Both Azure Active Directory (Azure AD) B2B collaboration and Azure AD B2C allow you toowork with external users in Azure AD.</span></span> <span data-ttu-id="55416-105">但它們究竟差在哪兒？</span><span class="sxs-lookup"><span data-stu-id="55416-105">But how do they compare?</span></span>


<span data-ttu-id="55416-106">B2B 共同作業</span><span class="sxs-lookup"><span data-stu-id="55416-106">B2B collaboration capabilities</span></span> |     <span data-ttu-id="55416-107">Azure AD B2C 獨立供應項目</span><span class="sxs-lookup"><span data-stu-id="55416-107">Azure AD B2C stand-alone offering</span></span>
-------- | --------
<span data-ttu-id="55416-108">適用於： 想要從夥伴組織，不論身分識別提供者的 toobe 無法 tooauthenticate 使用者的組織。</span><span class="sxs-lookup"><span data-stu-id="55416-108">Intended for: Organizations that want toobe able tooauthenticate users from a partner organization, regardless of identity provider.</span></span> | <span data-ttu-id="55416-109">適用於︰邀請您的行動和 Web 應用程式的客戶 (無論是個人、機構或組織客戶) 加入您的 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="55416-109">Intended for: Inviting customers of your mobile and web apps, whether individuals, institutional or organizational customers into your Azure AD.</span></span>
<span data-ttu-id="55416-110">支援的身分識別︰本機有工作或學校帳戶的員工、本機有工作或學校帳戶的合作夥伴、或任何電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="55416-110">Identities supported: Employees with work or school accounts, partners with work or school accounts, or any email address.</span></span> <span data-ttu-id="55416-111">推出 toosupport 直接聯盟。</span><span class="sxs-lookup"><span data-stu-id="55416-111">Soon toosupport direct federation.</span></span>  | <span data-ttu-id="55416-112">支援的身分識別︰具有本機應用程式帳戶的取用者使用者 (任何電子郵件地址或使用者名稱) 或任何以直接聯盟支援的社交身分識別。</span><span class="sxs-lookup"><span data-stu-id="55416-112">Identities supported: Consumer users with local application accounts (any email address or user name) or any supported social identity with direct federation.</span></span>
<span data-ttu-id="55416-113">中有哪些目錄 hello 合作夥伴使用者： hello 外部組織的使用者中受管理的夥伴特別 hello 與員工，但註解式相同的目錄。</span><span class="sxs-lookup"><span data-stu-id="55416-113">Which directory hello partner users are in: Partner users from hello external organization are managed in hello same directory as employees, but annotated specially.</span></span> <span data-ttu-id="55416-114">它們可以受到管理 hello 相同方式成為員工，可以是相同的群組加入的 toohello 等等</span><span class="sxs-lookup"><span data-stu-id="55416-114">They can be managed hello same way as employees, can be added toohello same groups, and so on</span></span>  | <span data-ttu-id="55416-115">中有哪些目錄 hello 客戶使用者實體： hello 應用程式目錄中。</span><span class="sxs-lookup"><span data-stu-id="55416-115">Which directory hello customer user entities are in: In hello application directory.</span></span> <span data-ttu-id="55416-116">分開管理 hello 組織的員工和合作夥伴目錄 （如果有的話。</span><span class="sxs-lookup"><span data-stu-id="55416-116">Managed separately from hello organization’s employee and partner directory (if any.</span></span>
<span data-ttu-id="55416-117">單一登入 (SSO) tooall Azure AD 連接應用程式的支援。</span><span class="sxs-lookup"><span data-stu-id="55416-117">Single sign-on (SSO) tooall Azure AD-connected apps is supported.</span></span> <span data-ttu-id="55416-118">例如，您可以提供存取 tooOffice 365 或內部部署應用程式，而且 tooother SaaS 應用程式，例如 Salesforce 或工作日。</span><span class="sxs-lookup"><span data-stu-id="55416-118">For example, you can provide access tooOffice 365 or on-premises apps, and tooother SaaS apps such as Salesforce or Workday.</span></span>  |  <span data-ttu-id="55416-119">SSO toocustomer 擁有 hello Azure AD B2C 租用戶內的應用程式都支援。</span><span class="sxs-lookup"><span data-stu-id="55416-119">SSO toocustomer owned apps within hello Azure AD B2C tenants is supported.</span></span> <span data-ttu-id="55416-120">SSO tooOffice 365 或 tooother Microsoft 和非 Microsoft SaaS 應用程式不支援。</span><span class="sxs-lookup"><span data-stu-id="55416-120">SSO tooOffice 365 or tooother Microsoft and non-Microsoft SaaS apps is not supported.</span></span>
<span data-ttu-id="55416-121">夥伴生命週期： hello 主機/邀請組織所管理。</span><span class="sxs-lookup"><span data-stu-id="55416-121">Partner lifecycle: Managed by hello host/inviting organization.</span></span>  | <span data-ttu-id="55416-122">客戶生命週期： 自助式或由 hello 應用程式管理。</span><span class="sxs-lookup"><span data-stu-id="55416-122">Customer lifecycle: Self-serve or managed by hello application.</span></span>
<span data-ttu-id="55416-123">安全性原則與相容性： hello 主機/邀請組織所管理。</span><span class="sxs-lookup"><span data-stu-id="55416-123">Security policy and compliance: Managed by hello host/inviting organization.</span></span>  | <span data-ttu-id="55416-124">安全性原則與相容性： hello 應用程式管理。</span><span class="sxs-lookup"><span data-stu-id="55416-124">Security policy and compliance: Managed by hello application.</span></span>
<span data-ttu-id="55416-125">商標︰使用主控/邀請組織的品牌。</span><span class="sxs-lookup"><span data-stu-id="55416-125">Branding: Host/inviting organization’s brand is used.</span></span>  |    <span data-ttu-id="55416-126">商標︰由應用程式管理。</span><span class="sxs-lookup"><span data-stu-id="55416-126">Branding: Managed by application.</span></span> <span data-ttu-id="55416-127">通常會 toobe 產品品牌，與 hello 組織淡出到 hello 背景。</span><span class="sxs-lookup"><span data-stu-id="55416-127">Typically tends toobe product branded, with hello organization fading into hello background.</span></span>
<span data-ttu-id="55416-128">其他資訊：[部落格文章](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/01/azure-ad-b2b-new-updates-make-cross-business-collab-easy/)、[文件](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b)</span><span class="sxs-lookup"><span data-stu-id="55416-128">More info: [Blog post](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/01/azure-ad-b2b-new-updates-make-cross-business-collab-easy/), [Documentation](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b)</span></span>  | <span data-ttu-id="55416-129">其他資訊：[產品頁面](https://azure.microsoft.com/en-us/services/active-directory-b2c/)、[文件](https://docs.microsoft.com/en-us/azure/active-directory-b2c/)</span><span class="sxs-lookup"><span data-stu-id="55416-129">More info: [Product page](https://azure.microsoft.com/en-us/services/active-directory-b2c/), [Documentation](https://docs.microsoft.com/en-us/azure/active-directory-b2c/)</span></span>


### <a name="next-steps"></a><span data-ttu-id="55416-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="55416-130">Next steps</span></span>

<span data-ttu-id="55416-131">請瀏覽有關 Azure AD B2B 共同作業的其他文章：</span><span class="sxs-lookup"><span data-stu-id="55416-131">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="55416-132">何謂 Azure AD B2B 共同作業？</span><span class="sxs-lookup"><span data-stu-id="55416-132">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="55416-133">B2B 共同作業使用者屬性</span><span class="sxs-lookup"><span data-stu-id="55416-133">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="55416-134">新增 B2B 共同作業使用者 tooa 角色</span><span class="sxs-lookup"><span data-stu-id="55416-134">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="55416-135">委派 B2B 共同作業邀請</span><span class="sxs-lookup"><span data-stu-id="55416-135">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="55416-136">動態群組和 B2B 共同作業</span><span class="sxs-lookup"><span data-stu-id="55416-136">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="55416-137">設定適用於 B2B 共同作業的 SaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="55416-137">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="55416-138">B2B 共同作業使用者權杖</span><span class="sxs-lookup"><span data-stu-id="55416-138">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="55416-139">B2B 共同作業使用者宣告對應</span><span class="sxs-lookup"><span data-stu-id="55416-139">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="55416-140">Office 365 外部共用</span><span class="sxs-lookup"><span data-stu-id="55416-140">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="55416-141">B2B 共同作業目前的限制</span><span class="sxs-lookup"><span data-stu-id="55416-141">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
* [<span data-ttu-id="55416-142">取得 B2B 共同作業的支援</span><span class="sxs-lookup"><span data-stu-id="55416-142">Getting support for B2B collaboration</span></span>](active-directory-b2b-support.md)
