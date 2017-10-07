---
title: "Azure Active Directory B2C：Multi-Factor Authentication | Microsoft Docs"
description: "如何 tooenable 消費者導向應用程式中的 Multi-factor Authentication 保護 Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 53ef86c4-1586-45dc-9952-dbbd62f68afc
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 29beb1e6ab5d8ab5a65f9c5c068d9e71c60418dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-enable-multi-factor-authentication-in-your-consumer-facing-applications"></a><span data-ttu-id="5189a-103">Azure Active Directory B2C：在取用者導向應用程式中啟用 Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="5189a-103">Azure Active Directory B2C: Enable Multi-Factor Authentication in your consumer-facing applications</span></span>
<span data-ttu-id="5189a-104">直接與整合 azure Active Directory (Azure AD) B2C [Azure Multi-factor Authentication](../multi-factor-authentication/multi-factor-authentication.md) ，讓您可以在消費者導向應用程式中新增第二層的安全性 toosign 向上鍵和登入體驗。</span><span class="sxs-lookup"><span data-stu-id="5189a-104">Azure Active Directory (Azure AD) B2C integrates directly with [Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md) so that you can add a second layer of security toosign-up and sign-in experiences in your consumer-facing applications.</span></span> <span data-ttu-id="5189a-105">您連一行程式碼都不用寫，即可達成此目標。</span><span class="sxs-lookup"><span data-stu-id="5189a-105">And you can do this without writing a single line of code.</span></span> <span data-ttu-id="5189a-106">目前我們支援撥打電話與簡訊驗證。</span><span class="sxs-lookup"><span data-stu-id="5189a-106">Currently we support phone call and text message verification.</span></span> <span data-ttu-id="5189a-107">如果您已經建立註冊和登入原則，您仍然可以啟用 Multi-Factor Authentication。</span><span class="sxs-lookup"><span data-stu-id="5189a-107">If you already created sign-up and sign-in policies, you can still enable Multi-Factor Authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="5189a-108">Multi-Factor Authentication 也可以在建立註冊和登入原則時啟用，而非單靠編輯現有原則來啟用。</span><span class="sxs-lookup"><span data-stu-id="5189a-108">Multi-Factor Authentication can also be enabled when you create sign-up and sign-in policies, not just by editing existing policies.</span></span>
> 
> 

<span data-ttu-id="5189a-109">這項功能可協助應用程式處理 hello 如下的案例：</span><span class="sxs-lookup"><span data-stu-id="5189a-109">This feature helps applications handle scenarios such as hello following:</span></span>

* <span data-ttu-id="5189a-110">您不需要 Multi-factor Authentication tooaccess 一個應用程式，但您需要 tooaccess 另一個。</span><span class="sxs-lookup"><span data-stu-id="5189a-110">You don't require Multi-Factor Authentication tooaccess one application, but you do require it tooaccess another one.</span></span> <span data-ttu-id="5189a-111">例如，hello 取用者可以登入自動保險應用程式與社交或本機帳戶，但必須驗證 hello 電話號碼，才能存取 hello 家用保險應用程式中註冊 hello 相同目錄。</span><span class="sxs-lookup"><span data-stu-id="5189a-111">For example, hello consumer can sign into an auto insurance application with a social or local account, but must verify hello phone number before accessing hello home insurance application registered in hello same directory.</span></span>
* <span data-ttu-id="5189a-112">您不需要 Multi-factor Authentication tooaccess 應用程式一般情況下，但您需要 tooaccess hello 機密部分內。</span><span class="sxs-lookup"><span data-stu-id="5189a-112">You don't require Multi-Factor Authentication tooaccess an application in general, but you do require it tooaccess hello sensitive portions within it.</span></span> <span data-ttu-id="5189a-113">比方說，hello 取用者可以登入 tooa 銀行應用程式與社交或本機帳戶，請檢查帳戶餘額，但必須驗證 hello 電話號碼，然後再嘗試連線傳輸。</span><span class="sxs-lookup"><span data-stu-id="5189a-113">For example, hello consumer can sign in tooa banking application with a social or local account and check account balance, but must verify hello phone number before attempting a wire transfer.</span></span>

## <a name="modify-your-sign-up-policy-tooenable-multi-factor-authentication"></a><span data-ttu-id="5189a-114">修改您的註冊原則 tooenable 多重要素驗證</span><span class="sxs-lookup"><span data-stu-id="5189a-114">Modify your sign-up policy tooenable Multi-Factor Authentication</span></span>
1. <span data-ttu-id="5189a-115">[遵循這些步驟 toonavigate toohello B2C 功能刀鋒視窗上 hello Azure 入口網站](active-directory-b2c-app-registration.md#navigate-to-b2c-settings)。</span><span class="sxs-lookup"><span data-stu-id="5189a-115">[Follow these steps toonavigate toohello B2C features blade on hello Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="5189a-116">按一下 [註冊原則] 。</span><span class="sxs-lookup"><span data-stu-id="5189a-116">Click **Sign-up policies**.</span></span>
3. <span data-ttu-id="5189a-117">按一下 註冊原則 (例如，"B2C_1_SiUp 」) tooopen 它。</span><span class="sxs-lookup"><span data-stu-id="5189a-117">Click your sign-up policy (for example, "B2C_1_SiUp") tooopen it.</span></span>
4. <span data-ttu-id="5189a-118">按一下**multi-factor authentication**開啟 hello**狀態**太**ON**。</span><span class="sxs-lookup"><span data-stu-id="5189a-118">Click **Multi-factor authentication** and turn hello **State** too**ON**.</span></span> <span data-ttu-id="5189a-119">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="5189a-119">Click **OK**.</span></span>
5. <span data-ttu-id="5189a-120">按一下**儲存**在 hello hello 刀鋒視窗最上方。</span><span class="sxs-lookup"><span data-stu-id="5189a-120">Click **Save** at hello top of hello blade.</span></span>

<span data-ttu-id="5189a-121">您可以使用 hello 「 立即執行 」 功能 hello 原則 tooverify hello 取用者經驗。</span><span class="sxs-lookup"><span data-stu-id="5189a-121">You can use hello "Run now" feature on hello policy tooverify hello consumer experience.</span></span> <span data-ttu-id="5189a-122">確認 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="5189a-122">Confirm hello following:</span></span>

<span data-ttu-id="5189a-123">Hello Multi-factor Authentication 步驟之前，取得您目錄中建立取用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="5189a-123">A consumer account gets created in your directory before hello Multi-Factor Authentication step occurs.</span></span> <span data-ttu-id="5189a-124">Hello 步驟期間 hello 取用者會要求他或她的電話號碼，並確認 tooprovide。</span><span class="sxs-lookup"><span data-stu-id="5189a-124">During hello step, hello consumer is asked tooprovide his or her phone number and verify it.</span></span> <span data-ttu-id="5189a-125">如果驗證成功時，則會附加 hello 電話號碼 toohello 消費者帳戶，供日後使用。</span><span class="sxs-lookup"><span data-stu-id="5189a-125">If verification is successful, hello phone number is attached toohello consumer account for later use.</span></span> <span data-ttu-id="5189a-126">即使 hello 取用者取消，或卸除，他可要求的 tooverify 電話號碼再次期間 hello 下一次登入時 （使用多因素驗證啟用）。</span><span class="sxs-lookup"><span data-stu-id="5189a-126">Even if hello consumer cancels or drops out, he or she can be asked tooverify a phone number again during hello next sign-in (with Multi-Factor Authentication enabled).</span></span>

## <a name="modify-your-sign-in-policy-tooenable-multi-factor-authentication"></a><span data-ttu-id="5189a-127">修改您的登入原則 tooenable 多重要素驗證</span><span class="sxs-lookup"><span data-stu-id="5189a-127">Modify your sign-in policy tooenable Multi-Factor Authentication</span></span>
1. <span data-ttu-id="5189a-128">[遵循這些步驟 toonavigate toohello B2C 功能刀鋒視窗上 hello Azure 入口網站](active-directory-b2c-app-registration.md#navigate-to-b2c-settings)。</span><span class="sxs-lookup"><span data-stu-id="5189a-128">[Follow these steps toonavigate toohello B2C features blade on hello Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="5189a-129">按一下 [登入原則] 。</span><span class="sxs-lookup"><span data-stu-id="5189a-129">Click **Sign-in policies**.</span></span>
3. <span data-ttu-id="5189a-130">按一下 登入的原則 (例如，"B2C_1_SiIn 」) tooopen 它。</span><span class="sxs-lookup"><span data-stu-id="5189a-130">Click your sign-in policy (for example, "B2C_1_SiIn") tooopen it.</span></span> <span data-ttu-id="5189a-131">按一下**編輯**在 hello hello 刀鋒視窗最上方。</span><span class="sxs-lookup"><span data-stu-id="5189a-131">Click **Edit** at hello top of hello blade.</span></span>
4. <span data-ttu-id="5189a-132">按一下**multi-factor authentication**開啟 hello**狀態**太**ON**。</span><span class="sxs-lookup"><span data-stu-id="5189a-132">Click **Multi-factor authentication** and turn hello **State** too**ON**.</span></span> <span data-ttu-id="5189a-133">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="5189a-133">Click **OK**.</span></span>
5. <span data-ttu-id="5189a-134">按一下**儲存**在 hello hello 刀鋒視窗最上方。</span><span class="sxs-lookup"><span data-stu-id="5189a-134">Click **Save** at hello top of hello blade.</span></span>

<span data-ttu-id="5189a-135">您可以使用 hello 「 立即執行 」 功能 hello 原則 tooverify hello 取用者經驗。</span><span class="sxs-lookup"><span data-stu-id="5189a-135">You can use hello "Run now" feature on hello policy tooverify hello consumer experience.</span></span> <span data-ttu-id="5189a-136">確認 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="5189a-136">Confirm hello following:</span></span>

<span data-ttu-id="5189a-137">Hello 取用者使用登入 （社交或本機帳戶），如果已驗證的電話號碼附加 toohello 消費者帳戶，他或她將被要求 tooverify 它。</span><span class="sxs-lookup"><span data-stu-id="5189a-137">When hello consumer signs in (using a social or local account), if a verified phone number is attached toohello consumer account, he or she is asked tooverify it.</span></span> <span data-ttu-id="5189a-138">如果沒有電話號碼已附加，hello 取用者要求 tooprovide 其中一個，並確認它。</span><span class="sxs-lookup"><span data-stu-id="5189a-138">If no phone number is attached, hello consumer is asked tooprovide one and verify it.</span></span> <span data-ttu-id="5189a-139">在驗證成功，附加 hello 電話號碼 toohello 消費者帳戶，供日後使用。</span><span class="sxs-lookup"><span data-stu-id="5189a-139">On successful verification, hello phone number is attached toohello consumer account for later use.</span></span>

## <a name="multi-factor-authentication-on-other-policies"></a><span data-ttu-id="5189a-140">其他原則上的 Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="5189a-140">Multi-Factor Authentication on other policies</span></span>
<span data-ttu-id="5189a-141">所描述的上述的註冊和登入原則，所以也可能 tooenable 上註冊的多重要素驗證或原則登入和密碼重設原則。</span><span class="sxs-lookup"><span data-stu-id="5189a-141">As described for sign-up & sign-in policies above, it is also possible tooenable multi-factor authentication on sign-up or sign-in policies and password reset policies.</span></span> <span data-ttu-id="5189a-142">很快即可用於設定檔編輯原則。</span><span class="sxs-lookup"><span data-stu-id="5189a-142">It will be available soon on profile editing policies.</span></span>

