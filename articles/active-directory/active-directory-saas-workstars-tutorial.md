---
title: "教學課程：Azure Active Directory 與 Workstars 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Workstars 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 51a4a4e4-ff60-4971-b3f8-a0367b70d220
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: 86250d7538f058d2a821ded7dda0b2fc185d80df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workstars"></a><span data-ttu-id="6c768-103">教學課程：Azure Active Directory 與 Workstars 整合</span><span class="sxs-lookup"><span data-stu-id="6c768-103">Tutorial: Azure Active Directory integration with Workstars</span></span>

<span data-ttu-id="6c768-104">在此教學課程中，您學會如何 toointegrate Workstars 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="6c768-104">In this tutorial, you learn how toointegrate Workstars with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6c768-105">與 Azure AD 整合 Workstars 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="6c768-105">Integrating Workstars with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6c768-106">您可以控制存取 tooWorkstars Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="6c768-106">You can control in Azure AD who has access tooWorkstars.</span></span>
- <span data-ttu-id="6c768-107">您可以啟用您的使用者 tooautomatically get 登入 tooWorkstars （單一登入） 具有其 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="6c768-107">You can enable your users tooautomatically get signed-on tooWorkstars (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="6c768-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="6c768-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="6c768-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="6c768-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c768-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="6c768-110">Prerequisites</span></span>

<span data-ttu-id="6c768-111">tooconfigure Workstars 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="6c768-111">tooconfigure Azure AD integration with Workstars, you need hello following items:</span></span>

- <span data-ttu-id="6c768-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="6c768-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6c768-113">已啟用 Workstars 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="6c768-113">A Workstars single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6c768-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="6c768-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6c768-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="6c768-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6c768-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="6c768-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6c768-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="6c768-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6c768-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="6c768-118">Scenario description</span></span>
<span data-ttu-id="6c768-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6c768-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6c768-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="6c768-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6c768-121">從 hello 圖庫加入 Workstars</span><span class="sxs-lookup"><span data-stu-id="6c768-121">Adding Workstars from hello gallery</span></span>
2. <span data-ttu-id="6c768-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6c768-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workstars-from-hello-gallery"></a><span data-ttu-id="6c768-123">從 hello 圖庫加入 Workstars</span><span class="sxs-lookup"><span data-stu-id="6c768-123">Adding Workstars from hello gallery</span></span>
<span data-ttu-id="6c768-124">tooconfigure hello 整合 Workstars 到 Azure AD，您需要 tooadd Workstars hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6c768-124">tooconfigure hello integration of Workstars into Azure AD, you need tooadd Workstars from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6c768-125">**tooadd Workstars 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="6c768-125">**tooadd Workstars from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6c768-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="6c768-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 按鈕][1]

2. <span data-ttu-id="6c768-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="6c768-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6c768-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="6c768-129">Then go too**All applications**.</span></span>

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. <span data-ttu-id="6c768-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="6c768-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 新應用程式按鈕][3]

4. <span data-ttu-id="6c768-133">在 hello 搜尋方塊中，輸入**Workstars**，選取**Workstars**然後按一下 從結果面板**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6c768-133">In hello search box, type **Workstars**, select **Workstars** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Workstars hello [結果] 清單中](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6c768-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6c768-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="6c768-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Workstars 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6c768-136">In this section, you configure and test Azure AD single sign-on with Workstars based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6c768-137">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Workstars 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="6c768-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workstars is tooa user in Azure AD.</span></span> <span data-ttu-id="6c768-138">換句話說，Azure AD 使用者與 hello Workstars 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="6c768-138">In other words, a link relationship between an Azure AD user and hello related user in Workstars needs toobe established.</span></span>

<span data-ttu-id="6c768-139">Workstars 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="6c768-139">In Workstars, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6c768-140">tooconfigure 及 Workstars 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="6c768-140">tooconfigure and test Azure AD single sign-on with Workstars, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6c768-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="6c768-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6c768-142">**[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="6c768-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6c768-143">**[建立測試使用者 Workstars](#create-a-workstars-test-user)**  -toohave 許 Simon Workstars 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="6c768-143">**[Create a Workstars test user](#create-a-workstars-test-user)** - toohave a counterpart of Britta Simon in Workstars that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6c768-144">**[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6c768-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6c768-145">**[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="6c768-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="6c768-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6c768-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="6c768-147">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Workstars 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="6c768-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workstars application.</span></span>

<span data-ttu-id="6c768-148">**tooconfigure Azure AD 單一登入與 Workstars，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="6c768-148">**tooconfigure Azure AD single sign-on with Workstars, perform hello following steps:**</span></span>

1. <span data-ttu-id="6c768-149">在 Azure 入口網站上 hello hello **Workstars**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="6c768-149">In hello Azure portal, on hello **Workstars** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="6c768-151">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6c768-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_samlbase.png)

3. <span data-ttu-id="6c768-153">在 hello **Workstars 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="6c768-153">On hello **Workstars Domain and URLs** section, perform hello following steps:</span></span>

    ![Workstars 網域與 URL 單一登入資訊](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_url.png)

    <span data-ttu-id="6c768-155">a.</span><span class="sxs-lookup"><span data-stu-id="6c768-155">a.</span></span> <span data-ttu-id="6c768-156">在 hello**識別碼**文字方塊中，型別 hello URL:`https://workstars.com`</span><span class="sxs-lookup"><span data-stu-id="6c768-156">In hello **Identifier** textbox, type hello URL: `https://workstars.com`</span></span>

    <span data-ttu-id="6c768-157">b.</span><span class="sxs-lookup"><span data-stu-id="6c768-157">b.</span></span> <span data-ttu-id="6c768-158">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.workstars.com/saml/login_check`</span><span class="sxs-lookup"><span data-stu-id="6c768-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.workstars.com/saml/login_check`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6c768-159">hello 值不是真正的。</span><span class="sxs-lookup"><span data-stu-id="6c768-159">hello value is not real.</span></span> <span data-ttu-id="6c768-160">更新 hello 值與 hello 實際的回覆 URL。</span><span class="sxs-lookup"><span data-stu-id="6c768-160">Update hello value with hello actual Reply URL.</span></span> <span data-ttu-id="6c768-161">請連絡[Workstars 支援小組](https://support.workstars.com)tooget hello 值。</span><span class="sxs-lookup"><span data-stu-id="6c768-161">Contact [Workstars support team](https://support.workstars.com) tooget hello value.</span></span>
 
4. <span data-ttu-id="6c768-162">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="6c768-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![hello 憑證下載連結](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_certificate.png) 

5. <span data-ttu-id="6c768-164">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="6c768-164">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-workstars-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6c768-166">在 hello **Workstars 組態**區段中，按一下**設定 Workstars** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="6c768-166">On hello **Workstars Configuration** section, click **Configure Workstars** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6c768-167">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="6c768-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Workstars 組態](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_configure.png) 

7. <span data-ttu-id="6c768-169">在另一個瀏覽器視窗中，系統管理員身分登入 tooyour Workstars 公司網站。</span><span class="sxs-lookup"><span data-stu-id="6c768-169">In another browser window, sign on tooyour Workstars company site as an administrator.</span></span>

8. <span data-ttu-id="6c768-170">在 hello 主要工具列上，按一下 **設定**。</span><span class="sxs-lookup"><span data-stu-id="6c768-170">In hello main toolbar, click **Settings**.</span></span>

    ![Workstars 設定](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_sett.png)

9. <span data-ttu-id="6c768-172">跳過**登入** > **設定**。</span><span class="sxs-lookup"><span data-stu-id="6c768-172">Go too**Sign On** > **Settings**.</span></span>

    ![Workstars 登入](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_signon.png)

    ![Workstars 設定](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_settings.png)

10. <span data-ttu-id="6c768-175">在 hello**單一登入 (SAML)-設定**頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="6c768-175">On hello **Single Sign On (SAML) - Settings** page, perform hello following steps:</span></span>
    
    ![Workstars SAML](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_saml.png)

    <span data-ttu-id="6c768-177">a.</span><span class="sxs-lookup"><span data-stu-id="6c768-177">a.</span></span> <span data-ttu-id="6c768-178">在 [識別提供者名稱] 文字方塊中，輸入 **Office 365**。</span><span class="sxs-lookup"><span data-stu-id="6c768-178">In **Identity Provider Name** textbox, type **Office 365**.</span></span>

    <span data-ttu-id="6c768-179">b.</span><span class="sxs-lookup"><span data-stu-id="6c768-179">b.</span></span> <span data-ttu-id="6c768-180">在 hello**身分識別提供者的實體識別碼**文字方塊中，貼上 hello 值**SAML 實體識別碼**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="6c768-180">In hello **Identity Provider Entity ID** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="6c768-181">c.</span><span class="sxs-lookup"><span data-stu-id="6c768-181">c.</span></span> <span data-ttu-id="6c768-182">[記事本] 中的 hello 下載的憑證檔案的 hello 內容複製並貼到 hello **x509 憑證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="6c768-182">Copy hello content of hello downloaded certificate file in notepad, and then paste it into hello **x509 Certificate** textbox.</span></span> 

    <span data-ttu-id="6c768-183">d.</span><span class="sxs-lookup"><span data-stu-id="6c768-183">d.</span></span> <span data-ttu-id="6c768-184">在 hello **SAML SSO URL**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="6c768-184">In hello **SAML SSO URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="6c768-185">e.</span><span class="sxs-lookup"><span data-stu-id="6c768-185">e.</span></span> <span data-ttu-id="6c768-186">在 hello**遠端登出 URL**文字方塊中，貼上 hello 值**登出 URL**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="6c768-186">In hello **Remote Logout URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="6c768-187">f.</span><span class="sxs-lookup"><span data-stu-id="6c768-187">f.</span></span> <span data-ttu-id="6c768-188">選取 [名稱識別碼] 作為 [電子郵件 (預設)]。</span><span class="sxs-lookup"><span data-stu-id="6c768-188">select **Name ID** as **Email (Default)**.</span></span>

    <span data-ttu-id="6c768-189">g.</span><span class="sxs-lookup"><span data-stu-id="6c768-189">g.</span></span> <span data-ttu-id="6c768-190">按一下 [確認]。</span><span class="sxs-lookup"><span data-stu-id="6c768-190">Click **Confirm**.</span></span>
    
> [!TIP]
> <span data-ttu-id="6c768-191">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="6c768-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6c768-192">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="6c768-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6c768-193">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6c768-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6c768-194">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="6c768-194">Create an Azure AD test user</span></span>

<span data-ttu-id="6c768-195">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="6c768-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="6c768-197">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="6c768-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6c768-198">在 hello Azure 入口網站，hello 左窗格中，按一下 hello **Azure Active Directory**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="6c768-198">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-workstars-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="6c768-200">toodisplay hello 使用者清單，請移過**使用者和群組**，然後按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="6c768-200">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-workstars-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="6c768-202">tooopen hello**使用者**對話方塊中，按一下 [**新增**頂端的 hello hello**所有使用者**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="6c768-202">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello [新增] 按鈕](./media/active-directory-saas-workstars-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="6c768-204">在 hello**使用者**對話方塊方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="6c768-204">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello [使用者] 對話方塊](./media/active-directory-saas-workstars-tutorial/create_aaduser_04.png)

    <span data-ttu-id="6c768-206">a.</span><span class="sxs-lookup"><span data-stu-id="6c768-206">a.</span></span> <span data-ttu-id="6c768-207">在 hello**名稱**方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="6c768-207">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6c768-208">b.</span><span class="sxs-lookup"><span data-stu-id="6c768-208">b.</span></span> <span data-ttu-id="6c768-209">在 hello**使用者名**方塊中，使用者許 Simon 類型 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="6c768-209">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="6c768-210">c.</span><span class="sxs-lookup"><span data-stu-id="6c768-210">c.</span></span> <span data-ttu-id="6c768-211">選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 hello**密碼**方塊。</span><span class="sxs-lookup"><span data-stu-id="6c768-211">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="6c768-212">d.</span><span class="sxs-lookup"><span data-stu-id="6c768-212">d.</span></span> <span data-ttu-id="6c768-213">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="6c768-213">Click **Create**.</span></span>
  
### <a name="create-a-workstars-test-user"></a><span data-ttu-id="6c768-214">建立 Workstars 測試使用者</span><span class="sxs-lookup"><span data-stu-id="6c768-214">Create a Workstars test user</span></span>

<span data-ttu-id="6c768-215">在本節中，您會在 Workstars 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="6c768-215">In this section, you create a user called Britta Simon in Workstars.</span></span> <span data-ttu-id="6c768-216">使用[Workstars 支援小組](https://support.workstars.com)tooadd hello hello Workstars 平台的使用者。</span><span class="sxs-lookup"><span data-stu-id="6c768-216">Work with [Workstars support team](https://support.workstars.com) tooadd hello users in hello Workstars platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="6c768-217">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="6c768-217">Assign hello Azure AD test user</span></span>

<span data-ttu-id="6c768-218">在本節中，您可以授與存取 tooWorkstars 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6c768-218">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkstars.</span></span>

![指派 hello 使用者角色][200] 

<span data-ttu-id="6c768-220">**tooassign 許 Simon tooWorkstars，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="6c768-220">**tooassign Britta Simon tooWorkstars, perform hello following steps:**</span></span>

1. <span data-ttu-id="6c768-221">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="6c768-221">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="6c768-223">在 [hello] 應用程式清單中，選取**Workstars**。</span><span class="sxs-lookup"><span data-stu-id="6c768-223">In hello applications list, select **Workstars**.</span></span>

    ![hello 應用程式清單中的 hello Workstars 連結](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_app.png)  

3. <span data-ttu-id="6c768-225">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="6c768-225">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello 「 使用者和群組 」 的連結][202]

4. <span data-ttu-id="6c768-227">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6c768-227">Click **Add** button.</span></span> <span data-ttu-id="6c768-228">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="6c768-228">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 將作業加入窗格][203]

5. <span data-ttu-id="6c768-230">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="6c768-230">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6c768-231">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6c768-231">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6c768-232">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6c768-232">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="6c768-233">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="6c768-233">Test single sign-on</span></span>

<span data-ttu-id="6c768-234">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="6c768-234">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6c768-235">當您按一下的 hello Workstars 磚 hello 存取面板中時，您應該取得自動登入 tooyour Workstars 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6c768-235">When you click hello Workstars tile in hello Access Panel, you should get automatically signed-on tooyour Workstars application.</span></span>
<span data-ttu-id="6c768-236">如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="6c768-236">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6c768-237">其他資源</span><span class="sxs-lookup"><span data-stu-id="6c768-237">Additional resources</span></span>

* [<span data-ttu-id="6c768-238">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6c768-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6c768-239">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="6c768-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_203.png

