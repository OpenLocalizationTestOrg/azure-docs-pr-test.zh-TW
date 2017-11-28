---
title: "Azure Active Directory B2C：針對自訂原則進行疑難排解 | Microsoft Docs"
description: "了解方法 toosolving 錯誤時使用的 Azure Active Directory 中的自訂原則。"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: joroja
ms.openlocfilehash: b9e1b46df1ddb29cdb90953e4a0d6f1dd085441f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-ad-b2c-custom-policies-and-identity-experience-framework"></a><span data-ttu-id="32b65-103">針對 Azure AD B2C 自訂原則和身分識別體驗架構進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="32b65-103">Troubleshoot Azure AD B2C custom policies and Identity Experience Framework</span></span>

<span data-ttu-id="32b65-104">如果您使用 Azure Active Directory B2C (Azure AD B2C) 的自訂原則，您可能會遇到設定 hello 身分識別遇到架構原則語言 XML 格式的挑戰。</span><span class="sxs-lookup"><span data-stu-id="32b65-104">If you use Azure Active Directory B2C (Azure AD B2C) custom policies, you might experience challenges setting up hello Identity Experience Framework in its policy language XML format.</span></span>  <span data-ttu-id="32b65-105">學習 toowrite 自訂原則可以如同學習新的語言。</span><span class="sxs-lookup"><span data-stu-id="32b65-105">Learning toowrite custom policies can be like learning a new language.</span></span> <span data-ttu-id="32b65-106">在本文中，我們將說明可協助您快速找出並解決問題的工具和提示。</span><span class="sxs-lookup"><span data-stu-id="32b65-106">In this article, we describe tools and tips that can help you quickly discover and resolve issues.</span></span> 

> [!NOTE]
> <span data-ttu-id="32b65-107">本文著重在針對 Azure AD B2C 自訂原則設定進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="32b65-107">This article focuses on troubleshooting your Azure AD B2C custom policy configuration.</span></span> <span data-ttu-id="32b65-108">它不能處理 hello 信賴憑證者的合作對象應用程式或其身分識別文件庫。</span><span class="sxs-lookup"><span data-stu-id="32b65-108">It doesn't address hello relying party application or its identity library.</span></span>

## <a name="xml-editing"></a><span data-ttu-id="32b65-109">XML 編輯</span><span class="sxs-lookup"><span data-stu-id="32b65-109">XML editing</span></span>

<span data-ttu-id="32b65-110">hello 最常見的錯誤，在將自訂原則設定不正確格式化 XML。</span><span class="sxs-lookup"><span data-stu-id="32b65-110">hello most common error in setting up custom policies is improperly formatted XML.</span></span> <span data-ttu-id="32b65-111">良好的 XML 編輯器幾乎不可或缺。</span><span class="sxs-lookup"><span data-stu-id="32b65-111">A good XML editor is nearly essential.</span></span> <span data-ttu-id="32b65-112">良好的 XML 編輯器會顯示 XML 原貌、為內容加上色彩、預先填入常用字詞、保持編製 XML 元素的索引，而且可以根據結構描述進行驗證。</span><span class="sxs-lookup"><span data-stu-id="32b65-112">A good XML editor displays XML natively, color-codes content, prefills common terms, keeps XML elements indexed, and can validate with schema.</span></span> <span data-ttu-id="32b65-113">以下是我們最喜愛的兩個 XML 編輯器：</span><span class="sxs-lookup"><span data-stu-id="32b65-113">Here are two of our favorite XML editors:</span></span>

* [<span data-ttu-id="32b65-114">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="32b65-114">Visual Studio Code</span></span>](https://code.visualstudio.com/)
* [<span data-ttu-id="32b65-115">Notepad++</span><span class="sxs-lookup"><span data-stu-id="32b65-115">Notepad++</span></span>](https://notepad-plus-plus.org/)

<span data-ttu-id="32b65-116">在您上傳 XML 檔案之前，XML 結構描述驗證會識別錯誤。</span><span class="sxs-lookup"><span data-stu-id="32b65-116">XML schema validation identifies errors before you upload your XML file.</span></span> <span data-ttu-id="32b65-117">在 hello 根資料夾中的 hello 入門套件，取得 TrustFrameworkPolicy_0.3.0.0.xsd hello XML 結構描述定義。</span><span class="sxs-lookup"><span data-stu-id="32b65-117">In hello root folder of hello starter pack, get hello XML schema definition TrustFrameworkPolicy_0.3.0.0.xsd.</span></span> <span data-ttu-id="32b65-118">如需詳細資訊，請在 hello 文件的 XML 編輯器中，請尋找*XML 工具*和*XML 驗證*。</span><span class="sxs-lookup"><span data-stu-id="32b65-118">For more information, in hello documentation of your XML editor, look for *XML tools* and *XML validation*.</span></span>

<span data-ttu-id="32b65-119">您可能會發現檢閱 XML 規則很有幫助。</span><span class="sxs-lookup"><span data-stu-id="32b65-119">You might find a review of XML rules helpful.</span></span> <span data-ttu-id="32b65-120">Azure AD B2C 會拒絕它所偵測到的任何 XML 格式錯誤。</span><span class="sxs-lookup"><span data-stu-id="32b65-120">Azure AD B2C rejects any XML formatting errors that it detects.</span></span> <span data-ttu-id="32b65-121">格式錯誤的 XML 有時可能會產生令人誤解的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="32b65-121">Occasionally, incorrectly formatted XML might cause error messages that are misleading.</span></span>

## <a name="upload-policies-and-policy-validation"></a><span data-ttu-id="32b65-122">上傳原則和原則驗證</span><span class="sxs-lookup"><span data-stu-id="32b65-122">Upload policies and policy validation</span></span>

 <span data-ttu-id="32b65-123">XML 檔案上傳驗證是自動執行。</span><span class="sxs-lookup"><span data-stu-id="32b65-123">XML file upload validation is automatic.</span></span> <span data-ttu-id="32b65-124">大部分的錯誤會造成 hello 上載 toofail。</span><span class="sxs-lookup"><span data-stu-id="32b65-124">Most errors cause hello upload toofail.</span></span> <span data-ttu-id="32b65-125">驗證包含您要上傳的 hello 原則檔案。</span><span class="sxs-lookup"><span data-stu-id="32b65-125">Validation includes hello policy file that you are uploading.</span></span> <span data-ttu-id="32b65-126">它也包含 hello 鏈結的 hello 上傳檔案太參照的檔案 (hello 信賴憑證者的合作對象原則檔、 hello 擴充功能檔案與 hello 基底檔案)。</span><span class="sxs-lookup"><span data-stu-id="32b65-126">It also includes hello chain of files hello upload file refers too(hello relying party policy file, hello extensions file, and hello base file).</span></span> 
 
 <span data-ttu-id="32b65-127">常見的驗證錯誤 hello 如下。</span><span class="sxs-lookup"><span data-stu-id="32b65-127">Common validation errors include hello following.</span></span>

<span data-ttu-id="32b65-128">錯誤程式碼片段︰`... makes a reference tooClaimType with id "displaName" but neither hello policy nor any of its base policies contain such an element`</span><span class="sxs-lookup"><span data-stu-id="32b65-128">Error snippet: `... makes a reference tooClaimType with id "displaName" but neither hello policy nor any of its base policies contain such an element`</span></span>
* <span data-ttu-id="32b65-129">hello ClaimType 值可能拼錯，或者不存在於 hello 結構描述。</span><span class="sxs-lookup"><span data-stu-id="32b65-129">hello ClaimType value might be misspelled, or does not exist in hello schema.</span></span>
* <span data-ttu-id="32b65-130">ClaimType 值必須定義至少一個 hello hello 原則中的檔案。</span><span class="sxs-lookup"><span data-stu-id="32b65-130">ClaimType values must be defined in at least one of hello files in hello policy.</span></span> 
    <span data-ttu-id="32b65-131">例如：` <ClaimType Id="socialIdpUserId">`</span><span class="sxs-lookup"><span data-stu-id="32b65-131">For example: ` <ClaimType Id="socialIdpUserId">`</span></span>
* <span data-ttu-id="32b65-132">如果 ClaimType 定義在 hello 延伸模組檔案中，但它也會用於 TechnicalProfile 值 hello 基底檔案中上, 傳 hello 基底檔案會導致錯誤。</span><span class="sxs-lookup"><span data-stu-id="32b65-132">If ClaimType is defined in hello extensions file, but it's also used in a TechnicalProfile value in hello base file, uploading hello base file results in an error.</span></span>

<span data-ttu-id="32b65-133">錯誤程式碼片段︰`...makes a reference tooa ClaimsTransformation with id...`</span><span class="sxs-lookup"><span data-stu-id="32b65-133">Error snippet: `...makes a reference tooa ClaimsTransformation with id...`</span></span>
* <span data-ttu-id="32b65-134">針對 hello 錯誤可能是 hello 相同 hello ClaimType 錯誤與 hello 原因。</span><span class="sxs-lookup"><span data-stu-id="32b65-134">hello causes for hello error might be hello same as for hello ClaimType error.</span></span>

<span data-ttu-id="32b65-135">錯誤程式碼片段︰`Reason: User is currently logged as a user of 'yourtenant.onmicrosoft.com' tenant. In order toomanage 'yourtenant.onmicrosoft.com', please login as a user of 'yourtenant.onmicrosoft.com' tenant`</span><span class="sxs-lookup"><span data-stu-id="32b65-135">Error snippet: `Reason: User is currently logged as a user of 'yourtenant.onmicrosoft.com' tenant. In order toomanage 'yourtenant.onmicrosoft.com', please login as a user of 'yourtenant.onmicrosoft.com' tenant`</span></span>
* <span data-ttu-id="32b65-136">請檢查該 hello hello 中的 TenantId 值 **\<TrustFrameworkPolicy\>** 和 **\<BasePolicy\>** 項目符合目標 Azure AD B2C租用戶。</span><span class="sxs-lookup"><span data-stu-id="32b65-136">Check that hello TenantId value in hello **\<TrustFrameworkPolicy\>** and **\<BasePolicy\>** elements match your target Azure AD B2C tenant.</span></span>  

## <a name="troubleshoot-hello-runtime"></a><span data-ttu-id="32b65-137">疑難排解 hello 執行階段</span><span class="sxs-lookup"><span data-stu-id="32b65-137">Troubleshoot hello runtime</span></span>

* <span data-ttu-id="32b65-138">使用`Run Now`和`https://jwt.io`tootest 您獨立於您的 web 或行動應用程式的原則。</span><span class="sxs-lookup"><span data-stu-id="32b65-138">Use `Run Now` and `https://jwt.io` tootest your policies independently of your web or mobile application.</span></span> <span data-ttu-id="32b65-139">此網站的作用就像信賴憑證者應用程式。</span><span class="sxs-lookup"><span data-stu-id="32b65-139">This website acts like a relying party application.</span></span> <span data-ttu-id="32b65-140">它會顯示 hello JSON Web Token (JWT) 所產生的 Azure AD B2C 原則 hello 內容。</span><span class="sxs-lookup"><span data-stu-id="32b65-140">It displays hello contents of hello JSON Web Token (JWT) that is generated by your Azure AD B2C policy.</span></span> <span data-ttu-id="32b65-141">toocreate 測試應用程式在識別經驗 Framework 中，使用 hello 下列值：</span><span class="sxs-lookup"><span data-stu-id="32b65-141">toocreate a test application in Identity Experience Framework, use hello following values:</span></span>
    * <span data-ttu-id="32b65-142">名稱︰TestApp</span><span class="sxs-lookup"><span data-stu-id="32b65-142">Name: TestApp</span></span>
    * <span data-ttu-id="32b65-143">Web 應用程式/Web API：無</span><span class="sxs-lookup"><span data-stu-id="32b65-143">Web App/Web API: No</span></span>
    * <span data-ttu-id="32b65-144">原生用戶端︰否</span><span class="sxs-lookup"><span data-stu-id="32b65-144">Native client: No</span></span>

* <span data-ttu-id="32b65-145">tootrace hello 之間交換訊息的用戶端瀏覽器及 Azure AD B2C 使用[Fiddler](http://www.telerik.com/fiddler)。</span><span class="sxs-lookup"><span data-stu-id="32b65-145">tootrace hello exchange of messages between your client browser and Azure AD B2C, use [Fiddler](http://www.telerik.com/fiddler).</span></span> <span data-ttu-id="32b65-146">它可協助您了解使用者旅程圖在協調流程步驟中的何處失敗。</span><span class="sxs-lookup"><span data-stu-id="32b65-146">It can help you get an indication of where your user journey is failing in your orchestration steps.</span></span>

* <span data-ttu-id="32b65-147">在**開發模式**，使用**Application Insights** tootrace hello 活動的身分識別體驗架構的使用者之旅。</span><span class="sxs-lookup"><span data-stu-id="32b65-147">In **Development mode**, use **Application Insights** tootrace hello activity of your Identity Experience Framework user journey.</span></span> <span data-ttu-id="32b65-148">在**開發模式**，您可以觀察 hello 交換 hello 身分識別體驗架構之間的宣告和 hello 各種宣告提供者所定義的技術的設定檔，例如身分識別提供者，應用程式開發介面為基礎的服務，hello Azure AD B2C 使用者目錄中及其他服務，例如 Azure 多 Multi-factor-authentication。</span><span class="sxs-lookup"><span data-stu-id="32b65-148">In **Development mode**, you can observe hello exchange of claims between hello Identity Experience Framework and hello various claims providers that are defined by technical profiles, such as identity providers, API-based services, hello Azure AD B2C user directory, and other services, like Azure Multi-Factor-Authentication.</span></span>  

## <a name="recommended-practices"></a><span data-ttu-id="32b65-149">建議的做法</span><span class="sxs-lookup"><span data-stu-id="32b65-149">Recommended practices</span></span>

<span data-ttu-id="32b65-150">**為您的情節保留多個版本。將它們和您的應用程式一起放在一個專案中。**</span><span class="sxs-lookup"><span data-stu-id="32b65-150">**Keep multiple versions of your scenarios. Group them in a project with your application.**</span></span> <span data-ttu-id="32b65-151">hello 基底、 延伸與信賴憑證者的合作對象檔案會直接相互依存性。</span><span class="sxs-lookup"><span data-stu-id="32b65-151">hello base, extensions, and relying party files are directly dependent on each other.</span></span> <span data-ttu-id="32b65-152">將它們儲存成一個群組。</span><span class="sxs-lookup"><span data-stu-id="32b65-152">Save them as a group.</span></span> <span data-ttu-id="32b65-153">當新功能加入 tooyour 原則時，保留不同工作版本。</span><span class="sxs-lookup"><span data-stu-id="32b65-153">As new features are added tooyour policies, keep separate working versions.</span></span> <span data-ttu-id="32b65-154">階段自己的工作版本檔案系統與 hello 與他們互動的應用程式程式碼。</span><span class="sxs-lookup"><span data-stu-id="32b65-154">Stage working versions in your own file system with hello application code they interact with.</span></span>  <span data-ttu-id="32b65-155">您的應用程式可能會在一個租用戶中叫用許多不同的信賴憑證者原則。</span><span class="sxs-lookup"><span data-stu-id="32b65-155">Your applications might invoke many different relying party policies in a tenant.</span></span> <span data-ttu-id="32b65-156">它們可能會變成預期從您的 Azure AD B2C 原則的 hello 宣告而定。</span><span class="sxs-lookup"><span data-stu-id="32b65-156">They might become dependent on hello claims that they expect from your Azure AD B2C policies.</span></span>

<span data-ttu-id="32b65-157">**使用已知的使用者旅程圖來開發和測試技術設定檔。**</span><span class="sxs-lookup"><span data-stu-id="32b65-157">**Develop and test technical profiles with known user journeys.**</span></span> <span data-ttu-id="32b65-158">使用已測試的入門套件原則 tooset 設定您的技術檔。</span><span class="sxs-lookup"><span data-stu-id="32b65-158">Use tested starter pack policies tooset up your technical profiles.</span></span> <span data-ttu-id="32b65-159">將它們併入您自己的使用者旅程圖之前，先個別進行測試。</span><span class="sxs-lookup"><span data-stu-id="32b65-159">Test them separately before you incorporate them into your own user journeys.</span></span>

<span data-ttu-id="32b65-160">**使用已測試的技術設定檔來開發和測試使用者旅程圖。**</span><span class="sxs-lookup"><span data-stu-id="32b65-160">**Develop and test user journeys with tested technical profiles.**</span></span> <span data-ttu-id="32b65-161">以累加方式變更使用者之旅 hello 協調流程的步驟。</span><span class="sxs-lookup"><span data-stu-id="32b65-161">Change hello orchestration steps of a user journey incrementally.</span></span> <span data-ttu-id="32b65-162">漸進地建置您想要的情節。</span><span class="sxs-lookup"><span data-stu-id="32b65-162">Progressively build your intended scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="32b65-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="32b65-163">Next steps</span></span>

* <span data-ttu-id="32b65-164">在 GitHub 中下載 hello [active-directory-b2c-custom-policy-starterpack] (https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/archive/master.zip).zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="32b65-164">In GitHub, download hello [active-directory-b2c-custom-policy-starterpack] (https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/archive/master.zip) .zip file.</span></span>
