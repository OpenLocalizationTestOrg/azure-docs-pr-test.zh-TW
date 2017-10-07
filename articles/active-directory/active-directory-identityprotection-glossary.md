---
title: "Active Directory Identity Protection 字彙 aaaAzure |Microsoft 文件"
description: "Azure Active Directory Identity Protection 詞彙"
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, 管理應用程式, 安全性, 風險, 風險層級, 弱點, 安全性原則, 詞彙"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 833119a5-33d6-4482-adda-fa35218c72c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: ff2e96d20e2a3f1df24b78e66be5a0c6807e60a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-glossary"></a><span data-ttu-id="47756-104">Azure Active Directory Identity Protection 詞彙</span><span class="sxs-lookup"><span data-stu-id="47756-104">Azure Active Directory Identity Protection Glossary</span></span>
### <a name="at-risk-user"></a><span data-ttu-id="47756-105">有風險 (使用者)</span><span class="sxs-lookup"><span data-stu-id="47756-105">At risk (User)</span></span>
<span data-ttu-id="47756-106">具有一或多個作用中風險事件的使用者。</span><span class="sxs-lookup"><span data-stu-id="47756-106">A user with one or more active risk events.</span></span> 

### <a name="atypical-sign-in-location"></a><span data-ttu-id="47756-107">非典型登入位置</span><span class="sxs-lookup"><span data-stu-id="47756-107">Atypical sign-in location</span></span>
<span data-ttu-id="47756-108">登入不是標準 hello 特定使用者、 類似使用者，或 hello 租用戶的地理位置。</span><span class="sxs-lookup"><span data-stu-id="47756-108">A sign-in from a geographic location that is not typical for hello specific user, similar users, or hello tenant.</span></span>

### <a name="azure-ad-identity-protection"></a><span data-ttu-id="47756-109">Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="47756-109">Azure AD Identity Protection</span></span>
<span data-ttu-id="47756-110">Azure Active Directory 的安全性模組，可供整合檢視會影響組織身分識別的風險事件和潛在弱點。</span><span class="sxs-lookup"><span data-stu-id="47756-110">A security module of Azure Active Directory that provides a consolidated view into risk events and potential vulnerabilities affecting an organization’s identities.</span></span>

### <a name="conditional-access"></a><span data-ttu-id="47756-111">條件式存取</span><span class="sxs-lookup"><span data-stu-id="47756-111">Conditional access</span></span>
<span data-ttu-id="47756-112">保護存取 tooresources 的原則。</span><span class="sxs-lookup"><span data-stu-id="47756-112">A policy for securing access tooresources.</span></span> <span data-ttu-id="47756-113">條件式存取規則儲存在 hello Azure Active Directory，而且由 Azure AD 授與存取 toohello 資源之前加以評估。</span><span class="sxs-lookup"><span data-stu-id="47756-113">Conditional access rules are stored in hello Azure Active Directory and are evaluated by Azure AD before granting access toohello resource.</span></span>  <span data-ttu-id="47756-114">範例規則包括根據使用者位置、裝置健康狀態或使用者驗證方法來限制存取。</span><span class="sxs-lookup"><span data-stu-id="47756-114">Example rules include restricting access based on user location, device health or user authentication method.</span></span>

### <a name="credentials"></a><span data-ttu-id="47756-115">認證</span><span class="sxs-lookup"><span data-stu-id="47756-115">Credentials</span></span>
<span data-ttu-id="47756-116">包含之識別與已使用的 toogain 存取 toolocal 和網路資源的識別證明的資訊。</span><span class="sxs-lookup"><span data-stu-id="47756-116">Information that includes identification and proof of identification that is used toogain access toolocal and network resources.</span></span> <span data-ttu-id="47756-117">認證範例包括使用者名稱和密碼、智慧卡和憑證。</span><span class="sxs-lookup"><span data-stu-id="47756-117">Examples of credentials are user names and passwords, smart cards, and certificates.</span></span>

### <a name="event"></a><span data-ttu-id="47756-118">Event</span><span class="sxs-lookup"><span data-stu-id="47756-118">Event</span></span>
<span data-ttu-id="47756-119">Azure Active Directory 中的活動記錄。</span><span class="sxs-lookup"><span data-stu-id="47756-119">A record of an activity in Azure Active Directory.</span></span>

### <a name="false-positive-risk-event"></a><span data-ttu-id="47756-120">誤判 (風險事件)</span><span class="sxs-lookup"><span data-stu-id="47756-120">False-positive (risk event)</span></span>
<span data-ttu-id="47756-121">手動設定識別身分保護使用者，表示該 hello 風險事件已調查和不正確地標示為風險事件的風險事件狀態。</span><span class="sxs-lookup"><span data-stu-id="47756-121">A risk event status set manually by an Identity Protection user, indicating that hello risk event was investigated and was incorrectly flagged as a risk event.</span></span>

### <a name="identity"></a><span data-ttu-id="47756-122">身分識別</span><span class="sxs-lookup"><span data-stu-id="47756-122">Identity</span></span>
<span data-ttu-id="47756-123">必須透過以密碼或憑證等準則為基礎的驗證作業來確認的個人或實體。</span><span class="sxs-lookup"><span data-stu-id="47756-123">A person or entity that must be verified by means of authentication, based on criteria such as password or a certificate.</span></span>

### <a name="identity-risk-event"></a><span data-ttu-id="47756-124">身分識別風險事件</span><span class="sxs-lookup"><span data-stu-id="47756-124">Identity risk event</span></span>
<span data-ttu-id="47756-125">由 Identity Protection 標示為異常的 AAD 事件，有可能表示身分識別已被入侵。</span><span class="sxs-lookup"><span data-stu-id="47756-125">AAD event that was flagged as anomalous by Identity Protection, and may indicate that an identity has been compromised.</span></span>

### <a name="ignored-risk-event"></a><span data-ttu-id="47756-126">已忽略 (風險事件)</span><span class="sxs-lookup"><span data-stu-id="47756-126">Ignored (risk event)</span></span>
<span data-ttu-id="47756-127">手動設定識別身分保護使用者，指出該 hello 風險事件已關閉但不採取補救動作的風險事件狀態。</span><span class="sxs-lookup"><span data-stu-id="47756-127">A risk event status set manually by an Identity Protection user, indicating that hello risk event is closed without taking a remediation action.</span></span>

### <a name="impossible-travel-from-atypical-locations"></a><span data-ttu-id="47756-128">不可能來自非典型位置的移動</span><span class="sxs-lookup"><span data-stu-id="47756-128">Impossible travel from atypical locations</span></span>
<span data-ttu-id="47756-129">周遊這些之間的風險事件觸發時需要 toophysically 兩個相同的使用者會偵測到，其中至少一個是從非典型的登入位置，以及在 hello hello 登入之間的時間長度小於最小的 hello 時間的 hello 登入。位置。</span><span class="sxs-lookup"><span data-stu-id="47756-129">A risk event triggered when two sign-ins for hello same user are detected, where at least one of them is from an atypical sign-in location, and where hello time between hello sign-ins is shorter than hello minimum time it would take toophysically travel between these locations.</span></span>  

### <a name="investigation"></a><span data-ttu-id="47756-130">調查</span><span class="sxs-lookup"><span data-stu-id="47756-130">Investigation</span></span>
<span data-ttu-id="47756-131">hello 檢閱 hello 活動、 記錄和其他相關資訊的程序相關 tooa 風險事件 toodecide 是否補救或安全防護功能步驟，了解如何 hello 身分識別已遭到洩露，並了解如何 hello使用遭盜用身分識別。</span><span class="sxs-lookup"><span data-stu-id="47756-131">hello process of reviewing hello activities, logs, and other relevant information related tooa risk event toodecide whether remediation or mitigation steps are necessary, understand if and how hello identity was compromised, and understand how hello compromised identity was used.</span></span>

### <a name="leaked-credentials"></a><span data-ttu-id="47756-132">認證外洩</span><span class="sxs-lookup"><span data-stu-id="47756-132">Leaked credentials</span></span>
<span data-ttu-id="47756-133">風險事件觸發時發現目前的使用者認證 （使用者名稱和密碼） 公開公佈在我們的研究人員 hello 深色 web。</span><span class="sxs-lookup"><span data-stu-id="47756-133">A risk event triggered when current user credentials (user name and password) are found posted publicly in hello Dark   web by our researchers.</span></span>

### <a name="mitigation"></a><span data-ttu-id="47756-134">緩和</span><span class="sxs-lookup"><span data-stu-id="47756-134">Mitigation</span></span>
<span data-ttu-id="47756-135">動作 toolimit 或消除 hello 的攻擊者 tooexploit 遭盜用身分識別或裝置的能力，而不還原 hello 身分識別或裝置 tooa 安全狀態。</span><span class="sxs-lookup"><span data-stu-id="47756-135">An action toolimit or eliminate hello ability of an attacker tooexploit a compromised identity or device without restoring hello identity or device tooa safe state.</span></span> <span data-ttu-id="47756-136">緩和措施無法解決先前 hello 身分識別或裝置相關聯的風險事件。</span><span class="sxs-lookup"><span data-stu-id="47756-136">A mitigation does not resolve previous risk events associated with hello identity or device.</span></span>

### <a name="multi-factor-authentication"></a><span data-ttu-id="47756-137">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="47756-137">Multi-factor authentication</span></span>
<span data-ttu-id="47756-138">驗證方法，需要兩個或多個驗證方法，其可能包括 hello 使用者擁有的項目，這類憑證;項目 hello 使用者知道，例如使用者名稱、 密碼或複雜密碼。實體的屬性，例如指紋。與個人的屬性，例如個人簽章。</span><span class="sxs-lookup"><span data-stu-id="47756-138">An authentication method that requires two or more authentication methods, which may include something hello user has, such a certificate; something hello user knows, such as user names, passwords, or pass phrases; physical attributes, such as a thumbprint; and personal attributes, such as a personal signature.</span></span>

### <a name="offline-detection"></a><span data-ttu-id="47756-139">離線偵測</span><span class="sxs-lookup"><span data-stu-id="47756-139">Offline detection</span></span>
<span data-ttu-id="47756-140">hello 偵測異常和 hello 事實，已發生的事件之後的事件，例如登入嘗試的 hello 風險評估。</span><span class="sxs-lookup"><span data-stu-id="47756-140">hello detection of anomalies and evaluation of hello risk of an event such as sign-in attempt after hello fact, for an event that has already happened.</span></span>

### <a name="policy-condition"></a><span data-ttu-id="47756-141">原則條件</span><span class="sxs-lookup"><span data-stu-id="47756-141">Policy condition</span></span>
<span data-ttu-id="47756-142">安全性原則會定義 hello 實體群組、 使用者、 應用程式、 裝置平台，裝置狀態、 IP 範圍 （用戶端類型） 從它 hello 原則中包含或排除的一部分。</span><span class="sxs-lookup"><span data-stu-id="47756-142">A part of a security policy which defines hello entities (groups, users, apps, device platforms, Device states, IP ranges, client types) included in hello policy or excluded from it.</span></span>

### <a name="policy-rule"></a><span data-ttu-id="47756-143">原則規則</span><span class="sxs-lookup"><span data-stu-id="47756-143">Policy rule</span></span>
<span data-ttu-id="47756-144">hello 部分說明 hello 情況會觸發 hello 原則以及 hello 所採取動作時，就會觸發 hello 原則的安全性原則。</span><span class="sxs-lookup"><span data-stu-id="47756-144">hello part of a security policy which describes hello circumstances that would trigger hello policy, and hello actions taken when hello policy is triggered.</span></span>

### <a name="prevention"></a><span data-ttu-id="47756-145">預防</span><span class="sxs-lookup"><span data-stu-id="47756-145">Prevention</span></span>
<span data-ttu-id="47756-146">動作 tooprevent 損害 toohello 透過濫用的組織的身分識別或裝置懷疑，或者知道 toobe 入侵。</span><span class="sxs-lookup"><span data-stu-id="47756-146">An action tooprevent damage toohello organization through abuse of an identity or device suspected or know toobe compromised.</span></span> <span data-ttu-id="47756-147">防止動作不保護 hello 裝置或識別，並無法解決先前的風險事件。</span><span class="sxs-lookup"><span data-stu-id="47756-147">A prevention action does not secure hello device or identity, and does not resolve previous risk events.</span></span>

### <a name="privileged-user"></a><span data-ttu-id="47756-148">特殊權限 (使用者)</span><span class="sxs-lookup"><span data-stu-id="47756-148">Privileged (user)</span></span>
<span data-ttu-id="47756-149">在 Azure Active Directory，例如為全域管理員，具有永久或暫時的系統管理員權限 tooone 或更多資源的 hello 的風險事件期間，在使用者計費管理員、 服務系統管理員、 使用者管理員和密碼系統管理員。</span><span class="sxs-lookup"><span data-stu-id="47756-149">A user that at hello time of a risk event, had permanent or temporary admin permissions tooone or more resource in Azure Active Directory, such as a Global Administrator, Billing Administrator, Service Administrator, User administrator, and Password Administrator.</span></span> 

### <a name="real-time"></a><span data-ttu-id="47756-150">即時</span><span class="sxs-lookup"><span data-stu-id="47756-150">Real-time</span></span>
<span data-ttu-id="47756-151">請參閱即時偵測。</span><span class="sxs-lookup"><span data-stu-id="47756-151">See Real-time detection.</span></span>

### <a name="real-time-detection"></a><span data-ttu-id="47756-152">即時偵測</span><span class="sxs-lookup"><span data-stu-id="47756-152">Real-time detection</span></span>
<span data-ttu-id="47756-153">hello 異常偵測的事件，例如登入嘗試 hello 事件之前的 hello 風險評估允許和 tooproceed。</span><span class="sxs-lookup"><span data-stu-id="47756-153">hello detection of anomalies and evaluation of hello risk of an event such as sign-in attempt before hello event is allowed tooproceed.</span></span>

### <a name="remediated-risk-event"></a><span data-ttu-id="47756-154">已補救 (風險事件)</span><span class="sxs-lookup"><span data-stu-id="47756-154">Remediated (risk event)</span></span>
<span data-ttu-id="47756-155">自動設定的識別身分保護，指出該 hello 風險事件補救這種類型的風險事件使用 hello 標準的補救動作的風險事件狀態。</span><span class="sxs-lookup"><span data-stu-id="47756-155">A risk event status set automatically by Identity Protection, indicating that hello risk event was remediated using hello standard remediation action for this type of risk event.</span></span> <span data-ttu-id="47756-156">例如，當 hello 使用者密碼重設時，許多指示該 hello 先前的密碼已遭到洩露的風險事件都會自動補救。</span><span class="sxs-lookup"><span data-stu-id="47756-156">For example, when hello user password is reset, many risk events that indicate that hello previous password was compromised are automatically remediated.</span></span>

### <a name="remediation"></a><span data-ttu-id="47756-157">補救</span><span class="sxs-lookup"><span data-stu-id="47756-157">Remediation</span></span>
<span data-ttu-id="47756-158">動作 toosecure 身分識別或先前可疑或已知 toobe 的裝置遭到洩露。</span><span class="sxs-lookup"><span data-stu-id="47756-158">An action toosecure an identity or a device that were previously suspected or known toobe compromised.</span></span> <span data-ttu-id="47756-159">補救動作還原 hello 身分識別或裝置 tooa 安全的狀態，並解決先前 hello 身分識別或裝置相關聯的風險事件。</span><span class="sxs-lookup"><span data-stu-id="47756-159">A remediation action restores hello identity or device tooa safe state, and resolves previous risk events associated with hello identity or device.</span></span>

### <a name="resolved-risk-event"></a><span data-ttu-id="47756-160">已解決 (風險事件)</span><span class="sxs-lookup"><span data-stu-id="47756-160">Resolved (risk event)</span></span>
<span data-ttu-id="47756-161">手動設定識別身分保護使用者，表示 hello 使用者採取適當的補救動作以外的識別身分保護，且該 hello 風險事件應該被視為風險事件狀態已關閉。</span><span class="sxs-lookup"><span data-stu-id="47756-161">A risk event status set manually by an Identity Protection user, indicating that hello user took an appropriate remediation action outside Identity Protection, and that hello risk event should be considered closed.</span></span>

### <a name="risk-event-status"></a><span data-ttu-id="47756-162">風險事件狀態</span><span class="sxs-lookup"><span data-stu-id="47756-162">Risk event status</span></span>
<span data-ttu-id="47756-163">風險事件屬性，指出是否 hello 事件為作用中，而且如果已關閉，關閉它 hello 原因。</span><span class="sxs-lookup"><span data-stu-id="47756-163">A property of a risk event, indicating whether hello event is active, and if closed, hello reason for closing it.</span></span>

### <a name="risk-event-type"></a><span data-ttu-id="47756-164">風險事件類型</span><span class="sxs-lookup"><span data-stu-id="47756-164">Risk event type</span></span>
<span data-ttu-id="47756-165">某項分類 hello 的風險事件，指出造成 hello 事件 toobe 視為危險的異常 hello 型別。</span><span class="sxs-lookup"><span data-stu-id="47756-165">A category for hello risk event, indicating hello type of anomaly that caused hello event toobe considered risky.</span></span>

### <a name="risk-level-risk-event"></a><span data-ttu-id="47756-166">風險層級 (風險事件)</span><span class="sxs-lookup"><span data-stu-id="47756-166">Risk level (risk event)</span></span>
<span data-ttu-id="47756-167">（高、 中或低） 它們的相對值指示 hello 風險事件 toohelp 識別身分保護使用者 hello 嚴重性排定優先順序採取 tooreduce hello 風險 tootheir 組織 hello 動作。</span><span class="sxs-lookup"><span data-stu-id="47756-167">An indication (High, Medium, or Low) of hello severity of hello risk event toohelp Identity Protection users prioritize hello actions they take tooreduce hello risk tootheir organization.</span></span> 

### <a name="risk-level-sign-in"></a><span data-ttu-id="47756-168">風險層級 (登入)</span><span class="sxs-lookup"><span data-stu-id="47756-168">Risk level (sign-in)</span></span>
<span data-ttu-id="47756-169">表示 （高、 中或低） hello 可能性特定登入，其他人正在嘗試 toouse hello 使用者的身分識別。</span><span class="sxs-lookup"><span data-stu-id="47756-169">An indication (High, Medium, or Low) of hello likelihood that for a specific sign-in, someone else is attempting toouse hello user’s identity.</span></span>

### <a name="risk-level-user-compromise"></a><span data-ttu-id="47756-170">風險層級 (使用者入侵)</span><span class="sxs-lookup"><span data-stu-id="47756-170">Risk level (user compromise)</span></span>
<span data-ttu-id="47756-171">Hello 身分識別已遭洩漏的可能性表示 （高、 中或低）。</span><span class="sxs-lookup"><span data-stu-id="47756-171">An indication (High, Medium, or Low) of hello likelihood that an identity has been compromised.</span></span>

### <a name="risk-level-vulnerability"></a><span data-ttu-id="47756-172">風險層級 (弱點)</span><span class="sxs-lookup"><span data-stu-id="47756-172">Risk level (vulnerability)</span></span>
<span data-ttu-id="47756-173">（高、 中或低） 它們的相對值指示 hello 弱點 toohelp 識別身分保護使用者 hello 嚴重性排定優先順序採取 tooreduce hello 風險 tootheir 組織 hello 動作。</span><span class="sxs-lookup"><span data-stu-id="47756-173">An indication (High, Medium, or Low) of hello severity of hello vulnerability toohelp Identity Protection users prioritize hello actions they take tooreduce hello risk tootheir organization.</span></span>

### <a name="secure-identity"></a><span data-ttu-id="47756-174">安全 (身分識別)</span><span class="sxs-lookup"><span data-stu-id="47756-174">Secure (identity)</span></span>
<span data-ttu-id="47756-175">採取補救動作，例如密碼變更或重新安裝映像 toorestore 潛在受危害的身分識別 tooan 洩露的狀態機器。</span><span class="sxs-lookup"><span data-stu-id="47756-175">Take remediation action such as a password change or machine reimaging toorestore a potentially compromised identity tooan uncompromised state.</span></span>

### <a name="security-policy"></a><span data-ttu-id="47756-176">安全性原則</span><span class="sxs-lookup"><span data-stu-id="47756-176">Security policy</span></span>
<span data-ttu-id="47756-177">原則規則和條件的集合。</span><span class="sxs-lookup"><span data-stu-id="47756-177">A collection of policy rules and condition.</span></span> <span data-ttu-id="47756-178">原則可以套用的 tooentities 像是使用者、 群組、 應用程式、 裝置、 裝置平台，裝置狀態、 IP 範圍，以及 Auth2.0 用戶端類型。</span><span class="sxs-lookup"><span data-stu-id="47756-178">A policy can be applied tooentities such as users, groups, apps, devices, device platforms, device states, IP ranges, and Auth2.0 client types.</span></span> <span data-ttu-id="47756-179">啟用原則時，它會評估每次發出資源的語彙基元 hello 原則中所包含的實體時。</span><span class="sxs-lookup"><span data-stu-id="47756-179">When a policy is enabled, it is evaluated whenever an entity included in hello policy is issued a token for a resource.</span></span>

### <a name="sign-in-v"></a><span data-ttu-id="47756-180">登入 (動詞)</span><span class="sxs-lookup"><span data-stu-id="47756-180">Sign in (v)</span></span>
<span data-ttu-id="47756-181">在 Azure Active Directory tooauthenticate tooan 身分識別。</span><span class="sxs-lookup"><span data-stu-id="47756-181">tooauthenticate tooan identity in Azure Active Directory.</span></span>

### <a name="sign-in-n"></a><span data-ttu-id="47756-182">登入 (名詞)</span><span class="sxs-lookup"><span data-stu-id="47756-182">Sign-in (n)</span></span>
<span data-ttu-id="47756-183">hello 程序或驗證 Azure Active Directory 和擷取這項作業的 hello 事件中的身分識別的動作。</span><span class="sxs-lookup"><span data-stu-id="47756-183">hello process or action of authenticating an identity in Azure Active Directory, and hello event that captures this operation.</span></span>

### <a name="sign-in-from-anonymous-ip-address"></a><span data-ttu-id="47756-184">從匿名 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="47756-184">Sign-in from anonymous IP address</span></span>
<span data-ttu-id="47756-185">從被視為匿名 Proxy IP 位址的 IP 位址成功登入之後所觸發的風險事件。</span><span class="sxs-lookup"><span data-stu-id="47756-185">A risk event triggered after a successful sign-in from IP address that has been identified as an anonymous proxy IP address.</span></span>

### <a name="sign-in-from-infected-device"></a><span data-ttu-id="47756-186">從受感染的裝置登入</span><span class="sxs-lookup"><span data-stu-id="47756-186">Sign-in from infected device</span></span>
<span data-ttu-id="47756-187">風險事件觸發時登入來自已知 toobe 裝置所使用一或多個遭入侵，主動嘗試 toocommunicate bot 伺服器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="47756-187">A risk event triggered when a sign-in originates from an IP address which is known toobe used by one or more compromised devices, which are actively attempting toocommunicate with a bot server.</span></span>

### <a name="sign-in-from-ip-address-with-suspicious-activity"></a><span data-ttu-id="47756-188">從具有可疑活動的 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="47756-188">Sign-in from IP address with suspicious activity</span></span>
<span data-ttu-id="47756-189">從短期內透過多個使用者帳戶多次嘗試登入失敗的 IP 位址成功登入之後所觸發的風險事件。</span><span class="sxs-lookup"><span data-stu-id="47756-189">A risk event triggered after a successful sign-in from an IP address with a high number of failed login attempts across multiple user accounts over a short period of time.</span></span>

### <a name="sign-in-from-unfamiliar-location"></a><span data-ttu-id="47756-190">從不熟悉的位置登入</span><span class="sxs-lookup"><span data-stu-id="47756-190">Sign-in from unfamiliar location</span></span>
<span data-ttu-id="47756-191">當使用者從新的位置 (IP、經緯度和 ASN) 成功登入時所觸發的風險事件。</span><span class="sxs-lookup"><span data-stu-id="47756-191">A risk event triggered when a user successfully signs in from a new location (IP, Latitude/Longitude and ASN).</span></span>

### <a name="sign-in-risk"></a><span data-ttu-id="47756-192">登入風險</span><span class="sxs-lookup"><span data-stu-id="47756-192">Sign-in risk</span></span>
<span data-ttu-id="47756-193">請參閱風險層級 (登入)</span><span class="sxs-lookup"><span data-stu-id="47756-193">See Risk level (sign-in)</span></span>

### <a name="sign-in-risk-policy"></a><span data-ttu-id="47756-194">登入風險原則</span><span class="sxs-lookup"><span data-stu-id="47756-194">Sign-in risk policy</span></span>
<span data-ttu-id="47756-195">條件式存取原則，評估 hello 風險 tooa 特定登入，並根據預先定義的條件和規則的防護措施。</span><span class="sxs-lookup"><span data-stu-id="47756-195">A conditional access policy that evaluates hello risk tooa specific sign-in and applies mitigations based on predefined conditions and rules.</span></span>

### <a name="user-compromise-risk"></a><span data-ttu-id="47756-196">使用者入侵風險</span><span class="sxs-lookup"><span data-stu-id="47756-196">User compromise risk</span></span>
<span data-ttu-id="47756-197">請參閱風險層級 (使用者入侵)</span><span class="sxs-lookup"><span data-stu-id="47756-197">See Risk level (user compromise)</span></span>

### <a name="user-risk"></a><span data-ttu-id="47756-198">使用者風險</span><span class="sxs-lookup"><span data-stu-id="47756-198">User risk</span></span>
<span data-ttu-id="47756-199">請參閱風險層級 (使用者入侵)。</span><span class="sxs-lookup"><span data-stu-id="47756-199">See Risk level (user compromise).</span></span>

### <a name="user-risk-policy"></a><span data-ttu-id="47756-200">使用者風險原則</span><span class="sxs-lookup"><span data-stu-id="47756-200">User risk policy</span></span>
<span data-ttu-id="47756-201">條件式存取原則，會考慮 hello 登入，並根據預先定義的條件和規則的防護措施。</span><span class="sxs-lookup"><span data-stu-id="47756-201">A conditional access policy that considers hello sign-in and applies mitigations based on predefined conditions and rules.</span></span>

### <a name="users-flagged-for-risk"></a><span data-ttu-id="47756-202">標示有風險的使用者</span><span class="sxs-lookup"><span data-stu-id="47756-202">Users flagged for risk</span></span>
<span data-ttu-id="47756-203">具有作用中或已補救之風險事件的使用者</span><span class="sxs-lookup"><span data-stu-id="47756-203">Users that have risk events which are either active or remediated</span></span>

### <a name="vulnerability"></a><span data-ttu-id="47756-204">弱點</span><span class="sxs-lookup"><span data-stu-id="47756-204">Vulnerability</span></span>
<span data-ttu-id="47756-205">設定或讓 hello 目錄很容易遭受 tooexploits 或潛在威脅的 Azure Active Directory 中的條件。</span><span class="sxs-lookup"><span data-stu-id="47756-205">A configuration or condition in Azure Active Directory which makes hello directory susceptible tooexploits or threats.</span></span>

## <a name="see-also"></a><span data-ttu-id="47756-206">另請參閱</span><span class="sxs-lookup"><span data-stu-id="47756-206">See also</span></span>
* [<span data-ttu-id="47756-207">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="47756-207">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

