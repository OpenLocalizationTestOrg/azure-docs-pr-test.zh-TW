---
title: "教學課程：Azure Active Directory 與 Soonr Workplace 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Soonr Workplace 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
editor: na
ms.assetid: b75f5f00-ea8b-4850-ae2e-134e5d678d97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 76946e4af624d70f2202601ee935523ca3db4314
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-soonr-workplace"></a><span data-ttu-id="adb62-103">教學課程：Azure Active Directory 與 Soonr Workplace 整合</span><span class="sxs-lookup"><span data-stu-id="adb62-103">Tutorial: Azure Active Directory integration with Soonr Workplace</span></span>

<span data-ttu-id="adb62-104">本教學課程旨在說明如何整合 Soonr Workplace 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="adb62-104">The objective of this tutorial is to show you how to integrate Soonr Workplace with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="adb62-105">將 Soonr Workplace 與 Azure AD 整合可提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="adb62-105">Integrating Soonr Workplace with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="adb62-106">您可以在 Azure AD 中控制可存取 Soonr Workplace 的人員</span><span class="sxs-lookup"><span data-stu-id="adb62-106">You can control in Azure AD who has access to Soonr Workplace</span></span>
- <span data-ttu-id="adb62-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Soonr Workplace (單一登入)</span><span class="sxs-lookup"><span data-stu-id="adb62-107">You can enable your users to automatically get signed-on to Soonr Workplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="adb62-108">您可以在 Azure 傳統入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="adb62-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="adb62-109">若您想了解 SaaS app 與 Azure AD 整合的更多詳細資訊，請參閱 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="adb62-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="adb62-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="adb62-110">Prerequisites</span></span>

<span data-ttu-id="adb62-111">若要設定 Azure AD 與 Soonr Workplace 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="adb62-111">To configure Azure AD integration with Soonr Workplace, you need the following items:</span></span>

- <span data-ttu-id="adb62-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="adb62-112">An Azure AD subscription</span></span>
- <span data-ttu-id="adb62-113">已啟用 Soonr Workplace 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="adb62-113">A Soonr Workplace single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="adb62-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="adb62-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="adb62-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="adb62-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="adb62-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="adb62-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="adb62-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="adb62-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="adb62-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="adb62-118">Scenario description</span></span>
<span data-ttu-id="adb62-119">此教學課程的目標是讓您在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="adb62-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="adb62-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="adb62-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="adb62-121">從資源庫新增 Soonr Workplace</span><span class="sxs-lookup"><span data-stu-id="adb62-121">Adding Soonr Workplace from the gallery</span></span>
2. <span data-ttu-id="adb62-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="adb62-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-soonr-workplace-from-the-gallery"></a><span data-ttu-id="adb62-123">從資源庫新增 Soonr Workplace</span><span class="sxs-lookup"><span data-stu-id="adb62-123">Adding Soonr Workplace from the gallery</span></span>
<span data-ttu-id="adb62-124">若要設定將 Soonr Workplace 整合到 Azure AD 中，您需要從資源庫將 Soonr Workplace 新增到受管理的 SaaS 應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="adb62-124">To configure the integration of Soonr Workplace into Azure AD, you need to add Soonr Workplace from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="adb62-125">**若要從資源庫新增 Soonr Workplace，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="adb62-125">**To add Soonr Workplace from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="adb62-126">在 **Azure 傳統入口網站**中，按一下左方瀏覽窗格的 [Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="adb62-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="adb62-128">從 [目錄]  清單中，選取要啟用目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="adb62-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="adb62-129">若要開啟應用程式檢視，請在目錄檢視中，按一下頂端功能表中的 [應用程式]  。</span><span class="sxs-lookup"><span data-stu-id="adb62-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![應用程式][2]

4. <span data-ttu-id="adb62-131">按一下頁面底部的 [新增]  。</span><span class="sxs-lookup"><span data-stu-id="adb62-131">Click **Add** at the bottom of the page.</span></span>

    ![應用程式][3]

5. <span data-ttu-id="adb62-133">在 [欲執行動作] 對話方塊上，按一下 [從資源庫中新增應用程式]。</span><span class="sxs-lookup"><span data-stu-id="adb62-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
 
    ![應用程式][4]

6. <span data-ttu-id="adb62-135">在搜尋方塊中，輸入 **Soonr Workplace**。</span><span class="sxs-lookup"><span data-stu-id="adb62-135">In the search box, type **Soonr Workplace**.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_01.png)

7. <span data-ttu-id="adb62-137">在結果窗格中，選取 [Soonr Workplace]，然後按一下 [完成] 以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="adb62-137">In the results pane, select **Soonr Workplace**, and then click **Complete** to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_02.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="adb62-139">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="adb62-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="adb62-140">本節的目標是要說明如何以名為 "Britta Simon"的測試使用者為基礎，設定及測試與 Soonr Workplace 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="adb62-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Soonr Workplace based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="adb62-141">若要讓單一登入能夠運作，Azure AD 必須知道 Soonr Workplace 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="adb62-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Soonr Workplace to an user in Azure AD is.</span></span> <span data-ttu-id="adb62-142">換句話說，必須在 Azure AD 使用者與 Soonr Workplace 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="adb62-142">In other words, a link relationship between an Azure AD user and the related user in Soonr Workplace needs to be established.</span></span>  

<span data-ttu-id="adb62-143">建立此連結關聯性的方法，就是將 Azure AD 中**使用者名稱**的值指派為 Soonr Workplace 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="adb62-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Soonr Workplace.</span></span>

<span data-ttu-id="adb62-144">若要設定及測試與 Soonr Workplace 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="adb62-144">To configure and test Azure AD single sign-on with Soonr Workplace, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="adb62-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="adb62-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="adb62-146">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="adb62-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="adb62-147">**[建立 Soonr Workplace 測試使用者](#creating-a-soonr-workplace-test-user)** - 在 Soonr Workplace 中建立一個與 Azure AD 中代表 Britta Simon 的項目連結的 Britta Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="adb62-147">**[Creating a Soonr Workplace test user](#creating-a-soonr-workplace-test-user)** - to have a counterpart of Britta Simon in Soonr Workplace that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="adb62-148">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="adb62-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="adb62-149">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="adb62-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="adb62-150">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="adb62-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="adb62-151">在本節中，您會在傳統入口網站中啟用 Azure AD 單一登入，並在您的 Soonr Workplace 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="adb62-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Soonr Workplace application.</span></span>


<span data-ttu-id="adb62-152">**若要設定透過 Soonr Workplace 使用 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="adb62-152">**To configure Azure AD single sign-on with Soonr Workplace, perform the following steps:**</span></span>

1. <span data-ttu-id="adb62-153">在 Azure 傳統入口網站中的 [Soonr Workplace] 應用程式整合頁面上，按一下 [設定單一登入] 來開啟 [設定單一登入] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="adb62-153">In the Azure classic portal, on the **Soonr Workplace** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>

    ![設定單一登入][6] 

2. <span data-ttu-id="adb62-155">在 [要如何讓使用者登入 Soonr Workplace] 頁面上，選取 [Azure AD 單一登入]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="adb62-155">On the **How would you like users to sign on to Soonr Workplace** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![設定單一登入](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_03.png) 

3. <span data-ttu-id="adb62-157">在 [設定應用程式設定]  對話方塊頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="adb62-157">On the **Configure App Settings** dialog page, perform the following steps:.</span></span>

    ![設定單一登入](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_04.png) 

    <span data-ttu-id="adb62-159">a.</span><span class="sxs-lookup"><span data-stu-id="adb62-159">a.</span></span> <span data-ttu-id="adb62-160">在 [登入 URL] 文字方塊中，以下列模式輸入 URL：`https://<server-name>.soonr.com/singlesignon/saml/SSO`。</span><span class="sxs-lookup"><span data-stu-id="adb62-160">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.</span></span>

    <span data-ttu-id="adb62-161">b.</span><span class="sxs-lookup"><span data-stu-id="adb62-161">b.</span></span> <span data-ttu-id="adb62-162">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="adb62-162">Click **Next**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="adb62-163">請注意，這不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="adb62-163">Please note that this is not the real value.</span></span> <span data-ttu-id="adb62-164">您必須使用實際的「登入 URL」來更新此值。</span><span class="sxs-lookup"><span data-stu-id="adb62-164">You have to update this value with the actual Sign On URL.</span></span> <span data-ttu-id="adb62-165">請連絡 Soonr Workplace 支援小組以取得此值。</span><span class="sxs-lookup"><span data-stu-id="adb62-165">Contact Soonr Workplace support team to get this value.</span></span>

4. <span data-ttu-id="adb62-166">於 [在 Soonr Workplace 上設定單一登入] 頁面上，按 [下載中繼資料]，然後將檔案儲存在您的電腦上：</span><span class="sxs-lookup"><span data-stu-id="adb62-166">On the **Configure single sign-on at Soonr Workplace** page, click **Download metadata** and then save the file on your computer:</span></span>

    ![設定單一登入](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_05.png) 

5. <span data-ttu-id="adb62-168">若要為您的應用程式設定 SSO，請連絡 Soonr Workplace 支援小組並提供下列資訊：</span><span class="sxs-lookup"><span data-stu-id="adb62-168">To get SSO configured for your application, contact your Soonr Workplace support team and provide them with the following:</span></span> 

    <span data-ttu-id="adb62-169">•  已下載的**中繼資料**檔案</span><span class="sxs-lookup"><span data-stu-id="adb62-169">•  The downloaded **Metadata** file</span></span>

    <span data-ttu-id="adb62-170">•  **簽發者 URL**</span><span class="sxs-lookup"><span data-stu-id="adb62-170">•  The **Issuer URL**</span></span>

    <span data-ttu-id="adb62-171">• **SAML SSO URL**</span><span class="sxs-lookup"><span data-stu-id="adb62-171">•  The **SAML SSO URL**</span></span>

    <span data-ttu-id="adb62-172">•  **單一登出服務 URL**</span><span class="sxs-lookup"><span data-stu-id="adb62-172">•  The **Single Sign-Out Service URL**</span></span>

    >[!NOTE]
    ><span data-ttu-id="adb62-173"><a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask 工作場所</a>已取代此應用程式，您可以參考<a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">這個</a>教學課程，以了解如何使用 Azure AD 來設定應用程式。</span><span class="sxs-lookup"><span data-stu-id="adb62-173">This application is superseded by <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask Workplace</a> and you can refer <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">this</a> tutorial for configuring the application with Azure AD.</span></span>
   
6. <span data-ttu-id="adb62-174">在 Azure 傳統入口網站中，選取單一登入設定確認，然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="adb62-174">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>

    ![Azure AD 單一登入][10]

7. <span data-ttu-id="adb62-176">在 [單一登入確認] 頁面上，按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="adb62-176">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
  
    ![Azure AD 單一登入][11]



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="adb62-178">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="adb62-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="adb62-179">本節目標是在 Azure 傳統入口網站中建立名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="adb62-179">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

![建立 Azure AD 使用者][20]

<span data-ttu-id="adb62-181">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="adb62-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="adb62-182">在 **Azure 傳統入口網站**中，按一下左方瀏覽窗格的 [Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="adb62-182">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-soonr-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="adb62-184">從 [目錄]  清單中，選取要啟用目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="adb62-184">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="adb62-185">若要顯示使用者清單，請按一下頂端功能表的 [使用者] 。</span><span class="sxs-lookup"><span data-stu-id="adb62-185">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-soonr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="adb62-187">若要開啟 [新增使用者] 對話方塊，請按一下底部工具列上的 [新增使用者]。</span><span class="sxs-lookup"><span data-stu-id="adb62-187">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-soonr-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="adb62-189">在 [告訴我們這位使用者]  對話方塊頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="adb62-189">On the **Tell us about this user** dialog page, perform the following steps:</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-soonr-tutorial/create_aaduser_05.png) 

    <span data-ttu-id="adb62-191">a.</span><span class="sxs-lookup"><span data-stu-id="adb62-191">a.</span></span> <span data-ttu-id="adb62-192">針對 [使用者類型]，選取 [您組織中的新使用者]。</span><span class="sxs-lookup"><span data-stu-id="adb62-192">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="adb62-193">b.</span><span class="sxs-lookup"><span data-stu-id="adb62-193">b.</span></span> <span data-ttu-id="adb62-194">在 [使用者名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="adb62-194">In the User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="adb62-195">c.</span><span class="sxs-lookup"><span data-stu-id="adb62-195">c.</span></span> <span data-ttu-id="adb62-196">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="adb62-196">Click **Next**.</span></span>

6.  <span data-ttu-id="adb62-197">在 [使用者設定檔]  對話方塊頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="adb62-197">On the **User Profile** dialog page, perform the following steps:</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-soonr-tutorial/create_aaduser_06.png) 

    <span data-ttu-id="adb62-199">a.</span><span class="sxs-lookup"><span data-stu-id="adb62-199">a.</span></span> <span data-ttu-id="adb62-200">在 [名字] 文字方塊中，輸入 **Britta**。</span><span class="sxs-lookup"><span data-stu-id="adb62-200">In the **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="adb62-201">b.</span><span class="sxs-lookup"><span data-stu-id="adb62-201">b.</span></span> <span data-ttu-id="adb62-202">在 [姓氏] 文字方塊中，輸入 **Simon**。</span><span class="sxs-lookup"><span data-stu-id="adb62-202">In the **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="adb62-203">c.</span><span class="sxs-lookup"><span data-stu-id="adb62-203">c.</span></span> <span data-ttu-id="adb62-204">在 [顯示名稱] 文字方塊中，輸入 **Britta Simon**。</span><span class="sxs-lookup"><span data-stu-id="adb62-204">In the **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="adb62-205">d.</span><span class="sxs-lookup"><span data-stu-id="adb62-205">d.</span></span> <span data-ttu-id="adb62-206">在 [角色] 清單中選取 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="adb62-206">In the **Role** list, select **User**.</span></span>

    <span data-ttu-id="adb62-207">e.</span><span class="sxs-lookup"><span data-stu-id="adb62-207">e.</span></span> <span data-ttu-id="adb62-208">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="adb62-208">Click **Next**.</span></span>

7. <span data-ttu-id="adb62-209">在 [取得暫時密碼] 對話方塊頁面上，按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="adb62-209">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-soonr-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="adb62-211">在 [取得暫時密碼]  對話方塊頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="adb62-211">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-soonr-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="adb62-213">a.</span><span class="sxs-lookup"><span data-stu-id="adb62-213">a.</span></span> <span data-ttu-id="adb62-214">記下 [新密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="adb62-214">Write down the value of the **New Password**.</span></span>

    <span data-ttu-id="adb62-215">b.</span><span class="sxs-lookup"><span data-stu-id="adb62-215">b.</span></span> <span data-ttu-id="adb62-216">按一下頁面底部的 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="adb62-216">Click **Complete**.</span></span>   



### <a name="creating-a-soonr-workplace-test-user"></a><span data-ttu-id="adb62-217">建立 Soonr Workplace 測試使用者</span><span class="sxs-lookup"><span data-stu-id="adb62-217">Creating a Soonr Workplace test user</span></span>

<span data-ttu-id="adb62-218">本節的目標是在 Soonr Workplace 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="adb62-218">The objective of this section is to create a user called Britta Simon in Soonr Workplace.</span></span> <span data-ttu-id="adb62-219">請與 Soonr Workplace 支援小組合作，在平台中建立使用者。</span><span class="sxs-lookup"><span data-stu-id="adb62-219">Please work with Soonr Workplace support team to create a user in the platform.</span></span> <span data-ttu-id="adb62-220">您可以從<a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">這裡</a>向 Sooner 提出支援票證。</span><span class="sxs-lookup"><span data-stu-id="adb62-220">You can raise the support ticket with Soonr from <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">here</a>.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="adb62-221">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="adb62-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="adb62-222">本節的目標是授與 Britta Simon 對 Soonr Workplace 的存取權，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="adb62-222">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Soonr Workplace.</span></span>

![指派使用者][200] 

<span data-ttu-id="adb62-224">**若要將 Britta Simon 指派到 Soonr Workplace，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="adb62-224">**To assign Britta Simon to Soonr Workplace, perform the following steps:**</span></span>

1. <span data-ttu-id="adb62-225">在 Azure 傳統入口網站中，若要開啟應用程式檢視，請在目錄檢視中，按一下頂端功能表中的 [應用程式]  。</span><span class="sxs-lookup"><span data-stu-id="adb62-225">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="adb62-227">在應用程式清單中，選取 [Soonr Workplace] 。</span><span class="sxs-lookup"><span data-stu-id="adb62-227">In the applications list, select **Soonr Workplace**.</span></span>

    ![設定單一登入](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_50.png) 

1. <span data-ttu-id="adb62-229">在頂端的功能表中，按一下 [使用者] 。</span><span class="sxs-lookup"><span data-stu-id="adb62-229">In the menu on the top, click **Users**.</span></span>

    ![指派使用者][203] 

1. <span data-ttu-id="adb62-231">在 [使用者] 清單中，選取 [Britta Simon] 。</span><span class="sxs-lookup"><span data-stu-id="adb62-231">In the Users list, select **Britta Simon**.</span></span>

2. <span data-ttu-id="adb62-232">在底部的工具列中，按一下 [指派] 。</span><span class="sxs-lookup"><span data-stu-id="adb62-232">In the toolbar on the bottom, click **Assign**.</span></span>

    ![指派使用者][205]



### <a name="testing-single-sign-on"></a><span data-ttu-id="adb62-234">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="adb62-234">Testing single sign-on</span></span>

<span data-ttu-id="adb62-235">本節的目標是要使用存取面板來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="adb62-235">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="adb62-236">當您在存取面板中按一下 [Soonr Workplace] 圖格時，應該會自動登入您的 Soonr Workplace 應用程式。</span><span class="sxs-lookup"><span data-stu-id="adb62-236">When you click the Soonr Workplace tile in the Access Panel, you should get automatically signed-on to your Soonr Workplace application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="adb62-237">其他資源</span><span class="sxs-lookup"><span data-stu-id="adb62-237">Additional resources</span></span>

* [<span data-ttu-id="adb62-238">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="adb62-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="adb62-239">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="adb62-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_205.png
