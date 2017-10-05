---
title: "教學課程：Azure Active Directory 與 SciQuest Spend Director 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 SciQuest Spend Director 之間的單一登入。"
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 9fab641b-292e-4bef-91d1-8ccc4f3a0c1f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 84b707668dc45e92e6151f422f1c919f638533b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sciquest-spend-director"></a><span data-ttu-id="b49b4-103">教學課程：Azure Active Directory 與 SciQuest Spend Director 整合</span><span class="sxs-lookup"><span data-stu-id="b49b4-103">Tutorial: Azure Active Directory integration with SciQuest Spend Director</span></span>
<span data-ttu-id="b49b4-104">本教學課程旨在說明如何整合 SciQuest Spend Director 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="b49b4-104">The objective of this tutorial is to show you how to integrate SciQuest Spend Director with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="b49b4-105">SciQuest Spend Director 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="b49b4-105">Integrating SciQuest Spend Director with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="b49b4-106">您可以在 Azure AD 中控制可存取 SciQuest Spend Director 的人員。</span><span class="sxs-lookup"><span data-stu-id="b49b4-106">You can control in Azure AD who has access to SciQuest Spend Director</span></span> 
* <span data-ttu-id="b49b4-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 SciQuest Spend Director (單一登入)</span><span class="sxs-lookup"><span data-stu-id="b49b4-107">You can enable your users to automatically get signed-on to SciQuest Spend Director (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="b49b4-108">您可以在 Azure 傳統入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="b49b4-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="b49b4-109">若您想了解 SaaS app 與 Azure AD 整合的更多詳細資訊，請參閱 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="b49b4-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b49b4-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="b49b4-110">Prerequisites</span></span>
<span data-ttu-id="b49b4-111">若要使用 SciQuest Spend Director 設定 Azure AD 整合，您需要以下項目：</span><span class="sxs-lookup"><span data-stu-id="b49b4-111">To configure Azure AD integration with SciQuest Spend Director, you need the following items:</span></span>

* <span data-ttu-id="b49b4-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b49b4-112">An Azure AD subscription</span></span>
* <span data-ttu-id="b49b4-113">啟用 SciQuest Spend Director 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b49b4-113">A SciQuest Spend Director single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b49b4-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="b49b4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="b49b4-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="b49b4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="b49b4-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="b49b4-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="b49b4-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="b49b4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="b49b4-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="b49b4-118">Scenario Description</span></span>
<span data-ttu-id="b49b4-119">此教學課程的目標是讓您在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b49b4-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="b49b4-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="b49b4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b49b4-121">從資源庫新增 SciQuest Spend Director</span><span class="sxs-lookup"><span data-stu-id="b49b4-121">Adding SciQuest Spend Director from the gallery</span></span> 
2. <span data-ttu-id="b49b4-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b49b4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sciquest-spend-director-from-the-gallery"></a><span data-ttu-id="b49b4-123">從資源庫新增 SciQuest Spend Director</span><span class="sxs-lookup"><span data-stu-id="b49b4-123">Adding SciQuest Spend Director from the gallery</span></span>
<span data-ttu-id="b49b4-124">若要設定 SciQuest Spend Director 與 Azure AD 整合，您需要從資源庫將 SciQuest Spend Director 加入 受管理 SaaS app 的清單。</span><span class="sxs-lookup"><span data-stu-id="b49b4-124">To configure the integration of SciQuest Spend Director into Azure AD, you need to add SciQuest Spend Director from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b49b4-125">**若要從資源庫新增 SciQuest Spend Director，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="b49b4-125">**To add SciQuest Spend Director from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b49b4-126">在 **Azure 傳統入口網站**中，按一下左方瀏覽窗格的 [Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="b49b4-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="b49b4-128">從 [目錄]  清單中，選取要啟用目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="b49b4-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="b49b4-129">若要開啟應用程式檢視，請在目錄檢視中，按一下頂端功能表中的 [應用程式]  。</span><span class="sxs-lookup"><span data-stu-id="b49b4-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![應用程式][2]

4. <span data-ttu-id="b49b4-131">按一下頁面底部的 [新增]  。</span><span class="sxs-lookup"><span data-stu-id="b49b4-131">Click **Add** at the bottom of the page.</span></span>
   
    ![應用程式][3]

5. <span data-ttu-id="b49b4-133">在 [欲執行動作] 對話方塊上，按一下 [從資源庫中新增應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b49b4-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![應用程式][4]

6. <span data-ttu-id="b49b4-135">在搜尋方塊中，輸入 **sciQuest spend director**。</span><span class="sxs-lookup"><span data-stu-id="b49b4-135">In the search box, type **sciQuest spend director**.</span></span>
   
    ![應用程式][5]

7. <span data-ttu-id="b49b4-137">在結果窗格中，選取 [SciQuest Spend Director]，然後按一下 [完成] 來新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="b49b4-137">In the results pane, select **SciQuest Spend Director**, and then click **Complete** to add the application.</span></span>
   
    ![應用程式][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b49b4-139">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b49b4-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b49b4-140">本節的目標是說明如何以名為 "Britta Simon" 的測試使用者為基礎，使用 SciQuest Spend Director 來設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b49b4-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with SciQuest Spend Director based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b49b4-141">單一登入若要運作，Azure AD 必須知道 SciQuest Spend Director 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="b49b4-141">For single sign-on to work, Azure AD needs to know what the counterpart user in SciQuest Spend Director to an user in Azure AD is.</span></span> <span data-ttu-id="b49b4-142">換句話說，必須在 Azure AD 使用者與 SciQuest Spend Director 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="b49b4-142">In other words, a link relationship between an Azure AD user and the related user in SciQuest Spend Director needs to be established.</span></span>  
<span data-ttu-id="b49b4-143">建立此連結關聯性的方法是將 Azure AD 中的**使用者名稱**的值指定為 SciQuest Spend Director 中 **Username**的值。</span><span class="sxs-lookup"><span data-stu-id="b49b4-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SciQuest Spend Director.</span></span>

<span data-ttu-id="b49b4-144">若要使用 SciQuest Spend Director 設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="b49b4-144">To configure and test Azure AD single sign-on with SciQuest Spend Director, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b49b4-145">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="b49b4-145">**[Configuring Azure AD Single Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b49b4-146">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b49b4-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b49b4-147">**[建立 SciQuest Spend Director 測試使用者](#creating-a-halogen-software-test-user)** - 使 SciQuest Spend Director 中對應的 Britta Simon 連結到她在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="b49b4-147">**[Creating a SciQuest Spend Director test user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in SciQuest Spend Director that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="b49b4-148">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b49b4-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b49b4-149">**[測試單一登入](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="b49b4-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-single-sign-on"></a><span data-ttu-id="b49b4-150">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b49b4-150">Configuring Azure AD Single Single Sign-On</span></span>
<span data-ttu-id="b49b4-151">本節目標是在 Azure 傳統入口網站啟用 Azure AD 單一登入，並在您的 SciQuest Spend Director 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="b49b4-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your SciQuest Spend Director application.</span></span>

<span data-ttu-id="b49b4-152">**若要使用 SciQuest Spend Director 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="b49b4-152">**To configure Azure AD single sign-on with SciQuest Spend Director, perform the following steps:**</span></span>

1. <span data-ttu-id="b49b4-153">在 Azure 傳統入口網站的 [SciQuest Spend Director] 應用程式整合頁面上，按一下 [設定單一登入] 來開啟 [設定單一登入] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="b49b4-153">In the Azure classic portal, on the **SciQuest Spend Director** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![設定單一登入][8]

2. <span data-ttu-id="b49b4-155">在 [要如何讓使用者登入 SciQuest Spend Director] 頁面上，選取 [Azure AD 單一登入]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="b49b4-155">On the **How would you like users to sign on to SciQuest Spend Director** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD 單一登入][9]

3. <span data-ttu-id="b49b4-157">在 [設定應用程式設定]  對話方塊頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b49b4-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span> 
   
    ![設定 App 設定][10]
   
     <span data-ttu-id="b49b4-159">a.</span><span class="sxs-lookup"><span data-stu-id="b49b4-159">a.</span></span> <span data-ttu-id="b49b4-160">在 [登入 URL] 文字方塊中，使用以下模式輸入使用者登入您的 SciQuest Spend Director 應用程式時所使用的 URL：*https://.*sciquest.com/.**</span><span class="sxs-lookup"><span data-stu-id="b49b4-160">In the **Sign On URL** textbox, type your URL used by your users to sign on to your SciQuest Spend Director application using the following pattern: *https://.*sciquest.com/.**</span></span>
   
     <span data-ttu-id="b49b4-161">b.</span><span class="sxs-lookup"><span data-stu-id="b49b4-161">b.</span></span> <span data-ttu-id="b49b4-162">在 [回覆 URL] 文字方塊中，輸入您在 [登入 URL] 文字方塊所輸入的相同值。</span><span class="sxs-lookup"><span data-stu-id="b49b4-162">In the **Reply URL** textbox, type the same value you have typed into the **Sign On URL** textbox.</span></span> 
   
     <span data-ttu-id="b49b4-163">c.</span><span class="sxs-lookup"><span data-stu-id="b49b4-163">c.</span></span> <span data-ttu-id="b49b4-164">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="b49b4-164">Click **Next**.</span></span>

4. <span data-ttu-id="b49b4-165">在 [設定在 SciQuest Spend Director 單一登入] 頁面上，按一下 [下載中繼資料]，然後將中繼資料檔儲存在您的本機電腦上。</span><span class="sxs-lookup"><span data-stu-id="b49b4-165">On the **Configure single sign-on at SciQuest Spend Director** page, click **Download metadata**, and then save the metadata file locally on your computer.</span></span>
   
    ![何謂 Azure AD Connect][11]

5. <span data-ttu-id="b49b4-167">連絡 SciQuest 支援來啟用使用上述下載的中繼資料進行驗證的方法。</span><span class="sxs-lookup"><span data-stu-id="b49b4-167">Contact SciQuest support to enable this authentication method using the above downloaded metadata.</span></span>

6. <span data-ttu-id="b49b4-168">在 Azure 傳統入口網站上，選取單一登入設定確認，然後按一下 [完成] 來關閉 [設定單一登入] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="b49b4-168">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span> 
   
    ![何謂 Azure AD Connect][15]

7. <span data-ttu-id="b49b4-170">在 [單一登入確認] 頁面上，按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="b49b4-170">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b49b4-171">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b49b4-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="b49b4-172">本節的目標是要在 Azure 傳統入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="b49b4-172">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="b49b4-173">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="b49b4-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b49b4-174">在 **Azure 傳統入口網站**中，按一下左方瀏覽窗格的 [Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="b49b4-174">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![何謂 Azure AD Connect][100] 

2. <span data-ttu-id="b49b4-176">從 [目錄]  清單中，選取要啟用目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="b49b4-176">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="b49b4-177">若要顯示使用者清單，請按一下頂端功能表中的 [使用者] 。</span><span class="sxs-lookup"><span data-stu-id="b49b4-177">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![何謂 Azure AD Connect][101] 

4. <span data-ttu-id="b49b4-179">若要開啟 [新增使用者] 對話方塊，請按一下底部工具列上的 [新增使用者]。</span><span class="sxs-lookup"><span data-stu-id="b49b4-179">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![何謂 Azure AD Connect][102] 

5. <span data-ttu-id="b49b4-181">在 [告訴我們這位使用者]  對話方塊頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b49b4-181">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![何謂 Azure AD Connect][103] 
   
    <span data-ttu-id="b49b4-183">a.</span><span class="sxs-lookup"><span data-stu-id="b49b4-183">a.</span></span> <span data-ttu-id="b49b4-184">針對 [使用者類型]，選取 [您組織中的新使用者]。</span><span class="sxs-lookup"><span data-stu-id="b49b4-184">As **Type Of User**, select **New user in your organization**.</span></span>
   
    <span data-ttu-id="b49b4-185">b.</span><span class="sxs-lookup"><span data-stu-id="b49b4-185">b.</span></span> <span data-ttu-id="b49b4-186">在 [使用者名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="b49b4-186">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="b49b4-187">c.</span><span class="sxs-lookup"><span data-stu-id="b49b4-187">c.</span></span> <span data-ttu-id="b49b4-188">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="b49b4-188">Click **Next**.</span></span>

6. <span data-ttu-id="b49b4-189">在 [使用者設定檔]  對話方塊頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b49b4-189">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
    ![何謂 Azure AD Connect][104] 
   
    <span data-ttu-id="b49b4-191">a.</span><span class="sxs-lookup"><span data-stu-id="b49b4-191">a.</span></span> <span data-ttu-id="b49b4-192">在 [名字] 文字方塊中，輸入 **Britta**。</span><span class="sxs-lookup"><span data-stu-id="b49b4-192">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="b49b4-193">b.</span><span class="sxs-lookup"><span data-stu-id="b49b4-193">b.</span></span> <span data-ttu-id="b49b4-194">在 [姓氏] 文字方塊中輸入 **Simon**。</span><span class="sxs-lookup"><span data-stu-id="b49b4-194">In the **Last Name** txtbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="b49b4-195">c.</span><span class="sxs-lookup"><span data-stu-id="b49b4-195">c.</span></span> <span data-ttu-id="b49b4-196">在 [顯示名稱] 文字方塊中，輸入 **Britta Simon**。</span><span class="sxs-lookup"><span data-stu-id="b49b4-196">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="b49b4-197">d.</span><span class="sxs-lookup"><span data-stu-id="b49b4-197">d.</span></span> <span data-ttu-id="b49b4-198">在 [角色] 清單中選取 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="b49b4-198">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="b49b4-199">e.</span><span class="sxs-lookup"><span data-stu-id="b49b4-199">e.</span></span> <span data-ttu-id="b49b4-200">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="b49b4-200">Click **Next**.</span></span>

7. <span data-ttu-id="b49b4-201">在 [取得暫時密碼] 對話方塊頁面上，按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="b49b4-201">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![何謂 Azure AD Connect][105]  

8. <span data-ttu-id="b49b4-203">在 [取得暫時密碼]  對話方塊頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b49b4-203">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![何謂 Azure AD Connect][106]   
   
    <span data-ttu-id="b49b4-205">a.</span><span class="sxs-lookup"><span data-stu-id="b49b4-205">a.</span></span> <span data-ttu-id="b49b4-206">記下 [新密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="b49b4-206">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="b49b4-207">b.</span><span class="sxs-lookup"><span data-stu-id="b49b4-207">b.</span></span> <span data-ttu-id="b49b4-208">按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="b49b4-208">Click **Complete**.</span></span>   

### <a name="creating-a-sciquest-spend-director-test-user"></a><span data-ttu-id="b49b4-209">建立 SciQuest Spend Director 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b49b4-209">Creating a SciQuest Spend Director test user</span></span>
<span data-ttu-id="b49b4-210">本節目標是在 SciQuest Spend Director 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="b49b4-210">The objective of this section is to create a user called Britta Simon in SciQuest Spend Director.</span></span>

<span data-ttu-id="b49b4-211">您需要連絡您的 SciQuest Spend Director 支援小組，並提供他們與您的測試帳戶有關的詳細資料來建立帳戶。</span><span class="sxs-lookup"><span data-stu-id="b49b4-211">You need to contact your SciQuest Spend Director support team and provide them with the details about your test account to get it created.</span></span>

<span data-ttu-id="b49b4-212">您也可以利用 Just-In-Time 佈建功能，這是 SciQuest Spend Director 支援的單一登入功能。</span><span class="sxs-lookup"><span data-stu-id="b49b4-212">Alternatively, you can also leverage just-in-time provisioning, a single sign-on feature that is supported by SciQuest Spend Director.</span></span>  
<span data-ttu-id="b49b4-213">啟用 Just-In-Time 佈建時，如果使用者不存在，SciQuest Spend Director 就會在使用者嘗試執行單一登入期間自動建立使用者。</span><span class="sxs-lookup"><span data-stu-id="b49b4-213">If just-in-time provisioning is enabled, users are automatically created by SciQuest Spend Director during a single sign-on attempt if they don't exist.</span></span> <span data-ttu-id="b49b4-214">使用此功能時就不需要手動建立單一登入對應使用者。</span><span class="sxs-lookup"><span data-stu-id="b49b4-214">This feature eliminates the need to manually create single sign-on counterpart users.</span></span>

<span data-ttu-id="b49b4-215">若要啟用 Just-In-Time 佈建，您需要連絡您的 SciQuest Spend Director 支援小組。</span><span class="sxs-lookup"><span data-stu-id="b49b4-215">To get just-in-time provisioning enabled, you need to contact your your SciQuest Spend Director support team.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b49b4-216">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b49b4-216">Assigning the Azure AD test user</span></span>
<span data-ttu-id="b49b4-217">本節目標是授與 Britta Simon 對 SciQuest Spend Director 的存取權，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b49b4-217">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to SciQuest Spend Director.</span></span>

![何謂 Azure AD Connect][200]

<span data-ttu-id="b49b4-219">**若要指派 Britta Simon 到 SciQuest Spend Director，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="b49b4-219">**To assign Britta Simon to SciQuest Spend Director, perform the following steps:**</span></span>

1. <span data-ttu-id="b49b4-220">在 Azure 傳統入口網站中，若要開啟應用程式檢視，請在目錄檢視中，按一下頂端功能表中的 [應用程式]  。</span><span class="sxs-lookup"><span data-stu-id="b49b4-220">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![何謂 Azure AD Connect][201]

2. <span data-ttu-id="b49b4-222">在應用程式清單中，選取 [SciQuest Spend Director] 。</span><span class="sxs-lookup"><span data-stu-id="b49b4-222">In the applications list, select **SciQuest Spend Director**.</span></span>
   
    ![何謂 Azure AD Connect][202]

3. <span data-ttu-id="b49b4-224">在頂端的功能表中，按一下 [使用者] 。</span><span class="sxs-lookup"><span data-stu-id="b49b4-224">In the menu on the top, click **Users**.</span></span>
   
    ![何謂 Azure AD Connect][203]

4. <span data-ttu-id="b49b4-226">在 [使用者] 清單中，選取 [Britta Simon] 。</span><span class="sxs-lookup"><span data-stu-id="b49b4-226">In the Users list, select **Britta Simon**.</span></span>
   
    ![何謂 Azure AD Connect][204]

5. <span data-ttu-id="b49b4-228">在底部的工具列中，按一下 [指派] 。</span><span class="sxs-lookup"><span data-stu-id="b49b4-228">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![何謂 Azure AD Connect][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="b49b4-230">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="b49b4-230">Testing Single Sign-On</span></span>
<span data-ttu-id="b49b4-231">本節的目標是要使用存取面板來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="b49b4-231">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="b49b4-232">當您在存取面板中按一下 [SciQuest Spend Director] 圖格時，您應該會自動登入您的 SciQuest Spend Director 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b49b4-232">When you click the SciQuest Spend Director tile in the Access Panel, you should get automatically signed-on to your SciQuest Spend Director application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b49b4-233">其他資源</span><span class="sxs-lookup"><span data-stu-id="b49b4-233">Additional Resources</span></span>
* [<span data-ttu-id="b49b4-234">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="b49b4-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b49b4-235">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="b49b4-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_01.png
[6]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_05.png
[8]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_07.png
[10]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_08.png
[11]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_03.png
[15]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_04.png

[100]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_15.png 
[200]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_06.png
[203]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_18.png
[204]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_19.png
[205]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_20.png

