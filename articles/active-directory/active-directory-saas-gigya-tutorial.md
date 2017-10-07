---
title: "教學課程：Azure Active Directory 與 Gigya 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Gigya 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2c7d200b-9242-44a5-ac8a-ab3214a78e41
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 1992c5ad09b097563377a488fbf5a375f6511020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-gigya"></a><span data-ttu-id="385ab-103">教學課程：Azure Active Directory 與 Gigya 整合</span><span class="sxs-lookup"><span data-stu-id="385ab-103">Tutorial: Azure Active Directory integration with Gigya</span></span>

<span data-ttu-id="385ab-104">在此教學課程中，您學會如何 toointegrate Gigya 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="385ab-104">In this tutorial, you learn how toointegrate Gigya with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="385ab-105">與 Azure AD 整合 Gigya 可以提供下列優點的 hello:</span><span class="sxs-lookup"><span data-stu-id="385ab-105">Integrating Gigya with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="385ab-106">您可以控制存取 tooGigya Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="385ab-106">You can control in Azure AD who has access tooGigya</span></span>
- <span data-ttu-id="385ab-107">您可以啟用您的使用者 tooautomatically get 登入 tooGigya （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="385ab-107">You can enable your users tooautomatically get signed-on tooGigya (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="385ab-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="385ab-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="385ab-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="385ab-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="385ab-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="385ab-110">Prerequisites</span></span>

<span data-ttu-id="385ab-111">tooconfigure 與 Gigya 的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="385ab-111">tooconfigure Azure AD integration with Gigya, you need hello following items:</span></span>

- <span data-ttu-id="385ab-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="385ab-112">An Azure AD subscription</span></span>
- <span data-ttu-id="385ab-113">已啟用 Gigya 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="385ab-113">A Gigya single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="385ab-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="385ab-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="385ab-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="385ab-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="385ab-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="385ab-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="385ab-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="385ab-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="385ab-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="385ab-118">Scenario description</span></span>
<span data-ttu-id="385ab-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="385ab-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="385ab-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="385ab-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="385ab-121">從 hello 圖庫加入 Gigya</span><span class="sxs-lookup"><span data-stu-id="385ab-121">Adding Gigya from hello gallery</span></span>
2. <span data-ttu-id="385ab-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="385ab-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-gigya-from-hello-gallery"></a><span data-ttu-id="385ab-123">從 hello 圖庫加入 Gigya</span><span class="sxs-lookup"><span data-stu-id="385ab-123">Adding Gigya from hello gallery</span></span>
<span data-ttu-id="385ab-124">tooconfigure hello 整合 Gigya 的 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Gigya。</span><span class="sxs-lookup"><span data-stu-id="385ab-124">tooconfigure hello integration of Gigya into Azure AD, you need tooadd Gigya from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="385ab-125">**tooadd Gigya 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="385ab-125">**tooadd Gigya from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="385ab-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="385ab-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="385ab-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="385ab-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="385ab-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="385ab-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="385ab-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="385ab-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="385ab-133">在 [hello] 搜尋方塊中，輸入**Gigya**。</span><span class="sxs-lookup"><span data-stu-id="385ab-133">In hello search box, type **Gigya**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_search.png)

5. <span data-ttu-id="385ab-135">在 hello 結果 窗格中，選取  **Gigya**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="385ab-135">In hello results panel, select **Gigya**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="385ab-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="385ab-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="385ab-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Gigya 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="385ab-138">In this section, you configure and test Azure AD single sign-on with Gigya based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="385ab-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 Gigya 中是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="385ab-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Gigya is tooa user in Azure AD.</span></span> <span data-ttu-id="385ab-140">換句話說，Azure AD 使用者與 hello Gigya 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="385ab-140">In other words, a link relationship between an Azure AD user and hello related user in Gigya needs toobe established.</span></span>

<span data-ttu-id="385ab-141">在 Gigya 中，將指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="385ab-141">In Gigya, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="385ab-142">tooconfigure 及測試 Azure AD 單一登入 Gigya，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="385ab-142">tooconfigure and test Azure AD single sign-on with Gigya, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="385ab-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="385ab-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="385ab-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="385ab-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="385ab-145">**[建立測試使用者 Gigya](#creating-a-gigya-test-user)**  -toohave 許 Simon Gigya 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="385ab-145">**[Creating a Gigya test user](#creating-a-gigya-test-user)** - toohave a counterpart of Britta Simon in Gigya that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="385ab-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="385ab-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="385ab-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="385ab-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="385ab-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="385ab-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="385ab-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Gigya 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="385ab-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Gigya application.</span></span>

<span data-ttu-id="385ab-150">**tooconfigure Azure AD 單一登入 Gigya，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="385ab-150">**tooconfigure Azure AD single sign-on with Gigya, perform hello following steps:**</span></span>

1. <span data-ttu-id="385ab-151">在 Azure 入口網站上 hello hello **Gigya**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="385ab-151">In hello Azure portal, on hello **Gigya** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="385ab-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="385ab-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_samlbase.png)

3. <span data-ttu-id="385ab-155">在 hello **Gigya 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="385ab-155">On hello **Gigya Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_url.png)

    <span data-ttu-id="385ab-157">a.</span><span class="sxs-lookup"><span data-stu-id="385ab-157">a.</span></span> <span data-ttu-id="385ab-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`http://<companyname>.gigya.com`</span><span class="sxs-lookup"><span data-stu-id="385ab-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://<companyname>.gigya.com`</span></span>

    <span data-ttu-id="385ab-159">b.</span><span class="sxs-lookup"><span data-stu-id="385ab-159">b.</span></span> <span data-ttu-id="385ab-160">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://fidm.gigya.com/saml/v2.0/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="385ab-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://fidm.gigya.com/saml/v2.0/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="385ab-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="385ab-161">These values are not real.</span></span> <span data-ttu-id="385ab-162">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="385ab-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="385ab-163">請連絡[Gigya 用戶端支援小組](https://www.gigya.com/support-policy/)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="385ab-163">Contact [Gigya Client support team](https://www.gigya.com/support-policy/) tooget these values.</span></span> 
 
4. <span data-ttu-id="385ab-164">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="385ab-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_certificate.png) 

5. <span data-ttu-id="385ab-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="385ab-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-gigya-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="385ab-168">在 hello **Gigya 組態**區段中，按一下**設定 Gigya** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="385ab-168">On hello **Gigya Configuration** section, click **Configure Gigya** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="385ab-169">複製 hello **SAML 實體識別碼和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="385ab-169">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_configure.png) 

7. <span data-ttu-id="385ab-171">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 Gigya 公司網站。</span><span class="sxs-lookup"><span data-stu-id="385ab-171">In a different web browser window, log into your Gigya company site as an administrator.</span></span>

8. <span data-ttu-id="385ab-172">跳過**設定\>SAML 登入**，然後按一下hello**新增** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="385ab-172">Go too**Settings \> SAML Login**, and then click hello **Add** button.</span></span>
   
    <span data-ttu-id="385ab-173">![SAML 登入](./media/active-directory-saas-gigya-tutorial/ic789532.png "SAML 登入")</span><span class="sxs-lookup"><span data-stu-id="385ab-173">![SAML Login](./media/active-directory-saas-gigya-tutorial/ic789532.png "SAML Login")</span></span>

9. <span data-ttu-id="385ab-174">在 hello **SAML 登入**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="385ab-174">In hello **SAML Login** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="385ab-175">![SAML 設定](./media/active-directory-saas-gigya-tutorial/ic789533.png "SAML 設定")</span><span class="sxs-lookup"><span data-stu-id="385ab-175">![SAML Configuration](./media/active-directory-saas-gigya-tutorial/ic789533.png "SAML Configuration")</span></span>
   
    <span data-ttu-id="385ab-176">a.</span><span class="sxs-lookup"><span data-stu-id="385ab-176">a.</span></span> <span data-ttu-id="385ab-177">在 hello**名稱**文字方塊中，輸入您的組態名稱。</span><span class="sxs-lookup"><span data-stu-id="385ab-177">In hello **Name** textbox, type a name for your configuration.</span></span>
   
    <span data-ttu-id="385ab-178">b.</span><span class="sxs-lookup"><span data-stu-id="385ab-178">b.</span></span> <span data-ttu-id="385ab-179">在**簽發者**文字方塊中，貼上 hello 值**SAML 實體識別碼**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="385ab-179">In **Issuer** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure Portal.</span></span> 
   
    <span data-ttu-id="385ab-180">c.</span><span class="sxs-lookup"><span data-stu-id="385ab-180">c.</span></span> <span data-ttu-id="385ab-181">在**單一登入服務 URL**文字方塊中，貼上 hello 值**單一登入服務 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="385ab-181">In **Single Sign-On Service URL** textbox, paste hello value of **Single Sign-On Service URL** which you have copied from Azure Portal.</span></span>
   
    <span data-ttu-id="385ab-182">d.</span><span class="sxs-lookup"><span data-stu-id="385ab-182">d.</span></span> <span data-ttu-id="385ab-183">在**名稱識別碼格式**文字方塊中，貼上 hello 值**名稱識別碼格式**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="385ab-183">In **Name ID Format** textbox, paste hello value of **Name Identifier Format** which you have copied from Azure Portal.</span></span>
   
    <span data-ttu-id="385ab-184">e.</span><span class="sxs-lookup"><span data-stu-id="385ab-184">e.</span></span> <span data-ttu-id="385ab-185">從 Azure 入口網站中，複製到剪貼簿，其內容的 hello 下載 [記事本] 中開啟 base-64 編碼的憑證，然後將它貼入 toohello **X.509 憑證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="385ab-185">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox.</span></span>
   
    <span data-ttu-id="385ab-186">f.</span><span class="sxs-lookup"><span data-stu-id="385ab-186">f.</span></span> <span data-ttu-id="385ab-187">按一下 [儲存設定] 。</span><span class="sxs-lookup"><span data-stu-id="385ab-187">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="385ab-188">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="385ab-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="385ab-189">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="385ab-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="385ab-190">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="385ab-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="385ab-191">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="385ab-191">Creating an Azure AD test user</span></span>

<span data-ttu-id="385ab-192">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="385ab-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="385ab-194">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="385ab-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="385ab-195">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="385ab-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-gigya-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="385ab-197">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="385ab-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-gigya-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="385ab-199">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="385ab-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-gigya-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="385ab-201">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="385ab-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-gigya-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="385ab-203">a.</span><span class="sxs-lookup"><span data-stu-id="385ab-203">a.</span></span> <span data-ttu-id="385ab-204">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="385ab-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="385ab-205">b.</span><span class="sxs-lookup"><span data-stu-id="385ab-205">b.</span></span> <span data-ttu-id="385ab-206">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="385ab-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="385ab-207">c.</span><span class="sxs-lookup"><span data-stu-id="385ab-207">c.</span></span> <span data-ttu-id="385ab-208">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="385ab-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="385ab-209">d.</span><span class="sxs-lookup"><span data-stu-id="385ab-209">d.</span></span> <span data-ttu-id="385ab-210">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="385ab-210">Click **Create**.</span></span>
 
### <a name="creating-a-gigya-test-user"></a><span data-ttu-id="385ab-211">建立 Gigya 測試使用者</span><span class="sxs-lookup"><span data-stu-id="385ab-211">Creating a Gigya test user</span></span>

<span data-ttu-id="385ab-212">在訂單 tooenable Azure AD 使用者 toolog 入 Gigya，它們必須佈建到 Gigya。</span><span class="sxs-lookup"><span data-stu-id="385ab-212">In order tooenable Azure AD users toolog into Gigya, they must be provisioned into Gigya.</span></span>  
<span data-ttu-id="385ab-213">在 Gigya 的 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="385ab-213">In hello case of Gigya, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-accounts-perform-hello-following-steps"></a><span data-ttu-id="385ab-214">tooprovision 使用者帳戶，執行下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="385ab-214">tooprovision a user accounts, perform hello following steps:</span></span>

1. <span data-ttu-id="385ab-215">登入 tooyour **Gigya**系統管理員身分的公司網站。</span><span class="sxs-lookup"><span data-stu-id="385ab-215">Log in tooyour **Gigya** company site as an administrator.</span></span>

2. <span data-ttu-id="385ab-216">跳過**Admin\>管理使用者**，然後按一下**邀請使用者**。</span><span class="sxs-lookup"><span data-stu-id="385ab-216">Go too**Admin \> Manage Users**, and then click **Invite Users**.</span></span>
   
    <span data-ttu-id="385ab-217">![管理使用者](./media/active-directory-saas-gigya-tutorial/ic789535.png "管理使用者")</span><span class="sxs-lookup"><span data-stu-id="385ab-217">![Manage Users](./media/active-directory-saas-gigya-tutorial/ic789535.png "Manage Users")</span></span>

3. <span data-ttu-id="385ab-218">在 hello 邀請使用者 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="385ab-218">On hello Invite Users dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="385ab-219">![邀請使用者](./media/active-directory-saas-gigya-tutorial/ic789536.png "邀請使用者")</span><span class="sxs-lookup"><span data-stu-id="385ab-219">![Invite Users](./media/active-directory-saas-gigya-tutorial/ic789536.png "Invite Users")</span></span>
   
    <span data-ttu-id="385ab-220">a.</span><span class="sxs-lookup"><span data-stu-id="385ab-220">a.</span></span> <span data-ttu-id="385ab-221">在 hello**電子郵件**文字方塊中，您想要 tooprovision 之有效 Azure Active Directory 帳戶類型 hello 電子郵件別名。</span><span class="sxs-lookup"><span data-stu-id="385ab-221">In hello **Email** textbox, type hello email alias of a valid Azure Active Directory account you want tooprovision.</span></span>
    
    <span data-ttu-id="385ab-222">b.</span><span class="sxs-lookup"><span data-stu-id="385ab-222">b.</span></span> <span data-ttu-id="385ab-223">按一下 [邀請使用者] 。</span><span class="sxs-lookup"><span data-stu-id="385ab-223">Click **Invite User**.</span></span>
      
    > [!NOTE]
    > <span data-ttu-id="385ab-224">hello Azure Active Directory 帳戶持有者將會收到電子郵件，其中包含連結 tooconfirm hello 帳戶之前就會生效。</span><span class="sxs-lookup"><span data-stu-id="385ab-224">hello Azure Active Directory account holder will receive an email that includes a link tooconfirm hello account before it becomes active.</span></span>
    > 
    

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="385ab-225">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="385ab-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="385ab-226">在本節中，您可以授與存取 tooGigya 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="385ab-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooGigya.</span></span>

![指派使用者][200] 

<span data-ttu-id="385ab-228">**tooassign 許 Simon tooGigya，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="385ab-228">**tooassign Britta Simon tooGigya, perform hello following steps:**</span></span>

1. <span data-ttu-id="385ab-229">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="385ab-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="385ab-231">在 [hello] 應用程式清單中，選取**Gigya**。</span><span class="sxs-lookup"><span data-stu-id="385ab-231">In hello applications list, select **Gigya**.</span></span>

    ![設定單一登入](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_app.png) 

3. <span data-ttu-id="385ab-233">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="385ab-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="385ab-235">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="385ab-235">Click **Add** button.</span></span> <span data-ttu-id="385ab-236">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="385ab-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="385ab-238">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="385ab-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="385ab-239">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="385ab-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="385ab-240">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="385ab-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="385ab-241">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="385ab-241">Testing single sign-on</span></span>

<span data-ttu-id="385ab-242">hello 本節目標在於 tootest 您 Azure AD 的 SSO 組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="385ab-242">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="385ab-243">當您按一下 hello Gigya 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Gigya 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="385ab-243">When you click hello Gigya tile in hello Access Panel, you should get automatically signed-on tooyour Gigya application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="385ab-244">其他資源</span><span class="sxs-lookup"><span data-stu-id="385ab-244">Additional resources</span></span>

* [<span data-ttu-id="385ab-245">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="385ab-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="385ab-246">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="385ab-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_203.png

