---
title: "Azure AD 多層密碼安全性 | Microsoft Docs"
description: "說明 Azure AD 如何強制執行強式密碼，及保護使用者密碼免遭網路罪犯破解。"
services: active-directory
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: joflore
ms.openlocfilehash: 32464307ccb082b25538eaa522c1cdedef1ca555
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="a-multi-tiered-approach-to-azure-ad-password-security"></a><span data-ttu-id="f8f29-103">Azure AD 密碼安全性多層法</span><span class="sxs-lookup"><span data-stu-id="f8f29-103">A multi-tiered approach to Azure AD password security</span></span>

<span data-ttu-id="f8f29-104">本文討論身為使用者或系統管理員的您可以遵循的一些最佳做法，以保護您的 Azure Active Directory (Azure AD) 或 Microsoft 帳戶帳戶。</span><span class="sxs-lookup"><span data-stu-id="f8f29-104">This article discusses some best practices you can follow as a user or as an administrator to protect your Azure Active Directory (Azure AD) or Microsoft Account.</span></span>

 > [!NOTE]
 > <span data-ttu-id="f8f29-105">Azure AD 系統管理員可以使用[重設 Azure Active Directory 中使用者密碼 (英文)](active-directory-users-reset-password-azure-portal.md) 一文中的指導方針重設使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="f8f29-105">Azure AD administrators can reset user passwords using the guidance in the article [Reset the password for a user in Azure Active Directory](active-directory-users-reset-password-azure-portal.md).</span></span>
 >
 > <span data-ttu-id="f8f29-106">使用者可以使用[忘記 Azure AD 密碼說明 (英文)](active-directory-passwords-update-your-own-password.md) 一文中的指導方針重設自己的密碼。</span><span class="sxs-lookup"><span data-stu-id="f8f29-106">Users can reset their own password using the guidance in the article [Help I forgot my Azure AD password](active-directory-passwords-update-your-own-password.md).</span></span>
 >

## <a name="password-requirements"></a><span data-ttu-id="f8f29-107">密碼需求</span><span class="sxs-lookup"><span data-stu-id="f8f29-107">Password requirements</span></span>

<span data-ttu-id="f8f29-108">Azure AD 併入下列一般方法來保護密碼︰</span><span class="sxs-lookup"><span data-stu-id="f8f29-108">Azure AD incorporates the following common approaches to securing passwords:</span></span>

* <span data-ttu-id="f8f29-109">密碼長度需求</span><span class="sxs-lookup"><span data-stu-id="f8f29-109">Password length requirements</span></span>
* <span data-ttu-id="f8f29-110">密碼複雜性需求</span><span class="sxs-lookup"><span data-stu-id="f8f29-110">Password complexity requirements</span></span>
* <span data-ttu-id="f8f29-111">一般和定期密碼到期</span><span class="sxs-lookup"><span data-stu-id="f8f29-111">Regular and periodic password expiration</span></span>

<span data-ttu-id="f8f29-112">如需在 Azure Active Directory 中重設密碼的相關資訊，請參閱 [IT 專業人員的 Azure AD 自助式密碼重設 (英文) ](active-directory-passwords.md)主題。</span><span class="sxs-lookup"><span data-stu-id="f8f29-112">For information about password reset in Azure Active Directory, see the topic [Azure AD self-service password reset for the IT professional](active-directory-passwords.md).</span></span>

## <a name="azure-ad-password-protections"></a><span data-ttu-id="f8f29-113">Azure AD 密碼保護</span><span class="sxs-lookup"><span data-stu-id="f8f29-113">Azure AD password protections</span></span>

<span data-ttu-id="f8f29-114">Azure AD 和 Microsoft 帳戶系統使用業界證實可行的方法，以確保使用者和系統管理員密碼的保護，包括：</span><span class="sxs-lookup"><span data-stu-id="f8f29-114">Azure AD and the Microsoft Account System use industry proven approaches to ensure secure protection of user and administrator passwords including:</span></span>

* <span data-ttu-id="f8f29-115">動態禁用的密碼</span><span class="sxs-lookup"><span data-stu-id="f8f29-115">Dynamically banned passwords</span></span>
* <span data-ttu-id="f8f29-116">智慧型密碼鎖定</span><span class="sxs-lookup"><span data-stu-id="f8f29-116">Smart Password Lockout</span></span>

<span data-ttu-id="f8f29-117">如需以目前研究為基礎的密碼管理相關資訊，請參閱[密碼指引 (英文)](http://aka.ms/passwordguidance) 白皮書。</span><span class="sxs-lookup"><span data-stu-id="f8f29-117">For information about password management based on current research, see the whitepaper [Password Guidance](http://aka.ms/passwordguidance).</span></span>

### <a name="dynamically-banned-passwords"></a><span data-ttu-id="f8f29-118">動態禁用的密碼</span><span class="sxs-lookup"><span data-stu-id="f8f29-118">Dynamically banned passwords</span></span>

<span data-ttu-id="f8f29-119">Azure AD 和 Microsoft 帳戶藉由動態禁用常見密碼來提供密碼保護。</span><span class="sxs-lookup"><span data-stu-id="f8f29-119">Azure AD and Microsoft Accounts safeguard password protection by dynamically banning commonly used passwords.</span></span> <span data-ttu-id="f8f29-120">Azure ID Identity Protection 小組會定期分析遭到禁用的密碼清單，並防止使用者選取常用的密碼。</span><span class="sxs-lookup"><span data-stu-id="f8f29-120">The Azure ID Identity Protection team routinely analyzes banned password lists, preventing users from selecting commonly used passwords.</span></span> <span data-ttu-id="f8f29-121">此服務適用於 Azure AD 和 Microsoft 帳戶服務客戶。</span><span class="sxs-lookup"><span data-stu-id="f8f29-121">This service is available to Azure AD and the Microsoft Account Service customers.</span></span>

<span data-ttu-id="f8f29-122">建立密碼時，系統管理員務必鼓勵使用者選擇密碼片語，片語中須包含唯一的字母、數字、字元或文字組合。</span><span class="sxs-lookup"><span data-stu-id="f8f29-122">When creating passwords, it is important for administrators to encourage users to choose password phrases that include a unique combination of letters, numbers, characters, or words.</span></span> <span data-ttu-id="f8f29-123">這種方法有助於讓使用者密碼幾乎不可能遭到入侵，但使用者更容易記住。</span><span class="sxs-lookup"><span data-stu-id="f8f29-123">This approach helps to make user passwords nearly impossible to be compromised but easier for users to remember.</span></span>

#### <a name="password-breaches"></a><span data-ttu-id="f8f29-124">密碼漏洞</span><span class="sxs-lookup"><span data-stu-id="f8f29-124">Password breaches</span></span>

<span data-ttu-id="f8f29-125">Microsoft 一直努力在網路罪犯發生前加以防範。</span><span class="sxs-lookup"><span data-stu-id="f8f29-125">Microsoft is always working to stay one step ahead of cyber-criminals.</span></span>

<span data-ttu-id="f8f29-126">Azure AD Identity Protection 小組會持續分析常用的密碼。</span><span class="sxs-lookup"><span data-stu-id="f8f29-126">The Azure AD Identity Protection team continually analyzes passwords that are commonly used.</span></span> <span data-ttu-id="f8f29-127">網路罪犯也會使用類似的策略來告知其攻擊，例如建立[彩虹表](https://en.wikipedia.org/wiki/Rainbow_table)用來破解密碼雜湊。</span><span class="sxs-lookup"><span data-stu-id="f8f29-127">Cyber-criminals also use similar strategies to inform their attacks, such as building a [rainbow table](https://en.wikipedia.org/wiki/Rainbow_table) for cracking password hashes.</span></span>

<span data-ttu-id="f8f29-128">Microsoft 會持續分析[資料外洩](https://www.privacyrights.org/data-breaches)，以維護動態更新的禁用密碼清單，進而確保易受攻擊的密碼在成為 Azure AD 客戶的真正威脅之前遭到禁用。</span><span class="sxs-lookup"><span data-stu-id="f8f29-128">Microsoft continually analyzes [data breaches](https://www.privacyrights.org/data-breaches) to maintain a dynamically updated banned password list, which ensures that vulnerable passwords are banned before they become a real threat to Azure AD customers.</span></span> <span data-ttu-id="f8f29-129">如需目前安全性成果的詳細資訊，請參閱 [Microsoft Security Intelligence Report](https://www.microsoft.com/security/sir/default.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f8f29-129">For more information about our current security efforts, see the [Microsoft Security Intelligence Report](https://www.microsoft.com/security/sir/default.aspx).</span></span>

### <a name="smart-password-lockout"></a><span data-ttu-id="f8f29-130">智慧型密碼鎖定</span><span class="sxs-lookup"><span data-stu-id="f8f29-130">Smart Password Lockout</span></span>

<span data-ttu-id="f8f29-131">當 Azure AD 偵測到潛在網路罪犯嘗試入侵使用者密碼時，我們會使用智慧密碼鎖定來鎖定使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="f8f29-131">When Azure AD detects a potential cyber-criminal trying to hack into a user password, we lock the user account with Smart Password Lockout.</span></span> <span data-ttu-id="f8f29-132">Azure AD 設計用來判斷與特定登入工作階段相關聯的風險。</span><span class="sxs-lookup"><span data-stu-id="f8f29-132">Azure AD is designed to determine the risk associated with specific login sessions.</span></span> <span data-ttu-id="f8f29-133">接著我們會使用最新的安全性資料，來套用鎖定語意以阻止網路威脅。</span><span class="sxs-lookup"><span data-stu-id="f8f29-133">Then using the most up-to-date security data, we apply lockout semantics to stop cyber threats.</span></span>

<span data-ttu-id="f8f29-134">如果使用者的 Azure AD 遭到鎖定，其畫面如下所示︰</span><span class="sxs-lookup"><span data-stu-id="f8f29-134">If a user is locked out of Azure AD, their screen looks similar to the one that follows:</span></span>

  ![Azure AD 遭到鎖定](./media/active-directory-secure-passwords/locked-out-azuread.png)

<span data-ttu-id="f8f29-136">對於其他 Microsoft 帳戶，其畫面如下所示︰</span><span class="sxs-lookup"><span data-stu-id="f8f29-136">For other Microsoft accounts, their screen looks similar to the one that follows:</span></span>

  ![Microsoft 帳戶遭到鎖定](./media/active-directory-secure-passwords/locked-out-ms-accounts.png)

<span data-ttu-id="f8f29-138">如需在 Azure Active Directory 中重設密碼的相關資訊，請參閱 [IT 專業人員的 Azure AD 自助式密碼重設 (英文) ](active-directory-passwords.md)主題。</span><span class="sxs-lookup"><span data-stu-id="f8f29-138">For information about password reset in Azure Active Directory, see the topic [Azure AD self-service password reset for the IT professional](active-directory-passwords.md).</span></span>

  >[!NOTE]
  ><span data-ttu-id="f8f29-139">如果您是 Azure AD 系統管理員，可以使用 [Windows Hello](https://www.microsoft.com/windows/windows-hello) 全然避免使用者建立傳統密碼。</span><span class="sxs-lookup"><span data-stu-id="f8f29-139">If you are an Azure AD administrator, you may want to use [Windows Hello](https://www.microsoft.com/windows/windows-hello) to avoid having your users create traditional passwords altogether.</span></span>
  >

## <a name="next-steps"></a><span data-ttu-id="f8f29-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f8f29-140">Next steps</span></span>

* [<span data-ttu-id="f8f29-141">如何更新自己的密碼</span><span class="sxs-lookup"><span data-stu-id="f8f29-141">How to update your own password</span></span>](active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="f8f29-142">Azure 身分識別管理的基本概念</span><span class="sxs-lookup"><span data-stu-id="f8f29-142">The fundamentals of Azure identity management</span></span>](fundamentals-identity.md)
* [<span data-ttu-id="f8f29-143">密碼重設活動報告</span><span class="sxs-lookup"><span data-stu-id="f8f29-143">Report on password reset activity</span></span>](active-directory-passwords-reporting.md)


