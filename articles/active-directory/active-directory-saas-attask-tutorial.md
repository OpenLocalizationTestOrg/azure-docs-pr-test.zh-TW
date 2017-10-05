---
title: "教學課程： Azure Active Directory 整合與@Task|Microsoft 文件"
description: "了解如何設定 Azure Active Directory 與 @Task 之間的單一登入。"
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: ebb19ca6cbaf04106fbce937d95651e709854cfd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-task"></a><span data-ttu-id="1d065-103">教學課程：Azure Active Directory 與 @Task 整合</span><span class="sxs-lookup"><span data-stu-id="1d065-103">Tutorial: Azure Active Directory integration with @Task</span></span>
<span data-ttu-id="1d065-104">本教學課程旨在說明如何整合 @Task 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="1d065-104">The objective of this tutorial is to show you how to integrate @Task with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="1d065-105">@Task 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="1d065-105">Integrating @Task with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="1d065-106">您可以在 Azure AD 中控制可存取 @Task 的人員</span><span class="sxs-lookup"><span data-stu-id="1d065-106">You can control in Azure AD who has access to @Task</span></span>
* <span data-ttu-id="1d065-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 @Task (單一登入)</span><span class="sxs-lookup"><span data-stu-id="1d065-107">You can enable your users to automatically get signed-on to @Task (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="1d065-108">您可以在 Azure 傳統入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="1d065-108">You can manage your accounts in one central location - the Azure classic Portal</span></span>

<span data-ttu-id="1d065-109">若您想了解 SaaS app 與 Azure AD 整合的更多詳細資訊，請參閱 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="1d065-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1d065-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="1d065-110">Prerequisites</span></span>
<span data-ttu-id="1d065-111">若要設定與 Azure AD 整合@Task，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="1d065-111">To configure Azure AD integration with @Task, you need the following items:</span></span>

* <span data-ttu-id="1d065-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1d065-112">An Azure AD subscription</span></span>
* <span data-ttu-id="1d065-113">啟用 @Task 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1d065-113">An @Task single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1d065-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="1d065-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="1d065-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="1d065-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="1d065-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="1d065-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="1d065-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="1d065-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="1d065-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="1d065-118">Scenario Description</span></span>
<span data-ttu-id="1d065-119">此教學課程的目標是讓您在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1d065-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="1d065-120">本教學課程中說明的案例由三個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="1d065-120">The scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="1d065-121">從資源庫新增 @Task</span><span class="sxs-lookup"><span data-stu-id="1d065-121">Adding @Task from the gallery</span></span> 
2. <span data-ttu-id="1d065-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1d065-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-task-from-the-gallery"></a><span data-ttu-id="1d065-123">從資源庫新增 @Task</span><span class="sxs-lookup"><span data-stu-id="1d065-123">Adding @Task from the gallery</span></span>
<span data-ttu-id="1d065-124">若要設定將 @Task 整合到 Azure AD 中，您需要從資源庫將 @Task 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="1d065-124">To configure the integration of @Task into Azure AD, you need to add @Task from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1d065-125">**若要從資源庫新增 @Task，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="1d065-125">**To add @Task from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1d065-126">在 **Azure 傳統入口網站**中，按一下左方瀏覽窗格的 [Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="1d065-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1] 
2. <span data-ttu-id="1d065-128">從 [目錄]  清單中，選取要啟用目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="1d065-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="1d065-129">若要開啟應用程式檢視，請在目錄檢視中，按一下頂端功能表中的 [應用程式]  。</span><span class="sxs-lookup"><span data-stu-id="1d065-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![應用程式][2] 
4. <span data-ttu-id="1d065-131">按一下頁面底部的 [新增]  。</span><span class="sxs-lookup"><span data-stu-id="1d065-131">Click **Add** at the bottom of the page.</span></span>
   
    ![應用程式][3] 
5. <span data-ttu-id="1d065-133">在 [欲執行動作] 對話方塊上，按一下 [從資源庫中新增應用程式]。</span><span class="sxs-lookup"><span data-stu-id="1d065-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![應用程式][4] 
6. <span data-ttu-id="1d065-135">在搜尋方塊中，輸入 **@Task**。</span><span class="sxs-lookup"><span data-stu-id="1d065-135">In the search box, type **@Task**.</span></span>
   
    ![應用程式][5] 
7. <span data-ttu-id="1d065-137">在結果窗格中，選取 [@Task]，然後按一下 [完成] 以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="1d065-137">In the results pane, select **@Task**, and then click **Complete** to add the application.</span></span>
   
    ![應用程式][30] 

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1d065-139">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1d065-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1d065-140">本節的目標是要說明如何以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 @Task 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1d065-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with @Task based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1d065-141">若要讓單一登入運作，Azure AD 必須知道與 @Task 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="1d065-141">For single sign-on to work, Azure AD needs to know what the counterpart user in @Task to an user in Azure AD is.</span></span> <span data-ttu-id="1d065-142">換句話說，必須建立 Azure AD 使用者和 @Task 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="1d065-142">In other words, a link relationship between an Azure AD user and the related user in @Task needs to be established.</span></span>   
<span data-ttu-id="1d065-143">建立此連結關聯性的方法是將 Azure AD 中**使用者名稱**的值指定為 @Task 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="1d065-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in @Task.</span></span>

<span data-ttu-id="1d065-144">設定和測試 Azure AD 單一登入與@Task，您必須完成下列的建置組塊：</span><span class="sxs-lookup"><span data-stu-id="1d065-144">To configure and test Azure AD single sign-on with @Task, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1d065-145">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="1d065-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1d065-146">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1d065-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1d065-147">**[建立 @Tasktest 使用者](#creating-a-halogen-software-test-user)** - 在 @Taskthat 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表 Britta Simon 的項目連結。</span><span class="sxs-lookup"><span data-stu-id="1d065-147">**[Creating a @Tasktest user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in @Taskthat is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="1d065-148">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1d065-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1d065-149">**[測試單一登入](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="1d065-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1d065-150">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1d065-150">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="1d065-151">本節的目標是要在 Azure 傳統入口網站中啟用 Azure AD 單一登入，並在您的 @Task 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="1d065-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your @Task application.</span></span>

<span data-ttu-id="1d065-152">**若要設定 Azure AD 單一登入與@Task，執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="1d065-152">**To configure Azure AD single sign-on with @Task, perform the following steps:**</span></span>

1. <span data-ttu-id="1d065-153">在 Azure 傳統入口網站的 **@Task** 應用程式整合頁面上，按一下 [設定單一登入] 來開啟 [設定單一登入] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="1d065-153">In the Azure classic portal, on the **@Task** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![設定單一登入][6] 
2. <span data-ttu-id="1d065-155">在 [要如何讓使用者登入 @Task] 頁面上，選取 [Azure AD 單一登入]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="1d065-155">On the **How would you like users to sign on to @Task** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD 單一登入][7] 
3. <span data-ttu-id="1d065-157">在 [設定應用程式設定]  對話方塊頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1d065-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![設定 App 設定][8] 
   
     <span data-ttu-id="1d065-159">a.</span><span class="sxs-lookup"><span data-stu-id="1d065-159">a.</span></span> <span data-ttu-id="1d065-160">在 [登入 URL] 文字方塊中，輸入您的使用者用來登入 @Task 應用程式的 URL (例如：*https://<Tenant name>.attask-ondemand.com*。</span><span class="sxs-lookup"><span data-stu-id="1d065-160">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your @Task application (e.g.:*https://<Tenant name>.attask-ondemand.com*).</span></span>
   
     <span data-ttu-id="1d065-161">b.</span><span class="sxs-lookup"><span data-stu-id="1d065-161">b.</span></span> <span data-ttu-id="1d065-162">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="1d065-162">Click **Next**.</span></span>
4. <span data-ttu-id="1d065-163">在 [設定在 @Task 單一登入] 頁面上，按一下 [下載中繼資料]，將中繼資料檔儲存在您的本機電腦中，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="1d065-163">On the **Configure single sign-on at @Task** page, click **Download metadata**, save the metadata file locally on your computer, and then click **Next**.</span></span>
   
    ![何謂 Azure AD Connect][9] 
5. <span data-ttu-id="1d065-165">以系統管理員身分登入您的 @Task 公司網站。</span><span class="sxs-lookup"><span data-stu-id="1d065-165">Sign-on to your @Task company site as administrator.</span></span>
6. <span data-ttu-id="1d065-166">移至 [單一登入組態] 。</span><span class="sxs-lookup"><span data-stu-id="1d065-166">Go to **Single Sign On Configuration**.</span></span>
7. <span data-ttu-id="1d065-167">在 [單一登入]  對話方塊中，執行下列步驟</span><span class="sxs-lookup"><span data-stu-id="1d065-167">On the **Single Sign-On** dialog, perform the following steps</span></span>
   
    ![設定單一登入][23]
   
    <span data-ttu-id="1d065-169">a.</span><span class="sxs-lookup"><span data-stu-id="1d065-169">a.</span></span> <span data-ttu-id="1d065-170">針對 [類型]，選取 [SAML 2.0]。</span><span class="sxs-lookup"><span data-stu-id="1d065-170">As **Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="1d065-171">b.</span><span class="sxs-lookup"><span data-stu-id="1d065-171">b.</span></span> <span data-ttu-id="1d065-172">選取 [服務提供者識別碼]。</span><span class="sxs-lookup"><span data-stu-id="1d065-172">Select **Service Provider ID**.</span></span>
   
    <span data-ttu-id="1d065-173">c.</span><span class="sxs-lookup"><span data-stu-id="1d065-173">c.</span></span> <span data-ttu-id="1d065-174">在 Azure 傳統入口網站上，複製 [遠端登入 URL]，然後將它貼到 [遠端登入 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="1d065-174">On the Azure classic portal, copy the **Remote Login URL**, and then paste it into the **Login Portal URL** textbox.</span></span>
   
    <span data-ttu-id="1d065-175">d.</span><span class="sxs-lookup"><span data-stu-id="1d065-175">d.</span></span> <span data-ttu-id="1d065-176">在 Azure 傳統入口網站上，複製 [單一登出服務 URL]，然後將它貼到 [登出 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="1d065-176">On the Azure classic portal, copy the **Single Sign-Out Service URL**, and then paste it into the **Sign-Out URL** textbox.</span></span>
   
    <span data-ttu-id="1d065-177">e.</span><span class="sxs-lookup"><span data-stu-id="1d065-177">e.</span></span> <span data-ttu-id="1d065-178">在 Azure 傳統入口網站上，複製 [變更密碼 URL]，然後將它貼到 [變更密碼 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="1d065-178">On the Azure classic portal, copy the **Change Password URL**, and then paste it into the **Change Password URL** textbox.</span></span>
   
    <span data-ttu-id="1d065-179">f.</span><span class="sxs-lookup"><span data-stu-id="1d065-179">f.</span></span> <span data-ttu-id="1d065-180">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="1d065-180">Click **Save**.</span></span>
8. <span data-ttu-id="1d065-181">在 Azure 傳統入口網站中，選取單一登入設定確認，然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="1d065-181">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![何謂 Azure AD Connect][10]
9. <span data-ttu-id="1d065-183">在 [單一登入確認] 頁面上，按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="1d065-183">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![何謂 Azure AD Connect][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1d065-185">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1d065-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="1d065-186">本節目標是在 Azure 傳統入口網站中建立名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="1d065-186">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

![建立 Azure AD 使用者][20]

<span data-ttu-id="1d065-188">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="1d065-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1d065-189">在 **Azure 傳統入口網站**中，按一下左方瀏覽窗格的 [Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="1d065-189">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-attask-tutorial/create_aaduser_02.png) 
2. <span data-ttu-id="1d065-191">從 [目錄]  清單中，選取要啟用目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="1d065-191">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="1d065-192">若要顯示使用者清單，請按一下頂端功能表的 [使用者] 。</span><span class="sxs-lookup"><span data-stu-id="1d065-192">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-attask-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="1d065-194">若要開啟 [新增使用者] 對話方塊，請按一下底部工具列上的 [新增使用者]。</span><span class="sxs-lookup"><span data-stu-id="1d065-194">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-attask-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="1d065-196">在 [告訴我們這位使用者]  對話方塊頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1d065-196">On the **Tell us about this user** dialog page, perform the following steps:</span></span> 
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-attask-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="1d065-198">a.</span><span class="sxs-lookup"><span data-stu-id="1d065-198">a.</span></span> <span data-ttu-id="1d065-199">針對 [使用者類型]，選取 [您組織中的新使用者]。</span><span class="sxs-lookup"><span data-stu-id="1d065-199">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="1d065-200">b.</span><span class="sxs-lookup"><span data-stu-id="1d065-200">b.</span></span> <span data-ttu-id="1d065-201">在 [使用者名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="1d065-201">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="1d065-202">c.</span><span class="sxs-lookup"><span data-stu-id="1d065-202">c.</span></span> <span data-ttu-id="1d065-203">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="1d065-203">Click **Next**.</span></span>
6. <span data-ttu-id="1d065-204">在 [使用者設定檔]  對話方塊頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1d065-204">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-attask-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="1d065-206">a.</span><span class="sxs-lookup"><span data-stu-id="1d065-206">a.</span></span> <span data-ttu-id="1d065-207">在 [名字] 文字方塊中，輸入 **Britta**。</span><span class="sxs-lookup"><span data-stu-id="1d065-207">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="1d065-208">b.</span><span class="sxs-lookup"><span data-stu-id="1d065-208">b.</span></span> <span data-ttu-id="1d065-209">在 [姓氏] 文字方塊中，輸入 **Simon**。</span><span class="sxs-lookup"><span data-stu-id="1d065-209">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="1d065-210">c.</span><span class="sxs-lookup"><span data-stu-id="1d065-210">c.</span></span> <span data-ttu-id="1d065-211">在 [顯示名稱] 文字方塊中，輸入 **Britta Simon**。</span><span class="sxs-lookup"><span data-stu-id="1d065-211">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="1d065-212">d.</span><span class="sxs-lookup"><span data-stu-id="1d065-212">d.</span></span> <span data-ttu-id="1d065-213">在 [角色] 清單中選取 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="1d065-213">In the **Role** list, select **User**.</span></span>

    <span data-ttu-id="1d065-214">e.</span><span class="sxs-lookup"><span data-stu-id="1d065-214">e.</span></span> <span data-ttu-id="1d065-215">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="1d065-215">Click **Next**.</span></span>

7. <span data-ttu-id="1d065-216">在 [取得暫時密碼] 對話方塊頁面上，按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="1d065-216">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-attask-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="1d065-218">在 [取得暫時密碼]  對話方塊頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1d065-218">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-attask-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="1d065-220">a.</span><span class="sxs-lookup"><span data-stu-id="1d065-220">a.</span></span> <span data-ttu-id="1d065-221">記下 [新密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="1d065-221">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="1d065-222">b.</span><span class="sxs-lookup"><span data-stu-id="1d065-222">b.</span></span> <span data-ttu-id="1d065-223">按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="1d065-223">Click **Complete**.</span></span>   

### <a name="creating-an-task-test-user"></a><span data-ttu-id="1d065-224">建立 @Task 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1d065-224">Creating an @Task test user</span></span>
<span data-ttu-id="1d065-225">本節目標是在 @Task 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="1d065-225">The objective of this section is to create a user called Britta Simon in @Task.</span></span>

<span data-ttu-id="1d065-226">**若要建立使用者，在呼叫許 Simon @Task，執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="1d065-226">**To create a user called Britta Simon in @Task, perform the following steps:**</span></span>

1. <span data-ttu-id="1d065-227">以系統管理員身分登入您的 @Task 公司網站。</span><span class="sxs-lookup"><span data-stu-id="1d065-227">Sign on to your @Task company site as administrator.</span></span>
2. <span data-ttu-id="1d065-228">在頂端的功能表中，按一下 [人員] 。</span><span class="sxs-lookup"><span data-stu-id="1d065-228">In the menu on the top, click **People**.</span></span>
3. <span data-ttu-id="1d065-229">按一下 [新增人員] 。</span><span class="sxs-lookup"><span data-stu-id="1d065-229">Click **New Person**.</span></span> 
4. <span data-ttu-id="1d065-230">在 [新增人員] 對話方塊上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1d065-230">On the New Person dialog, perform the following steps:</span></span>
   
    ![建立 @Task 測試使用者][21] 
   
    <span data-ttu-id="1d065-232">a.</span><span class="sxs-lookup"><span data-stu-id="1d065-232">a.</span></span> <span data-ttu-id="1d065-233">在 [名字] 文字方塊中，輸入 "Britta"。</span><span class="sxs-lookup"><span data-stu-id="1d065-233">In the **First Name** textbox, type "Britta".</span></span>
   
    <span data-ttu-id="1d065-234">b.</span><span class="sxs-lookup"><span data-stu-id="1d065-234">b.</span></span> <span data-ttu-id="1d065-235">在 [姓氏] 文字方塊中，輸入 "Simon"。</span><span class="sxs-lookup"><span data-stu-id="1d065-235">In the **Last Name** textbox, type "Simon".</span></span>
   
    <span data-ttu-id="1d065-236">c.</span><span class="sxs-lookup"><span data-stu-id="1d065-236">c.</span></span> <span data-ttu-id="1d065-237">在 [電子郵件地址] 文字方塊中，輸入 Azure Active Directory 中 Britta Simon 的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="1d065-237">In the **Email Address** textbox, type Britta Simon's email address in Azure Active Directory.</span></span>
   
    <span data-ttu-id="1d065-238">d.</span><span class="sxs-lookup"><span data-stu-id="1d065-238">d.</span></span> <span data-ttu-id="1d065-239">按一下 [新增人員] 。</span><span class="sxs-lookup"><span data-stu-id="1d065-239">Click **Add Person**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1d065-240">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1d065-240">Assigning the Azure AD test user</span></span>
<span data-ttu-id="1d065-241">本節目標是授與 Britta Simon 對 @Task 的存取權，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1d065-241">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to @Task.</span></span>

![指派使用者][200] 

<span data-ttu-id="1d065-243">**若要指派至許 Simon @Task，執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="1d065-243">**To assign Britta Simon to @Task, perform the following steps:**</span></span>

1. <span data-ttu-id="1d065-244">在 Azure 傳統入口網站中，若要開啟應用程式檢視，請在目錄檢視中，按一下頂端功能表中的 [應用程式]  。</span><span class="sxs-lookup"><span data-stu-id="1d065-244">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![指派使用者][201] 
2. <span data-ttu-id="1d065-246">在應用程式清單中，選取 [@Task] 。</span><span class="sxs-lookup"><span data-stu-id="1d065-246">In the applications list, select **@Task**.</span></span>
   
    ![指派使用者][202] 
3. <span data-ttu-id="1d065-248">在頂端的功能表中，按一下 [使用者] 。</span><span class="sxs-lookup"><span data-stu-id="1d065-248">In the menu on the top, click **Users**.</span></span>
   
    ![指派使用者][203] 
4. <span data-ttu-id="1d065-250">在 [使用者] 清單中，選取 [Britta Simon] 。</span><span class="sxs-lookup"><span data-stu-id="1d065-250">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="1d065-251">在底部的工具列中，按一下 [指派] 。</span><span class="sxs-lookup"><span data-stu-id="1d065-251">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![指派使用者][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="1d065-253">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="1d065-253">Testing Single Sign-On</span></span>
<span data-ttu-id="1d065-254">本節的目標是要使用存取面板來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="1d065-254">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="1d065-255">當您在存取面板中按一下 @Task 圖格時，應該會自動登入您的 @Task 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1d065-255">When you click the @Task tile in the Access Panel, you should get automatically signed-on to your @Task application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1d065-256">其他資源</span><span class="sxs-lookup"><span data-stu-id="1d065-256">Additional Resources</span></span>
* [<span data-ttu-id="1d065-257">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="1d065-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1d065-258">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="1d065-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-attask-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-attask-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-attask-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-attask-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_01.png
[30]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_02.png


[6]: ./media/active-directory-saas-attask-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_03.png
[8]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_04.png
[9]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_05.png
[10]: ./media/active-directory-saas-attask-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-attask-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-attask-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_08.png


[23]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_06.png

[200]: ./media/active-directory-saas-attask-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-attask-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_09.png
[203]: ./media/active-directory-saas-attask-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-attask-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-attask-tutorial/tutorial_general_205.png






