---
title: "教學課程：Azure Active Directory 與 Halosys 整合 | Microsoft Docs"
description: "了解如何使用 Halosys 搭配 Azure Active Directory 來啟用單一登入、自動化佈建和更多功能！"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 42a0eb7c-5cb7-44a9-b00b-b0e7df4b63e8
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 18c5cd8eb4ca211f8ae2b8dd994c0e8c48625a2f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halosys"></a><span data-ttu-id="f5086-103">教學課程：Azure Active Directory 與 Halosys 整合</span><span class="sxs-lookup"><span data-stu-id="f5086-103">Tutorial: Azure Active Directory integration with Halosys</span></span>

<span data-ttu-id="f5086-104">在本教學課程中，您將了解如何整合 Halosys 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="f5086-104">In this tutorial, you learn how to integrate Halosys with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f5086-105">Halosys 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="f5086-105">Integrating Halosys with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f5086-106">您可以在 Azure AD 中控制可存取 Halosys 的人員</span><span class="sxs-lookup"><span data-stu-id="f5086-106">You can control in Azure AD who has access to Halosys</span></span>
- <span data-ttu-id="f5086-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Halosys (單一登入)</span><span class="sxs-lookup"><span data-stu-id="f5086-107">You can enable your users to automatically get signed-on to Halosys (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f5086-108">您可以在 Azure 傳統入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="f5086-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="f5086-109">若您想了解 SaaS app 與 Azure AD 整合的更多詳細資訊，請參閱 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="f5086-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f5086-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="f5086-110">Prerequisites</span></span>

<span data-ttu-id="f5086-111">若要設定與 Halosys 的 Azure AD 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="f5086-111">To configure Azure AD integration with Halosys, you need the following items:</span></span>

- <span data-ttu-id="f5086-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f5086-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f5086-113">已啟用 Halosys 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f5086-113">A Halosys single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="f5086-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="f5086-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="f5086-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="f5086-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f5086-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="f5086-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="f5086-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="f5086-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="f5086-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="f5086-118">Scenario description</span></span>
<span data-ttu-id="f5086-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f5086-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="f5086-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="f5086-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f5086-121">從資源庫新增 Halosys</span><span class="sxs-lookup"><span data-stu-id="f5086-121">Adding Halosys from the gallery</span></span>
2. <span data-ttu-id="f5086-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f5086-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-halosys-from-the-gallery"></a><span data-ttu-id="f5086-123">從資源庫新增 Halosys</span><span class="sxs-lookup"><span data-stu-id="f5086-123">Adding Halosys from the gallery</span></span>
<span data-ttu-id="f5086-124">若要設定 Halosys 與 Azure AD 整合，您需要從資源庫將 Halosys 新增至受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="f5086-124">To configure the integration of Halosys into Azure AD, you need to add Halosys from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f5086-125">**若要從資源庫新增 Halosys，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f5086-125">**To add Halosys from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f5086-126">在 **Azure 傳統入口網站**中，按一下左方瀏覽窗格的 [Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="f5086-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]
2. <span data-ttu-id="f5086-128">從 [目錄]  清單中，選取要啟用目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="f5086-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="f5086-129">若要開啟應用程式檢視，請在目錄檢視中，按一下頂端功能表中的 [應用程式]  。</span><span class="sxs-lookup"><span data-stu-id="f5086-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![應用程式][2]

4. <span data-ttu-id="f5086-131">按一下頁面底部的 [新增]  。</span><span class="sxs-lookup"><span data-stu-id="f5086-131">Click **Add** at the bottom of the page.</span></span>

    ![應用程式][3]

5. <span data-ttu-id="f5086-133">在 [欲執行動作] 對話方塊上，按一下 [從資源庫中新增應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f5086-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>

    ![應用程式][4]

6. <span data-ttu-id="f5086-135">在搜尋方塊中，輸入 **Halosys**。</span><span class="sxs-lookup"><span data-stu-id="f5086-135">In the search box, type **Halosys**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_01.png)
    
7. <span data-ttu-id="f5086-137">在結果窗格中，選取 [Halosys]，然後按一下 [完成] 以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5086-137">In the results pane, select **Halosys**, and then click **Complete** to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_011.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f5086-139">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f5086-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f5086-140">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Halosys 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f5086-140">In this section, you configure and test Azure AD single sign-on with Halosys based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f5086-141">若要讓單一登入能夠運作，Azure AD 必須知道 Halosys 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="f5086-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Halosys is to a user in Azure AD.</span></span> <span data-ttu-id="f5086-142">換句話說，必須在 Azure AD 使用者與 Halosys 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="f5086-142">In other words, a link relationship between an Azure AD user and the related user in Halosys needs to be established.</span></span>

<span data-ttu-id="f5086-143">建立此連結關聯性的方法，就是指派 Azure AD 中**使用者名稱**的值做為 Halosys 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="f5086-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Halosys.</span></span>

<span data-ttu-id="f5086-144">若要設定及測試與 Halosys 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="f5086-144">To configure and test Azure AD single sign-on with Halosys, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f5086-145">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="f5086-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f5086-146">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f5086-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f5086-147">**[建立 Halosys 測試使用者](#creating-a-halosys-test-user)** - 在 Halosys 中建立一個與 Azure AD 中代表 Britta Simon 的項目連結的 Britta Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="f5086-147">**[Creating a Halosys test user](#creating-a-halosys-test-user)** - to have a counterpart of Britta Simon in Halosys that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="f5086-148">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f5086-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f5086-149">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="f5086-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f5086-150">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f5086-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f5086-151">在本節中，您會在傳統入口網站中啟用 Azure AD 單一登入，然後在您的 Halosys 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="f5086-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Halosys application.</span></span>


<span data-ttu-id="f5086-152">**若要設定與 Halosys 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f5086-152">**To configure Azure AD single sign-on with Halosys, perform the following steps:**</span></span>

1. <span data-ttu-id="f5086-153">在傳統入口網站的 **Halosys** 應用程式整合頁面上，按一下 [設定單一登入] 來開啟 [設定單一登入] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="f5086-153">In the classic portal, on the **Halosys** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
     
    ![設定單一登入][6] 

2. <span data-ttu-id="f5086-155">在 [要如何讓使用者登入 Halosys] 頁面上，選取 [Azure AD 單一登入]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="f5086-155">On the **How would you like users to sign on to Halosys** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![設定單一登入](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_03.png) 

3. <span data-ttu-id="f5086-157">在 [設定 App 設定]  對話方塊頁面執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f5086-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_04.png) 

    <span data-ttu-id="f5086-159">a.</span><span class="sxs-lookup"><span data-stu-id="f5086-159">a.</span></span> <span data-ttu-id="f5086-160">在 [登入 URL] 文字方塊中，使用以下模式輸入使用者登入您的 Halosys 應用程式時所使用的 URL：`https://<company-name>.Halosys.com/client-api/api`。</span><span class="sxs-lookup"><span data-stu-id="f5086-160">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Halosys application using the following pattern: `https://<company-name>.Halosys.com/client-api/api`.</span></span>

    <span data-ttu-id="f5086-161">在 [識別碼 URL] 文字方塊中，以下列模式輸入 URL：`https://<company-name>.Halosys.com`。</span><span class="sxs-lookup"><span data-stu-id="f5086-161">b.In the **Identifier URL** textbox, type the URL in the following pattern: `https://<company-name>.Halosys.com`.</span></span>   
         
4. <span data-ttu-id="f5086-162">在 [設定在 Halosys 單一登入] 頁面上，按一下 [下載中繼資料]，然後將檔案儲存在您的電腦中。</span><span class="sxs-lookup"><span data-stu-id="f5086-162">On the **Configure single sign-on at Halosys** page, click **Download metadata**, and then save the file on your computer:</span></span>

    ![設定單一登入](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_05.png)
   
5. <span data-ttu-id="f5086-164">若要為您的應用程式設定 SSO，請連絡 Halosys 支援小組，並提供下列資訊：</span><span class="sxs-lookup"><span data-stu-id="f5086-164">To get SSO configured for your application, contact Halosys support team and provide them with the following:</span></span>

    <span data-ttu-id="f5086-165">• 已下載的**中繼資料檔案**</span><span class="sxs-lookup"><span data-stu-id="f5086-165">• The downloaded **metadata file**</span></span>
    
    <span data-ttu-id="f5086-166">• **SAML SSO URL**</span><span class="sxs-lookup"><span data-stu-id="f5086-166">• The **SAML SSO URL**</span></span>
    

6. <span data-ttu-id="f5086-167">在傳統入口網站中，選取單一登入設定確認項目，然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="f5086-167">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Azure AD 單一登入][10]

7. <span data-ttu-id="f5086-169">在 [單一登入確認] 頁面上，按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="f5086-169">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Azure AD 單一登入][11]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f5086-171">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f5086-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="f5086-172">在本節中，您會在傳統入口網站中建立名稱為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="f5086-172">In this section, you create a test user in the classic portal called Britta Simon.</span></span>


![建立 Azure AD 使用者][20]

<span data-ttu-id="f5086-174">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f5086-174">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f5086-175">在 **Azure 傳統入口網站**中，按一下左方瀏覽窗格的 [Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="f5086-175">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-Halosys-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="f5086-177">從 [目錄]  清單中，選取要啟用目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="f5086-177">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="f5086-178">若要顯示使用者清單，請按一下頂端功能表的 [使用者] 。</span><span class="sxs-lookup"><span data-stu-id="f5086-178">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-Halosys-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f5086-180">若要開啟 [新增使用者] 對話方塊，請按一下底部工具列上的 [新增使用者]。</span><span class="sxs-lookup"><span data-stu-id="f5086-180">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-Halosys-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="f5086-182">在**告訴我們這位使用者**對話方塊頁面上，執行下列步驟：![建立 Azure AD 測試使用者](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png)</span><span class="sxs-lookup"><span data-stu-id="f5086-182">On the **Tell us about this user** dialog page, perform the following steps:  ![Creating an Azure AD test user](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png)</span></span> 

    <span data-ttu-id="f5086-183">a.</span><span class="sxs-lookup"><span data-stu-id="f5086-183">a.</span></span> <span data-ttu-id="f5086-184">針對 [使用者類型]，選取 [您組織中的新使用者]。</span><span class="sxs-lookup"><span data-stu-id="f5086-184">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="f5086-185">b.</span><span class="sxs-lookup"><span data-stu-id="f5086-185">b.</span></span> <span data-ttu-id="f5086-186">在 [使用者名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="f5086-186">In the User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f5086-187">c.</span><span class="sxs-lookup"><span data-stu-id="f5086-187">c.</span></span> <span data-ttu-id="f5086-188">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="f5086-188">Click **Next**.</span></span>

6.  <span data-ttu-id="f5086-189">在 [使用者設定檔] 對話方塊頁面上，執行下列步驟：![建立 Azure AD 測試使用者](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png)</span><span class="sxs-lookup"><span data-stu-id="f5086-189">On the **User Profile** dialog page, perform the following steps: ![Creating an Azure AD test user](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png)</span></span> 

    <span data-ttu-id="f5086-190">a.</span><span class="sxs-lookup"><span data-stu-id="f5086-190">a.</span></span> <span data-ttu-id="f5086-191">在 [名字] 文字方塊中，輸入 **Britta**。</span><span class="sxs-lookup"><span data-stu-id="f5086-191">In the **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="f5086-192">b.</span><span class="sxs-lookup"><span data-stu-id="f5086-192">b.</span></span> <span data-ttu-id="f5086-193">在 [姓氏] 文字方塊中，輸入 **Simon**。</span><span class="sxs-lookup"><span data-stu-id="f5086-193">In the **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="f5086-194">c.</span><span class="sxs-lookup"><span data-stu-id="f5086-194">c.</span></span> <span data-ttu-id="f5086-195">在 [顯示名稱] 文字方塊中，輸入 **Britta Simon**。</span><span class="sxs-lookup"><span data-stu-id="f5086-195">In the **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="f5086-196">d.</span><span class="sxs-lookup"><span data-stu-id="f5086-196">d.</span></span> <span data-ttu-id="f5086-197">在 [角色] 清單中選取 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="f5086-197">In the **Role** list, select **User**.</span></span>

    <span data-ttu-id="f5086-198">e.</span><span class="sxs-lookup"><span data-stu-id="f5086-198">e.</span></span> <span data-ttu-id="f5086-199">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="f5086-199">Click **Next**.</span></span>

7. <span data-ttu-id="f5086-200">在 [取得暫時密碼] 對話方塊頁面上，按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="f5086-200">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-Halosys-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="f5086-202">在 [取得暫時密碼]  對話方塊頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f5086-202">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-Halosys-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="f5086-204">a.</span><span class="sxs-lookup"><span data-stu-id="f5086-204">a.</span></span> <span data-ttu-id="f5086-205">記下 [新密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="f5086-205">Write down the value of the **New Password**.</span></span>

    <span data-ttu-id="f5086-206">b.</span><span class="sxs-lookup"><span data-stu-id="f5086-206">b.</span></span> <span data-ttu-id="f5086-207">按一下頁面底部的 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="f5086-207">Click **Complete**.</span></span>   



### <a name="creating-a-halosys-test-user"></a><span data-ttu-id="f5086-208">建立 Halosys 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f5086-208">Creating a Halosys test user</span></span>

<span data-ttu-id="f5086-209">在本節中，您要在 Halosys 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="f5086-209">In this section, you create a user called Britta Simon in Halosys.</span></span> <span data-ttu-id="f5086-210">請與 Halosys 支援小組合作，在 Halosys 平台中新增使用者。</span><span class="sxs-lookup"><span data-stu-id="f5086-210">Please work with Halosys support team to add the users in the Halosys platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f5086-211">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f5086-211">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f5086-212">在本節中，您會將 Halosys 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f5086-212">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Halosys.</span></span>

![指派使用者][200] 

<span data-ttu-id="f5086-214">**若要將 Britta Simon 指派給 Halosys，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f5086-214">**To assign Britta Simon to Halosys, perform the following steps:**</span></span>

1. <span data-ttu-id="f5086-215">在傳統入口網站中，若要開啟應用程式檢視，請在目錄檢視中，按一下頂端功能表中的 [應用程式]  。</span><span class="sxs-lookup"><span data-stu-id="f5086-215">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="f5086-217">在應用程式清單中，選取 [Halosys]。</span><span class="sxs-lookup"><span data-stu-id="f5086-217">In the applications list, select **Halosys**.</span></span>

    ![設定單一登入](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_50.png) 

3. <span data-ttu-id="f5086-219">在頂端的功能表中，按一下 [使用者] 。</span><span class="sxs-lookup"><span data-stu-id="f5086-219">In the menu on the top, click **Users**.</span></span>

    ![指派使用者][203]

4. <span data-ttu-id="f5086-221">在 [使用者] 清單中，選取 [Britta Simon] 。</span><span class="sxs-lookup"><span data-stu-id="f5086-221">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="f5086-222">在底部的工具列中，按一下 [指派] 。</span><span class="sxs-lookup"><span data-stu-id="f5086-222">In the toolbar on the bottom, click **Assign**.</span></span>

    ![指派使用者][205]


### <a name="testing-single-sign-on"></a><span data-ttu-id="f5086-224">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="f5086-224">Testing single sign-on</span></span>

<span data-ttu-id="f5086-225">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="f5086-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f5086-226">當您在存取面板中按一下 Halosys 圖格時，應該會自動登入您的 Halosys 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5086-226">When you click the Halosys tile in the Access Panel, you should get automatically signed-on to your Halosys application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="f5086-227">其他資源</span><span class="sxs-lookup"><span data-stu-id="f5086-227">Additional resources</span></span>

* [<span data-ttu-id="f5086-228">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="f5086-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f5086-229">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="f5086-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_205.png
