---
title: "教學課程：Azure Active Directory 與 Birst Agile Business Analytics 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Birst Agile Business Analytics 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 677183b1-5348-4302-88cc-5c8ab63a3c6c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 779f9e0a57ffb2274ea22a90ed9759734ab6916d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-birst-agile-business-analytics"></a><span data-ttu-id="fbed6-103">教學課程：Azure Active Directory 與 Birst Agile Business Analytics 整合</span><span class="sxs-lookup"><span data-stu-id="fbed6-103">Tutorial: Azure Active Directory integration with Birst Agile Business Analytics</span></span>

<span data-ttu-id="fbed6-104">在本教學課程中，您會了解如何將 Birst Agile Business Analytics 與 Azure Active Directory (Azure AD) 整合。</span><span class="sxs-lookup"><span data-stu-id="fbed6-104">In this tutorial, you learn how to integrate Birst Agile Business Analytics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fbed6-105">將 Birst Agile Business Analytics 與 Azure AD 整合可提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="fbed6-105">Integrating Birst Agile Business Analytics with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fbed6-106">您可以在 Azure AD 中控制可存取 Birst Agile Business Analytics 的人員</span><span class="sxs-lookup"><span data-stu-id="fbed6-106">You can control in Azure AD who has access to Birst Agile Business Analytics</span></span>
- <span data-ttu-id="fbed6-107">您可以讓使用者使用其 Azure AD 帳戶自動登入 Birst Agile Business Analytics (單一登入)</span><span class="sxs-lookup"><span data-stu-id="fbed6-107">You can enable your users to automatically get signed-on to Birst Agile Business Analytics (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fbed6-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="fbed6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="fbed6-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="fbed6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fbed6-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="fbed6-110">Prerequisites</span></span>

<span data-ttu-id="fbed6-111">若要設定 Azure AD 與 Birst Agile Business Analytics 的整合，需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="fbed6-111">To configure Azure AD integration with Birst Agile Business Analytics, you need the following items:</span></span>

- <span data-ttu-id="fbed6-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="fbed6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fbed6-113">已啟用 Birst Agile Business Analytics 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="fbed6-113">A Birst Agile Business Analytics single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fbed6-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="fbed6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fbed6-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="fbed6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fbed6-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="fbed6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fbed6-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="fbed6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fbed6-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="fbed6-118">Scenario description</span></span>
<span data-ttu-id="fbed6-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="fbed6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fbed6-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="fbed6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fbed6-121">從資源庫新增 Birst Agile Business Analytics</span><span class="sxs-lookup"><span data-stu-id="fbed6-121">Adding Birst Agile Business Analytics from the gallery</span></span>
2. <span data-ttu-id="fbed6-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="fbed6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-birst-agile-business-analytics-from-the-gallery"></a><span data-ttu-id="fbed6-123">從資源庫新增 Birst Agile Business Analytics</span><span class="sxs-lookup"><span data-stu-id="fbed6-123">Adding Birst Agile Business Analytics from the gallery</span></span>
<span data-ttu-id="fbed6-124">若要設定將 Birst Agile Business Analytics 整合到 Azure AD 中，您需要從資源庫將 Birst Agile Business Analytics 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="fbed6-124">To configure the integration of Birst Agile Business Analytics into Azure AD, you need to add Birst Agile Business Analytics from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fbed6-125">**若要從資源庫新增 Birst Agile Business Analytics，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="fbed6-125">**To add Birst Agile Business Analytics from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fbed6-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="fbed6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fbed6-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="fbed6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fbed6-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="fbed6-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="fbed6-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fbed6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="fbed6-133">在搜尋方塊中，輸入 **Birst Agile Business Analytics**。</span><span class="sxs-lookup"><span data-stu-id="fbed6-133">In the search box, type **Birst Agile Business Analytics**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-birst-tutorial/tutorial_birst_search.png)

5. <span data-ttu-id="fbed6-135">在結果面板中，選取 [Birst Agile Business Analytics]，然後按一下 [新增] 按鈕以新增該應用程式。</span><span class="sxs-lookup"><span data-stu-id="fbed6-135">In the results panel, select **Birst Agile Business Analytics**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-birst-tutorial/tutorial_birst_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fbed6-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="fbed6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fbed6-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Birst Agile Business Analytics 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="fbed6-138">In this section, you configure and test Azure AD single sign-on with Birst Agile Business Analytics based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="fbed6-139">若要讓單一登入能夠運作，Azure AD 必須知道 Birst Agile Business Analytics 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="fbed6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Birst Agile Business Analytics is to a user in Azure AD.</span></span> <span data-ttu-id="fbed6-140">換句話說，必須在 Azure AD 使用者與 Birst Agile Business Analytics 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="fbed6-140">In other words, a link relationship between an Azure AD user and the related user in Birst Agile Business Analytics needs to be established.</span></span>

<span data-ttu-id="fbed6-141">在 Birst Agile Business Analytics 中，將 [Username] 的值指派為 Azure AD 中 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="fbed6-141">In Birst Agile Business Analytics, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="fbed6-142">若要設定及測試與 Birst Agile Business Analytics 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="fbed6-142">To configure and test Azure AD single sign-on with Birst Agile Business Analytics, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fbed6-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="fbed6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="fbed6-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="fbed6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fbed6-145">**[建立 Birst Agile Business Analytics 測試使用者](#creating-a-birst-agile-business-analytics-test-user)** - 在 Birst Agile Business Analytics 中建立一個與 Azure AD 中代表 Britta Simon 之項目連結的 Britta Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="fbed6-145">**[Creating a Birst Agile Business Analytics test user](#creating-a-birst-agile-business-analytics-test-user)** - to have a counterpart of Britta Simon in Birst Agile Business Analytics that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="fbed6-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="fbed6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fbed6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="fbed6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fbed6-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="fbed6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fbed6-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Birst Agile Business Analytics 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="fbed6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Birst Agile Business Analytics application.</span></span>

<span data-ttu-id="fbed6-150">**若要設定與 Birst Agile Business Analytics 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="fbed6-150">**To configure Azure AD single sign-on with Birst Agile Business Analytics, perform the following steps:**</span></span>

1. <span data-ttu-id="fbed6-151">在 Azure 入口網站的 [Birst Agile Business Analytics] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="fbed6-151">In the Azure portal, on the **Birst Agile Business Analytics** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="fbed6-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="fbed6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-birst-tutorial/tutorial_birst_samlbase.png)

3. <span data-ttu-id="fbed6-155">在 [Birst Agile Business Analytics 網域及 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="fbed6-155">On the **Birst Agile Business Analytics Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-birst-tutorial/tutorial_birst_url.png)

     <span data-ttu-id="fbed6-157">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span><span class="sxs-lookup"><span data-stu-id="fbed6-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span>

     <span data-ttu-id="fbed6-158">此 URL 取決於您 Birst 帳戶所在的資料中心：</span><span class="sxs-lookup"><span data-stu-id="fbed6-158">The URL depends on the datacenter that your Birst account is located:</span></span> 

     * <span data-ttu-id="fbed6-159">針對美國資料中心，請使用下列模式：`https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span><span class="sxs-lookup"><span data-stu-id="fbed6-159">For US datacenter use following the pattern: `https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span> 

     * <span data-ttu-id="fbed6-160">針對歐洲資料中心，請使用下列模式：`https://login.eu1.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span><span class="sxs-lookup"><span data-stu-id="fbed6-160">For Europe datacenter use the following pattern: `https://login.eu1.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fbed6-161">這不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="fbed6-161">This value is not real.</span></span> <span data-ttu-id="fbed6-162">使用實際的「登入 URL」來更新此值。</span><span class="sxs-lookup"><span data-stu-id="fbed6-162">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="fbed6-163">請連絡 [Birst Agile Business Analytics 用戶端支援小組](mailto:info@birst.com)以取得此值。</span><span class="sxs-lookup"><span data-stu-id="fbed6-163">Contact [Birst Agile Business Analytics Client support team](mailto:info@birst.com) to get the value.</span></span> 
 
4. <span data-ttu-id="fbed6-164">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="fbed6-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-birst-tutorial/tutorial_birst_certificate.png) 

5. <span data-ttu-id="fbed6-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="fbed6-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-birst-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fbed6-168">在 [Birst Agile Business Analytics 組態] 區段上，按一下 [設定 Birst Agile Business Analytics] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="fbed6-168">On the **Birst Agile Business Analytics Configuration** section, click **Configure Birst Agile Business Analytics** to open **Configure sign-on** window.</span></span> <span data-ttu-id="fbed6-169">從 [快速參考] 區段中複製「登出 URL」、「SAML 實體識別碼」及「SAML 單一登入服務 URL」。</span><span class="sxs-lookup"><span data-stu-id="fbed6-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-birst-tutorial/tutorial_birst_configure.png) 

7. <span data-ttu-id="fbed6-171">若要在 **Birst Agile Business Analytics** 端設定單一登入，您必須將已下載的「憑證 (Base64)」、「登出 URL」、「SAML 實體識別碼」及「SAML 單一登入服務 URL」傳送給 [Birst Agile Business Analytics 支援小組](mailto:info@birst.com)。</span><span class="sxs-lookup"><span data-stu-id="fbed6-171">To configure single sign-on on **Birst Agile Business Analytics** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Birst Agile Business Analytics support team](mailto:info@birst.com).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="fbed6-172">請告知 Birst 小組這個整合需要 SHA256 演算法 (將不支援 SHA1)，以便他們能夠在適當的伺服器 (例如 **app2101** 等) 上設定 SSO。</span><span class="sxs-lookup"><span data-stu-id="fbed6-172">Mention to Birst team that this integration needs SHA256 Algorithm (SHA1 will not be supported) so that they can set the SSO on the appropriate server like **app2101** etc.</span></span>
  

> [!TIP]
> <span data-ttu-id="fbed6-173">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="fbed6-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="fbed6-174">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="fbed6-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="fbed6-175">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fbed6-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fbed6-176">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="fbed6-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="fbed6-177">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="fbed6-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="fbed6-179">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="fbed6-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fbed6-180">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="fbed6-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-birst-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fbed6-182">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="fbed6-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-birst-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fbed6-184">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="fbed6-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-birst-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fbed6-186">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="fbed6-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-birst-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fbed6-188">a.</span><span class="sxs-lookup"><span data-stu-id="fbed6-188">a.</span></span> <span data-ttu-id="fbed6-189">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="fbed6-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fbed6-190">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="fbed6-190">b.</span></span> <span data-ttu-id="fbed6-191">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="fbed6-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fbed6-192">c.</span><span class="sxs-lookup"><span data-stu-id="fbed6-192">c.</span></span> <span data-ttu-id="fbed6-193">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="fbed6-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="fbed6-194">d.</span><span class="sxs-lookup"><span data-stu-id="fbed6-194">d.</span></span> <span data-ttu-id="fbed6-195">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="fbed6-195">Click **Create**.</span></span>
 
### <a name="creating-a-birst-agile-business-analytics-test-user"></a><span data-ttu-id="fbed6-196">建立 Birst Agile Business Analytics 測試使用者</span><span class="sxs-lookup"><span data-stu-id="fbed6-196">Creating a Birst Agile Business Analytics test user</span></span>

<span data-ttu-id="fbed6-197">本節的目標是在 Birst Agile Business Analytics 中建立一個名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="fbed6-197">The objective of this section is to create a user called Britta Simon in Birst Agile Business Analytics.</span></span> <span data-ttu-id="fbed6-198">請與 [Birst Agile Business Analytics 支援小組](mailto:info@birst.com)合作，在 Birst 帳戶中新增使用者。</span><span class="sxs-lookup"><span data-stu-id="fbed6-198">Work with [Birst Agile Business Analytics support team](mailto:info@birst.com) to add the users in the Birst account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="fbed6-199">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="fbed6-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="fbed6-200">在本節中，您會將 Birst Agile Business Analytics 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="fbed6-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Birst Agile Business Analytics.</span></span>

![指派使用者][200] 

<span data-ttu-id="fbed6-202">**若要將 Britta Simon 指派給 Birst Agile Business Analytics，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="fbed6-202">**To assign Britta Simon to Birst Agile Business Analytics, perform the following steps:**</span></span>

1. <span data-ttu-id="fbed6-203">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="fbed6-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="fbed6-205">在應用程式清單中，選取 [Birst Agile Business Analytics]。</span><span class="sxs-lookup"><span data-stu-id="fbed6-205">In the applications list, select **Birst Agile Business Analytics**.</span></span>

    ![設定單一登入](./media/active-directory-saas-birst-tutorial/tutorial_birst_app.png) 

3. <span data-ttu-id="fbed6-207">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="fbed6-207">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="fbed6-209">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fbed6-209">Click **Add** button.</span></span> <span data-ttu-id="fbed6-210">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="fbed6-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="fbed6-212">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="fbed6-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="fbed6-213">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fbed6-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fbed6-214">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fbed6-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fbed6-215">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="fbed6-215">Testing single sign-on</span></span>

<span data-ttu-id="fbed6-216">本節的目標是要使用「存取面板」來測試您的 Azure AD SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="fbed6-216">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="fbed6-217">當您在「存取面板」中按一下 Birst Agile Business Analytics 圖格時，應該會自動登入您的 Birst Agile Business Analytics 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fbed6-217">When you click the Birst Agile Business Analytics tile in the Access Panel, you should get automatically signed-on to your Birst Agile Business Analytics application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="fbed6-218">其他資源</span><span class="sxs-lookup"><span data-stu-id="fbed6-218">Additional resources</span></span>

* [<span data-ttu-id="fbed6-219">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="fbed6-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fbed6-220">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="fbed6-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-birst-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-birst-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-birst-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-birst-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-birst-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-birst-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-birst-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-birst-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-birst-tutorial/tutorial_general_203.png

