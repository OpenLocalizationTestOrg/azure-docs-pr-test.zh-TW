---
title: "Azure AD 自助式密碼重設概觀 | Microsoft Docs"
description: "Azure AD 中的自助式密碼重設可為您的組織做些什麼？"
services: active-directory
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
ms.openlocfilehash: 3903c53b78e61b380bb812a9d3ade694655b5afb
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-self-service-password-reset-for-the-it-professional"></a><span data-ttu-id="74499-103">適用於 IT 專業人員的 Azure AD 自助式密碼重設</span><span class="sxs-lookup"><span data-stu-id="74499-103">Azure AD self-service password reset for the IT professional</span></span>

<span data-ttu-id="74499-104">「自助式」是世界各地許多 IT 部門內通行的行話，其具有不同的意義。</span><span class="sxs-lookup"><span data-stu-id="74499-104">"Self-service" is a buzzword thrown around inside many IT departments across the world with varying meanings.</span></span> <span data-ttu-id="74499-105">市場中充斥著各式產品，讓您能夠從雲端或內部部署管理內部部署群組、密碼或使用者設定檔。</span><span class="sxs-lookup"><span data-stu-id="74499-105">The market is flooded with products that allow you to manage on-premises groups, passwords, or user profiles from the cloud or on-premises.</span></span>

<span data-ttu-id="74499-106">Azure Active Directory (Azure AD) 自助式密碼重設 (SSPR) 以容易使用和部署突顯本身的特色。</span><span class="sxs-lookup"><span data-stu-id="74499-106">Azure Active Directory (Azure AD) self-service password reset (SSPR) sets itself apart with ease of use and deployment.</span></span> <span data-ttu-id="74499-107">Azure AD 自助式密碼重設結合了一組功能︰</span><span class="sxs-lookup"><span data-stu-id="74499-107">Azure AD self-service password reset combines a set of capabilities that:</span></span>

* <span data-ttu-id="74499-108">允許使用者管理自己的密碼</span><span class="sxs-lookup"><span data-stu-id="74499-108">Allow your users to manage their own password</span></span>
  * <span data-ttu-id="74499-109">從任何裝置</span><span class="sxs-lookup"><span data-stu-id="74499-109">From any device</span></span>
  * <span data-ttu-id="74499-110">在任何位置</span><span class="sxs-lookup"><span data-stu-id="74499-110">In any location</span></span>
  * <span data-ttu-id="74499-111">在任何時間</span><span class="sxs-lookup"><span data-stu-id="74499-111">At any time</span></span>
* <span data-ttu-id="74499-112">符合身為系統管理員的您所定義的原則規定</span><span class="sxs-lookup"><span data-stu-id="74499-112">Maintain compliance with policies you as an administrator define</span></span>

<span data-ttu-id="74499-113">如果您已準備就緒，即可利用我們的[快速入門指引](active-directory-passwords-getting-started.md)開始使用 Azure AD SSPR，並且快速地讓使用者重設自己的密碼。</span><span class="sxs-lookup"><span data-stu-id="74499-113">If you are ready, you can get started with Azure AD SSPR using our [quick start guidance](active-directory-passwords-getting-started.md) and quickly have your users resetting their own passwords.</span></span>

## <a name="what-is-possible"></a><span data-ttu-id="74499-114">可行功用</span><span class="sxs-lookup"><span data-stu-id="74499-114">What is possible</span></span>

* <span data-ttu-id="74499-115">**自助式密碼變更**可讓使用者或系統管理員變更其密碼，而不需要系統管理員的協助</span><span class="sxs-lookup"><span data-stu-id="74499-115">**Self-service password change** allows end users or administrators to change their passwords without administrator assistance</span></span>
* <span data-ttu-id="74499-116">**自助式帳戶解除鎖定**可讓使用者解除鎖定自己的帳戶，而不需要系統管理員的協助</span><span class="sxs-lookup"><span data-stu-id="74499-116">**Self-service account unlock** allows end users to unlock their own account without administrator assistance</span></span>
* <span data-ttu-id="74499-117">**自助式密碼重設**可讓使用者或系統管理員自動重設其密碼，而不需要系統管理員的協助。</span><span class="sxs-lookup"><span data-stu-id="74499-117">**Self-service password reset** allows end users or administrators to reset their passwords automatically without administrator assistance.</span></span> <span data-ttu-id="74499-118">自助式密碼重設需要 Azure AD Premium 或 Basic - [Azure Active Directory 版本](active-directory-editions.md)。</span><span class="sxs-lookup"><span data-stu-id="74499-118">Self-service password reset requires Azure AD Premium or Basic - [Azure Active Directory Editions](active-directory-editions.md).</span></span>
* <span data-ttu-id="74499-119">**由系統管理員起始的密碼重設**可讓系統管理員在 [Azure 入口網站](https://docs.microsoft.com/azure/azure-portal-overview)中重設使用者或其他系統管理員的密碼。</span><span class="sxs-lookup"><span data-stu-id="74499-119">**Administrator-initiated password reset** allows an administrator to reset an end user’s or another administrator’s password from within the [Azure portal](https://docs.microsoft.com/azure/azure-portal-overview)</span></span>
* <span data-ttu-id="74499-120">**密碼管理活動報告**讓系統管理員得以深入了解其組織內發生的密碼重設和註冊活動- [管理報告](active-directory-passwords-reporting.md)</span><span class="sxs-lookup"><span data-stu-id="74499-120">**Password management activity reports** give administrators insights into password reset and registration activity occurring in their organization - [Management reports](active-directory-passwords-reporting.md)</span></span>
* <span data-ttu-id="74499-121">**密碼回寫**允許從雲端管理內部部署密碼，讓同盟或密碼同步使用者能夠執行或代表執行上述所有案例。</span><span class="sxs-lookup"><span data-stu-id="74499-121">**Password Writeback** allows management of on-premises passwords from the cloud so all the preceeding scenarios can be performed by, or on the behalf of, federated or password synchronized users.</span></span> <span data-ttu-id="74499-122">如果要進行密碼回寫，就必須使用 [Azure AD Premium](active-directory-get-started-premium.md)。</span><span class="sxs-lookup"><span data-stu-id="74499-122">Password Writeback requires [Azure AD Premium](active-directory-get-started-premium.md).</span></span>

## <a name="why-choose-azure-ad-self-service-password-reset"></a><span data-ttu-id="74499-123">為何選擇 Azure AD 自助式密碼重設</span><span class="sxs-lookup"><span data-stu-id="74499-123">Why choose Azure AD self-service password reset</span></span>

* <span data-ttu-id="74499-124">**降低成本**，技術服務人員和支援輔助密碼重設通常佔 IT 組織費用的 20%</span><span class="sxs-lookup"><span data-stu-id="74499-124">**Reduce costs** as helpdesk and support assisted password reset is typically 20% of an IT organization’s spend</span></span>
* <span data-ttu-id="74499-125">**改善使用者體驗**和**降低技術服務人員音量**，做法是賦予使用者立即解決其密碼問題的能力，而不需呼叫技術服務人員或開啟支援要求。</span><span class="sxs-lookup"><span data-stu-id="74499-125">**Improve end-user experiences** and **reduce helpdesk volume** by giving end users the power to resolve their own password issues at once without calling a helpdesk or opening a support request.</span></span>
* <span data-ttu-id="74499-126">**發揮行動力**因為使用者可隨時隨地重設密碼。</span><span class="sxs-lookup"><span data-stu-id="74499-126">**Drive mobility** as users can reset their passwords from wherever they are.</span></span>

## <a name="azure-ad-self-service-password-reset-availability"></a><span data-ttu-id="74499-127">Azure AD 自助式密碼重設可用性</span><span class="sxs-lookup"><span data-stu-id="74499-127">Azure AD self-service password reset availability</span></span>

<span data-ttu-id="74499-128">視您的訂用帳戶而定，Azure AD 自助式密碼重設會以 3 個層級提供。</span><span class="sxs-lookup"><span data-stu-id="74499-128">Azure AD self-service password reset is available in three tiers depending on your subscription.</span></span>

* <span data-ttu-id="74499-129">**Azure AD Free** – 僅限雲端的系統管理員可以重設自己的密碼</span><span class="sxs-lookup"><span data-stu-id="74499-129">**Azure AD Free** – Cloud-only administrators can reset their own passwords</span></span>
* <span data-ttu-id="74499-130">**Azure AD Basic** 或任何**付費 Office 365 訂用帳戶** – 僅限雲端的使用者及僅限雲端的系統管理員可以重設自己的密碼</span><span class="sxs-lookup"><span data-stu-id="74499-130">**Azure AD Basic** or any **Paid Office 365 Subscription** – Cloud-only users and cloud-only administrators can reset their own passwords</span></span>
* <span data-ttu-id="74499-131">**Azure AD Premium** – 任何使用者或系統管理員，包括僅限雲端、同盟或密碼同步使用者可以重設自己的密碼。</span><span class="sxs-lookup"><span data-stu-id="74499-131">**Azure AD Premium** – Any user or administrator, including cloud-only, federated, or password synchronized users, can reset their own passwords.</span></span> <span data-ttu-id="74499-132">內部部署密碼需要啟用密碼回寫。</span><span class="sxs-lookup"><span data-stu-id="74499-132">On-premises passwords require password writeback to be enabled.</span></span>

## <a name="azure-ad-self-service-password-reset-a-sum-of-the-parts"></a><span data-ttu-id="74499-133">Azure AD 自助式密碼重設 (組件的概要)</span><span class="sxs-lookup"><span data-stu-id="74499-133">Azure AD self-service password reset, a sum of the parts</span></span>

<span data-ttu-id="74499-134">下列元件已啟用 Azure AD 中的自助式密碼重設：</span><span class="sxs-lookup"><span data-stu-id="74499-134">Self-service password reset in Azure AD is made up of the following components:</span></span>

* <span data-ttu-id="74499-135">**密碼管理組態入口網站**，您可以在其中控制如何透過 Azure 入口網站在租用戶中管理密碼的選項。</span><span class="sxs-lookup"><span data-stu-id="74499-135">**Password management configuration portal** where you can control options for how passwords are managed in your tenant via the Azure portal</span></span>
* <span data-ttu-id="74499-136">**密碼重設註冊入口網站**使用者可以在其中自行註冊密碼重設</span><span class="sxs-lookup"><span data-stu-id="74499-136">**Password reset registration portal** where users can self-register for password reset</span></span>
* <span data-ttu-id="74499-137">**密碼重設入口網站**，使用者可以在其中使用系統管理員所定義的挑戰和使用者提供的答案，以重設其密碼</span><span class="sxs-lookup"><span data-stu-id="74499-137">**Password reset portal** where users can reset their password using the challenges defined by the administrator and the answers users have provided</span></span>
* <span data-ttu-id="74499-138">**使用者密碼變更入口網站**，使用者可以在其中藉由輸入舊密碼並提供新密碼，以變更自己的密碼</span><span class="sxs-lookup"><span data-stu-id="74499-138">**User password change portal** where users can change their own passwords by entering their old password and providing a new password</span></span>
* <span data-ttu-id="74499-139">**密碼管理報告**，可供系統管理員在 Azure 入口網站其中檢視及分析其租用戶的密碼活動報告</span><span class="sxs-lookup"><span data-stu-id="74499-139">**Password management reports** where administrators can view and analyze password activity reports for their tenants in the Azure portal</span></span>
* <span data-ttu-id="74499-140">**使用 Azure AD Connect 將密碼回寫至內部部署環境**可讓您從雲端進行內部部署、同盟或密碼同步使用者的管理</span><span class="sxs-lookup"><span data-stu-id="74499-140">**Password writeback to on-premises using Azure AD Connect** allows you to enable management of on-premises, federated, or password synchronized users from the cloud</span></span>

## <a name="azure-ad-pricing-sla-updates-and-roadmap"></a><span data-ttu-id="74499-141">Azure AD 價格、SLA、更新和藍圖</span><span class="sxs-lookup"><span data-stu-id="74499-141">Azure AD pricing, SLA, updates, and roadmap</span></span>

<span data-ttu-id="74499-142">在下列頁面上可以找到這些主題的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="74499-142">More detail about these topics can be found on the following pages</span></span>

* [<span data-ttu-id="74499-143">**Azure AD 價格詳細資料**</span><span class="sxs-lookup"><span data-stu-id="74499-143">**Azure AD Pricing Details**</span></span>](https://azure.microsoft.com/pricing/details/active-directory/)
* [<span data-ttu-id="74499-144">**Office 365 價格**</span><span class="sxs-lookup"><span data-stu-id="74499-144">**Office 365 Pricing**</span></span>](https://products.office.com/compare-all-microsoft-office-products?tab=2)
* [<span data-ttu-id="74499-145">**Azure 服務等級協定**</span><span class="sxs-lookup"><span data-stu-id="74499-145">**Azure Service Level Agreements**</span></span>](https://azure.microsoft.com/support/legal/sla/)
* [<span data-ttu-id="74499-146">**Microsoft Online Services 的服務等級協定**</span><span class="sxs-lookup"><span data-stu-id="74499-146">**Service Level Agreement for Microsoft Online Services**</span></span>](http://go.microsoft.com/fwlink/?LinkID=272026&clcid=0x409)
* [<span data-ttu-id="74499-147">**Azure 更新**</span><span class="sxs-lookup"><span data-stu-id="74499-147">**Azure Updates**</span></span>](https://azure.microsoft.com/updates/)
* [<span data-ttu-id="74499-148">**Azure 藍圖**</span><span class="sxs-lookup"><span data-stu-id="74499-148">**Azure Roadmap**</span></span>](https://www.microsoft.com/cloud-platform/roadmap-recently-available)

## <a name="next-steps"></a><span data-ttu-id="74499-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="74499-149">Next steps</span></span>

<span data-ttu-id="74499-150">下列連結提供有關使用 Azure AD 重設密碼的其他資訊</span><span class="sxs-lookup"><span data-stu-id="74499-150">The following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="74499-151">[**快速入門**](active-directory-passwords-getting-started.md) - 開始執行 Azure AD 自助式密碼管理</span><span class="sxs-lookup"><span data-stu-id="74499-151">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="74499-152">[**授權**](active-directory-passwords-licensing.md) - 設定 Azure AD 授權</span><span class="sxs-lookup"><span data-stu-id="74499-152">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="74499-153">[**資料**](active-directory-passwords-data.md) -了解所需的資料以及如何將它使用於密碼管理</span><span class="sxs-lookup"><span data-stu-id="74499-153">[**Data**](active-directory-passwords-data.md) - Understand the data that is required and how it is used for password management</span></span>
* <span data-ttu-id="74499-154">[**推出**](active-directory-passwords-best-practices.md) - 使用此處提供的指引來規劃 SSPR 並將它部署至使用者</span><span class="sxs-lookup"><span data-stu-id="74499-154">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR to your users using the guidance found here</span></span>
* <span data-ttu-id="74499-155">[**自訂**](active-directory-passwords-customize.md) - 為您的公司自訂 SSPR 體驗的外觀與風格。</span><span class="sxs-lookup"><span data-stu-id="74499-155">[**Customize**](active-directory-passwords-customize.md) - Customize the look and feel of the SSPR experience for your company.</span></span>
* <span data-ttu-id="74499-156">[**報告**](active-directory-passwords-reporting.md) - 探索您的使用者是否、何時、何地存取 SSPR 功能</span><span class="sxs-lookup"><span data-stu-id="74499-156">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="74499-157">[**技術性深入探討**](active-directory-passwords-how-it-works.md) - 深入探索以了解其運作方式</span><span class="sxs-lookup"><span data-stu-id="74499-157">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind the curtain to understand how it works</span></span>
* <span data-ttu-id="74499-158">[**常見問題集**](active-directory-passwords-faq.md) - 如何？</span><span class="sxs-lookup"><span data-stu-id="74499-158">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="74499-159">原因為何？</span><span class="sxs-lookup"><span data-stu-id="74499-159">Why?</span></span> <span data-ttu-id="74499-160">何事？</span><span class="sxs-lookup"><span data-stu-id="74499-160">What?</span></span> <span data-ttu-id="74499-161">何地？</span><span class="sxs-lookup"><span data-stu-id="74499-161">Where?</span></span> <span data-ttu-id="74499-162">何人？</span><span class="sxs-lookup"><span data-stu-id="74499-162">Who?</span></span> <span data-ttu-id="74499-163">何時？</span><span class="sxs-lookup"><span data-stu-id="74499-163">When?</span></span> <span data-ttu-id="74499-164">- -您一直想要詢問之問題的答案</span><span class="sxs-lookup"><span data-stu-id="74499-164">- Answers to questions you always wanted to ask</span></span>
* <span data-ttu-id="74499-165">[**疑難排解**](active-directory-passwords-troubleshoot.md) - 了解如何解決我們看到的 SSPR 常見問題</span><span class="sxs-lookup"><span data-stu-id="74499-165">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how to resolve common issues that we see with SSPR</span></span>

