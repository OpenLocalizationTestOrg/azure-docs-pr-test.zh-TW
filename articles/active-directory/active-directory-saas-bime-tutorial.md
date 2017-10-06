---
title: "教學課程：Azure Active Directory 與 Bime 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Bime 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bdcf0729-c880-4c95-b739-0f6345b17dd8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 1213725028dd8ce90f22fa6e9c50ffabebc8f3fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bime"></a><span data-ttu-id="450f6-103">教學課程：Azure Active Directory 與 Bime 整合</span><span class="sxs-lookup"><span data-stu-id="450f6-103">Tutorial: Azure Active Directory integration with Bime</span></span>

<span data-ttu-id="450f6-104">在此教學課程中，您學會如何 toointegrate Bime 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="450f6-104">In this tutorial, you learn how toointegrate Bime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="450f6-105">整合 Azure AD 與 Bime 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="450f6-105">Integrating Bime with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="450f6-106">您可以控制存取 tooBime Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="450f6-106">You can control in Azure AD who has access tooBime</span></span>
- <span data-ttu-id="450f6-107">您可以啟用您的使用者 tooautomatically get 登入 tooBime （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="450f6-107">You can enable your users tooautomatically get signed-on tooBime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="450f6-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="450f6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="450f6-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="450f6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="450f6-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="450f6-110">Prerequisites</span></span>

<span data-ttu-id="450f6-111">tooconfigure Azure AD 與 Bime 的整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="450f6-111">tooconfigure Azure AD integration with Bime, you need hello following items:</span></span>

- <span data-ttu-id="450f6-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="450f6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="450f6-113">已啟用 Bime 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="450f6-113">A Bime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="450f6-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="450f6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="450f6-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="450f6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="450f6-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="450f6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="450f6-117">如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="450f6-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="450f6-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="450f6-118">Scenario description</span></span>
<span data-ttu-id="450f6-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="450f6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="450f6-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="450f6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="450f6-121">從 hello 圖庫加入 Bime</span><span class="sxs-lookup"><span data-stu-id="450f6-121">Adding Bime from hello gallery</span></span>
2. <span data-ttu-id="450f6-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="450f6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bime-from-hello-gallery"></a><span data-ttu-id="450f6-123">從 hello 圖庫加入 Bime</span><span class="sxs-lookup"><span data-stu-id="450f6-123">Adding Bime from hello gallery</span></span>
<span data-ttu-id="450f6-124">tooconfigure hello 整合 Bime 的 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Bime。</span><span class="sxs-lookup"><span data-stu-id="450f6-124">tooconfigure hello integration of Bime into Azure AD, you need tooadd Bime from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="450f6-125">**tooadd Bime 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="450f6-125">**tooadd Bime from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="450f6-126">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="450f6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="450f6-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="450f6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="450f6-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="450f6-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="450f6-131">tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="450f6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="450f6-133">在 [hello] 搜尋方塊中，輸入**Bime**。</span><span class="sxs-lookup"><span data-stu-id="450f6-133">In hello search box, type **Bime**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bime-tutorial/tutorial_bime_search.png)

5. <span data-ttu-id="450f6-135">在 [hello [結果] 窗格中，選取 [ **Bime**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="450f6-135">In hello results panel, select **Bime**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bime-tutorial/tutorial_bime_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="450f6-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="450f6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="450f6-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Bime 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="450f6-138">In this section, you configure and test Azure AD single sign-on with Bime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="450f6-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 Bime 中是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="450f6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Bime is tooa user in Azure AD.</span></span> <span data-ttu-id="450f6-140">換句話說，Azure AD 使用者與 Bime 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="450f6-140">In other words, a link relationship between an Azure AD user and hello related user in Bime needs toobe established.</span></span>

<span data-ttu-id="450f6-141">在 Bime 中，將指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="450f6-141">In Bime, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="450f6-142">tooconfigure 及測試 Azure AD 單一登入 Bime，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="450f6-142">tooconfigure and test Azure AD single sign-on with Bime, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="450f6-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="450f6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="450f6-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="450f6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="450f6-145">**[建立測試使用者 Bime](#creating-a-bime-test-user) ** -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示法的 Bime 中對應項目。</span><span class="sxs-lookup"><span data-stu-id="450f6-145">**[Creating a Bime test user](#creating-a-bime-test-user)** - toohave a counterpart of Britta Simon in Bime that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="450f6-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="450f6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="450f6-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="450f6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="450f6-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="450f6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="450f6-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Bime 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="450f6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Bime application.</span></span>

<span data-ttu-id="450f6-150">**tooconfigure Azure AD 單一登入 Bime 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="450f6-150">**tooconfigure Azure AD single sign-on with Bime, perform hello following steps:**</span></span>

1. <span data-ttu-id="450f6-151">在 Azure 入口網站上 hello hello **Bime**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="450f6-151">In hello Azure portal, on hello **Bime** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="450f6-153">在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="450f6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-bime-tutorial/tutorial_bime_samlbase.png)

3. <span data-ttu-id="450f6-155">在 [hello **Bime 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="450f6-155">On hello **Bime Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-bime-tutorial/tutorial_bime_url.png)

    <span data-ttu-id="450f6-157">a.</span><span class="sxs-lookup"><span data-stu-id="450f6-157">a.</span></span> <span data-ttu-id="450f6-158">在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<tenant-name>.Bimeapp.com`</span><span class="sxs-lookup"><span data-stu-id="450f6-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.Bimeapp.com`</span></span>

    <span data-ttu-id="450f6-159">b.</span><span class="sxs-lookup"><span data-stu-id="450f6-159">b.</span></span> <span data-ttu-id="450f6-160">在 [hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<tenant-name>.Bimeapp.com`</span><span class="sxs-lookup"><span data-stu-id="450f6-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant-name>.Bimeapp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="450f6-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="450f6-161">These values are not real.</span></span> <span data-ttu-id="450f6-162">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="450f6-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="450f6-163">請連絡[Bime 用戶端支援小組](https://bime.zendesk.com/hc/categories/202604307-Support-tech-notes-and-tips-)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="450f6-163">Contact [Bime Client support team](https://bime.zendesk.com/hc/categories/202604307-Support-tech-notes-and-tips-) tooget these values.</span></span> 
 
4. <span data-ttu-id="450f6-164">在 [hello **SAML 簽章憑證**區段，複製 hello**指紋**hello 憑證中的值。</span><span class="sxs-lookup"><span data-stu-id="450f6-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value from hello certificate.</span></span>

    ![設定單一登入](./media/active-directory-saas-bime-tutorial/tutorial_bime_certificate.png) 

5. <span data-ttu-id="450f6-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="450f6-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-bime-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="450f6-168">在 [hello **Bime 組態**區段中，按一下**設定 Bime** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="450f6-168">On hello **Bime Configuration** section, click **Configure Bime** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="450f6-169">複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="450f6-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-bime-tutorial/tutorial_bime_configure.png) 

7. <span data-ttu-id="450f6-171">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 Bime 公司網站。</span><span class="sxs-lookup"><span data-stu-id="450f6-171">In a different web browser window, log into your Bime company site as an administrator.</span></span>

8. <span data-ttu-id="450f6-172">在 [hello] 工具列中，按一下 [ **Admin**，然後**帳戶**。</span><span class="sxs-lookup"><span data-stu-id="450f6-172">In hello toolbar, click **Admin**, and then **Account**.</span></span>
   
    <span data-ttu-id="450f6-173">![管理](./media/active-directory-saas-bime-tutorial/ic775558.png "管理")</span><span class="sxs-lookup"><span data-stu-id="450f6-173">![Admin](./media/active-directory-saas-bime-tutorial/ic775558.png "Admin")</span></span>

9. <span data-ttu-id="450f6-174">在 hello 帳戶設定] 頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="450f6-174">On hello account configuration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="450f6-175">![設定單一登入](./media/active-directory-saas-bime-tutorial/ic775559.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="450f6-175">![Configure Single Sign-On](./media/active-directory-saas-bime-tutorial/ic775559.png "Configure Single Sign-On")</span></span>
   
    <span data-ttu-id="450f6-176">a.</span><span class="sxs-lookup"><span data-stu-id="450f6-176">a.</span></span> <span data-ttu-id="450f6-177">選取 [啟用 SAML 驗證] 。</span><span class="sxs-lookup"><span data-stu-id="450f6-177">Select **Enable SAML authentication**.</span></span>

    <span data-ttu-id="450f6-178">b.</span><span class="sxs-lookup"><span data-stu-id="450f6-178">b.</span></span> <span data-ttu-id="450f6-179">在 [hello**遠端登入 URL**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="450f6-179">In hello **Remote Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="450f6-180">c.</span><span class="sxs-lookup"><span data-stu-id="450f6-180">c.</span></span>  <span data-ttu-id="450f6-181">貼上 hello**指紋**值從 Azure 入口網站，將 hello**憑證指紋**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="450f6-181">Paste hello **Thumbprint** value from Azure portal into hello **Certificate Fingerprint** textbox.</span></span>       
   
    <span data-ttu-id="450f6-182">d.</span><span class="sxs-lookup"><span data-stu-id="450f6-182">d.</span></span> <span data-ttu-id="450f6-183">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="450f6-183">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="450f6-184">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="450f6-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="450f6-185">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="450f6-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="450f6-186">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="450f6-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="450f6-187">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="450f6-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="450f6-188">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="450f6-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="450f6-190">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="450f6-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="450f6-191">在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="450f6-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="450f6-193">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="450f6-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="450f6-195">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="450f6-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="450f6-197">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="450f6-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="450f6-199">a.</span><span class="sxs-lookup"><span data-stu-id="450f6-199">a.</span></span> <span data-ttu-id="450f6-200">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="450f6-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="450f6-201">b.</span><span class="sxs-lookup"><span data-stu-id="450f6-201">b.</span></span> <span data-ttu-id="450f6-202">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="450f6-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="450f6-203">c.</span><span class="sxs-lookup"><span data-stu-id="450f6-203">c.</span></span> <span data-ttu-id="450f6-204">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="450f6-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="450f6-205">d.</span><span class="sxs-lookup"><span data-stu-id="450f6-205">d.</span></span> <span data-ttu-id="450f6-206">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="450f6-206">Click **Create**.</span></span>
 
### <a name="creating-a-bime-test-user"></a><span data-ttu-id="450f6-207">建立 Bime 測試使用者</span><span class="sxs-lookup"><span data-stu-id="450f6-207">Creating a Bime test user</span></span>

<span data-ttu-id="450f6-208">在訂單 tooenable Azure AD 使用者 toolog tooBime 中，您必須是佈建到 Bime。</span><span class="sxs-lookup"><span data-stu-id="450f6-208">In order tooenable Azure AD users toolog in tooBime, they must be provisioned into Bime.</span></span> <span data-ttu-id="450f6-209">在 Bime 的 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="450f6-209">In hello case of Bime, provisioning is a manual task.</span></span>

<span data-ttu-id="450f6-210">**tooconfigure 使用者佈建，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="450f6-210">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="450f6-211">登入 tooyour **Bime**租用戶。</span><span class="sxs-lookup"><span data-stu-id="450f6-211">Log in tooyour **Bime** tenant.</span></span>

2. <span data-ttu-id="450f6-212">在 [hello] 工具列中，按一下 [ **Admin**，然後**使用者**。</span><span class="sxs-lookup"><span data-stu-id="450f6-212">In hello toolbar, click **Admin**, and then **Users**.</span></span>
   
    <span data-ttu-id="450f6-213">![管理](./media/active-directory-saas-bime-tutorial/ic775561.png "管理")</span><span class="sxs-lookup"><span data-stu-id="450f6-213">![Admin](./media/active-directory-saas-bime-tutorial/ic775561.png "Admin")</span></span>

3. <span data-ttu-id="450f6-214">在 [hello**使用者清單**，按一下 [**新增使用者**（"+"）。</span><span class="sxs-lookup"><span data-stu-id="450f6-214">In hello **Users List**, click **Add New User** (“+”).</span></span>
   
    <span data-ttu-id="450f6-215">![使用者](./media/active-directory-saas-bime-tutorial/ic775562.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="450f6-215">![Users](./media/active-directory-saas-bime-tutorial/ic775562.png "Users")</span></span>

4. <span data-ttu-id="450f6-216">在 [hello**使用者詳細資料**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="450f6-216">On hello **User Details** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="450f6-217">![使用者詳細資料](./media/active-directory-saas-bime-tutorial/ic775563.png "使用者詳細資料")</span><span class="sxs-lookup"><span data-stu-id="450f6-217">![User Details](./media/active-directory-saas-bime-tutorial/ic775563.png "User Details")</span></span>
   
    <span data-ttu-id="450f6-218">a.</span><span class="sxs-lookup"><span data-stu-id="450f6-218">a.</span></span> <span data-ttu-id="450f6-219">在 [hello**名字**文字方塊中，輸入 hello 名字，例如使用者的**許**。</span><span class="sxs-lookup"><span data-stu-id="450f6-219">In hello **First name** textbox, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="450f6-220">b.</span><span class="sxs-lookup"><span data-stu-id="450f6-220">b.</span></span> <span data-ttu-id="450f6-221">在 [hello**姓氏**文字方塊中，輸入 hello 姓氏的使用者，例如**Simon**。</span><span class="sxs-lookup"><span data-stu-id="450f6-221">In hello **Last name** textbox, enter hello last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="450f6-222">c.</span><span class="sxs-lookup"><span data-stu-id="450f6-222">c.</span></span> <span data-ttu-id="450f6-223">在 [hello**電子郵件**文字方塊中，輸入 hello 電子郵件的使用者，例如** brittasimon@contoso.com **。</span><span class="sxs-lookup"><span data-stu-id="450f6-223">In hello **Email** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="450f6-224">d.</span><span class="sxs-lookup"><span data-stu-id="450f6-224">d.</span></span> <span data-ttu-id="450f6-225">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="450f6-225">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="450f6-226">您可以使用任何其他 Bime 使用者帳戶建立工具或 Api 提供 Bime tooprovision AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="450f6-226">You can use any other Bime user account creation tools or APIs provided by Bime tooprovision AAD user accounts.</span></span>
>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="450f6-227">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="450f6-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="450f6-228">在本節中，您可以授與存取 tooBime 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="450f6-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBime.</span></span>

![指派使用者][200] 

<span data-ttu-id="450f6-230">**tooassign 許 Simon tooBime，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="450f6-230">**tooassign Britta Simon tooBime, perform hello following steps:**</span></span>

1. <span data-ttu-id="450f6-231">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="450f6-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="450f6-233">在 [hello] 應用程式清單中，選取**Bime**。</span><span class="sxs-lookup"><span data-stu-id="450f6-233">In hello applications list, select **Bime**.</span></span>

    ![設定單一登入](./media/active-directory-saas-bime-tutorial/tutorial_bime_app.png) 

3. <span data-ttu-id="450f6-235">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="450f6-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="450f6-237">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="450f6-237">Click **Add** button.</span></span> <span data-ttu-id="450f6-238">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="450f6-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="450f6-240">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="450f6-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="450f6-241">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="450f6-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="450f6-242">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="450f6-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="450f6-243">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="450f6-243">Testing single sign-on</span></span>

<span data-ttu-id="450f6-244">hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="450f6-244">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="450f6-245">當您按一下 hello Bime 磚 hello 存取面板中的時，您應該取得 tooyour 自動登入 Bime 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="450f6-245">When you click hello Bime tile in hello Access Panel, you should get automatically signed-on tooyour Bime application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="450f6-246">其他資源</span><span class="sxs-lookup"><span data-stu-id="450f6-246">Additional resources</span></span>

* [<span data-ttu-id="450f6-247">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="450f6-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="450f6-248">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="450f6-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bime-tutorial/tutorial_general_203.png

