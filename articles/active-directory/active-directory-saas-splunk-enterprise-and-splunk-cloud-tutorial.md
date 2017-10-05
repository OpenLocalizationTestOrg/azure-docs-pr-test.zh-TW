---
title: "教學課程：Azure Active Directory 與 Splunk Enterprise and Splunk Cloud 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Splunk Enterprise and Splunk Cloud 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b3e2b4a9-749c-4895-813d-db46f8dfdbf8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/09/2017
ms.author: jeedes
ms.openlocfilehash: b78e9b7161207a74880e912241d5e965b353d1c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a><span data-ttu-id="c35b9-103">教學課程：Azure Active Directory 與 Splunk Enterprise and Splunk Cloud 整合</span><span class="sxs-lookup"><span data-stu-id="c35b9-103">Tutorial: Azure Active Directory integration with Splunk Enterprise and Splunk Cloud</span></span>

<span data-ttu-id="c35b9-104">在本教學課程中，您會了解如何整合 Splunk Enterprise and Splunk Cloud 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="c35b9-104">In this tutorial, you learn how to integrate Splunk Enterprise and Splunk Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c35b9-105">Splunk Enterprise and Splunk Cloud 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="c35b9-105">Integrating Splunk Enterprise and Splunk Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c35b9-106">您可以在 Azure AD 中控制可存取 Splunk Enterprise and Splunk Cloud 的人員</span><span class="sxs-lookup"><span data-stu-id="c35b9-106">You can control in Azure AD who has access to Splunk Enterprise and Splunk Cloud</span></span>
- <span data-ttu-id="c35b9-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Splunk Enterprise and Splunk Cloud 單一登入 (SSO)</span><span class="sxs-lookup"><span data-stu-id="c35b9-107">You can enable your users to automatically get signed-on to Splunk Enterprise and Splunk Cloud single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="c35b9-108">您可以在 Azure 傳統入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="c35b9-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="c35b9-109">若您想了解 SaaS app 與 Azure AD 整合的更多詳細資訊，請參閱 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="c35b9-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c35b9-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="c35b9-110">Prerequisites</span></span>

<span data-ttu-id="c35b9-111">若要設定 Azure AD 與 Splunk Enterprise and Splunk Cloud 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="c35b9-111">To configure Azure AD integration with Splunk Enterprise and Splunk Cloud, you need the following items:</span></span>

- <span data-ttu-id="c35b9-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="c35b9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c35b9-113">已啟用 Splunk Enterprise or Splunk Cloud SSO 的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="c35b9-113">A Splunk Enterprise or Splunk Cloud SSO enabled subscription</span></span>


>[!NOTE]
><span data-ttu-id="c35b9-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="c35b9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="c35b9-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="c35b9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c35b9-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="c35b9-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="c35b9-117">如果您沒有 Azure AD 試用環境，您可以取得[一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="c35b9-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="c35b9-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="c35b9-118">Scenario description</span></span>
<span data-ttu-id="c35b9-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c35b9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="c35b9-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="c35b9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c35b9-121">從資源庫新增 Splunk Enterprise and Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="c35b9-121">Adding Splunk Enterprise and Splunk Cloud from the gallery</span></span>
2. <span data-ttu-id="c35b9-122">設定並測試 Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="c35b9-122">Configuring and testing Azure AD SSO</span></span>


## <a name="add-splunk-enterprise-and-splunk-cloud-from-the-gallery"></a><span data-ttu-id="c35b9-123">從資源庫新增 Splunk Enterprise and Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="c35b9-123">Add Splunk Enterprise and Splunk Cloud from the gallery</span></span>
<span data-ttu-id="c35b9-124">若要設定 Splunk Enterprise and Splunk Cloud 與 Azure AD 整合，您需要從資源庫將 Splunk Enterprise and Splunk Cloud 新增至受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="c35b9-124">To configure the integration of Splunk Enterprise and Splunk Cloud into Azure AD, you need to add Splunk Enterprise and Splunk Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c35b9-125">**若要從資源庫新增 Splunk Enterprise and Splunk Cloud，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="c35b9-125">**To add Splunk Enterprise and Splunk Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c35b9-126">在 **Azure 傳統入口網站**中，按一下左方瀏覽窗格的 [Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="c35b9-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]

2. <span data-ttu-id="c35b9-128">從 [目錄]  清單中，選取要啟用目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="c35b9-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="c35b9-129">若要開啟應用程式檢視，請在目錄檢視中，按一下頂端功能表中的 [應用程式]  。</span><span class="sxs-lookup"><span data-stu-id="c35b9-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![應用程式][2]

4. <span data-ttu-id="c35b9-131">按一下頁面底部的 [新增]  。</span><span class="sxs-lookup"><span data-stu-id="c35b9-131">Click **Add** at the bottom of the page.</span></span>

    ![應用程式][3]

5. <span data-ttu-id="c35b9-133">在 [欲執行動作] 對話方塊上，按一下 [從資源庫中新增應用程式]。</span><span class="sxs-lookup"><span data-stu-id="c35b9-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>

    ![應用程式][4]

6. <span data-ttu-id="c35b9-135">在搜尋方塊中，輸入 [Splunk Enterprise or Splunk Cloud]。</span><span class="sxs-lookup"><span data-stu-id="c35b9-135">In the search box, type **Splunk Enterprise or Splunk Cloud**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_01.png)

7. <span data-ttu-id="c35b9-137">在結果窗格中選取 [Splunk Enterprise and Splunk Cloud]，然後按一下 [完成] 以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="c35b9-137">In the results pane, select **Splunk Enterprise and Splunk Cloud**, and then click **Complete** to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_02.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c35b9-139">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c35b9-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="c35b9-140">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Splunk Enterprise and Splunk Cloud 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c35b9-140">In this section, you configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c35b9-141">若要讓單一登入運作，Azure AD 必須知道 Splunk Enterprise and Splunk Cloud 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="c35b9-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Splunk Enterprise and Splunk Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="c35b9-142">換句話說，必須建立 Azure AD 使用者和 Splunk Enterprise and Splunk Cloud 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="c35b9-142">In other words, a link relationship between an Azure AD user and the related user in Splunk Enterprise and Splunk Cloud needs to be established.</span></span>

<span data-ttu-id="c35b9-143">建立此連結關聯性的方法，就是將 Azure AD 中**使用者名稱**的值指派為 Splunk Enterprise and Splunk Cloud 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="c35b9-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Splunk Enterprise and Splunk Cloud.</span></span>

<span data-ttu-id="c35b9-144">若要設定及測試與 Splunk Enterprise and Splunk Cloud 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="c35b9-144">To configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c35b9-145">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="c35b9-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c35b9-146">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c35b9-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c35b9-147">**[建立 Splunk Enterprise and Splunk Cloud 測試使用者](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)** - 在 Splunk Enterprise and Splunk Cloud 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表 Britta Simon 的項目連結。</span><span class="sxs-lookup"><span data-stu-id="c35b9-147">**[Creating a Splunk Enterprise and Splunk Cloud test user](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)** - to have a counterpart of Britta Simon in Splunk Enterprise and Splunk Cloud that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="c35b9-148">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c35b9-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c35b9-149">**[測試單一登入](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="c35b9-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c35b9-150">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c35b9-150">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c35b9-151">在本節中，您會在傳統入口網站中啟用 Azure AD SSO，並在您的 Splunk Enterprise and Splunk Cloud 應用程式中設定 SSO。</span><span class="sxs-lookup"><span data-stu-id="c35b9-151">In this section, you enable Azure AD SSO in the classic portal and configure SSO in your Splunk Enterprise and Splunk Cloud application.</span></span>


<span data-ttu-id="c35b9-152">**若要使用 Splunk Enterprise and Splunk Cloud 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="c35b9-152">**To configure Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="c35b9-153">在傳統入口網站的 [Splunk Enterprise and Splunk Cloud] 應用程式整合頁面上，按一下 [設定單一登入] 來開啟 [設定單一登入] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="c35b9-153">In the classic portal, on the **Splunk Enterprise and Splunk Cloud** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
     
    ![設定單一登入][6] 

2. <span data-ttu-id="c35b9-155">在 [要如何讓使用者登入 Splunk Enterprise and Splunk Cloud] 頁面上，選取 [Azure AD 單一登入]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="c35b9-155">On the **How would you like users to sign on to Splunk Enterprise and Splunk Cloud** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![設定單一登入](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_03.png) 

3. <span data-ttu-id="c35b9-157">在 [設定 App 設定]  對話方塊頁面執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="c35b9-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_04.png) 
  1. <span data-ttu-id="c35b9-159">在 [登入 URL] 文字方塊中，使用以下模式輸入使用者登入您的 Splunk Enterprise and Splunk Cloud 應用程式時所使用的 URL：`https://<splunkserverUrl>/en-US/app/launcher/home`</span><span class="sxs-lookup"><span data-stu-id="c35b9-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Splunk Enterprise and Splunk Cloud application using the following pattern: `https://<splunkserverUrl>/en-US/app/launcher/home`</span></span>
  2. <span data-ttu-id="c35b9-160">在 [識別碼] 文字方塊中，輸入 Splunk 伺服器的 URL。</span><span class="sxs-lookup"><span data-stu-id="c35b9-160">In the **Identifier** textbox, type the URL of your Splunk Server.</span></span>
  3. <span data-ttu-id="c35b9-161">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://<splunkserver>/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="c35b9-161">In the **Reply URL** textbox, type the URL with the following pattern: `https://<splunkserver>/saml/acs`</span></span>
  4. <span data-ttu-id="c35b9-162">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="c35b9-162">Click **Next**.</span></span>
 
4. <span data-ttu-id="c35b9-163">在 [設定在 Splunk Enterprise and Splunk Cloud 設定單一登入] 頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="c35b9-163">On the **Configure single sign-on at Splunk Enterprise and Splunk Cloud** page, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_05.png)
  1. <span data-ttu-id="c35b9-165">按一下 [下載中繼資料]，然後將檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="c35b9-165">Click **Download metadata**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="c35b9-166">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="c35b9-166">Click **Next**.</span></span>

5. <span data-ttu-id="c35b9-167">若要為您的應用程式設定 SSO，請連絡 Splunk Enterprise and Splunk Cloud 支援小組，並提供下列資訊：</span><span class="sxs-lookup"><span data-stu-id="c35b9-167">To get SSO configured for your application, contact Splunk Enterprise and Splunk Cloud support team and provide them with the following:</span></span>

    * <span data-ttu-id="c35b9-168">已下載的**同盟中繼資料**</span><span class="sxs-lookup"><span data-stu-id="c35b9-168">The downloaded **federaton metadata**</span></span>
6. <span data-ttu-id="c35b9-169">在傳統入口網站中，選取單一登入組態確認，然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="c35b9-169">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Azure AD 單一登入][10]

7. <span data-ttu-id="c35b9-171">在 [單一登入確認] 頁面上，按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="c35b9-171">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Azure AD 單一登入][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c35b9-173">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="c35b9-173">Create an Azure AD test user</span></span>
<span data-ttu-id="c35b9-174">在本節中，您會在傳統入口網站中建立名稱為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="c35b9-174">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][20]

<span data-ttu-id="c35b9-176">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="c35b9-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c35b9-177">在 **Azure 傳統入口網站**中，按一下左方瀏覽窗格的 [Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="c35b9-177">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="c35b9-179">從 [目錄]  清單中，選取要啟用目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="c35b9-179">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="c35b9-180">若要顯示使用者清單，請按一下頂端功能表的 [使用者] 。</span><span class="sxs-lookup"><span data-stu-id="c35b9-180">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c35b9-182">若要開啟 [新增使用者] 對話方塊，請按一下底部工具列上的 [新增使用者]。</span><span class="sxs-lookup"><span data-stu-id="c35b9-182">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="c35b9-184">在 [告訴我們這位使用者]  對話方塊頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="c35b9-184">On the **Tell us about this user** dialog page, perform the following steps:</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="c35b9-186">針對 [使用者類型]，選取 [您組織中的新使用者]。</span><span class="sxs-lookup"><span data-stu-id="c35b9-186">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="c35b9-187">在 [使用者名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="c35b9-187">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="c35b9-188">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="c35b9-188">Click **Next**.</span></span>

6.  <span data-ttu-id="c35b9-189">在 [使用者設定檔]  對話方塊頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="c35b9-189">On the **User Profile** dialog page, perform the following steps:</span></span>
  
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="c35b9-191">在 [名字] 文字方塊中，輸入 **Britta**。</span><span class="sxs-lookup"><span data-stu-id="c35b9-191">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="c35b9-192">在 [姓氏] 文字方塊中，輸入 **Simon**。</span><span class="sxs-lookup"><span data-stu-id="c35b9-192">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="c35b9-193">在 [顯示名稱] 文字方塊中，輸入 **Britta Simon**。</span><span class="sxs-lookup"><span data-stu-id="c35b9-193">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="c35b9-194">在 [角色] 清單中選取 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="c35b9-194">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="c35b9-195">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="c35b9-195">Click **Next**.</span></span>

7. <span data-ttu-id="c35b9-196">在 [取得暫時密碼] 對話方塊頁面上，按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="c35b9-196">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="c35b9-198">在 [取得暫時密碼]  對話方塊頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="c35b9-198">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="c35b9-200">記下 [新密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="c35b9-200">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="c35b9-201">按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="c35b9-201">Click **Complete**.</span></span>   

### <a name="create-a-splunk-enterprise-and-splunk-cloud-test-user"></a><span data-ttu-id="c35b9-202">建立 Splunk Enterprise and Splunk Cloud 測試使用者</span><span class="sxs-lookup"><span data-stu-id="c35b9-202">Create a Splunk Enterprise and Splunk Cloud test user</span></span>

<span data-ttu-id="c35b9-203">在本節中，您要在 Splunk Enterprise and Splunk Cloud 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="c35b9-203">In this section, you create a user called Britta Simon in Splunk Enterprise and Splunk Cloud.</span></span> <span data-ttu-id="c35b9-204">請Splunk Enterprise and Splunk Cloud 支援小組合作，在 Splunk Enterprise and Splunk Cloud 平台中新增使用者。</span><span class="sxs-lookup"><span data-stu-id="c35b9-204">Please work with Splunk Enterprise and Splunk Cloud support team to add the users in the Splunk Enterprise and Splunk Cloud platform.</span></span>


### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="c35b9-205">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="c35b9-205">Assign the Azure AD test user</span></span>

<span data-ttu-id="c35b9-206">在本節中，您會將 Splunk Enterprise and Splunk Cloud 的存取權授與 Britta Simon，讓她能夠使用 Azure SSO。</span><span class="sxs-lookup"><span data-stu-id="c35b9-206">In this section, you enable Britta Simon to use Azure SSOy granting her access to Splunk Enterprise and Splunk Cloud.</span></span>

![指派使用者][200] 

<span data-ttu-id="c35b9-208">**若要將 Britta Simon 指派給 Splunk Enterprise and Splunk Cloud，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="c35b9-208">**To assign Britta Simon to Splunk Enterprise and Splunk Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="c35b9-209">在傳統入口網站中，若要開啟應用程式檢視，請在目錄檢視中，按一下頂端功能表中的 [應用程式]  。</span><span class="sxs-lookup"><span data-stu-id="c35b9-209">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="c35b9-211">在應用程式清單中，選取 [Splunk Enterprise and Splunk Cloud]。</span><span class="sxs-lookup"><span data-stu-id="c35b9-211">In the applications list, select **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![設定單一登入](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_50.png) 

3. <span data-ttu-id="c35b9-213">在頂端的功能表中，按一下 [使用者] 。</span><span class="sxs-lookup"><span data-stu-id="c35b9-213">In the menu on the top, click **Users**.</span></span>

    ![指派使用者][203]

4. <span data-ttu-id="c35b9-215">在 [使用者] 清單中，選取 [Britta Simon] 。</span><span class="sxs-lookup"><span data-stu-id="c35b9-215">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="c35b9-216">在底部的工具列中，按一下 [指派] 。</span><span class="sxs-lookup"><span data-stu-id="c35b9-216">In the toolbar on the bottom, click **Assign**.</span></span>

    ![指派使用者][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="c35b9-218">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="c35b9-218">Test single sign-on</span></span>

<span data-ttu-id="c35b9-219">在本節中，您會使用存取面板來測試您的 Azure AD SSO 設定。</span><span class="sxs-lookup"><span data-stu-id="c35b9-219">In this section, you test your Azure AD SSOonfiguration using the Access Panel.</span></span>

<span data-ttu-id="c35b9-220">當您在存取面板中按一下 [Splunk Enterprise and Splunk Cloud] 圖格時，應該會自動登入您的 Splunk Enterprise and Splunk Cloud 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c35b9-220">When you click the Splunk Enterprise and Splunk Cloud tile in the Access Panel, you should get automatically signed-on to your Splunk Enterprise and Splunk Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="c35b9-221">其他資源</span><span class="sxs-lookup"><span data-stu-id="c35b9-221">Additional resources</span></span>

* [<span data-ttu-id="c35b9-222">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="c35b9-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c35b9-223">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="c35b9-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_205.png
