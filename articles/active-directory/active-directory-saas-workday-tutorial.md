---
title: "教學課程：Azure Active Directory 與 Workday 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Workday 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e9da692e-4a65-4231-8ab3-bc9a87b10bca
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: aaa41e372e45f464c4540a70fc79c98dbc06d6b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workday"></a><span data-ttu-id="2b35f-103">教學課程：Azure Active Directory 與 Workday 整合</span><span class="sxs-lookup"><span data-stu-id="2b35f-103">Tutorial: Azure Active Directory integration with Workday</span></span>

<span data-ttu-id="2b35f-104">在此教學課程中，您學會如何 toointegrate Workday 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="2b35f-104">In this tutorial, you learn how toointegrate Workday with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2b35f-105">新的 Workday 整合與 Azure AD 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="2b35f-105">Integrating Workday with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2b35f-106">您可以控制存取 tooWorkday Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="2b35f-106">You can control in Azure AD who has access tooWorkday</span></span>
- <span data-ttu-id="2b35f-107">您可以啟用您的使用者 tooautomatically get 登入 tooWorkday （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="2b35f-107">You can enable your users tooautomatically get signed-on tooWorkday (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2b35f-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="2b35f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2b35f-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="2b35f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b35f-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="2b35f-110">Prerequisites</span></span>

<span data-ttu-id="2b35f-111">tooconfigure Azure AD 與 Workday 的整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="2b35f-111">tooconfigure Azure AD integration with Workday, you need hello following items:</span></span>

- <span data-ttu-id="2b35f-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="2b35f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2b35f-113">已啟用 Workday 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="2b35f-113">A Workday single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2b35f-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="2b35f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2b35f-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="2b35f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2b35f-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="2b35f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2b35f-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="2b35f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2b35f-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="2b35f-118">Scenario description</span></span>
<span data-ttu-id="2b35f-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="2b35f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2b35f-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="2b35f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2b35f-121">加入新的 Workday 從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="2b35f-121">Adding Workday from hello gallery</span></span>
2. <span data-ttu-id="2b35f-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="2b35f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workday-from-hello-gallery"></a><span data-ttu-id="2b35f-123">加入新的 Workday 從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="2b35f-123">Adding Workday from hello gallery</span></span>
<span data-ttu-id="2b35f-124">tooconfigure hello 整合 Workday 到 Azure AD，您會需要 tooadd Workday hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2b35f-124">tooconfigure hello integration of Workday into Azure AD, you need tooadd Workday from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2b35f-125">**tooadd Workday 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="2b35f-125">**tooadd Workday from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b35f-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="2b35f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2b35f-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="2b35f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2b35f-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="2b35f-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="2b35f-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="2b35f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="2b35f-133">在 [hello] 搜尋方塊中，輸入**Workday**。</span><span class="sxs-lookup"><span data-stu-id="2b35f-133">In hello search box, type **Workday**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workday-tutorial/tutorial_workday_search.png)

5. <span data-ttu-id="2b35f-135">在 hello 結果 窗格中，選取  **Workday**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2b35f-135">In hello results panel, select **Workday**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workday-tutorial/tutorial_workday_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2b35f-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="2b35f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2b35f-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Workday 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="2b35f-138">In this section, you configure and test Azure AD single sign-on with Workday based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2b35f-139">單一登入 toowork，Azure AD 需要 tooknow Workday 中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="2b35f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workday is tooa user in Azure AD.</span></span> <span data-ttu-id="2b35f-140">換句話說，Azure AD 使用者與 Workday 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="2b35f-140">In other words, a link relationship between an Azure AD user and hello related user in Workday needs toobe established.</span></span>

<span data-ttu-id="2b35f-141">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** workday。</span><span class="sxs-lookup"><span data-stu-id="2b35f-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Workday.</span></span>

<span data-ttu-id="2b35f-142">tooconfigure 及 Azure AD 單一登入與 Workday 的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="2b35f-142">tooconfigure and test Azure AD single sign-on with Workday, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2b35f-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="2b35f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2b35f-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="2b35f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2b35f-145">**[建立新的 Workday 的測試使用者](#creating-a-workday-test-user)** -toohave 許 Simon workday 連結的 toohello Azure AD 使用者表示法的對應項目。</span><span class="sxs-lookup"><span data-stu-id="2b35f-145">**[Creating a Workday test user](#creating-a-workday-test-user)** - toohave a counterpart of Britta Simon in Workday that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2b35f-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="2b35f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2b35f-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="2b35f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2b35f-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="2b35f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2b35f-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Workday 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="2b35f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workday application.</span></span>

<span data-ttu-id="2b35f-150">**tooconfigure Azure AD 單一登入與 Workday，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="2b35f-150">**tooconfigure Azure AD single sign-on with Workday, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b35f-151">在 Azure 入口網站上 hello hello **Workday**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="2b35f-151">In hello Azure portal, on hello **Workday** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="2b35f-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="2b35f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-workday-tutorial/tutorial_workday_samlbase.png)

3. <span data-ttu-id="2b35f-155">在 hello **Workday 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="2b35f-155">On hello **Workday Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-workday-tutorial/tutorial_workday_url.png)

    <span data-ttu-id="2b35f-157">a.</span><span class="sxs-lookup"><span data-stu-id="2b35f-157">a.</span></span> <span data-ttu-id="2b35f-158">在 hello**登入 URL**文字方塊中，做為型別 hello 值：`https://impl.workday.com/<tenant>/login-saml2.htmld`</span><span class="sxs-lookup"><span data-stu-id="2b35f-158">In hello **Sign-on URL** textbox, type hello value as: `https://impl.workday.com/<tenant>/login-saml2.htmld`</span></span>

    <span data-ttu-id="2b35f-159">b.</span><span class="sxs-lookup"><span data-stu-id="2b35f-159">b.</span></span> <span data-ttu-id="2b35f-160">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://impl.workday.com/<tenant>/login-saml.htmld`</span><span class="sxs-lookup"><span data-stu-id="2b35f-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://impl.workday.com/<tenant>/login-saml.htmld`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2b35f-161">這些值不是真正的 hello。</span><span class="sxs-lookup"><span data-stu-id="2b35f-161">These values are not hello real.</span></span> <span data-ttu-id="2b35f-162">更新這些值與 hello 實際登入 URL 和回覆 URL。</span><span class="sxs-lookup"><span data-stu-id="2b35f-162">Update these values with hello actual Sign-on URL and Reply URL.</span></span> <span data-ttu-id="2b35f-163">您的回覆 URL 必須有子網域 (例如：www、wd2、wd3、wd3-impl、wd5、wd5-impl)。</span><span class="sxs-lookup"><span data-stu-id="2b35f-163">Your reply URL must have a subdomain for example: www, wd2, wd3, wd3-impl, wd5, wd5-impl).</span></span> <span data-ttu-id="2b35f-164">例如，使用 " *http://www.myworkday.com* " 有效，但 " *http://myworkday.com* " 則無效。</span><span class="sxs-lookup"><span data-stu-id="2b35f-164">Using something like "*http://www.myworkday.com*" works but "*http://myworkday.com*" does not.</span></span> <span data-ttu-id="2b35f-165">請連絡[Workday 用戶端支援小組](https://www.workday.com/en-us/partners-services/services/support.html)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="2b35f-165">Contact [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) tooget these values.</span></span> 
 

4. <span data-ttu-id="2b35f-166">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="2b35f-166">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-workday-tutorial/tutorial_workday_certificate.png) 

5. <span data-ttu-id="2b35f-168">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="2b35f-168">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-workday-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2b35f-170">在 hello **Workday 組態**區段中，按一下**設定 Workday** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="2b35f-170">On hello **Workday Configuration** section, click **Configure Workday** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2b35f-171">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="2b35f-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    <span data-ttu-id="2b35f-172">![設定單一登入](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="2b35f-172">![Configure Single Sign-On](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS></span></span>
7. <span data-ttu-id="2b35f-173">在不同的網頁瀏覽器視窗中，系統管理員身分登入 tooyour Workday 公司網站。</span><span class="sxs-lookup"><span data-stu-id="2b35f-173">In a different web browser window, log in tooyour Workday company site as an administrator.</span></span>

8. <span data-ttu-id="2b35f-174">跳過**功能表\>Workbench**。</span><span class="sxs-lookup"><span data-stu-id="2b35f-174">Go too**Menu \> Workbench**.</span></span>
   
    <span data-ttu-id="2b35f-175">![Workbench](./media/active-directory-saas-workday-tutorial/IC782923.png "Workbench")</span><span class="sxs-lookup"><span data-stu-id="2b35f-175">![Workbench](./media/active-directory-saas-workday-tutorial/IC782923.png "Workbench")</span></span>

9. <span data-ttu-id="2b35f-176">跳過**帳戶管理**。</span><span class="sxs-lookup"><span data-stu-id="2b35f-176">Go too**Account Administration**.</span></span>
   
    <span data-ttu-id="2b35f-177">![帳戶管理](./media/active-directory-saas-workday-tutorial/IC782924.png "帳戶管理")</span><span class="sxs-lookup"><span data-stu-id="2b35f-177">![Account Administration](./media/active-directory-saas-workday-tutorial/IC782924.png "Account Administration")</span></span>

10. <span data-ttu-id="2b35f-178">跳過**編輯租用戶設定-安全性**。</span><span class="sxs-lookup"><span data-stu-id="2b35f-178">Go too**Edit Tenant Setup – Security**.</span></span>
   
    <span data-ttu-id="2b35f-179">![編輯租用戶安全性](./media/active-directory-saas-workday-tutorial/IC782925.png "編輯租用戶安全性")</span><span class="sxs-lookup"><span data-stu-id="2b35f-179">![Edit Tenant Security](./media/active-directory-saas-workday-tutorial/IC782925.png "Edit Tenant Security")</span></span>

11. <span data-ttu-id="2b35f-180">在 hello**重新導向 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="2b35f-180">In hello **Redirection URLs** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="2b35f-181">![重新導向 URL](./media/active-directory-saas-workday-tutorial/IC7829581.png "重新導向 URL")</span><span class="sxs-lookup"><span data-stu-id="2b35f-181">![Redirection URLs](./media/active-directory-saas-workday-tutorial/IC7829581.png "Redirection URLs")</span></span>
   
    <span data-ttu-id="2b35f-182">a.</span><span class="sxs-lookup"><span data-stu-id="2b35f-182">a.</span></span> <span data-ttu-id="2b35f-183">按一下 [加入資料列]。</span><span class="sxs-lookup"><span data-stu-id="2b35f-183">Click **Add Row**.</span></span>
   
    <span data-ttu-id="2b35f-184">b.</span><span class="sxs-lookup"><span data-stu-id="2b35f-184">b.</span></span> <span data-ttu-id="2b35f-185">在 hello**登入重新導向 URL**文字方塊和 hello**行動重新導向 URL**文字方塊中，型別 hello**登入 URL**您所輸入的 hello **Workday 網域和Url** hello Azure 入口網站的區段。</span><span class="sxs-lookup"><span data-stu-id="2b35f-185">In hello **Login Redirect URL** textbox and hello **Mobile Redirect URL** textbox, type hello **Sign-on URL** you have entered on hello **Workday Domain and URLs** section of hello Azure portal.</span></span>
   
    <span data-ttu-id="2b35f-186">c.</span><span class="sxs-lookup"><span data-stu-id="2b35f-186">c.</span></span> <span data-ttu-id="2b35f-187">Hello hello 上的 Azure 入口網站中**設定登入**視窗中，複製 hello**登出 URL**，然後將它貼入 hello**登出重新導向 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="2b35f-187">In hello Azure portal, on hello **Configure sign-on** window, copy hello **Sign-Out URL**, and then paste it into hello **Logout Redirect URL** textbox.</span></span>
   
    <span data-ttu-id="2b35f-188">d.</span><span class="sxs-lookup"><span data-stu-id="2b35f-188">d.</span></span>  <span data-ttu-id="2b35f-189">在**環境**文字方塊中，型別 hello 環境名稱。</span><span class="sxs-lookup"><span data-stu-id="2b35f-189">In **Environment** textbox, type hello environment name.</span></span>  

    >[!NOTE]
    > <span data-ttu-id="2b35f-190">hello hello 環境屬性的值會繫結 toohello hello 租用戶 URL 值：</span><span class="sxs-lookup"><span data-stu-id="2b35f-190">hello value of hello Environment attribute is tied toohello value of hello tenant URL:</span></span>  
    ><span data-ttu-id="2b35f-191">-如果 hello hello Workday 租用戶 URL 的網域名稱開頭為 impl，例如： *https://impl.workday.com/\<租用戶\>/login-saml2.htmld*)，hello**環境**屬性必須設定 tooImplementation。</span><span class="sxs-lookup"><span data-stu-id="2b35f-191">-If hello domain name of hello Workday tenant URL starts with impl for example: *https://impl.workday.com/\<tenant\>/login-saml2.htmld*), hello **Environment** attribute must be set tooImplementation.</span></span>  
    ><span data-ttu-id="2b35f-192">-如果 hello 網域名稱的其他項目，您需要 toocontact [Workday 用戶端支援小組](https://www.workday.com/en-us/partners-services/services/support.html)tooget hello 符合**環境**值。</span><span class="sxs-lookup"><span data-stu-id="2b35f-192">-If hello domain name starts with something else, you need toocontact [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) tooget hello matching **Environment** value.</span></span>

12. <span data-ttu-id="2b35f-193">在 hello **SAML 設定**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="2b35f-193">In hello **SAML Setup** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="2b35f-194">![SAML 設定](./media/active-directory-saas-workday-tutorial/IC782926.png "SAML 設定")</span><span class="sxs-lookup"><span data-stu-id="2b35f-194">![SAML Setup](./media/active-directory-saas-workday-tutorial/IC782926.png "SAML Setup")</span></span>
   
    <span data-ttu-id="2b35f-195">a.</span><span class="sxs-lookup"><span data-stu-id="2b35f-195">a.</span></span>  <span data-ttu-id="2b35f-196">按一下 [啟用 SAML 驗證] 。</span><span class="sxs-lookup"><span data-stu-id="2b35f-196">Select **Enable SAML Authentication**.</span></span>
   
    <span data-ttu-id="2b35f-197">b.</span><span class="sxs-lookup"><span data-stu-id="2b35f-197">b.</span></span>  <span data-ttu-id="2b35f-198">按一下 [加入資料列]。</span><span class="sxs-lookup"><span data-stu-id="2b35f-198">Click **Add Row**.</span></span>

13. <span data-ttu-id="2b35f-199">在 hello SAML 身分識別提供者 > 一節中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="2b35f-199">In hello SAML Identity Providers section, perform hello following steps:</span></span>
   
    <span data-ttu-id="2b35f-200">![SAML 身分識別提供者](./media/active-directory-saas-workday-tutorial/IC7829271.png "SAML 身分識別提供者")</span><span class="sxs-lookup"><span data-stu-id="2b35f-200">![SAML Identity Providers](./media/active-directory-saas-workday-tutorial/IC7829271.png "SAML Identity Providers")</span></span>
   
    <span data-ttu-id="2b35f-201">a.</span><span class="sxs-lookup"><span data-stu-id="2b35f-201">a.</span></span> <span data-ttu-id="2b35f-202">在 [hello 身分識別提供者名稱] 文字方塊中，輸入提供者名稱 (例如： *SPInitiatedSSO*)。</span><span class="sxs-lookup"><span data-stu-id="2b35f-202">In hello Identity Provider Name textbox, type a provider name (for example: *SPInitiatedSSO*).</span></span>
   
    <span data-ttu-id="2b35f-203">b.</span><span class="sxs-lookup"><span data-stu-id="2b35f-203">b.</span></span> <span data-ttu-id="2b35f-204">在 Azure 入口網站上 hello hello**設定登入**視窗中，複製 hello **SAML 實體識別碼**值並貼到 hello**簽發者**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="2b35f-204">In hello Azure portal, on hello **Configure sign-on** window, copy hello **SAML Entity ID** value, and then paste it into hello **Issuer** textbox.</span></span>
   
    <span data-ttu-id="2b35f-205">c.</span><span class="sxs-lookup"><span data-stu-id="2b35f-205">c.</span></span> <span data-ttu-id="2b35f-206">選取 [啟用 Workday 啟始的登出]。</span><span class="sxs-lookup"><span data-stu-id="2b35f-206">Select **Enable Workday Initiated Logout**.</span></span>
   
    <span data-ttu-id="2b35f-207">d.</span><span class="sxs-lookup"><span data-stu-id="2b35f-207">d.</span></span> <span data-ttu-id="2b35f-208">Hello hello 上的 Azure 入口網站中**設定登入**視窗中，複製 hello**登出 URL**值並貼到 hello**登出要求 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="2b35f-208">In hello Azure portal, on hello **Configure sign-on** window, copy hello **Sign-Out URL** value, and then paste it into hello **Logout Request URL** textbox.</span></span>

    <span data-ttu-id="2b35f-209">e.</span><span class="sxs-lookup"><span data-stu-id="2b35f-209">e.</span></span> <span data-ttu-id="2b35f-210">按一下 識別提供者公開金鑰憑證，然後按一下建立。</span><span class="sxs-lookup"><span data-stu-id="2b35f-210">Click **Identity Provider Public Key Certificate**, and then click **Create**.</span></span> 

    <span data-ttu-id="2b35f-211">![建立](./media/active-directory-saas-workday-tutorial/IC782928.png "建立")</span><span class="sxs-lookup"><span data-stu-id="2b35f-211">![Create](./media/active-directory-saas-workday-tutorial/IC782928.png "Create")</span></span>

    <span data-ttu-id="2b35f-212">f.</span><span class="sxs-lookup"><span data-stu-id="2b35f-212">f.</span></span> <span data-ttu-id="2b35f-213">按一下 [建立 x509 公開金鑰]。</span><span class="sxs-lookup"><span data-stu-id="2b35f-213">Click **Create x509 Public Key**.</span></span> 

    <span data-ttu-id="2b35f-214">![建立](./media/active-directory-saas-workday-tutorial/IC782929.png "建立")</span><span class="sxs-lookup"><span data-stu-id="2b35f-214">![Create](./media/active-directory-saas-workday-tutorial/IC782929.png "Create")</span></span>


14. <span data-ttu-id="2b35f-215">在 hello**檢視 x509 公開金鑰**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="2b35f-215">In hello **View x509 Public Key** section, perform hello following steps:</span></span> 
   
    <span data-ttu-id="2b35f-216">![檢視 x509 公開金鑰](./media/active-directory-saas-workday-tutorial/IC782930.png "檢視 x509 公開金鑰")</span><span class="sxs-lookup"><span data-stu-id="2b35f-216">![View x509 Public Key](./media/active-directory-saas-workday-tutorial/IC782930.png "View x509 Public Key")</span></span> 
   
    <span data-ttu-id="2b35f-217">a.</span><span class="sxs-lookup"><span data-stu-id="2b35f-217">a.</span></span> <span data-ttu-id="2b35f-218">在 hello**名稱**文字方塊中，輸入您的憑證名稱 (例如： *PPE\_SP*)。</span><span class="sxs-lookup"><span data-stu-id="2b35f-218">In hello **Name** textbox, type a name for your certificate (for example: *PPE\_SP*).</span></span>
   
    <span data-ttu-id="2b35f-219">b.</span><span class="sxs-lookup"><span data-stu-id="2b35f-219">b.</span></span> <span data-ttu-id="2b35f-220">在 hello**有效期自**文字方塊中，型別 hello 有效自 」 屬性值，您的憑證。</span><span class="sxs-lookup"><span data-stu-id="2b35f-220">In hello **Valid From** textbox, type hello valid from attribute value of your certificate.</span></span>
   
    <span data-ttu-id="2b35f-221">c.</span><span class="sxs-lookup"><span data-stu-id="2b35f-221">c.</span></span>  <span data-ttu-id="2b35f-222">在 hello**有效期到**文字方塊中，您的憑證類型 hello 有效 tooattribute 值。</span><span class="sxs-lookup"><span data-stu-id="2b35f-222">In hello **Valid To** textbox, type hello valid tooattribute value of your certificate.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="2b35f-223">取得 hello 有效開始日期，並按兩下 hello 有效 toodate 從 hello 下載的憑證。</span><span class="sxs-lookup"><span data-stu-id="2b35f-223">You can get hello valid from date and hello valid toodate from hello downloaded certificate by double-clicking it.</span></span>  <span data-ttu-id="2b35f-224">hello 日期會列於下 hello**詳細資料** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="2b35f-224">hello dates are listed under hello **Details** tab.</span></span>
    > 
    >
   
    <span data-ttu-id="2b35f-225">d.</span><span class="sxs-lookup"><span data-stu-id="2b35f-225">d.</span></span>  <span data-ttu-id="2b35f-226">在 [記事本]，然後再複製 hello 它的內容中開啟您的 base-64 編碼的憑證。</span><span class="sxs-lookup"><span data-stu-id="2b35f-226">Open your base-64 encoded certificate in notepad, and then copy hello content of it.</span></span>
   
    <span data-ttu-id="2b35f-227">e.</span><span class="sxs-lookup"><span data-stu-id="2b35f-227">e.</span></span>  <span data-ttu-id="2b35f-228">在 hello**憑證**文字方塊中，貼上剪貼簿 hello 內容。</span><span class="sxs-lookup"><span data-stu-id="2b35f-228">In hello **Certificate** textbox, paste hello content of your clipboard.</span></span>
   
    <span data-ttu-id="2b35f-229">f.</span><span class="sxs-lookup"><span data-stu-id="2b35f-229">f.</span></span>  <span data-ttu-id="2b35f-230">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="2b35f-230">Click **OK**.</span></span>

15. <span data-ttu-id="2b35f-231">執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="2b35f-231">Perform hello following steps:</span></span> 
   
    <span data-ttu-id="2b35f-232">![SSO 組態](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "SSO 組態")</span><span class="sxs-lookup"><span data-stu-id="2b35f-232">![SSO configuration](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "SSO configuration")</span></span>
   
    <span data-ttu-id="2b35f-233">a.</span><span class="sxs-lookup"><span data-stu-id="2b35f-233">a.</span></span>  <span data-ttu-id="2b35f-234">啟用 hello **x509 私密金鑰組**。</span><span class="sxs-lookup"><span data-stu-id="2b35f-234">Enable hello **x509 Private Key Pair**.</span></span>
   
    <span data-ttu-id="2b35f-235">b.</span><span class="sxs-lookup"><span data-stu-id="2b35f-235">b.</span></span>  <span data-ttu-id="2b35f-236">在 hello**服務提供者識別碼**文字方塊中，輸入**http://www.workday.com**。</span><span class="sxs-lookup"><span data-stu-id="2b35f-236">In hello **Service Provider ID** textbox, type **http://www.workday.com**.</span></span>
   
    <span data-ttu-id="2b35f-237">c.</span><span class="sxs-lookup"><span data-stu-id="2b35f-237">c.</span></span>  <span data-ttu-id="2b35f-238">選取 [啟用 SP 啟始的 SAML 驗證]。</span><span class="sxs-lookup"><span data-stu-id="2b35f-238">Select **Enable SP Initiated SAML Authentication**.</span></span>
   
    <span data-ttu-id="2b35f-239">d.</span><span class="sxs-lookup"><span data-stu-id="2b35f-239">d.</span></span>  <span data-ttu-id="2b35f-240">在 Azure 入口網站上 hello hello**設定登入**視窗中，複製 hello **SAML 單一登入服務 URL**值並貼到 hello **IdP SSO 服務 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="2b35f-240">In hello Azure portal, on hello **Configure sign-on** window, copy hello **SAML Single Sign-On Service URL** value, and then paste it into hello **IdP SSO Service URL** textbox.</span></span>
   
    <span data-ttu-id="2b35f-241">e.</span><span class="sxs-lookup"><span data-stu-id="2b35f-241">e.</span></span> <span data-ttu-id="2b35f-242">選取 [不要壓縮 SP 起始的驗證要求]。</span><span class="sxs-lookup"><span data-stu-id="2b35f-242">Select **Do Not Deflate SP-initiated Authentication Request**.</span></span>
   
    <span data-ttu-id="2b35f-243">f.</span><span class="sxs-lookup"><span data-stu-id="2b35f-243">f.</span></span> <span data-ttu-id="2b35f-244">選取 **SHA256** 做為 [驗證要求簽章方法]。</span><span class="sxs-lookup"><span data-stu-id="2b35f-244">As **Authentication Request Signature Method**, select **SHA256**.</span></span> 
   
    <span data-ttu-id="2b35f-245">![驗證要求簽章方法](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "驗證要求簽章方法")</span><span class="sxs-lookup"><span data-stu-id="2b35f-245">![Authentication Request Signature Method](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "Authentication Request Signature Method")</span></span> 
   
    <span data-ttu-id="2b35f-246">g.</span><span class="sxs-lookup"><span data-stu-id="2b35f-246">g.</span></span> <span data-ttu-id="2b35f-247">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="2b35f-247">Click **OK**.</span></span> 
   
    <span data-ttu-id="2b35f-248">![確定](./media/active-directory-saas-workday-tutorial/IC782933.png "確定")
<CE></span><span class="sxs-lookup"><span data-stu-id="2b35f-248">![OK](./media/active-directory-saas-workday-tutorial/IC782933.png "OK")
<CE></span></span>

> [!TIP]
> <span data-ttu-id="2b35f-249">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="2b35f-249">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2b35f-250">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="2b35f-250">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2b35f-251">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2b35f-251">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2b35f-252">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="2b35f-252">Creating an Azure AD test user</span></span>
<span data-ttu-id="2b35f-253">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="2b35f-253">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="2b35f-255">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="2b35f-255">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b35f-256">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="2b35f-256">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workday-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2b35f-258">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="2b35f-258">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workday-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2b35f-260">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="2b35f-260">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workday-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2b35f-262">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="2b35f-262">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workday-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2b35f-264">a.</span><span class="sxs-lookup"><span data-stu-id="2b35f-264">a.</span></span> <span data-ttu-id="2b35f-265">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="2b35f-265">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2b35f-266">b.</span><span class="sxs-lookup"><span data-stu-id="2b35f-266">b.</span></span> <span data-ttu-id="2b35f-267">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="2b35f-267">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2b35f-268">c.</span><span class="sxs-lookup"><span data-stu-id="2b35f-268">c.</span></span> <span data-ttu-id="2b35f-269">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="2b35f-269">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2b35f-270">d.</span><span class="sxs-lookup"><span data-stu-id="2b35f-270">d.</span></span> <span data-ttu-id="2b35f-271">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="2b35f-271">Click **Create**.</span></span>
 
### <a name="creating-a-workday-test-user"></a><span data-ttu-id="2b35f-272">建立 Workday 測試使用者</span><span class="sxs-lookup"><span data-stu-id="2b35f-272">Creating a Workday test user</span></span>

<span data-ttu-id="2b35f-273">tooget 佈建至 Workday 的測試使用者，您需要 toocontact hello [Workday 用戶端支援小組](https://www.workday.com/en-us/partners-services/services/support.html)。</span><span class="sxs-lookup"><span data-stu-id="2b35f-273">tooget a test user provisioned into Workday, you need toocontact hello [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html).</span></span>
<span data-ttu-id="2b35f-274">hello [Workday 用戶端支援小組](https://www.workday.com/en-us/partners-services/services/support.html)會為您建立 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="2b35f-274">hello [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) creates hello user for you.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2b35f-275">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="2b35f-275">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2b35f-276">在本節中，您可以授與存取 tooWorkday 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="2b35f-276">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkday.</span></span>

![指派使用者][200] 

<span data-ttu-id="2b35f-278">**tooassign 許 Simon tooWorkday，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="2b35f-278">**tooassign Britta Simon tooWorkday, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b35f-279">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="2b35f-279">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="2b35f-281">在 [hello] 應用程式清單中，選取**Workday**。</span><span class="sxs-lookup"><span data-stu-id="2b35f-281">In hello applications list, select **Workday**.</span></span>

    ![設定單一登入](./media/active-directory-saas-workday-tutorial/tutorial_workday_app.png) 

3. <span data-ttu-id="2b35f-283">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="2b35f-283">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="2b35f-285">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2b35f-285">Click **Add** button.</span></span> <span data-ttu-id="2b35f-286">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="2b35f-286">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="2b35f-288">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="2b35f-288">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2b35f-289">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2b35f-289">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2b35f-290">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2b35f-290">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2b35f-291">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="2b35f-291">Testing single sign-on</span></span>

<span data-ttu-id="2b35f-292">如果您想 tootest 您的單一登入設定，請開啟 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="2b35f-292">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="2b35f-293">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="2b35f-293">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2b35f-294">其他資源</span><span class="sxs-lookup"><span data-stu-id="2b35f-294">Additional resources</span></span>

* [<span data-ttu-id="2b35f-295">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2b35f-295">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2b35f-296">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="2b35f-296">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="2b35f-297">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="2b35f-297">Configure User Provisioning</span></span>](active-directory-saas-workday-inbound-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workday-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workday-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workday-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workday-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workday-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workday-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workday-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workday-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workday-tutorial/tutorial_general_203.png

