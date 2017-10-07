---
title: "教學課程：Azure Active Directory 與 TigerText Secure Messenger 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 TigerText 安全 Messenger 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 03f1e128-5bcb-4e49-b6a3-fe22eedc6d5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.openlocfilehash: a3d7bb9598658c75c567c15751740d885fe4fc27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tigertext-secure-messenger"></a><span data-ttu-id="04e38-103">教學課程：Azure Active Directory 與 TigerText Secure Messenger 整合</span><span class="sxs-lookup"><span data-stu-id="04e38-103">Tutorial: Azure Active Directory integration with TigerText Secure Messenger</span></span>

<span data-ttu-id="04e38-104">在此教學課程中，您學會如何 toointegrate TigerText Secure Messenger 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="04e38-104">In this tutorial, you learn how toointegrate TigerText Secure Messenger with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="04e38-105">與 Azure AD 整合 TigerText 安全 Messenger 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="04e38-105">Integrating TigerText Secure Messenger with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="04e38-106">您可以在 Azure AD 中擁有存取 tooTigerText 控制安全 Messenger</span><span class="sxs-lookup"><span data-stu-id="04e38-106">You can control in Azure AD who has access tooTigerText Secure Messenger</span></span>
- <span data-ttu-id="04e38-107">您可以啟用您的使用者 tooautomatically get 登入 tooTigerText 安全 Messenger （單一登入） 其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="04e38-107">You can enable your users tooautomatically get signed-on tooTigerText Secure Messenger (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="04e38-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="04e38-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="04e38-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="04e38-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="04e38-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="04e38-110">Prerequisites</span></span>

<span data-ttu-id="04e38-111">tooconfigure TigerText 安全 Messenger 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="04e38-111">tooconfigure Azure AD integration with TigerText Secure Messenger, you need hello following items:</span></span>

- <span data-ttu-id="04e38-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="04e38-112">An Azure AD subscription</span></span>
- <span data-ttu-id="04e38-113">已啟用 TigerText Secure Messenger 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="04e38-113">A TigerText Secure Messenger single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="04e38-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="04e38-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="04e38-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="04e38-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="04e38-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="04e38-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="04e38-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="04e38-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="04e38-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="04e38-118">Scenario description</span></span>
<span data-ttu-id="04e38-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="04e38-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="04e38-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="04e38-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="04e38-121">從 hello 圖庫新增 TigerText 安全 Messenger</span><span class="sxs-lookup"><span data-stu-id="04e38-121">Add TigerText Secure Messenger from hello gallery</span></span>
2. <span data-ttu-id="04e38-122">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="04e38-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tigertext-secure-messenger-from-hello-gallery"></a><span data-ttu-id="04e38-123">從 hello 圖庫新增 TigerText 安全 Messenger</span><span class="sxs-lookup"><span data-stu-id="04e38-123">Add TigerText Secure Messenger from hello gallery</span></span>
<span data-ttu-id="04e38-124">tooconfigure hello 整合 TigerText 安全 Messenger 到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd TigerText 安全 Messenger。</span><span class="sxs-lookup"><span data-stu-id="04e38-124">tooconfigure hello integration of TigerText Secure Messenger into Azure AD, you need tooadd TigerText Secure Messenger from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="04e38-125">**tooadd TigerText 安全 Messenger 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="04e38-125">**tooadd TigerText Secure Messenger from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="04e38-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="04e38-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="04e38-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="04e38-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="04e38-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="04e38-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="04e38-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="04e38-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="04e38-133">在 hello 搜尋方塊中，輸入**TigerText 安全 Messenger**，選取**TigerText 安全 Messenger**然後按一下 從結果面板**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="04e38-133">In hello search box, type **TigerText Secure Messenger**, select **TigerText Secure Messenger** from result panel then click **Add** button tooadd hello application.</span></span>

    ![從資源庫新增](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="04e38-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="04e38-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="04e38-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 TigerText Secure Messenger 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="04e38-136">In this section, you configure and test Azure AD single sign-on with TigerText Secure Messenger based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="04e38-137">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者 TigerText 安全 messenger 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="04e38-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TigerText Secure Messenger is tooa user in Azure AD.</span></span> <span data-ttu-id="04e38-138">換句話說，Azure AD 使用者與 hello TigerText 安全 messenger 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="04e38-138">In other words, a link relationship between an Azure AD user and hello related user in TigerText Secure Messenger needs toobe established.</span></span>

<span data-ttu-id="04e38-139">TigerText 安全 messenger hello hello 值指派**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="04e38-139">In TigerText Secure Messenger, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="04e38-140">tooconfigure 及 TigerText 安全 Messenger 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="04e38-140">tooconfigure and test Azure AD single sign-on with TigerText Secure Messenger, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="04e38-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="04e38-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="04e38-142">**[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="04e38-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="04e38-143">**[建立測試使用者 TigerText 安全 Messenger](#create-a-tigertext-secure-messenger-test-user)**  -toohave 許 Simon TigerText 安全 messenger 連結的 toohello Azure AD 使用者表示法的對應項目。</span><span class="sxs-lookup"><span data-stu-id="04e38-143">**[Create a TigerText Secure Messenger test user](#create-a-tigertext-secure-messenger-test-user)** - toohave a counterpart of Britta Simon in TigerText Secure Messenger that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="04e38-144">**[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="04e38-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="04e38-145">**[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="04e38-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="04e38-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="04e38-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="04e38-147">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 TigerText 安全 Messenger 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="04e38-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TigerText Secure Messenger application.</span></span>

<span data-ttu-id="04e38-148">**TigerText 安全 Messenger 與 Azure AD 單一登入 tooconfigure 執行 hello 下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="04e38-148">**tooconfigure Azure AD single sign-on with TigerText Secure Messenger, perform hello following steps:**</span></span>

1. <span data-ttu-id="04e38-149">在 Azure 入口網站上 hello hello **TigerText 安全 Messenger**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="04e38-149">In hello Azure portal, on hello **TigerText Secure Messenger** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="04e38-151">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="04e38-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![SAML 型登入](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_samlbase.png)

3. <span data-ttu-id="04e38-153">在 hello **TigerText 安全 Messenger 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="04e38-153">On hello **TigerText Secure Messenger Domain and URLs** section, perform hello following steps:</span></span>

    ![[TigerText Secure Messenger 網域與 URL] 區段](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_url.png)

    <span data-ttu-id="04e38-155">a.</span><span class="sxs-lookup"><span data-stu-id="04e38-155">a.</span></span> <span data-ttu-id="04e38-156">在 hello**登入 URL**文字方塊中，做為型別 URL:`https://home.tigertext.com`</span><span class="sxs-lookup"><span data-stu-id="04e38-156">In hello **Sign-on URL** textbox, type URL as: `https://home.tigertext.com`</span></span>

    <span data-ttu-id="04e38-157">b.</span><span class="sxs-lookup"><span data-stu-id="04e38-157">b.</span></span> <span data-ttu-id="04e38-158">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://saml-lb.tigertext.me/v1/organization/<instance Id>`</span><span class="sxs-lookup"><span data-stu-id="04e38-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://saml-lb.tigertext.me/v1/organization/<instance Id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="04e38-159">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="04e38-159">This value is not real.</span></span> <span data-ttu-id="04e38-160">更新此值以 hello 實際的識別項。</span><span class="sxs-lookup"><span data-stu-id="04e38-160">Update this value with hello actual Identifier.</span></span> <span data-ttu-id="04e38-161">請連絡[TigerText 安全訊息用戶端支援小組](mailTo:prosupport@tigertext.com)tooget 此值。</span><span class="sxs-lookup"><span data-stu-id="04e38-161">Contact [TigerText Secure Messenger Client support team](mailTo:prosupport@tigertext.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="04e38-162">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="04e38-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![[SAML 簽署憑證] 區段](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_certificate.png) 

5. <span data-ttu-id="04e38-164">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="04e38-164">Click **Save** button.</span></span>

    ![[儲存] 按鈕](./media/active-directory-saas-tigertext-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="04e38-166">tooget 單一登入設定應用程式，請連絡[TigerText 安全 Messenger 支援小組](mailTo:prosupport@tigertext.com)並提供給他們 hello**下載中繼資料**。</span><span class="sxs-lookup"><span data-stu-id="04e38-166">tooget single sign-on configured for your application, contact [TigerText Secure Messenger support team](mailTo:prosupport@tigertext.com) and provide them hello **Downloaded metadata**.</span></span>

> [!TIP]
> <span data-ttu-id="04e38-167">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="04e38-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="04e38-168">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="04e38-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="04e38-169">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="04e38-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="04e38-170">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="04e38-170">Create an Azure AD test user</span></span>
<span data-ttu-id="04e38-171">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="04e38-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="04e38-173">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="04e38-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="04e38-174">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="04e38-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tigertext-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="04e38-176">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="04e38-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![使用者與群組->所有使用者](./media/active-directory-saas-tigertext-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="04e38-178">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="04e38-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![[新增] 按鈕](./media/active-directory-saas-tigertext-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="04e38-180">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="04e38-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![使用者對話方塊](./media/active-directory-saas-tigertext-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="04e38-182">a.</span><span class="sxs-lookup"><span data-stu-id="04e38-182">a.</span></span> <span data-ttu-id="04e38-183">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="04e38-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="04e38-184">b.</span><span class="sxs-lookup"><span data-stu-id="04e38-184">b.</span></span> <span data-ttu-id="04e38-185">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="04e38-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="04e38-186">c.</span><span class="sxs-lookup"><span data-stu-id="04e38-186">c.</span></span> <span data-ttu-id="04e38-187">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="04e38-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="04e38-188">d.</span><span class="sxs-lookup"><span data-stu-id="04e38-188">d.</span></span> <span data-ttu-id="04e38-189">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="04e38-189">Click **Create**.</span></span>
 
### <a name="create-a-tigertext-secure-messenger-test-user"></a><span data-ttu-id="04e38-190">建立 TigerText Secure Messengerr 測試使用者</span><span class="sxs-lookup"><span data-stu-id="04e38-190">Create a TigerText Secure Messenger test user</span></span>

<span data-ttu-id="04e38-191">在本節中，您要在 TigerText 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="04e38-191">In this section, you create a user called Britta Simon in TigerText.</span></span> <span data-ttu-id="04e38-192">請太聯繫[TigerText 安全訊息用戶端支援小組](mailTo:prosupport@tigertext.com)tooadd hello hello TigerText 平台的使用者。</span><span class="sxs-lookup"><span data-stu-id="04e38-192">Please reach out too[TigerText Secure Messenger Client support team](mailTo:prosupport@tigertext.com) tooadd hello users in hello TigerText platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="04e38-193">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="04e38-193">Assign hello Azure AD test user</span></span>

<span data-ttu-id="04e38-194">在本節中，您必須啟用 Azure 單一登入許 Simon toouse 授與存取 tooTigerText 安全 Messenger。</span><span class="sxs-lookup"><span data-stu-id="04e38-194">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTigerText Secure Messenger.</span></span>

![指派使用者][200] 

<span data-ttu-id="04e38-196">**tooassign 許 Simon tooTigerText 安全 Messenger，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="04e38-196">**tooassign Britta Simon tooTigerText Secure Messenger, perform hello following steps:**</span></span>

1. <span data-ttu-id="04e38-197">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="04e38-197">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="04e38-199">在 [hello] 應用程式清單中，選取**TigerText 安全 Messenger**。</span><span class="sxs-lookup"><span data-stu-id="04e38-199">In hello applications list, select **TigerText Secure Messenger**.</span></span>

    ![應用程式清單中的 TigerText Secure Messenger](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_app.png) 

3. <span data-ttu-id="04e38-201">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="04e38-201">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="04e38-203">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="04e38-203">Click **Add** button.</span></span> <span data-ttu-id="04e38-204">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="04e38-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="04e38-206">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="04e38-206">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="04e38-207">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="04e38-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="04e38-208">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="04e38-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="04e38-209">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="04e38-209">Test single sign-on</span></span>

<span data-ttu-id="04e38-210">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="04e38-210">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="04e38-211">當您按一下 hello TigerText 磚 hello 存取面板中的時，您應該取得自動登入 tooyour TigerText 應用程式。</span><span class="sxs-lookup"><span data-stu-id="04e38-211">When you click hello TigerText tile in hello Access Panel, you should get automatically signed-on tooyour TigerText application.</span></span> <span data-ttu-id="04e38-212">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="04e38-212">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="04e38-213">其他資源</span><span class="sxs-lookup"><span data-stu-id="04e38-213">Additional resources</span></span>

* [<span data-ttu-id="04e38-214">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="04e38-214">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="04e38-215">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="04e38-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_203.png

