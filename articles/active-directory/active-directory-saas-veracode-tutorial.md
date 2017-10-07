---
title: "教學課程：Azure Active Directory 與 Veracode 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Veracode 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4fe78050-cb6d-4db9-96ec-58cc0779167f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: d17307b3864b7df8ee55f569d8f962e2e315b936
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-veracode"></a><span data-ttu-id="cff12-103">教學課程：Azure Active Directory 與 Veracode 整合</span><span class="sxs-lookup"><span data-stu-id="cff12-103">Tutorial: Azure Active Directory integration with Veracode</span></span>

<span data-ttu-id="cff12-104">在此教學課程中，您學會如何 toointegrate Veracode 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="cff12-104">In this tutorial, you learn how toointegrate Veracode with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cff12-105">Veracode 整合與 Azure AD 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="cff12-105">Integrating Veracode with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cff12-106">您可以控制存取 tooVeracode Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="cff12-106">You can control in Azure AD who has access tooVeracode.</span></span>
- <span data-ttu-id="cff12-107">您可以啟用您的使用者 tooautomatically get 登入 tooVeracode （單一登入） 具有其 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="cff12-107">You can enable your users tooautomatically get signed-on tooVeracode (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="cff12-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="cff12-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="cff12-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="cff12-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cff12-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="cff12-110">Prerequisites</span></span>

<span data-ttu-id="cff12-111">tooconfigure Azure AD 與 Veracode 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="cff12-111">tooconfigure Azure AD integration with Veracode, you need hello following items:</span></span>

- <span data-ttu-id="cff12-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="cff12-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cff12-113">已啟用 Veracode 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="cff12-113">A Veracode single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cff12-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="cff12-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cff12-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="cff12-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cff12-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="cff12-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cff12-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="cff12-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cff12-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="cff12-118">Scenario description</span></span>
<span data-ttu-id="cff12-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cff12-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cff12-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="cff12-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cff12-121">從 hello 圖庫新增 Veracode</span><span class="sxs-lookup"><span data-stu-id="cff12-121">Add Veracode from hello gallery</span></span>
2. <span data-ttu-id="cff12-122">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="cff12-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-veracode-from-hello-gallery"></a><span data-ttu-id="cff12-123">從 hello 圖庫新增 Veracode</span><span class="sxs-lookup"><span data-stu-id="cff12-123">Add Veracode from hello gallery</span></span>
<span data-ttu-id="cff12-124">tooconfigure hello 整合 Veracode 到 Azure AD，您需要 tooadd Veracode hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cff12-124">tooconfigure hello integration of Veracode into Azure AD, you need tooadd Veracode from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cff12-125">**tooadd Veracode 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="cff12-125">**tooadd Veracode from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cff12-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="cff12-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 按鈕][1]

2. <span data-ttu-id="cff12-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="cff12-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cff12-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="cff12-129">Then go too**All applications**.</span></span>

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. <span data-ttu-id="cff12-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="cff12-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 新應用程式按鈕][3]

4. <span data-ttu-id="cff12-133">在 hello 搜尋方塊中，輸入**Veracode**，選取**Veracode**然後按一下 從結果面板**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cff12-133">In hello search box, type **Veracode**, select  **Veracode** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Veracode hello [結果] 清單中](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="cff12-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="cff12-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="cff12-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Veracode 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cff12-136">In this section, you configure and test Azure AD single sign-on with Veracode based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cff12-137">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Veracode 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="cff12-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Veracode is tooa user in Azure AD.</span></span> <span data-ttu-id="cff12-138">換句話說，Azure AD 使用者與 Veracode 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="cff12-138">In other words, a link relationship between an Azure AD user and hello related user in Veracode needs toobe established.</span></span>

<span data-ttu-id="cff12-139">Veracode 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="cff12-139">In Veracode, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="cff12-140">tooconfigure 和測試 Azure AD 單一登入與 Veracode，您需要遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="cff12-140">tooconfigure and test Azure AD single sign-on with Veracode, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cff12-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="cff12-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cff12-142">**[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="cff12-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cff12-143">**[建立測試使用者 Veracode](#create-a-veracode-test-user)**  -toohave 許 Simon Veracode 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="cff12-143">**[Create a Veracode test user](#create-a-veracode-test-user)** - toohave a counterpart of Britta Simon in Veracode that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cff12-144">**[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cff12-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cff12-145">**[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="cff12-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="cff12-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="cff12-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="cff12-147">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Veracode 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="cff12-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Veracode application.</span></span>

<span data-ttu-id="cff12-148">**tooconfigure Azure AD 單一登入與 Veracode，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="cff12-148">**tooconfigure Azure AD single sign-on with Veracode, perform hello following steps:**</span></span>

1. <span data-ttu-id="cff12-149">在 Azure 入口網站上 hello hello **Veracode**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="cff12-149">In hello Azure portal, on hello **Veracode** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="cff12-151">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cff12-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_samlbase.png)

3. <span data-ttu-id="cff12-153">在 [hello **Veracode 網域和 Url** ] 區段中，使用者沒有 tooperform 任何步驟，因為與 Azure 已預先整合 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cff12-153">On hello **Veracode Domain and URLs** section, the user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span> 

    ![設定單一登入](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_url.png)

4. <span data-ttu-id="cff12-155">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="cff12-155">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![hello 憑證下載連結](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_certificate.png) 

5. <span data-ttu-id="cff12-157">hello 本節目標在於的 toooutline tooenable 使用者 tooauthenticate tooVeracode 的同盟，使用 Azure AD 的帳戶與如何 hello SAML 通訊協定為基礎。</span><span class="sxs-lookup"><span data-stu-id="cff12-157">hello objective of this section is toooutline how tooenable users tooauthenticate tooVeracode with their account in Azure AD using federation based on hello SAML protocol.</span></span>

    <span data-ttu-id="cff12-158">Veracode 應用程式需要特定格式，這需要您 tooadd 自訂屬性對應 tooyour hello SAML 判斷提示**saml 權杖屬性**組態。</span><span class="sxs-lookup"><span data-stu-id="cff12-158">Your Veracode application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **saml token attributes** configuration.</span></span> <span data-ttu-id="cff12-159">hello 下列螢幕擷取畫面會顯示這個範例。</span><span class="sxs-lookup"><span data-stu-id="cff12-159">hello following screenshot shows an example for this.</span></span>
    
    <span data-ttu-id="cff12-160">![屬性](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "屬性")</span><span class="sxs-lookup"><span data-stu-id="cff12-160">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "Attributes")</span></span>

6. <span data-ttu-id="cff12-161">tooadd hello 必要屬性對應，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="cff12-161">tooadd hello required attribute mappings, perform hello following steps:</span></span>

    | <span data-ttu-id="cff12-162">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="cff12-162">Attribute Name</span></span> | <span data-ttu-id="cff12-163">屬性值</span><span class="sxs-lookup"><span data-stu-id="cff12-163">Attribute Value</span></span> |
    |--- |--- |
    | <span data-ttu-id="cff12-164">firstname</span><span class="sxs-lookup"><span data-stu-id="cff12-164">firstname</span></span> |<span data-ttu-id="cff12-165">User.givenname</span><span class="sxs-lookup"><span data-stu-id="cff12-165">User.givenname</span></span> |
    | <span data-ttu-id="cff12-166">lastname</span><span class="sxs-lookup"><span data-stu-id="cff12-166">lastname</span></span> |<span data-ttu-id="cff12-167">User.surname</span><span class="sxs-lookup"><span data-stu-id="cff12-167">User.surname</span></span> |
    | <span data-ttu-id="cff12-168">電子郵件</span><span class="sxs-lookup"><span data-stu-id="cff12-168">email</span></span> |<span data-ttu-id="cff12-169">User.mail</span><span class="sxs-lookup"><span data-stu-id="cff12-169">User.mail</span></span> |
    
    <span data-ttu-id="cff12-170">a.</span><span class="sxs-lookup"><span data-stu-id="cff12-170">a.</span></span> <span data-ttu-id="cff12-171">上述的 hello 資料表中每個資料列，按一下 **新增使用者屬性**。</span><span class="sxs-lookup"><span data-stu-id="cff12-171">For each data row in hello table above, click **add user attribute**.</span></span>
    
    <span data-ttu-id="cff12-172">![屬性](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "屬性")</span><span class="sxs-lookup"><span data-stu-id="cff12-172">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "Attributes")</span></span>
    
    <span data-ttu-id="cff12-173">![屬性](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "屬性")</span><span class="sxs-lookup"><span data-stu-id="cff12-173">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "Attributes")</span></span>
    
    <span data-ttu-id="cff12-174">b.</span><span class="sxs-lookup"><span data-stu-id="cff12-174">b.</span></span> <span data-ttu-id="cff12-175">在 hello**屬性名稱**文字方塊中，該資料列所顯示的型別 hello 屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="cff12-175">In hello **Attribute Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="cff12-176">c.</span><span class="sxs-lookup"><span data-stu-id="cff12-176">c.</span></span> <span data-ttu-id="cff12-177">在 hello**屬性值**文字方塊中，顯示該資料列選取 hello 屬性值。</span><span class="sxs-lookup"><span data-stu-id="cff12-177">In hello **Attribute Value** textbox, select hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="cff12-178">d.</span><span class="sxs-lookup"><span data-stu-id="cff12-178">d.</span></span> <span data-ttu-id="cff12-179">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="cff12-179">Click **Ok**.</span></span>

7. <span data-ttu-id="cff12-180">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="cff12-180">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-veracode-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="cff12-182">在 hello **Veracode 組態**區段中，按一下**設定 Veracode** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="cff12-182">On hello **Veracode Configuration** section, click **Configure Veracode** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="cff12-183">複製 hello **SAML 實體識別碼**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="cff12-183">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Veracode 組態](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_configure.png) 

9. <span data-ttu-id="cff12-185">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 Veracode 公司網站。</span><span class="sxs-lookup"><span data-stu-id="cff12-185">In a different web browser window, log into your Veracode company site as an administrator.</span></span>

10. <span data-ttu-id="cff12-186">在 hello 最上層顯示 hello 功能表上，按一下**設定**，然後按一下**管理員**。</span><span class="sxs-lookup"><span data-stu-id="cff12-186">In hello menu on hello top, click **Settings**, and then click **Admin**.</span></span>
   
    <span data-ttu-id="cff12-187">![管理](./media/active-directory-saas-veracode-tutorial/ic802911.png "管理")</span><span class="sxs-lookup"><span data-stu-id="cff12-187">![Administration](./media/active-directory-saas-veracode-tutorial/ic802911.png "Administration")</span></span>

11. <span data-ttu-id="cff12-188">按一下 hello **SAML**  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="cff12-188">Click hello **SAML** tab.</span></span>

12. <span data-ttu-id="cff12-189">在 hello**組織 SAML 設定**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="cff12-189">In hello **Organization SAML Settings** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="cff12-190">![管理](./media/active-directory-saas-veracode-tutorial/ic802912.png "管理")</span><span class="sxs-lookup"><span data-stu-id="cff12-190">![Administration](./media/active-directory-saas-veracode-tutorial/ic802912.png "Administration")</span></span>
   
    <span data-ttu-id="cff12-191">a.</span><span class="sxs-lookup"><span data-stu-id="cff12-191">a.</span></span>  <span data-ttu-id="cff12-192">在**簽發者**文字方塊中，貼上 hello 值**SAML 實體識別碼**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="cff12-192">In  **Issuer** textbox, paste hello value of  **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="cff12-193">b.</span><span class="sxs-lookup"><span data-stu-id="cff12-193">b.</span></span> <span data-ttu-id="cff12-194">您下載的憑證，從 Azure 入口網站中，按一下 tooupload**選擇檔案**。</span><span class="sxs-lookup"><span data-stu-id="cff12-194">tooupload your downloaded certificate from Azure portal, click **Choose File**.</span></span>
   
    <span data-ttu-id="cff12-195">c.</span><span class="sxs-lookup"><span data-stu-id="cff12-195">c.</span></span> <span data-ttu-id="cff12-196">選取 [啟用自動註冊] 。</span><span class="sxs-lookup"><span data-stu-id="cff12-196">Select **Enable Self Registration**.</span></span>

13. <span data-ttu-id="cff12-197">在 hello**自我登錄設定**區段中，執行下列步驟，hello，然後按一下**儲存**:</span><span class="sxs-lookup"><span data-stu-id="cff12-197">In hello **Self Registration Settings** section, perform hello following steps, and then click **Save**:</span></span>
   
    <span data-ttu-id="cff12-198">![管理](./media/active-directory-saas-veracode-tutorial/ic802913.png "管理")</span><span class="sxs-lookup"><span data-stu-id="cff12-198">![Administration](./media/active-directory-saas-veracode-tutorial/ic802913.png "Administration")</span></span>
   
    <span data-ttu-id="cff12-199">a.</span><span class="sxs-lookup"><span data-stu-id="cff12-199">a.</span></span> <span data-ttu-id="cff12-200">在 [啟用新的使用者] 選取 [不需要啟用]。</span><span class="sxs-lookup"><span data-stu-id="cff12-200">As **New User Activation**, select **No Activation Required**.</span></span>
   
    <span data-ttu-id="cff12-201">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="cff12-201">b.</span></span> <span data-ttu-id="cff12-202">在 [使用者資料更新] 選取 [Veracode 使用者資料喜好設定]。</span><span class="sxs-lookup"><span data-stu-id="cff12-202">As **User Data Updates**, select **Preference Veracode User Data**.</span></span>
   
    <span data-ttu-id="cff12-203">c.</span><span class="sxs-lookup"><span data-stu-id="cff12-203">c.</span></span> <span data-ttu-id="cff12-204">如**SAML 屬性的詳細資料**，選取下列 hello:</span><span class="sxs-lookup"><span data-stu-id="cff12-204">For **SAML Attribute Details**, select hello following:</span></span>
      * <span data-ttu-id="cff12-205">**[使用者角色]**</span><span class="sxs-lookup"><span data-stu-id="cff12-205">**User Roles**</span></span>
      * <span data-ttu-id="cff12-206">**[原則系統管理員]**</span><span class="sxs-lookup"><span data-stu-id="cff12-206">**Policy Administrator**</span></span>
      * <span data-ttu-id="cff12-207">**[檢閱者]**</span><span class="sxs-lookup"><span data-stu-id="cff12-207">**Reviewer**</span></span>
      * <span data-ttu-id="cff12-208">**[安全性負責人]**</span><span class="sxs-lookup"><span data-stu-id="cff12-208">**Security Lead**</span></span>
      * <span data-ttu-id="cff12-209">**[行政人員]**</span><span class="sxs-lookup"><span data-stu-id="cff12-209">**Executive**</span></span>
      * <span data-ttu-id="cff12-210">**[傳送者]**</span><span class="sxs-lookup"><span data-stu-id="cff12-210">**Submitter**</span></span>
      * <span data-ttu-id="cff12-211">**[建立者]**</span><span class="sxs-lookup"><span data-stu-id="cff12-211">**Creator**</span></span>
      * <span data-ttu-id="cff12-212">**[所有掃描類型]**</span><span class="sxs-lookup"><span data-stu-id="cff12-212">**All Scan Types**</span></span>
      * <span data-ttu-id="cff12-213">**[小組成員資格]**</span><span class="sxs-lookup"><span data-stu-id="cff12-213">**Team Memberships**</span></span>
      * <span data-ttu-id="cff12-214">**[預設小組]**</span><span class="sxs-lookup"><span data-stu-id="cff12-214">**Default Team**</span></span>

> [!TIP]
> <span data-ttu-id="cff12-215">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="cff12-215">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cff12-216">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="cff12-216">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cff12-217">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cff12-217">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="cff12-218">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="cff12-218">Create an Azure AD test user</span></span>

<span data-ttu-id="cff12-219">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="cff12-219">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="cff12-221">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="cff12-221">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cff12-222">在 hello Azure 入口網站，hello 左窗格中，按一下 hello **Azure Active Directory**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="cff12-222">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-veracode-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="cff12-224">toodisplay hello 使用者清單，請移過**使用者和群組**，然後按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="cff12-224">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-veracode-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="cff12-226">tooopen hello**使用者**對話方塊中，按一下 [**新增**頂端的 hello hello**所有使用者**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="cff12-226">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello [新增] 按鈕](./media/active-directory-saas-veracode-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="cff12-228">在 hello**使用者**對話方塊方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="cff12-228">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello [使用者] 對話方塊](./media/active-directory-saas-veracode-tutorial/create_aaduser_04.png)

    <span data-ttu-id="cff12-230">a.</span><span class="sxs-lookup"><span data-stu-id="cff12-230">a.</span></span> <span data-ttu-id="cff12-231">在 hello**名稱**方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="cff12-231">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cff12-232">b.</span><span class="sxs-lookup"><span data-stu-id="cff12-232">b.</span></span> <span data-ttu-id="cff12-233">在 hello**使用者名**方塊中，使用者許 Simon 類型 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="cff12-233">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="cff12-234">c.</span><span class="sxs-lookup"><span data-stu-id="cff12-234">c.</span></span> <span data-ttu-id="cff12-235">選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 hello**密碼**方塊。</span><span class="sxs-lookup"><span data-stu-id="cff12-235">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="cff12-236">d.</span><span class="sxs-lookup"><span data-stu-id="cff12-236">d.</span></span> <span data-ttu-id="cff12-237">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="cff12-237">Click **Create**.</span></span>
 
### <a name="create-a-veracode-test-user"></a><span data-ttu-id="cff12-238">建立 Veracode 測試使用者</span><span class="sxs-lookup"><span data-stu-id="cff12-238">Create a Veracode test user</span></span>
<span data-ttu-id="cff12-239">在訂單 tooenable Azure AD 使用者 toolog Veracode 成，它們必須佈建到 Veracode。</span><span class="sxs-lookup"><span data-stu-id="cff12-239">In order tooenable Azure AD users toolog into Veracode, they must be provisioned into Veracode.</span></span> <span data-ttu-id="cff12-240">中的 Veracode hello 案例中，佈建是自動化的工作。</span><span class="sxs-lookup"><span data-stu-id="cff12-240">In hello case of Veracode, provisioning is an automated task.</span></span> <span data-ttu-id="cff12-241">沒有您適用的動作項目。</span><span class="sxs-lookup"><span data-stu-id="cff12-241">There is no action item for you.</span></span> <span data-ttu-id="cff12-242">使用者會自動建立必要 hello 第一個單一登入嘗試期間。</span><span class="sxs-lookup"><span data-stu-id="cff12-242">Users are automatically created if necessary during hello first single sign-on attempt.</span></span>

> [!NOTE]
> <span data-ttu-id="cff12-243">您可以使用任何其他 Veracode 使用者帳戶建立工具或 Api 提供 Veracode tooprovision Azure AD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="cff12-243">You can use any other Veracode user account creation tools or APIs provided by Veracode tooprovision Azure AD user accounts.</span></span>
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="cff12-244">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="cff12-244">Assign hello Azure AD test user</span></span>

<span data-ttu-id="cff12-245">在本節中，您可以授與存取 tooVeracode 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cff12-245">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooVeracode.</span></span>

![指派 hello 使用者角色][200] 

<span data-ttu-id="cff12-247">**tooassign 許 Simon tooVeracode，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="cff12-247">**tooassign Britta Simon tooVeracode, perform hello following steps:**</span></span>

1. <span data-ttu-id="cff12-248">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="cff12-248">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="cff12-250">在 [hello] 應用程式清單中，選取**Veracode**。</span><span class="sxs-lookup"><span data-stu-id="cff12-250">In hello applications list, select **Veracode**.</span></span>

    ![hello 應用程式清單中的 hello Veracode 連結](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_app.png)  

3. <span data-ttu-id="cff12-252">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="cff12-252">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello 「 使用者和群組 」 的連結][202]

4. <span data-ttu-id="cff12-254">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cff12-254">Click **Add** button.</span></span> <span data-ttu-id="cff12-255">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="cff12-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 將作業加入窗格][203]

5. <span data-ttu-id="cff12-257">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="cff12-257">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cff12-258">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cff12-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cff12-259">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cff12-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="cff12-260">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="cff12-260">Test single sign-on</span></span>

<span data-ttu-id="cff12-261">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="cff12-261">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cff12-262">當您按一下 hello Veracode 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Veracode 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cff12-262">When you click hello Veracode tile in hello Access Panel, you should get automatically signed-on tooyour Veracode application.</span></span>
<span data-ttu-id="cff12-263">如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="cff12-263">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="cff12-264">其他資源</span><span class="sxs-lookup"><span data-stu-id="cff12-264">Additional resources</span></span>

* [<span data-ttu-id="cff12-265">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cff12-265">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cff12-266">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="cff12-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_203.png

