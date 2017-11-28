---
title: "教學課程：Azure Active Directory 與 Voyance 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Voyance 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 539dc1f9-64c9-4dce-b259-2b0b49dcf857
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2017
ms.author: jeedes
ms.openlocfilehash: e2cb9eb6b20e8611a9f6e8529b7c85a8d86ec3e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-voyance"></a><span data-ttu-id="9a7f5-103">教學課程：Azure Active Directory 與 Voyance 整合</span><span class="sxs-lookup"><span data-stu-id="9a7f5-103">Tutorial: Azure Active Directory integration with Voyance</span></span>

<span data-ttu-id="9a7f5-104">在此教學課程中，您學會如何 toointegrate Voyance 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-104">In this tutorial, you learn how toointegrate Voyance with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9a7f5-105">與 Azure AD 整合 Voyance 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="9a7f5-105">Integrating Voyance with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9a7f5-106">您可以控制存取 tooVoyance Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="9a7f5-106">You can control in Azure AD who has access tooVoyance</span></span>
- <span data-ttu-id="9a7f5-107">您可以啟用您的使用者 tooautomatically get 登入 tooVoyance （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="9a7f5-107">You can enable your users tooautomatically get signed-on tooVoyance (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9a7f5-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="9a7f5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9a7f5-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a7f5-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="9a7f5-110">Prerequisites</span></span>

<span data-ttu-id="9a7f5-111">tooconfigure Voyance 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="9a7f5-111">tooconfigure Azure AD integration with Voyance, you need hello following items:</span></span>

- <span data-ttu-id="9a7f5-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="9a7f5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9a7f5-113">已啟用 Voyance 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="9a7f5-113">A Voyance single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9a7f5-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9a7f5-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="9a7f5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9a7f5-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9a7f5-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9a7f5-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="9a7f5-118">Scenario description</span></span>
<span data-ttu-id="9a7f5-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9a7f5-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="9a7f5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9a7f5-121">從 hello 圖庫加入 Voyance</span><span class="sxs-lookup"><span data-stu-id="9a7f5-121">Adding Voyance from hello gallery</span></span>
2. <span data-ttu-id="9a7f5-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="9a7f5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-voyance-from-hello-gallery"></a><span data-ttu-id="9a7f5-123">從 hello 圖庫加入 Voyance</span><span class="sxs-lookup"><span data-stu-id="9a7f5-123">Adding Voyance from hello gallery</span></span>
<span data-ttu-id="9a7f5-124">tooconfigure hello 整合 Voyance 到 Azure AD，您需要 tooadd Voyance hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-124">tooconfigure hello integration of Voyance into Azure AD, you need tooadd Voyance from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9a7f5-125">**tooadd Voyance 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="9a7f5-125">**tooadd Voyance from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9a7f5-126">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory] 按鈕][1]

2. <span data-ttu-id="9a7f5-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9a7f5-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-129">Then go too**All applications**.</span></span>

    ![hello 企業應用程式] 刀鋒視窗][2]
    
3. <span data-ttu-id="9a7f5-131">tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 新應用程式按鈕][3]

4. <span data-ttu-id="9a7f5-133">在 [hello] 搜尋方塊中，輸入**Voyance**，選取**Voyance**然後按一下 [從結果面板**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-133">In hello search box, type **Voyance**, select  **Voyance**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Voyance hello [結果] 清單中](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9a7f5-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="9a7f5-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="9a7f5-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Voyance 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-136">In this section, you configure and test Azure AD single sign-on with Voyance based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9a7f5-137">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Voyance 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Voyance is tooa user in Azure AD.</span></span> <span data-ttu-id="9a7f5-138">換句話說，Azure AD 使用者與 hello Voyance 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-138">In other words, a link relationship between an Azure AD user and hello related user in Voyance needs toobe established.</span></span>

<span data-ttu-id="9a7f5-139">Voyance 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-139">In Voyance, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9a7f5-140">tooconfigure 及 Voyance 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="9a7f5-140">tooconfigure and test Azure AD single sign-on with Voyance, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9a7f5-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9a7f5-142">**[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9a7f5-143">**[建立測試使用者 Voyance](#create-a-voyance-test-user) ** -toohave 許 Simon Voyance 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-143">**[Create a Voyance test user](#create-a-voyance-test-user)** - toohave a counterpart of Britta Simon in Voyance that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9a7f5-144">**[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9a7f5-145">**[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9a7f5-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="9a7f5-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="9a7f5-147">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Voyance 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Voyance application.</span></span>

<span data-ttu-id="9a7f5-148">**tooconfigure Azure AD 單一登入與 Voyance，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="9a7f5-148">**tooconfigure Azure AD single sign-on with Voyance, perform hello following steps:**</span></span>

1. <span data-ttu-id="9a7f5-149">在 Azure 入口網站上 hello hello **Voyance**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-149">In hello Azure portal, on hello **Voyance** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="9a7f5-151">在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_samlbase.png)

3. <span data-ttu-id="9a7f5-153">在 [hello **Voyance 網域和 Url**區段中，執行下列步驟，如果您想 tooconfigure hello 應用程式中的 hello **IDP**初始模式：</span><span class="sxs-lookup"><span data-stu-id="9a7f5-153">On hello **Voyance Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![IDP 的 Voyance 網域和 URL 單一登入資訊](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url1.png)

    <span data-ttu-id="9a7f5-155">a.</span><span class="sxs-lookup"><span data-stu-id="9a7f5-155">a.</span></span> <span data-ttu-id="9a7f5-156">在 [hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.nyansa.com`</span><span class="sxs-lookup"><span data-stu-id="9a7f5-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.nyansa.com`</span></span>

    <span data-ttu-id="9a7f5-157">b.</span><span class="sxs-lookup"><span data-stu-id="9a7f5-157">b.</span></span> <span data-ttu-id="9a7f5-158">在 [hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.nyansa.com/saml/create/`</span><span class="sxs-lookup"><span data-stu-id="9a7f5-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.nyansa.com/saml/create/`</span></span>

4. <span data-ttu-id="9a7f5-159">請檢查**顯示進階的 URL 設定**並執行下列步驟，如果您想 tooconfigure hello 應用程式中的 hello **SP**初始模式：</span><span class="sxs-lookup"><span data-stu-id="9a7f5-159">Check **Show advanced URL settings** and perform hello following step if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![SP 的 Voyance 網域和 URL 單一登入資訊](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url2.png)

    <span data-ttu-id="9a7f5-161">在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.nyansa.com/`</span><span class="sxs-lookup"><span data-stu-id="9a7f5-161">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.nyansa.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="9a7f5-162">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-162">These values are not real.</span></span> <span data-ttu-id="9a7f5-163">更新這些值與實際的 hello，識別項、 回覆 URL 和登入 URL。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-163">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="9a7f5-164">請連絡[Voyance 用戶端支援小組](mailto:support@nyansa.com)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-164">Contact [Voyance Client support team](mailto:support@nyansa.com) tooget these values.</span></span> 

5. <span data-ttu-id="9a7f5-165">在 [hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-165">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![hello 憑證下載連結](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_certificate.png) 

6. <span data-ttu-id="9a7f5-167">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-167">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-voyance-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="9a7f5-169">在 [hello **Voyance 組態**區段中，按一下**設定 Voyance** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-169">On hello **Voyance Configuration** section, click **Configure Voyance** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9a7f5-170">複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="9a7f5-170">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Voyance 組態](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_configure.png) 

8. <span data-ttu-id="9a7f5-172">在不同的網頁瀏覽器視窗中，以系統管理員身分登入 tooyour Voyance 租用戶。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-172">In a different web browser window, sign-on tooyour Voyance tenant as an administrator.</span></span>

9. <span data-ttu-id="9a7f5-173">移 toohello 右上角的 hello 巡覽列，然後按一下 [hello] 下拉式清單，指出 「**Acme 大學**"。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-173">Go toohello top right corner of hello navigation bar and click on hello drop-down that says "**Acme University**".</span></span>
    
    ![在應用程式端設定單一登入 Acme 大學](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_001.png) 

10. <span data-ttu-id="9a7f5-175">按一下 [系統管理員設定]。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-175">Click "**Admin Settings**".</span></span>

    ![在應用程式端設定單一登入 系統管理員設定](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_002.png)

11. <span data-ttu-id="9a7f5-177">按一下 [使用者存取] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-177">Click "**User Access**" tab.</span></span>

    ![在應用程式端設定單一登入 使用者存取](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_003.png)

12. <span data-ttu-id="9a7f5-179">按一下 hello"**已停用 SSO**」 按鈕 tooconfigure Azure AD 使用 SAML 2.0 IdP 身分。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-179">Click hello "**SSO is disabled**" button tooconfigure Azure AD as an IdP using SAML 2.0.</span></span>

    ![在應用程式端設定單一登入 [SSO 已停用] 按鈕](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_004.png)

13. <span data-ttu-id="9a7f5-181">跳過**SAML v2**區段，然後執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9a7f5-181">Go too**SAML v2** section and perform below steps:</span></span>

    ![在應用程式端設定單一登入 SAML v2](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_005.png)
    
    <span data-ttu-id="9a7f5-183">a.</span><span class="sxs-lookup"><span data-stu-id="9a7f5-183">a.</span></span> <span data-ttu-id="9a7f5-184">選取 [啟用] 。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-184">Select **Enabled**.</span></span>
    
    <span data-ttu-id="9a7f5-185">b.</span><span class="sxs-lookup"><span data-stu-id="9a7f5-185">b.</span></span> <span data-ttu-id="9a7f5-186">貼上**SAML 單一登入服務 URL**，其中您從 hello Azure 入口網站複製到 hello **IdP 登入 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-186">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal Into hello **IdP Login URL** textbox.</span></span>

    <span data-ttu-id="9a7f5-187">c.</span><span class="sxs-lookup"><span data-stu-id="9a7f5-187">c.</span></span> <span data-ttu-id="9a7f5-188">在 [記事本]，複製到剪貼簿，其內容的 hello 中開啟下載的 Base64 編碼憑證，然後將它貼入 toohello **IdP 憑證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-188">Open your downloaded Base64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **IdP Cert** textbox.</span></span>
    
    <span data-ttu-id="9a7f5-189">d.</span><span class="sxs-lookup"><span data-stu-id="9a7f5-189">d.</span></span> <span data-ttu-id="9a7f5-190">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="9a7f5-191">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="9a7f5-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9a7f5-192">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9a7f5-193">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9a7f5-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9a7f5-194">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="9a7f5-194">Create an Azure AD test user</span></span>

<span data-ttu-id="9a7f5-195">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 測試使用者][100]

<span data-ttu-id="9a7f5-197">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="9a7f5-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9a7f5-198">在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-198">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![hello Azure Active Directory] 按鈕](./media/active-directory-saas-voyance-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9a7f5-200">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-200">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-voyance-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9a7f5-202">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-202">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![hello [新增] 按鈕](./media/active-directory-saas-voyance-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9a7f5-204">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="9a7f5-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![hello [使用者] 對話方塊](./media/active-directory-saas-voyance-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9a7f5-206">a.</span><span class="sxs-lookup"><span data-stu-id="9a7f5-206">a.</span></span> <span data-ttu-id="9a7f5-207">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9a7f5-208">b.</span><span class="sxs-lookup"><span data-stu-id="9a7f5-208">b.</span></span> <span data-ttu-id="9a7f5-209">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9a7f5-210">c.</span><span class="sxs-lookup"><span data-stu-id="9a7f5-210">c.</span></span> <span data-ttu-id="9a7f5-211">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9a7f5-212">d.</span><span class="sxs-lookup"><span data-stu-id="9a7f5-212">d.</span></span> <span data-ttu-id="9a7f5-213">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-213">Click **Create**.</span></span>
 
### <a name="create-a-voyance-test-user"></a><span data-ttu-id="9a7f5-214">建立 Voyance 測試使用者</span><span class="sxs-lookup"><span data-stu-id="9a7f5-214">Create a Voyance test user</span></span>

<span data-ttu-id="9a7f5-215">hello 本節目標在於 toocreate Voyance 中呼叫許 Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-215">hello objective of this section is toocreate a user called Britta Simon in Voyance.</span></span> <span data-ttu-id="9a7f5-216">Voyance 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-216">Voyance supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="9a7f5-217">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-217">There is no action item for you in this section.</span></span> <span data-ttu-id="9a7f5-218">如果尚未存在期間嘗試 tooaccess Voyance，建立新的使用者。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-218">A new user is created during an attempt tooaccess Voyance if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="9a7f5-219">若要手動 toocreate 使用者，您需要 toocontact [Voyance 支援小組](maiLto:support@nyansa.com)。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-219">If you need toocreate a user manually, you need toocontact [Voyance support team](maiLto:support@nyansa.com).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="9a7f5-220">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="9a7f5-220">Assign hello Azure AD test user</span></span>

<span data-ttu-id="9a7f5-221">在本節中，您可以授與存取 tooVoyance 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooVoyance.</span></span>

![指派 hello 使用者角色][200]

<span data-ttu-id="9a7f5-223">**tooassign 許 Simon tooVoyance，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="9a7f5-223">**tooassign Britta Simon tooVoyance, perform hello following steps:**</span></span>

1. <span data-ttu-id="9a7f5-224">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="9a7f5-226">在 [hello] 應用程式清單中，選取**Voyance**。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-226">In hello applications list, select **Voyance**.</span></span>

    ![hello 應用程式清單中的 hello Voyance 連結](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_app.png) 

3. <span data-ttu-id="9a7f5-228">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello 「 使用者和群組 」 的連結][202]

4. <span data-ttu-id="9a7f5-230">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-230">Click **Add** button.</span></span> <span data-ttu-id="9a7f5-231">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 將作業加入窗格][203]

5. <span data-ttu-id="9a7f5-233">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9a7f5-234">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9a7f5-235">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="9a7f5-236">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="9a7f5-236">Test single sign-on</span></span>

<span data-ttu-id="9a7f5-237">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9a7f5-238">當您按一下 hello Voyance 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Voyance 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9a7f5-238">When you click hello Voyance tile in hello Access Panel, you should get automatically signed-on tooyour Voyance application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9a7f5-239">其他資源</span><span class="sxs-lookup"><span data-stu-id="9a7f5-239">Additional resources</span></span>

* [<span data-ttu-id="9a7f5-240">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9a7f5-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9a7f5-241">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="9a7f5-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_203.png

