---
title: "教學課程：Azure Active Directory 與 Tangoe 命令高階行動裝置整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Tangoe 命令 Premium Mobile 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2b0b544c-9c2c-49cd-862b-ec2ee9330126
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 7bd1cd6afade58a4a47a173b249f92eb84e42112
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tangoe-command-premium-mobile"></a><span data-ttu-id="7ea31-103">教學課程：Azure Active Directory 整合 Tangoe 命令高階行動裝置</span><span class="sxs-lookup"><span data-stu-id="7ea31-103">Tutorial: Azure Active Directory integration with Tangoe Command Premium Mobile</span></span>

<span data-ttu-id="7ea31-104">在此教學課程中，您學會如何 toointegrate Tangoe 命令 Premium 行動裝置與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="7ea31-104">In this tutorial, you learn how toointegrate Tangoe Command Premium Mobile with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7ea31-105">與 Azure AD 整合 Tangoe 命令 Premium 行動可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="7ea31-105">Integrating Tangoe Command Premium Mobile with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7ea31-106">您可以控制存取 tooTangoe 命令 Premium 行動裝置版的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="7ea31-106">You can control in Azure AD who has access tooTangoe Command Premium Mobile</span></span>
- <span data-ttu-id="7ea31-107">您可以使用其 Azure AD 帳戶啟用您使用者 tooautomatically get 登入 tooTangoe 命令 Premium 行動 （單一登入）</span><span class="sxs-lookup"><span data-stu-id="7ea31-107">You can enable your users tooautomatically get signed-on tooTangoe Command Premium Mobile (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7ea31-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="7ea31-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7ea31-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="7ea31-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ea31-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="7ea31-110">Prerequisites</span></span>

<span data-ttu-id="7ea31-111">tooconfigure Tangoe 命令 Premium 行動裝置與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="7ea31-111">tooconfigure Azure AD integration with Tangoe Command Premium Mobile, you need hello following items:</span></span>

- <span data-ttu-id="7ea31-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7ea31-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7ea31-113">已啟用 Tangoe 命令高階行動裝置單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7ea31-113">A Tangoe Command Premium Mobile single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7ea31-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="7ea31-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7ea31-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="7ea31-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7ea31-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="7ea31-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7ea31-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="7ea31-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7ea31-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="7ea31-118">Scenario description</span></span>
<span data-ttu-id="7ea31-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7ea31-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7ea31-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="7ea31-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7ea31-121">從 hello 圖庫新增 Tangoe 命令 Premium 行動裝置</span><span class="sxs-lookup"><span data-stu-id="7ea31-121">Add Tangoe Command Premium Mobile from hello gallery</span></span>
2. <span data-ttu-id="7ea31-122">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7ea31-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tangoe-command-premium-mobile-from-hello-gallery"></a><span data-ttu-id="7ea31-123">從 hello 圖庫新增 Tangoe 命令 Premium 行動裝置</span><span class="sxs-lookup"><span data-stu-id="7ea31-123">Add Tangoe Command Premium Mobile from hello gallery</span></span>
<span data-ttu-id="7ea31-124">tooconfigure hello 整合 Tangoe 命令 Premium 行動到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Tangoe 命令 Premium 行動裝置。</span><span class="sxs-lookup"><span data-stu-id="7ea31-124">tooconfigure hello integration of Tangoe Command Premium Mobile into Azure AD, you need tooadd Tangoe Command Premium Mobile from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7ea31-125">**tooadd Tangoe 命令 Premium Mobile 從 hello 組件庫，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="7ea31-125">**tooadd Tangoe Command Premium Mobile from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7ea31-126">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="7ea31-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7ea31-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="7ea31-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7ea31-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="7ea31-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="7ea31-131">tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="7ea31-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="7ea31-133">在 hello 搜尋方塊中，輸入**Tangoe 命令 Premium 行動**，選取**Tangoe 命令 Premium 行動**然後按一下 [從結果面板**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ea31-133">In hello search box, type **Tangoe Command Premium Mobile**, select **Tangoe Command Premium Mobile** from result panel then click **Add** button tooadd hello application.</span></span>

    ![<span data-ttu-id="7ea31-134">從資源庫新增 Tangoe 命令高階行動裝置</span><span class="sxs-lookup"><span data-stu-id="7ea31-134">Add Tangoe Command Premium Mobile from gallery</span></span> ](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7ea31-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7ea31-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="7ea31-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Tangoe 命令高階行動裝置設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7ea31-136">In this section, you configure and test Azure AD single sign-on with Tangoe Command Premium Mobile based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7ea31-137">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 Tangoe 命令 Premium Mobile 中是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="7ea31-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Tangoe Command Premium Mobile is tooa user in Azure AD.</span></span> <span data-ttu-id="7ea31-138">換句話說，Azure AD 使用者與 hello Tangoe 命令 Premium Mobile 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="7ea31-138">In other words, a link relationship between an Azure AD user and hello related user in Tangoe Command Premium Mobile needs toobe established.</span></span>

<span data-ttu-id="7ea31-139">在 Tangoe 命令 Premium 行動，將指派 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="7ea31-139">In Tangoe Command Premium Mobile, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7ea31-140">tooconfigure 及 Tangoe 命令 Premium 行動裝置與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="7ea31-140">tooconfigure and test Azure AD single sign-on with Tangoe Command Premium Mobile, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7ea31-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="7ea31-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7ea31-142">**[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="7ea31-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7ea31-143">**[建立測試使用者 Tangoe 命令 Premium 行動](#create-a-tangoe-command-premium-mobile-test-user)** -toohave 許 Simon 中 Tangoe 命令 Premium Mobile 是連結的 toohello Azure AD 使用者表示法的對應項目。</span><span class="sxs-lookup"><span data-stu-id="7ea31-143">**[Create a Tangoe Command Premium Mobile test user](#create-a-tangoe-command-premium-mobile-test-user)** - toohave a counterpart of Britta Simon in Tangoe Command Premium Mobile that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7ea31-144">**[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7ea31-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7ea31-145">**[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="7ea31-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7ea31-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7ea31-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7ea31-147">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Tangoe 命令 Premium 行動應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="7ea31-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Tangoe Command Premium Mobile application.</span></span>

<span data-ttu-id="7ea31-148">**與 Tangoe 命令 Premium Mobile、 Azure AD 單一登入 tooconfigure 執行 hello 下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7ea31-148">**tooconfigure Azure AD single sign-on with Tangoe Command Premium Mobile, perform hello following steps:**</span></span>

1. <span data-ttu-id="7ea31-149">在 Azure 入口網站上 hello hello **Tangoe 命令 Premium 行動**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="7ea31-149">In hello Azure portal, on hello **Tangoe Command Premium Mobile** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="7ea31-151">在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7ea31-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![SAML 型登入](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_samlbase.png)

3. <span data-ttu-id="7ea31-153">在 [hello **Tangoe 命令 Premium 行動網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="7ea31-153">On hello **Tangoe Command Premium Mobile Domain and URLs** section, perform hello following steps:</span></span>

    ![Tangoe 命令高階行動裝置網域與 URL](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_url.png)

    <span data-ttu-id="7ea31-155">a.</span><span class="sxs-lookup"><span data-stu-id="7ea31-155">a.</span></span> <span data-ttu-id="7ea31-156">在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`</span><span class="sxs-lookup"><span data-stu-id="7ea31-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`</span></span>

    <span data-ttu-id="7ea31-157">b.</span><span class="sxs-lookup"><span data-stu-id="7ea31-157">b.</span></span> <span data-ttu-id="7ea31-158">在 [hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://sso.tangoe.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="7ea31-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://sso.tangoe.com/sp/ACS.saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7ea31-159">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="7ea31-159">These values are not real.</span></span> <span data-ttu-id="7ea31-160">Hello 實際的回覆 URL 和登入 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="7ea31-160">Update these values with hello actual  Reply URL and Sign-On URL.</span></span> <span data-ttu-id="7ea31-161">請連絡[Tangoe 命令 Premium 行動用戶端支援小組](https://www.tangoe.com/contact-2/)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="7ea31-161">Contact [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) tooget these values.</span></span> 

4. <span data-ttu-id="7ea31-162">在 [hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="7ea31-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![[SAML 簽署憑證] 區段](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_certificate.png) 

5. <span data-ttu-id="7ea31-164">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="7ea31-164">Click **Save** button.</span></span>

    ![[儲存] 按鈕](./media/active-directory-saas-tangoe-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="7ea31-166">在 [hello **Tangoe 命令 Premium 行動裝置組態**區段中，按一下**設定 Tangoe 命令 Premium 行動**tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="7ea31-166">On hello **Tangoe Command Premium Mobile Configuration** section, click **Configure Tangoe Command Premium Mobile** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7ea31-167">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="7ea31-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![[Tangoe 命令高階行動裝置設定] 區段](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_configure.png) 

7. <span data-ttu-id="7ea31-169">tooget SSO 設定應用程式，請連絡您[Tangoe 命令 Premium 行動用戶端支援小組](https://www.tangoe.com/contact-2/)並提供下列 hello:</span><span class="sxs-lookup"><span data-stu-id="7ea31-169">tooget SSO configured for your application, contact your [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) and provide hello following:</span></span>

   - <span data-ttu-id="7ea31-170">hello 下載的中繼資料檔案</span><span class="sxs-lookup"><span data-stu-id="7ea31-170">hello downloaded metadata file</span></span>
   - <span data-ttu-id="7ea31-171">hello **SAML 實體識別碼**</span><span class="sxs-lookup"><span data-stu-id="7ea31-171">hello **SAML Entity ID**</span></span>
   - <span data-ttu-id="7ea31-172">hello **SAML 單一登入服務 URL**</span><span class="sxs-lookup"><span data-stu-id="7ea31-172">hello **SAML Single Sign-On Service URL**</span></span>
   - <span data-ttu-id="7ea31-173">hello**登出 URL**</span><span class="sxs-lookup"><span data-stu-id="7ea31-173">hello **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="7ea31-174">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="7ea31-174">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7ea31-175">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="7ea31-175">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7ea31-176">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7ea31-176">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7ea31-177">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7ea31-177">Create an Azure AD test user</span></span>
<span data-ttu-id="7ea31-178">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="7ea31-178">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="7ea31-180">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="7ea31-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7ea31-181">在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="7ea31-181">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tangoe-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7ea31-183">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="7ea31-183">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![[使用者和群組] -> [所有使用者]](./media/active-directory-saas-tangoe-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7ea31-185">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="7ea31-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![新增使用者](./media/active-directory-saas-tangoe-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7ea31-187">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="7ea31-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![使用者對話方塊頁面](./media/active-directory-saas-tangoe-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7ea31-189">a.</span><span class="sxs-lookup"><span data-stu-id="7ea31-189">a.</span></span> <span data-ttu-id="7ea31-190">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="7ea31-190">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7ea31-191">b.</span><span class="sxs-lookup"><span data-stu-id="7ea31-191">b.</span></span> <span data-ttu-id="7ea31-192">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="7ea31-192">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7ea31-193">c.</span><span class="sxs-lookup"><span data-stu-id="7ea31-193">c.</span></span> <span data-ttu-id="7ea31-194">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="7ea31-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7ea31-195">d.</span><span class="sxs-lookup"><span data-stu-id="7ea31-195">d.</span></span> <span data-ttu-id="7ea31-196">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="7ea31-196">Click **Create**.</span></span>
 
### <a name="create-a-tangoe-command-premium-mobile-test-user"></a><span data-ttu-id="7ea31-197">建立 Tangoe 命令高階行動裝置測試使用者</span><span class="sxs-lookup"><span data-stu-id="7ea31-197">Create a Tangoe Command Premium Mobile test user</span></span>

<span data-ttu-id="7ea31-198">在本節中，您要在 Tangoe 命令高階行動裝置中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="7ea31-198">In this section, you create a user called Britta Simon in Tangoe Command Premium Mobile.</span></span> 

<span data-ttu-id="7ea31-199">Tangoe 命令 Premium 行動應用程式需要所有的 hello 使用者 toobe hello 進行單一登入前的應用程式中，佈建。</span><span class="sxs-lookup"><span data-stu-id="7ea31-199">Tangoe Command Premium Mobile application needs all hello users toobe provisioned in hello application before doing Single Sign On.</span></span> <span data-ttu-id="7ea31-200">工作，所以請以 hello [Tangoe 命令 Premium 行動用戶端支援小組](https://www.tangoe.com/contact-2/)tooprovision hello 應用程式的所有這些使用者。</span><span class="sxs-lookup"><span data-stu-id="7ea31-200">So please work with hello [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) tooprovision all these users into hello application.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="7ea31-201">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7ea31-201">Assign hello Azure AD test user</span></span>

<span data-ttu-id="7ea31-202">在本節中，您可以授與存取 tooTangoe 命令 Premium 行動裝置啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7ea31-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTangoe Command Premium Mobile.</span></span>

![指派使用者][200] 

<span data-ttu-id="7ea31-204">**tooassign 許 Simon tooTangoe 命令 Premium 行動裝置，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="7ea31-204">**tooassign Britta Simon tooTangoe Command Premium Mobile, perform hello following steps:**</span></span>

1. <span data-ttu-id="7ea31-205">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="7ea31-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="7ea31-207">在 [hello] 應用程式清單中，選取**Tangoe 命令 Premium 行動**。</span><span class="sxs-lookup"><span data-stu-id="7ea31-207">In hello applications list, select **Tangoe Command Premium Mobile**.</span></span>

    ![應用程式清單中的 Tangoe 命令高階行動裝置](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_app.png) 

3. <span data-ttu-id="7ea31-209">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="7ea31-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="7ea31-211">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7ea31-211">Click **Add** button.</span></span> <span data-ttu-id="7ea31-212">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="7ea31-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="7ea31-214">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="7ea31-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7ea31-215">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7ea31-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7ea31-216">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7ea31-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7ea31-217">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="7ea31-217">Test single sign-on</span></span>

<span data-ttu-id="7ea31-218">本節中，您可以測試使用存取面板 hello Azure AD 的 SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="7ea31-218">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="7ea31-219">當您按一下 hello Tangoe 命令 Premium 行動磚 hello 存取面板中的時，您應該取得自動登入 tooyour Tangoe 命令 Premium 行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ea31-219">When you click hello Tangoe Command Premium Mobile tile in hello Access Panel, you should get automatically signed-on tooyour Tangoe Command Premium Mobile application.</span></span> <span data-ttu-id="7ea31-220">如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="7ea31-220">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7ea31-221">其他資源</span><span class="sxs-lookup"><span data-stu-id="7ea31-221">Additional resources</span></span>

* [<span data-ttu-id="7ea31-222">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7ea31-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7ea31-223">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="7ea31-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_203.png

