---
title: "教學課程：Azure Active Directory 與 Boomi 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Boomi 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8e05afa9-2eda-4975-a0cc-6d408065860f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: ce64a4561697d311a8c7b1b244315bb552c5cfb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-boomi"></a><span data-ttu-id="8d31f-103">教學課程：Azure Active Directory 與 Boomi 整合</span><span class="sxs-lookup"><span data-stu-id="8d31f-103">Tutorial: Azure Active Directory integration with Boomi</span></span>

<span data-ttu-id="8d31f-104">在此教學課程中，您學會如何 toointegrate Boomi 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="8d31f-104">In this tutorial, you learn how toointegrate Boomi with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8d31f-105">與 Azure AD 整合 Boomi 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="8d31f-105">Integrating Boomi with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8d31f-106">您可以控制存取 tooBoomi Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="8d31f-106">You can control in Azure AD who has access tooBoomi</span></span>
- <span data-ttu-id="8d31f-107">您可以啟用您的使用者 tooautomatically get 登入 tooBoomi （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="8d31f-107">You can enable your users tooautomatically get signed-on tooBoomi (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8d31f-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="8d31f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8d31f-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="8d31f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d31f-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="8d31f-110">Prerequisites</span></span>

<span data-ttu-id="8d31f-111">tooconfigure 與 Boomi 的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="8d31f-111">tooconfigure Azure AD integration with Boomi, you need hello following items:</span></span>

- <span data-ttu-id="8d31f-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="8d31f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8d31f-113">啟用 Boomi 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="8d31f-113">A Boomi single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8d31f-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="8d31f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8d31f-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="8d31f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8d31f-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="8d31f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8d31f-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="8d31f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8d31f-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="8d31f-118">Scenario description</span></span>
<span data-ttu-id="8d31f-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8d31f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8d31f-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="8d31f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8d31f-121">從 hello 圖庫加入 Boomi</span><span class="sxs-lookup"><span data-stu-id="8d31f-121">Adding Boomi from hello gallery</span></span>
2. <span data-ttu-id="8d31f-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="8d31f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-boomi-from-hello-gallery"></a><span data-ttu-id="8d31f-123">從 hello 圖庫加入 Boomi</span><span class="sxs-lookup"><span data-stu-id="8d31f-123">Adding Boomi from hello gallery</span></span>
<span data-ttu-id="8d31f-124">tooconfigure hello 整合 Boomi 的 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Boomi。</span><span class="sxs-lookup"><span data-stu-id="8d31f-124">tooconfigure hello integration of Boomi into Azure AD, you need tooadd Boomi from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8d31f-125">**tooadd Boomi 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="8d31f-125">**tooadd Boomi from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d31f-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="8d31f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8d31f-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="8d31f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8d31f-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="8d31f-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="8d31f-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="8d31f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="8d31f-133">在 [hello] 搜尋方塊中，輸入**Boomi**。</span><span class="sxs-lookup"><span data-stu-id="8d31f-133">In hello search box, type **Boomi**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_search.png)

5. <span data-ttu-id="8d31f-135">在 hello 結果 窗格中，選取  **Boomi**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8d31f-135">In hello results panel, select **Boomi**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8d31f-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="8d31f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8d31f-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Boomi 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8d31f-138">In this section, you configure and test Azure AD single sign-on with Boomi based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8d31f-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 Boomi 中是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="8d31f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Boomi is tooa user in Azure AD.</span></span> <span data-ttu-id="8d31f-140">換句話說，Azure AD 使用者與 hello Boomi 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="8d31f-140">In other words, a link relationship between an Azure AD user and hello related user in Boomi needs toobe established.</span></span>

<span data-ttu-id="8d31f-141">在 Boomi 中，將指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="8d31f-141">In Boomi, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8d31f-142">tooconfigure 及測試 Azure AD 單一登入 Boomi，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="8d31f-142">tooconfigure and test Azure AD single sign-on with Boomi, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8d31f-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="8d31f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8d31f-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="8d31f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8d31f-145">**[建立測試使用者 Boomi](#creating-a-boomi-test-user)**  -toohave 許 Simon Boomi 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="8d31f-145">**[Creating a Boomi test user](#creating-a-boomi-test-user)** - toohave a counterpart of Britta Simon in Boomi that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8d31f-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8d31f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8d31f-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="8d31f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8d31f-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="8d31f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8d31f-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Boomi 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="8d31f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Boomi application.</span></span>

<span data-ttu-id="8d31f-150">**tooconfigure Azure AD 單一登入 Boomi，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="8d31f-150">**tooconfigure Azure AD single sign-on with Boomi, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d31f-151">在 Azure 入口網站上 hello hello **Boomi**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="8d31f-151">In hello Azure portal, on hello **Boomi** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="8d31f-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8d31f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_samlbase.png)

3. <span data-ttu-id="8d31f-155">在 hello **Boomi 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="8d31f-155">On hello **Boomi Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_url.png)

    <span data-ttu-id="8d31f-157">a.</span><span class="sxs-lookup"><span data-stu-id="8d31f-157">a.</span></span> <span data-ttu-id="8d31f-158">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://platform.boomi.com/sso/<accountname>/saml`</span><span class="sxs-lookup"><span data-stu-id="8d31f-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://platform.boomi.com/sso/<accountname>/saml`</span></span>

    <span data-ttu-id="8d31f-159">b.</span><span class="sxs-lookup"><span data-stu-id="8d31f-159">b.</span></span> <span data-ttu-id="8d31f-160">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://platform.boomi.com/sso/<accountname>/saml`</span><span class="sxs-lookup"><span data-stu-id="8d31f-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://platform.boomi.com/sso/<accountname>/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8d31f-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="8d31f-161">These values are not real.</span></span> <span data-ttu-id="8d31f-162">以 hello 實際的識別項和回覆 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="8d31f-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="8d31f-163">請連絡[Boomi 支援小組](https://boomi.com/company/contact/)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="8d31f-163">Contact [Boomi support team](https://boomi.com/company/contact/) tooget these values.</span></span>

4. <span data-ttu-id="8d31f-164">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="8d31f-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_certificate.png)

4. <span data-ttu-id="8d31f-166">Boomi 應用程式預期 hello SAML 判斷提示，以特定格式。</span><span class="sxs-lookup"><span data-stu-id="8d31f-166">Boomi application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="8d31f-167">請設定下列宣告為此應用程式的 hello。</span><span class="sxs-lookup"><span data-stu-id="8d31f-167">Please configure hello following claims for this application.</span></span> <span data-ttu-id="8d31f-168">您可以從 hello 管理 hello 這些屬性的值"**使用者屬性**」 一節，在應用程式整合頁面上。</span><span class="sxs-lookup"><span data-stu-id="8d31f-168">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="8d31f-169">hello 下列螢幕擷取畫面會顯示這個範例。</span><span class="sxs-lookup"><span data-stu-id="8d31f-169">hello following screenshot shows an example for this.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-boomi-tutorial/tutorial_attribute.png)

5. <span data-ttu-id="8d31f-171">在 hello**使用者屬性**區段 hello**單一登入** 對話方塊中，每個資料列 hello 下表中所示執行 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="8d31f-171">In hello **User Attributes** section on hello **Single sign-on** dialog, for each row shown in hello table below, perform hello following steps:</span></span>

    | <span data-ttu-id="8d31f-172">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="8d31f-172">Attribute Name</span></span> | <span data-ttu-id="8d31f-173">屬性值</span><span class="sxs-lookup"><span data-stu-id="8d31f-173">Attribute Value</span></span> |
    | -------------- | --------------- |
    | <span data-ttu-id="8d31f-174">FEDERATION_ID</span><span class="sxs-lookup"><span data-stu-id="8d31f-174">FEDERATION_ID</span></span> | <span data-ttu-id="8d31f-175">user.mail</span><span class="sxs-lookup"><span data-stu-id="8d31f-175">user.mail</span></span> |
    
    <span data-ttu-id="8d31f-176">a.</span><span class="sxs-lookup"><span data-stu-id="8d31f-176">a.</span></span> <span data-ttu-id="8d31f-177">按一下**加入屬性**tooopen hello**加入屬性**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="8d31f-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_04.png)
    
    ![設定單一登入](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="8d31f-180">b.</span><span class="sxs-lookup"><span data-stu-id="8d31f-180">b.</span></span> <span data-ttu-id="8d31f-181">在 hello**名稱**文字方塊中，該資料列所顯示的型別 hello 屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="8d31f-181">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="8d31f-182">c.</span><span class="sxs-lookup"><span data-stu-id="8d31f-182">c.</span></span> <span data-ttu-id="8d31f-183">從 hello**值**清單，顯示該資料列的型別 hello 屬性值。</span><span class="sxs-lookup"><span data-stu-id="8d31f-183">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="8d31f-184">d.</span><span class="sxs-lookup"><span data-stu-id="8d31f-184">d.</span></span> <span data-ttu-id="8d31f-185">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="8d31f-185">Click **Ok**.</span></span>

6. <span data-ttu-id="8d31f-186">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="8d31f-186">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-boomi-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="8d31f-188">在 hello **Boomi 組態**區段中，按一下**設定 Boomi** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="8d31f-188">On hello **Boomi Configuration** section, click **Configure Boomi** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8d31f-189">複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="8d31f-189">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_configure.png) 

8. <span data-ttu-id="8d31f-191">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 Boomi 公司網站。</span><span class="sxs-lookup"><span data-stu-id="8d31f-191">In a different web browser window, log into your Boomi company site as an administrator.</span></span> 

9. <span data-ttu-id="8d31f-192">瀏覽過**公司名稱**並移過**設定**。</span><span class="sxs-lookup"><span data-stu-id="8d31f-192">Navigate too**Company Name** and go too**Set up**.</span></span>

10. <span data-ttu-id="8d31f-193">按一下 hello **SSO 選項**索引標籤上，執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="8d31f-193">Click hello **SSO Options** tab and perform below steps.</span></span>

    ![在應用程式端設定單一登入](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_11.png)

    <span data-ttu-id="8d31f-195">a.</span><span class="sxs-lookup"><span data-stu-id="8d31f-195">a.</span></span> <span data-ttu-id="8d31f-196">選取 [啟用 SAML 單一登入] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="8d31f-196">Check **Enable SAML Single Sign-On** checkbox.</span></span>

    <span data-ttu-id="8d31f-197">b.</span><span class="sxs-lookup"><span data-stu-id="8d31f-197">b.</span></span> <span data-ttu-id="8d31f-198">按一下**匯入**tooupload hello 下載憑證從 Azure AD 太**身分識別提供者憑證**。</span><span class="sxs-lookup"><span data-stu-id="8d31f-198">Click **Import** tooupload hello downloaded certificate from Azure AD too**Identity Provider Certificate**.</span></span>
    
    <span data-ttu-id="8d31f-199">c.</span><span class="sxs-lookup"><span data-stu-id="8d31f-199">c.</span></span> <span data-ttu-id="8d31f-200">在 [hello**身分識別提供者登入 URL**文字方塊中，將 hello 值放**SAML 單一登入服務 URL**從 Azure AD 應用程式設定] 視窗。</span><span class="sxs-lookup"><span data-stu-id="8d31f-200">In hello **Identity Provider Login URL** textbox, put hello value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="8d31f-201">d.</span><span class="sxs-lookup"><span data-stu-id="8d31f-201">d.</span></span> <span data-ttu-id="8d31f-202">針對 [同盟識別碼位置]，選取 [同盟識別碼位於 FEDERATION_ID 屬性元素] 選項按鈕。</span><span class="sxs-lookup"><span data-stu-id="8d31f-202">As **Federation Id Location**, select **Federation Id is in FEDERATION_ID Attribute element** radio button.</span></span> 

    <span data-ttu-id="8d31f-203">e.</span><span class="sxs-lookup"><span data-stu-id="8d31f-203">e.</span></span> <span data-ttu-id="8d31f-204">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="8d31f-204">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="8d31f-205">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="8d31f-205">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8d31f-206">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="8d31f-206">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8d31f-207">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8d31f-207">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8d31f-208">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="8d31f-208">Creating an Azure AD test user</span></span>
<span data-ttu-id="8d31f-209">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="8d31f-209">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="8d31f-211">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="8d31f-211">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d31f-212">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="8d31f-212">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-boomi-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8d31f-214">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="8d31f-214">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-boomi-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8d31f-216">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="8d31f-216">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-boomi-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8d31f-218">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="8d31f-218">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-boomi-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8d31f-220">a.</span><span class="sxs-lookup"><span data-stu-id="8d31f-220">a.</span></span> <span data-ttu-id="8d31f-221">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="8d31f-221">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8d31f-222">b.</span><span class="sxs-lookup"><span data-stu-id="8d31f-222">b.</span></span> <span data-ttu-id="8d31f-223">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="8d31f-223">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8d31f-224">c.</span><span class="sxs-lookup"><span data-stu-id="8d31f-224">c.</span></span> <span data-ttu-id="8d31f-225">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="8d31f-225">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8d31f-226">d.</span><span class="sxs-lookup"><span data-stu-id="8d31f-226">d.</span></span> <span data-ttu-id="8d31f-227">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="8d31f-227">Click **Create**.</span></span>
 
### <a name="creating-a-boomi-test-user"></a><span data-ttu-id="8d31f-228">建立 Boomi 測試使用者</span><span class="sxs-lookup"><span data-stu-id="8d31f-228">Creating a Boomi test user</span></span>

<span data-ttu-id="8d31f-229">在訂單 tooenable Azure AD 使用者 toolog tooBoomi 中，您必須是佈建到 Boomi。</span><span class="sxs-lookup"><span data-stu-id="8d31f-229">In order tooenable Azure AD users toolog in tooBoomi, they must be provisioned into Boomi.</span></span> <span data-ttu-id="8d31f-230">在 Boomi 的 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="8d31f-230">In hello case of Boomi, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="8d31f-231">tooprovision 使用者帳戶，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="8d31f-231">tooprovision a user account, perform hello following steps:</span></span>

1. <span data-ttu-id="8d31f-232">登入 tooyour Boomi 公司網站的系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="8d31f-232">Log in tooyour Boomi company site as an administrator.</span></span>

2. <span data-ttu-id="8d31f-233">登入之後，瀏覽過**使用者管理**並移過**使用者**。</span><span class="sxs-lookup"><span data-stu-id="8d31f-233">After logging in, navigate too**User Management** and go too**Users**.</span></span>

    <span data-ttu-id="8d31f-234">![使用者](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="8d31f-234">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "Users")</span></span>

3. <span data-ttu-id="8d31f-235">按一下 **+** 圖示和 hello**新增/維護使用者角色** 對話方塊隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="8d31f-235">Click **+**  icon and hello **Add/Maintain User Roles** dialog opens.</span></span>

    <span data-ttu-id="8d31f-236">![使用者](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="8d31f-236">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "Users")</span></span>

    <span data-ttu-id="8d31f-237">![使用者](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="8d31f-237">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "Users")</span></span>

    <span data-ttu-id="8d31f-238">a.</span><span class="sxs-lookup"><span data-stu-id="8d31f-238">a.</span></span> <span data-ttu-id="8d31f-239">在 hello**使用者電子郵件地址**文字方塊中，型別 hello 電子郵件的使用者喜歡BrittaSimon@contoso.com。</span><span class="sxs-lookup"><span data-stu-id="8d31f-239">In hello **User e-mail address** textbox, type hello email of user like BrittaSimon@contoso.com.</span></span>
    
    <span data-ttu-id="8d31f-240">b.</span><span class="sxs-lookup"><span data-stu-id="8d31f-240">b.</span></span> <span data-ttu-id="8d31f-241">在 hello**名字**文字方塊中，例如許使用者類型 hello 第一個名稱。</span><span class="sxs-lookup"><span data-stu-id="8d31f-241">In hello **First name** textbox, type hello First name of user like Britta.</span></span>

    <span data-ttu-id="8d31f-242">c.</span><span class="sxs-lookup"><span data-stu-id="8d31f-242">c.</span></span> <span data-ttu-id="8d31f-243">在 hello**姓氏**文字方塊中，型別 hello 最後一個名稱類似 Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="8d31f-243">In hello **Last name** textbox, type hello Last name of user like Simon.</span></span>
    
    <span data-ttu-id="8d31f-244">d.</span><span class="sxs-lookup"><span data-stu-id="8d31f-244">d.</span></span> <span data-ttu-id="8d31f-245">輸入 hello 使用者**同盟識別碼**。</span><span class="sxs-lookup"><span data-stu-id="8d31f-245">Enter hello user's **Federation ID**.</span></span> <span data-ttu-id="8d31f-246">每位使用者必須是唯一識別 hello 使用者 hello 帳戶內的同盟識別碼。</span><span class="sxs-lookup"><span data-stu-id="8d31f-246">Each user must have a Federation ID that uniquely identifies hello user within hello account.</span></span>
    
    <span data-ttu-id="8d31f-247">e.</span><span class="sxs-lookup"><span data-stu-id="8d31f-247">e.</span></span> <span data-ttu-id="8d31f-248">指派 hello**標準使用者**角色 toohello 使用者。</span><span class="sxs-lookup"><span data-stu-id="8d31f-248">Assign hello **Standard User** role toohello user.</span></span> <span data-ttu-id="8d31f-249">請勿指派 hello 系統管理員角色，因為這樣會使他一般氣氛存取權限，以及單一登入存取。</span><span class="sxs-lookup"><span data-stu-id="8d31f-249">Do not assign hello Administrator role because that would give him normal Atmosphere access as well as single sign-on access.</span></span>
    
    <span data-ttu-id="8d31f-250">f.</span><span class="sxs-lookup"><span data-stu-id="8d31f-250">f.</span></span> <span data-ttu-id="8d31f-251">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="8d31f-251">Click **OK**.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="8d31f-252">hello 使用者不會收到歡迎畫面的通知電子郵件包含可能是使用的 toolog toohello atomsphere 租用戶帳戶中，因為密碼透過 hello 身分識別提供者管理的密碼。</span><span class="sxs-lookup"><span data-stu-id="8d31f-252">hello user will not receive a welcome notification email containing a password that can be used toolog in toohello AtomSphere account because his password is managed through hello identity provider.</span></span> <span data-ttu-id="8d31f-253">您可以使用任何其他 Boomi 使用者帳戶建立工具或 Api 提供 Boomi tooprovision AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="8d31f-253">You may use any other Boomi user account creation tools or APIs provided by Boomi tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8d31f-254">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="8d31f-254">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8d31f-255">在本節中，您可以授與存取 tooBoomi 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8d31f-255">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBoomi.</span></span>

![指派使用者][200] 

<span data-ttu-id="8d31f-257">**tooassign 許 Simon tooBoomi，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="8d31f-257">**tooassign Britta Simon tooBoomi, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d31f-258">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="8d31f-258">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="8d31f-260">在 [hello] 應用程式清單中，選取**Boomi**。</span><span class="sxs-lookup"><span data-stu-id="8d31f-260">In hello applications list, select **Boomi**.</span></span>

    ![設定單一登入](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_app.png) 

3. <span data-ttu-id="8d31f-262">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="8d31f-262">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="8d31f-264">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8d31f-264">Click **Add** button.</span></span> <span data-ttu-id="8d31f-265">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="8d31f-265">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="8d31f-267">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="8d31f-267">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8d31f-268">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8d31f-268">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8d31f-269">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8d31f-269">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8d31f-270">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="8d31f-270">Testing single sign-on</span></span>

<span data-ttu-id="8d31f-271">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="8d31f-271">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8d31f-272">當您按一下 hello Boomi 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Boomi 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="8d31f-272">When you click hello Boomi tile in hello Access Panel, you should get automatically signed-on tooyour Boomi application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8d31f-273">其他資源</span><span class="sxs-lookup"><span data-stu-id="8d31f-273">Additional resources</span></span>

* [<span data-ttu-id="8d31f-274">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8d31f-274">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8d31f-275">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="8d31f-275">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_203.png

