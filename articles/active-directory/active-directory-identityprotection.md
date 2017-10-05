---
title: Azure Active Directory Identity Protection | Microsoft Docs
description: "了解 Azure AD Identity Protection 如何讓您限制攻擊者利用遭入侵的身分識別或裝置的能力，以及保護先前疑似或已知遭到入侵的身分識別或裝置。"
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
ms.openlocfilehash: 0c7a8d68c0df729441e3f7faa5cd06066db1261d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-identity-protection"></a><span data-ttu-id="23ba9-104">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="23ba9-104">Azure Active Directory Identity Protection</span></span>

<span data-ttu-id="23ba9-105">Azure Active Directory Identity Protection 是 Azure AD Premium P2 版本的一向功能，可讓您：</span><span class="sxs-lookup"><span data-stu-id="23ba9-105">Azure Active Directory Identity Protection is a feature of the Azure AD Premium P2 edition that enables you to:</span></span>

- <span data-ttu-id="23ba9-106">偵測會影響組織的身分識別的潛在弱點</span><span class="sxs-lookup"><span data-stu-id="23ba9-106">Detect potential vulnerabilities affecting your organization’s identities</span></span>

- <span data-ttu-id="23ba9-107">針對偵測到的與您組織的身分識別有關的可疑動作，設定自動回應</span><span class="sxs-lookup"><span data-stu-id="23ba9-107">Configure automated responses to detected suspicious actions that are related to your organization’s identities</span></span>  

- <span data-ttu-id="23ba9-108">調查可疑事件並採取適當動作以解決它們</span><span class="sxs-lookup"><span data-stu-id="23ba9-108">Investigate suspicious incidents and take appropriate action to resolve them</span></span>   


## <a name="getting-started"></a><span data-ttu-id="23ba9-109">開始使用</span><span class="sxs-lookup"><span data-stu-id="23ba9-109">Getting started</span></span>

<span data-ttu-id="23ba9-110">Microsoft 保護雲端身分識別已經超過十多年。</span><span class="sxs-lookup"><span data-stu-id="23ba9-110">Microsoft secures cloud-based identities for more than a decade.</span></span> <span data-ttu-id="23ba9-111">在您的環境中使用 Azure Active Directory Identity Protection，即可使用與 Microsoft 用來保護身份識別一樣的保護系統。</span><span class="sxs-lookup"><span data-stu-id="23ba9-111">With Azure Active Directory Identity Protection, in your environment, you can use the same protection systems Microsoft uses to secure identities.</span></span>

<span data-ttu-id="23ba9-112">大部分的安全性缺口出現於當攻擊者藉由竊取使用者的身分識別來取得環境的存取權時。</span><span class="sxs-lookup"><span data-stu-id="23ba9-112">The vast majority of security breaches take place when attackers gain access to an environment by stealing a user’s identity.</span></span> <span data-ttu-id="23ba9-113">這些年來，攻擊者變得越來越擅於利用協力廠商缺考，以及使用複雜的網路釣魚攻擊。</span><span class="sxs-lookup"><span data-stu-id="23ba9-113">Over the years, attackers have become increasingly effective in leveraging third party breaches and using sophisticated phishing attacks.</span></span> <span data-ttu-id="23ba9-114">只要攻擊者取得更低權限的使用者帳戶的存取權，他們即可相對容易地透過橫向移動存取重要的公司資源。</span><span class="sxs-lookup"><span data-stu-id="23ba9-114">As soon as an attacker gains access to even low privileged user accounts, it is relatively easy for them to gain access to important company resources through lateral movement.</span></span>

<span data-ttu-id="23ba9-115">如此一來，您必須：</span><span class="sxs-lookup"><span data-stu-id="23ba9-115">As a consequence of this, you need to:</span></span>

- <span data-ttu-id="23ba9-116">保護所有的識別身分，不論其權限層級</span><span class="sxs-lookup"><span data-stu-id="23ba9-116">Protect all identities regardless of their privilege level</span></span>

- <span data-ttu-id="23ba9-117">主動防止遭入侵的身分識別被濫用</span><span class="sxs-lookup"><span data-stu-id="23ba9-117">Proactively prevent compromised identities from being abused</span></span>

<span data-ttu-id="23ba9-118">探索遭入侵的身分識別並不容易。</span><span class="sxs-lookup"><span data-stu-id="23ba9-118">Discovering compromised identities is no easy task.</span></span> <span data-ttu-id="23ba9-119">Azure Active Directory 使用調適性機器學習運算法和啟發學習法來偵測表示可能遭入侵身份識別的異常與可疑事件。</span><span class="sxs-lookup"><span data-stu-id="23ba9-119">Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect anomalies and suspicious incidents that indicate potentially compromised identities.</span></span> <span data-ttu-id="23ba9-120">Identity Protection 會使用此資料來產生報告和警示，讓您評估偵測到的問題並採取適當的緩和或補救動作。</span><span class="sxs-lookup"><span data-stu-id="23ba9-120">Using this data, Identity Protection generates reports and alerts that enable you to evaluate the detected issues and take appropriate mitigation or remediation actions.</span></span>

<span data-ttu-id="23ba9-121">Azure Active Directory Identity Protection 不只是監視和報告工具而已。</span><span class="sxs-lookup"><span data-stu-id="23ba9-121">Azure Active Directory Identity Protection is more than a monitoring and reporting tool.</span></span> <span data-ttu-id="23ba9-122">若要保護您組織的身分識別，您可以設定以風險為基礎的原則，當達到指定風險層級時自動回應偵測到的問題。</span><span class="sxs-lookup"><span data-stu-id="23ba9-122">To protect your organization's identities, you can configure risk-based policies that automatically respond to detected issues when a specified risk level has been reached.</span></span> <span data-ttu-id="23ba9-123">除了 Azure Active Directory 與 EMS 所提供的其他條件式存取控制以外，這些的原則可以自動封鎖或起始調適性補救動作，包括重設密碼以及強制 Multi-Factor Authentication。</span><span class="sxs-lookup"><span data-stu-id="23ba9-123">These policies, in addition to other conditional access controls provided by Azure Active Directory and EMS, can either automatically block or initiate adaptive remediation actions including password resets and multi-factor authentication enforcement.</span></span>


#### <a name="identity-protection-capabilities"></a><span data-ttu-id="23ba9-124">Identity Protection 功能</span><span class="sxs-lookup"><span data-stu-id="23ba9-124">Identity Protection capabilities</span></span>

<span data-ttu-id="23ba9-125">**偵測弱點和風險帳戶：**</span><span class="sxs-lookup"><span data-stu-id="23ba9-125">**Detecting vulnerabilities and risky accounts:**</span></span>  

* <span data-ttu-id="23ba9-126">提供自訂建議，藉由反白顯示弱點來改善整體安全性狀態</span><span class="sxs-lookup"><span data-stu-id="23ba9-126">Providing custom recommendations to improve overall security posture by highlighting vulnerabilities</span></span>
* <span data-ttu-id="23ba9-127">計算登入風險層級</span><span class="sxs-lookup"><span data-stu-id="23ba9-127">Calculating sign-in risk levels</span></span>
* <span data-ttu-id="23ba9-128">計算使用者風險層級</span><span class="sxs-lookup"><span data-stu-id="23ba9-128">Calculating user risk levels</span></span>


<span data-ttu-id="23ba9-129">**調查風險事件：**</span><span class="sxs-lookup"><span data-stu-id="23ba9-129">**Investigating risk events:**</span></span>

* <span data-ttu-id="23ba9-130">傳送風險事件的通知</span><span class="sxs-lookup"><span data-stu-id="23ba9-130">Sending notifications for risk events</span></span>
* <span data-ttu-id="23ba9-131">使用相關和內容資訊來調查風險事件</span><span class="sxs-lookup"><span data-stu-id="23ba9-131">Investigating risk events using relevant and contextual information</span></span>
* <span data-ttu-id="23ba9-132">提供基本工作流程來追蹤調查</span><span class="sxs-lookup"><span data-stu-id="23ba9-132">Providing basic workflows to track investigations</span></span>
* <span data-ttu-id="23ba9-133">讓您輕鬆存取補救動作，例如重設密碼</span><span class="sxs-lookup"><span data-stu-id="23ba9-133">Providing easy access to remediation actions such as password reset</span></span>

<span data-ttu-id="23ba9-134">**以風險為基礎的條件式存取原則：**</span><span class="sxs-lookup"><span data-stu-id="23ba9-134">**Risk-based conditional access policies:**</span></span>

* <span data-ttu-id="23ba9-135">此原則會藉由封鎖登入或要求 Multi-Factor Authentication 挑戰來緩和有風險的登入。</span><span class="sxs-lookup"><span data-stu-id="23ba9-135">Policy to mitigate risky sign-ins by blocking sign-ins or requiring multi-factor authentication challenges.</span></span>
* <span data-ttu-id="23ba9-136">此原則會封鎖或保護有風險的使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="23ba9-136">Policy to block or secure risky user accounts</span></span>
* <span data-ttu-id="23ba9-137">此原則會要求使用者註冊以便進行 Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="23ba9-137">Policy to require users to register for multi-factor authentication</span></span>



## <a name="identity-protection-roles"></a><span data-ttu-id="23ba9-138">Identity Protection 角色</span><span class="sxs-lookup"><span data-stu-id="23ba9-138">Identity Protection roles</span></span>

<span data-ttu-id="23ba9-139">若要讓 Identity Protection 實作方面的管理活動達到負載平衡，您可以指派數個角色。</span><span class="sxs-lookup"><span data-stu-id="23ba9-139">To load balance the management activities around your Identity Protection implementation, you can assign several roles.</span></span> <span data-ttu-id="23ba9-140">Azure AD Identity Protection 支援 3 種目錄角色：</span><span class="sxs-lookup"><span data-stu-id="23ba9-140">Azure AD Identity Protection supports 3 directory roles:</span></span>

| <span data-ttu-id="23ba9-141">角色</span><span class="sxs-lookup"><span data-stu-id="23ba9-141">Role</span></span>                         | <span data-ttu-id="23ba9-142">可以執行</span><span class="sxs-lookup"><span data-stu-id="23ba9-142">Can do</span></span>                          | <span data-ttu-id="23ba9-143">無法執行</span><span class="sxs-lookup"><span data-stu-id="23ba9-143">Cannot do</span></span>
| :--                          | ---                                |  ---   |
| <span data-ttu-id="23ba9-144">全域管理員</span><span class="sxs-lookup"><span data-stu-id="23ba9-144">Global administrator</span></span>         | <span data-ttu-id="23ba9-145">完整存取 Identity Protection、將 Identity Protection 上架</span><span class="sxs-lookup"><span data-stu-id="23ba9-145">Full access to Identity Protection, Onboard Identity Protection</span></span>| |
| <span data-ttu-id="23ba9-146">安全性系統管理員</span><span class="sxs-lookup"><span data-stu-id="23ba9-146">Security administrator</span></span>       | <span data-ttu-id="23ba9-147">完整存取 Identity Protection</span><span class="sxs-lookup"><span data-stu-id="23ba9-147">Full access to Identity Protection</span></span> | <span data-ttu-id="23ba9-148">將 Identity Protection 上架、重設使用者密碼</span><span class="sxs-lookup"><span data-stu-id="23ba9-148">Onboard Identity Protection,  reset passwords for a user</span></span> |
| <span data-ttu-id="23ba9-149">安全性讀取者</span><span class="sxs-lookup"><span data-stu-id="23ba9-149">Security reader</span></span>              | <span data-ttu-id="23ba9-150">唯讀存取 Identity Protection</span><span class="sxs-lookup"><span data-stu-id="23ba9-150">Ready-only access to Identity Protection</span></span> | <span data-ttu-id="23ba9-151">讓 Identity Protection 上線、修復使用者、設定原則、重設密碼</span><span class="sxs-lookup"><span data-stu-id="23ba9-151">Onboard Identity Protection, remidiate users, configure policies,  reset passwords</span></span> |




<span data-ttu-id="23ba9-152">如需詳細資訊，請參閱[在 Azure Active Directory 中指派系統管理員角色](active-directory-assign-admin-roles-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="23ba9-152">For more details, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)</span></span>



## <a name="detection"></a><span data-ttu-id="23ba9-153">偵測</span><span class="sxs-lookup"><span data-stu-id="23ba9-153">Detection</span></span>

### <a name="vulnerabilities"></a><span data-ttu-id="23ba9-154">弱點</span><span class="sxs-lookup"><span data-stu-id="23ba9-154">Vulnerabilities</span></span>

<span data-ttu-id="23ba9-155">Azure Active Directory Identity Protection 會分析您的組態，並偵測可能影響您使用者身份識別的弱點。</span><span class="sxs-lookup"><span data-stu-id="23ba9-155">Azure Active Directory Identity Protection analyses your configuration and detects vulnerabilities that can have an impact on your user's identities.</span></span> <span data-ttu-id="23ba9-156">如需詳細資訊，請參閱 [Azure Active Directory Identity Protection 偵測到的弱點](active-directory-identityprotection-vulnerabilities.md)。</span><span class="sxs-lookup"><span data-stu-id="23ba9-156">For more details, see [Vulnerabilities detected by Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md).</span></span>

### <a name="risk-events"></a><span data-ttu-id="23ba9-157">風險事件</span><span class="sxs-lookup"><span data-stu-id="23ba9-157">Risk events</span></span>

<span data-ttu-id="23ba9-158">Azure Active Directory 使用調適性機器學習運算法和啟發學習法來偵測與您使用者身份識別有關的可疑動作。</span><span class="sxs-lookup"><span data-stu-id="23ba9-158">Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect suspicious actions that are related to your user's identities.</span></span> <span data-ttu-id="23ba9-159">系統會針對每個偵測到的可疑動作建立記錄。</span><span class="sxs-lookup"><span data-stu-id="23ba9-159">The system creates a record for each detected suspicious action.</span></span> <span data-ttu-id="23ba9-160">這些記錄又名風險事件。</span><span class="sxs-lookup"><span data-stu-id="23ba9-160">These records are also known as risk events.</span></span>  
<span data-ttu-id="23ba9-161">如需詳細資訊，請參閱 [Azure Active Directory風險事件](active-directory-identity-protection-risk-events.md)。</span><span class="sxs-lookup"><span data-stu-id="23ba9-161">For more details, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span>


## <a name="investigation"></a><span data-ttu-id="23ba9-162">調查</span><span class="sxs-lookup"><span data-stu-id="23ba9-162">Investigation</span></span>
<span data-ttu-id="23ba9-163">您通常會從 Identity Protection 儀表板開始使用 Identity Protection。</span><span class="sxs-lookup"><span data-stu-id="23ba9-163">Your journey through Identity Protection typically starts with the Identity Protection dashboard.</span></span>

<span data-ttu-id="23ba9-164">![補救](./media/active-directory-identityprotection/1000.png "補救")</span><span class="sxs-lookup"><span data-stu-id="23ba9-164">![Remediation](./media/active-directory-identityprotection/1000.png "Remediation")</span></span>

<span data-ttu-id="23ba9-165">儀表板可讓您存取：</span><span class="sxs-lookup"><span data-stu-id="23ba9-165">The dashboard gives you access to:</span></span>

* <span data-ttu-id="23ba9-166">報告，例如 [標示有風險的使用者]、[風險事件] 和 [弱點]</span><span class="sxs-lookup"><span data-stu-id="23ba9-166">Reports such as **Users flagged for risk**, **Risk events** and **Vulnerabilities**</span></span>
* <span data-ttu-id="23ba9-167">設定，例如 [安全性原則]、[通知] 和 [Multi-Factor Authentication 註冊] 的組態</span><span class="sxs-lookup"><span data-stu-id="23ba9-167">Settings such as the configuration of your **Security Policies**, **Notifications** and **multi-factor authentication registration**</span></span>

<span data-ttu-id="23ba9-168">這通常是調查的起點，而在調查過程中會檢閱風險事件相關活動、記錄檔和其他相關資訊，以決定是否需要採取補救或緩和步驟，了解身分識別如何遭到入侵，以及了解遭到入侵的身分識別如何被利用。</span><span class="sxs-lookup"><span data-stu-id="23ba9-168">It is typically your starting point for investigation, which is the process of reviewing the activities, logs, and other relevant information related to a risk event to decide whether remediation or mitigation steps are necessary,  and how the identity was compromised, and understand how the compromised identity was used.</span></span>

<span data-ttu-id="23ba9-169">您可以將調查活動繫結至 Azure Active Directory Protection 傳送的每封電子郵件 [通知](active-directory-identityprotection-notifications.md) 。</span><span class="sxs-lookup"><span data-stu-id="23ba9-169">You can tie your investigation activities to the [notifications](active-directory-identityprotection-notifications.md) Azure Active Directory Protection sends per email.</span></span>

<span data-ttu-id="23ba9-170">下列各節提供更多詳細資料以及調查的相關步驟。</span><span class="sxs-lookup"><span data-stu-id="23ba9-170">The following sections provide you with more details and the steps that are related to an investigation.</span></span>  


## <a name="risky-sign-ins"></a><span data-ttu-id="23ba9-171">有風險的登入</span><span class="sxs-lookup"><span data-stu-id="23ba9-171">Risky sign-ins</span></span>

<span data-ttu-id="23ba9-172">Azure Active Directory 會以即時和離線方式偵測[風險事件類型](active-directory-reporting-risk-events.md#risk-event-types)。</span><span class="sxs-lookup"><span data-stu-id="23ba9-172">Azure Active Directory detects [risk event types](active-directory-reporting-risk-events.md#risk-event-types) in real-time and offline.</span></span> <span data-ttu-id="23ba9-173">使用者登入時偵測到的每個風險事件，構成了名為有風險的登入的邏輯概念。</span><span class="sxs-lookup"><span data-stu-id="23ba9-173">Each risk event that has been detected for a sign-in of a user contributes to a logical concept called risky sign-in.</span></span> <span data-ttu-id="23ba9-174">有風險的登入表示可能不是由使用者帳戶合法擁有者執行的嘗試登入。</span><span class="sxs-lookup"><span data-stu-id="23ba9-174">A risky sign-in is an indicator for a sign-in attempt that might not have been performed by the legitimate owner of a user account.</span></span>


### <a name="sign-in-risk-level"></a><span data-ttu-id="23ba9-175">登入風險層級</span><span class="sxs-lookup"><span data-stu-id="23ba9-175">Sign-in risk level</span></span>

<span data-ttu-id="23ba9-176">登入風險層級指的是，不是由使用者帳戶合法擁有者執行的登入的可能性指示 (高、中或低)。</span><span class="sxs-lookup"><span data-stu-id="23ba9-176">A sign-in risk level is an indication (High, Medium, or Low) of the likelihood that a sign-in attempt was not performed by the legitimate owner of a user account.</span></span>

### <a name="mitigating-sign-in-risk-events"></a><span data-ttu-id="23ba9-177">緩和登入風險事件</span><span class="sxs-lookup"><span data-stu-id="23ba9-177">Mitigating sign-in risk events</span></span>

<span data-ttu-id="23ba9-178">緩和動作可限制攻擊者利用遭到入侵的身分識別或裝置的能力，但不需將身分識別或裝置還原至安全的狀態。</span><span class="sxs-lookup"><span data-stu-id="23ba9-178">A mitigation is an action to limit the ability of an attacker to exploit a compromised identity or device without restoring the identity or device to a safe state.</span></span> <span data-ttu-id="23ba9-179">緩和並未解決先前與身分識別或裝置相關聯的登入風險事件。</span><span class="sxs-lookup"><span data-stu-id="23ba9-179">A mitigation does not resolve previous sign-in risk events associated with the identity or device.</span></span>

<span data-ttu-id="23ba9-180">若要自動降低有風險的登入，您可以設定登入風險安全性原則。</span><span class="sxs-lookup"><span data-stu-id="23ba9-180">To mitigate risky sign-ins automatically, you can configure sign-in risk security policicies.</span></span> <span data-ttu-id="23ba9-181">使用這些原則時，請考慮使用者或登入的風險層級，以封鎖有風險的登入或要求使用者執行 Multi-Factor Authentication。</span><span class="sxs-lookup"><span data-stu-id="23ba9-181">Using these policies, you consider the risk level of the user or the sign-in to block risky sign-ins or require the user to perform multi-factor authentication.</span></span> <span data-ttu-id="23ba9-182">這些動作可防止攻擊者利用遭竊的身分識別而造成損害，而且會讓您有一些時間可保護身分識別。</span><span class="sxs-lookup"><span data-stu-id="23ba9-182">These actions may prevent an attacker from exploiting a stolen identity to cause damage, and may give you some time to secure the identity.</span></span>

### <a name="sign-in-risk-security-policy"></a><span data-ttu-id="23ba9-183">登入風險安全性原則</span><span class="sxs-lookup"><span data-stu-id="23ba9-183">Sign-in risk security policy</span></span>
<span data-ttu-id="23ba9-184">登入風險原則是條件式存取原則，可評估特定登入的風險，並根據預先定義的條件和規則來套用緩和動作。</span><span class="sxs-lookup"><span data-stu-id="23ba9-184">A sign-in risk policy is a conditional access policy that evaluates the risk to a specific sign-in and applies mitigations based on predefined conditions and rules.</span></span>

<span data-ttu-id="23ba9-185">![登入風險原則](./media/active-directory-identityprotection/1014.png "登入風險原則")</span><span class="sxs-lookup"><span data-stu-id="23ba9-185">![Sign-in risk policy](./media/active-directory-identityprotection/1014.png "Sign-in risk policy")</span></span>

<span data-ttu-id="23ba9-186">Azure AD Identity Protection 可讓您執行下列作業，以協助您管理有風險登入的緩和動作：</span><span class="sxs-lookup"><span data-stu-id="23ba9-186">Azure AD Identity Protection helps you manage the mitigation of risky sign-ins by enabling you to:</span></span>

* <span data-ttu-id="23ba9-187">設定要套用原則的使用者和群組：</span><span class="sxs-lookup"><span data-stu-id="23ba9-187">Set the users and groups the policy applies to:</span></span>

    <span data-ttu-id="23ba9-188">![登入風險原則](./media/active-directory-identityprotection/1015.png "登入風險原則")</span><span class="sxs-lookup"><span data-stu-id="23ba9-188">![Sign-in risk policy](./media/active-directory-identityprotection/1015.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="23ba9-189">設定可觸發原則的登入風險層級臨界值 (低、中或高)：</span><span class="sxs-lookup"><span data-stu-id="23ba9-189">Set the sign-in risk level threshold (low, medium, or high) that triggers the policy:</span></span>

    <span data-ttu-id="23ba9-190">![登入風險原則](./media/active-directory-identityprotection/1016.png "登入風險原則")</span><span class="sxs-lookup"><span data-stu-id="23ba9-190">![Sign-in risk policy](./media/active-directory-identityprotection/1016.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="23ba9-191">設定原則觸發時要強制執行的控制項︰</span><span class="sxs-lookup"><span data-stu-id="23ba9-191">Set the controls to be enforced when the policy triggers:</span></span>  

    <span data-ttu-id="23ba9-192">![登入風險原則](./media/active-directory-identityprotection/1017.png "登入風險原則")</span><span class="sxs-lookup"><span data-stu-id="23ba9-192">![Sign-in risk policy](./media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="23ba9-193">切換原則的狀態：</span><span class="sxs-lookup"><span data-stu-id="23ba9-193">Switch the state of your policy:</span></span>

    <span data-ttu-id="23ba9-194">![MFA 註冊](./media/active-directory-identityprotection/403.png "MFA 註冊")</span><span class="sxs-lookup"><span data-stu-id="23ba9-194">![MFA Registration](./media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="23ba9-195">在啟用變更前檢閱和評估其影響：</span><span class="sxs-lookup"><span data-stu-id="23ba9-195">Review and evaluate the impact of a change before activating it:</span></span>

    <span data-ttu-id="23ba9-196">![登入風險原則](./media/active-directory-identityprotection/1018.png "登入風險原則")</span><span class="sxs-lookup"><span data-stu-id="23ba9-196">![Sign-in risk policy](./media/active-directory-identityprotection/1018.png "Sign-in risk policy")</span></span>

#### <a name="what-you-need-to-know"></a><span data-ttu-id="23ba9-197">您所需了解的事情</span><span class="sxs-lookup"><span data-stu-id="23ba9-197">What you need to know</span></span>
<span data-ttu-id="23ba9-198">您可以設定登入風險安全性原則以要求 Multi-Factor Authentication︰</span><span class="sxs-lookup"><span data-stu-id="23ba9-198">You can configure a sign-in risk security policy to require multi-factor authentication:</span></span>

<span data-ttu-id="23ba9-199">![登入風險原則](./media/active-directory-identityprotection/1017.png "登入風險原則")</span><span class="sxs-lookup"><span data-stu-id="23ba9-199">![Sign-in risk policy](./media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>

<span data-ttu-id="23ba9-200">不過，基於安全性理由，這項設定只適用於已註冊 Multi-Factor Authentication 的使用者。</span><span class="sxs-lookup"><span data-stu-id="23ba9-200">However, for security reasons, this setting only works for users that have already been registered for multi-factor authentication.</span></span> <span data-ttu-id="23ba9-201">如果尚未註冊 Multi-Factor Authentication 的使用者很滿意要求 Multi-Factor Authentication 的條件，則會封鎖該使用者。</span><span class="sxs-lookup"><span data-stu-id="23ba9-201">If the condition to require multi-factor authentication is satisfied for a user who is not yet registered for multi-factor authentication, the user is blocked.</span></span>

<span data-ttu-id="23ba9-202">最佳作法是，如果您想對有風險的登入要求 Multi-Factor Authentication，您應該︰</span><span class="sxs-lookup"><span data-stu-id="23ba9-202">As a best practice, if you want to require multi-factor authentication for risky sign-ins, you should:</span></span>

1. <span data-ttu-id="23ba9-203">為受影響的使用者啟用 [Multi-Factor Authentication 註冊原則](#multi-factor-authentication-registration-policy)。</span><span class="sxs-lookup"><span data-stu-id="23ba9-203">Enable the [multi-factor authentication registration policy](#multi-factor-authentication-registration-policy) for the affected users.</span></span>
2. <span data-ttu-id="23ba9-204">要求受影響的使用者登入沒有危險的工作階段以執行 MFA 註冊</span><span class="sxs-lookup"><span data-stu-id="23ba9-204">Require the affected users to login in a non-risky session to perform a MFA registration</span></span>

<span data-ttu-id="23ba9-205">完成這些步驟可確保有風險的登入一定需要 Multi-Factor Authentication。</span><span class="sxs-lookup"><span data-stu-id="23ba9-205">Completing these steps ensures that multi-factor authentication is required for a risky sign-in.</span></span>

#### <a name="best-practices"></a><span data-ttu-id="23ba9-206">最佳作法</span><span class="sxs-lookup"><span data-stu-id="23ba9-206">Best practices</span></span>
<span data-ttu-id="23ba9-207">選擇 [高]  臨界值可減少觸發原則的次數，並將對使用者的影響降至最低。</span><span class="sxs-lookup"><span data-stu-id="23ba9-207">Choosing a **High** threshold reduces the number of times a policy is triggered and minimizes the impact to users.</span></span>  

<span data-ttu-id="23ba9-208">不過，它會從原則中排除標示 [低] 和 [中] 度風險的登入，而無法阻止攻擊者利用遭到入侵的身分識別。</span><span class="sxs-lookup"><span data-stu-id="23ba9-208">However, it excludes **Low** and **Medium** sign-ins flagged for risk from the policy, which may not block an attacker from exploiting a compromised identity.</span></span>

<span data-ttu-id="23ba9-209">設定原則時，</span><span class="sxs-lookup"><span data-stu-id="23ba9-209">When setting the policy,</span></span>

* <span data-ttu-id="23ba9-210">排除不會 / 不能有 Multi-Factor Authentication 的使用者</span><span class="sxs-lookup"><span data-stu-id="23ba9-210">Exclude users who do not/cannot have multi-factor authentication</span></span>
* <span data-ttu-id="23ba9-211">在啟用原則並不實用 (例如無法存取技術服務人員) 的地區設定中排除使用者</span><span class="sxs-lookup"><span data-stu-id="23ba9-211">Exclude users in locales where enabling the policy is not practical (for example no access to helpdesk)</span></span>
* <span data-ttu-id="23ba9-212">排除可能會產生大量誤判的使用者 (開發人員、安全性分析人員)</span><span class="sxs-lookup"><span data-stu-id="23ba9-212">Exclude users who are likely to generate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="23ba9-213">在原則推出初期，或如果您必須盡量減少使用者所看到的挑戰，請使用 [高]  臨界值。</span><span class="sxs-lookup"><span data-stu-id="23ba9-213">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="23ba9-214">如果您的組織需要更高的安全性，請使用 [低]  臨界值。</span><span class="sxs-lookup"><span data-stu-id="23ba9-214">Use a **Low**  threshold if your organization requires greater security.</span></span> <span data-ttu-id="23ba9-215">選取 [低]  臨界值會帶來額外的使用者登入挑戰，並提高安全性。</span><span class="sxs-lookup"><span data-stu-id="23ba9-215">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="23ba9-216">大部分組織的建議預設值是設定 [中]  臨界值的規則，以取得可用性與安全性之間的平衡。</span><span class="sxs-lookup"><span data-stu-id="23ba9-216">The recommended default for most organizations is to configure a rule for a **Medium** threshold to strike a balance between usability and security.</span></span>

<span data-ttu-id="23ba9-217">登入風險原則：</span><span class="sxs-lookup"><span data-stu-id="23ba9-217">The sign-in risk policy is:</span></span>

* <span data-ttu-id="23ba9-218">會套用至所有使用新式驗證的瀏覽器流量和登入。</span><span class="sxs-lookup"><span data-stu-id="23ba9-218">Applied to all browser traffic and sign-ins using modern authentication.</span></span>
* <span data-ttu-id="23ba9-219">不會套用至使用較舊安全性通訊協定的應用程式，其做法是停用位於同盟 IDP (例如 ADFS) 的 WS-Trust 端點。</span><span class="sxs-lookup"><span data-stu-id="23ba9-219">Not applied to applications using older security protocols by disabling the WS-Trust endpoint at the federated IDP, such as ADFS.</span></span>

<span data-ttu-id="23ba9-220">Identity Protection 主控台中的 [風險事件]  頁面會列出所有事件：</span><span class="sxs-lookup"><span data-stu-id="23ba9-220">The **Risk Events** page in the Identity Protection console lists all events:</span></span>

* <span data-ttu-id="23ba9-221">此原則已套用至</span><span class="sxs-lookup"><span data-stu-id="23ba9-221">This policy was applied to</span></span>
* <span data-ttu-id="23ba9-222">您可以檢閱活動並判斷動作是否適當</span><span class="sxs-lookup"><span data-stu-id="23ba9-222">You can review the activity and determine whether the action was appropriate or not</span></span>

<span data-ttu-id="23ba9-223">如需相關的使用者經驗概觀，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="23ba9-223">For an overview of the related user experience, see:</span></span>

* [<span data-ttu-id="23ba9-224">有風險的登入復原</span><span class="sxs-lookup"><span data-stu-id="23ba9-224">Risky sign-in recovery</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-recovery)
* [<span data-ttu-id="23ba9-225">已封鎖有風險的登入</span><span class="sxs-lookup"><span data-stu-id="23ba9-225">Risky sign-in blocked</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-blocked)  
* [<span data-ttu-id="23ba9-226">使用 Azure AD Identity Protection 時的登入體驗</span><span class="sxs-lookup"><span data-stu-id="23ba9-226">Sign-in experiences with Azure AD Identity Protection</span></span>](active-directory-identityprotection-flows.md)  

<span data-ttu-id="23ba9-227">**開啟相關的組態對話方塊**：</span><span class="sxs-lookup"><span data-stu-id="23ba9-227">**To open the related configuration dialog**:</span></span>

- <span data-ttu-id="23ba9-228">在 [Azure AD Identity Protection] 刀鋒視窗的 [設定] 區段中，按一下 [登入風險原則]。</span><span class="sxs-lookup"><span data-stu-id="23ba9-228">On the **Azure AD Identity Protection** blade, in the **Configure** section, click **Sign-in risk policy**.</span></span>

    <span data-ttu-id="23ba9-229">![使用者風險原則](./media/active-directory-identityprotection/1014.png "使用者風險原則")</span><span class="sxs-lookup"><span data-stu-id="23ba9-229">![User ridk policy](./media/active-directory-identityprotection/1014.png "User ridk policy")</span></span>



## <a name="users-flagged-for-risk"></a><span data-ttu-id="23ba9-230">標示有風險的使用者</span><span class="sxs-lookup"><span data-stu-id="23ba9-230">Users flagged for risk</span></span>

<span data-ttu-id="23ba9-231">由 Azure Active Directory 針對某個使用者所偵測到的所有[作用中風險事件](active-directory-identity-protection-risk-events.md)，構成了名為使用者風險的邏輯概念。</span><span class="sxs-lookup"><span data-stu-id="23ba9-231">All active [risk events](active-directory-identity-protection-risk-events.md) that were detected by Azure Active Directory for a user contribute to a logical concept called user risk.</span></span> <span data-ttu-id="23ba9-232">標幟為有風險的使用者表示可能被盜用的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="23ba9-232">A user flagged for risk is an indicator for a user account that might have been compromised.</span></span>

![標示有風險的使用者](./media/active-directory-identityprotection/1200.png)


### <a name="user-risk-level"></a><span data-ttu-id="23ba9-234">使用者風險層級</span><span class="sxs-lookup"><span data-stu-id="23ba9-234">User risk level</span></span>

<span data-ttu-id="23ba9-235">使用者風險層級可指出使用者的身分識別遭到入侵的可能性 (高、中或低)。</span><span class="sxs-lookup"><span data-stu-id="23ba9-235">A user risk level is an indication (High, Medium, or Low) of the likelihood that the user’s identity has been compromised.</span></span> <span data-ttu-id="23ba9-236">它會根據與使用者的身分識別相關聯的使用者風險事件進行計算。</span><span class="sxs-lookup"><span data-stu-id="23ba9-236">It is calculated based on the user risk events that are associated with a user's identity.</span></span>

<span data-ttu-id="23ba9-237">風險事件的狀態為 [作用中] 或 [已關閉]。</span><span class="sxs-lookup"><span data-stu-id="23ba9-237">The status of a risk event is either **Active** or **Closed**.</span></span> <span data-ttu-id="23ba9-238">只有 [作用中] 的風險事件會納入使用者風險層級計算。</span><span class="sxs-lookup"><span data-stu-id="23ba9-238">Only risk events that are **Active** contribute to the user risk level calculation.</span></span>

<span data-ttu-id="23ba9-239">使用下列輸入來計算使用者風險層級：</span><span class="sxs-lookup"><span data-stu-id="23ba9-239">The user risk level is calculated using the following inputs:</span></span>

* <span data-ttu-id="23ba9-240">影響使用者的作用中風險事件</span><span class="sxs-lookup"><span data-stu-id="23ba9-240">Active risk events impacting the user</span></span>
* <span data-ttu-id="23ba9-241">這些事件的風險層級</span><span class="sxs-lookup"><span data-stu-id="23ba9-241">Risk level of these events</span></span>
* <span data-ttu-id="23ba9-242">是否已採取任何補救動作</span><span class="sxs-lookup"><span data-stu-id="23ba9-242">Whether any remediation actions have been taken</span></span>

<span data-ttu-id="23ba9-243">![使用者風險](./media/active-directory-identityprotection/1031.png "使用者風險")</span><span class="sxs-lookup"><span data-stu-id="23ba9-243">![User risks](./media/active-directory-identityprotection/1031.png "User risks")</span></span>

<span data-ttu-id="23ba9-244">您可以使用使用者風險層級來建立條件式存取原則，以阻止有風險的使用者進行登入，或迫使他們安全地變更其密碼。</span><span class="sxs-lookup"><span data-stu-id="23ba9-244">You can use the user risk levels to create conditional access policies that block risky users from signing in, or force them to securely change their password.</span></span>

### <a name="closing-risk-events-manually"></a><span data-ttu-id="23ba9-245">手動關閉風險事件</span><span class="sxs-lookup"><span data-stu-id="23ba9-245">Closing risk events manually</span></span>

<span data-ttu-id="23ba9-246">在大部分情況下，您將採取補救動作 (例如重設安全的密碼) 來自動關閉風險事件。</span><span class="sxs-lookup"><span data-stu-id="23ba9-246">In most cases, you will take remediation actions such as a secure password reset to automatically close risk events.</span></span> <span data-ttu-id="23ba9-247">但是，這不一定都可行。</span><span class="sxs-lookup"><span data-stu-id="23ba9-247">However, this might not always be possible.</span></span>  
<span data-ttu-id="23ba9-248">比方說，在下列情況下即是如此︰</span><span class="sxs-lookup"><span data-stu-id="23ba9-248">This is, for example, the case, when:</span></span>

* <span data-ttu-id="23ba9-249">已刪除具有作用中風險事件的使用者</span><span class="sxs-lookup"><span data-stu-id="23ba9-249">A user with Active risk events has been deleted</span></span>
* <span data-ttu-id="23ba9-250">調查顯示合法的使用者已執行報告的風險事件</span><span class="sxs-lookup"><span data-stu-id="23ba9-250">An investigation reveals that a reported risk event has been perform by the legitimate user</span></span>

<span data-ttu-id="23ba9-251">因為 [作用中]  的風險事件會納入使用者風險計算，所以您可能必須以手動方式降低風險層級，但不要手動關閉風險事件。</span><span class="sxs-lookup"><span data-stu-id="23ba9-251">Because risk events that are **Active** contribute to the user risk calculation, you may have to manually lower a risk level by closing risk events manually.</span></span>  
<span data-ttu-id="23ba9-252">在調查過程中，您可以選擇採取下列任何動作，以變更風險事件的狀態：</span><span class="sxs-lookup"><span data-stu-id="23ba9-252">During the course of investigation, you can choose to take any of these actions to change the status of a risk event:</span></span>

<span data-ttu-id="23ba9-253">![動作](./media/active-directory-identityprotection/34.png "動作")</span><span class="sxs-lookup"><span data-stu-id="23ba9-253">![Actions](./media/active-directory-identityprotection/34.png "Actions")</span></span>

* <span data-ttu-id="23ba9-254">**解決** - 如果在調查風險事件之後，您在 Identity Protection 外部採取適當的補救動作，而且您認為應該將風險事件視為已關閉，請將事件標示為 [已解決]。</span><span class="sxs-lookup"><span data-stu-id="23ba9-254">**Resolve** - If after investigating a risk event, you took an appropriate remediation action outside Identity Protection, and you believe that the risk event should be considered closed, mark the event as Resolved.</span></span> <span data-ttu-id="23ba9-255">解決的事件會將風險事件的狀態設定為 [已關閉]，而此風險事件便不再算是使用者風險。</span><span class="sxs-lookup"><span data-stu-id="23ba9-255">Resolved events will set the risk event’s status to Closed and the risk event will no longer contribute to user risk.</span></span>
* <span data-ttu-id="23ba9-256">**標示為誤判** - 在某些情況下，您可能會調查某個風險事件並發現該事件被誤標為有風險。</span><span class="sxs-lookup"><span data-stu-id="23ba9-256">**Mark as false-positive** - In some cases, you may investigate a risk event and discover that it was incorrectly flagged as a risky.</span></span> <span data-ttu-id="23ba9-257">您可以將風險事件標示為誤判，以減少發生這種情況。</span><span class="sxs-lookup"><span data-stu-id="23ba9-257">You can help reduce the number of such occurrences by marking the risk event as False-positive.</span></span> <span data-ttu-id="23ba9-258">這可協助機器學習演算法未來改善類似事件的分類。</span><span class="sxs-lookup"><span data-stu-id="23ba9-258">This will help the machine learning algorithms to improve the classification of similar events in the future.</span></span> <span data-ttu-id="23ba9-259">誤判事件的狀態為 [已關閉]  ，而且不再算是使用者風險。</span><span class="sxs-lookup"><span data-stu-id="23ba9-259">The status of false-positive events is to **Closed** and they will no longer contribute to user risk.</span></span>
* <span data-ttu-id="23ba9-260">**忽略** - 如果您尚未採取任何補救動作，但希望風險事件從作用中清單中移除，您可忽略風險事件，且事件狀態將會是 [已關閉]。</span><span class="sxs-lookup"><span data-stu-id="23ba9-260">**Ignore** - If you have not taken any remediation action, but want the risk event to be removed from the active list, you can mark a risk event Ignore and the event status will be Closed.</span></span> <span data-ttu-id="23ba9-261">忽略的事件不算是使用者風險。</span><span class="sxs-lookup"><span data-stu-id="23ba9-261">Ignored events do not contribute to user risk.</span></span> <span data-ttu-id="23ba9-262">這個選項只能用於不尋常的情況下。</span><span class="sxs-lookup"><span data-stu-id="23ba9-262">This option should only be used under unusual circumstances.</span></span>
* <span data-ttu-id="23ba9-263">**重新啟用** - 可以重新啟用已手動關閉的風險事件 (藉由選擇 [解決]、[誤判] 或 [略過])，並將事件狀態設回 [作用中]。</span><span class="sxs-lookup"><span data-stu-id="23ba9-263">**Reactivate** - Risk events that were manually closed (by choosing **Resolve**, **False positive**, or **Ignore**) can be reactivated, setting the event status back to **Active**.</span></span> <span data-ttu-id="23ba9-264">重新啟用的風險事件會納入使用者風險層級計算。</span><span class="sxs-lookup"><span data-stu-id="23ba9-264">Reactivated risk events contribute to the user risk level calculation.</span></span> <span data-ttu-id="23ba9-265">無法重新啟用透過補救 (例如重設安全的密碼) 關閉的風險事件。</span><span class="sxs-lookup"><span data-stu-id="23ba9-265">Risk events closed through remediation (such as a secure password reset) cannot be reactivated.</span></span>

<span data-ttu-id="23ba9-266">**開啟相關的組態對話方塊**：</span><span class="sxs-lookup"><span data-stu-id="23ba9-266">**To open the related configuration dialog**:</span></span>

1. <span data-ttu-id="23ba9-267">在 [Azure AD Identity Protection] 刀鋒視窗的 [調查] 底下，按一下 [風險事件]。</span><span class="sxs-lookup"><span data-stu-id="23ba9-267">On the **Azure AD Identity Protection** blade, under **Investigate**, click **Risk events**.</span></span>

    <span data-ttu-id="23ba9-268">![手動密碼重設](./media/active-directory-identityprotection/1002.png "手動密碼重設")</span><span class="sxs-lookup"><span data-stu-id="23ba9-268">![Manual password reset](./media/active-directory-identityprotection/1002.png "Manual password reset")</span></span>
2. <span data-ttu-id="23ba9-269">在 [風險事件]  清單中，點選一個風險。</span><span class="sxs-lookup"><span data-stu-id="23ba9-269">In the **Risk events** list, click a risk.</span></span>

    <span data-ttu-id="23ba9-270">![手動密碼重設](./media/active-directory-identityprotection/1003.png "手動密碼重設")</span><span class="sxs-lookup"><span data-stu-id="23ba9-270">![Manual password reset](./media/active-directory-identityprotection/1003.png "Manual password reset")</span></span>
3. <span data-ttu-id="23ba9-271">在 [風險] 刀鋒視窗中，按右鍵點選一個使用者。</span><span class="sxs-lookup"><span data-stu-id="23ba9-271">On the risk blade, right-click a user.</span></span>

    <span data-ttu-id="23ba9-272">![手動密碼重設](./media/active-directory-identityprotection/1004.png "手動密碼重設")</span><span class="sxs-lookup"><span data-stu-id="23ba9-272">![Manual password reset](./media/active-directory-identityprotection/1004.png "Manual password reset")</span></span>

### <a name="closing-all-risk-events-for-a-user-manually"></a><span data-ttu-id="23ba9-273">手動關閉使用者的所有風險事件</span><span class="sxs-lookup"><span data-stu-id="23ba9-273">Closing all risk events for a user manually</span></span>
<span data-ttu-id="23ba9-274">Azure Active Directory Identity Protection 也提供按一下即可為使用者關閉所有事件的方法，而不需個別手動關閉使用者的風險事件。</span><span class="sxs-lookup"><span data-stu-id="23ba9-274">Instead of manually closing risk events for a user individually, Azure Active Directory Identity Protection also provides you with a method to close all events for a user with one click.</span></span>

<span data-ttu-id="23ba9-275">![動作](./media/active-directory-identityprotection/2222.png "動作")</span><span class="sxs-lookup"><span data-stu-id="23ba9-275">![Actions](./media/active-directory-identityprotection/2222.png "Actions")</span></span>

<span data-ttu-id="23ba9-276">當您按一下 [關閉所有事件] ，所有事件都已關閉，且受影響的使用者不再有風險。</span><span class="sxs-lookup"><span data-stu-id="23ba9-276">When you click **Dismiss all events**, all events are closed and the affected user is no longer at risk.</span></span>

### <a name="remediating-user-risk-events"></a><span data-ttu-id="23ba9-277">補救使用者風險事件</span><span class="sxs-lookup"><span data-stu-id="23ba9-277">Remediating user risk events</span></span>

<span data-ttu-id="23ba9-278">補救就是用來保護先前疑似或已知遭到入侵的身分識別或裝置的動作。</span><span class="sxs-lookup"><span data-stu-id="23ba9-278">A remediation is an action to secure an identity or a device that was previously suspected or known to be compromised.</span></span> <span data-ttu-id="23ba9-279">補救動作可讓身分識別或裝置還原到安全的狀態，以及解決先前與身分識別或裝置相關聯的風險事件。</span><span class="sxs-lookup"><span data-stu-id="23ba9-279">A remediation action restores the identity or device to a safe state, and resolves previous risk events associated with the identity or device.</span></span>

<span data-ttu-id="23ba9-280">若要補救使用者風險事件，您可以：</span><span class="sxs-lookup"><span data-stu-id="23ba9-280">To remediate user risk events, you can:</span></span>

* <span data-ttu-id="23ba9-281">手動重設安全密碼，以補救使用者風險事件</span><span class="sxs-lookup"><span data-stu-id="23ba9-281">Perform a secure password reset to remediate user risk events manually</span></span>
* <span data-ttu-id="23ba9-282">設定使用者風險安全性原則，以自動緩和或補救使用者風險事件</span><span class="sxs-lookup"><span data-stu-id="23ba9-282">Configure a user risk security policy to mitigate or remediate user risk events automatically</span></span>
* <span data-ttu-id="23ba9-283">重新製作受感染裝置的映像</span><span class="sxs-lookup"><span data-stu-id="23ba9-283">Re-image the infected device</span></span>  

#### <a name="manual-secure-password-reset"></a><span data-ttu-id="23ba9-284">手動重設安全密碼</span><span class="sxs-lookup"><span data-stu-id="23ba9-284">Manual secure password reset</span></span>
<span data-ttu-id="23ba9-285">重設安全的密碼是許多風險事件的有效補救動作，一旦執行，就會自動關閉這些風險事件並重新計算使用者風險層級。</span><span class="sxs-lookup"><span data-stu-id="23ba9-285">A secure password reset is an effective remediation for many risk events, and when performed, automatically closes these risk events and recalculates the user risk level.</span></span> <span data-ttu-id="23ba9-286">您可以使用 Identity Protection 儀表板，為有風險的使用者起始密碼重設。</span><span class="sxs-lookup"><span data-stu-id="23ba9-286">You can use the Identity Protection dashboard to initiate a password reset for a risky user.</span></span>

<span data-ttu-id="23ba9-287">相關的對話方塊提供兩個不同的方法，可以將密碼重設為︰</span><span class="sxs-lookup"><span data-stu-id="23ba9-287">The related dialog provides two different methods to reset a password:</span></span>

<span data-ttu-id="23ba9-288">**重設密碼** - 選取 [要求使用者重設密碼] 以允許使用者執行自助復原 (若該使用者已針對多重要素驗證註冊)。</span><span class="sxs-lookup"><span data-stu-id="23ba9-288">**Reset password** - Select **Require the user to reset their password** to allow the user to self-recover if the user has registered for multi-factor authentication.</span></span> <span data-ttu-id="23ba9-289">在使用者下次登入期間，使用者必須成功解決 Multi-Factor Authentication 挑戰，且被迫變更密碼。</span><span class="sxs-lookup"><span data-stu-id="23ba9-289">During the user's next sign-in, the user will be required to solve a multi-factor authentication challenge successfully and then, forced to change the password.</span></span> <span data-ttu-id="23ba9-290">如果使用者帳戶尚未註冊 Multi-Factor Authentication，則無法使用此選項。</span><span class="sxs-lookup"><span data-stu-id="23ba9-290">This option isn't available if the user account is not already registered multi-factor authentication.</span></span>

<span data-ttu-id="23ba9-291">**暫時密碼** - 選取 [產生暫時密碼]，立即讓現有的密碼失效，並且為使用者建立新的暫時密碼。</span><span class="sxs-lookup"><span data-stu-id="23ba9-291">**Temporary password** - Select **Generate a temporary password** to immediately invalidate the existing password, and create a new temporary password for the user.</span></span> <span data-ttu-id="23ba9-292">將新的暫時密碼傳送到使用者的備用電子郵件地址，或傳送給使用者的經理。</span><span class="sxs-lookup"><span data-stu-id="23ba9-292">Send the new temporary password to an alternate email address for the user or to the user's manager.</span></span> <span data-ttu-id="23ba9-293">因為此密碼是暫時的，所以會提示使用者在登入時變更密碼。</span><span class="sxs-lookup"><span data-stu-id="23ba9-293">Because the password is temporary, the user will be prompted to change the password upon sign-in.</span></span>

<span data-ttu-id="23ba9-294">![原則](./media/active-directory-identityprotection/1005.png "原則")</span><span class="sxs-lookup"><span data-stu-id="23ba9-294">![Policy](./media/active-directory-identityprotection/1005.png "Policy")</span></span>

<span data-ttu-id="23ba9-295">**開啟相關的組態對話方塊**：</span><span class="sxs-lookup"><span data-stu-id="23ba9-295">**To open the related configuration dialog**:</span></span>

1. <span data-ttu-id="23ba9-296">在 [Azure AD Identity Protection] 刀鋒視窗上，按一下 [標示為危險的使用者]。</span><span class="sxs-lookup"><span data-stu-id="23ba9-296">On the **Azure AD Identity Protection** blade, click **Users flagged for risk**.</span></span>

    <span data-ttu-id="23ba9-297">![手動密碼重設](./media/active-directory-identityprotection/1006.png "手動密碼重設")</span><span class="sxs-lookup"><span data-stu-id="23ba9-297">![Manual password reset](./media/active-directory-identityprotection/1006.png "Manual password reset")</span></span>
2. <span data-ttu-id="23ba9-298">從使用者清單中，選取具有至少一個風險事件的使用者。</span><span class="sxs-lookup"><span data-stu-id="23ba9-298">From the list of users, select a user with at least one risk events.</span></span>

    <span data-ttu-id="23ba9-299">![手動密碼重設](./media/active-directory-identityprotection/1007.png "手動密碼重設")</span><span class="sxs-lookup"><span data-stu-id="23ba9-299">![Manual password reset](./media/active-directory-identityprotection/1007.png "Manual password reset")</span></span>
3. <span data-ttu-id="23ba9-300">在 [使用者] 刀鋒視窗中，按一下 [重設密碼] 。</span><span class="sxs-lookup"><span data-stu-id="23ba9-300">On the user blade, click **Reset password**.</span></span>

    <span data-ttu-id="23ba9-301">![手動密碼重設](./media/active-directory-identityprotection/1008.png "手動密碼重設")</span><span class="sxs-lookup"><span data-stu-id="23ba9-301">![Manual password reset](./media/active-directory-identityprotection/1008.png "Manual password reset")</span></span>

### <a name="user-risk-security-policy"></a><span data-ttu-id="23ba9-302">使用者風險安全性原則</span><span class="sxs-lookup"><span data-stu-id="23ba9-302">User risk security policy</span></span>
<span data-ttu-id="23ba9-303">使用者風險安全性原則是條件式存取原則，可評估特定使用者的風險層級，並根據預先定義的條件和規則來套用補救和緩和動作。</span><span class="sxs-lookup"><span data-stu-id="23ba9-303">A user risk security policy is a conditional access policy that evaluates the risk level to a specific user and applies remediation and mitigation actions based on predefined conditions and rules.</span></span>

<span data-ttu-id="23ba9-304">![使用者風險原則](./media/active-directory-identityprotection/1009.png "使用者風險原則")</span><span class="sxs-lookup"><span data-stu-id="23ba9-304">![User ridk policy](./media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

<span data-ttu-id="23ba9-305">Azure AD Identity Protection 可讓您執行下列作業，以協助您管理標示有風險的使用者的緩和與補救動作：</span><span class="sxs-lookup"><span data-stu-id="23ba9-305">Azure AD Identity Protection helps you manage the mitigation and remediation of users flagged for risk by enabling you to:</span></span>

* <span data-ttu-id="23ba9-306">設定要套用原則的使用者和群組：</span><span class="sxs-lookup"><span data-stu-id="23ba9-306">Set the users and groups the policy applies to:</span></span>

    <span data-ttu-id="23ba9-307">![使用者風險原則](./media/active-directory-identityprotection/1010.png "使用者風險原則")</span><span class="sxs-lookup"><span data-stu-id="23ba9-307">![User ridk policy](./media/active-directory-identityprotection/1010.png "User ridk policy")</span></span>
* <span data-ttu-id="23ba9-308">設定可觸發原則的使用者風險層級臨界值 (低、中或高)：</span><span class="sxs-lookup"><span data-stu-id="23ba9-308">Set the user risk level threshold (low, medium, or high) that triggers the policy:</span></span>

    <span data-ttu-id="23ba9-309">![使用者風險原則](./media/active-directory-identityprotection/1011.png "使用者風險原則")</span><span class="sxs-lookup"><span data-stu-id="23ba9-309">![User ridk policy](./media/active-directory-identityprotection/1011.png "User ridk policy")</span></span>
* <span data-ttu-id="23ba9-310">設定原則觸發時要強制執行的控制項︰</span><span class="sxs-lookup"><span data-stu-id="23ba9-310">Set the controls to be enforced when the policy triggers:</span></span>

    <span data-ttu-id="23ba9-311">![使用者風險原則](./media/active-directory-identityprotection/1012.png "使用者風險原則")</span><span class="sxs-lookup"><span data-stu-id="23ba9-311">![User ridk policy](./media/active-directory-identityprotection/1012.png "User ridk policy")</span></span>
* <span data-ttu-id="23ba9-312">切換原則的狀態：</span><span class="sxs-lookup"><span data-stu-id="23ba9-312">Switch the state of your policy:</span></span>

    <span data-ttu-id="23ba9-313">![使用者風險原則](./media/active-directory-identityprotection/403.png "MFA 註冊")</span><span class="sxs-lookup"><span data-stu-id="23ba9-313">![User ridk policy](./media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="23ba9-314">在啟用變更前檢閱和評估其影響：</span><span class="sxs-lookup"><span data-stu-id="23ba9-314">Review and evaluate the impact of a change before activating it:</span></span>

    <span data-ttu-id="23ba9-315">![使用者風險原則](./media/active-directory-identityprotection/1013.png "使用者風險原則")</span><span class="sxs-lookup"><span data-stu-id="23ba9-315">![User ridk policy](./media/active-directory-identityprotection/1013.png "User ridk policy")</span></span>

<span data-ttu-id="23ba9-316">選擇 [高]  臨界值可減少觸發原則的次數，並將對使用者的影響降至最低。</span><span class="sxs-lookup"><span data-stu-id="23ba9-316">Choosing a **High** threshold reduces the number of times a policy is triggered and minimizes the impact to users.</span></span>
<span data-ttu-id="23ba9-317">不過，這會從原則中排除標示 [低] 和 [中] 度風險的使用者，而無法保護先前疑似或已知遭到入侵的身分識別或裝置。</span><span class="sxs-lookup"><span data-stu-id="23ba9-317">However, it excludes **Low** and **Medium** users flagged for risk from the policy, which may not secure identities or devices that were previously suspected or known to be compromised.</span></span>

<span data-ttu-id="23ba9-318">設定原則時，</span><span class="sxs-lookup"><span data-stu-id="23ba9-318">When setting the policy,</span></span>

* <span data-ttu-id="23ba9-319">排除可能會產生大量誤判的使用者 (開發人員、安全性分析人員)</span><span class="sxs-lookup"><span data-stu-id="23ba9-319">Exclude users who are likely to generate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="23ba9-320">在啟用原則並不實用 (例如無法存取技術服務人員) 的地區設定中排除使用者</span><span class="sxs-lookup"><span data-stu-id="23ba9-320">Exclude users in locales where enabling the policy is not practical (for example no access to helpdesk)</span></span>
* <span data-ttu-id="23ba9-321">在原則推出初期，或如果您必須盡量減少使用者所看到的挑戰，請使用 [高]  臨界值。</span><span class="sxs-lookup"><span data-stu-id="23ba9-321">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="23ba9-322">如果您的組織需要更高的安全性，請使用 [低]  臨界值。</span><span class="sxs-lookup"><span data-stu-id="23ba9-322">Use a **Low** threshold if your organization requires greater security.</span></span> <span data-ttu-id="23ba9-323">選取 [低]  臨界值會帶來額外的使用者登入挑戰，並提高安全性。</span><span class="sxs-lookup"><span data-stu-id="23ba9-323">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="23ba9-324">大部分組織的建議預設值是設定 [中]  臨界值的規則，以取得可用性與安全性之間的平衡。</span><span class="sxs-lookup"><span data-stu-id="23ba9-324">The recommended default for most organizations is to configure a rule for a **Medium** threshold to strike a balance between usability and security.</span></span>

<span data-ttu-id="23ba9-325">如需相關的使用者經驗概觀，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="23ba9-325">For an overview of the related user experience, see:</span></span>

* <span data-ttu-id="23ba9-326">[遭到入侵的帳戶復原流程](active-directory-identityprotection-flows.md#compromised-account-recovery)。</span><span class="sxs-lookup"><span data-stu-id="23ba9-326">[Compromised account recovery flow](active-directory-identityprotection-flows.md#compromised-account-recovery).</span></span>  
* <span data-ttu-id="23ba9-327">[遭到入侵的帳戶封鎖流程](active-directory-identityprotection-flows.md#compromised-account-blocked)。</span><span class="sxs-lookup"><span data-stu-id="23ba9-327">[Compromised account blocked flow](active-directory-identityprotection-flows.md#compromised-account-blocked).</span></span>  

<span data-ttu-id="23ba9-328">**開啟相關的組態對話方塊**：</span><span class="sxs-lookup"><span data-stu-id="23ba9-328">**To open the related configuration dialog**:</span></span>

- <span data-ttu-id="23ba9-329">在 [Azure AD Identity Protection] 刀鋒視窗的 [設定] 區段中，按一下 [使用者風險原則]。</span><span class="sxs-lookup"><span data-stu-id="23ba9-329">On the **Azure AD Identity Protection** blade, in the **Configure** section, click **User risk policy**.</span></span>

    <span data-ttu-id="23ba9-330">![使用者風險原則](./media/active-directory-identityprotection/1009.png "使用者風險原則")</span><span class="sxs-lookup"><span data-stu-id="23ba9-330">![User ridk policy](./media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

### <a name="mitigating-user-risk-events"></a><span data-ttu-id="23ba9-331">緩和使用者風險事件</span><span class="sxs-lookup"><span data-stu-id="23ba9-331">Mitigating user risk events</span></span>
<span data-ttu-id="23ba9-332">系統管理員可以設定使用者風險安全性原則，以根據風險層級防止使用者登入。</span><span class="sxs-lookup"><span data-stu-id="23ba9-332">Administrators can set a user risk security policy to block users upon sign-in depending on the risk level.</span></span>

<span data-ttu-id="23ba9-333">封鎖登入：</span><span class="sxs-lookup"><span data-stu-id="23ba9-333">Blocking a sign-in:</span></span>

* <span data-ttu-id="23ba9-334">避免對受影響的使用者產生新的使用者風險事件</span><span class="sxs-lookup"><span data-stu-id="23ba9-334">Prevents the generation of new user risk events for the affected user</span></span>
* <span data-ttu-id="23ba9-335">可讓系統管理員手動地補救會影響使用者身分識別的風險事件，並將它還原到安全的狀態</span><span class="sxs-lookup"><span data-stu-id="23ba9-335">Enables administrators to manually remediate the risk events affecting the user's identity and restore it to a secure state</span></span>



## <a name="multi-factor-authentication-registration-policy"></a><span data-ttu-id="23ba9-336">Multi-Factor Authentication 註冊原則</span><span class="sxs-lookup"><span data-stu-id="23ba9-336">Multi-factor authentication registration policy</span></span>
<span data-ttu-id="23ba9-337">Azure Multi-Factor Authentication 是除了使用使用者名稱與密碼之外，需要再利用其他方法驗證身份的驗證方法。</span><span class="sxs-lookup"><span data-stu-id="23ba9-337">Azure multi-factor authentication is a method of verifying who you are that requires the use of more than just a username and password.</span></span> <span data-ttu-id="23ba9-338">它可以為使用者登入和交易提供第二層安全性。</span><span class="sxs-lookup"><span data-stu-id="23ba9-338">It provides a second layer of security to user sign-ins and transactions.</span></span>  
<span data-ttu-id="23ba9-339">建議您要求對使用者登入進行 Azure Multi-Factor Authentication，因為它：</span><span class="sxs-lookup"><span data-stu-id="23ba9-339">We recommend that you require Azure multi-factor authentication for user sign-ins because it:</span></span>

* <span data-ttu-id="23ba9-340">提供增強式驗證與一系列簡單的驗證選項</span><span class="sxs-lookup"><span data-stu-id="23ba9-340">Delivers strong authentication with a range of easy verification options</span></span>
* <span data-ttu-id="23ba9-341">扮演著舉足輕重的角色，可讓您的組織防護帳戶遭竊及從中復原</span><span class="sxs-lookup"><span data-stu-id="23ba9-341">Plays a key role in preparing your organization to protect and recover from account compromises</span></span>

<span data-ttu-id="23ba9-342">![使用者風險原則](./media/active-directory-identityprotection/1019.png "使用者風險原則")</span><span class="sxs-lookup"><span data-stu-id="23ba9-342">![User ridk policy](./media/active-directory-identityprotection/1019.png "User ridk policy")</span></span>

<span data-ttu-id="23ba9-343">如需詳細資訊，請參閱 [什麼是 Azure Multi-Factor Authentication？](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="23ba9-343">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

<span data-ttu-id="23ba9-344">Azure AD Identity Protection 可讓您設定原則來執行下列作業，以協助您管理首次 Multi-Factor Authentication 註冊：</span><span class="sxs-lookup"><span data-stu-id="23ba9-344">Azure AD Identity Protection helps you manage the roll-out of multi-factor authentication registration by configuring a policy that enables you to:</span></span>

* <span data-ttu-id="23ba9-345">設定要套用原則的使用者和群組：</span><span class="sxs-lookup"><span data-stu-id="23ba9-345">Set the users and groups the policy applies to:</span></span>

    <span data-ttu-id="23ba9-346">![MFA 原則](./media/active-directory-identityprotection/1020.png "MFA 原則")</span><span class="sxs-lookup"><span data-stu-id="23ba9-346">![MFA policy](./media/active-directory-identityprotection/1020.png "MFA policy")</span></span>
* <span data-ttu-id="23ba9-347">設定原則觸發時要強制執行的控制項︰：</span><span class="sxs-lookup"><span data-stu-id="23ba9-347">Set the controls to be enforced when the policy triggers::</span></span>  

    <span data-ttu-id="23ba9-348">![MFA 原則](./media/active-directory-identityprotection/1021.png "MFA 原則")</span><span class="sxs-lookup"><span data-stu-id="23ba9-348">![MFA policy](./media/active-directory-identityprotection/1021.png "MFA policy")</span></span>
* <span data-ttu-id="23ba9-349">切換原則的狀態：</span><span class="sxs-lookup"><span data-stu-id="23ba9-349">Switch the state of your policy:</span></span>

    <span data-ttu-id="23ba9-350">![MFA 原則](./media/active-directory-identityprotection/403.png "MFA 原則")</span><span class="sxs-lookup"><span data-stu-id="23ba9-350">![MFA policy](./media/active-directory-identityprotection/403.png "MFA policy")</span></span>
* <span data-ttu-id="23ba9-351">檢視目前註冊狀態：</span><span class="sxs-lookup"><span data-stu-id="23ba9-351">View the current registration status:</span></span>

    <span data-ttu-id="23ba9-352">![MFA 原則](./media/active-directory-identityprotection/1022.png "MFA 原則")</span><span class="sxs-lookup"><span data-stu-id="23ba9-352">![MFA policy](./media/active-directory-identityprotection/1022.png "MFA policy")</span></span>

<span data-ttu-id="23ba9-353">如需相關的使用者經驗概觀，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="23ba9-353">For an overview of the related user experience, see:</span></span>

* <span data-ttu-id="23ba9-354">[Multi-Factor Authentication 註冊流程](active-directory-identityprotection-flows.md#multi-factor-authentication-registration)。</span><span class="sxs-lookup"><span data-stu-id="23ba9-354">[Multi-factor authentication registration flow](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).</span></span>  
* <span data-ttu-id="23ba9-355">[使用 Azure AD Identity Protection 時的登入體驗](active-directory-identityprotection-flows.md)。</span><span class="sxs-lookup"><span data-stu-id="23ba9-355">[Sign-in experiences with Azure AD Identity Protection](active-directory-identityprotection-flows.md).</span></span>  

<span data-ttu-id="23ba9-356">**開啟相關的組態對話方塊**：</span><span class="sxs-lookup"><span data-stu-id="23ba9-356">**To open the related configuration dialog**:</span></span>

- <span data-ttu-id="23ba9-357">在 [Azure AD Identity Protection] 刀鋒視窗的 [設定] 區段中，按一下 [Multi-Factor Authentication 註冊]。</span><span class="sxs-lookup"><span data-stu-id="23ba9-357">On the **Azure AD Identity Protection** blade, in the **Configure** section, click **Multi-factor authentication registration**.</span></span>

    <span data-ttu-id="23ba9-358">![MFA 原則](./media/active-directory-identityprotection/1019.png "MFA 原則")</span><span class="sxs-lookup"><span data-stu-id="23ba9-358">![MFA policy](./media/active-directory-identityprotection/1019.png "MFA policy")</span></span>

## <a name="next-steps"></a><span data-ttu-id="23ba9-359">後續步驟</span><span class="sxs-lookup"><span data-stu-id="23ba9-359">Next steps</span></span>
* [<span data-ttu-id="23ba9-360">第 9 頻道：Azure AD 和身分識別展示：Identity Protection 預覽</span><span class="sxs-lookup"><span data-stu-id="23ba9-360">Channel 9: Azure AD and Identity Show: Identity Protection Preview</span></span>](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

* [<span data-ttu-id="23ba9-361">啟用 Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="23ba9-361">Enabling Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-enable.md)

* [<span data-ttu-id="23ba9-362">Azure Active Directory Identity Protection 偵測到的弱點</span><span class="sxs-lookup"><span data-stu-id="23ba9-362">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-vulnerabilities.md)

* [<span data-ttu-id="23ba9-363">Azure Active Directory 風險事件</span><span class="sxs-lookup"><span data-stu-id="23ba9-363">Azure Active Directory risk events</span></span>](active-directory-identity-protection-risk-events.md)

* [<span data-ttu-id="23ba9-364">Azure Active Directory Identity Protection 通知</span><span class="sxs-lookup"><span data-stu-id="23ba9-364">Azure Active Directory Identity Protection notifications</span></span>](active-directory-identityprotection-notifications.md)

* [<span data-ttu-id="23ba9-365">Azure Active Directory Identity Protection 腳本</span><span class="sxs-lookup"><span data-stu-id="23ba9-365">Azure Active Directory Identity Protection playbook</span></span>](active-directory-identityprotection-playbook.md)

* [<span data-ttu-id="23ba9-366">Azure Active Directory Identity Protection 詞彙</span><span class="sxs-lookup"><span data-stu-id="23ba9-366">Azure Active Directory Identity Protection glossary</span></span>](active-directory-identityprotection-glossary.md)

* [<span data-ttu-id="23ba9-367">使用 Azure AD Identity Protection 時的登入體驗</span><span class="sxs-lookup"><span data-stu-id="23ba9-367">Sign-in experiences with Azure AD Identity Protection</span></span>](active-directory-identityprotection-flows.md)

* [<span data-ttu-id="23ba9-368">Azure Active Directory Identity Protection - 如何解鎖使用者</span><span class="sxs-lookup"><span data-stu-id="23ba9-368">Azure Active Directory Identity Protection - How to unblock users</span></span>](active-directory-identityprotection-unblock-howto.md)

* [<span data-ttu-id="23ba9-369">開始使用 Azure Active Directory Identity Protection 和 Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="23ba9-369">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>](active-directory-identityprotection-graph-getting-started.md)
