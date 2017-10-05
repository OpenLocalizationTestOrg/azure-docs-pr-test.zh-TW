---
title: "教學課程：Azure Active Directory 與 FirmPlay - Employee Advocacy for Recruiting 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 FirmPlay - Employee Advocacy for Recruiting 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a6799629-7546-43f8-a966-956db32864b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: 3cddd5b9508159089bf344dbb3882d462799747c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-firmplay---employee-advocacy-for-recruiting"></a><span data-ttu-id="65bc3-103">教學課程：Azure Active Directory 與 FirmPlay - Employee Advocacy for Recruiting 整合</span><span class="sxs-lookup"><span data-stu-id="65bc3-103">Tutorial: Azure Active Directory integration with FirmPlay - Employee Advocacy for Recruiting</span></span>

<span data-ttu-id="65bc3-104">在本教學課程中，您將了解如何整合 FirmPlay - Employee Advocacy for Recruiting 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="65bc3-104">In this tutorial, you learn how to integrate FirmPlay - Employee Advocacy for Recruiting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="65bc3-105">FirmPlay - Employee Advocacy for Recruiting 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="65bc3-105">Integrating FirmPlay - Employee Advocacy for Recruiting with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="65bc3-106">您可以在 Azure AD 中控制誰有 FirmPlay - Employee Advocacy for Recruiting 的存取權</span><span class="sxs-lookup"><span data-stu-id="65bc3-106">You can control in Azure AD who has access to FirmPlay - Employee Advocacy for Recruiting</span></span>
- <span data-ttu-id="65bc3-107">您可以讓使用者利用自己的 Azure AD 帳戶，來自動登入 FirmPlay - Employee Advocacy for Recruiting (單一登入)</span><span class="sxs-lookup"><span data-stu-id="65bc3-107">You can enable your users to automatically get signed-on to FirmPlay - Employee Advocacy for Recruiting (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="65bc3-108">您可以在 Azure 管理入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="65bc3-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="65bc3-109">若您想了解 SaaS app 與 Azure AD 整合的更多詳細資訊，請參閱 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="65bc3-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65bc3-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="65bc3-110">Prerequisites</span></span>

<span data-ttu-id="65bc3-111">如要設定 Azure AD 與 FirmPlay - Employee Advocacy for Recruiting 的整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="65bc3-111">To configure Azure AD integration with FirmPlay - Employee Advocacy for Recruiting, you need the following items:</span></span>

- <span data-ttu-id="65bc3-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="65bc3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="65bc3-113">已啟用 FirmPlay - Employee Advocacy for Recruiting 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="65bc3-113">A FirmPlay - Employee Advocacy for Recruiting single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="65bc3-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="65bc3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="65bc3-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="65bc3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="65bc3-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="65bc3-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="65bc3-117">如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="65bc3-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="65bc3-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="65bc3-118">Scenario description</span></span>
<span data-ttu-id="65bc3-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="65bc3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="65bc3-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="65bc3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="65bc3-121">從資源庫新增 FirmPlay - Employee Advocacy for Recruiting</span><span class="sxs-lookup"><span data-stu-id="65bc3-121">Adding FirmPlay - Employee Advocacy for Recruiting from the gallery</span></span>
2. <span data-ttu-id="65bc3-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="65bc3-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-firmplay---employee-advocacy-for-recruiting-from-the-gallery"></a><span data-ttu-id="65bc3-123">從資源庫新增 FirmPlay - Employee Advocacy for Recruiting</span><span class="sxs-lookup"><span data-stu-id="65bc3-123">Adding FirmPlay - Employee Advocacy for Recruiting from the gallery</span></span>
<span data-ttu-id="65bc3-124">若要設定將 FirmPlay - Employee Advocacy for Recruiting 整合到 Azure AD 中，您需要從資源庫將 FirmPlay - Employee Advocacy for Recruiting 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="65bc3-124">To configure the integration of FirmPlay - Employee Advocacy for Recruiting into Azure AD, you need to add FirmPlay - Employee Advocacy for Recruiting from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="65bc3-125">**若要從資源庫新增 FirmPlay - Employee Advocacy for Recruiting，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="65bc3-125">**To add FirmPlay - Employee Advocacy for Recruiting from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="65bc3-126">在 **[Azure 管理入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="65bc3-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="65bc3-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="65bc3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="65bc3-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="65bc3-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="65bc3-131">按一下對話方塊頂端的 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="65bc3-131">Click **Add** button on the top of the dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="65bc3-133">在搜尋方塊中，輸入 **FirmPlay - Employee Advocacy for Recruiting**。</span><span class="sxs-lookup"><span data-stu-id="65bc3-133">In the search box, type **FirmPlay - Employee Advocacy for Recruiting**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_001.png)

5. <span data-ttu-id="65bc3-135">在結果窗格中，選取 [FirmPlay - Employee Advocacy for Recruiting]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="65bc3-135">In the results panel, select **FirmPlay - Employee Advocacy for Recruiting**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="65bc3-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="65bc3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="65bc3-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 FirmPlay - Employee Advocacy for Recruiting 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="65bc3-138">In this section, you configure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="65bc3-139">若要讓單一登入運作，Azure AD 必須知道 FirmPlay - Employee Advocacy for Recruiting 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="65bc3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FirmPlay - Employee Advocacy for Recruiting is to a user in Azure AD.</span></span> <span data-ttu-id="65bc3-140">換句話說，必須要建立某位 Azure AD 使用者與 FirmPlay - Employee Advocacy for Recruiting 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="65bc3-140">In other words, a link relationship between an Azure AD user and the related user in FirmPlay - Employee Advocacy for Recruiting needs to be established.</span></span>

<span data-ttu-id="65bc3-141">建立此連結關聯性的方法，就是將 Azure AD 中**使用者名稱**的值指派為 FirmPlay - Employee Advocacy for Recruiting 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="65bc3-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in FirmPlay - Employee Advocacy for Recruiting.</span></span>

<span data-ttu-id="65bc3-142">若要使用 FirmPlay - Employee Advocacy for Recruiting 來設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="65bc3-142">To configure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="65bc3-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="65bc3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="65bc3-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="65bc3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="65bc3-145">**[建立 FirmPlay - Employee Advocacy for Recruiting 測試使用者](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)** - 在 FirmPlay - Employee Advocacy for Recruiting 中建立一個與 Azure AD 中代表 Britta Simon 的項目連結的 Britta Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="65bc3-145">**[Creating a FirmPlay - Employee Advocacy for Recruiting test user](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)** - to have a counterpart of Britta Simon in FirmPlay: Employee Advocacy for Recruiting that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="65bc3-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="65bc3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="65bc3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="65bc3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="65bc3-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="65bc3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="65bc3-149">在本節中，您會在 Azure 管理入口網站中啟用 Azure AD 單一登入，並在您的 FirmPlay - Employee Advocacy for Recruiting 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="65bc3-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your FirmPlay - Employee Advocacy for Recruiting application.</span></span>

<span data-ttu-id="65bc3-150">**若要設定與 FirmPlay - Employee Advocacy for Recruiting 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="65bc3-150">**To configure Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, perform the following steps:**</span></span>

1. <span data-ttu-id="65bc3-151">在 Azure 管理入口網站的 [FirmPlay - Employee Advocacy for Recruiting] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="65bc3-151">In the Azure Management portal, on the **FirmPlay - Employee Advocacy for Recruiting** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="65bc3-153">在 [單一登入] 對話方塊上，選取 [SAML 型登入] 做為 [模式]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="65bc3-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_01.png)

3. <span data-ttu-id="65bc3-155">在 [FirmPlay - Employee Advocacy for Recruiting 網域和 URL] 區段中，於 [登入 URL] 文字方塊中，使用下列模式輸入 URL：`https://<your-subdomain>.firmplay.com/`</span><span class="sxs-lookup"><span data-stu-id="65bc3-155">On the **FirmPlay - Employee Advocacy for Recruiting Domain and URLs** section, in the **Sign On URL** textbox, type a URL using the following pattern: `https://<your-subdomain>.firmplay.com/`</span></span>

    ![設定單一登入](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_02.png)

    > [!NOTE] 
    > <span data-ttu-id="65bc3-157">請注意，這不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="65bc3-157">Please note that this is not the real value.</span></span> <span data-ttu-id="65bc3-158">您必須使用實際的「登入 URL」來更新此值。</span><span class="sxs-lookup"><span data-stu-id="65bc3-158">You have to update this value with the actual Sign On URL.</span></span> <span data-ttu-id="65bc3-159">請連絡 [FirmPlay - Employee Advocacy for Recruiting 支援小組](mailto:engineering@firmplay.com)以取得此值。</span><span class="sxs-lookup"><span data-stu-id="65bc3-159">Contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) to get this value.</span></span> 

4. <span data-ttu-id="65bc3-160">在 [SAML 簽署憑證] 區段中，按一下 [建立新憑證]。</span><span class="sxs-lookup"><span data-stu-id="65bc3-160">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![設定單一登入](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_03.png)   

5. <span data-ttu-id="65bc3-162">在 [建立新憑證] 對話方塊中，按一下行事曆圖示並選取 [到期日]。</span><span class="sxs-lookup"><span data-stu-id="65bc3-162">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="65bc3-163">然後按一下 [儲存] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="65bc3-163">Then click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-firmplay-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="65bc3-165">在 [SAML 簽署憑證] 區段中，選取 [啟用新憑證] 並按一下 [儲存] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="65bc3-165">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_04.png)

7. <span data-ttu-id="65bc3-167">在 [變換憑證] 快顯視窗上，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="65bc3-167">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![設定單一登入](./media/active-directory-saas-firmplay-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="65bc3-169">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="65bc3-169">On the **SAML Signing Certificate** section, click **Certificate (base64)** and then save the certificate file on your computer.</span></span> 

    ![設定單一登入](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_05.png) 

9. <span data-ttu-id="65bc3-171">在 [FirmPlay - Employee Advocacy for Recruiting 組態] 區段上，按一下 [設定 FirmPlay - Employee Advocacy for Recruiting] 以開啟 [設定登入] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="65bc3-171">On the **FirmPlay - Employee Advocacy for Recruiting Configuration** section, click **Configure FirmPlay - Employee Advocacy for Recruiting** to open **Configure sign-on** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_06.png) 

    ![設定單一登入](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_07.png)

10. <span data-ttu-id="65bc3-174">若要為您的應用程式設定 SSO，請連絡 [FirmPlay - Employee Advocacy for Recruiting 支援小組](mailto:engineering@firmplay.com)，並提供下列資訊：</span><span class="sxs-lookup"><span data-stu-id="65bc3-174">To get SSO configured for your application, contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) and provide them with the following:</span></span> 

    <span data-ttu-id="65bc3-175">•  下載的「憑證檔案」</span><span class="sxs-lookup"><span data-stu-id="65bc3-175">•  The downloaded **Certificate file**</span></span>

    <span data-ttu-id="65bc3-176">•  **SAML 單一登入服務 URL**</span><span class="sxs-lookup"><span data-stu-id="65bc3-176">•  The **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="65bc3-177">•  **SAML 實體識別碼**</span><span class="sxs-lookup"><span data-stu-id="65bc3-177">•  The **SAML Entity ID**</span></span>

    <span data-ttu-id="65bc3-178">•  **登出 URL**</span><span class="sxs-lookup"><span data-stu-id="65bc3-178">•  The **Sign-Out URL**</span></span>
  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="65bc3-179">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="65bc3-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="65bc3-180">本節目標是在 Azure 管理入口網站中建立名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="65bc3-180">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="65bc3-182">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="65bc3-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="65bc3-183">在 **Azure 管理入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="65bc3-183">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-firmplay-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="65bc3-185">移至 [使用者和群組]，然後按一下 [所有使用者] 以顯示使用者清單。</span><span class="sxs-lookup"><span data-stu-id="65bc3-185">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-firmplay-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="65bc3-187">在對話方塊的頂端，按一下 [新增] 以開啟 [使用者] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="65bc3-187">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-firmplay-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="65bc3-189">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="65bc3-189">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-firmplay-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="65bc3-191">a.</span><span class="sxs-lookup"><span data-stu-id="65bc3-191">a.</span></span> <span data-ttu-id="65bc3-192">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="65bc3-192">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="65bc3-193">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="65bc3-193">b.</span></span> <span data-ttu-id="65bc3-194">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="65bc3-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="65bc3-195">c.</span><span class="sxs-lookup"><span data-stu-id="65bc3-195">c.</span></span> <span data-ttu-id="65bc3-196">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="65bc3-196">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="65bc3-197">d.</span><span class="sxs-lookup"><span data-stu-id="65bc3-197">d.</span></span> <span data-ttu-id="65bc3-198">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="65bc3-198">Click **Create**.</span></span> 



### <a name="creating-a-firmplay---employee-advocacy-for-recruiting-test-user"></a><span data-ttu-id="65bc3-199">建立 FirmPlay - Employee Advocacy for Recruiting 測試使用者</span><span class="sxs-lookup"><span data-stu-id="65bc3-199">Creating a FirmPlay - Employee Advocacy for Recruiting test user</span></span>

<span data-ttu-id="65bc3-200">在本節中，您要在 FirmPlay - Employee Advocacy for Recruiting 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="65bc3-200">In this section, you create a user called Britta Simon in FirmPlay - Employee Advocacy for Recruiting.</span></span> <span data-ttu-id="65bc3-201">請與 [FirmPlay - Employee Advocacy for Recruiting 支援小組](mailto:engineering@firmplay.com)合作，在 FirmPlay - Employee Advocacy for Recruiting 平台中新增使用者。</span><span class="sxs-lookup"><span data-stu-id="65bc3-201">Please work with [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) to add the users in the FirmPlay - Employee Advocacy for Recruiting platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="65bc3-202">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="65bc3-202">Assigning the Azure AD test user</span></span>

<span data-ttu-id="65bc3-203">在本節中，您會將 FirmPlay - Employee Advocacy for Recruiting 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="65bc3-203">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to FirmPlay - Employee Advocacy for Recruiting.</span></span>

![指派使用者][200] 

<span data-ttu-id="65bc3-205">**若要將 Britta Simon 指派給 FirmPlay - Employee Advocacy for Recruiting，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="65bc3-205">**To assign Britta Simon to FirmPlay - Employee Advocacy for Recruiting, perform the following steps:**</span></span>

1. <span data-ttu-id="65bc3-206">在 Azure 管理入口網站中，開啟應用程式檢視，然後瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="65bc3-206">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="65bc3-208">在應用程式清單中，選取 [FirmPlay - Employee Advocacy for Recruiting]。</span><span class="sxs-lookup"><span data-stu-id="65bc3-208">In the applications list, select **FirmPlay - Employee Advocacy for Recruiting**.</span></span>

    ![設定單一登入](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_50.png) 

3. <span data-ttu-id="65bc3-210">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="65bc3-210">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="65bc3-212">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="65bc3-212">Click **Add** button.</span></span> <span data-ttu-id="65bc3-213">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="65bc3-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="65bc3-215">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="65bc3-215">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="65bc3-216">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="65bc3-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="65bc3-217">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="65bc3-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="65bc3-218">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="65bc3-218">Testing single sign-on</span></span>

<span data-ttu-id="65bc3-219">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="65bc3-219">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="65bc3-220">當您在存取面板中按一下 [FirmPlay - Employee Advocacy for Recruiting] 圖格時，應該會自動登入您的 FirmPlay - Employee Advocacy for Recruiting 應用程式。</span><span class="sxs-lookup"><span data-stu-id="65bc3-220">When you click the FirmPlay - Employee Advocacy for Recruiting tile in the Access Panel, you should get automatically signed-on to your FirmPlay - Employee Advocacy for Recruiting application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="65bc3-221">其他資源</span><span class="sxs-lookup"><span data-stu-id="65bc3-221">Additional resources</span></span>

* [<span data-ttu-id="65bc3-222">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="65bc3-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="65bc3-223">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="65bc3-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_203.png