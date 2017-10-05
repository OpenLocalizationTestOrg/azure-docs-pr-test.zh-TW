---
title: "Azure Active Directory B2C：Multi-Factor Authentication | Microsoft Docs"
description: "如何在受 Azure Active Directory B2C 保護的取用者導向應用程式中啟用 Multi-Factor Authentication"
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
ms.openlocfilehash: 62ec48ab067cf02bc8409aca6da704a5418ec270
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-enable-multi-factor-authentication-in-your-consumer-facing-applications"></a><span data-ttu-id="3f4c7-103">Azure Active Directory B2C：在取用者導向應用程式中啟用 Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="3f4c7-103">Azure Active Directory B2C: Enable Multi-Factor Authentication in your consumer-facing applications</span></span>
<span data-ttu-id="3f4c7-104">Azure Active Directory (Azure AD) B2C 直接整合 [Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md) ，讓您能夠針對取用者導向應用程式的註冊與登入使用體驗，增添第二層安全性。</span><span class="sxs-lookup"><span data-stu-id="3f4c7-104">Azure Active Directory (Azure AD) B2C integrates directly with [Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md) so that you can add a second layer of security to sign-up and sign-in experiences in your consumer-facing applications.</span></span> <span data-ttu-id="3f4c7-105">您連一行程式碼都不用寫，即可達成此目標。</span><span class="sxs-lookup"><span data-stu-id="3f4c7-105">And you can do this without writing a single line of code.</span></span> <span data-ttu-id="3f4c7-106">目前我們支援撥打電話與簡訊驗證。</span><span class="sxs-lookup"><span data-stu-id="3f4c7-106">Currently we support phone call and text message verification.</span></span> <span data-ttu-id="3f4c7-107">如果您已經建立註冊和登入原則，您仍然可以啟用 Multi-Factor Authentication。</span><span class="sxs-lookup"><span data-stu-id="3f4c7-107">If you already created sign-up and sign-in policies, you can still enable Multi-Factor Authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="3f4c7-108">Multi-Factor Authentication 也可以在建立註冊和登入原則時啟用，而非單靠編輯現有原則來啟用。</span><span class="sxs-lookup"><span data-stu-id="3f4c7-108">Multi-Factor Authentication can also be enabled when you create sign-up and sign-in policies, not just by editing existing policies.</span></span>
> 
> 

<span data-ttu-id="3f4c7-109">此功能可協助應用程式處理諸如下列的各種案例：</span><span class="sxs-lookup"><span data-stu-id="3f4c7-109">This feature helps applications handle scenarios such as the following:</span></span>

* <span data-ttu-id="3f4c7-110">您在存取某一個應用程式時不需要 Multi-Factor Authentication，但在存取另一應用程式時需要它。</span><span class="sxs-lookup"><span data-stu-id="3f4c7-110">You don't require Multi-Factor Authentication to access one application, but you do require it to access another one.</span></span> <span data-ttu-id="3f4c7-111">例如，取用者可以使用社交或本機帳戶登入汽車保險應用程式，但必須先驗證電話號碼，才能存取同個目錄中註冊的家庭保險應用程式。</span><span class="sxs-lookup"><span data-stu-id="3f4c7-111">For example, the consumer can sign into an auto insurance application with a social or local account, but must verify the phone number before accessing the home insurance application registered in the same directory.</span></span>
* <span data-ttu-id="3f4c7-112">一般而言，您在存取應用程式時不需要 Multi-Factor Authentication，但在存取其中的敏感部分資訊時則需要它。</span><span class="sxs-lookup"><span data-stu-id="3f4c7-112">You don't require Multi-Factor Authentication to access an application in general, but you do require it to access the sensitive portions within it.</span></span> <span data-ttu-id="3f4c7-113">例如，取用者可使用社交或本機帳戶登入銀行應用程式來檢查帳戶餘額，但必須先完成電話號碼驗證，才能嘗試進行轉帳匯款作業。</span><span class="sxs-lookup"><span data-stu-id="3f4c7-113">For example, the consumer can sign in to a banking application with a social or local account and check account balance, but must verify the phone number before attempting a wire transfer.</span></span>

## <a name="modify-your-sign-up-policy-to-enable-multi-factor-authentication"></a><span data-ttu-id="3f4c7-114">修改註冊原則以啟用 Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="3f4c7-114">Modify your sign-up policy to enable Multi-Factor Authentication</span></span>
1. <span data-ttu-id="3f4c7-115">遵循下列步驟以[瀏覽至 B2C 功能刀鋒視窗](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) (位於 Azure 入口網站上)。</span><span class="sxs-lookup"><span data-stu-id="3f4c7-115">[Follow these steps to navigate to the B2C features blade on the Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="3f4c7-116">按一下 [註冊原則] 。</span><span class="sxs-lookup"><span data-stu-id="3f4c7-116">Click **Sign-up policies**.</span></span>
3. <span data-ttu-id="3f4c7-117">按一下以開啟註冊原則 (例如 "B2C_1_SiUp")。</span><span class="sxs-lookup"><span data-stu-id="3f4c7-117">Click your sign-up policy (for example, "B2C_1_SiUp") to open it.</span></span>
4. <span data-ttu-id="3f4c7-118">按一下 [多重要素驗證]，並將 [狀態] 設為 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="3f4c7-118">Click **Multi-factor authentication** and turn the **State** to **ON**.</span></span> <span data-ttu-id="3f4c7-119">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="3f4c7-119">Click **OK**.</span></span>
5. <span data-ttu-id="3f4c7-120">按一下刀鋒視窗頂端的 [儲存]  。</span><span class="sxs-lookup"><span data-stu-id="3f4c7-120">Click **Save** at the top of the blade.</span></span>

<span data-ttu-id="3f4c7-121">您可以使用原則上的「立即執行」功能來驗證取用者體驗。</span><span class="sxs-lookup"><span data-stu-id="3f4c7-121">You can use the "Run now" feature on the policy to verify the consumer experience.</span></span> <span data-ttu-id="3f4c7-122">確認下列項目：</span><span class="sxs-lookup"><span data-stu-id="3f4c7-122">Confirm the following:</span></span>

<span data-ttu-id="3f4c7-123">在進行 Multi-Factor Authentication 步驟之前，會在目錄中建立取用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="3f4c7-123">A consumer account gets created in your directory before the Multi-Factor Authentication step occurs.</span></span> <span data-ttu-id="3f4c7-124">在步驟執行過程中，系統會要求取用者提供電話號碼進行驗證。</span><span class="sxs-lookup"><span data-stu-id="3f4c7-124">During the step, the consumer is asked to provide his or her phone number and verify it.</span></span> <span data-ttu-id="3f4c7-125">若驗證成功，會將電話號碼附加至取用者帳戶以供之後使用。</span><span class="sxs-lookup"><span data-stu-id="3f4c7-125">If verification is successful, the phone number is attached to the consumer account for later use.</span></span> <span data-ttu-id="3f4c7-126">即使取用者取消或卸除，下次登入時系統仍會要求其再度驗證電話號碼 (已啟用 Multi-Factor Authentication)。</span><span class="sxs-lookup"><span data-stu-id="3f4c7-126">Even if the consumer cancels or drops out, he or she can be asked to verify a phone number again during the next sign-in (with Multi-Factor Authentication enabled).</span></span>

## <a name="modify-your-sign-in-policy-to-enable-multi-factor-authentication"></a><span data-ttu-id="3f4c7-127">修改登入原則以啟用 Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="3f4c7-127">Modify your sign-in policy to enable Multi-Factor Authentication</span></span>
1. <span data-ttu-id="3f4c7-128">遵循下列步驟以[瀏覽至 B2C 功能刀鋒視窗](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) (位於 Azure 入口網站上)。</span><span class="sxs-lookup"><span data-stu-id="3f4c7-128">[Follow these steps to navigate to the B2C features blade on the Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="3f4c7-129">按一下 [登入原則] 。</span><span class="sxs-lookup"><span data-stu-id="3f4c7-129">Click **Sign-in policies**.</span></span>
3. <span data-ttu-id="3f4c7-130">按一下以開啟登入原則 (例如 "B2C_1_SiIn")。</span><span class="sxs-lookup"><span data-stu-id="3f4c7-130">Click your sign-in policy (for example, "B2C_1_SiIn") to open it.</span></span> <span data-ttu-id="3f4c7-131">按一下刀鋒視窗頂端的 [編輯]  。</span><span class="sxs-lookup"><span data-stu-id="3f4c7-131">Click **Edit** at the top of the blade.</span></span>
4. <span data-ttu-id="3f4c7-132">按一下 [多重要素驗證]，並將 [狀態] 設為 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="3f4c7-132">Click **Multi-factor authentication** and turn the **State** to **ON**.</span></span> <span data-ttu-id="3f4c7-133">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="3f4c7-133">Click **OK**.</span></span>
5. <span data-ttu-id="3f4c7-134">按一下刀鋒視窗頂端的 [儲存]  。</span><span class="sxs-lookup"><span data-stu-id="3f4c7-134">Click **Save** at the top of the blade.</span></span>

<span data-ttu-id="3f4c7-135">您可以使用原則上的「立即執行」功能來驗證取用者體驗。</span><span class="sxs-lookup"><span data-stu-id="3f4c7-135">You can use the "Run now" feature on the policy to verify the consumer experience.</span></span> <span data-ttu-id="3f4c7-136">確認下列項目：</span><span class="sxs-lookup"><span data-stu-id="3f4c7-136">Confirm the following:</span></span>

<span data-ttu-id="3f4c7-137">取用者登入 (使用社交或本機帳戶) 時，若已將通過驗證的電話號碼附加至取用者帳戶，系統會要求其進行驗證。</span><span class="sxs-lookup"><span data-stu-id="3f4c7-137">When the consumer signs in (using a social or local account), if a verified phone number is attached to the consumer account, he or she is asked to verify it.</span></span> <span data-ttu-id="3f4c7-138">如果未附加電話號碼，系統會要求取用者提供電話號碼以進行驗證。</span><span class="sxs-lookup"><span data-stu-id="3f4c7-138">If no phone number is attached, the consumer is asked to provide one and verify it.</span></span> <span data-ttu-id="3f4c7-139">驗證成功之後，即會將電話號碼附加至取用者帳戶以供之後使用。</span><span class="sxs-lookup"><span data-stu-id="3f4c7-139">On successful verification, the phone number is attached to the consumer account for later use.</span></span>

## <a name="multi-factor-authentication-on-other-policies"></a><span data-ttu-id="3f4c7-140">其他原則上的 Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="3f4c7-140">Multi-Factor Authentication on other policies</span></span>
<span data-ttu-id="3f4c7-141">如同對上面的註冊和登入原則所述，也可以對註冊或登入原則和密碼重設原則啟用 Multi-Factor Authentication。</span><span class="sxs-lookup"><span data-stu-id="3f4c7-141">As described for sign-up & sign-in policies above, it is also possible to enable multi-factor authentication on sign-up or sign-in policies and password reset policies.</span></span> <span data-ttu-id="3f4c7-142">很快即可用於設定檔編輯原則。</span><span class="sxs-lookup"><span data-stu-id="3f4c7-142">It will be available soon on profile editing policies.</span></span>

