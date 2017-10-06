---
title: "教學課程：Azure Active Directory 與 Hightail 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Hightail 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e15206ac-74b0-46e4-9329-892c7d242ec0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 2b36fcf8d5773255fdf89de2dccdceb95c032bd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hightail"></a><span data-ttu-id="ce63b-103">教學課程：Azure Active Directory 與 Hightail 整合</span><span class="sxs-lookup"><span data-stu-id="ce63b-103">Tutorial: Azure Active Directory integration with Hightail</span></span>

<span data-ttu-id="ce63b-104">在此教學課程中，您學會如何 toointegrate Hightail 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="ce63b-104">In this tutorial, you learn how toointegrate Hightail with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ce63b-105">與 Azure AD 整合 Hightail 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="ce63b-105">Integrating Hightail with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ce63b-106">您可以控制存取 tooHightail Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="ce63b-106">You can control in Azure AD who has access tooHightail</span></span>
- <span data-ttu-id="ce63b-107">您可以啟用您的使用者 tooautomatically get 登入 tooHightail （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="ce63b-107">You can enable your users tooautomatically get signed-on tooHightail (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ce63b-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="ce63b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ce63b-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="ce63b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ce63b-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="ce63b-110">Prerequisites</span></span>

<span data-ttu-id="ce63b-111">tooconfigure Hightail 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="ce63b-111">tooconfigure Azure AD integration with Hightail, you need hello following items:</span></span>

- <span data-ttu-id="ce63b-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ce63b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ce63b-113">已啟用 Hightail 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ce63b-113">A Hightail single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ce63b-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="ce63b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ce63b-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="ce63b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ce63b-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="ce63b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ce63b-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="ce63b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ce63b-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="ce63b-118">Scenario description</span></span>
<span data-ttu-id="ce63b-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ce63b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ce63b-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="ce63b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ce63b-121">從 hello 圖庫加入 Hightail</span><span class="sxs-lookup"><span data-stu-id="ce63b-121">Adding Hightail from hello gallery</span></span>
2. <span data-ttu-id="ce63b-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ce63b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hightail-from-hello-gallery"></a><span data-ttu-id="ce63b-123">從 hello 圖庫加入 Hightail</span><span class="sxs-lookup"><span data-stu-id="ce63b-123">Adding Hightail from hello gallery</span></span>
<span data-ttu-id="ce63b-124">tooconfigure hello 整合 Hightail 到 Azure AD，您需要 tooadd Hightail hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ce63b-124">tooconfigure hello integration of Hightail into Azure AD, you need tooadd Hightail from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ce63b-125">**tooadd Hightail 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="ce63b-125">**tooadd Hightail from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ce63b-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="ce63b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ce63b-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="ce63b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ce63b-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="ce63b-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="ce63b-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="ce63b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="ce63b-133">在 [hello] 搜尋方塊中，輸入**Hightail**。</span><span class="sxs-lookup"><span data-stu-id="ce63b-133">In hello search box, type **Hightail**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_search.png)

5. <span data-ttu-id="ce63b-135">在 hello 結果 窗格中，選取  **Hightail**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ce63b-135">In hello results panel, select **Hightail**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ce63b-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ce63b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ce63b-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Hightail 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ce63b-138">In this section, you configure and test Azure AD single sign-on with Hightail based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ce63b-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Hightail 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="ce63b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Hightail is tooa user in Azure AD.</span></span> <span data-ttu-id="ce63b-140">換句話說，Azure AD 使用者與 hello Hightail 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="ce63b-140">In other words, a link relationship between an Azure AD user and hello related user in Hightail needs toobe established.</span></span>

<span data-ttu-id="ce63b-141">Hightail 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="ce63b-141">In Hightail, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ce63b-142">tooconfigure 及 Hightail 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="ce63b-142">tooconfigure and test Azure AD single sign-on with Hightail, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ce63b-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="ce63b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ce63b-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="ce63b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ce63b-145">**[建立測試使用者 Hightail](#creating-a-hightail-test-user)**  -toohave 許 Simon Hightail 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="ce63b-145">**[Creating a Hightail test user](#creating-a-hightail-test-user)** - toohave a counterpart of Britta Simon in Hightail that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ce63b-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ce63b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ce63b-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="ce63b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ce63b-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ce63b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ce63b-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Hightail 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="ce63b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Hightail application.</span></span>

<span data-ttu-id="ce63b-150">**tooconfigure Azure AD 單一登入與 Hightail，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="ce63b-150">**tooconfigure Azure AD single sign-on with Hightail, perform hello following steps:**</span></span>

1. <span data-ttu-id="ce63b-151">在 Azure 入口網站上 hello hello **Hightail**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="ce63b-151">In hello Azure portal, on hello **Hightail** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="ce63b-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ce63b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_samlbase.png)

3. <span data-ttu-id="ce63b-155">在 hello **Hightail 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="ce63b-155">On hello **Hightail Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url.png)

     <span data-ttu-id="ce63b-157">在 hello**回覆 URL**文字方塊中，做為型別 hello URL:`https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`</span><span class="sxs-lookup"><span data-stu-id="ce63b-157">In hello **Reply URL** textbox, type hello URL as: `https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ce63b-158">hello 上述值不是真正的價值。</span><span class="sxs-lookup"><span data-stu-id="ce63b-158">hello preceding value is not real value.</span></span> <span data-ttu-id="ce63b-159">您將會更新 hello 實際回覆 URL，在 hello 教學課程稍後會說明 hello 值。</span><span class="sxs-lookup"><span data-stu-id="ce63b-159">You will update hello value with hello actual Reply URL, which is explained later in hello tutorial.</span></span>
 
4. <span data-ttu-id="ce63b-160">在 hello **Hightail 網域和 Url**區段中，如果您想 tooconfigure hello 應用程式中的**SP 初始模式**，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="ce63b-160">On hello **Hightail Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![設定單一登入](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url1.png)

    <span data-ttu-id="ce63b-162">a.</span><span class="sxs-lookup"><span data-stu-id="ce63b-162">a.</span></span> <span data-ttu-id="ce63b-163">按一下 hello**顯示進階的 URL 設定**。</span><span class="sxs-lookup"><span data-stu-id="ce63b-163">Click hello **Show advanced URL settings**.</span></span>

    <span data-ttu-id="ce63b-164">b.</span><span class="sxs-lookup"><span data-stu-id="ce63b-164">b.</span></span> <span data-ttu-id="ce63b-165">在 hello**登入 URL**文字方塊中，做為型別 hello URL:`https://www.hightail.com/loginSSO`</span><span class="sxs-lookup"><span data-stu-id="ce63b-165">In hello **Sign On URL** textbox, type hello URL as: `https://www.hightail.com/loginSSO`</span></span>

4. <span data-ttu-id="ce63b-166">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="ce63b-166">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_certificate.png) 

5. <span data-ttu-id="ce63b-168">Hightail 應用程式特定的格式預期 hello SAML 判斷提示。</span><span class="sxs-lookup"><span data-stu-id="ce63b-168">Hightail application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="ce63b-169">請設定下列宣告為此應用程式的 hello。</span><span class="sxs-lookup"><span data-stu-id="ce63b-169">Please configure hello following claims for this application.</span></span> <span data-ttu-id="ce63b-170">您可以從 hello 管理這些屬性的 hello 值**」 屬性 「** hello 應用程式 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ce63b-170">You can manage hello values of these attributes from hello **"Atrribute"** tab of hello application.</span></span> <span data-ttu-id="ce63b-171">hello 下列螢幕擷取畫面會顯示這個範例。</span><span class="sxs-lookup"><span data-stu-id="ce63b-171">hello following screenshot shows an example for this.</span></span> 

    ![設定單一登入](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_attribute.png) 

6. <span data-ttu-id="ce63b-173">在 hello**使用者屬性**hello 區段**單一登入** 對話方塊中，hello 映像中所示設定 SAML 權杖屬性並執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="ce63b-173">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="ce63b-174">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="ce63b-174">Attribute Name</span></span> | <span data-ttu-id="ce63b-175">屬性值</span><span class="sxs-lookup"><span data-stu-id="ce63b-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="ce63b-176">名字</span><span class="sxs-lookup"><span data-stu-id="ce63b-176">FirstName</span></span> | <span data-ttu-id="ce63b-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="ce63b-177">user.givenname</span></span> |
    | <span data-ttu-id="ce63b-178">姓氏</span><span class="sxs-lookup"><span data-stu-id="ce63b-178">LastName</span></span> | <span data-ttu-id="ce63b-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="ce63b-179">user.surname</span></span> |
    | <span data-ttu-id="ce63b-180">電子郵件</span><span class="sxs-lookup"><span data-stu-id="ce63b-180">Email</span></span> | <span data-ttu-id="ce63b-181">user.mail</span><span class="sxs-lookup"><span data-stu-id="ce63b-181">user.mail</span></span> |    
    | <span data-ttu-id="ce63b-182">UserIdentity</span><span class="sxs-lookup"><span data-stu-id="ce63b-182">UserIdentity</span></span> | <span data-ttu-id="ce63b-183">user.mail</span><span class="sxs-lookup"><span data-stu-id="ce63b-183">user.mail</span></span> |
    
    <span data-ttu-id="ce63b-184">a.</span><span class="sxs-lookup"><span data-stu-id="ce63b-184">a.</span></span> <span data-ttu-id="ce63b-185">按一下**加入屬性**tooopen hello**加入屬性**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="ce63b-185">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_04.png)

    ![設定單一登入](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="ce63b-188">b.</span><span class="sxs-lookup"><span data-stu-id="ce63b-188">b.</span></span> <span data-ttu-id="ce63b-189">在 hello**名稱**文字方塊中，該資料列所顯示的型別 hello 屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="ce63b-189">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="ce63b-190">c.</span><span class="sxs-lookup"><span data-stu-id="ce63b-190">c.</span></span> <span data-ttu-id="ce63b-191">從 hello**值**清單，顯示該資料列的型別 hello 屬性值。</span><span class="sxs-lookup"><span data-stu-id="ce63b-191">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="ce63b-192">d.</span><span class="sxs-lookup"><span data-stu-id="ce63b-192">d.</span></span> <span data-ttu-id="ce63b-193">保留 hello**命名空間**空白。</span><span class="sxs-lookup"><span data-stu-id="ce63b-193">Leave hello **Namespace** blank.</span></span>
    
    <span data-ttu-id="ce63b-194">e.</span><span class="sxs-lookup"><span data-stu-id="ce63b-194">e.</span></span> <span data-ttu-id="ce63b-195">按一下 [ **確定**]。</span><span class="sxs-lookup"><span data-stu-id="ce63b-195">Click **Ok**.</span></span>

7. <span data-ttu-id="ce63b-196">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="ce63b-196">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-hightail-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="ce63b-198">在 hello **Hightail 組態**區段中，按一下**設定 Hightail** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="ce63b-198">On hello **Hightail Configuration** section, click **Configure Hightail** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ce63b-199">複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="ce63b-199">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_configure.png) 

    >[!NOTE] 
    ><span data-ttu-id="ce63b-201">請在 Hightail 應用程式中設定單一登入的 hello，允許清單，您的電子郵件網域 Hightail 小組，讓所有 hello 使用此網域的使用者可以使用單一登入功能。</span><span class="sxs-lookup"><span data-stu-id="ce63b-201">Before configuring hello Single Sign On at Hightail app, please white list your email domain with Hightail team so that all hello users who are using this domain can use Single Sign On functionality.</span></span>


9. <span data-ttu-id="ce63b-202">tooget SSO 設定應用程式，您需要 toosign 上 tooyour Hightail 租用戶系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="ce63b-202">tooget SSO configured for your application, you need toosign-on tooyour Hightail tenant as an administrator.</span></span>
   
    <span data-ttu-id="ce63b-203">a.</span><span class="sxs-lookup"><span data-stu-id="ce63b-203">a.</span></span> <span data-ttu-id="ce63b-204">在 hello 最上層顯示 hello 功能表上，按一下 hello**帳戶**索引標籤並選取**設定 SAML**。</span><span class="sxs-lookup"><span data-stu-id="ce63b-204">In hello menu on hello top, click hello **Account** tab and select **Configure SAML**.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_001.png) 

    <span data-ttu-id="ce63b-206">b.</span><span class="sxs-lookup"><span data-stu-id="ce63b-206">b.</span></span> <span data-ttu-id="ce63b-207">選取的 hello 核取方塊**啟用 SAML 驗證**。</span><span class="sxs-lookup"><span data-stu-id="ce63b-207">Select hello checkbox of **Enable SAML Authentication**.</span></span>

    ![設定單一登入](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_002.png) 

    <span data-ttu-id="ce63b-209">c.</span><span class="sxs-lookup"><span data-stu-id="ce63b-209">c.</span></span> <span data-ttu-id="ce63b-210">從 Azure 入口網站中，複製到剪貼簿，其內容的 hello 下載 [記事本] 中開啟 base-64 編碼的憑證，然後將它貼入 toohello **SAML 權杖簽署憑證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="ce63b-210">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **SAML Token Signing Certificate** textbox.</span></span>

    ![設定單一登入](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_003.png) 

    <span data-ttu-id="ce63b-212">d.</span><span class="sxs-lookup"><span data-stu-id="ce63b-212">d.</span></span> <span data-ttu-id="ce63b-213">在 hello **SAML 授權單位 （識別提供者）**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**從 Azure 入口網站複製。</span><span class="sxs-lookup"><span data-stu-id="ce63b-213">In hello **SAML Authority (Identity Provider)** textbox, paste hello value of **SAML Single Sign-On Service URL** copied from Azure portal.</span></span>

    ![設定單一登入](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_004.png)

    <span data-ttu-id="ce63b-215">e.</span><span class="sxs-lookup"><span data-stu-id="ce63b-215">e.</span></span> <span data-ttu-id="ce63b-216">如果您想 tooconfigure hello 應用程式中的**IDP 初始化模式**選取**「 身分識別提供者 (IdP) 起始登入 」**。</span><span class="sxs-lookup"><span data-stu-id="ce63b-216">If you wish tooconfigure hello application in **IDP initiated mode** select **"Identity Provider (IdP) initiated log in"**.</span></span> <span data-ttu-id="ce63b-217">若為 **SP 起始模式**，請選取 [服務提供者 (SP) 起始登入]。</span><span class="sxs-lookup"><span data-stu-id="ce63b-217">If **SP initiated mode** select **"Service Provider (SP) initiated log in"**.</span></span>

    ![設定單一登入](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_006.png)

    <span data-ttu-id="ce63b-219">f.</span><span class="sxs-lookup"><span data-stu-id="ce63b-219">f.</span></span> <span data-ttu-id="ce63b-220">複製您的執行個體的 hello SAML 取用者 URL 並貼上在**回覆 URL**  文字方塊中的**Hightail 網域和 Url** Azure 入口網站上的一節。</span><span class="sxs-lookup"><span data-stu-id="ce63b-220">Copy hello SAML consumer URL for your instance and paste it in **Reply URL** textbox in **Hightail Domain and URLs** section on Azure portal.</span></span>
    
    <span data-ttu-id="ce63b-221">g.</span><span class="sxs-lookup"><span data-stu-id="ce63b-221">g.</span></span> <span data-ttu-id="ce63b-222">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="ce63b-222">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="ce63b-223">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="ce63b-223">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ce63b-224">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="ce63b-224">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ce63b-225">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ce63b-225">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ce63b-226">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ce63b-226">Creating an Azure AD test user</span></span>
<span data-ttu-id="ce63b-227">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="ce63b-227">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="ce63b-229">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="ce63b-229">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ce63b-230">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="ce63b-230">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hightail-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ce63b-232">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="ce63b-232">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hightail-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ce63b-234">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="ce63b-234">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hightail-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ce63b-236">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="ce63b-236">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hightail-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ce63b-238">a.</span><span class="sxs-lookup"><span data-stu-id="ce63b-238">a.</span></span> <span data-ttu-id="ce63b-239">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="ce63b-239">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ce63b-240">b.</span><span class="sxs-lookup"><span data-stu-id="ce63b-240">b.</span></span> <span data-ttu-id="ce63b-241">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="ce63b-241">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ce63b-242">c.</span><span class="sxs-lookup"><span data-stu-id="ce63b-242">c.</span></span> <span data-ttu-id="ce63b-243">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="ce63b-243">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ce63b-244">d.</span><span class="sxs-lookup"><span data-stu-id="ce63b-244">d.</span></span> <span data-ttu-id="ce63b-245">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="ce63b-245">Click **Create**.</span></span>
 
### <a name="creating-a-hightail-test-user"></a><span data-ttu-id="ce63b-246">建立 Hightail 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ce63b-246">Creating a Hightail test user</span></span>

<span data-ttu-id="ce63b-247">hello 本節目標在於 toocreate Hightail 中呼叫許 Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="ce63b-247">hello objective of this section is toocreate a user called Britta Simon in Hightail.</span></span> 

<span data-ttu-id="ce63b-248">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="ce63b-248">There is no action item for you in this section.</span></span> <span data-ttu-id="ce63b-249">Hightail 中 just-in-time 使用者佈建以 hello 自訂宣告為基礎的支援。</span><span class="sxs-lookup"><span data-stu-id="ce63b-249">Hightail supports just-in-time user provisioning based on hello custom claims.</span></span> <span data-ttu-id="ce63b-250">如果您已設定 hello 自訂宣告，hello > 一節中所示**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)**以上所述，使用者會自動建立在 hello 應用程式不存在。</span><span class="sxs-lookup"><span data-stu-id="ce63b-250">If you have configured hello custom claims as shown in hello section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** above, a user is automatically created in hello application it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="ce63b-251">若要手動 toocreate 使用者，您需要 toocontact hello [Hightail 支援小組](mailto:support@hightail.com)。</span><span class="sxs-lookup"><span data-stu-id="ce63b-251">If you need toocreate a user manually, you need toocontact hello [Hightail support team](mailto:support@hightail.com).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ce63b-252">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="ce63b-252">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ce63b-253">在本節中，您可以授與存取 tooHightail 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ce63b-253">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHightail.</span></span>

![指派使用者][200] 

<span data-ttu-id="ce63b-255">**tooassign 許 Simon tooHightail，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="ce63b-255">**tooassign Britta Simon tooHightail, perform hello following steps:**</span></span>

1. <span data-ttu-id="ce63b-256">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="ce63b-256">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="ce63b-258">在 [hello] 應用程式清單中，選取**Hightail**。</span><span class="sxs-lookup"><span data-stu-id="ce63b-258">In hello applications list, select **Hightail**.</span></span>

    ![設定單一登入](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_app.png) 

3. <span data-ttu-id="ce63b-260">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="ce63b-260">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="ce63b-262">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ce63b-262">Click **Add** button.</span></span> <span data-ttu-id="ce63b-263">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="ce63b-263">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="ce63b-265">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="ce63b-265">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ce63b-266">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ce63b-266">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ce63b-267">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ce63b-267">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ce63b-268">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="ce63b-268">Testing single sign-on</span></span>

<span data-ttu-id="ce63b-269">hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="ce63b-269">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ce63b-270">當您按一下 hello Hightail 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Hightail 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ce63b-270">When you click hello Hightail tile in hello Access Panel, you should get automatically signed-on tooyour Hightail application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="ce63b-271">其他資源</span><span class="sxs-lookup"><span data-stu-id="ce63b-271">Additional resources</span></span>

* [<span data-ttu-id="ce63b-272">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ce63b-272">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ce63b-273">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="ce63b-273">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_203.png

