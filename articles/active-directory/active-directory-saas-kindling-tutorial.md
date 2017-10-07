---
title: "教學課程：將 Azure Active Directory 與 Kindling 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Kindling 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 71229751-74eb-4c2c-abb4-07caa95754c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 32ad6116c2690aea2060a2dd56e052f233ad7ae3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kindling"></a><span data-ttu-id="c5726-103">教學課程：Azure Active Directory 與 Kindling 整合</span><span class="sxs-lookup"><span data-stu-id="c5726-103">Tutorial: Azure Active Directory integration with Kindling</span></span>

<span data-ttu-id="c5726-104">在此教學課程中，您學會如何 toointegrate Kindling 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="c5726-104">In this tutorial, you learn how toointegrate Kindling with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c5726-105">與 Azure AD 整合 Kindling 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="c5726-105">Integrating Kindling with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c5726-106">您可以控制存取 tooKindling Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="c5726-106">You can control in Azure AD who has access tooKindling</span></span>
- <span data-ttu-id="c5726-107">您可以啟用您的使用者 tooautomatically get 登入 tooKindling （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="c5726-107">You can enable your users tooautomatically get signed-on tooKindling (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c5726-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="c5726-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c5726-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱。</span><span class="sxs-lookup"><span data-stu-id="c5726-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="c5726-110">[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="c5726-110">[what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c5726-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="c5726-111">Prerequisites</span></span>

<span data-ttu-id="c5726-112">Kindling tooconfigure Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="c5726-112">tooconfigure Azure AD integration with Kindling, you need hello following items:</span></span>

- <span data-ttu-id="c5726-113">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="c5726-113">An Azure AD subscription</span></span>
- <span data-ttu-id="c5726-114">Kindling 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="c5726-114">A Kindling single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c5726-115">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="c5726-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c5726-116">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="c5726-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c5726-117">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="c5726-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c5726-118">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="c5726-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c5726-119">案例描述</span><span class="sxs-lookup"><span data-stu-id="c5726-119">Scenario description</span></span>
<span data-ttu-id="c5726-120">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c5726-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c5726-121">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="c5726-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c5726-122">從 hello 圖庫加入 Kindling</span><span class="sxs-lookup"><span data-stu-id="c5726-122">Adding Kindling from hello gallery</span></span>
2. <span data-ttu-id="c5726-123">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c5726-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kindling-from-hello-gallery"></a><span data-ttu-id="c5726-124">從 hello 圖庫加入 Kindling</span><span class="sxs-lookup"><span data-stu-id="c5726-124">Adding Kindling from hello gallery</span></span>
<span data-ttu-id="c5726-125">tooconfigure hello Kindling 至 Azure AD 整合，您需要 tooadd Kindling hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c5726-125">tooconfigure hello integration of Kindling into Azure AD, you need tooadd Kindling from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c5726-126">**tooadd Kindling 從 hello 組件庫，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="c5726-126">**tooadd Kindling from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5726-127">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="c5726-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c5726-129">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="c5726-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c5726-130">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="c5726-130">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="c5726-132">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="c5726-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="c5726-134">在 [hello] 搜尋方塊中，輸入**Kindling**。</span><span class="sxs-lookup"><span data-stu-id="c5726-134">In hello search box, type **Kindling**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_search.png)

5. <span data-ttu-id="c5726-136">在 hello 結果 窗格中，選取  **Kindling**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c5726-136">In hello results panel, select **Kindling**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c5726-138">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c5726-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c5726-139">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Kindling 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c5726-139">In this section, you configure and test Azure AD single sign-on with Kindling based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c5726-140">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Kindling 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="c5726-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kindling is tooa user in Azure AD.</span></span> <span data-ttu-id="c5726-141">換句話說，Azure AD 使用者與 hello 之間的連結關聯性相關的建立 Kindling 需求 toobe 中的使用者。</span><span class="sxs-lookup"><span data-stu-id="c5726-141">In other words, a link relationship between an Azure AD user and hello related user in Kindling needs toobe established.</span></span>

<span data-ttu-id="c5726-142">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Kindling 中。</span><span class="sxs-lookup"><span data-stu-id="c5726-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Kindling.</span></span>

<span data-ttu-id="c5726-143">tooconfigure 及 Kindling 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="c5726-143">tooconfigure and test Azure AD single sign-on with Kindling, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c5726-144">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="c5726-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c5726-145">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="c5726-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c5726-146">**[建立測試使用者 Kindling](#creating-a-kindling-test-user)**  -toohave 對應項目許 Simon 中也就 Kindling 連結 toohello Azure AD 使用者表示法。</span><span class="sxs-lookup"><span data-stu-id="c5726-146">**[Creating a Kindling test user](#creating-a-kindling-test-user)** - toohave a counterpart of Britta Simon in Kindling that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c5726-147">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c5726-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c5726-148">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="c5726-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c5726-149">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c5726-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c5726-150">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Kindling 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="c5726-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kindling application.</span></span>

<span data-ttu-id="c5726-151">**tooconfigure Azure AD 單一登入與 Kindling，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="c5726-151">**tooconfigure Azure AD single sign-on with Kindling, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5726-152">在 Azure 入口網站上 hello hello **Kindling**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="c5726-152">In hello Azure portal, on hello **Kindling** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="c5726-154">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c5726-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_samlbase.png)

3. <span data-ttu-id="c5726-156">在 hello **Kindling 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="c5726-156">On hello **Kindling Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_url.png)

    <span data-ttu-id="c5726-158">a.</span><span class="sxs-lookup"><span data-stu-id="c5726-158">a.</span></span> <span data-ttu-id="c5726-159">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.kindlingapp.com`</span><span class="sxs-lookup"><span data-stu-id="c5726-159">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.kindlingapp.com`</span></span>

    <span data-ttu-id="c5726-160">b.</span><span class="sxs-lookup"><span data-stu-id="c5726-160">b.</span></span>  <span data-ttu-id="c5726-161">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.kindlingapp.com/saml/module.php/saml/sp/metadata.php/clientIDP`</span><span class="sxs-lookup"><span data-stu-id="c5726-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.kindlingapp.com/saml/module.php/saml/sp/metadata.php/clientIDP`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c5726-162">這些值不是真正的 hello。</span><span class="sxs-lookup"><span data-stu-id="c5726-162">These values are not hello real.</span></span> <span data-ttu-id="c5726-163">更新這些值與 hello 實際登入 URL 和識別碼。</span><span class="sxs-lookup"><span data-stu-id="c5726-163">Update these values with hello actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="c5726-164">請連絡[Kindling 支援小組](mailto:support@kindlingapp.com)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="c5726-164">Contact [Kindling support team](mailto:support@kindlingapp.com) tooget these values.</span></span>
 
4. <span data-ttu-id="c5726-165">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="c5726-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_certificate.png) 

5. <span data-ttu-id="c5726-167">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="c5726-167">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-kindling-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c5726-169">在 hello **Kindling 組態**區段中，按一下**設定 Kindling** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="c5726-169">On hello **Kindling Configuration** section, click **Configure Kindling** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c5726-170">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="c5726-170">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_configure.png) 

7. <span data-ttu-id="c5726-172">tooconfigure 單一登入上**Kindling**端，您需要下載 toosend hello**憑證 (Base64)**，**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**太[Kindling 支援小組](mailto:support@kindlingapp.com)。</span><span class="sxs-lookup"><span data-stu-id="c5726-172">tooconfigure single sign-on on **Kindling** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Kindling support team](mailto:support@kindlingapp.com).</span></span>

> [!TIP]
> <span data-ttu-id="c5726-173">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="c5726-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c5726-174">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="c5726-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c5726-175">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c5726-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c5726-176">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="c5726-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="c5726-177">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="c5726-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="c5726-179">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="c5726-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5726-180">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="c5726-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kindling-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c5726-182">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="c5726-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kindling-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c5726-184">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="c5726-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kindling-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c5726-186">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="c5726-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kindling-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c5726-188">a.</span><span class="sxs-lookup"><span data-stu-id="c5726-188">a.</span></span> <span data-ttu-id="c5726-189">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="c5726-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c5726-190">b.</span><span class="sxs-lookup"><span data-stu-id="c5726-190">b.</span></span> <span data-ttu-id="c5726-191">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="c5726-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c5726-192">c.</span><span class="sxs-lookup"><span data-stu-id="c5726-192">c.</span></span> <span data-ttu-id="c5726-193">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="c5726-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c5726-194">d.</span><span class="sxs-lookup"><span data-stu-id="c5726-194">d.</span></span> <span data-ttu-id="c5726-195">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="c5726-195">Click **Create**.</span></span>
 
### <a name="creating-a-kindling-test-user"></a><span data-ttu-id="c5726-196">建立 Kindling 測試使用者</span><span class="sxs-lookup"><span data-stu-id="c5726-196">Creating a Kindling test user</span></span>

<span data-ttu-id="c5726-197">hello 本節目標在於 toocreate Kindling 中呼叫許 Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="c5726-197">hello objective of this section is toocreate a user called Britta Simon in Kindling.</span></span> <span data-ttu-id="c5726-198">Kindling 支援 Just-in-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="c5726-198">Kindling supports just-in-time provisioning.</span></span> <span data-ttu-id="c5726-199">您已在 [設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)中啟用。</span><span class="sxs-lookup"><span data-stu-id="c5726-199">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="c5726-200">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="c5726-200">There is no action item for you in this section.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c5726-201">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="c5726-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c5726-202">在本節中，您可以授與存取 tooKindling 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c5726-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKindling.</span></span>

![指派使用者][200] 

<span data-ttu-id="c5726-204">**tooassign 許 Simon tooKindling，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="c5726-204">**tooassign Britta Simon tooKindling, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5726-205">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="c5726-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="c5726-207">在 [hello] 應用程式清單中，選取**Kindling**。</span><span class="sxs-lookup"><span data-stu-id="c5726-207">In hello applications list, select **Kindling**.</span></span>

    ![設定單一登入](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_app.png) 

3. <span data-ttu-id="c5726-209">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="c5726-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="c5726-211">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c5726-211">Click **Add** button.</span></span> <span data-ttu-id="c5726-212">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="c5726-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="c5726-214">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="c5726-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c5726-215">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c5726-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c5726-216">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c5726-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c5726-217">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="c5726-217">Testing single sign-on</span></span>

<span data-ttu-id="c5726-218">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="c5726-218">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c5726-219">當您按一下 hello Kindling 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Kindling 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c5726-219">When you click hello Kindling tile in hello Access Panel, you should get automatically signed-on tooyour Kindling application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c5726-220">其他資源</span><span class="sxs-lookup"><span data-stu-id="c5726-220">Additional resources</span></span>

* [<span data-ttu-id="c5726-221">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c5726-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c5726-222">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="c5726-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_203.png

