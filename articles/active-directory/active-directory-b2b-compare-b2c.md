---
title: "比較 Azure Active Directory 的 B2B 共同作業和 B2C | Microsoft Docs"
description: "Azure Active Directory B2B 共同作業和 Azure AD B2C 有何不同？"
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
ms.openlocfilehash: 44cbbc149787a2d6cf2e0e8750b98d33b52f6136
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="compare-b2b-collaboration-and-b2c-in-azure-active-directory"></a><span data-ttu-id="69e40-103">比較 Azure Active Directory 的 B2B 共同作業和 B2C</span><span class="sxs-lookup"><span data-stu-id="69e40-103">Compare B2B collaboration and B2C in Azure Active Directory</span></span>

<span data-ttu-id="69e40-104">Azure Active Directory (Azure AD) B2B 共同作業和 Azure AD B2C 皆可讓您在 Azure AD 中使用外部使用者進行操作。</span><span class="sxs-lookup"><span data-stu-id="69e40-104">Both Azure Active Directory (Azure AD) B2B collaboration and Azure AD B2C allow you to work with external users in Azure AD.</span></span> <span data-ttu-id="69e40-105">但它們究竟差在哪兒？</span><span class="sxs-lookup"><span data-stu-id="69e40-105">But how do they compare?</span></span>


<span data-ttu-id="69e40-106">B2B 共同作業</span><span class="sxs-lookup"><span data-stu-id="69e40-106">B2B collaboration capabilities</span></span> |     <span data-ttu-id="69e40-107">Azure AD B2C 獨立供應項目</span><span class="sxs-lookup"><span data-stu-id="69e40-107">Azure AD B2C stand-alone offering</span></span>
-------- | --------
<span data-ttu-id="69e40-108">適用於︰想要能夠驗證來自合作夥伴組織 (無論是否為識別提供者) 之使用者的組織。</span><span class="sxs-lookup"><span data-stu-id="69e40-108">Intended for: Organizations that want to be able to authenticate users from a partner organization, regardless of identity provider.</span></span> | <span data-ttu-id="69e40-109">適用於︰邀請您的行動和 Web 應用程式的客戶 (無論是個人、機構或組織客戶) 加入您的 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="69e40-109">Intended for: Inviting customers of your mobile and web apps, whether individuals, institutional or organizational customers into your Azure AD.</span></span>
<span data-ttu-id="69e40-110">支援的身分識別︰本機有工作或學校帳戶的員工、本機有工作或學校帳戶的合作夥伴、或任何電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="69e40-110">Identities supported: Employees with work or school accounts, partners with work or school accounts, or any email address.</span></span> <span data-ttu-id="69e40-111">即將支援直接聯盟。</span><span class="sxs-lookup"><span data-stu-id="69e40-111">Soon to support direct federation.</span></span>  | <span data-ttu-id="69e40-112">支援的身分識別︰具有本機應用程式帳戶的取用者使用者 (任何電子郵件地址或使用者名稱) 或任何以直接聯盟支援的社交身分識別。</span><span class="sxs-lookup"><span data-stu-id="69e40-112">Identities supported: Consumer users with local application accounts (any email address or user name) or any supported social identity with direct federation.</span></span>
<span data-ttu-id="69e40-113">合作夥伴使用者位於哪個目錄︰外部組織的合作夥伴使用者與員工在相同的管理目錄中，但特別註解。</span><span class="sxs-lookup"><span data-stu-id="69e40-113">Which directory the partner users are in: Partner users from the external organization are managed in the same directory as employees, but annotated specially.</span></span> <span data-ttu-id="69e40-114">管理他們的方式可和員工相同，可以加入到相同的群組等等</span><span class="sxs-lookup"><span data-stu-id="69e40-114">They can be managed the same way as employees, can be added to the same groups, and so on</span></span>  | <span data-ttu-id="69e40-115">客戶使用者實體位於哪個目錄︰在應用程式目錄中。</span><span class="sxs-lookup"><span data-stu-id="69e40-115">Which directory the customer user entities are in: In the application directory.</span></span> <span data-ttu-id="69e40-116">和組織的員工及合作夥伴目錄 (若有) 分開管理。</span><span class="sxs-lookup"><span data-stu-id="69e40-116">Managed separately from the organization’s employee and partner directory (if any.</span></span>
<span data-ttu-id="69e40-117">支援單一登入 (SSO) 至所有和 Azure AD 連線的應用程式。</span><span class="sxs-lookup"><span data-stu-id="69e40-117">Single sign-on (SSO) to all Azure AD-connected apps is supported.</span></span> <span data-ttu-id="69e40-118">例如，您可以提供 Office 365 或內部部署應用程式的存取權，以及其他 SaaS 應用程式 (例如 Salesforce 或 Workday) 的存取權。</span><span class="sxs-lookup"><span data-stu-id="69e40-118">For example, you can provide access to Office 365 or on-premises apps, and to other SaaS apps such as Salesforce or Workday.</span></span>  |  <span data-ttu-id="69e40-119">支援 SSO 至客戶在 Azure AD B2C 租用戶內擁有的應用程式。</span><span class="sxs-lookup"><span data-stu-id="69e40-119">SSO to customer owned apps within the Azure AD B2C tenants is supported.</span></span> <span data-ttu-id="69e40-120">不支援 SSO 至 Office 365 或其他 Microsoft 和非 Microsoft SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="69e40-120">SSO to Office 365 or to other Microsoft and non-Microsoft SaaS apps is not supported.</span></span>
<span data-ttu-id="69e40-121">合作夥伴生命週期︰由主控/邀請組織管理。</span><span class="sxs-lookup"><span data-stu-id="69e40-121">Partner lifecycle: Managed by the host/inviting organization.</span></span>  | <span data-ttu-id="69e40-122">客戶生命週期︰自助式管理或由應用程式管理。</span><span class="sxs-lookup"><span data-stu-id="69e40-122">Customer lifecycle: Self-serve or managed by the application.</span></span>
<span data-ttu-id="69e40-123">安全性原則和合規性︰由主控/邀請組織管理。</span><span class="sxs-lookup"><span data-stu-id="69e40-123">Security policy and compliance: Managed by the host/inviting organization.</span></span>  | <span data-ttu-id="69e40-124">安全性原則和合規性︰由應用程式管理。</span><span class="sxs-lookup"><span data-stu-id="69e40-124">Security policy and compliance: Managed by the application.</span></span>
<span data-ttu-id="69e40-125">商標︰使用主控/邀請組織的品牌。</span><span class="sxs-lookup"><span data-stu-id="69e40-125">Branding: Host/inviting organization’s brand is used.</span></span>  |    <span data-ttu-id="69e40-126">商標︰由應用程式管理。</span><span class="sxs-lookup"><span data-stu-id="69e40-126">Branding: Managed by application.</span></span> <span data-ttu-id="69e40-127">通常多半會是產品品牌加上組織在背景淡出的效果。</span><span class="sxs-lookup"><span data-stu-id="69e40-127">Typically tends to be product branded, with the organization fading into the background.</span></span>
<span data-ttu-id="69e40-128">其他資訊：[部落格文章](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/01/azure-ad-b2b-new-updates-make-cross-business-collab-easy/)、[文件](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b)</span><span class="sxs-lookup"><span data-stu-id="69e40-128">More info: [Blog post](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/01/azure-ad-b2b-new-updates-make-cross-business-collab-easy/), [Documentation](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b)</span></span>  | <span data-ttu-id="69e40-129">其他資訊：[產品頁面](https://azure.microsoft.com/en-us/services/active-directory-b2c/)、[文件](https://docs.microsoft.com/en-us/azure/active-directory-b2c/)</span><span class="sxs-lookup"><span data-stu-id="69e40-129">More info: [Product page](https://azure.microsoft.com/en-us/services/active-directory-b2c/), [Documentation](https://docs.microsoft.com/en-us/azure/active-directory-b2c/)</span></span>


### <a name="next-steps"></a><span data-ttu-id="69e40-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="69e40-130">Next steps</span></span>

<span data-ttu-id="69e40-131">請瀏覽有關 Azure AD B2B 共同作業的其他文章：</span><span class="sxs-lookup"><span data-stu-id="69e40-131">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="69e40-132">何謂 Azure AD B2B 共同作業？</span><span class="sxs-lookup"><span data-stu-id="69e40-132">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="69e40-133">B2B 共同作業使用者屬性</span><span class="sxs-lookup"><span data-stu-id="69e40-133">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="69e40-134">將 B2B 共同作業使用者新增至角色</span><span class="sxs-lookup"><span data-stu-id="69e40-134">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="69e40-135">委派 B2B 共同作業邀請</span><span class="sxs-lookup"><span data-stu-id="69e40-135">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="69e40-136">動態群組和 B2B 共同作業</span><span class="sxs-lookup"><span data-stu-id="69e40-136">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="69e40-137">設定適用於 B2B 共同作業的 SaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="69e40-137">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="69e40-138">B2B 共同作業使用者權杖</span><span class="sxs-lookup"><span data-stu-id="69e40-138">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="69e40-139">B2B 共同作業使用者宣告對應</span><span class="sxs-lookup"><span data-stu-id="69e40-139">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="69e40-140">Office 365 外部共用</span><span class="sxs-lookup"><span data-stu-id="69e40-140">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="69e40-141">B2B 共同作業目前的限制</span><span class="sxs-lookup"><span data-stu-id="69e40-141">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
* [<span data-ttu-id="69e40-142">取得 B2B 共同作業的支援</span><span class="sxs-lookup"><span data-stu-id="69e40-142">Getting support for B2B collaboration</span></span>](active-directory-b2b-support.md)
