---
title: "教學課程：Azure Active Directory 與 Predictix Assortment Planning 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Predictix 分類規劃之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 37e686ff-f8e5-40b1-9d7e-f64b076917b7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 1294b712caf12fdafaf65d70a02ee9fbdc3e84a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-predictix-assortment-planning"></a><span data-ttu-id="89b9a-103">教學課程：Azure Active Directory 與 Predictix Assortment Planning 整合</span><span class="sxs-lookup"><span data-stu-id="89b9a-103">Tutorial: Azure Active Directory integration with Predictix Assortment Planning</span></span>

<span data-ttu-id="89b9a-104">在此教學課程中，您學會如何 toointegrate Predictix 規劃與 Azure Active Directory (Azure AD) 的分類。</span><span class="sxs-lookup"><span data-stu-id="89b9a-104">In this tutorial, you learn how toointegrate Predictix Assortment Planning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="89b9a-105">整合 Predictix 分類的規劃與 Azure AD 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="89b9a-105">Integrating Predictix Assortment Planning with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="89b9a-106">您可以控制存取 tooPredictix 分類規劃 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="89b9a-106">You can control in Azure AD who has access tooPredictix Assortment Planning.</span></span>
- <span data-ttu-id="89b9a-107">您可以使用其 Azure AD 帳戶啟用您使用者 tooautomatically get 登入 tooPredictix 分類規劃 （單一登入）。</span><span class="sxs-lookup"><span data-stu-id="89b9a-107">You can enable your users tooautomatically get signed-on tooPredictix Assortment Planning (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="89b9a-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="89b9a-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="89b9a-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="89b9a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89b9a-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="89b9a-110">Prerequisites</span></span>

<span data-ttu-id="89b9a-111">tooconfigure Predictix 分類規劃 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="89b9a-111">tooconfigure Azure AD integration with Predictix Assortment Planning, you need hello following items:</span></span>

- <span data-ttu-id="89b9a-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="89b9a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="89b9a-113">啟用 Predictix Assortment Planning 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="89b9a-113">A Predictix Assortment Planning single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="89b9a-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="89b9a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="89b9a-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="89b9a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="89b9a-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="89b9a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="89b9a-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="89b9a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="89b9a-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="89b9a-118">Scenario description</span></span>
<span data-ttu-id="89b9a-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="89b9a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="89b9a-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="89b9a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="89b9a-121">從 hello 組件庫中加入 Predictix 分類的規劃</span><span class="sxs-lookup"><span data-stu-id="89b9a-121">Adding Predictix Assortment Planning from hello gallery</span></span>
2. <span data-ttu-id="89b9a-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="89b9a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-predictix-assortment-planning-from-hello-gallery"></a><span data-ttu-id="89b9a-123">從 hello 組件庫中加入 Predictix 分類的規劃</span><span class="sxs-lookup"><span data-stu-id="89b9a-123">Adding Predictix Assortment Planning from hello gallery</span></span>
<span data-ttu-id="89b9a-124">tooconfigure hello 整合 Predictix 分類規劃到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Predictix 分類的規劃。</span><span class="sxs-lookup"><span data-stu-id="89b9a-124">tooconfigure hello integration of Predictix Assortment Planning into Azure AD, you need tooadd Predictix Assortment Planning from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="89b9a-125">**tooadd Predictix 分類規劃從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="89b9a-125">**tooadd Predictix Assortment Planning from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="89b9a-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="89b9a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 按鈕][1]

2. <span data-ttu-id="89b9a-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="89b9a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="89b9a-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="89b9a-129">Then go too**All applications**.</span></span>

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. <span data-ttu-id="89b9a-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="89b9a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 新應用程式按鈕][3]

4. <span data-ttu-id="89b9a-133">在 hello 搜尋方塊中，輸入**Predictix 分類規劃**，選取**Predictix 分類規劃**然後按一下 從結果面板**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="89b9a-133">In hello search box, type **Predictix Assortment Planning**, select **Predictix Assortment Planning** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Predictix 規劃 hello [結果] 清單中的分類](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="89b9a-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="89b9a-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="89b9a-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Predictix Assortment Planning 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="89b9a-136">In this section, you configure and test Azure AD single sign-on with Predictix Assortment Planning based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="89b9a-137">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者 Predictix 分類規劃是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="89b9a-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Predictix Assortment Planning is tooa user in Azure AD.</span></span> <span data-ttu-id="89b9a-138">換句話說，Azure AD 使用者與 hello Predictix 分類規劃的相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="89b9a-138">In other words, a link relationship between an Azure AD user and hello related user in Predictix Assortment Planning needs toobe established.</span></span>

<span data-ttu-id="89b9a-139">Predictix 分類規劃 hello hello 值指派**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="89b9a-139">In Predictix Assortment Planning, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="89b9a-140">tooconfigure 及 Azure AD 單一登入具有 Predictix 分類計劃的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="89b9a-140">tooconfigure and test Azure AD single sign-on with Predictix Assortment Planning, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="89b9a-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="89b9a-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="89b9a-142">**[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="89b9a-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="89b9a-143">**[建立測試使用者 Predictix 分類規劃](#create-a-predictix-assortment-planning-test-user)** -toohave 許 Simon Predictix 分類規劃連結的 toohello Azure AD 使用者表示法的對應項目。</span><span class="sxs-lookup"><span data-stu-id="89b9a-143">**[Create a Predictix Assortment Planning test user](#create-a-predictix-assortment-planning-test-user)** - toohave a counterpart of Britta Simon in Predictix Assortment Planning that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="89b9a-144">**[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="89b9a-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="89b9a-145">**[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="89b9a-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="89b9a-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="89b9a-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="89b9a-147">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Predictix 分類規劃應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="89b9a-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Predictix Assortment Planning application.</span></span>

<span data-ttu-id="89b9a-148">**利用 Predictix 分類的規劃，Azure AD 單一登入 tooconfigure 執行 hello 下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="89b9a-148">**tooconfigure Azure AD single sign-on with Predictix Assortment Planning, perform hello following steps:**</span></span>

1. <span data-ttu-id="89b9a-149">在 Azure 入口網站上 hello hello **Predictix 分類規劃**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="89b9a-149">In hello Azure portal, on hello **Predictix Assortment Planning** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="89b9a-151">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="89b9a-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_samlbase.png)

3. <span data-ttu-id="89b9a-153">在 hello **Predictix 分類規劃網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="89b9a-153">On hello **Predictix Assortment Planning Domain and URLs** section, perform hello following steps:</span></span>

    ![Predictix Assortment Planning 網域及 URL 單一登入資訊](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_url.png)

    <span data-ttu-id="89b9a-155">a.</span><span class="sxs-lookup"><span data-stu-id="89b9a-155">a.</span></span> <span data-ttu-id="89b9a-156">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:</span><span class="sxs-lookup"><span data-stu-id="89b9a-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|--|
    | `https://<sub-domain>.ap.predictix.com/sso/request`|
    | `https://<sub-domain>.dev.ap.predictix.com/`|

    <span data-ttu-id="89b9a-157">b.</span><span class="sxs-lookup"><span data-stu-id="89b9a-157">b.</span></span> <span data-ttu-id="89b9a-158">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:</span><span class="sxs-lookup"><span data-stu-id="89b9a-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|--|
    | `https://<sub-domain>.ap.predictix.com`|
    | `https://<sub-domain>.dev.ap.predictix.com`|
    
    > [!NOTE] 
    > <span data-ttu-id="89b9a-159">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="89b9a-159">These values are not real.</span></span> <span data-ttu-id="89b9a-160">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="89b9a-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="89b9a-161">請連絡[Predictix 分類規劃用戶端支援小組](http://www.infor.com/support)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="89b9a-161">Contact [Predictix Assortment Planning Client support team](http://www.infor.com/support) tooget these values.</span></span> 
 


4. <span data-ttu-id="89b9a-162">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="89b9a-162">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![hello 憑證下載連結](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_certificate.png) 

5. <span data-ttu-id="89b9a-164">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="89b9a-164">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="89b9a-166">在 hello **Predictix 分類規劃 Configuration**區段中，按一下**設定 Predictix 分類規劃**tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="89b9a-166">On hello **Predictix Assortment Planning Configuration** section, click **Configure Predictix Assortment Planning** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="89b9a-167">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="89b9a-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Predictix Assortment Planning 設定](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_configure.png) 

7. <span data-ttu-id="89b9a-169">tooconfigure 單一登入上**Predictix 分類規劃**端，您需要下載 toosend hello **Certificate(Base64)**， **SAML 實體識別碼**， **SAML 單一登入服務 URL**，和**登出 URL**太[Predictix 分類規劃支援小組](http://www.infor.com/support)。</span><span class="sxs-lookup"><span data-stu-id="89b9a-169">tooconfigure single sign-on on **Predictix Assortment Planning** side, you need toosend hello downloaded **Certificate(Base64)**, **SAML Entity ID**, **SAML Single Sign-On Service URL**, and **Sign-Out URL**  too[Predictix Assortment Planning support team](http://www.infor.com/support).</span></span> <span data-ttu-id="89b9a-170">設定此設定 toohave hello SAML SSO 連線兩端上正確設定這些欄位。</span><span class="sxs-lookup"><span data-stu-id="89b9a-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="89b9a-171">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="89b9a-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="89b9a-172">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="89b9a-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="89b9a-173">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="89b9a-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="89b9a-174">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="89b9a-174">Create an Azure AD test user</span></span>

<span data-ttu-id="89b9a-175">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="89b9a-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="89b9a-177">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="89b9a-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="89b9a-178">在 hello Azure 入口網站，hello 左窗格中，按一下 hello **Azure Active Directory**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="89b9a-178">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="89b9a-180">toodisplay hello 使用者清單，請移過**使用者和群組**，然後按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="89b9a-180">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="89b9a-182">tooopen hello**使用者**對話方塊中，按一下 [**新增**頂端的 hello hello**所有使用者**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="89b9a-182">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello [新增] 按鈕](./media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="89b9a-184">在 hello**使用者**對話方塊方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="89b9a-184">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello [使用者] 對話方塊](./media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_04.png)

    <span data-ttu-id="89b9a-186">a.</span><span class="sxs-lookup"><span data-stu-id="89b9a-186">a.</span></span> <span data-ttu-id="89b9a-187">在 hello**名稱**方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="89b9a-187">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="89b9a-188">b.</span><span class="sxs-lookup"><span data-stu-id="89b9a-188">b.</span></span> <span data-ttu-id="89b9a-189">在 hello**使用者名**方塊中，使用者許 Simon 類型 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="89b9a-189">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="89b9a-190">c.</span><span class="sxs-lookup"><span data-stu-id="89b9a-190">c.</span></span> <span data-ttu-id="89b9a-191">選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 hello**密碼**方塊。</span><span class="sxs-lookup"><span data-stu-id="89b9a-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="89b9a-192">d.</span><span class="sxs-lookup"><span data-stu-id="89b9a-192">d.</span></span> <span data-ttu-id="89b9a-193">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="89b9a-193">Click **Create**.</span></span>
 
### <a name="create-a-predictix-assortment-planning-test-user"></a><span data-ttu-id="89b9a-194">建立 Predictix Assortment Planning 測試使用者</span><span class="sxs-lookup"><span data-stu-id="89b9a-194">Create a Predictix Assortment Planning test user</span></span>

<span data-ttu-id="89b9a-195">在本節中，您要在 Predictix Assortment Planning 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="89b9a-195">In this section, you create a user called Britta Simon in Predictix Assortment Planning.</span></span> <span data-ttu-id="89b9a-196">請使用[Predictix 分類規劃支援小組](http://www.infor.com/contact/)tooadd hello hello Predictix 分類規劃平台的使用者。</span><span class="sxs-lookup"><span data-stu-id="89b9a-196">Please work with [Predictix Assortment Planning support team](http://www.infor.com/contact/) tooadd hello users in hello Predictix Assortment Planning platform.</span></span>
 > [!NOTE]
 > <span data-ttu-id="89b9a-197">hello Azure Active Directory 帳戶持有者會收到一封電子郵件，並且遵循連結 tooconfirm 他們的帳戶之前就會生效。</span><span class="sxs-lookup"><span data-stu-id="89b9a-197">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="89b9a-198">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="89b9a-198">Assign hello Azure AD test user</span></span>

<span data-ttu-id="89b9a-199">在本節中，以啟用許 Simon toouse Azure 單一登入授與存取 tooPredictix 分類的規劃。</span><span class="sxs-lookup"><span data-stu-id="89b9a-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPredictix Assortment Planning.</span></span>

![指派 hello 使用者角色][200] 

<span data-ttu-id="89b9a-201">**tooassign 許 Simon tooPredictix 分類的規劃，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="89b9a-201">**tooassign Britta Simon tooPredictix Assortment Planning, perform hello following steps:**</span></span>

1. <span data-ttu-id="89b9a-202">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="89b9a-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="89b9a-204">在 [hello] 應用程式清單中，選取**Predictix 分類規劃**。</span><span class="sxs-lookup"><span data-stu-id="89b9a-204">In hello applications list, select **Predictix Assortment Planning**.</span></span>

    ![hello 應用程式清單中的 hello Predictix 分類規劃連結](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_app.png)  

3. <span data-ttu-id="89b9a-206">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="89b9a-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello 「 使用者和群組 」 的連結][202]

4. <span data-ttu-id="89b9a-208">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="89b9a-208">Click **Add** button.</span></span> <span data-ttu-id="89b9a-209">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="89b9a-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 將作業加入窗格][203]

5. <span data-ttu-id="89b9a-211">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="89b9a-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="89b9a-212">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="89b9a-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="89b9a-213">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="89b9a-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="89b9a-214">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="89b9a-214">Test single sign-on</span></span>

<span data-ttu-id="89b9a-215">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="89b9a-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="89b9a-216">當您按一下 hello Predictix 分類規劃並排顯示 hello 存取面板中的時，您應該取得自動登入 tooyour Predictix 分類規劃應用程式。</span><span class="sxs-lookup"><span data-stu-id="89b9a-216">When you click hello Predictix Assortment Planning tile in hello Access Panel, you should get automatically signed-on tooyour Predictix Assortment Planning application.</span></span>
<span data-ttu-id="89b9a-217">如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="89b9a-217">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="89b9a-218">其他資源</span><span class="sxs-lookup"><span data-stu-id="89b9a-218">Additional resources</span></span>

* [<span data-ttu-id="89b9a-219">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="89b9a-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="89b9a-220">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="89b9a-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_203.png

