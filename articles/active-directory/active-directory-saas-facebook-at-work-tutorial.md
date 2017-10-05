---
title: "教學課程：Azure Active Directory 與 Workplace by Facebook 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Workplace by Facebook 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: jeedes
ms.openlocfilehash: 27e62a00832484667117d8718db9f2fc05e2f4e2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a><span data-ttu-id="4b27b-103">教學課程：Azure Active Directory 與 Workplace by Facebook 整合</span><span class="sxs-lookup"><span data-stu-id="4b27b-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span></span>

<span data-ttu-id="4b27b-104">在本教學課程中，您會了解如何將 Workplace by Facebook 與 Azure Active Directory (Azure AD) 整合。</span><span class="sxs-lookup"><span data-stu-id="4b27b-104">In this tutorial, you learn how to integrate Workplace by Facebook with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4b27b-105">將 Workplace by Facebook 與 Azure AD 整合可提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="4b27b-105">Integrating Workplace by Facebook with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4b27b-106">您可以在 Azure AD 中控制可存取 Workplace by Facebook 的人員。</span><span class="sxs-lookup"><span data-stu-id="4b27b-106">You can control in Azure AD who has access to Workplace by Facebook.</span></span>
- <span data-ttu-id="4b27b-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Workplace by Facebook (單一登入)。</span><span class="sxs-lookup"><span data-stu-id="4b27b-107">You can enable your users to automatically get signed on to Workplace by Facebook (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="4b27b-108">您可以集中管理您的帳戶：Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="4b27b-108">You can manage your accounts in one central location: the Azure portal.</span></span>

<span data-ttu-id="4b27b-109">如需軟體即服務 (SaaS) 應用程式與 Azure AD 整合的更多詳細資訊，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="4b27b-109">For more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b27b-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="4b27b-110">Prerequisites</span></span>

<span data-ttu-id="4b27b-111">若要設定 Azure AD 與 Workplace by Facebook 的整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="4b27b-111">To configure Azure AD integration with Workplace by Facebook, you need the following items:</span></span>

- <span data-ttu-id="4b27b-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="4b27b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4b27b-113">已啟用 Workplace by Facebook (SSO) 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="4b27b-113">A Workplace by Facebook single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="4b27b-114">若要測試本教學課程中的步驟，請遵循下列建議：</span><span class="sxs-lookup"><span data-stu-id="4b27b-114">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="4b27b-115">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="4b27b-115">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4b27b-116">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="4b27b-116">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4b27b-117">案例描述</span><span class="sxs-lookup"><span data-stu-id="4b27b-117">Scenario description</span></span>
<span data-ttu-id="4b27b-118">在本教學課程中，您會在測試環境中測試 Azure AD SSO。</span><span class="sxs-lookup"><span data-stu-id="4b27b-118">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="4b27b-119">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="4b27b-119">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4b27b-120">從資源庫新增 Workplace by Facebook。</span><span class="sxs-lookup"><span data-stu-id="4b27b-120">Add Workplace by Facebook from the gallery.</span></span>
2. <span data-ttu-id="4b27b-121">設定和測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4b27b-121">Configure and test Azure AD single sign-on.</span></span>

## <a name="add-workplace-by-facebook-from-the-gallery"></a><span data-ttu-id="4b27b-122">從資源庫新增 Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="4b27b-122">Add Workplace by Facebook from the gallery</span></span>
<span data-ttu-id="4b27b-123">若要設定將 Workplace by Facebook 整合到 Azure AD 中，從資源庫將 Workplace by Facebook 新增到受管理的 SaaS 應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="4b27b-123">To configure the integration of Workplace by Facebook into Azure AD, add Workplace by Facebook from the gallery to your list of managed SaaS apps.</span></span>

1. <span data-ttu-id="4b27b-124">在 [Azure 入口網站](https://portal.azure.com)的左側窗格中，選取 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="4b27b-124">In the [Azure portal](https://portal.azure.com), in the left pane, select **Azure Active Directory**.</span></span> 

    ![Azure Active Directory 按鈕][1]

2. <span data-ttu-id="4b27b-126">瀏覽至 [企業應用程式] > [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="4b27b-126">Browse to **Enterprise applications** > **All applications**.</span></span>

    ![企業應用程式刀鋒視窗][2]
    
3. <span data-ttu-id="4b27b-128">若要新增新的應用程式，請選取對話方塊頂端的 [新增應用程式]。</span><span class="sxs-lookup"><span data-stu-id="4b27b-128">To add the new application, select **New application** on the top of the dialog box.</span></span>

    ![新增應用程式按鈕][3]

4. <span data-ttu-id="4b27b-130">在搜尋方塊中，輸入 **Workplace by Facebook**，從結果中選取 [Workplace by Facebook]。</span><span class="sxs-lookup"><span data-stu-id="4b27b-130">In the search box, type **Workplace by Facebook**, and select **Workplace by Facebook** from results.</span></span> <span data-ttu-id="4b27b-131">然後選取 [新增]，以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="4b27b-131">Then select **Add**, to add the application.</span></span>

    ![結果清單中的 Workplace by Facebook](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_search.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4b27b-133">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="4b27b-133">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="4b27b-134">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Workplace by Facebook 搭配運作的 Azure AD SSO。</span><span class="sxs-lookup"><span data-stu-id="4b27b-134">In this section, you configure and test Azure AD SSO with Workplace by Facebook, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4b27b-135">若要讓 SSO 能夠運作，Azure AD 必須知道 Workplace by Facebook 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="4b27b-135">For SSO to work, Azure AD needs to know what the counterpart user in Workplace by Facebook is to a user in Azure AD.</span></span> <span data-ttu-id="4b27b-136">換句話說，應在 Azure AD 使用者與 Workplace by Facebook 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="4b27b-136">In other words, a linked relationship between an Azure AD user and the related user in Workplace by Facebook should be established.</span></span>

<span data-ttu-id="4b27b-137">建立此關聯性的方法，就是將 Azure AD 中的**使用者名稱**值指派為 Workplace by Facebook 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="4b27b-137">Establish this relationship by assigning the value of the **user name** in Azure AD as the value of the **Username** in Workplace by Facebook.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="4b27b-138">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="4b27b-138">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="4b27b-139">在本節中，您會在 Azure 入口網站中啟用 Azure AD SSO，然後在 Workplace by Facebook 應用程式中設定 SSO。</span><span class="sxs-lookup"><span data-stu-id="4b27b-139">In this section, you enable Azure AD SSO in the Azure portal, and you configure SSO in your Workplace by Facebook application.</span></span>

1. <span data-ttu-id="4b27b-140">在 Azure 入口網站的 [Workplace by Facebook] 應用程式整合頁面上，選取 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="4b27b-140">In the Azure portal, on the **Workplace by Facebook** application integration page, select **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="4b27b-142">在 [單一登入] 對話方塊中，於 [模式] 選取 [SAML 登入]，以啟用 SSO。</span><span class="sxs-lookup"><span data-stu-id="4b27b-142">In the **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on** to enable SSO.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. <span data-ttu-id="4b27b-144">在 [Workplace by Facebook 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="4b27b-144">In the **Workplace by Facebook Domain and URLs** section, do the following:</span></span>

    <span data-ttu-id="4b27b-145">a.</span><span class="sxs-lookup"><span data-stu-id="4b27b-145">a.</span></span> <span data-ttu-id="4b27b-146">在 [登入 URL] 文字方塊中，以下列模式輸入 URL︰`https://<company subdomain>.facebook.com`</span><span class="sxs-lookup"><span data-stu-id="4b27b-146">In the **Sign-on URL** text box, type a URL that uses the following pattern: `https://<company subdomain>.facebook.com`</span></span>

    <span data-ttu-id="4b27b-147">b.</span><span class="sxs-lookup"><span data-stu-id="4b27b-147">b.</span></span> <span data-ttu-id="4b27b-148">在 [識別碼] 文字方塊中，以下列模式輸入 URL：`https://www.facebook.com/company/<scim company id>`</span><span class="sxs-lookup"><span data-stu-id="4b27b-148">In the **Identifier** text box, type a URL that uses the following pattern: `https://www.facebook.com/company/<scim company id>`</span></span>

    > [!NOTE]
    > <span data-ttu-id="4b27b-149">這些值僅為範例。</span><span class="sxs-lookup"><span data-stu-id="4b27b-149">These values are an example only.</span></span> <span data-ttu-id="4b27b-150">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="4b27b-150">Update these values with the actual sign-on URL and identifier.</span></span> <span data-ttu-id="4b27b-151">請連絡 [Workplace by Facebook 用戶端支援小組](https://workplace.fb.com/faq/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="4b27b-151">Contact the [Workplace by Facebook Client support team](https://workplace.fb.com/faq/) to get these values.</span></span> 

4. <span data-ttu-id="4b27b-152">在 [SAML 簽署憑證] 區段中，選取 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="4b27b-152">In the **SAML Signing Certificate** section, select **Certificate (Base64)**, and then save the certificate file on your computer.</span></span>

    ![憑證下載連結](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. <span data-ttu-id="4b27b-154">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="4b27b-154">Select **Save**.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4b27b-156">在 [Workplace by Facebook 設定] 區段中，選取 [設定 Workplace by Facebook] 可開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="4b27b-156">In the **Workplace by Facebook Configuration** section, select **Configure Workplace by Facebook** to open the **Configure sign-on** window.</span></span> <span data-ttu-id="4b27b-157">從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="4b27b-157">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference** section.</span></span>

    ![Workplace by Facebook 設定](./media/active-directory-saas-facebook-at-work-tutorial/config.png) 

7. <span data-ttu-id="4b27b-159">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 Workplace by Facebook 公司網站。</span><span class="sxs-lookup"><span data-stu-id="4b27b-159">In a different web browser window, sign in to your Workplace by Facebook company site as an administrator.</span></span>
  
   > [!NOTE] 
   > <span data-ttu-id="4b27b-160">在 SAML 驗證過程中，Workplace 可以使用大小最多 2.5 KB 的查詢字串，將參數傳遞給 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="4b27b-160">As part of the SAML authentication process, Workplace can use query strings of up to 2.5 kilobytes in size in order to pass parameters to Azure AD.</span></span>

8. <span data-ttu-id="4b27b-161">在 [公司儀表板] 中，請移至 [驗證] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="4b27b-161">In the **Company Dashboard**, go to the **Authentication** tab.</span></span>

9. <span data-ttu-id="4b27b-162">在 [SAML 驗證] 下，從下拉式清單中選取 [僅限 SSO]。</span><span class="sxs-lookup"><span data-stu-id="4b27b-162">Under **SAML Authentication**, select **SSO Only** from the drop-down list.</span></span>

10. <span data-ttu-id="4b27b-163">將您從 Azure 入口網站的 [Workplace by Facebook 設定] 區段中複製的值輸入對應的欄位中：</span><span class="sxs-lookup"><span data-stu-id="4b27b-163">Enter the values copied from the **Workplace by Facebook Configuration** section of the Azure portal into the corresponding fields:</span></span>

    *   <span data-ttu-id="4b27b-164">在 [SAML URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [單一登入服務 URL] 的值。</span><span class="sxs-lookup"><span data-stu-id="4b27b-164">In the **SAML URL** text box, paste the value of **Single Sign-On Service URL**, which you have copied from the Azure portal.</span></span>
    *   <span data-ttu-id="4b27b-165">在 [SAML 簽發者 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 實體識別碼] 值。</span><span class="sxs-lookup"><span data-stu-id="4b27b-165">In the **SAML Issuer URL** text box, paste the value of **SAML Entity ID**, which you have copied from the Azure portal.</span></span>
    *   <span data-ttu-id="4b27b-166">在 [SAML 登出重新導向] \(選擇性) 中，貼上您從 Azure 入口網站複製的 [登出 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="4b27b-166">In **SAML Logout Redirect (optional)**, paste the value of **Sign-Out URL**, which you have copied from the Azure portal.</span></span>
    *   <span data-ttu-id="4b27b-167">在記事本中開啟您從 Azure 入口網站下載的 **base-64 編碼憑證**。</span><span class="sxs-lookup"><span data-stu-id="4b27b-167">Open your **base-64 encoded certificate** in Notepad, downloaded from the Azure portal.</span></span> <span data-ttu-id="4b27b-168">將其內容複製到剪貼簿，然後將它貼到 [SAML 憑證] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="4b27b-168">Copy the content of it into your clipboard, and then paste it to the **SAML Certificate** text box.</span></span>

11. <span data-ttu-id="4b27b-169">您需要輸入 [SAML 組態] 區段下所列的對象 URL、收件者 URL 和 ACS (判斷提示取用者服務) URL。</span><span class="sxs-lookup"><span data-stu-id="4b27b-169">You might need to enter the audience URL, recipient URL, and ACS (Assertion Consumer Service) URL, listed under the **SAML Configuration** section.</span></span>

12. <span data-ttu-id="4b27b-170">捲動到區段的底部，然後選取 [測試 SSO]。</span><span class="sxs-lookup"><span data-stu-id="4b27b-170">Scroll to the bottom of the section, and select **Test SSO**.</span></span> <span data-ttu-id="4b27b-171">顯示 Azure AD 登入頁面的快顯視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="4b27b-171">A pop-up window appears, with the Azure AD sign-in page.</span></span> <span data-ttu-id="4b27b-172">若要驗證，請如往常一樣輸入認證。</span><span class="sxs-lookup"><span data-stu-id="4b27b-172">To authenticate, enter your credentials as normal.</span></span> <span data-ttu-id="4b27b-173">確保從 Azure AD 傳回的電子郵件地址與您用來登入的 Workplace 帳戶相同。</span><span class="sxs-lookup"><span data-stu-id="4b27b-173">Ensure the email address returned back from Azure AD is the same as the Workplace account you are logged in with.</span></span>

13. <span data-ttu-id="4b27b-174">如果順利完成測試，請捲動到頁面底部並選取 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="4b27b-174">If the test has finished successfully, scroll to the bottom of the page and select **Save**.</span></span>

14. <span data-ttu-id="4b27b-175">使用 Workplace 的所有使用者現在都會看到進行驗證的 Azure AD 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="4b27b-175">Anyone using Workplace is now presented with Azure AD sign-in page for authentication.</span></span>

<span data-ttu-id="4b27b-176">您可以選擇設定 SAML 登出 URL，其可用來指向 Azure AD 的登出頁面。</span><span class="sxs-lookup"><span data-stu-id="4b27b-176">You can choose to configure a SAML sign out URL, which can be used to point at the Azure AD sign-out page.</span></span> <span data-ttu-id="4b27b-177">當啟用並設定此設定時，就不會再將使用者導向至 Workplace 登出頁面。</span><span class="sxs-lookup"><span data-stu-id="4b27b-177">When this setting is enabled and configured, the user is no longer directed to the Workplace sign-out page.</span></span> <span data-ttu-id="4b27b-178">相反地，系統會將使用者重新導向至 [SAML 登出重新導向] 設定中所新增的 URL。</span><span class="sxs-lookup"><span data-stu-id="4b27b-178">Instead, the user is redirected to the URL that was added in the SAML sign-out redirect setting.</span></span>


> [!TIP]
> <span data-ttu-id="4b27b-179">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本。</span><span class="sxs-lookup"><span data-stu-id="4b27b-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app.</span></span> <span data-ttu-id="4b27b-180">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要選取 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="4b27b-180">After adding this app from the **Active Directory** > **Enterprise Applications** section, simply select the **Single Sign-On** tab, and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4b27b-181">您可以在 [Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)中閱讀更多有關內嵌文件功能的資訊。</span><span class="sxs-lookup"><span data-stu-id="4b27b-181">You can read more about the embedded documentation feature in the [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="configure-reauthentication-frequency"></a><span data-ttu-id="4b27b-182">設定重新驗證頻率</span><span class="sxs-lookup"><span data-stu-id="4b27b-182">Configure reauthentication frequency</span></span>

<span data-ttu-id="4b27b-183">您可以將 Workplace 設定為每一天、每三天、每一週、每兩週、每一個月或一律不會提示進行 SAML 檢查。</span><span class="sxs-lookup"><span data-stu-id="4b27b-183">You can configure Workplace to prompt for a SAML check every day, three days, one week, two weeks, one month, or never.</span></span>

> [!NOTE] 
><span data-ttu-id="4b27b-184">行動應用程式的 SAML 檢查最小值是設定為一週。</span><span class="sxs-lookup"><span data-stu-id="4b27b-184">The minimum value for the SAML check on mobile applications is set to one week.</span></span>

<span data-ttu-id="4b27b-185">您也可以強制所有使用者重設 SAML。</span><span class="sxs-lookup"><span data-stu-id="4b27b-185">You can also force a SAML reset for all users.</span></span> <span data-ttu-id="4b27b-186">若要這樣做，請使用 [要求所有使用者立即進行 SAML 驗證] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4b27b-186">To do this, use the **Require SAML authentication for all users now** button.</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4b27b-187">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="4b27b-187">Create an Azure AD test user</span></span>
<span data-ttu-id="4b27b-188">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="4b27b-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

1. <span data-ttu-id="4b27b-190">在 **Azure 入口網站**的左側窗格中，選取 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="4b27b-190">In the **Azure portal**, in the left pane, select **Azure Active Directory**.</span></span>

    ![Azure Active Directory 按鈕](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4b27b-192">若要顯示使用者清單，請移至 [使用者和群組]，然後選取 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="4b27b-192">To display the list of users, go to **Users and groups**, and select **All users**.</span></span>
    
    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4b27b-194">若要開啟 [使用者] 對話方塊，請選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="4b27b-194">To open the **User** dialog box, select **Add**.</span></span>
 
    ![[新增] 按鈕](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4b27b-196">在 [使用者] 對話方塊中，執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="4b27b-196">In the **User** dialog box, do the following:</span></span>
 
    ![[使用者] 對話方塊](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4b27b-198">a.</span><span class="sxs-lookup"><span data-stu-id="4b27b-198">a.</span></span> <span data-ttu-id="4b27b-199">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="4b27b-199">In the **Name** text box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4b27b-200">b.</span><span class="sxs-lookup"><span data-stu-id="4b27b-200">b.</span></span> <span data-ttu-id="4b27b-201">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="4b27b-201">In the **User name** text box, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4b27b-202">c.</span><span class="sxs-lookup"><span data-stu-id="4b27b-202">c.</span></span> <span data-ttu-id="4b27b-203">選取 [顯示密碼]，並將它寫下來。</span><span class="sxs-lookup"><span data-stu-id="4b27b-203">Select **Show Password**, and write it down.</span></span>

    <span data-ttu-id="4b27b-204">d.</span><span class="sxs-lookup"><span data-stu-id="4b27b-204">d.</span></span> <span data-ttu-id="4b27b-205">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="4b27b-205">Select **Create**.</span></span>
 
### <a name="create-a-workplace-by-facebook-test-user"></a><span data-ttu-id="4b27b-206">建立 Workplace by Facebook 測試使用者</span><span class="sxs-lookup"><span data-stu-id="4b27b-206">Create a Workplace by Facebook test user</span></span>

<span data-ttu-id="4b27b-207">本節會在 Workplace by Facebook 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="4b27b-207">In this section, a user called Britta Simon is created in Workplace by Facebook.</span></span> <span data-ttu-id="4b27b-208">Workplace by Facebook 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="4b27b-208">Workplace by Facebook supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="4b27b-209">在這一節沒有您需要進行的動作。</span><span class="sxs-lookup"><span data-stu-id="4b27b-209">There is no action for you in this section.</span></span> <span data-ttu-id="4b27b-210">如果使用者不存在於 Workplace by Facebook 中，當您嘗試存取 Workplace by Facebook 時，就會建立一個新的。</span><span class="sxs-lookup"><span data-stu-id="4b27b-210">If a user doesn't exist in Workplace by Facebook, a new one is created when you attempt to access Workplace by Facebook.</span></span>

>[!Note]
><span data-ttu-id="4b27b-211">如果您需要手動建立使用者，請連絡 [Workplace by Facebook 用戶端支援小組](https://workplace.fb.com/faq/)。</span><span class="sxs-lookup"><span data-stu-id="4b27b-211">If you need to create a user manually, contact the [Workplace by Facebook Client support team](https://workplace.fb.com/faq/).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="4b27b-212">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="4b27b-212">Assign the Azure AD test user</span></span>

<span data-ttu-id="4b27b-213">在本節中，您會將 Workplace by Facebook 的存取權授與 Britta Simon，讓她能夠使用 Azure SSO。</span><span class="sxs-lookup"><span data-stu-id="4b27b-213">In this section, you enable Britta Simon to use Azure SSO by granting access to Workplace by Facebook.</span></span>

![指派使用者][200] 

1. <span data-ttu-id="4b27b-215">在 Azure 入口網站中，開啟應用程式檢視。</span><span class="sxs-lookup"><span data-stu-id="4b27b-215">In the Azure portal, open the applications view.</span></span> <span data-ttu-id="4b27b-216">移至目錄檢視，移至 [企業應用程式]，然後選取 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="4b27b-216">Go to the directory view, go to **Enterprise applications**, and then select **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="4b27b-218">在應用程式清單中，選取 [Workplace by Facebook]。</span><span class="sxs-lookup"><span data-stu-id="4b27b-218">In the applications list, select **Workplace by Facebook**.</span></span>

    ![應用程式清單中的 Workplace by Facebook 連結](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_app.png) 

3. <span data-ttu-id="4b27b-220">在左側功能表中，選取 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="4b27b-220">In the menu on the left, select **Users and groups**.</span></span>

    ![[使用者和群組] 連結][202] 

4. <span data-ttu-id="4b27b-222">選取 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="4b27b-222">Select **Add**.</span></span> <span data-ttu-id="4b27b-223">然後在 [新增指派] 窗格中，選取 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="4b27b-223">Then, in the **Add Assignment** pane, select **Users and groups**.</span></span>

    ![[新增指派] 窗格][203]

5. <span data-ttu-id="4b27b-225">在 [使用者和群組] 對話方塊中，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="4b27b-225">In the **Users and groups** dialog box, select **Britta Simon** in the users list.</span></span>

6. <span data-ttu-id="4b27b-226">在 [使用者和群組] 對話方塊中，選取 [選取]。</span><span class="sxs-lookup"><span data-stu-id="4b27b-226">In the **Users and groups** dialog box, select **Select**.</span></span>

7. <span data-ttu-id="4b27b-227">在 [新增指派] 對話方塊中，選取 [指派]。</span><span class="sxs-lookup"><span data-stu-id="4b27b-227">In the **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="4b27b-228">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="4b27b-228">Test single sign-on</span></span>

<span data-ttu-id="4b27b-229">如果要測試您的 SSO 設定，請開啟存取面板。</span><span class="sxs-lookup"><span data-stu-id="4b27b-229">If you want to test your SSO settings, open the Access Panel.</span></span>
<span data-ttu-id="4b27b-230">如需詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="4b27b-230">For more information, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="4b27b-231">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4b27b-231">Next steps</span></span>

* <span data-ttu-id="4b27b-232">選取[如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單](active-directory-saas-tutorial-list.md)。</span><span class="sxs-lookup"><span data-stu-id="4b27b-232">See the [list of tutorials on how to integrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md).</span></span>
* <span data-ttu-id="4b27b-233">閱讀[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="4b27b-233">Read [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>
* <span data-ttu-id="4b27b-234">深入了解如何[設定使用者佈建](active-directory-saas-facebook-at-work-provisioning-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="4b27b-234">Learn more about how to [configure user provisioning](active-directory-saas-facebook-at-work-provisioning-tutorial.md).</span></span>



<!--Image references-->

[1]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_203.png

