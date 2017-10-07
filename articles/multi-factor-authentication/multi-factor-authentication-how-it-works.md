---
title: "aaaAzure Multi-factor Authentication 的運作方式"
description: "Azure Multi-factor Authentication 協助保護存取 toodata 和應用程式，同時滿足簡單登入程序的使用者需求。 它藉由要求第二種形式的驗證提供額外的安全性，並透過一系列簡單的驗證選項提供增強式驗證。"
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
ms.openlocfilehash: 82f234fb86f145c42e8e56b8bdd2d61720c9ff2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-multi-factor-authentication-works"></a><span data-ttu-id="96c2e-104">Azure Multi-Factor Authentication 的作用</span><span class="sxs-lookup"><span data-stu-id="96c2e-104">How Azure Multi-Factor Authentication works</span></span>
<span data-ttu-id="96c2e-105">hello 的雙步驟驗證的安全性在於其分層方法。</span><span class="sxs-lookup"><span data-stu-id="96c2e-105">hello security of two-step verification lies in its layered approach.</span></span> <span data-ttu-id="96c2e-106">使用多重驗證因素會為攻擊者帶來相當程度的挑戰。</span><span class="sxs-lookup"><span data-stu-id="96c2e-106">Compromising multiple authentication factors presents a significant challenge for attackers.</span></span> <span data-ttu-id="96c2e-107">即使攻擊者設法 toolearn hello 使用者的密碼，它是裝置的毫無用處也不用擁有 hello 信任。</span><span class="sxs-lookup"><span data-stu-id="96c2e-107">Even if an attacker manages toolearn hello user's password, it is useless without also having possession of hello trusted device.</span></span> 

![Proofup](./media/multi-factor-authentication-how-it-works/howitworks.png)

<span data-ttu-id="96c2e-109">Azure Multi-factor Authentication 協助保護存取 toodata 和應用程式，同時滿足簡單登入程序的使用者需求。</span><span class="sxs-lookup"><span data-stu-id="96c2e-109">Azure Multi-Factor Authentication helps safeguard access toodata and applications while meeting user demand for a simple sign-in process.</span></span>  <span data-ttu-id="96c2e-110">它藉由要求第二種形式的驗證提供額外的安全性，並透過一系列簡單的驗證選項提供增強式驗證。</span><span class="sxs-lookup"><span data-stu-id="96c2e-110">It provides additional security by requiring a second form of authentication and delivers strong authentication via a range of easy verification options.</span></span>


## <a name="methods-available-for-two-step-verification"></a><span data-ttu-id="96c2e-111">雙步驟驗證適用的方法</span><span class="sxs-lookup"><span data-stu-id="96c2e-111">Methods available for two-step verification</span></span>
<span data-ttu-id="96c2e-112">當使用者登入時，額外的驗證傳送 toohello 使用者。</span><span class="sxs-lookup"><span data-stu-id="96c2e-112">When a user signs in, an additional verification is sent toohello user.</span></span>  <span data-ttu-id="96c2e-113">hello 下面是可以用於這個第二個驗證方法的清單。</span><span class="sxs-lookup"><span data-stu-id="96c2e-113">hello following are a list of methods that can be used for this second verification.</span></span>

| <span data-ttu-id="96c2e-114">驗證方法</span><span class="sxs-lookup"><span data-stu-id="96c2e-114">Verification Method</span></span> | <span data-ttu-id="96c2e-115">說明</span><span class="sxs-lookup"><span data-stu-id="96c2e-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="96c2e-116">撥打電話</span><span class="sxs-lookup"><span data-stu-id="96c2e-116">Phone call</span></span> |<span data-ttu-id="96c2e-117">通話時會 tooa 使用者已註冊的電話。</span><span class="sxs-lookup"><span data-stu-id="96c2e-117">A call is placed tooa user’s registered phone.</span></span> <span data-ttu-id="96c2e-118">hello 使用者輸入 PIN，如有必要，然後按下 hello # 鍵。</span><span class="sxs-lookup"><span data-stu-id="96c2e-118">hello user enters a PIN if necessary then presses hello # key.</span></span> |
| <span data-ttu-id="96c2e-119">簡訊</span><span class="sxs-lookup"><span data-stu-id="96c2e-119">Text message</span></span> |<span data-ttu-id="96c2e-120">Tooa 使用者的行動電話，以六位數代碼時，就會傳送簡訊。</span><span class="sxs-lookup"><span data-stu-id="96c2e-120">A text message is sent tooa user’s mobile phone with a six-digit code.</span></span> <span data-ttu-id="96c2e-121">hello 使用者 hello 登入頁面上，輸入此代碼。</span><span class="sxs-lookup"><span data-stu-id="96c2e-121">hello user enters this code on hello sign-in page.</span></span> |
| <span data-ttu-id="96c2e-122">行動應用程式通知</span><span class="sxs-lookup"><span data-stu-id="96c2e-122">Mobile app notification</span></span> |<span data-ttu-id="96c2e-123">驗證要求會傳送 tooa 使用者的智慧型手機。</span><span class="sxs-lookup"><span data-stu-id="96c2e-123">A verification request is sent tooa user’s smart phone.</span></span> <span data-ttu-id="96c2e-124">hello 使用者輸入 PIN，如有必要，以選取**確認**hello 行動裝置應用程式上。</span><span class="sxs-lookup"><span data-stu-id="96c2e-124">hello user enters a PIN if necessary then selects **Verify** on hello mobile app.</span></span> |
| <span data-ttu-id="96c2e-125">行動應用程式驗證碼</span><span class="sxs-lookup"><span data-stu-id="96c2e-125">Mobile app verification code</span></span> |<span data-ttu-id="96c2e-126">hello 行動裝置應用程式，在使用者的智慧型手機上執行，會顯示驗證碼，以變更每隔 30 秒。</span><span class="sxs-lookup"><span data-stu-id="96c2e-126">hello mobile app, which is running on a user’s smart phone, displays a verification code that changes every 30 seconds.</span></span> <span data-ttu-id="96c2e-127">hello 使用者尋找 hello 最新的程式碼，並進入 hello 登入頁面上。</span><span class="sxs-lookup"><span data-stu-id="96c2e-127">hello user finds hello most recent code and enters it on hello sign-in page.</span></span> |
| <span data-ttu-id="96c2e-128">協力廠商 OATH 權杖</span><span class="sxs-lookup"><span data-stu-id="96c2e-128">Third-party OATH tokens</span></span> | <span data-ttu-id="96c2e-129">Azure Multi-factor Authentication Server 可以設定的 tooaccept 協力廠商驗證方法。</span><span class="sxs-lookup"><span data-stu-id="96c2e-129">Azure Multi-Factor Authentication Server can be configured tooaccept third-party verification methods.</span></span> |

<span data-ttu-id="96c2e-130">Azure Multi-Factor Authentication 為雲端與伺服器提供可選取的驗證方法。</span><span class="sxs-lookup"><span data-stu-id="96c2e-130">Azure Multi-Factor Authentication provides selectable verification methods for both cloud and server.</span></span> <span data-ttu-id="96c2e-131">您可以選擇可供使用者使用的方法：撥打電話、簡訊、應用程式通知或應用程式驗證碼。</span><span class="sxs-lookup"><span data-stu-id="96c2e-131">You can choose which methods are available for your users: phone call, text, app notification, or app codes.</span></span> <span data-ttu-id="96c2e-132">如需詳細資訊，請參閱 [可選取的驗證方法](multi-factor-authentication-whats-next.md#selectable-verification-methods)。</span><span class="sxs-lookup"><span data-stu-id="96c2e-132">For more information, see [selectable verification methods](multi-factor-authentication-whats-next.md#selectable-verification-methods).</span></span>

## <a name="next-steps"></a><span data-ttu-id="96c2e-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="96c2e-133">Next steps</span></span>

- <span data-ttu-id="96c2e-134">了解不同的 hello[版本和 Azure Multi-factor Authentication 的耗用量方法](multi-factor-authentication-versions-plans.md)</span><span class="sxs-lookup"><span data-stu-id="96c2e-134">Read about hello different [versions and consumption methods for Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span></span>

- <span data-ttu-id="96c2e-135">選擇是否 toodeploy Azure MFA [hello 雲端或內部部署中](multi-factor-authentication-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="96c2e-135">Choose whether toodeploy Azure MFA [in hello cloud or on-premises](multi-factor-authentication-get-started.md)</span></span>

- <span data-ttu-id="96c2e-136">閱讀[常見問題](multi-factor-authentication-faq.md)的解答</span><span class="sxs-lookup"><span data-stu-id="96c2e-136">Read answers for [Frequently asked questions](multi-factor-authentication-faq.md)</span></span>