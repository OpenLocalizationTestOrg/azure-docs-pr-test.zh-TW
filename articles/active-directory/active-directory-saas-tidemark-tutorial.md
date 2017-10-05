---
title: "教學課程：Azure Active Directory 與 Tidemark 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Tidemark 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5cf80d4e-6e8b-48ec-81c8-27872af5e5d5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 170dc58363b12ec671c2fab8c80c7720d3dbf352
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tidemark"></a><span data-ttu-id="8b302-103">教學課程：Azure Active Directory 與 Tidemark 整合</span><span class="sxs-lookup"><span data-stu-id="8b302-103">Tutorial: Azure Active Directory integration with Tidemark</span></span>

<span data-ttu-id="8b302-104">在本教學課程中，您將了解如何整合 Tidemark 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="8b302-104">In this tutorial, you learn how to integrate Tidemark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8b302-105">Tidemark 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="8b302-105">Integrating Tidemark with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8b302-106">您可以在 Azure AD 中控制可存取 Tidemark 的人員</span><span class="sxs-lookup"><span data-stu-id="8b302-106">You can control in Azure AD who has access to Tidemark</span></span>
- <span data-ttu-id="8b302-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Tidemark (單一登入)</span><span class="sxs-lookup"><span data-stu-id="8b302-107">You can enable your users to automatically get signed-on to Tidemark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8b302-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="8b302-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8b302-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="8b302-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b302-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="8b302-110">Prerequisites</span></span>

<span data-ttu-id="8b302-111">若要設定與 Tidemark 的 Azure AD 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="8b302-111">To configure Azure AD integration with Tidemark, you need the following items:</span></span>

- <span data-ttu-id="8b302-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="8b302-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8b302-113">已啟用 Tidemark 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="8b302-113">A Tidemark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8b302-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="8b302-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8b302-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="8b302-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8b302-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="8b302-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8b302-117">如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="8b302-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8b302-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="8b302-118">Scenario description</span></span>
<span data-ttu-id="8b302-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8b302-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8b302-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="8b302-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8b302-121">從資源庫加入 Tidemark</span><span class="sxs-lookup"><span data-stu-id="8b302-121">Adding Tidemark from the gallery</span></span>
2. <span data-ttu-id="8b302-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="8b302-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tidemark-from-the-gallery"></a><span data-ttu-id="8b302-123">從資源庫加入 Tidemark</span><span class="sxs-lookup"><span data-stu-id="8b302-123">Adding Tidemark from the gallery</span></span>
<span data-ttu-id="8b302-124">若要設定 Tidemark 與 Azure AD 整合，您需要從資源庫將 Tidemark 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="8b302-124">To configure the integration of Tidemark into Azure AD, you need to add Tidemark from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8b302-125">**若要從資源庫新增 Tidemark，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="8b302-125">**To add Tidemark from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8b302-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="8b302-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8b302-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="8b302-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8b302-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="8b302-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="8b302-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8b302-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="8b302-133">在搜尋方塊中，輸入 **Tidemark**。</span><span class="sxs-lookup"><span data-stu-id="8b302-133">In the search box, type **Tidemark**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_search.png)

5. <span data-ttu-id="8b302-135">在結果窗格中，選取 [Tidemark]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="8b302-135">In the results panel, select **Tidemark**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8b302-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="8b302-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8b302-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Tidemark 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8b302-138">In this section, you configure and test Azure AD single sign-on with Tidemark based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8b302-139">若要讓單一登入運作，Azure AD 必須知道 Tidemark 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="8b302-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Tidemark is to a user in Azure AD.</span></span> <span data-ttu-id="8b302-140">換句話說，必須在 Azure AD 使用者和 Tidemark 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="8b302-140">In other words, a link relationship between an Azure AD user and the related user in Tidemark needs to be established.</span></span>

<span data-ttu-id="8b302-141">在 Tidemark 中，將 Azure AD 中 [使用者名稱] 的值指派為 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="8b302-141">In Tidemark, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8b302-142">若要設定及測試對 Tidemark 的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="8b302-142">To configure and test Azure AD single sign-on with Tidemark, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8b302-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="8b302-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8b302-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8b302-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8b302-145">**[建立 Tidemark 測試使用者](#creating-a-tidemark-test-user)** - 使 Tidemark 中 Britta Simon 的對應使用者連結到該使用者在 Azure AD 中的代表身分。</span><span class="sxs-lookup"><span data-stu-id="8b302-145">**[Creating a Tidemark test user](#creating-a-tidemark-test-user)** - to have a counterpart of Britta Simon in Tidemark that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8b302-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8b302-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8b302-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="8b302-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8b302-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="8b302-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8b302-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Tidemark 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="8b302-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tidemark application.</span></span>

<span data-ttu-id="8b302-150">**若要使用 Tidemark 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="8b302-150">**To configure Azure AD single sign-on with Tidemark, perform the following steps:**</span></span>

1. <span data-ttu-id="8b302-151">在 Azure 入口網站的 [Tidemark] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="8b302-151">In the Azure portal, on the **Tidemark** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="8b302-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="8b302-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_samlbase.png)

3. <span data-ttu-id="8b302-155">在 [Tidemark 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="8b302-155">On the **Tidemark Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_url.png)

    <span data-ttu-id="8b302-157">a.</span><span class="sxs-lookup"><span data-stu-id="8b302-157">a.</span></span> <span data-ttu-id="8b302-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰</span><span class="sxs-lookup"><span data-stu-id="8b302-158">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span> 
    | |
    |--|
    | `https://<subdomain>.tidemark.com/login` |
    | `https://<subdomain>.tidemark.net/login` |

    <span data-ttu-id="8b302-159">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="8b302-159">b.</span></span> <span data-ttu-id="8b302-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：</span><span class="sxs-lookup"><span data-stu-id="8b302-160">In the **Identifier** textbox, type a URL using the following patterns:</span></span> 
    | |
    |--|
    | `https://<subdomain>.tidemark.com/saml` |
    | `https://<subdomain>.tidemark.net/saml` |

    > [!NOTE] 
    > <span data-ttu-id="8b302-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="8b302-161">These values are not real.</span></span> <span data-ttu-id="8b302-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="8b302-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8b302-163">請連絡 [Tidemark 客戶支援小組](http://www.tidemark.com/contact-us)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="8b302-163">Contact [Tidemark Client support team](http://www.tidemark.com/contact-us) to get these values.</span></span> 
 
4. <span data-ttu-id="8b302-164">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="8b302-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_certificate.png) 

5. <span data-ttu-id="8b302-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="8b302-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-tidemark-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8b302-168">在 [Tidemark 組態] 區段上，按一下 [設定 Tidemark] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="8b302-168">On the **Tidemark Configuration** section, click **Configure Tidemark** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8b302-169">從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="8b302-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_configure.png) 

7. <span data-ttu-id="8b302-171">若要在 **Tidemark** 端設定單一登入，您必須將已下載的 [憑證]\(Base64\)、[SAML實體辨識碼]、[登出 URL] 和 [SAML 單一登入服務 URL] 傳送給 [Tidemark 支援小組](http://www.tidemark.com/contact-us)。</span><span class="sxs-lookup"><span data-stu-id="8b302-171">To configure single sign-on on **Tidemark** side, you need to send the downloaded **Certificate(Base64), SAML Entity ID, Sign-Out URL and SAML Single Sign-On Service URL** to [Tidemark support team](http://www.tidemark.com/contact-us).</span></span> <span data-ttu-id="8b302-172">他們會進行此設定，讓兩端的 SAML SSO 連線都設定正確。</span><span class="sxs-lookup"><span data-stu-id="8b302-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="8b302-173">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="8b302-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8b302-174">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="8b302-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8b302-175">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8b302-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8b302-176">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="8b302-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="8b302-177">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="8b302-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="8b302-179">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="8b302-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8b302-180">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="8b302-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tidemark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8b302-182">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="8b302-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tidemark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8b302-184">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="8b302-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tidemark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8b302-186">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="8b302-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tidemark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8b302-188">a.</span><span class="sxs-lookup"><span data-stu-id="8b302-188">a.</span></span> <span data-ttu-id="8b302-189">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="8b302-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8b302-190">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="8b302-190">b.</span></span> <span data-ttu-id="8b302-191">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="8b302-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8b302-192">c.</span><span class="sxs-lookup"><span data-stu-id="8b302-192">c.</span></span> <span data-ttu-id="8b302-193">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="8b302-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8b302-194">d.</span><span class="sxs-lookup"><span data-stu-id="8b302-194">d.</span></span> <span data-ttu-id="8b302-195">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="8b302-195">Click **Create**.</span></span>
 
### <a name="creating-a-tidemark-test-user"></a><span data-ttu-id="8b302-196">建立 Tidemark 測試使用者</span><span class="sxs-lookup"><span data-stu-id="8b302-196">Creating a Tidemark test user</span></span>

<span data-ttu-id="8b302-197">本節的目標是在 Tidemark 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="8b302-197">The objective of this section is to create a user called Britta Simon in Tidemark.</span></span> <span data-ttu-id="8b302-198">請與 [Tidemark 支援小組](http://www.tidemark.com/contact-us)合作，在 Tidemark 帳戶中新增使用者。</span><span class="sxs-lookup"><span data-stu-id="8b302-198">Please work with [Tidemark support team](http://www.tidemark.com/contact-us) to add the users in the Tidemark account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8b302-199">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="8b302-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8b302-200">在本節中，您會將 Tidemark 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8b302-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tidemark.</span></span>

![指派使用者][200] 

<span data-ttu-id="8b302-202">**若要將 Britta Simon 指派到 Tidemark，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="8b302-202">**To assign Britta Simon to Tidemark, perform the following steps:**</span></span>

1. <span data-ttu-id="8b302-203">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="8b302-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="8b302-205">在應用程式清單中，選取 [Tidemark] 。</span><span class="sxs-lookup"><span data-stu-id="8b302-205">In the applications list, select **Tidemark**.</span></span>

    ![設定單一登入](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_app.png) 

3. <span data-ttu-id="8b302-207">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="8b302-207">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="8b302-209">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8b302-209">Click **Add** button.</span></span> <span data-ttu-id="8b302-210">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="8b302-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="8b302-212">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="8b302-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8b302-213">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8b302-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8b302-214">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8b302-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8b302-215">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="8b302-215">Testing single sign-on</span></span>

<span data-ttu-id="8b302-216">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="8b302-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8b302-217">當您在存取面板中按一下 [Tidemark] 磚時，應該會自動登入您的 Tidemark 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8b302-217">When you click the Tidemark tile in the Access Panel, you should get automatically signed-on to your Tidemark application.</span></span>
<span data-ttu-id="8b302-218">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="8b302-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8b302-219">其他資源</span><span class="sxs-lookup"><span data-stu-id="8b302-219">Additional resources</span></span>

* [<span data-ttu-id="8b302-220">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="8b302-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8b302-221">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="8b302-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_203.png
