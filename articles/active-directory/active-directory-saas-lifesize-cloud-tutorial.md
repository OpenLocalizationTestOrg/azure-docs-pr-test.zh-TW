---
title: "教學課程：Azure Active Directory 與 Lifesize Cloud 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Lifesize Cloud 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 75fab335-fdcd-4066-b42c-cc738fcb6513
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 7542360f9c75786bf400553090ba0a891d9c2fcc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lifesize-cloud"></a><span data-ttu-id="74391-103">教學課程：Azure Active Directory 與 Lifesize Cloud 整合</span><span class="sxs-lookup"><span data-stu-id="74391-103">Tutorial: Azure Active Directory integration with Lifesize Cloud</span></span>

<span data-ttu-id="74391-104">在本教學課程中，您會了解如何整合 Lifesize Cloud 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="74391-104">In this tutorial, you learn how to integrate Lifesize Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="74391-105">Lifesize Cloud 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="74391-105">Integrating Lifesize Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="74391-106">您可以在 Azure AD 中控制可存取 Lifesize Cloud 的人員</span><span class="sxs-lookup"><span data-stu-id="74391-106">You can control in Azure AD who has access to Lifesize Cloud</span></span>
- <span data-ttu-id="74391-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Lifesize Cloud (單一登入)</span><span class="sxs-lookup"><span data-stu-id="74391-107">You can enable your users to automatically get signed-on to Lifesize Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="74391-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="74391-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="74391-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="74391-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="74391-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="74391-110">Prerequisites</span></span>

<span data-ttu-id="74391-111">若要設定 Azure AD 與 Lifesize Cloud 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="74391-111">To configure Azure AD integration with Lifesize Cloud, you need the following items:</span></span>

- <span data-ttu-id="74391-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="74391-112">An Azure AD subscription</span></span>
- <span data-ttu-id="74391-113">已啟用 Lifesize Cloud 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="74391-113">A Lifesize Cloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="74391-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="74391-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="74391-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="74391-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="74391-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="74391-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="74391-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="74391-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="74391-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="74391-118">Scenario description</span></span>
<span data-ttu-id="74391-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="74391-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="74391-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="74391-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="74391-121">從資源庫新增 Lifesize Cloud</span><span class="sxs-lookup"><span data-stu-id="74391-121">Adding Lifesize Cloud from the gallery</span></span>
2. <span data-ttu-id="74391-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="74391-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lifesize-cloud-from-the-gallery"></a><span data-ttu-id="74391-123">從資源庫新增 Lifesize Cloud</span><span class="sxs-lookup"><span data-stu-id="74391-123">Adding Lifesize Cloud from the gallery</span></span>
<span data-ttu-id="74391-124">若要設定將 Lifesize Cloud 整合到 Azure AD 中，您需要從資源庫將 Lifesize Cloud 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="74391-124">To configure the integration of Lifesize Cloud into Azure AD, you need to add Lifesize Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="74391-125">**若要從資源庫新增 Lifesize Cloud，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="74391-125">**To add Lifesize Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="74391-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="74391-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="74391-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="74391-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="74391-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="74391-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="74391-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="74391-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="74391-133">在搜尋方塊中，輸入 **Lifesize Cloud**。</span><span class="sxs-lookup"><span data-stu-id="74391-133">In the search box, type **Lifesize Cloud**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_search.png)

5. <span data-ttu-id="74391-135">在結果面板中，選取 [Lifesize Cloud]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="74391-135">In the results panel, select **Lifesize Cloud**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="74391-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="74391-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="74391-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Lifesize Cloud 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="74391-138">In this section, you configure and test Azure AD single sign-on with Lifesize Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="74391-139">若要讓單一登入能夠運作，Azure AD 必須知道 Lifesize Cloud 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="74391-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lifesize Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="74391-140">換句話說，必須在 Azure AD 使用者與 Lifesize Cloud 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="74391-140">In other words, a link relationship between an Azure AD user and the related user in Lifesize Cloud needs to be established.</span></span>

<span data-ttu-id="74391-141">在 Lifesize Cloud 中，將 Azure AD 中 [使用者名稱] 的值指派為 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="74391-141">In Lifesize Cloud, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="74391-142">若要設定及測試與 Lifesize Cloud 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="74391-142">To configure and test Azure AD single sign-on with Lifesize Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="74391-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="74391-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="74391-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="74391-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="74391-145">**[建立 Lifesize Cloud 測試使用者](#creating-a-lifesize-cloud-test-user)** - 使 Lifesize Cloud 中 Britta Simon 的對應使用者連結到該使用者在 Azure AD 中的代表身分。</span><span class="sxs-lookup"><span data-stu-id="74391-145">**[Creating a Lifesize Cloud test user](#creating-a-lifesize-cloud-test-user)** - to have a counterpart of Britta Simon in Lifesize Cloud that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="74391-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="74391-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="74391-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="74391-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="74391-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="74391-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="74391-149">在本節中，您將在 Azure 入口網站中啟用 Azure AD 單一登入，並在 Lifesize Cloud 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="74391-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lifesize Cloud application.</span></span>

<span data-ttu-id="74391-150">**若要使用 Lifesize Cloud 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="74391-150">**To configure Azure AD single sign-on with Lifesize Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="74391-151">在 Azure 入口網站的 [Lifesize Cloud] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="74391-151">In the Azure portal, on the **Lifesize Cloud** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="74391-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="74391-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_samlbase.png)

3. <span data-ttu-id="74391-155">在 [Lifesize Cloud 網域及 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="74391-155">On the **Lifesize Cloud Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url.png)

    <span data-ttu-id="74391-157">a.</span><span class="sxs-lookup"><span data-stu-id="74391-157">a.</span></span> <span data-ttu-id="74391-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://login.lifesizecloud.com/ls/?acs`</span><span class="sxs-lookup"><span data-stu-id="74391-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://login.lifesizecloud.com/ls/?acs`</span></span>

    <span data-ttu-id="74391-159">b.</span><span class="sxs-lookup"><span data-stu-id="74391-159">b.</span></span> <span data-ttu-id="74391-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://login.lifesizecloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="74391-160">In the **Identifier** textbox, type a URL using the following pattern: `https://login.lifesizecloud.com/<companyname>`</span></span>

     
4. <span data-ttu-id="74391-161">勾選 [顯示進階的 URL 設定]，然後執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="74391-161">Check **Show advanced URL settings**, perform the following step:</span></span>    
   
    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url1.png)

    <span data-ttu-id="74391-163">在 [轉送狀態] 文字方塊中，輸入使用下列模式的 URL：`https://webapp.lifesizecloud.com/?ent=<identifier>`</span><span class="sxs-lookup"><span data-stu-id="74391-163">In the **Relay state** textbox, type a URL using the following pattern: `https://webapp.lifesizecloud.com/?ent=<identifier>`</span></span>
   
   > [!NOTE] 
   ><span data-ttu-id="74391-164">請注意這些不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="74391-164">Please note that these are not the real values.</span></span> <span data-ttu-id="74391-165">您必須使用實際的登入 URL、轉送狀態及識別碼來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="74391-165">you have to update these values with the actual Sign-On URL, Relay State, and Identifier.</span></span> <span data-ttu-id="74391-166">連絡 [Lifesize Cloud 用戶端支援小組](https://www.lifesize.com/support)，以取得登入 URL 和識別碼值，以及 SSO 設定 (本教學課程後面部分將說明) 中的 [轉送狀態] 值。</span><span class="sxs-lookup"><span data-stu-id="74391-166">Contact [Lifesize Cloud Client support team](https://www.lifesize.com/support) to get Sign-On URL, and Identifier values and you can get Relay State  value from SSO Configuration that is explained later in the tutorial.</span></span>

4. <span data-ttu-id="74391-167">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="74391-167">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_certificate.png) 

5. <span data-ttu-id="74391-169">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="74391-169">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="74391-171">在 [Lifesize Cloud 設定] 區段中，按一下 [設定 Lifesize Cloud] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="74391-171">On the **Lifesize Cloud Configuration** section, click **Configure Lifesize Cloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="74391-172">從 [快速參考] 區段中複製 **SAML 實體識別碼和 SAML 單一登入服務 URL**。</span><span class="sxs-lookup"><span data-stu-id="74391-172">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_configure.png) 

7. <span data-ttu-id="74391-174">若要取得為您的應用程式設定的 SSO，請使用系統管理員權限登入 Lifesize Cloud 應用程式。</span><span class="sxs-lookup"><span data-stu-id="74391-174">To get SSO configured for your application, login into the Lifesize Cloud application with Admin privileges.</span></span>

8. <span data-ttu-id="74391-175">在右上角按一下您的名稱，然後按一下 [進階設定]。</span><span class="sxs-lookup"><span data-stu-id="74391-175">In the top right corner click on your name and then click on the **Advance Settings**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_06.png)

9. <span data-ttu-id="74391-177">在 [進階設定] 中，現在按一下 [SSO 組態] 連結。</span><span class="sxs-lookup"><span data-stu-id="74391-177">In the Advance Settings now click on the **SSO Configuration** link.</span></span> <span data-ttu-id="74391-178">這會開啟您的執行個體的 [SSO 設定] 頁面。</span><span class="sxs-lookup"><span data-stu-id="74391-178">It will open the SSO Configuration page for your instance.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_07.png)

10. <span data-ttu-id="74391-180">現在設定 SSO 組態 UI 中的下列值。</span><span class="sxs-lookup"><span data-stu-id="74391-180">Now configure the following values in the SSO configuration UI.</span></span>    
   
    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_08.png)
    
    <span data-ttu-id="74391-182">a.</span><span class="sxs-lookup"><span data-stu-id="74391-182">a.</span></span> <span data-ttu-id="74391-183">在 [識別提供者簽發者] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 實體識別碼] 值。</span><span class="sxs-lookup"><span data-stu-id="74391-183">In **Identity Provider Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="74391-184">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="74391-184">b.</span></span>  <span data-ttu-id="74391-185">在 [登入 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="74391-185">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="74391-186">c.</span><span class="sxs-lookup"><span data-stu-id="74391-186">c.</span></span> <span data-ttu-id="74391-187">在從 Azure 入口網站下載的記事本檔案中開啟您的 base-64 編碼憑證，將憑證的內容複製到剪貼簿，再貼到 [X.509 憑證]  文字方塊。</span><span class="sxs-lookup"><span data-stu-id="74391-187">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.</span></span>
  
    <span data-ttu-id="74391-188">d.</span><span class="sxs-lookup"><span data-stu-id="74391-188">d.</span></span> <span data-ttu-id="74391-189">在 [名字] 文字方塊的 SAML 屬性對應中，輸入以下格式的值：**http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**</span><span class="sxs-lookup"><span data-stu-id="74391-189">In the SAML Attribute mappings for the First Name text box enter the value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**</span></span>
    
    <span data-ttu-id="74391-190">e.</span><span class="sxs-lookup"><span data-stu-id="74391-190">e.</span></span> <span data-ttu-id="74391-191">在 [姓氏] 文字方塊的 SAML 屬性對應中，輸入以下格式的值：**http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**</span><span class="sxs-lookup"><span data-stu-id="74391-191">In the SAML Attribute mapping for the **Last Name** text box enter the value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**</span></span>
    
    <span data-ttu-id="74391-192">f.</span><span class="sxs-lookup"><span data-stu-id="74391-192">f.</span></span> <span data-ttu-id="74391-193">在 [電子郵件] 文字方塊的 SAML 屬性對應中，輸入以下格式的值：**http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**</span><span class="sxs-lookup"><span data-stu-id="74391-193">In the SAML Attribute mapping for the **Email** text box enter the value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**</span></span>

11. <span data-ttu-id="74391-194">若要檢查組態，您可以按一下 [測試] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="74391-194">To check the configuration you can click on the **Test** button.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="74391-195">為使測試成功，您需要在 Azure AD 中完成組態精靈，同時提供存取權給可執行測試的使用者或群組。</span><span class="sxs-lookup"><span data-stu-id="74391-195">For successful testing you need to complete the configuration wizard in Azure AD and also provide access to users or groups who can perform the test.</span></span>

12. <span data-ttu-id="74391-196">檢查 [啟用 SSO] 按鈕以啟用 SSO。</span><span class="sxs-lookup"><span data-stu-id="74391-196">Enable the SSO by checking on the **Enable SSO** button.</span></span>

13. <span data-ttu-id="74391-197">現在按一下 [更新] 按鈕，以儲存所有設定。</span><span class="sxs-lookup"><span data-stu-id="74391-197">Now click on the **Update** button so that all the settings are saved.</span></span> <span data-ttu-id="74391-198">這會產生 RelayState 值。</span><span class="sxs-lookup"><span data-stu-id="74391-198">This will generate the RelayState value.</span></span> <span data-ttu-id="74391-199">複製文字方塊中產生的 RelayState 值，貼到 [Lifesize Cloud 網域及 URL] 區段下方的 [轉送狀態] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="74391-199">Copy the RelayState value, which is generated in the text box, paste it in the **Relay State** textbox under **Lifesize Cloud Domain and URLs** section.</span></span> 

> [!TIP]
> <span data-ttu-id="74391-200">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="74391-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="74391-201">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="74391-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="74391-202">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="74391-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="74391-203">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="74391-203">Creating an Azure AD test user</span></span>

<span data-ttu-id="74391-204">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="74391-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="74391-206">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="74391-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="74391-207">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="74391-207">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="74391-209">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="74391-209">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="74391-211">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="74391-211">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="74391-213">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="74391-213">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="74391-215">a.</span><span class="sxs-lookup"><span data-stu-id="74391-215">a.</span></span> <span data-ttu-id="74391-216">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="74391-216">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="74391-217">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="74391-217">b.</span></span> <span data-ttu-id="74391-218">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="74391-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="74391-219">c.</span><span class="sxs-lookup"><span data-stu-id="74391-219">c.</span></span> <span data-ttu-id="74391-220">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="74391-220">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="74391-221">d.</span><span class="sxs-lookup"><span data-stu-id="74391-221">d.</span></span> <span data-ttu-id="74391-222">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="74391-222">Click **Create**.</span></span>
 
### <a name="creating-a-lifesize-cloud-test-user"></a><span data-ttu-id="74391-223">建立 Lifesize Cloud 測試使用者</span><span class="sxs-lookup"><span data-stu-id="74391-223">Creating a Lifesize Cloud test user</span></span>

<span data-ttu-id="74391-224">在本節中，您要在 Lifesize Cloud 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="74391-224">In this section, you create a user called Britta Simon in Lifesize Cloud.</span></span> <span data-ttu-id="74391-225">Lifesize Cloud 支援自動使用者佈建。</span><span class="sxs-lookup"><span data-stu-id="74391-225">Lifesize cloud does support automatic user provisioning.</span></span> <span data-ttu-id="74391-226">在 Azure AD 驗證成功後，使用者將自動佈建於應用程式中。</span><span class="sxs-lookup"><span data-stu-id="74391-226">After successful authentication at Azure AD, the user will be automatically provisioned in the application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="74391-227">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="74391-227">Assigning the Azure AD test user</span></span>

<span data-ttu-id="74391-228">在本節中，您將把 Lifesize Cloud 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="74391-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lifesize Cloud.</span></span>

![指派使用者][200] 

<span data-ttu-id="74391-230">**若要將 Britta Simon 指派給 Lifesize Cloud，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="74391-230">**To assign Britta Simon to Lifesize Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="74391-231">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="74391-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="74391-233">在應用程式清單中，選取 [Lifesize Cloud]。 </span><span class="sxs-lookup"><span data-stu-id="74391-233">In the applications list, select **Lifesize Cloud**.</span></span>

    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_app.png) 

3. <span data-ttu-id="74391-235">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="74391-235">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="74391-237">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="74391-237">Click **Add** button.</span></span> <span data-ttu-id="74391-238">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="74391-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="74391-240">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="74391-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="74391-241">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="74391-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="74391-242">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="74391-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="74391-243">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="74391-243">Testing single sign-on</span></span>

<span data-ttu-id="74391-244">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="74391-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="74391-245">按一下存取面板中的 [Lifesize Cloud] 圖格，應會顯示 Lifesize Cloud 應用程式的登入頁面。</span><span class="sxs-lookup"><span data-stu-id="74391-245">When you click the Lifesize Cloud tile in the Access Panel, you should get login page of Lifesize Cloud application.</span></span>
<span data-ttu-id="74391-246">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="74391-246">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="74391-247">其他資源</span><span class="sxs-lookup"><span data-stu-id="74391-247">Additional resources</span></span>

* [<span data-ttu-id="74391-248">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="74391-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="74391-249">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="74391-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_203.png

