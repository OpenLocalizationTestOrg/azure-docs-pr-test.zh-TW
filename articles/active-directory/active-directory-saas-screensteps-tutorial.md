---
title: "教學課程：Azure Active Directory 與 ScreenSteps 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 ScreenSteps 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4563fe94-a88f-4895-a07f-79df44889cf9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: fd041e5fe4552727eeda2dabc1773d8043d410f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-screensteps"></a><span data-ttu-id="3a370-103">教學課程：Azure Active Directory 與 ScreenSteps 整合</span><span class="sxs-lookup"><span data-stu-id="3a370-103">Tutorial: Azure Active Directory integration with ScreenSteps</span></span>

<span data-ttu-id="3a370-104">在此教學課程中，您學會如何 toointegrate ScreenSteps 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="3a370-104">In this tutorial, you learn how toointegrate ScreenSteps with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3a370-105">整合 Azure AD 與 ScreenSteps 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="3a370-105">Integrating ScreenSteps with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3a370-106">您可以控制存取 tooScreenSteps Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="3a370-106">You can control in Azure AD who has access tooScreenSteps.</span></span>
- <span data-ttu-id="3a370-107">您可以啟用您的使用者 tooautomatically get 登入 tooScreenSteps （單一登入） 具有其 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="3a370-107">You can enable your users tooautomatically get signed-on tooScreenSteps (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="3a370-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="3a370-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="3a370-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="3a370-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3a370-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="3a370-110">Prerequisites</span></span>

<span data-ttu-id="3a370-111">tooconfigure Azure AD 與 ScreenSteps 的整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="3a370-111">tooconfigure Azure AD integration with ScreenSteps, you need hello following items:</span></span>

- <span data-ttu-id="3a370-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="3a370-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3a370-113">已啟用 ScreenSteps 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="3a370-113">A ScreenSteps single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3a370-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="3a370-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3a370-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="3a370-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3a370-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="3a370-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3a370-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="3a370-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3a370-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="3a370-118">Scenario description</span></span>
<span data-ttu-id="3a370-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3a370-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3a370-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="3a370-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3a370-121">從 hello 圖庫加入 ScreenSteps</span><span class="sxs-lookup"><span data-stu-id="3a370-121">Adding ScreenSteps from hello gallery</span></span>
2. <span data-ttu-id="3a370-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="3a370-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-screensteps-from-hello-gallery"></a><span data-ttu-id="3a370-123">從 hello 圖庫加入 ScreenSteps</span><span class="sxs-lookup"><span data-stu-id="3a370-123">Adding ScreenSteps from hello gallery</span></span>
<span data-ttu-id="3a370-124">tooconfigure hello 整合 ScreenSteps 的 Azure AD，您需要 tooadd ScreenSteps hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3a370-124">tooconfigure hello integration of ScreenSteps into Azure AD, you need tooadd ScreenSteps from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3a370-125">**tooadd ScreenSteps 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="3a370-125">**tooadd ScreenSteps from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3a370-126">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="3a370-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory] 按鈕][1]

2. <span data-ttu-id="3a370-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="3a370-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3a370-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="3a370-129">Then go too**All applications**.</span></span>

    ![hello 企業應用程式] 刀鋒視窗][2]
    
3. <span data-ttu-id="3a370-131">tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="3a370-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 新應用程式按鈕][3]

4. <span data-ttu-id="3a370-133">在 [hello] 搜尋方塊中，輸入**ScreenSteps**，選取**ScreenSteps**然後按一下 [從結果面板**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3a370-133">In hello search box, type **ScreenSteps**, select **ScreenSteps** from result panel then click **Add** button tooadd hello application.</span></span>

    ![ScreenSteps hello [結果] 清單中](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3a370-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="3a370-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="3a370-136">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 ScreenSteps 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3a370-136">In this section, you configure and test Azure AD single sign-on with ScreenSteps based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3a370-137">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 ScreenSteps 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="3a370-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ScreenSteps is tooa user in Azure AD.</span></span> <span data-ttu-id="3a370-138">換句話說，Azure AD 使用者與 ScreenSteps 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="3a370-138">In other words, a link relationship between an Azure AD user and hello related user in ScreenSteps needs toobe established.</span></span>

<span data-ttu-id="3a370-139">ScreenSteps 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="3a370-139">In ScreenSteps, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3a370-140">tooconfigure 及 Azure AD 單一登入與 ScreenSteps 的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="3a370-140">tooconfigure and test Azure AD single sign-on with ScreenSteps, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3a370-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="3a370-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3a370-142">**[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="3a370-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3a370-143">**[建立測試使用者 ScreenSteps](#create-a-screensteps-test-user) ** -toohave 許 Simon ScreenSteps 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="3a370-143">**[Create a ScreenSteps test user](#create-a-screensteps-test-user)** - toohave a counterpart of Britta Simon in ScreenSteps that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3a370-144">**[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3a370-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3a370-145">**[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="3a370-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="3a370-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="3a370-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="3a370-147">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 ScreenSteps 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="3a370-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ScreenSteps application.</span></span>

<span data-ttu-id="3a370-148">**tooconfigure Azure AD 單一登入與 ScreenSteps，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="3a370-148">**tooconfigure Azure AD single sign-on with ScreenSteps, perform hello following steps:**</span></span>

1. <span data-ttu-id="3a370-149">在 Azure 入口網站上 hello hello **ScreenSteps**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="3a370-149">In hello Azure portal, on hello **ScreenSteps** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="3a370-151">在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3a370-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_samlbase.png)

3. <span data-ttu-id="3a370-153">在 [hello **ScreenSteps 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="3a370-153">On hello **ScreenSteps Domain and URLs** section, perform hello following steps:</span></span>

    ![ScreenSteps 網域及 URL 單一登入資訊](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_url.png)

    <span data-ttu-id="3a370-155">在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<tenantname>.ScreenSteps.com`</span><span class="sxs-lookup"><span data-stu-id="3a370-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.ScreenSteps.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3a370-156">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="3a370-156">This value is not real.</span></span> <span data-ttu-id="3a370-157">更新此值以 hello 實際登入 URL，在本教學課程稍後會說明。</span><span class="sxs-lookup"><span data-stu-id="3a370-157">Update this value with hello actual Sign-On URL, which is explained later in this tutorial.</span></span> 

4. <span data-ttu-id="3a370-158">在 [hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="3a370-158">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![hello 憑證下載連結](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_certificate.png) 

5. <span data-ttu-id="3a370-160">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="3a370-160">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-screensteps-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3a370-162">在 [hello **ScreenSteps 組態**區段中，按一下**設定 ScreenSteps** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="3a370-162">On hello **ScreenSteps Configuration** section, click **Configure ScreenSteps** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="3a370-163">複製 hello**登出 URL 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="3a370-163">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![ScreenSteps 設定](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_configure.png) 

7. <span data-ttu-id="3a370-165">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 ScreenSteps 公司網站。</span><span class="sxs-lookup"><span data-stu-id="3a370-165">In a different web browser window, log into your ScreenSteps company site as an administrator.</span></span>

8. <span data-ttu-id="3a370-166">按一下 [帳戶設定]。</span><span class="sxs-lookup"><span data-stu-id="3a370-166">Click **Account Settings**.</span></span>

    <span data-ttu-id="3a370-167">![帳戶管理](./media/active-directory-saas-screensteps-tutorial/ic778523.png "帳戶管理")</span><span class="sxs-lookup"><span data-stu-id="3a370-167">![Account management](./media/active-directory-saas-screensteps-tutorial/ic778523.png "Account management")</span></span>

9. <span data-ttu-id="3a370-168">按一下 [單一登入] 。</span><span class="sxs-lookup"><span data-stu-id="3a370-168">Click **Single Sign-on**.</span></span>

    <span data-ttu-id="3a370-169">![遠端驗證](./media/active-directory-saas-screensteps-tutorial/ic778524.png "遠端驗證")</span><span class="sxs-lookup"><span data-stu-id="3a370-169">![Remote authentication](./media/active-directory-saas-screensteps-tutorial/ic778524.png "Remote authentication")</span></span>

10. <span data-ttu-id="3a370-170">按一下 [建立單一登入端點]。</span><span class="sxs-lookup"><span data-stu-id="3a370-170">Click **Create Single Sign-on Endpoint**.</span></span>

    <span data-ttu-id="3a370-171">![遠端驗證](./media/active-directory-saas-screensteps-tutorial/ic778525.png "遠端驗證")</span><span class="sxs-lookup"><span data-stu-id="3a370-171">![Remote authentication](./media/active-directory-saas-screensteps-tutorial/ic778525.png "Remote authentication")</span></span>

11. <span data-ttu-id="3a370-172">在 [hello**建立單一登入端點**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="3a370-172">In hello **Create Single Sign-on Endpoint** section, perform hello following steps:</span></span>

    <span data-ttu-id="3a370-173">![建立驗證端點](./media/active-directory-saas-screensteps-tutorial/ic778526.png "建立驗證端點")</span><span class="sxs-lookup"><span data-stu-id="3a370-173">![Create an authentication endpoint](./media/active-directory-saas-screensteps-tutorial/ic778526.png "Create an authentication endpoint")</span></span>
    
    <span data-ttu-id="3a370-174">a.</span><span class="sxs-lookup"><span data-stu-id="3a370-174">a.</span></span> <span data-ttu-id="3a370-175">在 [hello**標題**文字方塊中，輸入標題。</span><span class="sxs-lookup"><span data-stu-id="3a370-175">In hello **Title** textbox, type a title.</span></span>
    
    <span data-ttu-id="3a370-176">b.</span><span class="sxs-lookup"><span data-stu-id="3a370-176">b.</span></span> <span data-ttu-id="3a370-177">從 hello**模式**清單中，選取**SAML**。</span><span class="sxs-lookup"><span data-stu-id="3a370-177">From hello **Mode** list, select **SAML**.</span></span>
    
    <span data-ttu-id="3a370-178">c.</span><span class="sxs-lookup"><span data-stu-id="3a370-178">c.</span></span> <span data-ttu-id="3a370-179">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="3a370-179">Click **Create**.</span></span>

12. <span data-ttu-id="3a370-180">**編輯**hello 新端點。</span><span class="sxs-lookup"><span data-stu-id="3a370-180">**Edit** hello new endpoint.</span></span>

    <span data-ttu-id="3a370-181">![編輯端點](./media/active-directory-saas-screensteps-tutorial/ic778528.png "編輯端點")</span><span class="sxs-lookup"><span data-stu-id="3a370-181">![Edit endpoint](./media/active-directory-saas-screensteps-tutorial/ic778528.png "Edit endpoint")</span></span>

13. <span data-ttu-id="3a370-182">在 [hello**編輯單一登入端點**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="3a370-182">In hello **Edit Single Sign-on Endpoint** section, perform hello following steps:</span></span>

    <span data-ttu-id="3a370-183">![遠端驗證端點](./media/active-directory-saas-screensteps-tutorial/ic778527.png "遠端驗證端點")</span><span class="sxs-lookup"><span data-stu-id="3a370-183">![Remote authentication endpoint](./media/active-directory-saas-screensteps-tutorial/ic778527.png "Remote authentication endpoint")</span></span>

    <span data-ttu-id="3a370-184">a.</span><span class="sxs-lookup"><span data-stu-id="3a370-184">a.</span></span> <span data-ttu-id="3a370-185">按一下**上傳新的 SAML 憑證檔**，，然後上傳 hello 憑證，以便您從 Azure 入口網站下載。</span><span class="sxs-lookup"><span data-stu-id="3a370-185">Click **Upload new SAML Certificate file**, and then upload hello certificate, which you have downloaded from Azure portal.</span></span>
    
    <span data-ttu-id="3a370-186">b.</span><span class="sxs-lookup"><span data-stu-id="3a370-186">b.</span></span> <span data-ttu-id="3a370-187">貼上**SAML 單一登入服務 URL**值，您從 hello Azure 入口網站複製到 hello**遠端登入 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="3a370-187">Paste **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **Remote Login URL** textbox.</span></span>
    
    <span data-ttu-id="3a370-188">c.</span><span class="sxs-lookup"><span data-stu-id="3a370-188">c.</span></span> <span data-ttu-id="3a370-189">貼上**登出 URL**值，您從 hello Azure 入口網站複製到 hello**登出 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="3a370-189">Paste **Sign-Out URL** value, which you have copied from hello Azure portal into hello **Log out URL** textbox.</span></span>
    
    <span data-ttu-id="3a370-190">d.</span><span class="sxs-lookup"><span data-stu-id="3a370-190">d.</span></span> <span data-ttu-id="3a370-191">選取**群組**tooassign 使用者 toowhen 他們佈建。</span><span class="sxs-lookup"><span data-stu-id="3a370-191">Select a **Group** tooassign users toowhen they are provisioned.</span></span>
    
    <span data-ttu-id="3a370-192">e.</span><span class="sxs-lookup"><span data-stu-id="3a370-192">e.</span></span> <span data-ttu-id="3a370-193">按一下 [更新] 。</span><span class="sxs-lookup"><span data-stu-id="3a370-193">Click **Update**.</span></span>

    <span data-ttu-id="3a370-194">f.</span><span class="sxs-lookup"><span data-stu-id="3a370-194">f.</span></span> <span data-ttu-id="3a370-195">複製 hello **SAML 取用者 URL** toohello 剪貼簿並貼上 toohello**登入 URL** ] 文字方塊中的**ScreenSteps 網域和 Url** > 一節。</span><span class="sxs-lookup"><span data-stu-id="3a370-195">Copy hello **SAML Consumer URL** toohello clipboard and paste in toohello **Sign-on URL** textbox in **ScreenSteps Domain and URLs** section.</span></span>
    
    <span data-ttu-id="3a370-196">g.</span><span class="sxs-lookup"><span data-stu-id="3a370-196">g.</span></span> <span data-ttu-id="3a370-197">傳回 toohello**編輯單一登入端點**。</span><span class="sxs-lookup"><span data-stu-id="3a370-197">Return toohello **Edit Single Sign-on Endpoint**.</span></span>
    
    <span data-ttu-id="3a370-198">h.</span><span class="sxs-lookup"><span data-stu-id="3a370-198">h.</span></span> <span data-ttu-id="3a370-199">按一下 hello**設成預設值為帳戶**toouse 此端點的所有使用者登入 ScreenSteps] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3a370-199">Click hello **Make default for account** button toouse this endpoint for all users who log into ScreenSteps.</span></span> <span data-ttu-id="3a370-200">或者，您可以按一下 hello**新增 tooSite**按鈕中的特定網站的這個端點 toouse **ScreenSteps**。</span><span class="sxs-lookup"><span data-stu-id="3a370-200">Alternatively you can click hello **Add tooSite** button toouse this endpoint for specific sites in **ScreenSteps**.</span></span>

> [!TIP]
> <span data-ttu-id="3a370-201">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="3a370-201">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3a370-202">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="3a370-202">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3a370-203">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3a370-203">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3a370-204">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="3a370-204">Create an Azure AD test user</span></span>

<span data-ttu-id="3a370-205">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="3a370-205">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="3a370-207">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="3a370-207">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3a370-208">在 [hello Azure 入口網站，hello 左窗格中，按一下 [hello **Azure Active Directory** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3a370-208">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory] 按鈕](./media/active-directory-saas-screensteps-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="3a370-210">toodisplay hello 使用者清單，請移過**使用者和群組**，然後按一下 [**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="3a370-210">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-screensteps-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="3a370-212">tooopen hello**使用者**對話方塊中，按一下 [**新增**頂端的 hello hello**所有使用者**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="3a370-212">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello [新增] 按鈕](./media/active-directory-saas-screensteps-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="3a370-214">在 [hello**使用者**對話方塊方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="3a370-214">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello [使用者] 對話方塊](./media/active-directory-saas-screensteps-tutorial/create_aaduser_04.png)

    <span data-ttu-id="3a370-216">a.</span><span class="sxs-lookup"><span data-stu-id="3a370-216">a.</span></span> <span data-ttu-id="3a370-217">在 [hello**名稱**方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="3a370-217">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3a370-218">b.</span><span class="sxs-lookup"><span data-stu-id="3a370-218">b.</span></span> <span data-ttu-id="3a370-219">在 [hello**使用者名**方塊中，使用者許 Simon 類型 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="3a370-219">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="3a370-220">c.</span><span class="sxs-lookup"><span data-stu-id="3a370-220">c.</span></span> <span data-ttu-id="3a370-221">選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 [hello**密碼**方塊。</span><span class="sxs-lookup"><span data-stu-id="3a370-221">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="3a370-222">d.</span><span class="sxs-lookup"><span data-stu-id="3a370-222">d.</span></span> <span data-ttu-id="3a370-223">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="3a370-223">Click **Create**.</span></span>
 
### <a name="create-a-screensteps-test-user"></a><span data-ttu-id="3a370-224">建立 ScreenSteps 測試使用者</span><span class="sxs-lookup"><span data-stu-id="3a370-224">Create a ScreenSteps test user</span></span>

<span data-ttu-id="3a370-225">在本節中，您要在 ScreenSteps 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="3a370-225">In this section, you create a user called Britta Simon in ScreenSteps.</span></span> <span data-ttu-id="3a370-226">使用[ScreenSteps 用戶端支援小組](https://www.screensteps.com/contact)hello ScreenSteps 平台中新增 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="3a370-226">Work with [ScreenSteps Client support team](https://www.screensteps.com/contact) to add hello users in hello ScreenSteps platform.</span></span> <span data-ttu-id="3a370-227">您必須先建立和啟動使用者，然後才能使用單一登入。</span><span class="sxs-lookup"><span data-stu-id="3a370-227">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="3a370-228">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="3a370-228">Assign hello Azure AD test user</span></span>

<span data-ttu-id="3a370-229">在本節中，您可以授與存取 tooScreenSteps 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3a370-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooScreenSteps.</span></span>

![指派 hello 使用者角色][200] 

<span data-ttu-id="3a370-231">**tooassign 許 Simon tooScreenSteps，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="3a370-231">**tooassign Britta Simon tooScreenSteps, perform hello following steps:**</span></span>

1. <span data-ttu-id="3a370-232">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="3a370-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="3a370-234">在 [hello] 應用程式清單中，選取**ScreenSteps**。</span><span class="sxs-lookup"><span data-stu-id="3a370-234">In hello applications list, select **ScreenSteps**.</span></span>

    ![hello 應用程式清單中的 hello ScreenSteps 連結](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_app.png)  

3. <span data-ttu-id="3a370-236">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="3a370-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello 「 使用者和群組 」 的連結][202]

4. <span data-ttu-id="3a370-238">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3a370-238">Click **Add** button.</span></span> <span data-ttu-id="3a370-239">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="3a370-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 將作業加入窗格][203]

5. <span data-ttu-id="3a370-241">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="3a370-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3a370-242">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3a370-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3a370-243">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3a370-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="3a370-244">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="3a370-244">Test single sign-on</span></span>

<span data-ttu-id="3a370-245">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="3a370-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3a370-246">當您按一下的 hello ScreenSteps 磚 hello 存取面板中時，您應該取得自動登入 tooyour ScreenSteps 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="3a370-246">When you click hello ScreenSteps tile in hello Access Panel, you should get automatically signed-on tooyour ScreenSteps application.</span></span>
<span data-ttu-id="3a370-247">如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="3a370-247">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3a370-248">其他資源</span><span class="sxs-lookup"><span data-stu-id="3a370-248">Additional resources</span></span>

* [<span data-ttu-id="3a370-249">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3a370-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3a370-250">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="3a370-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_203.png

