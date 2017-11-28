---
title: "教學課程：Azure Active Directory 與 CloudPassage 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 CloudPassage 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfe1f14e-74e4-4680-ac9e-f7355e1c94cc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 32fb007b90f071626c9b40fb5afc341dd3c1ae99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cloudpassage"></a><span data-ttu-id="7efcd-103">教學課程：Azure Active Directory 與 CloudPassage 整合</span><span class="sxs-lookup"><span data-stu-id="7efcd-103">Tutorial: Azure Active Directory integration with CloudPassage</span></span>

<span data-ttu-id="7efcd-104">在此教學課程中，您學會如何 toointegrate CloudPassage 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="7efcd-104">In this tutorial, you learn how toointegrate CloudPassage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7efcd-105">與 Azure AD 整合 CloudPassage 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="7efcd-105">Integrating CloudPassage with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7efcd-106">您可以控制存取 tooCloudPassage Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="7efcd-106">You can control in Azure AD who has access tooCloudPassage</span></span>
- <span data-ttu-id="7efcd-107">您可以啟用您的使用者 tooautomatically get 登入 tooCloudPassage （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="7efcd-107">You can enable your users tooautomatically get signed-on tooCloudPassage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7efcd-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="7efcd-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7efcd-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="7efcd-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7efcd-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="7efcd-110">Prerequisites</span></span>

<span data-ttu-id="7efcd-111">tooconfigure CloudPassage 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="7efcd-111">tooconfigure Azure AD integration with CloudPassage, you need hello following items:</span></span>

- <span data-ttu-id="7efcd-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7efcd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7efcd-113">已啟用 CloudPassage 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7efcd-113">A CloudPassage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7efcd-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="7efcd-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7efcd-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="7efcd-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7efcd-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="7efcd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7efcd-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="7efcd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7efcd-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="7efcd-118">Scenario description</span></span>
<span data-ttu-id="7efcd-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7efcd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7efcd-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="7efcd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7efcd-121">從 hello 圖庫加入 CloudPassage</span><span class="sxs-lookup"><span data-stu-id="7efcd-121">Adding CloudPassage from hello gallery</span></span>
2. <span data-ttu-id="7efcd-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7efcd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cloudpassage-from-hello-gallery"></a><span data-ttu-id="7efcd-123">從 hello 圖庫加入 CloudPassage</span><span class="sxs-lookup"><span data-stu-id="7efcd-123">Adding CloudPassage from hello gallery</span></span>
<span data-ttu-id="7efcd-124">tooconfigure hello 整合 CloudPassage 到 Azure AD，您需要 tooadd CloudPassage hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7efcd-124">tooconfigure hello integration of CloudPassage into Azure AD, you need tooadd CloudPassage from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7efcd-125">**tooadd CloudPassage 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="7efcd-125">**tooadd CloudPassage from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7efcd-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="7efcd-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7efcd-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="7efcd-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7efcd-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="7efcd-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="7efcd-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="7efcd-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="7efcd-133">在 [hello] 搜尋方塊中，輸入**CloudPassage**。</span><span class="sxs-lookup"><span data-stu-id="7efcd-133">In hello search box, type **CloudPassage**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_search.png)

5. <span data-ttu-id="7efcd-135">在 hello 結果 窗格中，選取  **CloudPassage**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7efcd-135">In hello results panel, select **CloudPassage**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7efcd-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7efcd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7efcd-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 CloudPassage 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7efcd-138">In this section, you configure and test Azure AD single sign-on with CloudPassage based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7efcd-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 CloudPassage 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="7efcd-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in CloudPassage is tooa user in Azure AD.</span></span> <span data-ttu-id="7efcd-140">換句話說，Azure AD 使用者與 hello CloudPassage 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="7efcd-140">In other words, a link relationship between an Azure AD user and hello related user in CloudPassage needs toobe established.</span></span>

<span data-ttu-id="7efcd-141">CloudPassage 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="7efcd-141">In CloudPassage, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7efcd-142">tooconfigure 及 CloudPassage 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="7efcd-142">tooconfigure and test Azure AD single sign-on with CloudPassage, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7efcd-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="7efcd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7efcd-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="7efcd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7efcd-145">**[建立測試使用者 CloudPassage](#creating-a-cloudpassage-test-user)**  -toohave 許 Simon CloudPassage 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="7efcd-145">**[Creating a CloudPassage test user](#creating-a-cloudpassage-test-user)** - toohave a counterpart of Britta Simon in CloudPassage that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7efcd-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7efcd-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7efcd-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="7efcd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7efcd-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7efcd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7efcd-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 CloudPassage 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="7efcd-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your CloudPassage application.</span></span>

<span data-ttu-id="7efcd-150">**tooconfigure Azure AD 單一登入與 CloudPassage，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="7efcd-150">**tooconfigure Azure AD single sign-on with CloudPassage, perform hello following steps:**</span></span>

1. <span data-ttu-id="7efcd-151">在 Azure 入口網站上 hello hello **CloudPassage**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="7efcd-151">In hello Azure portal, on hello **CloudPassage** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="7efcd-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7efcd-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_samlbase.png)

3. <span data-ttu-id="7efcd-155">在 hello **CloudPassage 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="7efcd-155">On hello **CloudPassage Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_url.png)

    <span data-ttu-id="7efcd-157">a.</span><span class="sxs-lookup"><span data-stu-id="7efcd-157">a.</span></span> <span data-ttu-id="7efcd-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://portal.cloudpassage.com/saml/init/accountid`</span><span class="sxs-lookup"><span data-stu-id="7efcd-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://portal.cloudpassage.com/saml/init/accountid`</span></span>

    <span data-ttu-id="7efcd-159">b.</span><span class="sxs-lookup"><span data-stu-id="7efcd-159">b.</span></span> <span data-ttu-id="7efcd-160">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello: `https://portal.cloudpassage.com/saml/consume/accountid`。</span><span class="sxs-lookup"><span data-stu-id="7efcd-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://portal.cloudpassage.com/saml/consume/accountid`.</span></span> <span data-ttu-id="7efcd-161">您也可以按一下此屬性取得您的值**SSO 安裝程式文件**在 hello**單一登入設定**CloudPassage 入口網站 > 一節。</span><span class="sxs-lookup"><span data-stu-id="7efcd-161">You can get your value for this attribute by clicking **SSO Setup documentation** in hello **Single Sign-on Settings** section of your CloudPassage portal.</span></span>

    ![設定單一登入](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_05.png)
     
    > [!NOTE] 
    > <span data-ttu-id="7efcd-163">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="7efcd-163">These values are not real.</span></span> <span data-ttu-id="7efcd-164">更新這些值與實際回覆 URL hello，請登入 URL。</span><span class="sxs-lookup"><span data-stu-id="7efcd-164">Update these values with hello actual Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="7efcd-165">請連絡[CloudPassage 用戶端支援小組](https://www.cloudpassage.com/company/contact/)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="7efcd-165">Contact [CloudPassage Client support team](https://www.cloudpassage.com/company/contact/) tooget these values.</span></span> 

4. <span data-ttu-id="7efcd-166">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="7efcd-166">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_certificate.png) 

5. <span data-ttu-id="7efcd-168">CloudPassage 應用程式預期 hello SAML 判斷提示，以特定格式，這需要您 tooadd 自訂屬性對應 tooyour SAML token 屬性設定。</span><span class="sxs-lookup"><span data-stu-id="7efcd-168">Your CloudPassage application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span>   
<span data-ttu-id="7efcd-169">hello 下列螢幕擷取畫面會顯示這個範例。</span><span class="sxs-lookup"><span data-stu-id="7efcd-169">hello following screenshot shows an example for this.</span></span>
   
   ![設定單一登入](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_25.png) 

6. <span data-ttu-id="7efcd-171">在 hello**使用者屬性**區段 hello**單一登入** 對話方塊中，上述 hello 映像中所示設定 SAML 權杖屬性和執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="7efcd-171">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>

    | <span data-ttu-id="7efcd-172">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="7efcd-172">Attribute Name</span></span> | <span data-ttu-id="7efcd-173">屬性值</span><span class="sxs-lookup"><span data-stu-id="7efcd-173">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="7efcd-174">firstname</span><span class="sxs-lookup"><span data-stu-id="7efcd-174">firstname</span></span> |<span data-ttu-id="7efcd-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="7efcd-175">user.givenname</span></span> |
    | <span data-ttu-id="7efcd-176">lastname</span><span class="sxs-lookup"><span data-stu-id="7efcd-176">lastname</span></span> |<span data-ttu-id="7efcd-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="7efcd-177">user.surname</span></span> |
    | <span data-ttu-id="7efcd-178">電子郵件</span><span class="sxs-lookup"><span data-stu-id="7efcd-178">email</span></span> |<span data-ttu-id="7efcd-179">user.mail</span><span class="sxs-lookup"><span data-stu-id="7efcd-179">user.mail</span></span> |
    
    <span data-ttu-id="7efcd-180">a.</span><span class="sxs-lookup"><span data-stu-id="7efcd-180">a.</span></span> <span data-ttu-id="7efcd-181">按一下**加入屬性**tooopen hello**加入屬性**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="7efcd-181">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-cloudpassage-tutorial/tutorial_attribute_04.png)
    
    ![設定單一登入](./media/active-directory-saas-cloudpassage-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="7efcd-184">b.</span><span class="sxs-lookup"><span data-stu-id="7efcd-184">b.</span></span> <span data-ttu-id="7efcd-185">在 hello**名稱**文字方塊中，該資料列所顯示的型別 hello 屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="7efcd-185">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="7efcd-186">c.</span><span class="sxs-lookup"><span data-stu-id="7efcd-186">c.</span></span> <span data-ttu-id="7efcd-187">從 hello**值**清單，顯示該資料列的型別 hello 屬性值。</span><span class="sxs-lookup"><span data-stu-id="7efcd-187">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="7efcd-188">d.</span><span class="sxs-lookup"><span data-stu-id="7efcd-188">d.</span></span> <span data-ttu-id="7efcd-189">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="7efcd-189">Click **Ok**.</span></span>

7. <span data-ttu-id="7efcd-190">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="7efcd-190">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="7efcd-192">在 hello **CloudPassage 組態**區段中，按一下**設定 CloudPassage** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="7efcd-192">On hello **CloudPassage Configuration** section, click **Configure CloudPassage** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7efcd-193">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="7efcd-193">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_configure.png) 

9. <span data-ttu-id="7efcd-195">在不同的瀏覽器視窗中，以系統管理員身分登入 tooyour CloudPassage 公司網站。</span><span class="sxs-lookup"><span data-stu-id="7efcd-195">In a different browser window, sign-on tooyour CloudPassage company site as administrator.</span></span>

10. <span data-ttu-id="7efcd-196">在 hello 最上層顯示 hello 功能表上，按一下**設定**，然後按一下**網站管理**。</span><span class="sxs-lookup"><span data-stu-id="7efcd-196">In hello menu on hello top, click **Settings**, and then click **Site Administration**.</span></span> 
   
    ![設定單一登入][12]

11. <span data-ttu-id="7efcd-198">按一下 hello**驗證設定** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="7efcd-198">Click hello **Authentication Settings** tab.</span></span> 
   
    ![設定單一登入][13]

12. <span data-ttu-id="7efcd-200">在 hello**單一登入設定**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="7efcd-200">In hello **Single Sign-on Settings** section, perform hello following steps:</span></span> 
   
    ![設定單一登入][14]

    <span data-ttu-id="7efcd-202">a.</span><span class="sxs-lookup"><span data-stu-id="7efcd-202">a.</span></span> <span data-ttu-id="7efcd-203">選取 [啟用單一登入 (SSO) (SSO 安裝程式文件)/] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="7efcd-203">Select **Enable Single sign-on(SSO)(SSO Setup Documentation)** checkbox.</span></span>
    
    <span data-ttu-id="7efcd-204">b.</span><span class="sxs-lookup"><span data-stu-id="7efcd-204">b.</span></span> <span data-ttu-id="7efcd-205">貼上**SAML 實體識別碼**到 hello **SAML 簽發者 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="7efcd-205">Paste **SAML Entity ID** into hello **SAML issuer URL** textbox.</span></span>
  
    <span data-ttu-id="7efcd-206">c.</span><span class="sxs-lookup"><span data-stu-id="7efcd-206">c.</span></span> <span data-ttu-id="7efcd-207">貼上**SAML 單一登入服務 URL**到 hello **SAML 端點 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="7efcd-207">Paste **SAML Single Sign-On Service URL** into hello **SAML endpoint URL** textbox.</span></span>
  
    <span data-ttu-id="7efcd-208">d.</span><span class="sxs-lookup"><span data-stu-id="7efcd-208">d.</span></span> <span data-ttu-id="7efcd-209">貼上**登出 URL**到 hello**登出登陸頁面**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="7efcd-209">Paste **Sign-Out URL** into hello **Logout landing page** textbox.</span></span>
  
    <span data-ttu-id="7efcd-210">e.</span><span class="sxs-lookup"><span data-stu-id="7efcd-210">e.</span></span> <span data-ttu-id="7efcd-211">在 [記事本]，複製 hello 下載的憑證到剪貼簿的內容中開啟下載的憑證，然後將它貼到 hello **x509 憑證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="7efcd-211">Open your downloaded certificate in notepad, copy hello content of downloaded certificate into your clipboard, and then paste it into hello **x 509 certificate** textbox.</span></span>
  
    <span data-ttu-id="7efcd-212">f.</span><span class="sxs-lookup"><span data-stu-id="7efcd-212">f.</span></span> <span data-ttu-id="7efcd-213">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="7efcd-213">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="7efcd-214">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="7efcd-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7efcd-215">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="7efcd-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7efcd-216">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7efcd-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7efcd-217">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7efcd-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="7efcd-218">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="7efcd-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="7efcd-220">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="7efcd-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7efcd-221">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="7efcd-221">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7efcd-223">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="7efcd-223">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7efcd-225">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="7efcd-225">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7efcd-227">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="7efcd-227">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7efcd-229">a.</span><span class="sxs-lookup"><span data-stu-id="7efcd-229">a.</span></span> <span data-ttu-id="7efcd-230">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="7efcd-230">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7efcd-231">b.</span><span class="sxs-lookup"><span data-stu-id="7efcd-231">b.</span></span> <span data-ttu-id="7efcd-232">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="7efcd-232">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7efcd-233">c.</span><span class="sxs-lookup"><span data-stu-id="7efcd-233">c.</span></span> <span data-ttu-id="7efcd-234">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="7efcd-234">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7efcd-235">d.</span><span class="sxs-lookup"><span data-stu-id="7efcd-235">d.</span></span> <span data-ttu-id="7efcd-236">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="7efcd-236">Click **Create**.</span></span>
 
### <a name="creating-a-cloudpassage-test-user"></a><span data-ttu-id="7efcd-237">建立 CloudPassage 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7efcd-237">Creating a CloudPassage test user</span></span>

<span data-ttu-id="7efcd-238">hello 本節目標在於 toocreate CloudPassage 中呼叫許 Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="7efcd-238">hello objective of this section is toocreate a user called Britta Simon in CloudPassage.</span></span>

<span data-ttu-id="7efcd-239">**toocreate 呼叫許 Simon CloudPassage，在使用者執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="7efcd-239">**toocreate a user called Britta Simon in CloudPassage, perform hello following steps:**</span></span>

1. <span data-ttu-id="7efcd-240">登入 tooyour **CloudPassage**系統管理員身分的公司網站。</span><span class="sxs-lookup"><span data-stu-id="7efcd-240">Sign-on tooyour **CloudPassage** company site as an administrator.</span></span> 

2. <span data-ttu-id="7efcd-241">在 hello hello 上方的工具列中按一下**設定**，然後按一下**網站管理**。</span><span class="sxs-lookup"><span data-stu-id="7efcd-241">In hello toolbar on hello top, click **Settings**, and then click **Site Administration**.</span></span> 
   
   ![建立 CloudPassage 測試使用者][22] 

3. <span data-ttu-id="7efcd-243">按一下 hello**使用者**索引標籤，然後再按一下**新增使用者**。</span><span class="sxs-lookup"><span data-stu-id="7efcd-243">Click hello **Users** tab, and then click **Add New User**.</span></span> 
   
   ![建立 CloudPassage 測試使用者][23]

4. <span data-ttu-id="7efcd-245">在 hello**新增使用者**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="7efcd-245">In hello **Add New User** section, perform hello following steps:</span></span> 
   
   ![建立 CloudPassage 測試使用者][24]
    
    <span data-ttu-id="7efcd-247">a.</span><span class="sxs-lookup"><span data-stu-id="7efcd-247">a.</span></span> <span data-ttu-id="7efcd-248">在 hello**名字**文字方塊中，輸入許。</span><span class="sxs-lookup"><span data-stu-id="7efcd-248">In hello **First Name** textbox, type Britta.</span></span> 
  
    <span data-ttu-id="7efcd-249">b.</span><span class="sxs-lookup"><span data-stu-id="7efcd-249">b.</span></span> <span data-ttu-id="7efcd-250">在 hello**姓氏**文字方塊中，輸入 Simon。</span><span class="sxs-lookup"><span data-stu-id="7efcd-250">In hello **Last Name** textbox, type Simon.</span></span>
  
    <span data-ttu-id="7efcd-251">c.</span><span class="sxs-lookup"><span data-stu-id="7efcd-251">c.</span></span> <span data-ttu-id="7efcd-252">在 hello**使用者名稱**文字方塊中，hello**電子郵件**文字方塊中和 hello**重新輸入電子郵件**文字方塊中，在 Azure AD 中輸入許的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="7efcd-252">In hello **Username** textbox, hello **Email** textbox and hello **Retype Email** textbox, type Britta's user name in Azure AD.</span></span>
  
    <span data-ttu-id="7efcd-253">d.</span><span class="sxs-lookup"><span data-stu-id="7efcd-253">d.</span></span> <span data-ttu-id="7efcd-254">對於 [存取類型]，選取 [啟用 Halo 入口網站存取]。</span><span class="sxs-lookup"><span data-stu-id="7efcd-254">As **Access Type**, select **Enable Halo Portal Access**.</span></span>
  
    <span data-ttu-id="7efcd-255">e.</span><span class="sxs-lookup"><span data-stu-id="7efcd-255">e.</span></span> <span data-ttu-id="7efcd-256">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="7efcd-256">Click **Add**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7efcd-257">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="7efcd-257">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7efcd-258">在本節中，您可以授與存取 tooCloudPassage 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7efcd-258">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCloudPassage.</span></span>

![指派使用者][200] 

<span data-ttu-id="7efcd-260">**tooassign 許 Simon tooCloudPassage，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="7efcd-260">**tooassign Britta Simon tooCloudPassage, perform hello following steps:**</span></span>

1. <span data-ttu-id="7efcd-261">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="7efcd-261">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="7efcd-263">在 [hello] 應用程式清單中，選取**CloudPassage**。</span><span class="sxs-lookup"><span data-stu-id="7efcd-263">In hello applications list, select **CloudPassage**.</span></span>

    ![設定單一登入](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_app.png) 

3. <span data-ttu-id="7efcd-265">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="7efcd-265">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="7efcd-267">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7efcd-267">Click **Add** button.</span></span> <span data-ttu-id="7efcd-268">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="7efcd-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="7efcd-270">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="7efcd-270">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7efcd-271">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7efcd-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7efcd-272">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7efcd-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7efcd-273">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="7efcd-273">Testing single sign-on</span></span>

<span data-ttu-id="7efcd-274">hello 本節目標在於 tootest 您 Azure AD 的 SSO 組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="7efcd-274">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="7efcd-275">當您按一下 hello CloudPassage 磚 hello 存取面板中的時，您應該取得自動登入 tooyour CloudPassage 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7efcd-275">When you click hello CloudPassage tile in hello Access Panel, you should get automatically signed-on tooyour CloudPassage application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7efcd-276">其他資源</span><span class="sxs-lookup"><span data-stu-id="7efcd-276">Additional resources</span></span>

* [<span data-ttu-id="7efcd-277">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7efcd-277">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7efcd-278">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="7efcd-278">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_04.png
[12]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_07.png
[13]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_08.png
[14]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_09.png
[15]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_10.png
[22]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_15.png
[23]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_16.png
[24]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_17.png

[100]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_203.png

