---
title: "教學課程：Azure Active Directory 與 Flatter Files 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 之間更平面的檔案。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f86fe5e3-0e91-40d6-869c-3df6912d27ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 73ca2613b7bbaf9992ecf624ff5defabaa44f7a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-flatter-files"></a><span data-ttu-id="a17d4-103">教學課程：Azure Active Directory 與 Flatter Files 整合</span><span class="sxs-lookup"><span data-stu-id="a17d4-103">Tutorial: Azure Active Directory integration with Flatter Files</span></span>

<span data-ttu-id="a17d4-104">在此教學課程中，您學會如何 toointegrate 更平面的檔案與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="a17d4-104">In this tutorial, you learn how toointegrate Flatter Files with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a17d4-105">與 Azure AD 整合更平面的檔案可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="a17d4-105">Integrating Flatter Files with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a17d4-106">您可以控制可以存取 Azure AD 中 tooFlatter 檔案</span><span class="sxs-lookup"><span data-stu-id="a17d4-106">You can control in Azure AD who has access tooFlatter Files</span></span>
- <span data-ttu-id="a17d4-107">您可以啟用使用者 tooautomatically 取得其 Azure AD 帳戶的登入 tooFlatter 檔案 （單一登入）</span><span class="sxs-lookup"><span data-stu-id="a17d4-107">You can enable your users tooautomatically get signed-on tooFlatter Files (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a17d4-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="a17d4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a17d4-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="a17d4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a17d4-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="a17d4-110">Prerequisites</span></span>

<span data-ttu-id="a17d4-111">tooconfigure 更平面的檔案與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="a17d4-111">tooconfigure Azure AD integration with Flatter Files, you need hello following items:</span></span>

- <span data-ttu-id="a17d4-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a17d4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a17d4-113">已啟用 Flatter Files 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a17d4-113">A Flatter Files single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a17d4-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="a17d4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a17d4-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="a17d4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a17d4-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="a17d4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a17d4-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="a17d4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a17d4-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="a17d4-118">Scenario description</span></span>
<span data-ttu-id="a17d4-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a17d4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a17d4-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="a17d4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a17d4-121">從 hello 組件庫中加入更平面的檔案</span><span class="sxs-lookup"><span data-stu-id="a17d4-121">Adding Flatter Files from hello gallery</span></span>
2. <span data-ttu-id="a17d4-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a17d4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-flatter-files-from-hello-gallery"></a><span data-ttu-id="a17d4-123">從 hello 組件庫中加入更平面的檔案</span><span class="sxs-lookup"><span data-stu-id="a17d4-123">Adding Flatter Files from hello gallery</span></span>
<span data-ttu-id="a17d4-124">tooconfigure hello 整合更平面的檔案到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd 更平面的檔案。</span><span class="sxs-lookup"><span data-stu-id="a17d4-124">tooconfigure hello integration of Flatter Files into Azure AD, you need tooadd Flatter Files from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a17d4-125">**tooadd hello 圖庫中，從更平面的檔案執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a17d4-125">**tooadd Flatter Files from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a17d4-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="a17d4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a17d4-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a17d4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a17d4-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a17d4-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="a17d4-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="a17d4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="a17d4-133">在 [hello] 搜尋方塊中，輸入**平緩檔案**。</span><span class="sxs-lookup"><span data-stu-id="a17d4-133">In hello search box, type **Flatter Files**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_search.png)

5. <span data-ttu-id="a17d4-135">在 hello 結果 窗格中，選取 **更平面的檔案**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a17d4-135">In hello results panel, select **Flatter Files**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a17d4-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a17d4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a17d4-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Flatter Files 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a17d4-138">In this section, you configure and test Azure AD single sign-on with Flatter Files based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a17d4-139">單一登入 toowork，Azure AD 需要 tooknow hello 對應項目更平面的檔案中的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="a17d4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Flatter Files is tooa user in Azure AD.</span></span> <span data-ttu-id="a17d4-140">換句話說，Azure AD 使用者和更平面的檔案中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="a17d4-140">In other words, a link relationship between an Azure AD user and hello related user in Flatter Files needs toobe established.</span></span>

<span data-ttu-id="a17d4-141">更平面的檔案中指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="a17d4-141">In Flatter Files, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a17d4-142">tooconfigure 及測試 Azure AD 單一登入與更平面的檔案，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="a17d4-142">tooconfigure and test Azure AD single sign-on with Flatter Files, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a17d4-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="a17d4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a17d4-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="a17d4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a17d4-145">**[建立呈現檔案的測試使用者](#creating-a-flatter-files-test-user)** -toohave 許 Simon 呈現為連結的 toohello Azure AD 使用者表示的檔案中對應項目。</span><span class="sxs-lookup"><span data-stu-id="a17d4-145">**[Creating a Flatter Files test user](#creating-a-flatter-files-test-user)** - toohave a counterpart of Britta Simon in Flatter Files that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a17d4-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a17d4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a17d4-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="a17d4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a17d4-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a17d4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a17d4-149">在本節中，您要啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入應用程式更平面的檔案中。</span><span class="sxs-lookup"><span data-stu-id="a17d4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Flatter Files application.</span></span>

<span data-ttu-id="a17d4-150">**tooconfigure Azure AD 單一登入更平面的檔案，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a17d4-150">**tooconfigure Azure AD single sign-on with Flatter Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="a17d4-151">在 Azure 入口網站上 hello hello**平緩檔案**應用程式整合頁面上，按一下**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="a17d4-151">In hello Azure portal, on hello **Flatter Files** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="a17d4-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a17d4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_samlbase.png)

3. <span data-ttu-id="a17d4-155">在 hello**平緩檔案網域和 Url**區段中，hello 使用者沒有 tooperform 任何步驟，因為與 Azure 已預先整合 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a17d4-155">On hello **Flatter Files Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![設定單一登入](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_url.png)
 
4. <span data-ttu-id="a17d4-157">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="a17d4-157">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_certificate.png) 

5. <span data-ttu-id="a17d4-159">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="a17d4-159">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-flatter-files-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a17d4-161">在 hello**更平面的檔案組態**區段中，按一下**設定呈現檔案**tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="a17d4-161">On hello **Flatter Files Configuration** section, click **Configure Flatter Files** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a17d4-162">複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="a17d4-162">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_configure.png) 

7. <span data-ttu-id="a17d4-164">登入 tooyour 更平面的檔案系統管理員身分的應用程式。</span><span class="sxs-lookup"><span data-stu-id="a17d4-164">Sign-on tooyour Flatter Files application as an administrator.</span></span>

8. <span data-ttu-id="a17d4-165">按一下 [儀表板]。</span><span class="sxs-lookup"><span data-stu-id="a17d4-165">Click **DASHBOARD**.</span></span> 
   
    ![設定單一登入](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_05.png)  

9. <span data-ttu-id="a17d4-167">按一下**設定**，然後執行下列步驟在 hello hello**公司** 索引標籤：</span><span class="sxs-lookup"><span data-stu-id="a17d4-167">Click **Settings**, and then perform hello following steps on hello **Company** tab:</span></span> 
   
    ![設定單一登入](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_06.png)  
    
    <span data-ttu-id="a17d4-169">a.</span><span class="sxs-lookup"><span data-stu-id="a17d4-169">a.</span></span> <span data-ttu-id="a17d4-170">選取 [使用 SAML 2.0 進行驗證]。</span><span class="sxs-lookup"><span data-stu-id="a17d4-170">Select **Use SAML 2.0 for Authentication**.</span></span>
    
    <span data-ttu-id="a17d4-171">b.</span><span class="sxs-lookup"><span data-stu-id="a17d4-171">b.</span></span> <span data-ttu-id="a17d4-172">按一下 [設定 SAML]。</span><span class="sxs-lookup"><span data-stu-id="a17d4-172">Click **Configure SAML**.</span></span>

8. <span data-ttu-id="a17d4-173">在 [hello **SAML 設定**] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a17d4-173">On hello **SAML Configuration** dialog, perform hello following steps:</span></span> 
   
    ![設定單一登入](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_08.png)  
   
    <span data-ttu-id="a17d4-175">a.</span><span class="sxs-lookup"><span data-stu-id="a17d4-175">a.</span></span> <span data-ttu-id="a17d4-176">在 hello**網域**文字方塊中，輸入您已註冊的網域。</span><span class="sxs-lookup"><span data-stu-id="a17d4-176">In hello **Domain** textbox, type your registered domain.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="a17d4-177">如果您沒有已註冊的網域，請透過 [support@flatterfiles.com](mailto:support@flatterfiles.com)。</span><span class="sxs-lookup"><span data-stu-id="a17d4-177">If you don't have a registered domain yet, contact your Flatter Files support team via [support@flatterfiles.com](mailto:support@flatterfiles.com).</span></span> 
    
    <span data-ttu-id="a17d4-178">b.</span><span class="sxs-lookup"><span data-stu-id="a17d4-178">b.</span></span> <span data-ttu-id="a17d4-179">在**身分識別提供者 URL**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**有複製形成 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="a17d4-179">In **Identity Provider URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied form Azure portal.</span></span>
   
    <span data-ttu-id="a17d4-180">c.</span><span class="sxs-lookup"><span data-stu-id="a17d4-180">c.</span></span>  <span data-ttu-id="a17d4-181">在記事本中，複製到剪貼簿，其內容的 hello 中開啟 base-64 編碼的憑證，然後將它貼入 toohello**身分識別提供者憑證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="a17d4-181">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Identity Provider Certificate** textbox.</span></span>

    <span data-ttu-id="a17d4-182">d.</span><span class="sxs-lookup"><span data-stu-id="a17d4-182">d.</span></span> <span data-ttu-id="a17d4-183">按一下 [更新] 。</span><span class="sxs-lookup"><span data-stu-id="a17d4-183">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="a17d4-184">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="a17d4-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a17d4-185">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="a17d4-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a17d4-186">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a17d4-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a17d4-187">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a17d4-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="a17d4-188">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="a17d4-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="a17d4-190">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a17d4-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a17d4-191">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="a17d4-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a17d4-193">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="a17d4-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a17d4-195">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="a17d4-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a17d4-197">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a17d4-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a17d4-199">a.</span><span class="sxs-lookup"><span data-stu-id="a17d4-199">a.</span></span> <span data-ttu-id="a17d4-200">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="a17d4-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a17d4-201">b.</span><span class="sxs-lookup"><span data-stu-id="a17d4-201">b.</span></span> <span data-ttu-id="a17d4-202">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="a17d4-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a17d4-203">c.</span><span class="sxs-lookup"><span data-stu-id="a17d4-203">c.</span></span> <span data-ttu-id="a17d4-204">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="a17d4-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a17d4-205">d.</span><span class="sxs-lookup"><span data-stu-id="a17d4-205">d.</span></span> <span data-ttu-id="a17d4-206">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="a17d4-206">Click **Create**.</span></span>
 
### <a name="creating-a-flatter-files-test-user"></a><span data-ttu-id="a17d4-207">建立 Flatter Files 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a17d4-207">Creating a Flatter Files test user</span></span>

<span data-ttu-id="a17d4-208">hello 本節目標在於 toocreate 呼叫許 Simon 更平面的檔案中的使用者。</span><span class="sxs-lookup"><span data-stu-id="a17d4-208">hello objective of this section is toocreate a user called Britta Simon in Flatter Files.</span></span>

<span data-ttu-id="a17d4-209">**toocreate 呼叫許 Simon 更平面的檔案中的使用者執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a17d4-209">**toocreate a user called Britta Simon in Flatter Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="a17d4-210">登入 tooyour**平緩檔案**以系統管理員身分的公司網站。</span><span class="sxs-lookup"><span data-stu-id="a17d4-210">Sign on tooyour **Flatter Files** company site as administrator.</span></span>

2. <span data-ttu-id="a17d4-211">Hello hello 左側瀏覽窗格中按一下**設定**，然後按一下hello**使用者** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a17d4-211">In hello navigation pane on hello left, click **Settings**, and then click hello **Users** tab.</span></span>
   
    ![建立 Flatter Files 使用者](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_09.png)

3. <span data-ttu-id="a17d4-213">按一下 [加入使用者] 。</span><span class="sxs-lookup"><span data-stu-id="a17d4-213">Click **Add User**.</span></span> 

4. <span data-ttu-id="a17d4-214">在 [hello**新增使用者**] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a17d4-214">On hello **Add User** dialog, perform hello following steps:</span></span>
   
    ![建立 Flatter Files 使用者](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_10.png)

    <span data-ttu-id="a17d4-216">a.</span><span class="sxs-lookup"><span data-stu-id="a17d4-216">a.</span></span> <span data-ttu-id="a17d4-217">在 hello**名字**文字方塊中，輸入**許**。</span><span class="sxs-lookup"><span data-stu-id="a17d4-217">In hello **First Name** textbox, type **Britta**.</span></span>
   
    <span data-ttu-id="a17d4-218">b.</span><span class="sxs-lookup"><span data-stu-id="a17d4-218">b.</span></span> <span data-ttu-id="a17d4-219">在 hello**姓氏**文字方塊中，輸入**Simon**。</span><span class="sxs-lookup"><span data-stu-id="a17d4-219">In hello **Last Name** textbox, type **Simon**.</span></span> 
   
    <span data-ttu-id="a17d4-220">c.</span><span class="sxs-lookup"><span data-stu-id="a17d4-220">c.</span></span> <span data-ttu-id="a17d4-221">在 hello**電子郵件地址**文字方塊中，輸入許的電子郵件地址 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="a17d4-221">In hello **Email Address** textbox, type Britta's email address in hello Azure portal.</span></span>
   
    <span data-ttu-id="a17d4-222">d.</span><span class="sxs-lookup"><span data-stu-id="a17d4-222">d.</span></span> <span data-ttu-id="a17d4-223">按一下 [提交] 。</span><span class="sxs-lookup"><span data-stu-id="a17d4-223">Click **Submit**.</span></span>   


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a17d4-224">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="a17d4-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a17d4-225">在本節中，您可以啟用許 Simon toouse Azure 單一登入授與存取 tooFlatter 檔案。</span><span class="sxs-lookup"><span data-stu-id="a17d4-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFlatter Files.</span></span>

![指派使用者][200] 

<span data-ttu-id="a17d4-227">**tooassign 許 Simon tooFlatter 檔案，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a17d4-227">**tooassign Britta Simon tooFlatter Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="a17d4-228">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a17d4-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="a17d4-230">在 [hello] 應用程式清單中，選取**平緩檔案**。</span><span class="sxs-lookup"><span data-stu-id="a17d4-230">In hello applications list, select **Flatter Files**.</span></span>

    ![設定單一登入](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_app.png) 

3. <span data-ttu-id="a17d4-232">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="a17d4-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="a17d4-234">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a17d4-234">Click **Add** button.</span></span> <span data-ttu-id="a17d4-235">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="a17d4-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="a17d4-237">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="a17d4-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a17d4-238">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a17d4-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a17d4-239">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a17d4-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a17d4-240">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="a17d4-240">Testing single sign-on</span></span>

<span data-ttu-id="a17d4-241">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="a17d4-241">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a17d4-242">當您按一下的 hello 平緩檔案磚 hello 存取面板中時，您應該取得自動登入 tooyour 呈現檔案的應用程式。</span><span class="sxs-lookup"><span data-stu-id="a17d4-242">When you click hello Flatter Files tile in hello Access Panel, you should get automatically signed-on tooyour Flatter Files application.</span></span>
<span data-ttu-id="a17d4-243">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="a17d4-243">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a17d4-244">其他資源</span><span class="sxs-lookup"><span data-stu-id="a17d4-244">Additional resources</span></span>

* [<span data-ttu-id="a17d4-245">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a17d4-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a17d4-246">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="a17d4-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_203.png

