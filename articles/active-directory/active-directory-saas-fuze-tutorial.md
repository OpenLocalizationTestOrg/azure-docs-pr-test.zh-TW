---
title: "教學課程：Azure Active Directory 與 Fuze 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Fuze 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9780b4bf-1fd1-48c1-9ceb-f750225ae08a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeedes
ms.openlocfilehash: c7f7b095aac6202a7ec5248ee2bbb109615287a7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fuze"></a><span data-ttu-id="63f82-103">教學課程：Azure Active Directory 與 Fuze 整合</span><span class="sxs-lookup"><span data-stu-id="63f82-103">Tutorial: Azure Active Directory integration with Fuze</span></span>

<span data-ttu-id="63f82-104">在本教學課程中，您會了解如何整合 Fuze 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="63f82-104">In this tutorial, you learn how to integrate Fuze with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="63f82-105">Fuze 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="63f82-105">Integrating Fuze with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="63f82-106">您可以在 Azure AD 中控制可存取 Fuze 的人員</span><span class="sxs-lookup"><span data-stu-id="63f82-106">You can control in Azure AD who has access to Fuze</span></span>
- <span data-ttu-id="63f82-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Fuze (單一登入)</span><span class="sxs-lookup"><span data-stu-id="63f82-107">You can enable your users to automatically get signed-on to Fuze (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="63f82-108">您可以在 Azure 管理入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="63f82-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="63f82-109">若您想了解 SaaS app 與 Azure AD 整合的更多詳細資訊，請參閱 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="63f82-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="63f82-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="63f82-110">Prerequisites</span></span>

<span data-ttu-id="63f82-111">若要設定 Azure AD 與 Fuze 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="63f82-111">To configure Azure AD integration with Fuze, you need the following items:</span></span>

- <span data-ttu-id="63f82-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="63f82-112">An Azure AD subscription</span></span>
- <span data-ttu-id="63f82-113">啟用 Fuze 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="63f82-113">A Fuze single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="63f82-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="63f82-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="63f82-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="63f82-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="63f82-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="63f82-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="63f82-117">如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="63f82-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="63f82-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="63f82-118">Scenario description</span></span>
<span data-ttu-id="63f82-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="63f82-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="63f82-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="63f82-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="63f82-121">從資源庫新增 Fuze</span><span class="sxs-lookup"><span data-stu-id="63f82-121">Adding Fuze from the gallery</span></span>
2. <span data-ttu-id="63f82-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="63f82-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-fuze-from-the-gallery"></a><span data-ttu-id="63f82-123">從資源庫新增 Fuze</span><span class="sxs-lookup"><span data-stu-id="63f82-123">Adding Fuze from the gallery</span></span>
<span data-ttu-id="63f82-124">若要設定將 Fuze 整合到 Azure AD 中，您需要從資源庫將 Fuze 新增到受管理的 SaaS 應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="63f82-124">To configure the integration of Fuze into Azure AD, you need to add Fuze from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="63f82-125">**若要從資源庫新增 Fuze，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="63f82-125">**To add Fuze from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="63f82-126">在 **[Azure 管理入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="63f82-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="63f82-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="63f82-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="63f82-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="63f82-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="63f82-131">按一下對話方塊頂端的 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="63f82-131">Click **Add** button on the top of the dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="63f82-133">在搜尋方塊中，輸入 **Fuze**。</span><span class="sxs-lookup"><span data-stu-id="63f82-133">In the search box, type **Fuze**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_000.png)

5. <span data-ttu-id="63f82-135">在結果窗格中，選取 [Fuze]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="63f82-135">In the results panel, select **Fuze**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="63f82-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="63f82-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="63f82-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Fuze 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="63f82-138">In this section, you configure and test Azure AD single sign-on with Fuze based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="63f82-139">若要讓單一登入運作，Azure AD 必須知道 Fuze 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="63f82-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Fuze is to a user in Azure AD.</span></span> <span data-ttu-id="63f82-140">換句話說，必須建立 Azure AD 使用者和 Fuze 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="63f82-140">In other words, a link relationship between an Azure AD user and the related user in Fuze needs to be established.</span></span>

<span data-ttu-id="63f82-141">建立此連結關聯性的方法，是將 Azure AD 中**使用者名稱**的值，指派為 Fuze 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="63f82-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Fuze.</span></span>

<span data-ttu-id="63f82-142">若要設定及測試與 Fuze 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="63f82-142">To configure and test Azure AD single sign-on with Fuze, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="63f82-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="63f82-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="63f82-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="63f82-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="63f82-145">**[建立 Fuze 測試使用者](#creating-a-fuze-test-user)** - 在 Fuze 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表 Britta Simon 的項目連結。</span><span class="sxs-lookup"><span data-stu-id="63f82-145">**[Creating a Fuze test user](#creating-a-fuze-test-user)** - to have a counterpart of Britta Simon in Fuze that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="63f82-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="63f82-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="63f82-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="63f82-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="63f82-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="63f82-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="63f82-149">在本節中，您會在 Azure 管理入口網站中啟用 Azure AD 單一登入，並在您的 Fuze 中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="63f82-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Fuze application.</span></span>

<span data-ttu-id="63f82-150">**若要設定與 Fuze 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="63f82-150">**To configure Azure AD single sign-on with Fuze, perform the following steps:**</span></span>

1. <span data-ttu-id="63f82-151">在 Azure 管理入口網站的 [Fuze] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="63f82-151">In the Azure Management portal, on the **Fuze** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="63f82-153">在 [單一登入] 對話方塊上，選取 [SAML 型登入] 做為 [模式]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="63f82-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_01.png)

3. <span data-ttu-id="63f82-155">在 [Fuze 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="63f82-155">On the **Fuze Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_020.png)
    
    <span data-ttu-id="63f82-157">在 [登入 URL] 文字方塊中，將登入 URL 輸入為下列項目：`https://www.thinkingphones.com/jetspeed/portal/`</span><span class="sxs-lookup"><span data-stu-id="63f82-157">In the **Sign on URL** textbox, type the Sign-on URL as: `https://www.thinkingphones.com/jetspeed/portal/`</span></span>

4.  <span data-ttu-id="63f82-158">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="63f82-158">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-fuze-tutorial/tutorial_general_400.png)

5. <span data-ttu-id="63f82-160">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將 XML 檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="63f82-160">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the xml file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_05.png) 

6. <span data-ttu-id="63f82-162">若要在 **Fuze** 端設定單一登入，您必須將已下載的**中繼資料 XML** 傳送給 [Fuze 支援小組](https://www.fuze.com/support)。</span><span class="sxs-lookup"><span data-stu-id="63f82-162">To configure single sign-on on **Fuze** side, you need to send the downloaded **Metadata XML** to [Fuze support team](https://www.fuze.com/support).</span></span> <span data-ttu-id="63f82-163">他們會進行設定，讓 SAML SSO 連線在兩端都正確設定。</span><span class="sxs-lookup"><span data-stu-id="63f82-163">They will set this up in order to have the SAML SSO connection set properly on both sides.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="63f82-164">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="63f82-164">Creating an Azure AD test user</span></span>
<span data-ttu-id="63f82-165">本節目標是在 Azure 管理入口網站中建立名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="63f82-165">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="63f82-167">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="63f82-167">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="63f82-168">在 **Azure 管理入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="63f82-168">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-fuze-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="63f82-170">移至 [使用者和群組]，然後按一下 [所有使用者] 以顯示使用者清單。</span><span class="sxs-lookup"><span data-stu-id="63f82-170">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-fuze-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="63f82-172">在對話方塊的頂端，按一下 [新增] 以開啟 [使用者] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="63f82-172">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-fuze-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="63f82-174">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="63f82-174">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-fuze-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="63f82-176">a.</span><span class="sxs-lookup"><span data-stu-id="63f82-176">a.</span></span> <span data-ttu-id="63f82-177">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="63f82-177">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="63f82-178">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="63f82-178">b.</span></span> <span data-ttu-id="63f82-179">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="63f82-179">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="63f82-180">c.</span><span class="sxs-lookup"><span data-stu-id="63f82-180">c.</span></span> <span data-ttu-id="63f82-181">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="63f82-181">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="63f82-182">d.</span><span class="sxs-lookup"><span data-stu-id="63f82-182">d.</span></span> <span data-ttu-id="63f82-183">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="63f82-183">Click **Create**.</span></span> 


### <a name="creating-a-fuze-test-user"></a><span data-ttu-id="63f82-184">建立 Fuze 測試使用者</span><span class="sxs-lookup"><span data-stu-id="63f82-184">Creating a Fuze test user</span></span>

<span data-ttu-id="63f82-185">Fuze 應用程式僅在使用者佈建時完整支援，所以當他們登入時會自動建立。</span><span class="sxs-lookup"><span data-stu-id="63f82-185">Fuze application supports full Just in time user provision, so users will get created automatically when they sign-in.</span></span> <span data-ttu-id="63f82-186">如需任何其他詳細資料，請連絡 Fuze [支援](https://www.fuze.com/support)。</span><span class="sxs-lookup"><span data-stu-id="63f82-186">For any other clarification, please contact Fuze [support](https://www.fuze.com/support).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="63f82-187">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="63f82-187">Assigning the Azure AD test user</span></span>

<span data-ttu-id="63f82-188">在本節中，您會將 Fuze 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="63f82-188">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Fuze.</span></span>

![指派使用者][200] 

<span data-ttu-id="63f82-190">**若要將 Britta Simon 指派給 Fuze，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="63f82-190">**To assign Britta Simon to Fuze, perform the following steps:**</span></span>

1. <span data-ttu-id="63f82-191">在 Azure 管理入口網站中，開啟應用程式檢視，然後瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="63f82-191">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="63f82-193">在應用程式清單中，選取 [Fuze]。</span><span class="sxs-lookup"><span data-stu-id="63f82-193">In the applications list, select **Fuze**.</span></span>

    ![設定單一登入](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_50.png) 

3. <span data-ttu-id="63f82-195">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="63f82-195">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="63f82-197">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="63f82-197">Click **Add** button.</span></span> <span data-ttu-id="63f82-198">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="63f82-198">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="63f82-200">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="63f82-200">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="63f82-201">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="63f82-201">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="63f82-202">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="63f82-202">Click **Assign** button on **Add Assignment** dialog.</span></span>
    

### <a name="testing-single-sign-on"></a><span data-ttu-id="63f82-203">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="63f82-203">Testing single sign-on</span></span>

<span data-ttu-id="63f82-204">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="63f82-204">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="63f82-205">當您在存取面板中按一下 Fuze 圖格時，應該會自動登入您的 Fuze 應用程式。</span><span class="sxs-lookup"><span data-stu-id="63f82-205">When you click the Fuze tile in the Access Panel, you should get automatically signed-on to your Fuze application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="63f82-206">其他資源</span><span class="sxs-lookup"><span data-stu-id="63f82-206">Additional resources</span></span>

* [<span data-ttu-id="63f82-207">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="63f82-207">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="63f82-208">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="63f82-208">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_203.png