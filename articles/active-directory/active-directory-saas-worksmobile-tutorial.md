---
title: "教學課程：Azure Active Directory 與 WORKS MOBILE 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與適用於行動裝置之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 725f32fd-d0ad-49c7-b137-1cc246bf85d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 80192218a2e99a921834bb53e708d5e4fab413f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-works-mobile"></a><span data-ttu-id="3e7c9-103">教學課程：Azure Active Directory 與 WORKS MOBILE 整合</span><span class="sxs-lookup"><span data-stu-id="3e7c9-103">Tutorial: Azure Active Directory integration with WORKS MOBILE</span></span>

<span data-ttu-id="3e7c9-104">在本教學課程中，您了解 toointegrate 的運作方式與 Azure Active Directory (Azure AD) 的行動裝置。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-104">In this tutorial, you learn how toointegrate WORKS MOBILE with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3e7c9-105">與 Azure AD 整合適用於行動裝置可以提供下列優點的 hello:</span><span class="sxs-lookup"><span data-stu-id="3e7c9-105">Integrating WORKS MOBILE with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3e7c9-106">您可以控制存取 tooWORKS 行動裝置版的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="3e7c9-106">You can control in Azure AD who has access tooWORKS MOBILE</span></span>
- <span data-ttu-id="3e7c9-107">您可以啟用您的使用者 tooautomatically get 登入 tooWORKS （單一登入） 的行動裝置與他們的 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="3e7c9-107">You can enable your users tooautomatically get signed-on tooWORKS MOBILE (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3e7c9-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="3e7c9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3e7c9-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e7c9-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="3e7c9-110">Prerequisites</span></span>

<span data-ttu-id="3e7c9-111">tooconfigure 與適用於行動裝置版的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="3e7c9-111">tooconfigure Azure AD integration with WORKS MOBILE, you need hello following items:</span></span>

- <span data-ttu-id="3e7c9-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="3e7c9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3e7c9-113">已啟用 WORKS MOBILE 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="3e7c9-113">A WORKS MOBILE single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3e7c9-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3e7c9-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="3e7c9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3e7c9-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3e7c9-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3e7c9-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="3e7c9-118">Scenario description</span></span>
<span data-ttu-id="3e7c9-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3e7c9-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="3e7c9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3e7c9-121">新增適用於行動裝置從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="3e7c9-121">Adding WORKS MOBILE from hello gallery</span></span>
2. <span data-ttu-id="3e7c9-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="3e7c9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-works-mobile-from-hello-gallery"></a><span data-ttu-id="3e7c9-123">新增適用於行動裝置從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="3e7c9-123">Adding WORKS MOBILE from hello gallery</span></span>
<span data-ttu-id="3e7c9-124">tooconfigure hello 整合適用於行動裝置版的 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd 適用於行動裝置。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-124">tooconfigure hello integration of WORKS MOBILE into Azure AD, you need tooadd WORKS MOBILE from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3e7c9-125">**tooadd 適用於行動裝置從 hello 組件庫，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="3e7c9-125">**tooadd WORKS MOBILE from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3e7c9-126">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3e7c9-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3e7c9-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="3e7c9-131">tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="3e7c9-133">在 [hello] 搜尋方塊中，輸入**WORKS 行動**。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-133">In hello search box, type **WORKS MOBILE**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_search.png)

5. <span data-ttu-id="3e7c9-135">在 [hello [結果] 窗格中，選取**適用於行動**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-135">In hello results panel, select **WORKS MOBILE**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3e7c9-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="3e7c9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3e7c9-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 WORKS MOBILE 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-138">In this section, you configure and test Azure AD single sign-on with WORKS MOBILE based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3e7c9-139">單一登入 toowork，Azure AD 需要 tooknow hello 對應項目中適用於行動裝置的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in WORKS MOBILE is tooa user in Azure AD.</span></span> <span data-ttu-id="3e7c9-140">換句話說，Azure AD 使用者與 hello 中適用於行動裝置的相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-140">In other words, a link relationship between an Azure AD user and hello related user in WORKS MOBILE needs toobe established.</span></span>

<span data-ttu-id="3e7c9-141">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**使用者名稱**中適用於行動裝置。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in WORKS MOBILE.</span></span>

<span data-ttu-id="3e7c9-142">tooconfigure 及適用於行動裝置與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="3e7c9-142">tooconfigure and test Azure AD single sign-on with WORKS MOBILE, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3e7c9-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3e7c9-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3e7c9-145">**[建立適用於行動裝置版的測試使用者](#creating-a-works-mobile-test-user)** -toohave 許 Simon 適用於行動裝置版是連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-145">**[Creating a WORKS MOBILE test user](#creating-a-works-mobile-test-user)** - toohave a counterpart of Britta Simon in WORKS MOBILE that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3e7c9-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3e7c9-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3e7c9-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="3e7c9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3e7c9-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並適用於行動裝置應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your WORKS MOBILE application.</span></span>

<span data-ttu-id="3e7c9-150">**tooconfigure Azure AD 單一登入與適用於行動裝置，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="3e7c9-150">**tooconfigure Azure AD single sign-on with WORKS MOBILE, perform hello following steps:**</span></span>

1. <span data-ttu-id="3e7c9-151">在 Azure 入口網站上 hello hello **WORKS 行動**應用程式整合頁面上，按一下**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-151">In hello Azure portal, on hello **WORKS MOBILE** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="3e7c9-153">在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_samlbase.png)

3. <span data-ttu-id="3e7c9-155">在 [hello**適用於行動裝置的網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="3e7c9-155">On hello **WORKS MOBILE Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_url.png)

    <span data-ttu-id="3e7c9-157">a.</span><span class="sxs-lookup"><span data-stu-id="3e7c9-157">a.</span></span> <span data-ttu-id="3e7c9-158">在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.worksmobile.com/jp/myservice`</span><span class="sxs-lookup"><span data-stu-id="3e7c9-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.worksmobile.com/jp/myservice`</span></span>

    <span data-ttu-id="3e7c9-159">b.</span><span class="sxs-lookup"><span data-stu-id="3e7c9-159">b.</span></span> <span data-ttu-id="3e7c9-160">在 [hello**識別碼**文字方塊中，做為型別 hello 值`worksmobile.com`</span><span class="sxs-lookup"><span data-stu-id="3e7c9-160">In hello **Identifier** textbox, type hello value as `worksmobile.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3e7c9-161">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-161">This value is not real.</span></span> <span data-ttu-id="3e7c9-162">更新此值以 hello 實際的登入 URL。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-162">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="3e7c9-163">請連絡[適用於行動裝置用戶端支援小組](mailto:dl_ssoinfo@worksmobile.com)tooget 此值。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-163">Contact [WORKS MOBILE Client support team](mailto:dl_ssoinfo@worksmobile.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="3e7c9-164">在 [hello **SAML 簽章憑證**區段中，按一下**Certificate(Raw)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-164">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_certificate.png) 

5. <span data-ttu-id="3e7c9-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-worksmobile-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3e7c9-168">在 [hello**適用於行動裝置組態**區段中，按一下**設定適用於行動**tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-168">On hello **WORKS MOBILE Configuration** section, click **Configure WORKS MOBILE** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="3e7c9-169">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="3e7c9-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_configure.png) 

7. <span data-ttu-id="3e7c9-171">tooget SSO 設定應用程式，請連絡[適用於行動裝置支援小組](mailto:dl_ssoinfo@worksmobile.com)，提供下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="3e7c9-171">tooget SSO configured for your application, contact [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) and provide them with hello following information:</span></span> 

    <span data-ttu-id="3e7c9-172">• hello 下載**憑證檔案**</span><span class="sxs-lookup"><span data-stu-id="3e7c9-172">• hello downloaded **Certificate file**</span></span>

    <span data-ttu-id="3e7c9-173">• hello **SAML 單一登入服務 URL**</span><span class="sxs-lookup"><span data-stu-id="3e7c9-173">• hello **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="3e7c9-174">• hello **SAML 實體識別碼**</span><span class="sxs-lookup"><span data-stu-id="3e7c9-174">• hello **SAML Entity ID**</span></span>

    <span data-ttu-id="3e7c9-175">• hello**登出 URL**</span><span class="sxs-lookup"><span data-stu-id="3e7c9-175">• hello **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="3e7c9-176">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="3e7c9-176">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3e7c9-177">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-177">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3e7c9-178">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3e7c9-178">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3e7c9-179">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="3e7c9-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="3e7c9-180">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-180">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="3e7c9-182">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="3e7c9-182">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3e7c9-183">在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-183">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3e7c9-185">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-185">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3e7c9-187">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-187">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3e7c9-189">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="3e7c9-189">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3e7c9-191">a.</span><span class="sxs-lookup"><span data-stu-id="3e7c9-191">a.</span></span> <span data-ttu-id="3e7c9-192">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-192">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3e7c9-193">b.</span><span class="sxs-lookup"><span data-stu-id="3e7c9-193">b.</span></span> <span data-ttu-id="3e7c9-194">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-194">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3e7c9-195">c.</span><span class="sxs-lookup"><span data-stu-id="3e7c9-195">c.</span></span> <span data-ttu-id="3e7c9-196">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-196">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3e7c9-197">d.</span><span class="sxs-lookup"><span data-stu-id="3e7c9-197">d.</span></span> <span data-ttu-id="3e7c9-198">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-198">Click **Create**.</span></span>
 
### <a name="creating-a-works-mobile-test-user"></a><span data-ttu-id="3e7c9-199">建立 WORKS MOBILE 測試使用者</span><span class="sxs-lookup"><span data-stu-id="3e7c9-199">Creating a WORKS MOBILE test user</span></span>

 <span data-ttu-id="3e7c9-200">在本節中，您要在 WORKS MOBILE 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-200">In this section, you create a user called Britta Simon in WORKS MOBILE.</span></span> <span data-ttu-id="3e7c9-201">請使用[適用於行動裝置支援小組](mailto:dl_ssoinfo@worksmobile.com)tooadd hello hello WORKS MOBILE 平台的使用者。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-201">Please work with [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) tooadd hello users in hello WORKS MOBILE platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3e7c9-202">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="3e7c9-202">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3e7c9-203">在本節中，您可以授與存取 tooWORKS 行動裝置啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-203">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWORKS MOBILE.</span></span>

![指派使用者][200] 

<span data-ttu-id="3e7c9-205">**tooassign 許 Simon tooWORKS 行動裝置，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="3e7c9-205">**tooassign Britta Simon tooWORKS MOBILE, perform hello following steps:**</span></span>

1. <span data-ttu-id="3e7c9-206">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-206">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="3e7c9-208">在 [hello] 應用程式清單中，選取**WORKS 行動**。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-208">In hello applications list, select **WORKS MOBILE**.</span></span>

    ![設定單一登入](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_app.png) 

3. <span data-ttu-id="3e7c9-210">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-210">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="3e7c9-212">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-212">Click **Add** button.</span></span> <span data-ttu-id="3e7c9-213">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="3e7c9-215">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-215">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3e7c9-216">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3e7c9-217">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3e7c9-218">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="3e7c9-218">Testing single sign-on</span></span>

<span data-ttu-id="3e7c9-219">本節中，您可以測試使用存取面板 hello Azure AD 的 SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-219">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="3e7c9-220">當您按一下 hello WORKS 行動磚 hello 存取面板中的時，您應該取得自動登入 tooyour 適用於行動裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-220">When you click hello WORKS MOBILE tile in hello Access Panel, you should get automatically signed-on tooyour WORKS MOBILE application.</span></span>
<span data-ttu-id="3e7c9-221">如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="3e7c9-221">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3e7c9-222">其他資源</span><span class="sxs-lookup"><span data-stu-id="3e7c9-222">Additional resources</span></span>

* [<span data-ttu-id="3e7c9-223">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3e7c9-223">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3e7c9-224">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="3e7c9-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_203.png

