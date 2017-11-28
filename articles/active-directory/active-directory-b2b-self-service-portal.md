---
title: "Azure Active Directory B2B 共同作業的 aaaSelf 服務註冊入口網站 |Microsoft 文件"
description: "Azure Active Directory B2B 共同作業支援跨公司關聯性，方式是讓商務夥伴 tooselectively 存取公司的應用程式"
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
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: c78920ecf812f7efc06a8b54b1fff834c32904f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="self-service-portal-for-azure-ad-b2b-collaboration-sign-up"></a><span data-ttu-id="8a31a-103">Azure AD B2B 共同作業註冊的自助入口網站</span><span class="sxs-lookup"><span data-stu-id="8a31a-103">Self-service portal for Azure AD B2B collaboration sign-up</span></span>

<span data-ttu-id="8a31a-104">客戶可以進行許多事情 hello 內建功能的公開會透過我們的 IT 系統管理員[Azure 入口網站](https://portal.azure.com)以及我們[應用程式存取面板](https://myapps.microsoft.com)終端使用者。</span><span class="sxs-lookup"><span data-stu-id="8a31a-104">Customers can do a lot with hello built-in features that are exposed through our IT admin [Azure portal](https://portal.azure.com) and our [Application Access Panel](https://myapps.microsoft.com) for end users.</span></span> <span data-ttu-id="8a31a-105">但是您也注意，企業需要 toocustomize hello 登入工作流程的 B2B 使用者 toofit 其組織的需求。</span><span class="sxs-lookup"><span data-stu-id="8a31a-105">But we are also aware that businesses need toocustomize hello onboarding workflow for B2B users toofit their organization’s needs.</span></span> <span data-ttu-id="8a31a-106">透過[我們的 API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)，企業就可以達成這個目的。</span><span class="sxs-lookup"><span data-stu-id="8a31a-106">They can do that with [our API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation).</span></span>

<span data-ttu-id="8a31a-107">在與客戶討論過後，我們發現，企業有一項明顯的常見需求。</span><span class="sxs-lookup"><span data-stu-id="8a31a-107">In discussions with our customers, we see one common need rise up above all others.</span></span> <span data-ttu-id="8a31a-108">hello 邀請組織可能不知道事先人員 hello 個別外部共同作業者需要存取 tootheir 資源的人員。</span><span class="sxs-lookup"><span data-stu-id="8a31a-108">hello inviting organization may not know ahead of time who hello individual external collaborators are who need access tootheir resources.</span></span> <span data-ttu-id="8a31a-109">使用者從夥伴公司太註冊本身與一組原則邀請組織控制項的 hello，他們會希望的方式。</span><span class="sxs-lookup"><span data-stu-id="8a31a-109">They wanted a way for users from partner companies too sign themselves up with a set of policies that hello inviting organization controls.</span></span> <span data-ttu-id="8a31a-110">透過我們的 API 就能實現此案例，因此我們在 GitHub 上發佈了專門針對此需求的專案：[GitHub 專案範例](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web)。</span><span class="sxs-lookup"><span data-stu-id="8a31a-110">This scenario is possible through our APIs,  so we published a project on Github that did just that: [sample Github project](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).</span></span>

<span data-ttu-id="8a31a-111">我們的 Github 專案會示範如何組織可以使用我們的 Api 和以原則為基礎的自助註冊功能提供信任的夥伴，以判斷它們可存取的 hello 應用程式的規則。</span><span class="sxs-lookup"><span data-stu-id="8a31a-111">Our Github project demonstrates how organizations can use our APIs, and provide a policy-based, self-service sign-up capability for their trusted partners, with rules that determine hello apps they can access.</span></span> <span data-ttu-id="8a31a-112">在需要時，安全地儲存，而不需要邀請組織 toomanually 將產品上架的 hello 合作夥伴使用者可以取得存取 tooresources 它們。</span><span class="sxs-lookup"><span data-stu-id="8a31a-112">Partner users can get access tooresources when they need them, securely, without requiring hello inviting organization toomanually onboard them.</span></span> <span data-ttu-id="8a31a-113">您可以輕鬆部署到您選擇的 Azure 訂用帳戶的 hello 專案。</span><span class="sxs-lookup"><span data-stu-id="8a31a-113">You can easily deploy hello project into an Azure subscription of your choice.</span></span>

## <a name="as-is-code"></a><span data-ttu-id="8a31a-114">現狀程式碼</span><span class="sxs-lookup"><span data-stu-id="8a31a-114">As-is code</span></span>

<span data-ttu-id="8a31a-115">請記住，這段程式碼可做為範例 toodemonstrate 使用方式的 hello Azure Active Directory B2B 邀請應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="8a31a-115">Remember that this code is made available as a sample toodemonstrate usage of hello Azure Active Directory B2B invitation API.</span></span> <span data-ttu-id="8a31a-116">您應該讓開發小組或合作夥伴對此程式碼進行自訂，於檢閱過後再部署到生產案例。</span><span class="sxs-lookup"><span data-stu-id="8a31a-116">It should be customized by your dev team or a partner, and should be reviewed before being deployed in a production scenario.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a31a-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8a31a-117">Next steps</span></span>

<span data-ttu-id="8a31a-118">請瀏覽有關 Azure AD B2B 共同作業的其他文章：</span><span class="sxs-lookup"><span data-stu-id="8a31a-118">Browse our other articles on Azure AD B2B collaboration:</span></span>
* [<span data-ttu-id="8a31a-119">何謂 Azure AD B2B 共同作業？</span><span class="sxs-lookup"><span data-stu-id="8a31a-119">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="8a31a-120">Azure Active Directory 系統管理員如何新增 B2B 共同作業使用者？</span><span class="sxs-lookup"><span data-stu-id="8a31a-120">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="8a31a-121">資訊工作者如何新增 B2B 共同作業使用者？</span><span class="sxs-lookup"><span data-stu-id="8a31a-121">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="8a31a-122">hello hello B2B 共同作業邀請電子郵件項目</span><span class="sxs-lookup"><span data-stu-id="8a31a-122">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="8a31a-123">B2B 共同作業邀請兌換</span><span class="sxs-lookup"><span data-stu-id="8a31a-123">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="8a31a-124">Azure AD B2B 共同作業授權</span><span class="sxs-lookup"><span data-stu-id="8a31a-124">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="8a31a-125">針對 Azure Active Directory B2B 共同作業問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="8a31a-125">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="8a31a-126">Azure Active Directory B2B 共同作業常見問題 (FAQ)</span><span class="sxs-lookup"><span data-stu-id="8a31a-126">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="8a31a-127">適用於 B2B 共同作業使用者的多重要素驗證</span><span class="sxs-lookup"><span data-stu-id="8a31a-127">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="8a31a-128">在沒有邀請的情況下新增 B2B 共同作業使用者</span><span class="sxs-lookup"><span data-stu-id="8a31a-128">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="8a31a-129">Azure Active Directory 中應用程式管理的文章索引</span><span class="sxs-lookup"><span data-stu-id="8a31a-129">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)