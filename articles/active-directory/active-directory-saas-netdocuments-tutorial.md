---
title: "教學課程：Azure Active Directory 與 NetDocuments 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 NetDocuments 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1a47dc42-1a17-48a2-965e-eca4cfb2f197
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: ee9887553595a2492642aed4cb4abcd11d9cf599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netdocuments"></a><span data-ttu-id="fffe9-103">教學課程：Azure Active Directory 與 NetDocuments 整合</span><span class="sxs-lookup"><span data-stu-id="fffe9-103">Tutorial: Azure Active Directory integration with NetDocuments</span></span>

<span data-ttu-id="fffe9-104">在此教學課程中，您學會如何 toointegrate NetDocuments 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="fffe9-104">In this tutorial, you learn how toointegrate NetDocuments with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fffe9-105">與 Azure AD 整合 NetDocuments 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="fffe9-105">Integrating NetDocuments with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fffe9-106">您可以控制存取 tooNetDocuments Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="fffe9-106">You can control in Azure AD who has access tooNetDocuments</span></span>
- <span data-ttu-id="fffe9-107">您可以啟用您的使用者 tooautomatically get 登入 tooNetDocuments （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="fffe9-107">You can enable your users tooautomatically get signed-on tooNetDocuments (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fffe9-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="fffe9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="fffe9-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="fffe9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fffe9-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="fffe9-110">Prerequisites</span></span>

<span data-ttu-id="fffe9-111">tooconfigure 與 NetDocuments 的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="fffe9-111">tooconfigure Azure AD integration with NetDocuments, you need hello following items:</span></span>

- <span data-ttu-id="fffe9-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="fffe9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fffe9-113">已啟用 NetDocuments 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="fffe9-113">A NetDocuments single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fffe9-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="fffe9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fffe9-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="fffe9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fffe9-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="fffe9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fffe9-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="fffe9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fffe9-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="fffe9-118">Scenario description</span></span>
<span data-ttu-id="fffe9-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="fffe9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fffe9-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="fffe9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fffe9-121">從 hello 圖庫加入 NetDocuments</span><span class="sxs-lookup"><span data-stu-id="fffe9-121">Adding NetDocuments from hello gallery</span></span>
2. <span data-ttu-id="fffe9-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="fffe9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-netdocuments-from-hello-gallery"></a><span data-ttu-id="fffe9-123">從 hello 圖庫加入 NetDocuments</span><span class="sxs-lookup"><span data-stu-id="fffe9-123">Adding NetDocuments from hello gallery</span></span>
<span data-ttu-id="fffe9-124">tooconfigure hello 整合 NetDocuments 的 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd NetDocuments。</span><span class="sxs-lookup"><span data-stu-id="fffe9-124">tooconfigure hello integration of NetDocuments into Azure AD, you need tooadd NetDocuments from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fffe9-125">**tooadd NetDocuments 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="fffe9-125">**tooadd NetDocuments from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fffe9-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="fffe9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fffe9-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="fffe9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fffe9-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="fffe9-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="fffe9-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="fffe9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="fffe9-133">在 [hello] 搜尋方塊中，輸入**NetDocuments**。</span><span class="sxs-lookup"><span data-stu-id="fffe9-133">In hello search box, type **NetDocuments**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_search.png)

5. <span data-ttu-id="fffe9-135">在 hello 結果 窗格中，選取  **NetDocuments**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fffe9-135">In hello results panel, select **NetDocuments**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fffe9-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="fffe9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fffe9-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 NetDocuments 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="fffe9-138">In this section, you configure and test Azure AD single sign-on with NetDocuments based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fffe9-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 NetDocuments 中是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="fffe9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in NetDocuments is tooa user in Azure AD.</span></span> <span data-ttu-id="fffe9-140">換句話說，Azure AD 使用者與 hello NetDocuments 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="fffe9-140">In other words, a link relationship between an Azure AD user and hello related user in NetDocuments needs toobe established.</span></span>

<span data-ttu-id="fffe9-141">在 NetDocuments 中，將指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="fffe9-141">In NetDocuments, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="fffe9-142">tooconfigure 及測試 Azure AD 單一登入 NetDocuments，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="fffe9-142">tooconfigure and test Azure AD single sign-on with NetDocuments, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fffe9-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="fffe9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fffe9-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="fffe9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fffe9-145">**[建立測試使用者 NetDocuments](#creating-a-netdocuments-test-user)**  -toohave 許 Simon NetDocuments 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="fffe9-145">**[Creating a NetDocuments test user](#creating-a-netdocuments-test-user)** - toohave a counterpart of Britta Simon in NetDocuments that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fffe9-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="fffe9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fffe9-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="fffe9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fffe9-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="fffe9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fffe9-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 NetDocuments 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="fffe9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your NetDocuments application.</span></span>

<span data-ttu-id="fffe9-150">**tooconfigure Azure AD 單一登入 NetDocuments，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="fffe9-150">**tooconfigure Azure AD single sign-on with NetDocuments, perform hello following steps:**</span></span>

1. <span data-ttu-id="fffe9-151">在 Azure 入口網站上 hello hello **NetDocuments**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="fffe9-151">In hello Azure portal, on hello **NetDocuments** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="fffe9-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="fffe9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_samlbase.png)

3. <span data-ttu-id="fffe9-155">在 hello **NetDocuments 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="fffe9-155">On hello **NetDocuments Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_url.png)

    <span data-ttu-id="fffe9-157">a.</span><span class="sxs-lookup"><span data-stu-id="fffe9-157">a.</span></span> <span data-ttu-id="fffe9-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span><span class="sxs-lookup"><span data-stu-id="fffe9-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span></span>

    <span data-ttu-id="fffe9-159">b.</span><span class="sxs-lookup"><span data-stu-id="fffe9-159">b.</span></span> <span data-ttu-id="fffe9-160">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span><span class="sxs-lookup"><span data-stu-id="fffe9-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fffe9-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="fffe9-161">These values are not real.</span></span> <span data-ttu-id="fffe9-162">更新這些值與 hello 實際登入 URL 和回覆 URL。</span><span class="sxs-lookup"><span data-stu-id="fffe9-162">Update these values with hello actual Sign-on URL and Reply URL.</span></span> <span data-ttu-id="fffe9-163">請連絡[NetDocuments 支援小組](https://support.netdocuments.com/hc/)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="fffe9-163">Contact [NetDocuments support team](https://support.netdocuments.com/hc/) tooget these values.</span></span>
 
4. <span data-ttu-id="fffe9-164">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="fffe9-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_certificate.png) 

5. <span data-ttu-id="fffe9-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="fffe9-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-netdocuments-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fffe9-168">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 NetDocuments 公司網站。</span><span class="sxs-lookup"><span data-stu-id="fffe9-168">In a different web browser window, log into your NetDocuments company site as an administrator.</span></span>

7. <span data-ttu-id="fffe9-169">跳過**Admin**。</span><span class="sxs-lookup"><span data-stu-id="fffe9-169">Go too**Admin**.</span></span>

8. <span data-ttu-id="fffe9-170">按一下 [新增與移除使用者和群組] 。</span><span class="sxs-lookup"><span data-stu-id="fffe9-170">Click **Add and remove users and groups**.</span></span>
   
    <span data-ttu-id="fffe9-171">![存放庫](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "存放庫")</span><span class="sxs-lookup"><span data-stu-id="fffe9-171">![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")</span></span>

9. <span data-ttu-id="fffe9-172">按一下 [設定進階驗證選項]。</span><span class="sxs-lookup"><span data-stu-id="fffe9-172">Click **Configure advanced authentication options**.</span></span>
    
    <span data-ttu-id="fffe9-173">![設定進階驗證選項](./media/active-directory-saas-netdocuments-tutorial/ic795048.png "設定進階驗證選項")</span><span class="sxs-lookup"><span data-stu-id="fffe9-173">![Configure advanced authentication options](./media/active-directory-saas-netdocuments-tutorial/ic795048.png "Configure advanced authentication options")</span></span>

10. <span data-ttu-id="fffe9-174">在 [hello**同盟識別身分**] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="fffe9-174">On hello **Federated Identity** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="fffe9-175">![同盟識別身分](./media/active-directory-saas-netdocuments-tutorial/ic795049.png "同盟識別身分")</span><span class="sxs-lookup"><span data-stu-id="fffe9-175">![Federated Identitty](./media/active-directory-saas-netdocuments-tutorial/ic795049.png "Federated Identitty")</span></span>
   
    <span data-ttu-id="fffe9-176">a.</span><span class="sxs-lookup"><span data-stu-id="fffe9-176">a.</span></span> <span data-ttu-id="fffe9-177">對於**同盟識別身分伺服器類型**，請選取 [Active Directory 同盟服務]。</span><span class="sxs-lookup"><span data-stu-id="fffe9-177">As **Federated identity server type**, select **Active Directory Federation Services**.</span></span>
   
    <span data-ttu-id="fffe9-178">b.</span><span class="sxs-lookup"><span data-stu-id="fffe9-178">b.</span></span> <span data-ttu-id="fffe9-179">按一下**選擇檔案**，tooupload hello 下載您從 Azure 入口網站下載的中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="fffe9-179">Click **Choose file**, tooupload hello downloaded metadata file which you have downloaded from Azure portal.</span></span>
   
    <span data-ttu-id="fffe9-180">c.</span><span class="sxs-lookup"><span data-stu-id="fffe9-180">c.</span></span> <span data-ttu-id="fffe9-181">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="fffe9-181">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="fffe9-182">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="fffe9-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fffe9-183">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="fffe9-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fffe9-184">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fffe9-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fffe9-185">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="fffe9-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="fffe9-186">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="fffe9-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="fffe9-188">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="fffe9-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fffe9-189">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="fffe9-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fffe9-191">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="fffe9-191">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fffe9-193">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="fffe9-193">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fffe9-195">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="fffe9-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fffe9-197">a.</span><span class="sxs-lookup"><span data-stu-id="fffe9-197">a.</span></span> <span data-ttu-id="fffe9-198">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="fffe9-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fffe9-199">b.</span><span class="sxs-lookup"><span data-stu-id="fffe9-199">b.</span></span> <span data-ttu-id="fffe9-200">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="fffe9-200">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fffe9-201">c.</span><span class="sxs-lookup"><span data-stu-id="fffe9-201">c.</span></span> <span data-ttu-id="fffe9-202">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="fffe9-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="fffe9-203">d.</span><span class="sxs-lookup"><span data-stu-id="fffe9-203">d.</span></span> <span data-ttu-id="fffe9-204">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="fffe9-204">Click **Create**.</span></span>
 
### <a name="creating-a-netdocuments-test-user"></a><span data-ttu-id="fffe9-205">建立 NetDocuments 測試使用者</span><span class="sxs-lookup"><span data-stu-id="fffe9-205">Creating a NetDocuments test user</span></span>

<span data-ttu-id="fffe9-206">tooenable Azure AD 使用者 toolog 中 tooNetDocuments，它們必須佈建到 NetDocuments。</span><span class="sxs-lookup"><span data-stu-id="fffe9-206">tooenable Azure AD users toolog in tooNetDocuments, they must be provisioned into NetDocuments.</span></span>  
<span data-ttu-id="fffe9-207">在 NetDocuments 的 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="fffe9-207">In hello case of NetDocuments, provisioning is a manual task.</span></span>

<span data-ttu-id="fffe9-208">**tooprovision 使用者帳戶，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="fffe9-208">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="fffe9-209">登入 tooyour **NetDocuments**以系統管理員身分的公司網站。</span><span class="sxs-lookup"><span data-stu-id="fffe9-209">Sing on tooyour **NetDocuments** company site as administrator.</span></span>

2. <span data-ttu-id="fffe9-210">在 hello 最上層顯示 hello 功能表上，按一下**Admin**。</span><span class="sxs-lookup"><span data-stu-id="fffe9-210">In hello menu on hello top, click **Admin**.</span></span>
   
    <span data-ttu-id="fffe9-211">![管理](./media/active-directory-saas-netdocuments-tutorial/ic795051.png "管理")</span><span class="sxs-lookup"><span data-stu-id="fffe9-211">![Admin](./media/active-directory-saas-netdocuments-tutorial/ic795051.png "Admin")</span></span>

3. <span data-ttu-id="fffe9-212">按一下 [新增與移除使用者和群組] 。</span><span class="sxs-lookup"><span data-stu-id="fffe9-212">Click **Add and remove users and groups**.</span></span>
   
    <span data-ttu-id="fffe9-213">![存放庫](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "存放庫")</span><span class="sxs-lookup"><span data-stu-id="fffe9-213">![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")</span></span>

4. <span data-ttu-id="fffe9-214">在 hello**電子郵件地址**文字方塊中，您想 tooprovision，然後再按一下之有效 Azure Active Directory 帳戶類型 hello 電子郵件地址**新增使用者**。</span><span class="sxs-lookup"><span data-stu-id="fffe9-214">In hello **Email Address** textbox, type hello email address of a valid Azure Active Directory account you want tooprovision, and then click **Add User**.</span></span>
   
    <span data-ttu-id="fffe9-215">![電子郵件地址](./media/active-directory-saas-netdocuments-tutorial/ic795053.png "電子郵件地址")</span><span class="sxs-lookup"><span data-stu-id="fffe9-215">![Email Address](./media/active-directory-saas-netdocuments-tutorial/ic795053.png "Email Address")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="fffe9-216">hello Azure Active Directory 帳戶持有者會收到電子郵件，其中包含連結 tooconfirm hello 帳戶之前就會生效。</span><span class="sxs-lookup"><span data-stu-id="fffe9-216">hello Azure Active Directory account holder will get an email that includes a link tooconfirm hello account before it becomes active.</span></span> <span data-ttu-id="fffe9-217">您可以使用任何其他 NetDocuments 使用者帳戶建立工具或 Api 提供 NetDocuments tooprovision Azure Active Directory 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="fffe9-217">You can use any other NetDocuments user account creation tools or APIs provided by NetDocuments tooprovision Azure Active Directory user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="fffe9-218">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="fffe9-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="fffe9-219">在本節中，您可以授與存取 tooNetDocuments 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="fffe9-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNetDocuments.</span></span>

![指派使用者][200] 

<span data-ttu-id="fffe9-221">**tooassign 許 Simon tooNetDocuments，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="fffe9-221">**tooassign Britta Simon tooNetDocuments, perform hello following steps:**</span></span>

1. <span data-ttu-id="fffe9-222">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="fffe9-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="fffe9-224">在 [hello] 應用程式清單中，選取**NetDocuments**。</span><span class="sxs-lookup"><span data-stu-id="fffe9-224">In hello applications list, select **NetDocuments**.</span></span>

    ![設定單一登入](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_app.png) 

3. <span data-ttu-id="fffe9-226">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="fffe9-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="fffe9-228">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fffe9-228">Click **Add** button.</span></span> <span data-ttu-id="fffe9-229">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="fffe9-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="fffe9-231">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="fffe9-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fffe9-232">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fffe9-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fffe9-233">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fffe9-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fffe9-234">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="fffe9-234">Testing single sign-on</span></span>

<span data-ttu-id="fffe9-235">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="fffe9-235">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="fffe9-236">當您按一下的 hello NetDocuments 磚 hello 存取面板中時，您應該取得自動登入 tooyour NetDocuments 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="fffe9-236">When you click hello NetDocuments tile in hello Access Panel, you should get automatically signed-on tooyour NetDocuments application.</span></span>
<span data-ttu-id="fffe9-237">如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="fffe9-237">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fffe9-238">其他資源</span><span class="sxs-lookup"><span data-stu-id="fffe9-238">Additional resources</span></span>

* [<span data-ttu-id="fffe9-239">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fffe9-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fffe9-240">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="fffe9-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_203.png

