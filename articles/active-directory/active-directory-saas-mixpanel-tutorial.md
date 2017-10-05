---
title: "教學課程：Azure Active Directory 與 Mixpanel 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Mixpanel 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a2df26ef-d441-44ac-a9f3-b37bf9709bcb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 3dd11b3477de1329c1c8e45a6dbf212b1635fd95
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mixpanel"></a><span data-ttu-id="f942c-103">教學課程：Azure Active Directory 與 Mixpanel 整合</span><span class="sxs-lookup"><span data-stu-id="f942c-103">Tutorial: Azure Active Directory integration with Mixpanel</span></span>

<span data-ttu-id="f942c-104">在本教學課程中，您將了解如何整合 Mixpanel 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="f942c-104">In this tutorial, you learn how to integrate Mixpanel with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f942c-105">Mixpanel 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="f942c-105">Integrating Mixpanel with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f942c-106">您可以在 Azure AD 中控制可存取 Mixpanel 的人員</span><span class="sxs-lookup"><span data-stu-id="f942c-106">You can control in Azure AD who has access to Mixpanel</span></span>
- <span data-ttu-id="f942c-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Mixpanel (單一登入)</span><span class="sxs-lookup"><span data-stu-id="f942c-107">You can enable your users to automatically get signed-on to Mixpanel (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f942c-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="f942c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f942c-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="f942c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f942c-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="f942c-110">Prerequisites</span></span>

<span data-ttu-id="f942c-111">若要設定與 Mixpanel 的 Azure AD 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="f942c-111">To configure Azure AD integration with Mixpanel, you need the following items:</span></span>

- <span data-ttu-id="f942c-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f942c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f942c-113">已啟用 Mixpanel 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f942c-113">A Mixpanel single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f942c-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="f942c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f942c-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="f942c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f942c-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="f942c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f942c-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="f942c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f942c-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="f942c-118">Scenario description</span></span>
<span data-ttu-id="f942c-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f942c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f942c-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="f942c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f942c-121">從資源庫加入 Mixpanel</span><span class="sxs-lookup"><span data-stu-id="f942c-121">Adding Mixpanel from the gallery</span></span>
2. <span data-ttu-id="f942c-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f942c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mixpanel-from-the-gallery"></a><span data-ttu-id="f942c-123">從資源庫加入 Mixpanel</span><span class="sxs-lookup"><span data-stu-id="f942c-123">Adding Mixpanel from the gallery</span></span>
<span data-ttu-id="f942c-124">若要設定 Mixpanel 與 Azure AD 整合，您需要從資源庫將 Mixpanel 加入受管理的 SaaS 應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="f942c-124">To configure the integration of Mixpanel into Azure AD, you need to add Mixpanel from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f942c-125">**若要從資源庫加入 Mixpanel，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f942c-125">**To add Mixpanel from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f942c-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="f942c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f942c-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f942c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f942c-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f942c-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="f942c-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f942c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="f942c-133">在搜尋方塊中，輸入 **Mixpanel**。</span><span class="sxs-lookup"><span data-stu-id="f942c-133">In the search box, type **Mixpanel**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_search.png)

5. <span data-ttu-id="f942c-135">在結果窗格中，選取 [Mixpanel]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="f942c-135">In the results panel, select **Mixpanel**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f942c-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f942c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f942c-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Mixpanel 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f942c-138">In this section, you configure and test Azure AD single sign-on with Mixpanel based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f942c-139">若要讓單一登入運作，Azure AD 必須知道 Mixpanel 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="f942c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Mixpanel is to a user in Azure AD.</span></span> <span data-ttu-id="f942c-140">換句話說，必須在 Azure AD 使用者和 Mixpanel 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="f942c-140">In other words, a link relationship between an Azure AD user and the related user in Mixpanel needs to be established.</span></span>

<span data-ttu-id="f942c-141">在 Mixpanel 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="f942c-141">In Mixpanel, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f942c-142">若要設定及測試對 Mixpanel 的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="f942c-142">To configure and test Azure AD single sign-on with Mixpanel, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f942c-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="f942c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f942c-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f942c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f942c-145">**[建立 Mixpanel 測試使用者](#creating-a-mixpanel-test-user)** - 使 Mixpanel 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="f942c-145">**[Creating a Mixpanel test user](#creating-a-mixpanel-test-user)** - to have a counterpart of Britta Simon in Mixpanel that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f942c-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f942c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f942c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="f942c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f942c-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f942c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f942c-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Mixpanel 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="f942c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mixpanel application.</span></span>

<span data-ttu-id="f942c-150">**若要使用 Mixpanel 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f942c-150">**To configure Azure AD single sign-on with Mixpanel, perform the following steps:**</span></span>

1. <span data-ttu-id="f942c-151">在 Azure 入口網站的 [Mixpanel] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="f942c-151">In the Azure portal, on the **Mixpanel** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="f942c-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="f942c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_samlbase.png)

3. <span data-ttu-id="f942c-155">在 [Mixpanel 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f942c-155">On the **Mixpanel Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_url.png)

     <span data-ttu-id="f942c-157">在 [登入 URL] 文字方塊中，將 URL 輸入為：`https://mixpanel.com/login/`</span><span class="sxs-lookup"><span data-stu-id="f942c-157">In the **Sign-on URL** textbox, type a URL as: `https://mixpanel.com/login/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f942c-158">請在 [https://mixpanel.com/register/](https://mixpanel.com/register/) 註冊，來設定您的登入認證，及連絡 [Mixpanel 支援小組](mailto:support@mixpanel.com)來為您的租用戶啟用 SSO 設定。</span><span class="sxs-lookup"><span data-stu-id="f942c-158">Please register at [https://mixpanel.com/register/](https://mixpanel.com/register/) to set up your login credentials and  contact the [Mixpanel support team](mailto:support@mixpanel.com) to enable SSO settings for your tenant.</span></span> <span data-ttu-id="f942c-159">如有必要，您也可以向 Mixpanel 支援小組取得您的登入 URL 值。</span><span class="sxs-lookup"><span data-stu-id="f942c-159">You can also get your Sign On URL value if necessary from your Mixpanel support team.</span></span> 
 
4. <span data-ttu-id="f942c-160">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="f942c-160">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_certificate.png) 

5. <span data-ttu-id="f942c-162">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="f942c-162">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-mixpanel-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f942c-164">在 [Mixpanel 組態] 區段上，按一下 [設定 Mixpanel] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="f942c-164">On the **Mixpanel Configuration** section, click **Configure Mixpanel** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f942c-165">從 [快速參考] 區段中複製 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="f942c-165">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_configure.png) 

7. <span data-ttu-id="f942c-167">在不同的瀏覽器視窗中，以系統管理員身分登入您的 Mixpanel 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f942c-167">In a different browser window, sign-on to your Mixpanel application as an administrator.</span></span>

8. <span data-ttu-id="f942c-168">在頁面底部，按一下左邊角落的小 **齒輪** 圖示。</span><span class="sxs-lookup"><span data-stu-id="f942c-168">On bottom of the page, click the little **gear** icon in the left corner.</span></span> 
   
    ![Mixpanel 單一登入](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_06.png) 

9. <span data-ttu-id="f942c-170">按一下 [存取安全性] 索引標籤，然後按一下 [變更設定]。</span><span class="sxs-lookup"><span data-stu-id="f942c-170">Click the **Access security** tab, and then click **Change settings**.</span></span>
   
    ![Mixpanel 設定](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_08.png) 

10. <span data-ttu-id="f942c-172">在 [變更您的憑證] 對話方塊頁面上，按一下 [選擇檔案] 來上傳您下載的憑證，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="f942c-172">On the **Change your certificate** dialog page, click **Choose file** to upload your downloaded certificate, and then click **NEXT**.</span></span>
   
    ![Mixpanel 設定](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_09.png) 

11.  <span data-ttu-id="f942c-174">在 [變更驗證 URL] 對話方塊頁面上的 [驗證 URL] 文字方塊中，貼上您從 Azure 入口網站複製過來的 [SAML 單一登入服務 URL] 值，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="f942c-174">In the authentication URL textbox on the **Change your authentication  URL** dialog page, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal, and then click **NEXT**.</span></span>
   
   ![Mixpanel 設定](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_10.png) 

12. <span data-ttu-id="f942c-176">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="f942c-176">Click **Done**.</span></span>

> [!TIP]
> <span data-ttu-id="f942c-177">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="f942c-177">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f942c-178">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="f942c-178">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f942c-179">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f942c-179">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f942c-180">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f942c-180">Creating an Azure AD test user</span></span>
<span data-ttu-id="f942c-181">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="f942c-181">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="f942c-183">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f942c-183">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f942c-184">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="f942c-184">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f942c-186">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="f942c-186">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f942c-188">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="f942c-188">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f942c-190">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f942c-190">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f942c-192">a.</span><span class="sxs-lookup"><span data-stu-id="f942c-192">a.</span></span> <span data-ttu-id="f942c-193">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="f942c-193">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f942c-194">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="f942c-194">b.</span></span> <span data-ttu-id="f942c-195">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="f942c-195">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f942c-196">c.</span><span class="sxs-lookup"><span data-stu-id="f942c-196">c.</span></span> <span data-ttu-id="f942c-197">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="f942c-197">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f942c-198">d.</span><span class="sxs-lookup"><span data-stu-id="f942c-198">d.</span></span> <span data-ttu-id="f942c-199">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="f942c-199">Click **Create**.</span></span>
 
### <a name="creating-a-mixpanel-test-user"></a><span data-ttu-id="f942c-200">建立 Mixpanel 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f942c-200">Creating a Mixpanel test user</span></span>

<span data-ttu-id="f942c-201">本節目標是在 Mixpanel 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="f942c-201">The objective of this section is to create a user called Britta Simon in Mixpanel.</span></span> 

1. <span data-ttu-id="f942c-202">以系統管理員身分登入您的 Mixpanel 公司網站。</span><span class="sxs-lookup"><span data-stu-id="f942c-202">Sign on to your Mixpanel company site as an administrator.</span></span>

2. <span data-ttu-id="f942c-203">在頁面底部，按一下左邊角落的小齒輪圖示以開啟 [設定]  視窗。</span><span class="sxs-lookup"><span data-stu-id="f942c-203">On the bottom of the page, click the little gear button on the left corner to open the **Settings** window.</span></span>

3. <span data-ttu-id="f942c-204">按一下 [小組]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="f942c-204">Click the **Team** tab.</span></span>

4. <span data-ttu-id="f942c-205">在 [小組成員]  文字方塊中，輸入 Britta 在 Azure 中的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="f942c-205">In the **team member** textbox, type Britta's email address in the Azure.</span></span>
   
    ![Mixpanel 設定](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_11.png) 

5. <span data-ttu-id="f942c-207">按一下 [邀請] 。</span><span class="sxs-lookup"><span data-stu-id="f942c-207">Click **Invite**.</span></span> 

> [!Note]
> <span data-ttu-id="f942c-208">使用者會收到用來設定設定檔的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="f942c-208">The user will get an email to set up the profile.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f942c-209">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f942c-209">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f942c-210">在本節中，您會將 Mixpanel 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f942c-210">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mixpanel.</span></span>

![指派使用者][200] 

<span data-ttu-id="f942c-212">**若要將 Britta Simon 指派到 Mixpanel，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f942c-212">**To assign Britta Simon to Mixpanel, perform the following steps:**</span></span>

1. <span data-ttu-id="f942c-213">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f942c-213">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="f942c-215">在應用程式清單中，選取 [Mixpanel] 。</span><span class="sxs-lookup"><span data-stu-id="f942c-215">In the applications list, select **Mixpanel**.</span></span>

    ![設定單一登入](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_app.png) 

3. <span data-ttu-id="f942c-217">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="f942c-217">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="f942c-219">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f942c-219">Click **Add** button.</span></span> <span data-ttu-id="f942c-220">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="f942c-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="f942c-222">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="f942c-222">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f942c-223">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f942c-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f942c-224">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f942c-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f942c-225">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="f942c-225">Testing single sign-on</span></span>

<span data-ttu-id="f942c-226">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="f942c-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f942c-227">當您在存取面板中按一下 [Mixpanel] 磚時，應該會自動登入您的 Mixpanel 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f942c-227">When you click the Mixpanel tile in the Access Panel, you should get automatically signed-on to your Mixpanel application.</span></span>
<span data-ttu-id="f942c-228">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="f942c-228">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f942c-229">其他資源</span><span class="sxs-lookup"><span data-stu-id="f942c-229">Additional resources</span></span>

* [<span data-ttu-id="f942c-230">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="f942c-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f942c-231">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="f942c-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_203.png

