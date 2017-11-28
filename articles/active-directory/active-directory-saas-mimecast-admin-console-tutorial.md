---
title: "教學課程：Azure Active Directory 與 Mimecast Admin Console 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Mimecast 管理員主控台。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 81c50614-f49b-4bbc-97d5-3cf77154305f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 5a04a5abd9ff30d484bce0a5c97a1d3e48b69e4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-admin-console"></a><span data-ttu-id="1b2ae-103">教學課程：Azure Active Directory 與 Mimecast Admin Console 整合</span><span class="sxs-lookup"><span data-stu-id="1b2ae-103">Tutorial: Azure Active Directory integration with Mimecast Admin Console</span></span>

<span data-ttu-id="1b2ae-104">在此教學課程中，您學會如何與 Azure Active Directory (Azure AD) 的 toointegrate Mimecast 管理員主控台。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-104">In this tutorial, you learn how toointegrate Mimecast Admin Console with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1b2ae-105">與 Azure AD 整合 Mimecast 管理員主控台可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="1b2ae-105">Integrating Mimecast Admin Console with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1b2ae-106">您可以控制存取 tooMimecast 管理主控台的 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-106">You can control in Azure AD who has access tooMimecast Admin Console.</span></span>
- <span data-ttu-id="1b2ae-107">您可以啟用您的使用者 tooautomatically get 登入 tooMimecast （單一登入） 的系統管理員主控台與他們的 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-107">You can enable your users tooautomatically get signed-on tooMimecast Admin Console (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="1b2ae-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="1b2ae-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b2ae-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="1b2ae-110">Prerequisites</span></span>

<span data-ttu-id="1b2ae-111">tooconfigure 與 Mimecast 管理員主控台的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="1b2ae-111">tooconfigure Azure AD integration with Mimecast Admin Console, you need hello following items:</span></span>

- <span data-ttu-id="1b2ae-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1b2ae-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1b2ae-113">啟用 Mimecast Admin Console 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1b2ae-113">A Mimecast Admin Console single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1b2ae-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1b2ae-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="1b2ae-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1b2ae-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1b2ae-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1b2ae-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="1b2ae-118">Scenario description</span></span>
<span data-ttu-id="1b2ae-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1b2ae-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="1b2ae-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1b2ae-121">從 hello 圖庫加入 Mimecast 管理員主控台</span><span class="sxs-lookup"><span data-stu-id="1b2ae-121">Adding Mimecast Admin Console from hello gallery</span></span>
2. <span data-ttu-id="1b2ae-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1b2ae-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mimecast-admin-console-from-hello-gallery"></a><span data-ttu-id="1b2ae-123">從 hello 圖庫加入 Mimecast 管理員主控台</span><span class="sxs-lookup"><span data-stu-id="1b2ae-123">Adding Mimecast Admin Console from hello gallery</span></span>
<span data-ttu-id="1b2ae-124">tooconfigure hello 整合 Mimecast 管理員主控台至 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Mimecast 管理員主控台。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-124">tooconfigure hello integration of Mimecast Admin Console into Azure AD, you need tooadd Mimecast Admin Console from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1b2ae-125">**tooadd Mimecast 管理員主控台，從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1b2ae-125">**tooadd Mimecast Admin Console from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1b2ae-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 按鈕][1]

2. <span data-ttu-id="1b2ae-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1b2ae-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-129">Then go too**All applications**.</span></span>

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. <span data-ttu-id="1b2ae-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 新應用程式按鈕][3]

4. <span data-ttu-id="1b2ae-133">在 hello 搜尋方塊中，輸入**Mimecast 管理員主控台**，選取**Mimecast 管理員主控台**然後按一下 從結果面板**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-133">In hello search box, type **Mimecast Admin Console**, select **Mimecast Admin Console** from result panel then click **Add** button tooadd hello application.</span></span>

    ![在結果清單中 hello Mimecast 管理員主控台](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="1b2ae-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1b2ae-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="1b2ae-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Mimecast Admin Console 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-136">In this section, you configure and test Azure AD single sign-on with Mimecast Admin Console based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1b2ae-137">單一登入 toowork，Azure AD 需要 tooknow Mimecast 管理員主控台中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Mimecast Admin Console is tooa user in Azure AD.</span></span> <span data-ttu-id="1b2ae-138">換句話說，Azure AD 使用者與 Mimecast 管理員主控台中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-138">In other words, a link relationship between an Azure AD user and hello related user in Mimecast Admin Console needs toobe established.</span></span>

<span data-ttu-id="1b2ae-139">在 Mimecast 管理員主控台，將指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-139">In Mimecast Admin Console, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1b2ae-140">tooconfigure 及測試 Azure AD 單一登入 Mimecast 管理員主控台，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="1b2ae-140">tooconfigure and test Azure AD single sign-on with Mimecast Admin Console, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1b2ae-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1b2ae-142">**[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1b2ae-143">**[建立測試使用者 Mimecast 管理員主控台](#create-a-mimecast-admin-console-test-user)** -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示法的 Mimecast 管理員主控台中的對應項目。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-143">**[Create a Mimecast Admin Console test user](#create-a-mimecast-admin-console-test-user)** - toohave a counterpart of Britta Simon in Mimecast Admin Console that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1b2ae-144">**[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1b2ae-145">**[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="1b2ae-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1b2ae-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="1b2ae-147">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Mimecast 管理員主控台應用程式中。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Mimecast Admin Console application.</span></span>

<span data-ttu-id="1b2ae-148">**tooconfigure Azure AD 單一登入與 Mimecast 管理員主控台中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1b2ae-148">**tooconfigure Azure AD single sign-on with Mimecast Admin Console, perform hello following steps:**</span></span>

1. <span data-ttu-id="1b2ae-149">在 Azure 入口網站上 hello hello **Mimecast 管理員主控台**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-149">In hello Azure portal, on hello **Mimecast Admin Console** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="1b2ae-151">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_samlbase.png)

3. <span data-ttu-id="1b2ae-153">在 hello **Mimecast 管理員主控台網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1b2ae-153">On hello **Mimecast Admin Console Domain and URLs** section, perform hello following steps:</span></span>

    ![Mimecast Admin Console 網域與 URL 單一登入資訊](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_url.png)

    <span data-ttu-id="1b2ae-155">在 hello**登入 URL**文字方塊中，型別 hello URL:</span><span class="sxs-lookup"><span data-stu-id="1b2ae-155">In hello **Sign-on URL** textbox, type hello URL:</span></span>
    | |
    | -- |
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|

    > [!NOTE] 
    > <span data-ttu-id="1b2ae-156">hello 登入 URL 與區域特定相關。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-156">hello sign on URL is region specific.</span></span>

4. <span data-ttu-id="1b2ae-157">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-157">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![hello 憑證下載連結](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_certificate.png) 

5. <span data-ttu-id="1b2ae-159">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-159">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1b2ae-161">在 hello **Mimecast 管理員主控台設定**區段中，按一下**設定 Mimecast 管理員主控台**tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-161">On hello **Mimecast Admin Console Configuration** section, click **Configure Mimecast Admin Console** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1b2ae-162">複製 hello **SAML 實體識別碼和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="1b2ae-162">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Mimecast Admin Console 設定](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_configure.png) 

7. <span data-ttu-id="1b2ae-164">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 Mimecast Admin Console 公司網站。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-164">In a different web browser window, log into your Mimecast Admin Console as an administrator.</span></span>

8. <span data-ttu-id="1b2ae-165">跳過**服務\>應用程式**。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-165">Go too**Services \> Application**.</span></span>

    <span data-ttu-id="1b2ae-166">![服務](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "服務")</span><span class="sxs-lookup"><span data-stu-id="1b2ae-166">![Services](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "Services")</span></span>

9. <span data-ttu-id="1b2ae-167">按一下 [驗證設定檔] 。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-167">Click **Authentication Profiles**.</span></span>

    <span data-ttu-id="1b2ae-168">![驗證設定檔](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "驗證設定檔")</span><span class="sxs-lookup"><span data-stu-id="1b2ae-168">![Authentication Profiles](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "Authentication Profiles")</span></span>
    
10. <span data-ttu-id="1b2ae-169">按一下 [新驗證設定檔] 。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-169">Click **New Authentication Profile**.</span></span>

    <span data-ttu-id="1b2ae-170">![新驗證設定檔](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "新驗證設定檔")</span><span class="sxs-lookup"><span data-stu-id="1b2ae-170">![New Authentication Profiles](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "New Authentication Profiles")</span></span>

11. <span data-ttu-id="1b2ae-171">在 hello**驗證設定檔**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1b2ae-171">In hello **Authentication Profile** section, perform hello following steps:</span></span>

    <span data-ttu-id="1b2ae-172">![驗證設定檔](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "驗證設定檔")</span><span class="sxs-lookup"><span data-stu-id="1b2ae-172">![Authentication Profile](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "Authentication Profile")</span></span>
    
    <span data-ttu-id="1b2ae-173">a.</span><span class="sxs-lookup"><span data-stu-id="1b2ae-173">a.</span></span> <span data-ttu-id="1b2ae-174">在 hello**描述**文字方塊中，輸入您的組態名稱。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-174">In hello **Description** textbox, type a name for your configuration.</span></span>
    
    <span data-ttu-id="1b2ae-175">b.</span><span class="sxs-lookup"><span data-stu-id="1b2ae-175">b.</span></span> <span data-ttu-id="1b2ae-176">選取 [強制執行 Mimecast Admin Console 的 SAML 驗證] 。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-176">Select **Enforce SAML Authentication for Mimecast Admin Console**.</span></span>
    
    <span data-ttu-id="1b2ae-177">c.</span><span class="sxs-lookup"><span data-stu-id="1b2ae-177">c.</span></span> <span data-ttu-id="1b2ae-178">在 [提供者] 中選取 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-178">As **Provider**, select **Azure Active Directory**.</span></span>
    
    <span data-ttu-id="1b2ae-179">d.</span><span class="sxs-lookup"><span data-stu-id="1b2ae-179">d.</span></span> <span data-ttu-id="1b2ae-180">貼上**SAML 實體識別碼**，其中您從 hello Azure 入口網站複製到 hello**簽發者 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-180">Paste **SAML Entity ID**, which you have copied from hello Azure portal into hello **Issuer URL** textbox.</span></span>
    
    <span data-ttu-id="1b2ae-181">e.</span><span class="sxs-lookup"><span data-stu-id="1b2ae-181">e.</span></span> <span data-ttu-id="1b2ae-182">貼上**SAML 單一登入服務 URL**，其中您從 hello Azure 入口網站複製到 hello**登入 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-182">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **Login URL** textbox.</span></span>

    <span data-ttu-id="1b2ae-183">f.</span><span class="sxs-lookup"><span data-stu-id="1b2ae-183">f.</span></span> <span data-ttu-id="1b2ae-184">貼上**SAML 單一登入服務 URL**，其中您從 hello Azure 入口網站複製到 hello**登出 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-184">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **Logout URL** textbox.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="1b2ae-185">hello 登入 URL 值與 hello 登出 URL 值是 hello Mimecast 管理員主控台 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-185">hello Login URL value and hello Logout URL value are for hello Mimecast Admin Console hello same.</span></span>
    
    <span data-ttu-id="1b2ae-186">g.</span><span class="sxs-lookup"><span data-stu-id="1b2ae-186">g.</span></span> <span data-ttu-id="1b2ae-187">Base 64 憑證下載從 Azure 入口網站，在 [記事本] 開啟移除 hello 第一行 ("*--*") 和 hello 最後一行 ("*--*")，複本 hello 剩餘它的內容到剪貼簿，然後將它貼入 toohello**身分識別提供者憑證 （中繼資料）**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-187">Open your base-64 certificate downloaded from Azure portal in notepad, remove hello first line (“*--*“) and hello last line (“*--*“), copy hello remaining content of it into your clipboard, and then paste it toohello **Identity Provider Certificate (Metadata)** textbox.</span></span>
    
    <span data-ttu-id="1b2ae-188">h.</span><span class="sxs-lookup"><span data-stu-id="1b2ae-188">h.</span></span> <span data-ttu-id="1b2ae-189">選取 [允許單一登入] 。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-189">Select **Allow Single Sign On**.</span></span>
    
    <span data-ttu-id="1b2ae-190">i.</span><span class="sxs-lookup"><span data-stu-id="1b2ae-190">i.</span></span> <span data-ttu-id="1b2ae-191">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-191">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="1b2ae-192">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="1b2ae-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1b2ae-193">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1b2ae-194">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1b2ae-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1b2ae-195">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1b2ae-195">Create an Azure AD test user</span></span>

<span data-ttu-id="1b2ae-196">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="1b2ae-198">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1b2ae-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1b2ae-199">在 hello Azure 入口網站，hello 左窗格中，按一下 hello **Azure Active Directory**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-199">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="1b2ae-201">toodisplay hello 使用者清單，請移過**使用者和群組**，然後按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-201">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="1b2ae-203">tooopen hello**使用者**對話方塊中，按一下 [**新增**頂端的 hello hello**所有使用者**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-203">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello [新增] 按鈕](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="1b2ae-205">在 hello**使用者**對話方塊方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1b2ae-205">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello [使用者] 對話方塊](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_04.png)

    <span data-ttu-id="1b2ae-207">a.</span><span class="sxs-lookup"><span data-stu-id="1b2ae-207">a.</span></span> <span data-ttu-id="1b2ae-208">在 hello**名稱**方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-208">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1b2ae-209">b.</span><span class="sxs-lookup"><span data-stu-id="1b2ae-209">b.</span></span> <span data-ttu-id="1b2ae-210">在 hello**使用者名**方塊中，使用者許 Simon 類型 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-210">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="1b2ae-211">c.</span><span class="sxs-lookup"><span data-stu-id="1b2ae-211">c.</span></span> <span data-ttu-id="1b2ae-212">選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 hello**密碼**方塊。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-212">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="1b2ae-213">d.</span><span class="sxs-lookup"><span data-stu-id="1b2ae-213">d.</span></span> <span data-ttu-id="1b2ae-214">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-214">Click **Create**.</span></span>
 
### <a name="create-a-mimecast-admin-console-test-user"></a><span data-ttu-id="1b2ae-215">建立 Mimecast Admin Console 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1b2ae-215">Create a Mimecast Admin Console test user</span></span>

<span data-ttu-id="1b2ae-216">在訂單 tooenable Azure AD 使用者 toolog 入 Mimecast 管理員主控台，您必須是佈建到 Mimecast 管理員主控台。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-216">In order tooenable Azure AD users toolog into Mimecast Admin Console, they must be provisioned into Mimecast Admin Console.</span></span> <span data-ttu-id="1b2ae-217">在 Mimecast 管理員主控台的 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-217">In hello case of Mimecast Admin Console, provisioning is a manual task.</span></span>

* <span data-ttu-id="1b2ae-218">您可以建立使用者之前，您會需要 tooregister 網域。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-218">You need tooregister a domain before you can create users.</span></span>

<span data-ttu-id="1b2ae-219">**tooconfigure 使用者佈建，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1b2ae-219">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="1b2ae-220">登入 tooyour **Mimecast 管理員主控台**以系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-220">Sign on tooyour **Mimecast Admin Console** as administrator.</span></span>
2. <span data-ttu-id="1b2ae-221">跳過**目錄\>內部**。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-221">Go too**Directories \> Internal**.</span></span>
   
   <span data-ttu-id="1b2ae-222">![目錄](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "目錄")</span><span class="sxs-lookup"><span data-stu-id="1b2ae-222">![Directories](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "Directories")</span></span>
3. <span data-ttu-id="1b2ae-223">按一下 [註冊新網域] 。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-223">Click **Register New Domain**.</span></span>
   
   <span data-ttu-id="1b2ae-224">![註冊新網域](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "註冊新網域")</span><span class="sxs-lookup"><span data-stu-id="1b2ae-224">![Register New Domain](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "Register New Domain")</span></span>
4. <span data-ttu-id="1b2ae-225">在您建立好新網域之後，，按一下 [新位址] 。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-225">After your new domain has been created, click **New Address**.</span></span>
   
   <span data-ttu-id="1b2ae-226">![新位址](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "新位址")</span><span class="sxs-lookup"><span data-stu-id="1b2ae-226">![New Address](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "New Address")</span></span>
5. <span data-ttu-id="1b2ae-227">在 hello 新位址 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1b2ae-227">In hello new address dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="1b2ae-228">![儲存](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "儲存")</span><span class="sxs-lookup"><span data-stu-id="1b2ae-228">![Save](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "Save")</span></span>
   
   <span data-ttu-id="1b2ae-229">a.</span><span class="sxs-lookup"><span data-stu-id="1b2ae-229">a.</span></span> <span data-ttu-id="1b2ae-230">型別 hello**電子郵件地址**，**全域名稱**，**密碼**，和**確認密碼**屬性有效的 Azure AD 的帳戶，您想要tooprovision hello 到相關的文字方塊。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-230">Type hello **Email Address**, **Global Name**, **Password**, and **Confirm Password** attributes of a valid Azure AD account you want tooprovision into hello related textboxes.</span></span>

   <span data-ttu-id="1b2ae-231">b.</span><span class="sxs-lookup"><span data-stu-id="1b2ae-231">b.</span></span> <span data-ttu-id="1b2ae-232">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-232">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="1b2ae-233">您可以使用任何其他 Mimecast 管理員主控台使用者帳戶建立工具或 Api Mimecast 管理員主控台 tooprovision Azure AD 使用者帳戶所提供。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-233">You can use any other Mimecast Admin Console user account creation tools or APIs provided by Mimecast Admin Console tooprovision Azure AD user accounts.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="1b2ae-234">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1b2ae-234">Assign hello Azure AD test user</span></span>

<span data-ttu-id="1b2ae-235">在本節中，您可以授與存取 tooMimecast 管理主控台啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMimecast Admin Console.</span></span>

![指派 hello 使用者角色][200] 

<span data-ttu-id="1b2ae-237">**tooassign 許 Simon tooMimecast 管理主控台中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1b2ae-237">**tooassign Britta Simon tooMimecast Admin Console, perform hello following steps:**</span></span>

1. <span data-ttu-id="1b2ae-238">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-238">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="1b2ae-240">在 [hello] 應用程式清單中，選取**Mimecast 管理員主控台**。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-240">In hello applications list, select **Mimecast Admin Console**.</span></span>

    ![hello 應用程式清單中的 hello Mimecast 管理員主控台連結](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_app.png)  

3. <span data-ttu-id="1b2ae-242">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello 「 使用者和群組 」 的連結][202]

4. <span data-ttu-id="1b2ae-244">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-244">Click **Add** button.</span></span> <span data-ttu-id="1b2ae-245">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 將作業加入窗格][203]

5. <span data-ttu-id="1b2ae-247">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1b2ae-248">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1b2ae-249">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="1b2ae-250">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="1b2ae-250">Test single sign-on</span></span>

<span data-ttu-id="1b2ae-251">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-251">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1b2ae-252">當您按一下 hello Mimecast 管理員主控台的並排顯示 hello 存取面板中時，您應該取得 tooyour 自動登入 Mimecast 管理員主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-252">When you click hello Mimecast Admin Console tile in hello Access Panel, you should get automatically signed-on tooyour Mimecast Admin Console application.</span></span>
<span data-ttu-id="1b2ae-253">如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="1b2ae-253">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1b2ae-254">其他資源</span><span class="sxs-lookup"><span data-stu-id="1b2ae-254">Additional resources</span></span>

* [<span data-ttu-id="1b2ae-255">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1b2ae-255">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1b2ae-256">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="1b2ae-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_203.png

