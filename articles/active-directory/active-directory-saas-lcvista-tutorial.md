---
title: "教學課程：Azure Active Directory 與 LCVista 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 LCVista 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8db80d6e-3275-419f-aa39-6115a7bc9800
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: 5a4c7eb7d54b8b68c8241a97b9e516a3f6e55c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lcvista"></a><span data-ttu-id="cb806-103">教學課程：Azure Active Directory 與 LCVista 整合</span><span class="sxs-lookup"><span data-stu-id="cb806-103">Tutorial: Azure Active Directory integration with LCVista</span></span>

<span data-ttu-id="cb806-104">在此教學課程中，您學會如何 toointegrate LCVista 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="cb806-104">In this tutorial, you learn how toointegrate LCVista with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cb806-105">與 Azure AD 整合 LCVista 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="cb806-105">Integrating LCVista with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cb806-106">您可以控制存取 tooLCVista Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="cb806-106">You can control in Azure AD who has access tooLCVista</span></span>
- <span data-ttu-id="cb806-107">您可以啟用您的使用者 tooautomatically get 登入 tooLCVista （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="cb806-107">You can enable your users tooautomatically get signed-on tooLCVista (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cb806-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="cb806-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cb806-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="cb806-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb806-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="cb806-110">Prerequisites</span></span>

<span data-ttu-id="cb806-111">tooconfigure LCVista 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="cb806-111">tooconfigure Azure AD integration with LCVista, you need hello following items:</span></span>

- <span data-ttu-id="cb806-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="cb806-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cb806-113">啟用 LCVista 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="cb806-113">A LCVista single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cb806-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="cb806-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cb806-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="cb806-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cb806-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="cb806-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cb806-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="cb806-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cb806-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="cb806-118">Scenario description</span></span>
<span data-ttu-id="cb806-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cb806-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cb806-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="cb806-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cb806-121">從 hello 圖庫加入 LCVista</span><span class="sxs-lookup"><span data-stu-id="cb806-121">Adding LCVista from hello gallery</span></span>
2. <span data-ttu-id="cb806-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="cb806-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lcvista-from-hello-gallery"></a><span data-ttu-id="cb806-123">從 hello 圖庫加入 LCVista</span><span class="sxs-lookup"><span data-stu-id="cb806-123">Adding LCVista from hello gallery</span></span>
<span data-ttu-id="cb806-124">tooconfigure hello 整合 LCVista 到 Azure AD，您需要 tooadd LCVista hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cb806-124">tooconfigure hello integration of LCVista into Azure AD, you need tooadd LCVista from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cb806-125">**tooadd LCVista 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="cb806-125">**tooadd LCVista from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb806-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="cb806-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cb806-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="cb806-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cb806-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="cb806-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="cb806-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="cb806-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="cb806-133">在 [hello] 搜尋方塊中，輸入**LCVista**。</span><span class="sxs-lookup"><span data-stu-id="cb806-133">In hello search box, type **LCVista**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_search.png)

5. <span data-ttu-id="cb806-135">在 hello 結果 窗格中，選取  **LCVista**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cb806-135">In hello results panel, select **LCVista**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cb806-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="cb806-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cb806-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 LCVista 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cb806-138">In this section, you configure and test Azure AD single sign-on with LCVista based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cb806-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 LCVista 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="cb806-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LCVista is tooa user in Azure AD.</span></span> <span data-ttu-id="cb806-140">換句話說，Azure AD 使用者與 hello LCVista 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="cb806-140">In other words, a link relationship between an Azure AD user and hello related user in LCVista needs toobe established.</span></span>

<span data-ttu-id="cb806-141">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** LCVista 中。</span><span class="sxs-lookup"><span data-stu-id="cb806-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LCVista.</span></span>

<span data-ttu-id="cb806-142">tooconfigure 及 LCVista 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="cb806-142">tooconfigure and test Azure AD single sign-on with LCVista, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cb806-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="cb806-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cb806-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="cb806-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cb806-145">**[建立測試使用者 LCVista](#creating-a-lcvista-test-user)**  -toohave 許 Simon LCVista 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="cb806-145">**[Creating a LCVista test user](#creating-a-lcvista-test-user)** - toohave a counterpart of Britta Simon in LCVista that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cb806-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cb806-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cb806-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="cb806-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cb806-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="cb806-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cb806-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 LCVista 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="cb806-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LCVista application.</span></span>

<span data-ttu-id="cb806-150">**tooconfigure Azure AD 單一登入與 LCVista，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="cb806-150">**tooconfigure Azure AD single sign-on with LCVista, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb806-151">在 Azure 入口網站上 hello hello **LCVista**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="cb806-151">In hello Azure portal, on hello **LCVista** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="cb806-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cb806-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_samlbase.png)

3. <span data-ttu-id="cb806-155">在 hello **LCVista 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="cb806-155">On hello **LCVista Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_url.png)

    <span data-ttu-id="cb806-157">a.</span><span class="sxs-lookup"><span data-stu-id="cb806-157">a.</span></span> <span data-ttu-id="cb806-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.lcvista.com/rainier/login`</span><span class="sxs-lookup"><span data-stu-id="cb806-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.lcvista.com/rainier/login`</span></span>

    <span data-ttu-id="cb806-159">b.</span><span class="sxs-lookup"><span data-stu-id="cb806-159">b.</span></span> <span data-ttu-id="cb806-160">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.lcvista.com`</span><span class="sxs-lookup"><span data-stu-id="cb806-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.lcvista.com`</span></span> 
     
    > [!NOTE] 
    > <span data-ttu-id="cb806-161">這些值不是真正的 hello。</span><span class="sxs-lookup"><span data-stu-id="cb806-161">These values are not hello real.</span></span> <span data-ttu-id="cb806-162">更新這些值與實際的 hello 識別碼和登入 URL。</span><span class="sxs-lookup"><span data-stu-id="cb806-162">Update these values with hello actual Identifier and Sign-On URL.</span></span> <span data-ttu-id="cb806-163">請連絡[LCVista 用戶端支援小組](https://lcvista.com/contact)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="cb806-163">Contact [LCVista Client support team](https://lcvista.com/contact) tooget these values.</span></span> 

4. <span data-ttu-id="cb806-164">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="cb806-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_certificate.png) 

5. <span data-ttu-id="cb806-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="cb806-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-lcvista-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="cb806-168">在 hello **LCVista 組態**區段中，按一下**設定 LCVista** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="cb806-168">On hello **LCVista Configuration** section, click **Configure LCVista** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="cb806-169">複製 hello **SAML 實體識別碼**和**SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="cb806-169">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_configure.png) 

7.  <span data-ttu-id="cb806-171">登入 tooyour LCVista 應用程式，以系統管理員。</span><span class="sxs-lookup"><span data-stu-id="cb806-171">Sign on tooyour LCVista application as an administrator.</span></span>

8. <span data-ttu-id="cb806-172">在 hello **SAML 組態**區段中，檢查 hello**啟用 SAML 登入**，然後輸入 hello 詳細資料，如下列影像中所述。</span><span class="sxs-lookup"><span data-stu-id="cb806-172">In hello **SAML Config** section, check hello **Enable SAML login** and enter hello details as mentioned in below image.</span></span> 

    ![設定單一登入](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_config.png)

    <span data-ttu-id="cb806-174">a.</span><span class="sxs-lookup"><span data-stu-id="cb806-174">a.</span></span> <span data-ttu-id="cb806-175">貼上 hello**簽發者 URL**您已複製從 Azure AD 中 hello**實體識別碼**> 一節。</span><span class="sxs-lookup"><span data-stu-id="cb806-175">Paste hello **Issuer URL** which you have copied from Azure AD in hello **Entity ID** section.</span></span> 

    <span data-ttu-id="cb806-176">b.</span><span class="sxs-lookup"><span data-stu-id="cb806-176">b.</span></span> <span data-ttu-id="cb806-177">貼上 hello**單一登入服務 URL**您已複製從 Azure AD 中 hello **URL** > 一節。</span><span class="sxs-lookup"><span data-stu-id="cb806-177">Paste hello **Single Sign-On Service URL** which you have copied from Azure AD in hello **URL** section.</span></span>

    <span data-ttu-id="cb806-178">c.</span><span class="sxs-lookup"><span data-stu-id="cb806-178">c.</span></span> <span data-ttu-id="cb806-179">從中繼資料 (XML) 從 Azure 入口網站下載，複製 hello 值**X509Certificate**並將它貼在 hello **x509 憑證**> 一節。</span><span class="sxs-lookup"><span data-stu-id="cb806-179">From Metadata (XML) which you have downloaded from Azure portal, copy hello value **X509Certificate** and paste it in hello **x509 Certificate** section.</span></span>

    <span data-ttu-id="cb806-180">d.</span><span class="sxs-lookup"><span data-stu-id="cb806-180">d.</span></span> <span data-ttu-id="cb806-181">在 hello**名字屬性**文字方塊中，貼上 hello 值`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`。</span><span class="sxs-lookup"><span data-stu-id="cb806-181">In hello **First name attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>

    <span data-ttu-id="cb806-182">e.</span><span class="sxs-lookup"><span data-stu-id="cb806-182">e.</span></span> <span data-ttu-id="cb806-183">在 hello**姓氏**文字方塊中，貼上 hello 值`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`。</span><span class="sxs-lookup"><span data-stu-id="cb806-183">In hello **Last name attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>

    <span data-ttu-id="cb806-184">f.</span><span class="sxs-lookup"><span data-stu-id="cb806-184">f.</span></span> <span data-ttu-id="cb806-185">在 hello**電子郵件屬性**文字方塊中，貼上 hello 值`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`。</span><span class="sxs-lookup"><span data-stu-id="cb806-185">In hello **Email attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="cb806-186">g.</span><span class="sxs-lookup"><span data-stu-id="cb806-186">g.</span></span> <span data-ttu-id="cb806-187">在 hello **Username 屬性**文字方塊中，貼上 hello 值`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`。</span><span class="sxs-lookup"><span data-stu-id="cb806-187">In hello **Username attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>

    <span data-ttu-id="cb806-188">e.</span><span class="sxs-lookup"><span data-stu-id="cb806-188">e.</span></span> <span data-ttu-id="cb806-189">按一下**儲存**toosave hello 設定。</span><span class="sxs-lookup"><span data-stu-id="cb806-189">Click **Save** toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="cb806-190">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="cb806-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cb806-191">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="cb806-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cb806-192">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cb806-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cb806-193">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="cb806-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="cb806-194">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="cb806-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="cb806-196">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="cb806-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb806-197">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="cb806-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lcvista-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cb806-199">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="cb806-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lcvista-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cb806-201">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="cb806-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lcvista-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cb806-203">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="cb806-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lcvista-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cb806-205">a.</span><span class="sxs-lookup"><span data-stu-id="cb806-205">a.</span></span> <span data-ttu-id="cb806-206">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="cb806-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cb806-207">b.</span><span class="sxs-lookup"><span data-stu-id="cb806-207">b.</span></span> <span data-ttu-id="cb806-208">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="cb806-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cb806-209">c.</span><span class="sxs-lookup"><span data-stu-id="cb806-209">c.</span></span> <span data-ttu-id="cb806-210">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="cb806-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cb806-211">d.</span><span class="sxs-lookup"><span data-stu-id="cb806-211">d.</span></span> <span data-ttu-id="cb806-212">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="cb806-212">Click **Create**.</span></span>
 
### <a name="creating-a-lcvista-test-user"></a><span data-ttu-id="cb806-213">建立 LCVista 測試使用者</span><span class="sxs-lookup"><span data-stu-id="cb806-213">Creating a LCVista test user</span></span>

<span data-ttu-id="cb806-214">在本節中，您要在 LCVista 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="cb806-214">In this section, you create a user called Britta Simon in LCVista.</span></span> <span data-ttu-id="cb806-215">您需要 toocontact [LCVista 用戶端支援小組](https://lcvista.com/contact)tooadd hello hello LCVista 應用程式的使用者。</span><span class="sxs-lookup"><span data-stu-id="cb806-215">You need toocontact [LCVista Client support team](https://lcvista.com/contact) tooadd hello users in hello LCVista application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cb806-216">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="cb806-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cb806-217">在本節中，您可以授與存取 tooLCVista 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cb806-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLCVista.</span></span>

![指派使用者][200] 

<span data-ttu-id="cb806-219">**tooassign 許 Simon tooLCVista，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="cb806-219">**tooassign Britta Simon tooLCVista, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb806-220">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="cb806-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="cb806-222">在 [hello] 應用程式清單中，選取**LCVista**。</span><span class="sxs-lookup"><span data-stu-id="cb806-222">In hello applications list, select **LCVista**.</span></span>

    ![設定單一登入](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_app.png) 

3. <span data-ttu-id="cb806-224">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="cb806-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="cb806-226">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cb806-226">Click **Add** button.</span></span> <span data-ttu-id="cb806-227">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="cb806-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="cb806-229">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="cb806-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cb806-230">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cb806-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cb806-231">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cb806-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cb806-232">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="cb806-232">Testing single sign-on</span></span>

<span data-ttu-id="cb806-233">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="cb806-233">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span> <span data-ttu-id="cb806-234">按一下 hello LCVista 磚在 hello 存取面板，您將會重新導向 tooOrganization 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="cb806-234">Click hello LCVista tile in hello Access Panel, you will be redirected tooOrganization sign on page.</span></span> <span data-ttu-id="cb806-235">後成功登入，您就無法登入 tooyour LCVista 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cb806-235">After successful login, you will be signed-on tooyour LCVista application.</span></span> <span data-ttu-id="cb806-236">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](https://msdn.microsoft.com/library/dn308586)。</span><span class="sxs-lookup"><span data-stu-id="cb806-236">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cb806-237">其他資源</span><span class="sxs-lookup"><span data-stu-id="cb806-237">Additional resources</span></span>

* [<span data-ttu-id="cb806-238">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cb806-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cb806-239">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="cb806-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_203.png

