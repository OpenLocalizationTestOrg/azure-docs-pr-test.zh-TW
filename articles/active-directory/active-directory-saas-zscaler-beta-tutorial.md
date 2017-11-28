---
title: "教學課程：Azure Active Directory 與 Zscaler Beta 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Zscaler Beta 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 56b846ae-a1e7-45ae-a79d-992a87f075ba
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 1471c2b51ca5684a11acd40f4e450521605bb786
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-beta"></a><span data-ttu-id="bb8cf-103">教學課程：Azure Active Directory 與 Zscaler Beta 整合</span><span class="sxs-lookup"><span data-stu-id="bb8cf-103">Tutorial: Azure Active Directory integration with Zscaler Beta</span></span>

<span data-ttu-id="bb8cf-104">在此教學課程中，您學會如何 toointegrate Zscaler Beta 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-104">In this tutorial, you learn how toointegrate Zscaler Beta with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bb8cf-105">Zscaler Beta 整合與 Azure AD 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="bb8cf-105">Integrating Zscaler Beta with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bb8cf-106">您可以控制存取 tooZscaler beta 版的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="bb8cf-106">You can control in Azure AD who has access tooZscaler Beta</span></span>
- <span data-ttu-id="bb8cf-107">您可以啟用您的使用者 tooautomatically get 登入 tooZscaler Beta （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="bb8cf-107">You can enable your users tooautomatically get signed-on tooZscaler Beta (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bb8cf-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="bb8cf-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bb8cf-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bb8cf-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="bb8cf-110">Prerequisites</span></span>

<span data-ttu-id="bb8cf-111">tooconfigure Azure AD 與 Zscaler Beta 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="bb8cf-111">tooconfigure Azure AD integration with Zscaler Beta, you need hello following items:</span></span>

- <span data-ttu-id="bb8cf-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="bb8cf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bb8cf-113">已啟用 ZScaler Beta 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="bb8cf-113">A Zscaler Beta single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bb8cf-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bb8cf-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="bb8cf-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bb8cf-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bb8cf-117">如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bb8cf-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="bb8cf-118">Scenario description</span></span>
<span data-ttu-id="bb8cf-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bb8cf-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="bb8cf-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bb8cf-121">從 hello 圖庫加入 Zscaler Beta</span><span class="sxs-lookup"><span data-stu-id="bb8cf-121">Adding Zscaler Beta from hello gallery</span></span>
2. <span data-ttu-id="bb8cf-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="bb8cf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-beta-from-hello-gallery"></a><span data-ttu-id="bb8cf-123">從 hello 圖庫加入 Zscaler Beta</span><span class="sxs-lookup"><span data-stu-id="bb8cf-123">Adding Zscaler Beta from hello gallery</span></span>
<span data-ttu-id="bb8cf-124">tooconfigure hello 整合 Zscaler Beta 到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Zscaler Beta。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-124">tooconfigure hello integration of Zscaler Beta into Azure AD, you need tooadd Zscaler Beta from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bb8cf-125">**tooadd Zscaler Beta 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="bb8cf-125">**tooadd Zscaler Beta from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bb8cf-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bb8cf-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bb8cf-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="bb8cf-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="bb8cf-133">在 [hello] 搜尋方塊中，輸入**Zscaler Beta**。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-133">In hello search box, type **Zscaler Beta**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_search.png)

5. <span data-ttu-id="bb8cf-135">在 hello 結果 窗格中，選取  **Zscaler Beta**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-135">In hello results panel, select **Zscaler Beta**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bb8cf-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="bb8cf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bb8cf-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Zscaler Beta 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-138">In this section, you configure and test Azure AD single sign-on with Zscaler Beta based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bb8cf-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者 Zscaler beta 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zscaler Beta is tooa user in Azure AD.</span></span> <span data-ttu-id="bb8cf-140">換句話說，Azure AD 使用者與 Zscaler Beta 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-140">In other words, a link relationship between an Azure AD user and hello related user in Zscaler Beta needs toobe established.</span></span>

<span data-ttu-id="bb8cf-141">Zscaler Beta 中指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-141">In Zscaler Beta, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="bb8cf-142">tooconfigure 和測試 Azure AD 單一登入 Zscaler beta，您需要遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="bb8cf-142">tooconfigure and test Azure AD single sign-on with Zscaler Beta, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bb8cf-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bb8cf-144">**[設定 proxy 設定](#configuring-proxy-settings)** -tooconfigure hello 在 Internet Explorer proxy 設定</span><span class="sxs-lookup"><span data-stu-id="bb8cf-144">**[Configuring proxy settings](#configuring-proxy-settings)** - tooconfigure hello proxy settings in Internet Explorer</span></span>
3. <span data-ttu-id="bb8cf-145">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="bb8cf-146">**[建立 Zscaler Beta 測試使用者](#creating-a-zscaler-beta-test-user)** -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示法的 Zscaler Beta 中對應項目。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-146">**[Creating a Zscaler Beta test user](#creating-a-zscaler-beta-test-user)** - toohave a counterpart of Britta Simon in Zscaler Beta that is linked toohello Azure AD representation of user.</span></span>
5. <span data-ttu-id="bb8cf-147">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
6. <span data-ttu-id="bb8cf-148">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bb8cf-149">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="bb8cf-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bb8cf-150">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Zscaler Beta 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zscaler Beta application.</span></span>

<span data-ttu-id="bb8cf-151">**tooconfigure Azure AD 單一登入 Zscaler beta，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="bb8cf-151">**tooconfigure Azure AD single sign-on with Zscaler Beta, perform hello following steps:**</span></span>

1. <span data-ttu-id="bb8cf-152">在 Azure 入口網站上 hello hello **Zscaler Beta**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-152">In hello Azure portal, on hello **Zscaler Beta** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="bb8cf-154">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_samlbase.png)

3. <span data-ttu-id="bb8cf-156">在 hello **Zscaler Beta 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="bb8cf-156">On hello **Zscaler Beta Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_url.png)

    <span data-ttu-id="bb8cf-158">在 hello 登入 URL 文字方塊中，輸入您的使用者 」 toosign 上 Zscaler Beta 應用程式 tooyour 用 hello URL。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-158">In hello Sign-on URL textbox, type hello URL used by your users toosign-on tooyour Zscaler Beta application.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bb8cf-159">具有這個值與 hello tooupdate 實際的登入 URL。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-159">You have tooupdate this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="bb8cf-160">請連絡[Zscaler Beta 用戶端支援小組](https://www.zscaler.com/company/contact)tooget 此值。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-160">Contact [Zscaler Beta Client support team](https://www.zscaler.com/company/contact) tooget this value.</span></span> 

4. <span data-ttu-id="bb8cf-161">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_certificate.png) 

5. <span data-ttu-id="bb8cf-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bb8cf-165">在 hello **Zscaler Beta 設定**區段中，按一下**設定 Zscaler Beta** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-165">On hello **Zscaler Beta Configuration** section, click **Configure Zscaler Beta** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="bb8cf-166">複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="bb8cf-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_configure.png) 

7. <span data-ttu-id="bb8cf-168">在不同的網頁瀏覽器視窗中，以登入 tooyour Zscaler Beta 公司網站的系統管理員。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-168">In a different web browser window, log in tooyour Zscaler Beta company site as an administrator.</span></span>

8. <span data-ttu-id="bb8cf-169">在 hello 最上層顯示 hello 功能表上，按一下**管理**。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-169">In hello menu on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="bb8cf-170">![管理](./media/active-directory-saas-zscaler-beta-tutorial/ic800206.png "管理")</span><span class="sxs-lookup"><span data-stu-id="bb8cf-170">![Administration](./media/active-directory-saas-zscaler-beta-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="bb8cf-171">在 [管理系統管理員和角色] 下按一下 [管理使用者和驗證]。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="bb8cf-172">![管理使用者和驗證](./media/active-directory-saas-zscaler-beta-tutorial/ic800207.png "管理使用者和驗證")</span><span class="sxs-lookup"><span data-stu-id="bb8cf-172">![Manage Users & Authentication](./media/active-directory-saas-zscaler-beta-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="bb8cf-173">在 hello**選擇驗證選項，為您的組織**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="bb8cf-173">In hello **Choose Authentication Options for your Organization** section, perform hello following steps:</span></span>   
                
    <span data-ttu-id="bb8cf-174">![驗證](./media/active-directory-saas-zscaler-beta-tutorial/ic800208.png "驗證")</span><span class="sxs-lookup"><span data-stu-id="bb8cf-174">![Authentication](./media/active-directory-saas-zscaler-beta-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="bb8cf-175">a.</span><span class="sxs-lookup"><span data-stu-id="bb8cf-175">a.</span></span> <span data-ttu-id="bb8cf-176">選取 [使用 SAML 單一登入進行驗證] 。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-176">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="bb8cf-177">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-177">b.</span></span> <span data-ttu-id="bb8cf-178">按一下 [設定 SAML 單一登入參數] 。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-178">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="bb8cf-179">在 hello**設定 SAML 單一登入參數**對話方塊頁面上，執行下列步驟，hello，然後按一下**完成**</span><span class="sxs-lookup"><span data-stu-id="bb8cf-179">On hello **Configure SAML Single Sign-On Parameters** dialog page, perform hello following steps, and then click **Done**</span></span>

    <span data-ttu-id="bb8cf-180">![單一登入](./media/active-directory-saas-zscaler-beta-tutorial/ic800209.png "單一登入")</span><span class="sxs-lookup"><span data-stu-id="bb8cf-180">![Single Sign-On](./media/active-directory-saas-zscaler-beta-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="bb8cf-181">a.</span><span class="sxs-lookup"><span data-stu-id="bb8cf-181">a.</span></span> <span data-ttu-id="bb8cf-182">貼上 hello **SAML 單一登入服務 URL**值，您從 hello Azure 入口網站複製到 hello **hello SAML 入口網站 toowhich 使用者的 URL 會傳送驗證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-182">Paste hello **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **URL of hello SAML Portal toowhich users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="bb8cf-183">b.</span><span class="sxs-lookup"><span data-stu-id="bb8cf-183">b.</span></span> <span data-ttu-id="bb8cf-184">在 hello**屬性包含登入名稱**文字方塊中，輸入**NameID**。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-184">In hello **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="bb8cf-185">c.</span><span class="sxs-lookup"><span data-stu-id="bb8cf-185">c.</span></span> <span data-ttu-id="bb8cf-186">tooupload 下載的憑證，按一下  **Zscaler pem**。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-186">tooupload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="bb8cf-187">d.</span><span class="sxs-lookup"><span data-stu-id="bb8cf-187">d.</span></span> <span data-ttu-id="bb8cf-188">選取 [啟用 SAML 自動佈建] 。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-188">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="bb8cf-189">在 hello**設定使用者驗證**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="bb8cf-189">On hello **Configure User Authentication** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="bb8cf-190">![管理](./media/active-directory-saas-zscaler-beta-tutorial/ic800210.png "管理")</span><span class="sxs-lookup"><span data-stu-id="bb8cf-190">![Administration](./media/active-directory-saas-zscaler-beta-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="bb8cf-191">a.</span><span class="sxs-lookup"><span data-stu-id="bb8cf-191">a.</span></span> <span data-ttu-id="bb8cf-192">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-192">Click **Save**.</span></span>

    <span data-ttu-id="bb8cf-193">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-193">b.</span></span> <span data-ttu-id="bb8cf-194">按一下 [立即啟用] 。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-194">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="bb8cf-195">進行 Proxy 設定</span><span class="sxs-lookup"><span data-stu-id="bb8cf-195">Configuring proxy settings</span></span>
### <a name="tooconfigure-hello-proxy-settings-in-internet-explorer"></a><span data-ttu-id="bb8cf-196">在 Internet Explorer tooconfigure hello proxy 設定</span><span class="sxs-lookup"><span data-stu-id="bb8cf-196">tooconfigure hello proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="bb8cf-197">啟動 **Internet Explorer**。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-197">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="bb8cf-198">選取**網際網路選項**從 hello**工具**功能表開啟 hello**網際網路選項**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-198">Select **Internet options** from hello **Tools** menu for open hello **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="bb8cf-199">![網際網路選項](./media/active-directory-saas-zscaler-beta-tutorial/ic769492.png "網際網路選項")</span><span class="sxs-lookup"><span data-stu-id="bb8cf-199">![Internet Options](./media/active-directory-saas-zscaler-beta-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="bb8cf-200">按一下 hello**連線** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-200">Click hello **Connections** tab.</span></span>   
  
     <span data-ttu-id="bb8cf-201">![連線](./media/active-directory-saas-zscaler-beta-tutorial/ic769493.png "連線")</span><span class="sxs-lookup"><span data-stu-id="bb8cf-201">![Connections](./media/active-directory-saas-zscaler-beta-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="bb8cf-202">按一下**LAN 設定**tooopen hello **LAN 設定**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-202">Click **LAN settings** tooopen hello **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="bb8cf-203">在 hello Proxy 伺服器區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="bb8cf-203">In hello Proxy server section, perform hello following steps:</span></span>   
   
    <span data-ttu-id="bb8cf-204">![Proxy 伺服器](./media/active-directory-saas-zscaler-beta-tutorial/ic769494.png "Proxy 伺服器")</span><span class="sxs-lookup"><span data-stu-id="bb8cf-204">![Proxy server](./media/active-directory-saas-zscaler-beta-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="bb8cf-205">a.</span><span class="sxs-lookup"><span data-stu-id="bb8cf-205">a.</span></span> <span data-ttu-id="bb8cf-206">選取 [在您的區域網路使用 Proxy 伺服器]。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-206">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="bb8cf-207">b.</span><span class="sxs-lookup"><span data-stu-id="bb8cf-207">b.</span></span> <span data-ttu-id="bb8cf-208">在 [hello 位址] 文字方塊中輸入**gateway.zscalerbeta.net**。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-208">In hello Address textbox, type **gateway.zscalerbeta.net**.</span></span>

    <span data-ttu-id="bb8cf-209">c.</span><span class="sxs-lookup"><span data-stu-id="bb8cf-209">c.</span></span> <span data-ttu-id="bb8cf-210">在 [hello 連接埠] 文字方塊中，輸入**80**。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-210">In hello Port textbox, type **80**.</span></span>

    <span data-ttu-id="bb8cf-211">d.</span><span class="sxs-lookup"><span data-stu-id="bb8cf-211">d.</span></span> <span data-ttu-id="bb8cf-212">選取 [近端網址不使用 Proxy 伺服器] 。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-212">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="bb8cf-213">e.</span><span class="sxs-lookup"><span data-stu-id="bb8cf-213">e.</span></span> <span data-ttu-id="bb8cf-214">按一下**確定**tooclose hello**區域網路 (LAN) 設定**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-214">Click **OK** tooclose hello **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="bb8cf-215">按一下**確定**tooclose hello**網際網路選項**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-215">Click **OK** tooclose hello **Internet Options** dialog.</span></span>

> [!TIP]
> <span data-ttu-id="bb8cf-216">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="bb8cf-216">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bb8cf-217">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-217">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bb8cf-218">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bb8cf-218">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bb8cf-219">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="bb8cf-219">Creating an Azure AD test user</span></span>
<span data-ttu-id="bb8cf-220">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-220">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="bb8cf-222">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="bb8cf-222">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bb8cf-223">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-223">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscaler-beta-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bb8cf-225">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-225">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscaler-beta-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bb8cf-227">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-227">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscaler-beta-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bb8cf-229">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="bb8cf-229">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscaler-beta-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bb8cf-231">a.</span><span class="sxs-lookup"><span data-stu-id="bb8cf-231">a.</span></span> <span data-ttu-id="bb8cf-232">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-232">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bb8cf-233">b.</span><span class="sxs-lookup"><span data-stu-id="bb8cf-233">b.</span></span> <span data-ttu-id="bb8cf-234">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-234">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bb8cf-235">c.</span><span class="sxs-lookup"><span data-stu-id="bb8cf-235">c.</span></span> <span data-ttu-id="bb8cf-236">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-236">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bb8cf-237">d.</span><span class="sxs-lookup"><span data-stu-id="bb8cf-237">d.</span></span> <span data-ttu-id="bb8cf-238">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-238">Click **Create**.</span></span>
 
### <a name="creating-a-zscaler-beta-test-user"></a><span data-ttu-id="bb8cf-239">建立 Zscaler Beta 測試使用者</span><span class="sxs-lookup"><span data-stu-id="bb8cf-239">Creating a Zscaler Beta test user</span></span>

<span data-ttu-id="bb8cf-240">tooenable Azure AD 使用者 toolog 中 tooZscaler Beta，它們必須已佈建的 tooZscaler Beta。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-240">tooenable Azure AD users toolog in tooZscaler Beta, they must be provisioned tooZscaler Beta.</span></span> <span data-ttu-id="bb8cf-241">在 Zscaler beta 版的 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-241">In hello case of Zscaler Beta, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="bb8cf-242">tooconfigure 使用者佈建，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="bb8cf-242">tooconfigure user provisioning, perform hello following steps:</span></span>

1. <span data-ttu-id="bb8cf-243">登入 tooyour **Zscaler Beta**租用戶。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-243">Log in tooyour **Zscaler Beta** tenant.</span></span>

2. <span data-ttu-id="bb8cf-244">按一下 [系統管理] 。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-244">Click **Administration**.</span></span>   
   
    <span data-ttu-id="bb8cf-245">![管理](./media/active-directory-saas-zscaler-beta-tutorial/ic781035.png "管理")</span><span class="sxs-lookup"><span data-stu-id="bb8cf-245">![Administration](./media/active-directory-saas-zscaler-beta-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="bb8cf-246">按一下 [使用者管理] 。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-246">Click **User Management**.</span></span>   
        
     <span data-ttu-id="bb8cf-247">![新增](./media/active-directory-saas-zscaler-beta-tutorial/ic781036.png "新增")</span><span class="sxs-lookup"><span data-stu-id="bb8cf-247">![Add](./media/active-directory-saas-zscaler-beta-tutorial/ic781036.png "Add")</span></span>

4. <span data-ttu-id="bb8cf-248">在 hello**使用者**索引標籤上，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-248">In hello **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="bb8cf-249">![新增](./media/active-directory-saas-zscaler-beta-tutorial/ic781037.png "新增")</span><span class="sxs-lookup"><span data-stu-id="bb8cf-249">![Add](./media/active-directory-saas-zscaler-beta-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="bb8cf-250">在 hello 新增使用者 區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="bb8cf-250">In hello Add User section, perform hello following steps:</span></span>
        
    <span data-ttu-id="bb8cf-251">![新增使用者](./media/active-directory-saas-zscaler-beta-tutorial/ic781038.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="bb8cf-251">![Add User](./media/active-directory-saas-zscaler-beta-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="bb8cf-252">a.</span><span class="sxs-lookup"><span data-stu-id="bb8cf-252">a.</span></span> <span data-ttu-id="bb8cf-253">型別 hello **UserID**，**使用者顯示名稱**，**密碼**，**確認密碼**，然後選取**群組**和 hello**部門**的有效 azure 想 tooprovision AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-253">Type hello **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and hello **Department** of a valid Azure AD account you want tooprovision.</span></span>

    <span data-ttu-id="bb8cf-254">b.</span><span class="sxs-lookup"><span data-stu-id="bb8cf-254">b.</span></span> <span data-ttu-id="bb8cf-255">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-255">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="bb8cf-256">您可以使用任何其他 Zscaler Beta 使用者帳戶建立工具或 Api 提供 Zscaler Beta tooprovision Azure AD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-256">You can use any other Zscaler Beta user account creation tools or APIs provided by Zscaler Beta tooprovision Azure AD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bb8cf-257">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="bb8cf-257">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bb8cf-258">在本節中，以啟用許 Simon toouse Azure 單一登入授與存取 tooZscaler Beta。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-258">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZscaler Beta.</span></span>

![指派使用者][200] 

<span data-ttu-id="bb8cf-260">**tooassign 許 Simon tooZscaler Beta，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="bb8cf-260">**tooassign Britta Simon tooZscaler Beta, perform hello following steps:**</span></span>

1. <span data-ttu-id="bb8cf-261">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-261">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="bb8cf-263">在 [hello] 應用程式清單中，選取**Zscaler Beta**。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-263">In hello applications list, select **Zscaler Beta**.</span></span>

    ![設定單一登入](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_app.png) 

3. <span data-ttu-id="bb8cf-265">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-265">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="bb8cf-267">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-267">Click **Add** button.</span></span> <span data-ttu-id="bb8cf-268">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="bb8cf-270">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-270">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bb8cf-271">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bb8cf-272">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bb8cf-273">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="bb8cf-273">Testing single sign-on</span></span>

<span data-ttu-id="bb8cf-274">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-274">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bb8cf-275">當您按一下的 hello Zscaler Beta 磚 hello 存取面板中時，您應該取得自動登入 tooyour Zscaler Beta 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-275">When you click hello Zscaler Beta tile in hello Access Panel, you should get automatically signed-on tooyour Zscaler Beta application.</span></span>
<span data-ttu-id="bb8cf-276">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="bb8cf-276">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bb8cf-277">其他資源</span><span class="sxs-lookup"><span data-stu-id="bb8cf-277">Additional resources</span></span>

* [<span data-ttu-id="bb8cf-278">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bb8cf-278">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bb8cf-279">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="bb8cf-279">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_203.png

