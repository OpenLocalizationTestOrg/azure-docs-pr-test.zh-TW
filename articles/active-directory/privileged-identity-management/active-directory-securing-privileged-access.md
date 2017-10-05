---
title: "保護 Azure AD 的特殊權限存取 | Microsoft 文件"
description: "這個主題說明在 Azure、Azure Active Directory 和 Microsoft Online Services 之間保護特殊權限存取的方法。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: mwahl
ms.assetid: 235a0ce9-1daf-4433-8f65-9c6afcd64d08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: kgremban
ms.custom: pim
ms.openlocfilehash: acd1c11cecfa37f607fe5d82a76a40647093f43f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="securing-privileged-access-in-azure-ad"></a><span data-ttu-id="907b6-103">保護 Azure AD 中的特殊權限存取</span><span class="sxs-lookup"><span data-stu-id="907b6-103">Securing privileged access in Azure AD</span></span>
<span data-ttu-id="907b6-104">保護特殊權限存取，是有助保護現代組織企業資產很重要的第一個步驟。</span><span class="sxs-lookup"><span data-stu-id="907b6-104">Securing privileged access is a critical first step to help protect business assets in a modern organization.</span></span> <span data-ttu-id="907b6-105">特殊權限帳戶是可管理 IT 系統的帳戶。</span><span class="sxs-lookup"><span data-stu-id="907b6-105">Privileged accounts are accounts that administer and manage IT systems.</span></span> <span data-ttu-id="907b6-106">網路攻擊者會以這些帳戶為目標，來取得組織資料和系統的存取權。</span><span class="sxs-lookup"><span data-stu-id="907b6-106">Cyber-attackers target these accounts to gain access to an organization’s data and systems.</span></span> <span data-ttu-id="907b6-107">為了保護特殊權限存取，您應該讓帳戶和系統遠離遭遇惡意使用者的風險。</span><span class="sxs-lookup"><span data-stu-id="907b6-107">To secure privileged access, you should isolate the accounts and systems from the risk of being exposed to a malicious user.</span></span>

<span data-ttu-id="907b6-108">更多使用者開始透過雲端服務取得特殊權限存取。</span><span class="sxs-lookup"><span data-stu-id="907b6-108">More users are starting to get privileged access through cloud services.</span></span> <span data-ttu-id="907b6-109">這包括 Office365 的全域系統管理員、Azure 訂用帳戶系統管理員和有 VM 或 SaaS 應用程式系統管理存取權限的使用者。</span><span class="sxs-lookup"><span data-stu-id="907b6-109">This can include global administrators of Office365, Azure subscription administrators, and users who have administrative access in VMs or on SaaS apps.</span></span>

<span data-ttu-id="907b6-110">Microsoft 建議您遵循 [Securing Privileged Access (保護特殊權限存取)](https://technet.microsoft.com/library/mt631194.aspx)的這份藍圖。</span><span class="sxs-lookup"><span data-stu-id="907b6-110">Microsoft recommends you follow this roadmap on [Securing Privileged Access](https://technet.microsoft.com/library/mt631194.aspx).</span></span>

<span data-ttu-id="907b6-111">這些原則是否適用使用 Azure Active Directory、Office 365 或其他 Microsoft 服務和應用程式的客戶，取決於使用者帳戶是由 Active Directory 管理驗證，或在 Azure Active Directory 中管理驗證。</span><span class="sxs-lookup"><span data-stu-id="907b6-111">For customers using Azure Active Directory, Office 365, or other Microsoft services and applications, these principles apply whether user accounts are managed and authenticated by Active Directory or in Azure Active Directory.</span></span> <span data-ttu-id="907b6-112">下列章節提供支援保護特殊權限存取之 Azure AD 功能的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="907b6-112">The following sections provide more information on Azure AD features to support securing privileged access.</span></span>

## <a name="azure-multi-factor-authentication"></a><span data-ttu-id="907b6-113">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="907b6-113">Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="907b6-114">若要加強系統管理員驗證的安全性，您應先要求雙步驟驗證再授與權限。</span><span class="sxs-lookup"><span data-stu-id="907b6-114">To increase the security of administrator authentication, you should require two-step verification before granting privileges.</span></span> <span data-ttu-id="907b6-115">雙步驟驗證是除了使用使用者名稱與密碼之外，需要再利用其他方法驗證身分的驗證方法。</span><span class="sxs-lookup"><span data-stu-id="907b6-115">Two-step verification is a method of verifying who you are that requires the use of more than just a username and password.</span></span> <span data-ttu-id="907b6-116">它可以為使用者登入和交易提供第二層安全性。</span><span class="sxs-lookup"><span data-stu-id="907b6-116">It provides a second layer of security to user sign-ins and transactions.</span></span>

<span data-ttu-id="907b6-117">Azure Multi-Factor Authentication (MFA) 是 Microsoft 的雙步驟驗證解決方案，有助於保護對資料與應用程式的存取，同時可以滿足使用者對簡單登入程序的需求。</span><span class="sxs-lookup"><span data-stu-id="907b6-117">Azure Multi-Factor Authentication (MFA) is Microsoft's two-step verification solution, which helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="907b6-118">透過一系列簡單的驗證選項提供增強式驗證，選項包括：</span><span class="sxs-lookup"><span data-stu-id="907b6-118">It delivers strong authentication via a range of easy verification options including:</span></span>

- <span data-ttu-id="907b6-119">電話通話</span><span class="sxs-lookup"><span data-stu-id="907b6-119">phone calls</span></span>
- <span data-ttu-id="907b6-120">文字訊息</span><span class="sxs-lookup"><span data-stu-id="907b6-120">text messages</span></span>
- <span data-ttu-id="907b6-121">行動應用程式通知</span><span class="sxs-lookup"><span data-stu-id="907b6-121">mobile app notifications</span></span>
- <span data-ttu-id="907b6-122">行動應用程式驗證碼</span><span class="sxs-lookup"><span data-stu-id="907b6-122">mobile app verification codes</span></span>
- <span data-ttu-id="907b6-123">協力廠商 OATH 權杖</span><span class="sxs-lookup"><span data-stu-id="907b6-123">third-party OATH tokens</span></span>

<span data-ttu-id="907b6-124">如需 Azure Multi-Factor Authentication 運作方式的概觀，請參閱以下影片：</span><span class="sxs-lookup"><span data-stu-id="907b6-124">For an overview of how Azure Multi-Factor Authentication works see the following video:</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]

<span data-ttu-id="907b6-125">如需詳細資訊，請參閱 [MFA for Office 365 和 MFA for Azure](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/)。</span><span class="sxs-lookup"><span data-stu-id="907b6-125">For more information, see [MFA for Office 365 and MFA for Azure](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/).</span></span>

## <a name="time-bound-privileges"></a><span data-ttu-id="907b6-126">時間界限權限</span><span class="sxs-lookup"><span data-stu-id="907b6-126">Time-bound privileges</span></span>
<span data-ttu-id="907b6-127">某些組織可能會發現它們有太多擁有高權限角色的使用者。</span><span class="sxs-lookup"><span data-stu-id="907b6-127">Some organizations may find that they have too many users in highly privileged roles.</span></span> <span data-ttu-id="907b6-128">使用者可能因為某個特定活動，像是登入服務，而加入角色中，但之後卻不經常使用這些權限。</span><span class="sxs-lookup"><span data-stu-id="907b6-128">A user might have been added to the role for a particular activity, like to sign up for a service, but didn't use those privileges frequently afterward.</span></span>

<span data-ttu-id="907b6-129">若要降低權限的曝光時間，並增加其使用的能見度，請限制使用者只在需要執行工作時才 (Just in Time, JIT) 使用其權限。</span><span class="sxs-lookup"><span data-stu-id="907b6-129">To lower the exposure time of privileges and increase your visibility into their use, limit users to only taking on their privileges "just in time" (JIT), when they need to perform a task.</span></span> <span data-ttu-id="907b6-130">Azure Active Directory 與 Microsoft Online Services 可以使用 [Azure AD Privileged Identity Management (PIM)](http://aka.ms/AzurePIM)。</span><span class="sxs-lookup"><span data-stu-id="907b6-130">For Azure Active Directory and Microsoft Online Services, you can use [Azure AD Privileged Identity Management (PIM)](http://aka.ms/AzurePIM).</span></span>

![PIM 儀表板][2]

## <a name="attack-detection"></a><span data-ttu-id="907b6-132">攻擊偵測</span><span class="sxs-lookup"><span data-stu-id="907b6-132">Attack detection</span></span>
<span data-ttu-id="907b6-133">[Azure Active Directory Identity Protection](../active-directory-identityprotection.md) 提供整合的檢視，綜觀會影響組織身分識別的風險事件和潛在弱點。</span><span class="sxs-lookup"><span data-stu-id="907b6-133">[Azure Active Directory Identity Protection](../active-directory-identityprotection.md) provides a consolidated view into risk events and potential vulnerabilities affecting your organization’s identities.</span></span> <span data-ttu-id="907b6-134">Identity Protection 會根據風險事件，計算每位使用者的使用者風險層級，讓您設定以風險為基礎的原則來自動保護您組織的身分識別。</span><span class="sxs-lookup"><span data-stu-id="907b6-134">Based on risk events, Identity Protection calculates a user risk level for each user, enabling you to configure risk-based policies to automatically protect the identities of your organization.</span></span> <span data-ttu-id="907b6-135">這些原則和 Azure Active Directory 與 EMS 提供的其他條件式存取控制，可以自動封鎖使用者或提供建議，包括重設密碼以及強制 Multi-Factor Authentication。</span><span class="sxs-lookup"><span data-stu-id="907b6-135">These policies, along with other conditional access controls provided by Azure Active Directory and EMS, can automatically block the user or offer suggestions that include password resets and multi-factor authentication enforcement.</span></span>

![Azure AD Identity Protection][3]

## <a name="conditional-access"></a><span data-ttu-id="907b6-137">條件式存取</span><span class="sxs-lookup"><span data-stu-id="907b6-137">Conditional access</span></span>
<span data-ttu-id="907b6-138">搭配條件式存取控制時，Azure Active Directory 會在驗證使用者時先檢查您選擇的特定條件，然後才允許存取應用程式。</span><span class="sxs-lookup"><span data-stu-id="907b6-138">With conditional access control, Azure Active Directory checks the specific conditions you choose when authenticating a user, before allowing access to an application.</span></span> <span data-ttu-id="907b6-139">一旦符合這些條件，使用者就會通過驗證並獲允許存取應用程式。</span><span class="sxs-lookup"><span data-stu-id="907b6-139">Once those conditions are met, the user is authenticated and allowed access to the application.</span></span>

![使用 MFA 設定條件式存取規則][4]

## <a name="related-articles"></a><span data-ttu-id="907b6-141">相關文章</span><span class="sxs-lookup"><span data-stu-id="907b6-141">Related articles</span></span>
* <span data-ttu-id="907b6-142">啟用 [Azure Multi-Factor Authentication](../../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)</span><span class="sxs-lookup"><span data-stu-id="907b6-142">Enable [Azure Multi-Factor Authentication](../../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)</span></span>
* <span data-ttu-id="907b6-143">啟用 [Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-configure.md)</span><span class="sxs-lookup"><span data-stu-id="907b6-143">Enable [Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-configure.md)</span></span>
* <span data-ttu-id="907b6-144">啟用 [Azure AD Identity Protection](../active-directory-identityprotection.md)</span><span class="sxs-lookup"><span data-stu-id="907b6-144">Enable [Azure AD Identity Protection](../active-directory-identityprotection.md)</span></span>
* <span data-ttu-id="907b6-145">啟用[條件式存取控制](../active-directory-conditional-access.md)</span><span class="sxs-lookup"><span data-stu-id="907b6-145">Enable [conditional access controls](../active-directory-conditional-access.md)</span></span>

<span data-ttu-id="907b6-146">如需建置完整安全性藍圖的詳細資訊，請參閱 [Microsoft Cloud Security for Enterprise Architects (Microsoft 的企業架構雲端安全性)](http://aka.ms/securecustomer) 一文的＜Customer responsibilities and roadmap＞(客戶責任和藍圖) 一節。</span><span class="sxs-lookup"><span data-stu-id="907b6-146">For more information on building a complete security roadmap, see the “Customer responsibilities and roadmap” section of the [Microsoft Cloud Security for Enterprise Architects](http://aka.ms/securecustomer) document.</span></span> <span data-ttu-id="907b6-147">如需吸引人的 Microsoft 服務詳細資訊，協助您使用任一這些主題，請連絡您的 Microsoft 代表或瀏覽我們的 [Cybersecurity solutions (網路安全性方案) 網頁](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx)。</span><span class="sxs-lookup"><span data-stu-id="907b6-147">For more information on engaging Microsoft services to assist with any of these topics, contact your Microsoft representative or visit our [Cybersecurity solutions page](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx).</span></span>

<!--Image references-->
[1]: ../media/active-directory-privileged-identity-management-configure/Search_PIM.png
[2]: ../media/active-directory-privileged-identity-management-configure/PIM_Dash.png
[3]: ../media/active-directory-identityprotection/29.png
[4]: ../media/active-directory-conditional-access/conditionalaccess-saas-apps.png
