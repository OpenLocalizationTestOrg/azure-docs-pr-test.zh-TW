---
title: "教學課程：Azure Active Directory 與 Rightscale 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Rightscale 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3a8d376d-95fb-4dd7-832a-4fdd4dd7c87c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 222c4414a9f736a3589b4cdd0ed934696f6c31ef
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rightscale"></a><span data-ttu-id="00131-103">教學課程：Azure Active Directory 與 Rightscale 整合</span><span class="sxs-lookup"><span data-stu-id="00131-103">Tutorial: Azure Active Directory integration with Rightscale</span></span>

<span data-ttu-id="00131-104">在本教學課程中，您會了解如何整合 Rightscale 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="00131-104">In this tutorial, you learn how to integrate Rightscale with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="00131-105">Rightscale 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="00131-105">Integrating Rightscale with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="00131-106">您可以在 Azure AD 中控制可存取 Rightscale 的人員</span><span class="sxs-lookup"><span data-stu-id="00131-106">You can control in Azure AD who has access to Rightscale</span></span>
- <span data-ttu-id="00131-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Rightscale (單一登入)</span><span class="sxs-lookup"><span data-stu-id="00131-107">You can enable your users to automatically get signed-on to Rightscale (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="00131-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="00131-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="00131-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="00131-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="00131-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="00131-110">Prerequisites</span></span>

<span data-ttu-id="00131-111">若要設定 Azure AD 與 Rightscale 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="00131-111">To configure Azure AD integration with Rightscale, you need the following items:</span></span>

- <span data-ttu-id="00131-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="00131-112">An Azure AD subscription</span></span>
- <span data-ttu-id="00131-113">啟用 RightScale 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="00131-113">A Rightscale single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="00131-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="00131-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="00131-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="00131-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="00131-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="00131-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="00131-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="00131-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="00131-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="00131-118">Scenario description</span></span>
<span data-ttu-id="00131-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="00131-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="00131-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="00131-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="00131-121">從資源庫新增 Rightscale</span><span class="sxs-lookup"><span data-stu-id="00131-121">Adding Rightscale from the gallery</span></span>
2. <span data-ttu-id="00131-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="00131-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rightscale-from-the-gallery"></a><span data-ttu-id="00131-123">從資源庫新增 Rightscale</span><span class="sxs-lookup"><span data-stu-id="00131-123">Adding Rightscale from the gallery</span></span>
<span data-ttu-id="00131-124">若要設定將 Rightscale 整合到 Azure AD 中，您需要從資源庫將 Rightscale 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="00131-124">To configure the integration of Rightscale into Azure AD, you need to add Rightscale from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="00131-125">**若要從資源庫新增 Rightscale，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="00131-125">**To add Rightscale from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="00131-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="00131-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="00131-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="00131-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="00131-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="00131-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="00131-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="00131-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="00131-133">在搜尋方塊中，輸入 **Rightscale**。</span><span class="sxs-lookup"><span data-stu-id="00131-133">In the search box, type **Rightscale**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_search.png)

5. <span data-ttu-id="00131-135">在結果面板中，選取 [Rightscale]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="00131-135">In the results panel, select **Rightscale**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="00131-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="00131-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="00131-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Rightscale 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="00131-138">In this section, you configure and test Azure AD single sign-on with Rightscale based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="00131-139">若要讓單一登入運作，Azure AD 必須知道 Rightscale 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="00131-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Rightscale is to a user in Azure AD.</span></span> <span data-ttu-id="00131-140">換句話說，必須在 Azure AD 使用者和 Rightscale 中的相關使用者之間，建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="00131-140">In other words, a link relationship between an Azure AD user and the related user in Rightscale needs to be established.</span></span>

<span data-ttu-id="00131-141">在 Rightscale 中，將 Azure AD 中**使用者名稱**的值指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="00131-141">In Rightscale, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="00131-142">若要設定及測試與 Rightscale 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="00131-142">To configure and test Azure AD single sign-on with Rightscale, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="00131-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="00131-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="00131-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="00131-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="00131-145">**[建立 Rightscale 測試使用者](#creating-a-rightscale-test-user)** - 使 RightScale 中對應的 Britta Simon 連結到該該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="00131-145">**[Creating a Rightscale test user](#creating-a-rightscale-test-user)** - to have a counterpart of Britta Simon in Rightscale that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="00131-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="00131-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="00131-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="00131-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="00131-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="00131-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="00131-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Rightscale 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="00131-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Rightscale application.</span></span>

<span data-ttu-id="00131-150">**若要設定與 Rightscale 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="00131-150">**To configure Azure AD single sign-on with Rightscale, perform the following steps:**</span></span>

1. <span data-ttu-id="00131-151">在 Azure 入口網站的 [Rightscale] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="00131-151">In the Azure portal, on the **Rightscale** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="00131-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="00131-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_samlbase.png)

3. <span data-ttu-id="00131-155">如果您想要以 **IDP 起始模式**設定應用程式，則不需要在 [Rightscale 網域及 URL]**和 Url** 區段中執行任何步驟，因為應用程式已預先整合到 Azure。</span><span class="sxs-lookup"><span data-stu-id="00131-155">On the **Rightscale Domain and URLs** section, if you wish to configure the application in **IDP initiated mode** you do not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![設定單一登入](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url.png)

4. <span data-ttu-id="00131-157">如果您想要以 **SP 起始模式**設定應用程式，請在 [Rightscale 網域及 URL] 區段上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="00131-157">On the **Rightscale Domain and URLs** section, if you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![設定單一登入](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url1.png)

    <span data-ttu-id="00131-159">a.</span><span class="sxs-lookup"><span data-stu-id="00131-159">a.</span></span> <span data-ttu-id="00131-160">按一下 [顯示進階 URL 設定]。</span><span class="sxs-lookup"><span data-stu-id="00131-160">Click on the **Show advanced URL settings**.</span></span>

    <span data-ttu-id="00131-161">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="00131-161">b.</span></span> <span data-ttu-id="00131-162">在 [登入 URL] 文字方塊中，輸入 URL：`https://login.rightscale.com/`</span><span class="sxs-lookup"><span data-stu-id="00131-162">In the **Sign On URL** textbox, type the URL: `https://login.rightscale.com/`</span></span>

5. <span data-ttu-id="00131-163">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="00131-163">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_certificate.png) 

6. <span data-ttu-id="00131-165">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="00131-165">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-rightscale-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="00131-167">在 [Rightscale 組態] 區段上，按一下 [設定 Rightscale] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="00131-167">On the **Rightscale Configuration** section, click **Configure Rightscale** to open **Configure sign-on** window.</span></span> <span data-ttu-id="00131-168">從 [快速參考] 區段中複製 [SAML 實體識別碼] 和 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="00131-168">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    <span data-ttu-id="00131-169">![設定單一登入](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="00131-169">![Configure Single Sign-On](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS></span></span>
8. <span data-ttu-id="00131-170">若要取得為應用程式設定的 SSO，您必須以系統管理員身分登入 RightScale 租用戶。</span><span class="sxs-lookup"><span data-stu-id="00131-170">To get SSO configured for your application, you need to sign-on to your RightScale tenant as an administrator.</span></span>

    <span data-ttu-id="00131-171">a.</span><span class="sxs-lookup"><span data-stu-id="00131-171">a.</span></span> <span data-ttu-id="00131-172">在頂端的功能表中，按一下 [設定] 索引標籤，然後選取 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="00131-172">In the menu on the top, click the **Settings** tab and select **Single Sign-On**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_001.png) 

    <span data-ttu-id="00131-174">b.</span><span class="sxs-lookup"><span data-stu-id="00131-174">b.</span></span> <span data-ttu-id="00131-175">按一下 [新增] 按鈕來新增**您的 SAML 身分識別提供者**。</span><span class="sxs-lookup"><span data-stu-id="00131-175">Click the "**new**" button to add **Your SAML Identity Providers**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_002.png) 
 
    <span data-ttu-id="00131-177">c.</span><span class="sxs-lookup"><span data-stu-id="00131-177">c.</span></span> <span data-ttu-id="00131-178">在 [顯示名稱] 文字方塊中，輸入您的公司名稱。</span><span class="sxs-lookup"><span data-stu-id="00131-178">In the textbox of **Display Name**, input your company name.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_003.png)
 
    <span data-ttu-id="00131-180">d.</span><span class="sxs-lookup"><span data-stu-id="00131-180">d.</span></span> <span data-ttu-id="00131-181">選取 [Allow RightScale-initiated SSO using a discovery hint] (允許使用 Discovery Hint 的 RightScale 起始 SSO)，然後在下方文字方塊中輸入您的**網域名稱**。</span><span class="sxs-lookup"><span data-stu-id="00131-181">Select **Allow RightScale-initiated SSO using a discovery hint** and input your **domain name** in the below textbox.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_004.png)

    <span data-ttu-id="00131-183">e.</span><span class="sxs-lookup"><span data-stu-id="00131-183">e.</span></span> <span data-ttu-id="00131-184">將您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值，貼到 RightScale 的 [SAML SSO 端點] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="00131-184">Paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal into **SAML SSO Endpoint** in RightScale.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_006.png)

    <span data-ttu-id="00131-186">f.</span><span class="sxs-lookup"><span data-stu-id="00131-186">f.</span></span> <span data-ttu-id="00131-187">將您從 Azure 入口網站複製的 [SAML 實體識別碼] 值，貼到 RightScale 中的 [SAML 實體識別碼]。</span><span class="sxs-lookup"><span data-stu-id="00131-187">Paste the value of **SAML Entity ID** which you have copied from Azure portal into **SAML EntityID** in RightScale.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_008.png)

    <span data-ttu-id="00131-189">g.</span><span class="sxs-lookup"><span data-stu-id="00131-189">g.</span></span> <span data-ttu-id="00131-190">按一下 [瀏覽器]  按鈕來上傳您從 Azure 入口網站下載的憑證。</span><span class="sxs-lookup"><span data-stu-id="00131-190">Click **Browser** button to upload the certificate which you downloaded from Azure portal.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_009.png)

    <span data-ttu-id="00131-192">h.</span><span class="sxs-lookup"><span data-stu-id="00131-192">h.</span></span> <span data-ttu-id="00131-193">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="00131-193">Click **Save**.</span></span>
<CE>
> [!TIP]
> <span data-ttu-id="00131-194">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="00131-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="00131-195">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="00131-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="00131-196">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="00131-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="00131-197">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="00131-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="00131-198">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="00131-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="00131-200">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="00131-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="00131-201">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="00131-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-rightscale-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="00131-203">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="00131-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-rightscale-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="00131-205">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="00131-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-rightscale-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="00131-207">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="00131-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-rightscale-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="00131-209">a.</span><span class="sxs-lookup"><span data-stu-id="00131-209">a.</span></span> <span data-ttu-id="00131-210">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="00131-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="00131-211">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="00131-211">b.</span></span> <span data-ttu-id="00131-212">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="00131-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="00131-213">c.</span><span class="sxs-lookup"><span data-stu-id="00131-213">c.</span></span> <span data-ttu-id="00131-214">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="00131-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="00131-215">d.</span><span class="sxs-lookup"><span data-stu-id="00131-215">d.</span></span> <span data-ttu-id="00131-216">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="00131-216">Click **Create**.</span></span>
 
### <a name="creating-a-rightscale-test-user"></a><span data-ttu-id="00131-217">建立 Rightscale 測試使用者</span><span class="sxs-lookup"><span data-stu-id="00131-217">Creating a Rightscale test user</span></span>

<span data-ttu-id="00131-218">在本節中，您會在 RightScale 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="00131-218">In this section, you create a user called Britta Simon in RightScale.</span></span> <span data-ttu-id="00131-219">請與 [Rightscale 客戶支援小組](mailto:support@rightscale.com)合作，在 RightScale 平台中新增使用者。</span><span class="sxs-lookup"><span data-stu-id="00131-219">Work with [Rightscale Client support team](mailto:support@rightscale.com) to add the users in the RightScale platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="00131-220">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="00131-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="00131-221">在本節中，您會將 Rightscale 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="00131-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Rightscale.</span></span>

![指派使用者][200] 

<span data-ttu-id="00131-223">**若要將 Britta Simon 指派給 Rightscale，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="00131-223">**To assign Britta Simon to Rightscale, perform the following steps:**</span></span>

1. <span data-ttu-id="00131-224">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="00131-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="00131-226">在應用程式清單中，選取 [Rightscale]。</span><span class="sxs-lookup"><span data-stu-id="00131-226">In the applications list, select **Rightscale**.</span></span>

    ![設定單一登入](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_app.png) 

3. <span data-ttu-id="00131-228">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="00131-228">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="00131-230">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="00131-230">Click **Add** button.</span></span> <span data-ttu-id="00131-231">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="00131-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="00131-233">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="00131-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="00131-234">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="00131-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="00131-235">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="00131-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="00131-236">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="00131-236">Testing single sign-on</span></span>

<span data-ttu-id="00131-237">本節的目標是要使用「存取面板」來測試您的 Azure AD SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="00131-237">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="00131-238">當您在「存取面板」中按一下 [RightScale] 磚時，應該會自動登入您的 RightScale 應用程式。</span><span class="sxs-lookup"><span data-stu-id="00131-238">When you click the RightScale tile in the Access Panel, you should get automatically signed-on to your RightScale application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="00131-239">其他資源</span><span class="sxs-lookup"><span data-stu-id="00131-239">Additional resources</span></span>

* [<span data-ttu-id="00131-240">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="00131-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="00131-241">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="00131-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_203.png

