---
title: "教學課程：Azure Active Directory 與 UNIFI 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 UNIFI 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e1f49ee4-d2d4-4a82-9baf-0587ca1f20f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: af7cc1167b5c0cff2a1f4cdaa8a2b93f5a718f81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-unifi"></a><span data-ttu-id="c04e8-103">教學課程：Azure Active Directory 與 UNIFI 整合</span><span class="sxs-lookup"><span data-stu-id="c04e8-103">Tutorial: Azure Active Directory integration with UNIFI</span></span>

<span data-ttu-id="c04e8-104">在此教學課程中，您學會如何 toointegrate UNIFI 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="c04e8-104">In this tutorial, you learn how toointegrate UNIFI with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c04e8-105">與 Azure AD 整合 UNIFI 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="c04e8-105">Integrating UNIFI with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c04e8-106">您可以控制存取 tooUNIFI Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="c04e8-106">You can control in Azure AD who has access tooUNIFI</span></span>
- <span data-ttu-id="c04e8-107">您可以啟用您的使用者 tooautomatically get 登入 tooUNIFI （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="c04e8-107">You can enable your users tooautomatically get signed-on tooUNIFI (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c04e8-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="c04e8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c04e8-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="c04e8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c04e8-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="c04e8-110">Prerequisites</span></span>

<span data-ttu-id="c04e8-111">tooconfigure UNIFI 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="c04e8-111">tooconfigure Azure AD integration with UNIFI, you need hello following items:</span></span>

- <span data-ttu-id="c04e8-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="c04e8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c04e8-113">已啟用 UNIFI 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="c04e8-113">A UNIFI single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c04e8-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="c04e8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c04e8-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="c04e8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c04e8-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="c04e8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c04e8-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="c04e8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c04e8-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="c04e8-118">Scenario description</span></span>
<span data-ttu-id="c04e8-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c04e8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c04e8-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="c04e8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c04e8-121">從 hello 圖庫加入 UNIFI</span><span class="sxs-lookup"><span data-stu-id="c04e8-121">Adding UNIFI from hello gallery</span></span>
2. <span data-ttu-id="c04e8-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c04e8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-unifi-from-hello-gallery"></a><span data-ttu-id="c04e8-123">從 hello 圖庫加入 UNIFI</span><span class="sxs-lookup"><span data-stu-id="c04e8-123">Adding UNIFI from hello gallery</span></span>
<span data-ttu-id="c04e8-124">tooconfigure hello 整合 UNIFI 到 Azure AD，您需要 tooadd UNIFI hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c04e8-124">tooconfigure hello integration of UNIFI into Azure AD, you need tooadd UNIFI from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c04e8-125">**tooadd UNIFI 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="c04e8-125">**tooadd UNIFI from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c04e8-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="c04e8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c04e8-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="c04e8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c04e8-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="c04e8-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="c04e8-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="c04e8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="c04e8-133">在 [hello] 搜尋方塊中，輸入**UNIFI**。</span><span class="sxs-lookup"><span data-stu-id="c04e8-133">In hello search box, type **UNIFI**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_search.png)

5. <span data-ttu-id="c04e8-135">在 hello 結果 窗格中，選取  **UNIFI**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c04e8-135">In hello results panel, select **UNIFI**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c04e8-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c04e8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c04e8-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 UNIFI 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c04e8-138">In this section, you configure and test Azure AD single sign-on with UNIFI based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c04e8-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 UNIFI 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="c04e8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in UNIFI is tooa user in Azure AD.</span></span> <span data-ttu-id="c04e8-140">換句話說，Azure AD 使用者與 hello UNIFI 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="c04e8-140">In other words, a link relationship between an Azure AD user and hello related user in UNIFI needs toobe established.</span></span>

<span data-ttu-id="c04e8-141">UNIFI 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="c04e8-141">In UNIFI, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c04e8-142">tooconfigure 及 UNIFI 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="c04e8-142">tooconfigure and test Azure AD single sign-on with UNIFI, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c04e8-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="c04e8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c04e8-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="c04e8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c04e8-145">**[建立 UNIFI 測試使用者](#creating-a-unifi-test-user)** -toohave 許 Simon UNIFI 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="c04e8-145">**[Creating a UNIFI test user](#creating-a-unifi-test-user)** - toohave a counterpart of Britta Simon in UNIFI that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c04e8-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c04e8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c04e8-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="c04e8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c04e8-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c04e8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c04e8-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 UNIFI 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="c04e8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your UNIFI application.</span></span>

<span data-ttu-id="c04e8-150">**tooconfigure Azure AD 單一登入與 UNIFI，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="c04e8-150">**tooconfigure Azure AD single sign-on with UNIFI, perform hello following steps:**</span></span>

1. <span data-ttu-id="c04e8-151">在 Azure 入口網站上 hello hello **UNIFI**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="c04e8-151">In hello Azure portal, on hello **UNIFI** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="c04e8-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c04e8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_samlbase.png)

3. <span data-ttu-id="c04e8-155">在 hello **UNIFI 網域和 Url**區段中，如果您想 tooconfigure hello 應用程式中的**IDP**初始模式：</span><span class="sxs-lookup"><span data-stu-id="c04e8-155">On hello **UNIFI Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_url1.png)

    <span data-ttu-id="c04e8-157">在 hello**識別碼**文字方塊中，類型 hello 值：`INVIEWlabs`</span><span class="sxs-lookup"><span data-stu-id="c04e8-157">In hello **Identifier** textbox, type hello value: `INVIEWlabs`</span></span> 

4. <span data-ttu-id="c04e8-158">請檢查**顯示進階的 URL 設定**，如果您想 tooconfigure hello 應用程式中的**SP**初始模式：</span><span class="sxs-lookup"><span data-stu-id="c04e8-158">Check **Show advanced URL settings**, If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_url2.png)

    <span data-ttu-id="c04e8-160">在 hello**登入 URL**文字方塊中，型別 hello URL:`https://app.discoverunifi.com/login`</span><span class="sxs-lookup"><span data-stu-id="c04e8-160">In hello **Sign-on URL** textbox, type hello URL: `https://app.discoverunifi.com/login`</span></span>

5. <span data-ttu-id="c04e8-161">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="c04e8-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_certificate.png) 

6. <span data-ttu-id="c04e8-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="c04e8-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-unifi-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="c04e8-165">在 hello **UNIFI 組態**區段中，按一下**設定 UNIFI** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="c04e8-165">On hello **UNIFI Configuration** section, click **Configure UNIFI** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c04e8-166">複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="c04e8-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_configure.png)

8. <span data-ttu-id="c04e8-168">在不同的網頁瀏覽器視窗中，登入 tooyour **UNIFI**以系統管理員身分的公司網站。</span><span class="sxs-lookup"><span data-stu-id="c04e8-168">In a different web browser window, sign on tooyour **UNIFI** company site as administrator.</span></span>

9. <span data-ttu-id="c04e8-169">按一下 hello**使用者**。</span><span class="sxs-lookup"><span data-stu-id="c04e8-169">Click on hello **Users**.</span></span>

    ![設定單一登入](./media/active-directory-saas-unifi-tutorial/app1.png) 

10. <span data-ttu-id="c04e8-171">按一下 hello**新增身分識別提供者**。</span><span class="sxs-lookup"><span data-stu-id="c04e8-171">Click on hello **Add New Identity Provider**.</span></span>

    ![設定單一登入](./media/active-directory-saas-unifi-tutorial/app2.png)

11. <span data-ttu-id="c04e8-173">在 hello**新增身分識別提供者**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="c04e8-173">In hello **Add Identity Provider** section, perform hello following steps:</span></span>   

    ![設定單一登入](./media/active-directory-saas-unifi-tutorial/app3.png) 

    <span data-ttu-id="c04e8-175">a.</span><span class="sxs-lookup"><span data-stu-id="c04e8-175">a.</span></span> <span data-ttu-id="c04e8-176">在 hello**提供者名稱**文字方塊中，型別 hello hello 身分識別提供者名稱...</span><span class="sxs-lookup"><span data-stu-id="c04e8-176">In hello **Provider Name** textbox, type hello name of hello Identity Provider..</span></span>

    <span data-ttu-id="c04e8-177">b.</span><span class="sxs-lookup"><span data-stu-id="c04e8-177">b.</span></span> <span data-ttu-id="c04e8-178">在 hello hello**提供者 URL**文字方塊中貼上 hello **SAML 單一登入服務 URL**您從 Azure 入口網站複製的值。</span><span class="sxs-lookup"><span data-stu-id="c04e8-178">In hello hello **Provider URL** textbox paste hello **SAML Single Sign-On Service URL** value, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="c04e8-179">c.</span><span class="sxs-lookup"><span data-stu-id="c04e8-179">c.</span></span> <span data-ttu-id="c04e8-180">開啟 hello hello Azure 入口網站，在記事本中，從網站下載的憑證移除 hello **---BEGIN CERTIFICATE---**和**---憑證結尾---**標記，然後貼上剩餘的內容中的 hellohello**憑證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="c04e8-180">Open hello Certificate that you have downloaded from hello Azure portal in notepad, remove hello **---BEGIN CERTIFICATE---** and **---END CERTIFICATE---** tag and then paste hello remaining content in hello **Certificate** textbox.</span></span>

    <span data-ttu-id="c04e8-181">d.</span><span class="sxs-lookup"><span data-stu-id="c04e8-181">d.</span></span> <span data-ttu-id="c04e8-182">選取 hello**是預設提供者**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="c04e8-182">Select hello **is Default Provider** checkbox.</span></span>

> [!TIP]
> <span data-ttu-id="c04e8-183">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="c04e8-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c04e8-184">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="c04e8-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c04e8-185">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c04e8-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c04e8-186">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="c04e8-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="c04e8-187">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="c04e8-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="c04e8-189">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="c04e8-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c04e8-190">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="c04e8-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-unifi-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c04e8-192">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="c04e8-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-unifi-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c04e8-194">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="c04e8-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-unifi-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c04e8-196">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="c04e8-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-unifi-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c04e8-198">a.</span><span class="sxs-lookup"><span data-stu-id="c04e8-198">a.</span></span> <span data-ttu-id="c04e8-199">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="c04e8-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c04e8-200">b.</span><span class="sxs-lookup"><span data-stu-id="c04e8-200">b.</span></span> <span data-ttu-id="c04e8-201">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="c04e8-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c04e8-202">c.</span><span class="sxs-lookup"><span data-stu-id="c04e8-202">c.</span></span> <span data-ttu-id="c04e8-203">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="c04e8-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c04e8-204">d.</span><span class="sxs-lookup"><span data-stu-id="c04e8-204">d.</span></span> <span data-ttu-id="c04e8-205">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="c04e8-205">Click **Create**.</span></span>
 
### <a name="creating-a-unifi-test-user"></a><span data-ttu-id="c04e8-206">建立 UNIFI 測試使用者</span><span class="sxs-lookup"><span data-stu-id="c04e8-206">Creating a UNIFI test user</span></span>

<span data-ttu-id="c04e8-207">在本節中，您會建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="c04e8-207">In this section, you create a user called Britta Simon.</span></span> <span data-ttu-id="c04e8-208">**UNIFI** 支援自動使用者佈建，因此不不需要任何手動步驟。</span><span class="sxs-lookup"><span data-stu-id="c04e8-208">**UNIFI** supports automatic user provisioning so no manual steps are required.</span></span> <span data-ttu-id="c04e8-209">使用者會自動建立從 hello Azure AD 成功驗證之後。</span><span class="sxs-lookup"><span data-stu-id="c04e8-209">Users are created automatically after successful authentication from hello Azure AD.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c04e8-210">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="c04e8-210">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c04e8-211">在本節中，您可以授與存取 tooUNIFI 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c04e8-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooUNIFI.</span></span>

![指派使用者][200] 

<span data-ttu-id="c04e8-213">**tooassign 許 Simon tooUNIFI，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="c04e8-213">**tooassign Britta Simon tooUNIFI, perform hello following steps:**</span></span>

1. <span data-ttu-id="c04e8-214">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="c04e8-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="c04e8-216">在 [hello] 應用程式清單中，選取**UNIFI**。</span><span class="sxs-lookup"><span data-stu-id="c04e8-216">In hello applications list, select **UNIFI**.</span></span>

    ![設定單一登入](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_app.png) 

3. <span data-ttu-id="c04e8-218">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="c04e8-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="c04e8-220">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c04e8-220">Click **Add** button.</span></span> <span data-ttu-id="c04e8-221">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="c04e8-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="c04e8-223">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="c04e8-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c04e8-224">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c04e8-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c04e8-225">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c04e8-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c04e8-226">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="c04e8-226">Testing single sign-on</span></span>

<span data-ttu-id="c04e8-227">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="c04e8-227">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c04e8-228">當您按一下的 hello UNIFI 磚 hello 存取面板中時，您應該取得自動登入 tooyour UNIFI 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c04e8-228">When you click hello UNIFI tile in hello Access Panel, you should get automatically signed-on tooyour UNIFI application.</span></span>
<span data-ttu-id="c04e8-229">如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="c04e8-229">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c04e8-230">其他資源</span><span class="sxs-lookup"><span data-stu-id="c04e8-230">Additional resources</span></span>

* [<span data-ttu-id="c04e8-231">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c04e8-231">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c04e8-232">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="c04e8-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_203.png

