---
title: "教學課程：Azure Active Directory 與 BGS Online 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 BGS Online 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4fd6b29b-1b46-4fd1-9f5e-16b1c9d892cd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: d1abd3f8e2980e03fc092613183a261880fbce38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bgs-online"></a><span data-ttu-id="24704-103">教學課程：Azure Active Directory 與 BGS Online 整合</span><span class="sxs-lookup"><span data-stu-id="24704-103">Tutorial: Azure Active Directory integration with BGS Online</span></span>

<span data-ttu-id="24704-104">在本教學課程中，您將了解如何整合 BGS Online 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="24704-104">In this tutorial, you learn how to integrate BGS Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="24704-105">將 BGS Online 與 Azure AD 整合可提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="24704-105">Integrating BGS Online with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="24704-106">您可以在 Azure AD 中控制可存取 BGS Online 的人員</span><span class="sxs-lookup"><span data-stu-id="24704-106">You can control in Azure AD who has access to BGS Online</span></span>
- <span data-ttu-id="24704-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 BGS Online (單一登入)</span><span class="sxs-lookup"><span data-stu-id="24704-107">You can enable your users to automatically get signed-on to BGS Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="24704-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="24704-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="24704-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="24704-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24704-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="24704-110">Prerequisites</span></span>

<span data-ttu-id="24704-111">若要設定 Azure AD 與 BGS Online 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="24704-111">To configure Azure AD integration with BGS Online, you need the following items:</span></span>

- <span data-ttu-id="24704-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="24704-112">An Azure AD subscription</span></span>
- <span data-ttu-id="24704-113">已啟用 BGS Online 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="24704-113">A BGS Online single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="24704-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="24704-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="24704-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="24704-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="24704-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="24704-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="24704-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="24704-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="24704-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="24704-118">Scenario description</span></span>
<span data-ttu-id="24704-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="24704-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="24704-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="24704-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="24704-121">從資源庫新增 BGS Online</span><span class="sxs-lookup"><span data-stu-id="24704-121">Adding BGS Online from the gallery</span></span>
2. <span data-ttu-id="24704-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="24704-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bgs-online-from-the-gallery"></a><span data-ttu-id="24704-123">從資源庫新增 BGS Online</span><span class="sxs-lookup"><span data-stu-id="24704-123">Adding BGS Online from the gallery</span></span>
<span data-ttu-id="24704-124">若要設定將 BGS Online 整合到 Azure AD 中，您需要從資源庫將 BGS Online 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="24704-124">To configure the integration of BGS Online into Azure AD, you need to add BGS Online from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="24704-125">**若要從資源庫新增 BGS Online，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="24704-125">**To add BGS Online from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="24704-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="24704-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="24704-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="24704-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="24704-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="24704-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="24704-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="24704-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="24704-133">在搜尋方塊中，輸入 **BGS Online**。</span><span class="sxs-lookup"><span data-stu-id="24704-133">In the search box, type **BGS Online**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_search.png)

5. <span data-ttu-id="24704-135">在結果面板中，選取 [BGS Online]，然後按一下 [新增] 按鈕以新增該應用程式。</span><span class="sxs-lookup"><span data-stu-id="24704-135">In the results panel, select **BGS Online**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="24704-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="24704-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="24704-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 BGS Online 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="24704-138">In this section, you configure and test Azure AD single sign-on with BGS Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="24704-139">若要讓單一登入能夠運作，Azure AD 必須知道 BGS Online 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="24704-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BGS Online is to a user in Azure AD.</span></span> <span data-ttu-id="24704-140">換句話說，必須在 Azure AD 使用者與 BGS Online 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="24704-140">In other words, a link relationship between an Azure AD user and the related user in BGS Online needs to be established.</span></span>

<span data-ttu-id="24704-141">在 BGS Online 中，將 [Username] 的值指派為 Azure AD 中 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="24704-141">In BGS Online, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="24704-142">若要設定及測試與 BGS Online 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="24704-142">To configure and test Azure AD single sign-on with BGS Online, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="24704-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="24704-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="24704-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="24704-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="24704-145">**[建立 BGS Online 測試使用者](#creating-a-bgs-online-test-user)** - 在 BGS Online 中建立一個與 Azure AD 中代表 Britta Simon 之項目連結的 Britta Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="24704-145">**[Creating a BGS Online test user](#creating-a-bgs-online-test-user)** - to have a counterpart of Britta Simon in BGS Online that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="24704-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="24704-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="24704-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="24704-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="24704-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="24704-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="24704-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 BGS Online 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="24704-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BGS Online application.</span></span>

<span data-ttu-id="24704-150">**若要設定與 BGS Online 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="24704-150">**To configure Azure AD single sign-on with BGS Online, perform the following steps:**</span></span>

1. <span data-ttu-id="24704-151">在 Azure 入口網站的 [BGS Online] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="24704-151">In the Azure portal, on the **BGS Online** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="24704-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="24704-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_samlbase.png)

3. <span data-ttu-id="24704-155">在 [BGS Online 網域及 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="24704-155">On the **BGS Online Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_url.png)

    <span data-ttu-id="24704-157">a.</span><span class="sxs-lookup"><span data-stu-id="24704-157">a.</span></span> <span data-ttu-id="24704-158">在 [識別碼] 文字方塊中，使用下列模式來輸入 URL：</span><span class="sxs-lookup"><span data-stu-id="24704-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>

    <span data-ttu-id="24704-159">針對生產環境，請使用此模式 `https://<company name>.millwardbrown.report`</span><span class="sxs-lookup"><span data-stu-id="24704-159">For production environment, use this pattern `https://<company name>.millwardbrown.report`</span></span> 

    <span data-ttu-id="24704-160">針對測試環境，請使用此模式 `https://millwardbrown.marketingtracker.nl/mt5/`</span><span class="sxs-lookup"><span data-stu-id="24704-160">For test environment, use this pattern `https://millwardbrown.marketingtracker.nl/mt5/`</span></span>

    <span data-ttu-id="24704-161">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="24704-161">b.</span></span> <span data-ttu-id="24704-162">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：</span><span class="sxs-lookup"><span data-stu-id="24704-162">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    
    <span data-ttu-id="24704-163">針對生產環境，請使用此模式 `https://<company name>.millwardbrown.report/sso/saml/AssertionConsumerService.aspx`</span><span class="sxs-lookup"><span data-stu-id="24704-163">For production environment, use this pattern `https://<company name>.millwardbrown.report/sso/saml/AssertionConsumerService.aspx`</span></span> 
      
    <span data-ttu-id="24704-164">針對測試環境，請使用此模式 `https://millwardbrown.marketingtracker.nl/mt5/sso/saml/AssertionConsumerService.aspx`</span><span class="sxs-lookup"><span data-stu-id="24704-164">For test environment, use this pattern `https://millwardbrown.marketingtracker.nl/mt5/sso/saml/AssertionConsumerService.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="24704-165">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="24704-165">These values are not real.</span></span> <span data-ttu-id="24704-166">請使用實際的識別碼和回覆 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="24704-166">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="24704-167">請連絡 [BGS Online 支援小組](mailTo:bgsdashboardteam@millwardbrown.com)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="24704-167">Contact [BGS Online support team](mailTo:bgsdashboardteam@millwardbrown.com) to get these values.</span></span>
 

4. <span data-ttu-id="24704-168">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="24704-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_certificate.png) 

5. <span data-ttu-id="24704-170">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="24704-170">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-bgsonline-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="24704-172">在 [BGS Online 組態] 區段上，按一下 [設定 BGS Online] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="24704-172">On the **BGS Online Configuration** section, click **Configure BGS Online** to open **Configure sign-on** window.</span></span> <span data-ttu-id="24704-173">從 [快速參考] 區段中複製 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="24704-173">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_configure.png) 

7. <span data-ttu-id="24704-175">若要在 **BGS Online** 端設定單一登入，您必須將已下載的「中繼資料 XML」和「SAML 單一登入服務 URL」傳送給 [BGS Online 支援小組](mailto:bgsdashboardteam@millwardbrown.com)。</span><span class="sxs-lookup"><span data-stu-id="24704-175">To configure single sign-on on **BGS Online** side, you need to send the downloaded **Metadata XML** and **SAML Single Sign-On Service URL** to [BGS Online support team](mailto:bgsdashboardteam@millwardbrown.com).</span></span> 


> [!TIP]
> <span data-ttu-id="24704-176">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="24704-176">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="24704-177">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="24704-177">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="24704-178">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="24704-178">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="24704-179">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="24704-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="24704-180">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="24704-180">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="24704-182">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="24704-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="24704-183">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="24704-183">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="24704-185">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="24704-185">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="24704-187">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="24704-187">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="24704-189">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="24704-189">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="24704-191">a.</span><span class="sxs-lookup"><span data-stu-id="24704-191">a.</span></span> <span data-ttu-id="24704-192">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="24704-192">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="24704-193">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="24704-193">b.</span></span> <span data-ttu-id="24704-194">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="24704-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="24704-195">c.</span><span class="sxs-lookup"><span data-stu-id="24704-195">c.</span></span> <span data-ttu-id="24704-196">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="24704-196">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="24704-197">d.</span><span class="sxs-lookup"><span data-stu-id="24704-197">d.</span></span> <span data-ttu-id="24704-198">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="24704-198">Click **Create**.</span></span>
 
### <a name="creating-a-bgs-online-test-user"></a><span data-ttu-id="24704-199">建立 BGS Online 測試使用者</span><span class="sxs-lookup"><span data-stu-id="24704-199">Creating a BGS Online test user</span></span>

<span data-ttu-id="24704-200">在本節中，您會在 BGS Online 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="24704-200">In this section, you create a user called Britta Simon in BGS Online.</span></span> <span data-ttu-id="24704-201">請與 [BGS Online 支援小組](mailto:bgsdashboardteam@millwardbrown.com)合作，在 BGS Online 平台中新增使用者。</span><span class="sxs-lookup"><span data-stu-id="24704-201">Work with [BGS Online support team](mailto:bgsdashboardteam@millwardbrown.com) to add the users in the BGS Online platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="24704-202">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="24704-202">Assigning the Azure AD test user</span></span>

<span data-ttu-id="24704-203">在本節中，您會將 BGS Online 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="24704-203">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BGS Online.</span></span>

![指派使用者][200] 

<span data-ttu-id="24704-205">**若要將 Britta Simon 指派給 BGS Online，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="24704-205">**To assign Britta Simon to BGS Online, perform the following steps:**</span></span>

1. <span data-ttu-id="24704-206">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="24704-206">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="24704-208">在應用程式清單中，選取 [BGS Online]。</span><span class="sxs-lookup"><span data-stu-id="24704-208">In the applications list, select **BGS Online**.</span></span>

    ![設定單一登入](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_app.png) 

3. <span data-ttu-id="24704-210">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="24704-210">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="24704-212">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="24704-212">Click **Add** button.</span></span> <span data-ttu-id="24704-213">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="24704-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="24704-215">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="24704-215">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="24704-216">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="24704-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="24704-217">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="24704-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="24704-218">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="24704-218">Testing single sign-on</span></span>

<span data-ttu-id="24704-219">在本節中，您會使用存取面板來測試您的 Azure AD SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="24704-219">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="24704-220">當您在「存取面板」中按一下 [BGS Online] 圖格時，應該會自動登入您的 BGS Online 應用程式。</span><span class="sxs-lookup"><span data-stu-id="24704-220">When you click the BGS Online tile in the Access Panel, you should get automatically signed-on to your BGS Online application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="24704-221">其他資源</span><span class="sxs-lookup"><span data-stu-id="24704-221">Additional resources</span></span>

* [<span data-ttu-id="24704-222">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="24704-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="24704-223">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="24704-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_203.png

