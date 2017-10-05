---
title: "登入針對同盟單一登入設定之資源庫應用程式的問題 | Microsoft Docs"
description: "當登入您已使用 Azure AD 針對 SAML 型同盟單一登入設定之應用程式時所發生特定錯誤的指引"
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
ms.openlocfilehash: 0fc5a8eb3d033d60bf6082d61bf1698924ab91c6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-a-gallery-application-configured-for-federated-single-sign-on"></a><span data-ttu-id="f1109-103">登入針對同盟單一登入設定之資源庫應用程式的問題</span><span class="sxs-lookup"><span data-stu-id="f1109-103">Problems signing in to a gallery application configured for federated single sign-on</span></span>

<span data-ttu-id="f1109-104">若要疑難排解您的問題，您必須在 Azure AD 中驗證應用程式組態，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f1109-104">To troubleshoot your problem, you need to verify the application configuration in Azure AD as follow:</span></span>

-   <span data-ttu-id="f1109-105">您已遵循 Azure AD 資源庫應用程式的所有設定步驟。</span><span class="sxs-lookup"><span data-stu-id="f1109-105">You have followed all the configuration steps for the Azure AD gallery application.</span></span>

-   <span data-ttu-id="f1109-106">在 AAD 中設定的識別碼與回覆 URL 符合其在應用程式中的預期值</span><span class="sxs-lookup"><span data-stu-id="f1109-106">The Identifier and Reply URL configured in AAD match they expected values in the application</span></span>

-   <span data-ttu-id="f1109-107">您已將使用者指派至應用程式</span><span class="sxs-lookup"><span data-stu-id="f1109-107">You have assigned users to the application</span></span>

## <a name="application-not-found-in-directory"></a><span data-ttu-id="f1109-108">在目錄中找不到應用程式</span><span class="sxs-lookup"><span data-stu-id="f1109-108">Application not found in directory</span></span>

<span data-ttu-id="f1109-109">*錯誤 AADSTS70001：目錄中找不到識別碼為 ‘https://contoso.com’ 的應用程式*。</span><span class="sxs-lookup"><span data-stu-id="f1109-109">*Error AADSTS70001: Application with Identifier ‘https://contoso.com’ was not found in the directory*.</span></span>

<span data-ttu-id="f1109-110">**可能的原因**</span><span class="sxs-lookup"><span data-stu-id="f1109-110">**Possible cause**</span></span>

<span data-ttu-id="f1109-111">以 SAML 要求從應用程式傳送到 Azure AD 的簽發者要求屬性，不符合應用程式 Azure AD 中所設定的識別碼值。</span><span class="sxs-lookup"><span data-stu-id="f1109-111">The Issuer attribute sends from the application to Azure AD in the SAML request doesn’t match the Identifier value configured in the application Azure AD.</span></span>

<span data-ttu-id="f1109-112">**解決方案**</span><span class="sxs-lookup"><span data-stu-id="f1109-112">**Resolution**</span></span>

<span data-ttu-id="f1109-113">確保 SAML 要求中的簽發者屬性符合 Azure AD 中設定的識別碼值：</span><span class="sxs-lookup"><span data-stu-id="f1109-113">Ensure that the Issuer attribute in the SAML request it’s matching the Identifier value configured in Azure AD:</span></span>

1.  <span data-ttu-id="f1109-114">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="f1109-114">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="f1109-115">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="f1109-115">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f1109-116">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="f1109-116">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f1109-117">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f1109-117">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="f1109-118">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="f1109-118">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="f1109-119">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f1109-119">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="f1109-120">選取您要設定單一登入的應用程式</span><span class="sxs-lookup"><span data-stu-id="f1109-120">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="f1109-121">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="f1109-121">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="f1109-122">移至 [網域及 URL] 區段。</span><span class="sxs-lookup"><span data-stu-id="f1109-122">Go to **Domain and URLs** section.</span></span> <span data-ttu-id="f1109-123">確認 [識別碼] 文字方塊中的值符合錯誤中所顯示的識別碼值。</span><span class="sxs-lookup"><span data-stu-id="f1109-123">Verify that the value in the Identifier textbox is matching the value for the identifier value displayed in the error.</span></span>

<span data-ttu-id="f1109-124">您已在 Azure AD 中更新識別碼值，且該值符合應用程式以 SAML 要求傳送的值後，您應該能夠登入應用程式。</span><span class="sxs-lookup"><span data-stu-id="f1109-124">After you have updated the Identifier value in Azure AD and it’s matching the value sends by the application in the SAML request, you should be able to sign in to the application.</span></span>

## <a name="the-reply-address-does-not-match-the-reply-addresses-configured-for-the-application"></a><span data-ttu-id="f1109-125">回覆位址不符合為應用程式設定的回覆位址。</span><span class="sxs-lookup"><span data-stu-id="f1109-125">The reply address does not match the reply addresses configured for the application.</span></span>

<span data-ttu-id="f1109-126">*Error AADSTS50011：回覆位址 ‘https://contoso.com’ 不符合為應用程式設定的回覆位址*</span><span class="sxs-lookup"><span data-stu-id="f1109-126">*Error AADSTS50011: The reply address ‘https://contoso.com’ does not match the reply addresses configured for the application*</span></span>

<span data-ttu-id="f1109-127">**可能的原因**</span><span class="sxs-lookup"><span data-stu-id="f1109-127">**Possible cause**</span></span>

<span data-ttu-id="f1109-128">SAML 要求中的 AssertionConsumerServiceURL 值不符合在 Azure AD 中設定的 [回覆 URL] 值或模式。</span><span class="sxs-lookup"><span data-stu-id="f1109-128">The AssertionConsumerServiceURL value in the SAML request doesn't match the Reply URL value or pattern configured in Azure AD.</span></span> <span data-ttu-id="f1109-129">SAML 要求中的 AssertionConsumerServiceURL 值是您在錯誤中看到的 URL。</span><span class="sxs-lookup"><span data-stu-id="f1109-129">The AssertionConsumerServiceURL value in the SAML request is the URL you see in the error.</span></span>

<span data-ttu-id="f1109-130">**解決方案**</span><span class="sxs-lookup"><span data-stu-id="f1109-130">**Resolution**</span></span>

<span data-ttu-id="f1109-131">確保 SAML 要求中的 AssertionConsumerServiceURL 值符合在 Azure AD 中設定的 [回覆 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="f1109-131">Ensure that the AssertionConsumerServiceURL value in the SAML request it's matching the Reply URL value configured in Azure AD.</span></span>

1.  <span data-ttu-id="f1109-132">開啟 [Azure 入口網站](https://portal.azure.com/)，以**全域管理員**或 **共同管理員**身分登入</span><span class="sxs-lookup"><span data-stu-id="f1109-132">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="f1109-133">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="f1109-133">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f1109-134">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="f1109-134">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f1109-135">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f1109-135">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="f1109-136">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="f1109-136">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="f1109-137">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f1109-137">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="f1109-138">選取您要設定單一登入的應用程式</span><span class="sxs-lookup"><span data-stu-id="f1109-138">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="f1109-139">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="f1109-139">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="f1109-140">移至 [網域及 URL] 區段。</span><span class="sxs-lookup"><span data-stu-id="f1109-140">Go to **Domain and URLs** section.</span></span> <span data-ttu-id="f1109-141">驗證或更新 [回覆 URL] 文字方塊中的值，以符合 SAML 要求中的 AssertionConsumerServiceURL 值。</span><span class="sxs-lookup"><span data-stu-id="f1109-141">Verify or update the value in the Reply URL textbox to match the AssertionConsumerServiceURL value in the SAML request.</span></span>  
    * <span data-ttu-id="f1109-142">如果沒有看到 [回覆 URL] 文字方塊中，請選取 [顯示進階 URL 設定] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="f1109-142">If you don't see the Reply URL textbox, select the **Show advanced URL settings** checkbox.</span></span>

<span data-ttu-id="f1109-143">您已在 Azure AD 中更新 [回覆 URL] 值，且該值符合應用程式以 SAML 要求傳送的值後，您應該能夠登入應用程式。</span><span class="sxs-lookup"><span data-stu-id="f1109-143">After you have updated the Reply URL value in Azure AD and it’s matching the value sends by the application in the SAML request, you should be able to sign in to the application.</span></span>

## <a name="user-not-assigned-a-role"></a><span data-ttu-id="f1109-144">使用者未指派角色</span><span class="sxs-lookup"><span data-stu-id="f1109-144">User not assigned a role</span></span>

<span data-ttu-id="f1109-145">*錯誤 AADSTS50105：未將已登入的使用者 'brian@contoso.com' 指派至應用程式的角色*。</span><span class="sxs-lookup"><span data-stu-id="f1109-145">*Error AADSTS50105: The signed in user 'brian@contoso.com' is not assigned to a role for the application*.</span></span>

<span data-ttu-id="f1109-146">**可能的原因**</span><span class="sxs-lookup"><span data-stu-id="f1109-146">**Possible cause**</span></span>

<span data-ttu-id="f1109-147">尚未將 Azure AD 中應用程式的存取權授與使用者。</span><span class="sxs-lookup"><span data-stu-id="f1109-147">The user has not been granted access to the application in Azure AD.</span></span>

<span data-ttu-id="f1109-148">**解決方案**</span><span class="sxs-lookup"><span data-stu-id="f1109-148">**Resolution**</span></span>

<span data-ttu-id="f1109-149">若要直接將一或多個使用者指派至應用程式，請依照下列步驟執行︰</span><span class="sxs-lookup"><span data-stu-id="f1109-149">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="f1109-150">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="f1109-150">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="f1109-151">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="f1109-151">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f1109-152">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="f1109-152">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f1109-153">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f1109-153">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="f1109-154">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="f1109-154">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="f1109-155">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f1109-155">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="f1109-156">從清單中選取您想要指派使用者的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f1109-156">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="f1109-157">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="f1109-157">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="f1109-158">按一下 [使用者和群組] 清單頂端的 [新增] 按鈕，以開啟 [新增指派] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="f1109-158">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="f1109-159">從 [新增指派] 刀鋒視窗按一下 [使用者和群組] 選取器。</span><span class="sxs-lookup"><span data-stu-id="f1109-159">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="f1109-160">在 [依姓名或電子郵件地址搜尋] 搜尋方塊中，輸入您有興趣指派之使用者的**全名**或**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="f1109-160">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="f1109-161">將滑鼠停留在清單中的**使用者**上方，以顯示**核取方塊**。</span><span class="sxs-lookup"><span data-stu-id="f1109-161">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="f1109-162">按一下使用者設定檔照片或標誌旁邊的核取方塊，將使用者新增至 [已選取] 清單。</span><span class="sxs-lookup"><span data-stu-id="f1109-162">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="f1109-163">**選擇性︰**如果您想要**新增多位使用者**，請在 [依姓名或電子郵件地址搜尋] 搜尋方塊中，輸入另一個**全名**或**電子郵件地址**，然後按一下核取方塊，將此使用者新增至 [已選取] 清單。</span><span class="sxs-lookup"><span data-stu-id="f1109-163">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="f1109-164">當您完成選取使用者時，按一下 [選取] 按鈕，將他們新增到要指派至應用程式的使用者和群組清單。</span><span class="sxs-lookup"><span data-stu-id="f1109-164">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="f1109-165">**選擇性︰**按一下 [新增指派] 刀鋒視窗中的 [選取角色] 選取器，以選取要指派給您已選取使用者的角色。</span><span class="sxs-lookup"><span data-stu-id="f1109-165">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="f1109-166">按一下 [指派] 按鈕，將應用程式指派給選取的使用者。</span><span class="sxs-lookup"><span data-stu-id="f1109-166">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="f1109-167">稍待片刻，您已選取的使用者就能夠使用解決方案描述一節所述的方法，啟動這些應用程式。</span><span class="sxs-lookup"><span data-stu-id="f1109-167">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span></span>

## <a name="not-a-valid-saml-request"></a><span data-ttu-id="f1109-168">非有效的 SAML 要求</span><span class="sxs-lookup"><span data-stu-id="f1109-168">Not a valid SAML Request</span></span>

<span data-ttu-id="f1109-169">*錯誤 AADSTS75005：要求不是有效的 Saml2 通訊協定訊息。*</span><span class="sxs-lookup"><span data-stu-id="f1109-169">*Error AADSTS75005: The request is not a valid Saml2 protocol message.*</span></span>

<span data-ttu-id="f1109-170">**可能的原因**</span><span class="sxs-lookup"><span data-stu-id="f1109-170">**Possible cause**</span></span>

<span data-ttu-id="f1109-171">Azure AD 不支援應用程式為單一登入傳送的 SAML 要求。</span><span class="sxs-lookup"><span data-stu-id="f1109-171">Azure AD doesn’t support the SAML Request sent by the application for Single Sign-on.</span></span> <span data-ttu-id="f1109-172">以下為一些常見問題：</span><span class="sxs-lookup"><span data-stu-id="f1109-172">Some common issues are:</span></span>

-   <span data-ttu-id="f1109-173">SAML 要求中遺漏必要的欄位</span><span class="sxs-lookup"><span data-stu-id="f1109-173">Missing required fields in the SAML request</span></span>

-   <span data-ttu-id="f1109-174">SAML 要求編碼方法</span><span class="sxs-lookup"><span data-stu-id="f1109-174">SAML request encoded method</span></span>

<span data-ttu-id="f1109-175">**解決方案**</span><span class="sxs-lookup"><span data-stu-id="f1109-175">**Resolution**</span></span>

1.  <span data-ttu-id="f1109-176">擷取 SAML 要求。</span><span class="sxs-lookup"><span data-stu-id="f1109-176">Capture SAML request.</span></span> <span data-ttu-id="f1109-177">依照[如何偵錯 SAML 型單一登入 Azure Active Directory 中的應用程式](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging)教學課程學習如何擷取 SAML 要求。</span><span class="sxs-lookup"><span data-stu-id="f1109-177">follow the tutorial [How to debug SAML-based single sign-on to applications in Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) to learn how to capture the SAML request.</span></span>

2.  <span data-ttu-id="f1109-178">請連絡應用程式廠商並告知︰</span><span class="sxs-lookup"><span data-stu-id="f1109-178">Contact the application vendor and share:</span></span>

   -   <span data-ttu-id="f1109-179">SAML 要求</span><span class="sxs-lookup"><span data-stu-id="f1109-179">SAML request</span></span>

   -   [<span data-ttu-id="f1109-180">Azure AD 單一登入 SAML 通訊協定需求</span><span class="sxs-lookup"><span data-stu-id="f1109-180">Azure AD Single Sign-on SAML protocol requirements</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)

<span data-ttu-id="f1109-181">廠商應確認其支援單一登入的 AD SAML 實作。</span><span class="sxs-lookup"><span data-stu-id="f1109-181">They should validate they support the Azure AD SAML implementation for Single Sign-on.</span></span>

## <a name="no-resource-in-requiredresourceaccess-list"></a><span data-ttu-id="f1109-182">requiredResourceAccess 清單中沒有資源</span><span class="sxs-lookup"><span data-stu-id="f1109-182">No resource in requiredResourceAccess list</span></span>

<span data-ttu-id="f1109-183">*錯誤 AADSTS65005：用戶端應用程式已要求存取資源 '00000002-0000-0000-c000-000000000000'。此要求失敗，因為用戶端尚未在其 requiredResourceAccess 清單中指定此資源*。</span><span class="sxs-lookup"><span data-stu-id="f1109-183">*Error AADSTS65005:The client application has requested access to resource '00000002-0000-0000-c000-000000000000'. This request has failed because the client has not specified this resource in its requiredResourceAccess list*.</span></span>

<span data-ttu-id="f1109-184">**可能的原因**</span><span class="sxs-lookup"><span data-stu-id="f1109-184">**Possible cause**</span></span>

<span data-ttu-id="f1109-185">應用程式物件已損毀。</span><span class="sxs-lookup"><span data-stu-id="f1109-185">The application object is corrupted.</span></span>

<span data-ttu-id="f1109-186">**解決方式：選項 1**</span><span class="sxs-lookup"><span data-stu-id="f1109-186">**Resolution: option 1**</span></span>

<span data-ttu-id="f1109-187">若要解決此問題，請在 Azure AD 組態新增唯一的 [識別碼] 值。</span><span class="sxs-lookup"><span data-stu-id="f1109-187">To solve the problem, add the unique Identifier value in the Azure AD configuration.</span></span> <span data-ttu-id="f1109-188">若要新增 [識別碼] 值，請依照下列步驟執行︰</span><span class="sxs-lookup"><span data-stu-id="f1109-188">To add a Identifier value, follow the steps below:</span></span>

1.  <span data-ttu-id="f1109-189">開啟 [Azure 入口網站](https://portal.azure.com/)，以**全域管理員**或 **共同管理員**身分登入</span><span class="sxs-lookup"><span data-stu-id="f1109-189">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="f1109-190">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="f1109-190">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f1109-191">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="f1109-191">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f1109-192">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f1109-192">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="f1109-193">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="f1109-193">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="f1109-194">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f1109-194">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="f1109-195">選取您已設定單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f1109-195">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="f1109-196">應用程式載入之後，按一下應用程式左邊導覽功能表中的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="f1109-196">Once the application loads, click on the **Single sign-on** from the application’s left hand navigation menu</span></span>

8.  <span data-ttu-id="f1109-197">在 [網域和 URL] 區段之下，勾選 [顯示進階 URL 設定]。</span><span class="sxs-lookup"><span data-stu-id="f1109-197">Under the **Domain and URL** section, check on the **Show advanced URL settings**.</span></span>

9.  <span data-ttu-id="f1109-198">在 [識別碼] 文字方塊中輸入應用程式的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="f1109-198">in the **Identifier** textbox type a unique identifier for the application.</span></span>

10. <span data-ttu-id="f1109-199">**儲存**組態。</span><span class="sxs-lookup"><span data-stu-id="f1109-199">**Save** the configuration.</span></span>


<span data-ttu-id="f1109-200">**解決方式：選項 2**</span><span class="sxs-lookup"><span data-stu-id="f1109-200">**Resolution option 2**</span></span>

<span data-ttu-id="f1109-201">如果上述選項 1 無效，請試著從目錄中移除應用程式。</span><span class="sxs-lookup"><span data-stu-id="f1109-201">If option 1 above did not work for you, try removing the application from the directory.</span></span> <span data-ttu-id="f1109-202">然後，依照下列步驟新增並重新設定應用程式：</span><span class="sxs-lookup"><span data-stu-id="f1109-202">Then, add and reconfigure the application, follow the steps below:</span></span>

1.  <span data-ttu-id="f1109-203">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="f1109-203">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="f1109-204">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="f1109-204">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f1109-205">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="f1109-205">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f1109-206">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f1109-206">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="f1109-207">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="f1109-207">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="f1109-208">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f1109-208">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="f1109-209">選取您要設定單一登入的應用程式</span><span class="sxs-lookup"><span data-stu-id="f1109-209">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="f1109-210">按一下應用程式 [概觀] 刀鋒視窗左上角的 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="f1109-210">Click **Delete** at the top-left of the application **Overview** blade.</span></span>

8.  <span data-ttu-id="f1109-211">重新整理 Azure AD，並從 Azure AD 資源庫新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="f1109-211">Refresh Azure AD and Add the application from the Azure AD gallery.</span></span> <span data-ttu-id="f1109-212">接著，設定應用程式</span><span class="sxs-lookup"><span data-stu-id="f1109-212">Then, Configure the application</span></span>

<span data-ttu-id="f1109-213"><span id="_Hlk477190176" class="anchor"></span>在重新設定應用程式後，您應該能夠登入應用程式。</span><span class="sxs-lookup"><span data-stu-id="f1109-213"><span id="_Hlk477190176" class="anchor"></span>After reconfiguring the application, you should be able to sign in to the application.</span></span>

## <a name="certificate-or-key-not-configured"></a><span data-ttu-id="f1109-214">未設定憑證或金鑰</span><span class="sxs-lookup"><span data-stu-id="f1109-214">Certificate or key not configured</span></span>

<span data-ttu-id="f1109-215">*錯誤 AADSTS50003︰未設定簽署金鑰。*</span><span class="sxs-lookup"><span data-stu-id="f1109-215">*Error AADSTS50003: No signing key configured.*</span></span>

<span data-ttu-id="f1109-216">**可能的原因**</span><span class="sxs-lookup"><span data-stu-id="f1109-216">**Possible cause**</span></span>

<span data-ttu-id="f1109-217">應用程式物件已損毀，Azure AD 無法辨識為應用程式設定的憑證。</span><span class="sxs-lookup"><span data-stu-id="f1109-217">The application object is corrupted and Azure AD doesn’t recognize the certificate configured for the application.</span></span>

<span data-ttu-id="f1109-218">**解決方案**</span><span class="sxs-lookup"><span data-stu-id="f1109-218">**Resolution**</span></span>

<span data-ttu-id="f1109-219">若要刪除與建立新的憑證，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="f1109-219">To delete and create a new certificate, follow the steps below:</span></span>

1.  <span data-ttu-id="f1109-220">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="f1109-220">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="f1109-221">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="f1109-221">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f1109-222">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="f1109-222">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f1109-223">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f1109-223">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="f1109-224">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="f1109-224">click **All Applications** to view a list of all your applications.</span></span>

 * <span data-ttu-id="f1109-225">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f1109-225">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="f1109-226">選取您要設定單一登入的應用程式</span><span class="sxs-lookup"><span data-stu-id="f1109-226">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="f1109-227">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="f1109-227">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="f1109-228">在 [SAML 簽署憑證] 區段下方，按一下 [建立新憑證]。</span><span class="sxs-lookup"><span data-stu-id="f1109-228">click **Create new certificate** under the **SAML signing Certificate** section.</span></span>

9.  <span data-ttu-id="f1109-229">選取到期日。</span><span class="sxs-lookup"><span data-stu-id="f1109-229">Select Expiration date.</span></span> <span data-ttu-id="f1109-230">然後按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="f1109-230">Then, click **Save.**</span></span>

10. <span data-ttu-id="f1109-231">勾選 [Make new certificate active (啟用新憑證)] 以覆寫作用中的憑證。</span><span class="sxs-lookup"><span data-stu-id="f1109-231">Check **Make new certificate active** to override the active certificate.</span></span> <span data-ttu-id="f1109-232">然後按一下刀鋒視窗頂端的 [儲存]，接受啟用變換憑證。</span><span class="sxs-lookup"><span data-stu-id="f1109-232">Then, click **Save** at the top of the blade and accept to activate the rollover certificate.</span></span>

11. <span data-ttu-id="f1109-233">在 [SAML 簽署憑證] 區段下，按一下 [移除] 以移除**未使用**的憑證。</span><span class="sxs-lookup"><span data-stu-id="f1109-233">Under the **SAML Signing Certificate** section, click **remove** to remove the **Unused** certificate.</span></span>

## <a name="problem-when-customizing-the-saml-claims-sent-to-an-application"></a><span data-ttu-id="f1109-234">自訂傳送至應用程式的 SAML 宣告時發生問題</span><span class="sxs-lookup"><span data-stu-id="f1109-234">Problem when customizing the SAML claims sent to an application</span></span>

<span data-ttu-id="f1109-235">若要了解如何自訂傳送至應用程式的 SAML 屬性宣告，請參閱 [Azure Active Directory 中的宣告對應](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping)以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f1109-235">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f1109-236">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f1109-236">Next steps</span></span>
[<span data-ttu-id="f1109-237">如何偵錯 SAML 型單一登入 Azure Active Directory 中的應用程式</span><span class="sxs-lookup"><span data-stu-id="f1109-237">How to debug SAML-based single sign-on to applications in Azure AD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging)
