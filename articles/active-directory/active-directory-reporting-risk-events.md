---
title: "Azure Active Directory 風險事件 | Microsoft Docs"
description: "本主題詳述何謂風險事件。"
services: active-directory
keywords: "azure active directory identity protection, 安全性, 風險, 風險層級, 弱點, 安全性原則"
author: MarkusVi
manager: femila
ms.assetid: fa2c8b51-d43d-4349-8308-97e87665400b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 71ab5cb02ac70871fb8207ab9220b45d1c842dde
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-risk-events"></a><span data-ttu-id="b8b0d-104">Azure Active Directory 風險事件</span><span class="sxs-lookup"><span data-stu-id="b8b0d-104">Azure Active Directory risk events</span></span>

<span data-ttu-id="b8b0d-105">大部分的安全性缺口出現於當攻擊者藉由竊取使用者的身分識別來取得環境的存取權時。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-105">The vast majority of security breaches take place when attackers gain access to an environment by stealing a user’s identity.</span></span> <span data-ttu-id="b8b0d-106">探索遭入侵的身分識別並不容易。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-106">Discovering compromised identities is no easy task.</span></span> <span data-ttu-id="b8b0d-107">Azure Active Directory 使用調適性機器學習服務演算法和啟發學習法，來偵測與您使用者帳戶相關的可疑動作。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-107">Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect suspicious actions that are related to your user accounts.</span></span> <span data-ttu-id="b8b0d-108">偵測到的每個可疑動作會儲存在名為*風險事件*的記錄中。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-108">Each detected suspicious action is stored in a record called *risk event*.</span></span>

<span data-ttu-id="b8b0d-109">Azure Active Directory 目前會偵測六種風險事件類型：</span><span class="sxs-lookup"><span data-stu-id="b8b0d-109">Currently, Azure Active Directory detects six types of risk events:</span></span>

- [<span data-ttu-id="b8b0d-110">認證外洩的使用者</span><span class="sxs-lookup"><span data-stu-id="b8b0d-110">Users with leaked credentials</span></span>](#leaked-credentials) 
- [<span data-ttu-id="b8b0d-111">從匿名 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="b8b0d-111">Sign-ins from anonymous IP addresses</span></span>](#sign-ins-from-anonymous-ip-addresses) 
- [<span data-ttu-id="b8b0d-112">不可能進入非慣用位置</span><span class="sxs-lookup"><span data-stu-id="b8b0d-112">Impossible travel to atypical locations</span></span>](#impossible-travel-to-atypical-locations) 
- [<span data-ttu-id="b8b0d-113">從不熟悉的位置登入</span><span class="sxs-lookup"><span data-stu-id="b8b0d-113">Sign-ins from unfamiliar locations</span></span>](#sign-in-from-unfamiliar-locations)
- [<span data-ttu-id="b8b0d-114">從受感染的裝置登入</span><span class="sxs-lookup"><span data-stu-id="b8b0d-114">Sign-ins from infected devices</span></span>](#sign-ins-from-infected-devices) 
- [<span data-ttu-id="b8b0d-115">從具有可疑活動的 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="b8b0d-115">Sign-ins from IP addresses with suspicious activity</span></span>](#sign-ins-from-ip-addresses-with-suspicious-activity) 


![風險事件](./media/active-directory-reporting-risk-events/91.png)

<span data-ttu-id="b8b0d-117">本主題提供哪些屬於風險事件，以及您如何使用它們來保護 Azure AD 身分識別的概觀。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-117">This topic gives you a detailed overview of what risk events are and how you can use them to protect your Azure AD identities.</span></span>


## <a name="risk-event-types"></a><span data-ttu-id="b8b0d-118">風險事件類型</span><span class="sxs-lookup"><span data-stu-id="b8b0d-118">Risk event types</span></span>

<span data-ttu-id="b8b0d-119">風險事件類型屬性是風險事件記錄已為之建立的可疑動作的識別碼。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-119">The risk event type property is an identifier for the suspicious action a risk event record has been created for.</span></span>  
<span data-ttu-id="b8b0d-120">Microsoft 針對偵測程序的持續投資的結果是︰</span><span class="sxs-lookup"><span data-stu-id="b8b0d-120">Microsoft's continuous investments into the detection process lead to:</span></span>

- <span data-ttu-id="b8b0d-121">改善現有風險事件的偵測精確度</span><span class="sxs-lookup"><span data-stu-id="b8b0d-121">Improvements to the detection accuracy of existing risk events</span></span> 
- <span data-ttu-id="b8b0d-122">未來將會新增的新風險事件類型</span><span class="sxs-lookup"><span data-stu-id="b8b0d-122">New risk event types that will be added in the future</span></span>

### <a name="leaked-credentials"></a><span data-ttu-id="b8b0d-123">認證外洩</span><span class="sxs-lookup"><span data-stu-id="b8b0d-123">Leaked credentials</span></span>

<span data-ttu-id="b8b0d-124">當網路罪犯入侵合法使用者的有效密碼時，罪犯通常會共用這些認證。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-124">When cybercriminals compromise valid passwords of legitimate users, the criminals often share those credentials.</span></span> <span data-ttu-id="b8b0d-125">他們的做法通常是在深層網路上公開張貼或貼上站台，或是在黑市上交易或銷售認證。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-125">This is usually done by posting them publicly on the dark web or paste sites or by trading or selling the credentials on the black market.</span></span> <span data-ttu-id="b8b0d-126">Microsoft 的認證外洩服務取得使用者名稱 / 密碼組的方式，是監視公用及深層網路，以及使用：</span><span class="sxs-lookup"><span data-stu-id="b8b0d-126">The Microsoft leaked credentials service acquires username / password pairs by monitoring public and dark web sites and by working with:</span></span>

- <span data-ttu-id="b8b0d-127">研究員</span><span class="sxs-lookup"><span data-stu-id="b8b0d-127">Researchers</span></span>
- <span data-ttu-id="b8b0d-128">執法機關</span><span class="sxs-lookup"><span data-stu-id="b8b0d-128">Law enforcement</span></span>
- <span data-ttu-id="b8b0d-129">Microsoft 安全性小組</span><span class="sxs-lookup"><span data-stu-id="b8b0d-129">Security teams at Microsoft</span></span>
- <span data-ttu-id="b8b0d-130">其他受信任的來源</span><span class="sxs-lookup"><span data-stu-id="b8b0d-130">Other trusted sources</span></span> 

<span data-ttu-id="b8b0d-131">當服務取得使用者名稱 / 密碼組時，它們會針對 AAD 使用者目前的有效認證進行檢查。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-131">When the service acquires username / password pairs, they are checked against AAD users' current valid credentials.</span></span> <span data-ttu-id="b8b0d-132">找到相符項目時，表示使用者的密碼已遭入侵，並已建立認證外洩風險事件。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-132">When a match is found, it means that a user's password has been compromised, and a *leaked credentials risk event* is created.</span></span>

### <a name="sign-ins-from-anonymous-ip-addresses"></a><span data-ttu-id="b8b0d-133">從匿名 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="b8b0d-133">Sign-ins from anonymous IP addresses</span></span>

<span data-ttu-id="b8b0d-134">此風險事件類型會識別從被視為匿名 Proxy IP 位址的 IP 位址成功登入的使用者。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-134">This risk event type identifies users who have successfully signed in from an IP address that has been identified as an anonymous proxy IP address.</span></span> <span data-ttu-id="b8b0d-135">這些 Proxy 通常由想要隱藏其裝置 IP 位址的人員使用，而且可能用於惡意意圖。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-135">These proxies are used by people who want to hide their device’s IP address, and may be used for malicious intent.</span></span>


### <a name="impossible-travel-to-atypical-locations"></a><span data-ttu-id="b8b0d-136">不可能到達非典型位置的移動</span><span class="sxs-lookup"><span data-stu-id="b8b0d-136">Impossible travel to atypical locations</span></span>

<span data-ttu-id="b8b0d-137">此風險事件類型會識別來自距離遙遠的位置的兩次登入，而根據使用者過去的行為，其中至少有一個位置可能不尋常。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-137">This risk event type identifies two sign-ins originating from geographically distant locations, where at least one of the locations may also be atypical for the user, given past behavior.</span></span> <span data-ttu-id="b8b0d-138">此外，兩次登入之間的時間比使用者從第一個位置移到第二個位置所需的時間還要短，這表示有不同的使用者正在使用相同的認證。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-138">In addition, the time between the two sign-ins is shorter than the time it would have taken the user to travel from the first location to the second, indicating that a different user is using the same credentials.</span></span> 

<span data-ttu-id="b8b0d-139">這種機器學習演算法會忽略明顯的「誤判」，以致發生不可能的移動情況，例如，組織中的其他使用者定期使用的 VPN 和位置。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-139">This machine learning algorithm that ignores obvious "*false positives*" contributing to the impossible travel condition, such as VPNs and locations regularly used by other users in the organization.</span></span>  <span data-ttu-id="b8b0d-140">系統有為期 14 天的初始學習期間，它會在這段期間了解新使用者的登入行為。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-140">The system has an initial learning period of 14 days during which it learns a new user’s sign-in behavior.</span></span>

### <a name="sign-in-from-unfamiliar-locations"></a><span data-ttu-id="b8b0d-141">從不熟悉的位置登入</span><span class="sxs-lookup"><span data-stu-id="b8b0d-141">Sign-in from unfamiliar locations</span></span>

<span data-ttu-id="b8b0d-142">此風險事件類型會考量過去的登入位置 (IP、經緯度和 ASN) 以判斷新的 / 不熟悉的位置。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-142">This risk event type considers past sign-in locations (IP, Latitude / Longitude and ASN) to determine new / unfamiliar locations.</span></span> <span data-ttu-id="b8b0d-143">系統會儲存有關使用者先前所用位置的資訊，並考量這些「熟悉的」位置。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-143">The system stores information about previous locations used by a user, and considers these “familiar” locations.</span></span> <span data-ttu-id="b8b0d-144">從不在熟悉位置清單中的位置登入時，會觸發此風險事件。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-144">The risk event is triggered when the sign-in occurs from a location that's not already in the list of familiar locations.</span></span> <span data-ttu-id="b8b0d-145">系統有為期 30 天的初始學習期間，在這段期間內，它不會將任何新位置標示為不熟悉的位置。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-145">The system has an initial learning period of 30 days, during which it does not flag any new locations as unfamiliar locations.</span></span> <span data-ttu-id="b8b0d-146">系統也會忽略從熟悉的裝置以及地理上靠近熟悉位置的位置進行的登入。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-146">The system also ignores sign-ins from familiar devices, and locations that are geographically close to a familiar location.</span></span> 

### <a name="sign-ins-from-infected-devices"></a><span data-ttu-id="b8b0d-147">從受感染的裝置登入</span><span class="sxs-lookup"><span data-stu-id="b8b0d-147">Sign-ins from infected devices</span></span>

<span data-ttu-id="b8b0d-148">此風險事件類型會識別從感染惡意程式碼的裝置登入，已知這類登入會主動與 Bot 伺服器通訊。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-148">This risk event type identifies sign-ins from devices infected with malware, that are known to actively communicate with a bot server.</span></span> <span data-ttu-id="b8b0d-149">讓使用者裝置的 IP 位址與聯繫 Bot 伺服器的 IP 位址相互關聯，即可判定此類型。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-149">This is determined by correlating IP addresses of the user’s device against IP addresses that were in contact with a bot server.</span></span> 

### <a name="sign-ins-from-ip-addresses-with-suspicious-activity"></a><span data-ttu-id="b8b0d-150">從具有可疑活動的 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="b8b0d-150">Sign-ins from IP addresses with suspicious activity</span></span>
<span data-ttu-id="b8b0d-151">此風險事件類型會識別在短期內透過多個使用者帳戶多次嘗試登入失敗的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-151">This risk event type identifies IP addresses from which a high number of failed sign-in attempts were seen, across multiple user accounts, over a short period of time.</span></span> <span data-ttu-id="b8b0d-152">這符合攻擊者所使用的 IP 位址流量模式，而且強烈指出帳戶已經或即將遭到入侵。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-152">This matches traffic patterns of IP addresses used by attackers, and is a strong indicator that accounts are either already or are about to be compromised.</span></span> <span data-ttu-id="b8b0d-153">這種機器學習演算法會忽略明顯的「誤判」，例如，組織中的其他使用者定期使用的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-153">This is a machine learning algorithm that ignores obvious "*false-positives*", such as IP addresses that are regularly used by other users in the organization.</span></span>  <span data-ttu-id="b8b0d-154">系統有為期 14 天的初始學習期間，它會在這段期間了解新使用者和新租用戶的登入行為。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-154">The system has an initial learning period of 14 days where it learns the sign-in behavior of a new user and new tenant.</span></span>


## <a name="detection-type"></a><span data-ttu-id="b8b0d-155">偵測類型</span><span class="sxs-lookup"><span data-stu-id="b8b0d-155">Detection type</span></span>

<span data-ttu-id="b8b0d-156">偵測類型屬性是風險事件的偵測時間範圍指標 (即時或離線)。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-156">The detection type property is an indicator (Real-time or Offline) for the detection timeframe of a risk event.</span></span>  
<span data-ttu-id="b8b0d-157">目前，大部分的風險事件都是在風險事件發生之後，在後處理作業中以離線方式偵測的。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-157">Currently, most risk events are detected offline in a post-processing operation after the risk event has occurred.</span></span>

<span data-ttu-id="b8b0d-158">下表列出偵測類型要在相關報告中顯示所花費的時間：</span><span class="sxs-lookup"><span data-stu-id="b8b0d-158">The following table lists the amount of time it takes for a detection type to show up in a related report:</span></span>

| <span data-ttu-id="b8b0d-159">偵測類型</span><span class="sxs-lookup"><span data-stu-id="b8b0d-159">Detection Type</span></span> | <span data-ttu-id="b8b0d-160">報告延遲</span><span class="sxs-lookup"><span data-stu-id="b8b0d-160">Reporting Latency</span></span> |
| --- | --- |
| <span data-ttu-id="b8b0d-161">即時</span><span class="sxs-lookup"><span data-stu-id="b8b0d-161">Real-time</span></span> | <span data-ttu-id="b8b0d-162">5 至 10 分鐘</span><span class="sxs-lookup"><span data-stu-id="b8b0d-162">5 to 10 minutes</span></span> |
| <span data-ttu-id="b8b0d-163">離線</span><span class="sxs-lookup"><span data-stu-id="b8b0d-163">Offline</span></span> | <span data-ttu-id="b8b0d-164">2 至 4 小時</span><span class="sxs-lookup"><span data-stu-id="b8b0d-164">2 to 4 hours</span></span> |


<span data-ttu-id="b8b0d-165">針對 Azure Active Directory 要偵測的風險事件類型，偵測類型包括：</span><span class="sxs-lookup"><span data-stu-id="b8b0d-165">For the risk event types Azure Active Directory detects, the detection types are:</span></span>

| <span data-ttu-id="b8b0d-166">風險事件類型</span><span class="sxs-lookup"><span data-stu-id="b8b0d-166">Risk Event Type</span></span> | <span data-ttu-id="b8b0d-167">偵測類型</span><span class="sxs-lookup"><span data-stu-id="b8b0d-167">Detection Type</span></span> |
| :-- | --- | 
| [<span data-ttu-id="b8b0d-168">認證外洩的使用者</span><span class="sxs-lookup"><span data-stu-id="b8b0d-168">Users with leaked credentials</span></span>](#leaked-credentials) | <span data-ttu-id="b8b0d-169">離線</span><span class="sxs-lookup"><span data-stu-id="b8b0d-169">Offline</span></span> |
| [<span data-ttu-id="b8b0d-170">從匿名 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="b8b0d-170">Sign-ins from anonymous IP addresses</span></span>](#sign-ins-from-anonymous-ip-addresses) | <span data-ttu-id="b8b0d-171">即時</span><span class="sxs-lookup"><span data-stu-id="b8b0d-171">Real-time</span></span> |
| [<span data-ttu-id="b8b0d-172">不可能進入非慣用位置</span><span class="sxs-lookup"><span data-stu-id="b8b0d-172">Impossible travel to atypical locations</span></span>](#impossible-travel-to-atypical-locations) | <span data-ttu-id="b8b0d-173">離線</span><span class="sxs-lookup"><span data-stu-id="b8b0d-173">Offline</span></span> |
| [<span data-ttu-id="b8b0d-174">從不熟悉的位置登入</span><span class="sxs-lookup"><span data-stu-id="b8b0d-174">Sign-ins from unfamiliar locations</span></span>](#sign-in-from-unfamiliar-locations) | <span data-ttu-id="b8b0d-175">即時</span><span class="sxs-lookup"><span data-stu-id="b8b0d-175">Real-time</span></span> |
| [<span data-ttu-id="b8b0d-176">從受感染的裝置登入</span><span class="sxs-lookup"><span data-stu-id="b8b0d-176">Sign-ins from infected devices</span></span>](#sign-ins-from-infected-devices) | <span data-ttu-id="b8b0d-177">離線</span><span class="sxs-lookup"><span data-stu-id="b8b0d-177">Offline</span></span> |
| [<span data-ttu-id="b8b0d-178">從具有可疑活動的 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="b8b0d-178">Sign-ins from IP addresses with suspicious activity</span></span>](#sign-ins-from-ip-addresses-with-suspicious-activity) | <span data-ttu-id="b8b0d-179">離線</span><span class="sxs-lookup"><span data-stu-id="b8b0d-179">Offline</span></span>|


## <a name="risk-level"></a><span data-ttu-id="b8b0d-180">風險層級</span><span class="sxs-lookup"><span data-stu-id="b8b0d-180">Risk level</span></span>

<span data-ttu-id="b8b0d-181">風險事件的風險層級屬性是風險事件的嚴重性和信賴度的指標 (高、中或低)。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-181">The risk level property of a risk event is an indicator (High, Medium, or Low) for the severity and the confidence of a risk event.</span></span> <span data-ttu-id="b8b0d-182">這個屬性可協助您排定必須採取之動作的優先順序。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-182">This property helps you to prioritize the actions you must take.</span></span> 

<span data-ttu-id="b8b0d-183">風險事件的嚴重性代表做為身分識別入侵預測工具的訊號強度。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-183">The severity of the risk event represents the strength of the signal as a predictor of identity compromise.</span></span>  
<span data-ttu-id="b8b0d-184">信賴度是發生誤判可能性的指標。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-184">The confidence is an indicator for the possibility of false positives.</span></span> 

<span data-ttu-id="b8b0d-185">例如，</span><span class="sxs-lookup"><span data-stu-id="b8b0d-185">For example,</span></span> 

* <span data-ttu-id="b8b0d-186">**高**：高信賴度和高嚴重性風險事件。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-186">**High**: High confidence and high severity risk event.</span></span> <span data-ttu-id="b8b0d-187">這些事件強烈指出使用者的身分識別已遭入侵，而且應該立即補救任何受影響的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-187">These events are strong indicators that the user’s identity has been compromised, and any user accounts impacted should be remediated immediately.</span></span>

* <span data-ttu-id="b8b0d-188">**中**：高嚴重性，但信賴度較低的風險事件，或反之亦然。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-188">**Medium**: High severity, but lower confidence risk event, or vice versa.</span></span> <span data-ttu-id="b8b0d-189">這些事件具有潛在風險，而且應該補救任何受影響的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-189">These events are potentially risky, and any user accounts impacted should be remediated.</span></span>

* <span data-ttu-id="b8b0d-190">**低**：低信賴度和低嚴重性風險事件。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-190">**Low**: Low confidence and low severity risk event.</span></span> <span data-ttu-id="b8b0d-191">此事件可能不需要採取立即行動，但與其他風險事件結合時，可能強烈指出身分識別遭到入侵。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-191">This event may not require an immediate action, but when combined with other risk events, may provide a strong indication that the identity is compromised.</span></span>

![風險層級](./media/active-directory-reporting-risk-events/01.png)

### <a name="leaked-credentials"></a><span data-ttu-id="b8b0d-193">認證外洩</span><span class="sxs-lookup"><span data-stu-id="b8b0d-193">Leaked credentials</span></span>

<span data-ttu-id="b8b0d-194">認證外洩風險事件會被歸類為**高**，因為它們清楚指出攻擊者可使用使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-194">Leaked credentials risk events are classified as a **High**, because they provide a clear indication that the user name and password are available to an attacker.</span></span>

### <a name="sign-ins-from-anonymous-ip-addresses"></a><span data-ttu-id="b8b0d-195">從匿名 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="b8b0d-195">Sign-ins from anonymous IP addresses</span></span>

<span data-ttu-id="b8b0d-196">此風險事件類型的風險層級為**中**，因為匿名 IP 位址並未強烈指出帳戶遭到入侵。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-196">The risk level for this risk event type is **Medium** because an anonymous IP address is not a strong indication of an account compromise.</span></span>  
<span data-ttu-id="b8b0d-197">我們建議您立即連絡使用者，確認他們是否使用匿名 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-197">We recommend that you immediately contact the user to verify if they were using anonymous IP addresses.</span></span>


### <a name="impossible-travel-to-atypical-locations"></a><span data-ttu-id="b8b0d-198">不可能到達非典型位置的移動</span><span class="sxs-lookup"><span data-stu-id="b8b0d-198">Impossible travel to atypical locations</span></span>

<span data-ttu-id="b8b0d-199">不可能的移動通常會明顯指出駭客已能夠成功登入。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-199">Impossible travel is usually a good indicator that a hacker was able to successfully sign-in.</span></span> <span data-ttu-id="b8b0d-200">不過，當使用者使用新裝置或使用組織中其他使用者通常不會使用的 VPN 進行移動時，可能會發生誤判。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-200">However, false-positives may occur when a user is traveling using a new device or using a VPN that is typically not used by other users in the organization.</span></span> <span data-ttu-id="b8b0d-201">另一個誤判來源是誤將伺服器 IP 當作用戶端 IP 傳遞的應用程式，其可能會導致從裝載應用程式後端的資料中心進行登入 (這些通常是 Microsoft 資料中心，其可能導致從 Microsoft 擁有的 IP 位址進行登入)。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-201">Another source of false-positives is applications that incorrectly pass server IPs as client IPs, which may give the appearance of sign-ins taking place from the data center where that application’s back-end is hosted (often these are Microsoft datacenters, which may give the appearance of sign-ins taking place from Microsoft owned IP addresses).</span></span> <span data-ttu-id="b8b0d-202">由於這些誤判，以致此風險事件的風險層級為**中**。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-202">As a result of these false-positives, the risk level for this risk event is **Medium**.</span></span>

> [!TIP]
> <span data-ttu-id="b8b0d-203">您可以藉由設定[具名位置](active-directory-named-locations.md)，來降低針對此風險事件類型所報告的誤判數量。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-203">You can reduce the amount of reported false-positves for this risk event type by configuring [named locations](active-directory-named-locations.md).</span></span> 

### <a name="sign-in-from-unfamiliar-locations"></a><span data-ttu-id="b8b0d-204">從不熟悉的位置登入</span><span class="sxs-lookup"><span data-stu-id="b8b0d-204">Sign-in from unfamiliar locations</span></span>

<span data-ttu-id="b8b0d-205">不熟悉的位置可以強烈指出攻擊者可能使用遭竊的身分識別。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-205">Unfamiliar locations can provide a strong indication that an attacker is able to use a stolen identity.</span></span> <span data-ttu-id="b8b0d-206">當使用者正在移動、試用新裝置或使用新的 VPN 時，可能會發生誤判。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-206">False-positives may occur when a user is traveling, is trying out a new device, or is using a new VPN.</span></span> <span data-ttu-id="b8b0d-207">由於這些誤判，以致此事件類型的風險層級為**中**。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-207">As a result of these false positives, the risk level for this event type is **Medium**.</span></span>

### <a name="sign-ins-from-infected-devices"></a><span data-ttu-id="b8b0d-208">從受感染的裝置登入</span><span class="sxs-lookup"><span data-stu-id="b8b0d-208">Sign-ins from infected devices</span></span>

<span data-ttu-id="b8b0d-209">此風險事件可識別 IP 位址，而不是使用者裝置。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-209">This risk event identifies IP addresses, not user devices.</span></span> <span data-ttu-id="b8b0d-210">如果單一 IP 位址背後有數個裝置，而只有某些裝置受 Bot 網路控制，則來自其他裝置的登入可能會不必要地觸發此事件，這就是將此風險事件歸類為**低**的原因。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-210">If several devices are behind a single IP address, and only some are controlled by a bot network, sign-ins from other devices my trigger this event unnecessarily, which is the reason for classifying this risk event as **Low**.</span></span>  

<span data-ttu-id="b8b0d-211">建議您連絡使用者並掃描使用者的所有裝置。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-211">We recommend that you contact the user and scan all the user's devices.</span></span> <span data-ttu-id="b8b0d-212">使用者的個人裝置也可能受到感染，或如前所述，可能是其他人從與使用者相同的 IP 位址使用受感染的裝置。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-212">It is also possible that a user's personal device is infected, or as mentioned earlier, that someone else was using an infected device from the same IP address as the user.</span></span> <span data-ttu-id="b8b0d-213">受感染的裝置通常是受到防毒軟體尚未識別的惡意程式碼所感染，這也表示不良的使用者習慣可能會導致裝置受到感染。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-213">Infected devices are often infected by malware that have not yet been identified by anti-virus software, and may also indicate as bad user habits that may have caused the device to become infected.</span></span>

<span data-ttu-id="b8b0d-214">如需如何處理惡意程式碼感染的詳細資訊，請參閱 [惡意程式碼防護中心](http://go.microsoft.com/fwlink/?linkid=335773&clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-214">For more information about how to address malware infections, see the [Malware Protection Center](http://go.microsoft.com/fwlink/?linkid=335773&clcid=0x409).</span></span>


### <a name="sign-ins-from-ip-addresses-with-suspicious-activity"></a><span data-ttu-id="b8b0d-215">從具有可疑活動的 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="b8b0d-215">Sign-ins from IP addresses with suspicious activity</span></span>

<span data-ttu-id="b8b0d-216">我們建議您連絡使用者，確認他們是否實際從標示為可疑的 IP 位址進行登入。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-216">We recommend that you contact the user to verify if they actually signed in from an IP address that was marked as suspicious.</span></span> <span data-ttu-id="b8b0d-217">此事件類型的風險層級為「**中**」，因為相同 IP 位址背後可能有數個裝置，而只有某些裝置可能負責進行可疑的活動。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-217">The risk level for this event type is “**Medium**” because several devices may be behind the same IP address, while only some may be responsible for the suspicious activity.</span></span> 


 
## <a name="next-steps"></a><span data-ttu-id="b8b0d-218">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b8b0d-218">Next steps</span></span>

<span data-ttu-id="b8b0d-219">風險事件是保護您 Azure AD 身分識別的基礎。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-219">Risk events are the foundation for protecting your Azure AD's identities.</span></span> <span data-ttu-id="b8b0d-220">Azure AD 目前可以偵測六種風險事件：</span><span class="sxs-lookup"><span data-stu-id="b8b0d-220">Azure AD can currently detect six risk events:</span></span> 


| <span data-ttu-id="b8b0d-221">風險事件類型</span><span class="sxs-lookup"><span data-stu-id="b8b0d-221">Risk Event Type</span></span> | <span data-ttu-id="b8b0d-222">風險層級</span><span class="sxs-lookup"><span data-stu-id="b8b0d-222">Risk Level</span></span> | <span data-ttu-id="b8b0d-223">偵測類型</span><span class="sxs-lookup"><span data-stu-id="b8b0d-223">Detection Type</span></span> |
| :-- | --- | --- |
| [<span data-ttu-id="b8b0d-224">認證外洩的使用者</span><span class="sxs-lookup"><span data-stu-id="b8b0d-224">Users with leaked credentials</span></span>](#leaked-credentials) | <span data-ttu-id="b8b0d-225">高</span><span class="sxs-lookup"><span data-stu-id="b8b0d-225">High</span></span> | <span data-ttu-id="b8b0d-226">離線</span><span class="sxs-lookup"><span data-stu-id="b8b0d-226">Offline</span></span> |
| [<span data-ttu-id="b8b0d-227">從匿名 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="b8b0d-227">Sign-ins from anonymous IP addresses</span></span>](#sign-ins-from-anonymous-ip-addresses) | <span data-ttu-id="b8b0d-228">中型</span><span class="sxs-lookup"><span data-stu-id="b8b0d-228">Medium</span></span> | <span data-ttu-id="b8b0d-229">即時</span><span class="sxs-lookup"><span data-stu-id="b8b0d-229">Real-time</span></span> |
| [<span data-ttu-id="b8b0d-230">不可能進入非慣用位置</span><span class="sxs-lookup"><span data-stu-id="b8b0d-230">Impossible travel to atypical locations</span></span>](#impossible-travel-to-atypical-locations) | <span data-ttu-id="b8b0d-231">中型</span><span class="sxs-lookup"><span data-stu-id="b8b0d-231">Medium</span></span> | <span data-ttu-id="b8b0d-232">離線</span><span class="sxs-lookup"><span data-stu-id="b8b0d-232">Offline</span></span> |
| [<span data-ttu-id="b8b0d-233">從不熟悉的位置登入</span><span class="sxs-lookup"><span data-stu-id="b8b0d-233">Sign-ins from unfamiliar locations</span></span>](#sign-in-from-unfamiliar-locations) | <span data-ttu-id="b8b0d-234">中型</span><span class="sxs-lookup"><span data-stu-id="b8b0d-234">Medium</span></span> | <span data-ttu-id="b8b0d-235">即時</span><span class="sxs-lookup"><span data-stu-id="b8b0d-235">Real-time</span></span> |
| [<span data-ttu-id="b8b0d-236">從受感染的裝置登入</span><span class="sxs-lookup"><span data-stu-id="b8b0d-236">Sign-ins from infected devices</span></span>](#sign-ins-from-infected-devices) | <span data-ttu-id="b8b0d-237">低</span><span class="sxs-lookup"><span data-stu-id="b8b0d-237">Low</span></span> | <span data-ttu-id="b8b0d-238">離線</span><span class="sxs-lookup"><span data-stu-id="b8b0d-238">Offline</span></span> |
| [<span data-ttu-id="b8b0d-239">從具有可疑活動的 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="b8b0d-239">Sign-ins from IP addresses with suspicious activity</span></span>](#sign-ins-from-ip-addresses-with-suspicious-activity) | <span data-ttu-id="b8b0d-240">中型</span><span class="sxs-lookup"><span data-stu-id="b8b0d-240">Medium</span></span> | <span data-ttu-id="b8b0d-241">離線</span><span class="sxs-lookup"><span data-stu-id="b8b0d-241">Offline</span></span>|

<span data-ttu-id="b8b0d-242">您可以在何處找到已在您的環境中偵測到的風險事件？</span><span class="sxs-lookup"><span data-stu-id="b8b0d-242">Where can you find the risk events that have been detected in your environment?</span></span>
<span data-ttu-id="b8b0d-243">您可以在兩個地方檢閱已報告的風險事件：</span><span class="sxs-lookup"><span data-stu-id="b8b0d-243">There are two places where you review reported risk events:</span></span>

 - <span data-ttu-id="b8b0d-244">**Azure AD 報告** - 風險事件屬於 Azure AD 的安全性報表。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-244">**Azure AD reporting** - Risk events are part of Azure AD's security reports.</span></span> <span data-ttu-id="b8b0d-245">如需詳細資訊，請參閱[有風險的安全性報告上的使用者](active-directory-reporting-security-user-at-risk.md)和[有風險的登入安全性報告](active-directory-reporting-security-risky-sign-ins.md)。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-245">For more details, see the [users at risk security report](active-directory-reporting-security-user-at-risk.md) and the [risky sign-ins security report](active-directory-reporting-security-risky-sign-ins.md).</span></span>

 - <span data-ttu-id="b8b0d-246">**Azure AD Identity Protection** - 風險事件也屬於 [Azure Active Directory Identity Protection](active-directory-identityprotection.md) 的報告功能。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-246">**Azure AD Identity Protection** - Risk events are also part of [Azure Active Directory Identity Protection's](active-directory-identityprotection.md) reporting capabilities.</span></span>
    

<span data-ttu-id="b8b0d-247">儘管偵測風險事件已經代表保護您身分識別的重要層面，但您還是可以選擇手動處理它們，或甚至可藉由設定條件式存取原則來實作自動化回應。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-247">While the detection of risk events already represents an important aspect of protecting your identities, you also have the option to either manually address them or even implement automated responses by configuring conditional access policies.</span></span> <span data-ttu-id="b8b0d-248">如需詳細資料，請參閱 [Azure Active Directory Identity Protection](active-directory-identityprotection.md)。</span><span class="sxs-lookup"><span data-stu-id="b8b0d-248">For more details, see of [Azure Active Directory Identity Protection's](active-directory-identityprotection.md).</span></span>
 
