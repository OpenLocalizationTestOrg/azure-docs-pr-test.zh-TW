---
title: "aaaAzure AD 分層密碼安全性 |Microsoft 文件"
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
ms.openlocfilehash: 10d8b600d9f4c02355b2cd8c5dccf8505aaf210d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="a-multi-tiered-approach-tooazure-ad-password-security"></a><span data-ttu-id="f9c3d-103">多層式方法 tooAzure AD 密碼安全性</span><span class="sxs-lookup"><span data-stu-id="f9c3d-103">A multi-tiered approach tooAzure AD password security</span></span>

<span data-ttu-id="f9c3d-104">本文將告訴您您的 Azure Active Directory (Azure AD) 或 Microsoft 帳戶可以依照使用者或系統管理員 tooprotect 身分的一些最佳作法。</span><span class="sxs-lookup"><span data-stu-id="f9c3d-104">This article discusses some best practices you can follow as a user or as an administrator tooprotect your Azure Active Directory (Azure AD) or Microsoft Account.</span></span>

 > [!NOTE]
 > <span data-ttu-id="f9c3d-105">Azure AD 系統管理員可以重設使用者密碼使用 hello 文件中的 hello 指引[Azure Active Directory 中的使用者重設 hello 密碼](active-directory-users-reset-password-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="f9c3d-105">Azure AD administrators can reset user passwords using hello guidance in hello article [Reset hello password for a user in Azure Active Directory](active-directory-users-reset-password-azure-portal.md).</span></span>
 >
 > <span data-ttu-id="f9c3d-106">使用者可以重設自己的密碼使用 hello 文件中的 hello 指引[我忘記密碼 Azure AD 說明](active-directory-passwords-update-your-own-password.md)。</span><span class="sxs-lookup"><span data-stu-id="f9c3d-106">Users can reset their own password using hello guidance in hello article [Help I forgot my Azure AD password](active-directory-passwords-update-your-own-password.md).</span></span>
 >

## <a name="password-requirements"></a><span data-ttu-id="f9c3d-107">密碼需求</span><span class="sxs-lookup"><span data-stu-id="f9c3d-107">Password requirements</span></span>

<span data-ttu-id="f9c3d-108">Azure AD 會併入 hello 遵循一般的方法 toosecuring 密碼：</span><span class="sxs-lookup"><span data-stu-id="f9c3d-108">Azure AD incorporates hello following common approaches toosecuring passwords:</span></span>

* <span data-ttu-id="f9c3d-109">密碼長度需求</span><span class="sxs-lookup"><span data-stu-id="f9c3d-109">Password length requirements</span></span>
* <span data-ttu-id="f9c3d-110">密碼複雜性需求</span><span class="sxs-lookup"><span data-stu-id="f9c3d-110">Password complexity requirements</span></span>
* <span data-ttu-id="f9c3d-111">一般和定期密碼到期</span><span class="sxs-lookup"><span data-stu-id="f9c3d-111">Regular and periodic password expiration</span></span>

<span data-ttu-id="f9c3d-112">如需 Azure Active Directory 中重設密碼資訊，請參閱 hello 主題[Azure AD 自助式密碼重設 hello IT 專業人員](active-directory-passwords.md)。</span><span class="sxs-lookup"><span data-stu-id="f9c3d-112">For information about password reset in Azure Active Directory, see hello topic [Azure AD self-service password reset for hello IT professional](active-directory-passwords.md).</span></span>

## <a name="azure-ad-password-protections"></a><span data-ttu-id="f9c3d-113">Azure AD 密碼保護</span><span class="sxs-lookup"><span data-stu-id="f9c3d-113">Azure AD password protections</span></span>

<span data-ttu-id="f9c3d-114">Azure AD 與 Microsoft 帳戶系統使用已知的業界 hello 方法 tooensure 安全保護的使用者和系統管理員的密碼，包括：</span><span class="sxs-lookup"><span data-stu-id="f9c3d-114">Azure AD and hello Microsoft Account System use industry proven approaches tooensure secure protection of user and administrator passwords including:</span></span>

* <span data-ttu-id="f9c3d-115">動態禁用的密碼</span><span class="sxs-lookup"><span data-stu-id="f9c3d-115">Dynamically banned passwords</span></span>
* <span data-ttu-id="f9c3d-116">智慧型密碼鎖定</span><span class="sxs-lookup"><span data-stu-id="f9c3d-116">Smart Password Lockout</span></span>

<span data-ttu-id="f9c3d-117">根據目前的研究的密碼管理的相關資訊，請參閱 hello 白皮書[密碼指引](http://aka.ms/passwordguidance)。</span><span class="sxs-lookup"><span data-stu-id="f9c3d-117">For information about password management based on current research, see hello whitepaper [Password Guidance](http://aka.ms/passwordguidance).</span></span>

### <a name="dynamically-banned-passwords"></a><span data-ttu-id="f9c3d-118">動態禁用的密碼</span><span class="sxs-lookup"><span data-stu-id="f9c3d-118">Dynamically banned passwords</span></span>

<span data-ttu-id="f9c3d-119">Azure AD 和 Microsoft 帳戶藉由動態禁用常見密碼來提供密碼保護。</span><span class="sxs-lookup"><span data-stu-id="f9c3d-119">Azure AD and Microsoft Accounts safeguard password protection by dynamically banning commonly used passwords.</span></span> <span data-ttu-id="f9c3d-120">hello Azure 識別碼識別身分保護小組定期分析禁止的密碼清單，防止使用者選取常使用的密碼。</span><span class="sxs-lookup"><span data-stu-id="f9c3d-120">hello Azure ID Identity Protection team routinely analyzes banned password lists, preventing users from selecting commonly used passwords.</span></span> <span data-ttu-id="f9c3d-121">此服務是使用 tooAzure AD 和 hello Microsoft 帳戶服務的客戶。</span><span class="sxs-lookup"><span data-stu-id="f9c3d-121">This service is available tooAzure AD and hello Microsoft Account Service customers.</span></span>

<span data-ttu-id="f9c3d-122">建立密碼時, 很重要的系統管理員 tooencourage 使用者 toochoose 密碼片語包含字母、 數字、 字元或單字的唯一組合。</span><span class="sxs-lookup"><span data-stu-id="f9c3d-122">When creating passwords, it is important for administrators tooencourage users toochoose password phrases that include a unique combination of letters, numbers, characters, or words.</span></span> <span data-ttu-id="f9c3d-123">這種方式有助於幾乎不可能 toobe 危害但方便使用者 tooremember toomake 使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="f9c3d-123">This approach helps toomake user passwords nearly impossible toobe compromised but easier for users tooremember.</span></span>

#### <a name="password-breaches"></a><span data-ttu-id="f9c3d-124">密碼漏洞</span><span class="sxs-lookup"><span data-stu-id="f9c3d-124">Password breaches</span></span>

<span data-ttu-id="f9c3d-125">Microsoft 正在一律 toostay 前面網路罪犯的一個步驟。</span><span class="sxs-lookup"><span data-stu-id="f9c3d-125">Microsoft is always working toostay one step ahead of cyber-criminals.</span></span>

<span data-ttu-id="f9c3d-126">hello Azure AD Identity Protection 小組持續會分析常使用的密碼。</span><span class="sxs-lookup"><span data-stu-id="f9c3d-126">hello Azure AD Identity Protection team continually analyzes passwords that are commonly used.</span></span> <span data-ttu-id="f9c3d-127">網路罪犯也使用類似的策略 tooinform 其攻擊，例如建置[彩虹資料表](https://en.wikipedia.org/wiki/Rainbow_table)的破解密碼雜湊。</span><span class="sxs-lookup"><span data-stu-id="f9c3d-127">Cyber-criminals also use similar strategies tooinform their attacks, such as building a [rainbow table](https://en.wikipedia.org/wiki/Rainbow_table) for cracking password hashes.</span></span>

<span data-ttu-id="f9c3d-128">Microsoft 會持續分析[資料缺口](https://www.privacyrights.org/data-breaches)toomaintain 動態更新禁止的密碼清單中，以確保會禁止易受攻擊的密碼，才能實際威脅 tooAzure AD 客戶。</span><span class="sxs-lookup"><span data-stu-id="f9c3d-128">Microsoft continually analyzes [data breaches](https://www.privacyrights.org/data-breaches) toomaintain a dynamically updated banned password list, which ensures that vulnerable passwords are banned before they become a real threat tooAzure AD customers.</span></span> <span data-ttu-id="f9c3d-129">如需我們目前的安全性工作的詳細資訊，請參閱 hello [Microsoft 安全性智慧報表](https://www.microsoft.com/security/sir/default.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f9c3d-129">For more information about our current security efforts, see hello [Microsoft Security Intelligence Report](https://www.microsoft.com/security/sir/default.aspx).</span></span>

### <a name="smart-password-lockout"></a><span data-ttu-id="f9c3d-130">智慧型密碼鎖定</span><span class="sxs-lookup"><span data-stu-id="f9c3d-130">Smart Password Lockout</span></span>

<span data-ttu-id="f9c3d-131">當 Azure AD 偵測到潛在的網路罪犯嘗試 toohack 到使用者密碼時，我們會鎖定 hello 智慧密碼鎖定的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="f9c3d-131">When Azure AD detects a potential cyber-criminal trying toohack into a user password, we lock hello user account with Smart Password Lockout.</span></span> <span data-ttu-id="f9c3d-132">Azure AD 設計 toodetermine hello 風險與特定登入工作階段相關聯。</span><span class="sxs-lookup"><span data-stu-id="f9c3d-132">Azure AD is designed toodetermine hello risk associated with specific login sessions.</span></span> <span data-ttu-id="f9c3d-133">然後使用 hello 最新的安全性資料，我們套用鎖定語意 toostop e-security 威脅。</span><span class="sxs-lookup"><span data-stu-id="f9c3d-133">Then using hello most up-to-date security data, we apply lockout semantics toostop cyber threats.</span></span>

<span data-ttu-id="f9c3d-134">如果使用者已鎖定超出 Azure AD，其螢幕看起來類似 toohello 遵循的其中一個：</span><span class="sxs-lookup"><span data-stu-id="f9c3d-134">If a user is locked out of Azure AD, their screen looks similar toohello one that follows:</span></span>

  ![Azure AD 遭到鎖定](./media/active-directory-secure-passwords/locked-out-azuread.png)

<span data-ttu-id="f9c3d-136">針對其他 Microsoft 帳戶，其螢幕看起來類似 toohello 遵循的其中一個：</span><span class="sxs-lookup"><span data-stu-id="f9c3d-136">For other Microsoft accounts, their screen looks similar toohello one that follows:</span></span>

  ![Microsoft 帳戶遭到鎖定](./media/active-directory-secure-passwords/locked-out-ms-accounts.png)

<span data-ttu-id="f9c3d-138">如需 Azure Active Directory 中重設密碼資訊，請參閱 hello 主題[Azure AD 自助式密碼重設 hello IT 專業人員](active-directory-passwords.md)。</span><span class="sxs-lookup"><span data-stu-id="f9c3d-138">For information about password reset in Azure Active Directory, see hello topic [Azure AD self-service password reset for hello IT professional](active-directory-passwords.md).</span></span>

  >[!NOTE]
  ><span data-ttu-id="f9c3d-139">如果您是 Azure AD 管理員，您可能會想 toouse[用 Windows Hello](https://www.microsoft.com/windows/windows-hello) tooavoid 讓使用者完全建立傳統的密碼。</span><span class="sxs-lookup"><span data-stu-id="f9c3d-139">If you are an Azure AD administrator, you may want toouse [Windows Hello](https://www.microsoft.com/windows/windows-hello) tooavoid having your users create traditional passwords altogether.</span></span>
  >

## <a name="next-steps"></a><span data-ttu-id="f9c3d-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f9c3d-140">Next steps</span></span>

* [<span data-ttu-id="f9c3d-141">如何 tooupdate 您自己的密碼</span><span class="sxs-lookup"><span data-stu-id="f9c3d-141">How tooupdate your own password</span></span>](active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="f9c3d-142">hello Azure 身分識別管理的基本概念</span><span class="sxs-lookup"><span data-stu-id="f9c3d-142">hello fundamentals of Azure identity management</span></span>](fundamentals-identity.md)
* [<span data-ttu-id="f9c3d-143">密碼重設活動報告</span><span class="sxs-lookup"><span data-stu-id="f9c3d-143">Report on password reset activity</span></span>](active-directory-passwords-reporting.md)


