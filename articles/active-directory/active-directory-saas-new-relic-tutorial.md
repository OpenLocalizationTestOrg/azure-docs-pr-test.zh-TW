---
title: "教學課程：Azure Active Directory 與 New Relic 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 New Relic 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3186b9a8-f4d8-45e2-ad82-6275f95e7aa6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: dc8f0df3b18a32bde155e8911a581fc5f91af217
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-new-relic"></a><span data-ttu-id="5769b-103">教學課程：Azure Active Directory 與 New Relic 整合</span><span class="sxs-lookup"><span data-stu-id="5769b-103">Tutorial: Azure Active Directory integration with New Relic</span></span>

<span data-ttu-id="5769b-104">在此教學課程中，您學會如何 toointegrate New Relic 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="5769b-104">In this tutorial, you learn how toointegrate New Relic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5769b-105">New Relic 整合與 Azure AD 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="5769b-105">Integrating New Relic with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5769b-106">您可以控制存取 tooNew Relic 的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="5769b-106">You can control in Azure AD who has access tooNew Relic</span></span>
- <span data-ttu-id="5769b-107">您可以啟用您的使用者 tooautomatically get 登入 tooNew Relic （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="5769b-107">You can enable your users tooautomatically get signed-on tooNew Relic (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5769b-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="5769b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5769b-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="5769b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5769b-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="5769b-110">Prerequisites</span></span>

<span data-ttu-id="5769b-111">tooconfigure 與 New Relic 的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="5769b-111">tooconfigure Azure AD integration with New Relic, you need hello following items:</span></span>

- <span data-ttu-id="5769b-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="5769b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5769b-113">啟用 New Relic 單一登入的訂閱</span><span class="sxs-lookup"><span data-stu-id="5769b-113">A New Relic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5769b-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="5769b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5769b-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="5769b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5769b-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="5769b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5769b-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="5769b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5769b-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="5769b-118">Scenario description</span></span>
<span data-ttu-id="5769b-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5769b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5769b-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="5769b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5769b-121">New Relic 加入從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="5769b-121">Adding New Relic from hello gallery</span></span>
2. <span data-ttu-id="5769b-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5769b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-new-relic-from-hello-gallery"></a><span data-ttu-id="5769b-123">New Relic 加入從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="5769b-123">Adding New Relic from hello gallery</span></span>
<span data-ttu-id="5769b-124">tooconfigure hello 整合 New Relic 的 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd New Relic。</span><span class="sxs-lookup"><span data-stu-id="5769b-124">tooconfigure hello integration of New Relic into Azure AD, you need tooadd New Relic from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5769b-125">**tooadd New Relic 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="5769b-125">**tooadd New Relic from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5769b-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="5769b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5769b-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="5769b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5769b-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="5769b-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="5769b-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="5769b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="5769b-133">在 [hello] 搜尋方塊中，輸入**New Relic**。</span><span class="sxs-lookup"><span data-stu-id="5769b-133">In hello search box, type **New Relic**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_search.png)

5. <span data-ttu-id="5769b-135">在 hello 結果 窗格中，選取  **New Relic**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5769b-135">In hello results panel, select **New Relic**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5769b-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5769b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5769b-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 New Relic 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5769b-138">In this section, you configure and test Azure AD single sign-on with New Relic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5769b-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者 New Relic 中是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="5769b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in New Relic is tooa user in Azure AD.</span></span> <span data-ttu-id="5769b-140">換句話說，Azure AD 使用者與 hello New Relic 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="5769b-140">In other words, a link relationship between an Azure AD user and hello related user in New Relic needs toobe established.</span></span>

<span data-ttu-id="5769b-141">在 New Relic 中，將指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="5769b-141">In New Relic, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5769b-142">tooconfigure 及測試 Azure AD 單一登入 New Relic，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="5769b-142">tooconfigure and test Azure AD single sign-on with New Relic, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5769b-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="5769b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5769b-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="5769b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5769b-145">**[建立 New Relic 測試使用者](#creating-a-new-relic-test-user)** -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示法的 New Relic 中對應項目。</span><span class="sxs-lookup"><span data-stu-id="5769b-145">**[Creating a New Relic test user](#creating-a-new-relic-test-user)** - toohave a counterpart of Britta Simon in New Relic that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5769b-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5769b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5769b-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="5769b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5769b-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5769b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5769b-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 New Relic 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="5769b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your New Relic application.</span></span>

<span data-ttu-id="5769b-150">**tooconfigure Azure AD 單一登入 New Relic，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="5769b-150">**tooconfigure Azure AD single sign-on with New Relic, perform hello following steps:**</span></span>

1. <span data-ttu-id="5769b-151">在 Azure 入口網站上 hello hello **New Relic**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="5769b-151">In hello Azure portal, on hello **New Relic** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="5769b-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5769b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_samlbase.png)

3. <span data-ttu-id="5769b-155">在 hello**新 Relic 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="5769b-155">On hello **New Relic Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_url.png)

    <span data-ttu-id="5769b-157">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.newrelic.com`</span><span class="sxs-lookup"><span data-stu-id="5769b-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.newrelic.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5769b-158">hello 值不是真正的。</span><span class="sxs-lookup"><span data-stu-id="5769b-158">hello value is not real.</span></span> <span data-ttu-id="5769b-159">更新 hello 值與 hello 實際的登入 URL。</span><span class="sxs-lookup"><span data-stu-id="5769b-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="5769b-160">請連絡[新 Relic 用戶端支援小組](https://support.newrelic.com/)tooget hello 值。</span><span class="sxs-lookup"><span data-stu-id="5769b-160">Contact [New Relic Client support team](https://support.newrelic.com/) tooget hello value.</span></span> 
 
4. <span data-ttu-id="5769b-161">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="5769b-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_certificate.png) 

5. <span data-ttu-id="5769b-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="5769b-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-new-relic-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5769b-165">在 hello**新 Relic 組態**區段中，按一下**設定 New Relic** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="5769b-165">On hello **New Relic Configuration** section, click **Configure New Relic** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5769b-166">複製 hello**登出 URL 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="5769b-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_configure.png) 

7. <span data-ttu-id="5769b-168">在不同的網頁瀏覽器視窗中，登入 tooyour **New Relic**以系統管理員身分的公司網站。</span><span class="sxs-lookup"><span data-stu-id="5769b-168">In a different web browser window, sign on tooyour **New Relic** company site as administrator.</span></span>

8. <span data-ttu-id="5769b-169">在 hello 最上層顯示 hello 功能表上，按一下**帳戶設定**。</span><span class="sxs-lookup"><span data-stu-id="5769b-169">In hello menu on hello top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="5769b-170">![帳戶設定](./media/active-directory-saas-new-relic-tutorial/ic797036.png "帳戶設定")</span><span class="sxs-lookup"><span data-stu-id="5769b-170">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797036.png "Account Settings")</span></span>

9. <span data-ttu-id="5769b-171">按一下 hello**安全性和驗證**索引標籤，然後再按一下 [hello**單一登入**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="5769b-171">Click hello **Security and authentication** tab, and then click hello **Single sign on** tab.</span></span>
   
    <span data-ttu-id="5769b-172">![單一登入](./media/active-directory-saas-new-relic-tutorial/ic797037.png "單一登入")</span><span class="sxs-lookup"><span data-stu-id="5769b-172">![Single Sign-On](./media/active-directory-saas-new-relic-tutorial/ic797037.png "Single Sign-On")</span></span>

10. <span data-ttu-id="5769b-173">在 hello SAML 對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="5769b-173">On hello SAML dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="5769b-174">![SAML](./media/active-directory-saas-new-relic-tutorial/ic797038.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="5769b-174">![SAML](./media/active-directory-saas-new-relic-tutorial/ic797038.png "SAML")</span></span>
   
   <span data-ttu-id="5769b-175">a.</span><span class="sxs-lookup"><span data-stu-id="5769b-175">a.</span></span> <span data-ttu-id="5769b-176">按一下**選擇檔案**tooupload 下載的 Azure Active Directory 憑證。</span><span class="sxs-lookup"><span data-stu-id="5769b-176">Click **Choose File** tooupload your downloaded Azure Active Directory certificate.</span></span>

   <span data-ttu-id="5769b-177">b.</span><span class="sxs-lookup"><span data-stu-id="5769b-177">b.</span></span> <span data-ttu-id="5769b-178">在 hello**遠端登入 URL**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="5769b-178">In hello **Remote login URL** textbox,  paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="5769b-179">c.</span><span class="sxs-lookup"><span data-stu-id="5769b-179">c.</span></span> <span data-ttu-id="5769b-180">在 hello**登出登陸 URL**文字方塊中，貼上 hello 值**登出 URL**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="5769b-180">In hello **Logout landing URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

   <span data-ttu-id="5769b-181">d.</span><span class="sxs-lookup"><span data-stu-id="5769b-181">d.</span></span> <span data-ttu-id="5769b-182">按一下 [儲存我的變更] 。</span><span class="sxs-lookup"><span data-stu-id="5769b-182">Click **Save my changes**.</span></span>

> [!TIP]
> <span data-ttu-id="5769b-183">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="5769b-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5769b-184">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="5769b-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5769b-185">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5769b-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5769b-186">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="5769b-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="5769b-187">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="5769b-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="5769b-189">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="5769b-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5769b-190">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="5769b-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-new-relic-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5769b-192">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="5769b-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-new-relic-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5769b-194">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="5769b-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-new-relic-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5769b-196">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="5769b-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-new-relic-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5769b-198">a.</span><span class="sxs-lookup"><span data-stu-id="5769b-198">a.</span></span> <span data-ttu-id="5769b-199">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="5769b-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5769b-200">b.</span><span class="sxs-lookup"><span data-stu-id="5769b-200">b.</span></span> <span data-ttu-id="5769b-201">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="5769b-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5769b-202">c.</span><span class="sxs-lookup"><span data-stu-id="5769b-202">c.</span></span> <span data-ttu-id="5769b-203">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="5769b-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5769b-204">d.</span><span class="sxs-lookup"><span data-stu-id="5769b-204">d.</span></span> <span data-ttu-id="5769b-205">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="5769b-205">Click **Create**.</span></span>
 
### <a name="creating-a-new-relic-test-user"></a><span data-ttu-id="5769b-206">建立 New Relic 測試使用者</span><span class="sxs-lookup"><span data-stu-id="5769b-206">Creating a New Relic test user</span></span>

<span data-ttu-id="5769b-207">在訂單 tooenable Azure Active Directory 使用者 toolog tooNew Relic 中，您必須是佈建到 New Relic。</span><span class="sxs-lookup"><span data-stu-id="5769b-207">In order tooenable Azure Active Directory users toolog in tooNew Relic, they must be provisioned into New Relic.</span></span> <span data-ttu-id="5769b-208">中的 New Relic hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="5769b-208">In hello case of New Relic, provisioning is a manual task.</span></span>

<span data-ttu-id="5769b-209">**tooprovision 使用者帳戶 tooNew Relic，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="5769b-209">**tooprovision a user account tooNew Relic, perform hello following steps:**</span></span>

1. <span data-ttu-id="5769b-210">登入 tooyour **New Relic**以系統管理員身分的公司網站。</span><span class="sxs-lookup"><span data-stu-id="5769b-210">Log in tooyour **New Relic** company site as administrator.</span></span>

2. <span data-ttu-id="5769b-211">在 hello 最上層顯示 hello 功能表上，按一下**帳戶設定**。</span><span class="sxs-lookup"><span data-stu-id="5769b-211">In hello menu on hello top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="5769b-212">![帳戶設定](./media/active-directory-saas-new-relic-tutorial/ic797040.png "帳戶設定")</span><span class="sxs-lookup"><span data-stu-id="5769b-212">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797040.png "Account Settings")</span></span>

3. <span data-ttu-id="5769b-213">在 hello**帳戶**hello 窗格的左側，按一下**摘要**，然後按一下**新增使用者**。</span><span class="sxs-lookup"><span data-stu-id="5769b-213">In hello **Account** pane on hello left side, click **Summary**, and then click **Add user**.</span></span>
   
    <span data-ttu-id="5769b-214">![帳戶設定](./media/active-directory-saas-new-relic-tutorial/ic797041.png "帳戶設定")</span><span class="sxs-lookup"><span data-stu-id="5769b-214">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797041.png "Account Settings")</span></span>

4. <span data-ttu-id="5769b-215">在 [hello**作用中使用者**] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="5769b-215">On hello **Active users** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="5769b-216">![作用中使用者](./media/active-directory-saas-new-relic-tutorial/ic797042.png "作用中使用者")</span><span class="sxs-lookup"><span data-stu-id="5769b-216">![Active Users](./media/active-directory-saas-new-relic-tutorial/ic797042.png "Active Users")</span></span>
   
    <span data-ttu-id="5769b-217">a.</span><span class="sxs-lookup"><span data-stu-id="5769b-217">a.</span></span> <span data-ttu-id="5769b-218">在 hello**電子郵件**文字方塊中，型別 hello 電子郵件地址的有效的 Azure Active Directory 使用者，您想要 tooprovision。</span><span class="sxs-lookup"><span data-stu-id="5769b-218">In hello **Email** textbox, type hello email address of a valid Azure Active Directory user you want tooprovision.</span></span>

    <span data-ttu-id="5769b-219">b.</span><span class="sxs-lookup"><span data-stu-id="5769b-219">b.</span></span> <span data-ttu-id="5769b-220">針對 [角色]，選取 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="5769b-220">As **Role** select **User**.</span></span>

    <span data-ttu-id="5769b-221">c.</span><span class="sxs-lookup"><span data-stu-id="5769b-221">c.</span></span> <span data-ttu-id="5769b-222">按一下 [新增此使用者] 。</span><span class="sxs-lookup"><span data-stu-id="5769b-222">Click **Add this user**.</span></span>

>[!NOTE]
><span data-ttu-id="5769b-223">您可以使用任何其他 New Relic 使用者帳戶建立工具或 Api 提供 New Relic tooprovision AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="5769b-223">You can use any other New Relic user account creation tools or APIs provided by New Relic tooprovision AAD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5769b-224">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="5769b-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5769b-225">在本節中，您可以授與存取 tooNew Relic 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5769b-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNew Relic.</span></span>

![指派使用者][200] 

<span data-ttu-id="5769b-227">**tooassign 許 Simon tooNew Relic，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="5769b-227">**tooassign Britta Simon tooNew Relic, perform hello following steps:**</span></span>

1. <span data-ttu-id="5769b-228">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="5769b-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="5769b-230">在 [hello] 應用程式清單中，選取**New Relic**。</span><span class="sxs-lookup"><span data-stu-id="5769b-230">In hello applications list, select **New Relic**.</span></span>

    ![設定單一登入](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_app.png) 

3. <span data-ttu-id="5769b-232">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="5769b-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="5769b-234">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5769b-234">Click **Add** button.</span></span> <span data-ttu-id="5769b-235">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="5769b-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="5769b-237">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="5769b-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5769b-238">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5769b-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5769b-239">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5769b-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5769b-240">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="5769b-240">Testing single sign-on</span></span>

<span data-ttu-id="5769b-241">hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="5769b-241">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5769b-242">當您按一下 hello New Relic 磚 hello 存取面板中的時，您應該取得 tooyour 自動登入 New Relic 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5769b-242">When you click hello New Relic tile in hello Access Panel, you should get automatically signed-on tooyour New Relic application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5769b-243">其他資源</span><span class="sxs-lookup"><span data-stu-id="5769b-243">Additional resources</span></span>

* [<span data-ttu-id="5769b-244">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5769b-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5769b-245">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="5769b-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_203.png

