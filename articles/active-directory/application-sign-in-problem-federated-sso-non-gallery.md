---
title: "aaaProblems 登入 tooa 非組件庫的應用程式設定同盟單一登入 |Microsoft 文件"
description: "Hello 登入 tooan 設定 saml 同盟單一登入與 Azure AD 的應用程式時可能面臨的特定問題的指引"
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
ms.openlocfilehash: 1243456695c097f404a66fc89893efa2afdaaf22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooa-non-gallery-application-configured-for-federated-single-sign-on"></a><span data-ttu-id="29547-103">登入 tooa 非組件庫的應用程式設定同盟單一登入問題</span><span class="sxs-lookup"><span data-stu-id="29547-103">Problems signing in tooa non-gallery application configured for federated single sign-on</span></span>

<span data-ttu-id="29547-104">tootroubleshoot 您的問題，您需要在 Azure AD 做為後續 tooverify hello 應用程式組態：</span><span class="sxs-lookup"><span data-stu-id="29547-104">tootroubleshoot your problem, you need tooverify hello application configuration in Azure AD as follow:</span></span>

-   <span data-ttu-id="29547-105">您已依照 hello Azure AD 組件庫的應用程式的所有 hello 組態步驟。</span><span class="sxs-lookup"><span data-stu-id="29547-105">You have followed all hello configuration steps for hello Azure AD gallery application.</span></span>

-   <span data-ttu-id="29547-106">hello 識別碼和設定在 AAD 中的回覆 URL 符合它們 hello 應用程式中的預期值</span><span class="sxs-lookup"><span data-stu-id="29547-106">hello Identifier and Reply URL configured in AAD match they expected values in hello application</span></span>

-   <span data-ttu-id="29547-107">您已指派使用者 toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="29547-107">You have assigned users toohello application</span></span>

## <a name="application-not-found-in-directory"></a><span data-ttu-id="29547-108">在目錄中找不到應用程式</span><span class="sxs-lookup"><span data-stu-id="29547-108">Application not found in directory</span></span>

<span data-ttu-id="29547-109">*錯誤 AADSTS70001: Hello 目錄中未找到具有識別碼 'https://contoso.com' 的應用程式*。</span><span class="sxs-lookup"><span data-stu-id="29547-109">*Error AADSTS70001: Application with Identifier ‘https://contoso.com’ was not found in hello directory*.</span></span>

<span data-ttu-id="29547-110">**可能的原因**</span><span class="sxs-lookup"><span data-stu-id="29547-110">**Possible cause**</span></span>

<span data-ttu-id="29547-111">hello 簽發者屬性會從傳送 hello 應用程式 tooAzure hello SAML 要求中的 AD 與 hello hello 應用程式的 Azure AD 中設定的識別項值不相符。</span><span class="sxs-lookup"><span data-stu-id="29547-111">hello Issuer attribute sends from hello application tooAzure AD in hello SAML request doesn’t match hello Identifier value configured in hello application Azure AD.</span></span>

<span data-ttu-id="29547-112">**解決方案**</span><span class="sxs-lookup"><span data-stu-id="29547-112">**Resolution**</span></span>

<span data-ttu-id="29547-113">請確定它符合 hello Azure AD 中所設定的識別碼值的 hello SAML 要求中的 hello 簽發者屬性：</span><span class="sxs-lookup"><span data-stu-id="29547-113">Ensure that hello Issuer attribute in hello SAML request it’s matching hello Identifier value configured in Azure AD:</span></span>

1.  <span data-ttu-id="29547-114">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="29547-114">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="29547-115">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="29547-115">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="29547-116">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="29547-116">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="29547-117">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="29547-117">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="29547-118">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="29547-118">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="29547-119">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="29547-119">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="29547-120">選取您想 tooconfigure 單一登入的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="29547-120">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="29547-121">一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="29547-121">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="29547-122"><span id="_Hlk477190042" class="anchor"></span>跳過**網域和 Url** > 一節。</span><span class="sxs-lookup"><span data-stu-id="29547-122"><span id="_Hlk477190042" class="anchor"></span>Go too**Domain and URLs** section.</span></span> <span data-ttu-id="29547-123">請確認 hello 值在 hello 相符 hello 值顯示在 hello 錯誤中的 hello 識別碼值的文字方塊中的識別項。</span><span class="sxs-lookup"><span data-stu-id="29547-123">Verify that hello value in hello Identifier textbox is matching hello value for hello identifier value displayed in hello error.</span></span>

<span data-ttu-id="29547-124">您已在 Azure AD 中更新 hello 識別碼的值，並透過 hello hello SAML 要求中的應用程式將與其相符 hello 的值之後，您應該能夠 toosign toohello 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="29547-124">After you have updated hello Identifier value in Azure AD and it’s matching hello value sends by hello application in hello SAML request, you should be able toosign in toohello application.</span></span>

## <a name="hello-reply-address-does-not-match-hello-reply-addresses-configured-for-hello-application"></a><span data-ttu-id="29547-125">hello 回覆地址不符 hello 回覆地址為 hello 應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="29547-125">hello reply address does not match hello reply addresses configured for hello application.</span></span> 

<span data-ttu-id="29547-126">*錯誤 AADSTS50011: hello 的回覆地址 'https://contoso.com' 不符合為 hello 應用程式設定的 hello 回覆位址*</span><span class="sxs-lookup"><span data-stu-id="29547-126">*Error AADSTS50011: hello reply address ‘https://contoso.com’ does not match hello reply addresses configured for hello application*</span></span> 

<span data-ttu-id="29547-127">**可能的原因**</span><span class="sxs-lookup"><span data-stu-id="29547-127">**Possible cause**</span></span> 

<span data-ttu-id="29547-128">hello AssertionConsumerServiceURL hello SAML 要求中的值不符合 hello 回覆 URL 的值或在 Azure AD 中設定的模式。</span><span class="sxs-lookup"><span data-stu-id="29547-128">hello AssertionConsumerServiceURL value in hello SAML request doesn't match hello Reply URL value or pattern configured in Azure AD.</span></span> <span data-ttu-id="29547-129">hello AssertionConsumerServiceURL hello SAML 要求中的值是您在 hello 錯誤中看到的 hello URL。</span><span class="sxs-lookup"><span data-stu-id="29547-129">hello AssertionConsumerServiceURL value in hello SAML request is hello URL you see in hello error.</span></span> 

<span data-ttu-id="29547-130">**解決方案**</span><span class="sxs-lookup"><span data-stu-id="29547-130">**Resolution**</span></span> 

<span data-ttu-id="29547-131">請確定它的比對 hello 回覆 URL 值設定在 Azure AD 中的 hello SAML 要求中的 hello AssertionConsumerServiceURL 值。</span><span class="sxs-lookup"><span data-stu-id="29547-131">Ensure that hello AssertionConsumerServiceURL value in hello SAML request it's matching hello Reply URL value configured in Azure AD.</span></span> 
 
1.  <span data-ttu-id="29547-132">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="29547-132">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span> 

2.  <span data-ttu-id="29547-133">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="29547-133">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span> 

3.  <span data-ttu-id="29547-134">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="29547-134">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span> 

4.  <span data-ttu-id="29547-135">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="29547-135">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span> 

5.  <span data-ttu-id="29547-136">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="29547-136">click **All Applications** tooview a list of all your applications.</span></span> 

  * <span data-ttu-id="29547-137">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="29547-137">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and       set hello **Show** option too**All Applications.**</span></span>
  
6.  <span data-ttu-id="29547-138">選取您想 tooconfigure 單一登入的 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="29547-138">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="29547-139">一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="29547-139">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="29547-140">跳過**網域和 Url** > 一節。</span><span class="sxs-lookup"><span data-stu-id="29547-140">Go too**Domain and URLs** section.</span></span> <span data-ttu-id="29547-141">驗證或更新 hello 回覆 URL 文字方塊 toomatch hello AssertionConsumerServiceURL hello SAML 要求中的值中的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="29547-141">Verify or update hello value in hello Reply URL textbox toomatch hello AssertionConsumerServiceURL value in hello SAML request.</span></span>

  * <span data-ttu-id="29547-142">如果您沒有看到 hello 回覆 URL 文字方塊中，選取 hello**顯示進階的 URL 設定**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="29547-142">If you don't see hello Reply URL textbox, select hello **Show advanced URL settings** checkbox.</span></span> 

<span data-ttu-id="29547-143">您已在 Azure AD 中更新 hello 回覆 URL 值，以及它有之後符合 hello 值 hello 應用程式以傳送 hello SAML 要求，您應該能夠 toosign toohello 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="29547-143">After you have updated hello Reply URL value in Azure AD and it’s matching hello value sends by hello application in hello SAML request, you should be able toosign in toohello application.</span></span>

## <a name="user-not-assigned-a-role"></a><span data-ttu-id="29547-144">使用者未指派角色</span><span class="sxs-lookup"><span data-stu-id="29547-144">User not assigned a role</span></span>

<span data-ttu-id="29547-145">*錯誤 AADSTS50105: hello 登入的使用者 'brian@contoso.com' 未指派 tooa hello 應用程式角色*</span><span class="sxs-lookup"><span data-stu-id="29547-145">*Error AADSTS50105: hello signed in user 'brian@contoso.com' is not assigned tooa role for hello application*</span></span>

<span data-ttu-id="29547-146">**可能的原因**</span><span class="sxs-lookup"><span data-stu-id="29547-146">**Possible cause**</span></span>

<span data-ttu-id="29547-147">hello 使用者未被授與存取 toohello 應用程式在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="29547-147">hello user has not been granted access toohello application in Azure AD.</span></span>

<span data-ttu-id="29547-148">**解決方案**</span><span class="sxs-lookup"><span data-stu-id="29547-148">**Resolution**</span></span>

<span data-ttu-id="29547-149">tooassign 一或多個使用者 tooan 應用程式直接管理，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="29547-149">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="29547-150">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="29547-150">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="29547-151">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="29547-151">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="29547-152">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="29547-152">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="29547-153">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="29547-153">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="29547-154">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="29547-154">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="29547-155">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="29547-155">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="29547-156">選取您想要使用者 toofrom hello 清單 tooassign hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="29547-156">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="29547-157">一旦 hello 應用程式載入時，按一下 **使用者和群組**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="29547-157">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="29547-158">按一下 hello**新增**hello 頂端的按鈕**使用者和群組**清單 tooopen hello**將作業加入**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="29547-158">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="29547-159">按一下 hello**使用者和群組**選取器從 hello**將作業加入**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="29547-159">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="29547-160">Hello 中的型別**全名**或**電子郵件地址**hello 使用者您感興趣指派到 hello 的**依名稱或電子郵件地址搜尋**搜尋 方塊。</span><span class="sxs-lookup"><span data-stu-id="29547-160">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="29547-161">將滑鼠停留在 hello**使用者**在 hello 清單 tooreveal**核取方塊**。</span><span class="sxs-lookup"><span data-stu-id="29547-161">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="29547-162">按一下 [hello] 核取方塊下一步 toohello 使用者的設定檔的相片或標誌 tooadd 使用者 toohello**選取**清單。</span><span class="sxs-lookup"><span data-stu-id="29547-162">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="29547-163">**選擇性：**如果您希望太**新增多個使用者**，在另一個類型**全名**或**電子郵件地址**到 hello**依名稱搜尋電子郵件地址或**搜尋 方塊中，然後按一下 hello 核取方塊 tooadd 這個使用者 toohello**選取**清單。</span><span class="sxs-lookup"><span data-stu-id="29547-163">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="29547-164">當您完成選取的使用者，請按一下 hello**選取**按鈕 tooadd 它們的使用者和群組 toobe toohello 清單指派 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="29547-164">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="29547-165">**選擇性：**按一下 hello**選取角色**hello 中的選取器**將作業加入**刀鋒視窗 tooselect 角色 tooassign toohello 使用者已選取。</span><span class="sxs-lookup"><span data-stu-id="29547-165">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="29547-166">按一下 hello**指派**按鈕 tooassign hello 應用程式 toohello 選取的使用者。</span><span class="sxs-lookup"><span data-stu-id="29547-166">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="29547-167">一段短時間，您已選取的 hello 使用者是使用這些應用程式 hello hello 方案描述 部分中所述的方法可以 toolaunch。</span><span class="sxs-lookup"><span data-stu-id="29547-167">After a short period of time, hello users you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span>

## <a name="not-a-valid-saml-request"></a><span data-ttu-id="29547-168">非有效的 SAML 要求</span><span class="sxs-lookup"><span data-stu-id="29547-168">Not a valid SAML Request</span></span>

<span data-ttu-id="29547-169">*錯誤 AADSTS75005: hello 要求不是有效的 Saml2 通訊協定訊息。*</span><span class="sxs-lookup"><span data-stu-id="29547-169">*Error AADSTS75005: hello request is not a valid Saml2 protocol message.*</span></span>

<span data-ttu-id="29547-170">**可能的原因**</span><span class="sxs-lookup"><span data-stu-id="29547-170">**Possible cause**</span></span>

<span data-ttu-id="29547-171">Azure AD 不支援 SAML 要求 hello 進行單一登入的應用程式所傳送的 hello。</span><span class="sxs-lookup"><span data-stu-id="29547-171">Azure AD doesn’t support hello SAML Request sent by hello application for Single Sign-on.</span></span> <span data-ttu-id="29547-172">以下為一些常見問題：</span><span class="sxs-lookup"><span data-stu-id="29547-172">Some common issues are:</span></span>

-   <span data-ttu-id="29547-173">遺漏 hello SAML 要求中的必要的欄位</span><span class="sxs-lookup"><span data-stu-id="29547-173">Missing required fields in hello SAML request</span></span>

-   <span data-ttu-id="29547-174">SAML 要求編碼方法</span><span class="sxs-lookup"><span data-stu-id="29547-174">SAML request encoded method</span></span>

<span data-ttu-id="29547-175">**解決方案**</span><span class="sxs-lookup"><span data-stu-id="29547-175">**Resolution**</span></span>

1.  <span data-ttu-id="29547-176">擷取 SAML 要求。</span><span class="sxs-lookup"><span data-stu-id="29547-176">Capture SAML request.</span></span> <span data-ttu-id="29547-177">依照 hello 教學課程[如何 toodebug SAML 型單一登入 tooapplications 在 Azure AD 中](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging)toolearn toocapture hello SAML 要求的方式。</span><span class="sxs-lookup"><span data-stu-id="29547-177">follow hello tutorial on [how toodebug SAML-based single sign-on tooapplications in Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) toolearn how toocapture hello SAML request.</span></span>

2.  <span data-ttu-id="29547-178">請連絡 hello 應用程式廠商及共用：</span><span class="sxs-lookup"><span data-stu-id="29547-178">Contact hello application vendor and share:</span></span>

    -   <span data-ttu-id="29547-179">SAML 要求</span><span class="sxs-lookup"><span data-stu-id="29547-179">SAML request</span></span>

    -   [<span data-ttu-id="29547-180">Azure AD 單一登入 SAML 通訊協定需求</span><span class="sxs-lookup"><span data-stu-id="29547-180">Azure AD Single Sign-on SAML protocol requirements</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)

<span data-ttu-id="29547-181">它們應該先驗證它們的單一登入支援 hello Azure AD SAML 實作。</span><span class="sxs-lookup"><span data-stu-id="29547-181">They should validate they support hello Azure AD SAML implementation for Single Sign-on.</span></span>

## <a name="no-resource-in-requiredresourceaccess-list"></a><span data-ttu-id="29547-182">requiredResourceAccess 清單中沒有資源</span><span class="sxs-lookup"><span data-stu-id="29547-182">No resource in requiredResourceAccess list</span></span>

<span data-ttu-id="29547-183">*錯誤 AADSTS65005: hello 用戶端應用程式已要求存取 tooresource ' 00000002-0000-0000-c000-000000000000'。此要求失敗，因為 hello 用戶端在其 requiredResourceAccess 清單中未指定此資源*。</span><span class="sxs-lookup"><span data-stu-id="29547-183">*Error AADSTS65005: hello client application has requested access tooresource '00000002-0000-0000-c000-000000000000'. This request has failed because hello client has not specified this resource in its requiredResourceAccess list*.</span></span>

<span data-ttu-id="29547-184">**可能的原因**</span><span class="sxs-lookup"><span data-stu-id="29547-184">**Possible cause**</span></span>

<span data-ttu-id="29547-185">hello 應用程式物件已損毀。</span><span class="sxs-lookup"><span data-stu-id="29547-185">hello application object is corrupted.</span></span>

<span data-ttu-id="29547-186">**解決方案**</span><span class="sxs-lookup"><span data-stu-id="29547-186">**Resolution**</span></span>

<span data-ttu-id="29547-187">toosolve hello 問題，請從 hello 目錄移除 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="29547-187">toosolve hello problem, remove hello application from hello directory.</span></span> <span data-ttu-id="29547-188">接著，新增和重新設定 hello 應用程式，請遵循 hello 執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="29547-188">Then, add and reconfigure hello application, follow hello steps below:</span></span>

1.  <span data-ttu-id="29547-189">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="29547-189">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="29547-190">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="29547-190">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="29547-191">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="29547-191">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="29547-192">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="29547-192">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="29547-193">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="29547-193">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="29547-194">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="29547-194">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="29547-195">選取您想 tooconfigure 單一登入的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="29547-195">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="29547-196">按一下**刪除**hello 左上方的 hello 應用程式在**概觀**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="29547-196">Click **Delete** at hello top-left of hello application **Overview** blade.</span></span>

8.  <span data-ttu-id="29547-197">重新整理 Azure AD，並從 hello Azure AD 圖庫新增 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="29547-197">Refresh Azure AD and Add hello application from hello Azure AD gallery.</span></span> <span data-ttu-id="29547-198">然後，設定一次 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="29547-198">Then, Configure hello application again.</span></span>

<span data-ttu-id="29547-199">之後重新設定 hello 應用程式，您應該能夠 toosign toohello 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="29547-199">After reconfiguring hello application, you should be able toosign in toohello application.</span></span>

## <a name="certificate-or-key-not-configured"></a><span data-ttu-id="29547-200">未設定憑證或金鑰</span><span class="sxs-lookup"><span data-stu-id="29547-200">Certificate or key not configured</span></span>

<span data-ttu-id="29547-201">錯誤 AADSTS50003︰未設定簽署金鑰。</span><span class="sxs-lookup"><span data-stu-id="29547-201">Error AADSTS50003: No signing key configured.</span></span>

<span data-ttu-id="29547-202">**可能的原因**</span><span class="sxs-lookup"><span data-stu-id="29547-202">**Possible cause**</span></span>

<span data-ttu-id="29547-203">hello 應用程式物件已損毀，且 Azure AD 無法辨識 hello hello 應用程式設定的憑證。</span><span class="sxs-lookup"><span data-stu-id="29547-203">hello application object is corrupted and Azure AD doesn’t recognize hello certificate configured for hello application.</span></span>

<span data-ttu-id="29547-204">**解決方案**</span><span class="sxs-lookup"><span data-stu-id="29547-204">**Resolution**</span></span>

<span data-ttu-id="29547-205">toodelete 並建立新的憑證，請依照下列步驟執行 hello:</span><span class="sxs-lookup"><span data-stu-id="29547-205">toodelete and create a new certificate, follow hello steps below:</span></span>

1.  <span data-ttu-id="29547-206">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="29547-206">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="29547-207">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="29547-207">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="29547-208">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="29547-208">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="29547-209">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="29547-209">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="29547-210">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="29547-210">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="29547-211">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="29547-211">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="29547-212">選取您想 tooconfigure 單一登入的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="29547-212">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="29547-213">一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="29547-213">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="29547-214">按一下**建立新憑證**下 hello **SAML 簽章憑證**> 一節。</span><span class="sxs-lookup"><span data-stu-id="29547-214">click **Create new certificate** under hello **SAML signing Certificate** section.</span></span>

9.  <span data-ttu-id="29547-215">選取到期日。</span><span class="sxs-lookup"><span data-stu-id="29547-215">Select Expiration date.</span></span> <span data-ttu-id="29547-216">然後按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="29547-216">Then, click **Save.**</span></span>

10. <span data-ttu-id="29547-217">請檢查**啟用新的憑證**toooverride hello 作用中憑證。</span><span class="sxs-lookup"><span data-stu-id="29547-217">Check **Make new certificate active** toooverride hello active certificate.</span></span> <span data-ttu-id="29547-218">然後，按一下 **儲存**在 hello hello 刀鋒視窗頂端，並接受 tooactivate hello 變換憑證。</span><span class="sxs-lookup"><span data-stu-id="29547-218">Then, click **Save** at hello top of hello blade and accept tooactivate hello rollover certificate.</span></span>

11. <span data-ttu-id="29547-219">在 hello **SAML 簽章憑證**區段中，按一下**移除**tooremove hello**未使用**憑證。</span><span class="sxs-lookup"><span data-stu-id="29547-219">Under hello **SAML Signing Certificate** section, click **remove** tooremove hello **Unused** certificate.</span></span>

## <a name="problem-when-customizing-hello-saml-claims-sent-tooan-application"></a><span data-ttu-id="29547-220">自訂 hello SAML 宣告時的問題傳送 tooan 應用程式</span><span class="sxs-lookup"><span data-stu-id="29547-220">Problem when customizing hello SAML claims sent tooan application</span></span>

<span data-ttu-id="29547-221">toolearn 如何 toocustomize hello SAML 屬性宣告傳送 tooyour 應用程式，請參閱[宣告 Azure Active Directory 中的對應](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="29547-221">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="29547-222">後續步驟</span><span class="sxs-lookup"><span data-stu-id="29547-222">Next steps</span></span>
[<span data-ttu-id="29547-223">Azure AD 單一登入 SAML 通訊協定需求</span><span class="sxs-lookup"><span data-stu-id="29547-223">Azure AD Single Sign-on SAML protocol requirements</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)
