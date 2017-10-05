---
title: "教學課程：Azure Active Directory 與 Marketo 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Marketo 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b88c45f5-d288-4717-835c-ca965add8735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: e146fd5a8075bc9c7ba049b25e5f301fc2645ed9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-marketo"></a><span data-ttu-id="be1a9-103">教學課程：Azure Active Directory 與 Marketo 整合</span><span class="sxs-lookup"><span data-stu-id="be1a9-103">Tutorial: Azure Active Directory integration with Marketo</span></span>

<span data-ttu-id="be1a9-104">在本教學課程中，您會了解如何整合 Marketo 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="be1a9-104">In this tutorial, you learn how to integrate Marketo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="be1a9-105">Marketo 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="be1a9-105">Integrating Marketo with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="be1a9-106">您可以在 Azure AD 中控制可存取 Marketo 的人員</span><span class="sxs-lookup"><span data-stu-id="be1a9-106">You can control in Azure AD who has access to Marketo</span></span>
- <span data-ttu-id="be1a9-107">您可以讓使用者利用自己的 Azure AD 帳戶，來自動登入 Marketo (單一登入)</span><span class="sxs-lookup"><span data-stu-id="be1a9-107">You can enable your users to automatically get signed-on to Marketo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="be1a9-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="be1a9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="be1a9-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="be1a9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="be1a9-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="be1a9-110">Prerequisites</span></span>

<span data-ttu-id="be1a9-111">若要設定 Azure AD 與 Marketo 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="be1a9-111">To configure Azure AD integration with Marketo, you need the following items:</span></span>

- <span data-ttu-id="be1a9-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="be1a9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="be1a9-113">啟用 Marketo 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="be1a9-113">A Marketo single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="be1a9-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="be1a9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="be1a9-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="be1a9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="be1a9-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="be1a9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="be1a9-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="be1a9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="be1a9-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="be1a9-118">Scenario description</span></span>
<span data-ttu-id="be1a9-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="be1a9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="be1a9-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="be1a9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="be1a9-121">從資源庫新增 Marketo</span><span class="sxs-lookup"><span data-stu-id="be1a9-121">Adding Marketo from the gallery</span></span>
2. <span data-ttu-id="be1a9-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="be1a9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-marketo-from-the-gallery"></a><span data-ttu-id="be1a9-123">從資源庫新增 Marketo</span><span class="sxs-lookup"><span data-stu-id="be1a9-123">Adding Marketo from the gallery</span></span>
<span data-ttu-id="be1a9-124">若要設定 Marketo 與 Azure AD 整合，您需要從資源庫將 Marketo 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="be1a9-124">To configure the integration of Marketo into Azure AD, you need to add Marketo from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="be1a9-125">**若要從資源庫加入 Marketo，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="be1a9-125">**To add Marketo from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="be1a9-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="be1a9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="be1a9-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="be1a9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="be1a9-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="be1a9-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="be1a9-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="be1a9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="be1a9-133">在搜尋方塊中，輸入 **Marketo**。</span><span class="sxs-lookup"><span data-stu-id="be1a9-133">In the search box, type **Marketo**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_search.png)

5. <span data-ttu-id="be1a9-135">在結果面板中，選取 [Marketo]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="be1a9-135">In the results panel, select **Marketo**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="be1a9-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="be1a9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="be1a9-138">在本節中，您將以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Marketo 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="be1a9-138">In this section, you configure and test Azure AD single sign-on with Marketo based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="be1a9-139">若要讓單一登入運作，Azure AD 必須知道 Marketo 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="be1a9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Marketo is to a user in Azure AD.</span></span> <span data-ttu-id="be1a9-140">換句話說，必須要建立某位 Azure AD 使用者與 Marketo 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="be1a9-140">In other words, a link relationship between an Azure AD user and the related user in Marketo needs to be established.</span></span>

<span data-ttu-id="be1a9-141">在 Marketor 中，將 Azure AD 中 [使用者名稱]的值指派為 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="be1a9-141">In Marketo, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="be1a9-142">若要設定及測試與 Marketo 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="be1a9-142">To configure and test Azure AD single sign-on with Marketo, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="be1a9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="be1a9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="be1a9-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="be1a9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="be1a9-145">**[建立 Marketo 測試使用者](#creating-a-marketo-test-user)** - 使 Marketo 中 Britta Simon 的對應使用者連結到該使用者在 Azure AD 中的代表身分。</span><span class="sxs-lookup"><span data-stu-id="be1a9-145">**[Creating a Marketo test user](#creating-a-marketo-test-user)** - to have a counterpart of Britta Simon in Marketo that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="be1a9-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="be1a9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="be1a9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="be1a9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="be1a9-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="be1a9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="be1a9-149">在本節中，您將在 Azure 入口網站中啟用 Azure AD 單一登入，並在 Marketo 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="be1a9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Marketo application.</span></span>

<span data-ttu-id="be1a9-150">**若要使用 Marketo 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="be1a9-150">**To configure Azure AD single sign-on with Marketo, perform the following steps:**</span></span>

1. <span data-ttu-id="be1a9-151">在 Azure 入口網站的 [Marketo] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="be1a9-151">In the Azure portal, on the **Marketo** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="be1a9-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="be1a9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_samlbase.png)

3. <span data-ttu-id="be1a9-155">在 [Marketo 網域及 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="be1a9-155">On the **Marketo Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_url.png)

    <span data-ttu-id="be1a9-157">a.</span><span class="sxs-lookup"><span data-stu-id="be1a9-157">a.</span></span> <span data-ttu-id="be1a9-158">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://saml.marketo.com/sp`</span><span class="sxs-lookup"><span data-stu-id="be1a9-158">In the **Identifier** textbox, type a URL using the following pattern: `https://saml.marketo.com/sp`</span></span>

    <span data-ttu-id="be1a9-159">b.</span><span class="sxs-lookup"><span data-stu-id="be1a9-159">b.</span></span> <span data-ttu-id="be1a9-160">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://login.marketo.com/saml/assertion/\<munchkinid\>`</span><span class="sxs-lookup"><span data-stu-id="be1a9-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://login.marketo.com/saml/assertion/\<munchkinid\>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="be1a9-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="be1a9-161">These values are not real.</span></span> <span data-ttu-id="be1a9-162">請使用實際的識別碼和回覆 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="be1a9-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="be1a9-163">請連絡 [Marketo 支援小組](http://investors.marketo.com/contactus.cfm)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="be1a9-163">Contact [Marketo support team](http://investors.marketo.com/contactus.cfm) to get these values.</span></span>
 
4. <span data-ttu-id="be1a9-164">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="be1a9-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_certificate.png) 

5. <span data-ttu-id="be1a9-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="be1a9-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="be1a9-168">在 [Marketo 設定] 區段中，按一下 [設定 Marketo] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="be1a9-168">On the **Marketo Configuration** section, click **Configure Marketo** to open **Configure sign-on** window.</span></span> <span data-ttu-id="be1a9-169">從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="be1a9-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_configure.png) 

7. <span data-ttu-id="be1a9-171">若要取得您的應用程式的 Munchkin 識別碼，請使用系統管理員認證登入 Marketo，執行以下動作︰</span><span class="sxs-lookup"><span data-stu-id="be1a9-171">To get Munchkin Id of your application, log in to Marketo using admin credentials and perform following actions:</span></span>
   
    <span data-ttu-id="be1a9-172">a.</span><span class="sxs-lookup"><span data-stu-id="be1a9-172">a.</span></span> <span data-ttu-id="be1a9-173">使用管理員認證登入 Marketo 應用程式。</span><span class="sxs-lookup"><span data-stu-id="be1a9-173">Log in to Marketo app using admin credentials.</span></span>
   
    <span data-ttu-id="be1a9-174">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="be1a9-174">b.</span></span> <span data-ttu-id="be1a9-175">按一下頂端瀏覽窗格中的 [管理] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="be1a9-175">Click the **Admin** button on the top navigation pane.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="be1a9-177">c.</span><span class="sxs-lookup"><span data-stu-id="be1a9-177">c.</span></span> <span data-ttu-id="be1a9-178">瀏覽至 [整合] 功能表，然後按一下 [Munchkin] 連結。</span><span class="sxs-lookup"><span data-stu-id="be1a9-178">Navigate to the Integration menu and click the **Munchkin link**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_11.png)
   
    <span data-ttu-id="be1a9-180">d.</span><span class="sxs-lookup"><span data-stu-id="be1a9-180">d.</span></span> <span data-ttu-id="be1a9-181">複製螢幕上顯示的 Munchkin 識別碼，完成 Azure AD 設定精靈中的回覆 URL。</span><span class="sxs-lookup"><span data-stu-id="be1a9-181">Copy the Munchkin Id shown on the screen and complete your Reply URL in the Azure AD configuration wizard.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_12.png) 

8. <span data-ttu-id="be1a9-183">若要設定應用程式中的 SSO，請遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="be1a9-183">To configure the SSO in the application, follow the below steps:</span></span>
   
    <span data-ttu-id="be1a9-184">a.</span><span class="sxs-lookup"><span data-stu-id="be1a9-184">a.</span></span> <span data-ttu-id="be1a9-185">使用管理員認證登入 Marketo 應用程式。</span><span class="sxs-lookup"><span data-stu-id="be1a9-185">Log in to Marketo app using admin credentials.</span></span>
   
    <span data-ttu-id="be1a9-186">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="be1a9-186">b.</span></span> <span data-ttu-id="be1a9-187">按一下頂端瀏覽窗格中的 [管理] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="be1a9-187">Click the **Admin** button on the top navigation pane.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="be1a9-189">c.</span><span class="sxs-lookup"><span data-stu-id="be1a9-189">c.</span></span> <span data-ttu-id="be1a9-190">瀏覽至 [整合] 功能表，然後按一下 [單一登入] 。</span><span class="sxs-lookup"><span data-stu-id="be1a9-190">Navigate to the Integration menu and click **Single Sign On**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_07.png) 
   
    <span data-ttu-id="be1a9-192">d.</span><span class="sxs-lookup"><span data-stu-id="be1a9-192">d.</span></span> <span data-ttu-id="be1a9-193">若要啟用 SAML 設定，按一下 [編輯]按鈕。</span><span class="sxs-lookup"><span data-stu-id="be1a9-193">To enable the SAML Settings, click **Edit** button.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_08.png) 
   
    <span data-ttu-id="be1a9-195">e.</span><span class="sxs-lookup"><span data-stu-id="be1a9-195">e.</span></span> <span data-ttu-id="be1a9-196">**已啟用**單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="be1a9-196">**Enabled** Single Sign-On settings.</span></span>
   
    <span data-ttu-id="be1a9-197">f.</span><span class="sxs-lookup"><span data-stu-id="be1a9-197">f.</span></span> <span data-ttu-id="be1a9-198">在 [簽發者識別碼] 文字方塊中，貼上 [SAML 實體識別碼]。</span><span class="sxs-lookup"><span data-stu-id="be1a9-198">Paste the **SAML Entity ID**, in the **Issuer ID** textbox.</span></span>
   
    <span data-ttu-id="be1a9-199">g.</span><span class="sxs-lookup"><span data-stu-id="be1a9-199">g.</span></span> <span data-ttu-id="be1a9-200">在 [實體識別碼] 文字方塊中，輸入 URL `http://saml.marketo.com/sp`。</span><span class="sxs-lookup"><span data-stu-id="be1a9-200">In the **Entity ID** textbox, enter the URL as `http://saml.marketo.com/sp`.</span></span>
   
    <span data-ttu-id="be1a9-201">h.</span><span class="sxs-lookup"><span data-stu-id="be1a9-201">h.</span></span> <span data-ttu-id="be1a9-202">選取 [使用者識別碼位置] 做為 [名稱識別碼元素]。</span><span class="sxs-lookup"><span data-stu-id="be1a9-202">Select the User ID Location as **Name Identifier element**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_09.png)
   
    > [!NOTE]
    > <span data-ttu-id="be1a9-204">如果您的使用者識別碼不是 UPN 值，則至 [屬性] 索引標籤中變更其值。</span><span class="sxs-lookup"><span data-stu-id="be1a9-204">If your User Identifier is not UPN value then change the value in the Attribute tab.</span></span>
   
    <span data-ttu-id="be1a9-205">i.</span><span class="sxs-lookup"><span data-stu-id="be1a9-205">i.</span></span> <span data-ttu-id="be1a9-206">上傳您從 Azure AD 設定精靈下載的憑證。</span><span class="sxs-lookup"><span data-stu-id="be1a9-206">Upload the certificate, which you have downloaded from Azure AD configuration wizard.</span></span> <span data-ttu-id="be1a9-207">**儲存**設定。</span><span class="sxs-lookup"><span data-stu-id="be1a9-207">**Save** the settings.</span></span>
   
    <span data-ttu-id="be1a9-208">j.</span><span class="sxs-lookup"><span data-stu-id="be1a9-208">j.</span></span> <span data-ttu-id="be1a9-209">編輯 [重新導向頁面] 設定。</span><span class="sxs-lookup"><span data-stu-id="be1a9-209">Edit the Redirect Pages settings.</span></span>
   
    <span data-ttu-id="be1a9-210">k.</span><span class="sxs-lookup"><span data-stu-id="be1a9-210">k.</span></span> <span data-ttu-id="be1a9-211">在 [登入 URL] 文字方塊中，貼上 **SAML 單一登入服務 URL**。</span><span class="sxs-lookup"><span data-stu-id="be1a9-211">Paste the **SAML Single Sign-On Service URL** in the **Login URL** textbox.</span></span>
   
    <span data-ttu-id="be1a9-212">l.</span><span class="sxs-lookup"><span data-stu-id="be1a9-212">l.</span></span> <span data-ttu-id="be1a9-213">在 [登出 URL] 文字方塊中，貼上登出 URL。</span><span class="sxs-lookup"><span data-stu-id="be1a9-213">Paste the **Sign-Out URL** in the **Logout URL** textbox.</span></span>
   
    <span data-ttu-id="be1a9-214">m.</span><span class="sxs-lookup"><span data-stu-id="be1a9-214">m.</span></span> <span data-ttu-id="be1a9-215">在 [錯誤 URL] 中，複製您的 **Marketo 執行個體 URL**，並按一下 [儲存] 按鈕以儲存設定。</span><span class="sxs-lookup"><span data-stu-id="be1a9-215">In the **Error URL**, copy your **Marketo instance URL** and click **Save** button to save settings.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_10.png)

9. <span data-ttu-id="be1a9-217">若要啟用使用者的 SSO，完成下列動作：</span><span class="sxs-lookup"><span data-stu-id="be1a9-217">To enable the SSO for users, complete the following actions:</span></span>
   
    <span data-ttu-id="be1a9-218">a.</span><span class="sxs-lookup"><span data-stu-id="be1a9-218">a.</span></span> <span data-ttu-id="be1a9-219">使用管理員認證登入 Marketo 應用程式。</span><span class="sxs-lookup"><span data-stu-id="be1a9-219">Log in to Marketo app using admin credentials.</span></span>
   
    <span data-ttu-id="be1a9-220">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="be1a9-220">b.</span></span> <span data-ttu-id="be1a9-221">按一下頂端瀏覽窗格中的 [管理] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="be1a9-221">Click the **Admin** button on the top navigation pane.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="be1a9-223">c.</span><span class="sxs-lookup"><span data-stu-id="be1a9-223">c.</span></span> <span data-ttu-id="be1a9-224">瀏覽至 [安全性] 功能表，然後按一下 [登入設定]。</span><span class="sxs-lookup"><span data-stu-id="be1a9-224">Navigate to the **Security** menu and click **Login Settings**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_13.png)
   
    <span data-ttu-id="be1a9-226">d.</span><span class="sxs-lookup"><span data-stu-id="be1a9-226">d.</span></span> <span data-ttu-id="be1a9-227">勾選 [需要 SSO] 選項，並 [儲存]設定。</span><span class="sxs-lookup"><span data-stu-id="be1a9-227">Check the **Require SSO** option and **Save** the settings.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_14.png)

> [!TIP]
> <span data-ttu-id="be1a9-229">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="be1a9-229">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="be1a9-230">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="be1a9-230">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="be1a9-231">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="be1a9-231">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="be1a9-232">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="be1a9-232">Creating an Azure AD test user</span></span>
<span data-ttu-id="be1a9-233">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="be1a9-233">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="be1a9-235">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="be1a9-235">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="be1a9-236">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="be1a9-236">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-marketo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="be1a9-238">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="be1a9-238">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-marketo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="be1a9-240">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="be1a9-240">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-marketo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="be1a9-242">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="be1a9-242">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-marketo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="be1a9-244">a.</span><span class="sxs-lookup"><span data-stu-id="be1a9-244">a.</span></span> <span data-ttu-id="be1a9-245">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="be1a9-245">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="be1a9-246">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="be1a9-246">b.</span></span> <span data-ttu-id="be1a9-247">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="be1a9-247">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="be1a9-248">c.</span><span class="sxs-lookup"><span data-stu-id="be1a9-248">c.</span></span> <span data-ttu-id="be1a9-249">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="be1a9-249">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="be1a9-250">d.</span><span class="sxs-lookup"><span data-stu-id="be1a9-250">d.</span></span> <span data-ttu-id="be1a9-251">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="be1a9-251">Click **Create**.</span></span>
 
### <a name="creating-a-marketo-test-user"></a><span data-ttu-id="be1a9-252">建立 Marketo 測試使用者</span><span class="sxs-lookup"><span data-stu-id="be1a9-252">Creating a Marketo test user</span></span>

<span data-ttu-id="be1a9-253">在本節中，您要在 Marketo 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="be1a9-253">In this section, you create a user called Britta Simon in Marketo.</span></span> <span data-ttu-id="be1a9-254">遵循以下步驟在 Marketo 平台中建立使用者。</span><span class="sxs-lookup"><span data-stu-id="be1a9-254">follow these steps to create a user in Marketo platform.</span></span>

1. <span data-ttu-id="be1a9-255">使用管理員認證登入 Marketo 應用程式。</span><span class="sxs-lookup"><span data-stu-id="be1a9-255">Log in to Marketo app using admin credentials.</span></span>

2. <span data-ttu-id="be1a9-256">按一下頂端瀏覽窗格中的 [管理] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="be1a9-256">Click the **Admin** button on the top navigation pane.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 

3. <span data-ttu-id="be1a9-258">瀏覽至 [安全性] 功能表，然後按一下 [使用者與角色]</span><span class="sxs-lookup"><span data-stu-id="be1a9-258">Navigate to the **Security** menu and click **Users & Roles**</span></span>
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_19.png)  

4. <span data-ttu-id="be1a9-260">按一下 [使用者] 索引標籤上的 [邀請新使用者]  連結</span><span class="sxs-lookup"><span data-stu-id="be1a9-260">Click the **Invite New User** link on the Users tab</span></span>
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_15.png) 

5. <span data-ttu-id="be1a9-262">在 [邀請新使用者] 精靈中填寫下列資訊。</span><span class="sxs-lookup"><span data-stu-id="be1a9-262">In the Invite New User wizard fill the following information</span></span>
   
    <span data-ttu-id="be1a9-263">a.</span><span class="sxs-lookup"><span data-stu-id="be1a9-263">a.</span></span> <span data-ttu-id="be1a9-264">在 [電子郵件] 文字方塊中輸入使用者的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="be1a9-264">Enter the user **Email** address in the textbox</span></span>
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_16.png)
   
    <span data-ttu-id="be1a9-266">b.</span><span class="sxs-lookup"><span data-stu-id="be1a9-266">b.</span></span> <span data-ttu-id="be1a9-267">在 [名字] 文字方塊中輸入名字。</span><span class="sxs-lookup"><span data-stu-id="be1a9-267">Enter the **First Name** in the textbox</span></span>
   
    <span data-ttu-id="be1a9-268">c.</span><span class="sxs-lookup"><span data-stu-id="be1a9-268">c.</span></span> <span data-ttu-id="be1a9-269">在 [姓氏] 文字方塊中輸入姓氏。</span><span class="sxs-lookup"><span data-stu-id="be1a9-269">Enter the **Last Name**  in the textbox</span></span>
   
    <span data-ttu-id="be1a9-270">d.</span><span class="sxs-lookup"><span data-stu-id="be1a9-270">d.</span></span> <span data-ttu-id="be1a9-271">按一下 [下一步] </span><span class="sxs-lookup"><span data-stu-id="be1a9-271">Click **Next**</span></span>

6. <span data-ttu-id="be1a9-272">在 [權限]  索引標籤中選取 [userRoles]，然後按一下 [下一步]</span><span class="sxs-lookup"><span data-stu-id="be1a9-272">In the **Permissions** tab, select the **userRoles** and click **Next**</span></span>
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_17.png)
7. <span data-ttu-id="be1a9-274">按一下 [傳送] 按鈕，傳送使用者邀請</span><span class="sxs-lookup"><span data-stu-id="be1a9-274">Click the **Send** button to send the user invitation</span></span>
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_18.png)

8. <span data-ttu-id="be1a9-276">使用者會收到電子郵件通知，他必須按一下連結，並變更密碼才能啟動帳戶。</span><span class="sxs-lookup"><span data-stu-id="be1a9-276">User receives the email notification and has to click the link and change the password to activate the account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="be1a9-277">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="be1a9-277">Assigning the Azure AD test user</span></span>

<span data-ttu-id="be1a9-278">在本節中，您將把 Marketo 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="be1a9-278">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Marketo.</span></span>

![指派使用者][200] 

<span data-ttu-id="be1a9-280">**若要將 Britta Simon 指派到 Marketo，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="be1a9-280">**To assign Britta Simon to Marketo, perform the following steps:**</span></span>

1. <span data-ttu-id="be1a9-281">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="be1a9-281">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="be1a9-283">在應用程式清單中，選取 [Marketo] 。</span><span class="sxs-lookup"><span data-stu-id="be1a9-283">In the applications list, select **Marketo**.</span></span>

    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_app.png) 

3. <span data-ttu-id="be1a9-285">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="be1a9-285">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="be1a9-287">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="be1a9-287">Click **Add** button.</span></span> <span data-ttu-id="be1a9-288">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="be1a9-288">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="be1a9-290">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="be1a9-290">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="be1a9-291">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="be1a9-291">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="be1a9-292">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="be1a9-292">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="be1a9-293">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="be1a9-293">Testing single sign-on</span></span>

<span data-ttu-id="be1a9-294">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="be1a9-294">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="be1a9-295">當您在存取面板中按一下 [Marketo] 圖格時，應該會自動登入您的 Marketo 應用程式。</span><span class="sxs-lookup"><span data-stu-id="be1a9-295">When you click the Marketo tile in the Access Panel, you should get automatically signed-on to your Marketo application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="be1a9-296">其他資源</span><span class="sxs-lookup"><span data-stu-id="be1a9-296">Additional resources</span></span>

* [<span data-ttu-id="be1a9-297">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="be1a9-297">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="be1a9-298">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="be1a9-298">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_203.png

