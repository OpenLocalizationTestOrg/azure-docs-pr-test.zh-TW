---
title: "教學課程：Azure Active Directory 與 ICIMS 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 ICIMS 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 72dbd649-e4b1-4d72-ad76-636d84922596
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 3fa970f008e64e84b0a1280f691f0181851b757c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-icims"></a><span data-ttu-id="9f4ae-103">教學課程：Azure Active Directory 與 ICIMS 整合</span><span class="sxs-lookup"><span data-stu-id="9f4ae-103">Tutorial: Azure Active Directory integration with ICIMS</span></span>

<span data-ttu-id="9f4ae-104">在此教學課程中，您學會如何 toointegrate ICIMS 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-104">In this tutorial, you learn how toointegrate ICIMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9f4ae-105">與 Azure AD 整合 ICIMS 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="9f4ae-105">Integrating ICIMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9f4ae-106">您可以控制存取 tooICIMS Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="9f4ae-106">You can control in Azure AD who has access tooICIMS</span></span>
- <span data-ttu-id="9f4ae-107">您可以啟用您的使用者 tooautomatically get 登入 tooICIMS （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="9f4ae-107">You can enable your users tooautomatically get signed-on tooICIMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9f4ae-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="9f4ae-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9f4ae-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9f4ae-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="9f4ae-110">Prerequisites</span></span>

<span data-ttu-id="9f4ae-111">tooconfigure ICIMS 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="9f4ae-111">tooconfigure Azure AD integration with ICIMS, you need hello following items:</span></span>

- <span data-ttu-id="9f4ae-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="9f4ae-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9f4ae-113">已啟用 ICIMS 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="9f4ae-113">An ICIMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9f4ae-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9f4ae-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="9f4ae-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9f4ae-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9f4ae-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9f4ae-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="9f4ae-118">Scenario description</span></span>
<span data-ttu-id="9f4ae-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9f4ae-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="9f4ae-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9f4ae-121">從 hello 圖庫加入 ICIMS</span><span class="sxs-lookup"><span data-stu-id="9f4ae-121">Adding ICIMS from hello gallery</span></span>
2. <span data-ttu-id="9f4ae-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="9f4ae-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-icims-from-hello-gallery"></a><span data-ttu-id="9f4ae-123">從 hello 圖庫加入 ICIMS</span><span class="sxs-lookup"><span data-stu-id="9f4ae-123">Adding ICIMS from hello gallery</span></span>
<span data-ttu-id="9f4ae-124">tooconfigure hello 整合 ICIMS 到 Azure AD，您需要 tooadd ICIMS hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-124">tooconfigure hello integration of ICIMS into Azure AD, you need tooadd ICIMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9f4ae-125">**tooadd ICIMS 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="9f4ae-125">**tooadd ICIMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f4ae-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 按鈕][1]

2. <span data-ttu-id="9f4ae-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9f4ae-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-129">Then go too**All applications**.</span></span>

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. <span data-ttu-id="9f4ae-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 新應用程式按鈕][3]

4. <span data-ttu-id="9f4ae-133">在 hello 搜尋方塊中，輸入**ICIMS**，選取**ICIMS**然後按一下 從結果面板**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-133">In hello search box, type **ICIMS**, select **ICIMS** from result panel then click **Add** button tooadd hello application.</span></span>

    ![ICIMS hello [結果] 清單中](./media/active-directory-saas-icims-tutorial/tutorial_icims_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9f4ae-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="9f4ae-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="9f4ae-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 ICIMS 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-136">In this section, you configure and test Azure AD single sign-on with ICIMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9f4ae-137">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 ICIMS 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ICIMS is tooa user in Azure AD.</span></span> <span data-ttu-id="9f4ae-138">換句話說，Azure AD 使用者與 hello ICIMS 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-138">In other words, a link relationship between an Azure AD user and hello related user in ICIMS needs toobe established.</span></span>

<span data-ttu-id="9f4ae-139">ICIMS 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-139">In ICIMS, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9f4ae-140">tooconfigure 及 ICIMS 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="9f4ae-140">tooconfigure and test Azure AD single sign-on with ICIMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9f4ae-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9f4ae-142">**[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9f4ae-143">**[建立測試使用者 ICIMS](#create-an-icims-test-user)**  -toohave 許 Simon ICIMS 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-143">**[Create an ICIMS test user](#create-an-icims-test-user)** - toohave a counterpart of Britta Simon in ICIMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9f4ae-144">**[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9f4ae-145">**[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9f4ae-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="9f4ae-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="9f4ae-147">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 ICIMS 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ICIMS application.</span></span>

<span data-ttu-id="9f4ae-148">**tooconfigure Azure AD 單一登入與 ICIMS，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="9f4ae-148">**tooconfigure Azure AD single sign-on with ICIMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f4ae-149">在 Azure 入口網站上 hello hello **ICIMS**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-149">In hello Azure portal, on hello **ICIMS** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="9f4ae-151">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-icims-tutorial/tutorial_icims_samlbase.png)

3. <span data-ttu-id="9f4ae-153">在 hello **ICIMS 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="9f4ae-153">On hello **ICIMS Domain and URLs** section, perform hello following steps:</span></span>

    ![ICIMS 網域及 URL 單一登入資訊](./media/active-directory-saas-icims-tutorial/tutorial_icims_url.png)

    <span data-ttu-id="9f4ae-155">a.</span><span class="sxs-lookup"><span data-stu-id="9f4ae-155">a.</span></span> <span data-ttu-id="9f4ae-156">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<tenant name>.icims.com`</span><span class="sxs-lookup"><span data-stu-id="9f4ae-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant name>.icims.com`</span></span>

    <span data-ttu-id="9f4ae-157">b.</span><span class="sxs-lookup"><span data-stu-id="9f4ae-157">b.</span></span> <span data-ttu-id="9f4ae-158">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<tenant name>.icims.com`</span><span class="sxs-lookup"><span data-stu-id="9f4ae-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant name>.icims.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9f4ae-159">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-159">These values are not real.</span></span> <span data-ttu-id="9f4ae-160">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="9f4ae-161">請連絡[ICIMS 用戶端支援小組](https://www.icims.com/contact-us)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-161">Contact [ICIMS Client support team](https://www.icims.com/contact-us) tooget these values.</span></span> 
 
4. <span data-ttu-id="9f4ae-162">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![hello 憑證下載連結](./media/active-directory-saas-icims-tutorial/tutorial_icims_certificate.png) 

5. <span data-ttu-id="9f4ae-164">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-164">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-icims-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9f4ae-166">在 hello **ICIMS 組態**區段中，按一下**設定 ICIMS** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-166">On hello **ICIMS Configuration** section, click **Configure ICIMS** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9f4ae-167">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="9f4ae-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![ICIMS 組態](./media/active-directory-saas-icims-tutorial/tutorial_icims_configure.png) 

7. <span data-ttu-id="9f4ae-169">tooconfigure 單一登入上**ICIMS**端，您需要下載 toosend hello**中繼資料 XML**，**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**太[ICIMS 支援小組](https://www.icims.com/contact-us)。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-169">tooconfigure single sign-on on **ICIMS** side, you need toosend hello downloaded **Metadata XML**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[ICIMS support team](https://www.icims.com/contact-us).</span></span> <span data-ttu-id="9f4ae-170">設定此設定 toohave hello SAML SSO 連線兩端上正確設定這些欄位。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="9f4ae-171">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="9f4ae-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9f4ae-172">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9f4ae-173">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9f4ae-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9f4ae-174">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="9f4ae-174">Create an Azure AD test user</span></span>
<span data-ttu-id="9f4ae-175">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 測試使用者][100]

<span data-ttu-id="9f4ae-177">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="9f4ae-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f4ae-178">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-icims-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9f4ae-180">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-icims-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9f4ae-182">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![hello [新增] 按鈕](./media/active-directory-saas-icims-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9f4ae-184">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="9f4ae-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![hello [使用者] 對話方塊](./media/active-directory-saas-icims-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9f4ae-186">a.</span><span class="sxs-lookup"><span data-stu-id="9f4ae-186">a.</span></span> <span data-ttu-id="9f4ae-187">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9f4ae-188">b.</span><span class="sxs-lookup"><span data-stu-id="9f4ae-188">b.</span></span> <span data-ttu-id="9f4ae-189">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9f4ae-190">c.</span><span class="sxs-lookup"><span data-stu-id="9f4ae-190">c.</span></span> <span data-ttu-id="9f4ae-191">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9f4ae-192">d.</span><span class="sxs-lookup"><span data-stu-id="9f4ae-192">d.</span></span> <span data-ttu-id="9f4ae-193">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-193">Click **Create**.</span></span>
 
### <a name="create-an-icims-test-user"></a><span data-ttu-id="9f4ae-194">建立 ICIMS 測試使用者</span><span class="sxs-lookup"><span data-stu-id="9f4ae-194">Create an ICIMS test user</span></span>

<span data-ttu-id="9f4ae-195">hello 本節目標在於 toocreate ICIMS 中呼叫許 Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-195">hello objective of this section is toocreate a user called Britta Simon in ICIMS.</span></span> <span data-ttu-id="9f4ae-196">使用[ICIMS 支援小組](https://www.icims.com/contact-us)tooadd hello hello ICIMS 帳戶的使用者。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-196">Work with [ICIMS support team](https://www.icims.com/contact-us) tooadd hello users in hello ICIMS account.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="9f4ae-197">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="9f4ae-197">Assign hello Azure AD test user</span></span>

<span data-ttu-id="9f4ae-198">在本節中，您可以授與存取 tooICIMS 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooICIMS.</span></span>

![指派 hello 使用者角色][200]

<span data-ttu-id="9f4ae-200">**tooassign 許 Simon tooICIMS，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="9f4ae-200">**tooassign Britta Simon tooICIMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f4ae-201">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="9f4ae-203">在 [hello] 應用程式清單中，選取**ICIMS**。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-203">In hello applications list, select **ICIMS**.</span></span>

    ![hello 應用程式清單中的 hello ICIMS 連結](./media/active-directory-saas-icims-tutorial/tutorial_icims_app.png) 

3. <span data-ttu-id="9f4ae-205">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello 「 使用者和群組 」 的連結][202] 

4. <span data-ttu-id="9f4ae-207">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-207">Click **Add** button.</span></span> <span data-ttu-id="9f4ae-208">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 將作業加入窗格][203]

5. <span data-ttu-id="9f4ae-210">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9f4ae-211">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9f4ae-212">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="9f4ae-213">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="9f4ae-213">Test single sign-on</span></span>

<span data-ttu-id="9f4ae-214">hello 本節目標在於 tootest 您 Azure AD 的 SSO 組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-214">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="9f4ae-215">當您按一下的 hello ICIMS 磚 hello 存取面板中時，您應該取得自動登入 tooyour ICIMS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9f4ae-215">When you click hello ICIMS tile in hello Access Panel, you should get automatically signed-on tooyour ICIMS application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9f4ae-216">其他資源</span><span class="sxs-lookup"><span data-stu-id="9f4ae-216">Additional resources</span></span>

* [<span data-ttu-id="9f4ae-217">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9f4ae-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9f4ae-218">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="9f4ae-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-icims-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-icims-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-icims-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-icims-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-icims-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-icims-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-icims-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-icims-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-icims-tutorial/tutorial_general_203.png

