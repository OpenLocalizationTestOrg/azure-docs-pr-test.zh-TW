---
title: "教學課程：Azure Active Directory 與 Bonusly 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Bonusly 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 29fea32a-fa20-47b2-9e24-26feb47b0ae6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 60ad06c028463af81a7901ab321c4ae9346798ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bonusly"></a><span data-ttu-id="46218-103">教學課程：Azure Active Directory 與 Bonusly 整合</span><span class="sxs-lookup"><span data-stu-id="46218-103">Tutorial: Azure Active Directory integration with Bonusly</span></span>

<span data-ttu-id="46218-104">在此教學課程中，您學會如何 toointegrate Bonusly 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="46218-104">In this tutorial, you learn how toointegrate Bonusly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="46218-105">與 Azure AD 整合 Bonusly 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="46218-105">Integrating Bonusly with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="46218-106">您可以控制存取 tooBonusly Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="46218-106">You can control in Azure AD who has access tooBonusly</span></span>
- <span data-ttu-id="46218-107">您可以啟用您的使用者 tooautomatically get 登入 tooBonusly （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="46218-107">You can enable your users tooautomatically get signed-on tooBonusly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="46218-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="46218-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="46218-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="46218-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="46218-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="46218-110">Prerequisites</span></span>

<span data-ttu-id="46218-111">tooconfigure Bonusly 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="46218-111">tooconfigure Azure AD integration with Bonusly, you need hello following items:</span></span>

- <span data-ttu-id="46218-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="46218-112">An Azure AD subscription</span></span>
- <span data-ttu-id="46218-113">已啟用 Bonusly 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="46218-113">A Bonusly single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="46218-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="46218-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="46218-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="46218-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="46218-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="46218-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="46218-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="46218-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="46218-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="46218-118">Scenario description</span></span>
<span data-ttu-id="46218-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="46218-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="46218-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="46218-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="46218-121">從 hello 圖庫加入 Bonusly</span><span class="sxs-lookup"><span data-stu-id="46218-121">Adding Bonusly from hello gallery</span></span>
2. <span data-ttu-id="46218-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="46218-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bonusly-from-hello-gallery"></a><span data-ttu-id="46218-123">從 hello 圖庫加入 Bonusly</span><span class="sxs-lookup"><span data-stu-id="46218-123">Adding Bonusly from hello gallery</span></span>
<span data-ttu-id="46218-124">tooconfigure hello 整合 Bonusly 到 Azure AD，您需要 tooadd Bonusly hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="46218-124">tooconfigure hello integration of Bonusly into Azure AD, you need tooadd Bonusly from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="46218-125">**tooadd Bonusly 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="46218-125">**tooadd Bonusly from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="46218-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="46218-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 按鈕][1]

2. <span data-ttu-id="46218-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="46218-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="46218-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="46218-129">Then go too**All applications**.</span></span>

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. <span data-ttu-id="46218-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="46218-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 新應用程式按鈕][3]

4. <span data-ttu-id="46218-133">在 hello 搜尋方塊中，輸入**Bonusly**，選取**Bonusly**然後按一下 從結果面板**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="46218-133">In hello search box, type **Bonusly**, select **Bonusly** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Bonusly hello [結果] 清單中](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="46218-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="46218-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="46218-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Bonusly 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="46218-136">In this section, you configure and test Azure AD single sign-on with Bonusly based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="46218-137">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Bonusly 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="46218-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Bonusly is tooa user in Azure AD.</span></span> <span data-ttu-id="46218-138">換句話說，Azure AD 使用者與 hello Bonusly 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="46218-138">In other words, a link relationship between an Azure AD user and hello related user in Bonusly needs toobe established.</span></span>

<span data-ttu-id="46218-139">Bonusly 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="46218-139">In Bonusly, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="46218-140">tooconfigure 及 Bonusly 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="46218-140">tooconfigure and test Azure AD single sign-on with Bonusly, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="46218-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="46218-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="46218-142">**[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="46218-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="46218-143">**[建立 Bonusly 測試使用者](#create-a-bonusly-test-user)** -toohave 許 Simon Bonusly 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="46218-143">**[Create a Bonusly test user](#create-a-bonusly-test-user)** - toohave a counterpart of Britta Simon in Bonusly that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="46218-144">**[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="46218-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="46218-145">**[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="46218-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="46218-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="46218-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="46218-147">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Bonusly 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="46218-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Bonusly application.</span></span>

<span data-ttu-id="46218-148">**tooconfigure Azure AD 單一登入與 Bonusly，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="46218-148">**tooconfigure Azure AD single sign-on with Bonusly, perform hello following steps:**</span></span>

1. <span data-ttu-id="46218-149">在 Azure 入口網站上 hello hello **Bonusly**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="46218-149">In hello Azure portal, on hello **Bonusly** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="46218-151">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="46218-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_samlbase.png)

3. <span data-ttu-id="46218-153">在 hello **Bonusly 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="46218-153">On hello **Bonusly Domain and URLs** section, perform hello following steps:</span></span>

    ![Bonusly 網域及 URL 單一登入資訊](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_url.png)

    <span data-ttu-id="46218-155">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://Bonus.ly/saml/<tenant-name>`</span><span class="sxs-lookup"><span data-stu-id="46218-155">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://Bonus.ly/saml/<tenant-name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="46218-156">hello 值不是真正的。</span><span class="sxs-lookup"><span data-stu-id="46218-156">hello value is not real.</span></span> <span data-ttu-id="46218-157">更新 hello 值與 hello 實際的回覆 URL。</span><span class="sxs-lookup"><span data-stu-id="46218-157">Update hello value with hello actual Reply URL.</span></span> <span data-ttu-id="46218-158">請連絡[Bonusly 支援小組](https://Bonusly/contact)tooget hello 值。</span><span class="sxs-lookup"><span data-stu-id="46218-158">Contact [Bonusly support team](https://Bonusly/contact) tooget hello value.</span></span>
 
4. <span data-ttu-id="46218-159">在 hello **SAML 簽章憑證**區段，複製 hello**指紋**hello 憑證中的值。</span><span class="sxs-lookup"><span data-stu-id="46218-159">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value from hello certificate.</span></span>

    ![hello 憑證下載連結](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_certificate.png) 

5. <span data-ttu-id="46218-161">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="46218-161">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-bonus-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="46218-163">在 hello **Bonusly 組態**區段中，按一下**Bonusly 設定**tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="46218-163">On hello **Bonusly Configuration** section, click **Configure Bonusly** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="46218-164">複製 hello **SAML 實體識別碼和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="46218-164">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Bonusly 組態](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_configure.png) 

7. <span data-ttu-id="46218-166">在不同的瀏覽器視窗中，登入 tooyour **Bonusly**租用戶。</span><span class="sxs-lookup"><span data-stu-id="46218-166">In a different browser window, log in tooyour **Bonusly** tenant.</span></span>

8. <span data-ttu-id="46218-167">在 hello hello 上方的工具列中按一下**設定**，然後選取**整合和應用程式**。</span><span class="sxs-lookup"><span data-stu-id="46218-167">In hello toolbar on hello top, click **Settings**, and then select **Integrations and apps**.</span></span>
   
    <span data-ttu-id="46218-168">![Bonusly 社交區段](./media/active-directory-saas-bonus-tutorial/ic773686.png "Bonusly")</span><span class="sxs-lookup"><span data-stu-id="46218-168">![Bonusly Social Section](./media/active-directory-saas-bonus-tutorial/ic773686.png "Bonusly")</span></span>
9. <span data-ttu-id="46218-169">在 [單一登入] 下方，選取 [SAML]。</span><span class="sxs-lookup"><span data-stu-id="46218-169">Under **Single Sign-On**, select **SAML**.</span></span>

10. <span data-ttu-id="46218-170">在 hello **SAML**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="46218-170">On hello **SAML** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="46218-171">![Bonusly Saml 對話方塊頁面](./media/active-directory-saas-bonus-tutorial/ic773687.png "Bonusly")</span><span class="sxs-lookup"><span data-stu-id="46218-171">![Bonusly Saml Dialog page](./media/active-directory-saas-bonus-tutorial/ic773687.png "Bonusly")</span></span>
   
    <span data-ttu-id="46218-172">a.</span><span class="sxs-lookup"><span data-stu-id="46218-172">a.</span></span> <span data-ttu-id="46218-173">在 hello **IdP SSO 目標 URL**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="46218-173">In hello **IdP SSO target URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="46218-174">b.</span><span class="sxs-lookup"><span data-stu-id="46218-174">b.</span></span> <span data-ttu-id="46218-175">在 hello **IdP 簽發者**文字方塊中，貼上 hello 值**SAML 實體識別碼**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="46218-175">In hello **IdP Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="46218-176">c.</span><span class="sxs-lookup"><span data-stu-id="46218-176">c.</span></span> <span data-ttu-id="46218-177">在 hello **IdP 登入 URL**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="46218-177">In hello **IdP Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="46218-178">d.</span><span class="sxs-lookup"><span data-stu-id="46218-178">d.</span></span> <span data-ttu-id="46218-179">貼上**指紋**值從 Azure 入口網站複製到 hello**憑證指紋**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="46218-179">Paste the **Thumbprint** value copied from Azure portal into hello **Cert Fingerprint** textbox.</span></span>
   
11. <span data-ttu-id="46218-180">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="46218-180">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="46218-181">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="46218-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="46218-182">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="46218-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="46218-183">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="46218-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="46218-184">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="46218-184">Create an Azure AD test user</span></span>
<span data-ttu-id="46218-185">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="46218-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 測試使用者][100]

<span data-ttu-id="46218-187">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="46218-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="46218-188">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="46218-188">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-bonus-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="46218-190">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="46218-190">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-bonus-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="46218-192">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="46218-192">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![hello [新增] 按鈕](./media/active-directory-saas-bonus-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="46218-194">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="46218-194">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![hello [使用者] 對話方塊](./media/active-directory-saas-bonus-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="46218-196">a.</span><span class="sxs-lookup"><span data-stu-id="46218-196">a.</span></span> <span data-ttu-id="46218-197">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="46218-197">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="46218-198">b.</span><span class="sxs-lookup"><span data-stu-id="46218-198">b.</span></span> <span data-ttu-id="46218-199">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="46218-199">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="46218-200">c.</span><span class="sxs-lookup"><span data-stu-id="46218-200">c.</span></span> <span data-ttu-id="46218-201">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="46218-201">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="46218-202">d.</span><span class="sxs-lookup"><span data-stu-id="46218-202">d.</span></span> <span data-ttu-id="46218-203">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="46218-203">Click **Create**.</span></span>
 
### <a name="create-a-bonusly-test-user"></a><span data-ttu-id="46218-204">建立 Bonusly 測試使用者</span><span class="sxs-lookup"><span data-stu-id="46218-204">Create a Bonusly test user</span></span>

<span data-ttu-id="46218-205">在訂單 tooenable Azure AD 使用者 toolog tooBonusly 中，您必須是佈建到 Bonusly。</span><span class="sxs-lookup"><span data-stu-id="46218-205">In order tooenable Azure AD users toolog in tooBonusly, they must be provisioned into Bonusly.</span></span> <span data-ttu-id="46218-206">中的 Bonusly hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="46218-206">In hello case of Bonusly, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="46218-207">您可以使用任何其他 Bonusly 使用者帳戶建立工具或 Api 提供 Bonusly tooprovision AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="46218-207">You can use any other Bonusly user account creation tools or APIs provided by Bonusly tooprovision AAD user accounts.</span></span>
>  

<span data-ttu-id="46218-208">**tooconfigure 使用者佈建，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="46218-208">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="46218-209">在網頁瀏覽器視窗中，登入 tooyour Bonusly 租用戶。</span><span class="sxs-lookup"><span data-stu-id="46218-209">In a web browser window, log in tooyour Bonusly tenant.</span></span>

2. <span data-ttu-id="46218-210">按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="46218-210">Click **Settings**.</span></span>
 
    <span data-ttu-id="46218-211">![設定](./media/active-directory-saas-bonus-tutorial/ic781041.png "設定")</span><span class="sxs-lookup"><span data-stu-id="46218-211">![Settings](./media/active-directory-saas-bonus-tutorial/ic781041.png "Settings")</span></span>

3. <span data-ttu-id="46218-212">按一下 hello**使用者和加分** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="46218-212">Click hello **Users and bonuses** tab.</span></span>
   
    <span data-ttu-id="46218-213">![使用者和獎勵](./media/active-directory-saas-bonus-tutorial/ic781042.png "使用者和獎勵")</span><span class="sxs-lookup"><span data-stu-id="46218-213">![Users and bonuses](./media/active-directory-saas-bonus-tutorial/ic781042.png "Users and bonuses")</span></span>

4. <span data-ttu-id="46218-214">按一下 [管理使用者] 。</span><span class="sxs-lookup"><span data-stu-id="46218-214">Click **Manage Users**.</span></span>
   
    <span data-ttu-id="46218-215">![管理使用者](./media/active-directory-saas-bonus-tutorial/ic781043.png "管理使用者")</span><span class="sxs-lookup"><span data-stu-id="46218-215">![Manage Users](./media/active-directory-saas-bonus-tutorial/ic781043.png "Manage Users")</span></span>

5. <span data-ttu-id="46218-216">按一下 [加入使用者] 。</span><span class="sxs-lookup"><span data-stu-id="46218-216">Click **Add User**.</span></span>
   
    <span data-ttu-id="46218-217">![新增使用者](./media/active-directory-saas-bonus-tutorial/ic781044.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="46218-217">![Add User](./media/active-directory-saas-bonus-tutorial/ic781044.png "Add User")</span></span>

6. <span data-ttu-id="46218-218">在 [hello**新增使用者**] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="46218-218">On hello **Add User** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="46218-219">![新增使用者](./media/active-directory-saas-bonus-tutorial/ic781045.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="46218-219">![Add User](./media/active-directory-saas-bonus-tutorial/ic781045.png "Add User")</span></span>  

    <span data-ttu-id="46218-220">a.</span><span class="sxs-lookup"><span data-stu-id="46218-220">a.</span></span> <span data-ttu-id="46218-221">在 hello**名字**文字方塊中，輸入 hello 名字，例如使用者的**許**。</span><span class="sxs-lookup"><span data-stu-id="46218-221">In hello **First name** textbox, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="46218-222">b.</span><span class="sxs-lookup"><span data-stu-id="46218-222">b.</span></span> <span data-ttu-id="46218-223">在 hello**姓氏**文字方塊中，輸入 hello 姓氏的使用者，例如**Simon**。</span><span class="sxs-lookup"><span data-stu-id="46218-223">In hello **Last name** textbox, enter hello last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="46218-224">c.</span><span class="sxs-lookup"><span data-stu-id="46218-224">c.</span></span> <span data-ttu-id="46218-225">在 hello**電子郵件**文字方塊中，輸入 hello 電子郵件的使用者，例如 **brittasimon@contoso.com** 。</span><span class="sxs-lookup"><span data-stu-id="46218-225">In hello **Email** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="46218-226">d.</span><span class="sxs-lookup"><span data-stu-id="46218-226">d.</span></span> <span data-ttu-id="46218-227">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="46218-227">Click **Save**.</span></span>
   
     >[!NOTE]
     ><span data-ttu-id="46218-228">hello Azure AD 帳戶持有者會收到電子郵件，其中包含連結 tooconfirm hello 帳戶之前就會生效。</span><span class="sxs-lookup"><span data-stu-id="46218-228">hello Azure AD account holder receives an email that includes a link tooconfirm hello account before it becomes active.</span></span>
     >  

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="46218-229">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="46218-229">Assign hello Azure AD test user</span></span>

<span data-ttu-id="46218-230">在本節中，您可以授與存取 tooBonusly 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="46218-230">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBonusly.</span></span>

![指派 hello 使用者角色][200] 

<span data-ttu-id="46218-232">**tooassign 許 Simon tooBonusly，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="46218-232">**tooassign Britta Simon tooBonusly, perform hello following steps:**</span></span>

1. <span data-ttu-id="46218-233">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="46218-233">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="46218-235">在 [hello] 應用程式清單中，選取**Bonusly**。</span><span class="sxs-lookup"><span data-stu-id="46218-235">In hello applications list, select **Bonusly**.</span></span>

    ![hello Bonusly hello 應用程式清單中的連結](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_app.png) 

3. <span data-ttu-id="46218-237">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="46218-237">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello 「 使用者和群組 」 的連結][202] 

4. <span data-ttu-id="46218-239">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="46218-239">Click **Add** button.</span></span> <span data-ttu-id="46218-240">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="46218-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 將作業加入窗格][203]

5. <span data-ttu-id="46218-242">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="46218-242">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="46218-243">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="46218-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="46218-244">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="46218-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="46218-245">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="46218-245">Test single sign-on</span></span>

<span data-ttu-id="46218-246">hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="46218-246">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="46218-247">當您按一下 hello Bonusly 磚中的 hello 存取面板，您應該取得自動登入 tooyour Bonusly 應用程式。</span><span class="sxs-lookup"><span data-stu-id="46218-247">When you click hello Bonusly tile in hello Access Panel, you should get automatically signed-on tooyour Bonusly application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="46218-248">其他資源</span><span class="sxs-lookup"><span data-stu-id="46218-248">Additional resources</span></span>

* [<span data-ttu-id="46218-249">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="46218-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="46218-250">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="46218-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_203.png

