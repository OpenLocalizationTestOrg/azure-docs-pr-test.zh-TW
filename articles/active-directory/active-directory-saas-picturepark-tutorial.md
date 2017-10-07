---
title: "教學課程：Azure Active Directory 與 Picturepark 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Picturepark 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 31c21cd4-9c00-4cad-9538-a13996dc872f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: jeedes
ms.openlocfilehash: 3d826d3f73aad2f0d123f8697c6caafad7bc926a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-picturepark"></a><span data-ttu-id="95a82-103">教學課程：Azure Active Directory 與 Picturepark 整合</span><span class="sxs-lookup"><span data-stu-id="95a82-103">Tutorial: Azure Active Directory integration with Picturepark</span></span>

<span data-ttu-id="95a82-104">在此教學課程中，您學會如何 toointegrate Picturepark 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="95a82-104">In this tutorial, you learn how toointegrate Picturepark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="95a82-105">與 Azure AD 整合 Picturepark 可以提供下列優點的 hello:</span><span class="sxs-lookup"><span data-stu-id="95a82-105">Integrating Picturepark with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="95a82-106">您可以控制存取 tooPicturepark Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="95a82-106">You can control in Azure AD who has access tooPicturepark</span></span>
- <span data-ttu-id="95a82-107">您可以啟用您的使用者 tooautomatically get 登入 tooPicturepark （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="95a82-107">You can enable your users tooautomatically get signed-on tooPicturepark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="95a82-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="95a82-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="95a82-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="95a82-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95a82-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="95a82-110">Prerequisites</span></span>

<span data-ttu-id="95a82-111">tooconfigure 與 Picturepark 的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="95a82-111">tooconfigure Azure AD integration with Picturepark, you need hello following items:</span></span>

- <span data-ttu-id="95a82-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="95a82-112">An Azure AD subscription</span></span>
- <span data-ttu-id="95a82-113">啟用 Picturepark 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="95a82-113">A Picturepark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="95a82-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="95a82-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="95a82-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="95a82-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="95a82-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="95a82-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="95a82-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="95a82-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="95a82-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="95a82-118">Scenario description</span></span>
<span data-ttu-id="95a82-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="95a82-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="95a82-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="95a82-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="95a82-121">從 hello 圖庫加入 Picturepark</span><span class="sxs-lookup"><span data-stu-id="95a82-121">Adding Picturepark from hello gallery</span></span>
2. <span data-ttu-id="95a82-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="95a82-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-picturepark-from-hello-gallery"></a><span data-ttu-id="95a82-123">從 hello 圖庫加入 Picturepark</span><span class="sxs-lookup"><span data-stu-id="95a82-123">Adding Picturepark from hello gallery</span></span>
<span data-ttu-id="95a82-124">tooconfigure hello 整合 Picturepark 的 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Picturepark。</span><span class="sxs-lookup"><span data-stu-id="95a82-124">tooconfigure hello integration of Picturepark into Azure AD, you need tooadd Picturepark from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="95a82-125">**tooadd Picturepark 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="95a82-125">**tooadd Picturepark from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="95a82-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="95a82-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="95a82-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="95a82-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="95a82-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="95a82-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="95a82-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="95a82-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="95a82-133">在 [hello] 搜尋方塊中，輸入**Picturepark**。</span><span class="sxs-lookup"><span data-stu-id="95a82-133">In hello search box, type **Picturepark**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_search.png)

5. <span data-ttu-id="95a82-135">在 hello 結果 窗格中，選取  **Picturepark**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="95a82-135">In hello results panel, select **Picturepark**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="95a82-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="95a82-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="95a82-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Picturepark 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="95a82-138">In this section, you configure and test Azure AD single sign-on with Picturepark based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="95a82-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 Picturepark 中是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="95a82-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Picturepark is tooa user in Azure AD.</span></span> <span data-ttu-id="95a82-140">換句話說，Azure AD 使用者與 hello Picturepark 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="95a82-140">In other words, a link relationship between an Azure AD user and hello related user in Picturepark needs toobe established.</span></span>

<span data-ttu-id="95a82-141">在 Picturepark 中，將指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="95a82-141">In Picturepark, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="95a82-142">tooconfigure 及測試 Azure AD 單一登入 Picturepark，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="95a82-142">tooconfigure and test Azure AD single sign-on with Picturepark, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="95a82-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="95a82-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="95a82-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="95a82-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="95a82-145">**[建立測試使用者 Picturepark](#creating-a-picturepark-test-user)**  -toohave 許 Simon Picturepark 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="95a82-145">**[Creating a Picturepark test user](#creating-a-picturepark-test-user)** - toohave a counterpart of Britta Simon in Picturepark that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="95a82-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="95a82-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="95a82-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="95a82-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="95a82-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="95a82-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="95a82-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Picturepark 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="95a82-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Picturepark application.</span></span>

<span data-ttu-id="95a82-150">**tooconfigure Azure AD 單一登入 Picturepark，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="95a82-150">**tooconfigure Azure AD single sign-on with Picturepark, perform hello following steps:**</span></span>

1. <span data-ttu-id="95a82-151">在 Azure 入口網站上 hello hello **Picturepark**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="95a82-151">In hello Azure portal, on hello **Picturepark** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="95a82-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="95a82-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_samlbase.png)

3. <span data-ttu-id="95a82-155">在 hello **Picturepark 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="95a82-155">On hello **Picturepark Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_url.png)

    <span data-ttu-id="95a82-157">a.</span><span class="sxs-lookup"><span data-stu-id="95a82-157">a.</span></span> <span data-ttu-id="95a82-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.picturepark.com`</span><span class="sxs-lookup"><span data-stu-id="95a82-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.picturepark.com`</span></span>

    <span data-ttu-id="95a82-159">b.</span><span class="sxs-lookup"><span data-stu-id="95a82-159">b.</span></span> <span data-ttu-id="95a82-160">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:</span><span class="sxs-lookup"><span data-stu-id="95a82-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span> 
    
    |  |
    |--|
    | `https://<companyname>.current-picturepark.com`|
    | `https://<companyname>.picturepark.com`|
    | `https://<companyname>.next-picturepark.com`|
    | |

    > [!NOTE] 
    > <span data-ttu-id="95a82-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="95a82-161">These values are not real.</span></span> <span data-ttu-id="95a82-162">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="95a82-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="95a82-163">請連絡[Picturepark Client 的支援團隊](https://picturepark.com/about/contact/)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="95a82-163">Contact [Picturepark Client support team](https://picturepark.com/about/contact/) tooget these values.</span></span> 
 
4. <span data-ttu-id="95a82-164">在 hello **SAML 簽章憑證**區段，複製 hello**指紋**憑證值。</span><span class="sxs-lookup"><span data-stu-id="95a82-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![設定單一登入](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_certificate.png) 

5. <span data-ttu-id="95a82-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="95a82-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-picturepark-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="95a82-168">在 hello **Picturepark 組態**區段中，按一下**設定 Picturepark** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="95a82-168">On hello **Picturepark Configuration** section, click **Configure Picturepark** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="95a82-169">複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="95a82-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_configure.png) 

7. <span data-ttu-id="95a82-171">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 Picturepark 公司網站。</span><span class="sxs-lookup"><span data-stu-id="95a82-171">In a different web browser window, log into your Picturepark company site as an administrator.</span></span>

8. <span data-ttu-id="95a82-172">在 hello hello 上方的工具列中按一下**系統管理工具**，然後按一下**管理主控台**。</span><span class="sxs-lookup"><span data-stu-id="95a82-172">In hello toolbar on hello top, click **Administrative tools**, and then click **Management Console**.</span></span>
   
    <span data-ttu-id="95a82-173">![管理主控台](./media/active-directory-saas-picturepark-tutorial/ic795062.png "管理主控台")</span><span class="sxs-lookup"><span data-stu-id="95a82-173">![Management Console](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Management Console")</span></span>

9. <span data-ttu-id="95a82-174">按一下 驗證，然後按一下識別提供者。</span><span class="sxs-lookup"><span data-stu-id="95a82-174">Click **Authentication**, and then click **Identity providers**.</span></span>
   
    <span data-ttu-id="95a82-175">![驗證](./media/active-directory-saas-picturepark-tutorial/ic795063.png "驗證")</span><span class="sxs-lookup"><span data-stu-id="95a82-175">![Authentication](./media/active-directory-saas-picturepark-tutorial/ic795063.png "Authentication")</span></span>

10. <span data-ttu-id="95a82-176">在 hello**身分識別提供者組態**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="95a82-176">In hello **Identity provider configuration** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="95a82-177">![識別提供者組態](./media/active-directory-saas-picturepark-tutorial/ic795064.png "識別提供者組態")</span><span class="sxs-lookup"><span data-stu-id="95a82-177">![Identity provider configuration](./media/active-directory-saas-picturepark-tutorial/ic795064.png "Identity provider configuration")</span></span>
   
    <span data-ttu-id="95a82-178">a.</span><span class="sxs-lookup"><span data-stu-id="95a82-178">a.</span></span> <span data-ttu-id="95a82-179">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="95a82-179">Click **Add**.</span></span>
  
    <span data-ttu-id="95a82-180">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="95a82-180">b.</span></span> <span data-ttu-id="95a82-181">輸入組態的名稱。</span><span class="sxs-lookup"><span data-stu-id="95a82-181">Type a name for your configuration.</span></span>
   
    <span data-ttu-id="95a82-182">c.</span><span class="sxs-lookup"><span data-stu-id="95a82-182">c.</span></span> <span data-ttu-id="95a82-183">選取 [設定為預設值] 。</span><span class="sxs-lookup"><span data-stu-id="95a82-183">Select **Set as default**.</span></span>
   
    <span data-ttu-id="95a82-184">d.</span><span class="sxs-lookup"><span data-stu-id="95a82-184">d.</span></span> <span data-ttu-id="95a82-185">在**簽發者 URI**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="95a82-185">In **Issuer URI** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="95a82-186">e.</span><span class="sxs-lookup"><span data-stu-id="95a82-186">e.</span></span> <span data-ttu-id="95a82-187">在**受信任簽發者指紋列印**文字方塊中，貼上 hello 值**指紋**從複製的**SAML 簽章憑證**> 一節。</span><span class="sxs-lookup"><span data-stu-id="95a82-187">In **Trusted Issuer Thumb Print** textbox, paste hello value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span></span> 

11. <span data-ttu-id="95a82-188">按一下 [JoinDefaultUsersGroup] 。</span><span class="sxs-lookup"><span data-stu-id="95a82-188">Click **JoinDefaultUsersGroup**.</span></span>

12. <span data-ttu-id="95a82-189">tooset hello **Emailaddress**中 hello 屬性**宣告**文字方塊中，輸入`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="95a82-189">tooset hello **Emailaddress** attribute in hello **Claim** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` and click **Save**.</span></span>

      <span data-ttu-id="95a82-190">![組態](./media/active-directory-saas-picturepark-tutorial/ic795065.png "組態")</span><span class="sxs-lookup"><span data-stu-id="95a82-190">![Configuration](./media/active-directory-saas-picturepark-tutorial/ic795065.png "Configuration")</span></span>

> [!TIP]
> <span data-ttu-id="95a82-191">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="95a82-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="95a82-192">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="95a82-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="95a82-193">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="95a82-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="95a82-194">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="95a82-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="95a82-195">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="95a82-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="95a82-197">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="95a82-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="95a82-198">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="95a82-198">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-picturepark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="95a82-200">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="95a82-200">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-picturepark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="95a82-202">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="95a82-202">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-picturepark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="95a82-204">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="95a82-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-picturepark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="95a82-206">a.</span><span class="sxs-lookup"><span data-stu-id="95a82-206">a.</span></span> <span data-ttu-id="95a82-207">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="95a82-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="95a82-208">b.</span><span class="sxs-lookup"><span data-stu-id="95a82-208">b.</span></span> <span data-ttu-id="95a82-209">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="95a82-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="95a82-210">c.</span><span class="sxs-lookup"><span data-stu-id="95a82-210">c.</span></span> <span data-ttu-id="95a82-211">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="95a82-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="95a82-212">d.</span><span class="sxs-lookup"><span data-stu-id="95a82-212">d.</span></span> <span data-ttu-id="95a82-213">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="95a82-213">Click **Create**.</span></span>
 
### <a name="creating-a-picturepark-test-user"></a><span data-ttu-id="95a82-214">建立 Picturepark 測試使用者</span><span class="sxs-lookup"><span data-stu-id="95a82-214">Creating a Picturepark test user</span></span>

<span data-ttu-id="95a82-215">在訂單 tooenable Azure AD 使用者 toolog 入 Picturepark，它們必須佈建到 Picturepark。</span><span class="sxs-lookup"><span data-stu-id="95a82-215">In order tooenable Azure AD users toolog into Picturepark, they must be provisioned into Picturepark.</span></span> <span data-ttu-id="95a82-216">在 Picturepark 的 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="95a82-216">In hello case of Picturepark, provisioning is a manual task.</span></span>

<span data-ttu-id="95a82-217">**tooprovision 使用者帳戶，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="95a82-217">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="95a82-218">登入 tooyour **Picturepark**租用戶。</span><span class="sxs-lookup"><span data-stu-id="95a82-218">Log in tooyour **Picturepark** tenant.</span></span>

2. <span data-ttu-id="95a82-219">在 hello hello 上方的工具列中按一下**系統管理工具**，然後按一下**使用者**。</span><span class="sxs-lookup"><span data-stu-id="95a82-219">In hello toolbar on hello top, click **Administrative tools**, and then click **Users**.</span></span>
   
    <span data-ttu-id="95a82-220">![使用者](./media/active-directory-saas-picturepark-tutorial/ic795067.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="95a82-220">![Users](./media/active-directory-saas-picturepark-tutorial/ic795067.png "Users")</span></span>

3. <span data-ttu-id="95a82-221">在 hello**使用者概觀**索引標籤上，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="95a82-221">In hello **Users overview** tab, click **New**.</span></span>
   
    <span data-ttu-id="95a82-222">![使用者管理](./media/active-directory-saas-picturepark-tutorial/ic795068.png "使用者管理")</span><span class="sxs-lookup"><span data-stu-id="95a82-222">![User management](./media/active-directory-saas-picturepark-tutorial/ic795068.png "User management")</span></span>

4. <span data-ttu-id="95a82-223">在 hello **Create User**  對話方塊中，執行 hello 想 tooprovision 下列有效的 Azure Active Directory 使用者的步驟：</span><span class="sxs-lookup"><span data-stu-id="95a82-223">On hello **Create User** dialog, perform hello following steps of a valid Azure Active Directory User you want tooprovision:</span></span>
   
    <span data-ttu-id="95a82-224">![建立使用者](./media/active-directory-saas-picturepark-tutorial/ic795069.png "建立使用者")</span><span class="sxs-lookup"><span data-stu-id="95a82-224">![Create User](./media/active-directory-saas-picturepark-tutorial/ic795069.png "Create User")</span></span>
   
    <span data-ttu-id="95a82-225">a.</span><span class="sxs-lookup"><span data-stu-id="95a82-225">a.</span></span> <span data-ttu-id="95a82-226">在 hello**電子郵件地址**文字方塊中，型別 hello**電子郵件地址**hello 使用者的 **BrittaSimon@contoso.com** 。</span><span class="sxs-lookup"><span data-stu-id="95a82-226">In hello **Email Address** textbox, type hello **email address** of hello user **BrittaSimon@contoso.com**.</span></span>  
   
    <span data-ttu-id="95a82-227">b.</span><span class="sxs-lookup"><span data-stu-id="95a82-227">b.</span></span> <span data-ttu-id="95a82-228">在 hello**密碼**和**確認密碼**等文字方塊中，型別 hello**密碼**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="95a82-228">In hello **Password** and **Confirm Password** textboxes, type hello **password** of BrittaSimon.</span></span> 
   
    <span data-ttu-id="95a82-229">c.</span><span class="sxs-lookup"><span data-stu-id="95a82-229">c.</span></span> <span data-ttu-id="95a82-230">在 hello**名字**文字方塊中，型別 hello**名字**hello 使用者的**許**。</span><span class="sxs-lookup"><span data-stu-id="95a82-230">In hello **First Name** textbox, type hello **First Name** of hello user **Britta**.</span></span> 
   
    <span data-ttu-id="95a82-231">d.</span><span class="sxs-lookup"><span data-stu-id="95a82-231">d.</span></span> <span data-ttu-id="95a82-232">在 hello**姓氏**文字方塊中，型別 hello**姓氏**hello 使用者的**Simon**。</span><span class="sxs-lookup"><span data-stu-id="95a82-232">In hello **Last Name** textbox, type hello **Last Name** of hello user **Simon**.</span></span>
   
    <span data-ttu-id="95a82-233">e.</span><span class="sxs-lookup"><span data-stu-id="95a82-233">e.</span></span> <span data-ttu-id="95a82-234">在 hello**公司**文字方塊中，型別 hello**公司名稱**的 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="95a82-234">In hello **Company** textbox, type hello **Company name** of hello user.</span></span> 
   
    <span data-ttu-id="95a82-235">f.</span><span class="sxs-lookup"><span data-stu-id="95a82-235">f.</span></span> <span data-ttu-id="95a82-236">在 hello**國家/地區**文字方塊中，選取 hello**國家/地區**的 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="95a82-236">In hello **Country** textbox, select hello **Country** of hello user.</span></span>
  
    <span data-ttu-id="95a82-237">g.</span><span class="sxs-lookup"><span data-stu-id="95a82-237">g.</span></span> <span data-ttu-id="95a82-238">在 hello **ZIP**文字方塊中，型別 hello**郵遞區號**的 hello 縣 （市）。</span><span class="sxs-lookup"><span data-stu-id="95a82-238">In hello **ZIP** textbox, type hello **ZIP code** of hello city.</span></span>
   
    <span data-ttu-id="95a82-239">h.</span><span class="sxs-lookup"><span data-stu-id="95a82-239">h.</span></span> <span data-ttu-id="95a82-240">在 hello**縣 （市)**文字方塊中，型別 hello**縣 （市） 名稱**的 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="95a82-240">In hello **City** textbox, type hello **City name** of hello user.</span></span>

    <span data-ttu-id="95a82-241">i.</span><span class="sxs-lookup"><span data-stu-id="95a82-241">i.</span></span> <span data-ttu-id="95a82-242">選取 [語言] 。</span><span class="sxs-lookup"><span data-stu-id="95a82-242">Select a **Language**.</span></span>
   
    <span data-ttu-id="95a82-243">j.</span><span class="sxs-lookup"><span data-stu-id="95a82-243">j.</span></span> <span data-ttu-id="95a82-244">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="95a82-244">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="95a82-245">您可以使用任何其他 Picturepark 使用者帳戶建立工具或 Api 提供 Picturepark tooprovision Azure AD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="95a82-245">You can use any other Picturepark user account creation tools or APIs provided by Picturepark tooprovision Azure AD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="95a82-246">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="95a82-246">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="95a82-247">在本節中，您可以授與存取 tooPicturepark 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="95a82-247">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPicturepark.</span></span>

![指派使用者][200] 

<span data-ttu-id="95a82-249">**tooassign 許 Simon tooPicturepark，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="95a82-249">**tooassign Britta Simon tooPicturepark, perform hello following steps:**</span></span>

1. <span data-ttu-id="95a82-250">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="95a82-250">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="95a82-252">在 [hello] 應用程式清單中，選取**Picturepark**。</span><span class="sxs-lookup"><span data-stu-id="95a82-252">In hello applications list, select **Picturepark**.</span></span>

    ![設定單一登入](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_app.png) 

3. <span data-ttu-id="95a82-254">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="95a82-254">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="95a82-256">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="95a82-256">Click **Add** button.</span></span> <span data-ttu-id="95a82-257">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="95a82-257">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="95a82-259">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="95a82-259">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="95a82-260">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="95a82-260">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="95a82-261">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="95a82-261">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="95a82-262">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="95a82-262">Testing single sign-on</span></span>

<span data-ttu-id="95a82-263">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="95a82-263">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="95a82-264">當您按一下 hello Picturepark 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Picturepark 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="95a82-264">When you click hello Picturepark tile in hello Access Panel, you should get automatically signed-on tooyour Picturepark application.</span></span> <span data-ttu-id="95a82-265">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="95a82-265">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="95a82-266">其他資源</span><span class="sxs-lookup"><span data-stu-id="95a82-266">Additional resources</span></span>

* [<span data-ttu-id="95a82-267">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="95a82-267">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="95a82-268">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="95a82-268">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_203.png

