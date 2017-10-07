---
title: "教學課程：Azure Active Directory 與 TimeOffManager 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 TimeOffManager 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3685912f-d5aa-4730-ab58-35a088fc1cc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: c871257bfb49883e31b1c4860a9d7faa70e9ab48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-timeoffmanager"></a><span data-ttu-id="7ccd3-103">教學課程：Azure Active Directory 與 TimeOffManager 整合</span><span class="sxs-lookup"><span data-stu-id="7ccd3-103">Tutorial: Azure Active Directory integration with TimeOffManager</span></span>

<span data-ttu-id="7ccd3-104">在此教學課程中，您學會如何 toointegrate TimeOffManager 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-104">In this tutorial, you learn how toointegrate TimeOffManager with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7ccd3-105">與 Azure AD 整合 TimeOffManager 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="7ccd3-105">Integrating TimeOffManager with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7ccd3-106">您可以控制存取 tooTimeOffManager Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="7ccd3-106">You can control in Azure AD who has access tooTimeOffManager</span></span>
- <span data-ttu-id="7ccd3-107">您可以啟用您的使用者 tooautomatically get 登入 tooTimeOffManager （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="7ccd3-107">You can enable your users tooautomatically get signed-on tooTimeOffManager (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7ccd3-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="7ccd3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7ccd3-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ccd3-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="7ccd3-110">Prerequisites</span></span>

<span data-ttu-id="7ccd3-111">tooconfigure 與 TimeOffManager 的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="7ccd3-111">tooconfigure Azure AD integration with TimeOffManager, you need hello following items:</span></span>

- <span data-ttu-id="7ccd3-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7ccd3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7ccd3-113">啟用 TimeOffManager 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7ccd3-113">A TimeOffManager single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7ccd3-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7ccd3-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="7ccd3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7ccd3-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7ccd3-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7ccd3-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="7ccd3-118">Scenario description</span></span>
<span data-ttu-id="7ccd3-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7ccd3-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="7ccd3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7ccd3-121">從 hello 圖庫新增 TimeOffManager</span><span class="sxs-lookup"><span data-stu-id="7ccd3-121">Add TimeOffManager from hello gallery</span></span>
2. <span data-ttu-id="7ccd3-122">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7ccd3-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-timeoffmanager-from-hello-gallery"></a><span data-ttu-id="7ccd3-123">從 hello 圖庫新增 TimeOffManager</span><span class="sxs-lookup"><span data-stu-id="7ccd3-123">Add TimeOffManager from hello gallery</span></span>
<span data-ttu-id="7ccd3-124">tooconfigure hello 整合 TimeOffManager 的 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd TimeOffManager。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-124">tooconfigure hello integration of TimeOffManager into Azure AD, you need tooadd TimeOffManager from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7ccd3-125">**tooadd TimeOffManager 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="7ccd3-125">**tooadd TimeOffManager from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7ccd3-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7ccd3-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7ccd3-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="7ccd3-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="7ccd3-133">在 [hello] 搜尋方塊中，輸入**TimeOffManager**，選取**TimeOffManager**從結果面板，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-133">In hello search box, type **TimeOffManager**, select **TimeOffManager** from result panel and then click **Add** button tooadd hello application.</span></span>

    ![從資源庫新增](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7ccd3-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7ccd3-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="7ccd3-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 TimeOffManager 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-136">In this section, you configure and test Azure AD single sign-on with TimeOffManager based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7ccd3-137">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 TimeOffManager 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TimeOffManager is tooa user in Azure AD.</span></span> <span data-ttu-id="7ccd3-138">換句話說，Azure AD 使用者與 hello TimeOffManager 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-138">In other words, a link relationship between an Azure AD user and hello related user in TimeOffManager needs toobe established.</span></span>

<span data-ttu-id="7ccd3-139">TimeOffManager 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-139">In TimeOffManager, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7ccd3-140">tooconfigure 及測試 Azure AD 單一登入 TimeOffManager，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="7ccd3-140">tooconfigure and test Azure AD single sign-on with TimeOffManager, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7ccd3-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7ccd3-142">**[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7ccd3-143">**[建立測試使用者 TimeOffManager](#create-a-timeoffmanager-test-user)**  -toohave 許 Simon TimeOffManager 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-143">**[Create a TimeOffManager test user](#create-a-timeoffmanager-test-user)** - toohave a counterpart of Britta Simon in TimeOffManager that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7ccd3-144">**[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7ccd3-145">**[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7ccd3-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7ccd3-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7ccd3-147">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 TimeOffManager 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TimeOffManager application.</span></span>

<span data-ttu-id="7ccd3-148">**tooconfigure Azure AD 單一登入 TimeOffManager，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="7ccd3-148">**tooconfigure Azure AD single sign-on with TimeOffManager, perform hello following steps:**</span></span>

1. <span data-ttu-id="7ccd3-149">在 Azure 入口網站上 hello hello **TimeOffManager**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-149">In hello Azure portal, on hello **TimeOffManager** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="7ccd3-151">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![SAML 型登入](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_samlbase.png)

3. <span data-ttu-id="7ccd3-153">在 hello **TimeOffManager 網域和 Url**區段中，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="7ccd3-153">On hello **TimeOffManager Domain and URLs** section, perform hello following:</span></span>

     ![[TimeOffManager 網域與 URL] 區段](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_url.png)

    <span data-ttu-id="7ccd3-155">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`</span><span class="sxs-lookup"><span data-stu-id="7ccd3-155">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7ccd3-156">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-156">This value is not real.</span></span> <span data-ttu-id="7ccd3-157">更新此值與 hello 實際的回覆 URL。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-157">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="7ccd3-158">您可以取得此值從**單一登入設定 頁面**這稍後會加以說明 hello 教學課程中或連絡[TimeOffManager 支援小組](http://www.timeoffmanager.com/contact-us.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-158">You can get this value from **Single Sign on settings page** which is explained later in hello tutorial or Contact [TimeOffManager support team](http://www.timeoffmanager.com/contact-us.aspx).</span></span>
 
4. <span data-ttu-id="7ccd3-159">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-159">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![[SAML 簽署憑證] 區段](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_certificate.png) 

5. <span data-ttu-id="7ccd3-161">hello 本節目標在於的 toooutline tooenable 使用者 tooauthenticate tooTimeOffManger 的同盟，使用 Azure AD 的帳戶與如何 hello SAML 通訊協定為基礎。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-161">hello objective of this section is toooutline how tooenable users tooauthenticate tooTimeOffManger with their account in Azure AD using federation based on hello SAML protocol.</span></span>
    
    <span data-ttu-id="7ccd3-162">TimeOffManger 應用程式預期 hello SAML 判斷提示，以特定格式，這需要您 tooadd 自訂屬性對應 tooyour SAML token 屬性設定。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-162">Your TimeOffManger application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="7ccd3-163">hello 下列螢幕擷取畫面會顯示這個範例。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-163">hello following screenshot shows an example for this.</span></span>

    <span data-ttu-id="7ccd3-164">![saml 權杖屬性](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "saml 權杖屬性")</span><span class="sxs-lookup"><span data-stu-id="7ccd3-164">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "saml token attributes")</span></span>
    
    | <span data-ttu-id="7ccd3-165">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="7ccd3-165">Attribute Name</span></span> | <span data-ttu-id="7ccd3-166">屬性值</span><span class="sxs-lookup"><span data-stu-id="7ccd3-166">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="7ccd3-167">Firstname</span><span class="sxs-lookup"><span data-stu-id="7ccd3-167">Firstname</span></span> |<span data-ttu-id="7ccd3-168">User.givenname</span><span class="sxs-lookup"><span data-stu-id="7ccd3-168">User.givenname</span></span> |
    | <span data-ttu-id="7ccd3-169">lastname</span><span class="sxs-lookup"><span data-stu-id="7ccd3-169">Lastname</span></span> |<span data-ttu-id="7ccd3-170">User.surname</span><span class="sxs-lookup"><span data-stu-id="7ccd3-170">User.surname</span></span> |
    | <span data-ttu-id="7ccd3-171">電子郵件</span><span class="sxs-lookup"><span data-stu-id="7ccd3-171">Email</span></span> |<span data-ttu-id="7ccd3-172">User.mail</span><span class="sxs-lookup"><span data-stu-id="7ccd3-172">User.mail</span></span> |
    
    <span data-ttu-id="7ccd3-173">a.</span><span class="sxs-lookup"><span data-stu-id="7ccd3-173">a.</span></span>  <span data-ttu-id="7ccd3-174">上述的 hello 資料表中每個資料列，按一下 **新增使用者屬性**。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-174">For each data row in hello table above, click **add user attribute**.</span></span>
    
    <span data-ttu-id="7ccd3-175">![saml 權杖屬性](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "saml 權杖屬性")</span><span class="sxs-lookup"><span data-stu-id="7ccd3-175">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "saml token attributes")</span></span>
    
    <span data-ttu-id="7ccd3-176">![saml 權杖屬性](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "saml 權杖屬性")</span><span class="sxs-lookup"><span data-stu-id="7ccd3-176">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "saml token attributes")</span></span>
    
    <span data-ttu-id="7ccd3-177">b.</span><span class="sxs-lookup"><span data-stu-id="7ccd3-177">b.</span></span>  <span data-ttu-id="7ccd3-178">在 hello**屬性名稱**文字方塊中，該資料列所顯示的型別 hello 屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-178">In hello **Attribute Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="7ccd3-179">c.</span><span class="sxs-lookup"><span data-stu-id="7ccd3-179">c.</span></span>  <span data-ttu-id="7ccd3-180">在 hello**屬性值**文字方塊中，顯示該資料列選取 hello 屬性值。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-180">In hello **Attribute Value** textbox, select hello attribute  value shown for that row.</span></span>
    
    <span data-ttu-id="7ccd3-181">d.</span><span class="sxs-lookup"><span data-stu-id="7ccd3-181">d.</span></span>  <span data-ttu-id="7ccd3-182">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-182">Click **Ok**.</span></span>
    
6. <span data-ttu-id="7ccd3-183">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-183">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="7ccd3-185">在 hello **TimeOffManager 組態**區段中，按一下**設定 TimeOffManager** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-185">On hello **TimeOffManager Configuration** section, click **Configure TimeOffManager** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7ccd3-186">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="7ccd3-186">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![[TimeOffManager 設定] 區段](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_configure.png) 

8. <span data-ttu-id="7ccd3-188">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 TimeOffManager 公司網站。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-188">In a different web browser window, log into your TimeOffManager company site as an administrator.</span></span>

9. <span data-ttu-id="7ccd3-189">跳過**帳戶\>帳戶選項\>單一登入設定**。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-189">Go too**Account \> Account Options \> Single Sign-On Settings**.</span></span>
   
   <span data-ttu-id="7ccd3-190">![單一登入設定](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "單一登入設定")</span><span class="sxs-lookup"><span data-stu-id="7ccd3-190">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "Single Sign-On Settings")</span></span>
7. <span data-ttu-id="7ccd3-191">在 hello**單一登入設定**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="7ccd3-191">In hello **Single Sign-On Settings** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="7ccd3-192">![單一登入設定](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "單一登入設定")</span><span class="sxs-lookup"><span data-stu-id="7ccd3-192">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "Single Sign-On Settings")</span></span>
   
   <span data-ttu-id="7ccd3-193">a.</span><span class="sxs-lookup"><span data-stu-id="7ccd3-193">a.</span></span> <span data-ttu-id="7ccd3-194">在記事本中，複製到剪貼簿，其內容的 hello 中開啟 base-64 編碼的憑證，然後貼上 hello 整個憑證**X.509 憑證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-194">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste hello entire Certificate into **X.509 Certificate** textbox.</span></span>
   
   <span data-ttu-id="7ccd3-195">b.</span><span class="sxs-lookup"><span data-stu-id="7ccd3-195">b.</span></span> <span data-ttu-id="7ccd3-196">在**Idp 簽發者**文字方塊中，貼上 hello 值**SAML 實體識別碼**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-196">In **Idp Issuer** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="7ccd3-197">c.</span><span class="sxs-lookup"><span data-stu-id="7ccd3-197">c.</span></span> <span data-ttu-id="7ccd3-198">在**IdP 端點 URL**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-198">In **IdP Endpoint URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="7ccd3-199">d.</span><span class="sxs-lookup"><span data-stu-id="7ccd3-199">d.</span></span> <span data-ttu-id="7ccd3-200">在 [強制 SAML] 選取 [否]。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-200">As **Enforce SAML**, select **No**.</span></span>
   
   <span data-ttu-id="7ccd3-201">e.</span><span class="sxs-lookup"><span data-stu-id="7ccd3-201">e.</span></span> <span data-ttu-id="7ccd3-202">在 [自動建立使用者] 選取 [是]。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-202">As **Auto-Create Users**, select **Yes**.</span></span>
   
   <span data-ttu-id="7ccd3-203">f.</span><span class="sxs-lookup"><span data-stu-id="7ccd3-203">f.</span></span> <span data-ttu-id="7ccd3-204">在**登出 URL**文字方塊中，貼上 hello 值**登出 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-204">In **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="7ccd3-205">g.</span><span class="sxs-lookup"><span data-stu-id="7ccd3-205">g.</span></span> <span data-ttu-id="7ccd3-206">按一下 [儲存變更]。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-206">click **Save Changes**.</span></span>

11. <span data-ttu-id="7ccd3-207">在**單一登入設定**頁面上，複製 hello 值**判斷提示取用者服務 URL**並將它貼在 hello**回覆 URL**底下的文字方塊**TimeOffManager網域和 Url** Azure 入口網站中的區段。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-207">In **Single Sign on settings** page, copy hello value of **Assertion Consumer Service URL** and paste it in hello **Reply URL** text box under **TimeOffManager Domain and URLs** section in Azure portal.</span></span> 

      <span data-ttu-id="7ccd3-208">![單一登入設定](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "單一登入設定")</span><span class="sxs-lookup"><span data-stu-id="7ccd3-208">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "Single Sign-On Settings")</span></span>

> [!TIP]
> <span data-ttu-id="7ccd3-209">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="7ccd3-209">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7ccd3-210">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-210">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7ccd3-211">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7ccd3-211">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7ccd3-212">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7ccd3-212">Create an Azure AD test user</span></span>
<span data-ttu-id="7ccd3-213">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-213">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="7ccd3-215">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="7ccd3-215">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7ccd3-216">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-216">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7ccd3-218">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-218">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![[使用者和群組] --> [所有使用者]](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7ccd3-220">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-220">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![[新增] 按鈕](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7ccd3-222">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="7ccd3-222">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![使用者對話方塊頁面](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7ccd3-224">a.</span><span class="sxs-lookup"><span data-stu-id="7ccd3-224">a.</span></span> <span data-ttu-id="7ccd3-225">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-225">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7ccd3-226">b.</span><span class="sxs-lookup"><span data-stu-id="7ccd3-226">b.</span></span> <span data-ttu-id="7ccd3-227">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-227">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7ccd3-228">c.</span><span class="sxs-lookup"><span data-stu-id="7ccd3-228">c.</span></span> <span data-ttu-id="7ccd3-229">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-229">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7ccd3-230">d.</span><span class="sxs-lookup"><span data-stu-id="7ccd3-230">d.</span></span> <span data-ttu-id="7ccd3-231">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-231">Click **Create**.</span></span>
 
### <a name="create-a-timeoffmanager-test-user"></a><span data-ttu-id="7ccd3-232">建立 TimeOffManager 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7ccd3-232">Create a TimeOffManager test user</span></span>

<span data-ttu-id="7ccd3-233">在順序 tooenable Azure AD 使用者 toolog 入 TimeOffManager，它們必須已佈建的 tooTimeOffManager。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-233">In order tooenable Azure AD users toolog into TimeOffManager, they must be provisioned tooTimeOffManager.</span></span>  

<span data-ttu-id="7ccd3-234">TimeOffManager 支援即時使用者佈建。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-234">TimeOffManager supports just in time user provisioning.</span></span> <span data-ttu-id="7ccd3-235">沒有您適用的動作項目。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-235">There is no action item for you.</span></span>  

<span data-ttu-id="7ccd3-236">會自動在 hello 第一個登入使用單一登入期間新增 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-236">hello users are added automatically during hello first login using single sign on.</span></span>

>[!NOTE]
><span data-ttu-id="7ccd3-237">您可以使用任何其他 TimeOffManager 使用者帳戶建立工具或 Api 提供 TimeOffManager tooprovision Azure AD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-237">You can use any other TimeOffManager user account creation tools or APIs provided by TimeOffManager tooprovision Azure AD user accounts.</span></span>
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="7ccd3-238">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7ccd3-238">Assign hello Azure AD test user</span></span>

<span data-ttu-id="7ccd3-239">在本節中，您可以授與存取 tooTimeOffManager 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-239">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTimeOffManager.</span></span>

![指派使用者][200] 

<span data-ttu-id="7ccd3-241">**tooassign 許 Simon tooTimeOffManager，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="7ccd3-241">**tooassign Britta Simon tooTimeOffManager, perform hello following steps:**</span></span>

1. <span data-ttu-id="7ccd3-242">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-242">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="7ccd3-244">在 [hello] 應用程式清單中，選取**TimeOffManager**。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-244">In hello applications list, select **TimeOffManager**.</span></span>

    ![應用程式清單中的 TimeOffManager](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_app.png) 

3. <span data-ttu-id="7ccd3-246">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-246">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="7ccd3-248">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-248">Click **Add** button.</span></span> <span data-ttu-id="7ccd3-249">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="7ccd3-251">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-251">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7ccd3-252">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7ccd3-253">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7ccd3-254">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="7ccd3-254">Test single sign-on</span></span>

<span data-ttu-id="7ccd3-255">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-255">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7ccd3-256">當您按一下 hello TimeOffManager 磚 hello 存取面板中的時，您應該取得自動登入 tooyour TimeOffManager 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-256">When you click hello TimeOffManager tile in hello Access Panel, you should get automatically signed-on tooyour TimeOffManager application.</span></span> <span data-ttu-id="7ccd3-257">如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="7ccd3-257">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7ccd3-258">其他資源</span><span class="sxs-lookup"><span data-stu-id="7ccd3-258">Additional resources</span></span>

* [<span data-ttu-id="7ccd3-259">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7ccd3-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7ccd3-260">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="7ccd3-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_203.png

