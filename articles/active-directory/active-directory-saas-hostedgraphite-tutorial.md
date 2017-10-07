---
title: "教學課程：Azure Active Directory 與 Hosted Graphite 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與裝載 Graphite 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a1ac4d7f-d079-4f3c-b6da-0f520d427ceb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: d8914f6417ba8fbdef1a48e1b36635200ba130d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hosted-graphite"></a><span data-ttu-id="6fcec-103">教學課程：Azure Active Directory 與 Hosted Graphite 整合</span><span class="sxs-lookup"><span data-stu-id="6fcec-103">Tutorial: Azure Active Directory integration with Hosted Graphite</span></span>

<span data-ttu-id="6fcec-104">在此教學課程中，您學會如何 toointegrate Hosted Graphite 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="6fcec-104">In this tutorial, you learn how toointegrate Hosted Graphite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6fcec-105">與 Azure AD 整合裝載 Graphite 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="6fcec-105">Integrating Hosted Graphite with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6fcec-106">您可以控制存取 tooHosted Graphite Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="6fcec-106">You can control in Azure AD who has access tooHosted Graphite</span></span>
- <span data-ttu-id="6fcec-107">您可以啟用您的使用者 tooautomatically get 登入 tooHosted Graphite （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="6fcec-107">You can enable your users tooautomatically get signed-on tooHosted Graphite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6fcec-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="6fcec-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6fcec-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="6fcec-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6fcec-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="6fcec-110">Prerequisites</span></span>

<span data-ttu-id="6fcec-111">tooconfigure 與裝載 Graphite 的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="6fcec-111">tooconfigure Azure AD integration with Hosted Graphite, you need hello following items:</span></span>

- <span data-ttu-id="6fcec-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="6fcec-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6fcec-113">已啟用 Hosted Graphite 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="6fcec-113">A Hosted Graphite single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6fcec-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="6fcec-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6fcec-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="6fcec-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6fcec-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="6fcec-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6fcec-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="6fcec-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6fcec-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="6fcec-118">Scenario description</span></span>
<span data-ttu-id="6fcec-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6fcec-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6fcec-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="6fcec-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6fcec-121">加入裝載 Graphite 從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="6fcec-121">Adding Hosted Graphite from hello gallery</span></span>
2. <span data-ttu-id="6fcec-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6fcec-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hosted-graphite-from-hello-gallery"></a><span data-ttu-id="6fcec-123">加入裝載 Graphite 從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="6fcec-123">Adding Hosted Graphite from hello gallery</span></span>
<span data-ttu-id="6fcec-124">tooconfigure hello 整合裝載 Graphite 到 Azure AD，您需要 tooadd Hosted Graphite hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6fcec-124">tooconfigure hello integration of Hosted Graphite into Azure AD, you need tooadd Hosted Graphite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6fcec-125">**tooadd Hosted Graphite 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="6fcec-125">**tooadd Hosted Graphite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6fcec-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="6fcec-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6fcec-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="6fcec-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6fcec-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="6fcec-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="6fcec-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="6fcec-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="6fcec-133">在 [hello] 搜尋方塊中，輸入**裝載 Graphite**。</span><span class="sxs-lookup"><span data-stu-id="6fcec-133">In hello search box, type **Hosted Graphite**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_search.png)

5. <span data-ttu-id="6fcec-135">在 hello 結果 窗格中，選取 **裝載 Graphite**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6fcec-135">In hello results panel, select **Hosted Graphite**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6fcec-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6fcec-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6fcec-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Hosted Graphite 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6fcec-138">In this section, you configure and test Azure AD single sign-on with Hosted Graphite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6fcec-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中裝載 Graphite 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="6fcec-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Hosted Graphite is tooa user in Azure AD.</span></span> <span data-ttu-id="6fcec-140">換句話說，Azure AD 使用者與 hello 裝載 Graphite 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="6fcec-140">In other words, a link relationship between an Azure AD user and hello related user in Hosted Graphite needs toobe established.</span></span>

<span data-ttu-id="6fcec-141">在裝載 Graphite，將指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="6fcec-141">In Hosted Graphite, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6fcec-142">tooconfigure 及裝載 Graphite 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="6fcec-142">tooconfigure and test Azure AD single sign-on with Hosted Graphite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6fcec-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="6fcec-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6fcec-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="6fcec-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6fcec-145">**[建立裝載 Graphite 測試使用者](#creating-a-hosted-graphite-test-user)** -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示裝載 Graphite 中對應項目。</span><span class="sxs-lookup"><span data-stu-id="6fcec-145">**[Creating a Hosted Graphite test user](#creating-a-hosted-graphite-test-user)** - toohave a counterpart of Britta Simon in Hosted Graphite that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6fcec-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6fcec-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6fcec-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="6fcec-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6fcec-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6fcec-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6fcec-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入裝載 Graphite 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="6fcec-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Hosted Graphite application.</span></span>

<span data-ttu-id="6fcec-150">**tooconfigure Azure AD 單一登入裝載 Graphite，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="6fcec-150">**tooconfigure Azure AD single sign-on with Hosted Graphite, perform hello following steps:**</span></span>

1. <span data-ttu-id="6fcec-151">在 Azure 入口網站上 hello hello**裝載 Graphite**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="6fcec-151">In hello Azure portal, on hello **Hosted Graphite** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="6fcec-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6fcec-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_samlbase.png)

3. <span data-ttu-id="6fcec-155">在 hello**裝載 Graphite 網域和 Url**區段中，如果您想 tooconfigure hello 應用程式中的**IDP 初始化模式**，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="6fcec-155">On hello **Hosted Graphite Domain and URLs** section, if you wish tooconfigure hello application in **IDP initiated mode**, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_url.png)

    <span data-ttu-id="6fcec-157">a.</span><span class="sxs-lookup"><span data-stu-id="6fcec-157">a.</span></span> <span data-ttu-id="6fcec-158">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://www.hostedgraphite.com/metadata/<user id>`</span><span class="sxs-lookup"><span data-stu-id="6fcec-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.hostedgraphite.com/metadata/<user id>`</span></span>

    <span data-ttu-id="6fcec-159">b.</span><span class="sxs-lookup"><span data-stu-id="6fcec-159">b.</span></span> <span data-ttu-id="6fcec-160">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://www.hostedgraphite.com/complete/saml/<user id>`</span><span class="sxs-lookup"><span data-stu-id="6fcec-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://www.hostedgraphite.com/complete/saml/<user id>`</span></span>

4. <span data-ttu-id="6fcec-161">在 hello**裝載 Graphite 網域和 Url**區段中，如果您想 tooconfigure hello 應用程式中的**SP 初始模式**，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="6fcec-161">On hello **Hosted Graphite Domain and URLs** section, if you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_10.png)
  
    <span data-ttu-id="6fcec-163">a.</span><span class="sxs-lookup"><span data-stu-id="6fcec-163">a.</span></span> <span data-ttu-id="6fcec-164">按一下 hello**顯示進階的 URL 設定**選項</span><span class="sxs-lookup"><span data-stu-id="6fcec-164">Click on hello **Show advanced URL settings** option</span></span>

    <span data-ttu-id="6fcec-165">b.</span><span class="sxs-lookup"><span data-stu-id="6fcec-165">b.</span></span> <span data-ttu-id="6fcec-166">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://www.hostedgraphite.com/login/saml/<user id>/`</span><span class="sxs-lookup"><span data-stu-id="6fcec-166">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://www.hostedgraphite.com/login/saml/<user id>/`</span></span>   

    > [!NOTE] 
    > <span data-ttu-id="6fcec-167">請注意這些不是 hello 實際值。</span><span class="sxs-lookup"><span data-stu-id="6fcec-167">Please note that these are not hello real values.</span></span> <span data-ttu-id="6fcec-168">這些值以 hello 有 tooupdate 實際的識別項、 回覆 URL 和登入 URL。</span><span class="sxs-lookup"><span data-stu-id="6fcec-168">You have tooupdate these values with hello actual Identifier, Reply URL and Sign On URL.</span></span> <span data-ttu-id="6fcec-169">tooget 這些值，您可以移 tooAccess]-> [SAML 設定在您的應用程式端或連絡人[裝載 Graphite 支援小組](mailto:help@hostedgraphite.com)。</span><span class="sxs-lookup"><span data-stu-id="6fcec-169">tooget these values, you can go tooAccess->SAML setup on your Application side or Contact [Hosted Graphite support team](mailto:help@hostedgraphite.com).</span></span>
    >
 
5. <span data-ttu-id="6fcec-170">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="6fcec-170">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_certificate.png) 

6. <span data-ttu-id="6fcec-172">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="6fcec-172">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="6fcec-174">在 hello**裝載 Graphite 組態**區段中，按一下**設定裝載 Graphite** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="6fcec-174">On hello **Hosted Graphite Configuration** section, click **Configure Hosted Graphite** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6fcec-175">複製 hello **SAML 實體識別碼和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="6fcec-175">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_configure.png) 

8. <span data-ttu-id="6fcec-177">以系統管理員身分登入 tooyour 裝載 Graphite 租用戶。</span><span class="sxs-lookup"><span data-stu-id="6fcec-177">Sign-on tooyour Hosted Graphite tenant as an administrator.</span></span>

9. <span data-ttu-id="6fcec-178">移 toohello **SAML 設定 頁面**hello 提要欄位中 (**存取 SAML 設定->** )。</span><span class="sxs-lookup"><span data-stu-id="6fcec-178">Go toohello **SAML Setup page** in hello sidebar (**Access -> SAML Setup**).</span></span>
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_000.png)

10. <span data-ttu-id="6fcec-180">確認這些 Url 符合您的設定對 hello**裝載 Graphite 網域和 Url** hello Azure 入口網站的區段。</span><span class="sxs-lookup"><span data-stu-id="6fcec-180">Confirm these URls match your configuration done on hello **Hosted Graphite Domain and URLs** section of hello Azure portal.</span></span>
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_001.png)

11. <span data-ttu-id="6fcec-182">在**實體或簽發者 ID**和**SSO 登入 URL**等文字方塊中，貼上的 hello 值**SAML 實體識別碼**和**SAML 單一登入服務 URL**您已複製從 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="6fcec-182">In  **Entity or Issuer ID** and **SSO Login URL** textboxes, paste hello value of **SAML Entity ID** and **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_002.png)
   

12. <span data-ttu-id="6fcec-184">選取 [唯讀] 做為 [預設使用者角色]。</span><span class="sxs-lookup"><span data-stu-id="6fcec-184">Select "**Read-only**" as **Default User Role**.</span></span>
    
    ![在應用程式端設定單一登入](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_004.png)

13. <span data-ttu-id="6fcec-186">從 Azure 入口網站中，複製到剪貼簿，其內容的 hello 下載 [記事本] 中開啟 base-64 編碼的憑證，然後將它貼入 toohello **X.509 憑證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="6fcec-186">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox.</span></span>
    
    ![在應用程式端設定單一登入](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_005.png)

14. <span data-ttu-id="6fcec-188">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="6fcec-188">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="6fcec-189">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="6fcec-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6fcec-190">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="6fcec-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6fcec-191">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6fcec-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6fcec-192">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="6fcec-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="6fcec-193">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="6fcec-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="6fcec-195">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="6fcec-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6fcec-196">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="6fcec-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6fcec-198">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="6fcec-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6fcec-200">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="6fcec-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6fcec-202">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="6fcec-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6fcec-204">a.</span><span class="sxs-lookup"><span data-stu-id="6fcec-204">a.</span></span> <span data-ttu-id="6fcec-205">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="6fcec-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6fcec-206">b.</span><span class="sxs-lookup"><span data-stu-id="6fcec-206">b.</span></span> <span data-ttu-id="6fcec-207">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="6fcec-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6fcec-208">c.</span><span class="sxs-lookup"><span data-stu-id="6fcec-208">c.</span></span> <span data-ttu-id="6fcec-209">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="6fcec-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6fcec-210">d.</span><span class="sxs-lookup"><span data-stu-id="6fcec-210">d.</span></span> <span data-ttu-id="6fcec-211">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="6fcec-211">Click **Create**.</span></span>
 
### <a name="creating-a-hosted-graphite-test-user"></a><span data-ttu-id="6fcec-212">建立 Hosted Graphite 測試使用者</span><span class="sxs-lookup"><span data-stu-id="6fcec-212">Creating a Hosted Graphite test user</span></span>

<span data-ttu-id="6fcec-213">hello 本節目標在於 toocreate 中裝載 Graphite 呼叫許 Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="6fcec-213">hello objective of this section is toocreate a user called Britta Simon in Hosted Graphite.</span></span> <span data-ttu-id="6fcec-214">Hosted Graphite 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="6fcec-214">Hosted Graphite supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="6fcec-215">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="6fcec-215">There is no action item for you in this section.</span></span> <span data-ttu-id="6fcec-216">如果尚未存在，將會嘗試 tooaccess Hosted Graphite 期間建立新使用者。</span><span class="sxs-lookup"><span data-stu-id="6fcec-216">A new user will be created during an attempt tooaccess Hosted Graphite if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="6fcec-217">若要手動 toocreate 使用者，您需要透過 toocontact hello 裝載 Graphite 支援小組< mailto:help@hostedgraphite.com >。</span><span class="sxs-lookup"><span data-stu-id="6fcec-217">If you need toocreate a user manually, you need toocontact hello Hosted Graphite support team via <mailto:help@hostedgraphite.com>.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6fcec-218">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="6fcec-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6fcec-219">在本節中，您可以授與存取 tooHosted Graphite 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6fcec-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHosted Graphite.</span></span>

![指派使用者][200] 

<span data-ttu-id="6fcec-221">**tooassign 許 Simon tooHosted Graphite，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="6fcec-221">**tooassign Britta Simon tooHosted Graphite, perform hello following steps:**</span></span>

1. <span data-ttu-id="6fcec-222">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="6fcec-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="6fcec-224">在 [hello] 應用程式清單中，選取**裝載 Graphite**。</span><span class="sxs-lookup"><span data-stu-id="6fcec-224">In hello applications list, select **Hosted Graphite**.</span></span>

    ![設定單一登入](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_app.png) 

3. <span data-ttu-id="6fcec-226">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="6fcec-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="6fcec-228">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6fcec-228">Click **Add** button.</span></span> <span data-ttu-id="6fcec-229">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="6fcec-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="6fcec-231">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="6fcec-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6fcec-232">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6fcec-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6fcec-233">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6fcec-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6fcec-234">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="6fcec-234">Testing single sign-on</span></span>

<span data-ttu-id="6fcec-235">hello 本節目標在於 tootest 您 Azure AD 的 SSO 組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="6fcec-235">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="6fcec-236">當您按一下 hello 裝載 Graphite 磚 hello 存取面板中的時，您應該取得自動登入 tooyour 裝載 Graphite 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6fcec-236">When you click hello Hosted Graphite tile in hello Access Panel, you should get automatically signed-on tooyour Hosted Graphite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6fcec-237">其他資源</span><span class="sxs-lookup"><span data-stu-id="6fcec-237">Additional resources</span></span>

* [<span data-ttu-id="6fcec-238">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6fcec-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6fcec-239">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="6fcec-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_203.png

