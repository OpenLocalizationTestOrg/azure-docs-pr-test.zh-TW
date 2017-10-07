---
title: "教學課程：Azure Active Directory 與 Zoho 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Zoho 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 9874e1f3-ade5-42e7-a700-e08b3731236a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: 5d1c196d3b97babab196f509ea68e7d61523a7e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoho"></a><span data-ttu-id="65717-103">教學課程：Azure Active Directory 與 Zoho 整合</span><span class="sxs-lookup"><span data-stu-id="65717-103">Tutorial: Azure Active Directory integration with Zoho</span></span>

<span data-ttu-id="65717-104">在此教學課程中，您學會如何 toointegrate Zoho 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="65717-104">In this tutorial, you learn how toointegrate Zoho with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="65717-105">與 Azure AD 整合 Zoho 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="65717-105">Integrating Zoho with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="65717-106">您可以控制存取 tooZoho Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="65717-106">You can control in Azure AD who has access tooZoho.</span></span>
- <span data-ttu-id="65717-107">您可以啟用您的使用者 tooautomatically get 登入 tooZoho （單一登入） 具有其 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="65717-107">You can enable your users tooautomatically get signed-on tooZoho (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="65717-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="65717-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="65717-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="65717-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65717-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="65717-110">Prerequisites</span></span>

<span data-ttu-id="65717-111">tooconfigure 與 Zoho 的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="65717-111">tooconfigure Azure AD integration with Zoho, you need hello following items:</span></span>

- <span data-ttu-id="65717-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="65717-112">An Azure AD subscription</span></span>
- <span data-ttu-id="65717-113">已啟用 Zoho 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="65717-113">A Zoho single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="65717-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="65717-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="65717-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="65717-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="65717-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="65717-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="65717-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="65717-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="65717-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="65717-118">Scenario description</span></span>
<span data-ttu-id="65717-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="65717-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="65717-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="65717-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="65717-121">從 hello 圖庫加入 Zoho</span><span class="sxs-lookup"><span data-stu-id="65717-121">Adding Zoho from hello gallery</span></span>
2. <span data-ttu-id="65717-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="65717-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zoho-from-hello-gallery"></a><span data-ttu-id="65717-123">從 hello 圖庫加入 Zoho</span><span class="sxs-lookup"><span data-stu-id="65717-123">Adding Zoho from hello gallery</span></span>
<span data-ttu-id="65717-124">tooconfigure hello 整合 Zoho 到 Azure AD，您需要 tooadd Zoho hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="65717-124">tooconfigure hello integration of Zoho into Azure AD, you need tooadd Zoho from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="65717-125">**tooadd Zoho hello 圖庫中，從執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="65717-125">**tooadd Zoho from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="65717-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="65717-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 按鈕][1]

2. <span data-ttu-id="65717-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="65717-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="65717-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="65717-129">Then go too**All applications**.</span></span>

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. <span data-ttu-id="65717-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="65717-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 新應用程式按鈕][3]

4. <span data-ttu-id="65717-133">在 hello 搜尋方塊中，輸入**Zoho**，選取**Zoho**然後按一下 從結果面板**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="65717-133">In hello search box, type **Zoho**, select **Zoho** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Zoho hello [結果] 清單中](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="65717-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="65717-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="65717-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Zoho 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="65717-136">In this section, you configure and test Azure AD single sign-on with Zoho based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="65717-137">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 Zoho 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="65717-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zoho is tooa user in Azure AD.</span></span> <span data-ttu-id="65717-138">換句話說，Azure AD 使用者與 hello Zoho 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="65717-138">In other words, a link relationship between an Azure AD user and hello related user in Zoho needs toobe established.</span></span>

<span data-ttu-id="65717-139">在 Zoho，將指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="65717-139">In Zoho, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="65717-140">tooconfigure 及測試 Azure AD 單一登入 Zoho，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="65717-140">tooconfigure and test Azure AD single sign-on with Zoho, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="65717-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="65717-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="65717-142">**[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="65717-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="65717-143">**[建立測試使用者 Zoho](#create-a-zoho-test-user)**  -toohave 許 Simon Zoho 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="65717-143">**[Create a Zoho test user](#create-a-zoho-test-user)** - toohave a counterpart of Britta Simon in Zoho that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="65717-144">**[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="65717-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="65717-145">**[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="65717-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="65717-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="65717-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="65717-147">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Zoho 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="65717-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zoho application.</span></span>

<span data-ttu-id="65717-148">**tooconfigure Azure AD 單一登入 Zoho，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="65717-148">**tooconfigure Azure AD single sign-on with Zoho, perform hello following steps:**</span></span>

1. <span data-ttu-id="65717-149">在 Azure 入口網站上 hello hello **Zoho**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="65717-149">In hello Azure portal, on hello **Zoho** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="65717-151">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="65717-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_samlbase.png)

3. <span data-ttu-id="65717-153">在 hello **Zoho 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="65717-153">On hello **Zoho Domain and URLs** section, perform hello following steps:</span></span>

    ![Zoho 網域與 URL 單一登入資訊](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_url.png)

    <span data-ttu-id="65717-155">a.</span><span class="sxs-lookup"><span data-stu-id="65717-155">a.</span></span> <span data-ttu-id="65717-156">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<company name>.zohomail.com`</span><span class="sxs-lookup"><span data-stu-id="65717-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.zohomail.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="65717-157">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="65717-157">This value is not real.</span></span> <span data-ttu-id="65717-158">更新此值以 hello 實際的登入 URL。</span><span class="sxs-lookup"><span data-stu-id="65717-158">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="65717-159">請連絡[Zoho 用戶端支援小組](https://www.zoho.com/mail/contact.html)tooget 此值。</span><span class="sxs-lookup"><span data-stu-id="65717-159">Contact [Zoho Client support team](https://www.zoho.com/mail/contact.html) tooget this value.</span></span> 
 
4. <span data-ttu-id="65717-160">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="65717-160">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![hello 憑證下載連結](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_certificate.png) 

5. <span data-ttu-id="65717-162">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="65717-162">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="65717-164">在 hello **Zoho 組態**區段中，按一下**設定 Zoho** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="65717-164">On hello **Zoho Configuration** section, click **Configure Zoho** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="65717-165">複製 hello**登出 URL、 變更密碼 URL 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="65717-165">Copy hello **Sign-Out URL, Change Password URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Zoho 組態](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_configure.png) 

7. <span data-ttu-id="65717-167">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 Zoho Mail 公司網站。</span><span class="sxs-lookup"><span data-stu-id="65717-167">In a different web browser window, log into your Zoho Mail company site as an administrator.</span></span>

8. <span data-ttu-id="65717-168">移 toohello**控制台**。</span><span class="sxs-lookup"><span data-stu-id="65717-168">Go toohello **Control panel**.</span></span>
   
    <span data-ttu-id="65717-169">![控制台](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "控制台")</span><span class="sxs-lookup"><span data-stu-id="65717-169">![Control Panel](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "Control Panel")</span></span>

9. <span data-ttu-id="65717-170">按一下 hello **SAML 驗證** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="65717-170">Click hello **SAML Authentication** tab.</span></span>
   
    <span data-ttu-id="65717-171">![SAML 驗證](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "SAML 驗證")</span><span class="sxs-lookup"><span data-stu-id="65717-171">![SAML Authentication](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "SAML Authentication")</span></span>

10. <span data-ttu-id="65717-172">在 hello **SAML 驗證詳細資料**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="65717-172">In hello **SAML Authentication Details** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="65717-173">![SAML 驗證詳細資料](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "SAML 驗證詳細資料")</span><span class="sxs-lookup"><span data-stu-id="65717-173">![SAML Authentication Details](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "SAML Authentication Details")</span></span>
   
    <span data-ttu-id="65717-174">a.</span><span class="sxs-lookup"><span data-stu-id="65717-174">a.</span></span> <span data-ttu-id="65717-175">在 hello**登入 URL**文字方塊中，貼上**SAML 單一登入服務 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="65717-175">In hello **Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="65717-176">b.</span><span class="sxs-lookup"><span data-stu-id="65717-176">b.</span></span> <span data-ttu-id="65717-177">在 hello**登出 URL**文字方塊中，貼上**登出 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="65717-177">In hello **Logout URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="65717-178">c.</span><span class="sxs-lookup"><span data-stu-id="65717-178">c.</span></span> <span data-ttu-id="65717-179">在 hello**變更密碼 URL**文字方塊中，貼上**變更密碼 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="65717-179">In hello **Change Password URL** textbox, paste **Change Password URL** which you have copied from Azure portal.</span></span>
       
    <span data-ttu-id="65717-180">d.</span><span class="sxs-lookup"><span data-stu-id="65717-180">d.</span></span> <span data-ttu-id="65717-181">開啟您從 [記事本]，複製到剪貼簿，其內容的 hello Azure 入口網站下載的 base-64 編碼的憑證，然後將它貼入 toohello **PublicKey**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="65717-181">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **PublicKey** textbox.</span></span>
   
    <span data-ttu-id="65717-182">e.</span><span class="sxs-lookup"><span data-stu-id="65717-182">e.</span></span> <span data-ttu-id="65717-183">選取 [RSA] 做為 [演算法]。</span><span class="sxs-lookup"><span data-stu-id="65717-183">As **Algorithm**, select **RSA**.</span></span>
   
    <span data-ttu-id="65717-184">f.</span><span class="sxs-lookup"><span data-stu-id="65717-184">f.</span></span> <span data-ttu-id="65717-185">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="65717-185">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="65717-186">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="65717-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="65717-187">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="65717-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="65717-188">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="65717-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="65717-189">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="65717-189">Create an Azure AD test user</span></span>

<span data-ttu-id="65717-190">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="65717-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="65717-192">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="65717-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="65717-193">在 hello Azure 入口網站，hello 左窗格中，按一下 hello **Azure Active Directory**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="65717-193">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="65717-195">toodisplay hello 使用者清單，請移過**使用者和群組**，然後按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="65717-195">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="65717-197">tooopen hello**使用者**對話方塊中，按一下 [**新增**頂端的 hello hello**所有使用者**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="65717-197">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello [新增] 按鈕](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="65717-199">在 hello**使用者**對話方塊方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="65717-199">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello [使用者] 對話方塊](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_04.png)

    <span data-ttu-id="65717-201">a.</span><span class="sxs-lookup"><span data-stu-id="65717-201">a.</span></span> <span data-ttu-id="65717-202">在 hello**名稱**方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="65717-202">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="65717-203">b.</span><span class="sxs-lookup"><span data-stu-id="65717-203">b.</span></span> <span data-ttu-id="65717-204">在 hello**使用者名**方塊中，使用者許 Simon 類型 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="65717-204">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="65717-205">c.</span><span class="sxs-lookup"><span data-stu-id="65717-205">c.</span></span> <span data-ttu-id="65717-206">選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 hello**密碼**方塊。</span><span class="sxs-lookup"><span data-stu-id="65717-206">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="65717-207">d.</span><span class="sxs-lookup"><span data-stu-id="65717-207">d.</span></span> <span data-ttu-id="65717-208">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="65717-208">Click **Create**.</span></span>
 
### <a name="create-a-zoho-test-user"></a><span data-ttu-id="65717-209">建立 Zoho 測試使用者</span><span class="sxs-lookup"><span data-stu-id="65717-209">Create a Zoho test user</span></span>

<span data-ttu-id="65717-210">在訂單 tooenable Azure AD 使用者 toolog 入 Zoho Mail，您必須是佈建到 Zoho Mail。</span><span class="sxs-lookup"><span data-stu-id="65717-210">In order tooenable Azure AD users toolog into Zoho Mail, they must be provisioned into Zoho Mail.</span></span> <span data-ttu-id="65717-211">在 Zoho Mail 的 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="65717-211">In hello case of Zoho Mail, provisioning is a manual task.</span></span>

> [!NOTE]
> <span data-ttu-id="65717-212">您可以使用任何其他 Zoho Mail 使用者帳戶建立工具或 Api 提供 Zoho Mail tooprovision AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="65717-212">You can use any other Zoho Mail user account creation tools or APIs provided by Zoho Mail tooprovision AAD user accounts.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="65717-213">tooprovision 使用者帳戶，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="65717-213">tooprovision a user account, perform hello following steps:</span></span>

1. <span data-ttu-id="65717-214">登入 tooyour **Zoho Mail**系統管理員身分的公司網站。</span><span class="sxs-lookup"><span data-stu-id="65717-214">Log in tooyour **Zoho Mail** company site as an administrator.</span></span>

2. <span data-ttu-id="65717-215">跳過**控制台\>郵件和文件**。</span><span class="sxs-lookup"><span data-stu-id="65717-215">Go too**Control Panel \> Mail & Docs**.</span></span>

3. <span data-ttu-id="65717-216">跳過**使用者詳細資料\>新增使用者**。</span><span class="sxs-lookup"><span data-stu-id="65717-216">Go too**User Details \> Add User**.</span></span>
   
    <span data-ttu-id="65717-217">![新增使用者](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="65717-217">![Add User](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "Add User")</span></span>

4. <span data-ttu-id="65717-218">在 [hello**將使用者新增**] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="65717-218">On hello **Add users** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="65717-219">![新增使用者](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="65717-219">![Add User](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "Add User")</span></span>
   
    <span data-ttu-id="65717-220">a.</span><span class="sxs-lookup"><span data-stu-id="65717-220">a.</span></span> <span data-ttu-id="65717-221">在 hello**名字**文字方塊中，型別 hello 名字，例如使用者的**許**。</span><span class="sxs-lookup"><span data-stu-id="65717-221">In hello **First Name** textbox, type hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="65717-222">b.</span><span class="sxs-lookup"><span data-stu-id="65717-222">b.</span></span> <span data-ttu-id="65717-223">在 hello**姓氏**文字方塊中，型別 hello 姓氏的使用者，例如**Simon**。</span><span class="sxs-lookup"><span data-stu-id="65717-223">In hello **Last Name** textbox, type hello last name of user like **Simon**.</span></span>

    <span data-ttu-id="65717-224">c.</span><span class="sxs-lookup"><span data-stu-id="65717-224">c.</span></span> <span data-ttu-id="65717-225">在 hello**電子郵件識別碼**文字方塊中，例如使用者類型 hello 電子郵件識別碼 **brittasimon@contoso.com** 。</span><span class="sxs-lookup"><span data-stu-id="65717-225">In hello **Email ID** textbox, type hello email id of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="65717-226">d.</span><span class="sxs-lookup"><span data-stu-id="65717-226">d.</span></span> <span data-ttu-id="65717-227">在 hello**密碼**文字方塊中，輸入使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="65717-227">In hello **Password** textbox, enter password of user.</span></span>
   
    <span data-ttu-id="65717-228">e.</span><span class="sxs-lookup"><span data-stu-id="65717-228">e.</span></span> <span data-ttu-id="65717-229">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="65717-229">Click **OK**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="65717-230">hello Azure Active Directory 帳戶持有者將會收到含有連結 tooconfirm hello 帳戶的電子郵件之前就會生效。</span><span class="sxs-lookup"><span data-stu-id="65717-230">hello Azure Active Directory account holder will receive an email with a link tooconfirm hello account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="65717-231">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="65717-231">Assign hello Azure AD test user</span></span>

<span data-ttu-id="65717-232">在本節中，您可以授與存取 tooZoho 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="65717-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZoho.</span></span>

![指派 hello 使用者角色][200] 

<span data-ttu-id="65717-234">**tooassign 許 Simon tooZoho，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="65717-234">**tooassign Britta Simon tooZoho, perform hello following steps:**</span></span>

1. <span data-ttu-id="65717-235">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="65717-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="65717-237">在 [hello] 應用程式清單中，選取**Zoho**。</span><span class="sxs-lookup"><span data-stu-id="65717-237">In hello applications list, select **Zoho**.</span></span>

    ![hello 應用程式清單中的 hello Zoho 連結](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_app.png)  

3. <span data-ttu-id="65717-239">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="65717-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello 「 使用者和群組 」 的連結][202]

4. <span data-ttu-id="65717-241">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="65717-241">Click **Add** button.</span></span> <span data-ttu-id="65717-242">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="65717-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 將作業加入窗格][203]

5. <span data-ttu-id="65717-244">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="65717-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="65717-245">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="65717-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="65717-246">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="65717-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="65717-247">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="65717-247">Test single sign-on</span></span>

<span data-ttu-id="65717-248">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="65717-248">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="65717-249">當您按一下 hello Zoho 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Zoho 應用程式。</span><span class="sxs-lookup"><span data-stu-id="65717-249">When you click hello Zoho tile in hello Access Panel, you should get automatically signed-on tooyour Zoho application.</span></span>
<span data-ttu-id="65717-250">如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="65717-250">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="65717-251">其他資源</span><span class="sxs-lookup"><span data-stu-id="65717-251">Additional resources</span></span>

* [<span data-ttu-id="65717-252">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="65717-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="65717-253">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="65717-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_203.png

