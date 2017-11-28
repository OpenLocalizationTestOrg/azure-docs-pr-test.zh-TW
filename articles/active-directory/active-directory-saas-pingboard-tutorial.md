---
title: "教學課程：Azure Active Directory 與 Pingboard 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Pingboard 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 0a916b1f9ef32d8124aa11284d2115bb4fc0bbc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pingboard"></a><span data-ttu-id="cbde3-103">教學課程：Azure Active Directory 與 Pingboard 整合</span><span class="sxs-lookup"><span data-stu-id="cbde3-103">Tutorial: Azure Active Directory integration with Pingboard</span></span>

<span data-ttu-id="cbde3-104">在此教學課程中，您學會如何 toointegrate Pingboard 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="cbde3-104">In this tutorial, you learn how toointegrate Pingboard with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cbde3-105">與 Azure AD 整合 Pingboard 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="cbde3-105">Integrating Pingboard with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cbde3-106">您可以控制存取 tooPingboard Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="cbde3-106">You can control in Azure AD who has access tooPingboard</span></span>
- <span data-ttu-id="cbde3-107">您可以啟用您的使用者 tooautomatically get 登入 tooPingboard （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="cbde3-107">You can enable your users tooautomatically get signed-on tooPingboard (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cbde3-108">您可以管理您的帳戶，在單一中央位置-hello Azure 管理入口網站</span><span class="sxs-lookup"><span data-stu-id="cbde3-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="cbde3-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="cbde3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cbde3-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="cbde3-110">Prerequisites</span></span>

<span data-ttu-id="cbde3-111">tooconfigure Pingboard 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="cbde3-111">tooconfigure Azure AD integration with Pingboard, you need hello following items:</span></span>

- <span data-ttu-id="cbde3-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="cbde3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cbde3-113">已啟用 Pingboard 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="cbde3-113">A Pingboard single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cbde3-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="cbde3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cbde3-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="cbde3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cbde3-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="cbde3-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="cbde3-117">如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="cbde3-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cbde3-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="cbde3-118">Scenario description</span></span>
<span data-ttu-id="cbde3-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cbde3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cbde3-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="cbde3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cbde3-121">從 hello 圖庫加入 Pingboard</span><span class="sxs-lookup"><span data-stu-id="cbde3-121">Adding Pingboard from hello gallery</span></span>
2. <span data-ttu-id="cbde3-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="cbde3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pingboard-from-hello-gallery"></a><span data-ttu-id="cbde3-123">從 hello 圖庫加入 Pingboard</span><span class="sxs-lookup"><span data-stu-id="cbde3-123">Adding Pingboard from hello gallery</span></span>
<span data-ttu-id="cbde3-124">tooconfigure hello 整合 Pingboard 到 Azure AD，您需要 tooadd Pingboard hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cbde3-124">tooconfigure hello integration of Pingboard into Azure AD, you need tooadd Pingboard from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cbde3-125">**tooadd Pingboard 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="cbde3-125">**tooadd Pingboard from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cbde3-126">在 hello  **[Azure 管理入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="cbde3-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cbde3-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="cbde3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cbde3-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="cbde3-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="cbde3-131">按一下**新增**上 hello hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="cbde3-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="cbde3-133">在 [hello] 搜尋方塊中，輸入**Pingboard**。</span><span class="sxs-lookup"><span data-stu-id="cbde3-133">In hello search box, type **Pingboard**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_search.png)

5. <span data-ttu-id="cbde3-135">在 hello 結果 窗格中，選取  **Pingboard**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cbde3-135">In hello results panel, select **Pingboard**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cbde3-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="cbde3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cbde3-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Pingboard 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cbde3-138">In this section, you configure and test Azure AD single sign-on with Pingboard based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cbde3-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Pingboard 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="cbde3-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Pingboard is tooa user in Azure AD.</span></span> <span data-ttu-id="cbde3-140">換句話說，Azure AD 使用者與 hello Pingboard 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="cbde3-140">In other words, a link relationship between an Azure AD user and hello related user in Pingboard needs toobe established.</span></span>

<span data-ttu-id="cbde3-141">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Pingboard 中。</span><span class="sxs-lookup"><span data-stu-id="cbde3-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Pingboard.</span></span>

<span data-ttu-id="cbde3-142">tooconfigure 及 Pingboard 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="cbde3-142">tooconfigure and test Azure AD single sign-on with Pingboard, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cbde3-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="cbde3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cbde3-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="cbde3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cbde3-145">**[建立測試使用者 Pingboard](#creating-a-pingboard-test-user)**  -toohave 許 Simon 是連結的 toohello Azure AD 表示她的 Pingboard 中對應項目。</span><span class="sxs-lookup"><span data-stu-id="cbde3-145">**[Creating a Pingboard test user](#creating-a-pingboard-test-user)** - toohave a counterpart of Britta Simon in Pingboard that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="cbde3-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cbde3-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cbde3-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="cbde3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cbde3-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="cbde3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cbde3-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 管理入口網站中，並 Pingboard 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="cbde3-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Pingboard application.</span></span>

<span data-ttu-id="cbde3-150">**tooconfigure Azure AD 單一登入與 Pingboard，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="cbde3-150">**tooconfigure Azure AD single sign-on with Pingboard, perform hello following steps:**</span></span>

1. <span data-ttu-id="cbde3-151">在 hello Azure 管理入口網站上 hello **Pingboard**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="cbde3-151">In hello Azure Management portal, on hello **Pingboard** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="cbde3-153">在 [hello**單一登入**] 對話方塊中，做為**模式**選取**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cbde3-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_samlbase.png)

3. <span data-ttu-id="cbde3-155">在 hello **Pingboard 網域和 Url**區段中，執行下列步驟，如果您想 tooconfigure hello 應用程式中的 hello **IDP**初始模式：</span><span class="sxs-lookup"><span data-stu-id="cbde3-155">On hello **Pingboard Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_url.png)

    <span data-ttu-id="cbde3-157">a.</span><span class="sxs-lookup"><span data-stu-id="cbde3-157">a.</span></span> <span data-ttu-id="cbde3-158">在 hello**識別碼**文字方塊中，做為型別 hello 值：`http://<entity-id>.pingboard.com/sp`</span><span class="sxs-lookup"><span data-stu-id="cbde3-158">In hello **Identifier** textbox, type hello value as: `http://<entity-id>.pingboard.com/sp`</span></span>

    <span data-ttu-id="cbde3-159">b.</span><span class="sxs-lookup"><span data-stu-id="cbde3-159">b.</span></span> <span data-ttu-id="cbde3-160">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<entity-id>.pingboard.com/auth/saml/consume`</span><span class="sxs-lookup"><span data-stu-id="cbde3-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<entity-id>.pingboard.com/auth/saml/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cbde3-161">請注意這些不是 hello 實際值。</span><span class="sxs-lookup"><span data-stu-id="cbde3-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="cbde3-162">您有 tooupdate hello 實際的識別項和回覆 url 的這些值。</span><span class="sxs-lookup"><span data-stu-id="cbde3-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="cbde3-163">這裡我們建議您 toouse hello 唯一字串的值在 hello 識別項。</span><span class="sxs-lookup"><span data-stu-id="cbde3-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="cbde3-164">請連絡[Pingboard 用戶端支援小組](https://support.pingboard.com/)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="cbde3-164">Contact [Pingboard Client support team](https://support.pingboard.com/) tooget these values.</span></span> 

4. <span data-ttu-id="cbde3-165">請檢查**顯示進階的 URL 設定**，如果您想 tooconfigure hello 應用程式中的**SP**初始模式：</span><span class="sxs-lookup"><span data-stu-id="cbde3-165">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_sp_initiated01.png)

    <span data-ttu-id="cbde3-167">a.</span><span class="sxs-lookup"><span data-stu-id="cbde3-167">a.</span></span> <span data-ttu-id="cbde3-168">在 hello**登入 URL**文字方塊中，做為型別 hello 值：`http://<sub-domain>.pingboard.com/sign_in`</span><span class="sxs-lookup"><span data-stu-id="cbde3-168">In hello **Sign-on URL** textbox, type hello value as: `http://<sub-domain>.pingboard.com/sign_in`</span></span>
     
5. <span data-ttu-id="cbde3-169">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="cbde3-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_certificate.png) 

6. <span data-ttu-id="cbde3-171">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="cbde3-171">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-pingboard-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="cbde3-173">tooconfigure SSO Pingboard 端開啟新的瀏覽器視窗，並登入 tooyour Pingboard 帳戶。</span><span class="sxs-lookup"><span data-stu-id="cbde3-173">tooconfigure SSO on Pingboard side, open a new browser window and log in tooyour Pingboard Account.</span></span> <span data-ttu-id="cbde3-174">您必須是 Pingboard admin tooset 設定單一登上。</span><span class="sxs-lookup"><span data-stu-id="cbde3-174">You must be a Pingboard admin tooset up single sign on.</span></span>

8. <span data-ttu-id="cbde3-175">從 hello 上方的功能表選取**應用程式 > 整合**</span><span class="sxs-lookup"><span data-stu-id="cbde3-175">From hello top menu select **Apps > Integrations**</span></span>

    ![設定單一登入](./media/active-directory-saas-pingboard-tutorial/Pingboard_integration.png)

9.  <span data-ttu-id="cbde3-177">在 hello**整合**頁面上，尋找 hello **"Azure Active Directory"**磚，然後按一下它。</span><span class="sxs-lookup"><span data-stu-id="cbde3-177">On hello **Integrations** page, find hello **"Azure Active Directory"** tile, and click it.</span></span>

    ![設定單一登入](./media/active-directory-saas-pingboard-tutorial/Pingboard_aad.png)

10. <span data-ttu-id="cbde3-179">在 hello 強制回應之後按一下**「 設定 」**</span><span class="sxs-lookup"><span data-stu-id="cbde3-179">In hello modal that follows click **"Configure"**</span></span>

    ![設定單一登入](./media/active-directory-saas-pingboard-tutorial/Pingboard_configure.png)

11. <span data-ttu-id="cbde3-181">在 hello 遵循頁面上，您會發現 「 Azure SSO 整合會啟用。 」。</span><span class="sxs-lookup"><span data-stu-id="cbde3-181">On hello following page, you will notice that "Azure SSO Integration is enabled.".</span></span> <span data-ttu-id="cbde3-182">開啟 hello 下載中繼資料 XML 檔案中的內容 記事本 和 貼上 hello **IDP 中繼資料**。</span><span class="sxs-lookup"><span data-stu-id="cbde3-182">Open hello downloaded Metadata XML file in a notepad and paste hello content in **IDP Metadata**.</span></span>

    ![設定單一登入](./media/active-directory-saas-pingboard-tutorial/Pingboard_sso_configure.png)

12. <span data-ttu-id="cbde3-184">將驗證 hello 檔案，且現在會啟用單一登入的所有項目是否正確，</span><span class="sxs-lookup"><span data-stu-id="cbde3-184">hello file will be validated, and if everything is correct, single sign on will now be enabled</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cbde3-185">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="cbde3-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="cbde3-186">hello 本節目標在於 toocreate 呼叫許 Simon hello Azure 管理入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="cbde3-186">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="cbde3-188">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="cbde3-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cbde3-189">在 hello **Azure 管理入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="cbde3-189">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pingboard-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cbde3-191">跳過**使用者和群組**按一下**所有使用者**toodisplay hello 使用者清單。</span><span class="sxs-lookup"><span data-stu-id="cbde3-191">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pingboard-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cbde3-193">在 hello hello 對話方塊頂端按一下**新增**tooopen hello**使用者**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="cbde3-193">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pingboard-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cbde3-195">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="cbde3-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pingboard-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cbde3-197">a.</span><span class="sxs-lookup"><span data-stu-id="cbde3-197">a.</span></span> <span data-ttu-id="cbde3-198">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="cbde3-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cbde3-199">b.</span><span class="sxs-lookup"><span data-stu-id="cbde3-199">b.</span></span> <span data-ttu-id="cbde3-200">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="cbde3-200">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cbde3-201">c.</span><span class="sxs-lookup"><span data-stu-id="cbde3-201">c.</span></span> <span data-ttu-id="cbde3-202">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="cbde3-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cbde3-203">d.</span><span class="sxs-lookup"><span data-stu-id="cbde3-203">d.</span></span> <span data-ttu-id="cbde3-204">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="cbde3-204">Click **Create**.</span></span>
 
### <a name="creating-a-pingboard-test-user"></a><span data-ttu-id="cbde3-205">建立 Pingboard 測試使用者</span><span class="sxs-lookup"><span data-stu-id="cbde3-205">Creating a Pingboard test user</span></span>

<span data-ttu-id="cbde3-206">在訂單 tooenable Azure AD 使用者 toolog Pingboard 成，它們必須佈建到 Pingboard。</span><span class="sxs-lookup"><span data-stu-id="cbde3-206">In order tooenable Azure AD users toolog into Pingboard, they must be provisioned into Pingboard.</span></span>  
<span data-ttu-id="cbde3-207">中的 Pingboard hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="cbde3-207">In hello case of Pingboard, provisioning is a manual task.</span></span>

<span data-ttu-id="cbde3-208">**tooprovision 使用者帳戶，執行下列步驟 hello:**</span><span class="sxs-lookup"><span data-stu-id="cbde3-208">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="cbde3-209">登入 tooyour Pingboard 公司網站的系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="cbde3-209">Log in tooyour Pingboard company site as an administrator.</span></span>

2. <span data-ttu-id="cbde3-210">按一下 [目錄] 頁面上的 [新增員工] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cbde3-210">Click **“Add Employee”** button on **Directory** page.</span></span>

    ![新增員工](./media/active-directory-saas-pingboard-tutorial/create_testuser_add.png)

3. <span data-ttu-id="cbde3-212">在 hello **"加入 Employee"**對話方塊頁面上，執行下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="cbde3-212">On hello **“Add Employee”** dialog page, perform hello following steps.</span></span>

    ![邀請人員](./media/active-directory-saas-pingboard-tutorial/create_testuser_name.png)

    <span data-ttu-id="cbde3-214">a.</span><span class="sxs-lookup"><span data-stu-id="cbde3-214">a.</span></span> <span data-ttu-id="cbde3-215">在 hello**全名**文字方塊中，類型許 Simon 的 hello 完整名稱。</span><span class="sxs-lookup"><span data-stu-id="cbde3-215">In hello **Full Name** textbox, type hello full name of Britta Simon.</span></span>

    <span data-ttu-id="cbde3-216">b.</span><span class="sxs-lookup"><span data-stu-id="cbde3-216">b.</span></span> <span data-ttu-id="cbde3-217">在 [hello**電子郵件**許 Simon 帳戶類型 hello 電子郵件地址] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="cbde3-217">In hello **Email** textbox, type hello email address of Britta Simon account.</span></span>

    <span data-ttu-id="cbde3-218">c.</span><span class="sxs-lookup"><span data-stu-id="cbde3-218">c.</span></span> <span data-ttu-id="cbde3-219">在 hello**職稱**文字方塊中，類型許 Simon 的 hello 職稱。</span><span class="sxs-lookup"><span data-stu-id="cbde3-219">In hello **Job Title** textbox, type hello job title of Britta Simon.</span></span>

    <span data-ttu-id="cbde3-220">d.</span><span class="sxs-lookup"><span data-stu-id="cbde3-220">d.</span></span> <span data-ttu-id="cbde3-221">在 hello**位置**下拉式清單中，選取 hello 許 Simon 位置。</span><span class="sxs-lookup"><span data-stu-id="cbde3-221">In hello **Location** dropdown, select hello location  of Britta Simon.</span></span>
    
    <span data-ttu-id="cbde3-222">e.</span><span class="sxs-lookup"><span data-stu-id="cbde3-222">e.</span></span> <span data-ttu-id="cbde3-223">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="cbde3-223">Click **Add**.</span></span>   

4. <span data-ttu-id="cbde3-224">確認畫面會出現 tooconfirm hello 加入的使用者。</span><span class="sxs-lookup"><span data-stu-id="cbde3-224">A confirmation screen will come up tooconfirm hello addition of user.</span></span>
    
    ![確認](./media/active-directory-saas-pingboard-tutorial/create_testuser_confirm.png)
        
    > [!NOTE]
    > <span data-ttu-id="cbde3-226">hello Azure Active Directory 帳戶持有者將收到一封電子郵件，並遵循連結 tooconfirm 他們的帳戶之前就會生效。</span><span class="sxs-lookup"><span data-stu-id="cbde3-226">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cbde3-227">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="cbde3-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cbde3-228">在本節中，您可以授與他們存取 tooPingboard 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cbde3-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooPingboard.</span></span>

![指派使用者][200] 

<span data-ttu-id="cbde3-230">**tooassign 許 Simon tooPingboard，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="cbde3-230">**tooassign Britta Simon tooPingboard, perform hello following steps:**</span></span>

1. <span data-ttu-id="cbde3-231">在 hello Azure 管理入口網站中，開啟 hello 應用程式 檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="cbde3-231">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="cbde3-233">在 [hello] 應用程式清單中，選取**Pingboard**。</span><span class="sxs-lookup"><span data-stu-id="cbde3-233">In hello applications list, select **Pingboard**.</span></span>

    ![設定單一登入](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_app.png) 

3. <span data-ttu-id="cbde3-235">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="cbde3-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="cbde3-237">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cbde3-237">Click **Add** button.</span></span> <span data-ttu-id="cbde3-238">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="cbde3-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="cbde3-240">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="cbde3-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cbde3-241">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cbde3-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cbde3-242">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cbde3-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cbde3-243">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="cbde3-243">Testing single sign-on</span></span>

<span data-ttu-id="cbde3-244">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="cbde3-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cbde3-245">當您按一下 hello Pingboard 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Pingboard 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cbde3-245">When you click hello Pingboard tile in hello Access Panel, you should get automatically signed-on tooyour Pingboard application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cbde3-246">其他資源</span><span class="sxs-lookup"><span data-stu-id="cbde3-246">Additional resources</span></span>

* [<span data-ttu-id="cbde3-247">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cbde3-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cbde3-248">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="cbde3-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_203.png
