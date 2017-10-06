---
title: "教學課程：Azure Active Directory 與 Egnyte 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Egnyte 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8c2101d4-1779-4b36-8464-5c1ff780da18
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: d86fa28a1e7b23474cb76c08aef8539acadaf24d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-egnyte"></a><span data-ttu-id="5b458-103">教學課程：Azure Active Directory 與 Egnyte 整合</span><span class="sxs-lookup"><span data-stu-id="5b458-103">Tutorial: Azure Active Directory integration with Egnyte</span></span>

<span data-ttu-id="5b458-104">在此教學課程中，您學會如何 toointegrate Egnyte 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="5b458-104">In this tutorial, you learn how toointegrate Egnyte with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5b458-105">與 Azure AD 整合 Egnyte 可以提供下列優點的 hello:</span><span class="sxs-lookup"><span data-stu-id="5b458-105">Integrating Egnyte with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5b458-106">您可以控制存取 tooEgnyte Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="5b458-106">You can control in Azure AD who has access tooEgnyte</span></span>
- <span data-ttu-id="5b458-107">您可以啟用您的使用者 tooautomatically get 登入 tooEgnyte （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="5b458-107">You can enable your users tooautomatically get signed-on tooEgnyte (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5b458-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="5b458-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5b458-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="5b458-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b458-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="5b458-110">Prerequisites</span></span>

<span data-ttu-id="5b458-111">tooconfigure 與 Egnyte 的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="5b458-111">tooconfigure Azure AD integration with Egnyte, you need hello following items:</span></span>

- <span data-ttu-id="5b458-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="5b458-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5b458-113">已啟用 Egnyte 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="5b458-113">An Egnyte single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5b458-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="5b458-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5b458-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="5b458-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5b458-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="5b458-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5b458-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="5b458-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5b458-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="5b458-118">Scenario description</span></span>
<span data-ttu-id="5b458-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5b458-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5b458-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="5b458-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5b458-121">從 hello 圖庫加入 Egnyte</span><span class="sxs-lookup"><span data-stu-id="5b458-121">Adding Egnyte from hello gallery</span></span>
2. <span data-ttu-id="5b458-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5b458-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-egnyte-from-hello-gallery"></a><span data-ttu-id="5b458-123">從 hello 圖庫加入 Egnyte</span><span class="sxs-lookup"><span data-stu-id="5b458-123">Adding Egnyte from hello gallery</span></span>
<span data-ttu-id="5b458-124">tooconfigure hello 整合 Egnyte 的 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Egnyte。</span><span class="sxs-lookup"><span data-stu-id="5b458-124">tooconfigure hello integration of Egnyte into Azure AD, you need tooadd Egnyte from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5b458-125">**tooadd Egnyte 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="5b458-125">**tooadd Egnyte from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b458-126">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="5b458-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5b458-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="5b458-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5b458-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="5b458-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="5b458-131">tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="5b458-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="5b458-133">在 [hello] 搜尋方塊中，輸入**Egnyte**。</span><span class="sxs-lookup"><span data-stu-id="5b458-133">In hello search box, type **Egnyte**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_search.png)

5. <span data-ttu-id="5b458-135">在 [hello [結果] 窗格中，選取 [ **Egnyte**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5b458-135">In hello results panel, select **Egnyte**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5b458-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5b458-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5b458-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Egnyte 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5b458-138">In this section, you configure and test Azure AD single sign-on with Egnyte based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5b458-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 Egnyte 中是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="5b458-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Egnyte is tooa user in Azure AD.</span></span> <span data-ttu-id="5b458-140">換句話說，Azure AD 使用者與 hello Egnyte 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="5b458-140">In other words, a link relationship between an Azure AD user and hello related user in Egnyte needs toobe established.</span></span>

<span data-ttu-id="5b458-141">在 Egnyte 中，將指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="5b458-141">In Egnyte, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5b458-142">tooconfigure 及測試 Azure AD 單一登入 Egnyte，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="5b458-142">tooconfigure and test Azure AD single sign-on with Egnyte, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5b458-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="5b458-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5b458-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="5b458-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5b458-145">**[建立測試使用者 Egnyte](#creating-an-egnyte-test-user) ** -toohave 許 Simon Egnyte 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="5b458-145">**[Creating an Egnyte test user](#creating-an-egnyte-test-user)** - toohave a counterpart of Britta Simon in Egnyte that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5b458-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5b458-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5b458-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="5b458-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5b458-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5b458-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5b458-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Egnyte 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="5b458-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Egnyte application.</span></span>

<span data-ttu-id="5b458-150">**tooconfigure Azure AD 單一登入 Egnyte，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="5b458-150">**tooconfigure Azure AD single sign-on with Egnyte, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b458-151">在 Azure 入口網站上 hello hello **Egnyte**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="5b458-151">In hello Azure portal, on hello **Egnyte** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="5b458-153">在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5b458-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_samlbase.png)

3. <span data-ttu-id="5b458-155">在 [hello **Egnyte 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="5b458-155">On hello **Egnyte Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_url.png)

    <span data-ttu-id="5b458-157">在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.egnyte.com`</span><span class="sxs-lookup"><span data-stu-id="5b458-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.egnyte.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5b458-158">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="5b458-158">This value is not real.</span></span> <span data-ttu-id="5b458-159">更新此值以 hello 實際的登入 URL。</span><span class="sxs-lookup"><span data-stu-id="5b458-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="5b458-160">請連絡[Egnyte 用戶端支援小組](https://www.egnyte.com/corp/contact_egnyte.html)tooget 此值。</span><span class="sxs-lookup"><span data-stu-id="5b458-160">Contact [Egnyte Client support team](https://www.egnyte.com/corp/contact_egnyte.html) tooget this value.</span></span> 
 
4. <span data-ttu-id="5b458-161">在 [hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="5b458-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_certificate.png) 

5. <span data-ttu-id="5b458-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="5b458-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-egnyte-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5b458-165">在 [hello **Egnyte 設定**區段中，按一下**設定 Egnyte** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="5b458-165">On hello **Egnyte Configuration** section, click **Configure Egnyte** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5b458-166">複製 hello **SAML 實體識別碼和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="5b458-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_configure.png) 

7. <span data-ttu-id="5b458-168">在不同的網頁瀏覽器視窗中，系統管理員身分登入 tooyour Egnyte 公司網站。</span><span class="sxs-lookup"><span data-stu-id="5b458-168">In a different web browser window, log in tooyour Egnyte company site as an administrator.</span></span>

8. <span data-ttu-id="5b458-169">按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="5b458-169">Click **Settings**.</span></span>
   
   <span data-ttu-id="5b458-170">![設定](./media/active-directory-saas-egnyte-tutorial/ic787819.png "設定")</span><span class="sxs-lookup"><span data-stu-id="5b458-170">![Settings](./media/active-directory-saas-egnyte-tutorial/ic787819.png "Settings")</span></span>

9. <span data-ttu-id="5b458-171">在 [hello] 功能表中，按一下 [**設定**。</span><span class="sxs-lookup"><span data-stu-id="5b458-171">In hello menu, click **Settings**.</span></span>

   <span data-ttu-id="5b458-172">![設定](./media/active-directory-saas-egnyte-tutorial/ic787820.png "設定")</span><span class="sxs-lookup"><span data-stu-id="5b458-172">![Settings](./media/active-directory-saas-egnyte-tutorial/ic787820.png "Settings")</span></span>

10. <span data-ttu-id="5b458-173">按一下 hello**組態**索引標籤，然後再按一下**安全性**。</span><span class="sxs-lookup"><span data-stu-id="5b458-173">Click hello **Configuration** tab, and then click **Security**.</span></span>

    <span data-ttu-id="5b458-174">![安全性](./media/active-directory-saas-egnyte-tutorial/ic787821.png "安全性")</span><span class="sxs-lookup"><span data-stu-id="5b458-174">![Security](./media/active-directory-saas-egnyte-tutorial/ic787821.png "Security")</span></span>

11. <span data-ttu-id="5b458-175">在 [hello**單一登入驗證**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="5b458-175">In hello **Single Sign-On Authentication** section, perform hello following steps:</span></span>

    <span data-ttu-id="5b458-176">![單一登入驗證](./media/active-directory-saas-egnyte-tutorial/ic787822.png "單一登入驗證")</span><span class="sxs-lookup"><span data-stu-id="5b458-176">![Single Sign On Authentication](./media/active-directory-saas-egnyte-tutorial/ic787822.png "Single Sign On Authentication")</span></span>   
    
    <span data-ttu-id="5b458-177">a.</span><span class="sxs-lookup"><span data-stu-id="5b458-177">a.</span></span> <span data-ttu-id="5b458-178">針對 [單一登入驗證]，選取 **SAML 2.0**。</span><span class="sxs-lookup"><span data-stu-id="5b458-178">As **Single sign-on authentication**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="5b458-179">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="5b458-179">b.</span></span> <span data-ttu-id="5b458-180">針對 [識別提供者]，選取 [AzureAD]。</span><span class="sxs-lookup"><span data-stu-id="5b458-180">As **Identity provider**, select **AzureAD**.</span></span>
   
    <span data-ttu-id="5b458-181">c.</span><span class="sxs-lookup"><span data-stu-id="5b458-181">c.</span></span> <span data-ttu-id="5b458-182">貼上**SAML 單一登入服務 URL**從 Azure 入口網站複製到 hello**身分識別提供者登入 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="5b458-182">Paste **SAML Single Sign-On Service URL** copied from Azure portal into hello **Identity provider login URL** textbox.</span></span>
   
    <span data-ttu-id="5b458-183">d.</span><span class="sxs-lookup"><span data-stu-id="5b458-183">d.</span></span> <span data-ttu-id="5b458-184">貼上**SAML 實體識別碼**其中您從 Azure 入口網站複製到 hello**身分識別提供者的實體識別碼**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="5b458-184">Paste **SAML Entity ID** which you have copied from Azure portal into hello **Identity provider entity ID** textbox.</span></span>
      
    <span data-ttu-id="5b458-185">e.</span><span class="sxs-lookup"><span data-stu-id="5b458-185">e.</span></span> <span data-ttu-id="5b458-186">從 Azure 入口網站中，複製到剪貼簿，其內容的 hello 下載 [記事本] 中開啟 base-64 編碼的憑證，然後將它貼入 toohello**身分識別提供者憑證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="5b458-186">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **Identity provider certificate** textbox.</span></span>
   
    <span data-ttu-id="5b458-187">f.</span><span class="sxs-lookup"><span data-stu-id="5b458-187">f.</span></span> <span data-ttu-id="5b458-188">針對 [預設使用者對應]，選取 [電子郵件地址]。</span><span class="sxs-lookup"><span data-stu-id="5b458-188">As **Default user mapping**, select **Email address**.</span></span>
   
    <span data-ttu-id="5b458-189">g.</span><span class="sxs-lookup"><span data-stu-id="5b458-189">g.</span></span> <span data-ttu-id="5b458-190">針對 [使用網域指定的簽發者值]，選取 [停用]。</span><span class="sxs-lookup"><span data-stu-id="5b458-190">As **Use domain-specific issuer value**, select **disabled**.</span></span>
   
    <span data-ttu-id="5b458-191">h.</span><span class="sxs-lookup"><span data-stu-id="5b458-191">h.</span></span> <span data-ttu-id="5b458-192">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="5b458-192">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="5b458-193">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="5b458-193">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5b458-194">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="5b458-194">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5b458-195">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5b458-195">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5b458-196">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="5b458-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="5b458-197">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="5b458-197">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="5b458-199">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="5b458-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b458-200">在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="5b458-200">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-egnyte-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5b458-202">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="5b458-202">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-egnyte-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5b458-204">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="5b458-204">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-egnyte-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5b458-206">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="5b458-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-egnyte-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5b458-208">a.</span><span class="sxs-lookup"><span data-stu-id="5b458-208">a.</span></span> <span data-ttu-id="5b458-209">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="5b458-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5b458-210">b.</span><span class="sxs-lookup"><span data-stu-id="5b458-210">b.</span></span> <span data-ttu-id="5b458-211">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="5b458-211">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5b458-212">c.</span><span class="sxs-lookup"><span data-stu-id="5b458-212">c.</span></span> <span data-ttu-id="5b458-213">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="5b458-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5b458-214">d.</span><span class="sxs-lookup"><span data-stu-id="5b458-214">d.</span></span> <span data-ttu-id="5b458-215">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="5b458-215">Click **Create**.</span></span>
 
### <a name="creating-an-egnyte-test-user"></a><span data-ttu-id="5b458-216">建立 Egnyte 測試使用者</span><span class="sxs-lookup"><span data-stu-id="5b458-216">Creating an Egnyte test user</span></span>

<span data-ttu-id="5b458-217">tooenable Azure AD 使用者 toolog 中 tooEgnyte，它們必須佈建到 Egnyte。</span><span class="sxs-lookup"><span data-stu-id="5b458-217">tooenable Azure AD users toolog in tooEgnyte, they must be provisioned into Egnyte.</span></span> <span data-ttu-id="5b458-218">在 Egnyte 的 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="5b458-218">In hello case of Egnyte, provisioning is a manual task.</span></span>

<span data-ttu-id="5b458-219">**tooprovision 使用者帳戶，執行下列步驟 hello:**</span><span class="sxs-lookup"><span data-stu-id="5b458-219">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b458-220">登入 tooyour **Egnyte**以系統管理員身分的公司網站。</span><span class="sxs-lookup"><span data-stu-id="5b458-220">Log in tooyour **Egnyte** company site as administrator.</span></span>

2. <span data-ttu-id="5b458-221">跳過**設定\>使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="5b458-221">Go too**Settings \> Users & Groups**.</span></span>

3. <span data-ttu-id="5b458-222">按一下**新增使用者**，然後選取 hello 類型要 tooadd 的使用者。</span><span class="sxs-lookup"><span data-stu-id="5b458-222">Click **Add New User**, and then select hello type of user you want tooadd.</span></span>
   
   <span data-ttu-id="5b458-223">![使用者](./media/active-directory-saas-egnyte-tutorial/ic787824.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="5b458-223">![Users](./media/active-directory-saas-egnyte-tutorial/ic787824.png "Users")</span></span>

4. <span data-ttu-id="5b458-224">在 [hello**新增標準使用者**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="5b458-224">In hello **New Standard User** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="5b458-225">![新的標準使用者](./media/active-directory-saas-egnyte-tutorial/ic787825.png "新的標準使用者")</span><span class="sxs-lookup"><span data-stu-id="5b458-225">![New Standard User](./media/active-directory-saas-egnyte-tutorial/ic787825.png "New Standard User")</span></span>   

   <span data-ttu-id="5b458-226">a.</span><span class="sxs-lookup"><span data-stu-id="5b458-226">a.</span></span> <span data-ttu-id="5b458-227">型別 hello**電子郵件**， **Username**，以及您想要 tooprovision 之有效 Azure Active Directory 帳戶的其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="5b458-227">Type hello **Email**, **Username**, and other details of a valid Azure Active Directory account you want tooprovision.</span></span>
   
   <span data-ttu-id="5b458-228">b.</span><span class="sxs-lookup"><span data-stu-id="5b458-228">b.</span></span> <span data-ttu-id="5b458-229">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="5b458-229">Click **Save**.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="5b458-230">hello Azure Active Directory 帳戶持有者將會收到電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="5b458-230">hello Azure Active Directory account holder will receive a notification email.</span></span>
    >

>[!NOTE]
><span data-ttu-id="5b458-231">您可以使用任何其他 Egnyte 使用者帳戶建立工具或 Api 提供 Egnyte tooprovision AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="5b458-231">You can use any other Egnyte user account creation tools or APIs provided by Egnyte tooprovision AAD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5b458-232">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="5b458-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5b458-233">在本節中，您可以授與存取 tooEgnyte 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5b458-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEgnyte.</span></span>

![指派使用者][200] 

<span data-ttu-id="5b458-235">**tooassign 許 Simon tooEgnyte，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="5b458-235">**tooassign Britta Simon tooEgnyte, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b458-236">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="5b458-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="5b458-238">在 [hello] 應用程式清單中，選取**Egnyte**。</span><span class="sxs-lookup"><span data-stu-id="5b458-238">In hello applications list, select **Egnyte**.</span></span>

    ![設定單一登入](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_app.png) 

3. <span data-ttu-id="5b458-240">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="5b458-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="5b458-242">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5b458-242">Click **Add** button.</span></span> <span data-ttu-id="5b458-243">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="5b458-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="5b458-245">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="5b458-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5b458-246">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5b458-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5b458-247">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5b458-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5b458-248">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="5b458-248">Testing single sign-on</span></span>

<span data-ttu-id="5b458-249">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="5b458-249">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5b458-250">當您按一下 hello Egnyte 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Egnyte 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5b458-250">When you click hello Egnyte tile in hello Access Panel, you should get automatically signed-on tooyour Egnyte application.</span></span>
<span data-ttu-id="5b458-251">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="5b458-251">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5b458-252">其他資源</span><span class="sxs-lookup"><span data-stu-id="5b458-252">Additional resources</span></span>

* [<span data-ttu-id="5b458-253">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5b458-253">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5b458-254">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="5b458-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_203.png

