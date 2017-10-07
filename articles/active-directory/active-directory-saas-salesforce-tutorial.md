---
title: "教學課程：Azure Active Directory 與 Salesforce 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Salesforce 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2d7d420-dc91-41b8-a6b3-59579e043b35
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 1d848518ee30910e051cdc4746c599219f3b5a3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce"></a><span data-ttu-id="fb0f5-103">教學課程：Azure Active Directory 與 Salesforce 整合</span><span class="sxs-lookup"><span data-stu-id="fb0f5-103">Tutorial: Azure Active Directory integration with Salesforce</span></span>

<span data-ttu-id="fb0f5-104">在此教學課程中，您學會如何 toointegrate Salesforce 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-104">In this tutorial, you learn how toointegrate Salesforce with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fb0f5-105">Azure AD 與 Salesforce 整合為您提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="fb0f5-105">Integrating Salesforce with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fb0f5-106">您可以控制存取 tooSalesforce Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="fb0f5-106">You can control in Azure AD who has access tooSalesforce</span></span>
- <span data-ttu-id="fb0f5-107">您可以啟用您的使用者 tooautomatically get 登入 tooSalesforce （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="fb0f5-107">You can enable your users tooautomatically get signed-on tooSalesforce (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fb0f5-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="fb0f5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="fb0f5-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fb0f5-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="fb0f5-110">Prerequisites</span></span>

<span data-ttu-id="fb0f5-111">tooconfigure Azure AD 與 Salesforce 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="fb0f5-111">tooconfigure Azure AD integration with Salesforce, you need hello following items:</span></span>

- <span data-ttu-id="fb0f5-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="fb0f5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fb0f5-113">啟用 Salesforce 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="fb0f5-113">A Salesforce single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fb0f5-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fb0f5-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="fb0f5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fb0f5-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fb0f5-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fb0f5-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="fb0f5-118">Scenario description</span></span>
<span data-ttu-id="fb0f5-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fb0f5-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="fb0f5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fb0f5-121">從 hello 圖庫加入 Salesforce</span><span class="sxs-lookup"><span data-stu-id="fb0f5-121">Adding Salesforce from hello gallery</span></span>
2. <span data-ttu-id="fb0f5-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="fb0f5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-from-hello-gallery"></a><span data-ttu-id="fb0f5-123">從 hello 圖庫加入 Salesforce</span><span class="sxs-lookup"><span data-stu-id="fb0f5-123">Adding Salesforce from hello gallery</span></span>
<span data-ttu-id="fb0f5-124">tooconfigure hello 整合 Salesforce 到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Salesforce。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-124">tooconfigure hello integration of Salesforce into Azure AD, you need tooadd Salesforce from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fb0f5-125">**tooadd Salesforce hello 圖庫中，從執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="fb0f5-125">**tooadd Salesforce from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fb0f5-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fb0f5-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fb0f5-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="fb0f5-131">按一下**新的應用程式**上 hello hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="fb0f5-133">在 [hello] 搜尋方塊中，輸入**Salesforce**。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-133">In hello search box, type **Salesforce**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_search.png)

5. <span data-ttu-id="fb0f5-135">在 hello 結果 窗格中，選取  **Salesforce**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-135">In hello results panel, select **Salesforce**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fb0f5-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="fb0f5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fb0f5-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Salesforce 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-138">In this section, you configure and test Azure AD single sign-on with Salesforce based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="fb0f5-139">單一登入 toowork，Azure AD 需要 tooknow hello 對應項目在 Salesforce 中的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Salesforce is tooa user in Azure AD.</span></span> <span data-ttu-id="fb0f5-140">換句話說，Azure AD 使用者與在 Salesforce 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-140">In other words, a link relationship between an Azure AD user and hello related user in Salesforce needs toobe established.</span></span>

<span data-ttu-id="fb0f5-141">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username**在 Salesforce 中。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Salesforce.</span></span>

<span data-ttu-id="fb0f5-142">tooconfigure 及 Azure AD 單一登入與 Salesforce 的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="fb0f5-142">tooconfigure and test Azure AD single sign-on with Salesforce, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fb0f5-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fb0f5-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fb0f5-145">**[建立 Salesforce 測試使用者](#creating-a-salesforce-test-user)** -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示法的 Salesforce 中的對應項目。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-145">**[Creating a Salesforce test user](#creating-a-salesforce-test-user)** - toohave a counterpart of Britta Simon in Salesforce that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fb0f5-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fb0f5-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fb0f5-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="fb0f5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fb0f5-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Salesforce 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Salesforce application.</span></span>

<span data-ttu-id="fb0f5-150">**tooconfigure Azure AD 單一登入與 Salesforce，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="fb0f5-150">**tooconfigure Azure AD single sign-on with Salesforce, perform hello following steps:**</span></span>

1. <span data-ttu-id="fb0f5-151">在 Azure 入口網站上 hello hello **Salesforce**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-151">In hello Azure portal, on hello **Salesforce** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="fb0f5-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_samlbase.png)

3. <span data-ttu-id="fb0f5-155">在 hello **Salesforce 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="fb0f5-155">On hello **Salesforce Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_url.png)

    <span data-ttu-id="fb0f5-157">在 hello**登入 URL**文字方塊中，使用下列模式的 hello 類型 hello 值：</span><span class="sxs-lookup"><span data-stu-id="fb0f5-157">In hello **Sign-on URL** textbox, type hello value using hello following pattern:</span></span> 
   * <span data-ttu-id="fb0f5-158">企業帳戶： `https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="fb0f5-158">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>
   * <span data-ttu-id="fb0f5-159">開發人員帳戶： `https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="fb0f5-159">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fb0f5-160">這些值不是真正的 hello。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-160">These values are not hello real.</span></span> <span data-ttu-id="fb0f5-161">更新這些值與 hello 實際登入 URL。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-161">Update these values with hello actual Sign-on URL.</span></span> <span data-ttu-id="fb0f5-162">請連絡[Salesforce 用戶端支援小組](https://help.salesforce.com/support)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-162">Contact [Salesforce Client support team](https://help.salesforce.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="fb0f5-163">在 hello **SAML 簽章憑證**區段中，按一下**憑證**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-163">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_certificate.png) 

5. <span data-ttu-id="fb0f5-165">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-165">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-salesforce-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fb0f5-167">在 hello **Salesforce 組態**區段中，按一下**設定 Salesforce** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-167">On hello **Salesforce Configuration** section, click **Configure Salesforce** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="fb0f5-168">複製 hello **SAML 實體識別碼和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="fb0f5-168">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span> 

    <span data-ttu-id="fb0f5-169">![設定單一登入](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="fb0f5-169">![Configure Single Sign-On](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS></span></span>
7.  <span data-ttu-id="fb0f5-170">在您的瀏覽器中開啟新索引標籤，並登入 tooyour Salesforce 系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-170">Open a new tab in your browser and log in tooyour Salesforce administrator account.</span></span>

8.  <span data-ttu-id="fb0f5-171">在 hello**管理員**瀏覽窗格中，按一下**安全性控制**tooexpand hello 相關區段。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-171">Under hello **Administrator** navigation pane, click **Security Controls** tooexpand hello related section.</span></span> <span data-ttu-id="fb0f5-172">然後按一下 [單一登入設定]。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-172">Then click **Single Sign-On Settings**.</span></span>

    ![設定單一登入](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso.png)

9.  <span data-ttu-id="fb0f5-174">在 [hello**單一登入設定**頁面上，按一下 hello**編輯**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-174">On hello **Single Sign-On Settings** page, click hello **Edit** button.</span></span>
    <span data-ttu-id="fb0f5-175">![設定單一登入](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)</span><span class="sxs-lookup"><span data-stu-id="fb0f5-175">![Configure Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)</span></span>

      > [!NOTE]
      > <span data-ttu-id="fb0f5-176">如果您的 Salesforce 帳戶無法 tooenable 單一登入設定，您可能需要 toocontact [Salesforce 用戶端支援小組](https://help.salesforce.com/support)。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-176">If you are unable tooenable Single Sign-On settings for your Salesforce account, you may need toocontact [Salesforce Client support team](https://help.salesforce.com/support).</span></span> 

10. <span data-ttu-id="fb0f5-177">選取 啟用 SAML，然後按一下儲存。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-177">Select **SAML Enabled**, and then click **Save**.</span></span>

      ![設定單一登入](./media/active-directory-saas-salesforce-tutorial/sf-enable-saml.png)
11. <span data-ttu-id="fb0f5-179">SAML 單一登入設定，按一下 tooconfigure**新增**。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-179">tooconfigure your SAML single sign-on settings, click **New**.</span></span>

    ![設定單一登入](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-new.png)

12. <span data-ttu-id="fb0f5-181">在 hello **SAML 單一登入設定編輯**頁面上，進行下列設定的 hello:</span><span class="sxs-lookup"><span data-stu-id="fb0f5-181">On hello **SAML Single Sign-On Setting Edit** page, make hello following configurations:</span></span>

    ![設定單一登入](./media/active-directory-saas-salesforce-tutorial/sf-saml-config.png)

    <span data-ttu-id="fb0f5-183">a.</span><span class="sxs-lookup"><span data-stu-id="fb0f5-183">a.</span></span> <span data-ttu-id="fb0f5-184">Hello**名稱**欄位中，輸入易記的名稱，此組態中。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-184">For hello **Name** field, type in a friendly name for this configuration.</span></span> <span data-ttu-id="fb0f5-185">提供值**名稱**自動填入 hello **API 名稱**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-185">Providing a value for **Name** automatically populate hello **API Name** textbox.</span></span>

    <span data-ttu-id="fb0f5-186">b.</span><span class="sxs-lookup"><span data-stu-id="fb0f5-186">b.</span></span> <span data-ttu-id="fb0f5-187">貼上**SMAL 實體識別碼**值傳入 hello**簽發者**在 Salesforce 中的欄位。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-187">Paste **SMAL Entity ID** value into hello **Issuer** field in Salesforce.</span></span>

    <span data-ttu-id="fb0f5-188">c.</span><span class="sxs-lookup"><span data-stu-id="fb0f5-188">c.</span></span> <span data-ttu-id="fb0f5-189">在 [hello**實體識別碼] 文字方塊**，輸入您的 Salesforce 網域名稱使用下列模式的 hello:</span><span class="sxs-lookup"><span data-stu-id="fb0f5-189">In hello **Entity Id textbox**, type your Salesforce domain name using hello following pattern:</span></span>
      
      * <span data-ttu-id="fb0f5-190">企業帳戶： `https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="fb0f5-190">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>
      * <span data-ttu-id="fb0f5-191">開發人員帳戶： `https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="fb0f5-191">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>
      
    <span data-ttu-id="fb0f5-192">d.</span><span class="sxs-lookup"><span data-stu-id="fb0f5-192">d.</span></span> <span data-ttu-id="fb0f5-193">按一下**瀏覽**或**選擇檔案**tooopen hello**選擇檔案 tooUpload**  對話方塊中，選取您的 Salesforce 憑證，然後按一下**開啟**tooupload hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-193">Click **Browse** or **Choose File** tooopen hello **Choose File tooUpload** dialog, select your Salesforce certificate, and then click **Open** tooupload hello certificate.</span></span>

    <span data-ttu-id="fb0f5-194">e.</span><span class="sxs-lookup"><span data-stu-id="fb0f5-194">e.</span></span> <span data-ttu-id="fb0f5-195">對於 [SAML 身分識別類型]，請選取 [判斷提示包含使用者的 salesforce.com 使用者名稱]。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-195">For **SAML Identity Type**, select **Assertion contains User's salesforce.com username**.</span></span>

    <span data-ttu-id="fb0f5-196">f.</span><span class="sxs-lookup"><span data-stu-id="fb0f5-196">f.</span></span> <span data-ttu-id="fb0f5-197">如**SAML 識別位置**，選取**識別是 hello 的 hello Subject 陳述式的 NameIdentifier 元素中**</span><span class="sxs-lookup"><span data-stu-id="fb0f5-197">For **SAML Identity Location**, select **Identity is in hello NameIdentifier element of hello Subject statement**</span></span>

    <span data-ttu-id="fb0f5-198">g.</span><span class="sxs-lookup"><span data-stu-id="fb0f5-198">g.</span></span> <span data-ttu-id="fb0f5-199">貼上**單一登入服務 URL**到 hello**身分識別提供者登入 URL**在 Salesforce 中的欄位。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-199">Paste **Single Sign-On Service URL** into hello **Identity Provider Login URL** field in Salesforce.</span></span>
    
    <span data-ttu-id="fb0f5-200">h.</span><span class="sxs-lookup"><span data-stu-id="fb0f5-200">h.</span></span> <span data-ttu-id="fb0f5-201">對於 [服務提供者起始的要求繫結]，請選取 [HTTP 重新導向]。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-201">For **Service Provider Initiated Request Binding**, select **HTTP Redirect**.</span></span>
    
    <span data-ttu-id="fb0f5-202">i.</span><span class="sxs-lookup"><span data-stu-id="fb0f5-202">i.</span></span> <span data-ttu-id="fb0f5-203">最後，按一下 **儲存**tooapply SAML 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-203">Finally, click **Save** tooapply your SAML single sign-on settings.</span></span>

13. <span data-ttu-id="fb0f5-204">在 Salesforce 中的 hello 左瀏覽窗格，按一下 **定義域管理**tooexpand hello 相關的區段，然後按一下**我的網域**。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-204">On hello left navigation pane in Salesforce, click **Domain Management** tooexpand hello related section, and then click **My Domain**.</span></span>

    ![設定單一登入](./media/active-directory-saas-salesforce-tutorial/sf-my-domain.png)

14. <span data-ttu-id="fb0f5-206">捲動 toohello**驗證組態**區段，然後按一下 [hello**編輯**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-206">Scroll down toohello **Authentication Configuration** section, and click hello **Edit** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-salesforce-tutorial/sf-edit-auth-config.png)

15. <span data-ttu-id="fb0f5-208">在 hello**驗證服務**區段中，選取 SAML SSO 組態的 hello 易記名稱，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-208">In hello **Authentication Service** section, select hello friendly name of your SAML SSO configuration, and then click **Save**.</span></span>

    ![設定單一登入](./media/active-directory-saas-salesforce-tutorial/sf-auth-config.png)

    > [!NOTE]
    > <span data-ttu-id="fb0f5-210">如果選取一個以上的驗證服務，則使用者會喜歡哪一種驗證服務的提示的 tooselect toosign 中與在起始單一登入 tooyour Salesforce 環境。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-210">If more than one authentication service is selected, users are prompted tooselect which authentication service they like toosign in with while initiating single sign-on tooyour Salesforce environment.</span></span> <span data-ttu-id="fb0f5-211">如果您不要 toohappen，則您應該**核取所有其他驗證服務**。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-211">If you don’t want it toohappen, then you should **leave all other authentication services unchecked**.</span></span>
<CE>    
> [!TIP]
> <span data-ttu-id="fb0f5-212">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="fb0f5-212">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fb0f5-213">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-213">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fb0f5-214">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fb0f5-214">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fb0f5-215">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="fb0f5-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="fb0f5-216">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-216">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="fb0f5-218">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="fb0f5-218">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fb0f5-219">Hello 左瀏覽窗格中 hello **Azure 入口網站**，按一下  **Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-219">On hello left navigation pane in hello **Azure portal**, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforce-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fb0f5-221">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-221">toodisplay hello list of users, Go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforce-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fb0f5-223">在 hello hello 對話方塊頂端，按一下**新增**tooopen hello**使用者**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-223">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforce-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fb0f5-225">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="fb0f5-225">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforce-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fb0f5-227">a.</span><span class="sxs-lookup"><span data-stu-id="fb0f5-227">a.</span></span> <span data-ttu-id="fb0f5-228">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-228">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fb0f5-229">b.</span><span class="sxs-lookup"><span data-stu-id="fb0f5-229">b.</span></span> <span data-ttu-id="fb0f5-230">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-230">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fb0f5-231">c.</span><span class="sxs-lookup"><span data-stu-id="fb0f5-231">c.</span></span> <span data-ttu-id="fb0f5-232">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-232">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="fb0f5-233">d.</span><span class="sxs-lookup"><span data-stu-id="fb0f5-233">d.</span></span> <span data-ttu-id="fb0f5-234">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-234">Click **Create**.</span></span>
 
### <a name="creating-a-salesforce-test-user"></a><span data-ttu-id="fb0f5-235">建立 Salesforce 測試使用者</span><span class="sxs-lookup"><span data-stu-id="fb0f5-235">Creating a Salesforce test user</span></span>

<span data-ttu-id="fb0f5-236">本節會在 Salesforce 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-236">In this section, a user called Britta Simon is created in Salesforce.</span></span> <span data-ttu-id="fb0f5-237">Salesforce 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-237">Salesforce supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="fb0f5-238">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-238">There is no action item for you in this section.</span></span> <span data-ttu-id="fb0f5-239">如果使用者不在 Salesforce 中，當您嘗試 tooaccess Salesforce 時，會建立一個新。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-239">If a user doesn't already exist in Salesforce, a new one is created when you attempt tooaccess Salesforce.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="fb0f5-240">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="fb0f5-240">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="fb0f5-241">在本節中，您可以授與存取 tooSalesforce 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-241">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSalesforce.</span></span>

![指派使用者][200] 

<span data-ttu-id="fb0f5-243">**tooassign 許 Simon tooSalesforce，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="fb0f5-243">**tooassign Britta Simon tooSalesforce, perform hello following steps:**</span></span>

1. <span data-ttu-id="fb0f5-244">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-244">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="fb0f5-246">在 [hello] 應用程式清單中，選取**Salesforce**。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-246">In hello applications list, select **Salesforce**.</span></span>

    ![設定單一登入](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_app.png) 

3. <span data-ttu-id="fb0f5-248">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-248">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="fb0f5-250">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-250">Click **Add** button.</span></span> <span data-ttu-id="fb0f5-251">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="fb0f5-253">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-253">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fb0f5-254">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fb0f5-255">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fb0f5-256">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="fb0f5-256">Testing single sign-on</span></span>

<span data-ttu-id="fb0f5-257">您的單一登入設定，開啟 hello 存取面板的 tootest [https://myapps.microsoft.com](https://myapps.microsoft.com/)，然後登入 hello 測試帳戶，然後按一下**Salesforce**。</span><span class="sxs-lookup"><span data-stu-id="fb0f5-257">tootest your single sign-on settings, open hello Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), then sign into hello test account, and click **Salesforce**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fb0f5-258">其他資源</span><span class="sxs-lookup"><span data-stu-id="fb0f5-258">Additional resources</span></span>

* [<span data-ttu-id="fb0f5-259">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fb0f5-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fb0f5-260">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="fb0f5-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="fb0f5-261">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="fb0f5-261">Configure User Provisioning</span></span>](active-directory-saas-salesforce-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_203.png

