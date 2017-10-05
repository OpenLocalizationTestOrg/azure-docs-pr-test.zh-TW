---
title: "Azure Active Directory B2B 共同作業的自助式註冊入口網站 | Microsoft Docs"
description: "Azure Active Directory B2B 共同作業讓企業合作夥伴選擇性地存取您的公司應用程式，以支援公司間的關係"
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
ms.openlocfilehash: 307373c75bbb87cec683f7a3097f8f159c9d5e61
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="self-service-portal-for-azure-ad-b2b-collaboration-sign-up"></a><span data-ttu-id="99594-103">Azure AD B2B 共同作業註冊的自助入口網站</span><span class="sxs-lookup"><span data-stu-id="99594-103">Self-service portal for Azure AD B2B collaboration sign-up</span></span>

<span data-ttu-id="99594-104">客戶可以使用內建功能進行許多工作，這些功能是透過我們的 IT 系統管理員 [Azure 入口網站](https://portal.azure.com)所公開，至於終端使用者，則是透過我們的[應用程式存取面板](https://myapps.microsoft.com)來公開。</span><span class="sxs-lookup"><span data-stu-id="99594-104">Customers can do a lot with the built-in features that are exposed through our IT admin [Azure portal](https://portal.azure.com) and our [Application Access Panel](https://myapps.microsoft.com) for end users.</span></span> <span data-ttu-id="99594-105">但是我們也知道，企業需要自訂適用於 B2B 使用者的登入工作流程，以符合其組織的需求。</span><span class="sxs-lookup"><span data-stu-id="99594-105">But we are also aware that businesses need to customize the onboarding workflow for B2B users to fit their organization’s needs.</span></span> <span data-ttu-id="99594-106">透過[我們的 API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)，企業就可以達成這個目的。</span><span class="sxs-lookup"><span data-stu-id="99594-106">They can do that with [our API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation).</span></span>

<span data-ttu-id="99594-107">在與客戶討論過後，我們發現，企業有一項明顯的常見需求。</span><span class="sxs-lookup"><span data-stu-id="99594-107">In discussions with our customers, we see one common need rise up above all others.</span></span> <span data-ttu-id="99594-108">提出邀請的組織可能事先不知道需要存取其資源的外部共同作業者分別有誰。</span><span class="sxs-lookup"><span data-stu-id="99594-108">The inviting organization may not know ahead of time who the individual external collaborators are who need access to their resources.</span></span> <span data-ttu-id="99594-109">他們想要讓合作夥伴公司的使用者有方法可以自行註冊，並以提出邀請的組織所能控制的一組原則來加以規範。</span><span class="sxs-lookup"><span data-stu-id="99594-109">They wanted a way for users from partner companies to  sign themselves up with a set of policies that the inviting organization controls.</span></span> <span data-ttu-id="99594-110">透過我們的 API 就能實現此案例，因此我們在 GitHub 上發佈了專門針對此需求的專案：[GitHub 專案範例](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web)。</span><span class="sxs-lookup"><span data-stu-id="99594-110">This scenario is possible through our APIs,  so we published a project on Github that did just that: [sample Github project](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).</span></span>

<span data-ttu-id="99594-111">我們的 GitHub 專案會示範組織可以如何使用我們的 API，並為他們信任的合作夥伴提供以原則為基礎的自助式註冊功能，而且這些功能會有規則可以判斷合作夥伴能存取的應用程式。</span><span class="sxs-lookup"><span data-stu-id="99594-111">Our Github project demonstrates how organizations can use our APIs, and provide a policy-based, self-service sign-up capability for their trusted partners, with rules that determine the apps they can access.</span></span> <span data-ttu-id="99594-112">合作夥伴使用者可以在需要時安全地存取資源，而不需要提出邀請的組織手動讓使用者上線。</span><span class="sxs-lookup"><span data-stu-id="99594-112">Partner users can get access to resources when they need them, securely, without requiring the inviting organization to manually onboard them.</span></span> <span data-ttu-id="99594-113">您可以輕鬆地將專案部署到您選擇的 Azure 訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="99594-113">You can easily deploy the project into an Azure subscription of your choice.</span></span>

## <a name="as-is-code"></a><span data-ttu-id="99594-114">現狀程式碼</span><span class="sxs-lookup"><span data-stu-id="99594-114">As-is code</span></span>

<span data-ttu-id="99594-115">請記住，此程式碼只提供作為範例使用，目的是要示範如何使用 Azure Active Directory B2B 邀請 API。</span><span class="sxs-lookup"><span data-stu-id="99594-115">Remember that this code is made available as a sample to demonstrate usage of the Azure Active Directory B2B invitation API.</span></span> <span data-ttu-id="99594-116">您應該讓開發小組或合作夥伴對此程式碼進行自訂，於檢閱過後再部署到生產案例。</span><span class="sxs-lookup"><span data-stu-id="99594-116">It should be customized by your dev team or a partner, and should be reviewed before being deployed in a production scenario.</span></span>

## <a name="next-steps"></a><span data-ttu-id="99594-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="99594-117">Next steps</span></span>

<span data-ttu-id="99594-118">請瀏覽有關 Azure AD B2B 共同作業的其他文章：</span><span class="sxs-lookup"><span data-stu-id="99594-118">Browse our other articles on Azure AD B2B collaboration:</span></span>
* [<span data-ttu-id="99594-119">何謂 Azure AD B2B 共同作業？</span><span class="sxs-lookup"><span data-stu-id="99594-119">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="99594-120">Azure Active Directory 系統管理員如何新增 B2B 共同作業使用者？</span><span class="sxs-lookup"><span data-stu-id="99594-120">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="99594-121">資訊工作者如何新增 B2B 共同作業使用者？</span><span class="sxs-lookup"><span data-stu-id="99594-121">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="99594-122">B2B 共同作業邀請電子郵件的元素</span><span class="sxs-lookup"><span data-stu-id="99594-122">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="99594-123">B2B 共同作業邀請兌換</span><span class="sxs-lookup"><span data-stu-id="99594-123">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="99594-124">Azure AD B2B 共同作業授權</span><span class="sxs-lookup"><span data-stu-id="99594-124">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="99594-125">針對 Azure Active Directory B2B 共同作業問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="99594-125">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="99594-126">Azure Active Directory B2B 共同作業常見問題 (FAQ)</span><span class="sxs-lookup"><span data-stu-id="99594-126">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="99594-127">適用於 B2B 共同作業使用者的多重要素驗證</span><span class="sxs-lookup"><span data-stu-id="99594-127">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="99594-128">在沒有邀請的情況下新增 B2B 共同作業使用者</span><span class="sxs-lookup"><span data-stu-id="99594-128">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="99594-129">Azure Active Directory 中應用程式管理的文章索引</span><span class="sxs-lookup"><span data-stu-id="99594-129">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)