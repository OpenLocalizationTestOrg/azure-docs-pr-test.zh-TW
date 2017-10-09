---
title: "教學課程：Azure Active Directory 與 Humanity 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與人類之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6aa771e9-31c6-48d1-8dde-024bebc06943
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 7d8a04a2eb3c997f86f1e199c47809fa3dad60e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-humanity"></a><span data-ttu-id="7fe0f-103">教學課程：Azure Active Directory 與 Humanity 整合</span><span class="sxs-lookup"><span data-stu-id="7fe0f-103">Tutorial: Azure Active Directory integration with Humanity</span></span>

<span data-ttu-id="7fe0f-104">在此教學課程中，您學會如何 toointegrate 與 Azure Active Directory (Azure AD) 的最高。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-104">In this tutorial, you learn how toointegrate Humanity with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7fe0f-105">與 Azure AD 整合人類可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="7fe0f-105">Integrating Humanity with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7fe0f-106">您可以控制存取 tooHumanity Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="7fe0f-106">You can control in Azure AD who has access tooHumanity</span></span>
- <span data-ttu-id="7fe0f-107">您可以啟用您的使用者 tooautomatically get 登入 tooHumanity （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="7fe0f-107">You can enable your users tooautomatically get signed-on tooHumanity (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7fe0f-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="7fe0f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7fe0f-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7fe0f-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="7fe0f-110">Prerequisites</span></span>

<span data-ttu-id="7fe0f-111">tooconfigure 與人類的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="7fe0f-111">tooconfigure Azure AD integration with Humanity, you need hello following items:</span></span>

- <span data-ttu-id="7fe0f-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7fe0f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7fe0f-113">已啟用 Humanity 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7fe0f-113">A Humanity single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7fe0f-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7fe0f-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="7fe0f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7fe0f-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7fe0f-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7fe0f-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="7fe0f-118">Scenario description</span></span>
<span data-ttu-id="7fe0f-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7fe0f-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="7fe0f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7fe0f-121">從 hello 圖庫加入人類</span><span class="sxs-lookup"><span data-stu-id="7fe0f-121">Adding Humanity from hello gallery</span></span>
2. <span data-ttu-id="7fe0f-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7fe0f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-humanity-from-hello-gallery"></a><span data-ttu-id="7fe0f-123">從 hello 圖庫加入人類</span><span class="sxs-lookup"><span data-stu-id="7fe0f-123">Adding Humanity from hello gallery</span></span>
<span data-ttu-id="7fe0f-124">tooconfigure hello 人類至 Azure AD 整合，您需要 tooadd 人類 hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-124">tooconfigure hello integration of Humanity into Azure AD, you need tooadd Humanity from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7fe0f-125">**tooadd 人類 hello 圖庫中，從執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="7fe0f-125">**tooadd Humanity from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7fe0f-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7fe0f-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7fe0f-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="7fe0f-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="7fe0f-133">在 [hello] 搜尋方塊中，輸入**人類**。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-133">In hello search box, type **Humanity**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_search.png)

5. <span data-ttu-id="7fe0f-135">在 hello 結果 窗格中，選取 **人類**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-135">In hello results panel, select **Humanity**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7fe0f-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7fe0f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7fe0f-138">在本節中，您將以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Humanity 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-138">In this section, you configure and test Azure AD single sign-on with Humanity based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7fe0f-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中最高為 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Humanity is tooa user in Azure AD.</span></span> <span data-ttu-id="7fe0f-140">換句話說，Azure AD 使用者與 hello 中最高的相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-140">In other words, a link relationship between an Azure AD user and hello related user in Humanity needs toobe established.</span></span>

<span data-ttu-id="7fe0f-141">在最高，將指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-141">In Humanity, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7fe0f-142">tooconfigure 及 Azure AD 單一登入具有最高的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="7fe0f-142">tooconfigure and test Azure AD single sign-on with Humanity, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7fe0f-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7fe0f-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7fe0f-145">**[建立最高的測試使用者](#creating-a-humanity-test-user)** -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示法的人類中對應項目。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-145">**[Creating a Humanity test user](#creating-a-humanity-test-user)** - toohave a counterpart of Britta Simon in Humanity that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7fe0f-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7fe0f-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7fe0f-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7fe0f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7fe0f-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並人類應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Humanity application.</span></span>

<span data-ttu-id="7fe0f-150">**tooconfigure Azure AD 單一登入具有最高，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="7fe0f-150">**tooconfigure Azure AD single sign-on with Humanity, perform hello following steps:**</span></span>

1. <span data-ttu-id="7fe0f-151">在 Azure 入口網站上 hello hello**人類**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-151">In hello Azure portal, on hello **Humanity** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="7fe0f-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_samlbase.png)

3. <span data-ttu-id="7fe0f-155">在 hello**人類網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="7fe0f-155">On hello **Humanity Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_url.png)

    <span data-ttu-id="7fe0f-157">a.</span><span class="sxs-lookup"><span data-stu-id="7fe0f-157">a.</span></span> <span data-ttu-id="7fe0f-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://company.humanity.com/includes/saml/`</span><span class="sxs-lookup"><span data-stu-id="7fe0f-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://company.humanity.com/includes/saml/`</span></span>

    <span data-ttu-id="7fe0f-159">b.</span><span class="sxs-lookup"><span data-stu-id="7fe0f-159">b.</span></span> <span data-ttu-id="7fe0f-160">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://company.humanity.com/app/`</span><span class="sxs-lookup"><span data-stu-id="7fe0f-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://company.humanity.com/app/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7fe0f-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-161">These values are not real.</span></span> <span data-ttu-id="7fe0f-162">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="7fe0f-163">請連絡[人類用戶端支援小組](https://www.humanity.com/support/)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-163">Contact [Humanity Client support team](https://www.humanity.com/support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="7fe0f-164">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_certificate.png) 

5. <span data-ttu-id="7fe0f-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7fe0f-168">在 hello**人類組態**區段中，按一下**設定人類**tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-168">On hello **Humanity Configuration** section, click **Configure Humanity** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7fe0f-169">複製 hello **SAML 單一登入服務 URL 和登出 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="7fe0f-169">Copy hello **SAML Single Sign-On Service URL, and Sign-Out URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_configure.png) 

7. <span data-ttu-id="7fe0f-171">在不同的網頁瀏覽器視窗中，登入 tooyour**人類**系統管理員身分的公司網站。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-171">In a different web browser window, log in tooyour **Humanity** company site as an administrator.</span></span>

8. <span data-ttu-id="7fe0f-172">在 hello 最上層顯示 hello 功能表上，按一下**Admin**。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-172">In hello menu on hello top, click **Admin**.</span></span>
   
    <span data-ttu-id="7fe0f-173">![管理](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "管理")</span><span class="sxs-lookup"><span data-stu-id="7fe0f-173">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span></span>

9. <span data-ttu-id="7fe0f-174">在 [整合] 下方，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-174">Under **Integration**, click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="7fe0f-175">![單一登入](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "單一登入")</span><span class="sxs-lookup"><span data-stu-id="7fe0f-175">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "Single Sign-On")</span></span>

10. <span data-ttu-id="7fe0f-176">在 hello**單一登入**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="7fe0f-176">In hello **Single Sign-On** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="7fe0f-177">![單一登入](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "單一登入")</span><span class="sxs-lookup"><span data-stu-id="7fe0f-177">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "Single Sign-On")</span></span>
   
    <span data-ttu-id="7fe0f-178">a.</span><span class="sxs-lookup"><span data-stu-id="7fe0f-178">a.</span></span> <span data-ttu-id="7fe0f-179">選取 [已啟用 SAML] 。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-179">Select **SAML Enabled**.</span></span>

    <span data-ttu-id="7fe0f-180">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-180">b.</span></span> <span data-ttu-id="7fe0f-181">選取 [允許密碼登入]。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-181">Select **Allow Password Login**.</span></span>

    <span data-ttu-id="7fe0f-182">c.</span><span class="sxs-lookup"><span data-stu-id="7fe0f-182">c.</span></span> <span data-ttu-id="7fe0f-183">貼上 hello **SAML 單一登入服務 URL**值傳入 hello **SAML 簽發者 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-183">Paste hello **SAML Single Sign-On Service URL** value into hello **SAML Issuer URL** textbox.</span></span>

    <span data-ttu-id="7fe0f-184">d.</span><span class="sxs-lookup"><span data-stu-id="7fe0f-184">d.</span></span> <span data-ttu-id="7fe0f-185">貼上 hello**登出 URL**值傳入 hello**遠端登出 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-185">Paste hello **Sign-Out URL** value into hello **Remote Logout URL** textbox.</span></span>
   
    <span data-ttu-id="7fe0f-186">e.</span><span class="sxs-lookup"><span data-stu-id="7fe0f-186">e.</span></span> <span data-ttu-id="7fe0f-187">在記事本中，複製到剪貼簿，其內容的 hello 中開啟 base-64 編碼的憑證，然後將它貼入 toohello **X.509 憑證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-187">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox.</span></span>

11. <span data-ttu-id="7fe0f-188">按一下 [儲存設定] 。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-188">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="7fe0f-189">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="7fe0f-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7fe0f-190">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7fe0f-191">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7fe0f-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7fe0f-192">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7fe0f-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="7fe0f-193">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="7fe0f-195">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="7fe0f-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7fe0f-196">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7fe0f-198">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7fe0f-200">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7fe0f-202">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="7fe0f-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7fe0f-204">a.</span><span class="sxs-lookup"><span data-stu-id="7fe0f-204">a.</span></span> <span data-ttu-id="7fe0f-205">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7fe0f-206">b.</span><span class="sxs-lookup"><span data-stu-id="7fe0f-206">b.</span></span> <span data-ttu-id="7fe0f-207">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7fe0f-208">c.</span><span class="sxs-lookup"><span data-stu-id="7fe0f-208">c.</span></span> <span data-ttu-id="7fe0f-209">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7fe0f-210">d.</span><span class="sxs-lookup"><span data-stu-id="7fe0f-210">d.</span></span> <span data-ttu-id="7fe0f-211">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-211">Click **Create**.</span></span>
 
### <a name="creating-a-humanity-test-user"></a><span data-ttu-id="7fe0f-212">建立 Humanity 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7fe0f-212">Creating a Humanity test user</span></span>

<span data-ttu-id="7fe0f-213">在順序 tooenable Azure AD 使用者 toolog tooHumanity 中，您必須是佈建到最高。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-213">In order tooenable Azure AD users toolog in tooHumanity, they must be provisioned into Humanity.</span></span> <span data-ttu-id="7fe0f-214">在最高的 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-214">In hello case of Humanity, provisioning is a manual task.</span></span>

<span data-ttu-id="7fe0f-215">**tooprovision 使用者帳戶，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="7fe0f-215">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="7fe0f-216">登入 tooyour**人類**系統管理員身分的公司網站。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-216">Log in tooyour **Humanity** company site as an administrator.</span></span>

2. <span data-ttu-id="7fe0f-217">按一下 Admin 。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-217">Click **Admin**.</span></span>
   
    <span data-ttu-id="7fe0f-218">![管理](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "管理")</span><span class="sxs-lookup"><span data-stu-id="7fe0f-218">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span></span>

3. <span data-ttu-id="7fe0f-219">按一下 [職員] 。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-219">Click **Staff**.</span></span>
   
    <span data-ttu-id="7fe0f-220">![職員](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "職員")</span><span class="sxs-lookup"><span data-stu-id="7fe0f-220">![Staff](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "Staff")</span></span>

4. <span data-ttu-id="7fe0f-221">在 [動作] 下方，按一下 [新增員工]。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-221">Under **Actions**, click **Add Employees**.</span></span>
   
    <span data-ttu-id="7fe0f-222">![新增員工](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "新增員工")</span><span class="sxs-lookup"><span data-stu-id="7fe0f-222">![Add Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "Add Employees")</span></span>

5. <span data-ttu-id="7fe0f-223">在 hello**新增員工**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="7fe0f-223">In hello **Add Employees** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="7fe0f-224">![儲存員工](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "儲存員工")</span><span class="sxs-lookup"><span data-stu-id="7fe0f-224">![Save Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "Save Employees")</span></span>
   
    <span data-ttu-id="7fe0f-225">a.</span><span class="sxs-lookup"><span data-stu-id="7fe0f-225">a.</span></span> <span data-ttu-id="7fe0f-226">型別 hello**名字**，**姓氏**，和**電子郵件**的想成 hello tooprovision 的有效 AAD 帳戶相關的文字方塊。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-226">Type hello **First Name**, **Last Name**, and **Email** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>

    <span data-ttu-id="7fe0f-227">b.</span><span class="sxs-lookup"><span data-stu-id="7fe0f-227">b.</span></span> <span data-ttu-id="7fe0f-228">按一下 [儲存員工] 。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-228">Click **Save Employees**.</span></span>

>[!NOTE]
><span data-ttu-id="7fe0f-229">您可以使用任何其他人類使用者帳戶建立工具或 Api 提供最高 tooprovision AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-229">You can use any other Humanity user account creation tools or APIs provided by Humanity tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7fe0f-230">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="7fe0f-230">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7fe0f-231">在本節中，您可以授與存取 tooHumanity 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-231">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHumanity.</span></span>

![指派使用者][200] 

<span data-ttu-id="7fe0f-233">**tooassign 許 Simon tooHumanity，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="7fe0f-233">**tooassign Britta Simon tooHumanity, perform hello following steps:**</span></span>

1. <span data-ttu-id="7fe0f-234">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="7fe0f-236">在 [hello] 應用程式清單中，選取**人類**。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-236">In hello applications list, select **Humanity**.</span></span>

    ![設定單一登入](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_app.png) 

3. <span data-ttu-id="7fe0f-238">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="7fe0f-240">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-240">Click **Add** button.</span></span> <span data-ttu-id="7fe0f-241">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="7fe0f-243">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7fe0f-244">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7fe0f-245">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7fe0f-246">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="7fe0f-246">Testing single sign-on</span></span>

<span data-ttu-id="7fe0f-247">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-247">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7fe0f-248">當您按一下 hello 人類磚 hello 存取面板中的時，您應該取得自動登入 tooyour 人類應用程式。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-248">When you click hello Humanity tile in hello Access Panel, you should get automatically signed-on tooyour Humanity application.</span></span>
<span data-ttu-id="7fe0f-249">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="7fe0f-249">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7fe0f-250">其他資源</span><span class="sxs-lookup"><span data-stu-id="7fe0f-250">Additional resources</span></span>

* [<span data-ttu-id="7fe0f-251">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7fe0f-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7fe0f-252">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="7fe0f-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_203.png

