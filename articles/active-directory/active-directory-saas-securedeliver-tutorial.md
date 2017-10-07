---
title: "教學課程：Azure Active Directory 與 SECURE DELIVER 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 和安全傳遞之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fccd5668-fe6f-4e6d-a9ce-ba4f321c33d1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 13699a9abb8be24054b0810a8178cd5ef170c338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-secure-deliver"></a><span data-ttu-id="23883-103">教學課程：Azure Active Directory 與 SECURE DELIVER 整合</span><span class="sxs-lookup"><span data-stu-id="23883-103">Tutorial: Azure Active Directory integration with SECURE DELIVER</span></span>

<span data-ttu-id="23883-104">在本教學課程中，您學習如何保護 toointegrate 與 Azure Active Directory (Azure AD) 的傳遞。</span><span class="sxs-lookup"><span data-stu-id="23883-104">In this tutorial, you learn how toointegrate SECURE DELIVER with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="23883-105">整合與 Azure AD 的安全傳遞可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="23883-105">Integrating SECURE DELIVER with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="23883-106">您可以控制存取 tooSECURE 傳遞 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="23883-106">You can control in Azure AD who has access tooSECURE DELIVER</span></span>
- <span data-ttu-id="23883-107">您可以啟用您的使用者 tooautomatically get 登入 tooSECURE （單一登入） 的傳遞與他們的 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="23883-107">You can enable your users tooautomatically get signed-on tooSECURE DELIVER (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="23883-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="23883-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="23883-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="23883-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="23883-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="23883-110">Prerequisites</span></span>

<span data-ttu-id="23883-111">tooconfigure 與安全傳遞的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="23883-111">tooconfigure Azure AD integration with SECURE DELIVER, you need hello following items:</span></span>

- <span data-ttu-id="23883-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="23883-112">An Azure AD subscription</span></span>
- <span data-ttu-id="23883-113">已啟用 SECURE DELIVER 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="23883-113">A SECURE DELIVER single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="23883-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="23883-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="23883-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="23883-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="23883-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="23883-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="23883-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="23883-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="23883-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="23883-118">Scenario description</span></span>
<span data-ttu-id="23883-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="23883-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="23883-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="23883-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="23883-121">從 hello 組件庫中加入 安全傳遞</span><span class="sxs-lookup"><span data-stu-id="23883-121">Adding SECURE DELIVER from hello gallery</span></span>
2. <span data-ttu-id="23883-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="23883-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-secure-deliver-from-hello-gallery"></a><span data-ttu-id="23883-123">從 hello 組件庫中加入 安全傳遞</span><span class="sxs-lookup"><span data-stu-id="23883-123">Adding SECURE DELIVER from hello gallery</span></span>
<span data-ttu-id="23883-124">tooconfigure hello 整合安全傳送至 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd 安全傳遞。</span><span class="sxs-lookup"><span data-stu-id="23883-124">tooconfigure hello integration of SECURE DELIVER into Azure AD, you need tooadd SECURE DELIVER from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="23883-125">**tooadd 安全傳送 hello 圖庫中，從執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="23883-125">**tooadd SECURE DELIVER from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="23883-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="23883-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="23883-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="23883-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="23883-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="23883-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="23883-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="23883-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="23883-133">在 [hello] 搜尋方塊中，輸入**安全傳遞**。</span><span class="sxs-lookup"><span data-stu-id="23883-133">In hello search box, type **SECURE DELIVER**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_search.png)

5. <span data-ttu-id="23883-135">在 hello 結果 窗格中，選取 **安全傳遞**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="23883-135">In hello results panel, select **SECURE DELIVER**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="23883-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="23883-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="23883-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 SECURE DELIVER 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="23883-138">In this section, you configure and test Azure AD single sign-on with SECURE DELIVER based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="23883-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在安全傳遞是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="23883-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SECURE DELIVER is tooa user in Azure AD.</span></span> <span data-ttu-id="23883-140">換句話說，Azure AD 使用者與 hello 中安全傳遞相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="23883-140">In other words, a link relationship between an Azure AD user and hello related user in SECURE DELIVER needs toobe established.</span></span>

<span data-ttu-id="23883-141">在安全傳遞，將指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="23883-141">In SECURE DELIVER, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="23883-142">tooconfigure 及測試 Azure AD 單一登入與安全傳遞，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="23883-142">tooconfigure and test Azure AD single sign-on with SECURE DELIVER, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="23883-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="23883-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="23883-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="23883-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="23883-145">**[建立測試使用者安全傳遞](#creating-a-secure-deliver-test-user)** -toohave 許 Simon 中安全傳遞連結的 toohello Azure AD 使用者表示法的對應項目。</span><span class="sxs-lookup"><span data-stu-id="23883-145">**[Creating a SECURE DELIVER test user](#creating-a-secure-deliver-test-user)** - toohave a counterpart of Britta Simon in SECURE DELIVER that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="23883-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="23883-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="23883-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="23883-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="23883-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="23883-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="23883-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並安全傳遞應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="23883-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SECURE DELIVER application.</span></span>

<span data-ttu-id="23883-150">**tooconfigure Azure AD 單一登入與安全傳遞，請執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="23883-150">**tooconfigure Azure AD single sign-on with SECURE DELIVER, perform hello following steps:**</span></span>

1. <span data-ttu-id="23883-151">在 Azure 入口網站上 hello hello**安全傳遞**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="23883-151">In hello Azure portal, on hello **SECURE DELIVER** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="23883-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="23883-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_samlbase.png)

3. <span data-ttu-id="23883-155">在 hello**安全傳遞網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="23883-155">On hello **SECURE DELIVER Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_url.png)

    <span data-ttu-id="23883-157">a.</span><span class="sxs-lookup"><span data-stu-id="23883-157">a.</span></span> <span data-ttu-id="23883-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.i-securedeliver.jp/sd/<tenantname>/jsf/login/sso`</span><span class="sxs-lookup"><span data-stu-id="23883-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.i-securedeliver.jp/sd/<tenantname>/jsf/login/sso`</span></span>

    <span data-ttu-id="23883-159">b.</span><span class="sxs-lookup"><span data-stu-id="23883-159">b.</span></span> <span data-ttu-id="23883-160">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.i-securedeliver.jp/sd/<tenantname>/postResponse`</span><span class="sxs-lookup"><span data-stu-id="23883-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.i-securedeliver.jp/sd/<tenantname>/postResponse`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="23883-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="23883-161">These values are not real.</span></span> <span data-ttu-id="23883-162">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="23883-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="23883-163">請連絡[安全傳遞用戶端支援小組](mailto:iw-sd-support@fujifilm.com)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="23883-163">Contact [SECURE DELIVER Client support team](mailto:iw-sd-support@fujifilm.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="23883-164">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="23883-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_certificate.png) 

5. <span data-ttu-id="23883-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="23883-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-securedeliver-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="23883-168">在 hello**安全傳遞組態**區段中，按一下**設定安全傳遞**tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="23883-168">On hello **SECURE DELIVER Configuration** section, click **Configure SECURE DELIVER** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="23883-169">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="23883-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_configure.png) 

7. <span data-ttu-id="23883-171">tooconfigure 單一登入上**安全傳遞**端，您需要下載 toosend hello**憑證 (Base64)**，**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**太[安全傳遞支援小組](mailto:iw-sd-support@fujifilm.com)。</span><span class="sxs-lookup"><span data-stu-id="23883-171">tooconfigure single sign-on on **SECURE DELIVER** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[SECURE DELIVER support team](mailto:iw-sd-support@fujifilm.com).</span></span> <span data-ttu-id="23883-172">設定此設定 toohave hello SAML SSO 連線兩端上正確設定這些欄位。</span><span class="sxs-lookup"><span data-stu-id="23883-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="23883-173">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="23883-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="23883-174">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="23883-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="23883-175">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="23883-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="23883-176">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="23883-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="23883-177">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="23883-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="23883-179">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="23883-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="23883-180">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="23883-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-securedeliver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="23883-182">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="23883-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-securedeliver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="23883-184">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="23883-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-securedeliver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="23883-186">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="23883-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-securedeliver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="23883-188">a.</span><span class="sxs-lookup"><span data-stu-id="23883-188">a.</span></span> <span data-ttu-id="23883-189">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="23883-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="23883-190">b.</span><span class="sxs-lookup"><span data-stu-id="23883-190">b.</span></span> <span data-ttu-id="23883-191">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="23883-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="23883-192">c.</span><span class="sxs-lookup"><span data-stu-id="23883-192">c.</span></span> <span data-ttu-id="23883-193">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="23883-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="23883-194">d.</span><span class="sxs-lookup"><span data-stu-id="23883-194">d.</span></span> <span data-ttu-id="23883-195">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="23883-195">Click **Create**.</span></span>
 
### <a name="creating-a-secure-deliver-test-user"></a><span data-ttu-id="23883-196">建立 SECURE DELIVER 測試使用者</span><span class="sxs-lookup"><span data-stu-id="23883-196">Creating a SECURE DELIVER test user</span></span>

<span data-ttu-id="23883-197">hello 本節目標在於 toocreate 呼叫許 Simon 安全傳遞的使用者。</span><span class="sxs-lookup"><span data-stu-id="23883-197">hello objective of this section is toocreate a user called Britta Simon in SECURE DELIVER.</span></span> <span data-ttu-id="23883-198">使用[安全傳遞支援小組](mailto:iw-sd-support@fujifilm.com)tooadd hello hello 安全傳遞帳戶的使用者。</span><span class="sxs-lookup"><span data-stu-id="23883-198">Work with [SECURE DELIVER support team](mailto:iw-sd-support@fujifilm.com) tooadd hello users in hello SECURE DELIVER account.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="23883-199">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="23883-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="23883-200">在本節中，以啟用許 Simon toouse Azure 單一登入授與存取 tooSECURE 傳遞。</span><span class="sxs-lookup"><span data-stu-id="23883-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSECURE DELIVER.</span></span>

![指派使用者][200] 

<span data-ttu-id="23883-202">**tooassign 許 Simon tooSECURE 傳遞，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="23883-202">**tooassign Britta Simon tooSECURE DELIVER, perform hello following steps:**</span></span>

1. <span data-ttu-id="23883-203">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="23883-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="23883-205">在 [hello] 應用程式清單中，選取**安全傳遞**。</span><span class="sxs-lookup"><span data-stu-id="23883-205">In hello applications list, select **SECURE DELIVER**.</span></span>

    ![設定單一登入](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_app.png) 

3. <span data-ttu-id="23883-207">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="23883-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="23883-209">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="23883-209">Click **Add** button.</span></span> <span data-ttu-id="23883-210">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="23883-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="23883-212">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="23883-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="23883-213">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="23883-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="23883-214">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="23883-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="23883-215">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="23883-215">Testing single sign-on</span></span>

<span data-ttu-id="23883-216">hello 本節目標在於 tootest 您 Azure AD 的 SSO 組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="23883-216">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="23883-217">當您按一下 hello 安全傳遞並排顯示 hello 存取面板中的時，您應該取得自動登入 tooyour 安全傳遞應用程式。</span><span class="sxs-lookup"><span data-stu-id="23883-217">When you click hello SECURE DELIVER tile in hello Access Panel, you should get automatically signed-on tooyour SECURE DELIVER application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="23883-218">其他資源</span><span class="sxs-lookup"><span data-stu-id="23883-218">Additional resources</span></span>

* [<span data-ttu-id="23883-219">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="23883-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="23883-220">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="23883-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_203.png

