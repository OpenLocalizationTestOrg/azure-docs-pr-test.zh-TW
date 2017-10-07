---
title: "教學課程：Azure Active Directory 與 ClickTime 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 ClickTime 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d437b5ab-4d71-4c13-96d0-79018cebbbd4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jeedes
ms.openlocfilehash: a0259e31164cad6c6c77ed8aac1c50cd9a3e46ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clicktime"></a><span data-ttu-id="6729f-103">教學課程：Azure Active Directory 與 ClickTime 整合</span><span class="sxs-lookup"><span data-stu-id="6729f-103">Tutorial: Azure Active Directory integration with ClickTime</span></span>

<span data-ttu-id="6729f-104">在此教學課程中，您學會如何 toointegrate ClickTime 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="6729f-104">In this tutorial, you learn how toointegrate ClickTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6729f-105">整合 Azure AD 與 ClickTime 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="6729f-105">Integrating ClickTime with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6729f-106">您可以控制存取 tooClickTime Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="6729f-106">You can control in Azure AD who has access tooClickTime</span></span>
- <span data-ttu-id="6729f-107">您可以啟用您的使用者 tooautomatically get 登入 tooClickTime （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="6729f-107">You can enable your users tooautomatically get signed-on tooClickTime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6729f-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="6729f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6729f-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="6729f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6729f-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="6729f-110">Prerequisites</span></span>

<span data-ttu-id="6729f-111">tooconfigure Azure AD 與 ClickTime 的整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="6729f-111">tooconfigure Azure AD integration with ClickTime, you need hello following items:</span></span>

- <span data-ttu-id="6729f-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="6729f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6729f-113">啟用 ClickTime 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="6729f-113">A ClickTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6729f-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="6729f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6729f-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="6729f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6729f-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="6729f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6729f-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="6729f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6729f-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="6729f-118">Scenario description</span></span>
<span data-ttu-id="6729f-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6729f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6729f-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="6729f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6729f-121">從 hello 圖庫加入 ClickTime</span><span class="sxs-lookup"><span data-stu-id="6729f-121">Adding ClickTime from hello gallery</span></span>
2. <span data-ttu-id="6729f-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6729f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-clicktime-from-hello-gallery"></a><span data-ttu-id="6729f-123">從 hello 圖庫加入 ClickTime</span><span class="sxs-lookup"><span data-stu-id="6729f-123">Adding ClickTime from hello gallery</span></span>
<span data-ttu-id="6729f-124">tooconfigure hello 整合 ClickTime 的 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd ClickTime。</span><span class="sxs-lookup"><span data-stu-id="6729f-124">tooconfigure hello integration of ClickTime into Azure AD, you need tooadd ClickTime from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6729f-125">**tooadd ClickTime 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="6729f-125">**tooadd ClickTime from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6729f-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="6729f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 按鈕][1]

2. <span data-ttu-id="6729f-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="6729f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6729f-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="6729f-129">Then go too**All applications**.</span></span>

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. <span data-ttu-id="6729f-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="6729f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 新應用程式按鈕][3]

4. <span data-ttu-id="6729f-133">在 hello 搜尋方塊中，輸入**ClickTime**，選取**ClickTime**然後按一下 從結果面板**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6729f-133">In hello search box, type **ClickTime**, select **ClickTime** from result panel then click **Add** button tooadd hello application.</span></span>

    ![ClickTime hello [結果] 清單中](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6729f-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6729f-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="6729f-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 ClickTime 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6729f-136">In this section, you configure and test Azure AD single sign-on with ClickTime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6729f-137">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 ClickTime 中是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="6729f-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ClickTime is tooa user in Azure AD.</span></span> <span data-ttu-id="6729f-138">換句話說，Azure AD 使用者與 hello ClickTime 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="6729f-138">In other words, a link relationship between an Azure AD user and hello related user in ClickTime needs toobe established.</span></span>

<span data-ttu-id="6729f-139">在 ClickTime 中，將指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="6729f-139">In ClickTime, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6729f-140">tooconfigure 和測試 Azure AD 單一登入與 ClickTime，您需要遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="6729f-140">tooconfigure and test Azure AD single sign-on with ClickTime, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6729f-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="6729f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6729f-142">**[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="6729f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6729f-143">**[建立測試使用者 ClickTime](#create-a-clicktime-test-user)**  -toohave 許 Simon ClickTime 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="6729f-143">**[Create a ClickTime test user](#create-a-clicktime-test-user)** - toohave a counterpart of Britta Simon in ClickTime that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6729f-144">**[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6729f-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6729f-145">**[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="6729f-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="6729f-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6729f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="6729f-147">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 ClickTime 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="6729f-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ClickTime application.</span></span>

<span data-ttu-id="6729f-148">**tooconfigure Azure AD 單一登入與 ClickTime，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="6729f-148">**tooconfigure Azure AD single sign-on with ClickTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="6729f-149">在 Azure 入口網站上 hello hello **ClickTime**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="6729f-149">In hello Azure portal, on hello **ClickTime** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="6729f-151">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6729f-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_samlbase.png)

3. <span data-ttu-id="6729f-153">在 hello **ClickTime 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="6729f-153">On hello **ClickTime Domain and URLs** section, perform hello following steps:</span></span>

    ![ClickTime 網域與 URL 單一登入資訊](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_url.png)

    <span data-ttu-id="6729f-155">a.</span><span class="sxs-lookup"><span data-stu-id="6729f-155">a.</span></span> <span data-ttu-id="6729f-156">在 hello**識別碼**文字方塊中，輸入 URL:`https://app.clicktime.com/sp/`</span><span class="sxs-lookup"><span data-stu-id="6729f-156">In hello **Identifier** textbox, type a URL as: `https://app.clicktime.com/sp/`</span></span>
    
    <span data-ttu-id="6729f-157">b.</span><span class="sxs-lookup"><span data-stu-id="6729f-157">b.</span></span> <span data-ttu-id="6729f-158">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列的 hello 模式：</span><span class="sxs-lookup"><span data-stu-id="6729f-158">In hello **Reply URL** textbox, type a URL using hello following patterns:</span></span> 

    | |
    |--|
    | `https://app.clicktime.com/Login/` |
    | `https://app.clicktime.com/App/Login/Consume.aspx` |

4. <span data-ttu-id="6729f-159">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="6729f-159">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![hello 憑證下載連結](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_certificate.png) 

5. <span data-ttu-id="6729f-161">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="6729f-161">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-clicktime-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6729f-163">在 hello **ClickTime 組態**區段中，按一下**設定 ClickTime** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="6729f-163">On hello **ClickTime Configuration** section, click **Configure ClickTime** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6729f-164">複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="6729f-164">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![ClickTime 組態](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_configure.png) 

7. <span data-ttu-id="6729f-166">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 ClickTime 公司網站。</span><span class="sxs-lookup"><span data-stu-id="6729f-166">In a different web browser window, log into your ClickTime company site as an administrator.</span></span>

8. <span data-ttu-id="6729f-167">在 hello hello 上方的工具列中按一下**喜好設定**，然後按一下**安全性設定**。</span><span class="sxs-lookup"><span data-stu-id="6729f-167">In hello toolbar on hello top, click **Preferences**, and then click **Security Settings**.</span></span>

9. <span data-ttu-id="6729f-168">在 hello**單一登入喜好設定**組態區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="6729f-168">In hello **Single Sign-On Preferences** configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="6729f-169">![安全性設定](./media/active-directory-saas-clicktime-tutorial/tic777280.png "安全性設定")</span><span class="sxs-lookup"><span data-stu-id="6729f-169">![Security Settings](./media/active-directory-saas-clicktime-tutorial/tic777280.png "Security Settings")</span></span>
   
    <span data-ttu-id="6729f-170">a.</span><span class="sxs-lookup"><span data-stu-id="6729f-170">a.</span></span>  <span data-ttu-id="6729f-171">選取 [允許]，以搭配 **Azure AD** 使用單一登入 (SSO) 進行登入。</span><span class="sxs-lookup"><span data-stu-id="6729f-171">Select **Allow** sign-in using Single Sign-On (SSO) with **Azure AD**.</span></span>
   
    <span data-ttu-id="6729f-172">b.</span><span class="sxs-lookup"><span data-stu-id="6729f-172">b.</span></span> <span data-ttu-id="6729f-173">在 hello**身分識別提供者端點**文字方塊中，貼上**SAML 單一登入服務 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="6729f-173">In hello **Identity Provider Endpoint** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="6729f-174">c.</span><span class="sxs-lookup"><span data-stu-id="6729f-174">c.</span></span>  <span data-ttu-id="6729f-175">開啟 hello **base 64 編碼憑證**從 Azure 入口網站中下載**記事本**、 hello 內容複製並貼到 hello **X.509 憑證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="6729f-175">Open hello **base-64 encoded certificate** downloaded from Azure portal in **Notepad**, copy hello content, and then paste it into hello **X.509 Certificate** textbox.</span></span>
   
    <span data-ttu-id="6729f-176">d.</span><span class="sxs-lookup"><span data-stu-id="6729f-176">d.</span></span>  <span data-ttu-id="6729f-177">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="6729f-177">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="6729f-178">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="6729f-178">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6729f-179">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="6729f-179">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6729f-180">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6729f-180">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6729f-181">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="6729f-181">Create an Azure AD test user</span></span>
<span data-ttu-id="6729f-182">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="6729f-182">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 測試使用者][100]

<span data-ttu-id="6729f-184">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="6729f-184">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6729f-185">在 hello Azure 入口網站，hello 左窗格中，按一下 hello **Azure Active Directory**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="6729f-185">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-clicktime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6729f-187">toodisplay hello 使用者清單，請移過**使用者和群組**，然後按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="6729f-187">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>
    
    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-clicktime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6729f-189">tooopen hello**使用者**對話方塊中，按一下 [**新增**頂端的 hello hello**所有使用者**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="6729f-189">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>
 
    ![hello [新增] 按鈕](./media/active-directory-saas-clicktime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6729f-191">在 hello**使用者**對話方塊方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="6729f-191">In hello **User** dialog box, perform hello following steps:</span></span>
 
    ![hello [使用者] 對話方塊](./media/active-directory-saas-clicktime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6729f-193">a.</span><span class="sxs-lookup"><span data-stu-id="6729f-193">a.</span></span> <span data-ttu-id="6729f-194">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="6729f-194">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6729f-195">b.</span><span class="sxs-lookup"><span data-stu-id="6729f-195">b.</span></span> <span data-ttu-id="6729f-196">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="6729f-196">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6729f-197">c.</span><span class="sxs-lookup"><span data-stu-id="6729f-197">c.</span></span> <span data-ttu-id="6729f-198">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="6729f-198">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6729f-199">d.</span><span class="sxs-lookup"><span data-stu-id="6729f-199">d.</span></span> <span data-ttu-id="6729f-200">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="6729f-200">Click **Create**.</span></span>
 
### <a name="create-a-clicktime-test-user"></a><span data-ttu-id="6729f-201">建立 ClickTime 測試使用者</span><span class="sxs-lookup"><span data-stu-id="6729f-201">Create a ClickTime test user</span></span>

<span data-ttu-id="6729f-202">在訂單 tooenable Azure AD 使用者 toolog 入 ClickTime，它們必須佈建到 ClickTime。</span><span class="sxs-lookup"><span data-stu-id="6729f-202">In order tooenable Azure AD users toolog into ClickTime, they must be provisioned into ClickTime.</span></span>  
<span data-ttu-id="6729f-203">在 ClickTime 的 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="6729f-203">In hello case of ClickTime, provisioning is a manual task.</span></span>

> [!NOTE]
> <span data-ttu-id="6729f-204">您可以使用任何其他 ClickTime 使用者帳戶建立工具或 Api 提供 ClickTime tooprovision Azure AD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="6729f-204">You can use any other ClickTime user account creation tools or APIs provided by ClickTime tooprovision Azure AD user accounts.</span></span>

<span data-ttu-id="6729f-205">**tooprovision 使用者帳戶，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="6729f-205">**tooprovision a user account, perform hello following steps:**</span></span>
1. <span data-ttu-id="6729f-206">登入 tooyour **ClickTime**租用戶。</span><span class="sxs-lookup"><span data-stu-id="6729f-206">Log in tooyour **ClickTime** tenant.</span></span>
2. <span data-ttu-id="6729f-207">在 hello hello 上方的工具列中按一下**公司**，然後按一下**人員**。</span><span class="sxs-lookup"><span data-stu-id="6729f-207">In hello toolbar on hello top, click **Company**, and then click **People**.</span></span>
   
    <span data-ttu-id="6729f-208">![人員](./media/active-directory-saas-clicktime-tutorial/tic777282.png "人員")</span><span class="sxs-lookup"><span data-stu-id="6729f-208">![People](./media/active-directory-saas-clicktime-tutorial/tic777282.png "People")</span></span>
3. <span data-ttu-id="6729f-209">按一下 [新增人員] 。</span><span class="sxs-lookup"><span data-stu-id="6729f-209">Click **Add Person**.</span></span>
   
    <span data-ttu-id="6729f-210">![新增人員](./media/active-directory-saas-clicktime-tutorial/tic777283.png "新增人員")</span><span class="sxs-lookup"><span data-stu-id="6729f-210">![Add Person](./media/active-directory-saas-clicktime-tutorial/tic777283.png "Add Person")</span></span>
4. <span data-ttu-id="6729f-211">在 hello 人員 區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="6729f-211">In hello New Person section, perform hello following steps:</span></span>
   
    <span data-ttu-id="6729f-212">![人員](./media/active-directory-saas-clicktime-tutorial/tic777284.png "人員")</span><span class="sxs-lookup"><span data-stu-id="6729f-212">![People](./media/active-directory-saas-clicktime-tutorial/tic777284.png "People")</span></span>
   
    <span data-ttu-id="6729f-213">a.</span><span class="sxs-lookup"><span data-stu-id="6729f-213">a.</span></span>  <span data-ttu-id="6729f-214">在 hello**全名**文字方塊中，例如使用者的完整名稱的輸入**許 Simon**。</span><span class="sxs-lookup"><span data-stu-id="6729f-214">In hello **full name** textbox, type full name of user like **Britta Simon**.</span></span> 
  
    <span data-ttu-id="6729f-215">b.</span><span class="sxs-lookup"><span data-stu-id="6729f-215">b.</span></span>  <span data-ttu-id="6729f-216">在 hello**電子郵件地址**文字方塊中，型別 hello 電子郵件的使用者喜歡 **brittasimon@contoso.com** 。</span><span class="sxs-lookup"><span data-stu-id="6729f-216">In hello **email address** textbox, type hello email of user like **brittasimon@contoso.com**.</span></span>
       
    > [!NOTE]
    > <span data-ttu-id="6729f-217">如果您想要您可以設定新人員物件 hello 的其他屬性。</span><span class="sxs-lookup"><span data-stu-id="6729f-217">If you want to, you can set additional properties of hello new person object.</span></span>
   
    <span data-ttu-id="6729f-218">c.</span><span class="sxs-lookup"><span data-stu-id="6729f-218">c.</span></span>  <span data-ttu-id="6729f-219">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="6729f-219">Click **Save**.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="6729f-220">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="6729f-220">Assign hello Azure AD test user</span></span>

<span data-ttu-id="6729f-221">在本節中，您可以授與存取 tooClickTime 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6729f-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooClickTime.</span></span>

![指派 hello 使用者角色][200] 

<span data-ttu-id="6729f-223">**tooassign 許 Simon tooClickTime，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="6729f-223">**tooassign Britta Simon tooClickTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="6729f-224">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="6729f-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="6729f-226">在 [hello] 應用程式清單中，選取**ClickTime**。</span><span class="sxs-lookup"><span data-stu-id="6729f-226">In hello applications list, select **ClickTime**.</span></span>

    ![ClickTimne hello 應用程式清單中的連結](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_app.png) 

3. <span data-ttu-id="6729f-228">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="6729f-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello 「 使用者和群組 」 的連結][202] 

4. <span data-ttu-id="6729f-230">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6729f-230">Click **Add** button.</span></span> <span data-ttu-id="6729f-231">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="6729f-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 將作業加入窗格][203]

5. <span data-ttu-id="6729f-233">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="6729f-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6729f-234">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6729f-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6729f-235">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6729f-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="6729f-236">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="6729f-236">Test single sign-on</span></span>

<span data-ttu-id="6729f-237">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="6729f-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6729f-238">當您按一下 hello ClickTime 磚 hello 存取面板中的時，您應該取得自動登入 tooyour ClickTime 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="6729f-238">When you click hello ClickTime tile in hello Access Panel, you should get automatically signed-on tooyour ClickTime application.</span></span>
<span data-ttu-id="6729f-239">如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="6729f-239">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6729f-240">其他資源</span><span class="sxs-lookup"><span data-stu-id="6729f-240">Additional resources</span></span>

* [<span data-ttu-id="6729f-241">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6729f-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6729f-242">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="6729f-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_203.png

