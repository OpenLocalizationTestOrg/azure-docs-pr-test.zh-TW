---
title: "教學課程：Azure Active Directory 與 InsideView 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 InsideView 之間。"
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
ms.openlocfilehash: 979c0c24f3a18a193616061b8c2e78292233a56d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-insideview"></a><span data-ttu-id="b3cbf-103">教學課程：Azure Active Directory 與 InsideView 整合</span><span class="sxs-lookup"><span data-stu-id="b3cbf-103">Tutorial: Azure Active Directory integration with InsideView</span></span>

<span data-ttu-id="b3cbf-104">在此教學課程中，您學會如何 toointegrate InsideView 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-104">In this tutorial, you learn how toointegrate InsideView with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b3cbf-105">將 InsideView 整合與 Azure AD 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="b3cbf-105">Integrating InsideView with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b3cbf-106">您可以控制存取 tooInsideView Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="b3cbf-106">You can control in Azure AD who has access tooInsideView</span></span>
- <span data-ttu-id="b3cbf-107">您可以啟用您的使用者 tooautomatically get 登入 tooInsideView （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="b3cbf-107">You can enable your users tooautomatically get signed-on tooInsideView (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b3cbf-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="b3cbf-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b3cbf-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b3cbf-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="b3cbf-110">Prerequisites</span></span>

<span data-ttu-id="b3cbf-111">tooconfigure 與 InsideView 的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="b3cbf-111">tooconfigure Azure AD integration with InsideView, you need hello following items:</span></span>

- <span data-ttu-id="b3cbf-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b3cbf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b3cbf-113">已啟用 InsideView 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b3cbf-113">A InsideView single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b3cbf-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b3cbf-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="b3cbf-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b3cbf-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b3cbf-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b3cbf-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="b3cbf-118">Scenario description</span></span>
<span data-ttu-id="b3cbf-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b3cbf-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="b3cbf-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b3cbf-121">將 InsideView 加入從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="b3cbf-121">Adding InsideView from hello gallery</span></span>
2. <span data-ttu-id="b3cbf-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b3cbf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-insideview-from-hello-gallery"></a><span data-ttu-id="b3cbf-123">將 InsideView 加入從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="b3cbf-123">Adding InsideView from hello gallery</span></span>
<span data-ttu-id="b3cbf-124">tooconfigure hello 整合 InsideView tooAzure AD 中的，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd InsideView。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-124">tooconfigure hello integration of InsideView in tooAzure AD, you need tooadd InsideView from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b3cbf-125">**tooadd InsideView 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b3cbf-125">**tooadd InsideView from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b3cbf-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b3cbf-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b3cbf-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="b3cbf-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="b3cbf-133">在 [hello] 搜尋方塊中，輸入**InsideView**。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-133">In hello search box, type **InsideView**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_search.png)

5. <span data-ttu-id="b3cbf-135">在 hello 結果 窗格中，選取  **InsideView**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-135">In hello results panel, select **InsideView**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b3cbf-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b3cbf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b3cbf-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 InsideView 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-138">In this section, you configure and test Azure AD single sign-on with InsideView based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b3cbf-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 InsideView 中是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in InsideView is tooa user in Azure AD.</span></span> <span data-ttu-id="b3cbf-140">換句話說，Azure AD 使用者與 hello 在 InsideView 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-140">In other words, a link relationship between an Azure AD user and hello related user in InsideView needs toobe established.</span></span>

<span data-ttu-id="b3cbf-141">在 InsideView 中，將指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-141">In InsideView, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b3cbf-142">tooconfigure 及測試 Azure AD 單一登入 InsideView，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="b3cbf-142">tooconfigure and test Azure AD single sign-on with InsideView, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b3cbf-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b3cbf-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b3cbf-145">**[建立測試使用者 InsideView](#creating-a-insideview-test-user)**  -toohave 許 Simon InsideView 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-145">**[Creating a InsideView test user](#creating-a-insideview-test-user)** - toohave a counterpart of Britta Simon in InsideView that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b3cbf-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b3cbf-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b3cbf-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b3cbf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b3cbf-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 InsideView 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your InsideView application.</span></span>

<span data-ttu-id="b3cbf-150">**tooconfigure Azure AD 單一登入 InsideView，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b3cbf-150">**tooconfigure Azure AD single sign-on with InsideView, perform hello following steps:**</span></span>

1. <span data-ttu-id="b3cbf-151">在 Azure 入口網站上 hello hello **InsideView**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-151">In hello Azure portal, on hello **InsideView** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="b3cbf-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_samlbase.png)

3. <span data-ttu-id="b3cbf-155">在 hello **InsideView 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="b3cbf-155">On hello **InsideView Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_url.png)
    
    <span data-ttu-id="b3cbf-157">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://my.insideview.com/iv/<STS Name>/login.iv`</span><span class="sxs-lookup"><span data-stu-id="b3cbf-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://my.insideview.com/iv/<STS Name>/login.iv`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b3cbf-158">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-158">This value is not real.</span></span> <span data-ttu-id="b3cbf-159">更新此值與 hello 實際的回覆 URL。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-159">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="b3cbf-160">請連絡[InsideView 支援小組](mailto:support@insideview.com)tooget 此值。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-160">Contact [InsideView support team ](mailto:support@insideview.com) tooget this value.</span></span>
 
4. <span data-ttu-id="b3cbf-161">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Raw)**然後儲存 hello 憑證檔案儲存在您的電腦。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-161">On hello **SAML Signing Certificate** section, click **Certificate (Raw)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_certificate.png) 

5. <span data-ttu-id="b3cbf-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-insideview-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b3cbf-165">在 hello **InsideView 設定**區段中，按一下**設定 InsideView** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-165">On hello **InsideView Configuration** section, click **Configure InsideView** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b3cbf-166">複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="b3cbf-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_configure.png) 

7. <span data-ttu-id="b3cbf-168">在不同的網頁瀏覽器視窗中，系統管理員身分登入 tooyour InsideView 公司網站。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-168">In a different web browser window, log in tooyour InsideView company site as an administrator.</span></span>

8. <span data-ttu-id="b3cbf-169">在 hello hello 上方的工具列中按一下**Admin**，**單一登入設定**，然後按一下**新增 SAML**。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-169">In hello toolbar on hello top, click **Admin**, **SingleSignOn Settings**, and then click **Add SAML**.</span></span>
   
   <span data-ttu-id="b3cbf-170">![SAML 單一登入設定](./media/active-directory-saas-insideview-tutorial/ic794135.png "SAML 單一登入設定")</span><span class="sxs-lookup"><span data-stu-id="b3cbf-170">![SAML Single Sign On Settings](./media/active-directory-saas-insideview-tutorial/ic794135.png "SAML Single Sign On Settings")</span></span>

9. <span data-ttu-id="b3cbf-171">在 hello**加入新 SAML**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="b3cbf-171">In hello **Add a New SAML** section, perform hello following steps:</span></span>

    <span data-ttu-id="b3cbf-172">![加入新的 SAML](./media/active-directory-saas-insideview-tutorial/ic794136.png "加入新的 SAML")</span><span class="sxs-lookup"><span data-stu-id="b3cbf-172">![Add a New SAML](./media/active-directory-saas-insideview-tutorial/ic794136.png "Add a New SAML")</span></span>
   
    <span data-ttu-id="b3cbf-173">a.</span><span class="sxs-lookup"><span data-stu-id="b3cbf-173">a.</span></span> <span data-ttu-id="b3cbf-174">在 hello **STS 名稱**文字方塊中，輸入您的組態名稱。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-174">In hello **STS Name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="b3cbf-175">b.</span><span class="sxs-lookup"><span data-stu-id="b3cbf-175">b.</span></span> <span data-ttu-id="b3cbf-176">在**SamlP/Ws-fed 未經要求即端點**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-176">In **SamlP/WS-Fed Unsolicited EndPoint** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="b3cbf-177">c.</span><span class="sxs-lookup"><span data-stu-id="b3cbf-177">c.</span></span> <span data-ttu-id="b3cbf-178">開啟 base-64 編碼的憑證，您已從 Azure 入口網站中，複製 hello 到剪貼簿內容的下載，其中，然後將它貼入 toohello **STS 憑證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-178">Open your base-64 encoded certificate, which you have downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **STS Certificate** textbox.</span></span>

    <span data-ttu-id="b3cbf-179">d.</span><span class="sxs-lookup"><span data-stu-id="b3cbf-179">d.</span></span> <span data-ttu-id="b3cbf-180">在 hello **Crm 使用者 Id 對應**文字方塊中，輸入`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-180">In hello **Crm User Id Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
        
    <span data-ttu-id="b3cbf-181">e.</span><span class="sxs-lookup"><span data-stu-id="b3cbf-181">e.</span></span> <span data-ttu-id="b3cbf-182">在 hello **Crm 電子郵件對應**文字方塊中，輸入`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-182">In hello **Crm Email Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="b3cbf-183">f.</span><span class="sxs-lookup"><span data-stu-id="b3cbf-183">f.</span></span> <span data-ttu-id="b3cbf-184">在 hello **Crm 名字對應**文字方塊中，輸入`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-184">In hello **Crm First Name Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
    
    <span data-ttu-id="b3cbf-185">g.</span><span class="sxs-lookup"><span data-stu-id="b3cbf-185">g.</span></span> <span data-ttu-id="b3cbf-186">在 hello **Crm lastName 對應**文字方塊中，輸入`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-186">In hello **Crm lastName Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>  

    <span data-ttu-id="b3cbf-187">h.</span><span class="sxs-lookup"><span data-stu-id="b3cbf-187">h.</span></span> <span data-ttu-id="b3cbf-188">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-188">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="b3cbf-189">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="b3cbf-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b3cbf-190">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b3cbf-191">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b3cbf-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b3cbf-192">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b3cbf-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="b3cbf-193">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="b3cbf-195">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b3cbf-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b3cbf-196">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-insideview-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b3cbf-198">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-insideview-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b3cbf-200">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-insideview-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b3cbf-202">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="b3cbf-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-insideview-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b3cbf-204">a.</span><span class="sxs-lookup"><span data-stu-id="b3cbf-204">a.</span></span> <span data-ttu-id="b3cbf-205">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b3cbf-206">b.</span><span class="sxs-lookup"><span data-stu-id="b3cbf-206">b.</span></span> <span data-ttu-id="b3cbf-207">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b3cbf-208">c.</span><span class="sxs-lookup"><span data-stu-id="b3cbf-208">c.</span></span> <span data-ttu-id="b3cbf-209">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b3cbf-210">d.</span><span class="sxs-lookup"><span data-stu-id="b3cbf-210">d.</span></span> <span data-ttu-id="b3cbf-211">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-211">Click **Create**.</span></span>
 
### <a name="creating-a-insideview-test-user"></a><span data-ttu-id="b3cbf-212">建立 InsideView 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b3cbf-212">Creating a InsideView test user</span></span>

<span data-ttu-id="b3cbf-213">tooenable Azure AD 使用者 toolog 中 tooInsideView，必須將他們佈建 tooInsideView 中。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-213">tooenable Azure AD users toolog in tooInsideView, they must be provisioned in tooInsideView.</span></span> <span data-ttu-id="b3cbf-214">在 InsideView 的 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-214">In hello case of InsideView, provisioning is a manual task.</span></span>

<span data-ttu-id="b3cbf-215">在 InsideView 中，請連絡建立 tooget 使用者或連絡人[InsideView 支援小組](mailto:support@insideview.com)。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-215">tooget users or contacts created in InsideView, Contact [InsideView support team](mailto:support@insideview.com).</span></span>

>[!NOTE]
><span data-ttu-id="b3cbf-216">您可以使用任何其他 InsideView 使用者帳戶建立工具或 Api 提供 InsideView tooprovision Azure AD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-216">You can use any other InsideView user account creation tools or APIs provided by InsideView tooprovision Azure AD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b3cbf-217">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="b3cbf-217">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b3cbf-218">在本節中，您可以授與存取 tooInsideView 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-218">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooInsideView.</span></span>

![指派使用者][200] 

<span data-ttu-id="b3cbf-220">**tooassign 許 Simon tooInsideView，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b3cbf-220">**tooassign Britta Simon tooInsideView, perform hello following steps:**</span></span>

1. <span data-ttu-id="b3cbf-221">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-221">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="b3cbf-223">在 [hello] 應用程式清單中，選取**InsideView**。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-223">In hello applications list, select **InsideView**.</span></span>

    ![設定單一登入](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_app.png) 

3. <span data-ttu-id="b3cbf-225">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-225">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="b3cbf-227">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-227">Click **Add** button.</span></span> <span data-ttu-id="b3cbf-228">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-228">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="b3cbf-230">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-230">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b3cbf-231">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-231">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b3cbf-232">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-232">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b3cbf-233">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="b3cbf-233">Testing single sign-on</span></span>

<span data-ttu-id="b3cbf-234">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-234">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b3cbf-235">當您按一下將 InsideView 磚 hello hello 存取面板中的時，您應該取得自動登入 tooyour InsideView 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b3cbf-235">When you click hello InsideView tile in hello Access Panel, you should get automatically signed-on tooyour InsideView application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b3cbf-236">其他資源</span><span class="sxs-lookup"><span data-stu-id="b3cbf-236">Additional resources</span></span>

* [<span data-ttu-id="b3cbf-237">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b3cbf-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b3cbf-238">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="b3cbf-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

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

