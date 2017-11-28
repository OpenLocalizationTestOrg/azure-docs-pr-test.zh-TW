---
title: "教學課程：Azure Active Directory 與 Moxtra 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Moxtra 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2aed2d4b-1dcd-4839-8fed-9419d107c61c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 82e2fcc390ba508e86a3992ec1c81d0a0ffed96b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moxtra"></a><span data-ttu-id="1eab9-103">教學課程：Azure Active Directory 與 Moxtra 整合</span><span class="sxs-lookup"><span data-stu-id="1eab9-103">Tutorial: Azure Active Directory integration with Moxtra</span></span>

<span data-ttu-id="1eab9-104">在此教學課程中，您學會如何 toointegrate Moxtra 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="1eab9-104">In this tutorial, you learn how toointegrate Moxtra with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1eab9-105">Moxtra 整合與 Azure AD 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="1eab9-105">Integrating Moxtra with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1eab9-106">您可以控制存取 tooMoxtra Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="1eab9-106">You can control in Azure AD who has access tooMoxtra</span></span>
- <span data-ttu-id="1eab9-107">您可以啟用您的使用者 tooautomatically get 登入 tooMoxtra （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="1eab9-107">You can enable your users tooautomatically get signed-on tooMoxtra (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1eab9-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="1eab9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1eab9-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="1eab9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1eab9-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="1eab9-110">Prerequisites</span></span>

<span data-ttu-id="1eab9-111">tooconfigure Azure AD 與 Moxtra 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="1eab9-111">tooconfigure Azure AD integration with Moxtra, you need hello following items:</span></span>

- <span data-ttu-id="1eab9-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1eab9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1eab9-113">已啟用 Moxtra 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1eab9-113">A Moxtra single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1eab9-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="1eab9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1eab9-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="1eab9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1eab9-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="1eab9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1eab9-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="1eab9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1eab9-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="1eab9-118">Scenario description</span></span>
<span data-ttu-id="1eab9-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1eab9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1eab9-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="1eab9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1eab9-121">從 hello 圖庫加入 Moxtra</span><span class="sxs-lookup"><span data-stu-id="1eab9-121">Adding Moxtra from hello gallery</span></span>
2. <span data-ttu-id="1eab9-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1eab9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moxtra-from-hello-gallery"></a><span data-ttu-id="1eab9-123">從 hello 圖庫加入 Moxtra</span><span class="sxs-lookup"><span data-stu-id="1eab9-123">Adding Moxtra from hello gallery</span></span>
<span data-ttu-id="1eab9-124">tooconfigure hello 整合 Moxtra 到 Azure AD，您需要 tooadd Moxtra hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1eab9-124">tooconfigure hello integration of Moxtra into Azure AD, you need tooadd Moxtra from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1eab9-125">**tooadd Moxtra 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1eab9-125">**tooadd Moxtra from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1eab9-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="1eab9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1eab9-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="1eab9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1eab9-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="1eab9-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="1eab9-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="1eab9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="1eab9-133">在 [hello] 搜尋方塊中，輸入**Moxtra**。</span><span class="sxs-lookup"><span data-stu-id="1eab9-133">In hello search box, type **Moxtra**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_search.png)

5. <span data-ttu-id="1eab9-135">在 hello 結果 窗格中，選取  **Moxtra**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1eab9-135">In hello results panel, select **Moxtra**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1eab9-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1eab9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1eab9-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Moxtra 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1eab9-138">In this section, you configure and test Azure AD single sign-on with Moxtra based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1eab9-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Moxtra 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="1eab9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Moxtra is tooa user in Azure AD.</span></span> <span data-ttu-id="1eab9-140">換句話說，Azure AD 使用者與 Moxtra 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="1eab9-140">In other words, a link relationship between an Azure AD user and hello related user in Moxtra needs toobe established.</span></span>

<span data-ttu-id="1eab9-141">Moxtra 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="1eab9-141">In Moxtra, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1eab9-142">tooconfigure 和測試 Azure AD 單一登入與 Moxtra，您需要遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="1eab9-142">tooconfigure and test Azure AD single sign-on with Moxtra, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1eab9-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="1eab9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1eab9-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="1eab9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1eab9-145">**[建立測試使用者 Moxtra](#creating-a-moxtra-test-user)**  -toohave 許 Simon Moxtra 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="1eab9-145">**[Creating a Moxtra test user](#creating-a-moxtra-test-user)** - toohave a counterpart of Britta Simon in Moxtra that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1eab9-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1eab9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1eab9-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="1eab9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1eab9-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1eab9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1eab9-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Moxtra 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="1eab9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Moxtra application.</span></span>

<span data-ttu-id="1eab9-150">**tooconfigure Azure AD 單一登入與 Moxtra，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1eab9-150">**tooconfigure Azure AD single sign-on with Moxtra, perform hello following steps:**</span></span>

1. <span data-ttu-id="1eab9-151">在 Azure 入口網站上 hello hello **Moxtra**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="1eab9-151">In hello Azure portal, on hello **Moxtra** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="1eab9-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1eab9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_samlbase.png)

3. <span data-ttu-id="1eab9-155">在 hello **Moxtra 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1eab9-155">On hello **Moxtra Domain and URLs** section, perform hello following step:</span></span>

    ![設定單一登入](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_url.png)

    <span data-ttu-id="1eab9-157">在 hello**登入 URL**文字方塊中，輸入與 URL:`https://www.moxtra.com/service/#login`</span><span class="sxs-lookup"><span data-stu-id="1eab9-157">In hello **Sign-on URL** textbox, type a URL as: `https://www.moxtra.com/service/#login`</span></span>

4. <span data-ttu-id="1eab9-158">Moxtra 應用程式預期 hello SAML 判斷提示，以特定格式。</span><span class="sxs-lookup"><span data-stu-id="1eab9-158">Moxtra application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="1eab9-159">設定下列宣告為此應用程式的 hello。</span><span class="sxs-lookup"><span data-stu-id="1eab9-159">Configure hello following claims for this application.</span></span> <span data-ttu-id="1eab9-160">您可以從 hello 管理 hello 這些屬性的值"**使用者屬性**」 一節，在應用程式整合頁面上。</span><span class="sxs-lookup"><span data-stu-id="1eab9-160">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="1eab9-161">hello 下列螢幕擷取畫面顯示此組態範例。</span><span class="sxs-lookup"><span data-stu-id="1eab9-161">hello following screenshot shows an example for this configuration.</span></span> 

    ![設定單一登入](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_attributes.png)
    
5. <span data-ttu-id="1eab9-163">在 hello**使用者屬性**hello 區段**單一登入** 對話方塊中，hello 映像中所示設定 SAML 權杖屬性並執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1eab9-163">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="1eab9-164">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="1eab9-164">Attribute Name</span></span> | <span data-ttu-id="1eab9-165">屬性值</span><span class="sxs-lookup"><span data-stu-id="1eab9-165">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="1eab9-166">firstname</span><span class="sxs-lookup"><span data-stu-id="1eab9-166">firstname</span></span> | <span data-ttu-id="1eab9-167">user.givenname</span><span class="sxs-lookup"><span data-stu-id="1eab9-167">user.givenname</span></span> |
    | <span data-ttu-id="1eab9-168">lastname</span><span class="sxs-lookup"><span data-stu-id="1eab9-168">lastname</span></span> | <span data-ttu-id="1eab9-169">user.surname</span><span class="sxs-lookup"><span data-stu-id="1eab9-169">user.surname</span></span> |
    | <span data-ttu-id="1eab9-170">idpid</span><span class="sxs-lookup"><span data-stu-id="1eab9-170">idpid</span></span>    | <span data-ttu-id="1eab9-171">< SAML 實體識別碼 ></span><span class="sxs-lookup"><span data-stu-id="1eab9-171">< SAML Entity ID ></span></span> 

    > [!Note]
    > <span data-ttu-id="1eab9-172">hello 值**idpid**不是真正的屬性。</span><span class="sxs-lookup"><span data-stu-id="1eab9-172">hello value of **idpid** attribute is not real.</span></span> <span data-ttu-id="1eab9-173">您可以取得 hello 實際值從**快速參考**區段**Moxtra 組態**。</span><span class="sxs-lookup"><span data-stu-id="1eab9-173">You can get hello actual value from **Quick reference** section under **Moxtra Configuration**.</span></span>
    
    <span data-ttu-id="1eab9-174">a.</span><span class="sxs-lookup"><span data-stu-id="1eab9-174">a.</span></span> <span data-ttu-id="1eab9-175">按一下**加入屬性**tooopen hello**加入屬性**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="1eab9-175">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="1eab9-177">b.</span><span class="sxs-lookup"><span data-stu-id="1eab9-177">b.</span></span> <span data-ttu-id="1eab9-178">在 hello**名稱**文字方塊中，該資料列所顯示的型別 hello 屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="1eab9-178">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    ![設定單一登入](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="1eab9-180">c.</span><span class="sxs-lookup"><span data-stu-id="1eab9-180">c.</span></span> <span data-ttu-id="1eab9-181">從 hello**值**清單，顯示該資料列的型別 hello 屬性值。</span><span class="sxs-lookup"><span data-stu-id="1eab9-181">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="1eab9-182">d.</span><span class="sxs-lookup"><span data-stu-id="1eab9-182">d.</span></span> <span data-ttu-id="1eab9-183">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="1eab9-183">Click **Ok**.</span></span>
    
5. <span data-ttu-id="1eab9-184">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="1eab9-184">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_certificate.png) 

6. <span data-ttu-id="1eab9-186">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="1eab9-186">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-moxtra-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="1eab9-188">在 hello **Moxtra 組態**區段中，按一下**設定 Moxtra** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="1eab9-188">On hello **Moxtra Configuration** section, click **Configure Moxtra** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1eab9-189">複製 hello **SAML 實體識別碼和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="1eab9-189">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_configure.png) 

8. <span data-ttu-id="1eab9-191">在另一個瀏覽器視窗中，系統管理員身分登入 tooyour Moxtra 公司網站。</span><span class="sxs-lookup"><span data-stu-id="1eab9-191">In another browser window, sign on tooyour Moxtra company site as an administrator.</span></span>

9. <span data-ttu-id="1eab9-192">在左側 hello hello 工具列中按一下**管理主控台 > SAML 單一登入**，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="1eab9-192">In hello toolbar on hello left, click **Admin Console > SAML Single Sign-on**, and then click **New**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_06.png) 

10. <span data-ttu-id="1eab9-194">在 hello **SAML**頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1eab9-194">On hello **SAML** page, perform hello following steps:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_08.png)   
 
    <span data-ttu-id="1eab9-196">a.</span><span class="sxs-lookup"><span data-stu-id="1eab9-196">a.</span></span> <span data-ttu-id="1eab9-197">在 hello**名稱**文字方塊中，輸入您的組態名稱 (例如： *SAML*)。</span><span class="sxs-lookup"><span data-stu-id="1eab9-197">In hello **Name** textbox, type a name for your configuration (e.g.: *SAML*).</span></span> 
  
    <span data-ttu-id="1eab9-198">b.</span><span class="sxs-lookup"><span data-stu-id="1eab9-198">b.</span></span> <span data-ttu-id="1eab9-199">在 hello **IdP 實體識別碼**文字方塊中，貼上 hello 值**SAML 實體識別碼**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="1eab9-199">In hello **IdP Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="1eab9-200">c.</span><span class="sxs-lookup"><span data-stu-id="1eab9-200">c.</span></span> <span data-ttu-id="1eab9-201">在**登入 URL**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="1eab9-201">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="1eab9-202">d.</span><span class="sxs-lookup"><span data-stu-id="1eab9-202">d.</span></span> <span data-ttu-id="1eab9-203">在 hello **AuthnContextClassRef**文字方塊中，輸入**urn: oasis： 名稱： tc: SAML:2.0:ac:classes:Password**。</span><span class="sxs-lookup"><span data-stu-id="1eab9-203">In hello **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span> 
 
    <span data-ttu-id="1eab9-204">e.</span><span class="sxs-lookup"><span data-stu-id="1eab9-204">e.</span></span> <span data-ttu-id="1eab9-205">在 hello **NameID 格式**文字方塊中，輸入**urn: oasis： 名稱： tc: saml: 1.1 nameid-format-: emailAddress**。</span><span class="sxs-lookup"><span data-stu-id="1eab9-205">In hello **NameID Format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span> 
 
    <span data-ttu-id="1eab9-206">f.</span><span class="sxs-lookup"><span data-stu-id="1eab9-206">f.</span></span> <span data-ttu-id="1eab9-207">開啟憑證，從 [記事本] 中的 Azure 入口網站下載 hello 內容複製並貼到 hello**憑證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="1eab9-207">Open certificate which you have downloaded from Azure portal in notepad, copy hello content, and then paste it into hello **Certificate** textbox.</span></span>    
 
    <span data-ttu-id="1eab9-208">g.</span><span class="sxs-lookup"><span data-stu-id="1eab9-208">g.</span></span> <span data-ttu-id="1eab9-209">在 hello SAML 電子郵件網域 文字方塊中，輸入您的 SAML 電子郵件網域。</span><span class="sxs-lookup"><span data-stu-id="1eab9-209">In hello SAML email domain textbox, type your SAML email domain.</span></span>    
  
    >[!NOTE]
    ><span data-ttu-id="1eab9-210">toosee hello 步驟 tooverify hello 網域中，按一下 hello"**我**"下。</span><span class="sxs-lookup"><span data-stu-id="1eab9-210">toosee hello steps tooverify hello domain, click hello "**i**" below.</span></span>

    <span data-ttu-id="1eab9-211">h.</span><span class="sxs-lookup"><span data-stu-id="1eab9-211">h.</span></span> <span data-ttu-id="1eab9-212">按一下 [更新] 。</span><span class="sxs-lookup"><span data-stu-id="1eab9-212">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="1eab9-213">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="1eab9-213">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1eab9-214">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="1eab9-214">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1eab9-215">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1eab9-215">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1eab9-216">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1eab9-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="1eab9-217">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="1eab9-217">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="1eab9-219">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1eab9-219">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1eab9-220">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="1eab9-220">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-moxtra-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1eab9-222">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="1eab9-222">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-moxtra-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1eab9-224">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="1eab9-224">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-moxtra-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1eab9-226">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1eab9-226">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-moxtra-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1eab9-228">a.</span><span class="sxs-lookup"><span data-stu-id="1eab9-228">a.</span></span> <span data-ttu-id="1eab9-229">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="1eab9-229">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1eab9-230">b.</span><span class="sxs-lookup"><span data-stu-id="1eab9-230">b.</span></span> <span data-ttu-id="1eab9-231">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="1eab9-231">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1eab9-232">c.</span><span class="sxs-lookup"><span data-stu-id="1eab9-232">c.</span></span> <span data-ttu-id="1eab9-233">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="1eab9-233">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1eab9-234">d.</span><span class="sxs-lookup"><span data-stu-id="1eab9-234">d.</span></span> <span data-ttu-id="1eab9-235">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="1eab9-235">Click **Create**.</span></span>
 
### <a name="creating-a-moxtra-test-user"></a><span data-ttu-id="1eab9-236">建立 Moxtra 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1eab9-236">Creating a Moxtra test user</span></span>

<span data-ttu-id="1eab9-237">hello 本節目標在於 toocreate Moxtra 中呼叫許 Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="1eab9-237">hello objective of this section is toocreate a user called Britta Simon in Moxtra.</span></span>

<span data-ttu-id="1eab9-238">**toocreate 呼叫許 Simon Moxtra，在使用者執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1eab9-238">**toocreate a user called Britta Simon in Moxtra, perform hello following steps:**</span></span>

1. <span data-ttu-id="1eab9-239">登入 tooyour Moxtra 公司網站的系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="1eab9-239">Sign on tooyour Moxtra company site as an administrator.</span></span>

2. <span data-ttu-id="1eab9-240">在左側 hello hello 工具列中按一下**管理主控台 > 使用者管理**，然後**新增使用者**。</span><span class="sxs-lookup"><span data-stu-id="1eab9-240">In hello toolbar on hello left, click **Admin Console > User Management**, and then **Add User**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_10.png) 

3. <span data-ttu-id="1eab9-242">在 [hello**新增使用者**] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1eab9-242">On hello **Add User** dialog, perform hello following steps:</span></span>
  
    <span data-ttu-id="1eab9-243">a.</span><span class="sxs-lookup"><span data-stu-id="1eab9-243">a.</span></span> <span data-ttu-id="1eab9-244">在 hello**名字**文字方塊中，輸入**許**。</span><span class="sxs-lookup"><span data-stu-id="1eab9-244">In hello **First Name** textbox, type **Britta**.</span></span>
  
    <span data-ttu-id="1eab9-245">b.</span><span class="sxs-lookup"><span data-stu-id="1eab9-245">b.</span></span> <span data-ttu-id="1eab9-246">在 hello**姓氏**文字方塊中，輸入**Simon**。</span><span class="sxs-lookup"><span data-stu-id="1eab9-246">In hello **Last Name** textbox, type **Simon**.</span></span>
  
    <span data-ttu-id="1eab9-247">c.</span><span class="sxs-lookup"><span data-stu-id="1eab9-247">c.</span></span> <span data-ttu-id="1eab9-248">在 hello**電子郵件**文字方塊中，輸入許的電子郵件地址相同 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="1eab9-248">In hello **Email** textbox, type Britta's email address same as on Azure portal.</span></span>
  
    <span data-ttu-id="1eab9-249">d.</span><span class="sxs-lookup"><span data-stu-id="1eab9-249">d.</span></span> <span data-ttu-id="1eab9-250">在 hello**除法**文字方塊中，輸入**Dev**。</span><span class="sxs-lookup"><span data-stu-id="1eab9-250">In hello **Division** textbox, type **Dev**.</span></span>
  
    <span data-ttu-id="1eab9-251">e.</span><span class="sxs-lookup"><span data-stu-id="1eab9-251">e.</span></span> <span data-ttu-id="1eab9-252">在 hello**部門**文字方塊中，輸入**IT**。</span><span class="sxs-lookup"><span data-stu-id="1eab9-252">In hello **Department** textbox, type **IT**.</span></span>
  
    <span data-ttu-id="1eab9-253">f.</span><span class="sxs-lookup"><span data-stu-id="1eab9-253">f.</span></span> <span data-ttu-id="1eab9-254">選取 [系統管理員]。</span><span class="sxs-lookup"><span data-stu-id="1eab9-254">Select **Administrator**.</span></span>
  
    <span data-ttu-id="1eab9-255">g.</span><span class="sxs-lookup"><span data-stu-id="1eab9-255">g.</span></span> <span data-ttu-id="1eab9-256">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="1eab9-256">Click **Add**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1eab9-257">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="1eab9-257">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1eab9-258">在本節中，您可以授與存取 tooMoxtra 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1eab9-258">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMoxtra.</span></span>

![指派使用者][200] 

<span data-ttu-id="1eab9-260">**tooassign 許 Simon tooMoxtra，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1eab9-260">**tooassign Britta Simon tooMoxtra, perform hello following steps:**</span></span>

1. <span data-ttu-id="1eab9-261">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="1eab9-261">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="1eab9-263">在 [hello] 應用程式清單中，選取**Moxtra**。</span><span class="sxs-lookup"><span data-stu-id="1eab9-263">In hello applications list, select **Moxtra**.</span></span>

    ![設定單一登入](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_app.png) 

3. <span data-ttu-id="1eab9-265">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="1eab9-265">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="1eab9-267">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1eab9-267">Click **Add** button.</span></span> <span data-ttu-id="1eab9-268">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="1eab9-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="1eab9-270">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="1eab9-270">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1eab9-271">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1eab9-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1eab9-272">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1eab9-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1eab9-273">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="1eab9-273">Testing single sign-on</span></span>

<span data-ttu-id="1eab9-274">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="1eab9-274">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1eab9-275">當您按一下 hello Moxtra 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Moxtra 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1eab9-275">When you click hello Moxtra tile in hello Access Panel, you should get automatically signed-on tooyour Moxtra application.</span></span>
<span data-ttu-id="1eab9-276">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="1eab9-276">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1eab9-277">其他資源</span><span class="sxs-lookup"><span data-stu-id="1eab9-277">Additional resources</span></span>

* [<span data-ttu-id="1eab9-278">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1eab9-278">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1eab9-279">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="1eab9-279">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_203.png

