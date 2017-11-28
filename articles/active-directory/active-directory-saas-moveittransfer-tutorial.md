---
title: "教學課程：Azure Active Directory 與 MOVEit Transfer - Azure AD integration 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 之間 MOVEit 傳送-Azure AD 的整合。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8ff7102d-be73-4888-ae81-d8e3d01dd534
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 5bbe4f2d952bd45c4d58d55ffc3467b4eb871fd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moveit-transfer---azure-ad-integration"></a><span data-ttu-id="06368-103">教學課程：Azure Active Directory 與 MOVEit Transfer - Azure AD integration 整合</span><span class="sxs-lookup"><span data-stu-id="06368-103">Tutorial: Azure Active Directory integration with MOVEit Transfer - Azure AD integration</span></span>

<span data-ttu-id="06368-104">在此教學課程中，您學會如何 toointegrate MOVEit 傳送-Azure AD 與 Azure Active Directory (Azure AD) 整合。</span><span class="sxs-lookup"><span data-stu-id="06368-104">In this tutorial, you learn how toointegrate MOVEit Transfer - Azure AD integration with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="06368-105">整合 MOVEit 傳送-Azure AD 與 Azure AD 整合為您提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="06368-105">Integrating MOVEit Transfer - Azure AD integration with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="06368-106">您可以控制存取 tooMOVEit 傳送-Azure AD 整合 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="06368-106">You can control in Azure AD who has access tooMOVEit Transfer - Azure AD integration.</span></span>
- <span data-ttu-id="06368-107">您可以啟用您的使用者 tooautomatically get 登入 tooMOVEit 傳輸層使用其 Azure AD 帳戶的 Azure AD 整合 （單一登入）。</span><span class="sxs-lookup"><span data-stu-id="06368-107">You can enable your users tooautomatically get signed-on tooMOVEit Transfer - Azure AD integration (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="06368-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="06368-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="06368-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="06368-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="06368-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="06368-110">Prerequisites</span></span>

<span data-ttu-id="06368-111">tooconfigure MOVEit 傳送-Azure AD 整合與 Azure AD 整合您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="06368-111">tooconfigure Azure AD integration with MOVEit Transfer - Azure AD integration, you need hello following items:</span></span>

- <span data-ttu-id="06368-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="06368-112">An Azure AD subscription</span></span>
- <span data-ttu-id="06368-113">已啟用 MOVEit Transfer - Azure AD integration 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="06368-113">A MOVEit Transfer - Azure AD integration single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="06368-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="06368-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="06368-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="06368-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="06368-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="06368-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="06368-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="06368-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="06368-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="06368-118">Scenario description</span></span>
<span data-ttu-id="06368-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="06368-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="06368-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="06368-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="06368-121">加入 MOVEit 傳送-從 hello 組件庫的 Azure AD 整合</span><span class="sxs-lookup"><span data-stu-id="06368-121">Adding MOVEit Transfer - Azure AD integration from hello gallery</span></span>
2. <span data-ttu-id="06368-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="06368-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moveit-transfer---azure-ad-integration-from-hello-gallery"></a><span data-ttu-id="06368-123">加入 MOVEit 傳送-從 hello 組件庫的 Azure AD 整合</span><span class="sxs-lookup"><span data-stu-id="06368-123">Adding MOVEit Transfer - Azure AD integration from hello gallery</span></span>
<span data-ttu-id="06368-124">tooconfigure hello 整合 MOVEit 傳送-Azure AD 整合到 Azure AD，您需要 tooadd MOVEit 傳送-hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式的 Azure AD 整合。</span><span class="sxs-lookup"><span data-stu-id="06368-124">tooconfigure hello integration of MOVEit Transfer - Azure AD integration into Azure AD, you need tooadd MOVEit Transfer - Azure AD integration from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="06368-125">**tooadd MOVEit 傳送-Azure AD 整合，從 hello 組件庫，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="06368-125">**tooadd MOVEit Transfer - Azure AD integration from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="06368-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="06368-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 按鈕][1]

2. <span data-ttu-id="06368-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="06368-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="06368-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="06368-129">Then go too**All applications**.</span></span>

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. <span data-ttu-id="06368-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="06368-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 新應用程式按鈕][3]

4. <span data-ttu-id="06368-133">在 hello 搜尋方塊中，輸入**MOVEit 傳送-Azure AD 整合**，選取**MOVEit 傳送-Azure AD 整合**然後按一下 從結果面板**新增**按鈕 tooadd hello應用程式。</span><span class="sxs-lookup"><span data-stu-id="06368-133">In hello search box, type **MOVEit Transfer - Azure AD integration**, select **MOVEit Transfer - Azure AD integration** from result panel then click **Add** button tooadd hello application.</span></span>

    ![MOVEit 傳送-hello [結果] 清單中的 Azure AD 整合](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="06368-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="06368-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="06368-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 MOVEit Transfer - Azure AD integration 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="06368-136">In this section, you configure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="06368-137">針對單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者 MOVEit 傳輸-Azure AD 整合 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="06368-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in MOVEit Transfer - Azure AD integration is tooa user in Azure AD.</span></span> <span data-ttu-id="06368-138">換句話說，Azure AD 使用者與 hello MOVEit 傳輸層的相關的使用者之間的連結關聯性 Azure AD 的整合需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="06368-138">In other words, a link relationship between an Azure AD user and hello related user in MOVEit Transfer - Azure AD integration needs toobe established.</span></span>

<span data-ttu-id="06368-139">在 MOVEit 傳送-Azure AD 整合，將指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="06368-139">In MOVEit Transfer - Azure AD integration, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="06368-140">tooconfigure 和測試 Azure AD 單一登入與 MOVEit 傳送-Azure AD 整合，您需要遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="06368-140">tooconfigure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="06368-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="06368-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="06368-142">**[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="06368-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="06368-143">**[建立 MOVEit 傳送-Azure AD 整合測試使用者](#create-a-moveit-transfer---azure-ad-integration-test-user)** -toohave 許 Simon MOVEit 傳輸對應項目-Azure AD 整合的使用者連結的 toohello Azure AD 表示。</span><span class="sxs-lookup"><span data-stu-id="06368-143">**[Create a MOVEit Transfer - Azure AD integration test user](#create-a-moveit-transfer---azure-ad-integration-test-user)** - toohave a counterpart of Britta Simon in MOVEit Transfer - Azure AD integration that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="06368-144">**[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="06368-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="06368-145">**[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="06368-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="06368-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="06368-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="06368-147">在本節中，您啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入您 MOVEit 傳送-Azure AD 整合的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="06368-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your MOVEit Transfer - Azure AD integration application.</span></span>

<span data-ttu-id="06368-148">**tooconfigure Azure AD 單一登入 MOVEit 傳送-Azure AD 整合，以執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="06368-148">**tooconfigure Azure AD single sign-on with MOVEit Transfer - Azure AD integration, perform hello following steps:**</span></span>

1. <span data-ttu-id="06368-149">在 Azure 入口網站上 hello hello **MOVEit 傳送-Azure AD 整合**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="06368-149">In hello Azure portal, on hello **MOVEit Transfer - Azure AD integration** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="06368-151">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="06368-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_samlbase.png)

3. <span data-ttu-id="06368-153">在 hello **MOVEit 傳送-Azure AD 整合網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="06368-153">On hello **MOVEit Transfer - Azure AD integration Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_url.png)

    <span data-ttu-id="06368-155">a.</span><span class="sxs-lookup"><span data-stu-id="06368-155">a.</span></span> <span data-ttu-id="06368-156">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://contoso.com`</span><span class="sxs-lookup"><span data-stu-id="06368-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://contoso.com`</span></span>

    <span data-ttu-id="06368-157">b.</span><span class="sxs-lookup"><span data-stu-id="06368-157">b.</span></span> <span data-ttu-id="06368-158">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://contoso.com/<tenatid>`</span><span class="sxs-lookup"><span data-stu-id="06368-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://contoso.com/<tenatid>`</span></span>

    <span data-ttu-id="06368-159">c.</span><span class="sxs-lookup"><span data-stu-id="06368-159">c.</span></span> <span data-ttu-id="06368-160">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`</span><span class="sxs-lookup"><span data-stu-id="06368-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`</span></span>    
     
    > [!NOTE] 
    > <span data-ttu-id="06368-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="06368-161">These values are not real.</span></span> <span data-ttu-id="06368-162">更新這些值與實際的 hello，識別項、 回覆 URL 和登入 URL。</span><span class="sxs-lookup"><span data-stu-id="06368-162">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="06368-163">您可以參考這些值稍後在**服務提供者中繼資料 URL**區段或連絡人[MOVEit 傳送-Azure AD 整合用戶端支援小組](https://community.ipswitch.com/s/support)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="06368-163">You can refer these values later in **Service Provider Metadata URL** section or contact [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support) tooget these values.</span></span>

4. <span data-ttu-id="06368-164">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="06368-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![hello 憑證下載連結](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_certificate.png) 

5. <span data-ttu-id="06368-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="06368-166">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="06368-168">登入 tooyour MOVEit 傳輸租用戶系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="06368-168">Sign on tooyour MOVEit Transfer tenant as an administrator.</span></span>

7. <span data-ttu-id="06368-169">在 hello 左側瀏覽窗格中，按一下 **設定**。</span><span class="sxs-lookup"><span data-stu-id="06368-169">On hello left navigation pane, click **Settings**.</span></span>

    ![應用程式端上的設定區段](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_000.png)

8. <span data-ttu-id="06368-171">按一下 [單一登入] 連結，其位於 [安全性原則] -> [使用者驗證] 下。</span><span class="sxs-lookup"><span data-stu-id="06368-171">Click **Single Signon** link, which is under **Security Policies -> User Auth**.</span></span>

    ![應用程式端上的安全性原則](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_001.png)

9. <span data-ttu-id="06368-173">按一下 hello 中繼資料 URL 連結 toodownload hello 中繼資料文件。</span><span class="sxs-lookup"><span data-stu-id="06368-173">Click hello Metadata URL link toodownload hello metadata document.</span></span>

    ![服務提供者中繼資料 URL](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_002.png)
    
    * <span data-ttu-id="06368-175">確認**entityID**符合**識別碼**在 hello **MOVEit 傳送-Azure AD 整合網域和 Url** > 一節。</span><span class="sxs-lookup"><span data-stu-id="06368-175">Verify **entityID** matches **Identifier** in hello **MOVEit Transfer - Azure AD integration Domain and URLs** section .</span></span>
    * <span data-ttu-id="06368-176">確認**AssertionConsumerService**位置 URL 符合**回覆 URL**在 hello **MOVEit 傳送-Azure AD 整合網域和 Url** > 一節。</span><span class="sxs-lookup"><span data-stu-id="06368-176">Verify **AssertionConsumerService** Location URL matches **REPLY URL** in hello **MOVEit Transfer - Azure AD integration Domain and URLs** section.</span></span>
    
    ![在應用程式端設定單一登入](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_007.png)

10. <span data-ttu-id="06368-178">按一下**新增身分識別提供者**按鈕 tooadd 新的同盟身分識別提供者。</span><span class="sxs-lookup"><span data-stu-id="06368-178">Click **Add Identity Provider** button tooadd a new Federated Identity Provider.</span></span>

    ![新增識別提供者](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_003.png)

11. <span data-ttu-id="06368-180">按一下**瀏覽...** tooselect hello 您從 Azure 入口網站下載的中繼資料檔案，然後按一下 **新增身分識別提供者**tooupload hello 下載檔案。</span><span class="sxs-lookup"><span data-stu-id="06368-180">Click **Browse...** tooselect hello metadata file which you downloaded from Azure portal, then click **Add Identity Provider** tooupload hello downloaded file.</span></span>

    ![SAML 識別提供者](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_004.png)

12. <span data-ttu-id="06368-182">選取 「**是**"做為**啟用**在 hello**編輯同盟身分識別提供者設定...**頁面上，按一下 **儲存**。</span><span class="sxs-lookup"><span data-stu-id="06368-182">Select "**Yes**" as **Enabled** in hello **Edit Federated Identity Provider Settings...** page and click **Save**.</span></span>

    ![同盟識別提供者設定](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_005.png)

13. <span data-ttu-id="06368-184">在 hello**編輯同盟身分識別提供者使用者設定**頁面上，執行下列動作的 hello:</span><span class="sxs-lookup"><span data-stu-id="06368-184">In hello **Edit Federated Identity Provider User Settings** page, perform hello following actions:</span></span>
    
    ![編輯同盟識別提供者設定](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_006.png)
    
    <span data-ttu-id="06368-186">a.</span><span class="sxs-lookup"><span data-stu-id="06368-186">a.</span></span> <span data-ttu-id="06368-187">選取 [SAML NameID] 做為 [登入名稱]。</span><span class="sxs-lookup"><span data-stu-id="06368-187">Select **SAML NameID** as **Login name**.</span></span>
    
    <span data-ttu-id="06368-188">b.</span><span class="sxs-lookup"><span data-stu-id="06368-188">b.</span></span> <span data-ttu-id="06368-189">選取**其他**為**全名**在 hello**屬性名稱**文字方塊中放置 hello 值： `http://schemas.microsoft.com/identity/claims/displayname`。</span><span class="sxs-lookup"><span data-stu-id="06368-189">Select **Other** as **Full name** and in hello **Attribute name** textbox put hello value: `http://schemas.microsoft.com/identity/claims/displayname`.</span></span>
    
    <span data-ttu-id="06368-190">c.</span><span class="sxs-lookup"><span data-stu-id="06368-190">c.</span></span> <span data-ttu-id="06368-191">選取**其他**為**電子郵件**在 hello**屬性名稱**文字方塊中放置 hello 值： `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`。</span><span class="sxs-lookup"><span data-stu-id="06368-191">Select **Other** as **Email** and in hello **Attribute name** textbox put hello value: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
    
    <span data-ttu-id="06368-192">d.</span><span class="sxs-lookup"><span data-stu-id="06368-192">d.</span></span> <span data-ttu-id="06368-193">選取 [是] 做為 [在登入時自動建立帳戶]。</span><span class="sxs-lookup"><span data-stu-id="06368-193">Select **Yes** as **Auto-create account on signon**.</span></span>
    
    <span data-ttu-id="06368-194">e.</span><span class="sxs-lookup"><span data-stu-id="06368-194">e.</span></span> <span data-ttu-id="06368-195">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="06368-195">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="06368-196">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="06368-196">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="06368-197">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="06368-197">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="06368-198">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="06368-198">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="06368-199">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="06368-199">Create an Azure AD test user</span></span>

<span data-ttu-id="06368-200">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="06368-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="06368-202">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="06368-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="06368-203">在 hello Azure 入口網站，hello 左窗格中，按一下 hello **Azure Active Directory**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="06368-203">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="06368-205">toodisplay hello 使用者清單，請移過**使用者和群組**，然後按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="06368-205">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="06368-207">tooopen hello**使用者**對話方塊中，按一下 [**新增**頂端的 hello hello**所有使用者**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="06368-207">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello [新增] 按鈕](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="06368-209">在 hello**使用者**對話方塊方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="06368-209">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello [使用者] 對話方塊](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_04.png)

    <span data-ttu-id="06368-211">a.</span><span class="sxs-lookup"><span data-stu-id="06368-211">a.</span></span> <span data-ttu-id="06368-212">在 hello**名稱**方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="06368-212">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="06368-213">b.</span><span class="sxs-lookup"><span data-stu-id="06368-213">b.</span></span> <span data-ttu-id="06368-214">在 hello**使用者名**方塊中，使用者許 Simon 類型 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="06368-214">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="06368-215">c.</span><span class="sxs-lookup"><span data-stu-id="06368-215">c.</span></span> <span data-ttu-id="06368-216">選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 hello**密碼**方塊。</span><span class="sxs-lookup"><span data-stu-id="06368-216">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="06368-217">d.</span><span class="sxs-lookup"><span data-stu-id="06368-217">d.</span></span> <span data-ttu-id="06368-218">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="06368-218">Click **Create**.</span></span>
 
### <a name="create-a-moveit-transfer---azure-ad-integration-test-user"></a><span data-ttu-id="06368-219">建立 MOVEit Transfer - Azure AD integration 測試使用者</span><span class="sxs-lookup"><span data-stu-id="06368-219">Create a MOVEit Transfer - Azure AD integration test user</span></span>

<span data-ttu-id="06368-220">hello 本節目標在於 toocreate 呼叫許 Simon MOVEit 傳輸-Azure AD 整合的使用者。</span><span class="sxs-lookup"><span data-stu-id="06368-220">hello objective of this section is toocreate a user called Britta Simon in MOVEit Transfer - Azure AD integration.</span></span> <span data-ttu-id="06368-221">MOVEit Transfer - Azure AD integration 支援您已啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="06368-221">MOVEit Transfer - Azure AD integration supports just-in-time provisioning, which you have enabled.</span></span> <span data-ttu-id="06368-222">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="06368-222">There is no action item for you in this section.</span></span> <span data-ttu-id="06368-223">嘗試 tooaccess MOVEit 轉移-如果不存在的 Azure AD 整合期間，會建立新的使用者。</span><span class="sxs-lookup"><span data-stu-id="06368-223">A new user is created during an attempt tooaccess MOVEit Transfer - Azure AD integration if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="06368-224">若要手動 toocreate 使用者，您需要 toocontact hello [MOVEit 傳送-Azure AD 整合用戶端支援小組](https://community.ipswitch.com/s/support)。</span><span class="sxs-lookup"><span data-stu-id="06368-224">If you need toocreate a user manually, you need toocontact hello [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="06368-225">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="06368-225">Assign hello Azure AD test user</span></span>

<span data-ttu-id="06368-226">在本節中，以啟用許 Simon toouse Azure 單一登入授與存取 tooMOVEit 傳送-Azure AD 的整合。</span><span class="sxs-lookup"><span data-stu-id="06368-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMOVEit Transfer - Azure AD integration.</span></span>

![指派 hello 使用者角色][200] 

<span data-ttu-id="06368-228">**tooassign 許 Simon tooMOVEit 傳送-Azure AD 整合，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="06368-228">**tooassign Britta Simon tooMOVEit Transfer - Azure AD integration, perform hello following steps:**</span></span>

1. <span data-ttu-id="06368-229">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="06368-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="06368-231">在 [hello] 應用程式清單中，選取**MOVEit 傳送-Azure AD 整合**。</span><span class="sxs-lookup"><span data-stu-id="06368-231">In hello applications list, select **MOVEit Transfer - Azure AD integration**.</span></span>

    ![hello MOVEit 傳送-連結 hello 應用程式清單中的 Azure AD 整合](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_app.png)  

3. <span data-ttu-id="06368-233">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="06368-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello 「 使用者和群組 」 的連結][202]

4. <span data-ttu-id="06368-235">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="06368-235">Click **Add** button.</span></span> <span data-ttu-id="06368-236">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="06368-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 將作業加入窗格][203]

5. <span data-ttu-id="06368-238">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="06368-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="06368-239">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="06368-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="06368-240">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="06368-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="06368-241">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="06368-241">Test single sign-on</span></span>

<span data-ttu-id="06368-242">hello 本節目標在於 tootest 您 Azure AD 的 SSO 組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="06368-242">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="06368-243">當您按一下 hello MOVEit 傳送-Azure AD 整合圖格在 hello 存取面板，您應該取得自動登入 tooyour MOVEit 傳送-Azure AD 整合的應用程式。</span><span class="sxs-lookup"><span data-stu-id="06368-243">When you click hello MOVEit Transfer - Azure AD integration tile in hello Access Panel, you should get automatically signed-on tooyour MOVEit Transfer - Azure AD integration application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="06368-244">其他資源</span><span class="sxs-lookup"><span data-stu-id="06368-244">Additional resources</span></span>

* [<span data-ttu-id="06368-245">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="06368-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="06368-246">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="06368-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_203.png

