---
title: "Active Directory 識別身分保護 aaaAzure |Microsoft 文件"
description: "了解如何 Azure AD Identity Protection 可讓您 toolimit hello 能力，攻擊者 tooexploit 遭盜用身分識別的裝置或 toosecure 盜用身分識別或先前已 toobe 可疑或已知的裝置。"
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, 管理應用程式, 安全性, 風險, 風險層級, 弱點, 安全性原則"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: e7434eeb-4e98-4b6b-a895-b5598a6cccf1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: ecca4f3cdb65585687cf44a80024f26c7cab22ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection"></a><span data-ttu-id="07ad0-104">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="07ad0-104">Azure Active Directory Identity Protection</span></span>

<span data-ttu-id="07ad0-105">Azure Active Directory 識別身分保護是可讓您的 Azure AD Premium P2 hello 版本的功能：</span><span class="sxs-lookup"><span data-stu-id="07ad0-105">Azure Active Directory Identity Protection is a feature of hello Azure AD Premium P2 edition that enables you to:</span></span>

- <span data-ttu-id="07ad0-106">偵測會影響組織的身分識別的潛在弱點</span><span class="sxs-lookup"><span data-stu-id="07ad0-106">Detect potential vulnerabilities affecting your organization’s identities</span></span>

- <span data-ttu-id="07ad0-107">設定自動化的回應 toodetected 可疑動作相關的 tooyour 組織的身分識別</span><span class="sxs-lookup"><span data-stu-id="07ad0-107">Configure automated responses toodetected suspicious actions that are related tooyour organization’s identities</span></span>  

- <span data-ttu-id="07ad0-108">調查可疑的事件，並採取適當的動作 tooresolve 它們</span><span class="sxs-lookup"><span data-stu-id="07ad0-108">Investigate suspicious incidents and take appropriate action tooresolve them</span></span>   


## <a name="getting-started"></a><span data-ttu-id="07ad0-109">開始使用</span><span class="sxs-lookup"><span data-stu-id="07ad0-109">Getting started</span></span>

<span data-ttu-id="07ad0-110">Microsoft 保護雲端身分識別已經超過十多年。</span><span class="sxs-lookup"><span data-stu-id="07ad0-110">Microsoft secures cloud-based identities for more than a decade.</span></span> <span data-ttu-id="07ad0-111">Azure Active Directory 識別身分保護，在您環境中，您可以使用 hello 相同保護系統 Microsoft 會使用 toosecure 身分識別。</span><span class="sxs-lookup"><span data-stu-id="07ad0-111">With Azure Active Directory Identity Protection, in your environment, you can use hello same protection systems Microsoft uses toosecure identities.</span></span>

<span data-ttu-id="07ad0-112">攻擊者竊取使用者的身分識別取得存取 tooan 環境時，就會放置 hello 大部分的安全性缺口，這需要。</span><span class="sxs-lookup"><span data-stu-id="07ad0-112">hello vast majority of security breaches take place when attackers gain access tooan environment by stealing a user’s identity.</span></span> <span data-ttu-id="07ad0-113">Hello 年來，攻擊者已成為逐漸有效運用第三方漏洞，並使用複雜的網路釣魚攻擊。</span><span class="sxs-lookup"><span data-stu-id="07ad0-113">Over hello years, attackers have become increasingly effective in leveraging third party breaches and using sophisticated phishing attacks.</span></span> <span data-ttu-id="07ad0-114">攻擊者存取 tooeven 低特殊權限的使用者帳戶，因為它是相當簡單，透過橫向移動 toogain 存取 tooimportant 公司資源。</span><span class="sxs-lookup"><span data-stu-id="07ad0-114">As soon as an attacker gains access tooeven low privileged user accounts, it is relatively easy for them toogain access tooimportant company resources through lateral movement.</span></span>

<span data-ttu-id="07ad0-115">如此一來，您必須：</span><span class="sxs-lookup"><span data-stu-id="07ad0-115">As a consequence of this, you need to:</span></span>

- <span data-ttu-id="07ad0-116">保護所有的識別身分，不論其權限層級</span><span class="sxs-lookup"><span data-stu-id="07ad0-116">Protect all identities regardless of their privilege level</span></span>

- <span data-ttu-id="07ad0-117">主動防止遭入侵的身分識別被濫用</span><span class="sxs-lookup"><span data-stu-id="07ad0-117">Proactively prevent compromised identities from being abused</span></span>

<span data-ttu-id="07ad0-118">探索遭入侵的身分識別並不容易。</span><span class="sxs-lookup"><span data-stu-id="07ad0-118">Discovering compromised identities is no easy task.</span></span> <span data-ttu-id="07ad0-119">啟發學習法 toodetect 異常和可疑的事件，以表示可能會受到危害之身分識別和 azure Active Directory 使用彈性的機器學習演算法。</span><span class="sxs-lookup"><span data-stu-id="07ad0-119">Azure Active Directory uses adaptive machine learning algorithms and heuristics toodetect anomalies and suspicious incidents that indicate potentially compromised identities.</span></span> <span data-ttu-id="07ad0-120">Identity Protection 使用這項資料，產生的報告和警示，讓您 tooevaluate hello 偵測到問題並採取適當的安全防護或修復動作。</span><span class="sxs-lookup"><span data-stu-id="07ad0-120">Using this data, Identity Protection generates reports and alerts that enable you tooevaluate hello detected issues and take appropriate mitigation or remediation actions.</span></span>

<span data-ttu-id="07ad0-121">Azure Active Directory Identity Protection 不只是監視和報告工具而已。</span><span class="sxs-lookup"><span data-stu-id="07ad0-121">Azure Active Directory Identity Protection is more than a monitoring and reporting tool.</span></span> <span data-ttu-id="07ad0-122">tooprotect 貴組織的身分識別，您可以設定在達到指定的風險層級時，自動回應 toodetected 問題的風險為基礎原則。</span><span class="sxs-lookup"><span data-stu-id="07ad0-122">tooprotect your organization's identities, you can configure risk-based policies that automatically respond toodetected issues when a specified risk level has been reached.</span></span> <span data-ttu-id="07ad0-123">這些原則，除了 tooother 條件式存取 Azure Active Directory 和 EMS 所提供的控制項，可以自動封鎖或起始自動調整的修復動作，包括密碼重設以及強制多因素驗證。</span><span class="sxs-lookup"><span data-stu-id="07ad0-123">These policies, in addition tooother conditional access controls provided by Azure Active Directory and EMS, can either automatically block or initiate adaptive remediation actions including password resets and multi-factor authentication enforcement.</span></span>


#### <a name="identity-protection-capabilities"></a><span data-ttu-id="07ad0-124">Identity Protection 功能</span><span class="sxs-lookup"><span data-stu-id="07ad0-124">Identity Protection capabilities</span></span>

<span data-ttu-id="07ad0-125">**偵測弱點和風險帳戶：**</span><span class="sxs-lookup"><span data-stu-id="07ad0-125">**Detecting vulnerabilities and risky accounts:**</span></span>  

* <span data-ttu-id="07ad0-126">提供自訂的建議 tooimprove 透過的弱點可能會反白顯示整體的安全性狀態</span><span class="sxs-lookup"><span data-stu-id="07ad0-126">Providing custom recommendations tooimprove overall security posture by highlighting vulnerabilities</span></span>
* <span data-ttu-id="07ad0-127">計算登入風險層級</span><span class="sxs-lookup"><span data-stu-id="07ad0-127">Calculating sign-in risk levels</span></span>
* <span data-ttu-id="07ad0-128">計算使用者風險層級</span><span class="sxs-lookup"><span data-stu-id="07ad0-128">Calculating user risk levels</span></span>


<span data-ttu-id="07ad0-129">**調查風險事件：**</span><span class="sxs-lookup"><span data-stu-id="07ad0-129">**Investigating risk events:**</span></span>

* <span data-ttu-id="07ad0-130">傳送風險事件的通知</span><span class="sxs-lookup"><span data-stu-id="07ad0-130">Sending notifications for risk events</span></span>
* <span data-ttu-id="07ad0-131">使用相關和內容資訊來調查風險事件</span><span class="sxs-lookup"><span data-stu-id="07ad0-131">Investigating risk events using relevant and contextual information</span></span>
* <span data-ttu-id="07ad0-132">提供基本工作流程 tootrack 調查</span><span class="sxs-lookup"><span data-stu-id="07ad0-132">Providing basic workflows tootrack investigations</span></span>
* <span data-ttu-id="07ad0-133">讓您輕鬆存取 tooremediation 動作，例如密碼重設</span><span class="sxs-lookup"><span data-stu-id="07ad0-133">Providing easy access tooremediation actions such as password reset</span></span>

<span data-ttu-id="07ad0-134">**以風險為基礎的條件式存取原則：**</span><span class="sxs-lookup"><span data-stu-id="07ad0-134">**Risk-based conditional access policies:**</span></span>

* <span data-ttu-id="07ad0-135">原則 toomitigate 風險登入所封鎖登入，或要求多重要素驗證挑戰。</span><span class="sxs-lookup"><span data-stu-id="07ad0-135">Policy toomitigate risky sign-ins by blocking sign-ins or requiring multi-factor authentication challenges.</span></span>
* <span data-ttu-id="07ad0-136">原則 tooblock 或安全風險的使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="07ad0-136">Policy tooblock or secure risky user accounts</span></span>
* <span data-ttu-id="07ad0-137">原則 toorequire 使用者 tooregister 的多重要素驗證</span><span class="sxs-lookup"><span data-stu-id="07ad0-137">Policy toorequire users tooregister for multi-factor authentication</span></span>



## <a name="identity-protection-roles"></a><span data-ttu-id="07ad0-138">Identity Protection 角色</span><span class="sxs-lookup"><span data-stu-id="07ad0-138">Identity Protection roles</span></span>

<span data-ttu-id="07ad0-139">tooload 平衡 hello 管理活動的識別身分保護實作，您可以指派有數個角色。</span><span class="sxs-lookup"><span data-stu-id="07ad0-139">tooload balance hello management activities around your Identity Protection implementation, you can assign several roles.</span></span> <span data-ttu-id="07ad0-140">Azure AD Identity Protection 支援 3 種目錄角色：</span><span class="sxs-lookup"><span data-stu-id="07ad0-140">Azure AD Identity Protection supports 3 directory roles:</span></span>

| <span data-ttu-id="07ad0-141">角色</span><span class="sxs-lookup"><span data-stu-id="07ad0-141">Role</span></span>                         | <span data-ttu-id="07ad0-142">可以執行</span><span class="sxs-lookup"><span data-stu-id="07ad0-142">Can do</span></span>                          | <span data-ttu-id="07ad0-143">無法執行</span><span class="sxs-lookup"><span data-stu-id="07ad0-143">Cannot do</span></span>
| :--                          | ---                                |  ---   |
| <span data-ttu-id="07ad0-144">全域管理員</span><span class="sxs-lookup"><span data-stu-id="07ad0-144">Global administrator</span></span>         | <span data-ttu-id="07ad0-145">完整存取 tooIdentity 保護，內建的識別身分保護</span><span class="sxs-lookup"><span data-stu-id="07ad0-145">Full access tooIdentity Protection, Onboard Identity Protection</span></span>| |
| <span data-ttu-id="07ad0-146">安全性系統管理員</span><span class="sxs-lookup"><span data-stu-id="07ad0-146">Security administrator</span></span>       | <span data-ttu-id="07ad0-147">完整存取 tooIdentity 保護</span><span class="sxs-lookup"><span data-stu-id="07ad0-147">Full access tooIdentity Protection</span></span> | <span data-ttu-id="07ad0-148">將 Identity Protection 上架、重設使用者密碼</span><span class="sxs-lookup"><span data-stu-id="07ad0-148">Onboard Identity Protection,  reset passwords for a user</span></span> |
| <span data-ttu-id="07ad0-149">安全性讀取者</span><span class="sxs-lookup"><span data-stu-id="07ad0-149">Security reader</span></span>              | <span data-ttu-id="07ad0-150">唯讀存取 tooIdentity 保護</span><span class="sxs-lookup"><span data-stu-id="07ad0-150">Ready-only access tooIdentity Protection</span></span> | <span data-ttu-id="07ad0-151">讓 Identity Protection 上線、修復使用者、設定原則、重設密碼</span><span class="sxs-lookup"><span data-stu-id="07ad0-151">Onboard Identity Protection, remidiate users, configure policies,  reset passwords</span></span> |




<span data-ttu-id="07ad0-152">如需詳細資訊，請參閱[在 Azure Active Directory 中指派系統管理員角色](active-directory-assign-admin-roles-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="07ad0-152">For more details, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)</span></span>



## <a name="detection"></a><span data-ttu-id="07ad0-153">偵測</span><span class="sxs-lookup"><span data-stu-id="07ad0-153">Detection</span></span>

### <a name="vulnerabilities"></a><span data-ttu-id="07ad0-154">弱點</span><span class="sxs-lookup"><span data-stu-id="07ad0-154">Vulnerabilities</span></span>

<span data-ttu-id="07ad0-155">Azure Active Directory Identity Protection 會分析您的組態，並偵測可能影響您使用者身份識別的弱點。</span><span class="sxs-lookup"><span data-stu-id="07ad0-155">Azure Active Directory Identity Protection analyses your configuration and detects vulnerabilities that can have an impact on your user's identities.</span></span> <span data-ttu-id="07ad0-156">如需詳細資訊，請參閱 [Azure Active Directory Identity Protection 偵測到的弱點](active-directory-identityprotection-vulnerabilities.md)。</span><span class="sxs-lookup"><span data-stu-id="07ad0-156">For more details, see [Vulnerabilities detected by Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md).</span></span>

### <a name="risk-events"></a><span data-ttu-id="07ad0-157">風險事件</span><span class="sxs-lookup"><span data-stu-id="07ad0-157">Risk events</span></span>

<span data-ttu-id="07ad0-158">Azure Active Directory 使用彈性的機器學習演算法和啟發學習法 toodetect 可疑動作相關的 tooyour 使用者的身分識別。</span><span class="sxs-lookup"><span data-stu-id="07ad0-158">Azure Active Directory uses adaptive machine learning algorithms and heuristics toodetect suspicious actions that are related tooyour user's identities.</span></span> <span data-ttu-id="07ad0-159">hello 系統會建立每個偵測到可疑的動作記錄。</span><span class="sxs-lookup"><span data-stu-id="07ad0-159">hello system creates a record for each detected suspicious action.</span></span> <span data-ttu-id="07ad0-160">這些記錄又名風險事件。</span><span class="sxs-lookup"><span data-stu-id="07ad0-160">These records are also known as risk events.</span></span>  
<span data-ttu-id="07ad0-161">如需詳細資訊，請參閱 [Azure Active Directory風險事件](active-directory-identity-protection-risk-events.md)。</span><span class="sxs-lookup"><span data-stu-id="07ad0-161">For more details, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span>


## <a name="investigation"></a><span data-ttu-id="07ad0-162">調查</span><span class="sxs-lookup"><span data-stu-id="07ad0-162">Investigation</span></span>
<span data-ttu-id="07ad0-163">此外，透過識別身分保護您旅途愉快通常會以 hello Identity Protection 儀表板啟動。</span><span class="sxs-lookup"><span data-stu-id="07ad0-163">Your journey through Identity Protection typically starts with hello Identity Protection dashboard.</span></span>

<span data-ttu-id="07ad0-164">![補救](./media/active-directory-identityprotection/1000.png "補救")</span><span class="sxs-lookup"><span data-stu-id="07ad0-164">![Remediation](./media/active-directory-identityprotection/1000.png "Remediation")</span></span>

<span data-ttu-id="07ad0-165">hello 儀表板可讓您：</span><span class="sxs-lookup"><span data-stu-id="07ad0-165">hello dashboard gives you access to:</span></span>

* <span data-ttu-id="07ad0-166">報告，例如 [標示有風險的使用者]、[風險事件] 和 [弱點]</span><span class="sxs-lookup"><span data-stu-id="07ad0-166">Reports such as **Users flagged for risk**, **Risk events** and **Vulnerabilities**</span></span>
* <span data-ttu-id="07ad0-167">設定，例如 hello 設定您**安全性原則**，**通知**和**註冊多重要素驗證**</span><span class="sxs-lookup"><span data-stu-id="07ad0-167">Settings such as hello configuration of your **Security Policies**, **Notifications** and **multi-factor authentication registration**</span></span>

<span data-ttu-id="07ad0-168">它通常是您開始進行調查，是檢閱 hello 活動、 記錄和相關的 tooa 的風險事件 toodecide 是否補救或安全防護功能步驟所需的其他相關資訊的 hello 程序，和 hello 身分識別的方式遭到洩露，而且了解如何 hello 盜用身分識別使用。</span><span class="sxs-lookup"><span data-stu-id="07ad0-168">It is typically your starting point for investigation, which is hello process of reviewing hello activities, logs, and other relevant information related tooa risk event toodecide whether remediation or mitigation steps are necessary,  and how hello identity was compromised, and understand how hello compromised identity was used.</span></span>

<span data-ttu-id="07ad0-169">您可以將繫結您調查活動 toohello[通知](active-directory-identityprotection-notifications.md)Azure Active Directory Protection 會將每個電子郵件傳送。</span><span class="sxs-lookup"><span data-stu-id="07ad0-169">You can tie your investigation activities toohello [notifications](active-directory-identityprotection-notifications.md) Azure Active Directory Protection sends per email.</span></span>

<span data-ttu-id="07ad0-170">hello 下列各節提供更多詳細資料和相關的 tooan 調查的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="07ad0-170">hello following sections provide you with more details and hello steps that are related tooan investigation.</span></span>  


## <a name="risky-sign-ins"></a><span data-ttu-id="07ad0-171">有風險的登入</span><span class="sxs-lookup"><span data-stu-id="07ad0-171">Risky sign-ins</span></span>

<span data-ttu-id="07ad0-172">Azure Active Directory 會以即時和離線方式偵測[風險事件類型](active-directory-reporting-risk-events.md#risk-event-types)。</span><span class="sxs-lookup"><span data-stu-id="07ad0-172">Azure Active Directory detects [risk event types](active-directory-reporting-risk-events.md#risk-event-types) in real-time and offline.</span></span> <span data-ttu-id="07ad0-173">每個偵測到的登入之使用者的風險事件佔 tooa 呼叫有風險的登入的邏輯概念。</span><span class="sxs-lookup"><span data-stu-id="07ad0-173">Each risk event that has been detected for a sign-in of a user contributes tooa logical concept called risky sign-in.</span></span> <span data-ttu-id="07ad0-174">高風險的登入是可能不是執行 hello 合法的使用者帳戶擁有者的登入嘗試的指標。</span><span class="sxs-lookup"><span data-stu-id="07ad0-174">A risky sign-in is an indicator for a sign-in attempt that might not have been performed by hello legitimate owner of a user account.</span></span>


### <a name="sign-in-risk-level"></a><span data-ttu-id="07ad0-175">登入風險層級</span><span class="sxs-lookup"><span data-stu-id="07ad0-175">Sign-in risk level</span></span>

<span data-ttu-id="07ad0-176">登入風險層級是 （高、 中或低） 的指示 hello 可能性 hello 合法的使用者帳戶擁有者未執行的登入嘗試。</span><span class="sxs-lookup"><span data-stu-id="07ad0-176">A sign-in risk level is an indication (High, Medium, or Low) of hello likelihood that a sign-in attempt was not performed by hello legitimate owner of a user account.</span></span>

### <a name="mitigating-sign-in-risk-events"></a><span data-ttu-id="07ad0-177">緩和登入風險事件</span><span class="sxs-lookup"><span data-stu-id="07ad0-177">Mitigating sign-in risk events</span></span>

<span data-ttu-id="07ad0-178">緩和措施是動作 toolimit hello 攻擊者 tooexploit 遭盜用身分識別或裝置的能力而不還原 hello 身分識別或裝置 tooa 安全狀態。</span><span class="sxs-lookup"><span data-stu-id="07ad0-178">A mitigation is an action toolimit hello ability of an attacker tooexploit a compromised identity or device without restoring hello identity or device tooa safe state.</span></span> <span data-ttu-id="07ad0-179">緩和措施無法解決先前 hello 身分識別或裝置相關聯的登入的風險事件。</span><span class="sxs-lookup"><span data-stu-id="07ad0-179">A mitigation does not resolve previous sign-in risk events associated with hello identity or device.</span></span>

<span data-ttu-id="07ad0-180">toomitigate 危險的登入，您可以設定登入風險安全性 policicies。</span><span class="sxs-lookup"><span data-stu-id="07ad0-180">toomitigate risky sign-ins automatically, you can configure sign-in risk security policicies.</span></span> <span data-ttu-id="07ad0-181">您使用這些原則，請考慮 hello 使用者或登入 tooblock hello hello 風險層級有風險的登入或需要 hello 使用者 tooperform 多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="07ad0-181">Using these policies, you consider hello risk level of hello user or hello sign-in tooblock risky sign-ins or require hello user tooperform multi-factor authentication.</span></span> <span data-ttu-id="07ad0-182">這些動作可能防止攻擊者利用身分識別遭竊的 toocause 損毀，而且可能會提供一些時間 toosecure hello 身分識別。</span><span class="sxs-lookup"><span data-stu-id="07ad0-182">These actions may prevent an attacker from exploiting a stolen identity toocause damage, and may give you some time toosecure hello identity.</span></span>

### <a name="sign-in-risk-security-policy"></a><span data-ttu-id="07ad0-183">登入風險安全性原則</span><span class="sxs-lookup"><span data-stu-id="07ad0-183">Sign-in risk security policy</span></span>
<span data-ttu-id="07ad0-184">登入風險原則是條件式存取原則，評估 hello 風險 tooa 特定登入，並根據預先定義的條件和規則的防護措施。</span><span class="sxs-lookup"><span data-stu-id="07ad0-184">A sign-in risk policy is a conditional access policy that evaluates hello risk tooa specific sign-in and applies mitigations based on predefined conditions and rules.</span></span>

<span data-ttu-id="07ad0-185">![登入風險原則](./media/active-directory-identityprotection/1014.png "登入風險原則")</span><span class="sxs-lookup"><span data-stu-id="07ad0-185">![Sign-in risk policy](./media/active-directory-identityprotection/1014.png "Sign-in risk policy")</span></span>

<span data-ttu-id="07ad0-186">Azure AD Identity Protection 可協助您管理讓您以 hello 緩和風險的登入的：</span><span class="sxs-lookup"><span data-stu-id="07ad0-186">Azure AD Identity Protection helps you manage hello mitigation of risky sign-ins by enabling you to:</span></span>

* <span data-ttu-id="07ad0-187">設定使用者和群組 hello 原則會套用至 hello:</span><span class="sxs-lookup"><span data-stu-id="07ad0-187">Set hello users and groups hello policy applies to:</span></span>

    <span data-ttu-id="07ad0-188">![登入風險原則](./media/active-directory-identityprotection/1015.png "登入風險原則")</span><span class="sxs-lookup"><span data-stu-id="07ad0-188">![Sign-in risk policy](./media/active-directory-identityprotection/1015.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="07ad0-189">設定 hello 登入風險層級閾值 （低、 中或高），會觸發 hello 原則：</span><span class="sxs-lookup"><span data-stu-id="07ad0-189">Set hello sign-in risk level threshold (low, medium, or high) that triggers hello policy:</span></span>

    <span data-ttu-id="07ad0-190">![登入風險原則](./media/active-directory-identityprotection/1016.png "登入風險原則")</span><span class="sxs-lookup"><span data-stu-id="07ad0-190">![Sign-in risk policy](./media/active-directory-identityprotection/1016.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="07ad0-191">設定 hello 控制項 toobe hello 原則觸發程序時，強制執行：</span><span class="sxs-lookup"><span data-stu-id="07ad0-191">Set hello controls toobe enforced when hello policy triggers:</span></span>  

    <span data-ttu-id="07ad0-192">![登入風險原則](./media/active-directory-identityprotection/1017.png "登入風險原則")</span><span class="sxs-lookup"><span data-stu-id="07ad0-192">![Sign-in risk policy](./media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="07ad0-193">切換原則的 hello 狀態：</span><span class="sxs-lookup"><span data-stu-id="07ad0-193">Switch hello state of your policy:</span></span>

    <span data-ttu-id="07ad0-194">![MFA 註冊](./media/active-directory-identityprotection/403.png "MFA 註冊")</span><span class="sxs-lookup"><span data-stu-id="07ad0-194">![MFA Registration](./media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="07ad0-195">檢閱和評估 hello 變更的影響層面之後再啟動它：</span><span class="sxs-lookup"><span data-stu-id="07ad0-195">Review and evaluate hello impact of a change before activating it:</span></span>

    <span data-ttu-id="07ad0-196">![登入風險原則](./media/active-directory-identityprotection/1018.png "登入風險原則")</span><span class="sxs-lookup"><span data-stu-id="07ad0-196">![Sign-in risk policy](./media/active-directory-identityprotection/1018.png "Sign-in risk policy")</span></span>

#### <a name="what-you-need-tooknow"></a><span data-ttu-id="07ad0-197">您的需要 tooknow</span><span class="sxs-lookup"><span data-stu-id="07ad0-197">What you need tooknow</span></span>
<span data-ttu-id="07ad0-198">您可以設定登入風險安全性原則 toorequire multi-factor authentication:</span><span class="sxs-lookup"><span data-stu-id="07ad0-198">You can configure a sign-in risk security policy toorequire multi-factor authentication:</span></span>

<span data-ttu-id="07ad0-199">![登入風險原則](./media/active-directory-identityprotection/1017.png "登入風險原則")</span><span class="sxs-lookup"><span data-stu-id="07ad0-199">![Sign-in risk policy](./media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>

<span data-ttu-id="07ad0-200">不過，基於安全性理由，這項設定只適用於已註冊 Multi-Factor Authentication 的使用者。</span><span class="sxs-lookup"><span data-stu-id="07ad0-200">However, for security reasons, this setting only works for users that have already been registered for multi-factor authentication.</span></span> <span data-ttu-id="07ad0-201">如果您尚未註冊多重要素驗證的使用者會滿足 hello 條件 toorequire 多重要素驗證，則會封鎖 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="07ad0-201">If hello condition toorequire multi-factor authentication is satisfied for a user who is not yet registered for multi-factor authentication, hello user is blocked.</span></span>

<span data-ttu-id="07ad0-202">最佳作法是，如果您想 toorequire 多重要素驗證的高風險登入，您應該：</span><span class="sxs-lookup"><span data-stu-id="07ad0-202">As a best practice, if you want toorequire multi-factor authentication for risky sign-ins, you should:</span></span>

1. <span data-ttu-id="07ad0-203">啟用 hello[多重要素驗證註冊原則](#multi-factor-authentication-registration-policy)hello 受影響的使用者。</span><span class="sxs-lookup"><span data-stu-id="07ad0-203">Enable hello [multi-factor authentication registration policy](#multi-factor-authentication-registration-policy) for hello affected users.</span></span>
2. <span data-ttu-id="07ad0-204">需要 hello 受影響使用者 toologin 中非有風險的工作階段 tooperform MFA 註冊</span><span class="sxs-lookup"><span data-stu-id="07ad0-204">Require hello affected users toologin in a non-risky session tooperform a MFA registration</span></span>

<span data-ttu-id="07ad0-205">完成這些步驟可確保有風險的登入一定需要 Multi-Factor Authentication。</span><span class="sxs-lookup"><span data-stu-id="07ad0-205">Completing these steps ensures that multi-factor authentication is required for a risky sign-in.</span></span>

#### <a name="best-practices"></a><span data-ttu-id="07ad0-206">最佳作法</span><span class="sxs-lookup"><span data-stu-id="07ad0-206">Best practices</span></span>
<span data-ttu-id="07ad0-207">選擇**高**臨界值會減少 hello 原則，就會觸發和次數 hello 影響 toousers 降到最低。</span><span class="sxs-lookup"><span data-stu-id="07ad0-207">Choosing a **High** threshold reduces hello number of times a policy is triggered and minimizes hello impact toousers.</span></span>  

<span data-ttu-id="07ad0-208">不過，它會排除**低**和**媒體**登入標示為從 hello 原則可能不會封鎖從高畫質視訊識別攻擊的風險。</span><span class="sxs-lookup"><span data-stu-id="07ad0-208">However, it excludes **Low** and **Medium** sign-ins flagged for risk from hello policy, which may not block an attacker from exploiting a compromised identity.</span></span>

<span data-ttu-id="07ad0-209">當設定 hello 原則</span><span class="sxs-lookup"><span data-stu-id="07ad0-209">When setting hello policy,</span></span>

* <span data-ttu-id="07ad0-210">排除不會 / 不能有 Multi-Factor Authentication 的使用者</span><span class="sxs-lookup"><span data-stu-id="07ad0-210">Exclude users who do not/cannot have multi-factor authentication</span></span>
* <span data-ttu-id="07ad0-211">排除使用者在其中啟用 hello 原則不是實際的地區設定 (例如沒有存取 toohelpdesk)</span><span class="sxs-lookup"><span data-stu-id="07ad0-211">Exclude users in locales where enabling hello policy is not practical (for example no access toohelpdesk)</span></span>
* <span data-ttu-id="07ad0-212">排除的使用者可能 toogenerate 大量 false 誤判 （開發人員、 安全性分析師）</span><span class="sxs-lookup"><span data-stu-id="07ad0-212">Exclude users who are likely toogenerate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="07ad0-213">在原則推出初期，或如果您必須盡量減少使用者所看到的挑戰，請使用 [高]  臨界值。</span><span class="sxs-lookup"><span data-stu-id="07ad0-213">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="07ad0-214">如果您的組織需要更高的安全性，請使用 [低]  臨界值。</span><span class="sxs-lookup"><span data-stu-id="07ad0-214">Use a **Low**  threshold if your organization requires greater security.</span></span> <span data-ttu-id="07ad0-215">選取 [低]  臨界值會帶來額外的使用者登入挑戰，並提高安全性。</span><span class="sxs-lookup"><span data-stu-id="07ad0-215">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="07ad0-216">大部分的組織是 tooconfigure 的規則，建議使用預設的 hello**媒體**閾值 toostrike 可用性和安全性之間取得平衡。</span><span class="sxs-lookup"><span data-stu-id="07ad0-216">hello recommended default for most organizations is tooconfigure a rule for a **Medium** threshold toostrike a balance between usability and security.</span></span>

<span data-ttu-id="07ad0-217">hello 登入風險原則是：</span><span class="sxs-lookup"><span data-stu-id="07ad0-217">hello sign-in risk policy is:</span></span>

* <span data-ttu-id="07ad0-218">套用的 tooall 瀏覽器，並使用新式驗證的登入。</span><span class="sxs-lookup"><span data-stu-id="07ad0-218">Applied tooall browser traffic and sign-ins using modern authentication.</span></span>
* <span data-ttu-id="07ad0-219">停用使用舊的安全性通訊協定不套用的 tooapplications hello hello 同盟 IDP，例如 ADFS Ws-trust 端點。</span><span class="sxs-lookup"><span data-stu-id="07ad0-219">Not applied tooapplications using older security protocols by disabling hello WS-Trust endpoint at hello federated IDP, such as ADFS.</span></span>

<span data-ttu-id="07ad0-220">hello**風險事件**hello Identity Protection 主控台中的頁面會列出所有事件：</span><span class="sxs-lookup"><span data-stu-id="07ad0-220">hello **Risk Events** page in hello Identity Protection console lists all events:</span></span>

* <span data-ttu-id="07ad0-221">此原則已套用至</span><span class="sxs-lookup"><span data-stu-id="07ad0-221">This policy was applied to</span></span>
* <span data-ttu-id="07ad0-222">您可以檢閱 hello 活動，並判斷 hello 動作是否已適當</span><span class="sxs-lookup"><span data-stu-id="07ad0-222">You can review hello activity and determine whether hello action was appropriate or not</span></span>

<span data-ttu-id="07ad0-223">Hello 的概觀與相關的使用者經驗，請參閱：</span><span class="sxs-lookup"><span data-stu-id="07ad0-223">For an overview of hello related user experience, see:</span></span>

* [<span data-ttu-id="07ad0-224">有風險的登入復原</span><span class="sxs-lookup"><span data-stu-id="07ad0-224">Risky sign-in recovery</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-recovery)
* [<span data-ttu-id="07ad0-225">已封鎖有風險的登入</span><span class="sxs-lookup"><span data-stu-id="07ad0-225">Risky sign-in blocked</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-blocked)  
* [<span data-ttu-id="07ad0-226">使用 Azure AD Identity Protection 時的登入體驗</span><span class="sxs-lookup"><span data-stu-id="07ad0-226">Sign-in experiences with Azure AD Identity Protection</span></span>](active-directory-identityprotection-flows.md)  

<span data-ttu-id="07ad0-227">**tooopen hello 相關的組態對話方塊**:</span><span class="sxs-lookup"><span data-stu-id="07ad0-227">**tooopen hello related configuration dialog**:</span></span>

- <span data-ttu-id="07ad0-228">在 hello **Azure AD Identity Protection**刀鋒視窗中的，在 hello**設定**區段中，按一下**風險原則登入**。</span><span class="sxs-lookup"><span data-stu-id="07ad0-228">On hello **Azure AD Identity Protection** blade, in hello **Configure** section, click **Sign-in risk policy**.</span></span>

    <span data-ttu-id="07ad0-229">![使用者風險原則](./media/active-directory-identityprotection/1014.png "使用者風險原則")</span><span class="sxs-lookup"><span data-stu-id="07ad0-229">![User ridk policy](./media/active-directory-identityprotection/1014.png "User ridk policy")</span></span>



## <a name="users-flagged-for-risk"></a><span data-ttu-id="07ad0-230">標示有風險的使用者</span><span class="sxs-lookup"><span data-stu-id="07ad0-230">Users flagged for risk</span></span>

<span data-ttu-id="07ad0-231">所有作用中[風險事件](active-directory-identity-protection-risk-events.md)，偵測到由 Azure Active Directory 的使用者參與 tooa 呼叫使用者風險的邏輯概念。</span><span class="sxs-lookup"><span data-stu-id="07ad0-231">All active [risk events](active-directory-identity-protection-risk-events.md) that were detected by Azure Active Directory for a user contribute tooa logical concept called user risk.</span></span> <span data-ttu-id="07ad0-232">標幟為有風險的使用者表示可能被盜用的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="07ad0-232">A user flagged for risk is an indicator for a user account that might have been compromised.</span></span>

![標示有風險的使用者](./media/active-directory-identityprotection/1200.png)


### <a name="user-risk-level"></a><span data-ttu-id="07ad0-234">使用者風險層級</span><span class="sxs-lookup"><span data-stu-id="07ad0-234">User risk level</span></span>

<span data-ttu-id="07ad0-235">使用者的風險層級是 （高、 中或低） 的指示 hello 可能性 hello 使用者的身分識別已遭洩漏。</span><span class="sxs-lookup"><span data-stu-id="07ad0-235">A user risk level is an indication (High, Medium, or Low) of hello likelihood that hello user’s identity has been compromised.</span></span> <span data-ttu-id="07ad0-236">它會根據計算 hello 與使用者的身分識別相關聯的使用者的風險事件。</span><span class="sxs-lookup"><span data-stu-id="07ad0-236">It is calculated based on hello user risk events that are associated with a user's identity.</span></span>

<span data-ttu-id="07ad0-237">hello 」 狀態的風險事件是**Active**或**Closed**。</span><span class="sxs-lookup"><span data-stu-id="07ad0-237">hello status of a risk event is either **Active** or **Closed**.</span></span> <span data-ttu-id="07ad0-238">只有風險事件**Active**參與 toohello 使用者風險層級計算。</span><span class="sxs-lookup"><span data-stu-id="07ad0-238">Only risk events that are **Active** contribute toohello user risk level calculation.</span></span>

<span data-ttu-id="07ad0-239">hello 使用者風險層級的計算使用 hello 下列輸入：</span><span class="sxs-lookup"><span data-stu-id="07ad0-239">hello user risk level is calculated using hello following inputs:</span></span>

* <span data-ttu-id="07ad0-240">作用中的風險事件影響 hello 使用者</span><span class="sxs-lookup"><span data-stu-id="07ad0-240">Active risk events impacting hello user</span></span>
* <span data-ttu-id="07ad0-241">這些事件的風險層級</span><span class="sxs-lookup"><span data-stu-id="07ad0-241">Risk level of these events</span></span>
* <span data-ttu-id="07ad0-242">是否已採取任何補救動作</span><span class="sxs-lookup"><span data-stu-id="07ad0-242">Whether any remediation actions have been taken</span></span>

<span data-ttu-id="07ad0-243">![使用者風險](./media/active-directory-identityprotection/1031.png "使用者風險")</span><span class="sxs-lookup"><span data-stu-id="07ad0-243">![User risks](./media/active-directory-identityprotection/1031.png "User risks")</span></span>

<span data-ttu-id="07ad0-244">您可以使用 hello 使用者風險層級 toocreate 條件式存取原則來封鎖危險的使用者無法登入，或強制其 toosecurely 變更其密碼。</span><span class="sxs-lookup"><span data-stu-id="07ad0-244">You can use hello user risk levels toocreate conditional access policies that block risky users from signing in, or force them toosecurely change their password.</span></span>

### <a name="closing-risk-events-manually"></a><span data-ttu-id="07ad0-245">手動關閉風險事件</span><span class="sxs-lookup"><span data-stu-id="07ad0-245">Closing risk events manually</span></span>

<span data-ttu-id="07ad0-246">在大部分情況下，所採取的修復動作，例如安全的密碼重設 tooautomatically 關閉的風險事件。</span><span class="sxs-lookup"><span data-stu-id="07ad0-246">In most cases, you will take remediation actions such as a secure password reset tooautomatically close risk events.</span></span> <span data-ttu-id="07ad0-247">但是，這不一定都可行。</span><span class="sxs-lookup"><span data-stu-id="07ad0-247">However, this might not always be possible.</span></span>  
<span data-ttu-id="07ad0-248">這是，比方說，hello 情況下，當：</span><span class="sxs-lookup"><span data-stu-id="07ad0-248">This is, for example, hello case, when:</span></span>

* <span data-ttu-id="07ad0-249">已刪除具有作用中風險事件的使用者</span><span class="sxs-lookup"><span data-stu-id="07ad0-249">A user with Active risk events has been deleted</span></span>
* <span data-ttu-id="07ad0-250">調查會顯示 hello 合法使用者已執行報告的風險事件</span><span class="sxs-lookup"><span data-stu-id="07ad0-250">An investigation reveals that a reported risk event has been perform by hello legitimate user</span></span>

<span data-ttu-id="07ad0-251">風險事件是因為**Active**參與 toohello 使用者風險計算，您可能必須手動關閉風險事件，以降低風險層級的 toomanually。</span><span class="sxs-lookup"><span data-stu-id="07ad0-251">Because risk events that are **Active** contribute toohello user risk calculation, you may have toomanually lower a risk level by closing risk events manually.</span></span>  
<span data-ttu-id="07ad0-252">期間的調查 hello 過程中，您可以選擇 tootake 任何這些動作 toochange hello 狀態的風險事件：</span><span class="sxs-lookup"><span data-stu-id="07ad0-252">During hello course of investigation, you can choose tootake any of these actions toochange hello status of a risk event:</span></span>

<span data-ttu-id="07ad0-253">![動作](./media/active-directory-identityprotection/34.png "動作")</span><span class="sxs-lookup"><span data-stu-id="07ad0-253">![Actions](./media/active-directory-identityprotection/34.png "Actions")</span></span>

* <span data-ttu-id="07ad0-254">**解決**-如果之後調查風險事件中，您採取適當的補救動作外部識別身分保護，而您認為應該關閉，標記為已解決的 hello 事件視為該 hello 風險事件。</span><span class="sxs-lookup"><span data-stu-id="07ad0-254">**Resolve** - If after investigating a risk event, you took an appropriate remediation action outside Identity Protection, and you believe that hello risk event should be considered closed, mark hello event as Resolved.</span></span> <span data-ttu-id="07ad0-255">已解決的事件會 hello 風險事件的狀態 tooClosed 然後 hello 風險事件將無法再參與 toouser 風險。</span><span class="sxs-lookup"><span data-stu-id="07ad0-255">Resolved events will set hello risk event’s status tooClosed and hello risk event will no longer contribute toouser risk.</span></span>
* <span data-ttu-id="07ad0-256">**標示為誤判** - 在某些情況下，您可能會調查某個風險事件並發現該事件被誤標為有風險。</span><span class="sxs-lookup"><span data-stu-id="07ad0-256">**Mark as false-positive** - In some cases, you may investigate a risk event and discover that it was incorrectly flagged as a risky.</span></span> <span data-ttu-id="07ad0-257">您可以協助減少 hello 次數這種方式是標示為誤判 hello 風險事件。</span><span class="sxs-lookup"><span data-stu-id="07ad0-257">You can help reduce hello number of such occurrences by marking hello risk event as False-positive.</span></span> <span data-ttu-id="07ad0-258">這將有助於 hello 機器學習演算法 tooimprove hello 分類的類似事件，在未來的 hello。</span><span class="sxs-lookup"><span data-stu-id="07ad0-258">This will help hello machine learning algorithms tooimprove hello classification of similar events in hello future.</span></span> <span data-ttu-id="07ad0-259">hello 誤判事件狀態太**Closed**它們將無法再參與 toouser 風險。</span><span class="sxs-lookup"><span data-stu-id="07ad0-259">hello status of false-positive events is too**Closed** and they will no longer contribute toouser risk.</span></span>
* <span data-ttu-id="07ad0-260">**忽略**-如果您未採取任何修復動作後，但想 hello 風險事件 toobe hello 作用中的清單中移除，您可以將標記風險事件忽略 hello 事件狀態將會關閉。</span><span class="sxs-lookup"><span data-stu-id="07ad0-260">**Ignore** - If you have not taken any remediation action, but want hello risk event toobe removed from hello active list, you can mark a risk event Ignore and hello event status will be Closed.</span></span> <span data-ttu-id="07ad0-261">已忽略的事件不會構成 toouser 風險。</span><span class="sxs-lookup"><span data-stu-id="07ad0-261">Ignored events do not contribute toouser risk.</span></span> <span data-ttu-id="07ad0-262">這個選項只能用於不尋常的情況下。</span><span class="sxs-lookup"><span data-stu-id="07ad0-262">This option should only be used under unusual circumstances.</span></span>
* <span data-ttu-id="07ad0-263">**重新啟用**-風險已手動關閉的事件 (藉由選擇**解決**，**誤判**，或**忽略**) 就可以重新啟動，設定 hello事件狀態太回**Active**。</span><span class="sxs-lookup"><span data-stu-id="07ad0-263">**Reactivate** - Risk events that were manually closed (by choosing **Resolve**, **False positive**, or **Ignore**) can be reactivated, setting hello event status back too**Active**.</span></span> <span data-ttu-id="07ad0-264">已重新啟動的風險事件參與 toohello 使用者風險層級計算。</span><span class="sxs-lookup"><span data-stu-id="07ad0-264">Reactivated risk events contribute toohello user risk level calculation.</span></span> <span data-ttu-id="07ad0-265">無法重新啟用透過補救 (例如重設安全的密碼) 關閉的風險事件。</span><span class="sxs-lookup"><span data-stu-id="07ad0-265">Risk events closed through remediation (such as a secure password reset) cannot be reactivated.</span></span>

<span data-ttu-id="07ad0-266">**tooopen hello 相關的組態對話方塊**:</span><span class="sxs-lookup"><span data-stu-id="07ad0-266">**tooopen hello related configuration dialog**:</span></span>

1. <span data-ttu-id="07ad0-267">在 hello **Azure AD Identity Protection**刀鋒視窗底下**調查**，按一下**風險事件**。</span><span class="sxs-lookup"><span data-stu-id="07ad0-267">On hello **Azure AD Identity Protection** blade, under **Investigate**, click **Risk events**.</span></span>

    <span data-ttu-id="07ad0-268">![手動密碼重設](./media/active-directory-identityprotection/1002.png "手動密碼重設")</span><span class="sxs-lookup"><span data-stu-id="07ad0-268">![Manual password reset](./media/active-directory-identityprotection/1002.png "Manual password reset")</span></span>
2. <span data-ttu-id="07ad0-269">在 hello**風險事件**清單中，按一下有風險。</span><span class="sxs-lookup"><span data-stu-id="07ad0-269">In hello **Risk events** list, click a risk.</span></span>

    <span data-ttu-id="07ad0-270">![手動密碼重設](./media/active-directory-identityprotection/1003.png "手動密碼重設")</span><span class="sxs-lookup"><span data-stu-id="07ad0-270">![Manual password reset](./media/active-directory-identityprotection/1003.png "Manual password reset")</span></span>
3. <span data-ttu-id="07ad0-271">在 hello 風險刀鋒視窗中，以滑鼠右鍵按一下使用者。</span><span class="sxs-lookup"><span data-stu-id="07ad0-271">On hello risk blade, right-click a user.</span></span>

    <span data-ttu-id="07ad0-272">![手動密碼重設](./media/active-directory-identityprotection/1004.png "手動密碼重設")</span><span class="sxs-lookup"><span data-stu-id="07ad0-272">![Manual password reset](./media/active-directory-identityprotection/1004.png "Manual password reset")</span></span>

### <a name="closing-all-risk-events-for-a-user-manually"></a><span data-ttu-id="07ad0-273">手動關閉使用者的所有風險事件</span><span class="sxs-lookup"><span data-stu-id="07ad0-273">Closing all risk events for a user manually</span></span>
<span data-ttu-id="07ad0-274">而不是以手動方式關閉個別使用者的風險事件，Azure Active Directory 識別身分保護也提供您方法 tooclose 所有事件的使用者。</span><span class="sxs-lookup"><span data-stu-id="07ad0-274">Instead of manually closing risk events for a user individually, Azure Active Directory Identity Protection also provides you with a method tooclose all events for a user with one click.</span></span>

<span data-ttu-id="07ad0-275">![動作](./media/active-directory-identityprotection/2222.png "動作")</span><span class="sxs-lookup"><span data-stu-id="07ad0-275">![Actions](./media/active-directory-identityprotection/2222.png "Actions")</span></span>

<span data-ttu-id="07ad0-276">當您按一下**解除所有事件**，所有事件都已都關閉且 hello 受影響的使用者不再有風險。</span><span class="sxs-lookup"><span data-stu-id="07ad0-276">When you click **Dismiss all events**, all events are closed and hello affected user is no longer at risk.</span></span>

### <a name="remediating-user-risk-events"></a><span data-ttu-id="07ad0-277">補救使用者風險事件</span><span class="sxs-lookup"><span data-stu-id="07ad0-277">Remediating user risk events</span></span>

<span data-ttu-id="07ad0-278">修復是識別碼或裝置先前可疑或已知 toobe 危害動作 toosecure。</span><span class="sxs-lookup"><span data-stu-id="07ad0-278">A remediation is an action toosecure an identity or a device that was previously suspected or known toobe compromised.</span></span> <span data-ttu-id="07ad0-279">補救動作還原 hello 身分識別或裝置 tooa 安全的狀態，並解決先前 hello 身分識別或裝置相關聯的風險事件。</span><span class="sxs-lookup"><span data-stu-id="07ad0-279">A remediation action restores hello identity or device tooa safe state, and resolves previous risk events associated with hello identity or device.</span></span>

<span data-ttu-id="07ad0-280">tooremediate 使用者風險事件，您可以：</span><span class="sxs-lookup"><span data-stu-id="07ad0-280">tooremediate user risk events, you can:</span></span>

* <span data-ttu-id="07ad0-281">手動執行安全的密碼重設 tooremediate 使用者風險事件</span><span class="sxs-lookup"><span data-stu-id="07ad0-281">Perform a secure password reset tooremediate user risk events manually</span></span>
* <span data-ttu-id="07ad0-282">設定使用者風險安全性原則 toomitigate 或自動補救使用者風險事件</span><span class="sxs-lookup"><span data-stu-id="07ad0-282">Configure a user risk security policy toomitigate or remediate user risk events automatically</span></span>
* <span data-ttu-id="07ad0-283">重新安裝映像 hello 感染的裝置</span><span class="sxs-lookup"><span data-stu-id="07ad0-283">Re-image hello infected device</span></span>  

#### <a name="manual-secure-password-reset"></a><span data-ttu-id="07ad0-284">手動重設安全密碼</span><span class="sxs-lookup"><span data-stu-id="07ad0-284">Manual secure password reset</span></span>
<span data-ttu-id="07ad0-285">安全密碼重設為有效的補救，對於許多的風險事件，並執行時，自動關閉這些風險事件，並重新計算 hello 使用者風險層級。</span><span class="sxs-lookup"><span data-stu-id="07ad0-285">A secure password reset is an effective remediation for many risk events, and when performed, automatically closes these risk events and recalculates hello user risk level.</span></span> <span data-ttu-id="07ad0-286">您可以使用 hello Identity Protection 儀表板 tooinitiate 危險的使用者重設密碼。</span><span class="sxs-lookup"><span data-stu-id="07ad0-286">You can use hello Identity Protection dashboard tooinitiate a password reset for a risky user.</span></span>

<span data-ttu-id="07ad0-287">hello 相關的對話方塊提供兩個不同的方法 tooreset 密碼：</span><span class="sxs-lookup"><span data-stu-id="07ad0-287">hello related dialog provides two different methods tooreset a password:</span></span>

<span data-ttu-id="07ad0-288">**重設密碼**-選取**需要 hello 使用者 tooreset 密碼**tooallow hello 使用者 tooself 復原，如果 hello 使用者已註冊的多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="07ad0-288">**Reset password** - Select **Require hello user tooreset their password** tooallow hello user tooself-recover if hello user has registered for multi-factor authentication.</span></span> <span data-ttu-id="07ad0-289">Hello 使用者下一步 在登入期間，hello 使用者將會需要進行 multi-factor authentication 成功挑戰的 toosolve 並且然後、 強制 toochange hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="07ad0-289">During hello user's next sign-in, hello user will be required toosolve a multi-factor authentication challenge successfully and then, forced toochange hello password.</span></span> <span data-ttu-id="07ad0-290">無法使用，如果 hello 使用者帳戶還不是已註冊的多重要素驗證此選項。</span><span class="sxs-lookup"><span data-stu-id="07ad0-290">This option isn't available if hello user account is not already registered multi-factor authentication.</span></span>

<span data-ttu-id="07ad0-291">**暫時密碼**-選取**產生暫時密碼**tooimmediately 失效 hello 現有密碼，並建立新的暫時密碼 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="07ad0-291">**Temporary password** - Select **Generate a temporary password** tooimmediately invalidate hello existing password, and create a new temporary password for hello user.</span></span> <span data-ttu-id="07ad0-292">傳送 hello 新暫時密碼 tooan 替代電子郵件地址 hello 使用者或 toohello 使用者的管理員。</span><span class="sxs-lookup"><span data-stu-id="07ad0-292">Send hello new temporary password tooan alternate email address for hello user or toohello user's manager.</span></span> <span data-ttu-id="07ad0-293">因為 hello 密碼是暫時性的 hello 使用者將會提示的 toochange hello 密碼登入。</span><span class="sxs-lookup"><span data-stu-id="07ad0-293">Because hello password is temporary, hello user will be prompted toochange hello password upon sign-in.</span></span>

<span data-ttu-id="07ad0-294">![原則](./media/active-directory-identityprotection/1005.png "原則")</span><span class="sxs-lookup"><span data-stu-id="07ad0-294">![Policy](./media/active-directory-identityprotection/1005.png "Policy")</span></span>

<span data-ttu-id="07ad0-295">**tooopen hello 相關的組態對話方塊**:</span><span class="sxs-lookup"><span data-stu-id="07ad0-295">**tooopen hello related configuration dialog**:</span></span>

1. <span data-ttu-id="07ad0-296">在 hello **Azure AD Identity Protection**刀鋒視窗中，按一下 **使用者加上旗標的風險**。</span><span class="sxs-lookup"><span data-stu-id="07ad0-296">On hello **Azure AD Identity Protection** blade, click **Users flagged for risk**.</span></span>

    <span data-ttu-id="07ad0-297">![手動密碼重設](./media/active-directory-identityprotection/1006.png "手動密碼重設")</span><span class="sxs-lookup"><span data-stu-id="07ad0-297">![Manual password reset](./media/active-directory-identityprotection/1006.png "Manual password reset")</span></span>
2. <span data-ttu-id="07ad0-298">從 [hello] 清單中的使用者，選取具有至少一個風險事件的使用者。</span><span class="sxs-lookup"><span data-stu-id="07ad0-298">From hello list of users, select a user with at least one risk events.</span></span>

    <span data-ttu-id="07ad0-299">![手動密碼重設](./media/active-directory-identityprotection/1007.png "手動密碼重設")</span><span class="sxs-lookup"><span data-stu-id="07ad0-299">![Manual password reset](./media/active-directory-identityprotection/1007.png "Manual password reset")</span></span>
3. <span data-ttu-id="07ad0-300">在 hello 使用者刀鋒視窗中，按一下 **重設密碼**。</span><span class="sxs-lookup"><span data-stu-id="07ad0-300">On hello user blade, click **Reset password**.</span></span>

    <span data-ttu-id="07ad0-301">![手動密碼重設](./media/active-directory-identityprotection/1008.png "手動密碼重設")</span><span class="sxs-lookup"><span data-stu-id="07ad0-301">![Manual password reset](./media/active-directory-identityprotection/1008.png "Manual password reset")</span></span>

### <a name="user-risk-security-policy"></a><span data-ttu-id="07ad0-302">使用者風險安全性原則</span><span class="sxs-lookup"><span data-stu-id="07ad0-302">User risk security policy</span></span>
<span data-ttu-id="07ad0-303">使用者的風險安全性原則是條件式存取原則，評估 hello 風險層級 tooa 特定使用者，並根據預先定義的條件和規則的補救和補救動作。</span><span class="sxs-lookup"><span data-stu-id="07ad0-303">A user risk security policy is a conditional access policy that evaluates hello risk level tooa specific user and applies remediation and mitigation actions based on predefined conditions and rules.</span></span>

<span data-ttu-id="07ad0-304">![使用者風險原則](./media/active-directory-identityprotection/1009.png "使用者風險原則")</span><span class="sxs-lookup"><span data-stu-id="07ad0-304">![User ridk policy](./media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

<span data-ttu-id="07ad0-305">Azure AD Identity Protection 可協助您管理 hello 降低與補救的使用者，讓您標示為進行風險：</span><span class="sxs-lookup"><span data-stu-id="07ad0-305">Azure AD Identity Protection helps you manage hello mitigation and remediation of users flagged for risk by enabling you to:</span></span>

* <span data-ttu-id="07ad0-306">設定使用者和群組 hello 原則會套用至 hello:</span><span class="sxs-lookup"><span data-stu-id="07ad0-306">Set hello users and groups hello policy applies to:</span></span>

    <span data-ttu-id="07ad0-307">![使用者風險原則](./media/active-directory-identityprotection/1010.png "使用者風險原則")</span><span class="sxs-lookup"><span data-stu-id="07ad0-307">![User ridk policy](./media/active-directory-identityprotection/1010.png "User ridk policy")</span></span>
* <span data-ttu-id="07ad0-308">設定 hello 使用者風險層級閾值 （低、 中或高），會觸發 hello 原則：</span><span class="sxs-lookup"><span data-stu-id="07ad0-308">Set hello user risk level threshold (low, medium, or high) that triggers hello policy:</span></span>

    <span data-ttu-id="07ad0-309">![使用者風險原則](./media/active-directory-identityprotection/1011.png "使用者風險原則")</span><span class="sxs-lookup"><span data-stu-id="07ad0-309">![User ridk policy](./media/active-directory-identityprotection/1011.png "User ridk policy")</span></span>
* <span data-ttu-id="07ad0-310">設定 hello 控制項 toobe hello 原則觸發程序時，強制執行：</span><span class="sxs-lookup"><span data-stu-id="07ad0-310">Set hello controls toobe enforced when hello policy triggers:</span></span>

    <span data-ttu-id="07ad0-311">![使用者風險原則](./media/active-directory-identityprotection/1012.png "使用者風險原則")</span><span class="sxs-lookup"><span data-stu-id="07ad0-311">![User ridk policy](./media/active-directory-identityprotection/1012.png "User ridk policy")</span></span>
* <span data-ttu-id="07ad0-312">切換原則的 hello 狀態：</span><span class="sxs-lookup"><span data-stu-id="07ad0-312">Switch hello state of your policy:</span></span>

    <span data-ttu-id="07ad0-313">![使用者風險原則](./media/active-directory-identityprotection/403.png "MFA 註冊")</span><span class="sxs-lookup"><span data-stu-id="07ad0-313">![User ridk policy](./media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="07ad0-314">檢閱和評估 hello 變更的影響層面之後再啟動它：</span><span class="sxs-lookup"><span data-stu-id="07ad0-314">Review and evaluate hello impact of a change before activating it:</span></span>

    <span data-ttu-id="07ad0-315">![使用者風險原則](./media/active-directory-identityprotection/1013.png "使用者風險原則")</span><span class="sxs-lookup"><span data-stu-id="07ad0-315">![User ridk policy](./media/active-directory-identityprotection/1013.png "User ridk policy")</span></span>

<span data-ttu-id="07ad0-316">選擇**高**臨界值會減少 hello 原則，就會觸發和次數 hello 影響 toousers 降到最低。</span><span class="sxs-lookup"><span data-stu-id="07ad0-316">Choosing a **High** threshold reduces hello number of times a policy is triggered and minimizes hello impact toousers.</span></span>
<span data-ttu-id="07ad0-317">不過，它會排除**低**和**媒體**標示為受到 hello 原則，可能不安全身分識別或裝置的使用者先前已可疑或已知 toobe 入侵。</span><span class="sxs-lookup"><span data-stu-id="07ad0-317">However, it excludes **Low** and **Medium** users flagged for risk from hello policy, which may not secure identities or devices that were previously suspected or known toobe compromised.</span></span>

<span data-ttu-id="07ad0-318">當設定 hello 原則</span><span class="sxs-lookup"><span data-stu-id="07ad0-318">When setting hello policy,</span></span>

* <span data-ttu-id="07ad0-319">排除的使用者可能 toogenerate 大量 false 誤判 （開發人員、 安全性分析師）</span><span class="sxs-lookup"><span data-stu-id="07ad0-319">Exclude users who are likely toogenerate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="07ad0-320">排除使用者在其中啟用 hello 原則不是實際的地區設定 (例如沒有存取 toohelpdesk)</span><span class="sxs-lookup"><span data-stu-id="07ad0-320">Exclude users in locales where enabling hello policy is not practical (for example no access toohelpdesk)</span></span>
* <span data-ttu-id="07ad0-321">在原則推出初期，或如果您必須盡量減少使用者所看到的挑戰，請使用 [高]  臨界值。</span><span class="sxs-lookup"><span data-stu-id="07ad0-321">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="07ad0-322">如果您的組織需要更高的安全性，請使用 [低]  臨界值。</span><span class="sxs-lookup"><span data-stu-id="07ad0-322">Use a **Low** threshold if your organization requires greater security.</span></span> <span data-ttu-id="07ad0-323">選取 [低]  臨界值會帶來額外的使用者登入挑戰，並提高安全性。</span><span class="sxs-lookup"><span data-stu-id="07ad0-323">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="07ad0-324">大部分的組織是 tooconfigure 的規則，建議使用預設的 hello**媒體**閾值 toostrike 可用性和安全性之間取得平衡。</span><span class="sxs-lookup"><span data-stu-id="07ad0-324">hello recommended default for most organizations is tooconfigure a rule for a **Medium** threshold toostrike a balance between usability and security.</span></span>

<span data-ttu-id="07ad0-325">Hello 的概觀與相關的使用者經驗，請參閱：</span><span class="sxs-lookup"><span data-stu-id="07ad0-325">For an overview of hello related user experience, see:</span></span>

* <span data-ttu-id="07ad0-326">[遭到入侵的帳戶復原流程](active-directory-identityprotection-flows.md#compromised-account-recovery)。</span><span class="sxs-lookup"><span data-stu-id="07ad0-326">[Compromised account recovery flow](active-directory-identityprotection-flows.md#compromised-account-recovery).</span></span>  
* <span data-ttu-id="07ad0-327">[遭到入侵的帳戶封鎖流程](active-directory-identityprotection-flows.md#compromised-account-blocked)。</span><span class="sxs-lookup"><span data-stu-id="07ad0-327">[Compromised account blocked flow](active-directory-identityprotection-flows.md#compromised-account-blocked).</span></span>  

<span data-ttu-id="07ad0-328">**tooopen hello 相關的組態對話方塊**:</span><span class="sxs-lookup"><span data-stu-id="07ad0-328">**tooopen hello related configuration dialog**:</span></span>

- <span data-ttu-id="07ad0-329">在 hello **Azure AD Identity Protection**刀鋒視窗中的，在 hello**設定**區段中，按一下**使用者風險原則**。</span><span class="sxs-lookup"><span data-stu-id="07ad0-329">On hello **Azure AD Identity Protection** blade, in hello **Configure** section, click **User risk policy**.</span></span>

    <span data-ttu-id="07ad0-330">![使用者風險原則](./media/active-directory-identityprotection/1009.png "使用者風險原則")</span><span class="sxs-lookup"><span data-stu-id="07ad0-330">![User ridk policy](./media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

### <a name="mitigating-user-risk-events"></a><span data-ttu-id="07ad0-331">緩和使用者風險事件</span><span class="sxs-lookup"><span data-stu-id="07ad0-331">Mitigating user risk events</span></span>
<span data-ttu-id="07ad0-332">系統管理員可以根據 hello 風險層級設定使用者風險安全性原則 tooblock 使用者在登入。</span><span class="sxs-lookup"><span data-stu-id="07ad0-332">Administrators can set a user risk security policy tooblock users upon sign-in depending on hello risk level.</span></span>

<span data-ttu-id="07ad0-333">封鎖登入：</span><span class="sxs-lookup"><span data-stu-id="07ad0-333">Blocking a sign-in:</span></span>

* <span data-ttu-id="07ad0-334">防止 hello 產生 hello 受影響使用者的新使用者的風險事件</span><span class="sxs-lookup"><span data-stu-id="07ad0-334">Prevents hello generation of new user risk events for hello affected user</span></span>
* <span data-ttu-id="07ad0-335">可讓系統管理員 toomanually 補救 hello 風險事件影響 hello 使用者的身分識別，並將它還原 tooa 安全的狀態</span><span class="sxs-lookup"><span data-stu-id="07ad0-335">Enables administrators toomanually remediate hello risk events affecting hello user's identity and restore it tooa secure state</span></span>



## <a name="multi-factor-authentication-registration-policy"></a><span data-ttu-id="07ad0-336">Multi-Factor Authentication 註冊原則</span><span class="sxs-lookup"><span data-stu-id="07ad0-336">Multi-factor authentication registration policy</span></span>
<span data-ttu-id="07ad0-337">Azure 多因素驗證是確認您的身分的方法需要 hello 使用不只是使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="07ad0-337">Azure multi-factor authentication is a method of verifying who you are that requires hello use of more than just a username and password.</span></span> <span data-ttu-id="07ad0-338">它提供安全性 toouser 登入和交易的第二層。</span><span class="sxs-lookup"><span data-stu-id="07ad0-338">It provides a second layer of security toouser sign-ins and transactions.</span></span>  
<span data-ttu-id="07ad0-339">建議您要求對使用者登入進行 Azure Multi-Factor Authentication，因為它：</span><span class="sxs-lookup"><span data-stu-id="07ad0-339">We recommend that you require Azure multi-factor authentication for user sign-ins because it:</span></span>

* <span data-ttu-id="07ad0-340">提供增強式驗證與一系列簡單的驗證選項</span><span class="sxs-lookup"><span data-stu-id="07ad0-340">Delivers strong authentication with a range of easy verification options</span></span>
* <span data-ttu-id="07ad0-341">扮演一個關鍵角色準備您的組織 tooprotect 並從帳戶項目都會破壞復原</span><span class="sxs-lookup"><span data-stu-id="07ad0-341">Plays a key role in preparing your organization tooprotect and recover from account compromises</span></span>

<span data-ttu-id="07ad0-342">![使用者風險原則](./media/active-directory-identityprotection/1019.png "使用者風險原則")</span><span class="sxs-lookup"><span data-stu-id="07ad0-342">![User ridk policy](./media/active-directory-identityprotection/1019.png "User ridk policy")</span></span>

<span data-ttu-id="07ad0-343">如需詳細資訊，請參閱 [什麼是 Azure Multi-Factor Authentication？](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="07ad0-343">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

<span data-ttu-id="07ad0-344">Azure AD Identity Protection 可協助您管理 hello 推出多因素驗證註冊的設定原則，可讓您：</span><span class="sxs-lookup"><span data-stu-id="07ad0-344">Azure AD Identity Protection helps you manage hello roll-out of multi-factor authentication registration by configuring a policy that enables you to:</span></span>

* <span data-ttu-id="07ad0-345">設定使用者和群組 hello 原則會套用至 hello:</span><span class="sxs-lookup"><span data-stu-id="07ad0-345">Set hello users and groups hello policy applies to:</span></span>

    <span data-ttu-id="07ad0-346">![MFA 原則](./media/active-directory-identityprotection/1020.png "MFA 原則")</span><span class="sxs-lookup"><span data-stu-id="07ad0-346">![MFA policy](./media/active-directory-identityprotection/1020.png "MFA policy")</span></span>
* <span data-ttu-id="07ad0-347">Hello 原則觸發程序時，強制執行設定 hello 控制項 toobe::</span><span class="sxs-lookup"><span data-stu-id="07ad0-347">Set hello controls toobe enforced when hello policy triggers::</span></span>  

    <span data-ttu-id="07ad0-348">![MFA 原則](./media/active-directory-identityprotection/1021.png "MFA 原則")</span><span class="sxs-lookup"><span data-stu-id="07ad0-348">![MFA policy](./media/active-directory-identityprotection/1021.png "MFA policy")</span></span>
* <span data-ttu-id="07ad0-349">切換原則的 hello 狀態：</span><span class="sxs-lookup"><span data-stu-id="07ad0-349">Switch hello state of your policy:</span></span>

    <span data-ttu-id="07ad0-350">![MFA 原則](./media/active-directory-identityprotection/403.png "MFA 原則")</span><span class="sxs-lookup"><span data-stu-id="07ad0-350">![MFA policy](./media/active-directory-identityprotection/403.png "MFA policy")</span></span>
* <span data-ttu-id="07ad0-351">檢視目前登錄狀態 hello:</span><span class="sxs-lookup"><span data-stu-id="07ad0-351">View hello current registration status:</span></span>

    <span data-ttu-id="07ad0-352">![MFA 原則](./media/active-directory-identityprotection/1022.png "MFA 原則")</span><span class="sxs-lookup"><span data-stu-id="07ad0-352">![MFA policy](./media/active-directory-identityprotection/1022.png "MFA policy")</span></span>

<span data-ttu-id="07ad0-353">Hello 的概觀與相關的使用者經驗，請參閱：</span><span class="sxs-lookup"><span data-stu-id="07ad0-353">For an overview of hello related user experience, see:</span></span>

* <span data-ttu-id="07ad0-354">[Multi-Factor Authentication 註冊流程](active-directory-identityprotection-flows.md#multi-factor-authentication-registration)。</span><span class="sxs-lookup"><span data-stu-id="07ad0-354">[Multi-factor authentication registration flow](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).</span></span>  
* <span data-ttu-id="07ad0-355">[使用 Azure AD Identity Protection 時的登入體驗](active-directory-identityprotection-flows.md)。</span><span class="sxs-lookup"><span data-stu-id="07ad0-355">[Sign-in experiences with Azure AD Identity Protection](active-directory-identityprotection-flows.md).</span></span>  

<span data-ttu-id="07ad0-356">**tooopen hello 相關的組態對話方塊**:</span><span class="sxs-lookup"><span data-stu-id="07ad0-356">**tooopen hello related configuration dialog**:</span></span>

- <span data-ttu-id="07ad0-357">在 hello **Azure AD Identity Protection**刀鋒視窗中的，在 hello**設定**區段中，按一下**multi-factor authentication 註冊**。</span><span class="sxs-lookup"><span data-stu-id="07ad0-357">On hello **Azure AD Identity Protection** blade, in hello **Configure** section, click **Multi-factor authentication registration**.</span></span>

    <span data-ttu-id="07ad0-358">![MFA 原則](./media/active-directory-identityprotection/1019.png "MFA 原則")</span><span class="sxs-lookup"><span data-stu-id="07ad0-358">![MFA policy](./media/active-directory-identityprotection/1019.png "MFA policy")</span></span>

## <a name="next-steps"></a><span data-ttu-id="07ad0-359">後續步驟</span><span class="sxs-lookup"><span data-stu-id="07ad0-359">Next steps</span></span>
* [<span data-ttu-id="07ad0-360">第 9 頻道：Azure AD 和身分識別展示：Identity Protection 預覽</span><span class="sxs-lookup"><span data-stu-id="07ad0-360">Channel 9: Azure AD and Identity Show: Identity Protection Preview</span></span>](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

* [<span data-ttu-id="07ad0-361">啟用 Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="07ad0-361">Enabling Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-enable.md)

* [<span data-ttu-id="07ad0-362">Azure Active Directory Identity Protection 偵測到的弱點</span><span class="sxs-lookup"><span data-stu-id="07ad0-362">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-vulnerabilities.md)

* [<span data-ttu-id="07ad0-363">Azure Active Directory 風險事件</span><span class="sxs-lookup"><span data-stu-id="07ad0-363">Azure Active Directory risk events</span></span>](active-directory-identity-protection-risk-events.md)

* [<span data-ttu-id="07ad0-364">Azure Active Directory Identity Protection 通知</span><span class="sxs-lookup"><span data-stu-id="07ad0-364">Azure Active Directory Identity Protection notifications</span></span>](active-directory-identityprotection-notifications.md)

* [<span data-ttu-id="07ad0-365">Azure Active Directory Identity Protection 腳本</span><span class="sxs-lookup"><span data-stu-id="07ad0-365">Azure Active Directory Identity Protection playbook</span></span>](active-directory-identityprotection-playbook.md)

* [<span data-ttu-id="07ad0-366">Azure Active Directory Identity Protection 詞彙</span><span class="sxs-lookup"><span data-stu-id="07ad0-366">Azure Active Directory Identity Protection glossary</span></span>](active-directory-identityprotection-glossary.md)

* [<span data-ttu-id="07ad0-367">使用 Azure AD Identity Protection 時的登入體驗</span><span class="sxs-lookup"><span data-stu-id="07ad0-367">Sign-in experiences with Azure AD Identity Protection</span></span>](active-directory-identityprotection-flows.md)

* [<span data-ttu-id="07ad0-368">Azure Active Directory 識別身分保護-如何 toounblock 使用者</span><span class="sxs-lookup"><span data-stu-id="07ad0-368">Azure Active Directory Identity Protection - How toounblock users</span></span>](active-directory-identityprotection-unblock-howto.md)

* [<span data-ttu-id="07ad0-369">開始使用 Azure Active Directory Identity Protection 和 Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="07ad0-369">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>](active-directory-identityprotection-graph-getting-started.md)
