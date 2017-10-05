---
title: "登入後應用程式頁面的錯誤 | Microsoft Docs"
description: "如何解決當應用程式本身發生錯誤時 Azure AD 登入方面的問題"
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
ms.openlocfilehash: a8cd93256f79ece268ec3411dfbdf590f4b24447
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="error-on-an-applications-page-after-signing-in"></a><span data-ttu-id="9b829-103">登入後應用程式頁面的錯誤</span><span class="sxs-lookup"><span data-stu-id="9b829-103">Error on an application's page after signing in</span></span>

<span data-ttu-id="9b829-104">在此案例中，Azure AD 已將使用者登入，但應用程式顯示不允許使用者成功完成登入流程的錯誤。</span><span class="sxs-lookup"><span data-stu-id="9b829-104">In this scenario, Azure AD has signed the user in, but the application is displaying an error not allowing the user to successfully finish the sign in flow.</span></span> <span data-ttu-id="9b829-105">在此案例中，應用程式不接受由 Azure AD 發出的回應。</span><span class="sxs-lookup"><span data-stu-id="9b829-105">In this scenario, the application is not accepting the response issue by Azure AD.</span></span>

<span data-ttu-id="9b829-106">有一些可能的原因會造成應用程式不接受 Azure AD 的回應。</span><span class="sxs-lookup"><span data-stu-id="9b829-106">There are some possible reasons why the application didn’t accept the response from Azure AD.</span></span> <span data-ttu-id="9b829-107">如果應用程式中的錯誤不夠清楚，無法得知回應中遺漏了什麼，則：</span><span class="sxs-lookup"><span data-stu-id="9b829-107">If the error in the application is not clear enough to know what is missing in the response, then:</span></span>

-   <span data-ttu-id="9b829-108">如果應用程式是 Azure AD 資源庫，請確認您已依照[如何偵錯 SAML 型單一登入 Azure Active Directory 中的應用程式](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging)一文中所有的步驟進行。</span><span class="sxs-lookup"><span data-stu-id="9b829-108">If the application is the Azure AD Gallery, verify you have followed all the steps in the article [How to debug SAML-based single sign-on to applications in Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).</span></span>

-   <span data-ttu-id="9b829-109">使用如 [Fiddler](http://www.telerik.com/fiddler) 等工具擷取 SAML 要求、SAML 回應和 SAML 權杖。</span><span class="sxs-lookup"><span data-stu-id="9b829-109">Use a tool like [Fiddler](http://www.telerik.com/fiddler) to capture SAML request, SAML response and SAML token.</span></span>

-   <span data-ttu-id="9b829-110">將 SAML 回應與應用程式廠商分享，以得知遺漏的項目。</span><span class="sxs-lookup"><span data-stu-id="9b829-110">Share the SAML response with the application vendor to know what is missing.</span></span>

## <a name="missing-attributes-in-the-saml-response"></a><span data-ttu-id="9b829-111">SAML 回應中遺漏屬性</span><span class="sxs-lookup"><span data-stu-id="9b829-111">Missing attributes in the SAML response</span></span>

<span data-ttu-id="9b829-112">若要在 Azure AD 組態中新增要以 Azure AD 回應傳送的屬性，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="9b829-112">To add an attribute in the Azure AD configuration to be sent in the Azure AD response, follow the steps below:</span></span>

1.  <span data-ttu-id="9b829-113">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="9b829-113">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9b829-114">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="9b829-114">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9b829-115">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="9b829-115">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9b829-116">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="9b829-116">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9b829-117">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="9b829-117">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="9b829-118">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="9b829-118">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9b829-119">選取您要設定單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="9b829-119">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="9b829-120">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="9b829-120">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9b829-121">按一下 [使用者屬性] 區段下方的 [檢視和編輯所有其他使用者屬性]，以編輯當使用者登入時要以 SAML 權杖傳送至應用程式的屬性。</span><span class="sxs-lookup"><span data-stu-id="9b829-121">click **View and edit all other user attributes under** the **User Attributes** section to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="9b829-122">若要新增屬性：</span><span class="sxs-lookup"><span data-stu-id="9b829-122">To add an attribute:</span></span>

   * <span data-ttu-id="9b829-123">按一下 [新增屬性]。</span><span class="sxs-lookup"><span data-stu-id="9b829-123">click **Add attribute**.</span></span> <span data-ttu-id="9b829-124">輸入 [名稱]，然後從下拉式清單選取 [值]。</span><span class="sxs-lookup"><span data-stu-id="9b829-124">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   * <span data-ttu-id="9b829-125">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="9b829-125">Click **Save.**</span></span> <span data-ttu-id="9b829-126">您會在資料表中看到新屬性。</span><span class="sxs-lookup"><span data-stu-id="9b829-126">You see the new attribute in the table.</span></span>

9.  <span data-ttu-id="9b829-127">儲存組態。</span><span class="sxs-lookup"><span data-stu-id="9b829-127">Save the configuration.</span></span>

<span data-ttu-id="9b829-128">下次使用者登入應用程式，Azure AD 會以 SAML 回應傳送新的屬性。</span><span class="sxs-lookup"><span data-stu-id="9b829-128">Next time the user signs in to the application, Azure AD send the new attribute in the SAML response.</span></span>

## <a name="the-application-expects-a-different-user-identifier-value-or-format"></a><span data-ttu-id="9b829-129">應用程式預期不同的使用者識別碼值或格式</span><span class="sxs-lookup"><span data-stu-id="9b829-129">The application expects a different User Identifier value or format</span></span>

<span data-ttu-id="9b829-130">登入應用程式失敗，因為 SAML 回應中遺漏如角色等屬性，或因為應用程式所預期的 EntityID 屬性格式不同。</span><span class="sxs-lookup"><span data-stu-id="9b829-130">The sign-in to the application is failing because the SAML response is missing attributes such as roles or because the application is expecting a different format for the EntityID attribute.</span></span>

## <a name="add-an-attribute-in-the-azure-ad-application-configuration"></a><span data-ttu-id="9b829-131">在 Azure AD 應用程式組態中新增屬性：</span><span class="sxs-lookup"><span data-stu-id="9b829-131">Add an attribute in the Azure AD application configuration:</span></span>

<span data-ttu-id="9b829-132">若要變更的使用者識別碼值，請依照下列步驟執行︰</span><span class="sxs-lookup"><span data-stu-id="9b829-132">To change the User Identifier value, follow the steps below:</span></span>

1.  <span data-ttu-id="9b829-133">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="9b829-133">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9b829-134">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="9b829-134">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9b829-135">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="9b829-135">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9b829-136">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="9b829-136">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9b829-137">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="9b829-137">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="9b829-138">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="9b829-138">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9b829-139">選取您要設定單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="9b829-139">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="9b829-140">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="9b829-140">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9b829-141">在 [使用者屬性] 下方，從 [使用者識別碼] 下拉式清單選取使用者的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="9b829-141">Under the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

## <a name="change-entityid-user-identifier-format"></a><span data-ttu-id="9b829-142">變更 EntityID (使用者識別碼) 格式</span><span class="sxs-lookup"><span data-stu-id="9b829-142">Change EntityID (User Identifier) format</span></span>

<span data-ttu-id="9b829-143">如果應用程式預期 EntityID 屬性為另一種格式。</span><span class="sxs-lookup"><span data-stu-id="9b829-143">If the application expects another format for the EntityID attribute.</span></span> <span data-ttu-id="9b829-144">接著，在使用者驗證之後，您將無法選取 Azure AD 要在回應中傳送至應用程式的 EntityID (使用者識別碼) 格式。</span><span class="sxs-lookup"><span data-stu-id="9b829-144">Then, you won’t be able to select the EntityID (User Identifier) format that Azure AD sends to the application in the response after user authentication.</span></span>

<span data-ttu-id="9b829-145">Azure AD 會根據由應用程式以 SAML AuthRequest 選取的值或要求的格式，來選取 NameID 屬性 (使用者識別碼) 的格式。</span><span class="sxs-lookup"><span data-stu-id="9b829-145">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="9b829-146">如需詳細資訊，請參閱 NameIDPolicy 區段下方的[單一登入 SAML 通訊協定](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest)一文。</span><span class="sxs-lookup"><span data-stu-id="9b829-146">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>

## <a name="the-application-expects-a-different-signature-method-for-the-saml-response"></a><span data-ttu-id="9b829-147">應用程式所預期的 SAML 回應簽章方法不同</span><span class="sxs-lookup"><span data-stu-id="9b829-147">The application expects a different signature method for the SAML response</span></span>

<span data-ttu-id="9b829-148">若要變更 Azure Active Directory 數位簽署 SAML 權杖的部分，</span><span class="sxs-lookup"><span data-stu-id="9b829-148">To change what parts of the SAML token are digitally signed by Azure Active Directory.</span></span> <span data-ttu-id="9b829-149">請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="9b829-149">Follow the steps below:</span></span>

1.  <span data-ttu-id="9b829-150">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="9b829-150">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9b829-151">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="9b829-151">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9b829-152">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="9b829-152">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9b829-153">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="9b829-153">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9b829-154">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="9b829-154">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="9b829-155">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="9b829-155">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9b829-156">選取您要設定單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="9b829-156">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="9b829-157">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="9b829-157">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9b829-158">按一下 [SAML 簽署憑證] 區段下方的 [Show advanced certificate signing settings (顯示進階憑證設定)]。</span><span class="sxs-lookup"><span data-stu-id="9b829-158">click **Show advanced certificate signing settings** under the **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="9b829-159">選取應用程式所預期的適當**簽署選項**：</span><span class="sxs-lookup"><span data-stu-id="9b829-159">Select the appropriate **Signing Option** expected by the application:</span></span>

  * <span data-ttu-id="9b829-160">簽署 SAML 回應</span><span class="sxs-lookup"><span data-stu-id="9b829-160">Sign SAML response</span></span>

  * <span data-ttu-id="9b829-161">簽署 SAML 回應及判斷提示</span><span class="sxs-lookup"><span data-stu-id="9b829-161">Sign SAML response and assertion</span></span>

  * <span data-ttu-id="9b829-162">簽署 SAML 判斷提示</span><span class="sxs-lookup"><span data-stu-id="9b829-162">Sign SAML assertion</span></span>

<span data-ttu-id="9b829-163">下次使用者登入應用程式，Azure AD 會簽署所選的 SAML 回應部分。</span><span class="sxs-lookup"><span data-stu-id="9b829-163">Next time the user signs in to the application, Azure AD sign the part of the SAML response selected.</span></span>

## <a name="the-application-expects-the-signing-algorithm-to-be-sha-1"></a><span data-ttu-id="9b829-164">應用程式預期的簽署演算法是 SHA-1</span><span class="sxs-lookup"><span data-stu-id="9b829-164">The application expects the signing algorithm to be SHA-1</span></span>

<span data-ttu-id="9b829-165">根據預設，Azure AD 會使用最安全的演算法簽署 SAML 權杖。</span><span class="sxs-lookup"><span data-stu-id="9b829-165">By default, Azure AD signs the SAML token using the most security algorithm.</span></span> <span data-ttu-id="9b829-166">不建議將簽署演算法變更為 SHA-1，除非應用程式需要。</span><span class="sxs-lookup"><span data-stu-id="9b829-166">Changing the sign algorithm to SHA-1 is not recommended unless required by the application.</span></span>

<span data-ttu-id="9b829-167">若要變更簽署演算法，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="9b829-167">To change the signing algorithm, follow the steps below:</span></span>

1.  <span data-ttu-id="9b829-168">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="9b829-168">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9b829-169">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="9b829-169">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9b829-170">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="9b829-170">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9b829-171">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="9b829-171">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9b829-172">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="9b829-172">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="9b829-173">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="9b829-173">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9b829-174">選取您要設定單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="9b829-174">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="9b829-175">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="9b829-175">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9b829-176">按一下 [SAML 簽署憑證] 區段下方的 [Show advanced certificate signing settings (顯示進階憑證設定)]。</span><span class="sxs-lookup"><span data-stu-id="9b829-176">click **Show advanced certificate signing settings** under the **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="9b829-177">在 [簽署演算法] 中選取 [SHA-1]。</span><span class="sxs-lookup"><span data-stu-id="9b829-177">Select SHA-1, in the **Signing Algorithm**.</span></span>

<span data-ttu-id="9b829-178">下次使用者登入應用程式，Azure AD 會使用 SHA-1 演算法簽署 SAML 權杖。</span><span class="sxs-lookup"><span data-stu-id="9b829-178">Next time the user signs in to the application, Azure AD sign the SAML token using SHA-1 algorithm.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b829-179">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9b829-179">Next steps</span></span>
[<span data-ttu-id="9b829-180">如何偵錯 SAML 型單一登入 Azure Active Directory 中的應用程式</span><span class="sxs-lookup"><span data-stu-id="9b829-180">How to debug SAML-based single sign-on to applications in Azure Active Directory</span></span>](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging)
