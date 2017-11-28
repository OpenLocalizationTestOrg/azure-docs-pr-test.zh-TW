---
title: "教學課程：Azure Active Directory 與 Help Scout 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與協助 Scout 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0aad9910-0bc1-4394-9f73-267cf39973ab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: jeedes
ms.openlocfilehash: 58edd140eb1eb5980796ca743b5f7acd891729a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-help-scout"></a><span data-ttu-id="ee9ec-103">教學課程：Azure Active Directory 與 Help Scout 整合</span><span class="sxs-lookup"><span data-stu-id="ee9ec-103">Tutorial: Azure Active Directory integration with Help Scout</span></span>

<span data-ttu-id="ee9ec-104">在本教學課程中，您學習如何 toointegrate 協助搜索與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-104">In this tutorial, you learn how toointegrate Help Scout with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ee9ec-105">您會收到 hello 協助 Scout 整合與 Azure AD 中的下列優點：</span><span class="sxs-lookup"><span data-stu-id="ee9ec-105">You get hello following benefits from integrating Help Scout with Azure AD:</span></span>

- <span data-ttu-id="ee9ec-106">在 Azure AD 中，您可以控制誰可以存取 tooHelp Scout。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-106">In Azure AD, you can control who has access tooHelp Scout.</span></span>
- <span data-ttu-id="ee9ec-107">您可以自動登入您的使用者 tooHelp Scout 使用單一登入和使用者的 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-107">You can automatically sign in your users tooHelp Scout by using single sign-on and a user's Azure AD account.</span></span>
- <span data-ttu-id="ee9ec-108">您可以管理您的帳戶，在一個集中位置，hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-108">You can manage your accounts in one, central location, hello Azure portal.</span></span>

<span data-ttu-id="ee9ec-109">toolearn 進一步了解軟體即服務 (SaaS) 應用程式與 Azure AD 整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory？](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-109">toolearn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ee9ec-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="ee9ec-110">Prerequisites</span></span>

<span data-ttu-id="ee9ec-111">Azure AD 整合，以協助搜索 tooset，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="ee9ec-111">tooset up Azure AD integration with Help Scout, you need hello following items:</span></span>

- <span data-ttu-id="ee9ec-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ee9ec-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ee9ec-113">Help Scout 訂用帳戶，並開啟單一登入</span><span class="sxs-lookup"><span data-stu-id="ee9ec-113">A Help Scout subscription, with single sign-on turned on</span></span> 

> [!NOTE]
> <span data-ttu-id="ee9ec-114">如果您在測試 hello 步驟在本教學課程，我們建議您不要在生產環境中測試它們。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-114">If you test hello steps in this tutorial, we recommend that you don't test them in a production environment.</span></span>

<span data-ttu-id="ee9ec-115">測試本教學課程中的 hello 步驟建議：</span><span class="sxs-lookup"><span data-stu-id="ee9ec-115">Recommendations for testing hello steps in this tutorial:</span></span>

- <span data-ttu-id="ee9ec-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-116">Do not use your production environment, unless it's necessary.</span></span>
- <span data-ttu-id="ee9ec-117">如果您沒有 Azure AD 試用環境，可以[取得一個月的免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-117">If you don't have an Azure AD trial environment, you can [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ee9ec-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="ee9ec-118">Scenario description</span></span>
<span data-ttu-id="ee9ec-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="ee9ec-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="ee9ec-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ee9ec-121">從 hello 圖庫新增協助搜索。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-121">Add Help Scout from hello gallery.</span></span>
2. <span data-ttu-id="ee9ec-122">設定和測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-122">Set up and test Azure AD single sign-on.</span></span>

## <a name="add-help-scout-from-hello-gallery"></a><span data-ttu-id="ee9ec-123">從 hello 圖庫新增協助 Scout</span><span class="sxs-lookup"><span data-stu-id="ee9ec-123">Add Help Scout from hello gallery</span></span>
<span data-ttu-id="ee9ec-124">協助 Scout 與 Azure AD，hello 圖庫中的 hello 整合 tooset 協助 Scout tooyour 之新增受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-124">tooset up hello integration of Help Scout with Azure AD, in hello gallery, add Help Scout tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ee9ec-125">tooadd 協助 Scout 從 hello 組件庫：</span><span class="sxs-lookup"><span data-stu-id="ee9ec-125">tooadd Help Scout from hello gallery:</span></span>

1. <span data-ttu-id="ee9ec-126">在 hello [Azure 入口網站](https://portal.azure.com)，在 hello 左側的功能表中選取**Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-126">In hello [Azure portal](https://portal.azure.com), in hello left menu, select **Azure Active Directory**.</span></span> 

    ![hello Azure Active Directory 按鈕][1]

2. <span data-ttu-id="ee9ec-128">選取 [企業應用程式]，然後選取 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![hello 企業應用程式 頁面][2]
    
3. <span data-ttu-id="ee9ec-130">tooadd 新的應用程式中，選取**新的應用程式**。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-130">tooadd a new application, select **New application**.</span></span>

    ![hello 新應用程式按鈕][3]

4. <span data-ttu-id="ee9ec-132">在 [hello] 搜尋方塊中，輸入**協助 Scout**。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-132">In hello search box, enter **Help Scout**.</span></span> <span data-ttu-id="ee9ec-133">在 hello 搜尋結果中，選取 **協助 Scout**，然後選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-133">In hello search results, select **Help Scout**, and then select **Add**.</span></span>

    ![協助 Scout hello [結果] 清單中](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_addfromgallery.png)

## <a name="set-up-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ee9ec-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ee9ec-135">Set up and test Azure AD single sign-on</span></span>

<span data-ttu-id="ee9ec-136">在本節中，您會以名為 Britta Simon 的測試使用者作為基礎，設定及測試與 Help Scout 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-136">In this section, you set up and test Azure AD single sign-on with Help Scout based on a test user named *Britta Simon*.</span></span>

<span data-ttu-id="ee9ec-137">Azure AD 單一登入 toowork，需要 tooknow hello Azure AD 中協助搜索的對等項目的使用者。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-137">For single sign-on toowork, Azure AD needs tooknow hello Azure AD counterpart user in Help Scout.</span></span> <span data-ttu-id="ee9ec-138">必須先建立 Azure AD 使用者與協助 Scout 中的 hello 相關的使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-138">A link relationship between an Azure AD user and hello related user in Help Scout must be established.</span></span>

<span data-ttu-id="ee9ec-139">tooestablish hello 連結關聯性，以協助搜索，適用於**Username**，hello hello 值指派**使用者名**在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-139">tooestablish hello link relationship, in Help Scout, for **Username**, assign hello value of hello **user name** in Azure AD.</span></span>

<span data-ttu-id="ee9ec-140">tooconfigure 和測試 Azure AD 單一登入以協助搜索，完成下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="ee9ec-140">tooconfigure and test Azure AD single sign-on with Help Scout, complete hello following tasks:</span></span>

1. <span data-ttu-id="ee9ec-141">[設定 Azure AD 單一登入](#set-up-azure-ad-single-sign-on)。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-141">[Set up Azure AD single sign-on](#set-up-azure-ad-single-sign-on).</span></span> <span data-ttu-id="ee9ec-142">設定使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-142">Sets up a user toouse this feature.</span></span>
2. <span data-ttu-id="ee9ec-143">[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-143">[Create an Azure AD test user](#create-an-azure-ad-test-user).</span></span> <span data-ttu-id="ee9ec-144">測試 Azure AD 單一登入與 hello 使用者許 Simon。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-144">Tests Azure AD single sign-on with hello user Britta Simon.</span></span>
3. <span data-ttu-id="ee9ec-145">[建立 Help Scout 測試使用者](#create-a-help-scout-test-user)。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-145">[Create a Help Scout test user](#create-a-help-scout-test-user).</span></span> <span data-ttu-id="ee9ec-146">協助 Scout 是連結的 toohello hello 使用者表示 Azure AD 中建立許 Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-146">Creates a counterpart of Britta Simon in Help Scout that is linked toohello Azure AD representation of hello user.</span></span>
4. <span data-ttu-id="ee9ec-147">[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-147">[Assign hello Azure AD test user](#assign-the-azure-ad-test-user).</span></span> <span data-ttu-id="ee9ec-148">設定 Azure AD 單一登入許 Simon toouse。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-148">Sets up Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ee9ec-149">[測試單一登入](#test-single-sign-on)。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-149">[Test single sign-on](#test-single-sign-on).</span></span> <span data-ttu-id="ee9ec-150">請確認該 hello 設定可正常運作。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-150">Verifies that hello configuration works.</span></span>

### <a name="set-up-azure-ad-single-sign-on"></a><span data-ttu-id="ee9ec-151">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ee9ec-151">Set up Azure AD single sign-on</span></span>

<span data-ttu-id="ee9ec-152">在本節中，您設定 Azure AD 單一登入 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-152">In this section, you set up Azure AD single sign-on in hello Azure portal.</span></span> <span data-ttu-id="ee9ec-153">然後，您要在 Help Scout 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-153">Then, you set up single sign-on in your Help Scout application.</span></span>

<span data-ttu-id="ee9ec-154">Azure AD 單一登入以協助搜索 tooset:</span><span class="sxs-lookup"><span data-stu-id="ee9ec-154">tooset up Azure AD single sign-on with Help Scout:</span></span>

1. <span data-ttu-id="ee9ec-155">在 Azure 入口網站上 hello hello**協助 Scout**應用程式整合頁面上，選取**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-155">In hello Azure portal, on hello **Help Scout** application integration page, select **Single sign-on**.</span></span>
 
    ![設定單一登入連結][4]

2. <span data-ttu-id="ee9ec-157">在 hello**單一登入** 頁面上，針對**模式**，選取**SAML 型登入**。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-157">On hello **Single sign-on** page, for **Mode**, select **SAML-based Sign-on**.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_samlbase.png)

3. <span data-ttu-id="ee9ec-159">在下**協助 Scout 網域和 Url**，如果您想 tooset hello 應用程式在 IDP 初始化模式中，完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="ee9ec-159">Under **Help Scout Domain and URLs**, if you want tooset up hello application in IDP-initiated mode, complete hello following steps:</span></span>

    1. <span data-ttu-id="ee9ec-160">在 hello**識別碼**方塊中，輸入 URL，其中具有 hello 下列模式：`urn:auth0:helpscout:<instancename>`</span><span class="sxs-lookup"><span data-stu-id="ee9ec-160">In hello **Identifier** box, enter a URL that has hello following pattern: `urn:auth0:helpscout:<instancename>`</span></span>

    2. <span data-ttu-id="ee9ec-161">在 hello**回覆 URL**方塊中，輸入 URL，其中具有 hello 下列模式：`https://helpscout.auth0.com/login/callback?connection=<instancename>`</span><span class="sxs-lookup"><span data-stu-id="ee9ec-161">In hello **Reply URL** box, enter a URL that has hello following pattern: `https://helpscout.auth0.com/login/callback?connection=<instancename>`</span></span>

    ![Help Scout 網域與 URL 單一登入資訊](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url.png)

4. <span data-ttu-id="ee9ec-163">如果您想 tooset hello 應用程式在 SP 初始模式中，選取 hello**顯示進階的 URL 設定**核取方塊，並執行再 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="ee9ec-163">If you want tooset up hello application in SP-initiated mode, select hello **Show advanced URL settings** check box, and then do hello following:</span></span>

    * <span data-ttu-id="ee9ec-164">在 hello**登入 URL**方塊中，輸入 URL，其中具有下列格式的 hello:`https://secure.helpscout.net/members/login/`</span><span class="sxs-lookup"><span data-stu-id="ee9ec-164">In hello **Sign on URL** box, enter a URL that has hello following format: `https://secure.helpscout.net/members/login/`</span></span>

    ![Help Scout 網域與 URL 單一登入資訊](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url1.png)
 
    > [!NOTE] 
    > <span data-ttu-id="ee9ec-166">這些 Url 中的 hello 值為僅供示範之。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-166">hello values in these URLs are for demonstration only.</span></span> <span data-ttu-id="ee9ec-167">更新 hello 值與 hello 實際的識別項 URL 和回覆 URL。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-167">Update hello values with hello actual identifier URL and reply URL.</span></span> <span data-ttu-id="ee9ec-168">tooget 這些值，請連絡[協助 Scout 支援小組](mailto:help@helpscout.com)。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-168">tooget these values, contact [Help Scout support team](mailto:help@helpscout.com).</span></span> 

5. <span data-ttu-id="ee9ec-169">在下**SAML 簽章憑證**，選取**中繼資料 XML**，然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-169">Under **SAML Signing Certificate**, select **Metadata XML**, and then save hello metadata file on your computer.</span></span>

    ![hello 憑證下載連結](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_certificate.png) 

6. <span data-ttu-id="ee9ec-171">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-171">Select **Save**.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-helpscout-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="ee9ec-173">tooset 設定單一登入 hello 協助 Scout 端、 傳送嗨下載中繼資料 XML 檔案 toohello[協助 Scout 支援小組](mailto:help@helpscout.com)。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-173">tooset up single sign-on on hello Help Scout side, send hello downloaded metadata XML file toohello [Help Scout support team](mailto:help@helpscout.com).</span></span> <span data-ttu-id="ee9ec-174">hello 協助 Scout 支援小組適用於這項設定，以便雙方 hello SAML 單一登入連接已正確設定。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-174">hello Help Scout support team applies this setting so that hello SAML single sign-on connection is set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="ee9ec-175">您可以讀取這些指示 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定您的應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="ee9ec-175">You can read a concise version of these instructions in hello [Azure portal](https://portal.azure.com), while you are setting up your app!</span></span> <span data-ttu-id="ee9ec-176">選取 [新增 hello 應用程式之後**Active Directory** > **企業應用程式**，選取 hello**單一登入**] 索引標籤。您可以存取 hello 內嵌文件以 hello**組態**區段中的，在 hello hello 頁面底部。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-176">After you add hello app by selecting **Active Directory** > **Enterprise Applications**, select hello **Single Sign-On** tab. You can access hello embedded documentation in hello **Configuration** section, at hello bottom of hello page.</span></span> <span data-ttu-id="ee9ec-177">如需詳細資訊，請參閱 [Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-177">For more information, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ee9ec-178">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ee9ec-178">Create an Azure AD test user</span></span>

<span data-ttu-id="ee9ec-179">在本節中的 hello Azure 入口網站，您會建立名為許 Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-179">In this section, in hello Azure portal, you create a test user named Britta Simon.</span></span>

![建立 Azure AD 測試使用者][100]

<span data-ttu-id="ee9ec-181">toocreate 在 Azure AD 中的測試使用者：</span><span class="sxs-lookup"><span data-stu-id="ee9ec-181">toocreate a test user in Azure AD:</span></span>

1. <span data-ttu-id="ee9ec-182">在 hello Azure 入口網站，在 hello 左功能表中，選取  **Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-182">In hello Azure portal, in hello left menu, select **Azure Active Directory**.</span></span>

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-helpscout-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="ee9ec-184">toodisplay hello 使用者清單，選取**使用者和群組**，然後選取**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-184">toodisplay hello list of users, select **Users and groups**, and then select **All users**.</span></span>

    ![選取 [使用者和群組]，然後選取 [所有使用者]](./media/active-directory-saas-helpscout-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="ee9ec-186">tooopen hello**使用者**對話方塊頂端的 hello hello**所有使用者**頁面上，選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-186">tooopen hello **User** dialog box, at hello top of hello **All Users** page, select **Add**.</span></span>

    ![hello [新增] 按鈕](./media/active-directory-saas-helpscout-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="ee9ec-188">在 hello**使用者**對話方塊中，完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="ee9ec-188">In hello **User** dialog box, complete hello following steps:</span></span>

    1. <span data-ttu-id="ee9ec-189">在 hello**名稱**方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-189">In hello **Name** box, enter **BrittaSimon**.</span></span>

    2. <span data-ttu-id="ee9ec-190">在 hello**使用者名**方塊中，輸入使用者許 Simon hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-190">In hello **User name** box, enter hello email address of user Britta Simon.</span></span>

    3. <span data-ttu-id="ee9ec-191">選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 hello**密碼**方塊。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    4. <span data-ttu-id="ee9ec-192">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-192">Select **Create**.</span></span>

        ![hello [使用者] 對話方塊](./media/active-directory-saas-helpscout-tutorial/create_aaduser_04.png)

 
### <a name="create-a-help-scout-test-user"></a><span data-ttu-id="ee9ec-194">建立 Help Scout 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ee9ec-194">Create a Help Scout test user</span></span>

<span data-ttu-id="ee9ec-195">本章節的 hello 物件是 toocreate 名為許 Simon 協助 Scout 中的使用者。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-195">hello object of this section is toocreate a user named Britta Simon in Help Scout.</span></span> <span data-ttu-id="ee9ec-196">Help Scout 支援預設啟用的 Just-In-Time (JIT) 佈建。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-196">Help Scout supports just-in-time (JIT) provisioning, which is turned on by default.</span></span>

<span data-ttu-id="ee9ec-197">在本節中，沒有任何動作或工作 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-197">In this section, there's no action or task toocomplete.</span></span> <span data-ttu-id="ee9ec-198">如果使用者不存在於協助 Scout，當您嘗試 tooaccess 協助 Scout 被建立一個新。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-198">If a user doesn't already exist in Help Scout, a new one is created when you attempt tooaccess Help Scout.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="ee9ec-199">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ee9ec-199">Assign hello Azure AD test user</span></span>

<span data-ttu-id="ee9ec-200">在本節中，您允許 hello 使用者許 Simon toouse Azure AD 單一登入授與 hello 使用者帳戶存取 tooHelp Scout。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-200">In this section, you allow hello user Britta Simon toouse Azure AD single sign-on by granting hello user account access tooHelp Scout.</span></span>

![指派 hello 使用者角色][200] 

<span data-ttu-id="ee9ec-202">tooassign 許 Simon tooHelp Scout:</span><span class="sxs-lookup"><span data-stu-id="ee9ec-202">tooassign Britta Simon tooHelp Scout:</span></span>

1. <span data-ttu-id="ee9ec-203">在 hello Azure 入口網站，開啟 hello 應用程式檢視，並前往 toohello 目錄檢視。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-203">In hello Azure portal, open hello applications view, and then go toohello directory view.</span></span> <span data-ttu-id="ee9ec-204">選取 [企業應用程式]，然後選取 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-204">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="ee9ec-206">在 [hello] 應用程式清單中，選取**協助 Scout**。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-206">In hello applications list, select **Help Scout**.</span></span>

    ![hello 應用程式清單中的 hello 協助 Scout 連結](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_app.png)  

3. <span data-ttu-id="ee9ec-208">在 hello 左窗格中，選取 **使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-208">In hello left menu, select **Users and groups**.</span></span>

    ![hello 使用者和群組連結][202]

4. <span data-ttu-id="ee9ec-210">選取 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-210">Select **Add**.</span></span> <span data-ttu-id="ee9ec-211">然後，在 hello**將作業加入**頁面上，選取**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-211">Then, on hello **Add Assignment** page, select **Users and groups**.</span></span>

    ![hello 將作業加入窗格][203]

5. <span data-ttu-id="ee9ec-213">在 hello**使用者和群組**頁面 hello 清單中的使用者，選取**許 Simon**。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-213">On hello **Users and groups** page, in hello list of users, select **Britta Simon**.</span></span>

6. <span data-ttu-id="ee9ec-214">在 hello**使用者和群組**頁面上，選取**選取**。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-214">On hello **Users and groups** page, select **Select**.</span></span>

7. <span data-ttu-id="ee9ec-215">在 hello**將作業加入**頁面上，選取**指派**。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-215">On hello **Add Assignment** page, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ee9ec-216">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="ee9ec-216">Test single sign-on</span></span>

<span data-ttu-id="ee9ec-217">在本節中，您測試您 Azure AD 單一登入組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-217">In this section, you test your Azure AD single sign-on configuration by using hello access panel.</span></span>

<span data-ttu-id="ee9ec-218">當您選取 hello 協助 Scout 磚 hello 存取面板中時，您應該會自動登入 tooyour 協助 Scout 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-218">When you select hello Help Scout tile in hello access panel, you should be automatically signed in tooyour Help Scout application.</span></span>

<span data-ttu-id="ee9ec-219">如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="ee9ec-219">For more information about the access panel, see [Introduction toohello access panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ee9ec-220">其他資源</span><span class="sxs-lookup"><span data-stu-id="ee9ec-220">Additional resources</span></span>

* [<span data-ttu-id="ee9ec-221">如何教學課程清單 toointegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ee9ec-221">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ee9ec-222">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="ee9ec-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_203.png

