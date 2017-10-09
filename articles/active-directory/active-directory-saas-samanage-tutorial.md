---
title: "教學課程：Azure Active Directory 與 Samanage 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Samanage 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0db4fb0-7eec-48c2-9c7a-beab1ab49bc2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: c8edc29f113b8088438618a731e97c0f4f155b9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-samanage"></a><span data-ttu-id="e310c-103">教學課程：Azure Active Directory 與 Samanage 整合</span><span class="sxs-lookup"><span data-stu-id="e310c-103">Tutorial: Azure Active Directory integration with Samanage</span></span>

<span data-ttu-id="e310c-104">在此教學課程中，您學會如何 toointegrate Samanage 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="e310c-104">In this tutorial, you learn how toointegrate Samanage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e310c-105">整合 Azure AD 與 Samanage 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="e310c-105">Integrating Samanage with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e310c-106">您可以控制存取 tooSamanage Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="e310c-106">You can control in Azure AD who has access tooSamanage</span></span>
- <span data-ttu-id="e310c-107">您可以啟用您的使用者 tooautomatically get 登入 tooSamanage （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="e310c-107">You can enable your users tooautomatically get signed-on tooSamanage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e310c-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="e310c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e310c-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="e310c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e310c-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="e310c-110">Prerequisites</span></span>

<span data-ttu-id="e310c-111">tooconfigure Azure AD 與 Samanage 的整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="e310c-111">tooconfigure Azure AD integration with Samanage, you need hello following items:</span></span>

- <span data-ttu-id="e310c-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e310c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e310c-113">啟用 Samanage 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e310c-113">A Samanage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e310c-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="e310c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e310c-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="e310c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e310c-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="e310c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e310c-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="e310c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e310c-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="e310c-118">Scenario description</span></span>
<span data-ttu-id="e310c-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e310c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e310c-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="e310c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e310c-121">從 hello 圖庫加入 Samanage</span><span class="sxs-lookup"><span data-stu-id="e310c-121">Adding Samanage from hello gallery</span></span>
2. <span data-ttu-id="e310c-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e310c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-samanage-from-hello-gallery"></a><span data-ttu-id="e310c-123">從 hello 圖庫加入 Samanage</span><span class="sxs-lookup"><span data-stu-id="e310c-123">Adding Samanage from hello gallery</span></span>
<span data-ttu-id="e310c-124">tooconfigure hello 整合 Samanage 的 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Samanage。</span><span class="sxs-lookup"><span data-stu-id="e310c-124">tooconfigure hello integration of Samanage into Azure AD, you need tooadd Samanage from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e310c-125">**tooadd Samanage hello 圖庫中，從執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="e310c-125">**tooadd Samanage from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e310c-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="e310c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e310c-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="e310c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e310c-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="e310c-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="e310c-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="e310c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="e310c-133">在 [hello] 搜尋方塊中，輸入**Samanage**。</span><span class="sxs-lookup"><span data-stu-id="e310c-133">In hello search box, type **Samanage**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_search.png)

5. <span data-ttu-id="e310c-135">在 hello 結果 窗格中，選取  **Samanage**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e310c-135">In hello results panel, select **Samanage**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e310c-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e310c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e310c-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Samanage 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e310c-138">In this section, you configure and test Azure AD single sign-on with Samanage based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e310c-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者 Samanage 中是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="e310c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Samanage is tooa user in Azure AD.</span></span> <span data-ttu-id="e310c-140">換句話說，Azure AD 使用者與 hello Samanage 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="e310c-140">In other words, a link relationship between an Azure AD user and hello related user in Samanage needs toobe established.</span></span>

<span data-ttu-id="e310c-141">在 Samanage 中，將指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="e310c-141">In Samanage, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e310c-142">tooconfigure 及測試 Azure AD 單一登入 Samanage，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="e310c-142">tooconfigure and test Azure AD single sign-on with Samanage, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e310c-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="e310c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e310c-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="e310c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e310c-145">**[建立測試使用者 Samanage](#creating-a-samanage-test-user)**  -toohave 許 Simon Samanage 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="e310c-145">**[Creating a Samanage test user](#creating-a-samanage-test-user)** - toohave a counterpart of Britta Simon in Samanage that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e310c-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e310c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e310c-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="e310c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e310c-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e310c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e310c-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Samanage 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="e310c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Samanage application.</span></span>

<span data-ttu-id="e310c-150">**tooconfigure Azure AD 單一登入 Samanage 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="e310c-150">**tooconfigure Azure AD single sign-on with Samanage, perform hello following steps:**</span></span>

1. <span data-ttu-id="e310c-151">在 Azure 入口網站上 hello hello **Samanage**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="e310c-151">In hello Azure portal, on hello **Samanage** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="e310c-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e310c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_samlbase.png)

3. <span data-ttu-id="e310c-155">在 hello **Samanage 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="e310c-155">On hello **Samanage Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_url.png)

    <span data-ttu-id="e310c-157">a.</span><span class="sxs-lookup"><span data-stu-id="e310c-157">a.</span></span> <span data-ttu-id="e310c-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<Company Name>.samanage.com/saml_login/<Company Name>`</span><span class="sxs-lookup"><span data-stu-id="e310c-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<Company Name>.samanage.com/saml_login/<Company Name>`</span></span>

    <span data-ttu-id="e310c-159">b.</span><span class="sxs-lookup"><span data-stu-id="e310c-159">b.</span></span> <span data-ttu-id="e310c-160">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<Company Name>.samanage.com`</span><span class="sxs-lookup"><span data-stu-id="e310c-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<Company Name>.samanage.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e310c-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="e310c-161">These values are not real.</span></span> <span data-ttu-id="e310c-162">Hello 實際登入 URL 和識別碼，在 hello 教學課程稍後會說明更新這些值。</span><span class="sxs-lookup"><span data-stu-id="e310c-162">Update these values with hello actual Sign-on URL and Identifier, which is explained later in hello tutorial.</span></span> <span data-ttu-id="e310c-163">如需詳細資料，請連絡 [Samanage 客戶支援小組](https://www.samanage.com/support)。</span><span class="sxs-lookup"><span data-stu-id="e310c-163">For more details contact [Samanage Client support team](https://www.samanage.com/support).</span></span>    
 
4. <span data-ttu-id="e310c-164">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="e310c-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_certificate.png) 

5. <span data-ttu-id="e310c-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="e310c-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-samanage-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e310c-168">在 hello **Samanage 組態**區段中，按一下**設定 Samanage** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="e310c-168">On hello **Samanage Configuration** section, click **Configure Samanage** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e310c-169">複製 hello**登出 URL 和 SAML 實體識別碼**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="e310c-169">Copy hello **Sign-Out URL, and SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_configure.png) 

7. <span data-ttu-id="e310c-171">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 Samanage 公司網站。</span><span class="sxs-lookup"><span data-stu-id="e310c-171">In a different web browser window, log into your Samanage company site as an administrator.</span></span>

8. <span data-ttu-id="e310c-172">按一下 [儀表板] 並選取左側導覽窗格中的 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="e310c-172">Click **Dashboard** and select **Setup** in left navigation pane.</span></span>
   
    <span data-ttu-id="e310c-173">![儀表板](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "儀表板")</span><span class="sxs-lookup"><span data-stu-id="e310c-173">![Dashboard](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Dashboard")</span></span>

9. <span data-ttu-id="e310c-174">按一下 [單一登入] 。</span><span class="sxs-lookup"><span data-stu-id="e310c-174">Click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="e310c-175">![單一登入](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_002.png "單一登入")</span><span class="sxs-lookup"><span data-stu-id="e310c-175">![Single Sign-On](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_002.png "Single Sign-On")</span></span>

10. <span data-ttu-id="e310c-176">瀏覽過**使用 SAML 登入**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="e310c-176">Navigate too**Login using SAML** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="e310c-177">![使用 SAML 登入](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_003.png "使用 SAML 登入")</span><span class="sxs-lookup"><span data-stu-id="e310c-177">![Login using SAML](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_003.png "Login using SAML")</span></span>
 
    <span data-ttu-id="e310c-178">a.</span><span class="sxs-lookup"><span data-stu-id="e310c-178">a.</span></span> <span data-ttu-id="e310c-179">按一下 [使用 SAML 啟用單一登入]。</span><span class="sxs-lookup"><span data-stu-id="e310c-179">Click **Enable Single Sign-On with SAML**.</span></span>  
 
    <span data-ttu-id="e310c-180">b.</span><span class="sxs-lookup"><span data-stu-id="e310c-180">b.</span></span> <span data-ttu-id="e310c-181">在 hello**身分識別提供者 URL**文字方塊中，貼上 hello 值**SAML 實體識別碼**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="e310c-181">In hello **Identity Provider URL** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>    
 
    <span data-ttu-id="e310c-182">c.</span><span class="sxs-lookup"><span data-stu-id="e310c-182">c.</span></span> <span data-ttu-id="e310c-183">確認 hello**登入 URL**相符項目 hello**登入 URL**的**Samanage 網域和 Url** Azure 入口網站中的區段。</span><span class="sxs-lookup"><span data-stu-id="e310c-183">Confirm hello **Login URL** matches hello **Sign On URL** of **Samanage Domain and URLs** section in Azure portal.</span></span>
 
    <span data-ttu-id="e310c-184">d.</span><span class="sxs-lookup"><span data-stu-id="e310c-184">d.</span></span> <span data-ttu-id="e310c-185">在 hello**登出 URL**文字方塊中，輸入 hello 值**登出 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="e310c-185">In hello **Logout URL** textbox, enter hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="e310c-186">e.</span><span class="sxs-lookup"><span data-stu-id="e310c-186">e.</span></span> <span data-ttu-id="e310c-187">在 hello **SAML 簽發者**在您的身分識別提供者中的文字方塊中，型別 hello 應用程式識別碼 URI 設定。</span><span class="sxs-lookup"><span data-stu-id="e310c-187">In hello **SAML Issuer** textbox, type hello app id URI set in your identity provider.</span></span>
 
    <span data-ttu-id="e310c-188">f.</span><span class="sxs-lookup"><span data-stu-id="e310c-188">f.</span></span> <span data-ttu-id="e310c-189">開啟您從 [記事本]，複製到剪貼簿，其內容的 hello Azure 入口網站下載的 base-64 編碼的憑證，然後將它貼入 toohello**貼上您的身分識別提供者 x.509 憑證下方**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="e310c-189">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **Paste your Identity Provider x.509 Certificate below** textbox.</span></span>
 
    <span data-ttu-id="e310c-190">g.</span><span class="sxs-lookup"><span data-stu-id="e310c-190">g.</span></span> <span data-ttu-id="e310c-191">按一下 [若 Samanage 中不存在使用者則加以建立]。</span><span class="sxs-lookup"><span data-stu-id="e310c-191">Click **Create users if they do not exist in Samanage**.</span></span>
 
    <span data-ttu-id="e310c-192">h.</span><span class="sxs-lookup"><span data-stu-id="e310c-192">h.</span></span> <span data-ttu-id="e310c-193">按一下 [更新] 。</span><span class="sxs-lookup"><span data-stu-id="e310c-193">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="e310c-194">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="e310c-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e310c-195">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="e310c-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e310c-196">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e310c-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e310c-197">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e310c-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="e310c-198">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="e310c-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="e310c-200">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="e310c-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e310c-201">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="e310c-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-samanage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e310c-203">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="e310c-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-samanage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e310c-205">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="e310c-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-samanage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e310c-207">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="e310c-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-samanage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e310c-209">a.</span><span class="sxs-lookup"><span data-stu-id="e310c-209">a.</span></span> <span data-ttu-id="e310c-210">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="e310c-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e310c-211">b.</span><span class="sxs-lookup"><span data-stu-id="e310c-211">b.</span></span> <span data-ttu-id="e310c-212">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="e310c-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e310c-213">c.</span><span class="sxs-lookup"><span data-stu-id="e310c-213">c.</span></span> <span data-ttu-id="e310c-214">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="e310c-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e310c-215">d.</span><span class="sxs-lookup"><span data-stu-id="e310c-215">d.</span></span> <span data-ttu-id="e310c-216">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="e310c-216">Click **Create**.</span></span>
 
### <a name="creating-a-samanage-test-user"></a><span data-ttu-id="e310c-217">建立 Samanage 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e310c-217">Creating a Samanage test user</span></span>

<span data-ttu-id="e310c-218">tooenable Azure AD 使用者 toolog 中 tooSamanage，它們必須佈建到 Samanage。</span><span class="sxs-lookup"><span data-stu-id="e310c-218">tooenable Azure AD users toolog in tooSamanage, they must be provisioned into Samanage.</span></span>  
<span data-ttu-id="e310c-219">在 Samanage 的 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="e310c-219">In hello case of Samanage, provisioning is a manual task.</span></span>

<span data-ttu-id="e310c-220">**tooprovision 使用者帳戶，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="e310c-220">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="e310c-221">以系統管理員身分登入您的 Samanage 公司網站。</span><span class="sxs-lookup"><span data-stu-id="e310c-221">Log into your Samanage company site as an administrator.</span></span>

2. <span data-ttu-id="e310c-222">按一下 [儀表板] 並選取左側導覽窗格中的 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="e310c-222">Click **Dashboard** and select **Setup** in left navigation pan.</span></span>
   
    <span data-ttu-id="e310c-223">![設定](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "設定")</span><span class="sxs-lookup"><span data-stu-id="e310c-223">![Setup](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Setup")</span></span>

3. <span data-ttu-id="e310c-224">按一下 hello**使用者** 索引標籤</span><span class="sxs-lookup"><span data-stu-id="e310c-224">Click hello **Users** tab</span></span>
   
    <span data-ttu-id="e310c-225">![使用者](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_006.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="e310c-225">![Users](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_006.png "Users")</span></span>

4. <span data-ttu-id="e310c-226">按一下 [新使用者] 。</span><span class="sxs-lookup"><span data-stu-id="e310c-226">Click **New User**.</span></span>
   
    <span data-ttu-id="e310c-227">![新增使用者](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_007.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="e310c-227">![New User](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_007.png "New User")</span></span>

5. <span data-ttu-id="e310c-228">型別 hello**名稱**和 hello**電子郵件地址**tooprovision 然後按一下的 Azure Active Directory 帳戶**建立使用者**。</span><span class="sxs-lookup"><span data-stu-id="e310c-228">Type hello **Name** and hello **Email Address** of an Azure Active Directory account you want tooprovision and click **Create user**.</span></span>
   
    <span data-ttu-id="e310c-229">![建立使用者](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_008.png "建立使用者")</span><span class="sxs-lookup"><span data-stu-id="e310c-229">![Create User](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_008.png "Create User")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="e310c-230">hello Azure Active Directory 帳戶持有者將收到一封電子郵件，並遵循連結 tooconfirm 他們的帳戶之前就會生效。</span><span class="sxs-lookup"><span data-stu-id="e310c-230">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span> <span data-ttu-id="e310c-231">您可以使用任何其他 Samanage 使用者帳戶建立工具或 Api 提供 Samanage tooprovision Azure Active Directory 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="e310c-231">You can use any other Samanage user account creation tools or APIs provided by Samanage tooprovision Azure Active Directory user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e310c-232">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="e310c-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e310c-233">在本節中，您可以授與存取 tooSamanage 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e310c-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSamanage.</span></span>

![指派使用者][200] 

<span data-ttu-id="e310c-235">**tooassign 許 Simon tooSamanage，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="e310c-235">**tooassign Britta Simon tooSamanage, perform hello following steps:**</span></span>

1. <span data-ttu-id="e310c-236">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="e310c-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="e310c-238">在 [hello] 應用程式清單中，選取**Samanage**。</span><span class="sxs-lookup"><span data-stu-id="e310c-238">In hello applications list, select **Samanage**.</span></span>

    ![設定單一登入](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_app.png) 

3. <span data-ttu-id="e310c-240">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="e310c-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="e310c-242">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e310c-242">Click **Add** button.</span></span> <span data-ttu-id="e310c-243">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="e310c-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="e310c-245">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="e310c-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e310c-246">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e310c-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e310c-247">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e310c-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e310c-248">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="e310c-248">Testing single sign-on</span></span>

<span data-ttu-id="e310c-249">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="e310c-249">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e310c-250">當您按一下 hello Samanage 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Samanage 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="e310c-250">When you click hello Samanage tile in hello Access Panel, you should get automatically signed-on tooyour Samanage application.</span></span>
<span data-ttu-id="e310c-251">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="e310c-251">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e310c-252">其他資源</span><span class="sxs-lookup"><span data-stu-id="e310c-252">Additional resources</span></span>

* [<span data-ttu-id="e310c-253">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e310c-253">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e310c-254">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="e310c-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_203.png

