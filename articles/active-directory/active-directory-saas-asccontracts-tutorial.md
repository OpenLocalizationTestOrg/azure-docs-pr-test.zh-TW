---
title: "教學課程：Azure Active Directory 與 ASC Contracts 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 ASC Contracts 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f7f54202-1581-4e55-a97e-02633ff9382d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/21/2017
ms.author: jeedes
ms.openlocfilehash: 87ea3cc55f9683e7d5b9912a87d675575cea0347
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asc-contracts"></a><span data-ttu-id="9b2b5-103">教學課程：Azure Active Directory 與 ASC Contracts</span><span class="sxs-lookup"><span data-stu-id="9b2b5-103">Tutorial: Azure Active Directory integration with ASC Contracts</span></span>

<span data-ttu-id="9b2b5-104">在本教學課程中，您將了解如何整合 ASC Contracts 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-104">In this tutorial, you learn how to integrate ASC Contracts with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9b2b5-105">ASC Contracts 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="9b2b5-105">Integrating ASC Contracts with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9b2b5-106">您可以在 Azure AD 中控制可存取 ASC Contracts 的人員</span><span class="sxs-lookup"><span data-stu-id="9b2b5-106">You can control in Azure AD who has access to ASC Contracts</span></span>
- <span data-ttu-id="9b2b5-107">您可以讓您的使用者使用他們的 Azure AD 帳戶自動登入 ASC Contracts (單一登入)</span><span class="sxs-lookup"><span data-stu-id="9b2b5-107">You can enable your users to automatically get signed-on to ASC Contracts (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9b2b5-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="9b2b5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9b2b5-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b2b5-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="9b2b5-110">Prerequisites</span></span>

<span data-ttu-id="9b2b5-111">若要設定與 ASC Contracts 的 Azure AD 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="9b2b5-111">To configure Azure AD integration with ASC Contracts, you need the following items:</span></span>

- <span data-ttu-id="9b2b5-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="9b2b5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9b2b5-113">啟用 ASC Contracts 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="9b2b5-113">An ASC Contracts single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9b2b5-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9b2b5-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="9b2b5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9b2b5-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9b2b5-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9b2b5-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="9b2b5-118">Scenario description</span></span>
<span data-ttu-id="9b2b5-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9b2b5-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="9b2b5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9b2b5-121">從資源庫新增 ASC Contracts</span><span class="sxs-lookup"><span data-stu-id="9b2b5-121">Adding ASC Contracts from the gallery</span></span>
2. <span data-ttu-id="9b2b5-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="9b2b5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-asc-contracts-from-the-gallery"></a><span data-ttu-id="9b2b5-123">從資源庫新增 ASC Contracts</span><span class="sxs-lookup"><span data-stu-id="9b2b5-123">Adding ASC Contracts from the gallery</span></span>
<span data-ttu-id="9b2b5-124">若要設定將 ASC Contracts 整合到 Azure AD 中，您需要從資源庫將 ASC Contracts 新增到受管理的 SaaS app 清單。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-124">To configure the integration of ASC Contracts into Azure AD, you need to add ASC Contracts from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9b2b5-125">**若要從資源庫新增 ASC Contracts，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="9b2b5-125">**To add ASC Contracts from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9b2b5-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9b2b5-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9b2b5-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="9b2b5-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="9b2b5-133">在搜尋方塊中，輸入 **ASC Contracts**。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-133">In the search box, type **ASC Contracts**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_search.png)

5. <span data-ttu-id="9b2b5-135">在結果窗格中，選取 [ASC Contracts]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-135">In the results panel, select **ASC Contracts**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9b2b5-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="9b2b5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9b2b5-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 ASC Contracts 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-138">In this section, you configure and test Azure AD single sign-on with ASC Contracts based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9b2b5-139">若要讓單一登入能夠運作，Azure AD 必須知道 ASC Contracts 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ASC Contracts is to a user in Azure AD.</span></span> <span data-ttu-id="9b2b5-140">換句話說，必須在 Azure AD 使用者和 ASC Contracts 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-140">In other words, a link relationship between an Azure AD user and the related user in ASC Contracts needs to be established.</span></span>

<span data-ttu-id="9b2b5-141">建立此連結關聯性的方法，就是指派 Azure AD 中**使用者名稱**的值作為 ASC Contracts 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ASC Contracts.</span></span>

<span data-ttu-id="9b2b5-142">若要設定及測試對 ASC Contracts 的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="9b2b5-142">To configure and test Azure AD single sign-on with ASC Contracts, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9b2b5-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9b2b5-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9b2b5-145">**[建立 ASC Contracts 測試使用者](#creating-an-asc-contracts-test-user)** - 在 ASC Contracts 中建立一個與 Azure AD 中代表 Britta Simon 的項目連結的 Britta Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-145">**[Creating an ASC Contracts test user](#creating-an-asc-contracts-test-user)** - to have a counterpart of Britta Simon in ASC Contracts that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9b2b5-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9b2b5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9b2b5-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="9b2b5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9b2b5-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 ASC Contracts 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ASC Contracts application.</span></span>

<span data-ttu-id="9b2b5-150">**若要使用 ASC Contracts 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="9b2b5-150">**To configure Azure AD single sign-on with ASC Contracts, perform the following steps:**</span></span>

1. <span data-ttu-id="9b2b5-151">在 Azure 入口網站的 [ASC Contracts] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-151">In the Azure portal, on the **ASC Contracts** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="9b2b5-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_samlbase.png)

3. <span data-ttu-id="9b2b5-155">在 [ASC Contracts 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9b2b5-155">On the **ASC Contracts Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_url.png)

    <span data-ttu-id="9b2b5-157">a.</span><span class="sxs-lookup"><span data-stu-id="9b2b5-157">a.</span></span> <span data-ttu-id="9b2b5-158">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<subdomain>.asccontracts.com/shibboleth`</span><span class="sxs-lookup"><span data-stu-id="9b2b5-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.asccontracts.com/shibboleth`</span></span>

    <span data-ttu-id="9b2b5-159">b.</span><span class="sxs-lookup"><span data-stu-id="9b2b5-159">b.</span></span> <span data-ttu-id="9b2b5-160">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://<subdomain>.asccontracts.com/shibboleth.sso/login`</span><span class="sxs-lookup"><span data-stu-id="9b2b5-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.asccontracts.com/shibboleth.sso/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9b2b5-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-161">These values are not real.</span></span> <span data-ttu-id="9b2b5-162">請使用實際的識別碼和回覆 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="9b2b5-163">請連絡 ASC Networks Inc. (ASC) 小組 (電話是 **613.599.6178**) 以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-163">Contact ASC Networks Inc. (ASC) team at **613.599.6178** to get these values.</span></span>

4. <span data-ttu-id="9b2b5-164">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_certificate.png) 

5. <span data-ttu-id="9b2b5-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-asccontracts-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9b2b5-168">若要在 **ASC Contracts** 端設定單一登入，請致電 ASC Networks Inc. (ASC) 支援小組 (電話是 **613.599.6178**)，並向他們提供所下載的**中繼資料 XML**。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-168">To configure single sign-on on **ASC Contracts** side, call ASC Networks Inc. (ASC) support at **613.599.6178** and provide them with the downloaded **Metadata XML**.</span></span> <span data-ttu-id="9b2b5-169">他們將會此應用程式設定妥當，讓兩端的 SAML SSO 連線都設定正確。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-169">They set this application up to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="9b2b5-170">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="9b2b5-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9b2b5-171">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9b2b5-172">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9b2b5-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9b2b5-173">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="9b2b5-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="9b2b5-174">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="9b2b5-176">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="9b2b5-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9b2b5-177">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9b2b5-179">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9b2b5-181">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9b2b5-183">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9b2b5-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9b2b5-185">a.</span><span class="sxs-lookup"><span data-stu-id="9b2b5-185">a.</span></span> <span data-ttu-id="9b2b5-186">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9b2b5-187">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-187">b.</span></span> <span data-ttu-id="9b2b5-188">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9b2b5-189">c.</span><span class="sxs-lookup"><span data-stu-id="9b2b5-189">c.</span></span> <span data-ttu-id="9b2b5-190">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9b2b5-191">d.</span><span class="sxs-lookup"><span data-stu-id="9b2b5-191">d.</span></span> <span data-ttu-id="9b2b5-192">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-192">Click **Create**.</span></span>
 
### <a name="creating-an-asc-contracts-test-user"></a><span data-ttu-id="9b2b5-193">建立 ASC Contracts 測試使用者</span><span class="sxs-lookup"><span data-stu-id="9b2b5-193">Creating an ASC Contracts test user</span></span>

<span data-ttu-id="9b2b5-194">與 ASC Networks Inc. (ASC) 支援小組 (電話是 **613.599.6178**) 合作，以將使用者新增到 ASC Contracts 平台。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-194">Work with ASC Networks Inc. (ASC) support team at **613.599.6178** to get the users added in the ASC Contracts platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9b2b5-195">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="9b2b5-195">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9b2b5-196">在本節中，您會把 ASC Contracts 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ASC Contracts.</span></span>

![指派使用者][200] 

<span data-ttu-id="9b2b5-198">**若要將 Britta Simon 指派給 ASC Contracts，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="9b2b5-198">**To assign Britta Simon to ASC Contracts, perform the following steps:**</span></span>

1. <span data-ttu-id="9b2b5-199">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="9b2b5-201">在應用程式清單中，選取 [ASC Contracts]。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-201">In the applications list, select **ASC Contracts**.</span></span>

    ![設定單一登入](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_app.png) 

3. <span data-ttu-id="9b2b5-203">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-203">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="9b2b5-205">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-205">Click **Add** button.</span></span> <span data-ttu-id="9b2b5-206">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="9b2b5-208">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9b2b5-209">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9b2b5-210">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9b2b5-211">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="9b2b5-211">Testing single sign-on</span></span>

<span data-ttu-id="9b2b5-212">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9b2b5-213">當您在存取面板中按一下 [ASC Contracts] 圖格時，應該會自動登入您的 ASC Contracts 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-213">When you click the ASC Contracts tile in the Access Panel, you should get automatically signed-on to your ASC Contracts application.</span></span> <span data-ttu-id="9b2b5-214">如需存取面板的詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="9b2b5-214">For more information about the Access Panel, see.</span></span> <span data-ttu-id="9b2b5-215">[存取面板簡介](https://msdn.microsoft.com/library/dn308586)。</span><span class="sxs-lookup"><span data-stu-id="9b2b5-215">[Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9b2b5-216">其他資源</span><span class="sxs-lookup"><span data-stu-id="9b2b5-216">Additional resources</span></span>

* [<span data-ttu-id="9b2b5-217">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="9b2b5-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9b2b5-218">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="9b2b5-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_203.png

