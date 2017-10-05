---
title: "教學課程：Azure Active Directory 與 Bynder 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Bynder 之間的單一登入。"
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 4fb0ab26-b3b9-420a-8072-a0be80ea021e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 6786d7eb6a11405278ef7267f25279f9e39b3bde
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bynder"></a><span data-ttu-id="d9727-103">教學課程：Azure Active Directory 與 Bynder 整合</span><span class="sxs-lookup"><span data-stu-id="d9727-103">Tutorial: Azure Active Directory integration with Bynder</span></span>
<span data-ttu-id="d9727-104">本教學課程旨在說明如何整合 Bynder 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="d9727-104">The objective of this tutorial is to show you how to integrate Bynder with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d9727-105">將 Bynder 與 Azure AD 整合可提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="d9727-105">Integrating Bynder with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="d9727-106">您可以在 Azure AD 中控制可存取 Bynder 的人員</span><span class="sxs-lookup"><span data-stu-id="d9727-106">You can control in Azure AD who has access to Bynder</span></span>
* <span data-ttu-id="d9727-107">您可以讓使用者使用其 Azure AD 帳戶自動登入 Bynder 單一登入 (SSO)</span><span class="sxs-lookup"><span data-stu-id="d9727-107">You can enable your users to automatically get signed-on to Bynder single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="d9727-108">您可以在 Azure 傳統入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="d9727-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="d9727-109">若您想了解 SaaS app 與 Azure AD 整合的更多詳細資訊，請參閱 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="d9727-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9727-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="d9727-110">Prerequisites</span></span>
<span data-ttu-id="d9727-111">若要設定 Azure AD 與 Bynder 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="d9727-111">To configure Azure AD integration with Bynder, you need the following items:</span></span>

* <span data-ttu-id="d9727-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d9727-112">An Azure AD subscription</span></span>
* <span data-ttu-id="d9727-113">已啟用 Bynder 單一登入 (SSO) 的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d9727-113">A Bynder single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="d9727-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="d9727-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="d9727-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="d9727-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="d9727-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="d9727-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="d9727-117">如果您沒有 Azure AD 試用環境，您可以取得[一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="d9727-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d9727-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="d9727-118">Scenario description</span></span>
<span data-ttu-id="d9727-119">本教學課程的目標是讓您在測試環境中測試 Microsoft Azure AD SSO。</span><span class="sxs-lookup"><span data-stu-id="d9727-119">The objective of this tutorial is to enable you to test Microsoft Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="d9727-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="d9727-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d9727-121">從資源庫新增 Bynder</span><span class="sxs-lookup"><span data-stu-id="d9727-121">Adding Bynder from the gallery</span></span>
2. <span data-ttu-id="d9727-122">設定並測試 Microsoft Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="d9727-122">Configuring and testing Microsoft Azure AD SSO</span></span>

## <a name="add-bynder-from-the-gallery"></a><span data-ttu-id="d9727-123">從資源庫新增 Bynder</span><span class="sxs-lookup"><span data-stu-id="d9727-123">Add Bynder from the gallery</span></span>
<span data-ttu-id="d9727-124">若要設定將 Bynder 整合到 Azure AD 中，您需要從資源庫將 Bynder 新增到受管理的 SaaS 應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="d9727-124">To configure the integration of Bynder into Azure AD, you need to add Bynder from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d9727-125">**若要從資源庫新增 Bynder，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d9727-125">**To add Bynder from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d9727-126">在 **Azure 傳統入口網站**中，按一下左方瀏覽窗格的 [Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="d9727-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="d9727-128">從 [目錄]  清單中，選取要啟用目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="d9727-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="d9727-129">若要開啟應用程式檢視，請在目錄檢視中，按一下頂端功能表中的 [應用程式]  。</span><span class="sxs-lookup"><span data-stu-id="d9727-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![應用程式][2]
4. <span data-ttu-id="d9727-131">按一下頁面底部的 [新增]  。</span><span class="sxs-lookup"><span data-stu-id="d9727-131">Click **Add** at the bottom of the page.</span></span>
   
    ![應用程式][3]
5. <span data-ttu-id="d9727-133">在 [欲執行動作] 對話方塊上，按一下 [從資源庫中新增應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d9727-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![應用程式][4]
6. <span data-ttu-id="d9727-135">在搜尋方塊中，輸入 **Bynder**。</span><span class="sxs-lookup"><span data-stu-id="d9727-135">In the search box, type **Bynder**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_01.png)
7. <span data-ttu-id="d9727-137">在結果窗格中，選取 [Bynder]，然後按一下 [完成] 以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="d9727-137">In the results panel, select **Bynder**, and then click **Complete** to add the application.</span></span>
   
    ![選取資源庫中的應用程式](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_001.png)

## <a name="configure-and-test-microsoft-azure-ad-sso"></a><span data-ttu-id="d9727-139">設定並測試 Microsoft Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="d9727-139">Configure and test Microsoft Azure AD SSO</span></span>
<span data-ttu-id="d9727-140">本節的目標是要說明如何以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Bynder 搭配運作的 Microsoft Azure AD SSO。</span><span class="sxs-lookup"><span data-stu-id="d9727-140">The objective of this section is to show you how to configure and test Microsoft Azure AD SSO with Bynder based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d9727-141">若要讓 SSO 運作，Azure AD 必須知道 Bynder 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="d9727-141">For SSO to work, Azure AD needs to know what the counterpart user in Bynder to an user in Azure AD is.</span></span> <span data-ttu-id="d9727-142">換句話說，必須建立 Azure AD 使用者和 Bynder 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="d9727-142">In other words, a link relationship between an Azure AD user and the related user in Bynder needs to be established.</span></span>

<span data-ttu-id="d9727-143">建立此連結關聯性的方法，是將 Azure AD 中**使用者名稱**的值，指派為 Bynder 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="d9727-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Bynder.</span></span>

<span data-ttu-id="d9727-144">若要設定及測試對 Bynder 的 Microsoft Azure AD SSO，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="d9727-144">To configure and test Microsoft Azure AD SSO with Bynder, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d9727-145">**[設定 Microsoft Azure AD 單一登入](#configuring-azure-ad-single-single-sign-on)** - 讓使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="d9727-145">**[Configuring Microsoft Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d9727-146">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Microsoft Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d9727-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Microsoft Azure AD Single Sign-On with Britta Simon.</span></span>
3. <span data-ttu-id="d9727-147">**[建立 Bynder 測試使用者](#creating-a-bynder-test-user)** - 在 Bynder 中建立 Britta Simon 的對應項目，且該項目必須與 Azure AD 中代表 Britta Simon 的項目連結。</span><span class="sxs-lookup"><span data-stu-id="d9727-147">**[Creating a Bynder test user](#creating-a-bynder-test-user)** - to have a counterpart of Britta Simon in Bynder that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="d9727-148">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Microsoft Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d9727-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Microsoft Azure AD Single Sign-On.</span></span>
5. <span data-ttu-id="d9727-149">**[測試單一登入](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="d9727-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-microsoft-azure-ad-sso"></a><span data-ttu-id="d9727-150">設定 Microsoft Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="d9727-150">Configuring Microsoft Azure AD SSO</span></span>
<span data-ttu-id="d9727-151">在本節中，您會在傳統入口網站中啟用 Microsoft Azure AD SSO，並在您的 Bynder 應用程式中設定 SSO。</span><span class="sxs-lookup"><span data-stu-id="d9727-151">In this section, you enable Microsoft Azure AD SSO in the classic portal and configure SSO in your Bynder application.</span></span>

<span data-ttu-id="d9727-152">**若要設定與 Bynder 搭配運作的 Microsoft Azure AD SSO，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d9727-152">**To configure Microsoft Azure AD SSO with Bynder, perform the following steps:**</span></span>

1. <span data-ttu-id="d9727-153">在傳統入口網站的 **Bynder** 應用程式整合頁面上，按一下 [設定單一登入] 來開啟 [設定單一登入] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="d9727-153">In the classic portal, on the **Bynder** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![設定單一登入][6] 
2. <span data-ttu-id="d9727-155">在 [要如何讓使用者登入 Bynder] 頁面上，選取 [Microsoft Azure AD 單一登入]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="d9727-155">On the **How would you like users to sign on to Bynder** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_03.png)
3. <span data-ttu-id="d9727-157">在 [設定應用程式設定] 對話方塊頁面上，如果您想要以 **IDP 起始模式**設定應用程式，請執行下列步驟，然後按 [下一步]：</span><span class="sxs-lookup"><span data-stu-id="d9727-157">On the **Configure App Settings** dialog page, If you wish to configure the application in **IDP initiated mode**, perform the following steps and click **Next**:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_04.png)
  1. <span data-ttu-id="d9727-159">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://<company name>.getbynder.com/sso/SAML/authenticate/`</span><span class="sxs-lookup"><span data-stu-id="d9727-159">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.getbynder.com/sso/SAML/authenticate/`</span></span>
  2. <span data-ttu-id="d9727-160">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="d9727-160">Click **Next**.</span></span>
4. <span data-ttu-id="d9727-161">如果您想要在 [設定應用程式設定] 對話方塊頁面上以 **SP 起始模式**設定應用程式，則請按一下 [顯示進階設定 (選擇性)]，然後輸入**登入 URL** 並按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="d9727-161">If you wish to configure the application in **SP initiated mode** on the **Configure App Settings** dialog page, then click on the **“Show advanced settings (optional)”** and then enter the **Sign On URL** and click **Next**.</span></span>

    ![設定單一登入](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_10.png)
  1. <span data-ttu-id="d9727-163">在 [登入 URL] 文字方塊中，以下列模式輸入 URL：`https://<company name>.getbynder.com/login/`</span><span class="sxs-lookup"><span data-stu-id="d9727-163">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.getbynder.com/login/`</span></span>
  2. <span data-ttu-id="d9727-164">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="d9727-164">Click **Next**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="d9727-165">本教學課程中的 [登入 URL] 值只是預留位置。</span><span class="sxs-lookup"><span data-stu-id="d9727-165">The value for the Sign On URL in this tutorial is just a placeholfer.</span></span> <span data-ttu-id="d9727-166">若要取得您環境的實際值，請連絡 Bynder。</span><span class="sxs-lookup"><span data-stu-id="d9727-166">To get the actual vlaue for your environment, contact Bynder.</span></span>
   >

5. <span data-ttu-id="d9727-167">在 [設定在 Bynder 單一登入] 頁面上，執行下列步驟，然後按 [下一步]：</span><span class="sxs-lookup"><span data-stu-id="d9727-167">On the **Configure single sign-on at Bynder** page, perform the following steps and click **Next**:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_05.png)  
  1. <span data-ttu-id="d9727-169">按一下 [下載中繼資料]，然後將檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="d9727-169">Click **Download metadata**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="d9727-170">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="d9727-170">Click **Next**.</span></span>
6. <span data-ttu-id="d9727-171">若要為您的應用程式設定 SSO，請連絡 Bynder 支援小組。</span><span class="sxs-lookup"><span data-stu-id="d9727-171">To get SSO configured for your application, contact your Bynder support team.</span></span> <span data-ttu-id="d9727-172">附加下載的中繼資料檔案，並與 Bynder 小組共用，以便在 Bynder 端設定 SSO。</span><span class="sxs-lookup"><span data-stu-id="d9727-172">Attach the downloaded metadata file and share it with Bynder team to set up SSO on their side.</span></span>
7. <span data-ttu-id="d9727-173">在傳統入口網站中，選取單一登入設定確認項目，然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="d9727-173">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD 單一登入][10]
8. <span data-ttu-id="d9727-175">在 [單一登入確認] 頁面上，按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="d9727-175">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD 單一登入][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d9727-177">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d9727-177">Create an Azure AD test user</span></span>
<span data-ttu-id="d9727-178">本節的目標是要在傳統入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="d9727-178">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][20]

<span data-ttu-id="d9727-180">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d9727-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d9727-181">在 **Azure 傳統入口網站**中，按一下左方瀏覽窗格的 [Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="d9727-181">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bynder-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="d9727-183">從 [目錄]  清單中，選取要啟用目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="d9727-183">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="d9727-184">若要顯示使用者清單，請按一下頂端功能表的 [使用者] 。</span><span class="sxs-lookup"><span data-stu-id="d9727-184">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bynder-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="d9727-186">若要開啟 [新增使用者] 對話方塊，請按一下底部工具列上的 [新增使用者]。</span><span class="sxs-lookup"><span data-stu-id="d9727-186">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bynder-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="d9727-188">在 [告訴我們這位使用者]  對話方塊頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d9727-188">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bynder-tutorial/create_aaduser_05.png)
  1. <span data-ttu-id="d9727-190">針對 [使用者類型]，選取 [您組織中的新使用者]。</span><span class="sxs-lookup"><span data-stu-id="d9727-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="d9727-191">在 [使用者名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="d9727-191">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="d9727-192">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="d9727-192">Click **Next**.</span></span>
6. <span data-ttu-id="d9727-193">在 [使用者設定檔]  對話方塊頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d9727-193">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![建立 Azure AD 測試使用者](./media/active-directory-saas-bynder-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="d9727-195">在 [名字] 文字方塊中，輸入 **Britta**。</span><span class="sxs-lookup"><span data-stu-id="d9727-195">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="d9727-196">在 [姓氏] 文字方塊中，輸入 **Simon**。</span><span class="sxs-lookup"><span data-stu-id="d9727-196">In the **Last Name** textbox, type, **Simon**.</span></span> 
  3. <span data-ttu-id="d9727-197">在 [顯示名稱] 文字方塊中，輸入 **Britta Simon**。</span><span class="sxs-lookup"><span data-stu-id="d9727-197">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="d9727-198">在 [角色] 清單中選取 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="d9727-198">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="d9727-199">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="d9727-199">Click **Next**.</span></span>
7. <span data-ttu-id="d9727-200">在 [取得暫時密碼] 對話方塊頁面上，按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="d9727-200">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bynder-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="d9727-202">在 [取得暫時密碼]  對話方塊頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d9727-202">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bynder-tutorial/create_aaduser_08.png)
   1. <span data-ttu-id="d9727-204">記下 [新密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="d9727-204">Write down the value of the **New Password**.</span></span>
   2. <span data-ttu-id="d9727-205">按一下頁面底部的 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="d9727-205">Click **Complete**.</span></span>   

### <a name="create-a-bynder-test-user"></a><span data-ttu-id="d9727-206">建立 Bynder 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d9727-206">Create a Bynder test user</span></span>
<span data-ttu-id="d9727-207">本節的目標是要在 Bynder 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="d9727-207">The objective of this section is to create a user called Britta Simon in Bynder.</span></span> <span data-ttu-id="d9727-208">Bynder 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="d9727-208">Bynder supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="d9727-209">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="d9727-209">There is no action item for you in this section.</span></span> <span data-ttu-id="d9727-210">嘗試存取 Bynder 時，如果使用者還不存在，就會建立新使用者。</span><span class="sxs-lookup"><span data-stu-id="d9727-210">A new user will be created during an attempt to access Bynder if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="d9727-211">如果您需要手動建立使用者，就必須連絡 Bynder 支援小組。</span><span class="sxs-lookup"><span data-stu-id="d9727-211">If you need to create an user manually, you need to contact the Bynder support team.</span></span> 
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="d9727-212">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d9727-212">Assign the Azure AD test user</span></span>
<span data-ttu-id="d9727-213">本節的目標是授與 Britta Simon 對 Bynder 的存取權，使她能夠使用 Azure SSO。</span><span class="sxs-lookup"><span data-stu-id="d9727-213">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Bynder.</span></span>

   ![指派使用者][200]

<span data-ttu-id="d9727-215">**如要將 Britta Simon 指派給 Bynder，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d9727-215">**To assign Britta Simon to Bynder, perform the following steps:**</span></span>

1. <span data-ttu-id="d9727-216">在傳統入口網站中，若要開啟應用程式檢視，請在目錄檢視中，按一下頂端功能表中的 [應用程式]  。</span><span class="sxs-lookup"><span data-stu-id="d9727-216">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![指派使用者][201]
2. <span data-ttu-id="d9727-218">在應用程式清單中，選取 [Bynder] 。</span><span class="sxs-lookup"><span data-stu-id="d9727-218">In the applications list, select **Bynder**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_50.png)
3. <span data-ttu-id="d9727-220">在頂端的功能表中，按一下 [使用者] 。</span><span class="sxs-lookup"><span data-stu-id="d9727-220">In the menu on the top, click **Users**.</span></span>
   
    ![指派使用者][203]
4. <span data-ttu-id="d9727-222">在 [使用者] 清單中，選取 [Britta Simon] 。</span><span class="sxs-lookup"><span data-stu-id="d9727-222">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="d9727-223">在底部的工具列中，按一下 [指派] 。</span><span class="sxs-lookup"><span data-stu-id="d9727-223">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![指派使用者][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="d9727-225">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="d9727-225">Test single sign-on</span></span>
<span data-ttu-id="d9727-226">本節的目標是要使用「存取面板」來測試您的 Microsoft Azure AD SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="d9727-226">The objective of this section is to test your Microsoft Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="d9727-227">當您在「存取面板」中按一下 [Bynder ] 圖格時，應該會自動登入您的 Bynder 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d9727-227">When you click the Bynder tile in the Access Panel, you should get automatically signed-on to your Bynder application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d9727-228">其他資源</span><span class="sxs-lookup"><span data-stu-id="d9727-228">Additional resources</span></span>
* [<span data-ttu-id="d9727-229">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="d9727-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d9727-230">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="d9727-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_205.png
