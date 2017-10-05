---
title: "如何委派使用者註冊和產品訂閱"
description: "了解如何在 Azure API Management 中將使用者註冊和產品訂閱委派給第三方。"
services: api-management
documentationcenter: 
author: antonba
manager: erikre
editor: 
ms.assetid: 8b7ad5ee-a873-4966-a400-7e508bbbe158
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 2637ab6405f2d4ea1da84981295a144874dfa4f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-delegate-user-registration-and-product-subscription"></a><span data-ttu-id="98fdd-103">如何委派使用者註冊和產品訂閱</span><span class="sxs-lookup"><span data-stu-id="98fdd-103">How to delegate user registration and product subscription</span></span>
<span data-ttu-id="98fdd-104">委派可讓您使用現有的網站來處理開發人員登入/註冊和產品訂閱，而非使用開發人員入口網站中的內建功能。</span><span class="sxs-lookup"><span data-stu-id="98fdd-104">Delegation allows you to use your existing website for handling developer sign-in/sign-up and subscription to products as opposed to using the built-in functionality in the developer portal.</span></span> <span data-ttu-id="98fdd-105">這樣可讓您的網站擁有使用者資料，並以自訂方式來執行這些步驟的驗證。</span><span class="sxs-lookup"><span data-stu-id="98fdd-105">This enables your website to own the user data and perform the validation of these steps in a custom way.</span></span>

## <span data-ttu-id="98fdd-106"><a name="delegate-signin-up"> </a>委派開發人員登入和註冊</span><span class="sxs-lookup"><span data-stu-id="98fdd-106"><a name="delegate-signin-up"> </a>Delegating developer sign-in and sign-up</span></span>
<span data-ttu-id="98fdd-107">若要將開發人員登入和註冊委派給您現有的網站，您必須在網站上建立特殊的委派端點，作為從 API 管理開發人員入口網站起始的任何這類要求的進入點。</span><span class="sxs-lookup"><span data-stu-id="98fdd-107">To delegate developer sign-in and sign-up to your existing website you will need to create a special delegation endpoint on your site that acts as the entry-point for any such request initiated from the API Management developer portal.</span></span>

<span data-ttu-id="98fdd-108">最終工作流程如下所示：</span><span class="sxs-lookup"><span data-stu-id="98fdd-108">The final workflow will be as follows:</span></span>

1. <span data-ttu-id="98fdd-109">開發人員在 API 管理開發人員入口網站按一下登入或註冊連結</span><span class="sxs-lookup"><span data-stu-id="98fdd-109">Developer clicks on the sign-in or sign-up link at the API Management developer portal</span></span>
2. <span data-ttu-id="98fdd-110">瀏覽器重新導向至委派端點</span><span class="sxs-lookup"><span data-stu-id="98fdd-110">Browser is redirected to the delegation endpoint</span></span>
3. <span data-ttu-id="98fdd-111">委派端點再轉而重新導向至或呈現 UI，要求使用者登入或註冊</span><span class="sxs-lookup"><span data-stu-id="98fdd-111">Delegation endpoint in return redirects to or presents UI asking user to sign-in or sign-up</span></span>
4. <span data-ttu-id="98fdd-112">成功時，將使用者重新導向回到他們所來自的 API 管理開發人員入口網站頁面</span><span class="sxs-lookup"><span data-stu-id="98fdd-112">On success, the user is redirected back to the API Management developer portal page they started from</span></span>

<span data-ttu-id="98fdd-113">首先，請設定 API 管理透過委派端點來傳遞要求。</span><span class="sxs-lookup"><span data-stu-id="98fdd-113">To begin, let's first set-up API Management to route requests via your delegation endpoint.</span></span> <span data-ttu-id="98fdd-114">在 API 管理發佈者入口網站中，按一下 [安全性]，然後按一下 [委派] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="98fdd-114">In the API Management publisher portal, click on **Security** and then click the **Delegation** tab.</span></span> <span data-ttu-id="98fdd-115">按一下核取方塊以啟用 [Delegate sign-in & sign-up]。</span><span class="sxs-lookup"><span data-stu-id="98fdd-115">Click the checkbox to enable 'Delegate sign-in & sign-up'.</span></span>

![Delegation page][api-management-delegation-signin-up]

* <span data-ttu-id="98fdd-117">決定特殊委派端點的 URL，並在 [ **Delegation endpoint URL** ] 欄位中輸入。</span><span class="sxs-lookup"><span data-stu-id="98fdd-117">Decide what the URL of your special delegation endpoint will be and enter it in the **Delegation endpoint URL** field.</span></span> 
* <span data-ttu-id="98fdd-118">在 [ **Delegation authentication key** ] 欄位中輸入密碼，用來計算提供給您驗證的簽章，以確定要求確實來自 Azure API 管理。</span><span class="sxs-lookup"><span data-stu-id="98fdd-118">Within the **Delegation authentication key** field enter a secret that will be used to compute a signature provided to you for verification to ensure that the request is indeed coming from Azure API Management.</span></span> <span data-ttu-id="98fdd-119">您可以按一下 [ **產生** ] 按鈕，讓 API 管理為您隨機產生金鑰。</span><span class="sxs-lookup"><span data-stu-id="98fdd-119">You can click the **generate** button to have API Managemnet randomly generate a key for you.</span></span>

<span data-ttu-id="98fdd-120">現在您需要建立「 **委派端點**」。</span><span class="sxs-lookup"><span data-stu-id="98fdd-120">Now you need to create the **delegation endpoint**.</span></span> <span data-ttu-id="98fdd-121">必須執行一些動作：</span><span class="sxs-lookup"><span data-stu-id="98fdd-121">It has to perform a number of actions:</span></span>

1. <span data-ttu-id="98fdd-122">接收下列形式的要求：</span><span class="sxs-lookup"><span data-stu-id="98fdd-122">Receive a request in the following form:</span></span>
   
   > <span data-ttu-id="98fdd-123">http://www.yourwebsite.com/apimdelegation?operation=SignIn&returnUrl={URL of source page}&salt={string}&sig={string}</span><span class="sxs-lookup"><span data-stu-id="98fdd-123">*http://www.yourwebsite.com/apimdelegation?operation=SignIn&returnUrl={URL of source page}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="98fdd-124">登入/註冊案例的查詢參數：</span><span class="sxs-lookup"><span data-stu-id="98fdd-124">Query parameters for the sign-in / sign-up case:</span></span>
   
   * <span data-ttu-id="98fdd-125">**operation**：識別委派要求的類型 - 在此案例中只能是 **SignIn**</span><span class="sxs-lookup"><span data-stu-id="98fdd-125">**operation**: identifies what type of delegation request it is - it can only be **SignIn** in this case</span></span>
   * <span data-ttu-id="98fdd-126">**returnUrl**：使用者按一下登入或註冊連結之頁面的 URL</span><span class="sxs-lookup"><span data-stu-id="98fdd-126">**returnUrl**: the URL of the page where the user clicked on a sign-in or sign-up link</span></span>
   * <span data-ttu-id="98fdd-127">**salt**：特殊 salt 字串，用於計算安全性雜湊</span><span class="sxs-lookup"><span data-stu-id="98fdd-127">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="98fdd-128">**sig**：已經過計算的安全性雜湊，用於和您已計算的雜湊進行比較</span><span class="sxs-lookup"><span data-stu-id="98fdd-128">**sig**: a computed security hash to be used for comparison to your own computed hash</span></span>
2. <span data-ttu-id="98fdd-129">確認要求來自 Azure API 管理 (選擇性，但基於安全性理由，強烈建議這麼做)</span><span class="sxs-lookup"><span data-stu-id="98fdd-129">Verify that the request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="98fdd-130">根據 **returnUrl** 和 **salt** 查詢參數，計算字串的 HMAC-SHA512 雜湊 ([以下提供範例程式碼])：</span><span class="sxs-lookup"><span data-stu-id="98fdd-130">Compute an HMAC-SHA512 hash of a string based on the **returnUrl** and **salt** query parameters ([example code provided below]):</span></span>
     
     > <span data-ttu-id="98fdd-131">HMAC(**salt** + '\n' + **returnUrl**)</span><span class="sxs-lookup"><span data-stu-id="98fdd-131">HMAC(**salt** + '\n' + **returnUrl**)</span></span>
     > 
     > 
   * <span data-ttu-id="98fdd-132">比較以上計算的雜湊和 **sig** 查詢參數的值。</span><span class="sxs-lookup"><span data-stu-id="98fdd-132">Compare the above-computed hash to the value of the **sig** query parameter.</span></span> <span data-ttu-id="98fdd-133">如果兩個雜湊相符，則繼續下一步，否則拒絕要求。</span><span class="sxs-lookup"><span data-stu-id="98fdd-133">If the two hashes match, move on to the next step, otherwise deny the request.</span></span>
3. <span data-ttu-id="98fdd-134">確認您收到的是登入/註冊要求：**operation** 查詢參數會設為 "**SignIn**"。</span><span class="sxs-lookup"><span data-stu-id="98fdd-134">Verify that you are receiving a request for sign-in/sign-up: the **operation** query parameter will be set to "**SignIn**".</span></span>
4. <span data-ttu-id="98fdd-135">顯示 UI 讓使用者登入或註冊</span><span class="sxs-lookup"><span data-stu-id="98fdd-135">Present the user with UI to sign-in or sign-up</span></span>
5. <span data-ttu-id="98fdd-136">如果使用者要註冊，您必須在 API 管理中為他們建立對應的帳戶。</span><span class="sxs-lookup"><span data-stu-id="98fdd-136">If the user is signing-up you have to create a corresponding account for them in API Management.</span></span> <span data-ttu-id="98fdd-137">使用 API Management REST API [建立使用者]。</span><span class="sxs-lookup"><span data-stu-id="98fdd-137">[Create a user] with the API Management REST API.</span></span> <span data-ttu-id="98fdd-138">這樣做時，請確定您所設定的使用者識別碼與使用者存放區中的識別碼相同，或與您可追蹤的識別碼相同。</span><span class="sxs-lookup"><span data-stu-id="98fdd-138">When doing so, ensure that you set the user ID to the same it is in your user store or to an ID that you can keep track of.</span></span>
6. <span data-ttu-id="98fdd-139">成功驗證使用者之後：</span><span class="sxs-lookup"><span data-stu-id="98fdd-139">When the user is successfully authenticated:</span></span>
   
   * <span data-ttu-id="98fdd-140">[要求單一登入 (SSO) 權杖] </span><span class="sxs-lookup"><span data-stu-id="98fdd-140">[request a single-sign-on (SSO) token] via the API Management REST API</span></span>
   * <span data-ttu-id="98fdd-141">將 returnUrl 查詢參數附加至您從上述 API 呼叫收到的 SSO URL：</span><span class="sxs-lookup"><span data-stu-id="98fdd-141">append a returnUrl query parameter to the SSO URL you have received from the API call above:</span></span>
     
     > <span data-ttu-id="98fdd-142">例如，https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span><span class="sxs-lookup"><span data-stu-id="98fdd-142">e.g. https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span></span> 
     > 
     > 
   * <span data-ttu-id="98fdd-143">將使用者重新導向至以上產生的 URL</span><span class="sxs-lookup"><span data-stu-id="98fdd-143">redirect the user to the above produced URL</span></span>

<span data-ttu-id="98fdd-144">除了 **SignIn** 作業之外，您也可以遵循上述步驟來執行帳戶管理，並使用以下其中一項作業。</span><span class="sxs-lookup"><span data-stu-id="98fdd-144">In addition to the **SignIn** operation, you can also perform account management by following the previous steps and using one of the following operations.</span></span>

* <span data-ttu-id="98fdd-145">**ChangePassword**</span><span class="sxs-lookup"><span data-stu-id="98fdd-145">**ChangePassword**</span></span>
* <span data-ttu-id="98fdd-146">**ChangeProfile**</span><span class="sxs-lookup"><span data-stu-id="98fdd-146">**ChangeProfile**</span></span>
* <span data-ttu-id="98fdd-147">**CloseAccount**</span><span class="sxs-lookup"><span data-stu-id="98fdd-147">**CloseAccount**</span></span>

<span data-ttu-id="98fdd-148">您必須傳遞下列查詢參數，供帳戶管理作業使用。</span><span class="sxs-lookup"><span data-stu-id="98fdd-148">You must pass the following query parameters for account management operations.</span></span>

* <span data-ttu-id="98fdd-149">**operation**：識別委派要求的類型 (ChangePassword、ChangeProfile 或 CloseAccount)</span><span class="sxs-lookup"><span data-stu-id="98fdd-149">**operation**: identifies what type of delegation request it is (ChangePassword, ChangeProfile, or CloseAccount)</span></span>
* <span data-ttu-id="98fdd-150">**userId**：要管理之帳戶的使用者 ID</span><span class="sxs-lookup"><span data-stu-id="98fdd-150">**userId**: the user id of the account to manage</span></span>
* <span data-ttu-id="98fdd-151">**salt**：特殊 salt 字串，用於計算安全性雜湊</span><span class="sxs-lookup"><span data-stu-id="98fdd-151">**salt**: a special salt string used for computing a security hash</span></span>
* <span data-ttu-id="98fdd-152">**sig**：已經過計算的安全性雜湊，用於和您已計算的雜湊進行比較</span><span class="sxs-lookup"><span data-stu-id="98fdd-152">**sig**: a computed security hash to be used for comparison to your own computed hash</span></span>

## <span data-ttu-id="98fdd-153"><a name="delegate-product-subscription"> </a>委派產品訂閱</span><span class="sxs-lookup"><span data-stu-id="98fdd-153"><a name="delegate-product-subscription"> </a>Delegating product subscription</span></span>
<span data-ttu-id="98fdd-154">委派產品訂閱的作法類似於委派使用者登入/註冊。</span><span class="sxs-lookup"><span data-stu-id="98fdd-154">Delegating product subscription works similarly to delegating user sign-in/-up.</span></span> <span data-ttu-id="98fdd-155">最終工作流程如下所示：</span><span class="sxs-lookup"><span data-stu-id="98fdd-155">The final workflow would be as follows:</span></span>

1. <span data-ttu-id="98fdd-156">開發人員在 API 管理開發人員入口網站中選取產品，然後按一下 [訂閱] 按鈕</span><span class="sxs-lookup"><span data-stu-id="98fdd-156">Developer selects a product in the API Management developer portal and clicks on the Subscribe button</span></span>
2. <span data-ttu-id="98fdd-157">瀏覽器重新導向至委派端點</span><span class="sxs-lookup"><span data-stu-id="98fdd-157">Browser is redirected to the delegation endpoint</span></span>
3. <span data-ttu-id="98fdd-158">委派端點執行必要的產品訂閱步驟 - 這由您決定，可能需要重新導向至另一個頁面來要求帳單資訊、詢問其他問題，或只是儲存資訊而不要求任何使用者動作</span><span class="sxs-lookup"><span data-stu-id="98fdd-158">Delegation endpoint performs required product subscription steps - this is up to you and may entail redirecting to another page to request billing information, asking additional questions, or simply storing the information and not requiring any user action</span></span>

<span data-ttu-id="98fdd-159">若要啟用此功能，請在 [委派] 頁面按一下 [委派產品訂用帳戶]。</span><span class="sxs-lookup"><span data-stu-id="98fdd-159">To enable the functionality, on the **Delegation** page click **Delegate product subscription**.</span></span>

<span data-ttu-id="98fdd-160">然後，確定委派端點會執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="98fdd-160">Then ensure the delegation endpoint performs the following actions:</span></span>

1. <span data-ttu-id="98fdd-161">接收下列形式的要求：</span><span class="sxs-lookup"><span data-stu-id="98fdd-161">Receive a request in the following form:</span></span>
   
   > <span data-ttu-id="98fdd-162">http://www.yourwebsite.com/apimdelegation?operation={operation}&productId={product to subscribe to}&userId={user making request}&salt={string}&sig={string}</span><span class="sxs-lookup"><span data-stu-id="98fdd-162">*http://www.yourwebsite.com/apimdelegation?operation={operation}&productId={product to subscribe to}&userId={user making request}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="98fdd-163">產品訂閱案例的查詢參數：</span><span class="sxs-lookup"><span data-stu-id="98fdd-163">Query parameters for the product subscription case:</span></span>
   
   * <span data-ttu-id="98fdd-164">**operation**：識別委派要求的類型。</span><span class="sxs-lookup"><span data-stu-id="98fdd-164">**operation**: identifies what type of delegation request it is.</span></span> <span data-ttu-id="98fdd-165">對於產品訂閱要求，有效的選項包括：</span><span class="sxs-lookup"><span data-stu-id="98fdd-165">For product subscription requests the valid options are:</span></span>
     * <span data-ttu-id="98fdd-166">"Subscribe"：為使用者訂閱具有提供之識別碼的 (請參閱下面) 指定產品的要求</span><span class="sxs-lookup"><span data-stu-id="98fdd-166">"Subscribe": a request to subscribe the user to a given product with provided ID (see below)</span></span>
     * <span data-ttu-id="98fdd-167">"Unsubscribe"：將為使用者取消訂閱產品的要求</span><span class="sxs-lookup"><span data-stu-id="98fdd-167">"Unsubscribe": a request to unsubscribe a user from a product</span></span>
     * <span data-ttu-id="98fdd-168">"Renew"：續約訂閱的要求 (例如，可能過期)</span><span class="sxs-lookup"><span data-stu-id="98fdd-168">"Renew": a requst to renew a subscription (e.g. that may be expiring)</span></span>
   * <span data-ttu-id="98fdd-169">**productId**：使用者要求訂閱之產品的識別碼</span><span class="sxs-lookup"><span data-stu-id="98fdd-169">**productId**: the ID of the product the user requested to subscribe to</span></span>
   * <span data-ttu-id="98fdd-170">**userId**：提出要求之使用者的識別碼</span><span class="sxs-lookup"><span data-stu-id="98fdd-170">**userId**: the ID of the user for whom the request is made</span></span>
   * <span data-ttu-id="98fdd-171">**salt**：特殊 salt 字串，用於計算安全性雜湊</span><span class="sxs-lookup"><span data-stu-id="98fdd-171">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="98fdd-172">**sig**：已經過計算的安全性雜湊，用於和您已計算的雜湊進行比較</span><span class="sxs-lookup"><span data-stu-id="98fdd-172">**sig**: a computed security hash to be used for comparison to your own computed hash</span></span>
2. <span data-ttu-id="98fdd-173">確認要求來自 Azure API 管理 (選擇性，但基於安全性理由，強烈建議這麼做)</span><span class="sxs-lookup"><span data-stu-id="98fdd-173">Verify that the request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="98fdd-174">根據 **productId**、**userId** 和 **salt** 查詢字串，計算字串的 HMAC-SHA512：</span><span class="sxs-lookup"><span data-stu-id="98fdd-174">Compute an HMAC-SHA512 of a string based on the **productId**, **userId** and **salt** query parameters:</span></span>
     
     > <span data-ttu-id="98fdd-175">HMAC(**salt** + '\n' + **productId** + '\n' + **userId**)</span><span class="sxs-lookup"><span data-stu-id="98fdd-175">HMAC(**salt** + '\n' + **productId** + '\n' + **userId**)</span></span>
     > 
     > 
   * <span data-ttu-id="98fdd-176">比較以上計算的雜湊和 **sig** 查詢參數的值。</span><span class="sxs-lookup"><span data-stu-id="98fdd-176">Compare the above-computed hash to the value of the **sig** query parameter.</span></span> <span data-ttu-id="98fdd-177">如果兩個雜湊相符，則繼續下一步，否則拒絕要求。</span><span class="sxs-lookup"><span data-stu-id="98fdd-177">If the two hashes match, move on to the next step, otherwise deny the request.</span></span>
3. <span data-ttu-id="98fdd-178">根據 **operation** 中要求的操作類型 (例如帳單、進一步的問題等)，執行任何產品訂閱處理</span><span class="sxs-lookup"><span data-stu-id="98fdd-178">Perform any product subscription processing based on the type of operation requested in **operation** - e.g. billing, further questions, etc.</span></span>
4. <span data-ttu-id="98fdd-179">當使用者在您這邊成功訂閱產品時， [呼叫 REST API 來訂閱產品]，讓使用者訂閱 API 管理產品。</span><span class="sxs-lookup"><span data-stu-id="98fdd-179">On successfully subscribing the user to the product on your side, subscribe the user to the API Management product by [calling the REST API for product subscription].</span></span>

## <span data-ttu-id="98fdd-180"><a name="delegate-example-code"> </a> 範例程式碼</span><span class="sxs-lookup"><span data-stu-id="98fdd-180"><a name="delegate-example-code"> </a> Example Code</span></span>
<span data-ttu-id="98fdd-181">這些程式碼範例示範如何取得「委派驗證金鑰」 (在發行者入口網站的 [委派] 畫面中設定)，以建立隨後用於驗證簽章的 HMAC，藉此證明所傳遞之 returnUrl 的有效性。</span><span class="sxs-lookup"><span data-stu-id="98fdd-181">These code samples show how to take the *delegation validation key*, which is set in the Delegation screen of the publisher portal, to create a HMAC which is then used to validate the signature, proving the validity of the passed returnUrl.</span></span> <span data-ttu-id="98fdd-182">相同的程式碼稍微修改一下後，也適用於 productId 和 userId。</span><span class="sxs-lookup"><span data-stu-id="98fdd-182">The same code works for the productId and userId with slight modification.</span></span>

<span data-ttu-id="98fdd-183">**產生 returnUrl 雜湊的 C# 程式碼**</span><span class="sxs-lookup"><span data-stu-id="98fdd-183">**C# code to generate hash of returnUrl**</span></span>

```c#
using System.Security.Cryptography;

string key = "delegation validation key";
string returnUrl = "returnUrl query parameter";
string salt = "salt query parameter";
string signature;
using (var encoder = new HMACSHA512(Convert.FromBase64String(key)))
{
    signature = Convert.ToBase64String(encoder.ComputeHash(Encoding.UTF8.GetBytes(salt + "\n" + returnUrl)));
    // change to (salt + "\n" + productId + "\n" + userId) when delegating product subscription
    // compare signature to sig query parameter
}
```

<span data-ttu-id="98fdd-184">**產生 returnUrl 雜湊的 NodeJS 程式碼**</span><span class="sxs-lookup"><span data-stu-id="98fdd-184">**NodeJS code to generate hash of returnUrl**</span></span>

```
var crypto = require('crypto');

var key = 'delegation validation key'; 
var returnUrl = 'returnUrl query parameter';
var salt = 'salt query parameter';

var hmac = crypto.createHmac('sha512', new Buffer(key, 'base64'));
var digest = hmac.update(salt + '\n' + returnUrl).digest();
// change to (salt + "\n" + productId + "\n" + userId) when delegating product subscription
// compare signature to sig query parameter

var signature = digest.toString('base64');
```

## <a name="next-steps"></a><span data-ttu-id="98fdd-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="98fdd-185">Next steps</span></span>
<span data-ttu-id="98fdd-186">如需委派的詳細資訊，請觀看以下影片。</span><span class="sxs-lookup"><span data-stu-id="98fdd-186">For more information on delegation, see the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Delegating-User-Authentication-and-Product-Subscription-to-a-3rd-Party-Site/player]
> 
> 

[Delegating developer sign-in and sign-up]: #delegate-signin-up
[Delegating product subscription]: #delegate-product-subscription
<span data-ttu-id="98fdd-187">[要求單一登入 (SSO) 權杖]: http://go.microsoft.com/fwlink/?LinkId=507409</span><span class="sxs-lookup"><span data-stu-id="98fdd-187">[request a single-sign-on (SSO) token]: http://go.microsoft.com/fwlink/?LinkId=507409</span></span>
<span data-ttu-id="98fdd-188">[建立使用者]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser</span><span class="sxs-lookup"><span data-stu-id="98fdd-188">[create a user]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser</span></span>
<span data-ttu-id="98fdd-189">[呼叫 REST API 來訂閱產品]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO</span><span class="sxs-lookup"><span data-stu-id="98fdd-189">[calling the REST API for product subscription]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO</span></span>
[Next steps]: #next-steps
<span data-ttu-id="98fdd-190">[以下提供範例程式碼]: #delegate-example-code</span><span class="sxs-lookup"><span data-stu-id="98fdd-190">[example code provided below]: #delegate-example-code</span></span>

[api-management-delegation-signin-up]: ./media/api-management-howto-setup-delegation/api-management-delegation-signin-up.png 
