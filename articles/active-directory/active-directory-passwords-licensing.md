---
title: "授權︰Azure AD SSPR | Microsoft Docs"
description: "Azure AD 自助式密碼重設授權需求"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 9cecaaac429165346f7082f1965dc8a21063fe7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="licensing-requirements-for-azure-ad-self-service-password-reset"></a><span data-ttu-id="49e0d-103">Azure AD 自助式密碼重設的授權需求</span><span class="sxs-lookup"><span data-stu-id="49e0d-103">Licensing requirements for Azure AD self-service password reset</span></span>

<span data-ttu-id="49e0d-104">Azure AD 密碼重設 toofunction，讓您**必須至少一個組織中指派的授權**。</span><span class="sxs-lookup"><span data-stu-id="49e0d-104">In order for Azure AD Password Reset toofunction, you **must have at least one license assigned in your organization**.</span></span> <span data-ttu-id="49e0d-105">我們不會強制執行每個使用者授權 hello 密碼重設的經驗。</span><span class="sxs-lookup"><span data-stu-id="49e0d-105">We do not enforce per-user licensing on hello password reset experience.</span></span> <span data-ttu-id="49e0d-106">toomaintain 符合您的 Microsoft 授權合約，您必須使用 premium 功能 tooassign 授權 tooany 使用者。</span><span class="sxs-lookup"><span data-stu-id="49e0d-106">toomaintain compliance with your Microsoft licensing agreement, you need tooassign licenses tooany users that use premium features.</span></span>

* <span data-ttu-id="49e0d-107">**僅限雲端使用者** - Office 365 (O365) 任何付費的 SKU，或 Azure AD Basic</span><span class="sxs-lookup"><span data-stu-id="49e0d-107">**Cloud only users** - Office 365 (O365) any paid SKU, or Azure AD Basic</span></span>
* <span data-ttu-id="49e0d-108">**雲端**及/或**內部部署使用者** - Azure AD Premium P1 或 P2、Enterprise Mobility + Security (EMS) 或 Secure Productive Enterprise (SPE)</span><span class="sxs-lookup"><span data-stu-id="49e0d-108">**Cloud** and/or **on-premises users** - Azure AD Premium P1 or P2, Enterprise Mobility + Security (EMS), or Secure Productive Enterprise (SPE)</span></span>

## <a name="licenses-required-for-password-writeback"></a><span data-ttu-id="49e0d-109">密碼回寫所需的授權</span><span class="sxs-lookup"><span data-stu-id="49e0d-109">Licenses required for password writeback</span></span>

<span data-ttu-id="49e0d-110">toouse 密碼回寫，您必須有一個 hello 遵循您的租用戶中指派的授權。</span><span class="sxs-lookup"><span data-stu-id="49e0d-110">toouse password writeback, you must have one of hello following licenses assigned in your tenant.</span></span>

* <span data-ttu-id="49e0d-111">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="49e0d-111">Azure AD Premium P1</span></span>
* <span data-ttu-id="49e0d-112">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="49e0d-112">Azure AD Premium P2</span></span>
* <span data-ttu-id="49e0d-113">Enterprise Mobility + Security E3</span><span class="sxs-lookup"><span data-stu-id="49e0d-113">Enterprise Mobility + Security E3</span></span>
* <span data-ttu-id="49e0d-114">Enterprise Mobility + Security E5</span><span class="sxs-lookup"><span data-stu-id="49e0d-114">Enterprise Mobility + Security E5</span></span>
* <span data-ttu-id="49e0d-115">Secure Productive Enterprise E3</span><span class="sxs-lookup"><span data-stu-id="49e0d-115">Secure Productive Enterprise E3</span></span>
* <span data-ttu-id="49e0d-116">Secure Productive Enterprise E5</span><span class="sxs-lookup"><span data-stu-id="49e0d-116">Secure Productive Enterprise E5</span></span>

> [!NOTE]
> <span data-ttu-id="49e0d-117">獨立 Office 365 授權計劃**不支援密碼回寫**和需要 hello 前的此功能 toowork 計劃的其中一個。</span><span class="sxs-lookup"><span data-stu-id="49e0d-117">Standalone Office 365 licensing plans **do not support password writeback** and require one of hello preceding plans for this functionality toowork.</span></span>

<span data-ttu-id="49e0d-118">Hello 遵循頁面上可以找到額外的授權資訊，包括成本</span><span class="sxs-lookup"><span data-stu-id="49e0d-118">Additional licensing info including costs can be found on hello following pages</span></span>

* [<span data-ttu-id="49e0d-119">Azure Active Directory 價格網站</span><span class="sxs-lookup"><span data-stu-id="49e0d-119">Azure Active Directory Pricing site</span></span>](https://azure.microsoft.com/pricing/details/active-directory/)
* [<span data-ttu-id="49e0d-120">Enterprise Mobility + Security</span><span class="sxs-lookup"><span data-stu-id="49e0d-120">Enterprise Mobility + Security</span></span>](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)
* [<span data-ttu-id="49e0d-121">Secure Productive Enterprise</span><span class="sxs-lookup"><span data-stu-id="49e0d-121">Secure Productive Enterprise</span></span>](https://www.microsoft.com/secure-productive-enterprise/default.aspx)

## <a name="enable-group-or-user-based-licensing"></a><span data-ttu-id="49e0d-122">啟用以群組或使用者為基礎的授權</span><span class="sxs-lookup"><span data-stu-id="49e0d-122">Enable group or user-based licensing</span></span>

<span data-ttu-id="49e0d-123">Azure AD 現在支援群組為基礎授權允許系統管理員 tooassign 授權大量 tooa 使用者群組，而不是將指派一次。</span><span class="sxs-lookup"><span data-stu-id="49e0d-123">Azure AD now supports group-based licensing allowing administrators tooassign licenses in bulk tooa group of users, rather than assigning them one at a time.</span></span> [<span data-ttu-id="49e0d-124">指派、驗證授權及解決其問題</span><span class="sxs-lookup"><span data-stu-id="49e0d-124">Assign, verify, and resolve problems with licenses</span></span>](active-directory-licensing-group-assignment-azure-portal.md#step-1-assign-the-required-licenses)

<span data-ttu-id="49e0d-125">並非所有位置都可使用某些 Microsoft 服務。</span><span class="sxs-lookup"><span data-stu-id="49e0d-125">Some Microsoft services are not available in all locations.</span></span> <span data-ttu-id="49e0d-126">Tooa 使用者可以指派授權之前，hello 系統管理員必須 hello 使用者指定 hello 「 使用量位置 」 屬性。</span><span class="sxs-lookup"><span data-stu-id="49e0d-126">Before a license can be assigned tooa user, hello administrator must specify hello “Usage location” property on hello user.</span></span> <span data-ttu-id="49e0d-127">指派的授權，才可以在 使用者 > 設定檔 > hello Azure 入口網站中的設定一節。</span><span class="sxs-lookup"><span data-stu-id="49e0d-127">Assignment of licenses can be done under User > Profile > Settings section in hello Azure portal.</span></span> <span data-ttu-id="49e0d-128">**當使用群組授權指派，請指定使用位置沒有任何使用者都會繼承 hello hello 目錄位置。**</span><span class="sxs-lookup"><span data-stu-id="49e0d-128">**When using group license assignment, any users without a usage location specified inherit hello location of hello directory.**</span></span>

## <a name="next-steps"></a><span data-ttu-id="49e0d-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="49e0d-129">Next steps</span></span>

<span data-ttu-id="49e0d-130">hello 下列連結提供有關密碼重設使用 Azure AD 的其他資訊</span><span class="sxs-lookup"><span data-stu-id="49e0d-130">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="49e0d-131">[**快速入門**](active-directory-passwords-getting-started.md) - 開始執行 Azure AD 自助式密碼管理</span><span class="sxs-lookup"><span data-stu-id="49e0d-131">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="49e0d-132">[**資料**](active-directory-passwords-data.md) -了解所需的 hello 資料及如何使用密碼管理</span><span class="sxs-lookup"><span data-stu-id="49e0d-132">[**Data**](active-directory-passwords-data.md) - Understand hello data that is required and how it is used for password management</span></span>
* <span data-ttu-id="49e0d-133">[**首度發行**](active-directory-passwords-best-practices.md) -計劃和部署 SSPR tooyour 使用者 hello 指引，請參閱</span><span class="sxs-lookup"><span data-stu-id="49e0d-133">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR tooyour users using hello guidance found here</span></span>
* <span data-ttu-id="49e0d-134">[**自訂**](active-directory-passwords-customize.md) -自訂的 hello SSPR 體驗您的公司 hello 外觀與風格。</span><span class="sxs-lookup"><span data-stu-id="49e0d-134">[**Customize**](active-directory-passwords-customize.md) - Customize hello look and feel of hello SSPR experience for your company.</span></span>
* <span data-ttu-id="49e0d-135">[**報告**](active-directory-passwords-reporting.md) - 探索您的使用者是否、何時、何地存取 SSPR 功能</span><span class="sxs-lookup"><span data-stu-id="49e0d-135">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="49e0d-136">[**技術的深入探討**](active-directory-passwords-how-it-works.md) -hello 帘 toounderstand 後方移它的運作方式</span><span class="sxs-lookup"><span data-stu-id="49e0d-136">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind hello curtain toounderstand how it works</span></span>
* <span data-ttu-id="49e0d-137">[**常見問題集**](active-directory-passwords-faq.md) - 如何？</span><span class="sxs-lookup"><span data-stu-id="49e0d-137">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="49e0d-138">原因為何？</span><span class="sxs-lookup"><span data-stu-id="49e0d-138">Why?</span></span> <span data-ttu-id="49e0d-139">何事？</span><span class="sxs-lookup"><span data-stu-id="49e0d-139">What?</span></span> <span data-ttu-id="49e0d-140">何地？</span><span class="sxs-lookup"><span data-stu-id="49e0d-140">Where?</span></span> <span data-ttu-id="49e0d-141">何人？</span><span class="sxs-lookup"><span data-stu-id="49e0d-141">Who?</span></span> <span data-ttu-id="49e0d-142">何時？</span><span class="sxs-lookup"><span data-stu-id="49e0d-142">When?</span></span> <span data-ttu-id="49e0d-143">-回答您總是想 tooask tooquestions</span><span class="sxs-lookup"><span data-stu-id="49e0d-143">- Answers tooquestions you always wanted tooask</span></span>
* <span data-ttu-id="49e0d-144">[**疑難排解**](active-directory-passwords-troubleshoot.md) -了解如何 tooresolve 常見問題，我們會看到與 SSPR</span><span class="sxs-lookup"><span data-stu-id="49e0d-144">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>

