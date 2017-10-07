---
title: "aaaAzure Active Directory 的風險事件 |Microsoft 文件"
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
ms.openlocfilehash: d771c1f43707744aac728c4f72000d855cbd6e1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-risk-events"></a><span data-ttu-id="0dd57-104">Azure Active Directory 風險事件</span><span class="sxs-lookup"><span data-stu-id="0dd57-104">Azure Active Directory risk events</span></span>

<span data-ttu-id="0dd57-105">攻擊者竊取使用者的身分識別取得存取 tooan 環境時，就會放置 hello 大部分的安全性缺口，這需要。</span><span class="sxs-lookup"><span data-stu-id="0dd57-105">hello vast majority of security breaches take place when attackers gain access tooan environment by stealing a user’s identity.</span></span> <span data-ttu-id="0dd57-106">探索遭入侵的身分識別並不容易。</span><span class="sxs-lookup"><span data-stu-id="0dd57-106">Discovering compromised identities is no easy task.</span></span> <span data-ttu-id="0dd57-107">Azure Active Directory 使用彈性的機器學習演算法和啟發學習法 toodetect 可疑動作相關的 tooyour 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="0dd57-107">Azure Active Directory uses adaptive machine learning algorithms and heuristics toodetect suspicious actions that are related tooyour user accounts.</span></span> <span data-ttu-id="0dd57-108">偵測到的每個可疑動作會儲存在名為*風險事件*的記錄中。</span><span class="sxs-lookup"><span data-stu-id="0dd57-108">Each detected suspicious action is stored in a record called *risk event*.</span></span>

<span data-ttu-id="0dd57-109">Azure Active Directory 目前會偵測六種風險事件類型：</span><span class="sxs-lookup"><span data-stu-id="0dd57-109">Currently, Azure Active Directory detects six types of risk events:</span></span>

- [<span data-ttu-id="0dd57-110">認證外洩的使用者</span><span class="sxs-lookup"><span data-stu-id="0dd57-110">Users with leaked credentials</span></span>](#leaked-credentials) 
- [<span data-ttu-id="0dd57-111">從匿名 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="0dd57-111">Sign-ins from anonymous IP addresses</span></span>](#sign-ins-from-anonymous-ip-addresses) 
- [<span data-ttu-id="0dd57-112">不可能的旅遊 tooatypical 位置</span><span class="sxs-lookup"><span data-stu-id="0dd57-112">Impossible travel tooatypical locations</span></span>](#impossible-travel-to-atypical-locations) 
- [<span data-ttu-id="0dd57-113">從不熟悉的位置登入</span><span class="sxs-lookup"><span data-stu-id="0dd57-113">Sign-ins from unfamiliar locations</span></span>](#sign-in-from-unfamiliar-locations)
- [<span data-ttu-id="0dd57-114">從受感染的裝置登入</span><span class="sxs-lookup"><span data-stu-id="0dd57-114">Sign-ins from infected devices</span></span>](#sign-ins-from-infected-devices) 
- [<span data-ttu-id="0dd57-115">從具有可疑活動的 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="0dd57-115">Sign-ins from IP addresses with suspicious activity</span></span>](#sign-ins-from-ip-addresses-with-suspicious-activity) 


![風險事件](./media/active-directory-reporting-risk-events/91.png)

<span data-ttu-id="0dd57-117">本主題提供您哪些風險事件的詳細的概觀會和您可以如何使用這些 tooprotect 您 Azure AD 身分識別。</span><span class="sxs-lookup"><span data-stu-id="0dd57-117">This topic gives you a detailed overview of what risk events are and how you can use them tooprotect your Azure AD identities.</span></span>


## <a name="risk-event-types"></a><span data-ttu-id="0dd57-118">風險事件類型</span><span class="sxs-lookup"><span data-stu-id="0dd57-118">Risk event types</span></span>

<span data-ttu-id="0dd57-119">hello 風險事件類型的屬性是已建立 hello 可疑動作的風險事件記錄的識別碼。</span><span class="sxs-lookup"><span data-stu-id="0dd57-119">hello risk event type property is an identifier for hello suspicious action a risk event record has been created for.</span></span>  
<span data-ttu-id="0dd57-120">Microsoft 的連續投資放在 hello 偵測處理程序會導致：</span><span class="sxs-lookup"><span data-stu-id="0dd57-120">Microsoft's continuous investments into hello detection process lead to:</span></span>

- <span data-ttu-id="0dd57-121">現有的風險事件的增強功能 toohello 偵測正確性</span><span class="sxs-lookup"><span data-stu-id="0dd57-121">Improvements toohello detection accuracy of existing risk events</span></span> 
- <span data-ttu-id="0dd57-122">將在未來的 hello 中加入的新風險事件類型</span><span class="sxs-lookup"><span data-stu-id="0dd57-122">New risk event types that will be added in hello future</span></span>

### <a name="leaked-credentials"></a><span data-ttu-id="0dd57-123">認證外洩</span><span class="sxs-lookup"><span data-stu-id="0dd57-123">Leaked credentials</span></span>

<span data-ttu-id="0dd57-124">當 cybercriminals 洩露合法使用者的有效密碼時，hello 罪犯通常會共用這些認證。</span><span class="sxs-lookup"><span data-stu-id="0dd57-124">When cybercriminals compromise valid passwords of legitimate users, hello criminals often share those credentials.</span></span> <span data-ttu-id="0dd57-125">這通常是經由張貼公開 hello 深色 web 或貼上站台上，或由交易或銷售 hello 黑市 hello 認證。</span><span class="sxs-lookup"><span data-stu-id="0dd57-125">This is usually done by posting them publicly on hello dark web or paste sites or by trading or selling hello credentials on hello black market.</span></span> <span data-ttu-id="0dd57-126">hello Microsoft 外洩認證服務取得使用者名稱 / 密碼組藉由監視公用及深色的網站，並使用：</span><span class="sxs-lookup"><span data-stu-id="0dd57-126">hello Microsoft leaked credentials service acquires username / password pairs by monitoring public and dark web sites and by working with:</span></span>

- <span data-ttu-id="0dd57-127">研究員</span><span class="sxs-lookup"><span data-stu-id="0dd57-127">Researchers</span></span>
- <span data-ttu-id="0dd57-128">執法機關</span><span class="sxs-lookup"><span data-stu-id="0dd57-128">Law enforcement</span></span>
- <span data-ttu-id="0dd57-129">Microsoft 安全性小組</span><span class="sxs-lookup"><span data-stu-id="0dd57-129">Security teams at Microsoft</span></span>
- <span data-ttu-id="0dd57-130">其他受信任的來源</span><span class="sxs-lookup"><span data-stu-id="0dd57-130">Other trusted sources</span></span> 

<span data-ttu-id="0dd57-131">當 hello 服務取得使用者名稱 / 密碼組，它們會針對檢查 AAD 使用者的目前有效的認證。</span><span class="sxs-lookup"><span data-stu-id="0dd57-131">When hello service acquires username / password pairs, they are checked against AAD users' current valid credentials.</span></span> <span data-ttu-id="0dd57-132">找到相符項目時，表示使用者的密碼已遭入侵，並已建立認證外洩風險事件。</span><span class="sxs-lookup"><span data-stu-id="0dd57-132">When a match is found, it means that a user's password has been compromised, and a *leaked credentials risk event* is created.</span></span>

### <a name="sign-ins-from-anonymous-ip-addresses"></a><span data-ttu-id="0dd57-133">從匿名 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="0dd57-133">Sign-ins from anonymous IP addresses</span></span>

<span data-ttu-id="0dd57-134">此風險事件類型會識別從被視為匿名 Proxy IP 位址的 IP 位址成功登入的使用者。</span><span class="sxs-lookup"><span data-stu-id="0dd57-134">This risk event type identifies users who have successfully signed in from an IP address that has been identified as an anonymous proxy IP address.</span></span> <span data-ttu-id="0dd57-135">這些 proxy 是 toohide 的人使用其裝置的 IP 位址，並可用於被用於惡意用途。</span><span class="sxs-lookup"><span data-stu-id="0dd57-135">These proxies are used by people who want toohide their device’s IP address, and may be used for malicious intent.</span></span>


### <a name="impossible-travel-tooatypical-locations"></a><span data-ttu-id="0dd57-136">不可能的旅遊 tooatypical 位置</span><span class="sxs-lookup"><span data-stu-id="0dd57-136">Impossible travel tooatypical locations</span></span>

<span data-ttu-id="0dd57-137">這個風險事件類型識別兩個登入來自不同地理位置不同的位置，其中至少一個 hello 位置也可能慣用 hello 使用者，根據過去的行為。</span><span class="sxs-lookup"><span data-stu-id="0dd57-137">This risk event type identifies two sign-ins originating from geographically distant locations, where at least one of hello locations may also be atypical for hello user, given past behavior.</span></span> <span data-ttu-id="0dd57-138">此外，hello hello 兩次登入之間的時間長度小於 hello 階段需花費 hello 使用者 tootravel 從第一個位置 toohello hello 第二個，表示有不同的使用者正在使用 hello 相同的認證。</span><span class="sxs-lookup"><span data-stu-id="0dd57-138">In addition, hello time between hello two sign-ins is shorter than hello time it would have taken hello user tootravel from hello first location toohello second, indicating that a different user is using hello same credentials.</span></span> 

<span data-ttu-id="0dd57-139">會忽略明顯此機器學習演算法"*誤判*」 參與 toohello 不可能的旅遊條件，例如 Vpn 和定期使用 hello 組織中其他使用者的位置。</span><span class="sxs-lookup"><span data-stu-id="0dd57-139">This machine learning algorithm that ignores obvious "*false positives*" contributing toohello impossible travel condition, such as VPNs and locations regularly used by other users in hello organization.</span></span>  <span data-ttu-id="0dd57-140">hello 系統具有初始學習期間內，是在 14 天的期間，它學習新的使用者登入行為。</span><span class="sxs-lookup"><span data-stu-id="0dd57-140">hello system has an initial learning period of 14 days during which it learns a new user’s sign-in behavior.</span></span>

### <a name="sign-in-from-unfamiliar-locations"></a><span data-ttu-id="0dd57-141">從不熟悉的位置登入</span><span class="sxs-lookup"><span data-stu-id="0dd57-141">Sign-in from unfamiliar locations</span></span>

<span data-ttu-id="0dd57-142">這個風險事件類型會考慮過去的登入位置 (IP、 緯度 / 經度和 ASN) toodetermine 新 / 不熟悉的位置。</span><span class="sxs-lookup"><span data-stu-id="0dd57-142">This risk event type considers past sign-in locations (IP, Latitude / Longitude and ASN) toodetermine new / unfamiliar locations.</span></span> <span data-ttu-id="0dd57-143">hello 系統儲存的使用者，使用先前的位置的相關資訊，並將這些 「 熟悉"的位置。</span><span class="sxs-lookup"><span data-stu-id="0dd57-143">hello system stores information about previous locations used by a user, and considers these “familiar” locations.</span></span> <span data-ttu-id="0dd57-144">hello 風險事件觸發 hello 登入，就會發生的位置，還不熟悉的位置 hello 清單中。</span><span class="sxs-lookup"><span data-stu-id="0dd57-144">hello risk event is triggered when hello sign-in occurs from a location that's not already in hello list of familiar locations.</span></span> <span data-ttu-id="0dd57-145">hello 系統具有初始學習期間的 30 天，在它不會不加上旗標任何新位置中，如不熟悉的位置。</span><span class="sxs-lookup"><span data-stu-id="0dd57-145">hello system has an initial learning period of 30 days, during which it does not flag any new locations as unfamiliar locations.</span></span> <span data-ttu-id="0dd57-146">hello 系統也會忽略從熟悉的裝置登入，並屬於不同地理位置關閉 tooa 熟悉的位置。</span><span class="sxs-lookup"><span data-stu-id="0dd57-146">hello system also ignores sign-ins from familiar devices, and locations that are geographically close tooa familiar location.</span></span> 

### <a name="sign-ins-from-infected-devices"></a><span data-ttu-id="0dd57-147">從受感染的裝置登入</span><span class="sxs-lookup"><span data-stu-id="0dd57-147">Sign-ins from infected devices</span></span>

<span data-ttu-id="0dd57-148">這個風險事件類型會識別裝置感染惡意程式碼，稱為 tooactively bot 伺服器通訊的登入。</span><span class="sxs-lookup"><span data-stu-id="0dd57-148">This risk event type identifies sign-ins from devices infected with malware, that are known tooactively communicate with a bot server.</span></span> <span data-ttu-id="0dd57-149">這取決於相互關聯的 hello 使用者的裝置已 bot 伺服器的 IP 位址的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0dd57-149">This is determined by correlating IP addresses of hello user’s device against IP addresses that were in contact with a bot server.</span></span> 

### <a name="sign-ins-from-ip-addresses-with-suspicious-activity"></a><span data-ttu-id="0dd57-150">從具有可疑活動的 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="0dd57-150">Sign-ins from IP addresses with suspicious activity</span></span>
<span data-ttu-id="0dd57-151">此風險事件類型會識別在短期內透過多個使用者帳戶多次嘗試登入失敗的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0dd57-151">This risk event type identifies IP addresses from which a high number of failed sign-in attempts were seen, across multiple user accounts, over a short period of time.</span></span> <span data-ttu-id="0dd57-152">這符合攻擊者，所使用的 IP 位址的流量模式，而且是強式的指標帳戶可能已經或即將 toobe 入侵。</span><span class="sxs-lookup"><span data-stu-id="0dd57-152">This matches traffic patterns of IP addresses used by attackers, and is a strong indicator that accounts are either already or are about toobe compromised.</span></span> <span data-ttu-id="0dd57-153">這是會忽略明顯的機器學習演算法"*false 誤判*"，例如 IP 位址的定期供 hello 組織中其他使用者。</span><span class="sxs-lookup"><span data-stu-id="0dd57-153">This is a machine learning algorithm that ignores obvious "*false-positives*", such as IP addresses that are regularly used by other users in hello organization.</span></span>  <span data-ttu-id="0dd57-154">hello 系統有 14 天的初始學習期間內，它會學習 hello 登入新的使用者和新的租用戶的行為。</span><span class="sxs-lookup"><span data-stu-id="0dd57-154">hello system has an initial learning period of 14 days where it learns hello sign-in behavior of a new user and new tenant.</span></span>


## <a name="detection-type"></a><span data-ttu-id="0dd57-155">偵測類型</span><span class="sxs-lookup"><span data-stu-id="0dd57-155">Detection type</span></span>

<span data-ttu-id="0dd57-156">hello 偵測類型屬性都是指標 （即時或離線） 的風險事件 hello 偵測時間範圍內。</span><span class="sxs-lookup"><span data-stu-id="0dd57-156">hello detection type property is an indicator (Real-time or Offline) for hello detection timeframe of a risk event.</span></span>  
<span data-ttu-id="0dd57-157">目前，大部分的風險事件皆偵測為離線後置處理作業中發生 hello 風險事件之後。</span><span class="sxs-lookup"><span data-stu-id="0dd57-157">Currently, most risk events are detected offline in a post-processing operation after hello risk event has occurred.</span></span>

<span data-ttu-id="0dd57-158">hello 下表列出花費的時間偵測類型 tooshow 相關的報表中的 hello 數量：</span><span class="sxs-lookup"><span data-stu-id="0dd57-158">hello following table lists hello amount of time it takes for a detection type tooshow up in a related report:</span></span>

| <span data-ttu-id="0dd57-159">偵測類型</span><span class="sxs-lookup"><span data-stu-id="0dd57-159">Detection Type</span></span> | <span data-ttu-id="0dd57-160">報告延遲</span><span class="sxs-lookup"><span data-stu-id="0dd57-160">Reporting Latency</span></span> |
| --- | --- |
| <span data-ttu-id="0dd57-161">即時</span><span class="sxs-lookup"><span data-stu-id="0dd57-161">Real-time</span></span> | <span data-ttu-id="0dd57-162">5 too10 分鐘</span><span class="sxs-lookup"><span data-stu-id="0dd57-162">5 too10 minutes</span></span> |
| <span data-ttu-id="0dd57-163">離線</span><span class="sxs-lookup"><span data-stu-id="0dd57-163">Offline</span></span> | <span data-ttu-id="0dd57-164">2 too4 小時</span><span class="sxs-lookup"><span data-stu-id="0dd57-164">2 too4 hours</span></span> |


<span data-ttu-id="0dd57-165">Azure Active Directory 偵測到 hello 風險事件類型，hello 偵測類型為：</span><span class="sxs-lookup"><span data-stu-id="0dd57-165">For hello risk event types Azure Active Directory detects, hello detection types are:</span></span>

| <span data-ttu-id="0dd57-166">風險事件類型</span><span class="sxs-lookup"><span data-stu-id="0dd57-166">Risk Event Type</span></span> | <span data-ttu-id="0dd57-167">偵測類型</span><span class="sxs-lookup"><span data-stu-id="0dd57-167">Detection Type</span></span> |
| :-- | --- | 
| [<span data-ttu-id="0dd57-168">認證外洩的使用者</span><span class="sxs-lookup"><span data-stu-id="0dd57-168">Users with leaked credentials</span></span>](#leaked-credentials) | <span data-ttu-id="0dd57-169">離線</span><span class="sxs-lookup"><span data-stu-id="0dd57-169">Offline</span></span> |
| [<span data-ttu-id="0dd57-170">從匿名 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="0dd57-170">Sign-ins from anonymous IP addresses</span></span>](#sign-ins-from-anonymous-ip-addresses) | <span data-ttu-id="0dd57-171">即時</span><span class="sxs-lookup"><span data-stu-id="0dd57-171">Real-time</span></span> |
| [<span data-ttu-id="0dd57-172">不可能的旅遊 tooatypical 位置</span><span class="sxs-lookup"><span data-stu-id="0dd57-172">Impossible travel tooatypical locations</span></span>](#impossible-travel-to-atypical-locations) | <span data-ttu-id="0dd57-173">離線</span><span class="sxs-lookup"><span data-stu-id="0dd57-173">Offline</span></span> |
| [<span data-ttu-id="0dd57-174">從不熟悉的位置登入</span><span class="sxs-lookup"><span data-stu-id="0dd57-174">Sign-ins from unfamiliar locations</span></span>](#sign-in-from-unfamiliar-locations) | <span data-ttu-id="0dd57-175">即時</span><span class="sxs-lookup"><span data-stu-id="0dd57-175">Real-time</span></span> |
| [<span data-ttu-id="0dd57-176">從受感染的裝置登入</span><span class="sxs-lookup"><span data-stu-id="0dd57-176">Sign-ins from infected devices</span></span>](#sign-ins-from-infected-devices) | <span data-ttu-id="0dd57-177">離線</span><span class="sxs-lookup"><span data-stu-id="0dd57-177">Offline</span></span> |
| [<span data-ttu-id="0dd57-178">從具有可疑活動的 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="0dd57-178">Sign-ins from IP addresses with suspicious activity</span></span>](#sign-ins-from-ip-addresses-with-suspicious-activity) | <span data-ttu-id="0dd57-179">離線</span><span class="sxs-lookup"><span data-stu-id="0dd57-179">Offline</span></span>|


## <a name="risk-level"></a><span data-ttu-id="0dd57-180">風險層級</span><span class="sxs-lookup"><span data-stu-id="0dd57-180">Risk level</span></span>

<span data-ttu-id="0dd57-181">hello 風險層級屬性的風險事件是 hello 嚴重性和 hello 信賴度的風險事件的指標 （高、 中或低）。</span><span class="sxs-lookup"><span data-stu-id="0dd57-181">hello risk level property of a risk event is an indicator (High, Medium, or Low) for hello severity and hello confidence of a risk event.</span></span> <span data-ttu-id="0dd57-182">這個屬性可協助您您必須採取 tooprioritize hello 動作。</span><span class="sxs-lookup"><span data-stu-id="0dd57-182">This property helps you tooprioritize hello actions you must take.</span></span> 

<span data-ttu-id="0dd57-183">hello hello 風險事件嚴重性的身分識別洩漏預測工具以表示 hello hello 訊號強度。</span><span class="sxs-lookup"><span data-stu-id="0dd57-183">hello severity of hello risk event represents hello strength of hello signal as a predictor of identity compromise.</span></span>  
<span data-ttu-id="0dd57-184">hello 信心是 hello 可能性誤判的指標。</span><span class="sxs-lookup"><span data-stu-id="0dd57-184">hello confidence is an indicator for hello possibility of false positives.</span></span> 

<span data-ttu-id="0dd57-185">例如，</span><span class="sxs-lookup"><span data-stu-id="0dd57-185">For example,</span></span> 

* <span data-ttu-id="0dd57-186">**高**：高信賴度和高嚴重性風險事件。</span><span class="sxs-lookup"><span data-stu-id="0dd57-186">**High**: High confidence and high severity risk event.</span></span> <span data-ttu-id="0dd57-187">這些事件是強式的指標，hello 使用者的身分識別已遭洩漏，，和任何受影響的使用者帳戶應該立即進行補救。</span><span class="sxs-lookup"><span data-stu-id="0dd57-187">These events are strong indicators that hello user’s identity has been compromised, and any user accounts impacted should be remediated immediately.</span></span>

* <span data-ttu-id="0dd57-188">**中**：高嚴重性，但信賴度較低的風險事件，或反之亦然。</span><span class="sxs-lookup"><span data-stu-id="0dd57-188">**Medium**: High severity, but lower confidence risk event, or vice versa.</span></span> <span data-ttu-id="0dd57-189">這些事件具有潛在風險，而且應該補救任何受影響的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="0dd57-189">These events are potentially risky, and any user accounts impacted should be remediated.</span></span>

* <span data-ttu-id="0dd57-190">**低**：低信賴度和低嚴重性風險事件。</span><span class="sxs-lookup"><span data-stu-id="0dd57-190">**Low**: Low confidence and low severity risk event.</span></span> <span data-ttu-id="0dd57-191">此事件可能不需要立即採取行動，但是結合其他風險的事件，則可能會受到強式表示 hello 身分識別提供。</span><span class="sxs-lookup"><span data-stu-id="0dd57-191">This event may not require an immediate action, but when combined with other risk events, may provide a strong indication that hello identity is compromised.</span></span>

![風險層級](./media/active-directory-reporting-risk-events/01.png)

### <a name="leaked-credentials"></a><span data-ttu-id="0dd57-193">認證外洩</span><span class="sxs-lookup"><span data-stu-id="0dd57-193">Leaked credentials</span></span>

<span data-ttu-id="0dd57-194">外洩風險事件分類為認證**高**，因為它們提供清楚 hello 使用者名稱和密碼是可用 tooan 攻擊者的指示。</span><span class="sxs-lookup"><span data-stu-id="0dd57-194">Leaked credentials risk events are classified as a **High**, because they provide a clear indication that hello user name and password are available tooan attacker.</span></span>

### <a name="sign-ins-from-anonymous-ip-addresses"></a><span data-ttu-id="0dd57-195">從匿名 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="0dd57-195">Sign-ins from anonymous IP addresses</span></span>

<span data-ttu-id="0dd57-196">這個風險事件類型的 hello 風險層級是**媒體**因為匿名 IP 位址不是強式帳戶遭到入侵的指示。</span><span class="sxs-lookup"><span data-stu-id="0dd57-196">hello risk level for this risk event type is **Medium** because an anonymous IP address is not a strong indication of an account compromise.</span></span>  
<span data-ttu-id="0dd57-197">我們建議您立即連絡 hello 使用者 tooverify，如同使用匿名 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0dd57-197">We recommend that you immediately contact hello user tooverify if they were using anonymous IP addresses.</span></span>


### <a name="impossible-travel-tooatypical-locations"></a><span data-ttu-id="0dd57-198">不可能的旅遊 tooatypical 位置</span><span class="sxs-lookup"><span data-stu-id="0dd57-198">Impossible travel tooatypical locations</span></span>

<span data-ttu-id="0dd57-199">不可能的旅遊通常是很好的指標，駭客已能 toosuccessfully 登入。</span><span class="sxs-lookup"><span data-stu-id="0dd57-199">Impossible travel is usually a good indicator that a hacker was able toosuccessfully sign-in.</span></span> <span data-ttu-id="0dd57-200">不過，使用新的裝置，還是使用通常不是由 hello 組織中其他使用者的 VPN 旅途使用者，可能會發生 false 誤判。</span><span class="sxs-lookup"><span data-stu-id="0dd57-200">However, false-positives may occur when a user is traveling using a new device or using a VPN that is typically not used by other users in hello organization.</span></span> <span data-ttu-id="0dd57-201">False 誤判的另一個來源是不正確地為用戶端 Ip 時，可能會提供給 hello 外觀傳遞伺服器 Ip 的應用程式的登入裝載 hello 其中該應用程式的後端的資料中心發生 （這些通常是 Microsoft 資料中心，這可能會產生 hello 外觀的登入正在進行中，從 Microsoft 所擁有的 IP 位址)。</span><span class="sxs-lookup"><span data-stu-id="0dd57-201">Another source of false-positives is applications that incorrectly pass server IPs as client IPs, which may give hello appearance of sign-ins taking place from hello data center where that application’s back-end is hosted (often these are Microsoft datacenters, which may give hello appearance of sign-ins taking place from Microsoft owned IP addresses).</span></span> <span data-ttu-id="0dd57-202">因為這些假象，而這個風險事件 hello 風險層級是**媒體**。</span><span class="sxs-lookup"><span data-stu-id="0dd57-202">As a result of these false-positives, hello risk level for this risk event is **Medium**.</span></span>

> [!TIP]
> <span data-ttu-id="0dd57-203">您可以減少這個風險事件類型的報告 false positves 的 hello 數量設定[名為位置](active-directory-named-locations.md)。</span><span class="sxs-lookup"><span data-stu-id="0dd57-203">You can reduce hello amount of reported false-positves for this risk event type by configuring [named locations](active-directory-named-locations.md).</span></span> 

### <a name="sign-in-from-unfamiliar-locations"></a><span data-ttu-id="0dd57-204">從不熟悉的位置登入</span><span class="sxs-lookup"><span data-stu-id="0dd57-204">Sign-in from unfamiliar locations</span></span>

<span data-ttu-id="0dd57-205">不熟悉的位置可提供強式表示攻擊者可以 toouse 遭竊的身分識別。</span><span class="sxs-lookup"><span data-stu-id="0dd57-205">Unfamiliar locations can provide a strong indication that an attacker is able toouse a stolen identity.</span></span> <span data-ttu-id="0dd57-206">當使用者正在移動、試用新裝置或使用新的 VPN 時，可能會發生誤判。</span><span class="sxs-lookup"><span data-stu-id="0dd57-206">False-positives may occur when a user is traveling, is trying out a new device, or is using a new VPN.</span></span> <span data-ttu-id="0dd57-207">由於這些誤判 hello 風險層級，此事件類型是**媒體**。</span><span class="sxs-lookup"><span data-stu-id="0dd57-207">As a result of these false positives, hello risk level for this event type is **Medium**.</span></span>

### <a name="sign-ins-from-infected-devices"></a><span data-ttu-id="0dd57-208">從受感染的裝置登入</span><span class="sxs-lookup"><span data-stu-id="0dd57-208">Sign-ins from infected devices</span></span>

<span data-ttu-id="0dd57-209">此風險事件可識別 IP 位址，而不是使用者裝置。</span><span class="sxs-lookup"><span data-stu-id="0dd57-209">This risk event identifies IP addresses, not user devices.</span></span> <span data-ttu-id="0dd57-210">如果數個裝置位於單一 IP 位址，且只有一些會受 bot 網路，請從其他裝置的登入我的觸發程序此事件不必要地，即 hello 原因來分類此風險事件做為**低**。</span><span class="sxs-lookup"><span data-stu-id="0dd57-210">If several devices are behind a single IP address, and only some are controlled by a bot network, sign-ins from other devices my trigger this event unnecessarily, which is hello reason for classifying this risk event as **Low**.</span></span>  

<span data-ttu-id="0dd57-211">我們建議您連絡 hello 使用者並掃描所有 hello 使用者的裝置。</span><span class="sxs-lookup"><span data-stu-id="0dd57-211">We recommend that you contact hello user and scan all hello user's devices.</span></span> <span data-ttu-id="0dd57-212">它也是可能感染使用者的個人裝置，或如先前所述，有其他人已使用受感染的裝置 hello 從相同 IP 位址以 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="0dd57-212">It is also possible that a user's personal device is infected, or as mentioned earlier, that someone else was using an infected device from hello same IP address as hello user.</span></span> <span data-ttu-id="0dd57-213">受感染的裝置通常會受到防毒軟體尚未識別，也可能表示為不正確的使用者習慣可能造成 hello 裝置 toobecome 感染的惡意程式碼。</span><span class="sxs-lookup"><span data-stu-id="0dd57-213">Infected devices are often infected by malware that have not yet been identified by anti-virus software, and may also indicate as bad user habits that may have caused hello device toobecome infected.</span></span>

<span data-ttu-id="0dd57-214">如需有關如何 tooaddress 惡意程式碼的感染項目，請參閱 hello[惡意程式碼防護中心](http://go.microsoft.com/fwlink/?linkid=335773&clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="0dd57-214">For more information about how tooaddress malware infections, see hello [Malware Protection Center](http://go.microsoft.com/fwlink/?linkid=335773&clcid=0x409).</span></span>


### <a name="sign-ins-from-ip-addresses-with-suspicious-activity"></a><span data-ttu-id="0dd57-215">從具有可疑活動的 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="0dd57-215">Sign-ins from IP addresses with suspicious activity</span></span>

<span data-ttu-id="0dd57-216">我們建議您連絡 hello 使用者 tooverify，如果它們實際用來登入已標記為可疑的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0dd57-216">We recommend that you contact hello user tooverify if they actually signed in from an IP address that was marked as suspicious.</span></span> <span data-ttu-id="0dd57-217">hello 風險層級，此事件類型是"**媒體**"因為數個裝置可能在後方 hello 相同的 IP 位址，而只對某些可能會負責 hello 可疑的活動。</span><span class="sxs-lookup"><span data-stu-id="0dd57-217">hello risk level for this event type is “**Medium**” because several devices may be behind hello same IP address, while only some may be responsible for hello suspicious activity.</span></span> 


 
## <a name="next-steps"></a><span data-ttu-id="0dd57-218">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0dd57-218">Next steps</span></span>

<span data-ttu-id="0dd57-219">風險事件是 hello foundation 來保護您的 Azure AD 身分識別。</span><span class="sxs-lookup"><span data-stu-id="0dd57-219">Risk events are hello foundation for protecting your Azure AD's identities.</span></span> <span data-ttu-id="0dd57-220">Azure AD 目前可以偵測六種風險事件：</span><span class="sxs-lookup"><span data-stu-id="0dd57-220">Azure AD can currently detect six risk events:</span></span> 


| <span data-ttu-id="0dd57-221">風險事件類型</span><span class="sxs-lookup"><span data-stu-id="0dd57-221">Risk Event Type</span></span> | <span data-ttu-id="0dd57-222">風險層級</span><span class="sxs-lookup"><span data-stu-id="0dd57-222">Risk Level</span></span> | <span data-ttu-id="0dd57-223">偵測類型</span><span class="sxs-lookup"><span data-stu-id="0dd57-223">Detection Type</span></span> |
| :-- | --- | --- |
| [<span data-ttu-id="0dd57-224">認證外洩的使用者</span><span class="sxs-lookup"><span data-stu-id="0dd57-224">Users with leaked credentials</span></span>](#leaked-credentials) | <span data-ttu-id="0dd57-225">高</span><span class="sxs-lookup"><span data-stu-id="0dd57-225">High</span></span> | <span data-ttu-id="0dd57-226">離線</span><span class="sxs-lookup"><span data-stu-id="0dd57-226">Offline</span></span> |
| [<span data-ttu-id="0dd57-227">從匿名 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="0dd57-227">Sign-ins from anonymous IP addresses</span></span>](#sign-ins-from-anonymous-ip-addresses) | <span data-ttu-id="0dd57-228">中型</span><span class="sxs-lookup"><span data-stu-id="0dd57-228">Medium</span></span> | <span data-ttu-id="0dd57-229">即時</span><span class="sxs-lookup"><span data-stu-id="0dd57-229">Real-time</span></span> |
| [<span data-ttu-id="0dd57-230">不可能的旅遊 tooatypical 位置</span><span class="sxs-lookup"><span data-stu-id="0dd57-230">Impossible travel tooatypical locations</span></span>](#impossible-travel-to-atypical-locations) | <span data-ttu-id="0dd57-231">中型</span><span class="sxs-lookup"><span data-stu-id="0dd57-231">Medium</span></span> | <span data-ttu-id="0dd57-232">離線</span><span class="sxs-lookup"><span data-stu-id="0dd57-232">Offline</span></span> |
| [<span data-ttu-id="0dd57-233">從不熟悉的位置登入</span><span class="sxs-lookup"><span data-stu-id="0dd57-233">Sign-ins from unfamiliar locations</span></span>](#sign-in-from-unfamiliar-locations) | <span data-ttu-id="0dd57-234">中型</span><span class="sxs-lookup"><span data-stu-id="0dd57-234">Medium</span></span> | <span data-ttu-id="0dd57-235">即時</span><span class="sxs-lookup"><span data-stu-id="0dd57-235">Real-time</span></span> |
| [<span data-ttu-id="0dd57-236">從受感染的裝置登入</span><span class="sxs-lookup"><span data-stu-id="0dd57-236">Sign-ins from infected devices</span></span>](#sign-ins-from-infected-devices) | <span data-ttu-id="0dd57-237">低</span><span class="sxs-lookup"><span data-stu-id="0dd57-237">Low</span></span> | <span data-ttu-id="0dd57-238">離線</span><span class="sxs-lookup"><span data-stu-id="0dd57-238">Offline</span></span> |
| [<span data-ttu-id="0dd57-239">從具有可疑活動的 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="0dd57-239">Sign-ins from IP addresses with suspicious activity</span></span>](#sign-ins-from-ip-addresses-with-suspicious-activity) | <span data-ttu-id="0dd57-240">中型</span><span class="sxs-lookup"><span data-stu-id="0dd57-240">Medium</span></span> | <span data-ttu-id="0dd57-241">離線</span><span class="sxs-lookup"><span data-stu-id="0dd57-241">Offline</span></span>|

<span data-ttu-id="0dd57-242">可以從何處 hello 偵測到您的環境中的風險事件？</span><span class="sxs-lookup"><span data-stu-id="0dd57-242">Where can you find hello risk events that have been detected in your environment?</span></span>
<span data-ttu-id="0dd57-243">您可以在兩個地方檢閱已報告的風險事件：</span><span class="sxs-lookup"><span data-stu-id="0dd57-243">There are two places where you review reported risk events:</span></span>

 - <span data-ttu-id="0dd57-244">**Azure AD 報告** - 風險事件屬於 Azure AD 的安全性報表。</span><span class="sxs-lookup"><span data-stu-id="0dd57-244">**Azure AD reporting** - Risk events are part of Azure AD's security reports.</span></span> <span data-ttu-id="0dd57-245">如需詳細資訊，請參閱 hello[風險安全性報告使用者](active-directory-reporting-security-user-at-risk.md)和 hello[危險的登入安全性報告](active-directory-reporting-security-risky-sign-ins.md)。</span><span class="sxs-lookup"><span data-stu-id="0dd57-245">For more details, see hello [users at risk security report](active-directory-reporting-security-user-at-risk.md) and hello [risky sign-ins security report](active-directory-reporting-security-risky-sign-ins.md).</span></span>

 - <span data-ttu-id="0dd57-246">**Azure AD Identity Protection** - 風險事件也屬於 [Azure Active Directory Identity Protection](active-directory-identityprotection.md) 的報告功能。</span><span class="sxs-lookup"><span data-stu-id="0dd57-246">**Azure AD Identity Protection** - Risk events are also part of [Azure Active Directory Identity Protection's](active-directory-identityprotection.md) reporting capabilities.</span></span>
    

<span data-ttu-id="0dd57-247">Hello 偵測的風險事件已代表保護您的身分識別的重要層面，而您也可以手動加以解決，或甚至會藉由設定條件式存取原則實作自動化的回應 hello 選項 tooeither。</span><span class="sxs-lookup"><span data-stu-id="0dd57-247">While hello detection of risk events already represents an important aspect of protecting your identities, you also have hello option tooeither manually address them or even implement automated responses by configuring conditional access policies.</span></span> <span data-ttu-id="0dd57-248">如需詳細資料，請參閱 [Azure Active Directory Identity Protection](active-directory-identityprotection.md)。</span><span class="sxs-lookup"><span data-stu-id="0dd57-248">For more details, see of [Azure Active Directory Identity Protection's](active-directory-identityprotection.md).</span></span>
 
