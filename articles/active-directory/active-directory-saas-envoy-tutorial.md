---
title: "教學課程：Azure Active Directory 與 Envoy 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Envoy 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 71f7afcc-1033-4098-9b7e-4f9f2b26f734
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 93add7c1f3cf1fc163acc505f11e34bd696c571c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-envoy"></a><span data-ttu-id="ed9c0-103">教學課程：Azure Active Directory 與 Envoy 整合</span><span class="sxs-lookup"><span data-stu-id="ed9c0-103">Tutorial: Azure Active Directory integration with Envoy</span></span>

<span data-ttu-id="ed9c0-104">在此教學課程中，您學會如何 toointegrate Envoy 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-104">In this tutorial, you learn how toointegrate Envoy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ed9c0-105">整合 Azure AD 與 Envoy 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="ed9c0-105">Integrating Envoy with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ed9c0-106">您可以控制存取 tooEnvoy Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-106">You can control in Azure AD who has access tooEnvoy.</span></span>
- <span data-ttu-id="ed9c0-107">您可以啟用您的使用者 tooautomatically get 登入 tooEnvoy （單一登入） 具有其 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-107">You can enable your users tooautomatically get signed-on tooEnvoy (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="ed9c0-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="ed9c0-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed9c0-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="ed9c0-110">Prerequisites</span></span>

<span data-ttu-id="ed9c0-111">tooconfigure Azure AD 與 Envoy 的整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="ed9c0-111">tooconfigure Azure AD integration with Envoy, you need hello following items:</span></span>

- <span data-ttu-id="ed9c0-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ed9c0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ed9c0-113">啟用 Envoy 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ed9c0-113">An Envoy single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ed9c0-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ed9c0-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="ed9c0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ed9c0-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ed9c0-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ed9c0-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="ed9c0-118">Scenario description</span></span>
<span data-ttu-id="ed9c0-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ed9c0-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="ed9c0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ed9c0-121">從 hello 圖庫加入 Envoy</span><span class="sxs-lookup"><span data-stu-id="ed9c0-121">Adding Envoy from hello gallery</span></span>
2. <span data-ttu-id="ed9c0-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ed9c0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-envoy-from-hello-gallery"></a><span data-ttu-id="ed9c0-123">從 hello 圖庫加入 Envoy</span><span class="sxs-lookup"><span data-stu-id="ed9c0-123">Adding Envoy from hello gallery</span></span>
<span data-ttu-id="ed9c0-124">tooconfigure hello 整合 Envoy 的 Azure AD，您需要 tooadd Envoy hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-124">tooconfigure hello integration of Envoy into Azure AD, you need tooadd Envoy from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ed9c0-125">**tooadd Envoy hello 圖庫中，從執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="ed9c0-125">**tooadd Envoy from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ed9c0-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 按鈕][1]

2. <span data-ttu-id="ed9c0-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ed9c0-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-129">Then go too**All applications**.</span></span>

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. <span data-ttu-id="ed9c0-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 新應用程式按鈕][3]

4. <span data-ttu-id="ed9c0-133">在 hello 搜尋方塊中，輸入**Envoy**，選取**Envoy**然後按一下 從結果面板**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-133">In hello search box, type **Envoy**, select **Envoy** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Envoy hello [結果] 清單中](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ed9c0-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ed9c0-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="ed9c0-136">在本節中，您會以名為 "Britta Simon" 的測試使用者作為基礎，使用 Envoy 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-136">In this section, you configure and test Azure AD single sign-on with Envoy based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ed9c0-137">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Envoy 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Envoy is tooa user in Azure AD.</span></span> <span data-ttu-id="ed9c0-138">換句話說，Azure AD 使用者與 Envoy 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-138">In other words, a link relationship between an Azure AD user and hello related user in Envoy needs toobe established.</span></span>

<span data-ttu-id="ed9c0-139">Envoy 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-139">In Envoy, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ed9c0-140">tooconfigure 及 Azure AD 單一登入與 Envoy 的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="ed9c0-140">tooconfigure and test Azure AD single sign-on with Envoy, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ed9c0-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ed9c0-142">**[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ed9c0-143">**[建立測試使用者 Envoy](#create-an-envoy-test-user)**  -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示法的 Envoy 中對應項目。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-143">**[Create an Envoy test user](#create-an-envoy-test-user)** - toohave a counterpart of Britta Simon in Envoy that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ed9c0-144">**[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ed9c0-145">**[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ed9c0-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ed9c0-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ed9c0-147">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Envoy 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Envoy application.</span></span>

<span data-ttu-id="ed9c0-148">**tooconfigure Azure AD 單一登入與 Envoy，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="ed9c0-148">**tooconfigure Azure AD single sign-on with Envoy, perform hello following steps:**</span></span>

1. <span data-ttu-id="ed9c0-149">在 Azure 入口網站上 hello hello **Envoy**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-149">In hello Azure portal, on hello **Envoy** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="ed9c0-151">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_samlbase.png)

3. <span data-ttu-id="ed9c0-153">在 hello **Envoy 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="ed9c0-153">On hello **Envoy Domain and URLs** section, perform hello following steps:</span></span>

    ![Envoy 網域與 URL 單一登入資訊](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_url.png)

    <span data-ttu-id="ed9c0-155">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<tenant-name>.Envoy.com`</span><span class="sxs-lookup"><span data-stu-id="ed9c0-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.Envoy.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="ed9c0-156">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-156">This value is not real.</span></span> <span data-ttu-id="ed9c0-157">更新此值以 hello 實際的登入 URL。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-157">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="ed9c0-158">請連絡[Envoy 用戶端支援小組](https://envoy.com/contact/)tooget 此值。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-158">Contact [Envoy Client support team](https://envoy.com/contact/) tooget this value.</span></span>

4. <span data-ttu-id="ed9c0-159">在 hello **SAML 簽章憑證**區段，複製 hello**指紋**憑證值...</span><span class="sxs-lookup"><span data-stu-id="ed9c0-159">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate..</span></span>

    ![hello 憑證下載連結](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_certificate.png) 

5. <span data-ttu-id="ed9c0-161">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-161">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-envoy-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ed9c0-163">在 hello **Envoy 組態**區段中，按一下**設定 Envoy** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-163">On hello **Envoy Configuration** section, click **Configure Envoy** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ed9c0-164">複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="ed9c0-164">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Envoy 組態](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_configure.png)

7. <span data-ttu-id="ed9c0-166">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 Envoy 公司網站。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-166">In a different web browser window, log into your Envoy company site as an administrator.</span></span>

8. <span data-ttu-id="ed9c0-167">在 hello hello 上方的工具列中按一下**設定**。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-167">In hello toolbar on hello top, click **Settings**.</span></span>

    <span data-ttu-id="ed9c0-168">![Envoy](./media/active-directory-saas-envoy-tutorial/ic776782.png "Envoy")</span><span class="sxs-lookup"><span data-stu-id="ed9c0-168">![Envoy](./media/active-directory-saas-envoy-tutorial/ic776782.png "Envoy")</span></span>

9. <span data-ttu-id="ed9c0-169">按一下 [公司] 。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-169">Click **Company**.</span></span>

    <span data-ttu-id="ed9c0-170">![公司](./media/active-directory-saas-envoy-tutorial/ic776783.png "公司")</span><span class="sxs-lookup"><span data-stu-id="ed9c0-170">![Company](./media/active-directory-saas-envoy-tutorial/ic776783.png "Company")</span></span>

10. <span data-ttu-id="ed9c0-171">按一下 [SAML] 。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-171">Click **SAML**.</span></span>

    <span data-ttu-id="ed9c0-172">![SAML](./media/active-directory-saas-envoy-tutorial/ic776784.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="ed9c0-172">![SAML](./media/active-directory-saas-envoy-tutorial/ic776784.png "SAML")</span></span>

11. <span data-ttu-id="ed9c0-173">在 hello **SAML 驗證**組態區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="ed9c0-173">In hello **SAML Authentication** configuration section, perform hello following steps:</span></span>

    <span data-ttu-id="ed9c0-174">![SAML 驗證](./media/active-directory-saas-envoy-tutorial/ic776785.png "SAML 驗證")</span><span class="sxs-lookup"><span data-stu-id="ed9c0-174">![SAML authentication](./media/active-directory-saas-envoy-tutorial/ic776785.png "SAML authentication")</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="ed9c0-175">hello 總部位置識別碼 hello 值是自動產生 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-175">hello value for hello HQ location ID is auto generated by hello application.</span></span>
    
    <span data-ttu-id="ed9c0-176">a.</span><span class="sxs-lookup"><span data-stu-id="ed9c0-176">a.</span></span> <span data-ttu-id="ed9c0-177">在**指紋**文字方塊中，貼上 hello**指紋**憑證，您從 Azure 入口網站複製的值。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-177">In **Fingerprint** textbox, paste hello **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="ed9c0-178">b.</span><span class="sxs-lookup"><span data-stu-id="ed9c0-178">b.</span></span> <span data-ttu-id="ed9c0-179">貼上**SAML 單一登入服務 URL**已複製的值形成 hello Azure 入口網站至 hello**身分識別提供者 HTTP SAML URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-179">Paste **SAML Single Sign-On Service URL** value, which you have copied form hello Azure portal into hello **IDENTITY PROVIDER HTTP SAML URL** textbox.</span></span>
    
    <span data-ttu-id="ed9c0-180">c.</span><span class="sxs-lookup"><span data-stu-id="ed9c0-180">c.</span></span> <span data-ttu-id="ed9c0-181">按一下 [儲存變更] 。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-181">Click **Save changes**.</span></span>

> [!TIP]
> <span data-ttu-id="ed9c0-182">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="ed9c0-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ed9c0-183">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ed9c0-184">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ed9c0-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ed9c0-185">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ed9c0-185">Create an Azure AD test user</span></span>

<span data-ttu-id="ed9c0-186">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="ed9c0-188">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="ed9c0-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ed9c0-189">在 hello Azure 入口網站，hello 左窗格中，按一下 hello **Azure Active Directory**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-189">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-envoy-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="ed9c0-191">toodisplay hello 使用者清單，請移過**使用者和群組**，然後按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-191">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-envoy-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="ed9c0-193">tooopen hello**使用者**對話方塊中，按一下 [**新增**頂端的 hello hello**所有使用者**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-193">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello [新增] 按鈕](./media/active-directory-saas-envoy-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="ed9c0-195">在 hello**使用者**對話方塊方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="ed9c0-195">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello [使用者] 對話方塊](./media/active-directory-saas-envoy-tutorial/create_aaduser_04.png)

    <span data-ttu-id="ed9c0-197">a.</span><span class="sxs-lookup"><span data-stu-id="ed9c0-197">a.</span></span> <span data-ttu-id="ed9c0-198">在 hello**名稱**方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-198">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ed9c0-199">b.</span><span class="sxs-lookup"><span data-stu-id="ed9c0-199">b.</span></span> <span data-ttu-id="ed9c0-200">在 hello**使用者名**方塊中，使用者許 Simon 類型 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-200">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="ed9c0-201">c.</span><span class="sxs-lookup"><span data-stu-id="ed9c0-201">c.</span></span> <span data-ttu-id="ed9c0-202">選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 hello**密碼**方塊。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-202">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="ed9c0-203">d.</span><span class="sxs-lookup"><span data-stu-id="ed9c0-203">d.</span></span> <span data-ttu-id="ed9c0-204">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-204">Click **Create**.</span></span>
 
### <a name="create-an-envoy-test-user"></a><span data-ttu-id="ed9c0-205">建立 Envoy 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ed9c0-205">Create an Envoy test user</span></span>

<span data-ttu-id="ed9c0-206">不沒有您 tooconfigure 使用者佈建 tooEnvoy 任何動作項目。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-206">There is no action item for you tooconfigure user provisioning tooEnvoy.</span></span> <span data-ttu-id="ed9c0-207">當指派的使用者嘗試 toolog 入 Envoy 使用 hello 存取面板時，Envoy 會檢查 hello 使用者是否存在。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-207">When an assigned user tries toolog into Envoy using hello access panel, Envoy checks whether hello user exists.</span></span> <span data-ttu-id="ed9c0-208">如果尚無可用的使用者帳戶，Envoy 會自動予以建立。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-208">If there is no user account available yet, it is automatically created by Envoy.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="ed9c0-209">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ed9c0-209">Assign hello Azure AD test user</span></span>

<span data-ttu-id="ed9c0-210">在本節中，您可以授與存取 tooEnvoy 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-210">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEnvoy.</span></span>

![指派 hello 使用者角色][200] 

<span data-ttu-id="ed9c0-212">**tooassign 許 Simon tooEnvoy，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="ed9c0-212">**tooassign Britta Simon tooEnvoy, perform hello following steps:**</span></span>

1. <span data-ttu-id="ed9c0-213">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-213">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="ed9c0-215">在 [hello] 應用程式清單中，選取**Envoy**。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-215">In hello applications list, select **Envoy**.</span></span>

    ![hello 應用程式清單中的 hello Envoy 連結](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_app.png)  

3. <span data-ttu-id="ed9c0-217">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-217">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello 「 使用者和群組 」 的連結][202]

4. <span data-ttu-id="ed9c0-219">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-219">Click **Add** button.</span></span> <span data-ttu-id="ed9c0-220">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 將作業加入窗格][203]

5. <span data-ttu-id="ed9c0-222">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-222">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ed9c0-223">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ed9c0-224">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ed9c0-225">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="ed9c0-225">Test single sign-on</span></span>

<span data-ttu-id="ed9c0-226">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-226">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ed9c0-227">當您按一下 hello Envoy 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Envoy 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-227">When you click hello Envoy tile in hello Access Panel, you should get automatically signed-on tooyour Envoy application.</span></span>
<span data-ttu-id="ed9c0-228">如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="ed9c0-228">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ed9c0-229">其他資源</span><span class="sxs-lookup"><span data-stu-id="ed9c0-229">Additional resources</span></span>

* [<span data-ttu-id="ed9c0-230">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ed9c0-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ed9c0-231">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="ed9c0-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_203.png

