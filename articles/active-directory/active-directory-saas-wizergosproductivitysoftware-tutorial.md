---
title: "教學課程：Azure Active Directory 與 Wizergos Productivity Software 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Wizergos Productivity Software 之間的單一登入。"
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: acc04396-13c5-4c24-ab9a-30fbc9234ebd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: 73b3bc05aeb337c12acb7e47c0dbebe6d0196530
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wizergos-productivity-software"></a><span data-ttu-id="8a293-103">教學課程：Azure Active Directory 與 Wizergos Productivity Software 整合</span><span class="sxs-lookup"><span data-stu-id="8a293-103">Tutorial: Azure Active Directory integration with Wizergos Productivity Software</span></span>
<span data-ttu-id="8a293-104">本教學課程旨在說明如何整合 Wizergos Productivity Software 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="8a293-104">The objective of this tutorial is to show you how to integrate Wizergos Productivity Software  with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8a293-105">Wizergos Productivity Software 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="8a293-105">Integrating Wizergos Productivity Software with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="8a293-106">您可以在 Azure AD 中控制可存取 Wizergos Productivity Software 的人員</span><span class="sxs-lookup"><span data-stu-id="8a293-106">You can control in Azure AD who has access to Wizergos Productivity Software</span></span>
* <span data-ttu-id="8a293-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Wizergos Productivity Software 單一登入 (SSO)</span><span class="sxs-lookup"><span data-stu-id="8a293-107">You can enable your users to automatically get signed-on to Wizergos Productivity Software single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="8a293-108">您可以在 Azure 傳統入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="8a293-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="8a293-109">若您想了解 SaaS app 與 Azure AD 整合的更多詳細資訊，請參閱 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="8a293-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a293-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="8a293-110">Prerequisites</span></span>
<span data-ttu-id="8a293-111">若要設定 Azure AD 與 Wizergos Productivity Software 整合，您需要以下項目：</span><span class="sxs-lookup"><span data-stu-id="8a293-111">To configure Azure AD integration with Wizergos Productivity Software, you need the following items:</span></span>

* <span data-ttu-id="8a293-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="8a293-112">An Azure AD subscription</span></span>
* <span data-ttu-id="8a293-113">啟用 Wizergos Productivity Software SSO 的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="8a293-113">A Wizergos Productivity Software SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="8a293-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="8a293-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="8a293-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="8a293-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="8a293-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="8a293-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="8a293-117">如果您沒有 Azure AD 試用環境，您可以取得[一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="8a293-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8a293-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="8a293-118">Scenario description</span></span>
<span data-ttu-id="8a293-119">此教學課程的目標是讓您在測試環境中測試 Azure AD SSO。</span><span class="sxs-lookup"><span data-stu-id="8a293-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="8a293-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="8a293-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8a293-121">從資源庫新增 Wizergos Productivity Software</span><span class="sxs-lookup"><span data-stu-id="8a293-121">Adding Wizergos Productivity Software from the gallery</span></span>
2. <span data-ttu-id="8a293-122">設定並測試 Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="8a293-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-wizergos-productivity-software-from-the-gallery"></a><span data-ttu-id="8a293-123">從資源庫新增 Wizergos Productivity Software</span><span class="sxs-lookup"><span data-stu-id="8a293-123">Adding Wizergos Productivity Software from the gallery</span></span>
<span data-ttu-id="8a293-124">若要設定 Wizergos Productivity Software 與 Azure AD 整合，您需要從資源庫將 Wizergos Productivity Software 加入受管理 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="8a293-124">To configure the integration of Wizergos Productivity Software into Azure AD, you need to add Wizergos Productivity Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8a293-125">**若要從資源庫新增 Wizergos Productivity Software，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="8a293-125">**To add Wizergos Productivity Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8a293-126">在 **Azure 傳統入口網站**中，按一下左方瀏覽窗格的 [Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="8a293-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="8a293-128">從 [目錄]  清單中，選取要啟用目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="8a293-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="8a293-129">若要開啟應用程式檢視，請在目錄檢視中，按一下頂端功能表中的 [應用程式]  。</span><span class="sxs-lookup"><span data-stu-id="8a293-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![應用程式][2]
4. <span data-ttu-id="8a293-131">按一下頁面底部的 [新增]  。</span><span class="sxs-lookup"><span data-stu-id="8a293-131">Click **Add** at the bottom of the page.</span></span>
   
    ![應用程式][3]
5. <span data-ttu-id="8a293-133">在 [欲執行動作] 對話方塊上，按一下 [從資源庫中新增應用程式]。</span><span class="sxs-lookup"><span data-stu-id="8a293-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![應用程式][4]
6. <span data-ttu-id="8a293-135">在 [搜尋] 方塊中，輸入 **Wizergos Productivity Software**。</span><span class="sxs-lookup"><span data-stu-id="8a293-135">In the search box, type **Wizergos Productivity Software**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_01.png)
7. <span data-ttu-id="8a293-137">在結果窗格中，選取 [Wizergos Productivity Software]，然後按一下 [完成] 來新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="8a293-137">In the results panel, select **Wizergos Productivity Software**, and then click **Complete** to add the application.</span></span>
   
    ![選取資源庫中的應用程式](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_001.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="8a293-139">設定並測試 Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="8a293-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="8a293-140">本節的目標是說明如何以名為 "Britta Simon" 的測試使用者為基礎，使用 Wizergos Productivity Software 來設定及測試 Azure AD SSO。</span><span class="sxs-lookup"><span data-stu-id="8a293-140">The objective of this section is to show you how to configure and test Azure AD SSO with Wizergos Productivity Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8a293-141">若要讓 SSO 運作，Azure AD 必須知道 Wizergos Productivity Software 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="8a293-141">For SSO to work, Azure AD needs to know what the counterpart user in Wizergos Productivity Software to an user in Azure AD is.</span></span> <span data-ttu-id="8a293-142">換句話說，Azure AD 使用者和 Wizergos Productivity Software 中的相關使用者之間必須建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="8a293-142">In other words, a link relationship between an Azure AD user and the related user in Wizergos Productivity Software needs to be established.</span></span>

<span data-ttu-id="8a293-143">建立此連結關聯性的方法，就是將 Azure AD 中**使用者名稱**的值指派為 Wizergos Productivity Software 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="8a293-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Wizergos Productivity Software.</span></span>

<span data-ttu-id="8a293-144">若要設定及測試對 BynWizergos Productivity Softwareder 的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="8a293-144">To configure and test Azure AD single sign-on with BynWizergos Productivity Softwareder, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8a293-145">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="8a293-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8a293-146">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8a293-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8a293-147">**[建立 Wizergos Productivity Software 測試使用者](#creating-a-wizergos-productivity-software-test-user)** - 使 Wizergos Productivity Software 中對應的 Britta Simon 連結到她在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="8a293-147">**[Creating a Wizergos Productivity Software test user](#creating-a-wizergos-productivity-software-test-user)** - to have a counterpart of Britta Simon in Wizergos Productivity Software that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="8a293-148">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8a293-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8a293-149">**[測試單一登入](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="8a293-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="8a293-150">設定 Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="8a293-150">Configuring Azure AD SSO</span></span>
<span data-ttu-id="8a293-151">在本節中，您會在傳統入口網站中啟用 Azure AD 單一登入，並在您的 Wizergos Productivity Software 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="8a293-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Wizergos Productivity Software application.</span></span>

<span data-ttu-id="8a293-152">**若要使用 Wizergos Productivity Software 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="8a293-152">**To configure Azure AD single sign-on with Wizergos Productivity Software, perform the following steps:**</span></span>

1. <span data-ttu-id="8a293-153">在傳統入口網站的 [Wizergos Productivity Software] 應用程式整合頁面上，按一下 [設定單一登入] 來開啟 [設定單一登入] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="8a293-153">In the classic portal, on the **Wizergos Productivity Software** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![設定單一登入][6] 
2. <span data-ttu-id="8a293-155">在 [要如何讓使用者登入 Wizergos Productivity Software] 頁面上，選取 [Azure AD 單一登入]，然後按 [下一步]：</span><span class="sxs-lookup"><span data-stu-id="8a293-155">On the **How would you like users to sign on to Wizergos Productivity Software** page, select **Azure AD Single Sign-On**, and then click **Next**:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_03.png)
3. <span data-ttu-id="8a293-157">在 [設定應用程式設定] 對話方塊頁面上，按 [下一步]：</span><span class="sxs-lookup"><span data-stu-id="8a293-157">On the **Configure App Settings** dialog page, click **Next**:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_04.png)
4. <span data-ttu-id="8a293-159">於 [設定在 Recognize 單一燈入] 頁面上，按一下 [下載憑證]，然後將該檔案儲存在您的電腦上：</span><span class="sxs-lookup"><span data-stu-id="8a293-159">On the **Configure single sign-on at Wizergos Productivity Software** page, click **Download certificate**, and then save the file on your computer:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_05.png)
5. <span data-ttu-id="8a293-161">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 Wizergos Productivity Software 租用戶。</span><span class="sxs-lookup"><span data-stu-id="8a293-161">In a different web browser window, sign-on to your Wizergos Productivity Software tenant as an administrator.</span></span>
6. <span data-ttu-id="8a293-162">從漢堡功能表中，選取 [系統管理] 。</span><span class="sxs-lookup"><span data-stu-id="8a293-162">From the hamburger menu, select **Admin**.</span></span>
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_000.png)
7. <span data-ttu-id="8a293-164">在 [系統管理] 頁面左側的功能表中，選取 [驗證]，然後按一下 [Azure AD]。</span><span class="sxs-lookup"><span data-stu-id="8a293-164">In Admin page on left hand menu select **AUTHENTICATION** and click on **Azure AD**.</span></span>
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_002.png)
8. <span data-ttu-id="8a293-166">在 [驗證]  區段上執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="8a293-166">Perform the following steps on **AUTHENTICATION** section.</span></span>
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_003.png)
  1. <span data-ttu-id="8a293-168">按一下 [上傳] 按鈕來上傳從 Azure AD 下載的憑證。</span><span class="sxs-lookup"><span data-stu-id="8a293-168">Click **UPLOAD** button to upload the downloaded certificate from Azure AD.</span></span> 
  2. <span data-ttu-id="8a293-169">在 [簽發者 URL] 文字方塊中，放入得自 Azure AD 應用程式組態精靈的 [簽發者 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="8a293-169">In the **Issuer URL** textbox put the value of **Issuer URL** from Azure AD application configuration wizard.</span></span>
  3. <span data-ttu-id="8a293-170">在 [單一登入 URL] 文字方塊中，放入來自 Azure AD 應用程式組態精靈的 [單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="8a293-170">In the **Single Sign-On URL** textbox put the value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
  4. <span data-ttu-id="8a293-171">在 [單一登出 URL] 文字方塊中，放入來自 Azure AD 應用程式組態精靈的 [單一登出服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="8a293-171">In the **Single Sign-Out URL** textbox put the value of **Single Sign-out Service URL** from Azure AD application configuration wizard.</span></span>
  5. <span data-ttu-id="8a293-172">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="8a293-172">Click **Save** button.</span></span>
9. <span data-ttu-id="8a293-173">在傳統入口網站中，選取單一登入設定確認，然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="8a293-173">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD 單一登入][10]
10. <span data-ttu-id="8a293-175">在 [單一登入確認] 頁面上，按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="8a293-175">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
    
    ![Azure AD 單一登入][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8a293-177">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="8a293-177">Create an Azure AD test user</span></span>
<span data-ttu-id="8a293-178">本節的目標是要在傳統入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="8a293-178">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][20]

<span data-ttu-id="8a293-180">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="8a293-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8a293-181">在 **Azure 傳統入口網站**中，按一下左方瀏覽窗格的 [Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="8a293-181">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="8a293-183">從 [目錄]  清單中，選取要啟用目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="8a293-183">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="8a293-184">若要顯示使用者清單，請按一下頂端功能表的 [使用者] 。</span><span class="sxs-lookup"><span data-stu-id="8a293-184">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="8a293-186">若要開啟 [新增使用者] 對話方塊，請按一下底部工具列上的 [新增使用者]。</span><span class="sxs-lookup"><span data-stu-id="8a293-186">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="8a293-188">在 [告訴我們這位使用者]  對話方塊頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="8a293-188">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="8a293-190">針對 [使用者類型]，選取 [您組織中的新使用者]。</span><span class="sxs-lookup"><span data-stu-id="8a293-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="8a293-191">在 [使用者名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="8a293-191">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="8a293-192">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="8a293-192">Click **Next**.</span></span>
6. <span data-ttu-id="8a293-193">在 [使用者設定檔]  對話方塊頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="8a293-193">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![建立 Azure AD 測試使用者](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="8a293-195">在 [名字] 文字方塊中，輸入 **Britta**。</span><span class="sxs-lookup"><span data-stu-id="8a293-195">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="8a293-196">在 [姓氏] 文字方塊中，輸入 **Simon**。</span><span class="sxs-lookup"><span data-stu-id="8a293-196">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="8a293-197">在 [顯示名稱] 文字方塊中，輸入 **Britta Simon**。</span><span class="sxs-lookup"><span data-stu-id="8a293-197">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="8a293-198">在 [角色] 清單中選取 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="8a293-198">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="8a293-199">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="8a293-199">Click **Next**.</span></span>
7. <span data-ttu-id="8a293-200">在 [取得暫時密碼] 對話方塊頁面上，按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="8a293-200">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="8a293-202">在 [取得暫時密碼]  對話方塊頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="8a293-202">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_08.png)
  1. <span data-ttu-id="8a293-204">記下 [新密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="8a293-204">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="8a293-205">按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="8a293-205">Click **Complete**.</span></span>   

### <a name="create-a-wizergos-productivity-software-test-user"></a><span data-ttu-id="8a293-206">建立 Wizergos Productivity Software 測試使用者</span><span class="sxs-lookup"><span data-stu-id="8a293-206">Create a Wizergos Productivity Software test user</span></span>
<span data-ttu-id="8a293-207">在本節中，您要在 Wizergos Productivity Software 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="8a293-207">In this section, you create a user called Britta Simon in Wizergos Productivity Software.</span></span> <span data-ttu-id="8a293-208">請透過 [support@wizergos.com](emailTo:support@wizergos.com) 聯繫 Wizergos Productivity Software 支援小組，以將使用者加入至 Wizergos Productivity Software 平台。</span><span class="sxs-lookup"><span data-stu-id="8a293-208">Please work with Wizergos Productivity Software support team via [support@wizergos.com](emailTo:support@wizergos.com) to add the users in the Wizergos Productivity Software platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="8a293-209">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="8a293-209">Assign the Azure AD test user</span></span>
<span data-ttu-id="8a293-210">本節的目標是授與 Britta Simon 對 Wizergos Productivity Software 的存取權，讓她能夠使用 Azure SSO。</span><span class="sxs-lookup"><span data-stu-id="8a293-210">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Wizergos Productivity Software.</span></span>

  ![指派使用者][200]

<span data-ttu-id="8a293-212">**若要指派 Britta Simon 到 Wizergos Productivity Software，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="8a293-212">**To assign Britta Simon to Wizergos Productivity Software, perform the following steps:**</span></span>

1. <span data-ttu-id="8a293-213">在傳統入口網站中，若要開啟應用程式檢視，請在目錄檢視中，按一下頂端功能表中的 [應用程式]  。</span><span class="sxs-lookup"><span data-stu-id="8a293-213">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![指派使用者][201]
2. <span data-ttu-id="8a293-215">在應用程式清單中，選取 [Wizergos Productivity Software] 。</span><span class="sxs-lookup"><span data-stu-id="8a293-215">In the applications list, select **Wizergos Productivity Software**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_50.png)
3. <span data-ttu-id="8a293-217">在頂端的功能表中，按一下 [使用者] 。</span><span class="sxs-lookup"><span data-stu-id="8a293-217">In the menu on the top, click **Users**.</span></span>
   
    ![指派使用者][203]
4. <span data-ttu-id="8a293-219">在 [使用者] 清單中，選取 [Britta Simon] 。</span><span class="sxs-lookup"><span data-stu-id="8a293-219">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="8a293-220">在底部的工具列中，按一下 [指派] 。</span><span class="sxs-lookup"><span data-stu-id="8a293-220">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![指派使用者][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="8a293-222">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="8a293-222">Test single sign-on</span></span>
<span data-ttu-id="8a293-223">本節的目標是要使用「存取面板」來測試您的 Azure AD SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="8a293-223">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="8a293-224">當您在 [存取面板] 中按一下 [Wizergos Productivity Software] 圖格時，您應該會自動登入您的 Wizergos Productivity Software 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8a293-224">When you click the Wizergos Productivity Software tile in the Access Panel, you should get automatically signed-on to your Wizergos Productivity Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8a293-225">其他資源</span><span class="sxs-lookup"><span data-stu-id="8a293-225">Additional resources</span></span>
* [<span data-ttu-id="8a293-226">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="8a293-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8a293-227">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="8a293-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_205.png
