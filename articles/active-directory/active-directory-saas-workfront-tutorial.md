---
title: "教學課程：Azure Active Directory 與 Workfront 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Workfront 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: e7249b9ec769f19cf5aa7d44ff6f58705df4020a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workfront"></a><span data-ttu-id="cb692-103">教學課程：Azure Active Directory 與 Workfront 整合</span><span class="sxs-lookup"><span data-stu-id="cb692-103">Tutorial: Azure Active Directory integration with Workfront</span></span>

<span data-ttu-id="cb692-104">在此教學課程中，您學會如何 toointegrate Workfront 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="cb692-104">In this tutorial, you learn how toointegrate Workfront with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cb692-105">與 Azure AD 整合 Workfront 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="cb692-105">Integrating Workfront with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cb692-106">您可以控制存取 tooWorkfront Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="cb692-106">You can control in Azure AD who has access tooWorkfront</span></span>
- <span data-ttu-id="cb692-107">您可以啟用您的使用者 tooautomatically get 登入 tooWorkfront （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="cb692-107">You can enable your users tooautomatically get signed-on tooWorkfront (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cb692-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="cb692-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cb692-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="cb692-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb692-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="cb692-110">Prerequisites</span></span>

<span data-ttu-id="cb692-111">tooconfigure Workfront 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="cb692-111">tooconfigure Azure AD integration with Workfront, you need hello following items:</span></span>

- <span data-ttu-id="cb692-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="cb692-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cb692-113">已啟用 Workfront 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="cb692-113">A Workfront single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cb692-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="cb692-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cb692-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="cb692-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cb692-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="cb692-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cb692-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="cb692-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cb692-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="cb692-118">Scenario description</span></span>
<span data-ttu-id="cb692-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cb692-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cb692-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="cb692-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cb692-121">從 hello 圖庫加入 Workfront</span><span class="sxs-lookup"><span data-stu-id="cb692-121">Adding Workfront from hello gallery</span></span>
2. <span data-ttu-id="cb692-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="cb692-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workfront-from-hello-gallery"></a><span data-ttu-id="cb692-123">從 hello 圖庫加入 Workfront</span><span class="sxs-lookup"><span data-stu-id="cb692-123">Adding Workfront from hello gallery</span></span>
<span data-ttu-id="cb692-124">tooconfigure hello 整合 Workfront 到 Azure AD，您需要 tooadd Workfront hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cb692-124">tooconfigure hello integration of Workfront into Azure AD, you need tooadd Workfront from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cb692-125">**tooadd Workfront 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="cb692-125">**tooadd Workfront from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb692-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="cb692-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cb692-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="cb692-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cb692-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="cb692-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="cb692-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="cb692-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="cb692-133">在 [hello] 搜尋方塊中，輸入**Workfront**。</span><span class="sxs-lookup"><span data-stu-id="cb692-133">In hello search box, type **Workfront**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_search.png)

5. <span data-ttu-id="cb692-135">在 hello 結果 窗格中，選取  **Workfront**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cb692-135">In hello results panel, select **Workfront**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cb692-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="cb692-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cb692-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Workfront 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cb692-138">In this section, you configure and test Azure AD single sign-on with Workfront based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cb692-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Workfront 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="cb692-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workfront is tooa user in Azure AD.</span></span> <span data-ttu-id="cb692-140">換句話說，Azure AD 使用者與 hello Workfront 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="cb692-140">In other words, a link relationship between an Azure AD user and hello related user in Workfront needs toobe established.</span></span>

<span data-ttu-id="cb692-141">Workfront 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="cb692-141">In Workfront, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="cb692-142">tooconfigure 及 Workfront 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="cb692-142">tooconfigure and test Azure AD single sign-on with Workfront, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cb692-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="cb692-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cb692-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="cb692-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cb692-145">**[建立測試使用者 Workfront](#creating-a-workfront-test-user)**  -toohave 許 Simon Workfront 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="cb692-145">**[Creating a Workfront test user](#creating-a-workfront-test-user)** - toohave a counterpart of Britta Simon in Workfront that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cb692-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cb692-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cb692-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="cb692-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cb692-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="cb692-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cb692-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Workfront 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="cb692-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workfront application.</span></span>

<span data-ttu-id="cb692-150">**tooconfigure Azure AD 單一登入與 Workfront，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="cb692-150">**tooconfigure Azure AD single sign-on with Workfront, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb692-151">在 Azure 入口網站上 hello hello **Workfront**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="cb692-151">In hello Azure portal, on hello **Workfront** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="cb692-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cb692-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_samlbase.png)

3. <span data-ttu-id="cb692-155">在 hello **Workfront 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="cb692-155">On hello **Workfront Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_url.png)

    <span data-ttu-id="cb692-157">a.</span><span class="sxs-lookup"><span data-stu-id="cb692-157">a.</span></span> <span data-ttu-id="cb692-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.attask-ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="cb692-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.attask-ondemand.com`</span></span>

    <span data-ttu-id="cb692-159">b.</span><span class="sxs-lookup"><span data-stu-id="cb692-159">b.</span></span> <span data-ttu-id="cb692-160">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.attasksandbox.com/SAML2`</span><span class="sxs-lookup"><span data-stu-id="cb692-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.attasksandbox.com/SAML2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cb692-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="cb692-161">These values are not real.</span></span> <span data-ttu-id="cb692-162">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="cb692-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="cb692-163">請連絡[Workfront 用戶端支援小組](https://www.workfront.com/contact-us/)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="cb692-163">Contact [Workfront Client support team](https://www.workfront.com/contact-us/) tooget these values.</span></span> 
 
4. <span data-ttu-id="cb692-164">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="cb692-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello Certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_certificate.png) 

5. <span data-ttu-id="cb692-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="cb692-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-workfront-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cb692-168">在 hello **Workfront 組態**區段中，按一下**設定 Workfront** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="cb692-168">On hello **Workfront Configuration** section, click **Configure Workfront** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="cb692-169">複製 hello**登出 URL 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="cb692-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_configure.png) 

7. <span data-ttu-id="cb692-171">以系統管理員身分登入 tooyour Workfront 公司網站。</span><span class="sxs-lookup"><span data-stu-id="cb692-171">Sign-on tooyour Workfront company site as administrator.</span></span>

8. <span data-ttu-id="cb692-172">跳過**單一登入組態**。</span><span class="sxs-lookup"><span data-stu-id="cb692-172">Go too**Single Sign On Configuration**.</span></span>

9. <span data-ttu-id="cb692-173">在 [hello**單一登入**] 對話方塊中，執行下列步驟的 hello</span><span class="sxs-lookup"><span data-stu-id="cb692-173">On hello **Single Sign-On** dialog, perform hello following steps</span></span>
    
    ![設定單一登入][23]
   
    <span data-ttu-id="cb692-175">a.</span><span class="sxs-lookup"><span data-stu-id="cb692-175">a.</span></span> <span data-ttu-id="cb692-176">針對 [類型]，選取 [SAML 2.0]。</span><span class="sxs-lookup"><span data-stu-id="cb692-176">As **Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="cb692-177">b.</span><span class="sxs-lookup"><span data-stu-id="cb692-177">b.</span></span> <span data-ttu-id="cb692-178">選取 [服務提供者識別碼]。</span><span class="sxs-lookup"><span data-stu-id="cb692-178">Select **Service Provider ID**.</span></span>
   
    <span data-ttu-id="cb692-179">c.</span><span class="sxs-lookup"><span data-stu-id="cb692-179">c.</span></span> <span data-ttu-id="cb692-180">貼上 hello **SAML 單一登入服務 URL**到 hello**登入入口網站 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="cb692-180">Paste hello **SAML Single Sign-On Service URL** into hello **Login Portal URL** textbox.</span></span>
   
    <span data-ttu-id="cb692-181">d.</span><span class="sxs-lookup"><span data-stu-id="cb692-181">d.</span></span> <span data-ttu-id="cb692-182">貼上**單一登出服務 URL**到 hello**登出 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="cb692-182">Paste **Single Sign-Out Service URL** into hello **Sign-Out URL** textbox.</span></span>
   
    <span data-ttu-id="cb692-183">e.</span><span class="sxs-lookup"><span data-stu-id="cb692-183">e.</span></span> <span data-ttu-id="cb692-184">貼上**變更密碼 URL**到 hello**變更密碼 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="cb692-184">Paste **Change Password URL** into hello **Change Password URL** textbox.</span></span>
   
    <span data-ttu-id="cb692-185">f.</span><span class="sxs-lookup"><span data-stu-id="cb692-185">f.</span></span> <span data-ttu-id="cb692-186">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="cb692-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="cb692-187">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="cb692-187">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cb692-188">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="cb692-188">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cb692-189">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cb692-189">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cb692-190">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="cb692-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="cb692-191">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="cb692-191">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="cb692-193">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="cb692-193">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb692-194">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="cb692-194">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workfront-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cb692-196">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="cb692-196">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workfront-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cb692-198">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="cb692-198">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workfront-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cb692-200">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="cb692-200">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workfront-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cb692-202">a.</span><span class="sxs-lookup"><span data-stu-id="cb692-202">a.</span></span> <span data-ttu-id="cb692-203">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="cb692-203">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cb692-204">b.</span><span class="sxs-lookup"><span data-stu-id="cb692-204">b.</span></span> <span data-ttu-id="cb692-205">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="cb692-205">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cb692-206">c.</span><span class="sxs-lookup"><span data-stu-id="cb692-206">c.</span></span> <span data-ttu-id="cb692-207">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="cb692-207">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cb692-208">d.</span><span class="sxs-lookup"><span data-stu-id="cb692-208">d.</span></span> <span data-ttu-id="cb692-209">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="cb692-209">Click **Create**.</span></span>
 
### <a name="creating-a-workfront-test-user"></a><span data-ttu-id="cb692-210">建立 Workfront 測試使用者</span><span class="sxs-lookup"><span data-stu-id="cb692-210">Creating a Workfront test user</span></span>

<span data-ttu-id="cb692-211">hello 本節目標在於 toocreate Workfront 中呼叫許 Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="cb692-211">hello objective of this section is toocreate a user called Britta Simon in Workfront.</span></span>

<span data-ttu-id="cb692-212">**toocreate 呼叫許 Simon Workfront，在使用者執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="cb692-212">**toocreate a user called Britta Simon in Workfront, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb692-213">登入 tooyour Workfront 公司站台系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="cb692-213">Sign on tooyour Workfront company site as administrator.</span></span>
2. <span data-ttu-id="cb692-214">在 hello 最上層顯示 hello 功能表上，按一下**人員**。</span><span class="sxs-lookup"><span data-stu-id="cb692-214">In hello menu on hello top, click **People**.</span></span>
3. <span data-ttu-id="cb692-215">按一下 [新增人員] 。</span><span class="sxs-lookup"><span data-stu-id="cb692-215">Click **New Person**.</span></span> 
4. <span data-ttu-id="cb692-216">在 hello 新增人員 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="cb692-216">On hello New Person dialog, perform hello following steps:</span></span>
   
    ![建立 Workfront 測試使用者][21] 
   
    <span data-ttu-id="cb692-218">a.</span><span class="sxs-lookup"><span data-stu-id="cb692-218">a.</span></span> <span data-ttu-id="cb692-219">在 hello**名字**文字方塊中，輸入 「 許。 」</span><span class="sxs-lookup"><span data-stu-id="cb692-219">In hello **First Name** textbox, type "Britta."</span></span>
   
    <span data-ttu-id="cb692-220">b.</span><span class="sxs-lookup"><span data-stu-id="cb692-220">b.</span></span> <span data-ttu-id="cb692-221">在 hello**姓氏**文字方塊中，輸入 「 Simon。 」</span><span class="sxs-lookup"><span data-stu-id="cb692-221">In hello **Last Name** textbox, type "Simon."</span></span>
   
    <span data-ttu-id="cb692-222">c.</span><span class="sxs-lookup"><span data-stu-id="cb692-222">c.</span></span> <span data-ttu-id="cb692-223">在 hello**電子郵件地址**文字方塊中，輸入 Azure Active Directory 中許 Simon 的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="cb692-223">In hello **Email Address** textbox, type Britta Simon's email address in Azure Active Directory.</span></span>
   
    <span data-ttu-id="cb692-224">d.</span><span class="sxs-lookup"><span data-stu-id="cb692-224">d.</span></span> <span data-ttu-id="cb692-225">按一下 [新增人員] 。</span><span class="sxs-lookup"><span data-stu-id="cb692-225">Click **Add Person**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cb692-226">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="cb692-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cb692-227">在本節中，您可以授與存取 tooWorkfront 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cb692-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkfront.</span></span>

![指派使用者][200] 

<span data-ttu-id="cb692-229">**tooassign 許 Simon tooWorkfront，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="cb692-229">**tooassign Britta Simon tooWorkfront, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb692-230">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="cb692-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="cb692-232">在 [hello] 應用程式清單中，選取**Workfront**。</span><span class="sxs-lookup"><span data-stu-id="cb692-232">In hello applications list, select **Workfront**.</span></span>

    ![設定單一登入](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_app.png) 

3. <span data-ttu-id="cb692-234">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="cb692-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="cb692-236">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cb692-236">Click **Add** button.</span></span> <span data-ttu-id="cb692-237">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="cb692-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="cb692-239">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="cb692-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cb692-240">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cb692-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cb692-241">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cb692-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cb692-242">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="cb692-242">Testing single sign-on</span></span>

<span data-ttu-id="cb692-243">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="cb692-243">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cb692-244">當您按一下 hello Workfront 磚 hello 存取面板中的時，您應該取得 Workfront 應用程式的登入頁面。</span><span class="sxs-lookup"><span data-stu-id="cb692-244">When you click hello Workfront tile in hello Access Panel, you should get login page of Workfront application.</span></span>
<span data-ttu-id="cb692-245">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="cb692-245">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="cb692-246">其他資源</span><span class="sxs-lookup"><span data-stu-id="cb692-246">Additional resources</span></span>

* [<span data-ttu-id="cb692-247">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cb692-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cb692-248">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="cb692-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_04.png
[21]:./media/active-directory-saas-workfront-tutorial/tutorial_attask_08.png
[23]:./media/active-directory-saas-workfront-tutorial/tutorial_attask_06.png
[100]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_203.png

