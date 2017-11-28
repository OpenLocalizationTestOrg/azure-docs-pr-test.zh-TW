---
title: "教學課程：Azure Active Directory 與 HappyFox 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 HappyFox 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8204ee77-f64b-4fac-b64a-25ea534feac0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jeedes
ms.openlocfilehash: 1190652d7d1144c7eddea339cb3f9175912407fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-happyfox"></a><span data-ttu-id="7ef68-103">教學課程：Azure Active Directory 與 HappyFox 整合</span><span class="sxs-lookup"><span data-stu-id="7ef68-103">Tutorial: Azure Active Directory integration with HappyFox</span></span>

<span data-ttu-id="7ef68-104">在此教學課程中，您學會如何 toointegrate HappyFox 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="7ef68-104">In this tutorial, you learn how toointegrate HappyFox with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7ef68-105">與 Azure AD 整合 HappyFox 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="7ef68-105">Integrating HappyFox with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7ef68-106">您可以控制存取 tooHappyFox Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="7ef68-106">You can control in Azure AD who has access tooHappyFox</span></span>
- <span data-ttu-id="7ef68-107">您可以啟用您的使用者 tooautomatically get 登入 tooHappyFox （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="7ef68-107">You can enable your users tooautomatically get signed-on tooHappyFox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7ef68-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="7ef68-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7ef68-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="7ef68-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ef68-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="7ef68-110">Prerequisites</span></span>

<span data-ttu-id="7ef68-111">tooconfigure HappyFox 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="7ef68-111">tooconfigure Azure AD integration with HappyFox, you need hello following items:</span></span>

- <span data-ttu-id="7ef68-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7ef68-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7ef68-113">啟用 HappyFox 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7ef68-113">A HappyFox single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7ef68-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="7ef68-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7ef68-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="7ef68-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7ef68-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="7ef68-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7ef68-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="7ef68-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7ef68-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="7ef68-118">Scenario description</span></span>
<span data-ttu-id="7ef68-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7ef68-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7ef68-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="7ef68-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7ef68-121">從 hello 圖庫加入 HappyFox</span><span class="sxs-lookup"><span data-stu-id="7ef68-121">Adding HappyFox from hello gallery</span></span>
2. <span data-ttu-id="7ef68-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7ef68-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-happyfox-from-hello-gallery"></a><span data-ttu-id="7ef68-123">從 hello 圖庫加入 HappyFox</span><span class="sxs-lookup"><span data-stu-id="7ef68-123">Adding HappyFox from hello gallery</span></span>
<span data-ttu-id="7ef68-124">tooconfigure hello 整合 HappyFox 到 Azure AD，您需要 tooadd HappyFox hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ef68-124">tooconfigure hello integration of HappyFox into Azure AD, you need tooadd HappyFox from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7ef68-125">**tooadd HappyFox 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="7ef68-125">**tooadd HappyFox from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7ef68-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="7ef68-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7ef68-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="7ef68-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7ef68-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="7ef68-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="7ef68-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="7ef68-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="7ef68-133">在 [hello] 搜尋方塊中，輸入**HappyFox**。</span><span class="sxs-lookup"><span data-stu-id="7ef68-133">In hello search box, type **HappyFox**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_search.png)

5. <span data-ttu-id="7ef68-135">在 hello 結果 窗格中，選取  **HappyFox**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ef68-135">In hello results panel, select **HappyFox**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7ef68-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7ef68-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7ef68-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 HappyFox 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7ef68-138">In this section, you configure and test Azure AD single sign-on with HappyFox based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7ef68-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 HappyFox 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="7ef68-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in HappyFox is tooa user in Azure AD.</span></span> <span data-ttu-id="7ef68-140">換句話說，Azure AD 使用者與 hello HappyFox 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="7ef68-140">In other words, a link relationship between an Azure AD user and hello related user in HappyFox needs toobe established.</span></span>

<span data-ttu-id="7ef68-141">HappyFox 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="7ef68-141">In HappyFox, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7ef68-142">tooconfigure 及 HappyFox 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="7ef68-142">tooconfigure and test Azure AD single sign-on with HappyFox, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7ef68-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="7ef68-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7ef68-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="7ef68-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7ef68-145">**[建立測試使用者 HappyFox](#creating-a-happyfox-test-user)**  -toohave 許 Simon HappyFox 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="7ef68-145">**[Creating a HappyFox test user](#creating-a-happyfox-test-user)** - toohave a counterpart of Britta Simon in HappyFox that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7ef68-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7ef68-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7ef68-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="7ef68-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7ef68-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7ef68-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7ef68-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 HappyFox 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="7ef68-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your HappyFox application.</span></span>

<span data-ttu-id="7ef68-150">**tooconfigure Azure AD 單一登入與 HappyFox，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="7ef68-150">**tooconfigure Azure AD single sign-on with HappyFox, perform hello following steps:**</span></span>

1. <span data-ttu-id="7ef68-151">在 Azure 入口網站上 hello hello **HappyFox**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="7ef68-151">In hello Azure portal, on hello **HappyFox** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="7ef68-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7ef68-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_samlbase.png)

3. <span data-ttu-id="7ef68-155">在 hello **HappyFox 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="7ef68-155">On hello **HappyFox Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_url.png)

    <span data-ttu-id="7ef68-157">a.</span><span class="sxs-lookup"><span data-stu-id="7ef68-157">a.</span></span> <span data-ttu-id="7ef68-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.happyfox.com/`</span><span class="sxs-lookup"><span data-stu-id="7ef68-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.happyfox.com/`</span></span>

    <span data-ttu-id="7ef68-159">b.</span><span class="sxs-lookup"><span data-stu-id="7ef68-159">b.</span></span> <span data-ttu-id="7ef68-160">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.happyfox.com/saml/metadata/`</span><span class="sxs-lookup"><span data-stu-id="7ef68-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.happyfox.com/saml/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7ef68-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="7ef68-161">These values are not real.</span></span> <span data-ttu-id="7ef68-162">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="7ef68-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="7ef68-163">請連絡[HappyFox 用戶端支援小組](https://support.happyfox.com/home)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="7ef68-163">Contact [HappyFox Client support team](https://support.happyfox.com/home) tooget these values.</span></span> 
 
4. <span data-ttu-id="7ef68-164">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="7ef68-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello Certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_certificate.png) 

5. <span data-ttu-id="7ef68-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="7ef68-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-happyfox-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7ef68-168">在 hello **HappyFox 組態**區段中，按一下**設定 HappyFox** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="7ef68-168">On hello **HappyFox Configuration** section, click **Configure HappyFox** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7ef68-169">複製 hello **SAML 單一登入服務 URL**從 hello**快速參考章節**。</span><span class="sxs-lookup"><span data-stu-id="7ef68-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section**.</span></span>

    ![設定單一登入](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_configure.png) 

7. <span data-ttu-id="7ef68-171">登入 tooyour HappyFox 人員入口網站並瀏覽過**管理**，按一下**整合** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="7ef68-171">Sign on tooyour HappyFox staff portal and navigate too**Manage**, Click on **Integrations** tab.</span></span>

    ![設定單一登入](./media/active-directory-saas-happyfox-tutorial/header.png) 

8. <span data-ttu-id="7ef68-173">在 hello 整合索引標籤上，按一下 **設定**下**SAML 整合**tooopen hello 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="7ef68-173">In hello Integrations tab, Click **Configure** under **SAML Integration** tooopen hello Single Sign On Settings.</span></span>

    ![設定單一登入](./media/active-directory-saas-happyfox-tutorial/configure.png) 

9. <span data-ttu-id="7ef68-175">在 [SAML 組態] 區段中，貼上 hello **SAML 單一登入服務 URL**從 Azure 入口網站將複製的**SSO 目標 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="7ef68-175">Inside SAML configuration section, paste hello **SAML Single Sign-On Service URL** that you have copied from Azure portal into **SSO Target URL** textbox.</span></span>

    ![設定單一登入](./media/active-directory-saas-happyfox-tutorial/targeturl.png)

10. <span data-ttu-id="7ef68-177">開啟 hello 從 [記事本] 中的 Azure 入口網站下載的憑證，並將其內容中的**IdP 簽章**> 一節。</span><span class="sxs-lookup"><span data-stu-id="7ef68-177">Open hello certificate downloaded from Azure portal in notepad and paste its content in **IdP Signature** section.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-happyfox-tutorial/cert.png)

11. <span data-ttu-id="7ef68-179">按一下 [儲存設定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7ef68-179">Click **Save Settings** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-happyfox-tutorial/savesettings.png)

> [!TIP]
> <span data-ttu-id="7ef68-181">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="7ef68-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7ef68-182">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="7ef68-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7ef68-183">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7ef68-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7ef68-184">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7ef68-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="7ef68-185">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="7ef68-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="7ef68-187">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="7ef68-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7ef68-188">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="7ef68-188">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-happyfox-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7ef68-190">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="7ef68-190">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-happyfox-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7ef68-192">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="7ef68-192">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-happyfox-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7ef68-194">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="7ef68-194">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-happyfox-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7ef68-196">a.</span><span class="sxs-lookup"><span data-stu-id="7ef68-196">a.</span></span> <span data-ttu-id="7ef68-197">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="7ef68-197">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7ef68-198">b.</span><span class="sxs-lookup"><span data-stu-id="7ef68-198">b.</span></span> <span data-ttu-id="7ef68-199">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="7ef68-199">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7ef68-200">c.</span><span class="sxs-lookup"><span data-stu-id="7ef68-200">c.</span></span> <span data-ttu-id="7ef68-201">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="7ef68-201">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7ef68-202">d.</span><span class="sxs-lookup"><span data-stu-id="7ef68-202">d.</span></span> <span data-ttu-id="7ef68-203">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="7ef68-203">Click **Create**.</span></span>
 
### <a name="creating-a-happyfox-test-user"></a><span data-ttu-id="7ef68-204">建立 HappyFox 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7ef68-204">Creating a HappyFox test user</span></span>

<span data-ttu-id="7ef68-205">應用程式支援恰好在即時使用者佈建，以及之後驗證使用者會自動建立 hello 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="7ef68-205">Application supports Just in time user provisioning and after authentication users are created in hello application automatically.</span></span>
        
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7ef68-206">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="7ef68-206">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7ef68-207">在本節中，您可以授與存取 tooHappyFox 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7ef68-207">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHappyFox.</span></span>

![指派使用者][200] 

<span data-ttu-id="7ef68-209">**tooassign 許 Simon tooHappyFox，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="7ef68-209">**tooassign Britta Simon tooHappyFox, perform hello following steps:**</span></span>

1. <span data-ttu-id="7ef68-210">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="7ef68-210">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="7ef68-212">在 [hello] 應用程式清單中，選取**HappyFox**。</span><span class="sxs-lookup"><span data-stu-id="7ef68-212">In hello applications list, select **HappyFox**.</span></span>

    ![設定單一登入](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_app.png) 

3. <span data-ttu-id="7ef68-214">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="7ef68-214">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="7ef68-216">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7ef68-216">Click **Add** button.</span></span> <span data-ttu-id="7ef68-217">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="7ef68-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="7ef68-219">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="7ef68-219">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7ef68-220">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7ef68-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7ef68-221">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7ef68-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7ef68-222">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="7ef68-222">Testing single sign-on</span></span>

<span data-ttu-id="7ef68-223">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="7ef68-223">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

1. <span data-ttu-id="7ef68-224">當您按一下 hello HappyFox 磚 hello 存取面板中的時，您應該取得 HappyFox 應用程式的登入頁面。</span><span class="sxs-lookup"><span data-stu-id="7ef68-224">When you click hello HappyFox tile in hello Access Panel, you should get login page of HappyFox application.</span></span> <span data-ttu-id="7ef68-225">您應該會看見 hello **'SAML'** hello 登入頁面上的按鈕。</span><span class="sxs-lookup"><span data-stu-id="7ef68-225">You should see hello **‘SAML’** button on hello sign-in page.</span></span>

    ![外掛程式](./media/active-directory-saas-happyfox-tutorial/saml.png) 

2. <span data-ttu-id="7ef68-227">按一下 hello **'SAML'**按鈕 toolog tooHappyFox 使用 Azure AD 帳戶中的。</span><span class="sxs-lookup"><span data-stu-id="7ef68-227">Click hello **‘SAML’** button toolog in tooHappyFox using your Azure AD account.</span></span>

<span data-ttu-id="7ef68-228">如需 hello 存取面板的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="7ef68-228">For more information about hello Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7ef68-229">其他資源</span><span class="sxs-lookup"><span data-stu-id="7ef68-229">Additional resources</span></span>

* [<span data-ttu-id="7ef68-230">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7ef68-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7ef68-231">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="7ef68-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_203.png

