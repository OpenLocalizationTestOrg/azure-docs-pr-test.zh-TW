---
title: "教學課程：Azure Active Directory 與 Druva 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Druva 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ab92b600-1fea-4905-b1c7-ef8e4d8c495c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: a1c36c06d6d005e0aa363fbf34efe630e4cca1ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-druva"></a><span data-ttu-id="b7504-103">教學課程：Azure Active Directory 與 Druva 整合</span><span class="sxs-lookup"><span data-stu-id="b7504-103">Tutorial: Azure Active Directory integration with Druva</span></span>

<span data-ttu-id="b7504-104">在此教學課程中，您學會如何 toointegrate Druva 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="b7504-104">In this tutorial, you learn how toointegrate Druva with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b7504-105">與 Azure AD 整合 Druva 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="b7504-105">Integrating Druva with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b7504-106">您可以控制存取 tooDruva Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="b7504-106">You can control in Azure AD who has access tooDruva.</span></span>
- <span data-ttu-id="b7504-107">您可以啟用您的使用者 tooautomatically get 登入 tooDruva （單一登入） 具有其 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="b7504-107">You can enable your users tooautomatically get signed-on tooDruva (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="b7504-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="b7504-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="b7504-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="b7504-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b7504-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="b7504-110">Prerequisites</span></span>

<span data-ttu-id="b7504-111">tooconfigure 與 Druva 的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="b7504-111">tooconfigure Azure AD integration with Druva, you need hello following items:</span></span>

- <span data-ttu-id="b7504-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b7504-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b7504-113">已啟用 Druva 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b7504-113">A Druva single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b7504-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="b7504-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b7504-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="b7504-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b7504-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="b7504-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b7504-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="b7504-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b7504-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="b7504-118">Scenario description</span></span>
<span data-ttu-id="b7504-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b7504-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b7504-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="b7504-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b7504-121">從 hello 圖庫加入 Druva</span><span class="sxs-lookup"><span data-stu-id="b7504-121">Adding Druva from hello gallery</span></span>
2. <span data-ttu-id="b7504-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b7504-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-druva-from-hello-gallery"></a><span data-ttu-id="b7504-123">從 hello 圖庫加入 Druva</span><span class="sxs-lookup"><span data-stu-id="b7504-123">Adding Druva from hello gallery</span></span>
<span data-ttu-id="b7504-124">tooconfigure hello 整合 Druva 的 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Druva。</span><span class="sxs-lookup"><span data-stu-id="b7504-124">tooconfigure hello integration of Druva into Azure AD, you need tooadd Druva from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b7504-125">**tooadd Druva 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b7504-125">**tooadd Druva from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b7504-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="b7504-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 按鈕][1]

2. <span data-ttu-id="b7504-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="b7504-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b7504-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="b7504-129">Then go too**All applications**.</span></span>

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. <span data-ttu-id="b7504-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="b7504-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 新應用程式按鈕][3]

4. <span data-ttu-id="b7504-133">在 hello 搜尋方塊中，輸入**Druva**，選取**Druva**然後按一下 從結果面板**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b7504-133">In hello search box, type **Druva**, select **Druva** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Druva hello [結果] 清單中](./media/active-directory-saas-druva-tutorial/tutorial_druva_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b7504-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b7504-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b7504-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Druva 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b7504-136">In this section, you configure and test Azure AD single sign-on with Druva based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b7504-137">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 Druva 中是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="b7504-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Druva is tooa user in Azure AD.</span></span> <span data-ttu-id="b7504-138">換句話說，Azure AD 使用者與 hello Druva 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="b7504-138">In other words, a link relationship between an Azure AD user and hello related user in Druva needs toobe established.</span></span>

<span data-ttu-id="b7504-139">在 Druva 中，將指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="b7504-139">In Druva, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b7504-140">tooconfigure 及測試 Azure AD 單一登入 Druva，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="b7504-140">tooconfigure and test Azure AD single sign-on with Druva, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b7504-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="b7504-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b7504-142">**[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="b7504-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b7504-143">**[建立測試使用者 Druva](#create-a-druva-test-user)**  -toohave 許 Simon Druva 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="b7504-143">**[Create a Druva test user](#create-a-druva-test-user)** - toohave a counterpart of Britta Simon in Druva that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b7504-144">**[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b7504-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b7504-145">**[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="b7504-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b7504-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b7504-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b7504-147">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Druva 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="b7504-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Druva application.</span></span>

<span data-ttu-id="b7504-148">**tooconfigure Azure AD 單一登入 Druva，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b7504-148">**tooconfigure Azure AD single sign-on with Druva, perform hello following steps:**</span></span>

1. <span data-ttu-id="b7504-149">在 Azure 入口網站上 hello hello **Druva**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="b7504-149">In hello Azure portal, on hello **Druva** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="b7504-151">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b7504-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-druva-tutorial/tutorial_druva_samlbase.png)

3. <span data-ttu-id="b7504-153">在 hello **Druva 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="b7504-153">On hello **Druva Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-druva-tutorial/tutorial_druva_url.png)

    <span data-ttu-id="b7504-155">在 hello**登入 URL**文字方塊中，型別 hello URL:`https://cloud.druva.com/home`</span><span class="sxs-lookup"><span data-stu-id="b7504-155">In hello **Sign-on URL** textbox, type hello URL: `https://cloud.druva.com/home`</span></span>

4. <span data-ttu-id="b7504-156">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="b7504-156">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![hello 憑證下載連結](./media/active-directory-saas-druva-tutorial/tutorial_druva_certificate.png) 

5. <span data-ttu-id="b7504-158">您的 Druva 應用程式需要以特定格式，這需要您 tooadd 自訂屬性對應 tooyour hello SAML 判斷提示**SAML 權杖屬性**組態。</span><span class="sxs-lookup"><span data-stu-id="b7504-158">Your Druva application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **SAML Token Attributes** configuration.</span></span> 

    ![設定單一登入](./media/active-directory-saas-druva-tutorial/tutorial_druva_attribute.png)

6. <span data-ttu-id="b7504-160">在 hello**使用者屬性**hello 區段**單一登入** 對話方塊中，hello 上述影像中所示設定 SAML 權杖屬性和執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="b7504-160">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello preceding image and perform hello following steps:</span></span>

    | <span data-ttu-id="b7504-161">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="b7504-161">Attribute Name</span></span>      | <span data-ttu-id="b7504-162">屬性值</span><span class="sxs-lookup"><span data-stu-id="b7504-162">Attribute Value</span></span>      |
    | ------------------- | -------------------- |
    | <span data-ttu-id="b7504-163">insync\_auth\_token</span><span class="sxs-lookup"><span data-stu-id="b7504-163">insync\_auth\_token</span></span> |<span data-ttu-id="b7504-164">輸入 hello 權杖產生的值</span><span class="sxs-lookup"><span data-stu-id="b7504-164">Enter hello token generated value</span></span> |
    
    <span data-ttu-id="b7504-165">a.</span><span class="sxs-lookup"><span data-stu-id="b7504-165">a.</span></span> <span data-ttu-id="b7504-166">按一下**加入屬性**tooopen hello**加入屬性**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="b7504-166">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-druva-tutorial/tutorial_attribute_04.png)
    
    ![設定單一登入](./media/active-directory-saas-druva-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="b7504-169">b.</span><span class="sxs-lookup"><span data-stu-id="b7504-169">b.</span></span> <span data-ttu-id="b7504-170">在 hello**名稱**文字方塊中，該資料列所顯示的型別 hello 屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="b7504-170">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="b7504-171">c.</span><span class="sxs-lookup"><span data-stu-id="b7504-171">c.</span></span> <span data-ttu-id="b7504-172">從 hello**值**清單，顯示該資料列的型別 hello 屬性值。</span><span class="sxs-lookup"><span data-stu-id="b7504-172">From hello **Value** list, type hello attribute value shown for that row.</span></span> <span data-ttu-id="b7504-173">稍後在教學課程說明 hello 權杖產生的值。</span><span class="sxs-lookup"><span data-stu-id="b7504-173">hello token generated value is explained later in tutorial.</span></span>
    
    <span data-ttu-id="b7504-174">d.</span><span class="sxs-lookup"><span data-stu-id="b7504-174">d.</span></span> <span data-ttu-id="b7504-175">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="b7504-175">Click **Ok**.</span></span>    

7. <span data-ttu-id="b7504-176">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="b7504-176">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-druva-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="b7504-178">在 hello **Druva 組態**區段中，按一下**設定 Druva** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="b7504-178">On hello **Druva Configuration** section, click **Configure Druva** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b7504-179">複製 hello**登出 URL 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="b7504-179">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-druva-tutorial/tutorial_druva_configure.png) 

9. <span data-ttu-id="b7504-181">在不同的網頁瀏覽器視窗中，系統管理員身分登入 tooyour Druva 公司網站。</span><span class="sxs-lookup"><span data-stu-id="b7504-181">In a different web browser window, log in tooyour Druva company site as an administrator.</span></span>

10. <span data-ttu-id="b7504-182">跳過**管理\>設定**。</span><span class="sxs-lookup"><span data-stu-id="b7504-182">Go too**Manage \> Settings**.</span></span>

    <span data-ttu-id="b7504-183">![設定](./media/active-directory-saas-druva-tutorial/ic795091.png "設定")</span><span class="sxs-lookup"><span data-stu-id="b7504-183">![Settings](./media/active-directory-saas-druva-tutorial/ic795091.png "Settings")</span></span>

11. <span data-ttu-id="b7504-184">在 hello 單一登入設定 對話方塊，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="b7504-184">On hello Single Sign-On Settings dialog, perform hello following steps:</span></span>

    <span data-ttu-id="b7504-185">![單一登入設定](./media/active-directory-saas-druva-tutorial/ic795092.png "單一登入設定")</span><span class="sxs-lookup"><span data-stu-id="b7504-185">![Single Sign-On Settings](./media/active-directory-saas-druva-tutorial/ic795092.png "Single Sign-On Settings")</span></span>
    
    <span data-ttu-id="b7504-186">a.</span><span class="sxs-lookup"><span data-stu-id="b7504-186">a.</span></span> <span data-ttu-id="b7504-187">貼上**SAML 單一登入服務 URL**值，您從 hello Azure 入口網站複製到 hello**識別碼提供者登入 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="b7504-187">Paste **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **ID Provider Login URL** textbox.</span></span>
    
    <span data-ttu-id="b7504-188">b.</span><span class="sxs-lookup"><span data-stu-id="b7504-188">b.</span></span> <span data-ttu-id="b7504-189">貼上**登出 URL**值，您從 hello Azure 入口網站複製到 hello **ID 提供者登出 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="b7504-189">Paste **Sign-Out URL** value, which you have copied from hello Azure portal into hello **ID Provider Logout URL** textbox.</span></span>
    
     <span data-ttu-id="b7504-190">c.</span><span class="sxs-lookup"><span data-stu-id="b7504-190">c.</span></span> <span data-ttu-id="b7504-191">在記事本中，複製到剪貼簿，其內容的 hello 中開啟 base-64 編碼的憑證，然後將它貼入 toohello **ID 提供者憑證**文字方塊</span><span class="sxs-lookup"><span data-stu-id="b7504-191">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **ID Provider Certificate** textbox</span></span>
     
     <span data-ttu-id="b7504-192">d.</span><span class="sxs-lookup"><span data-stu-id="b7504-192">d.</span></span> <span data-ttu-id="b7504-193">tooopen hello**設定**頁面上，按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="b7504-193">tooopen hello **Settings** page, click **Save**.</span></span>

12. <span data-ttu-id="b7504-194">在 hello**設定**頁面上，按一下**產生 SSO 語彙基元**。</span><span class="sxs-lookup"><span data-stu-id="b7504-194">On hello **Settings** page, click **Generate SSO Token**.</span></span>

    <span data-ttu-id="b7504-195">![設定](./media/active-directory-saas-druva-tutorial/ic795093.png "設定")</span><span class="sxs-lookup"><span data-stu-id="b7504-195">![Settings](./media/active-directory-saas-druva-tutorial/ic795093.png "Settings")</span></span>

13. <span data-ttu-id="b7504-196">在 [hello**單一登入驗證語彙基元**] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="b7504-196">On hello **Single Sign-on Authentication Token** dialog, perform hello following steps:</span></span>

    <span data-ttu-id="b7504-197">![SSO 權杖](./media/active-directory-saas-druva-tutorial/ic795094.png "SSO 權杖")</span><span class="sxs-lookup"><span data-stu-id="b7504-197">![SSO Token](./media/active-directory-saas-druva-tutorial/ic795094.png "SSO Token")</span></span>
    
    <span data-ttu-id="b7504-198">a.</span><span class="sxs-lookup"><span data-stu-id="b7504-198">a.</span></span> <span data-ttu-id="b7504-199">按一下**複製**，貼上複製值在 hello**值** 文字方塊中 hello**加入屬性**> 一節。</span><span class="sxs-lookup"><span data-stu-id="b7504-199">Click **Copy**, Paste copied value in hello **Value** textbox in hello **Add Attribute** section.</span></span>
    
    <span data-ttu-id="b7504-200">b.</span><span class="sxs-lookup"><span data-stu-id="b7504-200">b.</span></span> <span data-ttu-id="b7504-201">按一下 [關閉] 。</span><span class="sxs-lookup"><span data-stu-id="b7504-201">Click **Close**.</span></span>

> [!TIP]
> <span data-ttu-id="b7504-202">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="b7504-202">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b7504-203">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="b7504-203">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b7504-204">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b7504-204">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b7504-205">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b7504-205">Create an Azure AD test user</span></span>

<span data-ttu-id="b7504-206">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="b7504-206">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="b7504-208">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b7504-208">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b7504-209">在 hello Azure 入口網站，hello 左窗格中，按一下 hello **Azure Active Directory**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="b7504-209">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-druva-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="b7504-211">toodisplay hello 使用者清單，請移過**使用者和群組**，然後按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="b7504-211">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-druva-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="b7504-213">tooopen hello**使用者**對話方塊中，按一下 [**新增**頂端的 hello hello**所有使用者**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="b7504-213">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello [新增] 按鈕](./media/active-directory-saas-druva-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="b7504-215">在 hello**使用者**對話方塊方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="b7504-215">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello [使用者] 對話方塊](./media/active-directory-saas-druva-tutorial/create_aaduser_04.png)

    <span data-ttu-id="b7504-217">a.</span><span class="sxs-lookup"><span data-stu-id="b7504-217">a.</span></span> <span data-ttu-id="b7504-218">在 hello**名稱**方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="b7504-218">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b7504-219">b.</span><span class="sxs-lookup"><span data-stu-id="b7504-219">b.</span></span> <span data-ttu-id="b7504-220">在 hello**使用者名**方塊中，使用者許 Simon 類型 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="b7504-220">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="b7504-221">c.</span><span class="sxs-lookup"><span data-stu-id="b7504-221">c.</span></span> <span data-ttu-id="b7504-222">選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 hello**密碼**方塊。</span><span class="sxs-lookup"><span data-stu-id="b7504-222">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="b7504-223">d.</span><span class="sxs-lookup"><span data-stu-id="b7504-223">d.</span></span> <span data-ttu-id="b7504-224">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="b7504-224">Click **Create**.</span></span>
 
### <a name="create-a-druva-test-user"></a><span data-ttu-id="b7504-225">建立 Druva 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b7504-225">Create a Druva test user</span></span>

<span data-ttu-id="b7504-226">在訂單 tooenable Azure AD 使用者 toolog tooDruva 中，您必須是佈建到 Druva。</span><span class="sxs-lookup"><span data-stu-id="b7504-226">In order tooenable Azure AD users toolog in tooDruva, they must be provisioned into Druva.</span></span> <span data-ttu-id="b7504-227">在 Druva 的 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="b7504-227">In hello case of Druva, provisioning is a manual task.</span></span>

<span data-ttu-id="b7504-228">**tooconfigure 使用者佈建，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b7504-228">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="b7504-229">登入 tooyour **Druva**以系統管理員身分的公司網站。</span><span class="sxs-lookup"><span data-stu-id="b7504-229">Log in tooyour **Druva** company site as administrator.</span></span>

2. <span data-ttu-id="b7504-230">跳過**管理\>使用者**。</span><span class="sxs-lookup"><span data-stu-id="b7504-230">Go too**Manage \> Users**.</span></span>
   
   <span data-ttu-id="b7504-231">![管理使用者](./media/active-directory-saas-druva-tutorial/ic795097.png "管理使用者")</span><span class="sxs-lookup"><span data-stu-id="b7504-231">![Manage Users](./media/active-directory-saas-druva-tutorial/ic795097.png "Manage Users")</span></span>

3. <span data-ttu-id="b7504-232">按一下 [新建] 。</span><span class="sxs-lookup"><span data-stu-id="b7504-232">Click **Create New**.</span></span>
   
   <span data-ttu-id="b7504-233">![管理使用者](./media/active-directory-saas-druva-tutorial/ic795098.png "管理使用者")</span><span class="sxs-lookup"><span data-stu-id="b7504-233">![Manage Users](./media/active-directory-saas-druva-tutorial/ic795098.png "Manage Users")</span></span>

4. <span data-ttu-id="b7504-234">Hello 建立新的使用者在對話方塊上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="b7504-234">On hello Create New User dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="b7504-235">![建立新的使用者](./media/active-directory-saas-druva-tutorial/ic795099.png "建立新的使用者")</span><span class="sxs-lookup"><span data-stu-id="b7504-235">![Create NewUser](./media/active-directory-saas-druva-tutorial/ic795099.png "Create NewUser")</span></span>
   
   <span data-ttu-id="b7504-236">a.</span><span class="sxs-lookup"><span data-stu-id="b7504-236">a.</span></span> <span data-ttu-id="b7504-237">在 hello**電子郵件地址**文字方塊中，輸入 hello 電子郵件的使用者，例如 **brittasimon@contoso.com** 。</span><span class="sxs-lookup"><span data-stu-id="b7504-237">In hello **Email address** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>
   
   <span data-ttu-id="b7504-238">b.</span><span class="sxs-lookup"><span data-stu-id="b7504-238">b.</span></span> <span data-ttu-id="b7504-239">在 hello**名稱**文字方塊中，輸入 hello 類似的使用者名稱**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="b7504-239">In hello **Name** textbox, enter hello name of user like **BrittaSimon**.</span></span>
   
   <span data-ttu-id="b7504-240">c.</span><span class="sxs-lookup"><span data-stu-id="b7504-240">c.</span></span> <span data-ttu-id="b7504-241">按一下 [建立使用者] 。</span><span class="sxs-lookup"><span data-stu-id="b7504-241">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="b7504-242">您可以使用任何其他 Druva 使用者帳戶建立工具或 Api 提供 Druva tooprovision Azure AD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="b7504-242">You can use any other Druva user account creation tools or APIs provided by Druva tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="b7504-243">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b7504-243">Assign hello Azure AD test user</span></span>

<span data-ttu-id="b7504-244">在本節中，您可以授與存取 tooDruva 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b7504-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDruva.</span></span>

![指派 hello 使用者角色][200] 

<span data-ttu-id="b7504-246">**tooassign 許 Simon tooDruva，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b7504-246">**tooassign Britta Simon tooDruva, perform hello following steps:**</span></span>

1. <span data-ttu-id="b7504-247">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="b7504-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="b7504-249">在 [hello] 應用程式清單中，選取**Druva**。</span><span class="sxs-lookup"><span data-stu-id="b7504-249">In hello applications list, select **Druva**.</span></span>

    ![hello 應用程式清單中的 hello Druva 連結](./media/active-directory-saas-druva-tutorial/tutorial_druva_app.png)  

3. <span data-ttu-id="b7504-251">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="b7504-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello 「 使用者和群組 」 的連結][202]

4. <span data-ttu-id="b7504-253">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b7504-253">Click **Add** button.</span></span> <span data-ttu-id="b7504-254">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="b7504-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 將作業加入窗格][203]

5. <span data-ttu-id="b7504-256">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="b7504-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b7504-257">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b7504-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b7504-258">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b7504-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b7504-259">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="b7504-259">Test single sign-on</span></span>

<span data-ttu-id="b7504-260">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="b7504-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b7504-261">當您按一下 hello Druva 磚 hello 存取面板中的時，您應該取得 tooyour 自動登入 Druva 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b7504-261">When you click hello Druva tile in hello Access Panel, you should get automatically signed-on tooyour Druva application.</span></span>
<span data-ttu-id="b7504-262">如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="b7504-262">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b7504-263">其他資源</span><span class="sxs-lookup"><span data-stu-id="b7504-263">Additional resources</span></span>

* [<span data-ttu-id="b7504-264">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b7504-264">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b7504-265">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="b7504-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-druva-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-druva-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-druva-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-druva-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-druva-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-druva-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-druva-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-druva-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-druva-tutorial/tutorial_general_203.png

