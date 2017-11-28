---
title: "教學課程：Azure Active Directory 與 Jitbit Helpdesk 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Jitbit Helpdesk 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 15ce27d4-0621-4103-8a34-e72c98d72ec3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 0f6c837bbb910c1e84f7ed9da676c5ab40f75338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jitbit-helpdesk"></a><span data-ttu-id="45dae-103">教學課程：Azure Active Directory 與 Jitbit Helpdesk 整合</span><span class="sxs-lookup"><span data-stu-id="45dae-103">Tutorial: Azure Active Directory integration with Jitbit Helpdesk</span></span>

<span data-ttu-id="45dae-104">在此教學課程中，您學會如何 toointegrate Jitbit Helpdesk 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="45dae-104">In this tutorial, you learn how toointegrate Jitbit Helpdesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="45dae-105">整合 Azure AD 與 Jitbit Helpdesk 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="45dae-105">Integrating Jitbit Helpdesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="45dae-106">您可以控制存取 tooJitbit 技術服務人員的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="45dae-106">You can control in Azure AD who has access tooJitbit Helpdesk</span></span>
- <span data-ttu-id="45dae-107">您可以啟用您的使用者 tooautomatically get 登入 tooJitbit （單一登入） 的技術服務人員使用他們的 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="45dae-107">You can enable your users tooautomatically get signed-on tooJitbit Helpdesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="45dae-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="45dae-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="45dae-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="45dae-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="45dae-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="45dae-110">Prerequisites</span></span>

<span data-ttu-id="45dae-111">tooconfigure Azure AD 與 Jitbit Helpdesk 的整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="45dae-111">tooconfigure Azure AD integration with Jitbit Helpdesk, you need hello following items:</span></span>

- <span data-ttu-id="45dae-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="45dae-112">An Azure AD subscription</span></span>
- <span data-ttu-id="45dae-113">已啟用 Jitbit Helpdesk 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="45dae-113">A Jitbit Helpdesk single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="45dae-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="45dae-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="45dae-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="45dae-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="45dae-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="45dae-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="45dae-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="45dae-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="45dae-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="45dae-118">Scenario description</span></span>
<span data-ttu-id="45dae-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="45dae-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="45dae-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="45dae-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="45dae-121">從 hello 圖庫加入 Jitbit Helpdesk</span><span class="sxs-lookup"><span data-stu-id="45dae-121">Adding Jitbit Helpdesk from hello gallery</span></span>
2. <span data-ttu-id="45dae-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="45dae-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jitbit-helpdesk-from-hello-gallery"></a><span data-ttu-id="45dae-123">從 hello 圖庫加入 Jitbit Helpdesk</span><span class="sxs-lookup"><span data-stu-id="45dae-123">Adding Jitbit Helpdesk from hello gallery</span></span>
<span data-ttu-id="45dae-124">tooconfigure hello 整合 Jitbit Helpdesk 的 Azure AD，您需要 tooadd Jitbit Helpdesk hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="45dae-124">tooconfigure hello integration of Jitbit Helpdesk into Azure AD, you need tooadd Jitbit Helpdesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="45dae-125">**tooadd Jitbit Helpdesk 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="45dae-125">**tooadd Jitbit Helpdesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="45dae-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="45dae-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="45dae-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="45dae-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="45dae-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="45dae-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="45dae-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="45dae-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="45dae-133">在 [hello] 搜尋方塊中，輸入**Jitbit Helpdesk**。</span><span class="sxs-lookup"><span data-stu-id="45dae-133">In hello search box, type **Jitbit Helpdesk**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_search.png)

5. <span data-ttu-id="45dae-135">在 hello 結果 窗格中，選取  **Jitbit Helpdesk**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="45dae-135">In hello results panel, select **Jitbit Helpdesk**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="45dae-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="45dae-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="45dae-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Jitbit Helpdesk 設定和測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="45dae-138">In this section, you configure and test Azure AD single sign-on with Jitbit Helpdesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="45dae-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 Jitbit Helpdesk 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="45dae-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Jitbit Helpdesk is tooa user in Azure AD.</span></span> <span data-ttu-id="45dae-140">換句話說，Azure AD 使用者與 Jitbit Helpdesk 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="45dae-140">In other words, a link relationship between an Azure AD user and hello related user in Jitbit Helpdesk needs toobe established.</span></span>

<span data-ttu-id="45dae-141">在 Jitbit Helpdesk 中，將指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="45dae-141">In Jitbit Helpdesk, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="45dae-142">tooconfigure 和測試 Azure AD 單一登入與 Jitbit Helpdesk，您需要遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="45dae-142">tooconfigure and test Azure AD single sign-on with Jitbit Helpdesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="45dae-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="45dae-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="45dae-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="45dae-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="45dae-145">**[建立測試使用者 Jitbit Helpdesk](#creating-a-jitbit-helpdesk-test-user)**  -toohave 許 Simon Jitbit Helpdesk 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="45dae-145">**[Creating a Jitbit Helpdesk test user](#creating-a-jitbit-helpdesk-test-user)** - toohave a counterpart of Britta Simon in Jitbit Helpdesk that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="45dae-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="45dae-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="45dae-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="45dae-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="45dae-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="45dae-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="45dae-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Jitbit Helpdesk 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="45dae-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Jitbit Helpdesk application.</span></span>

<span data-ttu-id="45dae-150">**tooconfigure Azure AD 單一登入與 Jitbit Helpdesk，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="45dae-150">**tooconfigure Azure AD single sign-on with Jitbit Helpdesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="45dae-151">在 Azure 入口網站上 hello hello **Jitbit Helpdesk**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="45dae-151">In hello Azure portal, on hello **Jitbit Helpdesk** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="45dae-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="45dae-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_samlbase.png)

3. <span data-ttu-id="45dae-155">在 hello **Jitbit Helpdesk 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="45dae-155">On hello **Jitbit Helpdesk Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_url.png)

    <span data-ttu-id="45dae-157">a.</span><span class="sxs-lookup"><span data-stu-id="45dae-157">a.</span></span> <span data-ttu-id="45dae-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:</span><span class="sxs-lookup"><span data-stu-id="45dae-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span> 
    | |     
    | ----------------------------------------|
    | `https://<hostname>/helpdesk/User/Login`|
    | `https://<tenant-name>.Jitbit.com`|
    | |
    
    > [!NOTE] 
    > <span data-ttu-id="45dae-159">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="45dae-159">This value is not real.</span></span> <span data-ttu-id="45dae-160">更新此值以 hello 實際的登入 URL。</span><span class="sxs-lookup"><span data-stu-id="45dae-160">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="45dae-161">請連絡[Jitbit Helpdesk 用戶端支援小組](https://www.jitbit.com/support/)tooget 此值。</span><span class="sxs-lookup"><span data-stu-id="45dae-161">Contact [Jitbit Helpdesk Client support team](https://www.jitbit.com/support/) tooget this value.</span></span> 
    
    <span data-ttu-id="45dae-162">b.</span><span class="sxs-lookup"><span data-stu-id="45dae-162">b.</span></span>  <span data-ttu-id="45dae-163">在 hello**識別碼**文字方塊中，輸入 URL，如下所示：`https://www.jitbit.com/web-helpdesk/`</span><span class="sxs-lookup"><span data-stu-id="45dae-163">In hello **Identifier** textbox, type a URL as following: `https://www.jitbit.com/web-helpdesk/`</span></span>

    
 


4. <span data-ttu-id="45dae-164">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="45dae-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_certificate.png) 

5. <span data-ttu-id="45dae-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="45dae-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="45dae-168">在 hello **Jitbit Helpdesk 設定**區段中，按一下**設定 Jitbit Helpdesk** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="45dae-168">On hello **Jitbit Helpdesk Configuration** section, click **Configure Jitbit Helpdesk** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="45dae-169">複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="45dae-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_configure.png) 

7. <span data-ttu-id="45dae-171">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 Jitbit Helpdesk 公司網站。</span><span class="sxs-lookup"><span data-stu-id="45dae-171">In a different web browser window, log into your Jitbit Helpdesk company site as an administrator.</span></span>

8. <span data-ttu-id="45dae-172">在 hello hello 上方的工具列中按一下**管理**。</span><span class="sxs-lookup"><span data-stu-id="45dae-172">In hello toolbar on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="45dae-173">![管理](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "管理")</span><span class="sxs-lookup"><span data-stu-id="45dae-173">![Administration](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administration")</span></span>

9. <span data-ttu-id="45dae-174">按一下 [一般設定] 。</span><span class="sxs-lookup"><span data-stu-id="45dae-174">Click **General settings**.</span></span>
   
    <span data-ttu-id="45dae-175">![使用者、公司和權限](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "使用者、公司和權限")</span><span class="sxs-lookup"><span data-stu-id="45dae-175">![Users, companies, and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "Users, companies, and permissions")</span></span>

10. <span data-ttu-id="45dae-176">在 hello**驗證設定**組態區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="45dae-176">In hello **Authentication settings** configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="45dae-177">![驗證設定](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "驗證設定")</span><span class="sxs-lookup"><span data-stu-id="45dae-177">![Authentication settings](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "Authentication settings")</span></span>
    
    <span data-ttu-id="45dae-178">a.</span><span class="sxs-lookup"><span data-stu-id="45dae-178">a.</span></span> <span data-ttu-id="45dae-179">選取**啟用 SAML 2.0 單一登入**，在使用單一登入 (SSO)，toosign **OneLogin**。</span><span class="sxs-lookup"><span data-stu-id="45dae-179">Select **Enable SAML 2.0 single sign on**, toosign in using Single Sign-On (SSO), with **OneLogin**.</span></span>

    <span data-ttu-id="45dae-180">b.</span><span class="sxs-lookup"><span data-stu-id="45dae-180">b.</span></span> <span data-ttu-id="45dae-181">在 hello**端點 URL**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="45dae-181">In hello **EndPoint URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="45dae-182">c.</span><span class="sxs-lookup"><span data-stu-id="45dae-182">c.</span></span> <span data-ttu-id="45dae-183">開啟您**base-64**編碼在記事本中，複製到剪貼簿，其內容的 hello 的憑證，然後將它貼入 toohello **X.509 憑證**文字方塊</span><span class="sxs-lookup"><span data-stu-id="45dae-183">Open your **base-64** encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox</span></span>

    <span data-ttu-id="45dae-184">d.</span><span class="sxs-lookup"><span data-stu-id="45dae-184">d.</span></span> <span data-ttu-id="45dae-185">按一下 [儲存變更] 。</span><span class="sxs-lookup"><span data-stu-id="45dae-185">Click **Save changes**.</span></span>

> [!TIP]
> <span data-ttu-id="45dae-186">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="45dae-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="45dae-187">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="45dae-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="45dae-188">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="45dae-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="45dae-189">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="45dae-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="45dae-190">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="45dae-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="45dae-192">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="45dae-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="45dae-193">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="45dae-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="45dae-195">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="45dae-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="45dae-197">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="45dae-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="45dae-199">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="45dae-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="45dae-201">a.</span><span class="sxs-lookup"><span data-stu-id="45dae-201">a.</span></span> <span data-ttu-id="45dae-202">在 hello**名稱**文字方塊中，型別名稱做為**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="45dae-202">In hello **Name** textbox, type name as **BrittaSimon**.</span></span>

    <span data-ttu-id="45dae-203">b.</span><span class="sxs-lookup"><span data-stu-id="45dae-203">b.</span></span> <span data-ttu-id="45dae-204">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="45dae-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="45dae-205">c.</span><span class="sxs-lookup"><span data-stu-id="45dae-205">c.</span></span> <span data-ttu-id="45dae-206">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="45dae-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="45dae-207">d.</span><span class="sxs-lookup"><span data-stu-id="45dae-207">d.</span></span> <span data-ttu-id="45dae-208">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="45dae-208">Click **Create**.</span></span>
 
### <a name="creating-a-jitbit-helpdesk-test-user"></a><span data-ttu-id="45dae-209">建立 Jitbit Helpdesk 測試使用者</span><span class="sxs-lookup"><span data-stu-id="45dae-209">Creating a Jitbit Helpdesk test user</span></span>

<span data-ttu-id="45dae-210">在訂單 tooenable Azure AD 使用者 toolog 到 Jitbit Helpdesk，它們必須佈建到 Jitbit Helpdesk。</span><span class="sxs-lookup"><span data-stu-id="45dae-210">In order tooenable Azure AD users toolog into Jitbit Helpdesk, they must be provisioned into Jitbit Helpdesk.</span></span>  <span data-ttu-id="45dae-211">在 Jitbit Helpdesk 的 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="45dae-211">In hello case of Jitbit Helpdesk, provisioning is a manual task.</span></span>

<span data-ttu-id="45dae-212">**tooprovision 使用者帳戶，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="45dae-212">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="45dae-213">登入 tooyour **Jitbit Helpdesk**租用戶。</span><span class="sxs-lookup"><span data-stu-id="45dae-213">Log in tooyour **Jitbit Helpdesk** tenant.</span></span>

2. <span data-ttu-id="45dae-214">在 hello 最上層顯示 hello 功能表上，按一下**管理**。</span><span class="sxs-lookup"><span data-stu-id="45dae-214">In hello menu on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="45dae-215">![管理](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "管理")</span><span class="sxs-lookup"><span data-stu-id="45dae-215">![Administration](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administration")</span></span>

3. <span data-ttu-id="45dae-216">按一下 [使用者、公司和權限] 。</span><span class="sxs-lookup"><span data-stu-id="45dae-216">Click **Users, companies and permissions**.</span></span>
   
    <span data-ttu-id="45dae-217">![使用者、公司和權限](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "使用者、公司和權限")</span><span class="sxs-lookup"><span data-stu-id="45dae-217">![Users, companies, and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "Users, companies, and permissions")</span></span>

4. <span data-ttu-id="45dae-218">按一下 [新增使用者] 。</span><span class="sxs-lookup"><span data-stu-id="45dae-218">Click **Add user**.</span></span>
   
    <span data-ttu-id="45dae-219">![新增使用者](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="45dae-219">![Add user](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "Add user")</span></span>
   
5. <span data-ttu-id="45dae-220">在 hello 建立 > 一節中，輸入您想 tooprovision，如下所示的 hello Azure AD 帳戶的 hello 資料：</span><span class="sxs-lookup"><span data-stu-id="45dae-220">In hello Create section, type hello data of hello Azure AD account you want tooprovision as follows:</span></span>

    <span data-ttu-id="45dae-221">![建立](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "建立")</span><span class="sxs-lookup"><span data-stu-id="45dae-221">![Create](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "Create")</span></span>
   
   <span data-ttu-id="45dae-222">a.</span><span class="sxs-lookup"><span data-stu-id="45dae-222">a.</span></span> <span data-ttu-id="45dae-223">在 hello **Username**文字方塊中，輸入**BrittaSimon**，hello 與 hello Azure 入口網站的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="45dae-223">In hello **Username** textbox, type **BrittaSimon**, hello user name as in hello Azure portal.</span></span>

   <span data-ttu-id="45dae-224">b.</span><span class="sxs-lookup"><span data-stu-id="45dae-224">b.</span></span> <span data-ttu-id="45dae-225">在 hello**電子郵件**文字方塊中，類型的電子郵件的 hello 使用者喜歡 **BrittaSimon@contoso.com** 。</span><span class="sxs-lookup"><span data-stu-id="45dae-225">In hello **Email** textbox, type email of hello user like **BrittaSimon@contoso.com**.</span></span>

   <span data-ttu-id="45dae-226">c.</span><span class="sxs-lookup"><span data-stu-id="45dae-226">c.</span></span> <span data-ttu-id="45dae-227">在 hello**名字**文字方塊中，型別第一個名稱類似的 hello 使用者**許**。</span><span class="sxs-lookup"><span data-stu-id="45dae-227">In hello **First Name** textbox, type first name of hello user like **Britta**.</span></span>

   <span data-ttu-id="45dae-228">d.</span><span class="sxs-lookup"><span data-stu-id="45dae-228">d.</span></span> <span data-ttu-id="45dae-229">在 hello**姓氏**文字方塊中，姓氏類似 hello 使用者類型**Simon**。</span><span class="sxs-lookup"><span data-stu-id="45dae-229">In hello **Last Name** textbox, type last name of hello user like **Simon**.</span></span>
   
   <span data-ttu-id="45dae-230">e.</span><span class="sxs-lookup"><span data-stu-id="45dae-230">e.</span></span> <span data-ttu-id="45dae-231">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="45dae-231">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="45dae-232">您可以使用任何其他 Jitbit Helpdesk 使用者帳戶建立工具或 Api 提供 Jitbit Helpdesk tooprovision Azure AD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="45dae-232">You can use any other Jitbit Helpdesk user account creation tools or APIs provided by Jitbit Helpdesk tooprovision Azure AD user accounts.</span></span>
> 
        

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="45dae-233">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="45dae-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="45dae-234">在本節中，以啟用許 Simon toouse Azure 單一登入授與存取 tooJitbit 技術服務人員。</span><span class="sxs-lookup"><span data-stu-id="45dae-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJitbit Helpdesk.</span></span>

![指派使用者][200] 

<span data-ttu-id="45dae-236">**tooassign 許 Simon tooJitbit 技術服務人員，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="45dae-236">**tooassign Britta Simon tooJitbit Helpdesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="45dae-237">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="45dae-237">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="45dae-239">在 [hello] 應用程式清單中，選取**Jitbit Helpdesk**。</span><span class="sxs-lookup"><span data-stu-id="45dae-239">In hello applications list, select **Jitbit Helpdesk**.</span></span>

    ![設定單一登入](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_app.png) 

3. <span data-ttu-id="45dae-241">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="45dae-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="45dae-243">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="45dae-243">Click **Add** button.</span></span> <span data-ttu-id="45dae-244">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="45dae-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="45dae-246">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="45dae-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="45dae-247">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="45dae-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="45dae-248">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="45dae-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="45dae-249">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="45dae-249">Testing single sign-on</span></span>

<span data-ttu-id="45dae-250">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="45dae-250">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="45dae-251">當您按一下的 hello Jitbit Helpdesk 磚 hello 存取面板中時，您應該取得 Jitbit Helpdesk 的應用程式的登入頁面。</span><span class="sxs-lookup"><span data-stu-id="45dae-251">When you click hello Jitbit Helpdesk tile in hello Access Panel, you should get login page of Jitbit Helpdesk application.</span></span>
<span data-ttu-id="45dae-252">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="45dae-252">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="45dae-253">其他資源</span><span class="sxs-lookup"><span data-stu-id="45dae-253">Additional resources</span></span>

* [<span data-ttu-id="45dae-254">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="45dae-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="45dae-255">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="45dae-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_203.png

