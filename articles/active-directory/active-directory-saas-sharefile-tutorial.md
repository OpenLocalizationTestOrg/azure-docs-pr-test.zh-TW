---
title: "教學課程：Azure Active Directory 與 Citrix ShareFile 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Citrix ShareFile 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: e14fc310-bac4-4f09-99ef-87e5c77288b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2017
ms.author: jeedes
ms.openlocfilehash: d7eaf140e56c40f9f621062849dd8558588ffd1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-sharefile"></a><span data-ttu-id="61e73-103">教學課程：Azure Active Directory 與 Citrix ShareFile 整合</span><span class="sxs-lookup"><span data-stu-id="61e73-103">Tutorial: Azure Active Directory integration with Citrix ShareFile</span></span>

<span data-ttu-id="61e73-104">在此教學課程中，您學會如何 toointegrate Citrix ShareFile 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="61e73-104">In this tutorial, you learn how toointegrate Citrix ShareFile with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="61e73-105">整合 Azure AD 與 Citrix ShareFile 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="61e73-105">Integrating Citrix ShareFile with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="61e73-106">您可以控制存取 tooCitrix ShareFile 的 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="61e73-106">You can control in Azure AD who has access tooCitrix ShareFile.</span></span>
- <span data-ttu-id="61e73-107">您可以啟用您的使用者 tooautomatically get 登入 tooCitrix ShareFile （單一登入） 具有其 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="61e73-107">You can enable your users tooautomatically get signed-on tooCitrix ShareFile (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="61e73-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="61e73-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="61e73-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="61e73-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="61e73-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="61e73-110">Prerequisites</span></span>

<span data-ttu-id="61e73-111">tooconfigure Azure AD 與 Citrix ShareFile 的整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="61e73-111">tooconfigure Azure AD integration with Citrix ShareFile, you need hello following items:</span></span>

- <span data-ttu-id="61e73-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="61e73-112">An Azure AD subscription</span></span>
- <span data-ttu-id="61e73-113">已啟用 Citrix ShareFile 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="61e73-113">A Citrix ShareFile single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="61e73-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="61e73-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="61e73-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="61e73-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="61e73-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="61e73-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="61e73-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="61e73-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="61e73-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="61e73-118">Scenario description</span></span>
<span data-ttu-id="61e73-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="61e73-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="61e73-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="61e73-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="61e73-121">新增 Citrix ShareFile 從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="61e73-121">Add Citrix ShareFile from hello gallery</span></span>
2. <span data-ttu-id="61e73-122">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="61e73-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-citrix-sharefile-from-hello-gallery"></a><span data-ttu-id="61e73-123">新增 Citrix ShareFile 從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="61e73-123">Add Citrix ShareFile from hello gallery</span></span>
<span data-ttu-id="61e73-124">tooconfigure hello 整合 Citrix ShareFile 的 Azure AD，您需要 tooadd Citrix ShareFile hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="61e73-124">tooconfigure hello integration of Citrix ShareFile into Azure AD, you need tooadd Citrix ShareFile from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="61e73-125">**tooadd Citrix ShareFile 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="61e73-125">**tooadd Citrix ShareFile from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="61e73-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="61e73-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 按鈕][1]

2. <span data-ttu-id="61e73-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="61e73-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="61e73-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="61e73-129">Then go too**All applications**.</span></span>

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. <span data-ttu-id="61e73-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="61e73-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 新應用程式按鈕][3]

4. <span data-ttu-id="61e73-133">在 hello 搜尋方塊中，輸入**Citrix ShareFile**，選取**Citrix ShareFile**然後按一下 從結果面板**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="61e73-133">In hello search box, type **Citrix ShareFile**, select **Citrix ShareFile** from result panel then click **Add** button tooadd hello application.</span></span>

    ![在 hello Citrix ShareFile 結果清單](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="61e73-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="61e73-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="61e73-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Citrix ShareFile 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="61e73-136">In this section, you configure and test Azure AD single sign-on with Citrix ShareFile based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="61e73-137">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者 Citrix ShareFile 中是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="61e73-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Citrix ShareFile is tooa user in Azure AD.</span></span> <span data-ttu-id="61e73-138">換句話說，Azure AD 使用者與 Citrix ShareFile 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="61e73-138">In other words, a link relationship between an Azure AD user and hello related user in Citrix ShareFile needs toobe established.</span></span>

<span data-ttu-id="61e73-139">在 Citrix ShareFile 中，將指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="61e73-139">In Citrix ShareFile, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="61e73-140">tooconfigure 和測試 Azure AD 單一登入與 Citrix ShareFile，您需要遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="61e73-140">tooconfigure and test Azure AD single sign-on with Citrix ShareFile, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="61e73-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="61e73-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="61e73-142">**[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="61e73-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="61e73-143">**[建立測試使用者 Citrix ShareFile](#create-a-citrix-sharefile-test-user)**  -toohave 許 Simon Citrix ShareFile 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="61e73-143">**[Create a Citrix ShareFile test user](#create-a-citrix-sharefile-test-user)** - toohave a counterpart of Britta Simon in Citrix ShareFile that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="61e73-144">**[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="61e73-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="61e73-145">**[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="61e73-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="61e73-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="61e73-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="61e73-147">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Citrix ShareFile 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="61e73-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Citrix ShareFile application.</span></span>

<span data-ttu-id="61e73-148">**tooconfigure Azure AD 單一登入與 Citrix ShareFile，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="61e73-148">**tooconfigure Azure AD single sign-on with Citrix ShareFile, perform hello following steps:**</span></span>

1. <span data-ttu-id="61e73-149">在 Azure 入口網站上 hello hello **Citrix ShareFile**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="61e73-149">In hello Azure portal, on hello **Citrix ShareFile** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="61e73-151">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="61e73-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_samlbase.png)

3. <span data-ttu-id="61e73-153">在 hello **Citrix ShareFile 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="61e73-153">On hello **Citrix ShareFile Domain and URLs** section, perform hello following steps:</span></span>

    ![Citrix ShareFile 網域與 URL 單一登入資訊](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_url.png)
    
    <span data-ttu-id="61e73-155">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<tenant-name>.sharefile.com/saml/login`</span><span class="sxs-lookup"><span data-stu-id="61e73-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.sharefile.com/saml/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="61e73-156">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="61e73-156">This value is not real.</span></span> <span data-ttu-id="61e73-157">更新此值以 hello 實際的登入 URL。</span><span class="sxs-lookup"><span data-stu-id="61e73-157">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="61e73-158">請連絡[Citrix ShareFile 用戶端支援小組](https://www.citrix.co.in/products/sharefile/support.html)tooget 此值。</span><span class="sxs-lookup"><span data-stu-id="61e73-158">Contact [Citrix ShareFile Client support team](https://www.citrix.co.in/products/sharefile/support.html) tooget this value.</span></span> 

4. <span data-ttu-id="61e73-159">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="61e73-159">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![hello 憑證下載連結](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_certificate.png) 

5. <span data-ttu-id="61e73-161">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="61e73-161">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-sharefile-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="61e73-163">在 hello **Citrix ShareFile 設定**區段中，按一下**設定 Citrix ShareFile** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="61e73-163">On hello **Citrix ShareFile Configuration** section, click **Configure Citrix ShareFile** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="61e73-164">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="61e73-164">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Citrix ShareFile 設定](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_configure.png) 

7. <span data-ttu-id="61e73-166">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 **Citrix ShareFile** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="61e73-166">In a different web browser window, log into your **Citrix ShareFile** company site as an administrator.</span></span>

8. <span data-ttu-id="61e73-167">在 hello hello 上方的工具列中按一下**Admin**。</span><span class="sxs-lookup"><span data-stu-id="61e73-167">In hello toolbar on hello top, click **Admin**.</span></span>

9. <span data-ttu-id="61e73-168">在 hello 左側瀏覽窗格中，選取**設定單一登入**。</span><span class="sxs-lookup"><span data-stu-id="61e73-168">In hello left navigation pane, select **Configure Single Sign-On**.</span></span>
   
    <span data-ttu-id="61e73-169">![帳戶管理](./media/active-directory-saas-sharefile-tutorial/ic773627.png "帳戶管理")</span><span class="sxs-lookup"><span data-stu-id="61e73-169">![Account Administration](./media/active-directory-saas-sharefile-tutorial/ic773627.png "Account Administration")</span></span>

10. <span data-ttu-id="61e73-170">在 hello**單一登入 / SAML 2.0 設定**對話方塊頁面的 下**基本設定**，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="61e73-170">On hello **Single Sign-On/ SAML 2.0 Configuration** dialog page under **Basic Settings**, perform hello following steps:</span></span>
   
    <span data-ttu-id="61e73-171">![單一登入](./media/active-directory-saas-sharefile-tutorial/ic773628.png "單一登入")</span><span class="sxs-lookup"><span data-stu-id="61e73-171">![Single sign-on](./media/active-directory-saas-sharefile-tutorial/ic773628.png "Single sign-on")</span></span>
   
    <span data-ttu-id="61e73-172">a.</span><span class="sxs-lookup"><span data-stu-id="61e73-172">a.</span></span> <span data-ttu-id="61e73-173">按一下 [啟用 SAML] 。</span><span class="sxs-lookup"><span data-stu-id="61e73-173">Click **Enable SAML**.</span></span>
    
    <span data-ttu-id="61e73-174">b.</span><span class="sxs-lookup"><span data-stu-id="61e73-174">b.</span></span> <span data-ttu-id="61e73-175">在**您的 IDP 簽發者 / 實體識別碼**文字方塊中，貼上 hello 值**SAML 實體識別碼**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="61e73-175">In **Your IDP Issuer/ Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="61e73-176">c.</span><span class="sxs-lookup"><span data-stu-id="61e73-176">c.</span></span> <span data-ttu-id="61e73-177">按一下**變更**下一步 toohello **X.509 憑證**欄位，然後從您下載的憑證上傳 hello hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="61e73-177">Click **Change** next toohello **X.509 Certificate** field and then upload hello certificate you downloaded from hello Azure portal.</span></span>
    
    <span data-ttu-id="61e73-178">d.</span><span class="sxs-lookup"><span data-stu-id="61e73-178">d.</span></span> <span data-ttu-id="61e73-179">在**登入 URL**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="61e73-179">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="61e73-180">e.</span><span class="sxs-lookup"><span data-stu-id="61e73-180">e.</span></span> <span data-ttu-id="61e73-181">在**登出 URL**文字方塊中，貼上 hello 值**登出 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="61e73-181">In **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

11. <span data-ttu-id="61e73-182">按一下**儲存**hello Citrix ShareFile 管理入口網站上。</span><span class="sxs-lookup"><span data-stu-id="61e73-182">Click **Save** on hello Citrix ShareFile management portal.</span></span>

> [!TIP]
> <span data-ttu-id="61e73-183">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="61e73-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="61e73-184">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="61e73-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="61e73-185">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="61e73-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="61e73-186">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="61e73-186">Create an Azure AD test user</span></span>

<span data-ttu-id="61e73-187">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="61e73-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="61e73-189">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="61e73-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="61e73-190">在 hello Azure 入口網站，hello 左窗格中，按一下 hello **Azure Active Directory**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="61e73-190">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-sharefile-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="61e73-192">toodisplay hello 使用者清單，請移過**使用者和群組**，然後按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="61e73-192">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-sharefile-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="61e73-194">tooopen hello**使用者**對話方塊中，按一下 [**新增**頂端的 hello hello**所有使用者**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="61e73-194">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello [新增] 按鈕](./media/active-directory-saas-sharefile-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="61e73-196">在 hello**使用者**對話方塊方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="61e73-196">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello [使用者] 對話方塊](./media/active-directory-saas-sharefile-tutorial/create_aaduser_04.png)

    <span data-ttu-id="61e73-198">a.</span><span class="sxs-lookup"><span data-stu-id="61e73-198">a.</span></span> <span data-ttu-id="61e73-199">在 hello**名稱**方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="61e73-199">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="61e73-200">b.</span><span class="sxs-lookup"><span data-stu-id="61e73-200">b.</span></span> <span data-ttu-id="61e73-201">在 hello**使用者名**方塊中，使用者許 Simon 類型 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="61e73-201">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="61e73-202">c.</span><span class="sxs-lookup"><span data-stu-id="61e73-202">c.</span></span> <span data-ttu-id="61e73-203">選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 hello**密碼**方塊。</span><span class="sxs-lookup"><span data-stu-id="61e73-203">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="61e73-204">d.</span><span class="sxs-lookup"><span data-stu-id="61e73-204">d.</span></span> <span data-ttu-id="61e73-205">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="61e73-205">Click **Create**.</span></span>
 
### <a name="create-a-citrix-sharefile-test-user"></a><span data-ttu-id="61e73-206">建立 Citrix ShareFile 測試使用者</span><span class="sxs-lookup"><span data-stu-id="61e73-206">Create a Citrix ShareFile test user</span></span>

<span data-ttu-id="61e73-207">在訂單 tooenable Azure AD 使用者 toolog 到 Citrix ShareFile，它們必須佈建到 Citrix ShareFile。</span><span class="sxs-lookup"><span data-stu-id="61e73-207">In order tooenable Azure AD users toolog into Citrix ShareFile, they must be provisioned into Citrix ShareFile.</span></span> <span data-ttu-id="61e73-208">在 Citrix ShareFile 的 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="61e73-208">In hello case of Citrix ShareFile, provisioning is a manual task.</span></span>

<span data-ttu-id="61e73-209">**tooprovision 使用者帳戶，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="61e73-209">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="61e73-210">登入 tooyour **Citrix ShareFile**租用戶。</span><span class="sxs-lookup"><span data-stu-id="61e73-210">Log in tooyour **Citrix ShareFile** tenant.</span></span>

2. <span data-ttu-id="61e73-211">按一下 [管理使用者] \> [管理使用者首頁] \> [+ 建立員工]。</span><span class="sxs-lookup"><span data-stu-id="61e73-211">Click **Manage Users \> Manage Users Home \> + Create Employee**.</span></span>
   
   <span data-ttu-id="61e73-212">![建立員工](./media/active-directory-saas-sharefile-tutorial/IC781050.png "建立員工")</span><span class="sxs-lookup"><span data-stu-id="61e73-212">![Create Employee](./media/active-directory-saas-sharefile-tutorial/IC781050.png "Create Employee")</span></span>

3. <span data-ttu-id="61e73-213">在 hello**基本資訊**區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="61e73-213">On hello **Basic Information** section, perform below steps:</span></span>
   
   <span data-ttu-id="61e73-214">![基本資訊](./media/active-directory-saas-sharefile-tutorial/IC799951.png "的基本資訊")</span><span class="sxs-lookup"><span data-stu-id="61e73-214">![Basic Information](./media/active-directory-saas-sharefile-tutorial/IC799951.png "Basic Information")</span></span>
   
   <span data-ttu-id="61e73-215">a.</span><span class="sxs-lookup"><span data-stu-id="61e73-215">a.</span></span> <span data-ttu-id="61e73-216">在 hello**電子郵件地址**文字方塊中，型別 hello 電子郵件地址做為許 Simon  **brittasimon@contoso.com** 。</span><span class="sxs-lookup"><span data-stu-id="61e73-216">In hello **Email Address** textbox, type hello email address of Britta Simon as **brittasimon@contoso.com**.</span></span>
   
   <span data-ttu-id="61e73-217">b.</span><span class="sxs-lookup"><span data-stu-id="61e73-217">b.</span></span> <span data-ttu-id="61e73-218">在 hello**名字**文字方塊中，輸入**名字**做為使用者的**許**。</span><span class="sxs-lookup"><span data-stu-id="61e73-218">In hello **First Name** textbox, type **first name** of user as **Britta**.</span></span>
   
   <span data-ttu-id="61e73-219">c.</span><span class="sxs-lookup"><span data-stu-id="61e73-219">c.</span></span> <span data-ttu-id="61e73-220">在 hello**姓氏**文字方塊中，輸入**姓氏**做為使用者的**Simon**。</span><span class="sxs-lookup"><span data-stu-id="61e73-220">In hello **Last Name** textbox, type **last name** of user as **Simon**.</span></span>

4. <span data-ttu-id="61e73-221">按一下 [加入使用者] 。</span><span class="sxs-lookup"><span data-stu-id="61e73-221">Click **Add User**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="61e73-222">hello Azure AD 帳戶持有者將收到一封電子郵件，並遵循連結 tooconfirm 他們的帳戶之前就會生效。您可以使用任何其他 Citrix ShareFile 使用者帳戶建立工具或 Api 提供 Citrix ShareFile tooprovision Azure AD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="61e73-222">hello Azure AD account holder will receive an email and follow a link tooconfirm their account before it becomes active.You can use any other Citrix ShareFile user account creation tools or APIs provided by Citrix ShareFile tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="61e73-223">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="61e73-223">Assign hello Azure AD test user</span></span>

<span data-ttu-id="61e73-224">在本節中，您可以授與存取 tooCitrix ShareFile 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="61e73-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCitrix ShareFile.</span></span>

![指派 hello 使用者角色][200] 

<span data-ttu-id="61e73-226">**tooassign 許 Simon tooCitrix ShareFile 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="61e73-226">**tooassign Britta Simon tooCitrix ShareFile, perform hello following steps:**</span></span>

1. <span data-ttu-id="61e73-227">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="61e73-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="61e73-229">在 [hello] 應用程式清單中，選取**Citrix ShareFile**。</span><span class="sxs-lookup"><span data-stu-id="61e73-229">In hello applications list, select **Citrix ShareFile**.</span></span>

    ![hello hello 應用程式清單中的 Citrix ShareFile 連結](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_app.png)  

3. <span data-ttu-id="61e73-231">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="61e73-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello 「 使用者和群組 」 的連結][202]

4. <span data-ttu-id="61e73-233">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="61e73-233">Click **Add** button.</span></span> <span data-ttu-id="61e73-234">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="61e73-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 將作業加入窗格][203]

5. <span data-ttu-id="61e73-236">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="61e73-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="61e73-237">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="61e73-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="61e73-238">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="61e73-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="61e73-239">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="61e73-239">Test single sign-on</span></span>

<span data-ttu-id="61e73-240">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="61e73-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="61e73-241">當您按一下的 hello Citrix ShareFile 磚 hello 存取面板中時，您應該取得自動登入 tooyour Citrix ShareFile 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="61e73-241">When you click hello Citrix ShareFile tile in hello Access Panel, you should get automatically signed-on tooyour Citrix ShareFile application.</span></span>
<span data-ttu-id="61e73-242">如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="61e73-242">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="61e73-243">其他資源</span><span class="sxs-lookup"><span data-stu-id="61e73-243">Additional resources</span></span>

* [<span data-ttu-id="61e73-244">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="61e73-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="61e73-245">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="61e73-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_203.png

