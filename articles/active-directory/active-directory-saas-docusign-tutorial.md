---
title: "教學課程：Azure Active Directory 與 DocuSign 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 DocuSign 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a691288b-84c1-40fb-84bd-5b06878865f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: 29c99fdf39d366df90abc070f7b836320935035c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-docusign"></a><span data-ttu-id="298c1-103">教學課程：Azure Active Directory 與 DocuSign 整合</span><span class="sxs-lookup"><span data-stu-id="298c1-103">Tutorial: Azure Active Directory integration with DocuSign</span></span>

<span data-ttu-id="298c1-104">在本教學課程中，您會了解如何整合 DocuSign 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="298c1-104">In this tutorial, you learn how to integrate DocuSign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="298c1-105">DocuSign 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="298c1-105">Integrating DocuSign with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="298c1-106">您可以在 Azure AD 中控制可存取 DocuSign 的人員</span><span class="sxs-lookup"><span data-stu-id="298c1-106">You can control in Azure AD who has access to DocuSign</span></span>
- <span data-ttu-id="298c1-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 DocuSign (單一登入)</span><span class="sxs-lookup"><span data-stu-id="298c1-107">You can enable your users to automatically get signed-on to DocuSign (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="298c1-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="298c1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="298c1-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="298c1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="298c1-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="298c1-110">Prerequisites</span></span>

<span data-ttu-id="298c1-111">若要設定 Azure AD 與 DocuSign 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="298c1-111">To configure Azure AD integration with DocuSign, you need the following items:</span></span>

- <span data-ttu-id="298c1-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="298c1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="298c1-113">已啟用 DocuSign 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="298c1-113">A DocuSign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="298c1-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="298c1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="298c1-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="298c1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="298c1-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="298c1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="298c1-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="298c1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="298c1-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="298c1-118">Scenario description</span></span>
<span data-ttu-id="298c1-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="298c1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="298c1-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="298c1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="298c1-121">從資源庫新增 DocuSign</span><span class="sxs-lookup"><span data-stu-id="298c1-121">Adding DocuSign from the gallery</span></span>
2. <span data-ttu-id="298c1-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="298c1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-docusign-from-the-gallery"></a><span data-ttu-id="298c1-123">從資源庫新增 DocuSign</span><span class="sxs-lookup"><span data-stu-id="298c1-123">Adding DocuSign from the gallery</span></span>
<span data-ttu-id="298c1-124">若要設定將 DocuSign 整合到 Azure AD 中，您需要從資源庫將 DocuSign 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="298c1-124">To configure the integration of DocuSign into Azure AD, you need to add DocuSign from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="298c1-125">**若要從資源庫新增 DocuSign，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="298c1-125">**To add DocuSign from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="298c1-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="298c1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="298c1-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="298c1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="298c1-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="298c1-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="298c1-131">按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="298c1-131">Click **New application** button on the top of the dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="298c1-133">在搜尋方塊中，輸入 **DocuSign**。</span><span class="sxs-lookup"><span data-stu-id="298c1-133">In the search box, type **DocuSign**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_search.png)

5. <span data-ttu-id="298c1-135">在結果窗格中，選取 [DocuSign]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="298c1-135">In the results panel, select **DocuSign**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="298c1-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="298c1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="298c1-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 DocuSign 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="298c1-138">In this section, you configure and test Azure AD single sign-on with DocuSign based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="298c1-139">若要讓單一登入運作，Azure AD 必須知道 DocuSign 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="298c1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in DocuSign is to a user in Azure AD.</span></span> <span data-ttu-id="298c1-140">換句話說，必須建立 Azure AD 使用者和 DocuSign 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="298c1-140">In other words, a link relationship between an Azure AD user and the related user in DocuSign needs to be established.</span></span>

<span data-ttu-id="298c1-141">建立此連結關聯性的方法，就是將 Azure AD 中**使用者名稱**的值指派為 DocuSign 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="298c1-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in DocuSign.</span></span>

<span data-ttu-id="298c1-142">若要設定及測試與 DocuSign 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="298c1-142">To configure and test Azure AD single sign-on with DocuSign, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="298c1-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="298c1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="298c1-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="298c1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="298c1-145">**[建立 DocuSign 測試使用者](#creating-a-docusign-test-user)** - 在 DocuSign 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="298c1-145">**[Creating a DocuSign test user](#creating-a-docusign-test-user)** - to have a counterpart of Britta Simon in DocuSign that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="298c1-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="298c1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="298c1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="298c1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="298c1-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="298c1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="298c1-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 DocuSign 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="298c1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your DocuSign application.</span></span>

<span data-ttu-id="298c1-150">**若要使用 DocuSign 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="298c1-150">**To configure Azure AD single sign-on with DocuSign, perform the following steps:**</span></span>

1. <span data-ttu-id="298c1-151">在 Azure 入口網站的 [DocuSign] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="298c1-151">In the Azure portal, on the **DocuSign** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="298c1-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="298c1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_samlbase.png)

3. <span data-ttu-id="298c1-155">在 [SAML 簽署憑證] 區段上，按一下 [\憑證 (Base 64)\]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="298c1-155">On the **SAML Signing Certificate** section, click **Certificate(Base 64)** and then save certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_certificate.png) 

4. <span data-ttu-id="298c1-157">在 Azure 入口網站的 [DocuSign 設定] 區段中，按一下 [設定 DocuSign] 可開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="298c1-157">On the **DocuSign Configuration** section of Azure portal, Click **Configure DocuSign** to open Configure sign-on window.</span></span> <span data-ttu-id="298c1-158">從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="298c1-158">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>
    
    ![設定單一登入](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_configure.png)

5. <span data-ttu-id="298c1-160">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 **DocuSign 系統管理入口網站**。</span><span class="sxs-lookup"><span data-stu-id="298c1-160">In a different web browser window, login to your **DocuSign admin portal** as an administrator.</span></span>

6. <span data-ttu-id="298c1-161">在左側導覽功能表中按一下 [網域] 。</span><span class="sxs-lookup"><span data-stu-id="298c1-161">In the navigation menu on the left, click **Domains**.</span></span>
   
    ![設定單一登入][51]

7. <span data-ttu-id="298c1-163">在右窗格中，按一下 [宣告網域] 。</span><span class="sxs-lookup"><span data-stu-id="298c1-163">On the right pane, click **Claim Domain**.</span></span>
   
    ![設定單一登入][52]

8. <span data-ttu-id="298c1-165">在 [宣告網域] 對話方塊，於 [網域名稱] 文字方塊內輸入您的公司網域，然後按一下 [宣告]。</span><span class="sxs-lookup"><span data-stu-id="298c1-165">On the **Claim a domain** dialog, in the **Domain Name** textbox, type your company domain, and then click **Claim**.</span></span> <span data-ttu-id="298c1-166">確定您已驗證網域，而且狀態為作用中。</span><span class="sxs-lookup"><span data-stu-id="298c1-166">Make sure that you verify the domain and the status is active.</span></span>
   
    ![設定單一登入][53]

9. <span data-ttu-id="298c1-168">在左側的功能表中，按一下 [識別提供者] </span><span class="sxs-lookup"><span data-stu-id="298c1-168">In menu on the left side, click **Identity Providers**</span></span>  
   
    ![設定單一登入][54]
10. <span data-ttu-id="298c1-170">在右窗格中，按一下 [新增識別提供者] 。</span><span class="sxs-lookup"><span data-stu-id="298c1-170">In the right pane, click **Add Identity Provider**.</span></span> 
   
    ![設定單一登入][55]

11. <span data-ttu-id="298c1-172">在 [識別提供者設定]  頁面上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="298c1-172">On the **Identity Provider Settings** page, perform the following steps:</span></span>
   
    ![設定單一登入][56]

    <span data-ttu-id="298c1-174">a.</span><span class="sxs-lookup"><span data-stu-id="298c1-174">a.</span></span> <span data-ttu-id="298c1-175">在 [名稱] 文字方塊中，輸入組態的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="298c1-175">In the **Name** textbox, type a unique name for your configuration.</span></span> <span data-ttu-id="298c1-176">請勿使用空格。</span><span class="sxs-lookup"><span data-stu-id="298c1-176">Do not use spaces.</span></span>

    <span data-ttu-id="298c1-177">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="298c1-177">b.</span></span> <span data-ttu-id="298c1-178">將 **SAML 實體識別碼**貼到 [識別提供者簽發者] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="298c1-178">Paste **SAML Entity ID** into the **Identity Provider Issuer** textbox.</span></span>

    <span data-ttu-id="298c1-179">c.</span><span class="sxs-lookup"><span data-stu-id="298c1-179">c.</span></span> <span data-ttu-id="298c1-180">將 [SAML 單一登入服務 URL] 貼到 [識別提供者登入 URL] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="298c1-180">Paste **SAML Single Sign-On Service URL** into the **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="298c1-181">d.</span><span class="sxs-lookup"><span data-stu-id="298c1-181">d.</span></span> <span data-ttu-id="298c1-182">將 [登出 URL] 貼到 [識別提供者登出 URL] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="298c1-182">Paste **Sign-Out URL** into the **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="298c1-183">e.</span><span class="sxs-lookup"><span data-stu-id="298c1-183">e.</span></span> <span data-ttu-id="298c1-184">選取 [登入驗證要求]。</span><span class="sxs-lookup"><span data-stu-id="298c1-184">Select **Sign AuthN Request**.</span></span>

    <span data-ttu-id="298c1-185">f.</span><span class="sxs-lookup"><span data-stu-id="298c1-185">f.</span></span> <span data-ttu-id="298c1-186">選取 [POST] 做為 [驗證要求傳送方式]。</span><span class="sxs-lookup"><span data-stu-id="298c1-186">As **Send AuthN request by**, select **POST**.</span></span>

    <span data-ttu-id="298c1-187">g.</span><span class="sxs-lookup"><span data-stu-id="298c1-187">g.</span></span> <span data-ttu-id="298c1-188">選取 [GET] 作為 [登出要求傳送方式]。</span><span class="sxs-lookup"><span data-stu-id="298c1-188">As **Send logout request by**, select **GET**.</span></span>

12. <span data-ttu-id="298c1-189">在 [自訂屬性對應] 區段中，選擇您想要與 Azure AD 宣告對應的欄位。</span><span class="sxs-lookup"><span data-stu-id="298c1-189">In the **Custom Attribute Mapping** section, choose the field you want to map with Azure AD Claim.</span></span> <span data-ttu-id="298c1-190">在此範例中，**emailaddress** 宣告的對應值是 **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**。</span><span class="sxs-lookup"><span data-stu-id="298c1-190">In this example, the **emailaddress** claim is mapped with the value of **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span> <span data-ttu-id="298c1-191">這是 Azure AD 針對電子郵件宣告所提供的預設宣告名稱。</span><span class="sxs-lookup"><span data-stu-id="298c1-191">It is the default claim name from Azure AD for email claim.</span></span> 
   
    > [!NOTE]
    > <span data-ttu-id="298c1-192">請使用適當的 **使用者識別碼**，將使用者從 Azure AD 對應到 DocuSign 使用者對應。</span><span class="sxs-lookup"><span data-stu-id="298c1-192">Use the appropriate **User identifier** to map the user from Azure AD to DocuSign user mapping.</span></span> <span data-ttu-id="298c1-193">選取適當的欄位，並根據組織的設定輸入適當的值。</span><span class="sxs-lookup"><span data-stu-id="298c1-193">Select the proper Field and enter the appropriate value based on your organization settings.</span></span>
          
    ![設定單一登入][57]

13. <span data-ttu-id="298c1-195">在 [識別提供者憑證] 區段中按一下 [新增憑證]，然後上傳您已從 Azure AD 入口網站下載的憑證。</span><span class="sxs-lookup"><span data-stu-id="298c1-195">In the **Identity Provider Certificate** section, click **Add Certificate**, and then upload the certificate you have downloaded from Azure AD portal.</span></span>   
   
    ![設定單一登入][58]

14. <span data-ttu-id="298c1-197">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="298c1-197">Click **Save**.</span></span>

15. <span data-ttu-id="298c1-198">在 [識別提供者] 區段中，按一下 [動作]，然後按一下 [端點]。</span><span class="sxs-lookup"><span data-stu-id="298c1-198">In the **Identity Providers** section, click **Actions**, and then click **Endpoints**.</span></span>   
   
    ![設定單一登入][59]
 
16. <span data-ttu-id="298c1-200">在 **DocuSign 系統管理入口網站**的 [檢視 SAML 2.0 端點] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="298c1-200">In the **View SAML 2.0 Endpoints** section on **DocuSign admin portal**, perform the following steps:</span></span>
   
    ![設定單一登入][60]
   
    <span data-ttu-id="298c1-202">a.</span><span class="sxs-lookup"><span data-stu-id="298c1-202">a.</span></span> <span data-ttu-id="298c1-203">複製**服務提供者簽發者 URL**，然後貼入 Azure 入口網站的 **DocuSign 網域與 URL** 區段上的 [識別碼] 文字方塊，請遵循下列模式：`https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`。</span><span class="sxs-lookup"><span data-stu-id="298c1-203">Copy the **Service Provider Issuer URL**, and then paste into the **Identifier** textbox on **DocuSign Domain and URLs** section of the Azure portal following the pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.</span></span>
   
    <span data-ttu-id="298c1-204">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="298c1-204">b.</span></span> <span data-ttu-id="298c1-205">複製**服務提供者登入 URL**，然後貼入 Azure 入口網站的 [DocuSign 網域與 URL] 區段上的 [登入 URL] 文字方塊，遵循下列模式：`https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`。</span><span class="sxs-lookup"><span data-stu-id="298c1-205">Copy the **Service Provider Login URL**, and then paste into the **Sign On URL** textbox on **DocuSign Domain and URLs** section of the Azure portal following the pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.</span></span>

    ![設定單一登入](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_url.png)
      
    <span data-ttu-id="298c1-207">c.</span><span class="sxs-lookup"><span data-stu-id="298c1-207">c.</span></span>  <span data-ttu-id="298c1-208">按一下 [關閉]。</span><span class="sxs-lookup"><span data-stu-id="298c1-208">Click **Close**</span></span>
    
17. <span data-ttu-id="298c1-209">在 Azure 入口網站上，按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="298c1-209">On the Azure portal, click **Save**.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-docusign-tutorial/tutorial_general_400.png)

> [!TIP]
> <span data-ttu-id="298c1-211">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="298c1-211">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="298c1-212">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="298c1-212">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="298c1-213">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="298c1-213">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="298c1-214">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="298c1-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="298c1-215">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="298c1-215">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="298c1-217">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="298c1-217">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="298c1-218">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="298c1-218">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-docusign-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="298c1-220">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="298c1-220">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-docusign-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="298c1-222">在對話方塊的頂端，按一下 [新增] 以開啟 [使用者] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="298c1-222">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-docusign-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="298c1-224">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="298c1-224">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-docusign-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="298c1-226">a.</span><span class="sxs-lookup"><span data-stu-id="298c1-226">a.</span></span> <span data-ttu-id="298c1-227">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="298c1-227">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="298c1-228">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="298c1-228">b.</span></span> <span data-ttu-id="298c1-229">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="298c1-229">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="298c1-230">c.</span><span class="sxs-lookup"><span data-stu-id="298c1-230">c.</span></span> <span data-ttu-id="298c1-231">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="298c1-231">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="298c1-232">d.</span><span class="sxs-lookup"><span data-stu-id="298c1-232">d.</span></span> <span data-ttu-id="298c1-233">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="298c1-233">Click **Create**.</span></span>
 
### <a name="creating-a-docusign-test-user"></a><span data-ttu-id="298c1-234">建立 DocuSign 測試使用者</span><span class="sxs-lookup"><span data-stu-id="298c1-234">Creating a DocuSign test user</span></span>

<span data-ttu-id="298c1-235">應用程式支援**及時 (Just In Time) 使用者佈建**，而在驗證之後，則會在應用程式中自動建立使用者。</span><span class="sxs-lookup"><span data-stu-id="298c1-235">Application supports **Just in time user provisioning** and after authentication users are created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="298c1-236">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="298c1-236">Assigning the Azure AD test user</span></span>

<span data-ttu-id="298c1-237">在本節中，您會將 DocuSign 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="298c1-237">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to DocuSign.</span></span>

![指派使用者][200] 

<span data-ttu-id="298c1-239">**若要將 Britta Simon 指派給 DocuSign，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="298c1-239">**To assign Britta Simon to DocuSign, perform the following steps:**</span></span>

1. <span data-ttu-id="298c1-240">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="298c1-240">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="298c1-242">在應用程式清單中，選取 [DocuSign]。</span><span class="sxs-lookup"><span data-stu-id="298c1-242">In the applications list, select **DocuSign**.</span></span>

    ![設定單一登入](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_app.png) 

3. <span data-ttu-id="298c1-244">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="298c1-244">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="298c1-246">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="298c1-246">Click **Add** button.</span></span> <span data-ttu-id="298c1-247">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="298c1-247">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="298c1-249">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="298c1-249">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="298c1-250">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="298c1-250">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="298c1-251">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="298c1-251">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="298c1-252">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="298c1-252">Testing single sign-on</span></span>

<span data-ttu-id="298c1-253">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="298c1-253">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="298c1-254">當您在存取面板中按一下 [DocuSign] 磚時，應該會自動登入您的 DocuSign 應用程式。</span><span class="sxs-lookup"><span data-stu-id="298c1-254">When you click the DocuSign tile in the Access Panel, you should get automatically signed-on to your DocuSign application.</span></span>
<span data-ttu-id="298c1-255">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="298c1-255">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="298c1-256">其他資源</span><span class="sxs-lookup"><span data-stu-id="298c1-256">Additional resources</span></span>

* [<span data-ttu-id="298c1-257">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="298c1-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="298c1-258">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="298c1-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="298c1-259">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="298c1-259">Configure User Provisioning</span></span>](active-directory-saas-docusign-provisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_04.png
[51]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_21.png
[52]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_22.png
[53]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_23.png
[54]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_19.png
[55]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_20.png
[56]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_24.png
[57]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_25.png
[58]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_26.png
[59]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_27.png
[60]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_28.png
[61]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_29.png
[100]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_203.png

