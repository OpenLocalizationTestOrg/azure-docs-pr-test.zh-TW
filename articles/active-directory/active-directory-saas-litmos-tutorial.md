---
title: "教學課程：Azure Active Directory 與 Litmos 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Litmos 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: jeedes
ms.assetid: cfaae4bb-e8e5-41d1-ac88-8cc369653036
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 026fd10058760f2d63d185ef4aa9d7de3b82525e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-litmos"></a><span data-ttu-id="a1a26-103">教學課程：Azure Active Directory 與 Litmos 整合</span><span class="sxs-lookup"><span data-stu-id="a1a26-103">Tutorial: Azure Active Directory integration with Litmos</span></span>

<span data-ttu-id="a1a26-104">在此教學課程中，您學會如何 toointegrate Litmos 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="a1a26-104">In this tutorial, you learn how toointegrate Litmos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a1a26-105">與 Azure AD 整合 Litmos 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="a1a26-105">Integrating Litmos with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a1a26-106">您可以控制存取 tooLitmos Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="a1a26-106">You can control in Azure AD who has access tooLitmos.</span></span>
- <span data-ttu-id="a1a26-107">您可以啟用您的使用者 tooautomatically get 登入 tooLitmos （單一登入） 具有其 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a1a26-107">You can enable your users tooautomatically get signed-on tooLitmos (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="a1a26-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="a1a26-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="a1a26-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="a1a26-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a1a26-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="a1a26-110">Prerequisites</span></span>

<span data-ttu-id="a1a26-111">tooconfigure Litmos 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="a1a26-111">tooconfigure Azure AD integration with Litmos, you need hello following items:</span></span>

- <span data-ttu-id="a1a26-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a1a26-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a1a26-113">啟用 Litmos 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a1a26-113">A Litmos single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a1a26-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="a1a26-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a1a26-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="a1a26-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a1a26-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="a1a26-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a1a26-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="a1a26-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a1a26-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="a1a26-118">Scenario description</span></span>
<span data-ttu-id="a1a26-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a1a26-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a1a26-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="a1a26-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a1a26-121">從 hello 圖庫加入 Litmos</span><span class="sxs-lookup"><span data-stu-id="a1a26-121">Adding Litmos from hello gallery</span></span>
2. <span data-ttu-id="a1a26-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a1a26-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-litmos-from-hello-gallery"></a><span data-ttu-id="a1a26-123">從 hello 圖庫加入 Litmos</span><span class="sxs-lookup"><span data-stu-id="a1a26-123">Adding Litmos from hello gallery</span></span>
<span data-ttu-id="a1a26-124">tooconfigure hello 整合 Litmos 到 Azure AD，您需要 tooadd Litmos hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a1a26-124">tooconfigure hello integration of Litmos into Azure AD, you need tooadd Litmos from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a1a26-125">**tooadd Litmos 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a1a26-125">**tooadd Litmos from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a1a26-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="a1a26-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 按鈕][1]

2. <span data-ttu-id="a1a26-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a1a26-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a1a26-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a1a26-129">Then go too**All applications**.</span></span>

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. <span data-ttu-id="a1a26-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="a1a26-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 新應用程式按鈕][3]

4. <span data-ttu-id="a1a26-133">在 hello 搜尋方塊中，輸入**Litmos**，選取**Litmos**然後按一下 從結果面板**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a1a26-133">In hello search box, type **Litmos**, select **Litmos** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Litmos hello [結果] 清單中](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a1a26-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a1a26-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="a1a26-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Litmos 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a1a26-136">In this section, you configure and test Azure AD single sign-on with Litmos based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a1a26-137">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Litmos 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="a1a26-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Litmos is tooa user in Azure AD.</span></span> <span data-ttu-id="a1a26-138">換句話說，Azure AD 使用者與 hello Litmos 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="a1a26-138">In other words, a link relationship between an Azure AD user and hello related user in Litmos needs toobe established.</span></span>

<span data-ttu-id="a1a26-139">Litmos 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="a1a26-139">In Litmos, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a1a26-140">tooconfigure 及 Litmos 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="a1a26-140">tooconfigure and test Azure AD single sign-on with Litmos, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a1a26-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="a1a26-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a1a26-142">**[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="a1a26-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a1a26-143">**[建立測試使用者 Litmos](#create-a-litmos-test-user)**  -toohave 許 Simon Litmos 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="a1a26-143">**[Create a Litmos test user](#create-a-litmos-test-user)** - toohave a counterpart of Britta Simon in Litmos that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a1a26-144">**[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a1a26-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a1a26-145">**[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="a1a26-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a1a26-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a1a26-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a1a26-147">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Litmos 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="a1a26-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Litmos application.</span></span>

<span data-ttu-id="a1a26-148">**tooconfigure Azure AD 單一登入與 Litmos，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a1a26-148">**tooconfigure Azure AD single sign-on with Litmos, perform hello following steps:**</span></span>

1. <span data-ttu-id="a1a26-149">在 Azure 入口網站上 hello hello **Litmos**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="a1a26-149">In hello Azure portal, on hello **Litmos** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="a1a26-151">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a1a26-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_samlbase.png)

3. <span data-ttu-id="a1a26-153">在 hello **Litmos 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a1a26-153">On hello **Litmos Domain and URLs** section, perform hello following steps:</span></span>

    ![Litmos 網域及 URL 單一登入資訊](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_url.png)

    <span data-ttu-id="a1a26-155">a.</span><span class="sxs-lookup"><span data-stu-id="a1a26-155">a.</span></span> <span data-ttu-id="a1a26-156">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.litmos.com/account/Login`</span><span class="sxs-lookup"><span data-stu-id="a1a26-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.litmos.com/account/Login`</span></span>

    <span data-ttu-id="a1a26-157">b.</span><span class="sxs-lookup"><span data-stu-id="a1a26-157">b.</span></span> <span data-ttu-id="a1a26-158">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.litmos.com/integration/samllogin`</span><span class="sxs-lookup"><span data-stu-id="a1a26-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.litmos.com/integration/samllogin`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a1a26-159">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="a1a26-159">These values are not real.</span></span> <span data-ttu-id="a1a26-160">這些值以 hello 實際識別項和回覆 URL 更新，稍後在教學課程中或連絡說明[Litmos 支援小組](https://www.litmos.com/contact-us/)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="a1a26-160">Update these values with hello actual Identifier and Reply URL, which are explained later in tutorial or contact [Litmos support team](https://www.litmos.com/contact-us/) tooget these values.</span></span>

4. <span data-ttu-id="a1a26-161">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="a1a26-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![hello 憑證下載連結](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_certificate.png)

5. <span data-ttu-id="a1a26-163">Hello 組態的一部分，您需要 toocustomize hello **SAML 權杖屬性**Litmos 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a1a26-163">As part of hello configuration, you need toocustomize hello **SAML Token Attributes** for your Litmos application.</span></span>

    ![屬性區段](./media/active-directory-saas-litmos-tutorial/tutorial_attribute.png)
           
    | <span data-ttu-id="a1a26-165">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="a1a26-165">Attribute Name</span></span>   | <span data-ttu-id="a1a26-166">屬性值</span><span class="sxs-lookup"><span data-stu-id="a1a26-166">Attribute Value</span></span> |   
    | ---------------  | ----------------|
    | <span data-ttu-id="a1a26-167">名字</span><span class="sxs-lookup"><span data-stu-id="a1a26-167">FirstName</span></span> |<span data-ttu-id="a1a26-168">user.givenname</span><span class="sxs-lookup"><span data-stu-id="a1a26-168">user.givenname</span></span> |
    | <span data-ttu-id="a1a26-169">姓氏</span><span class="sxs-lookup"><span data-stu-id="a1a26-169">LastName</span></span>  |<span data-ttu-id="a1a26-170">user.surname</span><span class="sxs-lookup"><span data-stu-id="a1a26-170">user.surname</span></span> |
    | <span data-ttu-id="a1a26-171">電子郵件</span><span class="sxs-lookup"><span data-stu-id="a1a26-171">Email</span></span> |<span data-ttu-id="a1a26-172">user.mail</span><span class="sxs-lookup"><span data-stu-id="a1a26-172">user.mail</span></span> |

    <span data-ttu-id="a1a26-173">a.</span><span class="sxs-lookup"><span data-stu-id="a1a26-173">a.</span></span> <span data-ttu-id="a1a26-174">按一下**加入屬性**tooopen hello**加入屬性**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="a1a26-174">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![新增屬性](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_04.png)

    ![新增屬性對話方塊](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="a1a26-177">b.</span><span class="sxs-lookup"><span data-stu-id="a1a26-177">b.</span></span> <span data-ttu-id="a1a26-178">在 hello**名稱**文字方塊中，該資料列所顯示的型別 hello 屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="a1a26-178">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="a1a26-179">c.</span><span class="sxs-lookup"><span data-stu-id="a1a26-179">c.</span></span> <span data-ttu-id="a1a26-180">從 hello**值**清單，顯示該資料列的型別 hello 屬性值。</span><span class="sxs-lookup"><span data-stu-id="a1a26-180">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="a1a26-181">d.</span><span class="sxs-lookup"><span data-stu-id="a1a26-181">d.</span></span> <span data-ttu-id="a1a26-182">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="a1a26-182">Click **Ok**.</span></span>     

6. <span data-ttu-id="a1a26-183">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="a1a26-183">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-litmos-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="a1a26-185">在不同的瀏覽器視窗中，以系統管理員身分登入 tooyour Litmos 公司網站。</span><span class="sxs-lookup"><span data-stu-id="a1a26-185">In a different browser window, sign-on tooyour Litmos company site as administrator.</span></span>

8. <span data-ttu-id="a1a26-186">在 hello hello 左側導覽列中按一下**帳戶**。</span><span class="sxs-lookup"><span data-stu-id="a1a26-186">In hello navigation bar on hello left side, click **Accounts**.</span></span>
   
    ![應用程式端的帳戶區段][22] 

9. <span data-ttu-id="a1a26-188">按一下 hello**整合** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a1a26-188">Click hello **Integrations** tab.</span></span>
   
    ![整合索引標籤][23] 

10. <span data-ttu-id="a1a26-190">在 hello**整合**索引標籤上，向下捲動太**第 3 個合作對象整合**，然後按一下 **SAML 2.0**  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a1a26-190">On hello **Integrations** tab, scroll down too**3rd Party Integrations**, and then click **SAML 2.0** tab.</span></span>
   
    ![SAML 2.0 區段][24] 

11. <span data-ttu-id="a1a26-192">複製下的 hello 值**litmos 是 hello SAML 端點：**並將它貼到 hello**回覆 URL**  文字方塊中 hello **Litmos 網域和 Url** Azure 入口網站中的區段。</span><span class="sxs-lookup"><span data-stu-id="a1a26-192">Copy hello value under **hello SAML endpoint for litmos is:** and paste it into hello **Reply URL** textbox in hello **Litmos Domain and URLs** section in Azure portal.</span></span> 
   
    ![SAML 端點][26] 

12. <span data-ttu-id="a1a26-194">在您**Litmos**應用程式中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a1a26-194">In your **Litmos** application, perform hello following steps:</span></span>
    
     ![Litmos 應用程式][25] 
     
     <span data-ttu-id="a1a26-196">a.</span><span class="sxs-lookup"><span data-stu-id="a1a26-196">a.</span></span> <span data-ttu-id="a1a26-197">按一下 [啟用 SAML] 。</span><span class="sxs-lookup"><span data-stu-id="a1a26-197">Click **Enable SAML**.</span></span>
    
     <span data-ttu-id="a1a26-198">b.</span><span class="sxs-lookup"><span data-stu-id="a1a26-198">b.</span></span> <span data-ttu-id="a1a26-199">在記事本中，複製到剪貼簿，其內容的 hello 中開啟 base-64 編碼的憑證，然後將它貼入 toohello **SAML X.509 憑證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="a1a26-199">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **SAML X.509 Certificate** textbox.</span></span>
     
     <span data-ttu-id="a1a26-200">c.</span><span class="sxs-lookup"><span data-stu-id="a1a26-200">c.</span></span> <span data-ttu-id="a1a26-201">按一下 [儲存變更] 。</span><span class="sxs-lookup"><span data-stu-id="a1a26-201">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="a1a26-202">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="a1a26-202">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a1a26-203">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="a1a26-203">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a1a26-204">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a1a26-204">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a1a26-205">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a1a26-205">Create an Azure AD test user</span></span>

<span data-ttu-id="a1a26-206">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="a1a26-206">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="a1a26-208">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a1a26-208">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a1a26-209">在 hello Azure 入口網站，hello 左窗格中，按一下 hello **Azure Active Directory**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="a1a26-209">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-litmos-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="a1a26-211">toodisplay hello 使用者清單，請移過**使用者和群組**，然後按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="a1a26-211">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-litmos-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="a1a26-213">tooopen hello**使用者**對話方塊中，按一下 [**新增**頂端的 hello hello**所有使用者**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="a1a26-213">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello [新增] 按鈕](./media/active-directory-saas-litmos-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="a1a26-215">在 hello**使用者**對話方塊方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a1a26-215">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello [使用者] 對話方塊](./media/active-directory-saas-litmos-tutorial/create_aaduser_04.png)

    <span data-ttu-id="a1a26-217">a.</span><span class="sxs-lookup"><span data-stu-id="a1a26-217">a.</span></span> <span data-ttu-id="a1a26-218">在 hello**名稱**方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="a1a26-218">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a1a26-219">b.</span><span class="sxs-lookup"><span data-stu-id="a1a26-219">b.</span></span> <span data-ttu-id="a1a26-220">在 hello**使用者名**方塊中，使用者許 Simon 類型 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="a1a26-220">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="a1a26-221">c.</span><span class="sxs-lookup"><span data-stu-id="a1a26-221">c.</span></span> <span data-ttu-id="a1a26-222">選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 hello**密碼**方塊。</span><span class="sxs-lookup"><span data-stu-id="a1a26-222">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="a1a26-223">d.</span><span class="sxs-lookup"><span data-stu-id="a1a26-223">d.</span></span> <span data-ttu-id="a1a26-224">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="a1a26-224">Click **Create**.</span></span>
  
### <a name="create-a-litmos-test-user"></a><span data-ttu-id="a1a26-225">建立 Litmos 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a1a26-225">Create a Litmos test user</span></span>

<span data-ttu-id="a1a26-226">hello 本節目標在於 toocreate Litmos 中呼叫許 Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="a1a26-226">hello objective of this section is toocreate a user called Britta Simon in Litmos.</span></span>  
<span data-ttu-id="a1a26-227">hello Litmos 應用程式支援恰好在時間佈建。</span><span class="sxs-lookup"><span data-stu-id="a1a26-227">hello Litmos application supports Just-in-Time provisioning.</span></span> <span data-ttu-id="a1a26-228">這表示，使用者帳戶會自動建立必要期間嘗試 tooaccess hello 應用程式使用存取面板 hello。</span><span class="sxs-lookup"><span data-stu-id="a1a26-228">This means, a user account is automatically created if necessary during an attempt tooaccess hello application using hello Access Panel.</span></span>

<span data-ttu-id="a1a26-229">**toocreate 呼叫許 Simon Litmos，在使用者執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a1a26-229">**toocreate a user called Britta Simon in Litmos, perform hello following steps:**</span></span>

1. <span data-ttu-id="a1a26-230">在不同的瀏覽器視窗中，以系統管理員身分登入 tooyour Litmos 公司網站。</span><span class="sxs-lookup"><span data-stu-id="a1a26-230">In a different browser window, sign-on tooyour Litmos company site as administrator.</span></span>

2. <span data-ttu-id="a1a26-231">在 hello hello 左側導覽列中按一下**帳戶**。</span><span class="sxs-lookup"><span data-stu-id="a1a26-231">In hello navigation bar on hello left side, click **Accounts**.</span></span>
   
    ![應用程式端的帳戶區段][22] 

3. <span data-ttu-id="a1a26-233">按一下 hello**整合** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a1a26-233">Click hello **Integrations** tab.</span></span>
   
    ![整合索引標籤][23] 

4. <span data-ttu-id="a1a26-235">在 hello**整合**索引標籤上，向下捲動太**第 3 個合作對象整合**，然後按一下 **SAML 2.0**  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a1a26-235">On hello **Integrations** tab, scroll down too**3rd Party Integrations**, and then click **SAML 2.0** tab.</span></span>
   
    ![SAML 2.0][24] 
    
5. <span data-ttu-id="a1a26-237">選取 [自動產生使用者]</span><span class="sxs-lookup"><span data-stu-id="a1a26-237">Select **Autogenerate Users**</span></span>
   
    ![自動產生使用者][27] 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="a1a26-239">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a1a26-239">Assign hello Azure AD test user</span></span>

<span data-ttu-id="a1a26-240">在本節中，您可以授與存取 tooLitmos 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a1a26-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLitmos.</span></span>

![指派 hello 使用者角色][200] 

<span data-ttu-id="a1a26-242">**tooassign 許 Simon tooLitmos，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a1a26-242">**tooassign Britta Simon tooLitmos, perform hello following steps:**</span></span>

1. <span data-ttu-id="a1a26-243">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a1a26-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="a1a26-245">在 [hello] 應用程式清單中，選取**Litmos**。</span><span class="sxs-lookup"><span data-stu-id="a1a26-245">In hello applications list, select **Litmos**.</span></span>

    ![hello 應用程式清單中的 hello Litmos 連結](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_app.png)  

3. <span data-ttu-id="a1a26-247">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="a1a26-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello 「 使用者和群組 」 的連結][202]

4. <span data-ttu-id="a1a26-249">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a1a26-249">Click **Add** button.</span></span> <span data-ttu-id="a1a26-250">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="a1a26-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 將作業加入窗格][203]

5. <span data-ttu-id="a1a26-252">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="a1a26-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a1a26-253">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a1a26-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a1a26-254">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a1a26-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a1a26-255">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="a1a26-255">Test single sign-on</span></span>

<span data-ttu-id="a1a26-256">hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="a1a26-256">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  

<span data-ttu-id="a1a26-257">當您按一下的 hello Litmos 磚 hello 存取面板中時，您應該取得自動登入 tooyour Litmos 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a1a26-257">When you click hello Litmos tile in hello Access Panel, you should get automatically signed-on tooyour Litmos application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a1a26-258">其他資源</span><span class="sxs-lookup"><span data-stu-id="a1a26-258">Additional resources</span></span>

* [<span data-ttu-id="a1a26-259">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a1a26-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a1a26-260">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="a1a26-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_04.png
[21]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_60.png
[22]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_61.png
[23]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_62.png
[24]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_63.png
[25]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_64.png
[26]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_65.png
[27]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_66.png

[100]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_203.png

