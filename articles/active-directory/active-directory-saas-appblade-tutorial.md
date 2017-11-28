---
title: "教學課程：Azure Active Directory 與 AppBlade 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 AppBlade 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3360d7aa-6518-4f99-88bd-b7f7258183e8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 06f3d8fcee97945c867bca6f3aebe15ecef04617
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-appblade"></a><span data-ttu-id="6a346-103">教學課程：Azure Active Directory 與 AppBlade 整合</span><span class="sxs-lookup"><span data-stu-id="6a346-103">Tutorial: Azure Active Directory integration with AppBlade</span></span>

<span data-ttu-id="6a346-104">在此教學課程中，您學會如何 toointegrate AppBlade 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="6a346-104">In this tutorial, you learn how toointegrate AppBlade with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6a346-105">與 Azure AD 整合 AppBlade 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="6a346-105">Integrating AppBlade with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6a346-106">您可以控制存取 tooAppBlade Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="6a346-106">You can control in Azure AD who has access tooAppBlade</span></span>
- <span data-ttu-id="6a346-107">您可以啟用您的使用者 tooautomatically get 登入 tooAppBlade （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="6a346-107">You can enable your users tooautomatically get signed-on tooAppBlade (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6a346-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="6a346-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6a346-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="6a346-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6a346-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="6a346-110">Prerequisites</span></span>

<span data-ttu-id="6a346-111">tooconfigure AppBlade 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="6a346-111">tooconfigure Azure AD integration with AppBlade, you need hello following items:</span></span>

- <span data-ttu-id="6a346-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="6a346-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6a346-113">已啟用 AppBlade 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="6a346-113">An AppBlade single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6a346-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="6a346-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6a346-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="6a346-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6a346-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="6a346-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6a346-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="6a346-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6a346-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="6a346-118">Scenario description</span></span>
<span data-ttu-id="6a346-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6a346-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6a346-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="6a346-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6a346-121">從 hello 圖庫加入 AppBlade</span><span class="sxs-lookup"><span data-stu-id="6a346-121">Adding AppBlade from hello gallery</span></span>
2. <span data-ttu-id="6a346-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6a346-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-appblade-from-hello-gallery"></a><span data-ttu-id="6a346-123">從 hello 圖庫加入 AppBlade</span><span class="sxs-lookup"><span data-stu-id="6a346-123">Adding AppBlade from hello gallery</span></span>
<span data-ttu-id="6a346-124">tooconfigure hello 整合 AppBlade 到 Azure AD，您需要 tooadd AppBlade hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6a346-124">tooconfigure hello integration of AppBlade into Azure AD, you need tooadd AppBlade from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6a346-125">**tooadd AppBlade 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="6a346-125">**tooadd AppBlade from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6a346-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="6a346-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6a346-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="6a346-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6a346-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="6a346-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="6a346-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="6a346-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="6a346-133">在 [hello] 搜尋方塊中，輸入**AppBlade**。</span><span class="sxs-lookup"><span data-stu-id="6a346-133">In hello search box, type **AppBlade**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_search.png)

5. <span data-ttu-id="6a346-135">在 hello 結果 窗格中，選取  **AppBlade**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6a346-135">In hello results panel, select **AppBlade**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6a346-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6a346-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6a346-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 AppBlade 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6a346-138">In this section, you configure and test Azure AD single sign-on with AppBlade based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6a346-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 AppBlade 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="6a346-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in AppBlade is tooa user in Azure AD.</span></span> <span data-ttu-id="6a346-140">換句話說，Azure AD 使用者與 hello AppBlade 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="6a346-140">In other words, a link relationship between an Azure AD user and hello related user in AppBlade needs toobe established.</span></span>

<span data-ttu-id="6a346-141">AppBlade 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="6a346-141">In AppBlade, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6a346-142">tooconfigure 及 AppBlade 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="6a346-142">tooconfigure and test Azure AD single sign-on with AppBlade, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6a346-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="6a346-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6a346-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="6a346-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6a346-145">**[建立測試使用者 AppBlade](#creating-an-appblade-test-user)**  -toohave 許 Simon AppBlade 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="6a346-145">**[Creating an AppBlade test user](#creating-an-appblade-test-user)** - toohave a counterpart of Britta Simon in AppBlade that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6a346-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6a346-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6a346-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="6a346-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6a346-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6a346-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6a346-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 AppBlade 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="6a346-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your AppBlade application.</span></span>

<span data-ttu-id="6a346-150">**tooconfigure Azure AD 單一登入與 AppBlade，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="6a346-150">**tooconfigure Azure AD single sign-on with AppBlade, perform hello following steps:**</span></span>

1. <span data-ttu-id="6a346-151">在 Azure 入口網站上 hello hello **AppBlade**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="6a346-151">In hello Azure portal, on hello **AppBlade** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="6a346-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6a346-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_samlbase.png)

3. <span data-ttu-id="6a346-155">在 hello **AppBlade 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="6a346-155">On hello **AppBlade Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_url.png)

    <span data-ttu-id="6a346-157">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.appblade.com/saml/<tenantid>`</span><span class="sxs-lookup"><span data-stu-id="6a346-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.appblade.com/saml/<tenantid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6a346-158">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="6a346-158">This value is not real.</span></span> <span data-ttu-id="6a346-159">更新 hello 值與 hello 實際的登入 URL。</span><span class="sxs-lookup"><span data-stu-id="6a346-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="6a346-160">請連絡[AppBlade 用戶端支援小組](mailto:support@appblade.com)tooget hello 值。</span><span class="sxs-lookup"><span data-stu-id="6a346-160">Contact [AppBlade Client support team](mailto:support@appblade.com) tooget hello value.</span></span> 
 
4. <span data-ttu-id="6a346-161">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="6a346-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_certificate.png) 

5. <span data-ttu-id="6a346-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="6a346-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-appblade-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6a346-165">tooconfigure 單一登入上**AppBlade**端，您需要下載 toosend hello**中繼資料 XML**太[AppBlade 支援小組](mailto:support@appblade.com)。</span><span class="sxs-lookup"><span data-stu-id="6a346-165">tooconfigure single sign-on on **AppBlade** side, you need toosend hello downloaded **Metadata XML** too[AppBlade support team](mailto:support@appblade.com).</span></span> <span data-ttu-id="6a346-166">此外，請要求他們 tooconfigure hello **SSO 簽發者 URL**為`https://appblade.com/saml`。</span><span class="sxs-lookup"><span data-stu-id="6a346-166">Also, please ask them tooconfigure hello **SSO Issuer URL** as `https://appblade.com/saml`.</span></span> <span data-ttu-id="6a346-167">單一登入 toowork 需要這項設定。</span><span class="sxs-lookup"><span data-stu-id="6a346-167">This setting is required for single sign-on toowork.</span></span>


> [!TIP]
> <span data-ttu-id="6a346-168">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="6a346-168">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6a346-169">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="6a346-169">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6a346-170">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6a346-170">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6a346-171">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="6a346-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="6a346-172">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="6a346-172">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="6a346-174">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="6a346-174">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6a346-175">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="6a346-175">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-appblade-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6a346-177">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="6a346-177">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-appblade-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6a346-179">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="6a346-179">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-appblade-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6a346-181">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="6a346-181">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-appblade-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6a346-183">a.</span><span class="sxs-lookup"><span data-stu-id="6a346-183">a.</span></span> <span data-ttu-id="6a346-184">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="6a346-184">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6a346-185">b.</span><span class="sxs-lookup"><span data-stu-id="6a346-185">b.</span></span> <span data-ttu-id="6a346-186">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="6a346-186">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6a346-187">c.</span><span class="sxs-lookup"><span data-stu-id="6a346-187">c.</span></span> <span data-ttu-id="6a346-188">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="6a346-188">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6a346-189">d.</span><span class="sxs-lookup"><span data-stu-id="6a346-189">d.</span></span> <span data-ttu-id="6a346-190">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="6a346-190">Click **Create**.</span></span>
 
### <a name="creating-an-appblade-test-user"></a><span data-ttu-id="6a346-191">建立 AppBlade 測試使用者</span><span class="sxs-lookup"><span data-stu-id="6a346-191">Creating an AppBlade test user</span></span>

<span data-ttu-id="6a346-192">hello 本節目標在於 toocreate AppBlade 中呼叫許 Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="6a346-192">hello objective of this section is toocreate a user called Britta Simon in AppBlade.</span></span> <span data-ttu-id="6a346-193">AppBlade 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="6a346-193">AppBlade supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="6a346-194">**請確定您已搭配 AppBlade 來設定網域名稱，以便進行使用者佈建。該唯一 hello 中 just-in-time 的使用者佈建運作方式。**</span><span class="sxs-lookup"><span data-stu-id="6a346-194">**Make sure that your domain name is configured with AppBlade for user provisioning. After that only hello just-in-time user provisioning works.**</span></span>

<span data-ttu-id="6a346-195">如果 hello 使用者已結束與 hello 網域 AppBlade 針對您的帳戶，然後 hello 使用者會自動為您指定的 hello 權限層級的成員加入 hello 帳戶電子郵件地址，這是一個 「 基本 」 （的基本使用者只能安裝應用程式），「 小組成員 」 （使用者可以上傳新的應用程式版本和管理專案） 或 「 系統管理員 」 （完整的系統管理員權限 toohello 帳戶）。</span><span class="sxs-lookup"><span data-stu-id="6a346-195">If hello user has an email address ending with hello domain configured by AppBlade for your account, then hello user will automatically join hello account as a member with hello permission level you specify, which is one of "Basic" (a basic user who can only install applications), "Team Member" (a user who can upload new app versions and manage projects), or "Administrator" (full admin privileges toohello account).</span></span> <span data-ttu-id="6a346-196">通常一個會選擇 Basic，然後升級使用者手動透過系統管理員登入 （AppBlade 事先需要 tooconfigure 電子郵件為基礎的系統管理員登入，或登入之後，將使用者升級代表 hello 客戶）。</span><span class="sxs-lookup"><span data-stu-id="6a346-196">Normally one would choose Basic and then promote users manually via an Admin login (AppBlade needs tooconfigure either an email-based admin login in advance or promote a user on behalf of hello customer after login).</span></span>

<span data-ttu-id="6a346-197">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="6a346-197">There is no action item for you in this section.</span></span> <span data-ttu-id="6a346-198">如果尚未存在期間嘗試 tooaccess AppBlade，建立新的使用者。</span><span class="sxs-lookup"><span data-stu-id="6a346-198">A new user is created during an attempt tooaccess AppBlade if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="6a346-199">若要手動 toocreate 使用者，您需要 toocontact hello [AppBlade 支援小組](mailto:support@appblade.com)。</span><span class="sxs-lookup"><span data-stu-id="6a346-199">If you need toocreate a user manually, you need toocontact hello [AppBlade support team](mailto:support@appblade.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6a346-200">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="6a346-200">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6a346-201">在本節中，您可以授與存取 tooAppBlade 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6a346-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAppBlade.</span></span>

![指派使用者][200] 

<span data-ttu-id="6a346-203">**tooassign 許 Simon tooAppBlade，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="6a346-203">**tooassign Britta Simon tooAppBlade, perform hello following steps:**</span></span>

1. <span data-ttu-id="6a346-204">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="6a346-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="6a346-206">在 [hello] 應用程式清單中，選取**AppBlade**。</span><span class="sxs-lookup"><span data-stu-id="6a346-206">In hello applications list, select **AppBlade**.</span></span>

    ![設定單一登入](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_app.png) 

3. <span data-ttu-id="6a346-208">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="6a346-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="6a346-210">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6a346-210">Click **Add** button.</span></span> <span data-ttu-id="6a346-211">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="6a346-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="6a346-213">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="6a346-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6a346-214">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6a346-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6a346-215">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6a346-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6a346-216">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="6a346-216">Testing single sign-on</span></span>

<span data-ttu-id="6a346-217">hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="6a346-217">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="6a346-218">當您按一下 hello AppBlade 磚 hello 存取面板中的時，您應該取得自動登入 tooyour AppBlade 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6a346-218">When you click hello AppBlade tile in hello Access Panel, you should get automatically signed-on tooyour AppBlade application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6a346-219">其他資源</span><span class="sxs-lookup"><span data-stu-id="6a346-219">Additional resources</span></span>

* [<span data-ttu-id="6a346-220">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6a346-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6a346-221">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="6a346-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_203.png

