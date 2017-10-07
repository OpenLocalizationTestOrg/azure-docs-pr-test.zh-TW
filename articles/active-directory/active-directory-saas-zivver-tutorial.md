---
title: "教學課程：Azure Active Directory 與 ZIVVER 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 ZIVVER 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 64cb7ea0-df6c-4963-84d8-6f435980e2de
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 0928abcc4dcbd97b892298f4919c8d44e1a058a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zivver"></a><span data-ttu-id="b925b-103">教學課程：Azure Active Directory 與 ZIVVER 整合</span><span class="sxs-lookup"><span data-stu-id="b925b-103">Tutorial: Azure Active Directory integration with ZIVVER</span></span>

<span data-ttu-id="b925b-104">在此教學課程中，您學會如何 toointegrate ZIVVER 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="b925b-104">In this tutorial, you learn how toointegrate ZIVVER with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b925b-105">與 Azure AD 整合 ZIVVER 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="b925b-105">Integrating ZIVVER with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b925b-106">您可以控制存取 tooZIVVER Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="b925b-106">You can control in Azure AD who has access tooZIVVER.</span></span>
- <span data-ttu-id="b925b-107">您可以啟用您的使用者 tooautomatically get 登入 tooZIVVER （單一登入） 具有其 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="b925b-107">You can enable your users tooautomatically get signed-on tooZIVVER (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="b925b-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="b925b-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="b925b-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="b925b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b925b-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="b925b-110">Prerequisites</span></span>

<span data-ttu-id="b925b-111">tooconfigure ZIVVER 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="b925b-111">tooconfigure Azure AD integration with ZIVVER, you need hello following items:</span></span>

- <span data-ttu-id="b925b-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b925b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b925b-113">已啟用 ZIVVER 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b925b-113">A ZIVVER single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b925b-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="b925b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b925b-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="b925b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b925b-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="b925b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b925b-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="b925b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b925b-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="b925b-118">Scenario description</span></span>
<span data-ttu-id="b925b-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b925b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b925b-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="b925b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b925b-121">從 hello 圖庫加入 ZIVVER</span><span class="sxs-lookup"><span data-stu-id="b925b-121">Adding ZIVVER from hello gallery</span></span>
2. <span data-ttu-id="b925b-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b925b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zivver-from-hello-gallery"></a><span data-ttu-id="b925b-123">從 hello 圖庫加入 ZIVVER</span><span class="sxs-lookup"><span data-stu-id="b925b-123">Adding ZIVVER from hello gallery</span></span>
<span data-ttu-id="b925b-124">tooconfigure hello 整合 ZIVVER 到 Azure AD，您需要 tooadd ZIVVER hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b925b-124">tooconfigure hello integration of ZIVVER into Azure AD, you need tooadd ZIVVER from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b925b-125">**tooadd ZIVVER 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b925b-125">**tooadd ZIVVER from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b925b-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="b925b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 按鈕][1]

2. <span data-ttu-id="b925b-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="b925b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b925b-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="b925b-129">Then go too**All applications**.</span></span>

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. <span data-ttu-id="b925b-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="b925b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 新應用程式按鈕][3]

4. <span data-ttu-id="b925b-133">在 hello 搜尋方塊中，輸入**ZIVVER**，選取**ZIVVER**然後按一下 從結果面板**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b925b-133">In hello search box, type **ZIVVER**, select **ZIVVER** from result panel then click **Add** button tooadd hello application.</span></span>

    ![ZIVVER hello [結果] 清單中](./media/active-directory-saas-zivver-tutorial/tutorial_zivver_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b925b-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b925b-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b925b-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 ZIVVER 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b925b-136">In this section, you configure and test Azure AD single sign-on with ZIVVER based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b925b-137">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 ZIVVER 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="b925b-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ZIVVER is tooa user in Azure AD.</span></span> <span data-ttu-id="b925b-138">換句話說，Azure AD 使用者與 hello ZIVVER 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="b925b-138">In other words, a link relationship between an Azure AD user and hello related user in ZIVVER needs toobe established.</span></span>

<span data-ttu-id="b925b-139">ZIVVER 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="b925b-139">In ZIVVER, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b925b-140">tooconfigure 及 ZIVVER 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="b925b-140">tooconfigure and test Azure AD single sign-on with ZIVVER, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b925b-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="b925b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b925b-142">**[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="b925b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b925b-143">**[建立測試使用者 ZIVVER](#create-a-zivver-test-user)**  -toohave 許 Simon ZIVVER 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="b925b-143">**[Create a ZIVVER test user](#create-a-zivver-test-user)** - toohave a counterpart of Britta Simon in ZIVVER that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b925b-144">**[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b925b-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b925b-145">**[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="b925b-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b925b-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b925b-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b925b-147">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 ZIVVER 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="b925b-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ZIVVER application.</span></span>

<span data-ttu-id="b925b-148">**tooconfigure Azure AD 單一登入與 ZIVVER，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b925b-148">**tooconfigure Azure AD single sign-on with ZIVVER, perform hello following steps:**</span></span>

1. <span data-ttu-id="b925b-149">在 Azure 入口網站上 hello hello **ZIVVER**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="b925b-149">In hello Azure portal, on hello **ZIVVER** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="b925b-151">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b925b-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-zivver-tutorial/tutorial_zivver_samlbase.png)

3. <span data-ttu-id="b925b-153">在 hello **ZIVVER 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="b925b-153">On hello **ZIVVER Domain and URLs** section, perform hello following steps:</span></span>

    ![ZIVVER 網域及 URL 單一登入資訊](./media/active-directory-saas-zivver-tutorial/tutorial_zivver_url.png)

    <span data-ttu-id="b925b-155">在 hello**識別碼**文字方塊中，型別 hello URL:`https://app.zivver.com/SAML/Zivver`</span><span class="sxs-lookup"><span data-stu-id="b925b-155">In hello **Identifier** textbox, type hello URL: `https://app.zivver.com/SAML/Zivver`</span></span>

4. <span data-ttu-id="b925b-156">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="b925b-156">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![hello 憑證下載連結](./media/active-directory-saas-zivver-tutorial/tutorial_zivver_certificate.png) 

5. <span data-ttu-id="b925b-158">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="b925b-158">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-zivver-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b925b-160">tooconfigure 單一登入上**ZIVVER**端，您需要下載 toosend hello**中繼資料 XML**太[ZIVVER 支援小組](https://support.zivver.com)。</span><span class="sxs-lookup"><span data-stu-id="b925b-160">tooconfigure single sign-on on **ZIVVER** side, you need toosend hello downloaded **Metadata XML** too[ZIVVER support team](https://support.zivver.com).</span></span> <span data-ttu-id="b925b-161">設定此設定 toohave hello SAML SSO 連線兩端上正確設定這些欄位。</span><span class="sxs-lookup"><span data-stu-id="b925b-161">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="b925b-162">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="b925b-162">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b925b-163">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="b925b-163">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b925b-164">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b925b-164">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b925b-165">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b925b-165">Create an Azure AD test user</span></span>

<span data-ttu-id="b925b-166">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="b925b-166">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="b925b-168">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b925b-168">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b925b-169">在 hello Azure 入口網站，hello 左窗格中，按一下 hello **Azure Active Directory**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="b925b-169">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-zivver-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="b925b-171">toodisplay hello 使用者清單，請移過**使用者和群組**，然後按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="b925b-171">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-zivver-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="b925b-173">tooopen hello**使用者**對話方塊中，按一下 [**新增**頂端的 hello hello**所有使用者**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="b925b-173">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello [新增] 按鈕](./media/active-directory-saas-zivver-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="b925b-175">在 hello**使用者**對話方塊方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="b925b-175">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello [使用者] 對話方塊](./media/active-directory-saas-zivver-tutorial/create_aaduser_04.png)

    <span data-ttu-id="b925b-177">a.</span><span class="sxs-lookup"><span data-stu-id="b925b-177">a.</span></span> <span data-ttu-id="b925b-178">在 hello**名稱**方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="b925b-178">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b925b-179">b.</span><span class="sxs-lookup"><span data-stu-id="b925b-179">b.</span></span> <span data-ttu-id="b925b-180">在 hello**使用者名**方塊中，使用者許 Simon 類型 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="b925b-180">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="b925b-181">c.</span><span class="sxs-lookup"><span data-stu-id="b925b-181">c.</span></span> <span data-ttu-id="b925b-182">選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 hello**密碼**方塊。</span><span class="sxs-lookup"><span data-stu-id="b925b-182">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="b925b-183">d.</span><span class="sxs-lookup"><span data-stu-id="b925b-183">d.</span></span> <span data-ttu-id="b925b-184">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="b925b-184">Click **Create**.</span></span>
  
### <a name="create-a-zivver-test-user"></a><span data-ttu-id="b925b-185">建立 ZIVVER 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b925b-185">Create a ZIVVER test user</span></span>

<span data-ttu-id="b925b-186">在本節中，您要在 ZIVVER 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="b925b-186">In this section, you create a user called Britta Simon in ZIVVER.</span></span> <span data-ttu-id="b925b-187">使用[ZIVVER 支援小組](https://support.zivver.com)tooadd hello hello ZIVVER 平台的使用者。</span><span class="sxs-lookup"><span data-stu-id="b925b-187">Work with [ZIVVER support team](https://support.zivver.com) tooadd hello users in hello ZIVVER platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="b925b-188">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b925b-188">Assign hello Azure AD test user</span></span>

<span data-ttu-id="b925b-189">在本節中，您可以授與存取 tooZIVVER 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b925b-189">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZIVVER.</span></span>

![指派 hello 使用者角色][200] 

<span data-ttu-id="b925b-191">**tooassign 許 Simon tooZIVVER，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b925b-191">**tooassign Britta Simon tooZIVVER, perform hello following steps:**</span></span>

1. <span data-ttu-id="b925b-192">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="b925b-192">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="b925b-194">在 [hello] 應用程式清單中，選取**ZIVVER**。</span><span class="sxs-lookup"><span data-stu-id="b925b-194">In hello applications list, select **ZIVVER**.</span></span>

    ![hello 應用程式清單中的 hello ZIVVER 連結](./media/active-directory-saas-zivver-tutorial/tutorial_zivver_app.png)  

3. <span data-ttu-id="b925b-196">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="b925b-196">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello 「 使用者和群組 」 的連結][202]

4. <span data-ttu-id="b925b-198">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b925b-198">Click **Add** button.</span></span> <span data-ttu-id="b925b-199">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="b925b-199">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 將作業加入窗格][203]

5. <span data-ttu-id="b925b-201">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="b925b-201">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b925b-202">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b925b-202">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b925b-203">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b925b-203">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b925b-204">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="b925b-204">Test single sign-on</span></span>

<span data-ttu-id="b925b-205">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="b925b-205">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b925b-206">當您按一下的 hello ZIVVER 磚 hello 存取面板中時，您應該取得自動登入 tooyour ZIVVER 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b925b-206">When you click hello ZIVVER tile in hello Access Panel, you should get automatically signed-on tooyour ZIVVER application.</span></span>
<span data-ttu-id="b925b-207">如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="b925b-207">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b925b-208">其他資源</span><span class="sxs-lookup"><span data-stu-id="b925b-208">Additional resources</span></span>

* [<span data-ttu-id="b925b-209">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b925b-209">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b925b-210">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="b925b-210">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_203.png

