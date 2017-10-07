---
title: "教學課程：Azure Active Directory 與 Teamphoria 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Teamphoria 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d569c705-6f0f-4ec1-b485-ba82526b5d32
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: f32be9742b76f7fe464036dadc108c62e4a787a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamphoria"></a><span data-ttu-id="da00f-103">教學課程：Azure Active Directory 與 Teamphoria 整合</span><span class="sxs-lookup"><span data-stu-id="da00f-103">Tutorial: Azure Active Directory integration with Teamphoria</span></span>

<span data-ttu-id="da00f-104">在此教學課程中，您學會如何 toointegrate Teamphoria 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="da00f-104">In this tutorial, you learn how toointegrate Teamphoria with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="da00f-105">與 Azure AD 整合 Teamphoria 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="da00f-105">Integrating Teamphoria with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="da00f-106">您可以控制存取 tooTeamphoria Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="da00f-106">You can control in Azure AD who has access tooTeamphoria</span></span>
- <span data-ttu-id="da00f-107">您可以啟用您的使用者 tooautomatically get 登入 tooTeamphoria （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="da00f-107">You can enable your users tooautomatically get signed-on tooTeamphoria (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="da00f-108">您可以管理您的帳戶，在單一中央位置-hello Azure 管理入口網站</span><span class="sxs-lookup"><span data-stu-id="da00f-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="da00f-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="da00f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with Teamphoria, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Teamphoria.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="da00f-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="da00f-110">Prerequisites</span></span>

<span data-ttu-id="da00f-111">tooconfigure Teamphoria 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="da00f-111">tooconfigure Azure AD integration with Teamphoria, you need hello following items:</span></span>

- <span data-ttu-id="da00f-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="da00f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="da00f-113">一個已啟用 Teamphoria 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="da00f-113">A Teamphoria single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="da00f-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="da00f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="da00f-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="da00f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="da00f-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="da00f-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="da00f-117">如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="da00f-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="da00f-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="da00f-118">Scenario description</span></span>
<span data-ttu-id="da00f-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="da00f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="da00f-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="da00f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="da00f-121">從 hello 圖庫加入 Teamphoria</span><span class="sxs-lookup"><span data-stu-id="da00f-121">Adding Teamphoria from hello gallery</span></span>
2. <span data-ttu-id="da00f-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="da00f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-teamphoria-from-hello-gallery"></a><span data-ttu-id="da00f-123">從 hello 圖庫加入 Teamphoria</span><span class="sxs-lookup"><span data-stu-id="da00f-123">Adding Teamphoria from hello gallery</span></span>
<span data-ttu-id="da00f-124">tooconfigure hello 整合 Teamphoria 到 Azure AD，您需要 tooadd Teamphoria hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="da00f-124">tooconfigure hello integration of Teamphoria into Azure AD, you need tooadd Teamphoria from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="da00f-125">**tooadd Teamphoria 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="da00f-125">**tooadd Teamphoria from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="da00f-126">在 [hello ** [Azure 管理入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="da00f-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="da00f-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="da00f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="da00f-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="da00f-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="da00f-131">按一下**新增**上 hello hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="da00f-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="da00f-133">在 [hello] 搜尋方塊中，輸入**Teamphoria**。</span><span class="sxs-lookup"><span data-stu-id="da00f-133">In hello search box, type **Teamphoria**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_search.png)

5. <span data-ttu-id="da00f-135">在 [hello [結果] 窗格中，選取 [ **Teamphoria**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="da00f-135">In hello results panel, select **Teamphoria**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="da00f-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="da00f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="da00f-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Teamphoria 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="da00f-138">In this section, you configure and test Azure AD single sign-on with Teamphoria based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="da00f-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Teamphoria 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="da00f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Teamphoria is tooa user in Azure AD.</span></span> <span data-ttu-id="da00f-140">換句話說，Azure AD 使用者與 hello Teamphoria 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="da00f-140">In other words, a link relationship between an Azure AD user and hello related user in Teamphoria needs toobe established.</span></span>

<span data-ttu-id="da00f-141">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Teamphoria 中。</span><span class="sxs-lookup"><span data-stu-id="da00f-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Teamphoria.</span></span>

<span data-ttu-id="da00f-142">tooconfigure 及 Teamphoria 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="da00f-142">tooconfigure and test Azure AD single sign-on with Teamphoria, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="da00f-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="da00f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="da00f-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="da00f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="da00f-145">**[建立測試使用者 Teamphoria](#creating-a-teamphoria-test-user) ** -toohave 許 Simon 是連結的 toohello Azure AD 表示她的 Teamphoria 中對應項目。</span><span class="sxs-lookup"><span data-stu-id="da00f-145">**[Creating a Teamphoria test user](#creating-a-teamphoria-test-user)** - toohave a counterpart of Britta Simon in Teamphoria that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="da00f-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="da00f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="da00f-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="da00f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="da00f-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="da00f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="da00f-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 管理入口網站中，並 Teamphoria 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="da00f-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Teamphoria application.</span></span>

<span data-ttu-id="da00f-150">**tooconfigure Azure AD 單一登入與 Teamphoria，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="da00f-150">**tooconfigure Azure AD single sign-on with Teamphoria, perform hello following steps:**</span></span>

1. <span data-ttu-id="da00f-151">在 hello Azure 管理入口網站上 hello **Teamphoria**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="da00f-151">In hello Azure Management portal, on hello **Teamphoria** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="da00f-153">在 [hello**單一登入**] 對話方塊中，做為**模式**選取**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="da00f-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_samlbase.png)

3. <span data-ttu-id="da00f-155">在 [hello **Teamphoria 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="da00f-155">On hello **Teamphoria Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_url.png)

    <span data-ttu-id="da00f-157">a.</span><span class="sxs-lookup"><span data-stu-id="da00f-157">a.</span></span> <span data-ttu-id="da00f-158">在 [hello**登入 URL**文字方塊中，使用下列模式的 hello 類型 hello URL:`https://<sub-domain>.teamphoria.com/login`</span><span class="sxs-lookup"><span data-stu-id="da00f-158">In hello **Sign-on URL** textbox, type hello URL using hello following pattern: `https://<sub-domain>.teamphoria.com/login`</span></span>  

    > [!NOTE] 
    > <span data-ttu-id="da00f-159">請注意這些不是 hello 實際值。</span><span class="sxs-lookup"><span data-stu-id="da00f-159">Please note that these are not hello real values.</span></span> <span data-ttu-id="da00f-160">這些值以 hello 有 tooupdate 實際的登入 URL。</span><span class="sxs-lookup"><span data-stu-id="da00f-160">You have tooupdate these values with hello actual Sign-On URL.</span></span> <span data-ttu-id="da00f-161">請連絡[Teamphoria 用戶端支援小組](https://www.teamphoria.com/)tooget hello 登入 URL。</span><span class="sxs-lookup"><span data-stu-id="da00f-161">Contact [Teamphoria Client support team](https://www.teamphoria.com/) tooget hello Sign-on URL.</span></span> 

4. <span data-ttu-id="da00f-162">在 [hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)** ，然後儲存您的電腦上的 [hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="da00f-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_certificate.png) 

5. <span data-ttu-id="da00f-164">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="da00f-164">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-teamphoria-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="da00f-166">在 [hello **Teamphoria 組態**區段中，按一下**設定 Teamphoria** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="da00f-166">On hello **Teamphoria Configuration** section, click **Configure Teamphoria** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="da00f-167">複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="da00f-167">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_configure.png) 

7. <span data-ttu-id="da00f-169">tooconfigure 單一登入上**Teamphoria**側邊，以系統管理員身分登入 tooyour Teamphoria 應用程式。</span><span class="sxs-lookup"><span data-stu-id="da00f-169">tooconfigure single sign-on on **Teamphoria** side, Login tooyour Teamphoria application as an administrator.</span></span>

8. <span data-ttu-id="da00f-170">跳過**系統管理設定**選項 hello 左邊工具列中，在按一下 [設定] 索引標籤的 hello hello**單一登入**tooopen hello SSO 組態視窗。</span><span class="sxs-lookup"><span data-stu-id="da00f-170">Go too**ADMIN SETTINGS** option in hello left toolbar and under hello hello Configure Tab click on **SINGLE SIGN-ON** tooopen hello SSO configuration window.</span></span>

    ![設定單一登入](./media/active-directory-saas-teamphoria-tutorial/admin_sso_configure.png)

9. <span data-ttu-id="da00f-172">按一下**新增身分識別提供者**hello 右上角 tooopen hello 在表單中加入 hello SSO 設定的選項。</span><span class="sxs-lookup"><span data-stu-id="da00f-172">Click on **ADD NEW IDENTITY PROVIDER** option in hello top right corner tooopen hello form for adding hello settings for SSO.</span></span>

    ![設定單一登入](./media/active-directory-saas-teamphoria-tutorial/add_new_identity_provider.png)

10. <span data-ttu-id="da00f-174">Hello 欄位中輸入 hello 詳細資料，如所述的以下層</span><span class="sxs-lookup"><span data-stu-id="da00f-174">Enter hello details in hello fields as described below-</span></span>

    ![設定單一登入](./media/active-directory-saas-teamphoria-tutorial/Teamphoria_sso_save.png)

    <span data-ttu-id="da00f-176">a.</span><span class="sxs-lookup"><span data-stu-id="da00f-176">a.</span></span> <span data-ttu-id="da00f-177">**顯示名稱**: hello] 管理頁面上輸入 hello 外掛程式 hello 顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="da00f-177">**DISPLAY NAME** : Enter hello display name of hello plugin on hello admin page.</span></span>

    <span data-ttu-id="da00f-178">b.</span><span class="sxs-lookup"><span data-stu-id="da00f-178">b.</span></span> <span data-ttu-id="da00f-179">**按鈕名稱**: hello hello] 索引標籤會顯示在 hello 登入頁面上，針對透過 SSO 登入名稱。</span><span class="sxs-lookup"><span data-stu-id="da00f-179">**BUTTON NAME** : hello name of hello tab which will display on hello login page for logging in via SSO.</span></span>

    <span data-ttu-id="da00f-180">c.</span><span class="sxs-lookup"><span data-stu-id="da00f-180">c.</span></span> <span data-ttu-id="da00f-181">**憑證**： 開啟 hello 憑證之前下載從 hello Azure 入口網站在 「 記事本 」 中的 hello 複製 hello 內容相同，並將它這裡貼 hello 方塊中。</span><span class="sxs-lookup"><span data-stu-id="da00f-181">**CERTIFICATE** : Open hello Certificate downloaded earlier from hello Azure portal in notepad, copy hello contents of hello same and paste it here in hello box.</span></span>

    <span data-ttu-id="da00f-182">d.</span><span class="sxs-lookup"><span data-stu-id="da00f-182">d.</span></span> <span data-ttu-id="da00f-183">**進入點**： 貼上 hello **SAML 單一登入服務 URL**複製舊版表單 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="da00f-183">**ENTRY POINT** : Paste hello **SAML Single Sign-On Service URL** copied earlier form hello Azure portal.</span></span>

    <span data-ttu-id="da00f-184">e.</span><span class="sxs-lookup"><span data-stu-id="da00f-184">e.</span></span> <span data-ttu-id="da00f-185">切換 hello 選項太**ON** ，然後按一下 [**儲存**。</span><span class="sxs-lookup"><span data-stu-id="da00f-185">Switch hello option too**ON** and click on **SAVE**.</span></span> 

<!--### Next steps

tooensure users can sign-in tooTeamphoria after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Teamphoria prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooTeamphoria in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Teamphoria users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="da00f-186">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="da00f-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="da00f-187">hello 本節目標在於 toocreate 呼叫許 Simon hello Azure 管理入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="da00f-187">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="da00f-189">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="da00f-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="da00f-190">在 [hello **Azure 管理入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="da00f-190">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="da00f-192">跳過**使用者和群組**按一下**所有使用者**toodisplay hello 使用者清單。</span><span class="sxs-lookup"><span data-stu-id="da00f-192">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="da00f-194">在 hello hello 對話方塊頂端按一下**新增**tooopen hello**使用者**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="da00f-194">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="da00f-196">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="da00f-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="da00f-198">a.</span><span class="sxs-lookup"><span data-stu-id="da00f-198">a.</span></span> <span data-ttu-id="da00f-199">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="da00f-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="da00f-200">b.</span><span class="sxs-lookup"><span data-stu-id="da00f-200">b.</span></span> <span data-ttu-id="da00f-201">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="da00f-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="da00f-202">c.</span><span class="sxs-lookup"><span data-stu-id="da00f-202">c.</span></span> <span data-ttu-id="da00f-203">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="da00f-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="da00f-204">d.</span><span class="sxs-lookup"><span data-stu-id="da00f-204">d.</span></span> <span data-ttu-id="da00f-205">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="da00f-205">Click **Create**.</span></span>
 
### <a name="creating-a-teamphoria-test-user"></a><span data-ttu-id="da00f-206">建立 Teamphoria 測試使用者</span><span class="sxs-lookup"><span data-stu-id="da00f-206">Creating a Teamphoria test user</span></span>

<span data-ttu-id="da00f-207">在訂單 tooenable Azure AD 使用者 toolog Teamphoria 成，它們必須佈建到 Teamphoria。</span><span class="sxs-lookup"><span data-stu-id="da00f-207">In order tooenable Azure AD users toolog into Teamphoria, they must be provisioned into Teamphoria.</span></span> <span data-ttu-id="da00f-208">中的 Teamphoria hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="da00f-208">In hello case of Teamphoria, provisioning is a manual task.</span></span>

<span data-ttu-id="da00f-209">**tooprovision 使用者帳戶，執行下列步驟 hello:**</span><span class="sxs-lookup"><span data-stu-id="da00f-209">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="da00f-210">登入 tooyour Teamphoria 公司網站的系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="da00f-210">Log in tooyour Teamphoria company site as an administrator.</span></span>

2. <span data-ttu-id="da00f-211">按一下**管理員**設定 hello 左工具列上，並在 [hello**管理**索引標籤處按一下**使用者**tooopen hello 管理頁面的使用者。</span><span class="sxs-lookup"><span data-stu-id="da00f-211">Click on **ADMIN** settings on hello left toolbar and under hello **MANAGE** tab Click on **USERS** tooopen hello admin page for users.</span></span>

    ![新增員工](./media/active-directory-saas-teamphoria-tutorial/admin_manage_users.png)

3. <span data-ttu-id="da00f-213">按一下 hello**手動邀請**選項。</span><span class="sxs-lookup"><span data-stu-id="da00f-213">Click on hello **MANUAL INVITE** option.</span></span>

    ![邀請人員](./media/active-directory-saas-teamphoria-tutorial/admin_manage_add_users.png)  

4. <span data-ttu-id="da00f-215">在這個頁面上執行下列動作。</span><span class="sxs-lookup"><span data-stu-id="da00f-215">On this page, perform following action.</span></span> 
    
    ![邀請人員](./media/active-directory-saas-teamphoria-tutorial/manual_user_invite.png)  

    <span data-ttu-id="da00f-217">a.</span><span class="sxs-lookup"><span data-stu-id="da00f-217">a.</span></span> <span data-ttu-id="da00f-218">在 [hello**電子郵件地址**文字方塊中，hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="da00f-218">In hello **EMAIL ADDRESS** textbox, hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="da00f-219">b.</span><span class="sxs-lookup"><span data-stu-id="da00f-219">b.</span></span> <span data-ttu-id="da00f-220">在 [hello**名字**文字方塊中，輸入**許**。</span><span class="sxs-lookup"><span data-stu-id="da00f-220">In hello **FIRST NAME** textbox, type **Britta**.</span></span>

    <span data-ttu-id="da00f-221">c.</span><span class="sxs-lookup"><span data-stu-id="da00f-221">c.</span></span> <span data-ttu-id="da00f-222">在 [hello**姓氏**文字方塊中，輸入**Simon**。</span><span class="sxs-lookup"><span data-stu-id="da00f-222">In hello **LAST NAME** textbox, type **Simon**.</span></span>

    <span data-ttu-id="da00f-223">d.</span><span class="sxs-lookup"><span data-stu-id="da00f-223">d.</span></span> <span data-ttu-id="da00f-224">按一下 [邀請 1 位使用者]。</span><span class="sxs-lookup"><span data-stu-id="da00f-224">Click **INVITE 1 USER**.</span></span> <span data-ttu-id="da00f-225">使用者需要 tooaccept hello 邀請 tooget hello 系統中建立。</span><span class="sxs-lookup"><span data-stu-id="da00f-225">User needs tooaccept hello invite tooget created in hello system.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="da00f-226">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="da00f-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="da00f-227">在本節中，您可以授與他們存取 tooTeamphoria 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="da00f-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooTeamphoria.</span></span>

![指派使用者][200] 

<span data-ttu-id="da00f-229">**tooassign 許 Simon tooTeamphoria，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="da00f-229">**tooassign Britta Simon tooTeamphoria, perform hello following steps:**</span></span>

1. <span data-ttu-id="da00f-230">在 [hello Azure 管理入口網站中，開啟 [hello 應用程式] 檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="da00f-230">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="da00f-232">在 [hello] 應用程式清單中，選取**Teamphoria**。</span><span class="sxs-lookup"><span data-stu-id="da00f-232">In hello applications list, select **Teamphoria**.</span></span>

    ![設定單一登入](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_app.png) 

3. <span data-ttu-id="da00f-234">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="da00f-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="da00f-236">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="da00f-236">Click **Add** button.</span></span> <span data-ttu-id="da00f-237">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="da00f-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="da00f-239">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="da00f-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="da00f-240">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="da00f-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="da00f-241">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="da00f-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="da00f-242">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="da00f-242">Testing single sign-on</span></span>

<span data-ttu-id="da00f-243">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="da00f-243">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="da00f-244">如果要測試您的單一登入設定，請開啟存取面板。</span><span class="sxs-lookup"><span data-stu-id="da00f-244">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="da00f-245">如需 [存取面板] 的詳細資訊，請參閱 [存取面板簡介](https://msdn.microsoft.com/library/dn308586)。</span><span class="sxs-lookup"><span data-stu-id="da00f-245">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="da00f-246">其他資源</span><span class="sxs-lookup"><span data-stu-id="da00f-246">Additional resources</span></span>

* [<span data-ttu-id="da00f-247">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="da00f-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="da00f-248">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="da00f-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_203.png

