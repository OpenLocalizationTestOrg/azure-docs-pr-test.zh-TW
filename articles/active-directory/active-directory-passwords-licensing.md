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
ms.openlocfilehash: 936134bddad19964f809a17f200ebbeed5aa853c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="licensing-requirements-for-azure-ad-self-service-password-reset"></a><span data-ttu-id="baa73-103">Azure AD 自助式密碼重設的授權需求</span><span class="sxs-lookup"><span data-stu-id="baa73-103">Licensing requirements for Azure AD self-service password reset</span></span>

<span data-ttu-id="baa73-104">為了讓 Azure AD 密碼重設為函式，您**必須至少在組織中被指派一個授權**。</span><span class="sxs-lookup"><span data-stu-id="baa73-104">In order for Azure AD Password Reset to function, you **must have at least one license assigned in your organization**.</span></span> <span data-ttu-id="baa73-105">我們不會對密碼重設體驗強制執行每個使用者的授權。</span><span class="sxs-lookup"><span data-stu-id="baa73-105">We do not enforce per-user licensing on the password reset experience.</span></span> <span data-ttu-id="baa73-106">若要符合您的 Microsoft 授權合約規定，您需要將授權指派給任何使用進階功能的使用者。</span><span class="sxs-lookup"><span data-stu-id="baa73-106">To maintain compliance with your Microsoft licensing agreement, you need to assign licenses to any users that use premium features.</span></span>

* <span data-ttu-id="baa73-107">**僅限雲端使用者** - Office 365 (O365) 任何付費的 SKU，或 Azure AD Basic</span><span class="sxs-lookup"><span data-stu-id="baa73-107">**Cloud only users** - Office 365 (O365) any paid SKU, or Azure AD Basic</span></span>
* <span data-ttu-id="baa73-108">**雲端**及/或**內部部署使用者** - Azure AD Premium P1 或 P2、Enterprise Mobility + Security (EMS) 或 Secure Productive Enterprise (SPE)</span><span class="sxs-lookup"><span data-stu-id="baa73-108">**Cloud** and/or **on-premises users** - Azure AD Premium P1 or P2, Enterprise Mobility + Security (EMS), or Secure Productive Enterprise (SPE)</span></span>

## <a name="licenses-required-for-password-writeback"></a><span data-ttu-id="baa73-109">密碼回寫所需的授權</span><span class="sxs-lookup"><span data-stu-id="baa73-109">Licenses required for password writeback</span></span>

<span data-ttu-id="baa73-110">若要使用密碼回寫，您的租用戶中必須已指派下列其中一項授權。</span><span class="sxs-lookup"><span data-stu-id="baa73-110">To use password writeback, you must have one of the following licenses assigned in your tenant.</span></span>

* <span data-ttu-id="baa73-111">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="baa73-111">Azure AD Premium P1</span></span>
* <span data-ttu-id="baa73-112">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="baa73-112">Azure AD Premium P2</span></span>
* <span data-ttu-id="baa73-113">Enterprise Mobility + Security E3</span><span class="sxs-lookup"><span data-stu-id="baa73-113">Enterprise Mobility + Security E3</span></span>
* <span data-ttu-id="baa73-114">Enterprise Mobility + Security E5</span><span class="sxs-lookup"><span data-stu-id="baa73-114">Enterprise Mobility + Security E5</span></span>
* <span data-ttu-id="baa73-115">Secure Productive Enterprise E3</span><span class="sxs-lookup"><span data-stu-id="baa73-115">Secure Productive Enterprise E3</span></span>
* <span data-ttu-id="baa73-116">Secure Productive Enterprise E5</span><span class="sxs-lookup"><span data-stu-id="baa73-116">Secure Productive Enterprise E5</span></span>

> [!NOTE]
> <span data-ttu-id="baa73-117">獨立的 Office 365 授權方案**不支援密碼回寫**，而且需要上述其中一個方案，這項功能才能運作。</span><span class="sxs-lookup"><span data-stu-id="baa73-117">Standalone Office 365 licensing plans **do not support password writeback** and require one of the preceding plans for this functionality to work.</span></span>

<span data-ttu-id="baa73-118">在下列頁面可以找到額外的授權資訊 (包括成本)：</span><span class="sxs-lookup"><span data-stu-id="baa73-118">Additional licensing info including costs can be found on the following pages</span></span>

* [<span data-ttu-id="baa73-119">Azure Active Directory 價格網站</span><span class="sxs-lookup"><span data-stu-id="baa73-119">Azure Active Directory Pricing site</span></span>](https://azure.microsoft.com/pricing/details/active-directory/)
* [<span data-ttu-id="baa73-120">Enterprise Mobility + Security</span><span class="sxs-lookup"><span data-stu-id="baa73-120">Enterprise Mobility + Security</span></span>](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)
* [<span data-ttu-id="baa73-121">Secure Productive Enterprise</span><span class="sxs-lookup"><span data-stu-id="baa73-121">Secure Productive Enterprise</span></span>](https://www.microsoft.com/secure-productive-enterprise/default.aspx)

## <a name="enable-group-or-user-based-licensing"></a><span data-ttu-id="baa73-122">啟用以群組或使用者為基礎的授權</span><span class="sxs-lookup"><span data-stu-id="baa73-122">Enable group or user-based licensing</span></span>

<span data-ttu-id="baa73-123">Azure AD 現在支援以群組為基礎的授權，允許系統管理員將大量授權指派給一群使用者，而不是一次指派一個授權。</span><span class="sxs-lookup"><span data-stu-id="baa73-123">Azure AD now supports group-based licensing allowing administrators to assign licenses in bulk to a group of users, rather than assigning them one at a time.</span></span> [<span data-ttu-id="baa73-124">指派、驗證授權及解決其問題</span><span class="sxs-lookup"><span data-stu-id="baa73-124">Assign, verify, and resolve problems with licenses</span></span>](active-directory-licensing-group-assignment-azure-portal.md#step-1-assign-the-required-licenses)

<span data-ttu-id="baa73-125">並非所有位置都可使用某些 Microsoft 服務。</span><span class="sxs-lookup"><span data-stu-id="baa73-125">Some Microsoft services are not available in all locations.</span></span> <span data-ttu-id="baa73-126">系統管理員必須先指定使用者的 [使用位置]屬性，才能將授權指派給使用者。</span><span class="sxs-lookup"><span data-stu-id="baa73-126">Before a license can be assigned to a user, the administrator must specify the “Usage location” property on the user.</span></span> <span data-ttu-id="baa73-127">可以在 Azure 入口網站中的 [使用者] > [設定檔] > [設定] 區段之下進行授權指派。</span><span class="sxs-lookup"><span data-stu-id="baa73-127">Assignment of licenses can be done under User > Profile > Settings section in the Azure portal.</span></span> <span data-ttu-id="baa73-128">**使用群組授權指派時，未指定使用位置的任何使用者在指派期間會繼承目錄的位置。**</span><span class="sxs-lookup"><span data-stu-id="baa73-128">**When using group license assignment, any users without a usage location specified inherit the location of the directory.**</span></span>

## <a name="next-steps"></a><span data-ttu-id="baa73-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="baa73-129">Next steps</span></span>

<span data-ttu-id="baa73-130">下列連結提供有關使用 Azure AD 重設密碼的其他資訊</span><span class="sxs-lookup"><span data-stu-id="baa73-130">The following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="baa73-131">[**快速入門**](active-directory-passwords-getting-started.md) - 開始執行 Azure AD 自助式密碼管理</span><span class="sxs-lookup"><span data-stu-id="baa73-131">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="baa73-132">[**資料**](active-directory-passwords-data.md) - 了解所需的資料以及如何將它使用於密碼管理</span><span class="sxs-lookup"><span data-stu-id="baa73-132">[**Data**](active-directory-passwords-data.md) - Understand the data that is required and how it is used for password management</span></span>
* <span data-ttu-id="baa73-133">[**推出**](active-directory-passwords-best-practices.md) - 使用此處提供的指引來規劃 SSPR 並將它部署至使用者</span><span class="sxs-lookup"><span data-stu-id="baa73-133">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR to your users using the guidance found here</span></span>
* <span data-ttu-id="baa73-134">[**自訂**](active-directory-passwords-customize.md) - 為您的公司自訂 SSPR 體驗的外觀與風格。</span><span class="sxs-lookup"><span data-stu-id="baa73-134">[**Customize**](active-directory-passwords-customize.md) - Customize the look and feel of the SSPR experience for your company.</span></span>
* <span data-ttu-id="baa73-135">[**報告**](active-directory-passwords-reporting.md) - 探索您的使用者是否、何時、何地存取 SSPR 功能</span><span class="sxs-lookup"><span data-stu-id="baa73-135">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="baa73-136">[**技術性深入探討**](active-directory-passwords-how-it-works.md) - 深入探索以了解其運作方式</span><span class="sxs-lookup"><span data-stu-id="baa73-136">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind the curtain to understand how it works</span></span>
* <span data-ttu-id="baa73-137">[**常見問題集**](active-directory-passwords-faq.md) - 如何？</span><span class="sxs-lookup"><span data-stu-id="baa73-137">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="baa73-138">原因為何？</span><span class="sxs-lookup"><span data-stu-id="baa73-138">Why?</span></span> <span data-ttu-id="baa73-139">何事？</span><span class="sxs-lookup"><span data-stu-id="baa73-139">What?</span></span> <span data-ttu-id="baa73-140">何地？</span><span class="sxs-lookup"><span data-stu-id="baa73-140">Where?</span></span> <span data-ttu-id="baa73-141">何人？</span><span class="sxs-lookup"><span data-stu-id="baa73-141">Who?</span></span> <span data-ttu-id="baa73-142">何時？</span><span class="sxs-lookup"><span data-stu-id="baa73-142">When?</span></span> <span data-ttu-id="baa73-143">- -您一直想要詢問之問題的答案</span><span class="sxs-lookup"><span data-stu-id="baa73-143">- Answers to questions you always wanted to ask</span></span>
* <span data-ttu-id="baa73-144">[**疑難排解**](active-directory-passwords-troubleshoot.md) - 了解如何解決我們看到的 SSPR 常見問題</span><span class="sxs-lookup"><span data-stu-id="baa73-144">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how to resolve common issues that we see with SSPR</span></span>

