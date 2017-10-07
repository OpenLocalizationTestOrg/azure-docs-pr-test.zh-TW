---
title: "教學課程：Azure Active Directory 與 Printix 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Printix 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4aea7320-b2d5-49e0-9b63-aeaff0f6fe66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 654810116091eb52912b377cc97afef803ee816e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-printix"></a><span data-ttu-id="76474-103">教學課程：Azure Active Directory 與 Printix 整合</span><span class="sxs-lookup"><span data-stu-id="76474-103">Tutorial: Azure Active Directory integration with Printix</span></span>

<span data-ttu-id="76474-104">在此教學課程中，您學會如何 toointegrate Printix 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="76474-104">In this tutorial, you learn how toointegrate Printix with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="76474-105">與 Azure AD 整合 Printix 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="76474-105">Integrating Printix with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="76474-106">您可以控制存取 tooPrintix Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="76474-106">You can control in Azure AD who has access tooPrintix</span></span>
- <span data-ttu-id="76474-107">您可以啟用您的使用者 tooautomatically get 登入 tooPrintix （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="76474-107">You can enable your users tooautomatically get signed-on tooPrintix (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="76474-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="76474-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="76474-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="76474-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="76474-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="76474-110">Prerequisites</span></span>

<span data-ttu-id="76474-111">tooconfigure Printix 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="76474-111">tooconfigure Azure AD integration with Printix, you need hello following items:</span></span>

- <span data-ttu-id="76474-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="76474-112">An Azure AD subscription</span></span>
- <span data-ttu-id="76474-113">已啟用 Printix 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="76474-113">A Printix single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="76474-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="76474-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="76474-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="76474-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="76474-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="76474-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="76474-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="76474-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="76474-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="76474-118">Scenario description</span></span>
<span data-ttu-id="76474-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="76474-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="76474-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="76474-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="76474-121">從 hello 圖庫加入 Printix</span><span class="sxs-lookup"><span data-stu-id="76474-121">Adding Printix from hello gallery</span></span>
2. <span data-ttu-id="76474-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="76474-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-printix-from-hello-gallery"></a><span data-ttu-id="76474-123">從 hello 圖庫加入 Printix</span><span class="sxs-lookup"><span data-stu-id="76474-123">Adding Printix from hello gallery</span></span>
<span data-ttu-id="76474-124">tooconfigure hello 整合 Printix 到 Azure AD，您需要 tooadd Printix hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="76474-124">tooconfigure hello integration of Printix into Azure AD, you need tooadd Printix from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="76474-125">**tooadd Printix 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="76474-125">**tooadd Printix from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="76474-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="76474-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="76474-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="76474-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="76474-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="76474-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="76474-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="76474-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="76474-133">在 [hello] 搜尋方塊中，輸入**Printix**。</span><span class="sxs-lookup"><span data-stu-id="76474-133">In hello search box, type **Printix**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-printix-tutorial/tutorial_printix_search.png)

5. <span data-ttu-id="76474-135">在 hello 結果 窗格中，選取  **Printix**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="76474-135">In hello results panel, select **Printix**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-printix-tutorial/tutorial_printix_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="76474-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="76474-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="76474-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Printix 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="76474-138">In this section, you configure and test Azure AD single sign-on with Printix based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="76474-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Printix 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="76474-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Printix is tooa user in Azure AD.</span></span> <span data-ttu-id="76474-140">換句話說，Azure AD 使用者與 hello Printix 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="76474-140">In other words, a link relationship between an Azure AD user and hello related user in Printix needs toobe established.</span></span>

<span data-ttu-id="76474-141">Printix 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="76474-141">In Printix, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="76474-142">tooconfigure 及 Printix 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="76474-142">tooconfigure and test Azure AD single sign-on with Printix, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="76474-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="76474-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="76474-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="76474-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="76474-145">**[建立測試使用者 Printix](#creating-a-printix-test-user)**  -toohave 許 Simon Printix 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="76474-145">**[Creating a Printix test user](#creating-a-printix-test-user)** - toohave a counterpart of Britta Simon in Printix that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="76474-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="76474-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="76474-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="76474-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="76474-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="76474-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="76474-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Printix 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="76474-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Printix application.</span></span>

<span data-ttu-id="76474-150">**tooconfigure Azure AD 單一登入與 Printix，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="76474-150">**tooconfigure Azure AD single sign-on with Printix, perform hello following steps:**</span></span>

1. <span data-ttu-id="76474-151">在 Azure 入口網站上 hello hello **Printix**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="76474-151">In hello Azure portal, on hello **Printix** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="76474-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="76474-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-printix-tutorial/tutorial_printix_samlbase.png)

3. <span data-ttu-id="76474-155">在 hello **Printix 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="76474-155">On hello **Printix Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-printix-tutorial/tutorial_printix_url.png)

    <span data-ttu-id="76474-157">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.printix.net`</span><span class="sxs-lookup"><span data-stu-id="76474-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.printix.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="76474-158">hello 值不是真正的。</span><span class="sxs-lookup"><span data-stu-id="76474-158">hello value is not real.</span></span> <span data-ttu-id="76474-159">更新 hello 值與 hello 實際的登入 URL。</span><span class="sxs-lookup"><span data-stu-id="76474-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="76474-160">請連絡[Printix 用戶端支援小組](mailto:support@printix.net)tooget hello 值。</span><span class="sxs-lookup"><span data-stu-id="76474-160">Contact [Printix Client support team](mailto:support@printix.net) tooget hello value.</span></span> 
 
4. <span data-ttu-id="76474-161">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="76474-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-printix-tutorial/tutorial_printix_certificate.png) 

5. <span data-ttu-id="76474-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="76474-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-printix-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="76474-165">以系統管理員身分登入 tooyour Printix 租用戶。</span><span class="sxs-lookup"><span data-stu-id="76474-165">Sign-on tooyour Printix tenant as an administrator.</span></span>

7. <span data-ttu-id="76474-166">在 hello 最上層顯示 hello 功能表上，按一下 hello 在 hello 右上角的圖示並選取"**驗證**"。</span><span class="sxs-lookup"><span data-stu-id="76474-166">In hello menu on hello top, click hello icon at hello upper right corner and select "**Authentication**".</span></span>
   
    ![設定單一登入](./media/active-directory-saas-printix-tutorial/tutorial_printix_06.png)

8. <span data-ttu-id="76474-168">在 hello**安裝**索引標籤上，選取**啟用 Azure/Office 365 驗證**</span><span class="sxs-lookup"><span data-stu-id="76474-168">On hello **Setup** tab, select **Enable Azure/Office 365 authentication**</span></span>
   
    ![設定單一登入](./media/active-directory-saas-printix-tutorial/tutorial_printix_07.png)

9. <span data-ttu-id="76474-170">在 [hello **Azure**索引標籤上，輸入的同盟中繼資料 URL toohello] 文字方塊中的"**同盟中繼資料文件**"。</span><span class="sxs-lookup"><span data-stu-id="76474-170">On hello **Azure** tab, input federation metadata URL toohello textbox of "**Federation metadata document**".</span></span> 

    <span data-ttu-id="76474-171">附加 hello 太下載從 Azure AD 中繼資料 xml 檔案[Printix 支援小組](mailto:support@printix.net)。</span><span class="sxs-lookup"><span data-stu-id="76474-171">Attach hello metadata xml file which you downloaded from Azure AD too[Printix support team](mailto:support@printix.net).</span></span> <span data-ttu-id="76474-172">然後他們 hello xml 檔案上傳，並提供同盟中繼資料 URL。</span><span class="sxs-lookup"><span data-stu-id="76474-172">Then they upload hello xml file and provide a federation metadata URL.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-printix-tutorial/tutorial_printix_08.png)
   
10. <span data-ttu-id="76474-174">按一下 hello"**測試**」 按鈕，然後按一下 「**確定**」 按鈕如果 hello 測試成功。</span><span class="sxs-lookup"><span data-stu-id="76474-174">Click hello "**Test**" button and click "**OK**" button if hello test was successful.</span></span>
   
     <span data-ttu-id="76474-175">Azure active directory 頁面會顯示按一下 hello 之後**測試** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="76474-175">Azure active directory page will show after clicking hello **test** button.</span></span> <span data-ttu-id="76474-176">「 hello 測試成功 」 此處代表輸入您 Azure 測試帳戶，它會顯示 hello 認證後訊息 「 設定測試過 [確定]"。然後按一下 [hello**確定**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="76474-176">"hello test was successful" here means after entering hello credentials of your Azure test account it will pop up a message "Settings tested OK".Then click hello **OK** button.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-printix-tutorial/tutorial_printix_09.png)

11. <span data-ttu-id="76474-178">按一下 hello**儲存**按鈕"**驗證**」 頁面。</span><span class="sxs-lookup"><span data-stu-id="76474-178">Click hello **Save** button on "**Authentication**" page.</span></span>


> [!TIP]
> <span data-ttu-id="76474-179">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="76474-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="76474-180">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="76474-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="76474-181">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="76474-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="76474-182">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="76474-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="76474-183">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="76474-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="76474-185">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="76474-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="76474-186">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="76474-186">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-printix-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="76474-188">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="76474-188">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-printix-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="76474-190">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="76474-190">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-printix-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="76474-192">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="76474-192">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-printix-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="76474-194">a.</span><span class="sxs-lookup"><span data-stu-id="76474-194">a.</span></span> <span data-ttu-id="76474-195">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="76474-195">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="76474-196">b.</span><span class="sxs-lookup"><span data-stu-id="76474-196">b.</span></span> <span data-ttu-id="76474-197">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="76474-197">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="76474-198">c.</span><span class="sxs-lookup"><span data-stu-id="76474-198">c.</span></span> <span data-ttu-id="76474-199">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="76474-199">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="76474-200">d.</span><span class="sxs-lookup"><span data-stu-id="76474-200">d.</span></span> <span data-ttu-id="76474-201">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="76474-201">Click **Create**.</span></span>
 
### <a name="creating-a-printix-test-user"></a><span data-ttu-id="76474-202">建立 Printix 測試使用者</span><span class="sxs-lookup"><span data-stu-id="76474-202">Creating a Printix test user</span></span>

<span data-ttu-id="76474-203">hello 本節目標在於 toocreate Printix 中呼叫許 Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="76474-203">hello objective of this section is toocreate a user called Britta Simon in Printix.</span></span> <span data-ttu-id="76474-204">Printix 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="76474-204">Printix supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="76474-205">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="76474-205">There is no action item for you in this section.</span></span> <span data-ttu-id="76474-206">如果尚未存在期間嘗試 tooaccess Printix，建立新的使用者。</span><span class="sxs-lookup"><span data-stu-id="76474-206">A new user is created during an attempt tooaccess Printix if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="76474-207">若要手動 toocreate 使用者，您需要 toocontact hello [Printix 支援小組](mailto:support@printix.net)。</span><span class="sxs-lookup"><span data-stu-id="76474-207">If you need toocreate a user manually, you need toocontact hello [Printix support team](mailto:support@printix.net).</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="76474-208">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="76474-208">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="76474-209">在本節中，您可以授與存取 tooPrintix 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="76474-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPrintix.</span></span>

![指派使用者][200] 

<span data-ttu-id="76474-211">**tooassign 許 Simon tooPrintix，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="76474-211">**tooassign Britta Simon tooPrintix, perform hello following steps:**</span></span>

1. <span data-ttu-id="76474-212">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="76474-212">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="76474-214">在 [hello] 應用程式清單中，選取**Printix**。</span><span class="sxs-lookup"><span data-stu-id="76474-214">In hello applications list, select **Printix**.</span></span>

    ![設定單一登入](./media/active-directory-saas-printix-tutorial/tutorial_printix_app.png) 

3. <span data-ttu-id="76474-216">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="76474-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="76474-218">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="76474-218">Click **Add** button.</span></span> <span data-ttu-id="76474-219">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="76474-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="76474-221">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="76474-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="76474-222">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="76474-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="76474-223">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="76474-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="76474-224">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="76474-224">Testing single sign-on</span></span>

<span data-ttu-id="76474-225">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="76474-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="76474-226">當您按一下 hello Printix 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Printix 應用程式。</span><span class="sxs-lookup"><span data-stu-id="76474-226">When you click hello Printix tile in hello Access Panel, you should get automatically signed-on tooyour Printix application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="76474-227">其他資源</span><span class="sxs-lookup"><span data-stu-id="76474-227">Additional resources</span></span>

* [<span data-ttu-id="76474-228">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="76474-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="76474-229">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="76474-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-printix-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-printix-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-printix-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-printix-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-printix-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-printix-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-printix-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-printix-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-printix-tutorial/tutorial_general_203.png

