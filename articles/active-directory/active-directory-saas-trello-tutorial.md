---
title: "教學課程：Azure Active Directory 與 Trello 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Trello 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cd5ae365-9ed6-43a6-920b-f7814b993949
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: de2f2ba6a0e5545983c351f26f99d14f436618c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-trello"></a><span data-ttu-id="4889d-103">教學課程：Azure Active Directory 與 Trello 整合</span><span class="sxs-lookup"><span data-stu-id="4889d-103">Tutorial: Azure Active Directory integration with Trello</span></span>

<span data-ttu-id="4889d-104">在此教學課程中，您學會如何 toointegrate Trello 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="4889d-104">In this tutorial, you learn how toointegrate Trello with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4889d-105">與 Azure AD 整合 Trello 為您提供下列優點的 hello:</span><span class="sxs-lookup"><span data-stu-id="4889d-105">Integrating Trello with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4889d-106">您可以控制存取 tooTrello Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="4889d-106">You can control in Azure AD who has access tooTrello</span></span>
- <span data-ttu-id="4889d-107">您可以啟用您的使用者 tooautomatically get 登入 tooTrello （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="4889d-107">You can enable your users tooautomatically get signed-on tooTrello (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4889d-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="4889d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4889d-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="4889d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4889d-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="4889d-110">Prerequisites</span></span>

<span data-ttu-id="4889d-111">tooconfigure Azure AD 與 Trello 的整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="4889d-111">tooconfigure Azure AD integration with Trello, you need hello following items:</span></span>

- <span data-ttu-id="4889d-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="4889d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4889d-113">已啟用 Trello 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="4889d-113">A Trello single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4889d-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="4889d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4889d-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="4889d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4889d-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="4889d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4889d-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="4889d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4889d-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="4889d-118">Scenario description</span></span>
<span data-ttu-id="4889d-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4889d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4889d-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="4889d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4889d-121">從 hello 圖庫加入 Trello</span><span class="sxs-lookup"><span data-stu-id="4889d-121">Adding Trello from hello gallery</span></span>
2. <span data-ttu-id="4889d-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="4889d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-trello-from-hello-gallery"></a><span data-ttu-id="4889d-123">從 hello 圖庫加入 Trello</span><span class="sxs-lookup"><span data-stu-id="4889d-123">Adding Trello from hello gallery</span></span>
<span data-ttu-id="4889d-124">tooconfigure hello 整合 Trello 到 Azure AD，您需要 tooadd Trello hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4889d-124">tooconfigure hello integration of Trello into Azure AD, you need tooadd Trello from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4889d-125">**tooadd Trello 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="4889d-125">**tooadd Trello from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4889d-126">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="4889d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4889d-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="4889d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4889d-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="4889d-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="4889d-131">tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="4889d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="4889d-133">在 [hello] 搜尋方塊中，輸入**Trello**。</span><span class="sxs-lookup"><span data-stu-id="4889d-133">In hello search box, type **Trello**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-trello-tutorial/tutorial_trello_search.png)

5. <span data-ttu-id="4889d-135">在 [hello [結果] 窗格中，選取 [ **Trello**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4889d-135">In hello results panel, select **Trello**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-trello-tutorial/tutorial_trello_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4889d-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="4889d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4889d-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Trello 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4889d-138">In this section, you configure and test Azure AD single sign-on with Trello based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4889d-139">單一登入 toowork，Azure AD 需要 tooknow hello 對應項目在 Trello 中的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="4889d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Trello is tooa user in Azure AD.</span></span> <span data-ttu-id="4889d-140">換句話說，Azure AD 使用者與 Trello 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="4889d-140">In other words, a link relationship between an Azure AD user and hello related user in Trello needs toobe established.</span></span>

<span data-ttu-id="4889d-141">在 Trello 中，將指派 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="4889d-141">In Trello, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4889d-142">tooconfigure 及 Azure AD 單一登入與 Trello 的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="4889d-142">tooconfigure and test Azure AD single sign-on with Trello, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4889d-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="4889d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4889d-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="4889d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4889d-145">**[建立 Trello 測試使用者](#creating-a-trello-test-user)** -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示法的 Trello 中對應項目。</span><span class="sxs-lookup"><span data-stu-id="4889d-145">**[Creating a Trello test user](#creating-a-trello-test-user)** - toohave a counterpart of Britta Simon in Trello that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4889d-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4889d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4889d-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="4889d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4889d-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="4889d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4889d-149">在本節中，您啟用 Azure AD 單一登入 hello Azure 入口網站中，並在 Trello 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="4889d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Trello application.</span></span>

<span data-ttu-id="4889d-150">**tooconfigure Azure AD 單一登入與 Trello，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="4889d-150">**tooconfigure Azure AD single sign-on with Trello, perform hello following steps:**</span></span>

1. <span data-ttu-id="4889d-151">在 Azure 入口網站上 hello hello **Trello**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="4889d-151">In hello Azure portal, on hello **Trello** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="4889d-153">在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4889d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-trello-tutorial/tutorial_trello_samlbase.png)

3. <span data-ttu-id="4889d-155">在 [hello **Trello 網域和 Url**區段中，如果您想 tooconfigure hello 應用程式中的**IDP 初始化模式**，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="4889d-155">On hello **Trello Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-trello-tutorial/tutorial_trello_url.png)

    <span data-ttu-id="4889d-157">在 [hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://trello.com/auth/saml/consume/<enterprise>`</span><span class="sxs-lookup"><span data-stu-id="4889d-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span></span>

4. <span data-ttu-id="4889d-158">在 [hello **Trello 網域和 Url**區段中，如果您想 tooconfigure hello 應用程式中的**SP 初始模式**，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="4889d-158">On hello **Trello Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![設定單一登入](./media/active-directory-saas-trello-tutorial/tutorial_trello_url1.png)

    <span data-ttu-id="4889d-160">a.</span><span class="sxs-lookup"><span data-stu-id="4889d-160">a.</span></span> <span data-ttu-id="4889d-161">按一下 hello**顯示進階的 URL 設定**。</span><span class="sxs-lookup"><span data-stu-id="4889d-161">Click on hello **Show advanced URL settings**.</span></span>

    <span data-ttu-id="4889d-162">b.</span><span class="sxs-lookup"><span data-stu-id="4889d-162">b.</span></span> <span data-ttu-id="4889d-163">在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://trello.com/auth/saml/consume/<enterprise>`</span><span class="sxs-lookup"><span data-stu-id="4889d-163">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span></span>

    >[!NOTE]
    ><span data-ttu-id="4889d-164">您應該會收到 hello **\<企業\>**從 Trello slug。</span><span class="sxs-lookup"><span data-stu-id="4889d-164">You should get hello **\<enterprise\>** slug from Trello.</span></span> <span data-ttu-id="4889d-165">如果您沒有 hello slug 值，請連絡[Trello 支援小組](mailto:support@trello.com)tooget 您企業的 hello 動態資料欄位。</span><span class="sxs-lookup"><span data-stu-id="4889d-165">If you don't have hello slug value, contact [Trello support team](mailto:support@trello.com) tooget hello slug for you enterprise.</span></span>
    > 

5. <span data-ttu-id="4889d-166">Trello 應用程式預期 hello SAML 判斷提示 toocontain 特定屬性。</span><span class="sxs-lookup"><span data-stu-id="4889d-166">Trello application expects hello SAML assertions toocontain specific attributes.</span></span> <span data-ttu-id="4889d-167">設定下列屬性，此應用程式的 hello。</span><span class="sxs-lookup"><span data-stu-id="4889d-167">Configure hello following attributes  for this application.</span></span> <span data-ttu-id="4889d-168">您可以從 hello 管理這些屬性的 hello 值**使用者屬性 」** hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4889d-168">You can manage hello values of these attributes from hello **"User Attributes"** of hello application.</span></span> <span data-ttu-id="4889d-169">hello 下列螢幕擷取畫面會顯示這個範例。</span><span class="sxs-lookup"><span data-stu-id="4889d-169">hello following screenshot shows an example for this.</span></span>

    ![設定單一登入](./media/active-directory-saas-trello-tutorial/tutorial_trello_attribute.png)

6. <span data-ttu-id="4889d-171">在 [hello **SAML 權杖屬性**] 對話方塊中，每個資料列 hello 下表中所示執行 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="4889d-171">On hello **SAML token attributes** dialog, for each row shown in hello table below, perform hello following steps:</span></span>
 
    | <span data-ttu-id="4889d-172">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="4889d-172">Attribute Name</span></span> | <span data-ttu-id="4889d-173">屬性值</span><span class="sxs-lookup"><span data-stu-id="4889d-173">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="4889d-174">User.Email</span><span class="sxs-lookup"><span data-stu-id="4889d-174">User.Email</span></span> | <span data-ttu-id="4889d-175">user.mail</span><span class="sxs-lookup"><span data-stu-id="4889d-175">user.mail</span></span> |
    | <span data-ttu-id="4889d-176">User.FirstName</span><span class="sxs-lookup"><span data-stu-id="4889d-176">User.FirstName</span></span> | <span data-ttu-id="4889d-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="4889d-177">user.givenname</span></span> |
    | <span data-ttu-id="4889d-178">User.LastName</span><span class="sxs-lookup"><span data-stu-id="4889d-178">User.LastName</span></span> | <span data-ttu-id="4889d-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="4889d-179">user.surname</span></span> |

    <span data-ttu-id="4889d-180">a.</span><span class="sxs-lookup"><span data-stu-id="4889d-180">a.</span></span> <span data-ttu-id="4889d-181">按一下**加入屬性**tooopen hello**加入屬性**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="4889d-181">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-trello-tutorial/tutorial_officespace_04.png)

    ![設定單一登入](./media/active-directory-saas-trello-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="4889d-184">b.</span><span class="sxs-lookup"><span data-stu-id="4889d-184">b.</span></span> <span data-ttu-id="4889d-185">在 [hello**名稱**文字方塊中，該資料列所顯示的型別 hello 屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="4889d-185">In hello **Name** textbox, type hello attribute name shown for that row.</span></span> 

    <span data-ttu-id="4889d-186">c.</span><span class="sxs-lookup"><span data-stu-id="4889d-186">c.</span></span> <span data-ttu-id="4889d-187">從 hello**值**清單，顯示該資料列的型別 hello 屬性值。</span><span class="sxs-lookup"><span data-stu-id="4889d-187">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="4889d-188">d.</span><span class="sxs-lookup"><span data-stu-id="4889d-188">d.</span></span> <span data-ttu-id="4889d-189">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="4889d-189">Click **Ok**.</span></span> 
 
7. <span data-ttu-id="4889d-190">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="4889d-190">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-trello-tutorial/tutorial_trello_certificate.png) 

8. <span data-ttu-id="4889d-192">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="4889d-192">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-trello-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4889d-194">在 [hello **Trello 組態**區段中，按一下**設定 Trello** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="4889d-194">On hello **Trello Configuration** section, click **Configure Trello** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4889d-195">複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="4889d-195">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-trello-tutorial/tutorial_trello_configure.png) 

9. <span data-ttu-id="4889d-197">設定應用程式的 SSO tooget 太移[Trello 企業 SSO 組態](https://trello.com/sso-configuration)頁面 toosend [Trello 支援小組](mailto:support@trello.com)hello **SAML 單一登入服務 URL**和附加 hello**憑證 (Base64)**。</span><span class="sxs-lookup"><span data-stu-id="4889d-197">tooget SSO configured for your application, go too[Trello enterprise SSO configuration](https://trello.com/sso-configuration) page toosend [Trello support team](mailto:support@trello.com) hello **SAML Single Sign-On Service URL** and attach hello **Certificate (Base64)**.</span></span>

> [!TIP]
> <span data-ttu-id="4889d-198">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="4889d-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4889d-199">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="4889d-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4889d-200">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4889d-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4889d-201">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="4889d-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="4889d-202">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="4889d-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="4889d-204">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="4889d-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4889d-205">在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="4889d-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-trello-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4889d-207">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="4889d-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-trello-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4889d-209">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="4889d-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-trello-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4889d-211">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="4889d-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-trello-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4889d-213">a.</span><span class="sxs-lookup"><span data-stu-id="4889d-213">a.</span></span> <span data-ttu-id="4889d-214">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="4889d-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4889d-215">b.</span><span class="sxs-lookup"><span data-stu-id="4889d-215">b.</span></span> <span data-ttu-id="4889d-216">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="4889d-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4889d-217">c.</span><span class="sxs-lookup"><span data-stu-id="4889d-217">c.</span></span> <span data-ttu-id="4889d-218">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="4889d-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4889d-219">d.</span><span class="sxs-lookup"><span data-stu-id="4889d-219">d.</span></span> <span data-ttu-id="4889d-220">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="4889d-220">Click **Create**.</span></span>
 
### <a name="creating-a-trello-test-user"></a><span data-ttu-id="4889d-221">建立 Trello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="4889d-221">Creating a Trello test user</span></span>

<span data-ttu-id="4889d-222">在本節中，您會在 Trello 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="4889d-222">In this section, you create a user called Britta Simon in Trello.</span></span> <span data-ttu-id="4889d-223">在本節中，您會在 Trello 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="4889d-223">In this section, you create a user called Britta Simon in Trello.</span></span> <span data-ttu-id="4889d-224">Trello 支援在 just-in-time 佈建和建立新的帳戶是 hello 登入第一次從 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="4889d-224">Trello supports just-in-time provisioning and a new account is created hello first time you sign in from Azure AD.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4889d-225">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="4889d-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4889d-226">在本節中，您可以授與存取 tooTrello 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4889d-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTrello.</span></span>

![指派使用者][200] 

<span data-ttu-id="4889d-228">**tooassign 許 Simon tooTrello，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="4889d-228">**tooassign Britta Simon tooTrello, perform hello following steps:**</span></span>

1. <span data-ttu-id="4889d-229">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="4889d-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="4889d-231">在 [hello] 應用程式清單中，選取**Trello**。</span><span class="sxs-lookup"><span data-stu-id="4889d-231">In hello applications list, select **Trello**.</span></span>

    ![設定單一登入](./media/active-directory-saas-trello-tutorial/tutorial_trello_app.png) 

3. <span data-ttu-id="4889d-233">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="4889d-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="4889d-235">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4889d-235">Click **Add** button.</span></span> <span data-ttu-id="4889d-236">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="4889d-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="4889d-238">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="4889d-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4889d-239">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4889d-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4889d-240">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4889d-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4889d-241">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="4889d-241">Testing single sign-on</span></span>

<span data-ttu-id="4889d-242">hello 本節目標在於 tootest 您 Azure AD 的 SSO 組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="4889d-242">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="4889d-243">當您按一下 hello Trello 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Trello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4889d-243">When you click hello Trello tile in hello Access Panel, you should get automatically signed-on tooyour Trello application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4889d-244">其他資源</span><span class="sxs-lookup"><span data-stu-id="4889d-244">Additional resources</span></span>

* [<span data-ttu-id="4889d-245">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4889d-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4889d-246">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="4889d-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-trello-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-trello-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-trello-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-trello-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-trello-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-trello-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-trello-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-trello-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-trello-tutorial/tutorial_general_203.png

