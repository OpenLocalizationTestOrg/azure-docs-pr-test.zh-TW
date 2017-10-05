---
title: "如何要求進行多重要素驗證 | Microsoft Docs"
description: "了解如何利用  Azure Active Directory Privileged Identity Management 擴充功能，為特殊權限的身分識別強制啟用 Multi-Factor Authentication (MFA)。"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 1e3dc4ad-3a6a-4a52-8417-3ca4f84ae05c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: b778774fa23be8219db3f716d79bac324a7de9d3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-require-mfa-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="517b4-103">Azure AD Privileged Identity Management：如何要求 MFA</span><span class="sxs-lookup"><span data-stu-id="517b4-103">How to require MFA in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="517b4-104">建議您針對所有系統管理員都要求進行多重要素驗證 (MFA)。</span><span class="sxs-lookup"><span data-stu-id="517b4-104">We recommend that you require multi-factor authentication (MFA) for all of your administrators.</span></span> <span data-ttu-id="517b4-105">這可降低密碼遭入侵所導致的攻擊風險。</span><span class="sxs-lookup"><span data-stu-id="517b4-105">This reduces the risk of an attack due to a compromised password.</span></span>

<span data-ttu-id="517b4-106">您可以要求使用者在登入時完成 MFA 挑戰。</span><span class="sxs-lookup"><span data-stu-id="517b4-106">You can require that users complete an MFA challenge when they sign in.</span></span> <span data-ttu-id="517b4-107">部落格文章 [MFA for Office 365 and MFA for Azure (MFA for Office 365 和 MFA for Azure)](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/) 比較 Office 和 Azure 訂用帳戶所包含的內容，以及 Microsoft Azure Multi-Factor Authentication 優惠提供的功能。</span><span class="sxs-lookup"><span data-stu-id="517b4-107">The blog post [MFA for Office 365 and MFA for Azure](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/) compares what is included in Office and Azure subscriptions, with the features contained in the Microsoft Azure Multi-Factor Authentication offering.</span></span>

<span data-ttu-id="517b4-108">您也可以要求使用者在啟用 Azure AD PIM 中的角色時，完成 MFA 挑戰。</span><span class="sxs-lookup"><span data-stu-id="517b4-108">You can also require that users complete an MFA challenge when they activate a role in Azure AD PIM.</span></span> <span data-ttu-id="517b4-109">如此一來，如果使用者沒有在登入時完成 MFA 挑戰，PIM 就會提示他們執行這項作業。</span><span class="sxs-lookup"><span data-stu-id="517b4-109">This way, if the user didn't complete an MFA challenge when they signed in, they will be prompted to do so by PIM.</span></span>

## <a name="requiring-mfa-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="517b4-110">在 Azure AD Privileged Identity Management 中強制啟用 MFA</span><span class="sxs-lookup"><span data-stu-id="517b4-110">Requiring MFA in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="517b4-111">當您以特殊權限角色管理員的身分管理 PIM 中的身分識別時，您可能會看到建議特殊權限帳戶使用 MFA 的警示。</span><span class="sxs-lookup"><span data-stu-id="517b4-111">When you manage identities in PIM as a privileged role administrator, you may see alerts that recommend MFA for privileged accounts.</span></span> <span data-ttu-id="517b4-112">按一下 PIM 儀表板中的安全性警示，新的刀鋒視窗會隨即開啟，並顯示應啟用 MFA 的系統管理員帳戶清單。</span><span class="sxs-lookup"><span data-stu-id="517b4-112">Click the security alert in the PIM dashboard, and a new blade will open with a list of the administrator accounts that should require MFA.</span></span>  <span data-ttu-id="517b4-113">您可以選取多個角色，然後按一下 [修正] 按鈕來要求使用 MFA；或者您也可以按一下個別角色旁邊的省略符號，然後按一下 [修正] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="517b4-113">You can require MFA by selecting multiple roles and then clicking the **Fix** button, or you can click the ellipses next to individual roles and then click the **Fix** button.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="517b4-114">目前 Azure MFA 只能與工作帳戶或學校帳戶搭配運作，而無法與 Microsoft 帳戶 (通常是用來登入 Skype、Xbox、Outlook.com 等 Microsoft 服務的個人帳戶) 搭配運作。</span><span class="sxs-lookup"><span data-stu-id="517b4-114">Right now, Azure MFA only works with work or school accounts, not Microsoft accounts (usually a personal account that's used to sign in to Microsoft services like Skype, Xbox, Outlook.com, etc.).</span></span> <span data-ttu-id="517b4-115">因此，任何使用者只要是使用 Microsoft 帳戶就無法成為合格的系統管理員，因為他們無法使用 MFA 來啟用其角色。</span><span class="sxs-lookup"><span data-stu-id="517b4-115">Because of this, anyone using a Microsoft account can't be an eligible admin because they can't use MFA to activate their roles.</span></span> <span data-ttu-id="517b4-116">如果這些使用者需要繼續使用 Microsoft 帳戶來管理工作負載，請立即將他們提升為永久系統管理員。</span><span class="sxs-lookup"><span data-stu-id="517b4-116">If these users need to continue managing workloads using a Microsoft account, elevate them to permanent administrators for now.</span></span>
> 
> 

<span data-ttu-id="517b4-117">或者，您也可以在 PIM 儀表板的 [角色] 區段中按一下特定角色，變更它的 MFA 需求。</span><span class="sxs-lookup"><span data-stu-id="517b4-117">Additionally, you can change the MFA requirement for a specific role by clicking on it in the Roles section of the PIM dashboard.</span></span> <span data-ttu-id="517b4-118">接著，按一下角色刀鋒視窗中的 [設定]，然後選取多重要素驗證底下的 [啟用]。</span><span class="sxs-lookup"><span data-stu-id="517b4-118">Then, click on **Settings** in the role blade and then selecting **Enable** under multi-factor authentication.</span></span>

## <a name="how-azure-ad-pim-validates-mfa"></a><span data-ttu-id="517b4-119">Azure AD PIM 如何驗證 MFA</span><span class="sxs-lookup"><span data-stu-id="517b4-119">How Azure AD PIM validates MFA</span></span>
<span data-ttu-id="517b4-120">在使用者啟用角色時有兩個選項可用來驗證 MFA。</span><span class="sxs-lookup"><span data-stu-id="517b4-120">There are two options for validating MFA when a user activates a role.</span></span>

<span data-ttu-id="517b4-121">最簡單的選項是讓啟用特殊權限角色的使用者依賴 Azure MFA。</span><span class="sxs-lookup"><span data-stu-id="517b4-121">The simplest option is to rely on Azure MFA for users who are activating a privileged role.</span></span> <span data-ttu-id="517b4-122">若要這樣做，請先確認這些使用者已獲授權；必要時，針對 Azure MFA 進行註冊。</span><span class="sxs-lookup"><span data-stu-id="517b4-122">To do this, first check that those users are licensed, if necessary, and have registered for Azure MFA.</span></span> <span data-ttu-id="517b4-123">如需有關如何執行此動作的詳細資訊，請參閱 [開始在雲端中使用 Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)。</span><span class="sxs-lookup"><span data-stu-id="517b4-123">More information on how to do this is in [Getting started with Azure Multi-Factor Authentication in the cloud](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span> <span data-ttu-id="517b4-124">建議 (但非必要) 設定 Azure AD，在這些使用者登入時，強制為他們執行 MFA。</span><span class="sxs-lookup"><span data-stu-id="517b4-124">It is recommended, but not required, that you configure Azure AD to enforce MFA for these users when they sign in.</span></span> <span data-ttu-id="517b4-125">這是因為 MFA 檢查將是由 Azure AD PIM 本身所進行。</span><span class="sxs-lookup"><span data-stu-id="517b4-125">This is because the MFA checks will be made by Azure AD PIM itself.</span></span>

<span data-ttu-id="517b4-126">或者，如果使用者驗證內部部署，您可以讓您的身分識別提供者負責進行 MFA。</span><span class="sxs-lookup"><span data-stu-id="517b4-126">Alternatively, if users authenticate on-premises you can have your identity provider be responsible for MFA.</span></span> <span data-ttu-id="517b4-127">例如，如果您已在存取 Azure AD 之前將 Active Directory 同盟服務設定為需要以智慧卡為基礎的驗證， [使用 Azure Multi-Factor Authentication 與 AD FS 保護雲端資源](../multi-factor-authentication/multi-factor-authentication-get-started-adfs-cloud.md) 包含用來設定 AD FS 來將宣告傳送至 Azure AD 的相關指示。</span><span class="sxs-lookup"><span data-stu-id="517b4-127">For example, if you have configured AD Federation Services to require smartcard-based authentication before accessing Azure AD, [Securing cloud resources with Azure Multi-Factor Authentication and AD FS](../multi-factor-authentication/multi-factor-authentication-get-started-adfs-cloud.md) includes instructions for configuring AD FS to send claims to Azure AD.</span></span> <span data-ttu-id="517b4-128">當使用者嘗試啟動角色時，Azure AD PIM 將會在其收到適當宣告時，接受系統已針對使用者驗證過 MFA。</span><span class="sxs-lookup"><span data-stu-id="517b4-128">When a user tries to activate a role, Azure AD PIM will accept that MFA has already been validated for the user once it receives the appropriate claims.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="517b4-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="517b4-129">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

