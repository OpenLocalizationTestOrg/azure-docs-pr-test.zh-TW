---
title: "教學課程：Azure Active Directory 與 Slack 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Slack 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffc5e73f-6c38-4bbb-876a-a7dd269d4e1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 7f0151401af4dc63d2f714d4b4f66380c4b51e0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-slack"></a><span data-ttu-id="edb66-103">教學課程：Azure Active Directory 與 Slack 整合</span><span class="sxs-lookup"><span data-stu-id="edb66-103">Tutorial: Azure Active Directory integration with Slack</span></span>

<span data-ttu-id="edb66-104">在此教學課程中，您學會如何 toointegrate 延與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="edb66-104">In this tutorial, you learn how toointegrate Slack with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="edb66-105">與 Azure AD 整合 Slack 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="edb66-105">Integrating Slack with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="edb66-106">您可以控制存取 tooSlack Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="edb66-106">You can control in Azure AD who has access tooSlack</span></span>
- <span data-ttu-id="edb66-107">您可以啟用您的使用者 tooautomatically get 登入 tooSlack （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="edb66-107">You can enable your users tooautomatically get signed-on tooSlack (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="edb66-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="edb66-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="edb66-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="edb66-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="edb66-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="edb66-110">Prerequisites</span></span>

<span data-ttu-id="edb66-111">tooconfigure 與 Slack 的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="edb66-111">tooconfigure Azure AD integration with Slack, you need hello following items:</span></span>

- <span data-ttu-id="edb66-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="edb66-112">An Azure AD subscription</span></span>
- <span data-ttu-id="edb66-113">啟用 Slack 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="edb66-113">A Slack single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="edb66-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="edb66-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="edb66-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="edb66-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="edb66-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="edb66-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="edb66-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="edb66-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="edb66-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="edb66-118">Scenario description</span></span>
<span data-ttu-id="edb66-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="edb66-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="edb66-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="edb66-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="edb66-121">從 hello 圖庫加入 Slack</span><span class="sxs-lookup"><span data-stu-id="edb66-121">Adding Slack from hello gallery</span></span>
2. <span data-ttu-id="edb66-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="edb66-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-slack-from-hello-gallery"></a><span data-ttu-id="edb66-123">從 hello 圖庫加入 Slack</span><span class="sxs-lookup"><span data-stu-id="edb66-123">Adding Slack from hello gallery</span></span>
<span data-ttu-id="edb66-124">tooconfigure hello Slack 至 Azure AD 整合，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Slack。</span><span class="sxs-lookup"><span data-stu-id="edb66-124">tooconfigure hello integration of Slack into Azure AD, you need tooadd Slack from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="edb66-125">**tooadd Slack hello 圖庫中，從執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="edb66-125">**tooadd Slack from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="edb66-126">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="edb66-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="edb66-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="edb66-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="edb66-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="edb66-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="edb66-131">tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="edb66-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="edb66-133">在 [hello] 搜尋方塊中，輸入**Slack**。</span><span class="sxs-lookup"><span data-stu-id="edb66-133">In hello search box, type **Slack**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-slack-tutorial/tutorial_slack_search.png)

5. <span data-ttu-id="edb66-135">在 [hello [結果] 窗格中，選取 [ **Slack**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="edb66-135">In hello results panel, select **Slack**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-slack-tutorial/tutorial_slack_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="edb66-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="edb66-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="edb66-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Slack 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="edb66-138">In this section, you configure and test Azure AD single sign-on with Slack based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="edb66-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Slack 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="edb66-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Slack is tooa user in Azure AD.</span></span> <span data-ttu-id="edb66-140">換句話說，Azure AD 使用者與 hello Slack 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="edb66-140">In other words, a link relationship between an Azure AD user and hello related user in Slack needs toobe established.</span></span>

<span data-ttu-id="edb66-141">Slack 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="edb66-141">In Slack, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="edb66-142">tooconfigure 及測試 Azure AD 單一登入 Slack，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="edb66-142">tooconfigure and test Azure AD single sign-on with Slack, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="edb66-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="edb66-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="edb66-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="edb66-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="edb66-145">**[建立 Slack 的測試使用者](#creating-a-slack-test-user)** -toohave 許 Simon Slack 是連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="edb66-145">**[Creating a Slack test user](#creating-a-slack-test-user)** - toohave a counterpart of Britta Simon in Slack that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="edb66-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="edb66-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="edb66-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="edb66-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="edb66-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="edb66-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="edb66-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Slack 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="edb66-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Slack application.</span></span>

<span data-ttu-id="edb66-150">**tooconfigure Azure AD 單一登入 Slack，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="edb66-150">**tooconfigure Azure AD single sign-on with Slack, perform hello following steps:**</span></span>

1. <span data-ttu-id="edb66-151">在 Azure 入口網站上 hello hello **Slack**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="edb66-151">In hello Azure portal, on hello **Slack** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="edb66-153">在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="edb66-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-slack-tutorial/tutorial_slack_samlbase.png)

3. <span data-ttu-id="edb66-155">在 [hello **Slack 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="edb66-155">On hello **Slack Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-slack-tutorial/tutorial_slack_url.png)

    <span data-ttu-id="edb66-157">a.</span><span class="sxs-lookup"><span data-stu-id="edb66-157">a.</span></span> <span data-ttu-id="edb66-158">在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.slack.com`</span><span class="sxs-lookup"><span data-stu-id="edb66-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.slack.com`</span></span>

    <span data-ttu-id="edb66-159">b.</span><span class="sxs-lookup"><span data-stu-id="edb66-159">b.</span></span> <span data-ttu-id="edb66-160">在 [hello**識別碼**文字方塊中，型別 hello URL:`https://slack.com`</span><span class="sxs-lookup"><span data-stu-id="edb66-160">In hello **Identifier** textbox, type hello URL: `https://slack.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="edb66-161">hello 值不是真正的。</span><span class="sxs-lookup"><span data-stu-id="edb66-161">hello value is not real.</span></span> <span data-ttu-id="edb66-162">您有 tooupdate hello 值與 hello 實際登入 URL。</span><span class="sxs-lookup"><span data-stu-id="edb66-162">You have tooupdate hello value with hello actual Sign On URL.</span></span> <span data-ttu-id="edb66-163">請連絡[Slack 的技術支援小組](https://slack.com/help/contact)tooget hello 值</span><span class="sxs-lookup"><span data-stu-id="edb66-163">Contact [Slack support team](https://slack.com/help/contact) tooget hello value</span></span>
     
4. <span data-ttu-id="edb66-164">Slack 的應用程式預期 hello SAML 判斷提示，以特定格式。</span><span class="sxs-lookup"><span data-stu-id="edb66-164">Slack application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="edb66-165">設定下列宣告為此應用程式的 hello。</span><span class="sxs-lookup"><span data-stu-id="edb66-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="edb66-166">您可以從 hello 管理 hello 這些屬性的值"**使用者屬性**」 一節，在應用程式整合頁面上。</span><span class="sxs-lookup"><span data-stu-id="edb66-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="edb66-167">hello 下列螢幕擷取畫面會顯示這個範例。</span><span class="sxs-lookup"><span data-stu-id="edb66-167">hello following screenshot shows an example for this.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute.png)

5. <span data-ttu-id="edb66-169">在 hello**使用者屬性**hello 區段**單一登入**對話方塊中，選取**user.mail**為**使用者識別碼**和每個資料列所示hello 在表中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="edb66-169">In hello **User Attributes** section on hello **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in hello table below, perform hello following steps:</span></span>
    
    | <span data-ttu-id="edb66-170">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="edb66-170">Attribute Name</span></span> | <span data-ttu-id="edb66-171">屬性值</span><span class="sxs-lookup"><span data-stu-id="edb66-171">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="edb66-172">first_name</span><span class="sxs-lookup"><span data-stu-id="edb66-172">first_name</span></span> | <span data-ttu-id="edb66-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="edb66-173">user.givenname</span></span> |
    | <span data-ttu-id="edb66-174">last_name</span><span class="sxs-lookup"><span data-stu-id="edb66-174">last_name</span></span> | <span data-ttu-id="edb66-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="edb66-175">user.surname</span></span> |
    | <span data-ttu-id="edb66-176">User.Email</span><span class="sxs-lookup"><span data-stu-id="edb66-176">User.Email</span></span> | <span data-ttu-id="edb66-177">user.mail</span><span class="sxs-lookup"><span data-stu-id="edb66-177">user.mail</span></span> |  
    | <span data-ttu-id="edb66-178">User.Username</span><span class="sxs-lookup"><span data-stu-id="edb66-178">User.Username</span></span> | <span data-ttu-id="edb66-179">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="edb66-179">user.userprincipalname</span></span> |

    <span data-ttu-id="edb66-180">a.</span><span class="sxs-lookup"><span data-stu-id="edb66-180">a.</span></span> <span data-ttu-id="edb66-181">按一下**屬性**tooopen**編輯屬性**對話方塊方塊，並執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="edb66-181">Click on **Attribute** tooopen **Edit Attribute** dialog box and perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute1.png)

    <span data-ttu-id="edb66-183">a.</span><span class="sxs-lookup"><span data-stu-id="edb66-183">a.</span></span> <span data-ttu-id="edb66-184">在 [hello**名稱**文字方塊中，該資料列所顯示的型別 hello 屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="edb66-184">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="edb66-185">b.</span><span class="sxs-lookup"><span data-stu-id="edb66-185">b.</span></span> <span data-ttu-id="edb66-186">從 hello**值**清單，顯示該資料列選取 hello 屬性值。</span><span class="sxs-lookup"><span data-stu-id="edb66-186">From hello **Value** list, select hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="edb66-187">c.</span><span class="sxs-lookup"><span data-stu-id="edb66-187">c.</span></span> <span data-ttu-id="edb66-188">按一下 [檔案] &gt; [新增] &gt; [專案] </span><span class="sxs-lookup"><span data-stu-id="edb66-188">Click **OK**</span></span>

6. <span data-ttu-id="edb66-189">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="edb66-189">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-slack-tutorial/tutorial_slack_certificate.png)

7. <span data-ttu-id="edb66-191">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="edb66-191">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-slack-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="edb66-193">在 [hello **Slack 組態**區段中，按一下**設定 Slack** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="edb66-193">On hello **Slack Configuration** section, click **Configure Slack** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="edb66-194">複製 hello **SAML 實體識別碼和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="edb66-194">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-slack-tutorial/tutorial_slack_configure.png) 

9.  <span data-ttu-id="edb66-196">在不同的網頁瀏覽器視窗中，系統管理員身分登入 tooyour Slack 公司網站。</span><span class="sxs-lookup"><span data-stu-id="edb66-196">In a different web browser window, log in tooyour Slack company site as an administrator.</span></span>

10.  <span data-ttu-id="edb66-197">瀏覽過**Microsoft Azure AD**然後跳過**小組設定**。</span><span class="sxs-lookup"><span data-stu-id="edb66-197">Navigate too**Microsoft Azure AD** then go too**Team Settings**.</span></span>

     ![在應用程式端設定單一登入](./media/active-directory-saas-slack-tutorial/tutorial_slack_001.png)

11.  <span data-ttu-id="edb66-199">在 [hello**小組設定**區段中，按一下 hello**驗證**索引標籤，然後再按一下**變更設定**。</span><span class="sxs-lookup"><span data-stu-id="edb66-199">In hello **Team Settings** section, click hello **Authentication** tab, and then click **Change Settings**.</span></span>

     ![在應用程式端設定單一登入](./media/active-directory-saas-slack-tutorial/tutorial_slack_002.png)

12. <span data-ttu-id="edb66-201">在 [hello **SAML 驗證設定**] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="edb66-201">On hello **SAML Authentication Settings** dialog, perform hello following steps:</span></span>

    ![在應用程式端設定單一登入](./media/active-directory-saas-slack-tutorial/tutorial_slack_003.png)

    <span data-ttu-id="edb66-203">a.</span><span class="sxs-lookup"><span data-stu-id="edb66-203">a.</span></span>  <span data-ttu-id="edb66-204">在 [hello **SAML 2.0 端點 (HTTP)**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="edb66-204">In hello **SAML 2.0 Endpoint (HTTP)** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="edb66-205">b.</span><span class="sxs-lookup"><span data-stu-id="edb66-205">b.</span></span>  <span data-ttu-id="edb66-206">在 [hello**身分識別提供者簽發者**文字方塊中，貼上 hello 值**SAML 實體識別碼**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="edb66-206">In hello **Identity Provider Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="edb66-207">c.</span><span class="sxs-lookup"><span data-stu-id="edb66-207">c.</span></span>  <span data-ttu-id="edb66-208">在 [記事本]，複製到剪貼簿，其內容的 hello 中開啟下載的憑證檔案，然後將它貼入 toohello**公開憑證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="edb66-208">Open your downloaded certificate file in notepad, copy hello content of it into your clipboard, and then paste it toohello **Public Certificate** textbox.</span></span>

    <span data-ttu-id="edb66-209">d.</span><span class="sxs-lookup"><span data-stu-id="edb66-209">d.</span></span> <span data-ttu-id="edb66-210">視您的 Slack 小組設定 hello 上面的三個設定。</span><span class="sxs-lookup"><span data-stu-id="edb66-210">Configure hello above three settings as appropriate for your Slack team.</span></span> <span data-ttu-id="edb66-211">如需 hello 設定的詳細資訊，請尋找 hello **Slack 的 SSO 設定指南**這裡。</span><span class="sxs-lookup"><span data-stu-id="edb66-211">For more information about hello settings, please find hello **Slack's SSO configuration guide** here.</span></span> `https://get.slack.help/hc/articles/220403548-Guide-to-single-sign-on-with-Slack%60`

    <span data-ttu-id="edb66-212">e.</span><span class="sxs-lookup"><span data-stu-id="edb66-212">e.</span></span>  <span data-ttu-id="edb66-213">按一下 [儲存組態] 。</span><span class="sxs-lookup"><span data-stu-id="edb66-213">Click **Save Configuration**.</span></span>
     
    <!-- Deselect **Allow users toochange their email address**.

    e.  Select **Allow users toochoose their own username**.

    f.  As **Authentication for your team must be used by**, select **It’s optional**. -->

> [!TIP]
> <span data-ttu-id="edb66-214">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="edb66-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="edb66-215">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="edb66-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="edb66-216">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="edb66-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="edb66-217">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="edb66-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="edb66-218">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="edb66-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="edb66-220">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="edb66-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="edb66-221">在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="edb66-221">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-slack-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="edb66-223">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="edb66-223">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-slack-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="edb66-225">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="edb66-225">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-slack-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="edb66-227">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="edb66-227">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-slack-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="edb66-229">a.</span><span class="sxs-lookup"><span data-stu-id="edb66-229">a.</span></span> <span data-ttu-id="edb66-230">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="edb66-230">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="edb66-231">b.</span><span class="sxs-lookup"><span data-stu-id="edb66-231">b.</span></span> <span data-ttu-id="edb66-232">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="edb66-232">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="edb66-233">c.</span><span class="sxs-lookup"><span data-stu-id="edb66-233">c.</span></span> <span data-ttu-id="edb66-234">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="edb66-234">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="edb66-235">d.</span><span class="sxs-lookup"><span data-stu-id="edb66-235">d.</span></span> <span data-ttu-id="edb66-236">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="edb66-236">Click **Create**.</span></span>
 
### <a name="creating-a-slack-test-user"></a><span data-ttu-id="edb66-237">建立 Slack 測試使用者</span><span class="sxs-lookup"><span data-stu-id="edb66-237">Creating a Slack test user</span></span>

<span data-ttu-id="edb66-238">hello 本節目標在於 toocreate 呼叫許 Simon Slack 的使用者。</span><span class="sxs-lookup"><span data-stu-id="edb66-238">hello objective of this section is toocreate a user called Britta Simon in Slack.</span></span> <span data-ttu-id="edb66-239">Slack 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="edb66-239">Slack supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="edb66-240">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="edb66-240">There is no action item for you in this section.</span></span> <span data-ttu-id="edb66-241">如果尚未存在期間嘗試 tooaccess Slack，建立新的使用者。</span><span class="sxs-lookup"><span data-stu-id="edb66-241">A new user is created during an attempt tooaccess Slack if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="edb66-242">若要手動 toocreate 使用者，您需要 tooContact [Slack 的技術支援小組](https://slack.com/help/contact)。</span><span class="sxs-lookup"><span data-stu-id="edb66-242">If you need toocreate a user manually, you need tooContact [Slack support team](https://slack.com/help/contact).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="edb66-243">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="edb66-243">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="edb66-244">在本節中，您可以授與存取 tooSlack 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="edb66-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSlack.</span></span>

![指派使用者][200] 

<span data-ttu-id="edb66-246">**tooassign 許 Simon tooSlack，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="edb66-246">**tooassign Britta Simon tooSlack, perform hello following steps:**</span></span>

1. <span data-ttu-id="edb66-247">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="edb66-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="edb66-249">在 [hello] 應用程式清單中，選取**Slack**。</span><span class="sxs-lookup"><span data-stu-id="edb66-249">In hello applications list, select **Slack**.</span></span>

    ![設定單一登入](./media/active-directory-saas-slack-tutorial/tutorial_slack_app.png) 

3. <span data-ttu-id="edb66-251">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="edb66-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="edb66-253">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="edb66-253">Click **Add** button.</span></span> <span data-ttu-id="edb66-254">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="edb66-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="edb66-256">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="edb66-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="edb66-257">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="edb66-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="edb66-258">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="edb66-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="edb66-259">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="edb66-259">Testing single sign-on</span></span>

<span data-ttu-id="edb66-260">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="edb66-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="edb66-261">當您按一下 hello Slack 磚中的 hello 存取面板，您應該取得 tooyour 自動登入 Slack 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="edb66-261">When you click hello Slack tile in hello Access Panel, you should get automatically signed-on tooyour Slack application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="edb66-262">其他資源</span><span class="sxs-lookup"><span data-stu-id="edb66-262">Additional resources</span></span>

* [<span data-ttu-id="edb66-263">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="edb66-263">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="edb66-264">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="edb66-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-slack-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-slack-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-slack-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-slack-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-slack-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-slack-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-slack-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-slack-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-slack-tutorial/tutorial_general_203.png

