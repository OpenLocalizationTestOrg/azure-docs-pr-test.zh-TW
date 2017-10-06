---
title: "教學課程：Azure Active Directory 與 Promapp 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Promapp 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 418d0601-6e7a-4997-a683-73fa30a2cfb5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: jeedes
ms.openlocfilehash: 02de7679b0c86d7aa8cacb41762f900dbf2ff231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-promapp"></a><span data-ttu-id="0aee5-103">教學課程：Azure Active Directory 與 Promapp 整合</span><span class="sxs-lookup"><span data-stu-id="0aee5-103">Tutorial: Azure Active Directory integration with Promapp</span></span>

<span data-ttu-id="0aee5-104">在此教學課程中，您學會如何 toointegrate Promapp 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="0aee5-104">In this tutorial, you learn how toointegrate Promapp with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0aee5-105">與 Azure AD 整合 Promapp 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="0aee5-105">Integrating Promapp with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0aee5-106">您可以控制存取 tooPromapp Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="0aee5-106">You can control in Azure AD who has access tooPromapp</span></span>
- <span data-ttu-id="0aee5-107">您可以啟用您的使用者 tooautomatically get 登入 tooPromapp （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="0aee5-107">You can enable your users tooautomatically get signed-on tooPromapp (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0aee5-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="0aee5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0aee5-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="0aee5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0aee5-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="0aee5-110">Prerequisites</span></span>

<span data-ttu-id="0aee5-111">tooconfigure Promapp 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="0aee5-111">tooconfigure Azure AD integration with Promapp, you need hello following items:</span></span>

- <span data-ttu-id="0aee5-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0aee5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0aee5-113">啟用 Promapp 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0aee5-113">A Promapp single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0aee5-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="0aee5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0aee5-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="0aee5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0aee5-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="0aee5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0aee5-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="0aee5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0aee5-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="0aee5-118">Scenario description</span></span>
<span data-ttu-id="0aee5-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0aee5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0aee5-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="0aee5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0aee5-121">從 hello 圖庫加入 Promapp</span><span class="sxs-lookup"><span data-stu-id="0aee5-121">Adding Promapp from hello gallery</span></span>
2. <span data-ttu-id="0aee5-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0aee5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-promapp-from-hello-gallery"></a><span data-ttu-id="0aee5-123">從 hello 圖庫加入 Promapp</span><span class="sxs-lookup"><span data-stu-id="0aee5-123">Adding Promapp from hello gallery</span></span>
<span data-ttu-id="0aee5-124">tooconfigure hello 整合 Promapp 到 Azure AD，您需要 tooadd Promapp hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0aee5-124">tooconfigure hello integration of Promapp into Azure AD, you need tooadd Promapp from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0aee5-125">**tooadd Promapp 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="0aee5-125">**tooadd Promapp from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0aee5-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="0aee5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0aee5-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="0aee5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0aee5-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="0aee5-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="0aee5-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="0aee5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="0aee5-133">在 [hello] 搜尋方塊中，輸入**Promapp**。</span><span class="sxs-lookup"><span data-stu-id="0aee5-133">In hello search box, type **Promapp**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_search.png)

5. <span data-ttu-id="0aee5-135">在 hello 結果 窗格中，選取  **Promapp**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0aee5-135">In hello results panel, select **Promapp**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0aee5-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0aee5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0aee5-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Promapp 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0aee5-138">In this section, you configure and test Azure AD single sign-on with Promapp based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0aee5-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Promapp 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="0aee5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Promapp is tooa user in Azure AD.</span></span> <span data-ttu-id="0aee5-140">換句話說，Azure AD 使用者與 hello Promapp 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="0aee5-140">In other words, a link relationship between an Azure AD user and hello related user in Promapp needs toobe established.</span></span>

<span data-ttu-id="0aee5-141">Promapp 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="0aee5-141">In Promapp, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0aee5-142">tooconfigure 及 Promapp 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="0aee5-142">tooconfigure and test Azure AD single sign-on with Promapp, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0aee5-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="0aee5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0aee5-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="0aee5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0aee5-145">**[建立測試使用者 Promapp](#creating-a-promapp-test-user)**  -toohave 許 Simon Promapp 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="0aee5-145">**[Creating a Promapp test user](#creating-a-promapp-test-user)** - toohave a counterpart of Britta Simon in Promapp that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0aee5-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0aee5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0aee5-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="0aee5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0aee5-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0aee5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0aee5-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Promapp 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="0aee5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Promapp application.</span></span>

<span data-ttu-id="0aee5-150">**tooconfigure Azure AD 單一登入與 Promapp，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="0aee5-150">**tooconfigure Azure AD single sign-on with Promapp, perform hello following steps:**</span></span>

1. <span data-ttu-id="0aee5-151">在 Azure 入口網站上 hello hello **Promapp**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="0aee5-151">In hello Azure portal, on hello **Promapp** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="0aee5-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0aee5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_samlbase.png)

3. <span data-ttu-id="0aee5-155">在 hello **Promapp 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="0aee5-155">On hello **Promapp Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_url.png)

    <span data-ttu-id="0aee5-157">a.</span><span class="sxs-lookup"><span data-stu-id="0aee5-157">a.</span></span> <span data-ttu-id="0aee5-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://DOMAINNAME.promapp.com/TENANTNAME/saml/authenticate`</span><span class="sxs-lookup"><span data-stu-id="0aee5-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://DOMAINNAME.promapp.com/TENANTNAME/saml/authenticate`</span></span>

    <span data-ttu-id="0aee5-159">b.</span><span class="sxs-lookup"><span data-stu-id="0aee5-159">b.</span></span> <span data-ttu-id="0aee5-160">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://DOMAINNAME.promapp.com/TENANTNAME`</span><span class="sxs-lookup"><span data-stu-id="0aee5-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://DOMAINNAME.promapp.com/TENANTNAME`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0aee5-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="0aee5-161">These values are not real.</span></span> <span data-ttu-id="0aee5-162">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="0aee5-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0aee5-163">請連絡[Promapp 用戶端支援小組](https://www.promapp.com/about-us/contact-us/)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="0aee5-163">Contact [Promapp Client support team](https://www.promapp.com/about-us/contact-us/) tooget these values.</span></span>

4. <span data-ttu-id="0aee5-164">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="0aee5-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_certificate.png) 

5. <span data-ttu-id="0aee5-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="0aee5-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-promapp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0aee5-168">在 hello **Promapp 組態**區段中，按一下**設定 Promapp** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="0aee5-168">On hello **Promapp Configuration** section, click **Configure Promapp** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0aee5-169">複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="0aee5-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_configure.png) 

7. <span data-ttu-id="0aee5-171">以系統管理員身分登入 tooyour Promapp 公司網站。</span><span class="sxs-lookup"><span data-stu-id="0aee5-171">Sign-on tooyour Promapp company site as administrator.</span></span> 

8. <span data-ttu-id="0aee5-172">在 hello 最上層顯示 hello 功能表上，按一下**Admin**。</span><span class="sxs-lookup"><span data-stu-id="0aee5-172">In hello menu on hello top, click **Admin**.</span></span> 
   
    ![Azure AD 單一登入][12]

9. <span data-ttu-id="0aee5-174">按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="0aee5-174">Click **Configure**.</span></span> 
   
    ![Azure AD 單一登入][13]

10. <span data-ttu-id="0aee5-176">在 [hello**安全性**] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="0aee5-176">On hello **Security** dialog, perform hello following steps:</span></span>
   
    ![Azure AD 單一登入][14]
    
    <span data-ttu-id="0aee5-178">a.</span><span class="sxs-lookup"><span data-stu-id="0aee5-178">a.</span></span> <span data-ttu-id="0aee5-179">貼上**SAML 單一登入服務 URL**，其中您從 hello Azure 入口網站複製到 hello **SSO 登入 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="0aee5-179">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **SSO-Login URL** textbox.</span></span>
    
    <span data-ttu-id="0aee5-180">b.</span><span class="sxs-lookup"><span data-stu-id="0aee5-180">b.</span></span> <span data-ttu-id="0aee5-181">針對 SSO - 單一登入模式，選取 選擇性，然後按一下儲存。</span><span class="sxs-lookup"><span data-stu-id="0aee5-181">As **SSO - Single Sign-on Mode**, select **Optional**, and then click **Save**.</span></span>

    <span data-ttu-id="0aee5-182">c.</span><span class="sxs-lookup"><span data-stu-id="0aee5-182">c.</span></span> <span data-ttu-id="0aee5-183">開啟 hello 下載 [記事本]，複製 hello 憑證內容中的憑證，而 hello 第一行 (---BEGIN CERTIFICATE---) 和 hello 最後一行 （---憑證結尾---），將它貼到 hello **SSO x.509 憑證**文字方塊中，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="0aee5-183">Open hello downloaded certificate in notepad, copy hello certificate content without hello first line (-----BEGIN CERTIFICATE-----) and hello last line (-----END CERTIFICATE-----), paste it into hello **SSO-x.509 Certificate** textbox, and then click **Save**.</span></span>
        
> [!TIP]
> <span data-ttu-id="0aee5-184">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="0aee5-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0aee5-185">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="0aee5-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0aee5-186">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0aee5-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0aee5-187">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0aee5-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="0aee5-188">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="0aee5-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="0aee5-190">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="0aee5-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0aee5-191">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="0aee5-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-promapp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0aee5-193">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="0aee5-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-promapp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0aee5-195">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="0aee5-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-promapp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0aee5-197">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="0aee5-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-promapp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0aee5-199">a.</span><span class="sxs-lookup"><span data-stu-id="0aee5-199">a.</span></span> <span data-ttu-id="0aee5-200">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="0aee5-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0aee5-201">b.</span><span class="sxs-lookup"><span data-stu-id="0aee5-201">b.</span></span> <span data-ttu-id="0aee5-202">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="0aee5-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0aee5-203">c.</span><span class="sxs-lookup"><span data-stu-id="0aee5-203">c.</span></span> <span data-ttu-id="0aee5-204">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="0aee5-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0aee5-205">d.</span><span class="sxs-lookup"><span data-stu-id="0aee5-205">d.</span></span> <span data-ttu-id="0aee5-206">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="0aee5-206">Click **Create**.</span></span>
 
### <a name="creating-a-promapp-test-user"></a><span data-ttu-id="0aee5-207">建立 Promapp 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0aee5-207">Creating a Promapp test user</span></span>

<span data-ttu-id="0aee5-208">hello Promapp 應用程式支援恰好在時間佈建。</span><span class="sxs-lookup"><span data-stu-id="0aee5-208">hello Promapp application supports Just-in-Time provisioning.</span></span> <span data-ttu-id="0aee5-209">這表示，使用者帳戶會自動建立必要期間嘗試 tooaccess hello 應用程式使用存取面板 hello。</span><span class="sxs-lookup"><span data-stu-id="0aee5-209">This means, a user account is automatically created if necessary during an attempt tooaccess hello application using hello Access Panel.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0aee5-210">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="0aee5-210">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0aee5-211">在本節中，您可以授與存取 tooPromapp 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0aee5-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPromapp.</span></span>

![指派使用者][200] 

<span data-ttu-id="0aee5-213">**tooassign 許 Simon tooPromapp，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="0aee5-213">**tooassign Britta Simon tooPromapp, perform hello following steps:**</span></span>

1. <span data-ttu-id="0aee5-214">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="0aee5-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="0aee5-216">在 [hello] 應用程式清單中，選取**Promapp**。</span><span class="sxs-lookup"><span data-stu-id="0aee5-216">In hello applications list, select **Promapp**.</span></span>

    ![設定單一登入](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_app.png) 

3. <span data-ttu-id="0aee5-218">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="0aee5-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="0aee5-220">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0aee5-220">Click **Add** button.</span></span> <span data-ttu-id="0aee5-221">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="0aee5-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="0aee5-223">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="0aee5-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0aee5-224">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0aee5-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0aee5-225">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0aee5-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0aee5-226">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="0aee5-226">Testing single sign-on</span></span>

<span data-ttu-id="0aee5-227">hello 本節目標在於 tootest 您 Azure AD 的 SSO 組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="0aee5-227">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="0aee5-228">當您按一下 hello Promapp 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Promapp 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0aee5-228">When you click hello Promapp tile in hello Access Panel, you should get automatically signed-on tooyour Promapp application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0aee5-229">其他資源</span><span class="sxs-lookup"><span data-stu-id="0aee5-229">Additional resources</span></span>

* [<span data-ttu-id="0aee5-230">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0aee5-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0aee5-231">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="0aee5-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_04.png
[12]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_05.png
[13]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_06.png
[14]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_07.png

[100]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_203.png

