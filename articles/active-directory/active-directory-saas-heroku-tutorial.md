---
title: "教學課程：Azure Active Directory 與 Heroku 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Heroku 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d7d72ec6-4a60-4524-8634-26d8fbbcc833
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: d30605e4757b484f327a784b73f939b62ef59373
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-heroku"></a><span data-ttu-id="a6509-103">教學課程：Azure Active Directory 與 Heroku 整合</span><span class="sxs-lookup"><span data-stu-id="a6509-103">Tutorial: Azure Active Directory integration with Heroku</span></span>

<span data-ttu-id="a6509-104">在本教學課程中，您會了解如何整合 Heroku 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="a6509-104">In this tutorial, you learn how to integrate Heroku with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a6509-105">Heroku 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="a6509-105">Integrating Heroku with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a6509-106">您可以在 Azure AD 中控制可存取 Heroku 的人員</span><span class="sxs-lookup"><span data-stu-id="a6509-106">You can control in Azure AD who has access to Heroku</span></span>
- <span data-ttu-id="a6509-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Heroku (單一登入)</span><span class="sxs-lookup"><span data-stu-id="a6509-107">You can enable your users to automatically get signed-on to Heroku (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a6509-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="a6509-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a6509-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="a6509-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a6509-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="a6509-110">Prerequisites</span></span>

<span data-ttu-id="a6509-111">若要設定與 Heroku 的 Azure AD 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="a6509-111">To configure Azure AD integration with Heroku, you need the following items:</span></span>

- <span data-ttu-id="a6509-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a6509-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a6509-113">已啟用 Heroku 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a6509-113">A Heroku single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a6509-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="a6509-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a6509-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="a6509-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a6509-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="a6509-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a6509-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="a6509-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a6509-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="a6509-118">Scenario description</span></span>
<span data-ttu-id="a6509-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a6509-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a6509-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="a6509-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a6509-121">從資源庫加入 Heroku</span><span class="sxs-lookup"><span data-stu-id="a6509-121">Adding Heroku from the gallery</span></span>
2. <span data-ttu-id="a6509-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a6509-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-heroku-from-the-gallery"></a><span data-ttu-id="a6509-123">從資源庫加入 Heroku</span><span class="sxs-lookup"><span data-stu-id="a6509-123">Adding Heroku from the gallery</span></span>
<span data-ttu-id="a6509-124">若要設定 Heroku 與 Azure AD 整合，您需要從資源庫將 Heroku 加入受管理的 SaaS 應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="a6509-124">To configure the integration of Heroku into Azure AD, you need to add Heroku from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a6509-125">**若要從資源庫加入 Heroku，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="a6509-125">**To add Heroku from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a6509-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="a6509-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a6509-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="a6509-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a6509-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="a6509-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="a6509-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a6509-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="a6509-133">在搜尋方塊中輸入 **Heroku**。</span><span class="sxs-lookup"><span data-stu-id="a6509-133">In the search box, type **Heroku**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_search.png)

5. <span data-ttu-id="a6509-135">在結果窗格中，選取 [Heroku]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="a6509-135">In the results panel, select **Heroku**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a6509-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a6509-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="a6509-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Heroku 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a6509-138">In this section, you configure and test Azure AD single sign-on with Heroku based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a6509-139">若要讓單一登入運作，Azure AD 必須知道 Heroku 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="a6509-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Heroku is to a user in Azure AD.</span></span> <span data-ttu-id="a6509-140">換句話說，必須在某位 Azure AD 使用者與 Heroku 中的相關使用者之間，建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="a6509-140">In other words, a link relationship between an Azure AD user and the related user in Heroku needs to be established.</span></span>

<span data-ttu-id="a6509-141">在 Heroku 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="a6509-141">In Heroku, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a6509-142">若要設定及測試對 Heroku 的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="a6509-142">To configure and test Azure AD single sign-on with Heroku, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a6509-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="a6509-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a6509-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a6509-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a6509-145">**[建立 Heroku 測試使用者](#creating-a-heroku-test-user)** - 在 Heroku 中建立一個 Britta Simon 對應項目，其要與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="a6509-145">**[Creating a Heroku test user](#creating-a-heroku-test-user)** - to have a counterpart of Britta Simon in Heroku that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a6509-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a6509-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a6509-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="a6509-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a6509-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a6509-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a6509-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Heroku 中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="a6509-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Heroku application.</span></span>

<span data-ttu-id="a6509-150">**若要使用 Heroku 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="a6509-150">**To configure Azure AD single sign-on with Heroku, perform the following steps:**</span></span>

1. <span data-ttu-id="a6509-151">在 Azure 入口網站的 [Heroku] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="a6509-151">In the Azure portal, on the **Heroku** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="a6509-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="a6509-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_samlbase.png)

3. <span data-ttu-id="a6509-155">在 [Heroku 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a6509-155">On the **Heroku Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_url.png)

    <span data-ttu-id="a6509-157">a.</span><span class="sxs-lookup"><span data-stu-id="a6509-157">a.</span></span> <span data-ttu-id="a6509-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰</span><span class="sxs-lookup"><span data-stu-id="a6509-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>    
    `https://sso.heroku.com/saml/<company-name>/init`

    <span data-ttu-id="a6509-159">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="a6509-159">b.</span></span> <span data-ttu-id="a6509-160">在 [識別碼 URL] 文字方塊中，使用下列模式輸入 URL：</span><span class="sxs-lookup"><span data-stu-id="a6509-160">In the **Identifier URL** textbox, type a URL using the following pattern:</span></span>            
    `https://sso.heroku.com/saml/<company-name>`

    > [!NOTE]
    ><span data-ttu-id="a6509-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="a6509-161">These values are not real.</span></span> <span data-ttu-id="a6509-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="a6509-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a6509-163">您可以從 Heroku 小組取得這些值，本文後面幾節會有相關說明。</span><span class="sxs-lookup"><span data-stu-id="a6509-163">You get these values from Heroku team, which is described in later sections of this article.</span></span> 
        
4. <span data-ttu-id="a6509-164">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="a6509-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_certificate.png) 

5. <span data-ttu-id="a6509-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="a6509-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-heroku-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a6509-168">若要在 Heroku 中啟用 SSO，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a6509-168">To enable SSO in Heroku, perform the following steps:</span></span>
   
    <span data-ttu-id="a6509-169">a.</span><span class="sxs-lookup"><span data-stu-id="a6509-169">a.</span></span> <span data-ttu-id="a6509-170">以系統管理員身分登入 Heroku 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a6509-170">Log in to the Heroku account as an administrator.</span></span>

    <span data-ttu-id="a6509-171">b.</span><span class="sxs-lookup"><span data-stu-id="a6509-171">b.</span></span> <span data-ttu-id="a6509-172">按一下 [設定]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a6509-172">Click the **Settings** tab.</span></span>

    <span data-ttu-id="a6509-173">c.</span><span class="sxs-lookup"><span data-stu-id="a6509-173">c.</span></span> <span data-ttu-id="a6509-174">按一下 [單一登入] 頁面的 [上傳中繼資料]。</span><span class="sxs-lookup"><span data-stu-id="a6509-174">On the **Single Sign On Page**, click **Upload Metadata**.</span></span>

    <span data-ttu-id="a6509-175">d.</span><span class="sxs-lookup"><span data-stu-id="a6509-175">d.</span></span> <span data-ttu-id="a6509-176">上傳您從 Azure 入口網站下載的中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="a6509-176">Upload the metadata file, which you have downloaded from the Azure portal.</span></span>

    <span data-ttu-id="a6509-177">e.</span><span class="sxs-lookup"><span data-stu-id="a6509-177">e.</span></span> <span data-ttu-id="a6509-178">安裝成功後，系統管理員會看到確認對話方塊，以及供使用者使用的 SSO 登入 URL。</span><span class="sxs-lookup"><span data-stu-id="a6509-178">When the setup is successful, administrators see a confirmation dialog and the URL of the SSO Login for end users is displayed.</span></span> 

    <span data-ttu-id="a6509-179">f.</span><span class="sxs-lookup"><span data-stu-id="a6509-179">f.</span></span> <span data-ttu-id="a6509-180">複製 [Heroku 登入 URL] 和 [Heroku 實體識別碼] 值，返回 Azure 入口網站中的 [Heroku 網域和 URL] 區段，並將這些值分別貼到 [登入 URL] 和 [識別碼] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="a6509-180">Copy the **Heroku Login URL** and **Heroku Entity ID** values and go back to **Heroku Domain and URLs** section in Azure portal and paste these values into the **Sign-On Url** and **Identifier** textboxes respectively.</span></span>

    ![設定單一登入](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_52.png) 
    
8. <span data-ttu-id="a6509-182">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="a6509-182">Click **Next**.</span></span>

> [!TIP]
> <span data-ttu-id="a6509-183">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="a6509-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a6509-184">從 [Active Directory 企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="a6509-184">After adding this app from the **Active Directory Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a6509-185">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a6509-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a6509-186">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a6509-186">Creating an Azure AD test user</span></span>

<span data-ttu-id="a6509-187">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="a6509-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="a6509-189">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="a6509-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a6509-190">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="a6509-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-heroku-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a6509-192">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="a6509-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-heroku-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a6509-194">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="a6509-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-heroku-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a6509-196">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a6509-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-heroku-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a6509-198">a.</span><span class="sxs-lookup"><span data-stu-id="a6509-198">a.</span></span> <span data-ttu-id="a6509-199">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="a6509-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a6509-200">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="a6509-200">b.</span></span> <span data-ttu-id="a6509-201">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="a6509-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a6509-202">c.</span><span class="sxs-lookup"><span data-stu-id="a6509-202">c.</span></span> <span data-ttu-id="a6509-203">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="a6509-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a6509-204">d.</span><span class="sxs-lookup"><span data-stu-id="a6509-204">d.</span></span> <span data-ttu-id="a6509-205">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="a6509-205">Click **Create**.</span></span>
 
### <a name="creating-a-heroku-test-user"></a><span data-ttu-id="a6509-206">建立 Heroku 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a6509-206">Creating a Heroku test user</span></span>

<span data-ttu-id="a6509-207">在本節中，您要在 Heroku 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="a6509-207">In this section, you create a user called Britta Simon in Heroku.</span></span> <span data-ttu-id="a6509-208">Heroku 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="a6509-208">Heroku supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="a6509-209">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="a6509-209">There is no action item for you in this section.</span></span> <span data-ttu-id="a6509-210">存取 Heroku 時，如果使用者還不存在，就會建立新使用者。</span><span class="sxs-lookup"><span data-stu-id="a6509-210">A new user is created when accessing Heroku if the user doesn't exist yet.</span></span> <span data-ttu-id="a6509-211">帳戶佈建之後，使用者會收到驗證電子郵件，而且必須按一下通知連結。</span><span class="sxs-lookup"><span data-stu-id="a6509-211">After the account is provisioned, the end user receives a verification email and needs to click the acknowledgement link.</span></span>

>[!NOTE]
><span data-ttu-id="a6509-212">如果您需要手動建立使用者，您需要連絡 [Heroku 用戶端支援小組](https://www.heroku.com/support)。</span><span class="sxs-lookup"><span data-stu-id="a6509-212">If you need to create a user manually, you need to contact the [Heroku Client support team](https://www.heroku.com/support).</span></span>
>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a6509-213">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a6509-213">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a6509-214">在本節中，您會把 Heroku 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a6509-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Heroku.</span></span>

![指派使用者][200] 

<span data-ttu-id="a6509-216">**若要將 Britta Simon 指派給 Heroku，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="a6509-216">**To assign Britta Simon to Heroku, perform the following steps:**</span></span>

1. <span data-ttu-id="a6509-217">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="a6509-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="a6509-219">在應用程式清單中，選取 [Heroku] 。</span><span class="sxs-lookup"><span data-stu-id="a6509-219">In the applications list, select **Heroku**.</span></span>

    ![設定單一登入](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_app.png) 

3. <span data-ttu-id="a6509-221">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="a6509-221">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="a6509-223">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a6509-223">Click **Add** button.</span></span> <span data-ttu-id="a6509-224">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="a6509-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="a6509-226">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="a6509-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a6509-227">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a6509-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a6509-228">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a6509-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a6509-229">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="a6509-229">Testing single sign-on</span></span>

<span data-ttu-id="a6509-230">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="a6509-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a6509-231">當您在存取面板中按一下 [Heroku] 圖格時，應該會自動登入您的 Heroku 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a6509-231">When you click the Heroku tile in the Access Panel, you should get automatically signed-on to your Heroku application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a6509-232">其他資源</span><span class="sxs-lookup"><span data-stu-id="a6509-232">Additional resources</span></span>

* [<span data-ttu-id="a6509-233">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="a6509-233">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a6509-234">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="a6509-234">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_203.png
