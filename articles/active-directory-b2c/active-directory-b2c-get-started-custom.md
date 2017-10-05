---
title: "Azure Active Directory B2C：開始使用自訂原則 | Microsoft Docs"
description: "如何開始使用 Azure Active Directory B2C 自訂原則"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 658c597e-3787-465e-b377-26aebc94e46d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: joroja;parahk;gsacavdm
ms.openlocfilehash: 4f14dbf4b66f10290cd4f98d56a005f97cc6a207
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-get-started-with-custom-policies"></a><span data-ttu-id="fd531-103">Azure Active Directory B2C：開始使用自訂原則</span><span class="sxs-lookup"><span data-stu-id="fd531-103">Azure Active Directory B2C: Get started with custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="fd531-104">完成本文中的步驟之後，您的自訂原則將支援透過電子郵件地址和密碼執行「本機帳戶」註冊或登入。</span><span class="sxs-lookup"><span data-stu-id="fd531-104">After you complete the steps in this article, your custom policy will support "local account" sign-up or sign-in via an email address and password.</span></span> <span data-ttu-id="fd531-105">您也會準備環境以新增識別提供者 (例如 Facebook 或 Azure Active Directory)。</span><span class="sxs-lookup"><span data-stu-id="fd531-105">You will also prepare your environment for adding identity providers (like Facebook or Azure Active Directory).</span></span> <span data-ttu-id="fd531-106">我們建議您先完成這些步驟，然後再了解 Azure Active Directory (Azure AD) B2C 識別體驗架構的其他用途。</span><span class="sxs-lookup"><span data-stu-id="fd531-106">We encourage you to complete these steps before reading about other uses of the Azure Active Directory (Azure AD) B2C Identity Experience Framework.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fd531-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="fd531-107">Prerequisites</span></span>

<span data-ttu-id="fd531-108">繼續之前，請確定具有 Azure AD B2C 租用戶。此租用戶是存放您的所有使用者、應用程式、原則等的容器。</span><span class="sxs-lookup"><span data-stu-id="fd531-108">Before proceeding, ensure that you have an Azure AD B2C tenant, which is a container for all your users, apps, policies, and more.</span></span> <span data-ttu-id="fd531-109">如果您還沒有租用戶，則必須[建立 Azure AD B2C 租用戶](active-directory-b2c-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="fd531-109">If you don't have one already, you need to [create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span> <span data-ttu-id="fd531-110">我們強烈建議所有開發人員完成 Azure AD B2C 內建原則的逐步解說，並使用內建原則來設定他們的應用程式，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="fd531-110">We strongly encourage all developers to complete the Azure AD B2C built-in policy walkthroughs and configure their applications with built-in policies before proceeding.</span></span> <span data-ttu-id="fd531-111">當您對原則名稱進行些微變更以叫用自訂原則之後，應用程式將會使用這兩種類型的原則。</span><span class="sxs-lookup"><span data-stu-id="fd531-111">Your applications will work with both types of policies once you make a minor change to the policy name to invoke the custom policy.</span></span>

>[!NOTE]
><span data-ttu-id="fd531-112">為了存取自訂原則編輯功能，您需要已與租用戶連結的有效 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="fd531-112">To access custom policy editing, you need a valid Azure subscription linked to your tenant.</span></span> <span data-ttu-id="fd531-113">如果您尚未[將 Azure AD B2C 租用戶連結到 Azure 訂用帳戶](active-directory-b2c-how-to-enable-billing.md)或已停用 Azure 訂用帳戶，將無法使用 [身分識別體驗架構] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fd531-113">If you haven't [linked your Azure AD B2C tenant to an Azure subscription](active-directory-b2c-how-to-enable-billing.md) or your Azure subscription is disabled, the Identity Experience Framework button won't be available.</span></span>

## <a name="add-signing-and-encryption-keys-to-your-b2c-tenant-for-use-by-custom-policies"></a><span data-ttu-id="fd531-114">將簽署和加密金鑰新增至 B2C 租用戶以供自訂原則使用</span><span class="sxs-lookup"><span data-stu-id="fd531-114">Add signing and encryption keys to your B2C tenant for use by custom policies</span></span>

1. <span data-ttu-id="fd531-115">在您的 Azure AD B2C 租用戶設定中，開啟 [識別體驗架構] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="fd531-115">Open the **Identity Experience Framework** blade in your Azure AD B2C tenant settings.</span></span>
2. <span data-ttu-id="fd531-116">選取**原則金鑰**以檢視您的租用戶中可用的金鑰。</span><span class="sxs-lookup"><span data-stu-id="fd531-116">Select **Policy Keys** to view the keys available in your tenant.</span></span>
3. <span data-ttu-id="fd531-117">如果 B2C_1A_TokenSigningKeyContainer 不存在，請加以建立：</span><span class="sxs-lookup"><span data-stu-id="fd531-117">Create B2C_1A_TokenSigningKeyContainer if it does not exist:</span></span><br>
    <span data-ttu-id="fd531-118">a.</span><span class="sxs-lookup"><span data-stu-id="fd531-118">a.</span></span> <span data-ttu-id="fd531-119">選取 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="fd531-119">Select **Add**.</span></span> <br>
    <span data-ttu-id="fd531-120">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="fd531-120">b.</span></span> <span data-ttu-id="fd531-121">選取 [產生]。</span><span class="sxs-lookup"><span data-stu-id="fd531-121">Select **Generate**.</span></span><br>
    <span data-ttu-id="fd531-122">c.</span><span class="sxs-lookup"><span data-stu-id="fd531-122">c.</span></span> <span data-ttu-id="fd531-123">針對 [名稱] 使用 `TokenSigningKeyContainer`。</span><span class="sxs-lookup"><span data-stu-id="fd531-123">For **Name**, use `TokenSigningKeyContainer`.</span></span> <br> 
    <span data-ttu-id="fd531-124">可能會自動加入前置詞 `B2C_1A_`。</span><span class="sxs-lookup"><span data-stu-id="fd531-124">The prefix `B2C_1A_` might be added automatically.</span></span><br>
    <span data-ttu-id="fd531-125">d.</span><span class="sxs-lookup"><span data-stu-id="fd531-125">d.</span></span> <span data-ttu-id="fd531-126">針對 [金鑰類型] 使用 [RSA]。</span><span class="sxs-lookup"><span data-stu-id="fd531-126">For **Key type**, use **RSA**.</span></span><br>
    <span data-ttu-id="fd531-127">e.</span><span class="sxs-lookup"><span data-stu-id="fd531-127">e.</span></span> <span data-ttu-id="fd531-128">針對 [日期] 使用預設值。</span><span class="sxs-lookup"><span data-stu-id="fd531-128">For **Dates**, use the defaults.</span></span> <br>
    <span data-ttu-id="fd531-129">f.</span><span class="sxs-lookup"><span data-stu-id="fd531-129">f.</span></span> <span data-ttu-id="fd531-130">針對 [金鑰使用方法] 使用 [簽章]。</span><span class="sxs-lookup"><span data-stu-id="fd531-130">For **Key usage**, use **Signature**.</span></span><br>
    <span data-ttu-id="fd531-131">g.</span><span class="sxs-lookup"><span data-stu-id="fd531-131">g.</span></span> <span data-ttu-id="fd531-132">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="fd531-132">Select **Create**.</span></span><br>
4. <span data-ttu-id="fd531-133">如果 B2C_1A_TokenEncryptionKeyContainer 不存在，請加以建立：</span><span class="sxs-lookup"><span data-stu-id="fd531-133">Create B2C_1A_TokenEncryptionKeyContainer if it does not exist:</span></span><br>
 <span data-ttu-id="fd531-134">a.</span><span class="sxs-lookup"><span data-stu-id="fd531-134">a.</span></span> <span data-ttu-id="fd531-135">選取 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="fd531-135">Select **Add**.</span></span><br>
 <span data-ttu-id="fd531-136">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="fd531-136">b.</span></span> <span data-ttu-id="fd531-137">選取 [產生]。</span><span class="sxs-lookup"><span data-stu-id="fd531-137">Select **Generate**.</span></span><br>
 <span data-ttu-id="fd531-138">c.</span><span class="sxs-lookup"><span data-stu-id="fd531-138">c.</span></span> <span data-ttu-id="fd531-139">針對 [名稱] 使用 `TokenEncryptionKeyContainer`。</span><span class="sxs-lookup"><span data-stu-id="fd531-139">For **Name**, use `TokenEncryptionKeyContainer`.</span></span> <br>
   <span data-ttu-id="fd531-140">可能會自動加入前置詞 `B2C_1A`_。</span><span class="sxs-lookup"><span data-stu-id="fd531-140">The prefix `B2C_1A`_ might be added automatically.</span></span><br>
 <span data-ttu-id="fd531-141">d.</span><span class="sxs-lookup"><span data-stu-id="fd531-141">d.</span></span> <span data-ttu-id="fd531-142">針對 [金鑰類型] 使用 [RSA]。</span><span class="sxs-lookup"><span data-stu-id="fd531-142">For **Key type**, use **RSA**.</span></span><br>
 <span data-ttu-id="fd531-143">e.</span><span class="sxs-lookup"><span data-stu-id="fd531-143">e.</span></span> <span data-ttu-id="fd531-144">針對 [日期] 使用預設值。</span><span class="sxs-lookup"><span data-stu-id="fd531-144">For **Dates**, use the defaults.</span></span><br>
 <span data-ttu-id="fd531-145">f.</span><span class="sxs-lookup"><span data-stu-id="fd531-145">f.</span></span> <span data-ttu-id="fd531-146">針對 [金鑰使用方法] 使用 [加密]。</span><span class="sxs-lookup"><span data-stu-id="fd531-146">For **Key usage**, use **Encryption**.</span></span><br>
 <span data-ttu-id="fd531-147">g.</span><span class="sxs-lookup"><span data-stu-id="fd531-147">g.</span></span> <span data-ttu-id="fd531-148">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="fd531-148">Select **Create**.</span></span><br>
5. <span data-ttu-id="fd531-149">建立 B2C_1A_FacebookSecret。</span><span class="sxs-lookup"><span data-stu-id="fd531-149">Create B2C_1A_FacebookSecret.</span></span> <br>
<span data-ttu-id="fd531-150">如果您已有 Facebook 應用程式的祕密，請將它當作原則金鑰來新增到您的租用戶。</span><span class="sxs-lookup"><span data-stu-id="fd531-150">If you already have a Facebook application secret, add it as a policy key to your tenant.</span></span> <span data-ttu-id="fd531-151">否則，您必須建立具有預留位置值的金鑰，原則才能通過驗證。</span><span class="sxs-lookup"><span data-stu-id="fd531-151">Otherwise, you must create the key with a placeholder value so that your policies pass validation.</span></span><br>
 <span data-ttu-id="fd531-152">a.</span><span class="sxs-lookup"><span data-stu-id="fd531-152">a.</span></span> <span data-ttu-id="fd531-153">選取 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="fd531-153">Select **Add**.</span></span><br>
 <span data-ttu-id="fd531-154">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="fd531-154">b.</span></span> <span data-ttu-id="fd531-155">針對 [選項] 使用 [手動]。</span><span class="sxs-lookup"><span data-stu-id="fd531-155">For **Options**, use **Manual**.</span></span><br>
 <span data-ttu-id="fd531-156">c.</span><span class="sxs-lookup"><span data-stu-id="fd531-156">c.</span></span> <span data-ttu-id="fd531-157">針對 [名稱] 使用 `FacebookSecret`。</span><span class="sxs-lookup"><span data-stu-id="fd531-157">For **Name**, use `FacebookSecret`.</span></span> <br>
 <span data-ttu-id="fd531-158">可能會自動加入前置詞 `B2C_1A_`。</span><span class="sxs-lookup"><span data-stu-id="fd531-158">The prefix `B2C_1A_` might be added automatically.</span></span><br>
 <span data-ttu-id="fd531-159">d.</span><span class="sxs-lookup"><span data-stu-id="fd531-159">d.</span></span> <span data-ttu-id="fd531-160">在 [祕密] 方塊中，輸入 developers.facebook.com 提供給您的 FacebookSecret，或輸入 `0` 作為預留位置。</span><span class="sxs-lookup"><span data-stu-id="fd531-160">In the **Secret** box, enter your FacebookSecret from developers.facebook.com or `0` as a placeholder.</span></span> <span data-ttu-id="fd531-161">這不是您的 Facebook 應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="fd531-161">*This is not your Facebook app ID.*</span></span> <br>
 <span data-ttu-id="fd531-162">e.</span><span class="sxs-lookup"><span data-stu-id="fd531-162">e.</span></span> <span data-ttu-id="fd531-163">針對 [金鑰使用方法] 使用 [簽章]。</span><span class="sxs-lookup"><span data-stu-id="fd531-163">For **Key usage**, use **Signature**.</span></span> <br>
 <span data-ttu-id="fd531-164">f.</span><span class="sxs-lookup"><span data-stu-id="fd531-164">f.</span></span> <span data-ttu-id="fd531-165">選取 [建立] 並確認建立。</span><span class="sxs-lookup"><span data-stu-id="fd531-165">Select **Create** and confirm creation.</span></span>

## <a name="register-identity-experience-framework-applications"></a><span data-ttu-id="fd531-166">註冊身分識別體驗架構應用程式</span><span class="sxs-lookup"><span data-stu-id="fd531-166">Register Identity Experience Framework applications</span></span>

<span data-ttu-id="fd531-167">Azure AD B2C 會要求您註冊兩個額外的應用程式，由引擎用來註冊和登入使用者。</span><span class="sxs-lookup"><span data-stu-id="fd531-167">Azure AD B2C requires you to register two extra applications that are used by the engine to sign up and sign in users.</span></span>

>[!NOTE]
><span data-ttu-id="fd531-168">您必須建立兩個應用程式，以使用本機帳戶來啟用登入︰IdentityExperienceFramework (Web 應用程式) 和 ProxyIdentityExperienceFramework (原生應用程式)，且具有來自 IdentityExperienceFramework 應用程式的委派權限。</span><span class="sxs-lookup"><span data-stu-id="fd531-168">You must create two applications that enable sign-in using local accounts: IdentityExperienceFramework (a web app) and ProxyIdentityExperienceFramework (a native app) with delegated permission from the IdentityExperienceFramework app.</span></span> <span data-ttu-id="fd531-169">本機帳戶只存在於您的租用戶。</span><span class="sxs-lookup"><span data-stu-id="fd531-169">Local accounts exist only in your tenant.</span></span> <span data-ttu-id="fd531-170">您的使用者會使用唯一的電子郵件地址/密碼組合進行註冊，以存取您租用戶所註冊的應用程式。</span><span class="sxs-lookup"><span data-stu-id="fd531-170">Your users sign up with a unique email address/password combination to access your tenant-registered applications.</span></span>

### <a name="create-the-identityexperienceframework-application"></a><span data-ttu-id="fd531-171">建立 IdentityExperienceFramework 應用程式</span><span class="sxs-lookup"><span data-stu-id="fd531-171">Create the IdentityExperienceFramework application</span></span>

1. <span data-ttu-id="fd531-172">在 [Azure 入口網站](https://portal.azure.com)中，切換至[您的 Azure AD B2C 租用戶環境](active-directory-b2c-navigate-to-b2c-context.md)。</span><span class="sxs-lookup"><span data-stu-id="fd531-172">In the [Azure portal](https://portal.azure.com), switch into the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md).</span></span>
2. <span data-ttu-id="fd531-173">開啟 [Azure Active Directory] 刀鋒視窗 (不是 [Azure AD B2C] 刀鋒視窗)。</span><span class="sxs-lookup"><span data-stu-id="fd531-173">Open the **Azure Active Directory** blade (not the **Azure AD B2C** blade).</span></span> <span data-ttu-id="fd531-174">您可能需要選取 [更多服務]，才能找到它。</span><span class="sxs-lookup"><span data-stu-id="fd531-174">You might need to select **More Services** to find it.</span></span>
3. <span data-ttu-id="fd531-175">選取 [應用程式註冊]。</span><span class="sxs-lookup"><span data-stu-id="fd531-175">Select **App registrations**.</span></span>
4. <span data-ttu-id="fd531-176">選取 [新增應用程式註冊]。</span><span class="sxs-lookup"><span data-stu-id="fd531-176">Select **New application registration**.</span></span>
   * <span data-ttu-id="fd531-177">針對 [名稱] 使用 `IdentityExperienceFramework`。</span><span class="sxs-lookup"><span data-stu-id="fd531-177">For **Name**, use `IdentityExperienceFramework`.</span></span>
   * <span data-ttu-id="fd531-178">針對 [應用程式類型] 使用 [Web 應用程式/API]。</span><span class="sxs-lookup"><span data-stu-id="fd531-178">For **Application type**, use **Web app/API**.</span></span>
   * <span data-ttu-id="fd531-179">針對 [登入 URL] 使用 `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`，其中 `yourtenant` 是您的 Azure AD B2C 租用戶網域名稱。</span><span class="sxs-lookup"><span data-stu-id="fd531-179">For **Sign-on URL**, use `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`, where `yourtenant` is your Azure AD B2C tenant domain name.</span></span>
5. <span data-ttu-id="fd531-180">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="fd531-180">Select **Create**.</span></span>
6. <span data-ttu-id="fd531-181">建立之後，選取新建立的應用程式 **IdentityExperienceFramework**。</span><span class="sxs-lookup"><span data-stu-id="fd531-181">Once it is created, select the newly created application **IdentityExperienceFramework**.</span></span><br>
   * <span data-ttu-id="fd531-182">選取 [屬性] 。</span><span class="sxs-lookup"><span data-stu-id="fd531-182">Select **Properties**.</span></span><br>
   * <span data-ttu-id="fd531-183">複製應用程式識別碼並加以儲存，以供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="fd531-183">Copy the application ID and save it for later.</span></span>

### <a name="create-the-proxyidentityexperienceframework-application"></a><span data-ttu-id="fd531-184">建立 ProxyIdentityExperienceFramework 應用程式</span><span class="sxs-lookup"><span data-stu-id="fd531-184">Create the ProxyIdentityExperienceFramework application</span></span>

1. <span data-ttu-id="fd531-185">選取 [應用程式註冊]。</span><span class="sxs-lookup"><span data-stu-id="fd531-185">Select **App registrations**.</span></span>
1. <span data-ttu-id="fd531-186">選取 [新增應用程式註冊]。</span><span class="sxs-lookup"><span data-stu-id="fd531-186">Select **New application registration**.</span></span>
   * <span data-ttu-id="fd531-187">針對 [名稱] 使用 `ProxyIdentityExperienceFramework`。</span><span class="sxs-lookup"><span data-stu-id="fd531-187">For **Name**, use `ProxyIdentityExperienceFramework`.</span></span>
   * <span data-ttu-id="fd531-188">針對 [應用程式類型] 使用 [原生]。</span><span class="sxs-lookup"><span data-stu-id="fd531-188">For **Application type**, use **Native**.</span></span>
   * <span data-ttu-id="fd531-189">針對 [重新導向 URI] 使用 `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`，其中 `yourtenant` 是您的 Azure AD B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="fd531-189">For **Redirect URI**, use `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`, where `yourtenant` is your Azure AD B2C tenant.</span></span>
1. <span data-ttu-id="fd531-190">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="fd531-190">Select **Create**.</span></span>
1. <span data-ttu-id="fd531-191">建立之後，選取應用程式 **ProxyIdentityExperienceFramework**。</span><span class="sxs-lookup"><span data-stu-id="fd531-191">Once it has been created, select the application **ProxyIdentityExperienceFramework**.</span></span><br>
   * <span data-ttu-id="fd531-192">選取 [屬性] 。</span><span class="sxs-lookup"><span data-stu-id="fd531-192">Select **Properties**.</span></span> <br>
   * <span data-ttu-id="fd531-193">複製應用程式識別碼並加以儲存，以供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="fd531-193">Copy the application ID and save it for later.</span></span>
1. <span data-ttu-id="fd531-194">選取 [必要權限]。</span><span class="sxs-lookup"><span data-stu-id="fd531-194">Select **Required permissions**.</span></span>
1. <span data-ttu-id="fd531-195">選取 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="fd531-195">Select **Add**.</span></span>
1. <span data-ttu-id="fd531-196">選取 [選取 API]。</span><span class="sxs-lookup"><span data-stu-id="fd531-196">Select **Select an API**.</span></span>
1. <span data-ttu-id="fd531-197">搜尋名稱 IdentityExperienceFramework。</span><span class="sxs-lookup"><span data-stu-id="fd531-197">Search for the name IdentityExperienceFramework.</span></span> <span data-ttu-id="fd531-198">在結果中選取 [IdentityExperienceFramework]，然後按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="fd531-198">Select **IdentityExperienceFramework** in the results, and then click **Select**.</span></span>
1. <span data-ttu-id="fd531-199">選取 [存取 IdentityExperienceFramework] 旁的核取方塊，然後按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="fd531-199">Select the check box next to **Access IdentityExperienceFramework**, and then click **Select**.</span></span>
1. <span data-ttu-id="fd531-200">選取 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="fd531-200">Select **Done**.</span></span>
1. <span data-ttu-id="fd531-201">選取 [授與權限]，然後選取 [是] 加以確認。</span><span class="sxs-lookup"><span data-stu-id="fd531-201">Select **Grant Permissions**, and then confirm by selecting **Yes**.</span></span>

## <a name="download-starter-pack-and-modify-policies"></a><span data-ttu-id="fd531-202">下載入門套件和修改原則</span><span class="sxs-lookup"><span data-stu-id="fd531-202">Download starter pack and modify policies</span></span>

<span data-ttu-id="fd531-203">自訂原則是一組需要上傳至 Azure AD B2C 租用戶的 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="fd531-203">Custom policies are a set of XML files that need to be uploaded to your Azure AD B2C tenant.</span></span> <span data-ttu-id="fd531-204">我們提供了入門套件以協助您加快進展速度。</span><span class="sxs-lookup"><span data-stu-id="fd531-204">We provide starter packs to get you going quickly.</span></span> <span data-ttu-id="fd531-205">下列清單中的每個入門套件，針對要完成所述的案例，均包含所需的最小數目技術設定檔與使用者旅程圖：</span><span class="sxs-lookup"><span data-stu-id="fd531-205">Each starter pack in the following list contains the smallest number of technical profiles and user journeys needed to achieve the scenarios described:</span></span>
 * <span data-ttu-id="fd531-206">LocalAccounts。</span><span class="sxs-lookup"><span data-stu-id="fd531-206">LocalAccounts.</span></span> <span data-ttu-id="fd531-207">只能使用本機帳戶。</span><span class="sxs-lookup"><span data-stu-id="fd531-207">Enables the use of local accounts only.</span></span>
 * <span data-ttu-id="fd531-208">SocialAccounts。</span><span class="sxs-lookup"><span data-stu-id="fd531-208">SocialAccounts.</span></span> <span data-ttu-id="fd531-209">只能使用社交 (或同盟) 帳戶。</span><span class="sxs-lookup"><span data-stu-id="fd531-209">Enables the use of social (or federated) accounts only.</span></span>
 * <span data-ttu-id="fd531-210">**SocialAndLocalAccounts**。</span><span class="sxs-lookup"><span data-stu-id="fd531-210">**SocialAndLocalAccounts**.</span></span> <span data-ttu-id="fd531-211">我們將在逐步解說中使用此檔案。</span><span class="sxs-lookup"><span data-stu-id="fd531-211">We use this file for the walkthrough.</span></span>
 * <span data-ttu-id="fd531-212">SocialAndLocalAccountsWithMFA。</span><span class="sxs-lookup"><span data-stu-id="fd531-212">SocialAndLocalAccountsWithMFA.</span></span> <span data-ttu-id="fd531-213">此處包含社交、本機及 Multi-Factor Authentication 選項。</span><span class="sxs-lookup"><span data-stu-id="fd531-213">Social, local, and Multi-Factor Authentication options are included here.</span></span>

<span data-ttu-id="fd531-214">每個入門套件均包含：</span><span class="sxs-lookup"><span data-stu-id="fd531-214">Each starter pack contains:</span></span>

* <span data-ttu-id="fd531-215">原則的[基底檔案](active-directory-b2c-overview-custom.md#policy-files)。</span><span class="sxs-lookup"><span data-stu-id="fd531-215">The [base file](active-directory-b2c-overview-custom.md#policy-files) of the policy.</span></span> <span data-ttu-id="fd531-216">需要對基底做一些修改。</span><span class="sxs-lookup"><span data-stu-id="fd531-216">Few modifications are required to the base.</span></span>
* <span data-ttu-id="fd531-217">原則的[擴充檔案](active-directory-b2c-overview-custom.md#policy-files)。</span><span class="sxs-lookup"><span data-stu-id="fd531-217">The [extension file](active-directory-b2c-overview-custom.md#policy-files) of the policy.</span></span>  <span data-ttu-id="fd531-218">大部分的設定變更都在這個檔案中完成。</span><span class="sxs-lookup"><span data-stu-id="fd531-218">This file is where most configuration changes are made.</span></span>
* <span data-ttu-id="fd531-219">[信賴憑證者檔案](active-directory-b2c-overview-custom.md#policy-files)是工作特定檔案，由應用程式呼叫。</span><span class="sxs-lookup"><span data-stu-id="fd531-219">[Relying party files](active-directory-b2c-overview-custom.md#policy-files) are task-specific files called by your application.</span></span>

>[!NOTE]
><span data-ttu-id="fd531-220">如果 XML 編輯器支援驗證，請根據入門套件根目錄中的 TrustFrameworkPolicy_0.3.0.0.xsd XML 結構描述來驗證檔案。</span><span class="sxs-lookup"><span data-stu-id="fd531-220">If your XML editor supports validation, validate the files against the TrustFrameworkPolicy_0.3.0.0.xsd XML schema that is located in the root directory of the starter pack.</span></span> <span data-ttu-id="fd531-221">在上載之前，XML 結構描述驗證會識別錯誤。</span><span class="sxs-lookup"><span data-stu-id="fd531-221">XML schema validation identifies errors before uploading.</span></span>

 <span data-ttu-id="fd531-222">現在就開始吧！</span><span class="sxs-lookup"><span data-stu-id="fd531-222">Let's get started:</span></span>

1. <span data-ttu-id="fd531-223">從 GitHub 下載 active-directory-b2c-custom-policy-starterpack。</span><span class="sxs-lookup"><span data-stu-id="fd531-223">Download active-directory-b2c-custom-policy-starterpack from GitHub.</span></span> <span data-ttu-id="fd531-224">[下載 .zip 檔案](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/archive/master.zip)或執行</span><span class="sxs-lookup"><span data-stu-id="fd531-224">[Download the .zip file](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/archive/master.zip) or run</span></span>

    ```console
    git clone https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack
    ```
2. <span data-ttu-id="fd531-225">開啟 SocialAndLocalAccounts 資料夾。</span><span class="sxs-lookup"><span data-stu-id="fd531-225">Open the SocialAndLocalAccounts folder.</span></span>  <span data-ttu-id="fd531-226">此資料夾中的基底檔案 (TrustFrameworkBase.xml) 包含本機和社交/公司帳戶所需的內容。</span><span class="sxs-lookup"><span data-stu-id="fd531-226">The base file (TrustFrameworkBase.xml) in this folder contains content needed for both local and social/corporate accounts.</span></span> <span data-ttu-id="fd531-227">社交內容不會干擾本機帳戶的啟動和執行步驟。</span><span class="sxs-lookup"><span data-stu-id="fd531-227">The social content does not interfere with the steps for getting local accounts up and running.</span></span>
3. <span data-ttu-id="fd531-228">開啟 TrustFrameworkBase.xml。</span><span class="sxs-lookup"><span data-stu-id="fd531-228">Open TrustFrameworkBase.xml.</span></span> <span data-ttu-id="fd531-229">如果您需要 XML 編輯器，請[試用 Visual Studio 程式碼](https://code.visualstudio.com/download)，這是一個輕巧的跨平台編輯器。</span><span class="sxs-lookup"><span data-stu-id="fd531-229">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
4. <span data-ttu-id="fd531-230">在 `TrustFrameworkPolicy` 根元素中，更新 `TenantId` 和 `PublicPolicyUri` 屬性，以您的 Azure AD B2C 租用戶網域名稱取代 `yourtenant.onmicrosoft.com`：</span><span class="sxs-lookup"><span data-stu-id="fd531-230">In the root `TrustFrameworkPolicy` element, update the `TenantId` and `PublicPolicyUri` attributes, replacing `yourtenant.onmicrosoft.com` with the domain name of your Azure AD B2C tenant:</span></span>
   ```xml
    <TrustFrameworkPolicy
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:xsd="http://www.w3.org/2001/XMLSchema"
    xmlns="http://schemas.microsoft.com/online/cpim/schemas/2013/06"
    PolicySchemaVersion="0.3.0.0"
    TenantId="yourtenant.onmicrosoft.com"
    PolicyId="B2C_1A_TrustFrameworkBase"
    PublicPolicyUri="http://yourtenant.onmicrosoft.com">
    ```
   >[!NOTE]
   ><span data-ttu-id="fd531-231">`PolicyId` 是您將在入口網站看到的原則名稱，也是其他原則檔案用來參考此原則檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="fd531-231">`PolicyId` is the policy name that you see in the portal and the name by which this policy file is referenced by other policy files.</span></span>

5. <span data-ttu-id="fd531-232">儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="fd531-232">Save the file.</span></span>
6. <span data-ttu-id="fd531-233">開啟 TrustFrameworkExtensions.xml。</span><span class="sxs-lookup"><span data-stu-id="fd531-233">Open TrustFrameworkExtensions.xml.</span></span> <span data-ttu-id="fd531-234">以您的 Azure AD B2C 租用戶取代 `yourtenant.onmicrosoft.com` 來進行這兩項相同的變更。</span><span class="sxs-lookup"><span data-stu-id="fd531-234">Make the same two changes by replacing `yourtenant.onmicrosoft.com` with your Azure AD B2C tenant.</span></span> <span data-ttu-id="fd531-235">加上在 `<TenantId>` 元素中進行相同的取代作業，總共進行三項變更。</span><span class="sxs-lookup"><span data-stu-id="fd531-235">Make the same replacement in the `<TenantId>` element for a total of three changes.</span></span> <span data-ttu-id="fd531-236">儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="fd531-236">Save the file.</span></span>
7. <span data-ttu-id="fd531-237">開啟 SignUpOrSignIn.xml。</span><span class="sxs-lookup"><span data-stu-id="fd531-237">Open SignUpOrSignIn.xml.</span></span> <span data-ttu-id="fd531-238">在三個地方以您的 Azure AD B2C 租用戶取代 `yourtenant.onmicrosoft.com` 來進行相同的變更。</span><span class="sxs-lookup"><span data-stu-id="fd531-238">Make the same changes by replacing `yourtenant.onmicrosoft.com` with your Azure AD B2C tenant in three places.</span></span> <span data-ttu-id="fd531-239">儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="fd531-239">Save the file.</span></span>
8. <span data-ttu-id="fd531-240">開啟密碼重設和設定檔編輯檔案。</span><span class="sxs-lookup"><span data-stu-id="fd531-240">Open the password reset and profile edit files.</span></span> <span data-ttu-id="fd531-241">在每個檔案中的三個地方，以您的 Azure AD B2C 租用戶取代 `yourtenant.onmicrosoft.com` 來進行相同的變更。</span><span class="sxs-lookup"><span data-stu-id="fd531-241">Make the same changes by replacing `yourtenant.onmicrosoft.com` with your Azure AD B2C tenant in three places in each file.</span></span> <span data-ttu-id="fd531-242">儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="fd531-242">Save the files.</span></span>

### <a name="add-the-application-ids-to-your-custom-policy"></a><span data-ttu-id="fd531-243">將應用程式識別碼新增至您的自訂原則</span><span class="sxs-lookup"><span data-stu-id="fd531-243">Add the application IDs to your custom policy</span></span>
<span data-ttu-id="fd531-244">在擴充檔案 (`TrustFrameworkExtensions.xml`) 中新增應用程式識別碼：</span><span class="sxs-lookup"><span data-stu-id="fd531-244">Add the application IDs to the extensions file (`TrustFrameworkExtensions.xml`):</span></span>

1. <span data-ttu-id="fd531-245">在擴充檔案 (TrustFrameworkExtensions.xml) 中，尋找 `<TechnicalProfile Id="login-NonInteractive">` 元素。</span><span class="sxs-lookup"><span data-stu-id="fd531-245">In the extensions file (TrustFrameworkExtensions.xml), find the element `<TechnicalProfile Id="login-NonInteractive">`.</span></span>
2. <span data-ttu-id="fd531-246">以您稍早建立之身分識別體驗架構應用程式的應用程式識別碼，取代 `IdentityExperienceFrameworkAppId` 的兩個執行個體。</span><span class="sxs-lookup"><span data-stu-id="fd531-246">Replace both instances of `IdentityExperienceFrameworkAppId` with the application ID of the Identity Experience Framework application that you created earlier.</span></span> <span data-ttu-id="fd531-247">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="fd531-247">Here is an example:</span></span>

   ```xml
   <Item Key="client_id">8322dedc-cbf4-43bc-8bb6-141d16f0f489</Item>
   ```
3. <span data-ttu-id="fd531-248">以您稍早建立之 Proxy 識別體驗架構應用程式的應用程式識別碼，取代 `ProxyIdentityExperienceFrameworkAppId` 的兩個執行個體。</span><span class="sxs-lookup"><span data-stu-id="fd531-248">Replace both instances of `ProxyIdentityExperienceFrameworkAppId` with the application ID of the Proxy Identity Experience Framework application that you created earlier.</span></span>
4. <span data-ttu-id="fd531-249">儲存擴充檔案。</span><span class="sxs-lookup"><span data-stu-id="fd531-249">Save your extensions file.</span></span>

## <a name="upload-the-policies-to-your-tenant"></a><span data-ttu-id="fd531-250">將原則上傳至您的租用戶</span><span class="sxs-lookup"><span data-stu-id="fd531-250">Upload the policies to your tenant</span></span>

1. <span data-ttu-id="fd531-251">在 [Azure 入口網站](https://portal.azure.com)中，切換至[您的 Azure AD B2C 租用戶環境](active-directory-b2c-navigate-to-b2c-context.md)，然後開啟 [Azure AD B2C] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="fd531-251">In the [Azure portal](https://portal.azure.com), switch into the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open the **Azure AD B2C** blade.</span></span>
2. <span data-ttu-id="fd531-252">選取 [識別體驗架構]。</span><span class="sxs-lookup"><span data-stu-id="fd531-252">Select **Identity Experience Framework**.</span></span>
3. <span data-ttu-id="fd531-253">選取 [上傳原則]。</span><span class="sxs-lookup"><span data-stu-id="fd531-253">Select **Upload Policy**.</span></span>

    >[!WARNING]
    ><span data-ttu-id="fd531-254">必須依下列順序上傳自訂原則檔︰</span><span class="sxs-lookup"><span data-stu-id="fd531-254">The custom policy files must be uploaded in the following order:</span></span>

1. <span data-ttu-id="fd531-255">上傳 TrustFrameworkBase.xml。</span><span class="sxs-lookup"><span data-stu-id="fd531-255">Upload TrustFrameworkBase.xml.</span></span>
2. <span data-ttu-id="fd531-256">上傳 TrustFrameworkExtensions.xml。</span><span class="sxs-lookup"><span data-stu-id="fd531-256">Upload TrustFrameworkExtensions.xml.</span></span>
3. <span data-ttu-id="fd531-257">上傳 SignUpOrSignin.xml。</span><span class="sxs-lookup"><span data-stu-id="fd531-257">Upload SignUpOrSignin.xml.</span></span>
4. <span data-ttu-id="fd531-258">上傳其他原則檔案。</span><span class="sxs-lookup"><span data-stu-id="fd531-258">Upload your other policy files.</span></span>

<span data-ttu-id="fd531-259">上傳檔案時，原則檔案的名稱前面會加上 `B2C_1A_`。</span><span class="sxs-lookup"><span data-stu-id="fd531-259">When a file is uploaded, the name of the policy file is prepended with `B2C_1A_`.</span></span>

## <a name="test-the-custom-policy-by-using-run-now"></a><span data-ttu-id="fd531-260">使用 [立即執行] 測試自訂原則</span><span class="sxs-lookup"><span data-stu-id="fd531-260">Test the custom policy by using Run Now</span></span>

1. <span data-ttu-id="fd531-261">開啟 [Azure AD B2C 設定]，然後移至 [識別體驗架構]。</span><span class="sxs-lookup"><span data-stu-id="fd531-261">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="fd531-262">[立即執行] 需要在租用戶上至少預先註冊一個應用程式。</span><span class="sxs-lookup"><span data-stu-id="fd531-262">**Run now** requires at least one application to be preregistered on the tenant.</span></span> <span data-ttu-id="fd531-263">您必須在 B2C 租用戶中 (使用 Azure AD B2C 中的 [應用程式] 功能表選取項目，或者使用識別體驗架構) 註冊應用程式，以同時叫用內建和自訂原則。</span><span class="sxs-lookup"><span data-stu-id="fd531-263">Applications must be registered in the B2C tenant, either by using the **Applications** menu selection in Azure AD B2C or by using the Identity Experience Framework to invoke both built-in and custom policies.</span></span> <span data-ttu-id="fd531-264">每個應用程式只需要一個註冊。</span><span class="sxs-lookup"><span data-stu-id="fd531-264">Only one registration per application is needed.</span></span><br><br>
   <span data-ttu-id="fd531-265">若要了解如何註冊應用程式，請參閱 Azure AD B2C [開始使用](active-directory-b2c-get-started.md)一文或[應用程式註冊](active-directory-b2c-app-registration.md)一文。</span><span class="sxs-lookup"><span data-stu-id="fd531-265">To learn how to register applications, see the Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or the [Application registration](active-directory-b2c-app-registration.md) article.</span></span>  

2. <span data-ttu-id="fd531-266">開啟 B2C_1A_signup_signin，此為您上傳的信賴憑證者 (RP) 自訂原則。</span><span class="sxs-lookup"><span data-stu-id="fd531-266">Open B2C_1A_signup_signin, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="fd531-267">選取 [立即執行]。</span><span class="sxs-lookup"><span data-stu-id="fd531-267">Select **Run now**.</span></span>

3. <span data-ttu-id="fd531-268">您應該可以使用電子郵件地址註冊。</span><span class="sxs-lookup"><span data-stu-id="fd531-268">You should be able to sign up using an email address.</span></span>

4. <span data-ttu-id="fd531-269">使用相同的帳戶登入，以確認您的設定正確。</span><span class="sxs-lookup"><span data-stu-id="fd531-269">Sign in with the same account to confirm that you have the correct configuration.</span></span>

>[!NOTE]
><span data-ttu-id="fd531-270">登入失敗的常見原因是 IdentityExperienceFramework 應用程式設定不正確。</span><span class="sxs-lookup"><span data-stu-id="fd531-270">A common cause of sign-in failure is an improperly configured IdentityExperienceFramework app.</span></span>


## <a name="next-steps"></a><span data-ttu-id="fd531-271">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fd531-271">Next steps</span></span>

### <a name="add-facebook-as-an-identity-provider"></a><span data-ttu-id="fd531-272">將 Facebook 新增為識別提供者</span><span class="sxs-lookup"><span data-stu-id="fd531-272">Add Facebook as an identity provider</span></span>
<span data-ttu-id="fd531-273">若要設定 Facebook：</span><span class="sxs-lookup"><span data-stu-id="fd531-273">To set up Facebook:</span></span>
1. <span data-ttu-id="fd531-274">[在 developers.facebook.com 中設定 Facebook 應用程式](active-directory-b2c-setup-fb-app.md)。</span><span class="sxs-lookup"><span data-stu-id="fd531-274">[Configure a Facebook application in developers.facebook.com](active-directory-b2c-setup-fb-app.md).</span></span>
2. <span data-ttu-id="fd531-275">[在 Azure AD B2C 租用戶中新增 Facebook 應用程式祕密](#add-signing-and-encryption-keys-to-your-b2c-tenant-for-use-by-custom-policies)。</span><span class="sxs-lookup"><span data-stu-id="fd531-275">[Add the Facebook application secret to your Azure AD B2C tenant](#add-signing-and-encryption-keys-to-your-b2c-tenant-for-use-by-custom-policies).</span></span>
3. <span data-ttu-id="fd531-276">在 TrustFrameworkExtensions 原則檔案中，使用 Facebook 應用程式識別碼取代 `client_id` 的值：</span><span class="sxs-lookup"><span data-stu-id="fd531-276">In the TrustFrameworkExtensions policy file, replace the value of `client_id` with the Facebook application ID:</span></span>

   ```xml
   <TechnicalProfile Id="Facebook-OAUTH">
     <Metadata>
     <!--Replace the value of client_id in this technical profile with the Facebook app ID"-->
       <Item Key="client_id">00000000000000</Item>
   ```
4. <span data-ttu-id="fd531-277">將 TrustFrameworkExtensions.xml 原則檔案上傳至您的租用戶。</span><span class="sxs-lookup"><span data-stu-id="fd531-277">Upload the TrustFrameworkExtensions.xml policy file to your tenant.</span></span>
5. <span data-ttu-id="fd531-278">使用 [立即執行] 進行測試，或直接從您已註冊的應用程式中叫用原則。</span><span class="sxs-lookup"><span data-stu-id="fd531-278">Test by using **Run now** or by invoking the policy directly from your registered application.</span></span>

### <a name="add-azure-active-directory-as-an-identity-provider"></a><span data-ttu-id="fd531-279">將 Azure Active Directory 新增為識別提供者</span><span class="sxs-lookup"><span data-stu-id="fd531-279">Add Azure Active Directory as an identity provider</span></span>
<span data-ttu-id="fd531-280">此入門指南中所使用的基底檔案已經包含您新增其他識別提供者時所需的部分內容。</span><span class="sxs-lookup"><span data-stu-id="fd531-280">The base file used in this getting started guide already contains some of the content that you need for adding other identity providers.</span></span> <span data-ttu-id="fd531-281">如需設定登入的相關資訊，請參閱 [Azure Active Directory B2C：使用 Azure AD 帳戶登入](active-directory-b2c-setup-aad-custom.md)一文。</span><span class="sxs-lookup"><span data-stu-id="fd531-281">For information on setting up sign-ins, see the [Azure Active Directory B2C: Sign in by using Azure AD accounts](active-directory-b2c-setup-aad-custom.md) article.</span></span>

<span data-ttu-id="fd531-282">如需使用識別體驗架構之 Azure AD B2C 中自訂原則的概觀，請參閱 [Azure Active Directory B2C：自訂原則](active-directory-b2c-overview-custom.md)一文。</span><span class="sxs-lookup"><span data-stu-id="fd531-282">For an overview of custom policies in Azure AD B2C that use the Identity Experience Framework, see the [Azure Active Directory B2C: Custom policies](active-directory-b2c-overview-custom.md) article.</span></span> 
