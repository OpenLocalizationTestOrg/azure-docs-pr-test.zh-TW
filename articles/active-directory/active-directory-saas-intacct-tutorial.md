---
title: "教學課程：Azure Active Directory 與 Intacct 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Intacct 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 92518e02-a62c-4b1b-a8e9-2803eb2b49ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 3500039615166c2f61fb408d85bb82dfaefba134
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intacct"></a><span data-ttu-id="b5049-103">教學課程：Azure Active Directory 與 Intacct 整合</span><span class="sxs-lookup"><span data-stu-id="b5049-103">Tutorial: Azure Active Directory integration with Intacct</span></span>

<span data-ttu-id="b5049-104">在此教學課程中，您學會如何 toointegrate Intacct 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="b5049-104">In this tutorial, you learn how toointegrate Intacct with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b5049-105">與 Azure AD 整合 Intacct 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="b5049-105">Integrating Intacct with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b5049-106">您可以控制存取 tooIntacct Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="b5049-106">You can control in Azure AD who has access tooIntacct</span></span>
- <span data-ttu-id="b5049-107">您可以啟用您的使用者 tooautomatically get 登入 tooIntacct （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="b5049-107">You can enable your users tooautomatically get signed-on tooIntacct (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b5049-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="b5049-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b5049-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="b5049-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b5049-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="b5049-110">Prerequisites</span></span>

<span data-ttu-id="b5049-111">tooconfigure 與 Intacct 的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="b5049-111">tooconfigure Azure AD integration with Intacct, you need hello following items:</span></span>

- <span data-ttu-id="b5049-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b5049-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b5049-113">已啟用 Intacct 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b5049-113">An Intacct single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b5049-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="b5049-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b5049-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="b5049-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b5049-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="b5049-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b5049-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="b5049-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b5049-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="b5049-118">Scenario description</span></span>
<span data-ttu-id="b5049-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b5049-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b5049-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="b5049-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b5049-121">從 hello 圖庫加入 Intacct</span><span class="sxs-lookup"><span data-stu-id="b5049-121">Adding Intacct from hello gallery</span></span>
2. <span data-ttu-id="b5049-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b5049-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intacct-from-hello-gallery"></a><span data-ttu-id="b5049-123">從 hello 圖庫加入 Intacct</span><span class="sxs-lookup"><span data-stu-id="b5049-123">Adding Intacct from hello gallery</span></span>
<span data-ttu-id="b5049-124">tooconfigure hello 整合 Intacct 的 Azure AD，您需要 tooadd Intacct hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b5049-124">tooconfigure hello integration of Intacct into Azure AD, you need tooadd Intacct from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b5049-125">**tooadd Intacct 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b5049-125">**tooadd Intacct from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b5049-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="b5049-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b5049-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="b5049-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b5049-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="b5049-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="b5049-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="b5049-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="b5049-133">在 [hello] 搜尋方塊中，輸入**Intacct**。</span><span class="sxs-lookup"><span data-stu-id="b5049-133">In hello search box, type **Intacct**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_search.png)

5. <span data-ttu-id="b5049-135">在 hello 結果 窗格中，選取  **Intacct**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b5049-135">In hello results panel, select **Intacct**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b5049-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b5049-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b5049-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Intacct 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b5049-138">In this section, you configure and test Azure AD single sign-on with Intacct based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b5049-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 Intacct 中是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="b5049-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Intacct is tooa user in Azure AD.</span></span> <span data-ttu-id="b5049-140">換句話說，Azure AD 使用者與 hello Intacct 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="b5049-140">In other words, a link relationship between an Azure AD user and hello related user in Intacct needs toobe established.</span></span>

<span data-ttu-id="b5049-141">在 Intacct 中，將指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="b5049-141">In Intacct, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b5049-142">tooconfigure 及測試 Azure AD 單一登入 Intacct，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="b5049-142">tooconfigure and test Azure AD single sign-on with Intacct, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b5049-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="b5049-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b5049-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="b5049-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b5049-145">**[建立測試使用者 Intacct](#creating-an-intacct-test-user)**  -toohave 許 Simon Intacct 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="b5049-145">**[Creating an Intacct test user](#creating-an-intacct-test-user)** - toohave a counterpart of Britta Simon in Intacct that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b5049-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b5049-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b5049-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="b5049-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b5049-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b5049-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b5049-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Intacct 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="b5049-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Intacct application.</span></span>

<span data-ttu-id="b5049-150">**tooconfigure Azure AD 單一登入 Intacct，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b5049-150">**tooconfigure Azure AD single sign-on with Intacct, perform hello following steps:**</span></span>

1. <span data-ttu-id="b5049-151">在 Azure 入口網站上 hello hello **Intacct**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="b5049-151">In hello Azure portal, on hello **Intacct** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="b5049-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b5049-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_samlbase.png)

3. <span data-ttu-id="b5049-155">在 hello **Intacct 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="b5049-155">On hello **Intacct Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_url.png)

    <span data-ttu-id="b5049-157">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:</span><span class="sxs-lookup"><span data-stu-id="b5049-157">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.intacct.com/ia/acct/sso_response.phtml`|
    | `https://www.intacct.com/ia/acct/sso_response.phtml` |

    > [!NOTE] 
    > <span data-ttu-id="b5049-158">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="b5049-158">This value is not real.</span></span> <span data-ttu-id="b5049-159">更新此值與 hello 實際的回覆 URL。</span><span class="sxs-lookup"><span data-stu-id="b5049-159">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="b5049-160">請連絡[Intacct 支援小組](https://us.intacct.com/support)tooget 此值。</span><span class="sxs-lookup"><span data-stu-id="b5049-160">Contact [Intacct support team](https://us.intacct.com/support) tooget this value.</span></span>

4. <span data-ttu-id="b5049-161">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="b5049-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_certificate.png) 

5. <span data-ttu-id="b5049-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="b5049-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-intacct-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b5049-165">在 hello **Intacct 組態**區段中，按一下**設定 Intacct** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="b5049-165">On hello **Intacct Configuration** section, click **Configure Intacct** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b5049-166">複製 hello **SAML 實體識別碼和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="b5049-166">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_configure.png) 

7. <span data-ttu-id="b5049-168">在不同的網頁瀏覽器視窗中，以系統管理員身分登入 tooyour Intacct 公司網站。</span><span class="sxs-lookup"><span data-stu-id="b5049-168">In a different web browser window, sign in tooyour Intacct company site as an administrator.</span></span>

8. <span data-ttu-id="b5049-169">按一下 hello**公司**索引標籤，然後再按一下**公司資訊**。</span><span class="sxs-lookup"><span data-stu-id="b5049-169">Click hello **Company** tab, and then click **Company Info**.</span></span>

    <span data-ttu-id="b5049-170">![公司](./media/active-directory-saas-intacct-tutorial/ic790037.png "公司")</span><span class="sxs-lookup"><span data-stu-id="b5049-170">![Company](./media/active-directory-saas-intacct-tutorial/ic790037.png "Company")</span></span>

9. <span data-ttu-id="b5049-171">按一下 hello**安全性**索引標籤，然後再按一下**編輯**。</span><span class="sxs-lookup"><span data-stu-id="b5049-171">Click hello **Security** tab, and then click **Edit**.</span></span>

    <span data-ttu-id="b5049-172">![安全性](./media/active-directory-saas-intacct-tutorial/ic790038.png "安全性")</span><span class="sxs-lookup"><span data-stu-id="b5049-172">![Security](./media/active-directory-saas-intacct-tutorial/ic790038.png "Security")</span></span>

10. <span data-ttu-id="b5049-173">在 hello**單一登入 (SSO)**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="b5049-173">In hello **Single sign on (SSO)** section, perform hello following steps:</span></span>

    <span data-ttu-id="b5049-174">![單一登入](./media/active-directory-saas-intacct-tutorial/ic790039.png "單一登入")</span><span class="sxs-lookup"><span data-stu-id="b5049-174">![Single sign on](./media/active-directory-saas-intacct-tutorial/ic790039.png "single sign on")</span></span>

    <span data-ttu-id="b5049-175">a.</span><span class="sxs-lookup"><span data-stu-id="b5049-175">a.</span></span> <span data-ttu-id="b5049-176">選取 [啟用單一登入] 。</span><span class="sxs-lookup"><span data-stu-id="b5049-176">Select **Enable single sign on**.</span></span>

    <span data-ttu-id="b5049-177">b.</span><span class="sxs-lookup"><span data-stu-id="b5049-177">b.</span></span> <span data-ttu-id="b5049-178">在 [身分識別提供者類型]，選取 **SAML 2.0**。</span><span class="sxs-lookup"><span data-stu-id="b5049-178">As **Identity provider type**, select **SAML 2.0**.</span></span>

    <span data-ttu-id="b5049-179">c.</span><span class="sxs-lookup"><span data-stu-id="b5049-179">c.</span></span> <span data-ttu-id="b5049-180">在**簽發者 URL**文字方塊中，貼上 hello 值**SAML 實體識別碼**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="b5049-180">In **Issuer URL** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="b5049-181">d.</span><span class="sxs-lookup"><span data-stu-id="b5049-181">d.</span></span> <span data-ttu-id="b5049-182">在**登入 URL**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="b5049-182">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="b5049-183">e.</span><span class="sxs-lookup"><span data-stu-id="b5049-183">e.</span></span> <span data-ttu-id="b5049-184">開啟您**base-64**編碼在記事本中，複製到剪貼簿，其內容的 hello 的憑證，然後將它貼入 toohello**憑證**方塊。</span><span class="sxs-lookup"><span data-stu-id="b5049-184">Open your **base-64** encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Certificate** box.</span></span>
   
    <span data-ttu-id="b5049-185">f.</span><span class="sxs-lookup"><span data-stu-id="b5049-185">f.</span></span> <span data-ttu-id="b5049-186">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="b5049-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="b5049-187">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="b5049-187">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b5049-188">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="b5049-188">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b5049-189">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b5049-189">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b5049-190">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b5049-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="b5049-191">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="b5049-191">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="b5049-193">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b5049-193">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b5049-194">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="b5049-194">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-intacct-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b5049-196">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="b5049-196">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-intacct-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b5049-198">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="b5049-198">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-intacct-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b5049-200">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="b5049-200">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-intacct-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b5049-202">a.</span><span class="sxs-lookup"><span data-stu-id="b5049-202">a.</span></span> <span data-ttu-id="b5049-203">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="b5049-203">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b5049-204">b.</span><span class="sxs-lookup"><span data-stu-id="b5049-204">b.</span></span> <span data-ttu-id="b5049-205">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="b5049-205">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b5049-206">c.</span><span class="sxs-lookup"><span data-stu-id="b5049-206">c.</span></span> <span data-ttu-id="b5049-207">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="b5049-207">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b5049-208">d.</span><span class="sxs-lookup"><span data-stu-id="b5049-208">d.</span></span> <span data-ttu-id="b5049-209">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="b5049-209">Click **Create**.</span></span>
 
### <a name="creating-an-intacct-test-user"></a><span data-ttu-id="b5049-210">建立 Intacct 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b5049-210">Creating an Intacct test user</span></span>

<span data-ttu-id="b5049-211">tooset 註冊 Azure AD 使用者讓他們可以登入 tooIntacct，它們必須佈建到 Intacct。</span><span class="sxs-lookup"><span data-stu-id="b5049-211">tooset up Azure AD users so they can sign in tooIntacct, they must be provisioned into Intacct.</span></span> <span data-ttu-id="b5049-212">在 Intacct 中，佈建是手動工作。</span><span class="sxs-lookup"><span data-stu-id="b5049-212">For Intacct, provisioning is a manual task.</span></span>

<span data-ttu-id="b5049-213">**tooprovision 使用者帳戶，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b5049-213">**tooprovision user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="b5049-214">登入 tooyour **Intacct**租用戶。</span><span class="sxs-lookup"><span data-stu-id="b5049-214">Sign in tooyour **Intacct** tenant.</span></span>

2. <span data-ttu-id="b5049-215">按一下 hello**公司**索引標籤，然後再按一下**使用者**。</span><span class="sxs-lookup"><span data-stu-id="b5049-215">Click hello **Company** tab, and then click **Users**.</span></span>

    <span data-ttu-id="b5049-216">![使用者](./media/active-directory-saas-intacct-tutorial/ic790041.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="b5049-216">![Users](./media/active-directory-saas-intacct-tutorial/ic790041.png "Users")</span></span>
3. <span data-ttu-id="b5049-217">按一下 hello**新增** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="b5049-217">Click hello **Add** tab.</span></span>

    <span data-ttu-id="b5049-218">![新增](./media/active-directory-saas-intacct-tutorial/ic790042.png "新增")</span><span class="sxs-lookup"><span data-stu-id="b5049-218">![Add](./media/active-directory-saas-intacct-tutorial/ic790042.png "Add")</span></span>
4. <span data-ttu-id="b5049-219">在 hello**使用者資訊**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="b5049-219">In hello **User Information** section, perform hello following steps:</span></span>

    <span data-ttu-id="b5049-220">![使用者資訊](./media/active-directory-saas-intacct-tutorial/ic790043.png "使用者資訊")</span><span class="sxs-lookup"><span data-stu-id="b5049-220">![User Information](./media/active-directory-saas-intacct-tutorial/ic790043.png "User Information")</span></span>

    <span data-ttu-id="b5049-221">a.</span><span class="sxs-lookup"><span data-stu-id="b5049-221">a.</span></span> <span data-ttu-id="b5049-222">輸入 hello**使用者識別碼**，hello**姓氏**，**名字**，hello**電子郵件地址**，hello**標題**，和 hello**電話**hello 將所要 tooprovision 的 Azure AD 帳戶**使用者資訊**> 一節。</span><span class="sxs-lookup"><span data-stu-id="b5049-222">Enter hello **User ID**, hello **Last name**, **First name**, hello **Email address**, hello **Title**, and hello **Phone** of an Azure AD account that you want tooprovision into hello **User Information** section.</span></span>

    <span data-ttu-id="b5049-223">b.</span><span class="sxs-lookup"><span data-stu-id="b5049-223">b.</span></span> <span data-ttu-id="b5049-224">選取 hello**系統管理員權限**想 tooprovision 的 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="b5049-224">Select hello **Admin privileges** of an Azure AD account that you want tooprovision.</span></span>
   
    <span data-ttu-id="b5049-225">c.</span><span class="sxs-lookup"><span data-stu-id="b5049-225">c.</span></span> <span data-ttu-id="b5049-226">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="b5049-226">Click **Save**.</span></span> <span data-ttu-id="b5049-227">hello Azure AD 帳戶持有者會收到一封電子郵件，並且遵循連結 tooconfirm 他們的帳戶之前就會生效。</span><span class="sxs-lookup"><span data-stu-id="b5049-227">hello Azure AD account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

>[!NOTE]
><span data-ttu-id="b5049-228">tooprovision Azure AD 使用者帳戶，您可以使用其他 Intacct 使用者帳戶建立工具或 Intacct 所提供的 Api。</span><span class="sxs-lookup"><span data-stu-id="b5049-228">tooprovision Azure AD user accounts, you can use other Intacct user account creation tools or APIs that are provided by Intacct.</span></span>
        
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b5049-229">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="b5049-229">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b5049-230">在本節中，您可以授與存取 tooIntacct 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b5049-230">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIntacct.</span></span>

![指派使用者][200] 

<span data-ttu-id="b5049-232">**tooassign 許 Simon tooIntacct，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b5049-232">**tooassign Britta Simon tooIntacct, perform hello following steps:**</span></span>

1. <span data-ttu-id="b5049-233">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="b5049-233">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="b5049-235">在 [hello] 應用程式清單中，選取**Intacct**。</span><span class="sxs-lookup"><span data-stu-id="b5049-235">In hello applications list, select **Intacct**.</span></span>

    ![設定單一登入](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_app.png) 

3. <span data-ttu-id="b5049-237">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="b5049-237">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="b5049-239">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b5049-239">Click **Add** button.</span></span> <span data-ttu-id="b5049-240">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="b5049-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="b5049-242">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="b5049-242">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b5049-243">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b5049-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b5049-244">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b5049-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b5049-245">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="b5049-245">Testing single sign-on</span></span>

<span data-ttu-id="b5049-246">在本節中，您 Azure AD 單一登入組態使用測試 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="b5049-246">In this section, you test your Azure AD single sign-on configuration by using hello Access Panel.</span></span>

<span data-ttu-id="b5049-247">當您按一下 hello Intacct 磚 hello 存取面板中的時，您應該會自動登入 tooyour Intacct 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b5049-247">When you click hello Intacct tile in hello Access Panel, you should be automatically signed in tooyour Intacct application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b5049-248">其他資源</span><span class="sxs-lookup"><span data-stu-id="b5049-248">Additional resources</span></span>

* [<span data-ttu-id="b5049-249">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b5049-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b5049-250">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="b5049-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_203.png

