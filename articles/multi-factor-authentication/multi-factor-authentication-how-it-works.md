---
title: "Azure Multi-Factor Authentication -它的作用"
description: "Azure Multi-Factor Authentication 有助於保護對資料與應用程式的存取，同時可以滿足使用者對簡單登入程序的需求。 它藉由要求第二種形式的驗證提供額外的安全性，並透過一系列簡單的驗證選項提供增強式驗證。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d14db902-9afe-4fca-b3a5-4bd54b3d8ec5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 6fee02885cc76b3a4fdad11e8702f623d6fe6597
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-azure-multi-factor-authentication-works"></a><span data-ttu-id="09da4-104">Azure Multi-Factor Authentication 的作用</span><span class="sxs-lookup"><span data-stu-id="09da4-104">How Azure Multi-Factor Authentication works</span></span>
<span data-ttu-id="09da4-105">雙步驟驗證的安全性仰賴其分層方法。</span><span class="sxs-lookup"><span data-stu-id="09da4-105">The security of two-step verification lies in its layered approach.</span></span> <span data-ttu-id="09da4-106">使用多重驗證因素會為攻擊者帶來相當程度的挑戰。</span><span class="sxs-lookup"><span data-stu-id="09da4-106">Compromising multiple authentication factors presents a significant challenge for attackers.</span></span> <span data-ttu-id="09da4-107">即使攻擊者試圖打探使用者的密碼，在不持有信任裝置的情況下便沒有任何意義。</span><span class="sxs-lookup"><span data-stu-id="09da4-107">Even if an attacker manages to learn the user's password, it is useless without also having possession of the trusted device.</span></span> 

![Proofup](./media/multi-factor-authentication-how-it-works/howitworks.png)

<span data-ttu-id="09da4-109">Azure Multi-Factor Authentication 有助於保護對資料與應用程式的存取，同時可以滿足使用者對簡單登入程序的需求。</span><span class="sxs-lookup"><span data-stu-id="09da4-109">Azure Multi-Factor Authentication helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span></span>  <span data-ttu-id="09da4-110">它藉由要求第二種形式的驗證提供額外的安全性，並透過一系列簡單的驗證選項提供增強式驗證。</span><span class="sxs-lookup"><span data-stu-id="09da4-110">It provides additional security by requiring a second form of authentication and delivers strong authentication via a range of easy verification options.</span></span>


## <a name="methods-available-for-two-step-verification"></a><span data-ttu-id="09da4-111">雙步驟驗證適用的方法</span><span class="sxs-lookup"><span data-stu-id="09da4-111">Methods available for two-step verification</span></span>
<span data-ttu-id="09da4-112">當使用者登入時，系統會將額外的驗證傳送給使用者。</span><span class="sxs-lookup"><span data-stu-id="09da4-112">When a user signs in, an additional verification is sent to the user.</span></span>  <span data-ttu-id="09da4-113">以下是適用於這個第二次驗證的方法清單。</span><span class="sxs-lookup"><span data-stu-id="09da4-113">The following are a list of methods that can be used for this second verification.</span></span>

| <span data-ttu-id="09da4-114">驗證方法</span><span class="sxs-lookup"><span data-stu-id="09da4-114">Verification Method</span></span> | <span data-ttu-id="09da4-115">說明</span><span class="sxs-lookup"><span data-stu-id="09da4-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="09da4-116">撥打電話</span><span class="sxs-lookup"><span data-stu-id="09da4-116">Phone call</span></span> |<span data-ttu-id="09da4-117">撥打一通電話到使用者所註冊的電話號碼。</span><span class="sxs-lookup"><span data-stu-id="09da4-117">A call is placed to a user’s registered phone.</span></span> <span data-ttu-id="09da4-118">使用者視需要輸入 PIN，然後按下 # 鍵。</span><span class="sxs-lookup"><span data-stu-id="09da4-118">The user enters a PIN if necessary then presses the # key.</span></span> |
| <span data-ttu-id="09da4-119">簡訊</span><span class="sxs-lookup"><span data-stu-id="09da4-119">Text message</span></span> |<span data-ttu-id="09da4-120">傳送含六位數代碼的簡訊到使用者的手機。</span><span class="sxs-lookup"><span data-stu-id="09da4-120">A text message is sent to a user’s mobile phone with a six-digit code.</span></span> <span data-ttu-id="09da4-121">使用者在登入頁面輸入此代碼。</span><span class="sxs-lookup"><span data-stu-id="09da4-121">The user enters this code on the sign-in page.</span></span> |
| <span data-ttu-id="09da4-122">行動應用程式通知</span><span class="sxs-lookup"><span data-stu-id="09da4-122">Mobile app notification</span></span> |<span data-ttu-id="09da4-123">傳送驗證要求到使用者的智慧型手機。</span><span class="sxs-lookup"><span data-stu-id="09da4-123">A verification request is sent to a user’s smart phone.</span></span> <span data-ttu-id="09da4-124">使用者視需要輸入 PIN，然後在行動裝置應用程式上選取 [驗證]。</span><span class="sxs-lookup"><span data-stu-id="09da4-124">The user enters a PIN if necessary then selects **Verify** on the mobile app.</span></span> |
| <span data-ttu-id="09da4-125">行動應用程式驗證碼</span><span class="sxs-lookup"><span data-stu-id="09da4-125">Mobile app verification code</span></span> |<span data-ttu-id="09da4-126">在使用者智慧型手機上執行的行動裝置應用程式，會顯示每 30 秒就變更一次的驗證碼。</span><span class="sxs-lookup"><span data-stu-id="09da4-126">The mobile app, which is running on a user’s smart phone, displays a verification code that changes every 30 seconds.</span></span> <span data-ttu-id="09da4-127">使用者尋找最新的驗證碼，並在登入頁面上輸入。</span><span class="sxs-lookup"><span data-stu-id="09da4-127">The user finds the most recent code and enters it on the sign-in page.</span></span> |
| <span data-ttu-id="09da4-128">協力廠商 OATH 權杖</span><span class="sxs-lookup"><span data-stu-id="09da4-128">Third-party OATH tokens</span></span> | <span data-ttu-id="09da4-129">Azure Multi-Factor Authentication Server 可以設定為接受協力廠商驗證方法。</span><span class="sxs-lookup"><span data-stu-id="09da4-129">Azure Multi-Factor Authentication Server can be configured to accept third-party verification methods.</span></span> |

<span data-ttu-id="09da4-130">Azure Multi-Factor Authentication 為雲端與伺服器提供可選取的驗證方法。</span><span class="sxs-lookup"><span data-stu-id="09da4-130">Azure Multi-Factor Authentication provides selectable verification methods for both cloud and server.</span></span> <span data-ttu-id="09da4-131">您可以選擇可供使用者使用的方法：撥打電話、簡訊、應用程式通知或應用程式驗證碼。</span><span class="sxs-lookup"><span data-stu-id="09da4-131">You can choose which methods are available for your users: phone call, text, app notification, or app codes.</span></span> <span data-ttu-id="09da4-132">如需詳細資訊，請參閱 [可選取的驗證方法](multi-factor-authentication-whats-next.md#selectable-verification-methods)。</span><span class="sxs-lookup"><span data-stu-id="09da4-132">For more information, see [selectable verification methods](multi-factor-authentication-whats-next.md#selectable-verification-methods).</span></span>

## <a name="next-steps"></a><span data-ttu-id="09da4-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="09da4-133">Next steps</span></span>

- <span data-ttu-id="09da4-134">請參閱不同的 [Azure Multi-Factor Authentication 版本和耗用方法](multi-factor-authentication-versions-plans.md)</span><span class="sxs-lookup"><span data-stu-id="09da4-134">Read about the different [versions and consumption methods for Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span></span>

- <span data-ttu-id="09da4-135">選擇要[在雲端還是內部部署](multi-factor-authentication-get-started.md)部署 Azure MFA</span><span class="sxs-lookup"><span data-stu-id="09da4-135">Choose whether to deploy Azure MFA [in the cloud or on-premises](multi-factor-authentication-get-started.md)</span></span>

- <span data-ttu-id="09da4-136">閱讀[常見問題](multi-factor-authentication-faq.md)的解答</span><span class="sxs-lookup"><span data-stu-id="09da4-136">Read answers for [Frequently asked questions](multi-factor-authentication-faq.md)</span></span>