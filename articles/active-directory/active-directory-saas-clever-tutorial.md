---
title: "教學課程：Azure Active Directory 與 Clever 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Clever 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 069ff13a-310e-4366-a147-d6ec5cca12a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 24430e1e6c750efa5787561aa151201b1fe7d428
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clever"></a><span data-ttu-id="b0083-103">教學課程：Azure Active Directory 與 Clever 整合</span><span class="sxs-lookup"><span data-stu-id="b0083-103">Tutorial: Azure Active Directory integration with Clever</span></span>

<span data-ttu-id="b0083-104">在此教學課程中，您學會如何 toointegrate Clever 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="b0083-104">In this tutorial, you learn how toointegrate Clever with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b0083-105">與 Azure AD 整合 Clever 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="b0083-105">Integrating Clever with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b0083-106">您可以控制存取 tooClever Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="b0083-106">You can control in Azure AD who has access tooClever.</span></span>
- <span data-ttu-id="b0083-107">您可以啟用您的使用者 tooautomatically get 登入 tooClever （單一登入） 具有其 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="b0083-107">You can enable your users tooautomatically get signed-on tooClever (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="b0083-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="b0083-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="b0083-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="b0083-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b0083-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="b0083-110">Prerequisites</span></span>

<span data-ttu-id="b0083-111">tooconfigure Clever 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="b0083-111">tooconfigure Azure AD integration with Clever, you need hello following items:</span></span>

- <span data-ttu-id="b0083-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b0083-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b0083-113">Clever 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b0083-113">A Clever single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b0083-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="b0083-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b0083-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="b0083-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b0083-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="b0083-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b0083-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="b0083-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b0083-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="b0083-118">Scenario description</span></span>
<span data-ttu-id="b0083-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b0083-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b0083-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="b0083-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b0083-121">從 hello 圖庫加入 Clever</span><span class="sxs-lookup"><span data-stu-id="b0083-121">Adding Clever from hello gallery</span></span>
2. <span data-ttu-id="b0083-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b0083-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-clever-from-hello-gallery"></a><span data-ttu-id="b0083-123">從 hello 圖庫加入 Clever</span><span class="sxs-lookup"><span data-stu-id="b0083-123">Adding Clever from hello gallery</span></span>
<span data-ttu-id="b0083-124">tooconfigure hello 整合 Clever 到 Azure AD，您需要 tooadd Clever hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b0083-124">tooconfigure hello integration of Clever into Azure AD, you need tooadd Clever from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b0083-125">**tooadd Clever 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b0083-125">**tooadd Clever from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b0083-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="b0083-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 按鈕][1]

2. <span data-ttu-id="b0083-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="b0083-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b0083-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="b0083-129">Then go too**All applications**.</span></span>

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. <span data-ttu-id="b0083-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="b0083-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 新應用程式按鈕][3]

4. <span data-ttu-id="b0083-133">在 hello 搜尋方塊中，輸入**Clever**，選取**Clever**然後按一下 從結果面板**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b0083-133">In hello search box, type **Clever**, select **Clever** from result panel then click **Add** button tooadd hello application.</span></span>

    ![聰明 hello [結果] 清單中](./media/active-directory-saas-clever-tutorial/tutorial_clever_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b0083-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b0083-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b0083-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Clever 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b0083-136">In this section, you configure and test Azure AD single sign-on with Clever based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b0083-137">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Clever 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="b0083-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Clever is tooa user in Azure AD.</span></span> <span data-ttu-id="b0083-138">換句話說，Azure AD 使用者與 hello Clever 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="b0083-138">In other words, a link relationship between an Azure AD user and hello related user in Clever needs toobe established.</span></span>

<span data-ttu-id="b0083-139">Clever 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="b0083-139">In Clever, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b0083-140">tooconfigure 及 Clever 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="b0083-140">tooconfigure and test Azure AD single sign-on with Clever, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b0083-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="b0083-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b0083-142">**[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="b0083-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b0083-143">**[建立聰明的測試使用者](#create-a-clever-test-user)** -toohave 許 Simon Clever 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="b0083-143">**[Create a Clever test user](#create-a-clever-test-user)** - toohave a counterpart of Britta Simon in Clever that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b0083-144">**[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b0083-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b0083-145">**[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="b0083-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b0083-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b0083-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b0083-147">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並聰明的應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="b0083-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Clever application.</span></span>

<span data-ttu-id="b0083-148">**tooconfigure Azure AD 單一登入與 Clever，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b0083-148">**tooconfigure Azure AD single sign-on with Clever, perform hello following steps:**</span></span>

1. <span data-ttu-id="b0083-149">在 Azure 入口網站上 hello hello **Clever**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="b0083-149">In hello Azure portal, on hello **Clever** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="b0083-151">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b0083-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-clever-tutorial/tutorial_clever_samlbase.png)

3. <span data-ttu-id="b0083-153">在 hello**聰明的網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="b0083-153">On hello **Clever Domain and URLs** section, perform hello following steps:</span></span>

    ![Clever 網域及 URL 單一登入資訊](./media/active-directory-saas-clever-tutorial/tutorial_clever_url.png)

    <span data-ttu-id="b0083-155">a.</span><span class="sxs-lookup"><span data-stu-id="b0083-155">a.</span></span> <span data-ttu-id="b0083-156">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://clever.com/in/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="b0083-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://clever.com/in/<companyname>`</span></span>

    <span data-ttu-id="b0083-157">b.</span><span class="sxs-lookup"><span data-stu-id="b0083-157">b.</span></span> <span data-ttu-id="b0083-158">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://clever.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="b0083-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://clever.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b0083-159">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="b0083-159">These values are not real.</span></span> <span data-ttu-id="b0083-160">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="b0083-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b0083-161">請連絡[聰明的用戶端支援小組](https://clever.com/about/contact/)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="b0083-161">Contact [Clever Client support team](https://clever.com/about/contact/) tooget these values.</span></span>

4. <span data-ttu-id="b0083-162">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="b0083-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![hello 憑證下載連結](./media/active-directory-saas-clever-tutorial/tutorial_clever_certificate.png)

5. <span data-ttu-id="b0083-164">hello 聰明的應用程式需要特定格式，這需要您 tooadd 自訂屬性對應 tooyour hello SAML 判斷提示**SAML 權杖屬性**組態。</span><span class="sxs-lookup"><span data-stu-id="b0083-164">hello Clever application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **SAML Token Attributes** configuration.</span></span>

    <span data-ttu-id="b0083-165">hello 下列螢幕擷取畫面會顯示這個範例。</span><span class="sxs-lookup"><span data-stu-id="b0083-165">hello following screenshot shows an example for this.</span></span>

    ![設定單一登入](./media/active-directory-saas-clever-tutorial/tutorial_clever_07.png) 

6. <span data-ttu-id="b0083-167">在 hello**使用者屬性**區段 hello**單一登入** 對話方塊中，上述 hello 映像中所示設定 SAML 權杖屬性和執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="b0083-167">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="b0083-168">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="b0083-168">Attribute Name</span></span>  | <span data-ttu-id="b0083-169">屬性值</span><span class="sxs-lookup"><span data-stu-id="b0083-169">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    | <span data-ttu-id="b0083-170">clever.student.credentials.district\_username</span><span class="sxs-lookup"><span data-stu-id="b0083-170">clever.student.credentials.district\_username</span></span>  | <span data-ttu-id="b0083-171">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="b0083-171">user.userprincipalname</span></span> |
    | <span data-ttu-id="b0083-172">Firstname</span><span class="sxs-lookup"><span data-stu-id="b0083-172">Firstname</span></span>  | <span data-ttu-id="b0083-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="b0083-173">user.givenname</span></span> |
    | <span data-ttu-id="b0083-174">lastname</span><span class="sxs-lookup"><span data-stu-id="b0083-174">Lastname</span></span>  | <span data-ttu-id="b0083-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="b0083-175">user.surname</span></span> |    

    <span data-ttu-id="b0083-176">a.</span><span class="sxs-lookup"><span data-stu-id="b0083-176">a.</span></span> <span data-ttu-id="b0083-177">按一下**加入屬性**tooopen hello**加入屬性**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="b0083-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-clever-tutorial/tutorial_attribute_04.png)
    
    ![設定單一登入](./media/active-directory-saas-clever-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="b0083-180">b.</span><span class="sxs-lookup"><span data-stu-id="b0083-180">b.</span></span> <span data-ttu-id="b0083-181">在 hello**名稱**文字方塊中，該資料列所顯示的型別 hello 屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="b0083-181">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="b0083-182">c.</span><span class="sxs-lookup"><span data-stu-id="b0083-182">c.</span></span> <span data-ttu-id="b0083-183">從 hello**值**清單，顯示該資料列的型別 hello 屬性值。</span><span class="sxs-lookup"><span data-stu-id="b0083-183">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="b0083-184">d.</span><span class="sxs-lookup"><span data-stu-id="b0083-184">d.</span></span> <span data-ttu-id="b0083-185">保留 hello**命名空間**空白的文字方塊。</span><span class="sxs-lookup"><span data-stu-id="b0083-185">Leave hello **Namespace** textbox blank.</span></span>
    
    <span data-ttu-id="b0083-186">d.</span><span class="sxs-lookup"><span data-stu-id="b0083-186">d.</span></span> <span data-ttu-id="b0083-187">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="b0083-187">Click **Ok**.</span></span>     

5. <span data-ttu-id="b0083-188">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="b0083-188">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-clever-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="b0083-190">toogenerate hello**中繼資料**url，請執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="b0083-190">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="b0083-191">a.</span><span class="sxs-lookup"><span data-stu-id="b0083-191">a.</span></span> <span data-ttu-id="b0083-192">按一下 [應用程式註冊]。</span><span class="sxs-lookup"><span data-stu-id="b0083-192">Click **App registrations**.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-clever-tutorial/tutorial_clever_appregistrations.png)
   
    <span data-ttu-id="b0083-194">b.</span><span class="sxs-lookup"><span data-stu-id="b0083-194">b.</span></span> <span data-ttu-id="b0083-195">按一下**端點**tooopen**端點** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="b0083-195">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![設定單一登入](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpointicon.png)

    <span data-ttu-id="b0083-197">c.</span><span class="sxs-lookup"><span data-stu-id="b0083-197">c.</span></span> <span data-ttu-id="b0083-198">按一下 hello 複製按鈕 toocopy**同盟中繼資料文件**url 並將它貼到 [記事本]。</span><span class="sxs-lookup"><span data-stu-id="b0083-198">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpoint.png)
     
    <span data-ttu-id="b0083-200">d.</span><span class="sxs-lookup"><span data-stu-id="b0083-200">d.</span></span> <span data-ttu-id="b0083-201">現在請 toohello 屬性頁的**Clever**和複製 hello**應用程式識別碼**使用**複製**按鈕，並將它貼到 [記事本]。</span><span class="sxs-lookup"><span data-stu-id="b0083-201">Now go toohello property page of **Clever** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-clever-tutorial/tutorial_clever_appid.png)

    <span data-ttu-id="b0083-203">e.</span><span class="sxs-lookup"><span data-stu-id="b0083-203">e.</span></span> <span data-ttu-id="b0083-204">產生 hello**中繼資料 URL**使用 hello 下列模式：`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="b0083-204">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>   

9. <span data-ttu-id="b0083-205">在不同的網頁瀏覽器視窗中，系統管理員身分登入 tooyour 聰明公司網站。</span><span class="sxs-lookup"><span data-stu-id="b0083-205">In a different web browser window, log in tooyour Clever company site as an administrator.</span></span>

10. <span data-ttu-id="b0083-206">在 hello 工具列中，按一下  **Instant 登入**。</span><span class="sxs-lookup"><span data-stu-id="b0083-206">In hello toolbar, click **Instant Login**.</span></span>

    <span data-ttu-id="b0083-207">![立即登入](./media/active-directory-saas-clever-tutorial/ic798984.png "立即登入")</span><span class="sxs-lookup"><span data-stu-id="b0083-207">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798984.png "Instant Login")</span></span>

11. <span data-ttu-id="b0083-208">在 hello **Instant 登入**頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="b0083-208">On hello **Instant Login** page, perform hello following steps:</span></span>
      
      <span data-ttu-id="b0083-209">![立即登入](./media/active-directory-saas-clever-tutorial/ic798985.png "立即登入")</span><span class="sxs-lookup"><span data-stu-id="b0083-209">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798985.png "Instant Login")</span></span>
      
      <span data-ttu-id="b0083-210">a.</span><span class="sxs-lookup"><span data-stu-id="b0083-210">a.</span></span> <span data-ttu-id="b0083-211">型別 hello**登入 URL**。</span><span class="sxs-lookup"><span data-stu-id="b0083-211">Type hello **Login URL**.</span></span>
      
      >[!NOTE]
      ><span data-ttu-id="b0083-212">hello**登入 URL**是自訂的值。</span><span class="sxs-lookup"><span data-stu-id="b0083-212">hello **Login URL** is a custom value.</span></span> <span data-ttu-id="b0083-213">請連絡[聰明的用戶端支援小組](https://clever.com/about/contact/)tooget 此值。</span><span class="sxs-lookup"><span data-stu-id="b0083-213">Contact [Clever Client support team](https://clever.com/about/contact/) tooget this value.</span></span>
      
      <span data-ttu-id="b0083-214">b.</span><span class="sxs-lookup"><span data-stu-id="b0083-214">b.</span></span> <span data-ttu-id="b0083-215">針對 [識別系統]，選取 [ADFS]。</span><span class="sxs-lookup"><span data-stu-id="b0083-215">As **Identity System**, select **ADFS**.</span></span>

      <span data-ttu-id="b0083-216">c.</span><span class="sxs-lookup"><span data-stu-id="b0083-216">c.</span></span> <span data-ttu-id="b0083-217">型別 hello**中繼資料 URL**在 hello**中繼資料 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="b0083-217">Type hello **Metadata URL** in hello **Metadata URL** textbox.</span></span>
      
      <span data-ttu-id="b0083-218">d.</span><span class="sxs-lookup"><span data-stu-id="b0083-218">d.</span></span> <span data-ttu-id="b0083-219">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="b0083-219">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="b0083-220">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="b0083-220">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b0083-221">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="b0083-221">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b0083-222">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b0083-222">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b0083-223">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b0083-223">Create an Azure AD test user</span></span>

<span data-ttu-id="b0083-224">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="b0083-224">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="b0083-226">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b0083-226">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b0083-227">在 hello Azure 入口網站，hello 左窗格中，按一下 hello **Azure Active Directory**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="b0083-227">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-clever-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="b0083-229">toodisplay hello 使用者清單，請移過**使用者和群組**，然後按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="b0083-229">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-clever-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="b0083-231">tooopen hello**使用者**對話方塊中，按一下 [**新增**頂端的 hello hello**所有使用者**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="b0083-231">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello [新增] 按鈕](./media/active-directory-saas-clever-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="b0083-233">在 hello**使用者**對話方塊方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="b0083-233">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello [使用者] 對話方塊](./media/active-directory-saas-clever-tutorial/create_aaduser_04.png)

    <span data-ttu-id="b0083-235">a.</span><span class="sxs-lookup"><span data-stu-id="b0083-235">a.</span></span> <span data-ttu-id="b0083-236">在 hello**名稱**方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="b0083-236">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b0083-237">b.</span><span class="sxs-lookup"><span data-stu-id="b0083-237">b.</span></span> <span data-ttu-id="b0083-238">在 hello**使用者名**方塊中，使用者許 Simon 類型 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="b0083-238">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="b0083-239">c.</span><span class="sxs-lookup"><span data-stu-id="b0083-239">c.</span></span> <span data-ttu-id="b0083-240">選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 hello**密碼**方塊。</span><span class="sxs-lookup"><span data-stu-id="b0083-240">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="b0083-241">d.</span><span class="sxs-lookup"><span data-stu-id="b0083-241">d.</span></span> <span data-ttu-id="b0083-242">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="b0083-242">Click **Create**.</span></span>
 
### <a name="create-a-clever-test-user"></a><span data-ttu-id="b0083-243">建立 Clever 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b0083-243">Create a Clever test user</span></span>

<span data-ttu-id="b0083-244">tooenable Azure AD 使用者 toolog 中 tooClever，它們必須佈建到 Clever。</span><span class="sxs-lookup"><span data-stu-id="b0083-244">tooenable Azure AD users toolog in tooClever, they must be provisioned into Clever.</span></span>

<span data-ttu-id="b0083-245">發生 Clever，搭配[聰明的用戶端支援小組](https://clever.com/about/contact/)hello 聰明平台中新增 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="b0083-245">In case of Clever, Work with [Clever Client support team](https://clever.com/about/contact/) to add hello users in hello Clever platform.</span></span> <span data-ttu-id="b0083-246">您必須先建立和啟動使用者，然後才能使用單一登入。</span><span class="sxs-lookup"><span data-stu-id="b0083-246">Users must be created and activated before you use single sign-on.</span></span> 

>[!NOTE]
><span data-ttu-id="b0083-247">您可以使用任何其他聰明的使用者帳戶建立工具或 Api 提供聰明 tooprovision Azure AD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="b0083-247">You can use any other Clever user account creation tools or APIs provided by Clever tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="b0083-248">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b0083-248">Assign hello Azure AD test user</span></span>

<span data-ttu-id="b0083-249">在本節中，您可以授與存取 tooClever 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b0083-249">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooClever.</span></span>

![指派 hello 使用者角色][200] 

<span data-ttu-id="b0083-251">**tooassign 許 Simon tooClever，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b0083-251">**tooassign Britta Simon tooClever, perform hello following steps:**</span></span>

1. <span data-ttu-id="b0083-252">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="b0083-252">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="b0083-254">在 [hello] 應用程式清單中，選取**Clever**。</span><span class="sxs-lookup"><span data-stu-id="b0083-254">In hello applications list, select **Clever**.</span></span>

    ![hello Clever hello 應用程式清單中的連結](./media/active-directory-saas-clever-tutorial/tutorial_clever_app.png)  

3. <span data-ttu-id="b0083-256">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="b0083-256">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello 「 使用者和群組 」 的連結][202]

4. <span data-ttu-id="b0083-258">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b0083-258">Click **Add** button.</span></span> <span data-ttu-id="b0083-259">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="b0083-259">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 將作業加入窗格][203]

5. <span data-ttu-id="b0083-261">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="b0083-261">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b0083-262">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b0083-262">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b0083-263">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b0083-263">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b0083-264">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="b0083-264">Test single sign-on</span></span>

<span data-ttu-id="b0083-265">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="b0083-265">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b0083-266">當您按一下 hello 聰明磚中的 hello 存取面板，您應該取得自動登入 tooyour 聰明的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b0083-266">When you click hello Clever tile in hello Access Panel, you should get automatically signed-on tooyour Clever application.</span></span>
<span data-ttu-id="b0083-267">如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="b0083-267">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b0083-268">其他資源</span><span class="sxs-lookup"><span data-stu-id="b0083-268">Additional resources</span></span>

* [<span data-ttu-id="b0083-269">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b0083-269">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b0083-270">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="b0083-270">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clever-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clever-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clever-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clever-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clever-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clever-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clever-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clever-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clever-tutorial/tutorial_general_203.png

