---
title: "教學課程：Azure Active Directory 與 PolicyStat 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 PolicyStat 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: af5eb0f1-1c8e-4809-b0c4-8ccfb915ca42
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 868053cd0d37359fd9b4aeb93dba42cbbaa09845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-policystat"></a><span data-ttu-id="39b57-103">教學課程：Azure Active Directory 與 PolicyStat 整合</span><span class="sxs-lookup"><span data-stu-id="39b57-103">Tutorial: Azure Active Directory integration with PolicyStat</span></span>

<span data-ttu-id="39b57-104">在此教學課程中，您學會如何 toointegrate PolicyStat 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="39b57-104">In this tutorial, you learn how toointegrate PolicyStat with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="39b57-105">與 Azure AD 整合 PolicyStat 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="39b57-105">Integrating PolicyStat with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="39b57-106">您可以控制存取 tooPolicyStat Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="39b57-106">You can control in Azure AD who has access tooPolicyStat</span></span>
- <span data-ttu-id="39b57-107">您可以啟用您的使用者 tooautomatically get 登入 tooPolicyStat （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="39b57-107">You can enable your users tooautomatically get signed-on tooPolicyStat (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="39b57-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="39b57-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="39b57-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="39b57-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="39b57-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="39b57-110">Prerequisites</span></span>

<span data-ttu-id="39b57-111">tooconfigure PolicyStat 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="39b57-111">tooconfigure Azure AD integration with PolicyStat, you need hello following items:</span></span>

- <span data-ttu-id="39b57-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="39b57-112">An Azure AD subscription</span></span>
- <span data-ttu-id="39b57-113">啟用 PolicyStat 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="39b57-113">A PolicyStat single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="39b57-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="39b57-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="39b57-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="39b57-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="39b57-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="39b57-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="39b57-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="39b57-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="39b57-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="39b57-118">Scenario description</span></span>
<span data-ttu-id="39b57-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="39b57-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="39b57-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="39b57-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="39b57-121">從 hello 圖庫加入 PolicyStat</span><span class="sxs-lookup"><span data-stu-id="39b57-121">Adding PolicyStat from hello gallery</span></span>
2. <span data-ttu-id="39b57-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="39b57-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-policystat-from-hello-gallery"></a><span data-ttu-id="39b57-123">從 hello 圖庫加入 PolicyStat</span><span class="sxs-lookup"><span data-stu-id="39b57-123">Adding PolicyStat from hello gallery</span></span>
<span data-ttu-id="39b57-124">tooconfigure hello 整合 PolicyStat 到 Azure AD，您需要 tooadd PolicyStat hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="39b57-124">tooconfigure hello integration of PolicyStat into Azure AD, you need tooadd PolicyStat from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="39b57-125">**tooadd PolicyStat 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="39b57-125">**tooadd PolicyStat from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="39b57-126">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="39b57-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="39b57-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="39b57-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="39b57-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="39b57-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="39b57-131">tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="39b57-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="39b57-133">在 [hello] 搜尋方塊中，輸入**PolicyStat**。</span><span class="sxs-lookup"><span data-stu-id="39b57-133">In hello search box, type **PolicyStat**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_search.png)

5. <span data-ttu-id="39b57-135">在 [hello [結果] 窗格中，選取 [ **PolicyStat**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="39b57-135">In hello results panel, select **PolicyStat**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="39b57-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="39b57-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="39b57-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 PolicyStat 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="39b57-138">In this section, you configure and test Azure AD single sign-on with PolicyStat based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="39b57-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 PolicyStat 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="39b57-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PolicyStat is tooa user in Azure AD.</span></span> <span data-ttu-id="39b57-140">換句話說，Azure AD 使用者與 hello PolicyStat 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="39b57-140">In other words, a link relationship between an Azure AD user and hello related user in PolicyStat needs toobe established.</span></span>

<span data-ttu-id="39b57-141">PolicyStat 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="39b57-141">In PolicyStat, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="39b57-142">tooconfigure 及 PolicyStat 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="39b57-142">tooconfigure and test Azure AD single sign-on with PolicyStat, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="39b57-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="39b57-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="39b57-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="39b57-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="39b57-145">**[建立測試使用者 PolicyStat](#creating-a-policystat-test-user) ** -toohave 許 Simon PolicyStat 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="39b57-145">**[Creating a PolicyStat test user](#creating-a-policystat-test-user)** - toohave a counterpart of Britta Simon in PolicyStat that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="39b57-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="39b57-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="39b57-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="39b57-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="39b57-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="39b57-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="39b57-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 PolicyStat 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="39b57-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your PolicyStat application.</span></span>

<span data-ttu-id="39b57-150">**tooconfigure Azure AD 單一登入與 PolicyStat，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="39b57-150">**tooconfigure Azure AD single sign-on with PolicyStat, perform hello following steps:**</span></span>

1. <span data-ttu-id="39b57-151">在 Azure 入口網站上 hello hello **PolicyStat**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="39b57-151">In hello Azure portal, on hello **PolicyStat** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="39b57-153">在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="39b57-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_samlbase.png)

3. <span data-ttu-id="39b57-155">在 [hello **PolicyStat 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="39b57-155">On hello **PolicyStat Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_url.png)

    <span data-ttu-id="39b57-157">a.</span><span class="sxs-lookup"><span data-stu-id="39b57-157">a.</span></span> <span data-ttu-id="39b57-158">在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.policystat.com`</span><span class="sxs-lookup"><span data-stu-id="39b57-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.policystat.com`</span></span>

    <span data-ttu-id="39b57-159">b.</span><span class="sxs-lookup"><span data-stu-id="39b57-159">b.</span></span> <span data-ttu-id="39b57-160">在 [hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.policystat.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="39b57-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.policystat.com/saml2/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="39b57-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="39b57-161">These values are not real.</span></span> <span data-ttu-id="39b57-162">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="39b57-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="39b57-163">請連絡[PolicyStat 用戶端支援小組](http://www.policystat.com/support/)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="39b57-163">Contact [PolicyStat Client support team](http://www.policystat.com/support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="39b57-164">在 [hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="39b57-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_certificate.png) 

5. <span data-ttu-id="39b57-166">hello 本節目標在於的 toooutline tooenable 使用者 tooauthenticate tooPolicyStat 的同盟，使用 Azure AD 的帳戶與如何 hello SAML 通訊協定為基礎。</span><span class="sxs-lookup"><span data-stu-id="39b57-166">hello objective of this section is toooutline how tooenable users tooauthenticate tooPolicyStat with their account in Azure AD using federation based on hello SAML protocol.</span></span>

    <span data-ttu-id="39b57-167">hello PolicyStat 應用程式需要特定格式，這需要您 tooadd 自訂屬性對應 tooyour hello SAML 判斷提示**SAML 權杖屬性**組態。</span><span class="sxs-lookup"><span data-stu-id="39b57-167">hello PolicyStat application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **SAML Token Attributes** configuration.</span></span>  

     <span data-ttu-id="39b57-168">hello 下列螢幕擷取畫面顯示此動作的範例。</span><span class="sxs-lookup"><span data-stu-id="39b57-168">hello following screenshot shows an example of this.</span></span>

     <span data-ttu-id="39b57-169">![屬性](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "屬性")</span><span class="sxs-lookup"><span data-stu-id="39b57-169">![Attributes](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "Attributes")</span></span>

6. <span data-ttu-id="39b57-170">tooadd hello 必要屬性對應，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="39b57-170">tooadd hello required attribute mappings, perform hello following steps:</span></span>

    | <span data-ttu-id="39b57-171">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="39b57-171">Attribute Name</span></span>    |   <span data-ttu-id="39b57-172">屬性值</span><span class="sxs-lookup"><span data-stu-id="39b57-172">Attribute Value</span></span> |
    |------------------- | -------------------- |
    | <span data-ttu-id="39b57-173">UID</span><span class="sxs-lookup"><span data-stu-id="39b57-173">uid</span></span> | <span data-ttu-id="39b57-174">ExtractMailPrefix([mail])</span><span class="sxs-lookup"><span data-stu-id="39b57-174">ExtractMailPrefix([mail])</span></span> |
    
    <span data-ttu-id="39b57-175">a.</span><span class="sxs-lookup"><span data-stu-id="39b57-175">a.</span></span> <span data-ttu-id="39b57-176">按一下**加入屬性**tooopen hello**加入屬性**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="39b57-176">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_04.png)

    ![設定單一登入](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addatribute.png)
    
    <span data-ttu-id="39b57-179">b.</span><span class="sxs-lookup"><span data-stu-id="39b57-179">b.</span></span> <span data-ttu-id="39b57-180">在 [hello**屬性名稱**文字方塊中，輸入**uid**。</span><span class="sxs-lookup"><span data-stu-id="39b57-180">In hello **Attribute Name** textbox, type **uid**.</span></span>

    <span data-ttu-id="39b57-181">c.</span><span class="sxs-lookup"><span data-stu-id="39b57-181">c.</span></span> <span data-ttu-id="39b57-182">在 [hello**屬性值**文字方塊中，選取**ExtractMailPrefix()**。</span><span class="sxs-lookup"><span data-stu-id="39b57-182">In hello **Attribute Value** textbox, select **ExtractMailPrefix()**.</span></span>    
   
    <span data-ttu-id="39b57-183">d.</span><span class="sxs-lookup"><span data-stu-id="39b57-183">d.</span></span> <span data-ttu-id="39b57-184">從 hello**郵件**清單中，選取**User.mail**。</span><span class="sxs-lookup"><span data-stu-id="39b57-184">From hello **Mail** list, select **User.mail**.</span></span>
    
    <span data-ttu-id="39b57-185">e.</span><span class="sxs-lookup"><span data-stu-id="39b57-185">e.</span></span> <span data-ttu-id="39b57-186">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="39b57-186">Click **Ok**</span></span>

7. <span data-ttu-id="39b57-187">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="39b57-187">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-policystat-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="39b57-189">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 PolicyStat 公司網站。</span><span class="sxs-lookup"><span data-stu-id="39b57-189">In a different web browser window, log into your PolicyStat company site as an administrator.</span></span>

9. <span data-ttu-id="39b57-190">按一下 hello **Admin**索引標籤，然後再按一下**單一登入組態**左側的導覽窗格中。</span><span class="sxs-lookup"><span data-stu-id="39b57-190">Click hello **Admin** tab, and then click **Single Sign-On Configuration** in left navigation pane.</span></span>
   
    <span data-ttu-id="39b57-191">![系統管理員功能表](./media/active-directory-saas-policystat-tutorial/ic808633.png "系統管理員功能表")</span><span class="sxs-lookup"><span data-stu-id="39b57-191">![Administrator Menu](./media/active-directory-saas-policystat-tutorial/ic808633.png "Administrator Menu")</span></span>

10. <span data-ttu-id="39b57-192">在 [hello**安裝**區段中，選取**啟用單一登入整合**。</span><span class="sxs-lookup"><span data-stu-id="39b57-192">In hello **Setup** section, select **Enable Single Sign-on Integration**.</span></span>
   
    <span data-ttu-id="39b57-193">![單一登入設定](./media/active-directory-saas-policystat-tutorial/ic808634.png "單一登入設定")</span><span class="sxs-lookup"><span data-stu-id="39b57-193">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808634.png "Single Sign-On Configuration")</span></span>

11. <span data-ttu-id="39b57-194">按一下**設定屬性**，然後在 hello**設定屬性**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="39b57-194">Click **Configure Attributes**, and then, in hello **Configure Attributes** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="39b57-195">![單一登入設定](./media/active-directory-saas-policystat-tutorial/ic808635.png "單一登入設定")</span><span class="sxs-lookup"><span data-stu-id="39b57-195">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808635.png "Single Sign-On Configuration")</span></span>
   
    <span data-ttu-id="39b57-196">a.</span><span class="sxs-lookup"><span data-stu-id="39b57-196">a.</span></span> <span data-ttu-id="39b57-197">在 [hello **Username 屬性**文字方塊中，輸入**uid**。</span><span class="sxs-lookup"><span data-stu-id="39b57-197">In hello **Username Attribute** textbox, type **uid**.</span></span>

    <span data-ttu-id="39b57-198">b.</span><span class="sxs-lookup"><span data-stu-id="39b57-198">b.</span></span> <span data-ttu-id="39b57-199">在 [hello**名字屬性**文字方塊中，輸入**firstname**使用者的**許**。</span><span class="sxs-lookup"><span data-stu-id="39b57-199">In hello **First Name Attribute** textbox, type **firstname** of user **Britta**.</span></span>

    <span data-ttu-id="39b57-200">c.</span><span class="sxs-lookup"><span data-stu-id="39b57-200">c.</span></span> <span data-ttu-id="39b57-201">在 [hello**姓氏**文字方塊中，輸入**lastname**使用者的**Simon**。</span><span class="sxs-lookup"><span data-stu-id="39b57-201">In hello **Last Name Attribute** textbox, type **lastname** of user **Simon**.</span></span>

    <span data-ttu-id="39b57-202">d.</span><span class="sxs-lookup"><span data-stu-id="39b57-202">d.</span></span> <span data-ttu-id="39b57-203">在 [hello**電子郵件屬性**文字方塊中，輸入**emailaddress**使用者的** BrittaSimon@contoso.com **。</span><span class="sxs-lookup"><span data-stu-id="39b57-203">In hello **Email Attribute** textbox, type **emailaddress** of user **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="39b57-204">e.</span><span class="sxs-lookup"><span data-stu-id="39b57-204">e.</span></span> <span data-ttu-id="39b57-205">按一下 [儲存變更] 。</span><span class="sxs-lookup"><span data-stu-id="39b57-205">Click **Save Changes**.</span></span>

12. <span data-ttu-id="39b57-206">按一下**您的 IDP 中繼資料**，然後在 hello**您的 IDP 中繼資料**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="39b57-206">Click **Your IDP Metadata**, and then, in hello **Your IDP Metadata** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="39b57-207">![單一登入設定](./media/active-directory-saas-policystat-tutorial/ic808636.png "單一登入設定")</span><span class="sxs-lookup"><span data-stu-id="39b57-207">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808636.png "Single Sign-On Configuration")</span></span>
   
    <span data-ttu-id="39b57-208">a.</span><span class="sxs-lookup"><span data-stu-id="39b57-208">a.</span></span> <span data-ttu-id="39b57-209">開啟您下載的中繼資料檔案，複製 hello 內容，並貼到 hello**您的身分識別提供者中繼資料**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="39b57-209">Open your downloaded metadata file, copy hello content, and  then paste it into hello **Your Identity Provider Metadata** textbox.</span></span>

    <span data-ttu-id="39b57-210">b.</span><span class="sxs-lookup"><span data-stu-id="39b57-210">b.</span></span> <span data-ttu-id="39b57-211">按一下 [儲存變更] 。</span><span class="sxs-lookup"><span data-stu-id="39b57-211">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="39b57-212">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="39b57-212">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="39b57-213">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="39b57-213">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="39b57-214">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="39b57-214">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="39b57-215">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="39b57-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="39b57-216">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="39b57-216">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="39b57-218">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="39b57-218">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="39b57-219">在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="39b57-219">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-policystat-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="39b57-221">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="39b57-221">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-policystat-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="39b57-223">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="39b57-223">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-policystat-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="39b57-225">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="39b57-225">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-policystat-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="39b57-227">a.</span><span class="sxs-lookup"><span data-stu-id="39b57-227">a.</span></span> <span data-ttu-id="39b57-228">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="39b57-228">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="39b57-229">b.</span><span class="sxs-lookup"><span data-stu-id="39b57-229">b.</span></span> <span data-ttu-id="39b57-230">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="39b57-230">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="39b57-231">c.</span><span class="sxs-lookup"><span data-stu-id="39b57-231">c.</span></span> <span data-ttu-id="39b57-232">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="39b57-232">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="39b57-233">d.</span><span class="sxs-lookup"><span data-stu-id="39b57-233">d.</span></span> <span data-ttu-id="39b57-234">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="39b57-234">Click **Create**.</span></span>
 
### <a name="creating-a-policystat-test-user"></a><span data-ttu-id="39b57-235">建立 PolicyStat 測試使用者</span><span class="sxs-lookup"><span data-stu-id="39b57-235">Creating a PolicyStat test user</span></span>

<span data-ttu-id="39b57-236">在訂單 tooenable Azure AD 使用者 toolog PolicyStat 成，它們必須佈建到 PolicyStat。</span><span class="sxs-lookup"><span data-stu-id="39b57-236">In order tooenable Azure AD users toolog into PolicyStat, they must be provisioned into PolicyStat.</span></span>  

<span data-ttu-id="39b57-237">PolicyStat 支援即時使用者佈建。</span><span class="sxs-lookup"><span data-stu-id="39b57-237">PolicyStat supports just in time user provisioning.</span></span> <span data-ttu-id="39b57-238">這表示，您不需要 tooadd hello 使用者手動 tooPolicyStat。</span><span class="sxs-lookup"><span data-stu-id="39b57-238">This means, you do not need tooadd hello users manually tooPolicyStat.</span></span> <span data-ttu-id="39b57-239">hello 使用者會取得自動加入 SSO 透過其第一個登入。</span><span class="sxs-lookup"><span data-stu-id="39b57-239">hello users will get added automatically on their first login through SSO.</span></span>

>[!NOTE]
><span data-ttu-id="39b57-240">您可以使用任何其他 PolicyStat 使用者帳戶建立工具或 Api 提供 PolicyStat tooprovision Azure AD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="39b57-240">You can use any other PolicyStat user account creation tools or APIs provided by PolicyStat tooprovision Azure AD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="39b57-241">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="39b57-241">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="39b57-242">在本節中，您可以授與存取 tooPolicyStat 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="39b57-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPolicyStat.</span></span>

![指派使用者][200] 

<span data-ttu-id="39b57-244">**tooassign 許 Simon tooPolicyStat，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="39b57-244">**tooassign Britta Simon tooPolicyStat, perform hello following steps:**</span></span>

1. <span data-ttu-id="39b57-245">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="39b57-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="39b57-247">在 [hello] 應用程式清單中，選取**PolicyStat**。</span><span class="sxs-lookup"><span data-stu-id="39b57-247">In hello applications list, select **PolicyStat**.</span></span>

    ![設定單一登入](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_app.png) 

3. <span data-ttu-id="39b57-249">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="39b57-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="39b57-251">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="39b57-251">Click **Add** button.</span></span> <span data-ttu-id="39b57-252">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="39b57-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="39b57-254">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="39b57-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="39b57-255">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="39b57-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="39b57-256">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="39b57-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="39b57-257">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="39b57-257">Testing single sign-on</span></span>

<span data-ttu-id="39b57-258">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="39b57-258">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="39b57-259">當您按一下 hello PolicyStat 磚 hello 存取面板中的時，您應該取得自動登入 tooyour PolicyStat 應用程式。</span><span class="sxs-lookup"><span data-stu-id="39b57-259">When you click hello PolicyStat tile in hello Access Panel, you should get automatically signed-on tooyour PolicyStat application.</span></span>
<span data-ttu-id="39b57-260">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="39b57-260">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="39b57-261">其他資源</span><span class="sxs-lookup"><span data-stu-id="39b57-261">Additional resources</span></span>

* [<span data-ttu-id="39b57-262">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="39b57-262">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="39b57-263">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="39b57-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_203.png

