---
title: "教學課程：Azure Active Directory 與 Kudos 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Kudos 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 39c47ce6-4944-47ba-8f53-3afa95398034
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: c1b481463574461f9948db2b83843fefa5d74e99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kudos"></a><span data-ttu-id="4347b-103">教學課程：Azure Active Directory 與 Kudos 整合</span><span class="sxs-lookup"><span data-stu-id="4347b-103">Tutorial: Azure Active Directory integration with Kudos</span></span>

<span data-ttu-id="4347b-104">在此教學課程中，您學會如何 toointegrate Kudos 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="4347b-104">In this tutorial, you learn how toointegrate Kudos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4347b-105">與 Azure AD 整合 Kudos 可以提供下列優點的 hello:</span><span class="sxs-lookup"><span data-stu-id="4347b-105">Integrating Kudos with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4347b-106">您可以控制存取 tooKudos Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="4347b-106">You can control in Azure AD who has access tooKudos</span></span>
- <span data-ttu-id="4347b-107">您可以啟用您的使用者 tooautomatically get 登入 tooKudos （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="4347b-107">You can enable your users tooautomatically get signed-on tooKudos (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4347b-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="4347b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4347b-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="4347b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4347b-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="4347b-110">Prerequisites</span></span>

<span data-ttu-id="4347b-111">tooconfigure 與 Kudos 的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="4347b-111">tooconfigure Azure AD integration with Kudos, you need hello following items:</span></span>

- <span data-ttu-id="4347b-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="4347b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4347b-113">已啟用 Kudos 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="4347b-113">A Kudos single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4347b-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="4347b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4347b-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="4347b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4347b-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="4347b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4347b-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="4347b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4347b-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="4347b-118">Scenario description</span></span>
<span data-ttu-id="4347b-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4347b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4347b-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="4347b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4347b-121">從 hello 圖庫加入 Kudos</span><span class="sxs-lookup"><span data-stu-id="4347b-121">Adding Kudos from hello gallery</span></span>
2. <span data-ttu-id="4347b-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="4347b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kudos-from-hello-gallery"></a><span data-ttu-id="4347b-123">從 hello 圖庫加入 Kudos</span><span class="sxs-lookup"><span data-stu-id="4347b-123">Adding Kudos from hello gallery</span></span>
<span data-ttu-id="4347b-124">tooconfigure hello 整合 Kudos 的 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Kudos。</span><span class="sxs-lookup"><span data-stu-id="4347b-124">tooconfigure hello integration of Kudos into Azure AD, you need tooadd Kudos from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4347b-125">**tooadd Kudos 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="4347b-125">**tooadd Kudos from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4347b-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="4347b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4347b-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="4347b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4347b-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="4347b-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="4347b-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="4347b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="4347b-133">在 [hello] 搜尋方塊中，輸入**Kudos**。</span><span class="sxs-lookup"><span data-stu-id="4347b-133">In hello search box, type **Kudos**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_search.png)

5. <span data-ttu-id="4347b-135">在 hello 結果 窗格中，選取  **Kudos**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4347b-135">In hello results panel, select **Kudos**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4347b-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="4347b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4347b-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Kudos 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4347b-138">In this section, you configure and test Azure AD single sign-on with Kudos based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4347b-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 Kudos 中是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="4347b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kudos is tooa user in Azure AD.</span></span> <span data-ttu-id="4347b-140">換句話說，Azure AD 使用者與 hello Kudos 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="4347b-140">In other words, a link relationship between an Azure AD user and hello related user in Kudos needs toobe established.</span></span>

<span data-ttu-id="4347b-141">在 Kudos 中，將指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="4347b-141">In Kudos, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4347b-142">tooconfigure 及測試 Azure AD 單一登入 Kudos，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="4347b-142">tooconfigure and test Azure AD single sign-on with Kudos, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4347b-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="4347b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4347b-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="4347b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4347b-145">**[建立測試使用者 Kudos](#creating-a-kudos-test-user)**  -toohave 許 Simon Kudos 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="4347b-145">**[Creating a Kudos test user](#creating-a-kudos-test-user)** - toohave a counterpart of Britta Simon in Kudos that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4347b-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4347b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4347b-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="4347b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4347b-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="4347b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4347b-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Kudos 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="4347b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kudos application.</span></span>

<span data-ttu-id="4347b-150">**tooconfigure Azure AD 單一登入 Kudos，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="4347b-150">**tooconfigure Azure AD single sign-on with Kudos, perform hello following steps:**</span></span>

1. <span data-ttu-id="4347b-151">在 Azure 入口網站上 hello hello **Kudos**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="4347b-151">In hello Azure portal, on hello **Kudos** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="4347b-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4347b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_samlbase.png)

3. <span data-ttu-id="4347b-155">在 hello **Kudos 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="4347b-155">On hello **Kudos Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_url.png)

    <span data-ttu-id="4347b-157">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<company>.kudosnow.com`</span><span class="sxs-lookup"><span data-stu-id="4347b-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company>.kudosnow.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="4347b-158">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="4347b-158">This value is not real.</span></span> <span data-ttu-id="4347b-159">更新此值以 hello 實際的登入 URL。</span><span class="sxs-lookup"><span data-stu-id="4347b-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="4347b-160">請連絡[Kudos 用戶端支援小組](http://success.kudosnow.com/home)tooget 此值。</span><span class="sxs-lookup"><span data-stu-id="4347b-160">Contact [Kudos Client support team](http://success.kudosnow.com/home) tooget this value.</span></span> 
 
4. <span data-ttu-id="4347b-161">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="4347b-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_certificate.png) 

5. <span data-ttu-id="4347b-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="4347b-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-kudos-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4347b-165">在 hello **Kudos 組態**區段中，按一下**設定 Kudos** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="4347b-165">On hello **Kudos Configuration** section, click **Configure Kudos** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4347b-166">複製 hello**登出 URL 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="4347b-166">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_configure.png) 

7. <span data-ttu-id="4347b-168">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 Kudos 公司網站。</span><span class="sxs-lookup"><span data-stu-id="4347b-168">In a different web browser window, log into your Kudos company site as an administrator.</span></span>

8. <span data-ttu-id="4347b-169">在 hello 最上層顯示 hello 功能表上，按一下**設定**。</span><span class="sxs-lookup"><span data-stu-id="4347b-169">In hello menu on hello top, click **Settings**.</span></span>
   
    <span data-ttu-id="4347b-170">![設定](./media/active-directory-saas-kudos-tutorial/ic787806.png "設定")</span><span class="sxs-lookup"><span data-stu-id="4347b-170">![Settings](./media/active-directory-saas-kudos-tutorial/ic787806.png "Settings")</span></span>

9. <span data-ttu-id="4347b-171">按一下 [整合 \> SSO]。</span><span class="sxs-lookup"><span data-stu-id="4347b-171">Click **Integrations \> SSO**.</span></span>

10. <span data-ttu-id="4347b-172">在 hello **SSO**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="4347b-172">In hello **SSO** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="4347b-173">![SSO](./media/active-directory-saas-kudos-tutorial/ic787807.png "SSO")</span><span class="sxs-lookup"><span data-stu-id="4347b-173">![SSO](./media/active-directory-saas-kudos-tutorial/ic787807.png "SSO")</span></span>
   
    <span data-ttu-id="4347b-174">a.</span><span class="sxs-lookup"><span data-stu-id="4347b-174">a.</span></span> <span data-ttu-id="4347b-175">在**登入 URL**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="4347b-175">In **Sign on URL** textbox, paste hello value of  **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="4347b-176">b.</span><span class="sxs-lookup"><span data-stu-id="4347b-176">b.</span></span> <span data-ttu-id="4347b-177">在記事本中，複製到剪貼簿，其內容的 hello 中開啟 base-64 編碼的憑證，然後將它貼入 toohello **X.509 憑證**文字方塊</span><span class="sxs-lookup"><span data-stu-id="4347b-177">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 certificate** textbox</span></span>
   
    <span data-ttu-id="4347b-178">c.</span><span class="sxs-lookup"><span data-stu-id="4347b-178">c.</span></span> <span data-ttu-id="4347b-179">在**登出 tooURL**，貼上的 hello 值**登出 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="4347b-179">In **Logout tooURL**, paste hello value of  **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="4347b-180">d.</span><span class="sxs-lookup"><span data-stu-id="4347b-180">d.</span></span> <span data-ttu-id="4347b-181">在 hello**您的 Kudos URL**文字方塊中，輸入您的公司名稱。</span><span class="sxs-lookup"><span data-stu-id="4347b-181">In hello **Your Kudos URL** textbox, type your company name.</span></span>
   
    <span data-ttu-id="4347b-182">e.</span><span class="sxs-lookup"><span data-stu-id="4347b-182">e.</span></span> <span data-ttu-id="4347b-183">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="4347b-183">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="4347b-184">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="4347b-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4347b-185">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="4347b-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4347b-186">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4347b-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4347b-187">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="4347b-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="4347b-188">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="4347b-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="4347b-190">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="4347b-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4347b-191">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="4347b-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kudos-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4347b-193">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="4347b-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kudos-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4347b-195">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="4347b-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kudos-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4347b-197">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="4347b-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kudos-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4347b-199">a.</span><span class="sxs-lookup"><span data-stu-id="4347b-199">a.</span></span> <span data-ttu-id="4347b-200">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="4347b-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4347b-201">b.</span><span class="sxs-lookup"><span data-stu-id="4347b-201">b.</span></span> <span data-ttu-id="4347b-202">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="4347b-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4347b-203">c.</span><span class="sxs-lookup"><span data-stu-id="4347b-203">c.</span></span> <span data-ttu-id="4347b-204">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="4347b-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4347b-205">d.</span><span class="sxs-lookup"><span data-stu-id="4347b-205">d.</span></span> <span data-ttu-id="4347b-206">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="4347b-206">Click **Create**.</span></span>
 
### <a name="creating-a-kudos-test-user"></a><span data-ttu-id="4347b-207">建立 Kudos 測試使用者</span><span class="sxs-lookup"><span data-stu-id="4347b-207">Creating a Kudos test user</span></span>

<span data-ttu-id="4347b-208">在訂單 tooenable Azure AD 使用者 toolog 入 Kudos，它們必須佈建到 Kudos。</span><span class="sxs-lookup"><span data-stu-id="4347b-208">In order tooenable Azure AD users toolog into Kudos, they must be provisioned into Kudos.</span></span> 

<span data-ttu-id="4347b-209">在 Kudos 的 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="4347b-209">In hello case of Kudos, provisioning is a manual task.</span></span>

<span data-ttu-id="4347b-210">**tooprovision 使用者帳戶，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="4347b-210">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="4347b-211">登入 tooyour **Kudos**以系統管理員身分的公司網站。</span><span class="sxs-lookup"><span data-stu-id="4347b-211">Log in tooyour **Kudos** company site as administrator.</span></span>

2. <span data-ttu-id="4347b-212">在 hello 最上層顯示 hello 功能表上，按一下**設定**。</span><span class="sxs-lookup"><span data-stu-id="4347b-212">In hello menu on hello top, click **Settings**.</span></span>
   
   <span data-ttu-id="4347b-213">![設定](./media/active-directory-saas-kudos-tutorial/ic787806.png "設定")</span><span class="sxs-lookup"><span data-stu-id="4347b-213">![Settings](./media/active-directory-saas-kudos-tutorial/ic787806.png "Settings")</span></span>

3. <span data-ttu-id="4347b-214">按一下 [使用者管理] 。</span><span class="sxs-lookup"><span data-stu-id="4347b-214">Click **User Admin**.</span></span>

4. <span data-ttu-id="4347b-215">按一下 hello**使用者**索引標籤，然後再按一下**將使用者新增**。</span><span class="sxs-lookup"><span data-stu-id="4347b-215">Click hello **Users** tab, and then click **Add a User**.</span></span>
   
   <span data-ttu-id="4347b-216">![使用者管理員](./media/active-directory-saas-kudos-tutorial/ic787809.png "使用者管理員")</span><span class="sxs-lookup"><span data-stu-id="4347b-216">![User Admin](./media/active-directory-saas-kudos-tutorial/ic787809.png "User Admin")</span></span>

5. <span data-ttu-id="4347b-217">在 hello**將使用者新增**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="4347b-217">In hello **Add a User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="4347b-218">![加入使用者](./media/active-directory-saas-kudos-tutorial/ic787810.png "加入使用者")</span><span class="sxs-lookup"><span data-stu-id="4347b-218">![Add a User](./media/active-directory-saas-kudos-tutorial/ic787810.png "Add a User")</span></span>
   
    <span data-ttu-id="4347b-219">a.</span><span class="sxs-lookup"><span data-stu-id="4347b-219">a.</span></span> <span data-ttu-id="4347b-220">型別 hello**名字**，**姓氏**，**電子郵件**和想成 hello tooprovision 之有效 Azure Active Directory 帳戶的其他詳細資料相關的文字方塊。</span><span class="sxs-lookup"><span data-stu-id="4347b-220">Type hello **First Name**, **Last Name**, **Email** and other details of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>
   
    <span data-ttu-id="4347b-221">b.</span><span class="sxs-lookup"><span data-stu-id="4347b-221">b.</span></span> <span data-ttu-id="4347b-222">按一下 [建立使用者] 。</span><span class="sxs-lookup"><span data-stu-id="4347b-222">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="4347b-223">您可以使用任何其他 Kudos 使用者帳戶建立工具或 Api 提供 Kudos tooprovision AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="4347b-223">You can use any other Kudos user account creation tools or APIs provided by Kudos tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4347b-224">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="4347b-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4347b-225">在本節中，您可以授與存取 tooKudos 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4347b-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKudos.</span></span>

![指派使用者][200] 

<span data-ttu-id="4347b-227">**tooassign 許 Simon tooKudos，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="4347b-227">**tooassign Britta Simon tooKudos, perform hello following steps:**</span></span>

1. <span data-ttu-id="4347b-228">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="4347b-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="4347b-230">在 [hello] 應用程式清單中，選取**Kudos**。</span><span class="sxs-lookup"><span data-stu-id="4347b-230">In hello applications list, select **Kudos**.</span></span>

    ![設定單一登入](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_app.png) 

3. <span data-ttu-id="4347b-232">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="4347b-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="4347b-234">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4347b-234">Click **Add** button.</span></span> <span data-ttu-id="4347b-235">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="4347b-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="4347b-237">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="4347b-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4347b-238">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4347b-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4347b-239">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4347b-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4347b-240">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="4347b-240">Testing single sign-on</span></span>

<span data-ttu-id="4347b-241">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="4347b-241">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4347b-242">當您按一下 hello Kudos 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Kudos 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4347b-242">When you click hello Kudos tile in hello Access Panel, you should get automatically signed-on tooyour Kudos application.</span></span> <span data-ttu-id="4347b-243">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="4347b-243">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4347b-244">其他資源</span><span class="sxs-lookup"><span data-stu-id="4347b-244">Additional resources</span></span>

* [<span data-ttu-id="4347b-245">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4347b-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4347b-246">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="4347b-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_203.png

