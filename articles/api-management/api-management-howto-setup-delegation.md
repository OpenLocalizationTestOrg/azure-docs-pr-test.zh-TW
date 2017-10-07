---
title: "aaaHow toodelegate 使用者註冊和產品訂用帳戶"
description: "了解如何 toodelegate 使用者註冊和產品訂用帳戶 tooa 協力廠商在 Azure API 管理。"
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
ms.openlocfilehash: 406648db2d2f37c4dcda466294726d331cc0551b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodelegate-user-registration-and-product-subscription"></a><span data-ttu-id="56b6a-103">如何 toodelegate 使用者註冊和產品訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="56b6a-103">How toodelegate user registration and product subscription</span></span>
<span data-ttu-id="56b6a-104">委派可讓您 toouse 處理做為開發人員登在 /-註冊和訂用帳戶 tooproducts 您現有的網站而非在 hello 開發人員入口網站中的 toousing hello 內建功能。</span><span class="sxs-lookup"><span data-stu-id="56b6a-104">Delegation allows you toouse your existing website for handling developer sign-in/sign-up and subscription tooproducts as opposed toousing hello built-in functionality in hello developer portal.</span></span> <span data-ttu-id="56b6a-105">這可讓您網站 tooown hello 的使用者資料，並在自訂的方式執行這些步驟的 hello 驗證。</span><span class="sxs-lookup"><span data-stu-id="56b6a-105">This enables your website tooown hello user data and perform hello validation of these steps in a custom way.</span></span>

## <span data-ttu-id="56b6a-106"><a name="delegate-signin-up"> </a>委派開發人員登入和註冊</span><span class="sxs-lookup"><span data-stu-id="56b6a-106"><a name="delegate-signin-up"> </a>Delegating developer sign-in and sign-up</span></span>
<span data-ttu-id="56b6a-107">toodelegate 開發人員登入並註冊 tooyour 現有網站做為 hello 從 hello API 管理開發人員入口網站起始任何這類要求的進入點的網站必須 toocreate 特殊委派端點。</span><span class="sxs-lookup"><span data-stu-id="56b6a-107">toodelegate developer sign-in and sign-up tooyour existing website you will need toocreate a special delegation endpoint on your site that acts as hello entry-point for any such request initiated from hello API Management developer portal.</span></span>

<span data-ttu-id="56b6a-108">hello 最後的工作流程會如下所示：</span><span class="sxs-lookup"><span data-stu-id="56b6a-108">hello final workflow will be as follows:</span></span>

1. <span data-ttu-id="56b6a-109">開發人員按一下 hello 登入或註冊連結在 hello API 管理開發人員入口網站</span><span class="sxs-lookup"><span data-stu-id="56b6a-109">Developer clicks on hello sign-in or sign-up link at hello API Management developer portal</span></span>
2. <span data-ttu-id="56b6a-110">瀏覽器會重新導向的 toohello 委派端點</span><span class="sxs-lookup"><span data-stu-id="56b6a-110">Browser is redirected toohello delegation endpoint</span></span>
3. <span data-ttu-id="56b6a-111">委派端點傳回 tooor 呈現 UI 詢問將使用者重新導向或註冊 toosign 中</span><span class="sxs-lookup"><span data-stu-id="56b6a-111">Delegation endpoint in return redirects tooor presents UI asking user toosign-in or sign-up</span></span>
4. <span data-ttu-id="56b6a-112">成功時，hello 使用者已重新導向後 toohello API 管理開發人員入口網站頁面從它們啟動</span><span class="sxs-lookup"><span data-stu-id="56b6a-112">On success, hello user is redirected back toohello API Management developer portal page they started from</span></span>

<span data-ttu-id="56b6a-113">toobegin，讓我們第一次設定 API 管理 tooroute 會要求透過您委派的端點。</span><span class="sxs-lookup"><span data-stu-id="56b6a-113">toobegin, let's first set-up API Management tooroute requests via your delegation endpoint.</span></span> <span data-ttu-id="56b6a-114">在 [hello API 管理發行者入口網站，按一下**安全性**然後按一下hello**委派**] 索引標籤。按一下 [hello] 核取方塊 tooenable 'Delegate 登入 （& s) 註冊'。</span><span class="sxs-lookup"><span data-stu-id="56b6a-114">In hello API Management publisher portal, click on **Security** and then click hello **Delegation** tab. Click hello checkbox tooenable 'Delegate sign-in & sign-up'.</span></span>

![Delegation page][api-management-delegation-signin-up]

* <span data-ttu-id="56b6a-116">決定哪些 hello 特殊委派端點 URL 會並進入 hello**委派端點 URL**欄位。</span><span class="sxs-lookup"><span data-stu-id="56b6a-116">Decide what hello URL of your special delegation endpoint will be and enter it in hello **Delegation endpoint URL** field.</span></span> 
* <span data-ttu-id="56b6a-117">在 hello**委派驗證金鑰**欄位中，輸入將會使用的 toocompute hello 要求的驗證 tooensure 的簽章提供 tooyou 確實來自 Azure API 管理的密碼。</span><span class="sxs-lookup"><span data-stu-id="56b6a-117">Within hello **Delegation authentication key** field enter a secret that will be used toocompute a signature provided tooyou for verification tooensure that hello request is indeed coming from Azure API Management.</span></span> <span data-ttu-id="56b6a-118">您可以按一下 hello**產生**按鈕 toohave API 積存，隨機產生金鑰。</span><span class="sxs-lookup"><span data-stu-id="56b6a-118">You can click hello **generate** button toohave API Managemnet randomly generate a key for you.</span></span>

<span data-ttu-id="56b6a-119">現在您需要 toocreate hello**委派端點**。</span><span class="sxs-lookup"><span data-stu-id="56b6a-119">Now you need toocreate hello **delegation endpoint**.</span></span> <span data-ttu-id="56b6a-120">它有 tooperform 數個動作：</span><span class="sxs-lookup"><span data-stu-id="56b6a-120">It has tooperform a number of actions:</span></span>

1. <span data-ttu-id="56b6a-121">在下列形式的 hello 收到的要求：</span><span class="sxs-lookup"><span data-stu-id="56b6a-121">Receive a request in hello following form:</span></span>
   
   > <span data-ttu-id="56b6a-122">http://www.yourwebsite.com/apimdelegation?operation=SignIn&returnUrl={URL of source page}&salt={string}&sig={string}</span><span class="sxs-lookup"><span data-stu-id="56b6a-122">*http://www.yourwebsite.com/apimdelegation?operation=SignIn&returnUrl={URL of source page}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="56b6a-123">Hello 登入 / 註冊案例的查詢參數：</span><span class="sxs-lookup"><span data-stu-id="56b6a-123">Query parameters for hello sign-in / sign-up case:</span></span>
   
   * <span data-ttu-id="56b6a-124">**operation**：識別委派要求的類型 - 在此案例中只能是 **SignIn**</span><span class="sxs-lookup"><span data-stu-id="56b6a-124">**operation**: identifies what type of delegation request it is - it can only be **SignIn** in this case</span></span>
   * <span data-ttu-id="56b6a-125">**returnUrl**: hello hello 使用者在登入或註冊連結的點選處的 hello 網頁的 URL</span><span class="sxs-lookup"><span data-stu-id="56b6a-125">**returnUrl**: hello URL of hello page where hello user clicked on a sign-in or sign-up link</span></span>
   * <span data-ttu-id="56b6a-126">**salt**：特殊 salt 字串，用於計算安全性雜湊</span><span class="sxs-lookup"><span data-stu-id="56b6a-126">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="56b6a-127">**sig**： 用於比較 tooyour 自己計算的安全性雜湊 toobe 計算雜湊</span><span class="sxs-lookup"><span data-stu-id="56b6a-127">**sig**: a computed security hash toobe used for comparison tooyour own computed hash</span></span>
2. <span data-ttu-id="56b6a-128">請確認該 hello 要求來自於 Azure API 管理 （選擇性，但強烈建議使用的安全性）</span><span class="sxs-lookup"><span data-stu-id="56b6a-128">Verify that hello request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="56b6a-129">計算字串 hello 為基礎的 hmac-sha512 雜湊**returnUrl**和**salt**查詢參數 ([下面提供的範例程式碼]):</span><span class="sxs-lookup"><span data-stu-id="56b6a-129">Compute an HMAC-SHA512 hash of a string based on hello **returnUrl** and **salt** query parameters ([example code provided below]):</span></span>
     
     > <span data-ttu-id="56b6a-130">HMAC(**salt** + '\n' + **returnUrl**)</span><span class="sxs-lookup"><span data-stu-id="56b6a-130">HMAC(**salt** + '\n' + **returnUrl**)</span></span>
     > 
     > 
   * <span data-ttu-id="56b6a-131">比較 hello hello 上面計算出雜湊 toohello 值**sig**查詢參數。</span><span class="sxs-lookup"><span data-stu-id="56b6a-131">Compare hello above-computed hash toohello value of hello **sig** query parameter.</span></span> <span data-ttu-id="56b6a-132">如果 hello 兩個雜湊相符，toohello 下一個步驟上移動，否則會拒絕 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="56b6a-132">If hello two hashes match, move on toohello next step, otherwise deny hello request.</span></span>
3. <span data-ttu-id="56b6a-133">確認您收到登輸入/符號上的要求： hello**作業**查詢參數會設定得 「**SignIn**"。</span><span class="sxs-lookup"><span data-stu-id="56b6a-133">Verify that you are receiving a request for sign-in/sign-up: hello **operation** query parameter will be set too"**SignIn**".</span></span>
4. <span data-ttu-id="56b6a-134">使用 UI 或註冊 toosign 中出現的 hello 使用者</span><span class="sxs-lookup"><span data-stu-id="56b6a-134">Present hello user with UI toosign-in or sign-up</span></span>
5. <span data-ttu-id="56b6a-135">如果 hello 使用者註冊您的 toocreate 對應帳戶它們在 API 管理。</span><span class="sxs-lookup"><span data-stu-id="56b6a-135">If hello user is signing-up you have toocreate a corresponding account for them in API Management.</span></span> <span data-ttu-id="56b6a-136">[建立使用者]以 hello API 管理 REST API。</span><span class="sxs-lookup"><span data-stu-id="56b6a-136">[Create a user] with hello API Management REST API.</span></span> <span data-ttu-id="56b6a-137">當此情況下，確定您設定 hello 使用者識別碼 toohello 您使用者存放區中相同或 tooan 識別碼，您可以追蹤。</span><span class="sxs-lookup"><span data-stu-id="56b6a-137">When doing so, ensure that you set hello user ID toohello same it is in your user store or tooan ID that you can keep track of.</span></span>
6. <span data-ttu-id="56b6a-138">當成功驗證 hello 使用者：</span><span class="sxs-lookup"><span data-stu-id="56b6a-138">When hello user is successfully authenticated:</span></span>
   
   * <span data-ttu-id="56b6a-139">[要求的單一登入 (SSO) 權杖]透過 hello API 管理 REST API</span><span class="sxs-lookup"><span data-stu-id="56b6a-139">[request a single-sign-on (SSO) token] via hello API Management REST API</span></span>
   * <span data-ttu-id="56b6a-140">附加 returnUrl 查詢參數 toohello SSO URL 收到來自上述的 hello API 呼叫：</span><span class="sxs-lookup"><span data-stu-id="56b6a-140">append a returnUrl query parameter toohello SSO URL you have received from hello API call above:</span></span>
     
     > <span data-ttu-id="56b6a-141">例如，https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span><span class="sxs-lookup"><span data-stu-id="56b6a-141">e.g. https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span></span> 
     > 
     > 
   * <span data-ttu-id="56b6a-142">重新導向 hello 使用者 toohello 上面所產生的 URL</span><span class="sxs-lookup"><span data-stu-id="56b6a-142">redirect hello user toohello above produced URL</span></span>

<span data-ttu-id="56b6a-143">在加法 toohello **SignIn**作業，您也可以執行帳戶管理 hello 上一個步驟，並使用其中一個 hello 下列作業。</span><span class="sxs-lookup"><span data-stu-id="56b6a-143">In addition toohello **SignIn** operation, you can also perform account management by following hello previous steps and using one of hello following operations.</span></span>

* <span data-ttu-id="56b6a-144">**ChangePassword**</span><span class="sxs-lookup"><span data-stu-id="56b6a-144">**ChangePassword**</span></span>
* <span data-ttu-id="56b6a-145">**ChangeProfile**</span><span class="sxs-lookup"><span data-stu-id="56b6a-145">**ChangeProfile**</span></span>
* <span data-ttu-id="56b6a-146">**CloseAccount**</span><span class="sxs-lookup"><span data-stu-id="56b6a-146">**CloseAccount**</span></span>

<span data-ttu-id="56b6a-147">您必須傳遞下列帳戶管理作業的查詢參數的 hello。</span><span class="sxs-lookup"><span data-stu-id="56b6a-147">You must pass hello following query parameters for account management operations.</span></span>

* <span data-ttu-id="56b6a-148">**operation**：識別委派要求的類型 (ChangePassword、ChangeProfile 或 CloseAccount)</span><span class="sxs-lookup"><span data-stu-id="56b6a-148">**operation**: identifies what type of delegation request it is (ChangePassword, ChangeProfile, or CloseAccount)</span></span>
* <span data-ttu-id="56b6a-149">**userId**: hello 帳戶 toomanage hello 使用者識別碼</span><span class="sxs-lookup"><span data-stu-id="56b6a-149">**userId**: hello user id of hello account toomanage</span></span>
* <span data-ttu-id="56b6a-150">**salt**：特殊 salt 字串，用於計算安全性雜湊</span><span class="sxs-lookup"><span data-stu-id="56b6a-150">**salt**: a special salt string used for computing a security hash</span></span>
* <span data-ttu-id="56b6a-151">**sig**： 用於比較 tooyour 自己計算的安全性雜湊 toobe 計算雜湊</span><span class="sxs-lookup"><span data-stu-id="56b6a-151">**sig**: a computed security hash toobe used for comparison tooyour own computed hash</span></span>

## <span data-ttu-id="56b6a-152"><a name="delegate-product-subscription"> </a>委派產品訂閱</span><span class="sxs-lookup"><span data-stu-id="56b6a-152"><a name="delegate-product-subscription"> </a>Delegating product subscription</span></span>
<span data-ttu-id="56b6a-153">委派產品訂用帳戶的運作方式類似 toodelegating 使用者登入/總。</span><span class="sxs-lookup"><span data-stu-id="56b6a-153">Delegating product subscription works similarly toodelegating user sign-in/-up.</span></span> <span data-ttu-id="56b6a-154">hello 最後的工作流程應如下所示：</span><span class="sxs-lookup"><span data-stu-id="56b6a-154">hello final workflow would be as follows:</span></span>

1. <span data-ttu-id="56b6a-155">開發人員在 hello API 管理開發人員入口網站中選取產品，然後按一下 hello 訂閱 」 按鈕</span><span class="sxs-lookup"><span data-stu-id="56b6a-155">Developer selects a product in hello API Management developer portal and clicks on hello Subscribe button</span></span>
2. <span data-ttu-id="56b6a-156">瀏覽器會重新導向的 toohello 委派端點</span><span class="sxs-lookup"><span data-stu-id="56b6a-156">Browser is redirected toohello delegation endpoint</span></span>
3. <span data-ttu-id="56b6a-157">委派端點會執行必要的產品訂用帳戶的步驟-這是總 tooyou，而且可能需要重新導向 tooanother 頁面 toorequest 帳單資訊、 詢問其他問題，或只儲存 hello 資訊並不需要任何使用者動作</span><span class="sxs-lookup"><span data-stu-id="56b6a-157">Delegation endpoint performs required product subscription steps - this is up tooyou and may entail redirecting tooanother page toorequest billing information, asking additional questions, or simply storing hello information and not requiring any user action</span></span>

<span data-ttu-id="56b6a-158">hello 上的 tooenable hello 功能**委派**頁面上，按一下**委派產品訂閱**。</span><span class="sxs-lookup"><span data-stu-id="56b6a-158">tooenable hello functionality, on hello **Delegation** page click **Delegate product subscription**.</span></span>

<span data-ttu-id="56b6a-159">請確定 hello 委派端點執行下列動作的 hello:</span><span class="sxs-lookup"><span data-stu-id="56b6a-159">Then ensure hello delegation endpoint performs hello following actions:</span></span>

1. <span data-ttu-id="56b6a-160">在下列形式的 hello 收到的要求：</span><span class="sxs-lookup"><span data-stu-id="56b6a-160">Receive a request in hello following form:</span></span>
   
   > <span data-ttu-id="56b6a-161">*http://www.yourwebsite.com/apimdelegation?operation= {作業} （& s) productId = {產品 toosubscribe 至} （& s) userId = {提出要求的 user} & salt = {string} （& s) sig = {string}*</span><span class="sxs-lookup"><span data-stu-id="56b6a-161">*http://www.yourwebsite.com/apimdelegation?operation={operation}&productId={product toosubscribe to}&userId={user making request}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="56b6a-162">Hello 產品訂閱案例的查詢參數：</span><span class="sxs-lookup"><span data-stu-id="56b6a-162">Query parameters for hello product subscription case:</span></span>
   
   * <span data-ttu-id="56b6a-163">**operation**：識別委派要求的類型。</span><span class="sxs-lookup"><span data-stu-id="56b6a-163">**operation**: identifies what type of delegation request it is.</span></span> <span data-ttu-id="56b6a-164">產品訂用帳戶要求 hello 有效的選項為：</span><span class="sxs-lookup"><span data-stu-id="56b6a-164">For product subscription requests hello valid options are:</span></span>
     * <span data-ttu-id="56b6a-165">「 訂閱 」: 指定產品要求 toosubscribe hello 使用者 tooa 提供識別碼 （請參閱下文）</span><span class="sxs-lookup"><span data-stu-id="56b6a-165">"Subscribe": a request toosubscribe hello user tooa given product with provided ID (see below)</span></span>
     * <span data-ttu-id="56b6a-166">「 取消 」: 要求 toounsubscribe 產品中的使用者</span><span class="sxs-lookup"><span data-stu-id="56b6a-166">"Unsubscribe": a request toounsubscribe a user from a product</span></span>
     * <span data-ttu-id="56b6a-167">「 更新 」: 要求的 toorenew 的訂用帳戶 （例如可能即將到期的時間）</span><span class="sxs-lookup"><span data-stu-id="56b6a-167">"Renew": a requst toorenew a subscription (e.g. that may be expiring)</span></span>
   * <span data-ttu-id="56b6a-168">**productId**: hello 識別碼 hello 產品 hello 使用者要求來 toosubscribe</span><span class="sxs-lookup"><span data-stu-id="56b6a-168">**productId**: hello ID of hello product hello user requested toosubscribe to</span></span>
   * <span data-ttu-id="56b6a-169">**userId**: hello hello 使用者針對 hello 要求識別碼</span><span class="sxs-lookup"><span data-stu-id="56b6a-169">**userId**: hello ID of hello user for whom hello request is made</span></span>
   * <span data-ttu-id="56b6a-170">**salt**：特殊 salt 字串，用於計算安全性雜湊</span><span class="sxs-lookup"><span data-stu-id="56b6a-170">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="56b6a-171">**sig**： 用於比較 tooyour 自己計算的安全性雜湊 toobe 計算雜湊</span><span class="sxs-lookup"><span data-stu-id="56b6a-171">**sig**: a computed security hash toobe used for comparison tooyour own computed hash</span></span>
2. <span data-ttu-id="56b6a-172">請確認該 hello 要求來自於 Azure API 管理 （選擇性，但強烈建議使用的安全性）</span><span class="sxs-lookup"><span data-stu-id="56b6a-172">Verify that hello request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="56b6a-173">計算字串 hello 為基礎的 hmac-sha512 **productId**， **userId**和**salt**查詢參數：</span><span class="sxs-lookup"><span data-stu-id="56b6a-173">Compute an HMAC-SHA512 of a string based on hello **productId**, **userId** and **salt** query parameters:</span></span>
     
     > <span data-ttu-id="56b6a-174">HMAC(**salt** + '\n' + **productId** + '\n' + **userId**)</span><span class="sxs-lookup"><span data-stu-id="56b6a-174">HMAC(**salt** + '\n' + **productId** + '\n' + **userId**)</span></span>
     > 
     > 
   * <span data-ttu-id="56b6a-175">比較 hello hello 上面計算出雜湊 toohello 值**sig**查詢參數。</span><span class="sxs-lookup"><span data-stu-id="56b6a-175">Compare hello above-computed hash toohello value of hello **sig** query parameter.</span></span> <span data-ttu-id="56b6a-176">如果 hello 兩個雜湊相符，toohello 下一個步驟上移動，否則會拒絕 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="56b6a-176">If hello two hashes match, move on toohello next step, otherwise deny hello request.</span></span>
3. <span data-ttu-id="56b6a-177">執行根據 hello 類型中所要求任何的作業產品訂用帳戶處理**作業**-例如計費，取得進一步的問題，依此類推。</span><span class="sxs-lookup"><span data-stu-id="56b6a-177">Perform any product subscription processing based on hello type of operation requested in **operation** - e.g. billing, further questions, etc.</span></span>
4. <span data-ttu-id="56b6a-178">在成功訂閱 hello 使用者 toohello 產品，在您身邊，訂閱 hello 使用者 toohello API 管理產品[呼叫 hello REST API 產品訂用帳戶]。</span><span class="sxs-lookup"><span data-stu-id="56b6a-178">On successfully subscribing hello user toohello product on your side, subscribe hello user toohello API Management product by [calling hello REST API for product subscription].</span></span>

## <span data-ttu-id="56b6a-179"><a name="delegate-example-code"> </a> 範例程式碼</span><span class="sxs-lookup"><span data-stu-id="56b6a-179"><a name="delegate-example-code"> </a> Example Code</span></span>
<span data-ttu-id="56b6a-180">這些程式碼範例顯示如何 tootake hello*委派驗證金鑰*hello 委派 hello 發行者入口網站畫面中設定、 toocreate 的 HMAC，然後使用 toovalidate hello 簽章，證明 hello hello 有效性傳回傳入的 Url。</span><span class="sxs-lookup"><span data-stu-id="56b6a-180">These code samples show how tootake hello *delegation validation key*, which is set in hello Delegation screen of hello publisher portal, toocreate a HMAC which is then used toovalidate hello signature, proving hello validity of hello passed returnUrl.</span></span> <span data-ttu-id="56b6a-181">相同的程式碼適用於 hello productId 和稍微修改的使用者識別碼 hello。</span><span class="sxs-lookup"><span data-stu-id="56b6a-181">hello same code works for hello productId and userId with slight modification.</span></span>

<span data-ttu-id="56b6a-182">**C# 程式碼 toogenerate 的雜湊 returnUrl**</span><span class="sxs-lookup"><span data-stu-id="56b6a-182">**C# code toogenerate hash of returnUrl**</span></span>

```c#
using System.Security.Cryptography;

string key = "delegation validation key";
string returnUrl = "returnUrl query parameter";
string salt = "salt query parameter";
string signature;
using (var encoder = new HMACSHA512(Convert.FromBase64String(key)))
{
    signature = Convert.ToBase64String(encoder.ComputeHash(Encoding.UTF8.GetBytes(salt + "\n" + returnUrl)));
    // change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
    // compare signature toosig query parameter
}
```

<span data-ttu-id="56b6a-183">**NodeJS 的 returnUrl toogenerate 雜湊程式碼**</span><span class="sxs-lookup"><span data-stu-id="56b6a-183">**NodeJS code toogenerate hash of returnUrl**</span></span>

```
var crypto = require('crypto');

var key = 'delegation validation key'; 
var returnUrl = 'returnUrl query parameter';
var salt = 'salt query parameter';

var hmac = crypto.createHmac('sha512', new Buffer(key, 'base64'));
var digest = hmac.update(salt + '\n' + returnUrl).digest();
// change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
// compare signature toosig query parameter

var signature = digest.toString('base64');
```

## <a name="next-steps"></a><span data-ttu-id="56b6a-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="56b6a-184">Next steps</span></span>
<span data-ttu-id="56b6a-185">如需委派的詳細資訊，請參閱下列視訊的 hello。</span><span class="sxs-lookup"><span data-stu-id="56b6a-185">For more information on delegation, see hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Delegating-User-Authentication-and-Product-Subscription-to-a-3rd-Party-Site/player]
> 
> 

[Delegating developer sign-in and sign-up]: #delegate-signin-up
[Delegating product subscription]: #delegate-product-subscription
[要求的單一登入 (SSO) 權杖]: http://go.microsoft.com/fwlink/?LinkId=507409
[建立使用者]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser
[呼叫 hello REST API 產品訂用帳戶]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO
[Next steps]: #next-steps
[下面提供的範例程式碼]: #delegate-example-code

[api-management-delegation-signin-up]: ./media/api-management-howto-setup-delegation/api-management-delegation-signin-up.png 
