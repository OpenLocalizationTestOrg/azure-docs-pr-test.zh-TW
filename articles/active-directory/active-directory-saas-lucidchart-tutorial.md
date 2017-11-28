---
title: "教學課程：Azure Active Directory 與 Lucidchart 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Lucidchart 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1068d364-11f3-43b5-bd6d-26f00ecd5baa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 774e5f423097650a3cae8e8ca13b2c65b8470736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lucidchart"></a><span data-ttu-id="11c88-103">教學課程：Azure Active Directory 與 Lucidchart 整合</span><span class="sxs-lookup"><span data-stu-id="11c88-103">Tutorial: Azure Active Directory integration with Lucidchart</span></span>

<span data-ttu-id="11c88-104">在此教學課程中，您學會如何 toointegrate Lucidchart 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="11c88-104">In this tutorial, you learn how toointegrate Lucidchart with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="11c88-105">與 Azure AD 整合 Lucidchart 可以提供下列優點的 hello:</span><span class="sxs-lookup"><span data-stu-id="11c88-105">Integrating Lucidchart with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="11c88-106">您可以控制存取 tooLucidchart Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="11c88-106">You can control in Azure AD who has access tooLucidchart</span></span>
- <span data-ttu-id="11c88-107">您可以啟用您的使用者 tooautomatically get 登入 tooLucidchart （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="11c88-107">You can enable your users tooautomatically get signed-on tooLucidchart (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="11c88-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="11c88-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="11c88-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="11c88-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="11c88-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="11c88-110">Prerequisites</span></span>

<span data-ttu-id="11c88-111">tooconfigure 與 Lucidchart 的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="11c88-111">tooconfigure Azure AD integration with Lucidchart, you need hello following items:</span></span>

- <span data-ttu-id="11c88-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="11c88-112">An Azure AD subscription</span></span>
- <span data-ttu-id="11c88-113">啟用 Lucidchart 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="11c88-113">A Lucidchart single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="11c88-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="11c88-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="11c88-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="11c88-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="11c88-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="11c88-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="11c88-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="11c88-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="11c88-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="11c88-118">Scenario description</span></span>
<span data-ttu-id="11c88-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="11c88-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="11c88-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="11c88-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="11c88-121">從 hello 圖庫加入 Lucidchart</span><span class="sxs-lookup"><span data-stu-id="11c88-121">Adding Lucidchart from hello gallery</span></span>
2. <span data-ttu-id="11c88-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="11c88-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lucidchart-from-hello-gallery"></a><span data-ttu-id="11c88-123">從 hello 圖庫加入 Lucidchart</span><span class="sxs-lookup"><span data-stu-id="11c88-123">Adding Lucidchart from hello gallery</span></span>
<span data-ttu-id="11c88-124">tooconfigure hello 整合 Lucidchart 的 Azure AD，您需要 tooadd Lucidchart hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="11c88-124">tooconfigure hello integration of Lucidchart into Azure AD, you need tooadd Lucidchart from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="11c88-125">**tooadd Lucidchart 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="11c88-125">**tooadd Lucidchart from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="11c88-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="11c88-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="11c88-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="11c88-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="11c88-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="11c88-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="11c88-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="11c88-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="11c88-133">在 [hello] 搜尋方塊中，輸入**Lucidchart**。</span><span class="sxs-lookup"><span data-stu-id="11c88-133">In hello search box, type **Lucidchart**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_search.png)

5. <span data-ttu-id="11c88-135">在 hello 結果 窗格中，選取  **Lucidchart**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="11c88-135">In hello results panel, select **Lucidchart**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="11c88-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="11c88-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="11c88-138">在本節中，您將以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Lucidchart 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="11c88-138">In this section, you configure and test Azure AD single sign-on with Lucidchart based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="11c88-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 Lucidchart 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="11c88-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lucidchart is tooa user in Azure AD.</span></span> <span data-ttu-id="11c88-140">換句話說，Azure AD 使用者與 Lucidchart 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="11c88-140">In other words, a link relationship between an Azure AD user and hello related user in Lucidchart needs toobe established.</span></span>

<span data-ttu-id="11c88-141">在 Lucidchart，將指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="11c88-141">In Lucidchart, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="11c88-142">tooconfigure 及 Azure AD 單一登入與 Lucidchart 的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="11c88-142">tooconfigure and test Azure AD single sign-on with Lucidchart, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="11c88-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="11c88-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="11c88-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="11c88-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="11c88-145">**[建立測試使用者 Lucidchart](#creating-a-lucidchart-test-user)**  -toohave 許 Simon Lucidchart 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="11c88-145">**[Creating a Lucidchart test user](#creating-a-lucidchart-test-user)** - toohave a counterpart of Britta Simon in Lucidchart that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="11c88-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="11c88-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="11c88-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="11c88-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="11c88-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="11c88-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="11c88-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入您 Lucidchart 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="11c88-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lucidchart application.</span></span>

<span data-ttu-id="11c88-150">**tooconfigure Azure AD 單一登入與 Lucidchart，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="11c88-150">**tooconfigure Azure AD single sign-on with Lucidchart, perform hello following steps:**</span></span>

1. <span data-ttu-id="11c88-151">在 Azure 入口網站上 hello hello **Lucidchart**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="11c88-151">In hello Azure portal, on hello **Lucidchart** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="11c88-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="11c88-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_samlbase.png)

3. <span data-ttu-id="11c88-155">在 hello **Lucidchart 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="11c88-155">On hello **Lucidchart Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_url.png)

    <span data-ttu-id="11c88-157">在 hello**登入 URL**文字方塊中，輸入與 URL:`https://chart2.office.lucidchart.com/saml/sso/azure`</span><span class="sxs-lookup"><span data-stu-id="11c88-157">In hello **Sign-on URL** textbox, type a URL as: `https://chart2.office.lucidchart.com/saml/sso/azure`</span></span>

4. <span data-ttu-id="11c88-158">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="11c88-158">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_certificate.png) 

5. <span data-ttu-id="11c88-160">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="11c88-160">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-lucidchart-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="11c88-162">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 Lucidchart 公司網站。</span><span class="sxs-lookup"><span data-stu-id="11c88-162">In a different web browser window, log into your Lucidchart company site as an administrator.</span></span>

7. <span data-ttu-id="11c88-163">在 hello 最上層顯示 hello 功能表上，按一下**小組**。</span><span class="sxs-lookup"><span data-stu-id="11c88-163">In hello menu on hello top, click **Team**.</span></span>
   
    <span data-ttu-id="11c88-164">![小組](./media/active-directory-saas-lucidchart-tutorial/ic791190.png "小組")</span><span class="sxs-lookup"><span data-stu-id="11c88-164">![Team](./media/active-directory-saas-lucidchart-tutorial/ic791190.png "Team")</span></span>

8. <span data-ttu-id="11c88-165">按一下 [應用程式] \> [管理 SAML]。</span><span class="sxs-lookup"><span data-stu-id="11c88-165">Click **Applications \> Manage SAML**.</span></span>
   
    <span data-ttu-id="11c88-166">![管理 SAML](./media/active-directory-saas-lucidchart-tutorial/ic791191.png "管理 SAML")</span><span class="sxs-lookup"><span data-stu-id="11c88-166">![Manage SAML](./media/active-directory-saas-lucidchart-tutorial/ic791191.png "Manage SAML")</span></span>

9. <span data-ttu-id="11c88-167">在 hello **SAML 驗證設定**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="11c88-167">On hello **SAML Authentication Settings** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="11c88-168">a.</span><span class="sxs-lookup"><span data-stu-id="11c88-168">a.</span></span> <span data-ttu-id="11c88-169">選取 啟用 SAML 驗證，然後按一下選用。</span><span class="sxs-lookup"><span data-stu-id="11c88-169">Select **Enable SAML Authentication**, and then click **Optional**.</span></span>

    <span data-ttu-id="11c88-170">![SAML 驗證設定](./media/active-directory-saas-lucidchart-tutorial/ic791192.png "SAML 驗證設定")</span><span class="sxs-lookup"><span data-stu-id="11c88-170">![SAML Authentication Settings](./media/active-directory-saas-lucidchart-tutorial/ic791192.png "SAML Authentication Settings")</span></span>
 
    <span data-ttu-id="11c88-171">b.</span><span class="sxs-lookup"><span data-stu-id="11c88-171">b.</span></span> <span data-ttu-id="11c88-172">在 hello**網域**文字方塊中，輸入您的網域，然後按一下**變更憑證**。</span><span class="sxs-lookup"><span data-stu-id="11c88-172">In hello **Domain** textbox, type your domain, and then click **Change Certificate**.</span></span>

    <span data-ttu-id="11c88-173">![變更憑證](./media/active-directory-saas-lucidchart-tutorial/ic791193.png "變更憑證")</span><span class="sxs-lookup"><span data-stu-id="11c88-173">![Change Certificate](./media/active-directory-saas-lucidchart-tutorial/ic791193.png "Change Certificate")</span></span>
 
    <span data-ttu-id="11c88-174">c.</span><span class="sxs-lookup"><span data-stu-id="11c88-174">c.</span></span> <span data-ttu-id="11c88-175">開啟您下載的中繼資料檔案，複製 hello 內容，並貼到 hello**上傳中繼資料**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="11c88-175">Open your downloaded metadata file, copy hello content, and then paste it into hello **Upload Metadata** textbox.</span></span>

    <span data-ttu-id="11c88-176">![上傳中繼資料](./media/active-directory-saas-lucidchart-tutorial/ic791194.png "上傳中繼資料")</span><span class="sxs-lookup"><span data-stu-id="11c88-176">![Upload Metadata](./media/active-directory-saas-lucidchart-tutorial/ic791194.png "Upload Metadata")</span></span>
 
    <span data-ttu-id="11c88-177">d.</span><span class="sxs-lookup"><span data-stu-id="11c88-177">d.</span></span> <span data-ttu-id="11c88-178">選取**自動加入新的使用者 toohello 小組**，然後按一下**儲存變更**。</span><span class="sxs-lookup"><span data-stu-id="11c88-178">Select **Automatically Add new users toohello team**, and then click **Save changes**.</span></span>

    <span data-ttu-id="11c88-179">![儲存變更](./media/active-directory-saas-lucidchart-tutorial/ic791195.png "儲存變更")</span><span class="sxs-lookup"><span data-stu-id="11c88-179">![Save Changes](./media/active-directory-saas-lucidchart-tutorial/ic791195.png "Save Changes")</span></span>

> [!TIP]
> <span data-ttu-id="11c88-180">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="11c88-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="11c88-181">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="11c88-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="11c88-182">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="11c88-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="11c88-183">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="11c88-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="11c88-184">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="11c88-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="11c88-186">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="11c88-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="11c88-187">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="11c88-187">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="11c88-189">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="11c88-189">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="11c88-191">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="11c88-191">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="11c88-193">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="11c88-193">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="11c88-195">a.</span><span class="sxs-lookup"><span data-stu-id="11c88-195">a.</span></span> <span data-ttu-id="11c88-196">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="11c88-196">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="11c88-197">b.</span><span class="sxs-lookup"><span data-stu-id="11c88-197">b.</span></span> <span data-ttu-id="11c88-198">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="11c88-198">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="11c88-199">c.</span><span class="sxs-lookup"><span data-stu-id="11c88-199">c.</span></span> <span data-ttu-id="11c88-200">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="11c88-200">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="11c88-201">d.</span><span class="sxs-lookup"><span data-stu-id="11c88-201">d.</span></span> <span data-ttu-id="11c88-202">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="11c88-202">Click **Create**.</span></span>
 
### <a name="creating-a-lucidchart-test-user"></a><span data-ttu-id="11c88-203">建立 Lucidchart 測試使用者</span><span class="sxs-lookup"><span data-stu-id="11c88-203">Creating a Lucidchart test user</span></span>

<span data-ttu-id="11c88-204">不沒有您 tooconfigure 使用者佈建 tooLucidchart 任何動作項目。</span><span class="sxs-lookup"><span data-stu-id="11c88-204">There is no action item for you tooconfigure user provisioning tooLucidchart.</span></span>  <span data-ttu-id="11c88-205">當指派的使用者嘗試 toolog 入 Lucidchart 使用 hello 存取面板時，Lucidchart 會檢查 hello 使用者是否存在。</span><span class="sxs-lookup"><span data-stu-id="11c88-205">When an assigned user tries toolog into Lucidchart using hello access panel, Lucidchart checks whether hello user exists.</span></span>  

<span data-ttu-id="11c88-206">如果尚無可用的使用者帳戶，Lucidchart 會自動予以建立。</span><span class="sxs-lookup"><span data-stu-id="11c88-206">If there is no user account available yet, it is automatically created by Lucidchart.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="11c88-207">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="11c88-207">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="11c88-208">在本節中，您可以授與存取 tooLucidchart 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="11c88-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLucidchart.</span></span>

![指派使用者][200] 

<span data-ttu-id="11c88-210">**tooassign 許 Simon tooLucidchart，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="11c88-210">**tooassign Britta Simon tooLucidchart, perform hello following steps:**</span></span>

1. <span data-ttu-id="11c88-211">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="11c88-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="11c88-213">在 [hello] 應用程式清單中，選取**Lucidchart**。</span><span class="sxs-lookup"><span data-stu-id="11c88-213">In hello applications list, select **Lucidchart**.</span></span>

    ![設定單一登入](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_app.png) 

3. <span data-ttu-id="11c88-215">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="11c88-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="11c88-217">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="11c88-217">Click **Add** button.</span></span> <span data-ttu-id="11c88-218">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="11c88-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="11c88-220">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="11c88-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="11c88-221">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="11c88-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="11c88-222">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="11c88-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="11c88-223">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="11c88-223">Testing single sign-on</span></span>

<span data-ttu-id="11c88-224">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="11c88-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="11c88-225">當您按一下 hello Lucidchart 磚 hello 存取面板中的時，您應該取得 tooyour 自動登入 Lucidchart 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="11c88-225">When you click hello Lucidchart tile in hello Access Panel, you should get automatically signed-on tooyour Lucidchart application.</span></span>
<span data-ttu-id="11c88-226">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="11c88-226">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="11c88-227">其他資源</span><span class="sxs-lookup"><span data-stu-id="11c88-227">Additional resources</span></span>

* [<span data-ttu-id="11c88-228">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="11c88-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="11c88-229">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="11c88-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_203.png

