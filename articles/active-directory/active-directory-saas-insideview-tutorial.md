---
title: "教學課程：Azure Active Directory 與 InsideView 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 InsideView 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c489a7ab-6b1f-4efb-8a66-8bc13bca78c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: f2b0a1d4bc44f8d0cd57c61e2d78950cb6a99854
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-insideview"></a><span data-ttu-id="69756-103">教學課程：Azure Active Directory 與 InsideView 整合</span><span class="sxs-lookup"><span data-stu-id="69756-103">Tutorial: Azure Active Directory integration with InsideView</span></span>

<span data-ttu-id="69756-104">在本教學課程中，您將了解如何整合 InsideView 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="69756-104">In this tutorial, you learn how to integrate InsideView with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="69756-105">InsideView 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="69756-105">Integrating InsideView with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="69756-106">您可以在 Azure AD 中控制可存取 InsideView 的人員</span><span class="sxs-lookup"><span data-stu-id="69756-106">You can control in Azure AD who has access to InsideView</span></span>
- <span data-ttu-id="69756-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 InsideView (單一登入)</span><span class="sxs-lookup"><span data-stu-id="69756-107">You can enable your users to automatically get signed-on to InsideView (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="69756-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="69756-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="69756-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="69756-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="69756-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="69756-110">Prerequisites</span></span>

<span data-ttu-id="69756-111">若要設定 Azure AD 與 InsideView 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="69756-111">To configure Azure AD integration with InsideView, you need the following items:</span></span>

- <span data-ttu-id="69756-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="69756-112">An Azure AD subscription</span></span>
- <span data-ttu-id="69756-113">已啟用 InsideView 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="69756-113">A InsideView single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="69756-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="69756-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="69756-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="69756-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="69756-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="69756-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="69756-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="69756-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="69756-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="69756-118">Scenario description</span></span>
<span data-ttu-id="69756-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="69756-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="69756-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="69756-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="69756-121">從資源庫新增 InsideView</span><span class="sxs-lookup"><span data-stu-id="69756-121">Adding InsideView from the gallery</span></span>
2. <span data-ttu-id="69756-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="69756-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-insideview-from-the-gallery"></a><span data-ttu-id="69756-123">從資源庫新增 InsideView</span><span class="sxs-lookup"><span data-stu-id="69756-123">Adding InsideView from the gallery</span></span>
<span data-ttu-id="69756-124">若要設定將 InsideView 整合到 Azure AD 中，您需要從資源庫將 InsideView 新增到受管理的 SaaS app 清單。</span><span class="sxs-lookup"><span data-stu-id="69756-124">To configure the integration of InsideView in to Azure AD, you need to add InsideView from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="69756-125">**若要從資源庫新增 InsideView，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="69756-125">**To add InsideView from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="69756-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="69756-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="69756-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="69756-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="69756-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="69756-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="69756-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="69756-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="69756-133">在搜尋方塊中，輸入 **InsideView**。</span><span class="sxs-lookup"><span data-stu-id="69756-133">In the search box, type **InsideView**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_search.png)

5. <span data-ttu-id="69756-135">在結果窗格中，選取 [InsideView]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="69756-135">In the results panel, select **InsideView**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="69756-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="69756-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="69756-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 InsideView 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="69756-138">In this section, you configure and test Azure AD single sign-on with InsideView based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="69756-139">若要讓單一登入運作，Azure AD 必須知道 InsideView 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="69756-139">For single sign-on to work, Azure AD needs to know what the counterpart user in InsideView is to a user in Azure AD.</span></span> <span data-ttu-id="69756-140">換句話說，必須建立 Azure AD 使用者和 InsideView 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="69756-140">In other words, a link relationship between an Azure AD user and the related user in InsideView needs to be established.</span></span>

<span data-ttu-id="69756-141">在 InsideView 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="69756-141">In InsideView, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="69756-142">若要設定及測試與 InsideView 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="69756-142">To configure and test Azure AD single sign-on with InsideView, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="69756-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="69756-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="69756-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="69756-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="69756-145">**[建立 InsideView 測試使用者](#creating-a-insideview-test-user)** - 使 InsideView 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="69756-145">**[Creating a InsideView test user](#creating-a-insideview-test-user)** - to have a counterpart of Britta Simon in InsideView that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="69756-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="69756-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="69756-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="69756-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="69756-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="69756-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="69756-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 InsideView 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="69756-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your InsideView application.</span></span>

<span data-ttu-id="69756-150">**若要設定與 InsideView 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="69756-150">**To configure Azure AD single sign-on with InsideView, perform the following steps:**</span></span>

1. <span data-ttu-id="69756-151">在 Azure 入口網站的 [InsideView] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="69756-151">In the Azure portal, on the **InsideView** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="69756-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="69756-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_samlbase.png)

3. <span data-ttu-id="69756-155">在 [InsideView 網域及 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="69756-155">On the **InsideView Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_url.png)
    
    <span data-ttu-id="69756-157">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://my.insideview.com/iv/<STS Name>/login.iv`</span><span class="sxs-lookup"><span data-stu-id="69756-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://my.insideview.com/iv/<STS Name>/login.iv`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="69756-158">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="69756-158">This value is not real.</span></span> <span data-ttu-id="69756-159">請使用實際的「回覆 URL」來更新此值。</span><span class="sxs-lookup"><span data-stu-id="69756-159">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="69756-160">請連絡 [InsideView 支援小組](mailto:support@insideview.com)以取得此值。</span><span class="sxs-lookup"><span data-stu-id="69756-160">Contact [InsideView support team ](mailto:support@insideview.com) to get this value.</span></span>
 
4. <span data-ttu-id="69756-161">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (原始)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="69756-161">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_certificate.png) 

5. <span data-ttu-id="69756-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="69756-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-insideview-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="69756-165">在 [InsideView 組態] 區段上，按一下 [設定 InsideView] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="69756-165">On the **InsideView Configuration** section, click **Configure InsideView** to open **Configure sign-on** window.</span></span> <span data-ttu-id="69756-166">從 [快速參考] 區段中複製 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="69756-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_configure.png) 

7. <span data-ttu-id="69756-168">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 InsideView 公司網站。</span><span class="sxs-lookup"><span data-stu-id="69756-168">In a different web browser window, log in to your InsideView company site as an administrator.</span></span>

8. <span data-ttu-id="69756-169">在頂端的工具列中，按一下 [系統管理員]，[單一登入設定設定]，然後按一下 [新增 SAML]。</span><span class="sxs-lookup"><span data-stu-id="69756-169">In the toolbar on the top, click **Admin**, **SingleSignOn Settings**, and then click **Add SAML**.</span></span>
   
   <span data-ttu-id="69756-170">![SAML 單一登入設定](./media/active-directory-saas-insideview-tutorial/ic794135.png "SAML 單一登入設定")</span><span class="sxs-lookup"><span data-stu-id="69756-170">![SAML Single Sign On Settings](./media/active-directory-saas-insideview-tutorial/ic794135.png "SAML Single Sign On Settings")</span></span>

9. <span data-ttu-id="69756-171">在 [加入新的 SAML]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="69756-171">In the **Add a New SAML** section, perform the following steps:</span></span>

    <span data-ttu-id="69756-172">![加入新的 SAML](./media/active-directory-saas-insideview-tutorial/ic794136.png "加入新的 SAML")</span><span class="sxs-lookup"><span data-stu-id="69756-172">![Add a New SAML](./media/active-directory-saas-insideview-tutorial/ic794136.png "Add a New SAML")</span></span>
   
    <span data-ttu-id="69756-173">a.</span><span class="sxs-lookup"><span data-stu-id="69756-173">a.</span></span> <span data-ttu-id="69756-174">在 [STS 名稱]  文字方塊中，輸入您的組態名稱。</span><span class="sxs-lookup"><span data-stu-id="69756-174">In the **STS Name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="69756-175">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="69756-175">b.</span></span> <span data-ttu-id="69756-176">在 [SamlP/WS-Fed 來路不明端點] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="69756-176">In **SamlP/WS-Fed Unsolicited EndPoint** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="69756-177">c.</span><span class="sxs-lookup"><span data-stu-id="69756-177">c.</span></span> <span data-ttu-id="69756-178">開啟您從 Azure 入口網站下載的 base-64 編碼憑證，將它的內容複製到您的剪貼簿，然後在 [STS 憑證] 文字方塊貼上。</span><span class="sxs-lookup"><span data-stu-id="69756-178">Open your base-64 encoded certificate, which you have downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **STS Certificate** textbox.</span></span>

    <span data-ttu-id="69756-179">d.</span><span class="sxs-lookup"><span data-stu-id="69756-179">d.</span></span> <span data-ttu-id="69756-180">在 [Crm 使用者識別碼對應] 文字方塊中，輸入 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`。</span><span class="sxs-lookup"><span data-stu-id="69756-180">In the **Crm User Id Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
        
    <span data-ttu-id="69756-181">e.</span><span class="sxs-lookup"><span data-stu-id="69756-181">e.</span></span> <span data-ttu-id="69756-182">在 [Crm 電子郵件對應] 文字方塊中，輸入 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`。</span><span class="sxs-lookup"><span data-stu-id="69756-182">In the **Crm Email Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="69756-183">f.</span><span class="sxs-lookup"><span data-stu-id="69756-183">f.</span></span> <span data-ttu-id="69756-184">在 [Crm 名字對應] 文字方塊中，輸入 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`。</span><span class="sxs-lookup"><span data-stu-id="69756-184">In the **Crm First Name Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
    
    <span data-ttu-id="69756-185">g.</span><span class="sxs-lookup"><span data-stu-id="69756-185">g.</span></span> <span data-ttu-id="69756-186">在 [Crm 姓氏對應] 文字方塊中，輸入 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`。</span><span class="sxs-lookup"><span data-stu-id="69756-186">In the **Crm lastName Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>  

    <span data-ttu-id="69756-187">h.</span><span class="sxs-lookup"><span data-stu-id="69756-187">h.</span></span> <span data-ttu-id="69756-188">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="69756-188">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="69756-189">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="69756-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="69756-190">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="69756-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="69756-191">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="69756-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="69756-192">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="69756-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="69756-193">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="69756-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="69756-195">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="69756-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="69756-196">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="69756-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-insideview-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="69756-198">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="69756-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-insideview-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="69756-200">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="69756-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-insideview-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="69756-202">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="69756-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-insideview-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="69756-204">a.</span><span class="sxs-lookup"><span data-stu-id="69756-204">a.</span></span> <span data-ttu-id="69756-205">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="69756-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="69756-206">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="69756-206">b.</span></span> <span data-ttu-id="69756-207">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="69756-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="69756-208">c.</span><span class="sxs-lookup"><span data-stu-id="69756-208">c.</span></span> <span data-ttu-id="69756-209">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="69756-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="69756-210">d.</span><span class="sxs-lookup"><span data-stu-id="69756-210">d.</span></span> <span data-ttu-id="69756-211">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="69756-211">Click **Create**.</span></span>
 
### <a name="creating-a-insideview-test-user"></a><span data-ttu-id="69756-212">建立 InsideView 測試使用者</span><span class="sxs-lookup"><span data-stu-id="69756-212">Creating a InsideView test user</span></span>

<span data-ttu-id="69756-213">若要讓 Azure AD 使用者可以登入 InsideView，則必須將他們佈建到 InsideView。</span><span class="sxs-lookup"><span data-stu-id="69756-213">To enable Azure AD users to log in to InsideView, they must be provisioned in to InsideView.</span></span> <span data-ttu-id="69756-214">在 InsideView 的情況下，佈建是手動工作。</span><span class="sxs-lookup"><span data-stu-id="69756-214">In the case of InsideView, provisioning is a manual task.</span></span>

<span data-ttu-id="69756-215">若要在 InsideView 中建立使用者或連絡人，請連絡 [InsideView 支援小組](mailto:support@insideview.com)。</span><span class="sxs-lookup"><span data-stu-id="69756-215">To get users or contacts created in InsideView, Contact [InsideView support team](mailto:support@insideview.com).</span></span>

>[!NOTE]
><span data-ttu-id="69756-216">您可以使用任何其他的 InsideView 使用者帳戶建立工具或 InsideView 提供的 API 來佈建 Azure AD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="69756-216">You can use any other InsideView user account creation tools or APIs provided by InsideView to provision Azure AD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="69756-217">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="69756-217">Assigning the Azure AD test user</span></span>

<span data-ttu-id="69756-218">在本節中，您會將 InsideView 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="69756-218">In this section, you enable Britta Simon to use Azure single sign-on by granting access to InsideView.</span></span>

![指派使用者][200] 

<span data-ttu-id="69756-220">**若要將 Britta Simon 指派給 InsideView，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="69756-220">**To assign Britta Simon to InsideView, perform the following steps:**</span></span>

1. <span data-ttu-id="69756-221">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="69756-221">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="69756-223">在應用程式清單中，選取 [InsideView]。</span><span class="sxs-lookup"><span data-stu-id="69756-223">In the applications list, select **InsideView**.</span></span>

    ![設定單一登入](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_app.png) 

3. <span data-ttu-id="69756-225">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="69756-225">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="69756-227">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="69756-227">Click **Add** button.</span></span> <span data-ttu-id="69756-228">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="69756-228">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="69756-230">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="69756-230">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="69756-231">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="69756-231">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="69756-232">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="69756-232">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="69756-233">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="69756-233">Testing single sign-on</span></span>

<span data-ttu-id="69756-234">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="69756-234">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="69756-235">當您在存取面板中按一下 [InsideView ] 圖格時，應該會自動登入您的 InsideView 應用程式。</span><span class="sxs-lookup"><span data-stu-id="69756-235">When you click the InsideView tile in the Access Panel, you should get automatically signed-on to your InsideView application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="69756-236">其他資源</span><span class="sxs-lookup"><span data-stu-id="69756-236">Additional resources</span></span>

* [<span data-ttu-id="69756-237">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="69756-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="69756-238">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="69756-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_203.png

