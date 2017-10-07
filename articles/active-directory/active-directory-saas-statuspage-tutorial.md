---
title: "教學課程：將 Azure Active Directory 與 StatusPage 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 StatusPage 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f6ee8bb3-df43-4c0d-bf84-89f18deac4b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 7c6717017984241e9e459273ead4b5e062311120
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-statuspage"></a><span data-ttu-id="0898a-103">教學課程：將 Azure Active Directory 與 StatusPage 整合</span><span class="sxs-lookup"><span data-stu-id="0898a-103">Tutorial: Azure Active Directory integration with StatusPage</span></span>

<span data-ttu-id="0898a-104">在此教學課程中，您學會如何 toointegrate StatusPage 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="0898a-104">In this tutorial, you learn how toointegrate StatusPage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0898a-105">與 Azure AD 整合 StatusPage 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="0898a-105">Integrating StatusPage with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0898a-106">您可以控制存取 tooStatusPage Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="0898a-106">You can control in Azure AD who has access tooStatusPage</span></span>
- <span data-ttu-id="0898a-107">您可以啟用您的使用者 tooautomatically get 登入 tooStatusPage （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="0898a-107">You can enable your users tooautomatically get signed-on tooStatusPage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0898a-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="0898a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0898a-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="0898a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0898a-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="0898a-110">Prerequisites</span></span>

<span data-ttu-id="0898a-111">tooconfigure StatusPage 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="0898a-111">tooconfigure Azure AD integration with StatusPage, you need hello following items:</span></span>

- <span data-ttu-id="0898a-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0898a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0898a-113">已啟用 StatusPage 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0898a-113">A StatusPage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0898a-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="0898a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0898a-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="0898a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0898a-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="0898a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0898a-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="0898a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0898a-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="0898a-118">Scenario description</span></span>
<span data-ttu-id="0898a-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0898a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0898a-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="0898a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0898a-121">從 hello 圖庫加入 StatusPage</span><span class="sxs-lookup"><span data-stu-id="0898a-121">Adding StatusPage from hello gallery</span></span>
2. <span data-ttu-id="0898a-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0898a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-statuspage-from-hello-gallery"></a><span data-ttu-id="0898a-123">從 hello 圖庫加入 StatusPage</span><span class="sxs-lookup"><span data-stu-id="0898a-123">Adding StatusPage from hello gallery</span></span>
<span data-ttu-id="0898a-124">tooconfigure hello 整合 StatusPage 到 Azure AD，您需要 tooadd StatusPage hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0898a-124">tooconfigure hello integration of StatusPage into Azure AD, you need tooadd StatusPage from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0898a-125">**tooadd StatusPage 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="0898a-125">**tooadd StatusPage from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0898a-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="0898a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0898a-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="0898a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0898a-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="0898a-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="0898a-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="0898a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="0898a-133">在 [hello] 搜尋方塊中，輸入**StatusPage**。</span><span class="sxs-lookup"><span data-stu-id="0898a-133">In hello search box, type **StatusPage**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_search.png)

5. <span data-ttu-id="0898a-135">在 hello 結果 窗格中，選取  **StatusPage**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0898a-135">In hello results panel, select **StatusPage**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0898a-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0898a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0898a-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 StatusPage 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0898a-138">In this section, you configure and test Azure AD single sign-on with StatusPage based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0898a-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 StatusPage 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="0898a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in StatusPage is tooa user in Azure AD.</span></span> <span data-ttu-id="0898a-140">換句話說，Azure AD 使用者與 hello StatusPage 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="0898a-140">In other words, a link relationship between an Azure AD user and hello related user in StatusPage needs toobe established.</span></span>

<span data-ttu-id="0898a-141">StatusPage 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="0898a-141">In StatusPage, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0898a-142">tooconfigure 及 StatusPage 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="0898a-142">tooconfigure and test Azure AD single sign-on with StatusPage, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0898a-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="0898a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0898a-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="0898a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0898a-145">**[建立測試使用者 StatusPage](#creating-a-statuspage-test-user)**  -toohave 許 Simon StatusPage 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="0898a-145">**[Creating a StatusPage test user](#creating-a-statuspage-test-user)** - toohave a counterpart of Britta Simon in StatusPage that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0898a-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0898a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0898a-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="0898a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0898a-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0898a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0898a-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 StatusPage 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="0898a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your StatusPage application.</span></span>

<span data-ttu-id="0898a-150">**tooconfigure Azure AD 單一登入與 StatusPage，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="0898a-150">**tooconfigure Azure AD single sign-on with StatusPage, perform hello following steps:**</span></span>

1. <span data-ttu-id="0898a-151">在 Azure 入口網站上 hello hello **StatusPage**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="0898a-151">In hello Azure portal, on hello **StatusPage** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="0898a-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0898a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_samlbase.png)

3. <span data-ttu-id="0898a-155">在 hello **StatusPage 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="0898a-155">On hello **StatusPage Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_url.png)

    <span data-ttu-id="0898a-157">a.</span><span class="sxs-lookup"><span data-stu-id="0898a-157">a.</span></span> <span data-ttu-id="0898a-158">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:</span><span class="sxs-lookup"><span data-stu-id="0898a-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.statuspagestaging.com/` |
    | `https://<subdomain>.statuspage.io/` |

    <span data-ttu-id="0898a-159">b.</span><span class="sxs-lookup"><span data-stu-id="0898a-159">b.</span></span> <span data-ttu-id="0898a-160">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:</span><span class="sxs-lookup"><span data-stu-id="0898a-160">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span> 
    | |
    |--|
    | `https://<subdomain>.statuspagestaging.com/sso/saml/consume` |
    | `https://<subdomain>.statuspage.io/sso/saml/consume` |

    > [!NOTE]
    > <span data-ttu-id="0898a-161">請連絡 hello StatusPage 支援團隊[ SupportTeam@statuspage.io ](mailto:SupportTeam@statuspage.io)toorequest 中繼資料所需的 tooconfigure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0898a-161">Contact hello StatusPage support team at [SupportTeam@statuspage.io](mailto:SupportTeam@statuspage.io)toorequest metadata necessary tooconfigure single sign-on.</span></span> 
    >
    ><span data-ttu-id="0898a-162">a.</span><span class="sxs-lookup"><span data-stu-id="0898a-162">a.</span></span> <span data-ttu-id="0898a-163">Hello 中繼資料，從複製 hello 簽發者值，並貼到 hello**識別碼**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="0898a-163">From hello metadata, copy hello Issuer value, and then paste it into hello **Identifier** textbox.</span></span>
    >
    ><span data-ttu-id="0898a-164">b.</span><span class="sxs-lookup"><span data-stu-id="0898a-164">b.</span></span> <span data-ttu-id="0898a-165">從 hello 中繼資料，複製 hello 回覆 URL，然後再將它貼到 hello**回覆 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="0898a-165">From hello metadata, copy hello Reply URL, and then paste it into hello **Reply URL** textbox.</span></span>

4. <span data-ttu-id="0898a-166">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="0898a-166">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_certificate.png) 

5. <span data-ttu-id="0898a-168">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="0898a-168">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-statuspage-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0898a-170">在 hello **StatusPage 組態**區段中，按一下**設定 StatusPage** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="0898a-170">On hello **StatusPage Configuration** section, click **Configure StatusPage** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0898a-171">複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="0898a-171">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_configure.png) 

7. <span data-ttu-id="0898a-173">在另一個瀏覽器視窗中，系統管理員身分登入 tooyour StatusPage 公司網站。</span><span class="sxs-lookup"><span data-stu-id="0898a-173">In another browser window, sign on tooyour StatusPage company site as an administrator.</span></span>

8. <span data-ttu-id="0898a-174">在 hello 主要工具列上，按一下 **管理帳戶**。</span><span class="sxs-lookup"><span data-stu-id="0898a-174">In hello main toolbar, click **Manage Account**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_06.png) 

10. <span data-ttu-id="0898a-176">按一下 hello**單一登入** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="0898a-176">Click hello **Single Sign-on** tab.</span></span> 
   
    ![設定單一登入](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_07.png) 

11. <span data-ttu-id="0898a-178">在 hello SSO 安裝程式 頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="0898a-178">On hello SSO Setup page, perform hello following steps:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_08.png) 

    ![設定單一登入](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_09.png) 
 
    <span data-ttu-id="0898a-181">a.</span><span class="sxs-lookup"><span data-stu-id="0898a-181">a.</span></span> <span data-ttu-id="0898a-182">在 hello **SSO 目標 URL**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="0898a-182">In hello **SSO Target URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0898a-183">b.</span><span class="sxs-lookup"><span data-stu-id="0898a-183">b.</span></span> <span data-ttu-id="0898a-184">開啟 [記事本]，複製 hello 內容，您所下載的憑證，然後將它貼到 hello**憑證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="0898a-184">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **Certificate** textbox.</span></span> 

    <span data-ttu-id="0898a-185">c.</span><span class="sxs-lookup"><span data-stu-id="0898a-185">c.</span></span> <span data-ttu-id="0898a-186">按一下 [儲存組態]。</span><span class="sxs-lookup"><span data-stu-id="0898a-186">Click **SAVE CONFIGURATION**.</span></span>

> [!TIP]
> <span data-ttu-id="0898a-187">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="0898a-187">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0898a-188">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="0898a-188">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0898a-189">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0898a-189">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0898a-190">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0898a-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="0898a-191">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="0898a-191">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="0898a-193">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="0898a-193">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0898a-194">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="0898a-194">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-statuspage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0898a-196">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="0898a-196">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-statuspage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0898a-198">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="0898a-198">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-statuspage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0898a-200">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="0898a-200">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-statuspage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0898a-202">a.</span><span class="sxs-lookup"><span data-stu-id="0898a-202">a.</span></span> <span data-ttu-id="0898a-203">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="0898a-203">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0898a-204">b.</span><span class="sxs-lookup"><span data-stu-id="0898a-204">b.</span></span> <span data-ttu-id="0898a-205">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="0898a-205">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0898a-206">c.</span><span class="sxs-lookup"><span data-stu-id="0898a-206">c.</span></span> <span data-ttu-id="0898a-207">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="0898a-207">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0898a-208">d.</span><span class="sxs-lookup"><span data-stu-id="0898a-208">d.</span></span> <span data-ttu-id="0898a-209">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="0898a-209">Click **Create**.</span></span>
 
### <a name="creating-a-statuspage-test-user"></a><span data-ttu-id="0898a-210">建立 StatusPage 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0898a-210">Creating a StatusPage test user</span></span>

<span data-ttu-id="0898a-211">hello 本節目標在於 toocreate StatusPage 中呼叫許 Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="0898a-211">hello objective of this section is toocreate a user called Britta Simon in StatusPage.</span></span>

<span data-ttu-id="0898a-212">StatusPage 支援 Just-in-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="0898a-212">StatusPage supports just-in-time provisioning.</span></span> <span data-ttu-id="0898a-213">您已在 [設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)中啟用。</span><span class="sxs-lookup"><span data-stu-id="0898a-213">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="0898a-214">**toocreate 呼叫許 Simon StatusPage，在使用者執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="0898a-214">**toocreate a user called Britta Simon in StatusPage, perform hello following steps:**</span></span>

1. <span data-ttu-id="0898a-215">以系統管理員身分登入 tooyour StatusPage 公司網站。</span><span class="sxs-lookup"><span data-stu-id="0898a-215">Sign-on tooyour StatusPage company site as an administrator.</span></span>

2. <span data-ttu-id="0898a-216">在 hello 最上層顯示 hello 功能表上，按一下**管理帳戶**。</span><span class="sxs-lookup"><span data-stu-id="0898a-216">In hello menu on hello top, click **Manage Account**.</span></span>

    ![設定單一登入](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_06.png)

3. <span data-ttu-id="0898a-218">按一下 hello**小組成員** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="0898a-218">Click hello **Team Members** tab.</span></span> 
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_10.png) 

4. <span data-ttu-id="0898a-220">按一下 [新增小組成員]。</span><span class="sxs-lookup"><span data-stu-id="0898a-220">Click **ADD TEAM MEMBER**.</span></span> 
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_11.png) 

5. <span data-ttu-id="0898a-222">型別 hello**電子郵件地址**，**名字**，和**姓氏**的有效的使用者將所要 tooprovision hello 相關的文字方塊。</span><span class="sxs-lookup"><span data-stu-id="0898a-222">Type hello **Email Address**, **First Name**, and **Sur Name** of a valid user you want tooprovision into hello related textboxes.</span></span> 
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_12.png) 

6. <span data-ttu-id="0898a-224">針對 [角色]，選擇 [用戶端系統管理員]。</span><span class="sxs-lookup"><span data-stu-id="0898a-224">As **Role**, choose **Client Administrator**.</span></span>

7. <span data-ttu-id="0898a-225">按一下 [建立帳戶]。</span><span class="sxs-lookup"><span data-stu-id="0898a-225">Click **CREATE ACCOUNT**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0898a-226">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="0898a-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0898a-227">在本節中，您可以授與存取 tooStatusPage 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0898a-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooStatusPage.</span></span>

![指派使用者][200] 

<span data-ttu-id="0898a-229">**tooassign 許 Simon tooStatusPage，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="0898a-229">**tooassign Britta Simon tooStatusPage, perform hello following steps:**</span></span>

1. <span data-ttu-id="0898a-230">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="0898a-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="0898a-232">在 [hello] 應用程式清單中，選取**StatusPage**。</span><span class="sxs-lookup"><span data-stu-id="0898a-232">In hello applications list, select **StatusPage**.</span></span>

    ![設定單一登入](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_app.png) 

3. <span data-ttu-id="0898a-234">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="0898a-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="0898a-236">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0898a-236">Click **Add** button.</span></span> <span data-ttu-id="0898a-237">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="0898a-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="0898a-239">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="0898a-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0898a-240">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0898a-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0898a-241">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0898a-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0898a-242">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="0898a-242">Testing single sign-on</span></span>

<span data-ttu-id="0898a-243">hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="0898a-243">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0898a-244">當您按一下 hello StatusPage 磚 hello 存取面板中的時，您應該取得自動登入 tooyour StatusPage 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0898a-244">When you click hello StatusPage tile in hello Access Panel, you should get automatically signed-on tooyour StatusPage application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0898a-245">其他資源</span><span class="sxs-lookup"><span data-stu-id="0898a-245">Additional resources</span></span>

* [<span data-ttu-id="0898a-246">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0898a-246">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0898a-247">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="0898a-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_203.png

