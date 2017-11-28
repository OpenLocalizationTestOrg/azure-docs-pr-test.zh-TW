---
title: "教學課程：Azure Active Directory 與 Adobe Creative Cloud 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Adobe 創意雲端之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9ba1171e-56b1-4475-b308-58637d35e5a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 5e66255e9785465974a23cd3ef79c24e28c0250f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-creative-cloud"></a><span data-ttu-id="7973f-103">教學課程：Azure Active Directory 與 Adobe Creative Cloud 整合</span><span class="sxs-lookup"><span data-stu-id="7973f-103">Tutorial: Azure Active Directory integration with Adobe Creative Cloud</span></span>

<span data-ttu-id="7973f-104">在此教學課程中，您學會如何 toointegrate Adobe c 雲端與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="7973f-104">In this tutorial, you learn how toointegrate Adobe Creative Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7973f-105">與 Azure AD 整合 Adobe 創意雲端可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="7973f-105">Integrating Adobe Creative Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7973f-106">您可以控制存取 tooAdobe 創意雲端的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="7973f-106">You can control in Azure AD who has access tooAdobe Creative Cloud</span></span>
- <span data-ttu-id="7973f-107">您可以使用其 Azure AD 帳戶啟用您的使用者 tooautomatically get 登入 tooAdobe 創意雲端 （單一登入）</span><span class="sxs-lookup"><span data-stu-id="7973f-107">You can enable your users tooautomatically get signed-on tooAdobe Creative Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7973f-108">您可以管理您的帳戶，在單一中央位置-hello Azure 管理入口網站</span><span class="sxs-lookup"><span data-stu-id="7973f-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="7973f-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="7973f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7973f-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="7973f-110">Prerequisites</span></span>

<span data-ttu-id="7973f-111">tooconfigure 與 Adobe 創意雲端的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="7973f-111">tooconfigure Azure AD integration with Adobe Creative Cloud, you need hello following items:</span></span>

- <span data-ttu-id="7973f-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7973f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7973f-113">已啟用 Adobe Creative Cloud 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7973f-113">A Adobe Creative Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7973f-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="7973f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7973f-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="7973f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7973f-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="7973f-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="7973f-117">如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="7973f-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7973f-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="7973f-118">Scenario description</span></span>
<span data-ttu-id="7973f-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7973f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7973f-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="7973f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7973f-121">從 hello 圖庫加入 Adobe 創意雲端</span><span class="sxs-lookup"><span data-stu-id="7973f-121">Adding Adobe Creative Cloud from hello gallery</span></span>
2. <span data-ttu-id="7973f-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7973f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adobe-creative-cloud-from-hello-gallery"></a><span data-ttu-id="7973f-123">從 hello 圖庫加入 Adobe 創意雲端</span><span class="sxs-lookup"><span data-stu-id="7973f-123">Adding Adobe Creative Cloud from hello gallery</span></span>
<span data-ttu-id="7973f-124">tooconfigure hello 整合 Adobe 創意雲端的 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Adobe 創意雲端。</span><span class="sxs-lookup"><span data-stu-id="7973f-124">tooconfigure hello integration of Adobe Creative Cloud into Azure AD, you need tooadd Adobe Creative Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7973f-125">**tooadd Adobe 創意雲端 hello 圖庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="7973f-125">**tooadd Adobe Creative Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7973f-126">在 [hello ** [Azure 管理入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="7973f-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7973f-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="7973f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7973f-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="7973f-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="7973f-131">按一下**新增**上 hello hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="7973f-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="7973f-133">在 [hello] 搜尋方塊中，輸入**Adobe 創意雲端**。</span><span class="sxs-lookup"><span data-stu-id="7973f-133">In hello search box, type **Adobe Creative Cloud**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_000.png)

5. <span data-ttu-id="7973f-135">在 [hello [結果] 窗格中，選取 [ **Adobe 創意雲端**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7973f-135">In hello results panel, select **Adobe Creative Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7973f-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7973f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7973f-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Adobe Creative Cloud 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7973f-138">In this section, you configure and test Azure AD single sign-on with Adobe Creative Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7973f-139">單一登入 toowork，Azure AD 需要 tooknow Adobe 創意雲端中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="7973f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Adobe Creative Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="7973f-140">換句話說，Azure AD 使用者與 Adobe 創意雲端中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="7973f-140">In other words, a link relationship between an Azure AD user and hello related user in Adobe Creative Cloud needs toobe established.</span></span>

<span data-ttu-id="7973f-141">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Adobe 創意雲端中。</span><span class="sxs-lookup"><span data-stu-id="7973f-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Adobe Creative Cloud.</span></span>

<span data-ttu-id="7973f-142">tooconfigure 和測試 Azure AD 單一登入與 Adobe 創意雲端，您需要遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="7973f-142">tooconfigure and test Azure AD single sign-on with Adobe Creative Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7973f-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="7973f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7973f-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="7973f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7973f-145">**[建立測試使用者 Adobe 創意雲端](#creating-an-adobe-creative-cloud-test-user)** -toohave 許 Simon Adobe 創意雲端是連結的 toohello Azure AD 的她的表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="7973f-145">**[Creating an Adobe Creative Cloud test user](#creating-an-adobe-creative-cloud-test-user)** - toohave a counterpart of Britta Simon in Adobe Creative Cloud that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="7973f-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7973f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7973f-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="7973f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7973f-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7973f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7973f-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 管理入口網站中，並設定單一登入 Adobe 創意雲端應用程式中。</span><span class="sxs-lookup"><span data-stu-id="7973f-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Adobe Creative Cloud application.</span></span>

<span data-ttu-id="7973f-150">**以 Adobe 創意雲端，Azure AD 單一登入 tooconfigure 執行 hello 下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7973f-150">**tooconfigure Azure AD single sign-on with Adobe Creative Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="7973f-151">在 hello Azure 管理入口網站上 hello **Adobe 創意雲端**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="7973f-151">In hello Azure Management portal, on hello **Adobe Creative Cloud** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="7973f-153">在 [hello**單一登入**] 對話方塊中，做為**模式**選取**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7973f-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_01.png)

3. <span data-ttu-id="7973f-155">在 [hello **Adobe 創意雲端網域和 Url**區段中，執行下列步驟，如果您想 tooconfigure hello 應用程式中的 hello **IDP**初始模式：</span><span class="sxs-lookup"><span data-stu-id="7973f-155">On hello **Adobe Creative Cloud Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url1.png)

    <span data-ttu-id="7973f-157">a.</span><span class="sxs-lookup"><span data-stu-id="7973f-157">a.</span></span> <span data-ttu-id="7973f-158">在 [hello**識別碼**文字方塊中，做為型別 hello 值：`https://www.okta.com/saml2/service-provider/<token>`</span><span class="sxs-lookup"><span data-stu-id="7973f-158">In hello **Identifier** textbox, type hello value as: `https://www.okta.com/saml2/service-provider/<token>`</span></span>

    <span data-ttu-id="7973f-159">b.</span><span class="sxs-lookup"><span data-stu-id="7973f-159">b.</span></span> <span data-ttu-id="7973f-160">在 [hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<company name>.okta.com/auth/saml20/accauthlinktest`</span><span class="sxs-lookup"><span data-stu-id="7973f-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.okta.com/auth/saml20/accauthlinktest`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7973f-161">請注意這些不是 hello 實際值。</span><span class="sxs-lookup"><span data-stu-id="7973f-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="7973f-162">您有 tooupdate hello 實際的識別項和回覆 url 的這些值。</span><span class="sxs-lookup"><span data-stu-id="7973f-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="7973f-163">這裡我們建議您 toouse hello 唯一字串的值在 hello 識別項。</span><span class="sxs-lookup"><span data-stu-id="7973f-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="7973f-164">若要手動 toocreate 使用者，您會需要 toocontact hello Adobe 創意雲端支援小組。</span><span class="sxs-lookup"><span data-stu-id="7973f-164">If you need toocreate an user manually, you need toocontact hello Adobe Creative Cloud support team.</span></span>

4. <span data-ttu-id="7973f-165">在 [hello **Adobe 創意雲端網域和 Url**區段中，執行下列步驟，如果您想 tooconfigure hello 應用程式中的 hello **SP**初始模式：</span><span class="sxs-lookup"><span data-stu-id="7973f-165">On hello **Adobe Creative Cloud Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url2.png)

    <span data-ttu-id="7973f-167">a.</span><span class="sxs-lookup"><span data-stu-id="7973f-167">a.</span></span> <span data-ttu-id="7973f-168">按一下 hello**顯示進階的 URL 設定**選項</span><span class="sxs-lookup"><span data-stu-id="7973f-168">Click on hello **Show advanced URL settings** option</span></span>

    <span data-ttu-id="7973f-169">b.</span><span class="sxs-lookup"><span data-stu-id="7973f-169">b.</span></span> <span data-ttu-id="7973f-170">在 [hello**登入 URL**文字方塊中，做為型別 hello 值：`https://adobe.com`</span><span class="sxs-lookup"><span data-stu-id="7973f-170">In hello **Sign-on URL** textbox, type hello value as: `https://adobe.com`</span></span>

5. <span data-ttu-id="7973f-171">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="7973f-171">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_05.png) 

6. <span data-ttu-id="7973f-173">在 [hello **Adobe 創意雲端組態**區段中，按一下**設定 Adobe 創意雲端**tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="7973f-173">On hello **Adobe Creative Cloud Configuration** section, click **Configure Adobe Creative Cloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7973f-174">請將複製 hello **SAML 實體識別碼**和**SAML SSO 服務 URL**從快速參考 > 一節。</span><span class="sxs-lookup"><span data-stu-id="7973f-174">Please copy hello **SAML Entity Id** and **SAML SSO Service URL** from Quick Reference section.</span></span>

    ![設定單一登入](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_06.png) 

7. <span data-ttu-id="7973f-176">在不同的網頁瀏覽器視窗中，以系統管理員身分登入 tooyour Adobe 創意雲端租用戶。</span><span class="sxs-lookup"><span data-stu-id="7973f-176">In a different web browser window, sign-on tooyour Adobe Creative Cloud tenant as an administrator.</span></span>

8.  <span data-ttu-id="7973f-177">跳過**識別**在 hello 左側的導覽窗格中，按一下您的網域。</span><span class="sxs-lookup"><span data-stu-id="7973f-177">Go too**Identity** on hello left navigation pane and click your domain.</span></span> <span data-ttu-id="7973f-178">然後執行下列步驟 hello**單一登入需要設定**> 一節。</span><span class="sxs-lookup"><span data-stu-id="7973f-178">Then perform hello following steps on **Single Sign On Configuration Required** section.</span></span>

    <span data-ttu-id="7973f-179">![設定](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "設定")</span><span class="sxs-lookup"><span data-stu-id="7973f-179">![Settings](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "Settings")</span></span>

9. <span data-ttu-id="7973f-180">按一下**瀏覽**tooupload hello 下載憑證從 Azure AD 太**IDP 憑證**。</span><span class="sxs-lookup"><span data-stu-id="7973f-180">Click **Browse** tooupload hello downloaded certificate from Azure AD too**IDP Certificate**.</span></span>

10. <span data-ttu-id="7973f-181">在 [hello **IDP 簽發者**文字方塊中，將 hello 值放**SAML 實體識別碼**您複製從**設定登入**Azure 入口網站中的區段。</span><span class="sxs-lookup"><span data-stu-id="7973f-181">In hello **IDP issuer** textbox, put hello value of **SAML Entity Id** which you copied from **Configure sign-on** section in Azure portal.</span></span>

11. <span data-ttu-id="7973f-182">在 [hello **IDP 登入 URL**文字方塊中，將 hello 值放**SAML SSO 服務 URL**您複製從**設定登入**Azure 入口網站中的區段。</span><span class="sxs-lookup"><span data-stu-id="7973f-182">In hello **IDP Login URL** textbox, put hello value of **SAML SSO Service URL** which you copied from **Configure sign-on** section in Azure portal.</span></span>

12. <span data-ttu-id="7973f-183">選取 [HTTP - 重新導向] 作為 **IDP 繫結**。</span><span class="sxs-lookup"><span data-stu-id="7973f-183">Select **HTTP - Redirect** as **IDP Binding**.</span></span>

13. <span data-ttu-id="7973f-184">選取 [電子郵件地址] 作為**使用者登入設定**。</span><span class="sxs-lookup"><span data-stu-id="7973f-184">Select **Email Address** as **User Login Setting**.</span></span>
 
14. <span data-ttu-id="7973f-185">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="7973f-185">Click **Save** button.</span></span>

15. <span data-ttu-id="7973f-186">hello 儀表板現在會呈現 hello XML **「 下載中繼資料 」**檔案。</span><span class="sxs-lookup"><span data-stu-id="7973f-186">hello dashboard will now present hello XML **"Download Metadata"** file.</span></span> <span data-ttu-id="7973f-187">它包含 Adobe 的 EntityDescriptor URL 和 AssertionConsumerService URL。</span><span class="sxs-lookup"><span data-stu-id="7973f-187">It contains Adobe’s EntityDescriptor URL and AssertionConsumerService URL.</span></span> <span data-ttu-id="7973f-188">請開啟 hello 檔案，並在 hello Azure AD 應用程式中設定它們。</span><span class="sxs-lookup"><span data-stu-id="7973f-188">Please open hello file and configure them in hello Azure AD application.</span></span>

    ![在應用程式端設定單一登入](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_002.png)

    ![在應用程式端設定單一登入](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_003.png)

    <span data-ttu-id="7973f-191">a.</span><span class="sxs-lookup"><span data-stu-id="7973f-191">a.</span></span> <span data-ttu-id="7973f-192">使用 hello EntityDescriptor 值 Adobe 提供您輸入**識別碼**上 hello**設定應用程式設定**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="7973f-192">Use hello EntityDescriptor value Adobe provided you for **Identifier** on hello **Configure App Settings** dialog.</span></span>

    <span data-ttu-id="7973f-193">b.</span><span class="sxs-lookup"><span data-stu-id="7973f-193">b.</span></span> <span data-ttu-id="7973f-194">使用 hello AssertionConsumerService 值 Adobe 提供您輸入**回覆 URL**上 hello**設定應用程式設定**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="7973f-194">Use hello AssertionConsumerService value Adobe provided you for **Reply URL** on hello **Configure App Settings** dialog.</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7973f-195">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7973f-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="7973f-196">hello 本節目標在於 toocreate 呼叫許 Simon hello Azure 管理入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="7973f-196">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="7973f-198">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="7973f-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7973f-199">在 [hello **Azure 管理入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="7973f-199">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7973f-201">跳過**使用者和群組**按一下**所有使用者**toodisplay hello 使用者清單。</span><span class="sxs-lookup"><span data-stu-id="7973f-201">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7973f-203">在 hello hello 對話方塊頂端按一下**新增**tooopen hello**使用者**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="7973f-203">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7973f-205">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="7973f-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7973f-207">a.</span><span class="sxs-lookup"><span data-stu-id="7973f-207">a.</span></span> <span data-ttu-id="7973f-208">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="7973f-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7973f-209">b.</span><span class="sxs-lookup"><span data-stu-id="7973f-209">b.</span></span> <span data-ttu-id="7973f-210">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="7973f-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7973f-211">c.</span><span class="sxs-lookup"><span data-stu-id="7973f-211">c.</span></span> <span data-ttu-id="7973f-212">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="7973f-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7973f-213">d.</span><span class="sxs-lookup"><span data-stu-id="7973f-213">d.</span></span> <span data-ttu-id="7973f-214">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="7973f-214">Click **Create**.</span></span> 

### <a name="creating-an-adobe-creative-cloud-test-user"></a><span data-ttu-id="7973f-215">建立 Adobe Creative Cloud 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7973f-215">Creating an Adobe Creative Cloud test user</span></span>

<span data-ttu-id="7973f-216">在訂單 tooenable Azure AD 使用者 toolog 到 Adobe 創意雲端，您必須是佈建到 Adobe 創意雲端。</span><span class="sxs-lookup"><span data-stu-id="7973f-216">In order tooenable Azure AD users toolog into Adobe Creative Cloud, they must be provisioned into Adobe Creative Cloud.</span></span>  
<span data-ttu-id="7973f-217">在 Adobe 創意雲端的 hello 情況下，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="7973f-217">In hello case of Adobe Creative Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="7973f-218">**tooprovision 使用者帳戶，執行下列步驟 hello:**</span><span class="sxs-lookup"><span data-stu-id="7973f-218">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="7973f-219">登入 tooyour Adobe 創意雲端公司站台系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="7973f-219">Log in tooyour Adobe Creative Cloud company site as an administrator.</span></span>

2. <span data-ttu-id="7973f-220">按一下 [人員] 。</span><span class="sxs-lookup"><span data-stu-id="7973f-220">Click **People**.</span></span>

    <span data-ttu-id="7973f-221">![人員](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "人員")</span><span class="sxs-lookup"><span data-stu-id="7973f-221">![People](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="7973f-222">按一下 [邀請使用者] 。</span><span class="sxs-lookup"><span data-stu-id="7973f-222">Click **Invite User**.</span></span>

    <span data-ttu-id="7973f-223">![邀請使用者](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "邀請使用者")</span><span class="sxs-lookup"><span data-stu-id="7973f-223">![Invite Users](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="7973f-224">在 [hello**邀請人員**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="7973f-224">On hello **Invite People** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="7973f-225">![邀請人員](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "邀請人員")</span><span class="sxs-lookup"><span data-stu-id="7973f-225">![Invite People](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="7973f-226">a.</span><span class="sxs-lookup"><span data-stu-id="7973f-226">a.</span></span> <span data-ttu-id="7973f-227">在 [hello**電子郵件**許 Simon 帳戶類型 hello 電子郵件地址] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="7973f-227">In hello **Email** textbox, type hello email address of Britta Simon account.</span></span>
    
    <span data-ttu-id="7973f-228">b.</span><span class="sxs-lookup"><span data-stu-id="7973f-228">b.</span></span> <span data-ttu-id="7973f-229">按一下 [邀請] 。</span><span class="sxs-lookup"><span data-stu-id="7973f-229">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7973f-230">hello Azure Active Directory 帳戶持有者將收到一封電子郵件，並遵循連結 tooconfirm 他們的帳戶之前就會生效。</span><span class="sxs-lookup"><span data-stu-id="7973f-230">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7973f-231">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="7973f-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7973f-232">在本節中，您可以授與他們存取 tooAdobe 創意雲端啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7973f-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooAdobe Creative Cloud.</span></span>

![指派使用者][200] 

<span data-ttu-id="7973f-234">**tooassign 許 Simon tooAdobe 創意雲端中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="7973f-234">**tooassign Britta Simon tooAdobe Creative Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="7973f-235">在 [hello Azure 管理入口網站中，開啟 [hello 應用程式] 檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="7973f-235">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="7973f-237">在 [hello] 應用程式清單中，選取**Adobe 創意雲端**。</span><span class="sxs-lookup"><span data-stu-id="7973f-237">In hello applications list, select **Adobe Creative Cloud**.</span></span>

    ![設定單一登入](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_50.png) 

3. <span data-ttu-id="7973f-239">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="7973f-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="7973f-241">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7973f-241">Click **Add** button.</span></span> <span data-ttu-id="7973f-242">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="7973f-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="7973f-244">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="7973f-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7973f-245">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7973f-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7973f-246">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7973f-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7973f-247">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="7973f-247">Testing single sign-on</span></span>

<span data-ttu-id="7973f-248">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="7973f-248">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7973f-249">當您按一下 hello Adobe 創意雲端磚 hello 存取面板中的時，您應該取得自動登入 tooyour Adobe 創意雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="7973f-249">When you click hello Adobe Creative Cloud tile in hello Access Panel, you should get automatically signed-on tooyour Adobe Creative Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="7973f-250">其他資源</span><span class="sxs-lookup"><span data-stu-id="7973f-250">Additional resources</span></span>

* [<span data-ttu-id="7973f-251">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7973f-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7973f-252">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="7973f-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_203.png