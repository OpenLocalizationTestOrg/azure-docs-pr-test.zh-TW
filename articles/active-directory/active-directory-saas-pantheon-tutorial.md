---
title: "教學課程：Azure Active Directory 與 Pantheon 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Pantheon 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2c965d1-666f-44c2-b08f-b73163096374
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 5c3e54aef1f64dbab77d40a8c098172d609bfec8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pantheon"></a><span data-ttu-id="58f8d-103">教學課程：Azure Active Directory 與 Pantheon 整合</span><span class="sxs-lookup"><span data-stu-id="58f8d-103">Tutorial: Azure Active Directory integration with Pantheon</span></span>

<span data-ttu-id="58f8d-104">在此教學課程中，您學會如何 toointegrate Pantheon 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="58f8d-104">In this tutorial, you learn how toointegrate Pantheon with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="58f8d-105">與 Azure AD 整合 Pantheon 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="58f8d-105">Integrating Pantheon with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="58f8d-106">您可以控制存取 tooPantheon Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="58f8d-106">You can control in Azure AD who has access tooPantheon</span></span>
- <span data-ttu-id="58f8d-107">您可以啟用您的使用者 tooautomatically get 登入 tooPantheon （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="58f8d-107">You can enable your users tooautomatically get signed-on tooPantheon (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="58f8d-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="58f8d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="58f8d-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="58f8d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58f8d-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="58f8d-110">Prerequisites</span></span>

<span data-ttu-id="58f8d-111">tooconfigure Pantheon 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="58f8d-111">tooconfigure Azure AD integration with Pantheon, you need hello following items:</span></span>

- <span data-ttu-id="58f8d-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="58f8d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="58f8d-113">已啟用 Pantheon 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="58f8d-113">A Pantheon single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="58f8d-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="58f8d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="58f8d-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="58f8d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="58f8d-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="58f8d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="58f8d-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="58f8d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="58f8d-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="58f8d-118">Scenario description</span></span>
<span data-ttu-id="58f8d-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="58f8d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="58f8d-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="58f8d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="58f8d-121">從 hello 圖庫加入 Pantheon</span><span class="sxs-lookup"><span data-stu-id="58f8d-121">Adding Pantheon from hello gallery</span></span>
2. <span data-ttu-id="58f8d-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="58f8d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pantheon-from-hello-gallery"></a><span data-ttu-id="58f8d-123">從 hello 圖庫加入 Pantheon</span><span class="sxs-lookup"><span data-stu-id="58f8d-123">Adding Pantheon from hello gallery</span></span>
<span data-ttu-id="58f8d-124">tooconfigure hello 整合 Pantheon 到 Azure AD，您需要 tooadd Pantheon hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="58f8d-124">tooconfigure hello integration of Pantheon into Azure AD, you need tooadd Pantheon from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="58f8d-125">**tooadd Pantheon 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="58f8d-125">**tooadd Pantheon from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="58f8d-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="58f8d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="58f8d-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="58f8d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="58f8d-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="58f8d-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="58f8d-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="58f8d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="58f8d-133">在 [hello] 搜尋方塊中，輸入**Pantheon**。</span><span class="sxs-lookup"><span data-stu-id="58f8d-133">In hello search box, type **Pantheon**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_search.png)

5. <span data-ttu-id="58f8d-135">在 hello 結果 窗格中，選取  **Pantheon**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="58f8d-135">In hello results panel, select **Pantheon**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="58f8d-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="58f8d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="58f8d-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Pantheon 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="58f8d-138">In this section, you configure and test Azure AD single sign-on with Pantheon based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="58f8d-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Pantheon 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="58f8d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Pantheon is tooa user in Azure AD.</span></span> <span data-ttu-id="58f8d-140">換句話說，Azure AD 使用者與 hello Pantheon 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="58f8d-140">In other words, a link relationship between an Azure AD user and hello related user in Pantheon needs toobe established.</span></span>

<span data-ttu-id="58f8d-141">Pantheon 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="58f8d-141">In Pantheon, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="58f8d-142">tooconfigure 及 Pantheon 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="58f8d-142">tooconfigure and test Azure AD single sign-on with Pantheon, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="58f8d-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="58f8d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="58f8d-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="58f8d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="58f8d-145">**[建立測試使用者 Pantheon](#creating-a-pantheon-test-user)**  -toohave 許 Simon Pantheon 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="58f8d-145">**[Creating a Pantheon test user](#creating-a-pantheon-test-user)** - toohave a counterpart of Britta Simon in Pantheon that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="58f8d-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="58f8d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="58f8d-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="58f8d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="58f8d-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="58f8d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="58f8d-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Pantheon 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="58f8d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Pantheon application.</span></span>

<span data-ttu-id="58f8d-150">**tooconfigure Azure AD 單一登入與 Pantheon，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="58f8d-150">**tooconfigure Azure AD single sign-on with Pantheon, perform hello following steps:**</span></span>

1. <span data-ttu-id="58f8d-151">在 Azure 入口網站上 hello hello **Pantheon**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="58f8d-151">In hello Azure portal, on hello **Pantheon** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="58f8d-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="58f8d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_samlbase.png)

3. <span data-ttu-id="58f8d-155">在 hello **Pantheon 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="58f8d-155">On hello **Pantheon Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_url.png)

    <span data-ttu-id="58f8d-157">a.</span><span class="sxs-lookup"><span data-stu-id="58f8d-157">a.</span></span> <span data-ttu-id="58f8d-158">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`urn:auth0:pantheon:<orgname>-SSO`</span><span class="sxs-lookup"><span data-stu-id="58f8d-158">In hello **Identifier** textbox, type a URL using hello following pattern: `urn:auth0:pantheon:<orgname>-SSO`</span></span>

    <span data-ttu-id="58f8d-159">b.</span><span class="sxs-lookup"><span data-stu-id="58f8d-159">b.</span></span> <span data-ttu-id="58f8d-160">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://pantheon.auth0.com/login/callback?connection=<orgname>-SSO`</span><span class="sxs-lookup"><span data-stu-id="58f8d-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://pantheon.auth0.com/login/callback?connection=<orgname>-SSO`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="58f8d-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="58f8d-161">These values are not real.</span></span> <span data-ttu-id="58f8d-162">以 hello 實際的識別項和回覆 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="58f8d-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="58f8d-163">請連絡[Pantheon 支援小組](https://pantheon.io/docs/getting-support/)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="58f8d-163">Contact [Pantheon support team](https://pantheon.io/docs/getting-support/) tooget these values.</span></span>

4. <span data-ttu-id="58f8d-164">Pantheon 應用程式預期 hello SAML 判斷提示，以特定格式，這需要您 tooset hello UserIdentifier hello 使用者的電子郵件地址的屬性值。</span><span class="sxs-lookup"><span data-stu-id="58f8d-164">Pantheon application expects hello SAML assertion in specific format, which requires you tooset hello UserIdentifier attribute value with hello user’s email address.</span></span> <span data-ttu-id="58f8d-165">預設 Azure AD 會使用 hello UserPrincipalName UserIdentifier 屬性。</span><span class="sxs-lookup"><span data-stu-id="58f8d-165">By default Azure AD uses hello UserPrincipalName for UserIdentifier attribute.</span></span> <span data-ttu-id="58f8d-166">但成功整合您需要 tooadjust 此值 toomatch，使用者的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="58f8d-166">But for successful integration you need tooadjust this value toomatch with user’s email address.</span></span> <span data-ttu-id="58f8d-167">在執行 hello 正確的對應之後才可 hello 整合。</span><span class="sxs-lookup"><span data-stu-id="58f8d-167">hello integration will only work after doing hello correct mapping.</span></span>

    ![設定單一登入](./media/active-directory-saas-pantheon-tutorial/tutorial_attribute.png)  


5. <span data-ttu-id="58f8d-169">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="58f8d-169">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_certificate.png)

6. <span data-ttu-id="58f8d-171">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="58f8d-171">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-pantheon-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="58f8d-173">在 hello **Pantheon 組態**區段中，按一下**設定 Pantheon** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="58f8d-173">On hello **Pantheon Configuration** section, click **Configure Pantheon** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="58f8d-174">複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="58f8d-174">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_configure.png) 

8. <span data-ttu-id="58f8d-176">tooconfigure 單一登入上**Pantheon**端，您需要下載 toosend hello**憑證**和**SAML 單一登入服務 URL**太[Pantheon支援小組](https://pantheon.io/docs/getting-support/)。</span><span class="sxs-lookup"><span data-stu-id="58f8d-176">tooconfigure single sign-on on **Pantheon** side, you need toosend hello downloaded **Certificate** and **SAML Single Sign-On Service URL** too[Pantheon support team](https://pantheon.io/docs/getting-support/).</span></span>

     > [!Note]
     > <span data-ttu-id="58f8d-177">您也需要 tooprovide hello 電子郵件網域資訊和日期時間時您想要 tooenable 此連線。</span><span class="sxs-lookup"><span data-stu-id="58f8d-177">You also need tooprovide hello Email Domain(s) information and Date Time when you want tooenable this connection.</span></span> <span data-ttu-id="58f8d-178">您可以從[這裡](https://pantheon.io/docs/sso-organizations/)找到更多詳細資訊</span><span class="sxs-lookup"><span data-stu-id="58f8d-178">You can find more details about it from [here](https://pantheon.io/docs/sso-organizations/)</span></span>

> [!TIP]
> <span data-ttu-id="58f8d-179">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="58f8d-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="58f8d-180">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="58f8d-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="58f8d-181">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="58f8d-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="58f8d-182">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="58f8d-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="58f8d-183">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="58f8d-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="58f8d-185">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="58f8d-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="58f8d-186">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="58f8d-186">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pantheon-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="58f8d-188">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="58f8d-188">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pantheon-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="58f8d-190">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="58f8d-190">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pantheon-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="58f8d-192">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="58f8d-192">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pantheon-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="58f8d-194">a.</span><span class="sxs-lookup"><span data-stu-id="58f8d-194">a.</span></span> <span data-ttu-id="58f8d-195">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="58f8d-195">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="58f8d-196">b.</span><span class="sxs-lookup"><span data-stu-id="58f8d-196">b.</span></span> <span data-ttu-id="58f8d-197">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="58f8d-197">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="58f8d-198">c.</span><span class="sxs-lookup"><span data-stu-id="58f8d-198">c.</span></span> <span data-ttu-id="58f8d-199">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="58f8d-199">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="58f8d-200">d.</span><span class="sxs-lookup"><span data-stu-id="58f8d-200">d.</span></span> <span data-ttu-id="58f8d-201">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="58f8d-201">Click **Create**.</span></span>
 
### <a name="creating-a-pantheon-test-user"></a><span data-ttu-id="58f8d-202">建立 Pantheon 測試使用者</span><span class="sxs-lookup"><span data-stu-id="58f8d-202">Creating a Pantheon test user</span></span>

<span data-ttu-id="58f8d-203">在本節中，您要在 Pantheon 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="58f8d-203">In this section, you create a user called Britta Simon in Pantheon.</span></span> <span data-ttu-id="58f8d-204">請遵循以下步驟 tooadd hello 使用者 Pantheon hello。</span><span class="sxs-lookup"><span data-stu-id="58f8d-204">Please follow hello below steps tooadd hello user in Pantheon.</span></span> 

>[!NOTE] 
><span data-ttu-id="58f8d-205">SSO toowork 使用者必須 toobe Pantheon 中建立第一個。</span><span class="sxs-lookup"><span data-stu-id="58f8d-205">For SSO toowork user needs toobe created first in Pantheon.</span></span>

1. <span data-ttu-id="58f8d-206">使用系統管理員認證登入 tooPantheon。</span><span class="sxs-lookup"><span data-stu-id="58f8d-206">Login tooPantheon with admin credentials.</span></span>

2. <span data-ttu-id="58f8d-207">瀏覽過**組織**儀表板頁面。</span><span class="sxs-lookup"><span data-stu-id="58f8d-207">Navigate too**Organization** dashboard page.</span></span>
 
3. <span data-ttu-id="58f8d-208">按一下 [人員] 。</span><span class="sxs-lookup"><span data-stu-id="58f8d-208">Click **People**.</span></span>

4. <span data-ttu-id="58f8d-209">按一下 [新增使用者] 。</span><span class="sxs-lookup"><span data-stu-id="58f8d-209">Click **Add user**.</span></span>

5. <span data-ttu-id="58f8d-210">輸入 hello 使用者的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="58f8d-210">Enter hello user's email address.</span></span>

6. <span data-ttu-id="58f8d-211">選擇 hello 使用者角色。</span><span class="sxs-lookup"><span data-stu-id="58f8d-211">Choose hello user's role.</span></span>

7. <span data-ttu-id="58f8d-212">按一下 [新增使用者] 。</span><span class="sxs-lookup"><span data-stu-id="58f8d-212">Click **Add user**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="58f8d-213">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="58f8d-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="58f8d-214">在本節中，您可以授與存取 tooPantheon 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="58f8d-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPantheon.</span></span>

![指派使用者][200] 

<span data-ttu-id="58f8d-216">**tooassign 許 Simon tooPantheon，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="58f8d-216">**tooassign Britta Simon tooPantheon, perform hello following steps:**</span></span>

1. <span data-ttu-id="58f8d-217">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="58f8d-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="58f8d-219">在 [hello] 應用程式清單中，選取**Pantheon**。</span><span class="sxs-lookup"><span data-stu-id="58f8d-219">In hello applications list, select **Pantheon**.</span></span>

    ![設定單一登入](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_app.png) 

3. <span data-ttu-id="58f8d-221">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="58f8d-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="58f8d-223">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="58f8d-223">Click **Add** button.</span></span> <span data-ttu-id="58f8d-224">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="58f8d-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="58f8d-226">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="58f8d-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="58f8d-227">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="58f8d-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="58f8d-228">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="58f8d-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="58f8d-229">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="58f8d-229">Testing single sign-on</span></span>

<span data-ttu-id="58f8d-230">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="58f8d-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="58f8d-231">當您按一下 hello Pantheon 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Pantheon 應用程式。</span><span class="sxs-lookup"><span data-stu-id="58f8d-231">When you click hello Pantheon tile in hello Access Panel, you should get automatically signed-on tooyour Pantheon application.</span></span>
<span data-ttu-id="58f8d-232">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="58f8d-232">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="58f8d-233">其他資源</span><span class="sxs-lookup"><span data-stu-id="58f8d-233">Additional resources</span></span>

* [<span data-ttu-id="58f8d-234">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="58f8d-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="58f8d-235">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="58f8d-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_203.png

