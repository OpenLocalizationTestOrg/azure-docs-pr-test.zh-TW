---
title: "教學課程：Azure Active Directory 與 Lifesize Cloud 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Lifesize 雲端之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 75fab335-fdcd-4066-b42c-cc738fcb6513
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: ae599907e872571b3220de7122006c7db8db4a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lifesize-cloud"></a><span data-ttu-id="3b496-103">教學課程：Azure Active Directory 與 Lifesize Cloud 整合</span><span class="sxs-lookup"><span data-stu-id="3b496-103">Tutorial: Azure Active Directory integration with Lifesize Cloud</span></span>

<span data-ttu-id="3b496-104">在此教學課程中，您學會如何 toointegrate Lifesize 雲端與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="3b496-104">In this tutorial, you learn how toointegrate Lifesize Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3b496-105">與 Azure AD 整合 Lifesize 雲端可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="3b496-105">Integrating Lifesize Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3b496-106">您可以控制存取 tooLifesize 雲端的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="3b496-106">You can control in Azure AD who has access tooLifesize Cloud</span></span>
- <span data-ttu-id="3b496-107">您可以啟用您的使用者 tooautomatically get 登入 tooLifesize （單一登入） 的雲端與他們的 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="3b496-107">You can enable your users tooautomatically get signed-on tooLifesize Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3b496-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="3b496-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3b496-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="3b496-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b496-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="3b496-110">Prerequisites</span></span>

<span data-ttu-id="3b496-111">tooconfigure 與 Lifesize 雲端的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="3b496-111">tooconfigure Azure AD integration with Lifesize Cloud, you need hello following items:</span></span>

- <span data-ttu-id="3b496-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="3b496-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3b496-113">已啟用 Lifesize Cloud 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="3b496-113">A Lifesize Cloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3b496-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="3b496-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3b496-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="3b496-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3b496-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="3b496-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3b496-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="3b496-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3b496-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="3b496-118">Scenario description</span></span>
<span data-ttu-id="3b496-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3b496-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3b496-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="3b496-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3b496-121">從 hello 圖庫加入 Lifesize 雲端</span><span class="sxs-lookup"><span data-stu-id="3b496-121">Adding Lifesize Cloud from hello gallery</span></span>
2. <span data-ttu-id="3b496-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="3b496-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lifesize-cloud-from-hello-gallery"></a><span data-ttu-id="3b496-123">從 hello 圖庫加入 Lifesize 雲端</span><span class="sxs-lookup"><span data-stu-id="3b496-123">Adding Lifesize Cloud from hello gallery</span></span>
<span data-ttu-id="3b496-124">tooconfigure hello 整合 Lifesize 雲端的 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Lifesize 雲端。</span><span class="sxs-lookup"><span data-stu-id="3b496-124">tooconfigure hello integration of Lifesize Cloud into Azure AD, you need tooadd Lifesize Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3b496-125">**tooadd Lifesize 雲端 hello 圖庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="3b496-125">**tooadd Lifesize Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3b496-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="3b496-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3b496-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="3b496-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3b496-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="3b496-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="3b496-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="3b496-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="3b496-133">在 [hello] 搜尋方塊中，輸入**Lifesize 雲端**。</span><span class="sxs-lookup"><span data-stu-id="3b496-133">In hello search box, type **Lifesize Cloud**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_search.png)

5. <span data-ttu-id="3b496-135">在 hello 結果 窗格中，選取  **Lifesize 雲端**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3b496-135">In hello results panel, select **Lifesize Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3b496-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="3b496-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3b496-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Lifesize Cloud 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3b496-138">In this section, you configure and test Azure AD single sign-on with Lifesize Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3b496-139">單一登入 toowork，Azure AD 需要 tooknow Lifesize 雲端中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="3b496-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lifesize Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="3b496-140">換句話說，Azure AD 使用者與 hello Lifesize 雲端中的相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="3b496-140">In other words, a link relationship between an Azure AD user and hello related user in Lifesize Cloud needs toobe established.</span></span>

<span data-ttu-id="3b496-141">Lifesize 雲端中指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="3b496-141">In Lifesize Cloud, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3b496-142">tooconfigure 和測試 Azure AD 單一登入與 Lifesize 雲端，您需要遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="3b496-142">tooconfigure and test Azure AD single sign-on with Lifesize Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3b496-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="3b496-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3b496-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="3b496-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3b496-145">**[建立測試使用者 Lifesize 雲端](#creating-a-lifesize-cloud-test-user)** -toohave 許 Simon Lifesize 雲端是連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="3b496-145">**[Creating a Lifesize Cloud test user](#creating-a-lifesize-cloud-test-user)** - toohave a counterpart of Britta Simon in Lifesize Cloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3b496-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3b496-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3b496-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="3b496-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3b496-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="3b496-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3b496-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Lifesize 雲端應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="3b496-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lifesize Cloud application.</span></span>

<span data-ttu-id="3b496-150">**tooconfigure Azure AD 單一登入與 Lifesize 雲端中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="3b496-150">**tooconfigure Azure AD single sign-on with Lifesize Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="3b496-151">在 Azure 入口網站上 hello hello **Lifesize 雲端**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="3b496-151">In hello Azure portal, on hello **Lifesize Cloud** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="3b496-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3b496-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_samlbase.png)

3. <span data-ttu-id="3b496-155">在 hello **Lifesize 雲端網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="3b496-155">On hello **Lifesize Cloud Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url.png)

    <span data-ttu-id="3b496-157">a.</span><span class="sxs-lookup"><span data-stu-id="3b496-157">a.</span></span> <span data-ttu-id="3b496-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://login.lifesizecloud.com/ls/?acs`</span><span class="sxs-lookup"><span data-stu-id="3b496-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://login.lifesizecloud.com/ls/?acs`</span></span>

    <span data-ttu-id="3b496-159">b.</span><span class="sxs-lookup"><span data-stu-id="3b496-159">b.</span></span> <span data-ttu-id="3b496-160">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://login.lifesizecloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="3b496-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://login.lifesizecloud.com/<companyname>`</span></span>

     
4. <span data-ttu-id="3b496-161">請檢查**顯示進階的 URL 設定**，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="3b496-161">Check **Show advanced URL settings**, perform hello following step:</span></span>  
   
    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url1.png)

    <span data-ttu-id="3b496-163">在 hello**轉送狀態**文字方塊中，輸入 URL，使用下列模式的 hello:`https://webapp.lifesizecloud.com/?ent=<identifier>`</span><span class="sxs-lookup"><span data-stu-id="3b496-163">In hello **Relay state** textbox, type a URL using hello following pattern: `https://webapp.lifesizecloud.com/?ent=<identifier>`</span></span>
   
   > [!NOTE] 
   ><span data-ttu-id="3b496-164">請注意這些不是 hello 實際值。</span><span class="sxs-lookup"><span data-stu-id="3b496-164">Please note that these are not hello real values.</span></span> <span data-ttu-id="3b496-165">這些值以 hello 有 tooupdate 實際的登入 URL、 轉送狀態和識別項。</span><span class="sxs-lookup"><span data-stu-id="3b496-165">you have tooupdate these values with hello actual Sign-On URL, Relay State, and Identifier.</span></span> <span data-ttu-id="3b496-166">請連絡[Lifesize 雲端的用戶端支援小組](https://www.lifesize.com/support)tooget 登入 URL 和識別碼值與您可以從在 hello 教學課程稍後會說明的 SSO 組態取得轉送的狀態值。</span><span class="sxs-lookup"><span data-stu-id="3b496-166">Contact [Lifesize Cloud Client support team](https://www.lifesize.com/support) tooget Sign-On URL, and Identifier values and you can get Relay State  value from SSO Configuration that is explained later in hello tutorial.</span></span>

4. <span data-ttu-id="3b496-167">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="3b496-167">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_certificate.png) 

5. <span data-ttu-id="3b496-169">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="3b496-169">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3b496-171">在 hello **Lifesize 雲端組態**區段中，按一下**設定 Lifesize 雲端**tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="3b496-171">On hello **Lifesize Cloud Configuration** section, click **Configure Lifesize Cloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="3b496-172">複製 hello **SAML 實體識別碼和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="3b496-172">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_configure.png) 

7. <span data-ttu-id="3b496-174">tooget SSO 設定您的應用程式登入 hello Lifesize 雲端應用程式，以管理員權限。</span><span class="sxs-lookup"><span data-stu-id="3b496-174">tooget SSO configured for your application, login into hello Lifesize Cloud application with Admin privileges.</span></span>

8. <span data-ttu-id="3b496-175">在右下角的 hello 頂端按一下您的名稱，然後按一下 hello**提前設定**。</span><span class="sxs-lookup"><span data-stu-id="3b496-175">In hello top right corner click on your name and then click on hello **Advance Settings**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_06.png)

9. <span data-ttu-id="3b496-177">在 hello 提前設定現在按一下 hello **SSO 組態**連結。</span><span class="sxs-lookup"><span data-stu-id="3b496-177">In hello Advance Settings now click on hello **SSO Configuration** link.</span></span> <span data-ttu-id="3b496-178">它會開啟 hello SSO 組態 頁面上執行個體。</span><span class="sxs-lookup"><span data-stu-id="3b496-178">It will open hello SSO Configuration page for your instance.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_07.png)

10. <span data-ttu-id="3b496-180">現在設定 hello hello SSO 組態 UI 中的值。</span><span class="sxs-lookup"><span data-stu-id="3b496-180">Now configure hello following values in hello SSO configuration UI.</span></span>    
   
    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_08.png)
    
    <span data-ttu-id="3b496-182">a.</span><span class="sxs-lookup"><span data-stu-id="3b496-182">a.</span></span> <span data-ttu-id="3b496-183">在**身分識別提供者簽發者**文字方塊中，貼上 hello 值**SAML 實體識別碼**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="3b496-183">In **Identity Provider Issuer** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3b496-184">b.</span><span class="sxs-lookup"><span data-stu-id="3b496-184">b.</span></span>  <span data-ttu-id="3b496-185">在**登入 URL**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="3b496-185">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3b496-186">c.</span><span class="sxs-lookup"><span data-stu-id="3b496-186">c.</span></span> <span data-ttu-id="3b496-187">從 Azure 入口網站中，複製到剪貼簿，其內容的 hello 下載 [記事本] 中開啟 base-64 編碼的憑證，然後將它貼入 toohello **X.509 憑證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="3b496-187">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox.</span></span>
  
    <span data-ttu-id="3b496-188">d.</span><span class="sxs-lookup"><span data-stu-id="3b496-188">d.</span></span> <span data-ttu-id="3b496-189">在 [hello SAML 屬性對應 hello 第一個名稱] 文字方塊中的輸入 hello 值做為**http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**</span><span class="sxs-lookup"><span data-stu-id="3b496-189">In hello SAML Attribute mappings for hello First Name text box enter hello value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**</span></span>
    
    <span data-ttu-id="3b496-190">e.</span><span class="sxs-lookup"><span data-stu-id="3b496-190">e.</span></span> <span data-ttu-id="3b496-191">在 hello SAML 屬性對應中的 hello**姓氏**文字方塊中，輸入 hello 值做為**http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**</span><span class="sxs-lookup"><span data-stu-id="3b496-191">In hello SAML Attribute mapping for hello **Last Name** text box enter hello value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**</span></span>
    
    <span data-ttu-id="3b496-192">f.</span><span class="sxs-lookup"><span data-stu-id="3b496-192">f.</span></span> <span data-ttu-id="3b496-193">在 hello SAML 屬性對應中的 hello**電子郵件**文字方塊中，輸入 hello 值做為**http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**</span><span class="sxs-lookup"><span data-stu-id="3b496-193">In hello SAML Attribute mapping for hello **Email** text box enter hello value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**</span></span>

11. <span data-ttu-id="3b496-194">您可以按一下 hello toocheck hello 組態**測試** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3b496-194">toocheck hello configuration you can click on hello **Test** button.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="3b496-195">測試成功 toocomplete hello 設定精靈 需要在 Azure AD 中與也提供存取 toousers 或群組，讓他們可以執行 hello 測試。</span><span class="sxs-lookup"><span data-stu-id="3b496-195">For successful testing you need toocomplete hello configuration wizard in Azure AD and also provide access toousers or groups who can perform hello test.</span></span>

12. <span data-ttu-id="3b496-196">藉由檢查 hello 上啟用 hello SSO**啟用 SSO**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="3b496-196">Enable hello SSO by checking on hello **Enable SSO** button.</span></span>

13. <span data-ttu-id="3b496-197">現在按一下 hello**更新**按鈕，使所有 hello 設定會都儲存。</span><span class="sxs-lookup"><span data-stu-id="3b496-197">Now click on hello **Update** button so that all hello settings are saved.</span></span> <span data-ttu-id="3b496-198">這會產生 hello RelayState 值。</span><span class="sxs-lookup"><span data-stu-id="3b496-198">This will generate hello RelayState value.</span></span> <span data-ttu-id="3b496-199">複製 hello RelayState 值，也就產生 hello 文字方塊中，將它貼在 hello**轉送狀態**底下的文字方塊中**Lifesize 雲端網域和 Url** > 一節。</span><span class="sxs-lookup"><span data-stu-id="3b496-199">Copy hello RelayState value, which is generated in hello text box, paste it in hello **Relay State** textbox under **Lifesize Cloud Domain and URLs** section.</span></span> 

> [!TIP]
> <span data-ttu-id="3b496-200">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="3b496-200">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3b496-201">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="3b496-201">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3b496-202">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3b496-202">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3b496-203">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="3b496-203">Creating an Azure AD test user</span></span>

<span data-ttu-id="3b496-204">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="3b496-204">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="3b496-206">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="3b496-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3b496-207">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="3b496-207">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3b496-209">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="3b496-209">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3b496-211">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="3b496-211">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3b496-213">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="3b496-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3b496-215">a.</span><span class="sxs-lookup"><span data-stu-id="3b496-215">a.</span></span> <span data-ttu-id="3b496-216">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="3b496-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3b496-217">b.</span><span class="sxs-lookup"><span data-stu-id="3b496-217">b.</span></span> <span data-ttu-id="3b496-218">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="3b496-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3b496-219">c.</span><span class="sxs-lookup"><span data-stu-id="3b496-219">c.</span></span> <span data-ttu-id="3b496-220">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="3b496-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3b496-221">d.</span><span class="sxs-lookup"><span data-stu-id="3b496-221">d.</span></span> <span data-ttu-id="3b496-222">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="3b496-222">Click **Create**.</span></span>
 
### <a name="creating-a-lifesize-cloud-test-user"></a><span data-ttu-id="3b496-223">建立 Lifesize Cloud 測試使用者</span><span class="sxs-lookup"><span data-stu-id="3b496-223">Creating a Lifesize Cloud test user</span></span>

<span data-ttu-id="3b496-224">在本節中，您要在 Lifesize Cloud 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="3b496-224">In this section, you create a user called Britta Simon in Lifesize Cloud.</span></span> <span data-ttu-id="3b496-225">Lifesize Cloud 支援自動使用者佈建。</span><span class="sxs-lookup"><span data-stu-id="3b496-225">Lifesize cloud does support automatic user provisioning.</span></span> <span data-ttu-id="3b496-226">驗證成功後在 Azure AD，hello 使用者將會自動佈建 hello 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="3b496-226">After successful authentication at Azure AD, hello user will be automatically provisioned in hello application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3b496-227">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="3b496-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3b496-228">在本節中，您可以授與存取 tooLifesize 雲端啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3b496-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLifesize Cloud.</span></span>

![指派使用者][200] 

<span data-ttu-id="3b496-230">**tooassign 許 Simon tooLifesize 雲端中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="3b496-230">**tooassign Britta Simon tooLifesize Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="3b496-231">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="3b496-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="3b496-233">在 [hello] 應用程式清單中，選取**Lifesize 雲端**。</span><span class="sxs-lookup"><span data-stu-id="3b496-233">In hello applications list, select **Lifesize Cloud**.</span></span>

    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_app.png) 

3. <span data-ttu-id="3b496-235">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="3b496-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="3b496-237">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3b496-237">Click **Add** button.</span></span> <span data-ttu-id="3b496-238">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="3b496-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="3b496-240">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="3b496-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3b496-241">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3b496-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3b496-242">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3b496-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3b496-243">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="3b496-243">Testing single sign-on</span></span>

<span data-ttu-id="3b496-244">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="3b496-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3b496-245">當您按一下的 hello Lifesize 雲端磚 hello 存取面板中時，您應該取得 Lifesize 雲端應用程式的登入頁面。</span><span class="sxs-lookup"><span data-stu-id="3b496-245">When you click hello Lifesize Cloud tile in hello Access Panel, you should get login page of Lifesize Cloud application.</span></span>
<span data-ttu-id="3b496-246">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="3b496-246">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3b496-247">其他資源</span><span class="sxs-lookup"><span data-stu-id="3b496-247">Additional resources</span></span>

* [<span data-ttu-id="3b496-248">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3b496-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3b496-249">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="3b496-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_203.png

