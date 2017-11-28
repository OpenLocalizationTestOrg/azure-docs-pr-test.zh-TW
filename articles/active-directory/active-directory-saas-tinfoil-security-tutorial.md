---
title: "教學課程：Azure Active Directory 與 TINFOIL SECURITY 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 TINFOIL SECURITY 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: da02da92-e3b0-4c09-ad6c-180882b0f9f8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 1a3fa9880d9e026c2d6d6548188df2269ff69139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tinfoil-security"></a><span data-ttu-id="1b184-103">教學課程：Azure Active Directory 與 TINFOIL SECURITY 整合</span><span class="sxs-lookup"><span data-stu-id="1b184-103">Tutorial: Azure Active Directory integration with TINFOIL SECURITY</span></span>

<span data-ttu-id="1b184-104">在此教學課程中，您學會如何 toointegrate TINFOIL SECURITY 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="1b184-104">In this tutorial, you learn how toointegrate TINFOIL SECURITY with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1b184-105">TINFOIL SECURITY 整合與 Azure AD 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="1b184-105">Integrating TINFOIL SECURITY with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1b184-106">您可以在 Azure AD 中擁有存取 tooTINFOIL 安全性控制</span><span class="sxs-lookup"><span data-stu-id="1b184-106">You can control in Azure AD who has access tooTINFOIL SECURITY</span></span>
- <span data-ttu-id="1b184-107">您可以啟用您的使用者 tooautomatically get 登入 tooTINFOIL （單一登入） 的安全性與他們的 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="1b184-107">You can enable your users tooautomatically get signed-on tooTINFOIL SECURITY (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1b184-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="1b184-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1b184-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="1b184-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b184-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="1b184-110">Prerequisites</span></span>

<span data-ttu-id="1b184-111">tooconfigure 與 TINFOIL SECURITY 的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="1b184-111">tooconfigure Azure AD integration with TINFOIL SECURITY, you need hello following items:</span></span>

- <span data-ttu-id="1b184-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1b184-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1b184-113">已啟用 TINFOIL SECURITY 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1b184-113">A TINFOIL SECURITY single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1b184-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="1b184-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1b184-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="1b184-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1b184-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="1b184-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1b184-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="1b184-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1b184-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="1b184-118">Scenario description</span></span>
<span data-ttu-id="1b184-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1b184-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1b184-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="1b184-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1b184-121">從 hello 圖庫新增 TINFOIL SECURITY</span><span class="sxs-lookup"><span data-stu-id="1b184-121">Add TINFOIL SECURITY from hello gallery</span></span>
2. <span data-ttu-id="1b184-122">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1b184-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tinfoil-security-from-hello-gallery"></a><span data-ttu-id="1b184-123">從 hello 圖庫新增 TINFOIL SECURITY</span><span class="sxs-lookup"><span data-stu-id="1b184-123">Add TINFOIL SECURITY from hello gallery</span></span>
<span data-ttu-id="1b184-124">tooconfigure hello 整合 TINFOIL SECURITY 的 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd TINFOIL SECURITY。</span><span class="sxs-lookup"><span data-stu-id="1b184-124">tooconfigure hello integration of TINFOIL SECURITY into Azure AD, you need tooadd TINFOIL SECURITY from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1b184-125">**tooadd TINFOIL SECURITY 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1b184-125">**tooadd TINFOIL SECURITY from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1b184-126">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="1b184-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1b184-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="1b184-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1b184-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="1b184-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="1b184-131">tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="1b184-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="1b184-133">在 [hello] 搜尋方塊中，輸入**TINFOIL SECURITY**，選取**TINFOIL SECURITY**然後按一下 [從結果面板**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1b184-133">In hello search box, type **TINFOIL SECURITY**, select  **TINFOIL SECURITY** from result panel then click **Add** button tooadd hello application.</span></span>

    ![來自資源庫的 TINFOIL SECURITY](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="1b184-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1b184-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="1b184-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 TINFOIL SECURITY 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1b184-136">In this section, you configure and test Azure AD single sign-on with TINFOIL SECURITY based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1b184-137">單一登入 toowork，Azure AD 需要 tooknow TINFOIL SECURITY 中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="1b184-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TINFOIL SECURITY is tooa user in Azure AD.</span></span> <span data-ttu-id="1b184-138">換句話說，Azure AD 使用者與 TINFOIL SECURITY 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="1b184-138">In other words, a link relationship between an Azure AD user and hello related user in TINFOIL SECURITY needs toobe established.</span></span>

<span data-ttu-id="1b184-139">在 TINFOIL SECURITY 指派 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="1b184-139">In TINFOIL SECURITY, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1b184-140">tooconfigure 及 Azure AD 單一登入與 TINFOIL SECURITY 的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="1b184-140">tooconfigure and test Azure AD single sign-on with TINFOIL SECURITY, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1b184-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="1b184-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1b184-142">**[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="1b184-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1b184-143">**[建立測試使用者 TINFOIL SECURITY](#create-a-tinfoil-security-test-user) ** -toohave 許 Simon TINFOIL SECURITY 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="1b184-143">**[Create a TINFOIL SECURITY test user](#create-a-tinfoil-security-test-user)** - toohave a counterpart of Britta Simon in TINFOIL SECURITY that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1b184-144">**[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1b184-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1b184-145">**[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="1b184-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="1b184-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1b184-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="1b184-147">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 TINFOIL SECURITY 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="1b184-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TINFOIL SECURITY application.</span></span>

<span data-ttu-id="1b184-148">**tooconfigure Azure AD 單一登入與 TINFOIL SECURITY，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1b184-148">**tooconfigure Azure AD single sign-on with TINFOIL SECURITY, perform hello following steps:**</span></span>

1. <span data-ttu-id="1b184-149">在 Azure 入口網站上 hello hello **TINFOIL SECURITY**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="1b184-149">In hello Azure portal, on hello **TINFOIL SECURITY** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="1b184-151">在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1b184-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![SAML 型登入](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_samlbase.png)

3. <span data-ttu-id="1b184-153">在 [hello **TINFOIL 安全性網域和 Url**區段中，hello 使用者沒有 tooperform 任何步驟，因為與 Azure 已預先整合 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1b184-153">On hello **TINFOIL SECURITY Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![設定單一登入](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_url.png)


4. <span data-ttu-id="1b184-155">在 [hello **SAML 簽章憑證**區段，複製 hello**指紋**值。</span><span class="sxs-lookup"><span data-stu-id="1b184-155">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value.</span></span>

    ![[SAML 簽署憑證] 區段](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_certificate.png) 

5. <span data-ttu-id="1b184-157">tooadd hello 必要屬性對應，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1b184-157">tooadd hello required attribute mappings, perform hello following steps:</span></span>
    
    <span data-ttu-id="1b184-158">![屬性](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "屬性")</span><span class="sxs-lookup"><span data-stu-id="1b184-158">![Attributes](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "Attributes")</span></span>
    
    | <span data-ttu-id="1b184-159">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="1b184-159">Attribute Name</span></span>    |   <span data-ttu-id="1b184-160">屬性值</span><span class="sxs-lookup"><span data-stu-id="1b184-160">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="1b184-161">accountid</span><span class="sxs-lookup"><span data-stu-id="1b184-161">accountid</span></span> | <span data-ttu-id="1b184-162">UXXXXXXXXXXXXX</span><span class="sxs-lookup"><span data-stu-id="1b184-162">UXXXXXXXXXXXXX</span></span> |
    
    <span data-ttu-id="1b184-163">a.</span><span class="sxs-lookup"><span data-stu-id="1b184-163">a.</span></span> <span data-ttu-id="1b184-164">按一下 [加入使用者屬性] 。</span><span class="sxs-lookup"><span data-stu-id="1b184-164">Click **add user attribute**.</span></span>
    
    <span data-ttu-id="1b184-165">![新增屬性](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "屬性")</span><span class="sxs-lookup"><span data-stu-id="1b184-165">![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "Attributes")</span></span>
    
    <span data-ttu-id="1b184-166">![新增屬性](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "屬性")</span><span class="sxs-lookup"><span data-stu-id="1b184-166">![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "Attributes")</span></span>
    
    <span data-ttu-id="1b184-167">b.</span><span class="sxs-lookup"><span data-stu-id="1b184-167">b.</span></span> <span data-ttu-id="1b184-168">在 [hello**屬性名稱**文字方塊中，輸入**accountid**。</span><span class="sxs-lookup"><span data-stu-id="1b184-168">In hello **Attribute Name** textbox, type **accountid**.</span></span>
    
    <span data-ttu-id="1b184-169">c.</span><span class="sxs-lookup"><span data-stu-id="1b184-169">c.</span></span> <span data-ttu-id="1b184-170">在 [hello**屬性值**文字方塊中，貼上 hello 帳戶識別碼值用來在稍後取得 hello 教學課程。</span><span class="sxs-lookup"><span data-stu-id="1b184-170">In hello **Attribute Value** textbox, paste hello account ID value which you will get later on hello tutorial.</span></span>
    
    <span data-ttu-id="1b184-171">d.</span><span class="sxs-lookup"><span data-stu-id="1b184-171">d.</span></span> <span data-ttu-id="1b184-172">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="1b184-172">Click **Ok**.</span></span>    

6. <span data-ttu-id="1b184-173">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="1b184-173">Click **Save** button.</span></span>

    ![[儲存] 按鈕](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="1b184-175">在 [hello **TINFOIL 安全性組態**區段中，按一下**設定 TINFOIL SECURITY** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="1b184-175">On hello **TINFOIL SECURITY Configuration** section, click **Configure TINFOIL SECURITY** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1b184-176">複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="1b184-176">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![TINFOIL SECURITY 組態](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_configure.png) 

8. <span data-ttu-id="1b184-178">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 TINFOIL SECURITY 公司網站。</span><span class="sxs-lookup"><span data-stu-id="1b184-178">In a different web browser window, log into your TINFOIL SECURITY company site as an administrator.</span></span>

9. <span data-ttu-id="1b184-179">在 hello hello 上方的工具列中按一下**我的帳戶**。</span><span class="sxs-lookup"><span data-stu-id="1b184-179">In hello toolbar on hello top, click **My Account**.</span></span>
   
    <span data-ttu-id="1b184-180">![儀表板](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "儀表板")</span><span class="sxs-lookup"><span data-stu-id="1b184-180">![Dashboard](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "Dashboard")</span></span>

10. <span data-ttu-id="1b184-181">按一下 [安全性] 。</span><span class="sxs-lookup"><span data-stu-id="1b184-181">Click **Security**.</span></span>
   
    <span data-ttu-id="1b184-182">![安全性](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "安全性")</span><span class="sxs-lookup"><span data-stu-id="1b184-182">![Security](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "Security")</span></span>

11. <span data-ttu-id="1b184-183">在 [hello**單一登入**組態頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1b184-183">On hello **Single Sign-On** configuration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="1b184-184">![單一登入](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "單一登入")</span><span class="sxs-lookup"><span data-stu-id="1b184-184">![Single Sign-On](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "Single Sign-On")</span></span>
   
    <span data-ttu-id="1b184-185">a.</span><span class="sxs-lookup"><span data-stu-id="1b184-185">a.</span></span> <span data-ttu-id="1b184-186">選取 [啟用 SAML] 。</span><span class="sxs-lookup"><span data-stu-id="1b184-186">Select **Enable SAML**.</span></span>
   
    <span data-ttu-id="1b184-187">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="1b184-187">b.</span></span> <span data-ttu-id="1b184-188">按一下 [手動設定] 。</span><span class="sxs-lookup"><span data-stu-id="1b184-188">Click **Manual Configuration**.</span></span>
   
    <span data-ttu-id="1b184-189">c.</span><span class="sxs-lookup"><span data-stu-id="1b184-189">c.</span></span> <span data-ttu-id="1b184-190">在**SAML Post URL**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**您從 Azure 入口網站複製的</span><span class="sxs-lookup"><span data-stu-id="1b184-190">In **SAML Post URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal</span></span>
   
    <span data-ttu-id="1b184-191">d.</span><span class="sxs-lookup"><span data-stu-id="1b184-191">d.</span></span> <span data-ttu-id="1b184-192">在**SAML 憑證指紋**文字方塊中，貼上 hello 值**指紋**從複製的**SAML 簽章憑證**> 一節。</span><span class="sxs-lookup"><span data-stu-id="1b184-192">In **SAML Certificate Fingerprint** textbox, paste hello value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span></span>
  
    <span data-ttu-id="1b184-193">e.</span><span class="sxs-lookup"><span data-stu-id="1b184-193">e.</span></span> <span data-ttu-id="1b184-194">複製**您的帳戶識別碼**值並貼上在 hello 值**屬性值**底下的文字方塊中**加入屬性**Azure 入口網站中的區段。</span><span class="sxs-lookup"><span data-stu-id="1b184-194">Copy **Your Account ID** value and paste hello value in **Attribute Value** textbox under **Add Attribute** section in Azure portal.</span></span>
   
    <span data-ttu-id="1b184-195">f.</span><span class="sxs-lookup"><span data-stu-id="1b184-195">f.</span></span> <span data-ttu-id="1b184-196">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="1b184-196">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="1b184-197">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="1b184-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1b184-198">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="1b184-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1b184-199">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1b184-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1b184-200">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1b184-200">Create an Azure AD test user</span></span>
<span data-ttu-id="1b184-201">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="1b184-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="1b184-203">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1b184-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1b184-204">在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="1b184-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1b184-206">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="1b184-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![<span data-ttu-id="1b184-207">[使用者和群組] -> [所有使用者]</span><span class="sxs-lookup"><span data-stu-id="1b184-207">Users and groups -> All users</span></span> ](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1b184-208">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="1b184-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![User](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1b184-210">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1b184-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1b184-212">a.</span><span class="sxs-lookup"><span data-stu-id="1b184-212">a.</span></span> <span data-ttu-id="1b184-213">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="1b184-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1b184-214">b.</span><span class="sxs-lookup"><span data-stu-id="1b184-214">b.</span></span> <span data-ttu-id="1b184-215">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="1b184-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1b184-216">c.</span><span class="sxs-lookup"><span data-stu-id="1b184-216">c.</span></span> <span data-ttu-id="1b184-217">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="1b184-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1b184-218">d.</span><span class="sxs-lookup"><span data-stu-id="1b184-218">d.</span></span> <span data-ttu-id="1b184-219">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="1b184-219">Click **Create**.</span></span>
 
### <a name="create-a-tinfoil-security-test-user"></a><span data-ttu-id="1b184-220">建立 TINFOIL SECURITY 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1b184-220">Create a TINFOIL SECURITY test user</span></span>

<span data-ttu-id="1b184-221">在訂單 tooenable Azure AD 使用者 toolog 至 TINFOIL SECURITY，它們必須佈建至 TINFOIL SECURITY。</span><span class="sxs-lookup"><span data-stu-id="1b184-221">In order tooenable Azure AD users toolog into TINFOIL SECURITY, they must be provisioned into TINFOIL SECURITY.</span></span> <span data-ttu-id="1b184-222">中的 [TINFOIL SECURITY hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="1b184-222">In hello case of TINFOIL SECURITY, provisioning is a manual task.</span></span>

<span data-ttu-id="1b184-223">**tooget 使用者佈建，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1b184-223">**tooget a user provisioned, perform hello following steps:**</span></span>

1. <span data-ttu-id="1b184-224">如果 hello 使用者屬於企業帳戶，您需要太[連絡 hello TINFOIL SECURITY 支援小組](https://www.tinfoilsecurity.com/contact)建立 tooget hello 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="1b184-224">If hello user is a part of an Enterprise account, you need too[contact hello TINFOIL SECURITY support team](https://www.tinfoilsecurity.com/contact) tooget hello user account created.</span></span>

2. <span data-ttu-id="1b184-225">如果 hello 使用者是一般 TINFOIL SECURITY SaaS 使用者，hello 使用者可以加入共同作業者 tooany hello 使用者站台。</span><span class="sxs-lookup"><span data-stu-id="1b184-225">If hello user is a regular TINFOIL SECURITY SaaS user, then hello user can add a collaborator tooany of hello user’s sites.</span></span> <span data-ttu-id="1b184-226">這個觸發程序的處理序 toosend 邀請 toohello 指定電子郵件 toocreate 新的 TINFOIL SECURITY 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="1b184-226">This triggers a process toosend an invitation toohello specified email toocreate a new TINFOIL SECURITY user account.</span></span>

> [!NOTE]
> <span data-ttu-id="1b184-227">您可以使用任何其他 TINFOIL SECURITY 使用者帳戶建立工具或 Api 提供 TINFOIL SECURITY tooprovision Azure AD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="1b184-227">You can use any other TINFOIL SECURITY user account creation tools or APIs provided by TINFOIL SECURITY tooprovision Azure AD user accounts.</span></span>
> 
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="1b184-228">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1b184-228">Assign hello Azure AD test user</span></span>

<span data-ttu-id="1b184-229">在本節中，以啟用許 Simon toouse Azure 單一登入授與存取 tooTINFOIL 安全性。</span><span class="sxs-lookup"><span data-stu-id="1b184-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTINFOIL SECURITY.</span></span>

![指派使用者][200] 

<span data-ttu-id="1b184-231">**tooassign 許 Simon tooTINFOIL 安全性，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1b184-231">**tooassign Britta Simon tooTINFOIL SECURITY, perform hello following steps:**</span></span>

1. <span data-ttu-id="1b184-232">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="1b184-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="1b184-234">在 [hello] 應用程式清單中，選取**TINFOIL SECURITY**。</span><span class="sxs-lookup"><span data-stu-id="1b184-234">In hello applications list, select **TINFOIL SECURITY**.</span></span>

    ![選取 TINFOIL SECURITY](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_app.png) 

3. <span data-ttu-id="1b184-236">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="1b184-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="1b184-238">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1b184-238">Click **Add** button.</span></span> <span data-ttu-id="1b184-239">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="1b184-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="1b184-241">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="1b184-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1b184-242">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1b184-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1b184-243">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1b184-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="1b184-244">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="1b184-244">Test single sign-on</span></span>

<span data-ttu-id="1b184-245">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="1b184-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1b184-246">當您按一下 hello TINFOIL SECURITY 磚 hello 存取面板中的時，您應該取得自動登入 tooyour TINFOIL SECURITY 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1b184-246">When you click hello TINFOIL SECURITY tile in hello Access Panel, you should get automatically signed-on tooyour TINFOIL SECURITY application.</span></span> <span data-ttu-id="1b184-247">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="1b184-247">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1b184-248">其他資源</span><span class="sxs-lookup"><span data-stu-id="1b184-248">Additional resources</span></span>

* [<span data-ttu-id="1b184-249">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1b184-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1b184-250">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="1b184-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_203.png

