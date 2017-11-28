---
title: "教學課程：Azure Active Directory 與 etouches 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 etouches 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 76cccaa8-859c-4c16-9d1d-8a6496fc7520
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 5f3ff7550e660b0fc52612140ca55061504b5edd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-etouches"></a><span data-ttu-id="77c5a-103">教學課程：Azure Active Directory 與 etouches 整合</span><span class="sxs-lookup"><span data-stu-id="77c5a-103">Tutorial: Azure Active Directory integration with etouches</span></span>

<span data-ttu-id="77c5a-104">在此教學課程中，您學會如何 toointegrate etouches 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="77c5a-104">In this tutorial, you learn how toointegrate etouches with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="77c5a-105">與 Azure AD 整合 etouches 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="77c5a-105">Integrating etouches with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="77c5a-106">您可以控制存取 tooetouches Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="77c5a-106">You can control in Azure AD who has access tooetouches</span></span>
- <span data-ttu-id="77c5a-107">您可以啟用您的使用者 tooautomatically get 登入 tooetouches （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="77c5a-107">You can enable your users tooautomatically get signed-on tooetouches (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="77c5a-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="77c5a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="77c5a-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="77c5a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77c5a-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="77c5a-110">Prerequisites</span></span>

<span data-ttu-id="77c5a-111">tooconfigure etouches 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="77c5a-111">tooconfigure Azure AD integration with etouches, you need hello following items:</span></span>

- <span data-ttu-id="77c5a-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="77c5a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="77c5a-113">啟用 etouches 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="77c5a-113">An etouches single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="77c5a-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="77c5a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="77c5a-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="77c5a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="77c5a-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="77c5a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="77c5a-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="77c5a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="77c5a-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="77c5a-118">Scenario description</span></span>
<span data-ttu-id="77c5a-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="77c5a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="77c5a-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="77c5a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="77c5a-121">從 hello 圖庫加入 etouches</span><span class="sxs-lookup"><span data-stu-id="77c5a-121">Adding etouches from hello gallery</span></span>
2. <span data-ttu-id="77c5a-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="77c5a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-etouches-from-hello-gallery"></a><span data-ttu-id="77c5a-123">從 hello 圖庫加入 etouches</span><span class="sxs-lookup"><span data-stu-id="77c5a-123">Adding etouches from hello gallery</span></span>
<span data-ttu-id="77c5a-124">tooconfigure hello 整合 etouches 到 Azure AD，您需要 tooadd etouches hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="77c5a-124">tooconfigure hello integration of etouches into Azure AD, you need tooadd etouches from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="77c5a-125">**tooadd etouches 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="77c5a-125">**tooadd etouches from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="77c5a-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="77c5a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 按鈕][1]

2. <span data-ttu-id="77c5a-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="77c5a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="77c5a-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="77c5a-129">Then go too**All applications**.</span></span>

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. <span data-ttu-id="77c5a-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="77c5a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 新應用程式按鈕][3]

4. <span data-ttu-id="77c5a-133">在 hello 搜尋方塊中，輸入**etouches**，選取**etouches**然後按一下 從結果面板**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="77c5a-133">In hello search box, type **etouches**, select **etouches** from result panel then click **Add** button tooadd hello application.</span></span>

    ![etouches hello [結果] 清單中](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="77c5a-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="77c5a-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="77c5a-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 etouches 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="77c5a-136">In this section, you configure and test Azure AD single sign-on with etouches based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="77c5a-137">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 etouches 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="77c5a-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in etouches is tooa user in Azure AD.</span></span> <span data-ttu-id="77c5a-138">換句話說，Azure AD 使用者與 hello etouches 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="77c5a-138">In other words, a link relationship between an Azure AD user and hello related user in etouches needs toobe established.</span></span>

<span data-ttu-id="77c5a-139">Etouches 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="77c5a-139">In etouches, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="77c5a-140">tooconfigure 及 etouches 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="77c5a-140">tooconfigure and test Azure AD single sign-on with etouches, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="77c5a-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="77c5a-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="77c5a-142">**[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="77c5a-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="77c5a-143">**[建立測試使用者 etouches](#create-an-etouches-test-user)**  -toohave 是連結的 toohello Azure AD 使用者表示法的 etouches 的許 Simon 的對應項目。</span><span class="sxs-lookup"><span data-stu-id="77c5a-143">**[Create an etouches test user](#create-an-etouches-test-user)** - toohave a counterpart of Britta Simon in etouches that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="77c5a-144">**[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="77c5a-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="77c5a-145">**[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="77c5a-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="77c5a-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="77c5a-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="77c5a-147">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 etouches 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="77c5a-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your etouches application.</span></span>

<span data-ttu-id="77c5a-148">**tooconfigure Azure AD 單一登入與 etouches，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="77c5a-148">**tooconfigure Azure AD single sign-on with etouches, perform hello following steps:**</span></span>

1. <span data-ttu-id="77c5a-149">在 Azure 入口網站上 hello hello **etouches**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="77c5a-149">In hello Azure portal, on hello **etouches** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="77c5a-151">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="77c5a-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_samlbase.png)

3. <span data-ttu-id="77c5a-153">在 hello **etouches 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="77c5a-153">On hello **etouches Domain and URLs** section, perform hello following steps:</span></span>

    ![etouches 網域及 URL 單一登入資訊](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_url.png)

    <span data-ttu-id="77c5a-155">a.</span><span class="sxs-lookup"><span data-stu-id="77c5a-155">a.</span></span> <span data-ttu-id="77c5a-156">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://www.eiseverywhere.com/saml/accounts/?sso&accountid=<ACCOUNTID>`</span><span class="sxs-lookup"><span data-stu-id="77c5a-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.eiseverywhere.com/saml/accounts/?sso&accountid=<ACCOUNTID>`</span></span>

    <span data-ttu-id="77c5a-157">b.</span><span class="sxs-lookup"><span data-stu-id="77c5a-157">b.</span></span> <span data-ttu-id="77c5a-158">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://www.eiseverywhere.com/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="77c5a-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.eiseverywhere.com/<instance name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="77c5a-159">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="77c5a-159">These values are not real.</span></span> <span data-ttu-id="77c5a-160">您可以更新 hello 值與實際的 hello 登入 URL 和識別碼，在 hello 教學課程稍後會說明。</span><span class="sxs-lookup"><span data-stu-id="77c5a-160">You update hello value with hello actual Sign on URL and Identifier, which is explained later in hello tutorial.</span></span>
    > 

4. <span data-ttu-id="77c5a-161">etouches 應用程式預期 hello SAML 判斷提示，以特定格式。</span><span class="sxs-lookup"><span data-stu-id="77c5a-161">etouches application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="77c5a-162">設定下列宣告為此應用程式的 hello。</span><span class="sxs-lookup"><span data-stu-id="77c5a-162">Configure hello following claims for this application.</span></span> <span data-ttu-id="77c5a-163">您可以從 hello 管理這些屬性的 hello 值**使用者屬性**hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="77c5a-163">You can manage hello values of these attributes from hello **User Attribute** of hello application.</span></span> <span data-ttu-id="77c5a-164">hello 下列螢幕擷取畫面會顯示這個範例。</span><span class="sxs-lookup"><span data-stu-id="77c5a-164">hello following screenshot shows an example for this.</span></span> 

    ![使用者屬性](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_attribute.png) 

5. <span data-ttu-id="77c5a-166">在 hello**使用者屬性**hello 區段**單一登入** 對話方塊中，hello 映像中所示設定 SAML 權杖屬性並執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="77c5a-166">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="77c5a-167">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="77c5a-167">Attribute Name</span></span> | <span data-ttu-id="77c5a-168">屬性值</span><span class="sxs-lookup"><span data-stu-id="77c5a-168">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="77c5a-169">電子郵件</span><span class="sxs-lookup"><span data-stu-id="77c5a-169">Email</span></span> | <span data-ttu-id="77c5a-170">user.mail</span><span class="sxs-lookup"><span data-stu-id="77c5a-170">user.mail</span></span> |    
    
    <span data-ttu-id="77c5a-171">a.</span><span class="sxs-lookup"><span data-stu-id="77c5a-171">a.</span></span> <span data-ttu-id="77c5a-172">按一下**加入屬性**tooopen hello**加入屬性**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="77c5a-172">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![新增屬性](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_04.png)

    ![[新增屬性] 對話方塊](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="77c5a-175">b.</span><span class="sxs-lookup"><span data-stu-id="77c5a-175">b.</span></span> <span data-ttu-id="77c5a-176">在 hello**名稱**文字方塊中，該資料列所顯示的型別 hello 屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="77c5a-176">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="77c5a-177">c.</span><span class="sxs-lookup"><span data-stu-id="77c5a-177">c.</span></span> <span data-ttu-id="77c5a-178">從 hello**值**清單，顯示該資料列的型別 hello 屬性值。</span><span class="sxs-lookup"><span data-stu-id="77c5a-178">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="77c5a-179">d.</span><span class="sxs-lookup"><span data-stu-id="77c5a-179">d.</span></span> <span data-ttu-id="77c5a-180">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="77c5a-180">Click **Ok**.</span></span> 

6. <span data-ttu-id="77c5a-181">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="77c5a-181">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![hello 憑證下載連結](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_certificate.png) 

7. <span data-ttu-id="77c5a-183">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="77c5a-183">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-etouches-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="77c5a-185">tooget SSO 設定應用程式執行下列步驟在 hello etouches 應用程式中的 hello:</span><span class="sxs-lookup"><span data-stu-id="77c5a-185">tooget SSO configured for your application, perform hello following steps in hello etouches application:</span></span> 

    ![etouches 組態](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_06.png) 

    <span data-ttu-id="77c5a-187">a.</span><span class="sxs-lookup"><span data-stu-id="77c5a-187">a.</span></span> <span data-ttu-id="77c5a-188">登入太**etouches**使用 hello 系統管理員權限的應用程式。</span><span class="sxs-lookup"><span data-stu-id="77c5a-188">Login too**etouches** application using hello Admin rights.</span></span>
   
    <span data-ttu-id="77c5a-189">b.</span><span class="sxs-lookup"><span data-stu-id="77c5a-189">b.</span></span> <span data-ttu-id="77c5a-190">移 toohello **SAML**組態。</span><span class="sxs-lookup"><span data-stu-id="77c5a-190">Go toohello **SAML** Configuration.</span></span>

    <span data-ttu-id="77c5a-191">c.</span><span class="sxs-lookup"><span data-stu-id="77c5a-191">c.</span></span> <span data-ttu-id="77c5a-192">在 [hello**一般設定**區段中，開啟下載的憑證，從 Azure 入口網站，在記事本中，複製 hello 內容，然後貼到 hello IDP 中繼資料] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="77c5a-192">In hello **General Settings** section, open your downloaded certificate from Azure portal in notepad, copy hello content, and then paste it into hello IDP metadata textbox.</span></span> 

    <span data-ttu-id="77c5a-193">d.</span><span class="sxs-lookup"><span data-stu-id="77c5a-193">d.</span></span> <span data-ttu-id="77c5a-194">按一下 hello**儲存，並保持** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="77c5a-194">Click on hello **Save & Stay** button.</span></span>
  
    <span data-ttu-id="77c5a-195">e.</span><span class="sxs-lookup"><span data-stu-id="77c5a-195">e.</span></span> <span data-ttu-id="77c5a-196">按一下 hello**更新中繼資料**hello SAML 中繼資料 區段中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="77c5a-196">Click on hello **Update Metadata** button in hello SAML Metadata section.</span></span> 

    <span data-ttu-id="77c5a-197">f.</span><span class="sxs-lookup"><span data-stu-id="77c5a-197">f.</span></span> <span data-ttu-id="77c5a-198">隨即會開啟 hello 頁面，並執行 SSO。</span><span class="sxs-lookup"><span data-stu-id="77c5a-198">This opens hello page and perform SSO.</span></span> <span data-ttu-id="77c5a-199">一次 hello SSO 運作，您可以設定 hello 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="77c5a-199">Once hello SSO is working then you can set up hello username.</span></span>

    <span data-ttu-id="77c5a-200">g.</span><span class="sxs-lookup"><span data-stu-id="77c5a-200">g.</span></span> <span data-ttu-id="77c5a-201">在 hello 使用者名稱 欄位中，選取 hello **emailaddress** hello 圖所示。</span><span class="sxs-lookup"><span data-stu-id="77c5a-201">In hello Username field, select hello **emailaddress** as shown in hello image below.</span></span> 

    <span data-ttu-id="77c5a-202">h.</span><span class="sxs-lookup"><span data-stu-id="77c5a-202">h.</span></span> <span data-ttu-id="77c5a-203">複製 hello**預存程序的實體識別碼**值並貼到 hello**識別碼**文字方塊中，位於**etouches 網域和 Url** Azure 入口網站上的一節。</span><span class="sxs-lookup"><span data-stu-id="77c5a-203">Copy hello **SP entity ID** value and paste it into hello **Identifier**  textbox, which is in **etouches Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="77c5a-204">i.</span><span class="sxs-lookup"><span data-stu-id="77c5a-204">i.</span></span> <span data-ttu-id="77c5a-205">複製 hello **SSO URL / ACS**值並貼到 hello**登入 URL**文字方塊中，位於**etouches 網域和 Url** Azure 入口網站上的一節。</span><span class="sxs-lookup"><span data-stu-id="77c5a-205">Copy hello **SSO URL / ACS** value and paste it into hello **Sign on URL** textbox, which is in **etouches Domain and URLs** section on Azure portal.</span></span>
   
> [!TIP]
> <span data-ttu-id="77c5a-206">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="77c5a-206">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="77c5a-207">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="77c5a-207">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="77c5a-208">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="77c5a-208">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="77c5a-209">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="77c5a-209">Create an Azure AD test user</span></span>
<span data-ttu-id="77c5a-210">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="77c5a-210">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 測試使用者][100]

<span data-ttu-id="77c5a-212">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="77c5a-212">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="77c5a-213">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="77c5a-213">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-etouches-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="77c5a-215">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="77c5a-215">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-etouches-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="77c5a-217">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="77c5a-217">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![hello [新增] 按鈕](./media/active-directory-saas-etouches-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="77c5a-219">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="77c5a-219">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![hello [使用者] 對話方塊](./media/active-directory-saas-etouches-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="77c5a-221">a.</span><span class="sxs-lookup"><span data-stu-id="77c5a-221">a.</span></span> <span data-ttu-id="77c5a-222">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="77c5a-222">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="77c5a-223">b.</span><span class="sxs-lookup"><span data-stu-id="77c5a-223">b.</span></span> <span data-ttu-id="77c5a-224">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="77c5a-224">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="77c5a-225">c.</span><span class="sxs-lookup"><span data-stu-id="77c5a-225">c.</span></span> <span data-ttu-id="77c5a-226">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="77c5a-226">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="77c5a-227">d.</span><span class="sxs-lookup"><span data-stu-id="77c5a-227">d.</span></span> <span data-ttu-id="77c5a-228">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="77c5a-228">Click **Create**.</span></span>
 
### <a name="create-an-etouches-test-user"></a><span data-ttu-id="77c5a-229">建立 etouches 測試使用者</span><span class="sxs-lookup"><span data-stu-id="77c5a-229">Create an etouches test user</span></span>

<span data-ttu-id="77c5a-230">在本節中，您會於 etouches 建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="77c5a-230">In this section, you create a user called Britta Simon in etouches.</span></span> <span data-ttu-id="77c5a-231">使用[etouches 用戶端支援小組](https://www.etouches.com/event-software/support/customer-support/)tooadd hello hello etouches 平台的使用者。</span><span class="sxs-lookup"><span data-stu-id="77c5a-231">Work with [etouches Client support team](https://www.etouches.com/event-software/support/customer-support/) tooadd hello users in hello etouches platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="77c5a-232">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="77c5a-232">Assign hello Azure AD test user</span></span>

<span data-ttu-id="77c5a-233">在本節中，您可以授與存取 tooetouches 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="77c5a-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooetouches.</span></span>

![指派 hello 使用者角色][200] 

<span data-ttu-id="77c5a-235">**tooassign 許 Simon tooetouches，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="77c5a-235">**tooassign Britta Simon tooetouches, perform hello following steps:**</span></span>

1. <span data-ttu-id="77c5a-236">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="77c5a-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="77c5a-238">在 [hello] 應用程式清單中，選取**etouches**。</span><span class="sxs-lookup"><span data-stu-id="77c5a-238">In hello applications list, select **etouches**.</span></span>

    ![hello 應用程式清單中的 hello etouches 連結](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_app.png) 

3. <span data-ttu-id="77c5a-240">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="77c5a-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello 「 使用者和群組 」 的連結][202] 

4. <span data-ttu-id="77c5a-242">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="77c5a-242">Click **Add** button.</span></span> <span data-ttu-id="77c5a-243">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="77c5a-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 將作業加入窗格][203]

5. <span data-ttu-id="77c5a-245">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="77c5a-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="77c5a-246">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="77c5a-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="77c5a-247">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="77c5a-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="77c5a-248">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="77c5a-248">Test single sign-on</span></span>


<span data-ttu-id="77c5a-249">hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="77c5a-249">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="77c5a-250">當您按一下的 hello etouches 磚 hello 存取面板中時，您應該取得自動登入 tooyour etouches 應用程式。</span><span class="sxs-lookup"><span data-stu-id="77c5a-250">When you click hello etouches tile in hello Access Panel, you should get automatically signed-on tooyour etouches application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="77c5a-251">其他資源</span><span class="sxs-lookup"><span data-stu-id="77c5a-251">Additional resources</span></span>

* [<span data-ttu-id="77c5a-252">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="77c5a-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="77c5a-253">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="77c5a-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_203.png

