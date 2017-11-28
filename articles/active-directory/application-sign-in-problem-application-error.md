---
title: "在應用程式的頁面上，在登入後 aaaError |Microsoft 文件"
description: "如何使用 Azure AD 的 tooresolve 問題時登入 hello 應用程式本身會發出錯誤"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 317b6f8e6417520ead80ae4e26c591ba6b134683
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="error-on-an-applications-page-after-signing-in"></a><span data-ttu-id="5f435-103">登入後應用程式頁面的錯誤</span><span class="sxs-lookup"><span data-stu-id="5f435-103">Error on an application's page after signing in</span></span>

<span data-ttu-id="5f435-104">在此案例中，Azure AD 已簽署 hello 使用者，但是 hello 應用程式會顯示不允許 hello 使用者 toosuccessfully 完成 hello 登流程中發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="5f435-104">In this scenario, Azure AD has signed hello user in, but hello application is displaying an error not allowing hello user toosuccessfully finish hello sign in flow.</span></span> <span data-ttu-id="5f435-105">在此案例中，hello 應用程式不接受 hello 回應問題由 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="5f435-105">In this scenario, hello application is not accepting hello response issue by Azure AD.</span></span>

<span data-ttu-id="5f435-106">有可能的原因為何 hello 應用程式不接受來自 Azure AD 的 hello 回應。</span><span class="sxs-lookup"><span data-stu-id="5f435-106">There are some possible reasons why hello application didn’t accept hello response from Azure AD.</span></span> <span data-ttu-id="5f435-107">如果 hello 應用程式中的 hello 錯誤是不明確，足以 tooknow 遺漏了什麼 hello 回應，然後：</span><span class="sxs-lookup"><span data-stu-id="5f435-107">If hello error in hello application is not clear enough tooknow what is missing in hello response, then:</span></span>

-   <span data-ttu-id="5f435-108">如果 hello 應用程式 hello Azure AD 的組件庫，請確認您已依照 hello 文件中的所有 hello 步驟[如何 toodebug SAML 型單一登入 tooapplications Azure Active Directory 中](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging)。</span><span class="sxs-lookup"><span data-stu-id="5f435-108">If hello application is hello Azure AD Gallery, verify you have followed all hello steps in hello article [How toodebug SAML-based single sign-on tooapplications in Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).</span></span>

-   <span data-ttu-id="5f435-109">使用這類工具[Fiddler](http://www.telerik.com/fiddler) toocapture SAML 要求，SAML 回應和 SAML 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="5f435-109">Use a tool like [Fiddler](http://www.telerik.com/fiddler) toocapture SAML request, SAML response and SAML token.</span></span>

-   <span data-ttu-id="5f435-110">缺少哪些資訊與 hello 應用程式廠商 tooknow 共用 hello SAML 回應。</span><span class="sxs-lookup"><span data-stu-id="5f435-110">Share hello SAML response with hello application vendor tooknow what is missing.</span></span>

## <a name="missing-attributes-in-hello-saml-response"></a><span data-ttu-id="5f435-111">Hello SAML 回應中遺漏屬性</span><span class="sxs-lookup"><span data-stu-id="5f435-111">Missing attributes in hello SAML response</span></span>

<span data-ttu-id="5f435-112">tooadd Azure AD hello 回應 hello Azure AD 組態 toobe 中的屬性，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="5f435-112">tooadd an attribute in hello Azure AD configuration toobe sent in hello Azure AD response, follow hello steps below:</span></span>

1.  <span data-ttu-id="5f435-113">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="5f435-113">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="5f435-114">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="5f435-114">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5f435-115">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="5f435-115">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5f435-116">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="5f435-116">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5f435-117">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="5f435-117">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="5f435-118">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="5f435-118">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="5f435-119">選取您想 tooconfigure 單一登入的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5f435-119">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="5f435-120">一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="5f435-120">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="5f435-121">按一下**檢視及編輯所有其他使用者屬性下**hello**使用者屬性**區段 tooedit hello 屬性 hello SAML 權杖中傳送的 toobe toohello 應用程式，當使用者登入。</span><span class="sxs-lookup"><span data-stu-id="5f435-121">click **View and edit all other user attributes under** hello **User Attributes** section tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="5f435-122">tooadd 屬性：</span><span class="sxs-lookup"><span data-stu-id="5f435-122">tooadd an attribute:</span></span>

   * <span data-ttu-id="5f435-123">按一下 [新增屬性]。</span><span class="sxs-lookup"><span data-stu-id="5f435-123">click **Add attribute**.</span></span> <span data-ttu-id="5f435-124">輸入 hello**名稱**和 hello 選取 hello**值**從 hello 下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="5f435-124">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   * <span data-ttu-id="5f435-125">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="5f435-125">Click **Save.**</span></span> <span data-ttu-id="5f435-126">您會看到 hello hello 資料表中的新屬性。</span><span class="sxs-lookup"><span data-stu-id="5f435-126">You see hello new attribute in hello table.</span></span>

9.  <span data-ttu-id="5f435-127">儲存 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="5f435-127">Save hello configuration.</span></span>

<span data-ttu-id="5f435-128">下一次 hello 使用者登入時 toohello 應用程式，Azure AD 傳送 hello SAML 回應 hello 新屬性。</span><span class="sxs-lookup"><span data-stu-id="5f435-128">Next time hello user signs in toohello application, Azure AD send hello new attribute in hello SAML response.</span></span>

## <a name="hello-application-expects-a-different-user-identifier-value-or-format"></a><span data-ttu-id="5f435-129">hello 應用程式預期不同的使用者識別碼值或格式</span><span class="sxs-lookup"><span data-stu-id="5f435-129">hello application expects a different User Identifier value or format</span></span>

<span data-ttu-id="5f435-130">hello 登入 toohello 應用程式失敗，因為 SAML 回應 hello 遺失屬性，例如角色或因為 hello 應用程式預期不同格式的 hello EntityID 屬性。</span><span class="sxs-lookup"><span data-stu-id="5f435-130">hello sign-in toohello application is failing because hello SAML response is missing attributes such as roles or because hello application is expecting a different format for hello EntityID attribute.</span></span>

## <a name="add-an-attribute-in-hello-azure-ad-application-configuration"></a><span data-ttu-id="5f435-131">將屬性加入 hello Azure AD 應用程式組態中：</span><span class="sxs-lookup"><span data-stu-id="5f435-131">Add an attribute in hello Azure AD application configuration:</span></span>

<span data-ttu-id="5f435-132">toochange hello 使用者識別碼的值，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="5f435-132">toochange hello User Identifier value, follow hello steps below:</span></span>

1.  <span data-ttu-id="5f435-133">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="5f435-133">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="5f435-134">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="5f435-134">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5f435-135">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="5f435-135">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5f435-136">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="5f435-136">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5f435-137">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="5f435-137">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="5f435-138">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="5f435-138">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="5f435-139">選取您想 tooconfigure 單一登入的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5f435-139">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="5f435-140">一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="5f435-140">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="5f435-141">在 [hello**使用者屬性**，選取 hello hello 中使用者的唯一識別碼**使用者識別碼**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="5f435-141">Under hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

## <a name="change-entityid-user-identifier-format"></a><span data-ttu-id="5f435-142">變更 EntityID (使用者識別碼) 格式</span><span class="sxs-lookup"><span data-stu-id="5f435-142">Change EntityID (User Identifier) format</span></span>

<span data-ttu-id="5f435-143">如果 hello 應用程式預期 hello EntityID 屬性的另一種格式。</span><span class="sxs-lookup"><span data-stu-id="5f435-143">If hello application expects another format for hello EntityID attribute.</span></span> <span data-ttu-id="5f435-144">然後，您必須能夠 tooselect hello EntityID （使用者識別碼） 格式，Azure AD 會傳送 toohello 應用程式以 hello 回應使用者驗證之後。</span><span class="sxs-lookup"><span data-stu-id="5f435-144">Then, you won’t be able tooselect hello EntityID (User Identifier) format that Azure AD sends toohello application in hello response after user authentication.</span></span>

<span data-ttu-id="5f435-145">Hello NameID 屬性 （使用者識別碼） 的 azure AD 選取 hello 格式會根據選取的 hello 值或 hello hello hello SAML AuthRequest 中的應用程式所要求的格式。</span><span class="sxs-lookup"><span data-stu-id="5f435-145">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="5f435-146">如需詳細資訊，請造訪 hello 文章[單一登入的 SAML 通訊協定](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest)hello 下一節 NameIDPolicy。</span><span class="sxs-lookup"><span data-stu-id="5f435-146">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>

## <a name="hello-application-expects-a-different-signature-method-for-hello-saml-response"></a><span data-ttu-id="5f435-147">hello 應用程式預期 hello SAML 回應不同的簽章方法</span><span class="sxs-lookup"><span data-stu-id="5f435-147">hello application expects a different signature method for hello SAML response</span></span>

<span data-ttu-id="5f435-148">Azure Active Directory 進行數位簽署 hello SAML 權杖中的哪些部分 toochange。</span><span class="sxs-lookup"><span data-stu-id="5f435-148">toochange what parts of hello SAML token are digitally signed by Azure Active Directory.</span></span> <span data-ttu-id="5f435-149">請遵循下列步驟執行 hello:</span><span class="sxs-lookup"><span data-stu-id="5f435-149">Follow hello steps below:</span></span>

1.  <span data-ttu-id="5f435-150">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="5f435-150">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="5f435-151">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="5f435-151">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5f435-152">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="5f435-152">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5f435-153">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="5f435-153">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5f435-154">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="5f435-154">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="5f435-155">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="5f435-155">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="5f435-156">選取您想 tooconfigure 單一登入的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5f435-156">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="5f435-157">一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="5f435-157">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="5f435-158">按一下**顯示進階憑證簽署設定**下 hello **SAML 簽章憑證**> 一節。</span><span class="sxs-lookup"><span data-stu-id="5f435-158">click **Show advanced certificate signing settings** under hello **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="5f435-159">選取適當的 hello**簽署選項**hello 應用程式所需要：</span><span class="sxs-lookup"><span data-stu-id="5f435-159">Select hello appropriate **Signing Option** expected by hello application:</span></span>

  * <span data-ttu-id="5f435-160">簽署 SAML 回應</span><span class="sxs-lookup"><span data-stu-id="5f435-160">Sign SAML response</span></span>

  * <span data-ttu-id="5f435-161">簽署 SAML 回應及判斷提示</span><span class="sxs-lookup"><span data-stu-id="5f435-161">Sign SAML response and assertion</span></span>

  * <span data-ttu-id="5f435-162">簽署 SAML 判斷提示</span><span class="sxs-lookup"><span data-stu-id="5f435-162">Sign SAML assertion</span></span>

<span data-ttu-id="5f435-163">下一次 hello 使用者登入時 toohello 應用程式，Azure AD 登 hello 選取 hello SAML 回應的一部分。</span><span class="sxs-lookup"><span data-stu-id="5f435-163">Next time hello user signs in toohello application, Azure AD sign hello part of hello SAML response selected.</span></span>

## <a name="hello-application-expects-hello-signing-algorithm-toobe-sha-1"></a><span data-ttu-id="5f435-164">hello 應用程式必須要有簽章演算法 toobe sha-1 hello</span><span class="sxs-lookup"><span data-stu-id="5f435-164">hello application expects hello signing algorithm toobe SHA-1</span></span>

<span data-ttu-id="5f435-165">根據預設，Azure AD 簽署 hello SAML 權杖使用 hello 大部分的安全性演算法。</span><span class="sxs-lookup"><span data-stu-id="5f435-165">By default, Azure AD signs hello SAML token using hello most security algorithm.</span></span> <span data-ttu-id="5f435-166">不建議變更 hello 登演算法 tooSHA-1，除非需要 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5f435-166">Changing hello sign algorithm tooSHA-1 is not recommended unless required by hello application.</span></span>

<span data-ttu-id="5f435-167">toochange hello 簽章演算法，請依照下列步驟執行 hello:</span><span class="sxs-lookup"><span data-stu-id="5f435-167">toochange hello signing algorithm, follow hello steps below:</span></span>

1.  <span data-ttu-id="5f435-168">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="5f435-168">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="5f435-169">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="5f435-169">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5f435-170">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="5f435-170">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5f435-171">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="5f435-171">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5f435-172">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="5f435-172">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="5f435-173">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="5f435-173">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="5f435-174">選取您想 tooconfigure 單一登入的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5f435-174">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="5f435-175">一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="5f435-175">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="5f435-176">按一下**顯示進階憑證簽署設定**下 hello **SAML 簽章憑證**> 一節。</span><span class="sxs-lookup"><span data-stu-id="5f435-176">click **Show advanced certificate signing settings** under hello **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="5f435-177">選取在 hello sha-1**簽署演算法**。</span><span class="sxs-lookup"><span data-stu-id="5f435-177">Select SHA-1, in hello **Signing Algorithm**.</span></span>

<span data-ttu-id="5f435-178">下一次 hello 使用者登入，toohello 應用程式中的，Azure AD 登 hello 使用 sha-1 演算法的 SAML 權杖。</span><span class="sxs-lookup"><span data-stu-id="5f435-178">Next time hello user signs in toohello application, Azure AD sign hello SAML token using SHA-1 algorithm.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f435-179">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5f435-179">Next steps</span></span>
[<span data-ttu-id="5f435-180">如何 toodebug SAML 型單一登入 tooapplications Azure Active Directory 中</span><span class="sxs-lookup"><span data-stu-id="5f435-180">How toodebug SAML-based single sign-on tooapplications in Azure Active Directory</span></span>](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging)
