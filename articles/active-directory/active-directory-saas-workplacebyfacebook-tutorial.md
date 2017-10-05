---
title: "教學課程：Azure Active Directory 與 Workplace by Facebook 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Workplace by Facebook 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 1590a66f215f0c093d24ff602c0ad951ba1e1eea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a><span data-ttu-id="092dc-103">教學課程：Azure Active Directory 與 Workplace by Facebook 整合</span><span class="sxs-lookup"><span data-stu-id="092dc-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span></span>

<span data-ttu-id="092dc-104">在本教學課程中，您會了解如何將 Workplace by Facebook 與 Azure Active Directory (Azure AD) 整合。</span><span class="sxs-lookup"><span data-stu-id="092dc-104">In this tutorial, you learn how to integrate Workplace by Facebook with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="092dc-105">將 Workplace by Facebook 與 Azure AD 整合可提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="092dc-105">Integrating Workplace by Facebook with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="092dc-106">您可以在 Azure AD 中控制可存取 Workplace by Facebook 的人員</span><span class="sxs-lookup"><span data-stu-id="092dc-106">You can control in Azure AD who has access to Workplace by Facebook</span></span>
- <span data-ttu-id="092dc-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Workplace by Facebook (單一登入)</span><span class="sxs-lookup"><span data-stu-id="092dc-107">You can enable your users to automatically get signed-on to Workplace by Facebook (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="092dc-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="092dc-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="092dc-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="092dc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="092dc-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="092dc-110">Prerequisites</span></span>

<span data-ttu-id="092dc-111">若要設定 Azure AD 與 Workplace by Facebook 的整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="092dc-111">To configure Azure AD integration with Workplace by Facebook, you need the following items:</span></span>

- <span data-ttu-id="092dc-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="092dc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="092dc-113">已啟用 Workplace by Facebook 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="092dc-113">A Workplace by Facebook single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="092dc-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="092dc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="092dc-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="092dc-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="092dc-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="092dc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="092dc-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="092dc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="092dc-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="092dc-118">Scenario description</span></span>
<span data-ttu-id="092dc-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="092dc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="092dc-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="092dc-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="092dc-121">從資源庫新增 Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="092dc-121">Adding Workplace by Facebook from the gallery</span></span>
2. <span data-ttu-id="092dc-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="092dc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workplace-by-facebook-from-the-gallery"></a><span data-ttu-id="092dc-123">從資源庫新增 Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="092dc-123">Adding Workplace by Facebook from the gallery</span></span>
<span data-ttu-id="092dc-124">若要設定將 Workplace by Facebook 整合到 Azure AD 中，您需要從資源庫將 Workplace by Facebook 新增到受管理的 SaaS 應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="092dc-124">To configure the integration of Workplace by Facebook into Azure AD, you need to add Workplace by Facebook from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="092dc-125">**若要從資源庫新增 Workplace by Facebook，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="092dc-125">**To add Workplace by Facebook from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="092dc-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="092dc-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="092dc-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="092dc-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="092dc-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="092dc-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="092dc-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="092dc-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="092dc-133">在搜尋方塊中，輸入 **Workplace by Facebook**。</span><span class="sxs-lookup"><span data-stu-id="092dc-133">In the search box, type **Workplace by Facebook**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_search.png)

5. <span data-ttu-id="092dc-135">在結果面板中，選取 [Workplace by Facebook]，然後按一下 [新增] 按鈕以新增該應用程式。</span><span class="sxs-lookup"><span data-stu-id="092dc-135">In the results panel, select **Workplace by Facebook**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="092dc-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="092dc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="092dc-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Workplace by Facebook 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="092dc-138">In this section, you configure and test Azure AD single sign-on with Workplace by Facebook based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="092dc-139">若要讓單一登入能夠運作，Azure AD 必須知道 Workplace by Facebook 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="092dc-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Workplace by Facebook is to a user in Azure AD.</span></span> <span data-ttu-id="092dc-140">換句話說，必須在 Azure AD 使用者與 Workplace by Facebook 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="092dc-140">In other words, a link relationship between an Azure AD user and the related user in Workplace by Facebook needs to be established.</span></span>

<span data-ttu-id="092dc-141">建立此連結關聯性的方法，就是將 Azure AD 中**使用者名稱**的值指派為 Workplace by Facebook 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="092dc-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Workplace by Facebook.</span></span>

<span data-ttu-id="092dc-142">若要設定及測試與 Workplace by Facebook 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="092dc-142">To configure and test Azure AD single sign-on with Workplace by Facebook, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="092dc-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="092dc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="092dc-144">**[設定重新驗證頻率](#configuring-reauthentication-frequency)** - 可設定要提示進行 SAML 檢查的 Workplace。</span><span class="sxs-lookup"><span data-stu-id="092dc-144">**[Configuring Reauthentication Frequency](#configuring-reauthentication-frequency)** - to configure Workplace to prompt for a SAML check.</span></span>
3. <span data-ttu-id="092dc-145">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="092dc-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="092dc-146">**[建立 Workplace by Facebook 測試使用者](#creating-a-workplace-by-facebook-test-user)** - 在 Workplace by Facebook 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="092dc-146">**[Creating a Workplace by Facebook test user](#creating-a-workplace-by-facebook-test-user)** - to have a counterpart of Britta Simon in Workplace by Facebook that is linked to the Azure AD representation of user.</span></span>
5. <span data-ttu-id="092dc-147">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="092dc-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
6. <span data-ttu-id="092dc-148">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="092dc-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="092dc-149">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="092dc-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="092dc-150">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Workplace by Facebook 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="092dc-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workplace by Facebook application.</span></span>

<span data-ttu-id="092dc-151">**若要設定透過 Workplace by Facebook 使用 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="092dc-151">**To configure Azure AD single sign-on with Workplace by Facebook, perform the following steps:**</span></span>

1. <span data-ttu-id="092dc-152">在 Azure 入口網站的 [Workplace by Facebook] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="092dc-152">In the Azure portal, on the **Workplace by Facebook** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="092dc-154">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="092dc-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. <span data-ttu-id="092dc-156">在 [Workplace by Facebook 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="092dc-156">On the **Workplace by Facebook Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_url.png)

    <span data-ttu-id="092dc-158">a.</span><span class="sxs-lookup"><span data-stu-id="092dc-158">a.</span></span> <span data-ttu-id="092dc-159">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<instancename>.facebook.com`</span><span class="sxs-lookup"><span data-stu-id="092dc-159">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instancename>.facebook.com`</span></span>

    <span data-ttu-id="092dc-160">b.</span><span class="sxs-lookup"><span data-stu-id="092dc-160">b.</span></span> <span data-ttu-id="092dc-161">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://www.facebook.com/company/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="092dc-161">In the **Identifier** textbox, type a URL using the following pattern: `https://www.facebook.com/company/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="092dc-162">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="092dc-162">These values are not the real.</span></span> <span data-ttu-id="092dc-163">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="092dc-163">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="092dc-164">請連絡 [Workplace by Facebook 用戶端支援小組](https://workplace.fb.com/faq/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="092dc-164">Contact [Workplace by Facebook Client support team](https://workplace.fb.com/faq/) to get these values.</span></span> 

4. <span data-ttu-id="092dc-165">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="092dc-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. <span data-ttu-id="092dc-167">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="092dc-167">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="092dc-169">在 [Workplace by Facebook 設定] 區段中，按一下 [設定 Workplace by Facebook] 可開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="092dc-169">On the **Workplace by Facebook Configuration** section, click **Configure Workplace by Facebook** to open **Configure sign-on** window.</span></span> <span data-ttu-id="092dc-170">從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="092dc-170">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-workplacebyfacebook-tutorial/config.png) 

7. <span data-ttu-id="092dc-172">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 Workplace by Facebook 公司網站。</span><span class="sxs-lookup"><span data-stu-id="092dc-172">In a different web browser window, login to your Workplace by Facebook company site as an administrator.</span></span>
  
   > [!NOTE] 
   > <span data-ttu-id="092dc-173">為將參數傳遞給 Azure AD，Workplace 可利用大小最多 2.5 KB 的查詢字串，作為 SAML 驗證流程的一部分。</span><span class="sxs-lookup"><span data-stu-id="092dc-173">As part of the SAML authentication process, Workplace may utilize query strings of up to 2.5 kilobytes in size in order to pass parameters to Azure AD.</span></span>

8. <span data-ttu-id="092dc-174">在 [公司儀表板] 中，請移至 [驗證] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="092dc-174">In the **Company Dashboard**, go to the **Authentication** tab.</span></span>

9. <span data-ttu-id="092dc-175">在 [SAML 驗證] 下，從下拉式清單中選取 [僅限 SSO]。</span><span class="sxs-lookup"><span data-stu-id="092dc-175">Under **SAML Authentication**, select **SSO Only** from the drop-down list.</span></span>

10. <span data-ttu-id="092dc-176">將您從 Azure 入口網站的 [Workplace by Facebook 設定] 區段中複製的值輸入對應的欄位中：</span><span class="sxs-lookup"><span data-stu-id="092dc-176">Input the values copied from **Workplace by Facebook Configuration** section of the Azure portal into the corresponding fields:</span></span>

    *   <span data-ttu-id="092dc-177">在 [SAML URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [單一登入服務 URL] 的值。</span><span class="sxs-lookup"><span data-stu-id="092dc-177">In **SAML URL** textbox, paste the value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="092dc-178">在 [SAML 簽發者 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 實體識別碼] 值。</span><span class="sxs-lookup"><span data-stu-id="092dc-178">In **SAML Issuer URL textbox**, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="092dc-179">在 [SAML 登出重新導向] \(選擇性) 中，貼上您從 Azure 入口網站複製的 [登出 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="092dc-179">In **SAML Logout Redirect** (Optional), paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="092dc-180">在從 Azure 入口網站下載的記事本檔案中開啟您的 **base-64 編碼憑證**，將憑證的內容複製到剪貼簿，再貼到 [SAML 憑證] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="092dc-180">Open your **base-64 encoded certificate** in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **SAML Certificate** textbox.</span></span>

11. <span data-ttu-id="092dc-181">您將需要輸入 [SAML 設定] 區段下所列的對象 URL、收件者 URL 和 ACS (判斷提示取用者服務) URL。</span><span class="sxs-lookup"><span data-stu-id="092dc-181">You may need to enter the Audience URL, Recipient URL, and ACS (Assertion Consumer Service) URL listed under the **SAML Configuration** section.</span></span>

12. <span data-ttu-id="092dc-182">捲動到區段的底部，然後按一下 [測試 SSO] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="092dc-182">Scroll to the bottom of the section and click the **Test SSO** button.</span></span> <span data-ttu-id="092dc-183">快顯視窗中的這個結果隨即顯示，並會出現 Azure AD 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="092dc-183">This results in a popup window appearing with Azure AD login page presented.</span></span> <span data-ttu-id="092dc-184">如往常輸入您的認證以進行驗證。</span><span class="sxs-lookup"><span data-stu-id="092dc-184">Enter your credentials in as normal to authenticate.</span></span> 

    <span data-ttu-id="092dc-185">**疑難排解：**確保從 Azure AD 傳回的電子郵件地址與您用來登入的 Workplace 帳戶相同。</span><span class="sxs-lookup"><span data-stu-id="092dc-185">**Troubleshooting:** Ensure the email address being returned back from Azure AD is the same as the Workplace account you are logged in with.</span></span>

13. <span data-ttu-id="092dc-186">一旦測試已順利完成後，捲動到頁面底部，然後按一下 [儲存] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="092dc-186">Once the test has been completed successfully, scroll to the bottom of the page and click the **Save** button.</span></span>

14. <span data-ttu-id="092dc-187">現在，使用 Workplace 的所有使用者都將會看到進行驗證的 Azure AD 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="092dc-187">All users using Workplace will now be presented with Azure AD login page for authentication.</span></span>

15. <span data-ttu-id="092dc-188">**SAML 登出重新導向 (選擇性)** -</span><span class="sxs-lookup"><span data-stu-id="092dc-188">**SAML Logout Redirect (optional)** -</span></span> 

    <span data-ttu-id="092dc-189">您可以選擇性地選擇設定 SAML 登出 URL，可用來指向 Azure AD 的登出頁面。</span><span class="sxs-lookup"><span data-stu-id="092dc-189">You can choose to optionally configure a SAML Logout Url, which can be used to point at Azure AD's logout page.</span></span> <span data-ttu-id="092dc-190">當啟用並設定此設定時，就不會再將使用者導向至 Workplace 登出頁面。</span><span class="sxs-lookup"><span data-stu-id="092dc-190">When this setting is enabled and configured, the user will no longer be directed to the Workplace logout page.</span></span> <span data-ttu-id="092dc-191">相反地，系統會將使用者重新導向至 [SAML 登出重新導向] 設定中所新增的 URL。</span><span class="sxs-lookup"><span data-stu-id="092dc-191">Instead, the user will be redirected to the url that was added in the SAML Logout Redirect setting.</span></span>


> [!TIP]
> <span data-ttu-id="092dc-192">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="092dc-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="092dc-193">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="092dc-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="092dc-194">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="092dc-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="configuring-reauthentication-frequency"></a><span data-ttu-id="092dc-195">設定重新驗證頻率</span><span class="sxs-lookup"><span data-stu-id="092dc-195">Configuring Reauthentication Frequency</span></span>

<span data-ttu-id="092dc-196">您可以將 Workplace 設定為每一天、每三天、每一週、每兩週、每一個月或一律不會提示進行 SAML 檢查。</span><span class="sxs-lookup"><span data-stu-id="092dc-196">You can configure Workplace to prompt for a SAML check every day, three days, week, two weeks, month or never.</span></span>

> [!NOTE] 
><span data-ttu-id="092dc-197">行動應用程式的 SAML 檢查最小值是設定為一週。</span><span class="sxs-lookup"><span data-stu-id="092dc-197">The minimum value for the SAML check on mobile applications is set to one week.</span></span>

<span data-ttu-id="092dc-198">您也可以使用下列按鈕來強制重設所有使用者的 SAML：所有使用者現在需要 SAML 驗證。</span><span class="sxs-lookup"><span data-stu-id="092dc-198">You can also force a SAML reset for all users using the button: Require SAML authentication for all users now.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="092dc-199">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="092dc-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="092dc-200">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="092dc-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="092dc-202">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="092dc-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="092dc-203">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="092dc-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="092dc-205">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="092dc-205">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="092dc-207">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="092dc-207">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="092dc-209">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="092dc-209">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="092dc-211">a.</span><span class="sxs-lookup"><span data-stu-id="092dc-211">a.</span></span> <span data-ttu-id="092dc-212">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="092dc-212">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="092dc-213">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="092dc-213">b.</span></span> <span data-ttu-id="092dc-214">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="092dc-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="092dc-215">c.</span><span class="sxs-lookup"><span data-stu-id="092dc-215">c.</span></span> <span data-ttu-id="092dc-216">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="092dc-216">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="092dc-217">d.</span><span class="sxs-lookup"><span data-stu-id="092dc-217">d.</span></span> <span data-ttu-id="092dc-218">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="092dc-218">Click **Create**.</span></span>
 
### <a name="creating-a-workplace-by-facebook-test-user"></a><span data-ttu-id="092dc-219">建立 Workplace by Facebook 測試使用者</span><span class="sxs-lookup"><span data-stu-id="092dc-219">Creating a Workplace by Facebook test user</span></span>

<span data-ttu-id="092dc-220">本節會在 Workplace by Facebook 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="092dc-220">In this section, a user called Britta Simon is created in Workplace by Facebook.</span></span> <span data-ttu-id="092dc-221">Workplace by Facebook 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="092dc-221">Workplace by Facebook supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="092dc-222">在這一節沒有您需要進行的動作。</span><span class="sxs-lookup"><span data-stu-id="092dc-222">There is no action for you in this section.</span></span> <span data-ttu-id="092dc-223">如果使用者不存在於 Workplace by Facebook 中，當您嘗試存取 Workplace by Facebook 時，就會建立一個新的。</span><span class="sxs-lookup"><span data-stu-id="092dc-223">If a user doesn't exist in Workplace by Facebook, a new one is created when you attempt to access Workplace by Facebook.</span></span>

>[!Note]
><span data-ttu-id="092dc-224">如果您需要手動建立使用者，請連絡 [Workplace by Facebook 用戶端支援小組](https://workplace.fb.com/faq/)</span><span class="sxs-lookup"><span data-stu-id="092dc-224">If you need to create a user manually, Contact [Workplace by Facebook Client support team](https://workplace.fb.com/faq/)</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="092dc-225">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="092dc-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="092dc-226">在本節中，您會將 Workplace by Facebook 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="092dc-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workplace by Facebook.</span></span>

![指派使用者][200] 

<span data-ttu-id="092dc-228">**若要將 Britta Simon 指派給 Workplace by Facebook，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="092dc-228">**To assign Britta Simon to Workplace by Facebook, perform the following steps:**</span></span>

1. <span data-ttu-id="092dc-229">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="092dc-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="092dc-231">在應用程式清單中，選取 [Workplace by Facebook]。</span><span class="sxs-lookup"><span data-stu-id="092dc-231">In the applications list, select **Workplace by Facebook**.</span></span>

    ![設定單一登入](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_app.png) 

3. <span data-ttu-id="092dc-233">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="092dc-233">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="092dc-235">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="092dc-235">Click **Add** button.</span></span> <span data-ttu-id="092dc-236">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="092dc-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="092dc-238">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="092dc-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="092dc-239">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="092dc-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="092dc-240">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="092dc-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="092dc-241">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="092dc-241">Testing single sign-on</span></span>

<span data-ttu-id="092dc-242">如果要測試您的單一登入設定，請開啟存取面板。</span><span class="sxs-lookup"><span data-stu-id="092dc-242">If you want to test your single sign-on settings, open the Access Panel.</span></span>
<span data-ttu-id="092dc-243">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="092dc-243">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="092dc-244">其他資源</span><span class="sxs-lookup"><span data-stu-id="092dc-244">Additional resources</span></span>

* [<span data-ttu-id="092dc-245">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="092dc-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="092dc-246">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="092dc-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="092dc-247">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="092dc-247">Configure User Provisioning</span></span>](active-directory-saas-workplacebyfacebook-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_203.png

