---
title: "教學課程：Azure Active Directory 與 Certify 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Certify 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0b36e020-175a-4534-b341-85260739f889
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: bbb2357d17535de438555a0b1f8256b134c8a40e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-certify"></a><span data-ttu-id="d9abd-103">教學課程：Azure Active Directory 與 Certify 整合</span><span class="sxs-lookup"><span data-stu-id="d9abd-103">Tutorial: Azure Active Directory integration with Certify</span></span>

<span data-ttu-id="d9abd-104">在本教學課程中，您將了解如何整合 Certify 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="d9abd-104">In this tutorial, you learn how to integrate Certify with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d9abd-105">將 Certify 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="d9abd-105">Integrating Certify with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d9abd-106">您可以在 Azure AD 中控制可存取 Certify 的人員</span><span class="sxs-lookup"><span data-stu-id="d9abd-106">You can control in Azure AD who has access to Certify</span></span>
- <span data-ttu-id="d9abd-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Certify (單一登入)</span><span class="sxs-lookup"><span data-stu-id="d9abd-107">You can enable your users to automatically get signed-on to Certify (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d9abd-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="d9abd-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d9abd-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="d9abd-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9abd-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="d9abd-110">Prerequisites</span></span>

<span data-ttu-id="d9abd-111">若要設定 Azure AD 與 Certify 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="d9abd-111">To configure Azure AD integration with Certify, you need the following items:</span></span>

- <span data-ttu-id="d9abd-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d9abd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d9abd-113">已啟用 Certify 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d9abd-113">A Certify single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d9abd-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="d9abd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d9abd-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="d9abd-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d9abd-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="d9abd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d9abd-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="d9abd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d9abd-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="d9abd-118">Scenario description</span></span>
<span data-ttu-id="d9abd-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d9abd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d9abd-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="d9abd-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d9abd-121">從資源庫新增 Certify</span><span class="sxs-lookup"><span data-stu-id="d9abd-121">Adding Certify from the gallery</span></span>
2. <span data-ttu-id="d9abd-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d9abd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-certify-from-the-gallery"></a><span data-ttu-id="d9abd-123">從資源庫新增 Certify</span><span class="sxs-lookup"><span data-stu-id="d9abd-123">Adding Certify from the gallery</span></span>
<span data-ttu-id="d9abd-124">若要設定將 Certify 整合到 Azure AD 中，您需要從資源庫將 Certify 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="d9abd-124">To configure the integration of Certify into Azure AD, you need to add Certify from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d9abd-125">**若要從資源庫新增 Certify，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d9abd-125">**To add Certify from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d9abd-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="d9abd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d9abd-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d9abd-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d9abd-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d9abd-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="d9abd-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d9abd-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="d9abd-133">在搜尋方塊中，輸入 **Certify**。</span><span class="sxs-lookup"><span data-stu-id="d9abd-133">In the search box, type **Certify**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-certify-tutorial/tutorial_certify_search.png)

5. <span data-ttu-id="d9abd-135">在結果窗格中，選取 [Certify]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="d9abd-135">In the results panel, select **Certify**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-certify-tutorial/tutorial_certify_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d9abd-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d9abd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d9abd-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Certify 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d9abd-138">In this section, you configure and test Azure AD single sign-on with Certify based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d9abd-139">若要讓單一登入運作，Azure AD 必須知道 Certify 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="d9abd-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Certify is to a user in Azure AD.</span></span> <span data-ttu-id="d9abd-140">換句話說，必須在 Azure AD 使用者與 Certify 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="d9abd-140">In other words, a link relationship between an Azure AD user and the related user in Certify needs to be established.</span></span>

<span data-ttu-id="d9abd-141">在 Certify 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="d9abd-141">In Certify, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d9abd-142">若要設定及測試與 Certify 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="d9abd-142">To configure and test Azure AD single sign-on with Certify, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d9abd-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="d9abd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d9abd-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d9abd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d9abd-145">**[建立 Certify 測試使用者](#creating-a-certify-test-user)** - 在 Certify 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表 Britta Simon 的項目連結。</span><span class="sxs-lookup"><span data-stu-id="d9abd-145">**[Creating a Certify test user](#creating-a-certify-test-user)** - to have a counterpart of Britta Simon in Certify that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d9abd-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d9abd-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d9abd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="d9abd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d9abd-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d9abd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d9abd-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Certify 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="d9abd-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Certify application.</span></span>

<span data-ttu-id="d9abd-150">**若要設定與 Certify 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d9abd-150">**To configure Azure AD single sign-on with Certify, perform the following steps:**</span></span>

1. <span data-ttu-id="d9abd-151">在 Azure 入口網站的 [Certify] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="d9abd-151">In the Azure portal, on the **Certify** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="d9abd-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="d9abd-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-certify-tutorial/tutorial_certify_samlbase.png)

3. <span data-ttu-id="d9abd-155">在 [Certify 網域及 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d9abd-155">On the **Certify Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-certify-tutorial/tutorial_certify_url.png)

    <span data-ttu-id="d9abd-157">在 [識別碼] 文字方塊中，輸入 URL：`https://www.certify.com`</span><span class="sxs-lookup"><span data-stu-id="d9abd-157">In the **Identifier** textbox, type the URL: `https://www.certify.com`</span></span>

4. <span data-ttu-id="d9abd-158">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (原始)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="d9abd-158">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-certify-tutorial/tutorial_certify_certificate.png) 

5. <span data-ttu-id="d9abd-160">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="d9abd-160">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-certify-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d9abd-162">在 [Certify 組態] 區段上，按一下 [設定 Certify] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="d9abd-162">On the **Certify Configuration** section, click **Configure Certify** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d9abd-163">從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="d9abd-163">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-certify-tutorial/tutorial_certify_configure.png) 

7. <span data-ttu-id="d9abd-165">若要在 **Certify** 端設定單一登入，您必須將已下載的「憑證 (原始)」、「登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL」傳送給 [Certify 支援小組](mailto:support@certify.com)。</span><span class="sxs-lookup"><span data-stu-id="d9abd-165">To configure single sign-on on **Certify** side, you need to send the downloaded **Certificate(Raw)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Certify support team](mailto:support@certify.com).</span></span> <span data-ttu-id="d9abd-166">他們會進行此設定，讓兩端的 SAML SSO 連線都設定正確。</span><span class="sxs-lookup"><span data-stu-id="d9abd-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="d9abd-167">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="d9abd-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d9abd-168">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="d9abd-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d9abd-169">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d9abd-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d9abd-170">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d9abd-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="d9abd-171">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="d9abd-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="d9abd-173">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d9abd-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d9abd-174">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="d9abd-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-certify-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d9abd-176">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="d9abd-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-certify-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d9abd-178">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="d9abd-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-certify-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d9abd-180">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d9abd-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-certify-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d9abd-182">a.</span><span class="sxs-lookup"><span data-stu-id="d9abd-182">a.</span></span> <span data-ttu-id="d9abd-183">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="d9abd-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d9abd-184">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="d9abd-184">b.</span></span> <span data-ttu-id="d9abd-185">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="d9abd-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d9abd-186">c.</span><span class="sxs-lookup"><span data-stu-id="d9abd-186">c.</span></span> <span data-ttu-id="d9abd-187">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="d9abd-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d9abd-188">d.</span><span class="sxs-lookup"><span data-stu-id="d9abd-188">d.</span></span> <span data-ttu-id="d9abd-189">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="d9abd-189">Click **Create**.</span></span>
 
### <a name="creating-a-certify-test-user"></a><span data-ttu-id="d9abd-190">建立 Certify 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d9abd-190">Creating a Certify test user</span></span>

<span data-ttu-id="d9abd-191">本節的目標是要在 Certify 中建立一個名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="d9abd-191">The objective of this section is to create a user called Britta Simon in Certify.</span></span> <span data-ttu-id="d9abd-192">Certify 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="d9abd-192">Certify supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="d9abd-193">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="d9abd-193">There is no action item for you in this section.</span></span> <span data-ttu-id="d9abd-194">嘗試存取 Certify 時，如果使用者還不存在，就會建立新使用者。</span><span class="sxs-lookup"><span data-stu-id="d9abd-194">A new user will be created during an attempt to access Certify if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="d9abd-195">如果您需要手動建立使用者，您需要連絡 [Certify 支援小組](mailto:support@certify.com)。</span><span class="sxs-lookup"><span data-stu-id="d9abd-195">If you need to create an user manually, you need to contact the [Certify support team](mailto:support@certify.com).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d9abd-196">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d9abd-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d9abd-197">在本節中，您會將 Certify 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d9abd-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Certify.</span></span>

![指派使用者][200] 

<span data-ttu-id="d9abd-199">**若要將 Britta Simon 指派給 Certify，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d9abd-199">**To assign Britta Simon to Certify, perform the following steps:**</span></span>

1. <span data-ttu-id="d9abd-200">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d9abd-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="d9abd-202">在應用程式清單中，選取 [Certify] 。</span><span class="sxs-lookup"><span data-stu-id="d9abd-202">In the applications list, select **Certify**.</span></span>

    ![設定單一登入](./media/active-directory-saas-certify-tutorial/tutorial_certify_app.png) 

3. <span data-ttu-id="d9abd-204">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="d9abd-204">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="d9abd-206">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d9abd-206">Click **Add** button.</span></span> <span data-ttu-id="d9abd-207">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="d9abd-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="d9abd-209">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="d9abd-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d9abd-210">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d9abd-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d9abd-211">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d9abd-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d9abd-212">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="d9abd-212">Testing single sign-on</span></span>

<span data-ttu-id="d9abd-213">本節的目標是要使用「存取面板」來測試您的 Azure AD SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="d9abd-213">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="d9abd-214">當您在「存取面板」中按一下 [Certify] 磚時，應該會自動登入您的 Certify 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d9abd-214">When you click the Certify tile in the Access Panel, you should get automatically signed-on to your Certify application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d9abd-215">其他資源</span><span class="sxs-lookup"><span data-stu-id="d9abd-215">Additional resources</span></span>

* [<span data-ttu-id="d9abd-216">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="d9abd-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d9abd-217">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="d9abd-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-certify-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-certify-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-certify-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-certify-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-certify-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-certify-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-certify-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-certify-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-certify-tutorial/tutorial_general_203.png

