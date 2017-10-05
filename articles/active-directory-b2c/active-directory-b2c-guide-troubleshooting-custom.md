---
title: "Azure Active Directory B2C：針對自訂原則進行疑難排解 | Microsoft Docs"
description: "深入了解在 Azure Active Directory 中使用自訂原則時解決錯誤的方法。"
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
ms.openlocfilehash: 023390ba36a74217503ff8b3076ad17978fe3fb8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-azure-ad-b2c-custom-policies-and-identity-experience-framework"></a><span data-ttu-id="6f43c-103">針對 Azure AD B2C 自訂原則和身分識別體驗架構進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="6f43c-103">Troubleshoot Azure AD B2C custom policies and Identity Experience Framework</span></span>

<span data-ttu-id="6f43c-104">如果您使用 Azure Active Directory B2C (Azure AD B2C) 自訂原則，當您以原則語言 XML 格式來設定身分識別體驗架構時，您可能會遇到挑戰。</span><span class="sxs-lookup"><span data-stu-id="6f43c-104">If you use Azure Active Directory B2C (Azure AD B2C) custom policies, you might experience challenges setting up the Identity Experience Framework in its policy language XML format.</span></span>  <span data-ttu-id="6f43c-105">學習撰寫自訂原則就如同學習新的語言。</span><span class="sxs-lookup"><span data-stu-id="6f43c-105">Learning to write custom policies can be like learning a new language.</span></span> <span data-ttu-id="6f43c-106">在本文中，我們將說明可協助您快速找出並解決問題的工具和提示。</span><span class="sxs-lookup"><span data-stu-id="6f43c-106">In this article, we describe tools and tips that can help you quickly discover and resolve issues.</span></span> 

> [!NOTE]
> <span data-ttu-id="6f43c-107">本文著重在針對 Azure AD B2C 自訂原則設定進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="6f43c-107">This article focuses on troubleshooting your Azure AD B2C custom policy configuration.</span></span> <span data-ttu-id="6f43c-108">其中不討論信賴憑證者應用程式或其身分識別程式庫。</span><span class="sxs-lookup"><span data-stu-id="6f43c-108">It doesn't address the relying party application or its identity library.</span></span>

## <a name="xml-editing"></a><span data-ttu-id="6f43c-109">XML 編輯</span><span class="sxs-lookup"><span data-stu-id="6f43c-109">XML editing</span></span>

<span data-ttu-id="6f43c-110">設定自訂原則時，最常見的錯誤是 XML 格式不正確。</span><span class="sxs-lookup"><span data-stu-id="6f43c-110">The most common error in setting up custom policies is improperly formatted XML.</span></span> <span data-ttu-id="6f43c-111">良好的 XML 編輯器幾乎不可或缺。</span><span class="sxs-lookup"><span data-stu-id="6f43c-111">A good XML editor is nearly essential.</span></span> <span data-ttu-id="6f43c-112">良好的 XML 編輯器會顯示 XML 原貌、為內容加上色彩、預先填入常用字詞、保持編製 XML 元素的索引，而且可以根據結構描述進行驗證。</span><span class="sxs-lookup"><span data-stu-id="6f43c-112">A good XML editor displays XML natively, color-codes content, prefills common terms, keeps XML elements indexed, and can validate with schema.</span></span> <span data-ttu-id="6f43c-113">以下是我們最喜愛的兩個 XML 編輯器：</span><span class="sxs-lookup"><span data-stu-id="6f43c-113">Here are two of our favorite XML editors:</span></span>

* [<span data-ttu-id="6f43c-114">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="6f43c-114">Visual Studio Code</span></span>](https://code.visualstudio.com/)
* [<span data-ttu-id="6f43c-115">Notepad++</span><span class="sxs-lookup"><span data-stu-id="6f43c-115">Notepad++</span></span>](https://notepad-plus-plus.org/)

<span data-ttu-id="6f43c-116">在您上傳 XML 檔案之前，XML 結構描述驗證會識別錯誤。</span><span class="sxs-lookup"><span data-stu-id="6f43c-116">XML schema validation identifies errors before you upload your XML file.</span></span> <span data-ttu-id="6f43c-117">在入門套件的根資料夾中，取得 XML 結構描述定義 TrustFrameworkPolicy_0.3.0.0.xsd。</span><span class="sxs-lookup"><span data-stu-id="6f43c-117">In the root folder of the starter pack, get the XML schema definition TrustFrameworkPolicy_0.3.0.0.xsd.</span></span> <span data-ttu-id="6f43c-118">如需詳細資訊，請在 XML 編輯器的文件中尋找「XML 工具」和「XML 驗證」。</span><span class="sxs-lookup"><span data-stu-id="6f43c-118">For more information, in the documentation of your XML editor, look for *XML tools* and *XML validation*.</span></span>

<span data-ttu-id="6f43c-119">您可能會發現檢閱 XML 規則很有幫助。</span><span class="sxs-lookup"><span data-stu-id="6f43c-119">You might find a review of XML rules helpful.</span></span> <span data-ttu-id="6f43c-120">Azure AD B2C 會拒絕它所偵測到的任何 XML 格式錯誤。</span><span class="sxs-lookup"><span data-stu-id="6f43c-120">Azure AD B2C rejects any XML formatting errors that it detects.</span></span> <span data-ttu-id="6f43c-121">格式錯誤的 XML 有時可能會產生令人誤解的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="6f43c-121">Occasionally, incorrectly formatted XML might cause error messages that are misleading.</span></span>

## <a name="upload-policies-and-policy-validation"></a><span data-ttu-id="6f43c-122">上傳原則和原則驗證</span><span class="sxs-lookup"><span data-stu-id="6f43c-122">Upload policies and policy validation</span></span>

 <span data-ttu-id="6f43c-123">XML 檔案上傳驗證是自動執行。</span><span class="sxs-lookup"><span data-stu-id="6f43c-123">XML file upload validation is automatic.</span></span> <span data-ttu-id="6f43c-124">大部分的錯誤會導致上傳失敗。</span><span class="sxs-lookup"><span data-stu-id="6f43c-124">Most errors cause the upload to fail.</span></span> <span data-ttu-id="6f43c-125">驗證包括您要上傳的原則檔。</span><span class="sxs-lookup"><span data-stu-id="6f43c-125">Validation includes the policy file that you are uploading.</span></span> <span data-ttu-id="6f43c-126">也包括上傳檔案所參考的一連串檔案 (信賴憑證者原則檔、擴充檔案和基底檔案)。</span><span class="sxs-lookup"><span data-stu-id="6f43c-126">It also includes the chain of files the upload file refers to (the relying party policy file, the extensions file, and the base file).</span></span> 
 
 <span data-ttu-id="6f43c-127">常見的驗證錯誤包括下列幾個。</span><span class="sxs-lookup"><span data-stu-id="6f43c-127">Common validation errors include the following.</span></span>

<span data-ttu-id="6f43c-128">錯誤程式碼片段︰`... makes a reference to ClaimType with id "displaName" but neither the policy nor any of its base policies contain such an element`</span><span class="sxs-lookup"><span data-stu-id="6f43c-128">Error snippet: `... makes a reference to ClaimType with id "displaName" but neither the policy nor any of its base policies contain such an element`</span></span>
* <span data-ttu-id="6f43c-129">ClaimType 值可能拼字錯誤，或不存在於結構描述中。</span><span class="sxs-lookup"><span data-stu-id="6f43c-129">The ClaimType value might be misspelled, or does not exist in the schema.</span></span>
* <span data-ttu-id="6f43c-130">ClaimType 值至少必須定義於原則內的其中一個檔案中。</span><span class="sxs-lookup"><span data-stu-id="6f43c-130">ClaimType values must be defined in at least one of the files in the policy.</span></span> 
    <span data-ttu-id="6f43c-131">例如：` <ClaimType Id="socialIdpUserId">`</span><span class="sxs-lookup"><span data-stu-id="6f43c-131">For example: ` <ClaimType Id="socialIdpUserId">`</span></span>
* <span data-ttu-id="6f43c-132">如果 ClaimType 定義於擴充檔案中，但也用於基底檔案的 TechnichalProfile 值中，則上傳基底檔案會導致錯誤。</span><span class="sxs-lookup"><span data-stu-id="6f43c-132">If ClaimType is defined in the extensions file, but it's also used in a TechnicalProfile value in the base file, uploading the base file results in an error.</span></span>

<span data-ttu-id="6f43c-133">錯誤程式碼片段︰`...makes a reference to a ClaimsTransformation with id...`</span><span class="sxs-lookup"><span data-stu-id="6f43c-133">Error snippet: `...makes a reference to a ClaimsTransformation with id...`</span></span>
* <span data-ttu-id="6f43c-134">此錯誤的原因可能與 ClaimType 錯誤一樣。</span><span class="sxs-lookup"><span data-stu-id="6f43c-134">The causes for the error might be the same as for the ClaimType error.</span></span>

<span data-ttu-id="6f43c-135">錯誤程式碼片段︰`Reason: User is currently logged as a user of 'yourtenant.onmicrosoft.com' tenant. In order to manage 'yourtenant.onmicrosoft.com', please login as a user of 'yourtenant.onmicrosoft.com' tenant`</span><span class="sxs-lookup"><span data-stu-id="6f43c-135">Error snippet: `Reason: User is currently logged as a user of 'yourtenant.onmicrosoft.com' tenant. In order to manage 'yourtenant.onmicrosoft.com', please login as a user of 'yourtenant.onmicrosoft.com' tenant`</span></span>
* <span data-ttu-id="6f43c-136">檢查 **\<TrustFrameworkPolicy\>** 和 **\<BasePolicy\>** 元素中的 TenantId 值符合目標 Azure AD B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="6f43c-136">Check that the TenantId value in the **\<TrustFrameworkPolicy\>** and **\<BasePolicy\>** elements match your target Azure AD B2C tenant.</span></span>  

## <a name="troubleshoot-the-runtime"></a><span data-ttu-id="6f43c-137">針對執行階段進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="6f43c-137">Troubleshoot the runtime</span></span>

* <span data-ttu-id="6f43c-138">使用 `Run Now` 和 `https://jwt.io`，在不受 Web 或行動應用程式的影響下測試您的原則。</span><span class="sxs-lookup"><span data-stu-id="6f43c-138">Use `Run Now` and `https://jwt.io` to test your policies independently of your web or mobile application.</span></span> <span data-ttu-id="6f43c-139">此網站的作用就像信賴憑證者應用程式。</span><span class="sxs-lookup"><span data-stu-id="6f43c-139">This website acts like a relying party application.</span></span> <span data-ttu-id="6f43c-140">它會顯示 Azure AD B2C 原則所產生的 JSON Web 權杖 (JWT) 內容。</span><span class="sxs-lookup"><span data-stu-id="6f43c-140">It displays the contents of the JSON Web Token (JWT) that is generated by your Azure AD B2C policy.</span></span> <span data-ttu-id="6f43c-141">若要在身分識別體驗架構中建立測試應用程式，請使用下列值：</span><span class="sxs-lookup"><span data-stu-id="6f43c-141">To create a test application in Identity Experience Framework, use the following values:</span></span>
    * <span data-ttu-id="6f43c-142">名稱︰TestApp</span><span class="sxs-lookup"><span data-stu-id="6f43c-142">Name: TestApp</span></span>
    * <span data-ttu-id="6f43c-143">Web 應用程式/Web API：無</span><span class="sxs-lookup"><span data-stu-id="6f43c-143">Web App/Web API: No</span></span>
    * <span data-ttu-id="6f43c-144">原生用戶端︰否</span><span class="sxs-lookup"><span data-stu-id="6f43c-144">Native client: No</span></span>

* <span data-ttu-id="6f43c-145">若要追蹤用戶端瀏覽器和 Azure AD B2C 之間的訊息交換，請使用 [Fiddler](http://www.telerik.com/fiddler)。</span><span class="sxs-lookup"><span data-stu-id="6f43c-145">To trace the exchange of messages between your client browser and Azure AD B2C, use [Fiddler](http://www.telerik.com/fiddler).</span></span> <span data-ttu-id="6f43c-146">它可協助您了解使用者旅程圖在協調流程步驟中的何處失敗。</span><span class="sxs-lookup"><span data-stu-id="6f43c-146">It can help you get an indication of where your user journey is failing in your orchestration steps.</span></span>

* <span data-ttu-id="6f43c-147">在**開發模式**中，請使用 **Application Insights** 來追蹤身分識別體驗架構使用者旅程圖的活動。</span><span class="sxs-lookup"><span data-stu-id="6f43c-147">In **Development mode**, use **Application Insights** to trace the activity of your Identity Experience Framework user journey.</span></span> <span data-ttu-id="6f43c-148">在**開發模式**中，您可以觀察在身分識別體驗架構和各種宣告提供者 (由技術設定檔定義) 之間的宣告交換，這些提供者包括識別提供者、API 型服務、Azure AD B2C 使用者目錄和其他服務 (例如 Azure Multi-Factor-Authentication)。</span><span class="sxs-lookup"><span data-stu-id="6f43c-148">In **Development mode**, you can observe the exchange of claims between the Identity Experience Framework and the various claims providers that are defined by technical profiles, such as identity providers, API-based services, the Azure AD B2C user directory, and other services, like Azure Multi-Factor-Authentication.</span></span>  

## <a name="recommended-practices"></a><span data-ttu-id="6f43c-149">建議的做法</span><span class="sxs-lookup"><span data-stu-id="6f43c-149">Recommended practices</span></span>

<span data-ttu-id="6f43c-150">**為您的情節保留多個版本。將它們和您的應用程式一起放在一個專案中。**</span><span class="sxs-lookup"><span data-stu-id="6f43c-150">**Keep multiple versions of your scenarios. Group them in a project with your application.**</span></span> <span data-ttu-id="6f43c-151">基底、擴充和信賴憑證者檔案直接相互依存。</span><span class="sxs-lookup"><span data-stu-id="6f43c-151">The base, extensions, and relying party files are directly dependent on each other.</span></span> <span data-ttu-id="6f43c-152">將它們儲存成一個群組。</span><span class="sxs-lookup"><span data-stu-id="6f43c-152">Save them as a group.</span></span> <span data-ttu-id="6f43c-153">有新功能新增至您的原則時，保留個別的工作版本。</span><span class="sxs-lookup"><span data-stu-id="6f43c-153">As new features are added to your policies, keep separate working versions.</span></span> <span data-ttu-id="6f43c-154">將工作版本和其所互動的應用程式程式碼，分階段放入您自己的檔案系統中。</span><span class="sxs-lookup"><span data-stu-id="6f43c-154">Stage working versions in your own file system with the application code they interact with.</span></span>  <span data-ttu-id="6f43c-155">您的應用程式可能會在一個租用戶中叫用許多不同的信賴憑證者原則。</span><span class="sxs-lookup"><span data-stu-id="6f43c-155">Your applications might invoke many different relying party policies in a tenant.</span></span> <span data-ttu-id="6f43c-156">它們可能會變成相依於您的 Azure AD B2C 原則可能提供的宣告。</span><span class="sxs-lookup"><span data-stu-id="6f43c-156">They might become dependent on the claims that they expect from your Azure AD B2C policies.</span></span>

<span data-ttu-id="6f43c-157">**使用已知的使用者旅程圖來開發和測試技術設定檔。**</span><span class="sxs-lookup"><span data-stu-id="6f43c-157">**Develop and test technical profiles with known user journeys.**</span></span> <span data-ttu-id="6f43c-158">使用已測試的入門套件原則來設定您的技術設定檔。</span><span class="sxs-lookup"><span data-stu-id="6f43c-158">Use tested starter pack policies to set up your technical profiles.</span></span> <span data-ttu-id="6f43c-159">將它們併入您自己的使用者旅程圖之前，先個別進行測試。</span><span class="sxs-lookup"><span data-stu-id="6f43c-159">Test them separately before you incorporate them into your own user journeys.</span></span>

<span data-ttu-id="6f43c-160">**使用已測試的技術設定檔來開發和測試使用者旅程圖。**</span><span class="sxs-lookup"><span data-stu-id="6f43c-160">**Develop and test user journeys with tested technical profiles.**</span></span> <span data-ttu-id="6f43c-161">累加地變更使用者旅程圖的協調流程步驟。</span><span class="sxs-lookup"><span data-stu-id="6f43c-161">Change the orchestration steps of a user journey incrementally.</span></span> <span data-ttu-id="6f43c-162">漸進地建置您想要的情節。</span><span class="sxs-lookup"><span data-stu-id="6f43c-162">Progressively build your intended scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f43c-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6f43c-163">Next steps</span></span>

* <span data-ttu-id="6f43c-164">在 GitHub 中，下載 [active-directory-b2c-custom-policy-starterpack] (https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/archive/master.zip) .zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="6f43c-164">In GitHub, download the [active-directory-b2c-custom-policy-starterpack] (https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/archive/master.zip) .zip file.</span></span>
