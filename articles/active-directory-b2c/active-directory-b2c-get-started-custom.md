---
title: "Azure Active Directory B2C：開始使用自訂原則 | Microsoft Docs"
description: "Tooget 如何開始使用 Azure Active Directory B2C 的自訂原則"
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
ms.openlocfilehash: 5ee133806395cddf18682769a6cad149889d82d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-get-started-with-custom-policies"></a><span data-ttu-id="ff3a3-103">Azure Active Directory B2C：開始使用自訂原則</span><span class="sxs-lookup"><span data-stu-id="ff3a3-103">Azure Active Directory B2C: Get started with custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="ff3a3-104">完成本文中的 hello 步驟之後，您的自訂原則將會支援 「 本機帳戶 」 註冊或登入透過電子郵件地址和密碼。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-104">After you complete hello steps in this article, your custom policy will support "local account" sign-up or sign-in via an email address and password.</span></span> <span data-ttu-id="ff3a3-105">您也會準備環境以新增識別提供者 (例如 Facebook 或 Azure Active Directory)。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-105">You will also prepare your environment for adding identity providers (like Facebook or Azure Active Directory).</span></span> <span data-ttu-id="ff3a3-106">我們鼓勵您 toocomplete 有關其他讀取之前，先依照使用的 hello Azure Active Directory (Azure AD) B2C 身分識別體驗架構。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-106">We encourage you toocomplete these steps before reading about other uses of hello Azure Active Directory (Azure AD) B2C Identity Experience Framework.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff3a3-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="ff3a3-107">Prerequisites</span></span>

<span data-ttu-id="ff3a3-108">繼續之前，請確定具有 Azure AD B2C 租用戶。此租用戶是存放您的所有使用者、應用程式、原則等的容器。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-108">Before proceeding, ensure that you have an Azure AD B2C tenant, which is a container for all your users, apps, policies, and more.</span></span> <span data-ttu-id="ff3a3-109">如果您還沒有已經，您需要太[建立 Azure AD B2C 租用戶](active-directory-b2c-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-109">If you don't have one already, you need too[create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span> <span data-ttu-id="ff3a3-110">我們強烈建議所有開發人員 toocomplete hello Azure AD B2C 內建原則逐步解說，並使用內建原則，才能繼續設定其應用程式。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-110">We strongly encourage all developers toocomplete hello Azure AD B2C built-in policy walkthroughs and configure their applications with built-in policies before proceeding.</span></span> <span data-ttu-id="ff3a3-111">一旦您進行微幅變更 toohello 原則名稱 tooinvoke hello 自訂原則，您的應用程式將會使用這兩種原則類型。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-111">Your applications will work with both types of policies once you make a minor change toohello policy name tooinvoke hello custom policy.</span></span>

>[!NOTE]
><span data-ttu-id="ff3a3-112">編輯 tooaccess 自訂原則，您需要有效的 Azure 訂用帳戶連結的 tooyour 租用戶。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-112">tooaccess custom policy editing, you need a valid Azure subscription linked tooyour tenant.</span></span> <span data-ttu-id="ff3a3-113">如果還沒有[連結您 Azure 訂用帳戶的 Azure AD B2C 租用戶 tooan](active-directory-b2c-how-to-enable-billing.md)或您的 Azure 訂用帳戶已停用，hello 身分識別體驗架構按鈕將無法使用。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-113">If you haven't [linked your Azure AD B2C tenant tooan Azure subscription](active-directory-b2c-how-to-enable-billing.md) or your Azure subscription is disabled, hello Identity Experience Framework button won't be available.</span></span>

## <a name="add-signing-and-encryption-keys-tooyour-b2c-tenant-for-use-by-custom-policies"></a><span data-ttu-id="ff3a3-114">新增簽章和加密金鑰 tooyour B2C 租用戶使用的自訂原則</span><span class="sxs-lookup"><span data-stu-id="ff3a3-114">Add signing and encryption keys tooyour B2C tenant for use by custom policies</span></span>

1. <span data-ttu-id="ff3a3-115">開啟 hello**身分識別體驗架構**刀鋒視窗，在您的 Azure AD B2C 租用戶設定。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-115">Open hello **Identity Experience Framework** blade in your Azure AD B2C tenant settings.</span></span>
2. <span data-ttu-id="ff3a3-116">選取**原則機碼**tooview hello 金鑰用於您的租用戶。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-116">Select **Policy Keys** tooview hello keys available in your tenant.</span></span>
3. <span data-ttu-id="ff3a3-117">如果 B2C_1A_TokenSigningKeyContainer 不存在，請加以建立：</span><span class="sxs-lookup"><span data-stu-id="ff3a3-117">Create B2C_1A_TokenSigningKeyContainer if it does not exist:</span></span><br>
    <span data-ttu-id="ff3a3-118">a.</span><span class="sxs-lookup"><span data-stu-id="ff3a3-118">a.</span></span> <span data-ttu-id="ff3a3-119">選取 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-119">Select **Add**.</span></span> <br>
    <span data-ttu-id="ff3a3-120">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-120">b.</span></span> <span data-ttu-id="ff3a3-121">選取 [產生]。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-121">Select **Generate**.</span></span><br>
    <span data-ttu-id="ff3a3-122">c.</span><span class="sxs-lookup"><span data-stu-id="ff3a3-122">c.</span></span> <span data-ttu-id="ff3a3-123">針對 [名稱] 使用 `TokenSigningKeyContainer`。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-123">For **Name**, use `TokenSigningKeyContainer`.</span></span> <br> 
    <span data-ttu-id="ff3a3-124">hello 前置詞`B2C_1A_`可能會自動加入。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-124">hello prefix `B2C_1A_` might be added automatically.</span></span><br>
    <span data-ttu-id="ff3a3-125">d.</span><span class="sxs-lookup"><span data-stu-id="ff3a3-125">d.</span></span> <span data-ttu-id="ff3a3-126">針對 [金鑰類型] 使用 [RSA]。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-126">For **Key type**, use **RSA**.</span></span><br>
    <span data-ttu-id="ff3a3-127">e.</span><span class="sxs-lookup"><span data-stu-id="ff3a3-127">e.</span></span> <span data-ttu-id="ff3a3-128">如**日期**，使用 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-128">For **Dates**, use hello defaults.</span></span> <br>
    <span data-ttu-id="ff3a3-129">f.</span><span class="sxs-lookup"><span data-stu-id="ff3a3-129">f.</span></span> <span data-ttu-id="ff3a3-130">針對 [金鑰使用方法] 使用 [簽章]。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-130">For **Key usage**, use **Signature**.</span></span><br>
    <span data-ttu-id="ff3a3-131">g.</span><span class="sxs-lookup"><span data-stu-id="ff3a3-131">g.</span></span> <span data-ttu-id="ff3a3-132">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-132">Select **Create**.</span></span><br>
4. <span data-ttu-id="ff3a3-133">如果 B2C_1A_TokenEncryptionKeyContainer 不存在，請加以建立：</span><span class="sxs-lookup"><span data-stu-id="ff3a3-133">Create B2C_1A_TokenEncryptionKeyContainer if it does not exist:</span></span><br>
 <span data-ttu-id="ff3a3-134">a.</span><span class="sxs-lookup"><span data-stu-id="ff3a3-134">a.</span></span> <span data-ttu-id="ff3a3-135">選取 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-135">Select **Add**.</span></span><br>
 <span data-ttu-id="ff3a3-136">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-136">b.</span></span> <span data-ttu-id="ff3a3-137">選取 [產生]。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-137">Select **Generate**.</span></span><br>
 <span data-ttu-id="ff3a3-138">c.</span><span class="sxs-lookup"><span data-stu-id="ff3a3-138">c.</span></span> <span data-ttu-id="ff3a3-139">針對 [名稱] 使用 `TokenEncryptionKeyContainer`。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-139">For **Name**, use `TokenEncryptionKeyContainer`.</span></span> <br>
   <span data-ttu-id="ff3a3-140">hello 前置詞`B2C_1A`_ 可能會自動加入。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-140">hello prefix `B2C_1A`_ might be added automatically.</span></span><br>
 <span data-ttu-id="ff3a3-141">d.</span><span class="sxs-lookup"><span data-stu-id="ff3a3-141">d.</span></span> <span data-ttu-id="ff3a3-142">針對 [金鑰類型] 使用 [RSA]。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-142">For **Key type**, use **RSA**.</span></span><br>
 <span data-ttu-id="ff3a3-143">e.</span><span class="sxs-lookup"><span data-stu-id="ff3a3-143">e.</span></span> <span data-ttu-id="ff3a3-144">如**日期**，使用 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-144">For **Dates**, use hello defaults.</span></span><br>
 <span data-ttu-id="ff3a3-145">f.</span><span class="sxs-lookup"><span data-stu-id="ff3a3-145">f.</span></span> <span data-ttu-id="ff3a3-146">針對 [金鑰使用方法] 使用 [加密]。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-146">For **Key usage**, use **Encryption**.</span></span><br>
 <span data-ttu-id="ff3a3-147">g.</span><span class="sxs-lookup"><span data-stu-id="ff3a3-147">g.</span></span> <span data-ttu-id="ff3a3-148">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-148">Select **Create**.</span></span><br>
5. <span data-ttu-id="ff3a3-149">建立 B2C_1A_FacebookSecret。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-149">Create B2C_1A_FacebookSecret.</span></span> <br>
<span data-ttu-id="ff3a3-150">如果您已經有 Facebook 應用程式密碼，請將它加入做為原則金鑰 tooyour 租用戶。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-150">If you already have a Facebook application secret, add it as a policy key tooyour tenant.</span></span> <span data-ttu-id="ff3a3-151">否則，您必須建立 hello 金鑰預留位置值，讓您的原則通過驗證。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-151">Otherwise, you must create hello key with a placeholder value so that your policies pass validation.</span></span><br>
 <span data-ttu-id="ff3a3-152">a.</span><span class="sxs-lookup"><span data-stu-id="ff3a3-152">a.</span></span> <span data-ttu-id="ff3a3-153">選取 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-153">Select **Add**.</span></span><br>
 <span data-ttu-id="ff3a3-154">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-154">b.</span></span> <span data-ttu-id="ff3a3-155">針對 [選項] 使用 [手動]。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-155">For **Options**, use **Manual**.</span></span><br>
 <span data-ttu-id="ff3a3-156">c.</span><span class="sxs-lookup"><span data-stu-id="ff3a3-156">c.</span></span> <span data-ttu-id="ff3a3-157">針對 [名稱] 使用 `FacebookSecret`。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-157">For **Name**, use `FacebookSecret`.</span></span> <br>
 <span data-ttu-id="ff3a3-158">hello 前置詞`B2C_1A_`可能會自動加入。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-158">hello prefix `B2C_1A_` might be added automatically.</span></span><br>
 <span data-ttu-id="ff3a3-159">d.</span><span class="sxs-lookup"><span data-stu-id="ff3a3-159">d.</span></span> <span data-ttu-id="ff3a3-160">在 [hello**密碼**方塊中，輸入您 FacebookSecret 從 developers.facebook.com 或`0`做為預留位置。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-160">In hello **Secret** box, enter your FacebookSecret from developers.facebook.com or `0` as a placeholder.</span></span> <span data-ttu-id="ff3a3-161">這不是您的 Facebook 應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-161">*This is not your Facebook app ID.*</span></span> <br>
 <span data-ttu-id="ff3a3-162">e.</span><span class="sxs-lookup"><span data-stu-id="ff3a3-162">e.</span></span> <span data-ttu-id="ff3a3-163">針對 [金鑰使用方法] 使用 [簽章]。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-163">For **Key usage**, use **Signature**.</span></span> <br>
 <span data-ttu-id="ff3a3-164">f.</span><span class="sxs-lookup"><span data-stu-id="ff3a3-164">f.</span></span> <span data-ttu-id="ff3a3-165">選取 [建立] 並確認建立。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-165">Select **Create** and confirm creation.</span></span>

## <a name="register-identity-experience-framework-applications"></a><span data-ttu-id="ff3a3-166">註冊身分識別體驗架構應用程式</span><span class="sxs-lookup"><span data-stu-id="ff3a3-166">Register Identity Experience Framework applications</span></span>

<span data-ttu-id="ff3a3-167">Azure AD B2C 需要 tooregister 兩個額外的應用程式所使用的總 hello 引擎 toosign 並登入使用者。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-167">Azure AD B2C requires you tooregister two extra applications that are used by hello engine toosign up and sign in users.</span></span>

>[!NOTE]
><span data-ttu-id="ff3a3-168">您必須建立兩個應用程式的啟用登入使用本機帳戶： IdentityExperienceFramework （web 應用程式） 和 ProxyIdentityExperienceFramework （原生應用程式） 與委派 hello IdentityExperienceFramework 應用程式的權限。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-168">You must create two applications that enable sign-in using local accounts: IdentityExperienceFramework (a web app) and ProxyIdentityExperienceFramework (a native app) with delegated permission from hello IdentityExperienceFramework app.</span></span> <span data-ttu-id="ff3a3-169">本機帳戶只存在於您的租用戶。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-169">Local accounts exist only in your tenant.</span></span> <span data-ttu-id="ff3a3-170">您的使用者註冊使用唯一的電子郵件地址/密碼組合 tooaccess 您租用戶註冊的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-170">Your users sign up with a unique email address/password combination tooaccess your tenant-registered applications.</span></span>

### <a name="create-hello-identityexperienceframework-application"></a><span data-ttu-id="ff3a3-171">建立 hello IdentityExperienceFramework 應用程式</span><span class="sxs-lookup"><span data-stu-id="ff3a3-171">Create hello IdentityExperienceFramework application</span></span>

1. <span data-ttu-id="ff3a3-172">在 [hello [Azure 入口網站](https://portal.azure.com)，切換至 hello[內容，您的 Azure AD B2C 租用戶](active-directory-b2c-navigate-to-b2c-context.md)。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-172">In hello [Azure portal](https://portal.azure.com), switch into hello [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md).</span></span>
2. <span data-ttu-id="ff3a3-173">開啟 hello **Azure Active Directory**刀鋒視窗 (不 hello **Azure AD B2C**刀鋒視窗)。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-173">Open hello **Azure Active Directory** blade (not hello **Azure AD B2C** blade).</span></span> <span data-ttu-id="ff3a3-174">您可能需要 tooselect**更服務**toofind 它。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-174">You might need tooselect **More Services** toofind it.</span></span>
3. <span data-ttu-id="ff3a3-175">選取 [應用程式註冊]。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-175">Select **App registrations**.</span></span>
4. <span data-ttu-id="ff3a3-176">選取 [新增應用程式註冊]。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-176">Select **New application registration**.</span></span>
   * <span data-ttu-id="ff3a3-177">針對 [名稱] 使用 `IdentityExperienceFramework`。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-177">For **Name**, use `IdentityExperienceFramework`.</span></span>
   * <span data-ttu-id="ff3a3-178">針對 [應用程式類型] 使用 [Web 應用程式/API]。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-178">For **Application type**, use **Web app/API**.</span></span>
   * <span data-ttu-id="ff3a3-179">針對 [登入 URL] 使用 `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`，其中 `yourtenant` 是您的 Azure AD B2C 租用戶網域名稱。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-179">For **Sign-on URL**, use `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`, where `yourtenant` is your Azure AD B2C tenant domain name.</span></span>
5. <span data-ttu-id="ff3a3-180">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-180">Select **Create**.</span></span>
6. <span data-ttu-id="ff3a3-181">一旦建立之後，選取新建立的 hello 應用程式**IdentityExperienceFramework**。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-181">Once it is created, select hello newly created application **IdentityExperienceFramework**.</span></span><br>
   * <span data-ttu-id="ff3a3-182">選取 [屬性] 。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-182">Select **Properties**.</span></span><br>
   * <span data-ttu-id="ff3a3-183">複製 hello 應用程式識別碼，並將它儲存為更新版本。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-183">Copy hello application ID and save it for later.</span></span>

### <a name="create-hello-proxyidentityexperienceframework-application"></a><span data-ttu-id="ff3a3-184">建立 hello ProxyIdentityExperienceFramework 應用程式</span><span class="sxs-lookup"><span data-stu-id="ff3a3-184">Create hello ProxyIdentityExperienceFramework application</span></span>

1. <span data-ttu-id="ff3a3-185">選取 [應用程式註冊]。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-185">Select **App registrations**.</span></span>
1. <span data-ttu-id="ff3a3-186">選取 [新增應用程式註冊]。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-186">Select **New application registration**.</span></span>
   * <span data-ttu-id="ff3a3-187">針對 [名稱] 使用 `ProxyIdentityExperienceFramework`。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-187">For **Name**, use `ProxyIdentityExperienceFramework`.</span></span>
   * <span data-ttu-id="ff3a3-188">針對 [應用程式類型] 使用 [原生]。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-188">For **Application type**, use **Native**.</span></span>
   * <span data-ttu-id="ff3a3-189">針對 [重新導向 URI] 使用 `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`，其中 `yourtenant` 是您的 Azure AD B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-189">For **Redirect URI**, use `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`, where `yourtenant` is your Azure AD B2C tenant.</span></span>
1. <span data-ttu-id="ff3a3-190">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-190">Select **Create**.</span></span>
1. <span data-ttu-id="ff3a3-191">一旦建立它，選取 hello 應用程式**ProxyIdentityExperienceFramework**。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-191">Once it has been created, select hello application **ProxyIdentityExperienceFramework**.</span></span><br>
   * <span data-ttu-id="ff3a3-192">選取 [屬性] 。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-192">Select **Properties**.</span></span> <br>
   * <span data-ttu-id="ff3a3-193">複製 hello 應用程式識別碼，並將它儲存為更新版本。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-193">Copy hello application ID and save it for later.</span></span>
1. <span data-ttu-id="ff3a3-194">選取 [必要權限]。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-194">Select **Required permissions**.</span></span>
1. <span data-ttu-id="ff3a3-195">選取 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-195">Select **Add**.</span></span>
1. <span data-ttu-id="ff3a3-196">選取 [選取 API]。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-196">Select **Select an API**.</span></span>
1. <span data-ttu-id="ff3a3-197">搜尋 hello 名稱 IdentityExperienceFramework。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-197">Search for hello name IdentityExperienceFramework.</span></span> <span data-ttu-id="ff3a3-198">選取**IdentityExperienceFramework**在 hello 結果，然後按一下 [**選取**。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-198">Select **IdentityExperienceFramework** in hello results, and then click **Select**.</span></span>
1. <span data-ttu-id="ff3a3-199">選取 [hello] 核取方塊旁太**存取 IdentityExperienceFramework**，然後按一下 [**選取**。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-199">Select hello check box next too**Access IdentityExperienceFramework**, and then click **Select**.</span></span>
1. <span data-ttu-id="ff3a3-200">選取 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-200">Select **Done**.</span></span>
1. <span data-ttu-id="ff3a3-201">選取 [授與權限]，然後選取 [是] 加以確認。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-201">Select **Grant Permissions**, and then confirm by selecting **Yes**.</span></span>

## <a name="download-starter-pack-and-modify-policies"></a><span data-ttu-id="ff3a3-202">下載入門套件和修改原則</span><span class="sxs-lookup"><span data-stu-id="ff3a3-202">Download starter pack and modify policies</span></span>

<span data-ttu-id="ff3a3-203">自訂的原則是一組需要上傳 toobe tooyour Azure AD B2C 租用戶的 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-203">Custom policies are a set of XML files that need toobe uploaded tooyour Azure AD B2C tenant.</span></span> <span data-ttu-id="ff3a3-204">我們提供入門套件 tooget 您快速地移。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-204">We provide starter packs tooget you going quickly.</span></span> <span data-ttu-id="ff3a3-205">Hello 下列清單中的每個入門套件包含 hello 的技術的設定檔的最小數目，而且使用者皆需要 tooachieve hello 案例所述：</span><span class="sxs-lookup"><span data-stu-id="ff3a3-205">Each starter pack in hello following list contains hello smallest number of technical profiles and user journeys needed tooachieve hello scenarios described:</span></span>
 * <span data-ttu-id="ff3a3-206">LocalAccounts。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-206">LocalAccounts.</span></span> <span data-ttu-id="ff3a3-207">可讓您使用本機帳戶只 hello。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-207">Enables hello use of local accounts only.</span></span>
 * <span data-ttu-id="ff3a3-208">SocialAccounts。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-208">SocialAccounts.</span></span> <span data-ttu-id="ff3a3-209">可讓您使用 hello 社交 （或同盟） 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-209">Enables hello use of social (or federated) accounts only.</span></span>
 * <span data-ttu-id="ff3a3-210">**SocialAndLocalAccounts**。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-210">**SocialAndLocalAccounts**.</span></span> <span data-ttu-id="ff3a3-211">我們 hello 逐步解說使用這個檔案。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-211">We use this file for hello walkthrough.</span></span>
 * <span data-ttu-id="ff3a3-212">SocialAndLocalAccountsWithMFA。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-212">SocialAndLocalAccountsWithMFA.</span></span> <span data-ttu-id="ff3a3-213">此處包含社交、本機及 Multi-Factor Authentication 選項。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-213">Social, local, and Multi-Factor Authentication options are included here.</span></span>

<span data-ttu-id="ff3a3-214">每個入門套件均包含：</span><span class="sxs-lookup"><span data-stu-id="ff3a3-214">Each starter pack contains:</span></span>

* <span data-ttu-id="ff3a3-215">hello[基底檔案](active-directory-b2c-overview-custom.md#policy-files)的 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-215">hello [base file](active-directory-b2c-overview-custom.md#policy-files) of hello policy.</span></span> <span data-ttu-id="ff3a3-216">一些修改，就需要的 toohello 基底。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-216">Few modifications are required toohello base.</span></span>
* <span data-ttu-id="ff3a3-217">hello[延伸模組檔案](active-directory-b2c-overview-custom.md#policy-files)的 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-217">hello [extension file](active-directory-b2c-overview-custom.md#policy-files) of hello policy.</span></span>  <span data-ttu-id="ff3a3-218">大部分的設定變更都在這個檔案中完成。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-218">This file is where most configuration changes are made.</span></span>
* <span data-ttu-id="ff3a3-219">[信賴憑證者檔案](active-directory-b2c-overview-custom.md#policy-files)是工作特定檔案，由應用程式呼叫。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-219">[Relying party files](active-directory-b2c-overview-custom.md#policy-files) are task-specific files called by your application.</span></span>

>[!NOTE]
><span data-ttu-id="ff3a3-220">如果您的 XML 編輯器支援驗證，驗證位於 hello 入門套件 hello 根目錄中的 hello TrustFrameworkPolicy_0.3.0.0.xsd XML 結構描述中的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-220">If your XML editor supports validation, validate hello files against hello TrustFrameworkPolicy_0.3.0.0.xsd XML schema that is located in hello root directory of hello starter pack.</span></span> <span data-ttu-id="ff3a3-221">在上載之前，XML 結構描述驗證會識別錯誤。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-221">XML schema validation identifies errors before uploading.</span></span>

 <span data-ttu-id="ff3a3-222">現在就開始吧！</span><span class="sxs-lookup"><span data-stu-id="ff3a3-222">Let's get started:</span></span>

1. <span data-ttu-id="ff3a3-223">從 GitHub 下載 active-directory-b2c-custom-policy-starterpack。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-223">Download active-directory-b2c-custom-policy-starterpack from GitHub.</span></span> <span data-ttu-id="ff3a3-224">[下載 hello.zip 檔案](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/archive/master.zip)或執行</span><span class="sxs-lookup"><span data-stu-id="ff3a3-224">[Download hello .zip file](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/archive/master.zip) or run</span></span>

    ```console
    git clone https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack
    ```
2. <span data-ttu-id="ff3a3-225">開啟 hello SocialAndLocalAccounts 資料夾。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-225">Open hello SocialAndLocalAccounts folder.</span></span>  <span data-ttu-id="ff3a3-226">hello 基底檔案 (TrustFrameworkBase.xml)，此資料夾中的包含所需的本機和公司身分證/帳戶內容。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-226">hello base file (TrustFrameworkBase.xml) in this folder contains content needed for both local and social/corporate accounts.</span></span> <span data-ttu-id="ff3a3-227">hello 社交內容不會干擾 hello 快速安裝的本機帳戶和執行的步驟。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-227">hello social content does not interfere with hello steps for getting local accounts up and running.</span></span>
3. <span data-ttu-id="ff3a3-228">開啟 TrustFrameworkBase.xml。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-228">Open TrustFrameworkBase.xml.</span></span> <span data-ttu-id="ff3a3-229">如果您需要 XML 編輯器，請[試用 Visual Studio 程式碼](https://code.visualstudio.com/download)，這是一個輕巧的跨平台編輯器。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-229">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
4. <span data-ttu-id="ff3a3-230">Hello 根目錄中`TrustFrameworkPolicy`元素中，更新 hello`TenantId`和`PublicPolicyUri`屬性、 取代`yourtenant.onmicrosoft.com`hello 網域名稱，您的 Azure AD B2C 租用戶：</span><span class="sxs-lookup"><span data-stu-id="ff3a3-230">In hello root `TrustFrameworkPolicy` element, update hello `TenantId` and `PublicPolicyUri` attributes, replacing `yourtenant.onmicrosoft.com` with hello domain name of your Azure AD B2C tenant:</span></span>
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
   ><span data-ttu-id="ff3a3-231">`PolicyId`是您在 hello 入口網站中看到的 hello 原則名稱和 hello 用這個原則檔正由其他原則檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-231">`PolicyId` is hello policy name that you see in hello portal and hello name by which this policy file is referenced by other policy files.</span></span>

5. <span data-ttu-id="ff3a3-232">儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-232">Save hello file.</span></span>
6. <span data-ttu-id="ff3a3-233">開啟 TrustFrameworkExtensions.xml。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-233">Open TrustFrameworkExtensions.xml.</span></span> <span data-ttu-id="ff3a3-234">進行相同的兩個變更 hello 取代`yourtenant.onmicrosoft.com`與 Azure AD B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-234">Make hello same two changes by replacing `yourtenant.onmicrosoft.com` with your Azure AD B2C tenant.</span></span> <span data-ttu-id="ff3a3-235">請 hello 相同 hello 中的取代`<TenantId>`總共有三個變更的項目。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-235">Make hello same replacement in hello `<TenantId>` element for a total of three changes.</span></span> <span data-ttu-id="ff3a3-236">儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-236">Save hello file.</span></span>
7. <span data-ttu-id="ff3a3-237">開啟 SignUpOrSignIn.xml。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-237">Open SignUpOrSignIn.xml.</span></span> <span data-ttu-id="ff3a3-238">進行相同變更 hello 取代`yourtenant.onmicrosoft.com`與 Azure AD B2C 租用戶在三個位置。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-238">Make hello same changes by replacing `yourtenant.onmicrosoft.com` with your Azure AD B2C tenant in three places.</span></span> <span data-ttu-id="ff3a3-239">儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-239">Save hello file.</span></span>
8. <span data-ttu-id="ff3a3-240">開啟 hello 密碼重設和設定檔編輯檔案。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-240">Open hello password reset and profile edit files.</span></span> <span data-ttu-id="ff3a3-241">進行相同變更 hello 取代`yourtenant.onmicrosoft.com`與 Azure AD B2C 租用戶的每個檔案中的三個位置。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-241">Make hello same changes by replacing `yourtenant.onmicrosoft.com` with your Azure AD B2C tenant in three places in each file.</span></span> <span data-ttu-id="ff3a3-242">儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-242">Save hello files.</span></span>

### <a name="add-hello-application-ids-tooyour-custom-policy"></a><span data-ttu-id="ff3a3-243">新增 hello 應用程式識別碼 tooyour 自訂原則</span><span class="sxs-lookup"><span data-stu-id="ff3a3-243">Add hello application IDs tooyour custom policy</span></span>
<span data-ttu-id="ff3a3-244">加入 hello 應用程式識別碼 toohello 延伸模組檔案 (`TrustFrameworkExtensions.xml`):</span><span class="sxs-lookup"><span data-stu-id="ff3a3-244">Add hello application IDs toohello extensions file (`TrustFrameworkExtensions.xml`):</span></span>

1. <span data-ttu-id="ff3a3-245">在 hello 延伸模組檔案 (TrustFrameworkExtensions.xml)，尋找 [hello 元素`<TechnicalProfile Id="login-NonInteractive">`。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-245">In hello extensions file (TrustFrameworkExtensions.xml), find hello element `<TechnicalProfile Id="login-NonInteractive">`.</span></span>
2. <span data-ttu-id="ff3a3-246">取代的兩個執行個體`IdentityExperienceFrameworkAppId`hello 的 hello 您稍早建立的身分識別體驗架構應用程式的應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-246">Replace both instances of `IdentityExperienceFrameworkAppId` with hello application ID of hello Identity Experience Framework application that you created earlier.</span></span> <span data-ttu-id="ff3a3-247">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="ff3a3-247">Here is an example:</span></span>

   ```xml
   <Item Key="client_id">8322dedc-cbf4-43bc-8bb6-141d16f0f489</Item>
   ```
3. <span data-ttu-id="ff3a3-248">取代的兩個執行個體`ProxyIdentityExperienceFrameworkAppId`hello 的 hello 您稍早建立的 Proxy 識別體驗架構應用程式的應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-248">Replace both instances of `ProxyIdentityExperienceFrameworkAppId` with hello application ID of hello Proxy Identity Experience Framework application that you created earlier.</span></span>
4. <span data-ttu-id="ff3a3-249">儲存擴充檔案。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-249">Save your extensions file.</span></span>

## <a name="upload-hello-policies-tooyour-tenant"></a><span data-ttu-id="ff3a3-250">上傳 hello 原則 tooyour 租用戶</span><span class="sxs-lookup"><span data-stu-id="ff3a3-250">Upload hello policies tooyour tenant</span></span>

1. <span data-ttu-id="ff3a3-251">在 hello [Azure 入口網站](https://portal.azure.com)，切換至 hello[內容，您的 Azure AD B2C 租用戶](active-directory-b2c-navigate-to-b2c-context.md)，並開啟 hello **Azure AD B2C**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-251">In hello [Azure portal](https://portal.azure.com), switch into hello [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open hello **Azure AD B2C** blade.</span></span>
2. <span data-ttu-id="ff3a3-252">選取 [識別體驗架構]。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-252">Select **Identity Experience Framework**.</span></span>
3. <span data-ttu-id="ff3a3-253">選取 [上傳原則]。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-253">Select **Upload Policy**.</span></span>

    >[!WARNING]
    ><span data-ttu-id="ff3a3-254">hello 自訂原則檔案必須上傳中順序的 hello:</span><span class="sxs-lookup"><span data-stu-id="ff3a3-254">hello custom policy files must be uploaded in hello following order:</span></span>

1. <span data-ttu-id="ff3a3-255">上傳 TrustFrameworkBase.xml。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-255">Upload TrustFrameworkBase.xml.</span></span>
2. <span data-ttu-id="ff3a3-256">上傳 TrustFrameworkExtensions.xml。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-256">Upload TrustFrameworkExtensions.xml.</span></span>
3. <span data-ttu-id="ff3a3-257">上傳 SignUpOrSignin.xml。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-257">Upload SignUpOrSignin.xml.</span></span>
4. <span data-ttu-id="ff3a3-258">上傳其他原則檔案。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-258">Upload your other policy files.</span></span>

<span data-ttu-id="ff3a3-259">上傳檔案時，hello hello 原則檔案名稱前面會加上`B2C_1A_`。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-259">When a file is uploaded, hello name of hello policy file is prepended with `B2C_1A_`.</span></span>

## <a name="test-hello-custom-policy-by-using-run-now"></a><span data-ttu-id="ff3a3-260">使用 [立即執行測試 hello 自訂原則</span><span class="sxs-lookup"><span data-stu-id="ff3a3-260">Test hello custom policy by using Run Now</span></span>

1. <span data-ttu-id="ff3a3-261">開啟**Azure AD B2C 設定**並移過**身分識別體驗架構**。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-261">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="ff3a3-262">**現在就執行**需要至少一個應用程式 toobe 預先 hello 租用戶上。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-262">**Run now** requires at least one application toobe preregistered on hello tenant.</span></span> <span data-ttu-id="ff3a3-263">應用程式必須使用 hello hello B2C 租用戶中註冊**應用程式**功能表選取項目在 Azure AD B2C 或使用 hello 身分識別體驗架構 tooinvoke 內建和自訂原則。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-263">Applications must be registered in hello B2C tenant, either by using hello **Applications** menu selection in Azure AD B2C or by using hello Identity Experience Framework tooinvoke both built-in and custom policies.</span></span> <span data-ttu-id="ff3a3-264">每個應用程式只需要一個註冊。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-264">Only one registration per application is needed.</span></span><br><br>
   <span data-ttu-id="ff3a3-265">如何 tooregister 應用程式，請參閱的 toolearn hello Azure AD B2C[開始](active-directory-b2c-get-started.md)文章或 hello[應用程式註冊](active-directory-b2c-app-registration.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-265">toolearn how tooregister applications, see hello Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or hello [Application registration](active-directory-b2c-app-registration.md) article.</span></span>  

2. <span data-ttu-id="ff3a3-266">開啟 B2C_1A_signup_signin、 hello 上載的信賴憑證者 (rp) 自訂原則。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-266">Open B2C_1A_signup_signin, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="ff3a3-267">選取 [立即執行]。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-267">Select **Run now**.</span></span>

3. <span data-ttu-id="ff3a3-268">您應該能夠 toosign 使用電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-268">You should be able toosign up using an email address.</span></span>

4. <span data-ttu-id="ff3a3-269">使用登入 hello tooconfirm，您必須使用相同帳戶 hello 正確的組態。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-269">Sign in with hello same account tooconfirm that you have hello correct configuration.</span></span>

>[!NOTE]
><span data-ttu-id="ff3a3-270">登入失敗的常見原因是 IdentityExperienceFramework 應用程式設定不正確。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-270">A common cause of sign-in failure is an improperly configured IdentityExperienceFramework app.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ff3a3-271">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ff3a3-271">Next steps</span></span>

### <a name="add-facebook-as-an-identity-provider"></a><span data-ttu-id="ff3a3-272">將 Facebook 新增為識別提供者</span><span class="sxs-lookup"><span data-stu-id="ff3a3-272">Add Facebook as an identity provider</span></span>
<span data-ttu-id="ff3a3-273">註冊 Facebook tooset:</span><span class="sxs-lookup"><span data-stu-id="ff3a3-273">tooset up Facebook:</span></span>
1. <span data-ttu-id="ff3a3-274">[在 developers.facebook.com 中設定 Facebook 應用程式](active-directory-b2c-setup-fb-app.md)。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-274">[Configure a Facebook application in developers.facebook.com](active-directory-b2c-setup-fb-app.md).</span></span>
2. <span data-ttu-id="ff3a3-275">[新增 hello Facebook 應用程式密碼 tooyour Azure AD B2C 租用戶](#add-signing-and-encryption-keys-to-your-b2c-tenant-for-use-by-custom-policies)。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-275">[Add hello Facebook application secret tooyour Azure AD B2C tenant](#add-signing-and-encryption-keys-to-your-b2c-tenant-for-use-by-custom-policies).</span></span>
3. <span data-ttu-id="ff3a3-276">在 hello TrustFrameworkExtensions 原則檔案中，以取代 hello 值`client_id`hello Facebook 應用程式識別碼：</span><span class="sxs-lookup"><span data-stu-id="ff3a3-276">In hello TrustFrameworkExtensions policy file, replace hello value of `client_id` with hello Facebook application ID:</span></span>

   ```xml
   <TechnicalProfile Id="Facebook-OAUTH">
     <Metadata>
     <!--Replace hello value of client_id in this technical profile with hello Facebook app ID"-->
       <Item Key="client_id">00000000000000</Item>
   ```
4. <span data-ttu-id="ff3a3-277">上傳 hello TrustFrameworkExtensions.xml 原則檔案 tooyour 租用戶。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-277">Upload hello TrustFrameworkExtensions.xml policy file tooyour tenant.</span></span>
5. <span data-ttu-id="ff3a3-278">使用測試**立即執行**或叫用 hello 原則直接從您已註冊的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-278">Test by using **Run now** or by invoking hello policy directly from your registered application.</span></span>

### <a name="add-azure-active-directory-as-an-identity-provider"></a><span data-ttu-id="ff3a3-279">將 Azure Active Directory 新增為識別提供者</span><span class="sxs-lookup"><span data-stu-id="ff3a3-279">Add Azure Active Directory as an identity provider</span></span>
<span data-ttu-id="ff3a3-280">hello 已經用於這個使用者入門指南的基底檔案可包含一些您需要新增其他身分識別提供者的 hello 內容。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-280">hello base file used in this getting started guide already contains some of hello content that you need for adding other identity providers.</span></span> <span data-ttu-id="ff3a3-281">如需設定登入資訊，請參閱 hello [Azure Active Directory B2C： 使用 Azure AD 帳戶登入](active-directory-b2c-setup-aad-custom.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-281">For information on setting up sign-ins, see hello [Azure Active Directory B2C: Sign in by using Azure AD accounts](active-directory-b2c-setup-aad-custom.md) article.</span></span>

<span data-ttu-id="ff3a3-282">如需在 Azure AD B2C 使用 hello 身分識別體驗架構的自訂原則的概觀，請參閱 hello [Azure Active Directory B2C： 自訂原則](active-directory-b2c-overview-custom.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="ff3a3-282">For an overview of custom policies in Azure AD B2C that use hello Identity Experience Framework, see hello [Azure Active Directory B2C: Custom policies](active-directory-b2c-overview-custom.md) article.</span></span> 
