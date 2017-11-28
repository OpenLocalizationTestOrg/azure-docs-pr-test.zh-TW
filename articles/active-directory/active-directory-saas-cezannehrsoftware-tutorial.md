---
title: "教學課程：Azure Active Directory 與 Cezanne HR Software 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Cezanne HR 軟體之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fb8f95bf-c3c1-4e1f-b2b3-3b67526be72d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 3675acd8871d62c2277def8074f7aa39ac46e2a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-cezanne-hr-software"></a><span data-ttu-id="7854a-103">教學課程：Azure Active Directory 與 Cezanne HR Software 整合</span><span class="sxs-lookup"><span data-stu-id="7854a-103">Tutorial: Integrate Azure Active Directory with Cezanne HR software</span></span>

<span data-ttu-id="7854a-104">在此教學課程中，您學會如何 toointegrate Cezanne HR 軟體與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="7854a-104">In this tutorial, you learn how toointegrate Cezanne HR software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7854a-105">與 Azure AD 整合 Cezanne HR 軟體可以提供下列優點 hello。</span><span class="sxs-lookup"><span data-stu-id="7854a-105">Integrating Cezanne HR software with Azure AD provides you with hello following benefits.</span></span> <span data-ttu-id="7854a-106">您可以：</span><span class="sxs-lookup"><span data-stu-id="7854a-106">You can:</span></span>

- <span data-ttu-id="7854a-107">在 Azure AD 中擁有存取 tooCezanne 控制 HR 軟體。</span><span class="sxs-lookup"><span data-stu-id="7854a-107">Control in Azure AD who has access tooCezanne HR software.</span></span>
- <span data-ttu-id="7854a-108">可讓您的使用者 tooautomatically 登入 tooCezanne HR 軟體搭配單一登入 (SSO) 與 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="7854a-108">Enable your users tooautomatically sign in tooCezanne HR software with single sign-on (SSO) with their Azure AD accounts.</span></span>
- <span data-ttu-id="7854a-109">管理您的帳戶，在單一中央位置： hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="7854a-109">Manage your accounts in one central location: hello Azure portal.</span></span>

<span data-ttu-id="7854a-110">toolearn 進一步了解軟體即服務 (SaaS) 應用程式與 Azure AD 整合，請參閱[什麼是應用程式存取及 SSO 與 Azure Active Directory？](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="7854a-110">toolearn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and SSO with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7854a-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="7854a-111">Prerequisites</span></span>

<span data-ttu-id="7854a-112">tooconfigure 與 Cezanne HR software 的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="7854a-112">tooconfigure Azure AD integration with Cezanne HR software, you need hello following items:</span></span>

- <span data-ttu-id="7854a-113">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7854a-113">An Azure AD subscription</span></span>
- <span data-ttu-id="7854a-114">已啟用 Cezanne HR Software SSO 的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7854a-114">A Cezanne HR software SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7854a-115">tootest hello 步驟在本教學課程，我們建議您不要使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="7854a-115">tootest hello steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="7854a-116">tootest hello 步驟在本教學課程，請遵循下列建議：</span><span class="sxs-lookup"><span data-stu-id="7854a-116">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="7854a-117">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="7854a-117">Don't use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7854a-118">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="7854a-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7854a-119">案例描述</span><span class="sxs-lookup"><span data-stu-id="7854a-119">Scenario description</span></span>
<span data-ttu-id="7854a-120">在本教學課程中，您會在測試環境中測試 Azure AD SSO。</span><span class="sxs-lookup"><span data-stu-id="7854a-120">In this tutorial, you test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="7854a-121">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="7854a-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="7854a-122">從 hello 圖庫加入 Cezanne HR 軟體</span><span class="sxs-lookup"><span data-stu-id="7854a-122">Adding Cezanne HR software from hello gallery</span></span>
* <span data-ttu-id="7854a-123">設定並測試 Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="7854a-123">Configuring and testing Azure AD SSO</span></span>

## <a name="add-cezanne-hr-software-from-hello-gallery"></a><span data-ttu-id="7854a-124">從 hello 圖庫新增 Cezanne HR 軟體</span><span class="sxs-lookup"><span data-stu-id="7854a-124">Add Cezanne HR software from hello gallery</span></span>
<span data-ttu-id="7854a-125">tooconfigure hello 整合 Cezanne HR 軟體到 Azure AD 中，從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單加入 Cezanne HR 軟體。</span><span class="sxs-lookup"><span data-stu-id="7854a-125">tooconfigure hello integration of Cezanne HR software into Azure AD, add Cezanne HR software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7854a-126">tooadd Cezanne HR 軟體 hello 圖庫中，從 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="7854a-126">tooadd Cezanne HR software from hello gallery, do hello following:</span></span>

1. <span data-ttu-id="7854a-127">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，在 [hello 左的窗格中選取 hello **Azure Active Directory** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7854a-127">In hello **[Azure portal](https://portal.azure.com)**, in hello left pane, select hello **Azure Active Directory** button.</span></span> 

    ![hello"Azure Active Directory"的按鈕][1]

2. <span data-ttu-id="7854a-129">選取 [企業應用程式] > [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7854a-129">Select **Enterprise applications** > **All applications**.</span></span>

    ![hello [所有應用程式] 連結][2]
    
3. <span data-ttu-id="7854a-131">新的應用程式，在 hello hello 頂端 tooadd**所有應用程式**對話方塊中，選取**新的應用程式**。</span><span class="sxs-lookup"><span data-stu-id="7854a-131">tooadd a new application, at hello top of hello **All applications** dialog box, select **New application**.</span></span>

    ![hello 「 新的應用程式 」 按鈕][3]

4. <span data-ttu-id="7854a-133">在 [hello] 搜尋方塊中，輸入**Cezanne HR 軟體**。</span><span class="sxs-lookup"><span data-stu-id="7854a-133">In hello search box, type **Cezanne HR Software**.</span></span>

    ![hello 搜尋方塊](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_search.png)

5. <span data-ttu-id="7854a-135">在 [hello 結果清單中，選取 [ **Cezanne HR 軟體**]，然後選取 [hello**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7854a-135">In hello results list, select **Cezanne HR Software** and then select hello **Add** button tooadd hello application.</span></span>

    ![hello 結果清單](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7854a-137">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7854a-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="7854a-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Cezanne HR Software 搭配運作的 Azure AD SSO。</span><span class="sxs-lookup"><span data-stu-id="7854a-138">In this section, you configure and test Azure AD SSO with Cezanne HR software based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7854a-139">SSO toowork Azure AD 需要 tooknow hello Cezanne HR 軟體對等項目的 toohello Azure AD 使用者。</span><span class="sxs-lookup"><span data-stu-id="7854a-139">For SSO toowork, Azure AD needs tooknow hello Cezanne HR software counterpart toohello Azure AD user.</span></span> <span data-ttu-id="7854a-140">換句話說，您必須建立 Azure AD 使用者與 hello 相關的使用者之間的連結關聯性中 hello Cezanne HR 軟體。</span><span class="sxs-lookup"><span data-stu-id="7854a-140">In other words, you must establish a link relationship between an Azure AD user and hello related user in hello Cezanne HR software.</span></span>

<span data-ttu-id="7854a-141">tooestablish hello 連結關聯性，指派 hello Cezanne HR 軟體**使用者名**值為 hello Azure AD **Username**值。</span><span class="sxs-lookup"><span data-stu-id="7854a-141">tooestablish hello link relationship, assign hello Cezanne HR software **user name** value as hello Azure AD **Username** value.</span></span>

<span data-ttu-id="7854a-142">tooconfigure 和測試 Azure AD SSO 使用 Cezanne HR 軟體，完成下列建置組塊的 hello。</span><span class="sxs-lookup"><span data-stu-id="7854a-142">tooconfigure and test Azure AD SSO by using Cezanne HR software, complete hello following building blocks.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="7854a-143">設定 Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="7854a-143">Configure Azure AD SSO</span></span>

<span data-ttu-id="7854a-144">本節中，您可以在 hello Azure 入口網站中啟用 Azure AD 的 SSO 及 Cezanne HR 軟體應用程式中設定 SSO，藉由 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="7854a-144">In this section, you can enable Azure AD SSO in hello Azure portal and configure SSO in your Cezanne HR software application by doing hello following:</span></span>

1. <span data-ttu-id="7854a-145">在 Azure 入口網站上 hello hello **Cezanne HR 軟體**應用程式整合頁面上，選取**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="7854a-145">In hello Azure portal, on hello **Cezanne HR Software** application integration page, select **Single sign-on**.</span></span>

    ![hello 「 單一登入 」 的命令][4]

2. <span data-ttu-id="7854a-147">在 [hello tooenable SSO，**單一登入**對話方塊中，選取 hello**模式**做為**SAML 型登入**。</span><span class="sxs-lookup"><span data-stu-id="7854a-147">tooenable SSO, in hello **Single sign-on** dialog box, select hello **Mode** as **SAML-based Sign-on**.</span></span>
 
    ![hello [模式] 方塊](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_samlbase.png)

3. <span data-ttu-id="7854a-149">在下**Cezanne HR 軟體網域和 Url**，請勿遵循 hello:</span><span class="sxs-lookup"><span data-stu-id="7854a-149">Under **Cezanne HR Software Domain and URLs**, do hello following:</span></span>

    ![hello"Cezanne HR 軟體網域和 Url 」 一節](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_url.png)

    <span data-ttu-id="7854a-151">a.</span><span class="sxs-lookup"><span data-stu-id="7854a-151">a.</span></span> <span data-ttu-id="7854a-152">在 [hello**登入 URL**方塊中，輸入 URL，請使用下列語法已經 hello:`https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="7854a-152">In hello **Sign-on URL** box, type a URL that has hello following syntax: `https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`</span></span>

    <span data-ttu-id="7854a-153">b.</span><span class="sxs-lookup"><span data-stu-id="7854a-153">b.</span></span> <span data-ttu-id="7854a-154">在 [hello**回覆 URL**方塊中，輸入 URL，請使用下列語法已經 hello:`https://w3.cezanneondemand.com:443/<tenantid>`</span><span class="sxs-lookup"><span data-stu-id="7854a-154">In hello **Reply URL** box, type a URL that has hello following syntax: `https://w3.cezanneondemand.com:443/<tenantid>`</span></span>    
     
    > [!NOTE] 
    > <span data-ttu-id="7854a-155">hello 上述值不是實際。</span><span class="sxs-lookup"><span data-stu-id="7854a-155">hello preceding values are not real.</span></span> <span data-ttu-id="7854a-156">Hello 實際的回覆 URL 與 hello 登入 URL 加以更新。</span><span class="sxs-lookup"><span data-stu-id="7854a-156">Update them with hello actual reply URL and hello sign-on URL.</span></span> <span data-ttu-id="7854a-157">tooobtain hello 值，請連絡 hello [Cezanne HR 軟體用戶端支援小組](mailto:info@cezannehr.com)。</span><span class="sxs-lookup"><span data-stu-id="7854a-157">tooobtain hello values, contact hello [Cezanne HR software client support team](mailto:info@cezannehr.com).</span></span>

4. <span data-ttu-id="7854a-158">在下**SAML 簽章憑證**，選取**憑證 (Base64)**，然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="7854a-158">Under **SAML Signing Certificate**, select **Certificate (Base64)**, and then save hello certificate file on your computer.</span></span>

    ![hello 「 SAML 簽章憑證 」 一節](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_certificate.png) 

5. <span data-ttu-id="7854a-160">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="7854a-160">Select **Save**.</span></span>

    ![hello [儲存] 按鈕](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="7854a-162">在下**Cezanne HR 軟體組態**，選取**設定 Cezanne HR 軟體**tooopen hello**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="7854a-162">Under **Cezanne HR Software Configuration**, select **Configure Cezanne HR Software** tooopen hello **Configure sign-on** window.</span></span> <span data-ttu-id="7854a-163">複製 hello **SAML 實體識別碼**和**SAML 單一登入服務**URL 從 hello**快速參考**> 一節。</span><span class="sxs-lookup"><span data-stu-id="7854a-163">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service** URL from hello **Quick Reference** section.</span></span>

    ![hello"Cezanne HR 軟體組態 > 一節](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_configure.png) 

7. <span data-ttu-id="7854a-165">在不同的網頁瀏覽器視窗中，登入 tooyour Cezanne HR software 租用戶系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="7854a-165">In a different web browser window, sign on tooyour Cezanne HR software tenant as an administrator.</span></span>

8. <span data-ttu-id="7854a-166">Hello 左窗格中，選取**系統安裝**。</span><span class="sxs-lookup"><span data-stu-id="7854a-166">In hello left pane, select **System Setup**.</span></span> <span data-ttu-id="7854a-167">選取 [安全性設定] > [單一登入設定]。</span><span class="sxs-lookup"><span data-stu-id="7854a-167">Select **Security Settings** > **Single Sign-On Configuration**.</span></span>

    ![hello 「 單一登入設定 」 連結](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_000.png)

9. <span data-ttu-id="7854a-169">在 [hello**允許使用者 toolog 中使用下列單一登入 (SSO) 服務的 hello**窗格中，選取 hello **SAML 2.0**核取方塊並選取 hello**進階組態**選項。</span><span class="sxs-lookup"><span data-stu-id="7854a-169">In hello **Allow users toolog in using hello following Single Sign-On (SSO) services** pane, select hello **SAML 2.0** check box and select hello **Advanced Configuration** option.</span></span>

    ![單一登入服務選項](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_001.png)

10. <span data-ttu-id="7854a-171">選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="7854a-171">Select **Add New**.</span></span>

    ![hello"新增] 按鈕](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_002.png)

11. <span data-ttu-id="7854a-173">在下**SAML 2.0 身分識別提供者**，請勿遵循 hello:</span><span class="sxs-lookup"><span data-stu-id="7854a-173">Under **SAML 2.0 Identity Providers**, do hello following:</span></span>

    ![hello < SAML 2.0 身分識別提供者 > 一節](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_003.png)
    
    <span data-ttu-id="7854a-175">a.</span><span class="sxs-lookup"><span data-stu-id="7854a-175">a.</span></span> <span data-ttu-id="7854a-176">在 [hello**顯示名稱**方塊中，輸入您的身分識別提供者的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="7854a-176">In hello **Display Name** box, enter hello name of your identity provider.</span></span>

    <span data-ttu-id="7854a-177">b.</span><span class="sxs-lookup"><span data-stu-id="7854a-177">b.</span></span> <span data-ttu-id="7854a-178">在 [hello**實體識別碼**方塊中，貼上 hello **SAML 實體識別碼**從 hello Azure 入口網站中複製。</span><span class="sxs-lookup"><span data-stu-id="7854a-178">In hello **Entity Identifier** box, paste hello **SAML Entity ID** that you copied from hello Azure portal.</span></span> 

    <span data-ttu-id="7854a-179">c.</span><span class="sxs-lookup"><span data-stu-id="7854a-179">c.</span></span> <span data-ttu-id="7854a-180">在 [hello **SAML 繫結**清單方塊中，選取**POST**。</span><span class="sxs-lookup"><span data-stu-id="7854a-180">In hello **SAML Binding** list box, select **POST**.</span></span>

    <span data-ttu-id="7854a-181">d.</span><span class="sxs-lookup"><span data-stu-id="7854a-181">d.</span></span> <span data-ttu-id="7854a-182">在 [hello**安全性權杖服務端點**方塊中，貼上 hello **SAML 單一登入服務**您所複製的 hello Azure 入口網站的 URL。</span><span class="sxs-lookup"><span data-stu-id="7854a-182">In hello **Security Token Service Endpoint** box, paste hello **SAML Single Sign-On Service** URL that you copied from hello Azure portal.</span></span> 
    
    <span data-ttu-id="7854a-183">e.</span><span class="sxs-lookup"><span data-stu-id="7854a-183">e.</span></span> <span data-ttu-id="7854a-184">在 [hello**使用者 ID 的屬性名稱**方塊中，輸入`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`。</span><span class="sxs-lookup"><span data-stu-id="7854a-184">In hello **User ID Attribute Name** box, enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
    
    <span data-ttu-id="7854a-185">f.</span><span class="sxs-lookup"><span data-stu-id="7854a-185">f.</span></span> <span data-ttu-id="7854a-186">tooupload hello 從 Azure AD 中，選取 hello 下載憑證**上傳**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7854a-186">tooupload hello downloaded certificate from Azure AD, select hello **Upload** button.</span></span>
    
    <span data-ttu-id="7854a-187">g.</span><span class="sxs-lookup"><span data-stu-id="7854a-187">g.</span></span> <span data-ttu-id="7854a-188">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="7854a-188">Select **OK**.</span></span> 

12. <span data-ttu-id="7854a-189">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="7854a-189">Select **Save**.</span></span>

    ![hello [儲存] 按鈕](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_004.png)

> [!TIP]
> <span data-ttu-id="7854a-191">當您設定 hello 應用程式時，您可以閱讀 hello hello 中前面指示的精簡版本[Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="7854a-191">As you set up hello app, you can read a concise version of hello preceding instructions in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="7854a-192">從 hello 新增 hello 應用程式之後**Active Directory** > **企業應用程式**區段中，選取 hello**單一登入**] 索引標籤。然後存取 hello 內嵌文件從 hello**組態**> 一節。</span><span class="sxs-lookup"><span data-stu-id="7854a-192">After you add hello app from hello **Active Directory** > **Enterprise applications** section, select hello **Single sign-on** tab. Then access hello embedded documentation from hello **Configuration** section.</span></span> 

<span data-ttu-id="7854a-193">toolearn 進一步了解 hello embedded 文件功能，請參閱[Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)。</span><span class="sxs-lookup"><span data-stu-id="7854a-193">toolearn more about hello embedded documentation feature, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7854a-194">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7854a-194">Create an Azure AD test user</span></span>
<span data-ttu-id="7854a-195">在本節中，您可以建立測試使用者許 Simon hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="7854a-195">In this section, you create test user Britta Simon in hello Azure portal.</span></span>

![hello 許 Simon 的測試使用者][100]

<span data-ttu-id="7854a-197">在 Azure AD 中的測試使用者 toocreate hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="7854a-197">toocreate a test user in Azure AD, do hello following:</span></span>

1. <span data-ttu-id="7854a-198">在 [hello **Azure 入口網站**，在 [hello 左的窗格中選取 hello **Azure Active Directory** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7854a-198">In hello **Azure portal**, in hello left pane, select hello **Azure Active Directory** button.</span></span>

    ![hello"Azure Active Directory"的按鈕](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7854a-200">toodisplay hello 使用者清單，選取**使用者和群組** > **所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="7854a-200">toodisplay hello list of users, select **Users and groups** > **All users**.</span></span>
    
    ![hello，"All users"連結](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_02.png) 
    
    <span data-ttu-id="7854a-202">hello**所有使用者**對話方塊隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="7854a-202">hello **All users** dialog box opens.</span></span>

3. <span data-ttu-id="7854a-203">tooopen hello**使用者**對話方塊中，選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="7854a-203">tooopen hello **User** dialog box, select **Add**.</span></span>
 
    ![hello [新增] 按鈕](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7854a-205">在 [hello**使用者**對話方塊方塊中，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="7854a-205">In hello **User** dialog box, do hello following:</span></span>
 
    ![hello [使用者] 對話方塊](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7854a-207">a.</span><span class="sxs-lookup"><span data-stu-id="7854a-207">a.</span></span> <span data-ttu-id="7854a-208">在 [hello**名稱**方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="7854a-208">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7854a-209">b.</span><span class="sxs-lookup"><span data-stu-id="7854a-209">b.</span></span> <span data-ttu-id="7854a-210">在 [hello**使用者名**方塊中，輸入使用者許 Simon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="7854a-210">In hello **User name** box, type user Britta Simon's **email address**.</span></span>

    <span data-ttu-id="7854a-211">c.</span><span class="sxs-lookup"><span data-stu-id="7854a-211">c.</span></span> <span data-ttu-id="7854a-212">選取 hello**顯示密碼**核取方塊，然後注意 hello 值所產生的 hello**密碼**方塊。</span><span class="sxs-lookup"><span data-stu-id="7854a-212">Select hello **Show Password** check box, and then note hello value that was generated in hello **Password** box.</span></span>

    <span data-ttu-id="7854a-213">d.</span><span class="sxs-lookup"><span data-stu-id="7854a-213">d.</span></span> <span data-ttu-id="7854a-214">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="7854a-214">Select **Create**.</span></span>
 
### <a name="create-a-cezanne-hr-software-test-user"></a><span data-ttu-id="7854a-215">建立 Cezanne HR Software 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7854a-215">Create a Cezanne HR software test user</span></span>

<span data-ttu-id="7854a-216">tooenable Azure AD 使用者 toosign tooCezanne HR 軟體，您必須佈建到 Cezanne HR 軟體。</span><span class="sxs-lookup"><span data-stu-id="7854a-216">tooenable Azure AD users toosign in tooCezanne HR software, they must be provisioned into Cezanne HR software.</span></span> <span data-ttu-id="7854a-217">中的 Cezanne HR 軟體 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="7854a-217">In hello case of Cezanne HR software, provisioning is a manual task.</span></span>

<span data-ttu-id="7854a-218">佈建使用者帳戶，藉由下列 hello:</span><span class="sxs-lookup"><span data-stu-id="7854a-218">Provision a user account by doing hello following:</span></span>

1.  <span data-ttu-id="7854a-219">Tooyour Cezanne HR software 公司網站管理員身分登入。</span><span class="sxs-lookup"><span data-stu-id="7854a-219">Sign in tooyour Cezanne HR software company site as an administrator.</span></span>

2.  <span data-ttu-id="7854a-220">Hello 左窗格中，選取**系統安裝** > **管理使用者** > **新增使用者**。</span><span class="sxs-lookup"><span data-stu-id="7854a-220">In hello left pane, select **System Setup** > **Manage Users** > **Add New User**.</span></span>

    <span data-ttu-id="7854a-221">![hello [加入新使用者] 連結](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "新使用者")</span><span class="sxs-lookup"><span data-stu-id="7854a-221">![hello "Add New User" link](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "New User")</span></span>

3.  <span data-ttu-id="7854a-222">在下**人員詳細資料**，請勿遵循 hello:</span><span class="sxs-lookup"><span data-stu-id="7854a-222">Under **Person Details**, do hello following:</span></span>

    <span data-ttu-id="7854a-223">![hello < 人員詳細資料 > 一節](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "新使用者")</span><span class="sxs-lookup"><span data-stu-id="7854a-223">![hello "Person Details" section](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "New User")</span></span>
    
    <span data-ttu-id="7854a-224">a.</span><span class="sxs-lookup"><span data-stu-id="7854a-224">a.</span></span> <span data-ttu-id="7854a-225">將 [內部使用者] 設為 [OFF]。</span><span class="sxs-lookup"><span data-stu-id="7854a-225">Set **Internal User** as **OFF**.</span></span>
    
    <span data-ttu-id="7854a-226">b.</span><span class="sxs-lookup"><span data-stu-id="7854a-226">b.</span></span> <span data-ttu-id="7854a-227">在 [hello**名字**方塊中，型別 hello 使用者的名字，例如**許**。</span><span class="sxs-lookup"><span data-stu-id="7854a-227">In hello **First Name** box, type hello user's first name, for example, **Britta**.</span></span>  
 
    <span data-ttu-id="7854a-228">c.</span><span class="sxs-lookup"><span data-stu-id="7854a-228">c.</span></span> <span data-ttu-id="7854a-229">在 [hello**姓氏**方塊中，型別 hello 使用者的姓氏，例如**Simon**。</span><span class="sxs-lookup"><span data-stu-id="7854a-229">In hello **Last Name** box, type hello user's last name, for example, **Simon**.</span></span>
    
    <span data-ttu-id="7854a-230">d.</span><span class="sxs-lookup"><span data-stu-id="7854a-230">d.</span></span> <span data-ttu-id="7854a-231">在 [hello**電子郵件**方塊中，輸入 hello 使用者的電子郵件地址，例如Brittasimon@contoso.com。</span><span class="sxs-lookup"><span data-stu-id="7854a-231">In hello **E-mail** box, type hello user's email address, for example, Brittasimon@contoso.com.</span></span>

4.  <span data-ttu-id="7854a-232">在下**帳戶資訊**，請勿遵循 hello:</span><span class="sxs-lookup"><span data-stu-id="7854a-232">Under **Account Information**, do hello following:</span></span>

    <span data-ttu-id="7854a-233">![hello 」 帳戶資訊 > 一節](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "新使用者")</span><span class="sxs-lookup"><span data-stu-id="7854a-233">![hello "Account Information" section](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "New User")</span></span>
    
    <span data-ttu-id="7854a-234">a.</span><span class="sxs-lookup"><span data-stu-id="7854a-234">a.</span></span> <span data-ttu-id="7854a-235">在 [hello **Username**方塊中，輸入 hello 使用者的電子郵件地址，例如Brittasimon@contoso.com。</span><span class="sxs-lookup"><span data-stu-id="7854a-235">In hello **Username** box, type hello user's email address, for example, Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="7854a-236">b.</span><span class="sxs-lookup"><span data-stu-id="7854a-236">b.</span></span> <span data-ttu-id="7854a-237">在 [hello**密碼**方塊中，輸入 hello 使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="7854a-237">In hello **Password** box, type hello user's password.</span></span>
    
    <span data-ttu-id="7854a-238">c.</span><span class="sxs-lookup"><span data-stu-id="7854a-238">c.</span></span> <span data-ttu-id="7854a-239">在 [hello**安全性角色**方塊中，選取**HR Professional**。</span><span class="sxs-lookup"><span data-stu-id="7854a-239">In hello **Security Role** box, select **HR Professional**.</span></span>
    
    <span data-ttu-id="7854a-240">d.</span><span class="sxs-lookup"><span data-stu-id="7854a-240">d.</span></span> <span data-ttu-id="7854a-241">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="7854a-241">Select **OK**.</span></span>

5. <span data-ttu-id="7854a-242">在 [hello**單一登入**索引標籤上，在 [hello **SAML 2.0 識別碼**區段中，選取**加入新**。</span><span class="sxs-lookup"><span data-stu-id="7854a-242">On hello **Single sign-on** tab, in hello **SAML 2.0 Identifiers** section, select **Add New**.</span></span>

    <span data-ttu-id="7854a-243">![hello"新增"按鈕](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="7854a-243">![hello "Add New" button](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "User")</span></span>

6. <span data-ttu-id="7854a-244">在 [hello**身分識別提供者**清單方塊中，選取您的身分識別提供者。</span><span class="sxs-lookup"><span data-stu-id="7854a-244">In hello **Identity Provider** list box, select your identity provider.</span></span> <span data-ttu-id="7854a-245">在 [hello**使用者識別碼**方塊中，輸入測試使用者許 Simon 的帳戶 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="7854a-245">In hello **User Identifier** box, enter hello email address for test user Britta Simon's account.</span></span>

    <span data-ttu-id="7854a-246">![hello 「 身分識別提供者 」 和 「 使用者識別碼 」 方塊](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="7854a-246">![hello "Identity Provider" and "User Identifier" boxes](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "User")</span></span>
    
7. <span data-ttu-id="7854a-247">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="7854a-247">Select **Save**.</span></span>

    <span data-ttu-id="7854a-248">![hello [儲存] 按鈕](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="7854a-248">![hello "Save" button](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "User")</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="7854a-249">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7854a-249">Assign hello Azure AD test user</span></span>

<span data-ttu-id="7854a-250">在本節中，您可以授與存取 tooCezanne HR 軟體啟用測試使用者許 Simon toouse Azure SSO。</span><span class="sxs-lookup"><span data-stu-id="7854a-250">In this section, you enable test user Britta Simon toouse Azure SSO by granting access tooCezanne HR software.</span></span>

![測試使用者存取][200] 

1. <span data-ttu-id="7854a-252">在 [hello Azure 入口網站，開啟 hello 應用程式檢視並前往 toohello 目錄檢視。</span><span class="sxs-lookup"><span data-stu-id="7854a-252">In hello Azure portal, open hello applications view and then go toohello directory view.</span></span> <span data-ttu-id="7854a-253">選取 [企業應用程式] > [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7854a-253">Select **Enterprise applications** > **All applications**.</span></span>

    ![hello [所有應用程式] 連結][201] 

2. <span data-ttu-id="7854a-255">在 [hello] 應用程式清單中，選取**Cezanne HR 軟體**。</span><span class="sxs-lookup"><span data-stu-id="7854a-255">In hello applications list, select **Cezanne HR Software**.</span></span>

    ![hello"應用程式] 清單](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_app.png) 

3. <span data-ttu-id="7854a-257">在左側 hello hello 功能表中選取**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="7854a-257">In hello menu on hello left, select **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="7854a-259">選取 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="7854a-259">Select **Add**.</span></span> <span data-ttu-id="7854a-260">接著在 hello**將作業加入**對話方塊中，選取**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="7854a-260">Then in hello **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![[使用者和群組] 連結][203]

5. <span data-ttu-id="7854a-262">在 [hello**使用者和群組**對話方塊中的，在 hello**使用者**清單中，選取**許 Simon**。</span><span class="sxs-lookup"><span data-stu-id="7854a-262">In hello **Users and groups** dialog box, in hello **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="7854a-263">在 [hello**使用者和群組**對話方塊中，選取**選取**。</span><span class="sxs-lookup"><span data-stu-id="7854a-263">In hello **Users and groups** dialog box, select **Select**.</span></span>

7. <span data-ttu-id="7854a-264">在 [hello**將作業加入**對話方塊中，選取**指派**。</span><span class="sxs-lookup"><span data-stu-id="7854a-264">In hello **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-sso"></a><span data-ttu-id="7854a-265">測試 SSO</span><span class="sxs-lookup"><span data-stu-id="7854a-265">Test SSO</span></span>

<span data-ttu-id="7854a-266">本節中，在中，您可以測試您的 Azure AD 的 SSO 組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="7854a-266">In this section, you test your Azure AD SSO configuration by using hello Access Panel.</span></span>

<span data-ttu-id="7854a-267">當您選取 hello Cezanne HR 軟體磚 hello 存取面板中時，您登入自動 tooyour Cezanne HR 軟體應用程式。</span><span class="sxs-lookup"><span data-stu-id="7854a-267">When you select hello Cezanne HR software tile in hello Access Panel, you sign on automatically tooyour Cezanne HR software application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7854a-268">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7854a-268">Next steps</span></span>

* [<span data-ttu-id="7854a-269">如何教學課程清單 toointegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7854a-269">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7854a-270">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="7854a-270">What is application access and SSO with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_203.png

