---
title: "Azure Active Directory Identity Protection 詞彙 | Microsoft Docs"
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
ms.openlocfilehash: 2cf64925cff9a78cf83532a1cfd231f7a1d98304
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-identity-protection-glossary"></a><span data-ttu-id="315ad-104">Azure Active Directory Identity Protection 詞彙</span><span class="sxs-lookup"><span data-stu-id="315ad-104">Azure Active Directory Identity Protection Glossary</span></span>
### <a name="at-risk-user"></a><span data-ttu-id="315ad-105">有風險 (使用者)</span><span class="sxs-lookup"><span data-stu-id="315ad-105">At risk (User)</span></span>
<span data-ttu-id="315ad-106">具有一或多個作用中風險事件的使用者。</span><span class="sxs-lookup"><span data-stu-id="315ad-106">A user with one or more active risk events.</span></span> 

### <a name="atypical-sign-in-location"></a><span data-ttu-id="315ad-107">非典型登入位置</span><span class="sxs-lookup"><span data-stu-id="315ad-107">Atypical sign-in location</span></span>
<span data-ttu-id="315ad-108">從特定使用者、類似使用者或租用戶不常用的地理位置登入。</span><span class="sxs-lookup"><span data-stu-id="315ad-108">A sign-in from a geographic location that is not typical for the specific user, similar users, or the tenant.</span></span>

### <a name="azure-ad-identity-protection"></a><span data-ttu-id="315ad-109">Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="315ad-109">Azure AD Identity Protection</span></span>
<span data-ttu-id="315ad-110">Azure Active Directory 的安全性模組，可供整合檢視會影響組織身分識別的風險事件和潛在弱點。</span><span class="sxs-lookup"><span data-stu-id="315ad-110">A security module of Azure Active Directory that provides a consolidated view into risk events and potential vulnerabilities affecting an organization’s identities.</span></span>

### <a name="conditional-access"></a><span data-ttu-id="315ad-111">條件式存取</span><span class="sxs-lookup"><span data-stu-id="315ad-111">Conditional access</span></span>
<span data-ttu-id="315ad-112">用來保護資源存取的原則。</span><span class="sxs-lookup"><span data-stu-id="315ad-112">A policy for securing access to resources.</span></span> <span data-ttu-id="315ad-113">條件式存取規則會儲存在 Azure Active Directory 中，並在授與資源的存取權之前由 Azure AD 評估。</span><span class="sxs-lookup"><span data-stu-id="315ad-113">Conditional access rules are stored in the Azure Active Directory and are evaluated by Azure AD before granting access to the resource.</span></span>  <span data-ttu-id="315ad-114">範例規則包括根據使用者位置、裝置健康狀態或使用者驗證方法來限制存取。</span><span class="sxs-lookup"><span data-stu-id="315ad-114">Example rules include restricting access based on user location, device health or user authentication method.</span></span>

### <a name="credentials"></a><span data-ttu-id="315ad-115">認證</span><span class="sxs-lookup"><span data-stu-id="315ad-115">Credentials</span></span>
<span data-ttu-id="315ad-116">包含識別碼以及用來取得存取本機和網路資源之識別證明的資訊。</span><span class="sxs-lookup"><span data-stu-id="315ad-116">Information that includes identification and proof of identification that is used to gain access to local and network resources.</span></span> <span data-ttu-id="315ad-117">認證範例包括使用者名稱和密碼、智慧卡和憑證。</span><span class="sxs-lookup"><span data-stu-id="315ad-117">Examples of credentials are user names and passwords, smart cards, and certificates.</span></span>

### <a name="event"></a><span data-ttu-id="315ad-118">Event</span><span class="sxs-lookup"><span data-stu-id="315ad-118">Event</span></span>
<span data-ttu-id="315ad-119">Azure Active Directory 中的活動記錄。</span><span class="sxs-lookup"><span data-stu-id="315ad-119">A record of an activity in Azure Active Directory.</span></span>

### <a name="false-positive-risk-event"></a><span data-ttu-id="315ad-120">誤判 (風險事件)</span><span class="sxs-lookup"><span data-stu-id="315ad-120">False-positive (risk event)</span></span>
<span data-ttu-id="315ad-121">由 Identity Protection 使用者手動設定的風險事件狀態，表示此風險事件已經過調查而且被誤標為風險事件。</span><span class="sxs-lookup"><span data-stu-id="315ad-121">A risk event status set manually by an Identity Protection user, indicating that the risk event was investigated and was incorrectly flagged as a risk event.</span></span>

### <a name="identity"></a><span data-ttu-id="315ad-122">身分識別</span><span class="sxs-lookup"><span data-stu-id="315ad-122">Identity</span></span>
<span data-ttu-id="315ad-123">必須透過以密碼或憑證等準則為基礎的驗證作業來確認的個人或實體。</span><span class="sxs-lookup"><span data-stu-id="315ad-123">A person or entity that must be verified by means of authentication, based on criteria such as password or a certificate.</span></span>

### <a name="identity-risk-event"></a><span data-ttu-id="315ad-124">身分識別風險事件</span><span class="sxs-lookup"><span data-stu-id="315ad-124">Identity risk event</span></span>
<span data-ttu-id="315ad-125">由 Identity Protection 標示為異常的 AAD 事件，有可能表示身分識別已被入侵。</span><span class="sxs-lookup"><span data-stu-id="315ad-125">AAD event that was flagged as anomalous by Identity Protection, and may indicate that an identity has been compromised.</span></span>

### <a name="ignored-risk-event"></a><span data-ttu-id="315ad-126">已忽略 (風險事件)</span><span class="sxs-lookup"><span data-stu-id="315ad-126">Ignored (risk event)</span></span>
<span data-ttu-id="315ad-127">由 Identity Protection 使用者手動設定的風險事件狀態，表示此風險事件已關閉，而不需採取補救動作。</span><span class="sxs-lookup"><span data-stu-id="315ad-127">A risk event status set manually by an Identity Protection user, indicating that the risk event is closed without taking a remediation action.</span></span>

### <a name="impossible-travel-from-atypical-locations"></a><span data-ttu-id="315ad-128">不可能來自非典型位置的移動</span><span class="sxs-lookup"><span data-stu-id="315ad-128">Impossible travel from atypical locations</span></span>
<span data-ttu-id="315ad-129">偵測到同一位使用者有兩次登入時所觸發的風險事件，其中至少一次登入是來自非典型登入位置，而且登入之間的時間比在兩地之間實際移動所需的最短時間還要短。</span><span class="sxs-lookup"><span data-stu-id="315ad-129">A risk event triggered when two sign-ins for the same user are detected, where at least one of them is from an atypical sign-in location, and where the time between the sign-ins is shorter than the minimum time it would take to physically travel between these locations.</span></span>  

### <a name="investigation"></a><span data-ttu-id="315ad-130">調查</span><span class="sxs-lookup"><span data-stu-id="315ad-130">Investigation</span></span>
<span data-ttu-id="315ad-131">檢閱風險事件相關活動、記錄檔和其他相關資訊的程序，以決定是否需要採取補救或緩和步驟，了解身分識別是否及如何遭到入侵，以及了解遭到入侵的身分識別如何被利用。</span><span class="sxs-lookup"><span data-stu-id="315ad-131">The process of reviewing the activities, logs, and other relevant information related to a risk event to decide whether remediation or mitigation steps are necessary, understand if and how the identity was compromised, and understand how the compromised identity was used.</span></span>

### <a name="leaked-credentials"></a><span data-ttu-id="315ad-132">認證外洩</span><span class="sxs-lookup"><span data-stu-id="315ad-132">Leaked credentials</span></span>
<span data-ttu-id="315ad-133">當我們的研究人員發現目前的使用者認證 (使用者名稱和密碼) 被公開張貼在黑暗網路 (Dark Web) 中時所觸發的風險事件。</span><span class="sxs-lookup"><span data-stu-id="315ad-133">A risk event triggered when current user credentials (user name and password) are found posted publicly in the Dark   web by our researchers.</span></span>

### <a name="mitigation"></a><span data-ttu-id="315ad-134">緩和</span><span class="sxs-lookup"><span data-stu-id="315ad-134">Mitigation</span></span>
<span data-ttu-id="315ad-135">此動作可限制或消除攻擊者利用遭到入侵的身分識別或裝置的能力，但不需將身分識別或裝置還原至安全的狀態。</span><span class="sxs-lookup"><span data-stu-id="315ad-135">An action to limit or eliminate the ability of an attacker to exploit a compromised identity or device without restoring the identity or device to a safe state.</span></span> <span data-ttu-id="315ad-136">緩和並未解決先前與身分識別或裝置相關聯的風險事件。</span><span class="sxs-lookup"><span data-stu-id="315ad-136">A mitigation does not resolve previous risk events associated with the identity or device.</span></span>

### <a name="multi-factor-authentication"></a><span data-ttu-id="315ad-137">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="315ad-137">Multi-factor authentication</span></span>
<span data-ttu-id="315ad-138">此種驗證方法需要兩個或更多驗證方法，其中可能包含使用者擁有的事物 (例如憑證)、使用者知道的事物 (例如使用者名稱、密碼或通關密語)、實體屬性 (例如指紋) 以及個人屬性 (例如個人簽章)。</span><span class="sxs-lookup"><span data-stu-id="315ad-138">An authentication method that requires two or more authentication methods, which may include something the user has, such a certificate; something the user knows, such as user names, passwords, or pass phrases; physical attributes, such as a thumbprint; and personal attributes, such as a personal signature.</span></span>

### <a name="offline-detection"></a><span data-ttu-id="315ad-139">離線偵測</span><span class="sxs-lookup"><span data-stu-id="315ad-139">Offline detection</span></span>
<span data-ttu-id="315ad-140">針對已經發生的事件，偵測異常狀況及評估事件的風險 (例如事後的登入嘗試)。</span><span class="sxs-lookup"><span data-stu-id="315ad-140">The detection of anomalies and evaluation of the risk of an event such as sign-in attempt after the fact, for an event that has already happened.</span></span>

### <a name="policy-condition"></a><span data-ttu-id="315ad-141">原則條件</span><span class="sxs-lookup"><span data-stu-id="315ad-141">Policy condition</span></span>
<span data-ttu-id="315ad-142">安全性原則的一部分，定義原則中包含或排除的實體 (群組、使用者、應用程式、裝置平台、裝置狀態、IP 範圍、用戶端類型)。</span><span class="sxs-lookup"><span data-stu-id="315ad-142">A part of a security policy which defines the entities (groups, users, apps, device platforms, Device states, IP ranges, client types) included in the policy or excluded from it.</span></span>

### <a name="policy-rule"></a><span data-ttu-id="315ad-143">原則規則</span><span class="sxs-lookup"><span data-stu-id="315ad-143">Policy rule</span></span>
<span data-ttu-id="315ad-144">安全性原則的一部分，說明會觸發此原則的情況，以及原則觸發時所採取的動作。</span><span class="sxs-lookup"><span data-stu-id="315ad-144">The part of a security policy which describes the circumstances that would trigger the policy, and the actions taken when the policy is triggered.</span></span>

### <a name="prevention"></a><span data-ttu-id="315ad-145">預防</span><span class="sxs-lookup"><span data-stu-id="315ad-145">Prevention</span></span>
<span data-ttu-id="315ad-146">預防藉由不當使用疑似或已知遭到入侵的身分識別或裝置來傷害組織的動作。</span><span class="sxs-lookup"><span data-stu-id="315ad-146">An action to prevent damage to the organization through abuse of an identity or device suspected or know to be compromised.</span></span> <span data-ttu-id="315ad-147">預防動作並不會保護裝置或身分識別的安全，且不會解決先前的風險事件。</span><span class="sxs-lookup"><span data-stu-id="315ad-147">A prevention action does not secure the device or identity, and does not resolve previous risk events.</span></span>

### <a name="privileged-user"></a><span data-ttu-id="315ad-148">特殊權限 (使用者)</span><span class="sxs-lookup"><span data-stu-id="315ad-148">Privileged (user)</span></span>
<span data-ttu-id="315ad-149">在發生風險事件時，擁有永久或暫時系統管理權限可存取 Azure Active Directory 中一或多項資源的使用者，例如全域管理員，計費管理員、服務管理員、使用者管理員和密碼管理員。</span><span class="sxs-lookup"><span data-stu-id="315ad-149">A user that at the time of a risk event, had permanent or temporary admin permissions to one or more resource in Azure Active Directory, such as a Global Administrator, Billing Administrator, Service Administrator, User administrator, and Password Administrator.</span></span> 

### <a name="real-time"></a><span data-ttu-id="315ad-150">即時</span><span class="sxs-lookup"><span data-stu-id="315ad-150">Real-time</span></span>
<span data-ttu-id="315ad-151">請參閱即時偵測。</span><span class="sxs-lookup"><span data-stu-id="315ad-151">See Real-time detection.</span></span>

### <a name="real-time-detection"></a><span data-ttu-id="315ad-152">即時偵測</span><span class="sxs-lookup"><span data-stu-id="315ad-152">Real-time detection</span></span>
<span data-ttu-id="315ad-153">在允許事件繼續進行之前，偵測異常狀況及評估事件的風險 (例如登入嘗試)。</span><span class="sxs-lookup"><span data-stu-id="315ad-153">The detection of anomalies and evaluation of the risk of an event such as sign-in attempt before the event is allowed to proceed.</span></span>

### <a name="remediated-risk-event"></a><span data-ttu-id="315ad-154">已補救 (風險事件)</span><span class="sxs-lookup"><span data-stu-id="315ad-154">Remediated (risk event)</span></span>
<span data-ttu-id="315ad-155">Identity Protection 自動設定的風險事件狀態，表示已使用此風險事件類型的標準補救動作來補救此風險事件。</span><span class="sxs-lookup"><span data-stu-id="315ad-155">A risk event status set automatically by Identity Protection, indicating that the risk event was remediated using the standard remediation action for this type of risk event.</span></span> <span data-ttu-id="315ad-156">例如，當使用者密碼重設時，會自動補救許多指出先前密碼已遭入侵的風險事件。</span><span class="sxs-lookup"><span data-stu-id="315ad-156">For example, when the user password is reset, many risk events that indicate that the previous password was compromised are automatically remediated.</span></span>

### <a name="remediation"></a><span data-ttu-id="315ad-157">補救</span><span class="sxs-lookup"><span data-stu-id="315ad-157">Remediation</span></span>
<span data-ttu-id="315ad-158">用來保護先前疑似或已知遭到入侵的身分識別或裝置的動作。</span><span class="sxs-lookup"><span data-stu-id="315ad-158">An action to secure an identity or a device that were previously suspected or known to be compromised.</span></span> <span data-ttu-id="315ad-159">補救動作可讓身分識別或裝置還原到安全的狀態，以及解決先前與身分識別或裝置相關聯的風險事件。</span><span class="sxs-lookup"><span data-stu-id="315ad-159">A remediation action restores the identity or device to a safe state, and resolves previous risk events associated with the identity or device.</span></span>

### <a name="resolved-risk-event"></a><span data-ttu-id="315ad-160">已解決 (風險事件)</span><span class="sxs-lookup"><span data-stu-id="315ad-160">Resolved (risk event)</span></span>
<span data-ttu-id="315ad-161">由 Identity Protection 使用者手動設定的風險事件狀態，表示使用者在 Identity Protection 外部採取適當的補救動作，而且應該將風險事件視為已關閉。</span><span class="sxs-lookup"><span data-stu-id="315ad-161">A risk event status set manually by an Identity Protection user, indicating that the user took an appropriate remediation action outside Identity Protection, and that the risk event should be considered closed.</span></span>

### <a name="risk-event-status"></a><span data-ttu-id="315ad-162">風險事件狀態</span><span class="sxs-lookup"><span data-stu-id="315ad-162">Risk event status</span></span>
<span data-ttu-id="315ad-163">風險事件的屬性，指出事件是否為作用中，若已關閉，則會指出其關閉原因。</span><span class="sxs-lookup"><span data-stu-id="315ad-163">A property of a risk event, indicating whether the event is active, and if closed, the reason for closing it.</span></span>

### <a name="risk-event-type"></a><span data-ttu-id="315ad-164">風險事件類型</span><span class="sxs-lookup"><span data-stu-id="315ad-164">Risk event type</span></span>
<span data-ttu-id="315ad-165">風險事件的類別，指出導致事件被視為有風險的異常類型。</span><span class="sxs-lookup"><span data-stu-id="315ad-165">A category for the risk event, indicating the type of anomaly that caused the event to be considered risky.</span></span>

### <a name="risk-level-risk-event"></a><span data-ttu-id="315ad-166">風險層級 (風險事件)</span><span class="sxs-lookup"><span data-stu-id="315ad-166">Risk level (risk event)</span></span>
<span data-ttu-id="315ad-167">指出風險事件的嚴重性 (高、中或低)，可協助 Identity Protection 使用者排定為了降低組織風險而採取之行動的優先順序。</span><span class="sxs-lookup"><span data-stu-id="315ad-167">An indication (High, Medium, or Low) of the severity of the risk event to help Identity Protection users prioritize the actions they take to reduce the risk to their organization.</span></span> 

### <a name="risk-level-sign-in"></a><span data-ttu-id="315ad-168">風險層級 (登入)</span><span class="sxs-lookup"><span data-stu-id="315ad-168">Risk level (sign-in)</span></span>
<span data-ttu-id="315ad-169">指出特定登入 (其他人正嘗試使用使用者的身分識別) 的可能性 (高、中或低)。</span><span class="sxs-lookup"><span data-stu-id="315ad-169">An indication (High, Medium, or Low) of the likelihood that for a specific sign-in, someone else is attempting to use the user’s identity.</span></span>

### <a name="risk-level-user-compromise"></a><span data-ttu-id="315ad-170">風險層級 (使用者入侵)</span><span class="sxs-lookup"><span data-stu-id="315ad-170">Risk level (user compromise)</span></span>
<span data-ttu-id="315ad-171">指出身分識別遭到入侵的可能性 (高、中或低)。</span><span class="sxs-lookup"><span data-stu-id="315ad-171">An indication (High, Medium, or Low) of the likelihood that an identity has been compromised.</span></span>

### <a name="risk-level-vulnerability"></a><span data-ttu-id="315ad-172">風險層級 (弱點)</span><span class="sxs-lookup"><span data-stu-id="315ad-172">Risk level (vulnerability)</span></span>
<span data-ttu-id="315ad-173">指出弱點的嚴重性 (高、中或低)，可協助 Identity Protection 使用者排定為了降低組織風險而採取之行動的優先順序。</span><span class="sxs-lookup"><span data-stu-id="315ad-173">An indication (High, Medium, or Low) of the severity of the vulnerability to help Identity Protection users prioritize the actions they take to reduce the risk to their organization.</span></span>

### <a name="secure-identity"></a><span data-ttu-id="315ad-174">安全 (身分識別)</span><span class="sxs-lookup"><span data-stu-id="315ad-174">Secure (identity)</span></span>
<span data-ttu-id="315ad-175">採取補救動作 (例如變更密碼或機器重新安裝映像)，將可能遭到入侵的身分識別還原至未遭入侵的狀態。</span><span class="sxs-lookup"><span data-stu-id="315ad-175">Take remediation action such as a password change or machine reimaging to restore a potentially compromised identity to an uncompromised state.</span></span>

### <a name="security-policy"></a><span data-ttu-id="315ad-176">安全性原則</span><span class="sxs-lookup"><span data-stu-id="315ad-176">Security policy</span></span>
<span data-ttu-id="315ad-177">原則規則和條件的集合。</span><span class="sxs-lookup"><span data-stu-id="315ad-177">A collection of policy rules and condition.</span></span> <span data-ttu-id="315ad-178">原則可以套用至各種實體，例如使用者、群組、應用程式、裝置、裝置平台、裝置狀態、IP 範圍和 Auth2.0 用戶端類型。</span><span class="sxs-lookup"><span data-stu-id="315ad-178">A policy can be applied to entities such as users, groups, apps, devices, device platforms, device states, IP ranges, and Auth2.0 client types.</span></span> <span data-ttu-id="315ad-179">啟用原則後，就會在納入原則的實體被核發資源的權杖時進行評估。</span><span class="sxs-lookup"><span data-stu-id="315ad-179">When a policy is enabled, it is evaluated whenever an entity included in the policy is issued a token for a resource.</span></span>

### <a name="sign-in-v"></a><span data-ttu-id="315ad-180">登入 (動詞)</span><span class="sxs-lookup"><span data-stu-id="315ad-180">Sign in (v)</span></span>
<span data-ttu-id="315ad-181">在 Azure Active Directory 中驗證身分識別。</span><span class="sxs-lookup"><span data-stu-id="315ad-181">To authenticate to an identity in Azure Active Directory.</span></span>

### <a name="sign-in-n"></a><span data-ttu-id="315ad-182">登入 (名詞)</span><span class="sxs-lookup"><span data-stu-id="315ad-182">Sign-in (n)</span></span>
<span data-ttu-id="315ad-183">在 Azure Active Directory 中驗證身分識別的程序或動作，以及擷取這項作業的事件。</span><span class="sxs-lookup"><span data-stu-id="315ad-183">The process or action of authenticating an identity in Azure Active Directory, and the event that captures this operation.</span></span>

### <a name="sign-in-from-anonymous-ip-address"></a><span data-ttu-id="315ad-184">從匿名 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="315ad-184">Sign-in from anonymous IP address</span></span>
<span data-ttu-id="315ad-185">從被視為匿名 Proxy IP 位址的 IP 位址成功登入之後所觸發的風險事件。</span><span class="sxs-lookup"><span data-stu-id="315ad-185">A risk event triggered after a successful sign-in from IP address that has been identified as an anonymous proxy IP address.</span></span>

### <a name="sign-in-from-infected-device"></a><span data-ttu-id="315ad-186">從受感染的裝置登入</span><span class="sxs-lookup"><span data-stu-id="315ad-186">Sign-in from infected device</span></span>
<span data-ttu-id="315ad-187">當登入源自已知由一或多個遭入侵裝置 (這類裝置會主動嘗試與 Bot 伺服器通訊) 使用的 IP 位址時所觸發的風險事件。</span><span class="sxs-lookup"><span data-stu-id="315ad-187">A risk event triggered when a sign-in originates from an IP address which is known to be used by one or more compromised devices, which are actively attempting to communicate with a bot server.</span></span>

### <a name="sign-in-from-ip-address-with-suspicious-activity"></a><span data-ttu-id="315ad-188">從具有可疑活動的 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="315ad-188">Sign-in from IP address with suspicious activity</span></span>
<span data-ttu-id="315ad-189">從短期內透過多個使用者帳戶多次嘗試登入失敗的 IP 位址成功登入之後所觸發的風險事件。</span><span class="sxs-lookup"><span data-stu-id="315ad-189">A risk event triggered after a successful sign-in from an IP address with a high number of failed login attempts across multiple user accounts over a short period of time.</span></span>

### <a name="sign-in-from-unfamiliar-location"></a><span data-ttu-id="315ad-190">從不熟悉的位置登入</span><span class="sxs-lookup"><span data-stu-id="315ad-190">Sign-in from unfamiliar location</span></span>
<span data-ttu-id="315ad-191">當使用者從新的位置 (IP、經緯度和 ASN) 成功登入時所觸發的風險事件。</span><span class="sxs-lookup"><span data-stu-id="315ad-191">A risk event triggered when a user successfully signs in from a new location (IP, Latitude/Longitude and ASN).</span></span>

### <a name="sign-in-risk"></a><span data-ttu-id="315ad-192">登入風險</span><span class="sxs-lookup"><span data-stu-id="315ad-192">Sign-in risk</span></span>
<span data-ttu-id="315ad-193">請參閱風險層級 (登入)</span><span class="sxs-lookup"><span data-stu-id="315ad-193">See Risk level (sign-in)</span></span>

### <a name="sign-in-risk-policy"></a><span data-ttu-id="315ad-194">登入風險原則</span><span class="sxs-lookup"><span data-stu-id="315ad-194">Sign-in risk policy</span></span>
<span data-ttu-id="315ad-195">一個條件式存取原則，可評估特定登入的風險，並根據預先定義的條件和規則來套用緩和動作。</span><span class="sxs-lookup"><span data-stu-id="315ad-195">A conditional access policy that evaluates the risk to a specific sign-in and applies mitigations based on predefined conditions and rules.</span></span>

### <a name="user-compromise-risk"></a><span data-ttu-id="315ad-196">使用者入侵風險</span><span class="sxs-lookup"><span data-stu-id="315ad-196">User compromise risk</span></span>
<span data-ttu-id="315ad-197">請參閱風險層級 (使用者入侵)</span><span class="sxs-lookup"><span data-stu-id="315ad-197">See Risk level (user compromise)</span></span>

### <a name="user-risk"></a><span data-ttu-id="315ad-198">使用者風險</span><span class="sxs-lookup"><span data-stu-id="315ad-198">User risk</span></span>
<span data-ttu-id="315ad-199">請參閱風險層級 (使用者入侵)。</span><span class="sxs-lookup"><span data-stu-id="315ad-199">See Risk level (user compromise).</span></span>

### <a name="user-risk-policy"></a><span data-ttu-id="315ad-200">使用者風險原則</span><span class="sxs-lookup"><span data-stu-id="315ad-200">User risk policy</span></span>
<span data-ttu-id="315ad-201">一個條件式存取原則，可根據預先定義的條件和規則來考量及套用緩和動作。</span><span class="sxs-lookup"><span data-stu-id="315ad-201">A conditional access policy that considers the sign-in and applies mitigations based on predefined conditions and rules.</span></span>

### <a name="users-flagged-for-risk"></a><span data-ttu-id="315ad-202">標示有風險的使用者</span><span class="sxs-lookup"><span data-stu-id="315ad-202">Users flagged for risk</span></span>
<span data-ttu-id="315ad-203">具有作用中或已補救之風險事件的使用者</span><span class="sxs-lookup"><span data-stu-id="315ad-203">Users that have risk events which are either active or remediated</span></span>

### <a name="vulnerability"></a><span data-ttu-id="315ad-204">弱點</span><span class="sxs-lookup"><span data-stu-id="315ad-204">Vulnerability</span></span>
<span data-ttu-id="315ad-205">Azure Active Directory 中的組態或狀況，此組態或狀況會使目錄容易受到入侵或威脅的影響。</span><span class="sxs-lookup"><span data-stu-id="315ad-205">A configuration or condition in Azure Active Directory which makes the directory susceptible to exploits or threats.</span></span>

## <a name="see-also"></a><span data-ttu-id="315ad-206">另請參閱</span><span class="sxs-lookup"><span data-stu-id="315ad-206">See also</span></span>
* [<span data-ttu-id="315ad-207">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="315ad-207">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

