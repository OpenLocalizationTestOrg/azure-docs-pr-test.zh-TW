---
title: "教學課程：Azure Active Directory 與 Ceridian Dayforce HCM 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Ceridian Dayforce HCM 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7adf1eb3-d063-45d6-96a8-fd53b329b3f3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 4d72f29b4e5e30ef8881806d789f6676fc541e2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ceridian-dayforce-hcm"></a><span data-ttu-id="21c16-103">教學課程：Azure Active Directory 與 Ceridian Dayforce HCM 整合</span><span class="sxs-lookup"><span data-stu-id="21c16-103">Tutorial: Azure Active Directory integration with Ceridian Dayforce HCM</span></span>

<span data-ttu-id="21c16-104">在此教學課程中，您學會如何 toointegrate Ceridian Dayforce HCM 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="21c16-104">In this tutorial, you learn how toointegrate Ceridian Dayforce HCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="21c16-105">與 Azure AD 整合 Ceridian Dayforce HCM 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="21c16-105">Integrating Ceridian Dayforce HCM with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="21c16-106">您可以控制存取 tooCeridian Dayforce HCM Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="21c16-106">You can control in Azure AD who has access tooCeridian Dayforce HCM.</span></span>
- <span data-ttu-id="21c16-107">您可以使用其 Azure AD 帳戶啟用您的使用者 tooautomatically get 登入 tooCeridian Dayforce HCM （單一登入）。</span><span class="sxs-lookup"><span data-stu-id="21c16-107">You can enable your users tooautomatically get signed-on tooCeridian Dayforce HCM (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="21c16-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="21c16-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="21c16-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="21c16-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="21c16-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="21c16-110">Prerequisites</span></span>

<span data-ttu-id="21c16-111">tooconfigure Ceridian Dayforce HCM 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="21c16-111">tooconfigure Azure AD integration with Ceridian Dayforce HCM, you need hello following items:</span></span>

- <span data-ttu-id="21c16-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="21c16-112">An Azure AD subscription</span></span>
- <span data-ttu-id="21c16-113">啟用 Ceridian Dayforce HCM 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="21c16-113">A Ceridian Dayforce HCM single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="21c16-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="21c16-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="21c16-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="21c16-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="21c16-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="21c16-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="21c16-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="21c16-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="21c16-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="21c16-118">Scenario description</span></span>
<span data-ttu-id="21c16-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="21c16-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="21c16-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="21c16-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="21c16-121">從 hello 圖庫加入 Ceridian Dayforce HCM</span><span class="sxs-lookup"><span data-stu-id="21c16-121">Adding Ceridian Dayforce HCM from hello gallery</span></span>
2. <span data-ttu-id="21c16-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="21c16-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ceridian-dayforce-hcm-from-hello-gallery"></a><span data-ttu-id="21c16-123">從 hello 圖庫加入 Ceridian Dayforce HCM</span><span class="sxs-lookup"><span data-stu-id="21c16-123">Adding Ceridian Dayforce HCM from hello gallery</span></span>
<span data-ttu-id="21c16-124">tooconfigure hello 整合 Ceridian Dayforce HCM 到 Azure AD，您需要 tooadd Ceridian Dayforce HCM hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="21c16-124">tooconfigure hello integration of Ceridian Dayforce HCM into Azure AD, you need tooadd Ceridian Dayforce HCM from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="21c16-125">**tooadd Ceridian Dayforce HCM 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="21c16-125">**tooadd Ceridian Dayforce HCM from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="21c16-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="21c16-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 按鈕][1]

2. <span data-ttu-id="21c16-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="21c16-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="21c16-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="21c16-129">Then go too**All applications**.</span></span>

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. <span data-ttu-id="21c16-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="21c16-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 新應用程式按鈕][3]

4. <span data-ttu-id="21c16-133">在 hello 搜尋方塊中，輸入**Ceridian Dayforce HCM**，選取**Ceridian Dayforce HCM**然後按一下 從結果面板**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="21c16-133">In hello search box, type **Ceridian Dayforce HCM**, select **Ceridian Dayforce HCM** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Ceridian Dayforce HCM hello [結果] 清單中](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="21c16-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="21c16-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="21c16-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Ceridian Dayforce HCM 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="21c16-136">In this section, you configure and test Azure AD single sign-on with Ceridian Dayforce HCM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="21c16-137">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Ceridian Dayforce HCM 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="21c16-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Ceridian Dayforce HCM is tooa user in Azure AD.</span></span> <span data-ttu-id="21c16-138">換句話說，Azure AD 使用者與 hello Ceridian Dayforce HCM 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="21c16-138">In other words, a link relationship between an Azure AD user and hello related user in Ceridian Dayforce HCM needs toobe established.</span></span>

<span data-ttu-id="21c16-139">Ceridian Dayforce HCM 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="21c16-139">In Ceridian Dayforce HCM, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="21c16-140">tooconfigure 及 Ceridian Dayforce HCM 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="21c16-140">tooconfigure and test Azure AD single sign-on with Ceridian Dayforce HCM, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="21c16-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="21c16-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="21c16-142">**[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="21c16-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="21c16-143">**[建立測試使用者 Ceridian Dayforce HCM](#create-a-ceridian-dayforce-hcm-test-user)**  -toohave 許 Simon Ceridian Dayforce HCM 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="21c16-143">**[Create a Ceridian Dayforce HCM test user](#create-a-ceridian-dayforce-hcm-test-user)** - toohave a counterpart of Britta Simon in Ceridian Dayforce HCM that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="21c16-144">**[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="21c16-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="21c16-145">**[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="21c16-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="21c16-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="21c16-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="21c16-147">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Ceridian Dayforce HCM 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="21c16-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Ceridian Dayforce HCM application.</span></span>

<span data-ttu-id="21c16-148">**tooconfigure Azure AD 單一登入與 Ceridian Dayforce HCM，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="21c16-148">**tooconfigure Azure AD single sign-on with Ceridian Dayforce HCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="21c16-149">在 Azure 入口網站上 hello hello **Ceridian Dayforce HCM**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="21c16-149">In hello Azure portal, on hello **Ceridian Dayforce HCM** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="21c16-151">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="21c16-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_samlbase.png)

3. <span data-ttu-id="21c16-153">在 hello **Ceridian Dayforce HCM 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="21c16-153">On hello **Ceridian Dayforce HCM Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_url.png)
    
    <span data-ttu-id="21c16-155">a.</span><span class="sxs-lookup"><span data-stu-id="21c16-155">a.</span></span> <span data-ttu-id="21c16-156">在 hello**登入 URL**文字方塊中，您的使用者 」 toosign 上 Ceridian Dayforce HCM 應用程式 tooyour 所使用的型別 hello URL。</span><span class="sxs-lookup"><span data-stu-id="21c16-156">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour Ceridian Dayforce HCM application.</span></span>
    
    | <span data-ttu-id="21c16-157">Environment</span><span class="sxs-lookup"><span data-stu-id="21c16-157">Environment</span></span> | <span data-ttu-id="21c16-158">URL</span><span class="sxs-lookup"><span data-stu-id="21c16-158">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="21c16-159">針對生產環境</span><span class="sxs-lookup"><span data-stu-id="21c16-159">For production</span></span> | `https://sso.dayforcehcm.com/<DayforcehcmNamespace>` |
    | <span data-ttu-id="21c16-160">針對測試</span><span class="sxs-lookup"><span data-stu-id="21c16-160">For test</span></span> | `https://ssotest.dayforcehcm.com/<DayforcehcmNamespace>` |
    
    <span data-ttu-id="21c16-161">b.</span><span class="sxs-lookup"><span data-stu-id="21c16-161">b.</span></span> <span data-ttu-id="21c16-162">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:</span><span class="sxs-lookup"><span data-stu-id="21c16-162">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    
    | <span data-ttu-id="21c16-163">Environment</span><span class="sxs-lookup"><span data-stu-id="21c16-163">Environment</span></span> | <span data-ttu-id="21c16-164">URL</span><span class="sxs-lookup"><span data-stu-id="21c16-164">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="21c16-165">針對生產環境</span><span class="sxs-lookup"><span data-stu-id="21c16-165">For production</span></span> | `https://ncpingfederate.dayforcehcm.com/sp` |
    | <span data-ttu-id="21c16-166">針對測試</span><span class="sxs-lookup"><span data-stu-id="21c16-166">For test</span></span> | `https://fs-test.dayforcehcm.com/sp` |
    
    <span data-ttu-id="21c16-167">c.</span><span class="sxs-lookup"><span data-stu-id="21c16-167">c.</span></span> <span data-ttu-id="21c16-168">在 hello**回覆 URL**文字方塊中，Azure AD toopost hello 回應所使用的型別 hello URL。</span><span class="sxs-lookup"><span data-stu-id="21c16-168">In hello **Reply URL** textbox, type hello URL used by Azure AD toopost hello response.</span></span>
    
    | <span data-ttu-id="21c16-169">Environment</span><span class="sxs-lookup"><span data-stu-id="21c16-169">Environment</span></span> | <span data-ttu-id="21c16-170">URL</span><span class="sxs-lookup"><span data-stu-id="21c16-170">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="21c16-171">針對生產環境</span><span class="sxs-lookup"><span data-stu-id="21c16-171">For production</span></span> | `https://ncpingfederate.dayforcehcm.com/sp/ACS.saml2` |
    | <span data-ttu-id="21c16-172">針對測試</span><span class="sxs-lookup"><span data-stu-id="21c16-172">For test</span></span> | `https://fs-test.dayforcehcm.com/sp/ACS.saml2` |
    
    > [!NOTE] 
    > <span data-ttu-id="21c16-173">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="21c16-173">These values are not real.</span></span> <span data-ttu-id="21c16-174">更新這些值與實際的 hello，識別項、 回覆 URL 和登入 URL。</span><span class="sxs-lookup"><span data-stu-id="21c16-174">Update these values with hello actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="21c16-175">請連絡[Ceridian Dayforce HCM 用戶端支援小組](https://www.ceridian.com/contact-us/index.html)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="21c16-175">Contact [Ceridian Dayforce HCM Client support team](https://www.ceridian.com/contact-us/index.html) tooget these values.</span></span>

4. <span data-ttu-id="21c16-176">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="21c16-176">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![hello 憑證下載連結](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_certificate.png) 

5. <span data-ttu-id="21c16-178">Ceridian Dayforce HCM 應用程式預期 hello SAML 判斷提示，以特定格式。</span><span class="sxs-lookup"><span data-stu-id="21c16-178">Your Ceridian Dayforce HCM application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="21c16-179">使用[Ceridian Dayforce HCM 支援小組](https://www.ceridian.com/contact-us/index.html)第一個 tooidentify hello 正確的使用者識別項。</span><span class="sxs-lookup"><span data-stu-id="21c16-179">Work with [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html) first tooidentify hello correct user identifier.</span></span> <span data-ttu-id="21c16-180">Microsoft 建議使用 hello **"name"**當做使用者識別碼屬性。</span><span class="sxs-lookup"><span data-stu-id="21c16-180">Microsoft recommends using hello **"name"** attribute as user identifier.</span></span> <span data-ttu-id="21c16-181">您可以從 hello 管理這些屬性的 hello 值**使用者屬性**應用程式整合頁面上的一節。</span><span class="sxs-lookup"><span data-stu-id="21c16-181">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span> <span data-ttu-id="21c16-182">hello 下列螢幕擷取畫面會顯示這個範例。</span><span class="sxs-lookup"><span data-stu-id="21c16-182">hello following screenshot shows an example for this.</span></span>  

    ![設定單一登入](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_07.png)

6. <span data-ttu-id="21c16-184">在 hello**使用者屬性**區段 hello**單一登入** 對話方塊中，上述 hello 映像中所示設定 SAML 權杖屬性和執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="21c16-184">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="21c16-185">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="21c16-185">Attribute Name</span></span>  | <span data-ttu-id="21c16-186">屬性值</span><span class="sxs-lookup"><span data-stu-id="21c16-186">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    | <span data-ttu-id="21c16-187">名稱</span><span class="sxs-lookup"><span data-stu-id="21c16-187">name</span></span>  | <span data-ttu-id="21c16-188">user.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="21c16-188">user.extensionattribute2</span></span> |    

    <span data-ttu-id="21c16-189">a.</span><span class="sxs-lookup"><span data-stu-id="21c16-189">a.</span></span> <span data-ttu-id="21c16-190">按一下**加入屬性**tooopen hello**加入屬性**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="21c16-190">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_04.png)

    ![設定單一登入](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="21c16-193">b.</span><span class="sxs-lookup"><span data-stu-id="21c16-193">b.</span></span> <span data-ttu-id="21c16-194">在 hello**名稱**文字方塊中，該資料列所顯示的型別 hello 屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="21c16-194">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="21c16-195">c.</span><span class="sxs-lookup"><span data-stu-id="21c16-195">c.</span></span> <span data-ttu-id="21c16-196">在 hello**值**清單中，您想要實作 toouse 選取 hello 使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="21c16-196">In hello **Value** list, select hello user attribute you want toouse for your implementation.</span></span>
    <span data-ttu-id="21c16-197">例如，如果您想 toouse hello EmployeeID 做為唯一的使用者識別碼，而且您已在 hello ExtensionAttribute2 儲存 hello 屬性值，然後選取  **user.extensionattribute2**。</span><span class="sxs-lookup"><span data-stu-id="21c16-197">For example, if you want toouse hello EmployeeID as unique user identifier and you have stored hello attribute value in hello ExtensionAttribute2, then select **user.extensionattribute2**.</span></span>
    
    <span data-ttu-id="21c16-198">d.</span><span class="sxs-lookup"><span data-stu-id="21c16-198">d.</span></span> <span data-ttu-id="21c16-199">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="21c16-199">Click **Ok**.</span></span>

7. <span data-ttu-id="21c16-200">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="21c16-200">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="21c16-202">在 hello **Ceridian Dayforce HCM 組態**區段中，按一下**設定 Ceridian Dayforce HCM** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="21c16-202">On hello **Ceridian Dayforce HCM Configuration** section, click **Configure Ceridian Dayforce HCM** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="21c16-203">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="21c16-203">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Ceridian Dayforce HCM 設定](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_configure.png) 

9. <span data-ttu-id="21c16-205">tooconfigure 單一登入上**Ceridian Dayforce HCM**端，您需要下載 toosend hello**中繼資料 XML**和**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**太[Ceridian Dayforce HCM 支援小組](https://www.ceridian.com/contact-us/index.html)。</span><span class="sxs-lookup"><span data-stu-id="21c16-205">tooconfigure single sign-on on **Ceridian Dayforce HCM** side, you need toosend hello downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html).</span></span>

> [!TIP]
> <span data-ttu-id="21c16-206">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="21c16-206">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="21c16-207">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="21c16-207">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="21c16-208">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="21c16-208">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="21c16-209">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="21c16-209">Create an Azure AD test user</span></span>

<span data-ttu-id="21c16-210">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="21c16-210">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="21c16-212">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="21c16-212">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="21c16-213">在 hello Azure 入口網站，hello 左窗格中，按一下 hello **Azure Active Directory**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="21c16-213">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="21c16-215">toodisplay hello 使用者清單，請移過**使用者和群組**，然後按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="21c16-215">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="21c16-217">tooopen hello**使用者**對話方塊中，按一下 [**新增**頂端的 hello hello**所有使用者**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="21c16-217">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello [新增] 按鈕](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="21c16-219">在 hello**使用者**對話方塊方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="21c16-219">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello [使用者] 對話方塊](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_04.png)

    <span data-ttu-id="21c16-221">a.</span><span class="sxs-lookup"><span data-stu-id="21c16-221">a.</span></span> <span data-ttu-id="21c16-222">在 hello**名稱**方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="21c16-222">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="21c16-223">b.</span><span class="sxs-lookup"><span data-stu-id="21c16-223">b.</span></span> <span data-ttu-id="21c16-224">在 hello**使用者名**方塊中，使用者許 Simon 類型 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="21c16-224">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="21c16-225">c.</span><span class="sxs-lookup"><span data-stu-id="21c16-225">c.</span></span> <span data-ttu-id="21c16-226">選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 hello**密碼**方塊。</span><span class="sxs-lookup"><span data-stu-id="21c16-226">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="21c16-227">d.</span><span class="sxs-lookup"><span data-stu-id="21c16-227">d.</span></span> <span data-ttu-id="21c16-228">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="21c16-228">Click **Create**.</span></span>
 
### <a name="create-a-ceridian-dayforce-hcm-test-user"></a><span data-ttu-id="21c16-229">建立 Ceridian Dayforce HCM 測試使用者</span><span class="sxs-lookup"><span data-stu-id="21c16-229">Create a Ceridian Dayforce HCM test user</span></span>

<span data-ttu-id="21c16-230">hello 本節目標在於 toocreate Ceridian Dayforce HCM 中呼叫許 Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="21c16-230">hello objective of this section is toocreate a user called Britta Simon in Ceridian Dayforce HCM.</span></span> <span data-ttu-id="21c16-231">使用 hello [Ceridian Dayforce HCM 支援小組](https://www.ceridian.com/contact-us/index.html)tooget hello Ceridian Dayforce HCM 應用程式中加入的使用者。</span><span class="sxs-lookup"><span data-stu-id="21c16-231">Work with hello [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html) tooget users added in hello Ceridian Dayforce HCM application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="21c16-232">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="21c16-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="21c16-233">在本節中，您可以授與存取 tooCeridian Dayforce HCM 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="21c16-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCeridian Dayforce HCM.</span></span>

![指派使用者][200] 

<span data-ttu-id="21c16-235">**tooassign 許 Simon tooCeridian Dayforce HCM，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="21c16-235">**tooassign Britta Simon tooCeridian Dayforce HCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="21c16-236">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="21c16-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="21c16-238">在 [hello] 應用程式清單中，選取**Ceridian Dayforce HCM**。</span><span class="sxs-lookup"><span data-stu-id="21c16-238">In hello applications list, select **Ceridian Dayforce HCM**.</span></span>

    ![設定單一登入](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png) 

3. <span data-ttu-id="21c16-240">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="21c16-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="21c16-242">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="21c16-242">Click **Add** button.</span></span> <span data-ttu-id="21c16-243">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="21c16-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="21c16-245">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="21c16-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="21c16-246">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="21c16-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="21c16-247">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="21c16-247">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="21c16-248">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="21c16-248">Assign hello Azure AD test user</span></span>

<span data-ttu-id="21c16-249">在本節中，您可以授與存取 tooCeridian Dayforce HCM 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="21c16-249">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCeridian Dayforce HCM.</span></span>

![指派 hello 使用者角色][200] 

<span data-ttu-id="21c16-251">**tooassign 許 Simon tooCeridian Dayforce HCM，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="21c16-251">**tooassign Britta Simon tooCeridian Dayforce HCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="21c16-252">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="21c16-252">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="21c16-254">在 [hello] 應用程式清單中，選取**Ceridian Dayforce HCM**。</span><span class="sxs-lookup"><span data-stu-id="21c16-254">In hello applications list, select **Ceridian Dayforce HCM**.</span></span>

    ![hello 應用程式清單中的 hello Ceridian Dayforce HCM 連結](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png)  

3. <span data-ttu-id="21c16-256">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="21c16-256">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello 「 使用者和群組 」 的連結][202]

4. <span data-ttu-id="21c16-258">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="21c16-258">Click **Add** button.</span></span> <span data-ttu-id="21c16-259">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="21c16-259">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 將作業加入窗格][203]

5. <span data-ttu-id="21c16-261">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="21c16-261">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="21c16-262">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="21c16-262">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="21c16-263">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="21c16-263">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="21c16-264">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="21c16-264">Test single sign-on</span></span>

<span data-ttu-id="21c16-265">hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="21c16-265">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="21c16-266">當您按一下 hello Ceridian Dayforce HCM 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Ceridian Dayforce HCM 應用程式。</span><span class="sxs-lookup"><span data-stu-id="21c16-266">When you click hello Ceridian Dayforce HCM tile in hello Access Panel, you should get automatically signed-on tooyour Ceridian Dayforce HCM application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="21c16-267">其他資源</span><span class="sxs-lookup"><span data-stu-id="21c16-267">Additional resources</span></span>

* [<span data-ttu-id="21c16-268">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="21c16-268">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="21c16-269">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="21c16-269">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_203.png

