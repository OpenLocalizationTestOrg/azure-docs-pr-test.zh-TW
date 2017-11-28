---
title: "教學課程：Azure Active Directory 與 myPolicies 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 myPolicies 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bf79e858-1dfb-4ab3-a6df-74b2d5a878d2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: jeedes
ms.openlocfilehash: d8890457ebdb1b80e0d3126d4210e6265ae7f1ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mypolicies"></a><span data-ttu-id="ef0ab-103">教學課程：Azure Active Directory 與 myPolicies 整合</span><span class="sxs-lookup"><span data-stu-id="ef0ab-103">Tutorial: Azure Active Directory integration with myPolicies</span></span>

<span data-ttu-id="ef0ab-104">在此教學課程中，您學會如何 toointegrate myPolicies 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-104">In this tutorial, you learn how toointegrate myPolicies with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ef0ab-105">與 Azure AD 整合 myPolicies 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="ef0ab-105">Integrating myPolicies with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ef0ab-106">您可以控制存取 toomyPolicies Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="ef0ab-106">You can control in Azure AD who has access toomyPolicies</span></span>
- <span data-ttu-id="ef0ab-107">您可以啟用您的使用者 tooautomatically get 登入 toomyPolicies （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="ef0ab-107">You can enable your users tooautomatically get signed-on toomyPolicies (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ef0ab-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="ef0ab-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ef0ab-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ef0ab-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="ef0ab-110">Prerequisites</span></span>

<span data-ttu-id="ef0ab-111">tooconfigure myPolicies 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="ef0ab-111">tooconfigure Azure AD integration with myPolicies, you need hello following items:</span></span>

- <span data-ttu-id="ef0ab-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ef0ab-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ef0ab-113">啟用 myPolicies 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ef0ab-113">A myPolicies single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ef0ab-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ef0ab-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="ef0ab-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ef0ab-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ef0ab-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ef0ab-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="ef0ab-118">Scenario description</span></span>
<span data-ttu-id="ef0ab-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ef0ab-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="ef0ab-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ef0ab-121">從 hello 圖庫加入 myPolicies</span><span class="sxs-lookup"><span data-stu-id="ef0ab-121">Adding myPolicies from hello gallery</span></span>
2. <span data-ttu-id="ef0ab-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ef0ab-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mypolicies-from-hello-gallery"></a><span data-ttu-id="ef0ab-123">從 hello 圖庫加入 myPolicies</span><span class="sxs-lookup"><span data-stu-id="ef0ab-123">Adding myPolicies from hello gallery</span></span>
<span data-ttu-id="ef0ab-124">tooconfigure hello 整合 myPolicies 到 Azure AD，您需要 tooadd myPolicies hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-124">tooconfigure hello integration of myPolicies into Azure AD, you need tooadd myPolicies from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ef0ab-125">**tooadd myPolicies 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="ef0ab-125">**tooadd myPolicies from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ef0ab-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ef0ab-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ef0ab-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="ef0ab-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="ef0ab-133">在 [hello] 搜尋方塊中，輸入**myPolicies**。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-133">In hello search box, type **myPolicies**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_search.png)

5. <span data-ttu-id="ef0ab-135">在 hello 結果 窗格中，選取  **myPolicies**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-135">In hello results panel, select **myPolicies**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ef0ab-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ef0ab-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ef0ab-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 myPolicies 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-138">In this section, you configure and test Azure AD single sign-on with myPolicies based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ef0ab-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 myPolicies 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in myPolicies is tooa user in Azure AD.</span></span> <span data-ttu-id="ef0ab-140">換句話說，Azure AD 使用者與 hello myPolicies 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-140">In other words, a link relationship between an Azure AD user and hello related user in myPolicies needs toobe established.</span></span>

<span data-ttu-id="ef0ab-141">MyPolicies 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-141">In myPolicies, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ef0ab-142">tooconfigure 及 myPolicies 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="ef0ab-142">tooconfigure and test Azure AD single sign-on with myPolicies, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ef0ab-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ef0ab-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ef0ab-145">**[建立測試使用者 myPolicies](#creating-a-mypolicies-test-user)**  -toohave 是連結的 toohello Azure AD 使用者表示法的 myPolicies 的許 Simon 的對應項目。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-145">**[Creating a myPolicies test user](#creating-a-mypolicies-test-user)** - toohave a counterpart of Britta Simon in myPolicies that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ef0ab-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ef0ab-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ef0ab-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ef0ab-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ef0ab-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 myPolicies 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your myPolicies application.</span></span>

<span data-ttu-id="ef0ab-150">**tooconfigure Azure AD 單一登入與 myPolicies，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="ef0ab-150">**tooconfigure Azure AD single sign-on with myPolicies, perform hello following steps:**</span></span>

1. <span data-ttu-id="ef0ab-151">在 Azure 入口網站上 hello hello **myPolicies**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-151">In hello Azure portal, on hello **myPolicies** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="ef0ab-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_samlbase.png)

3. <span data-ttu-id="ef0ab-155">在 hello **myPolicies 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="ef0ab-155">On hello **myPolicies Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_url.png)

    <span data-ttu-id="ef0ab-157">a.</span><span class="sxs-lookup"><span data-stu-id="ef0ab-157">a.</span></span> <span data-ttu-id="ef0ab-158">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<tenantname>.mypolicies.com/`</span><span class="sxs-lookup"><span data-stu-id="ef0ab-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.mypolicies.com/`</span></span>

    <span data-ttu-id="ef0ab-159">b.</span><span class="sxs-lookup"><span data-stu-id="ef0ab-159">b.</span></span> <span data-ttu-id="ef0ab-160">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<tenantname>.mypolicies.com/users/auth/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="ef0ab-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<tenantname>.mypolicies.com/users/auth/saml/callback`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ef0ab-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-161">These values are not real.</span></span> <span data-ttu-id="ef0ab-162">以 hello 實際的識別項和回覆 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="ef0ab-163">請連絡[myPolicies 支援小組](mailto:support@mypolicies.com)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-163">Contact [myPolicies support team](mailto:support@mypolicies.com) tooget these values.</span></span>

4. <span data-ttu-id="ef0ab-164">hello myPolicies 應用程式預期 hello SAML 判斷提示，以特定格式，這需要您 tooadd 自訂屬性對應 tooyour SAML token 屬性設定。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-164">hello myPolicies application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="ef0ab-165">設定下列宣告為此應用程式的 hello。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="ef0ab-166">您可以從 hello 管理 hello 這些屬性的值"**使用者屬性**」 一節，在應用程式整合頁面上。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="ef0ab-167">hello 下列螢幕擷取畫面會顯示這個範例。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-167">hello following screenshot shows an example for this.</span></span> 

    ![設定單一登入](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_attribute.png)

5. <span data-ttu-id="ef0ab-169">按一下**檢視和編輯所有其他使用者屬性**核取方塊在 hello**使用者屬性**區段 tooexpand hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-169">Click **View and edit all other user attributes** checkbox in hello **User Attributes** section tooexpand hello attributes.</span></span> <span data-ttu-id="ef0ab-170">執行下列步驟，在每個顯示 hello 屬性-hello</span><span class="sxs-lookup"><span data-stu-id="ef0ab-170">Perform hello following steps on each of hello displayed attributes-</span></span>

    | <span data-ttu-id="ef0ab-171">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="ef0ab-171">Attribute Name</span></span> | <span data-ttu-id="ef0ab-172">屬性值</span><span class="sxs-lookup"><span data-stu-id="ef0ab-172">Attribute Value</span></span> |
    | ------------------- | ---------- |
    | <span data-ttu-id="ef0ab-173">givenname</span><span class="sxs-lookup"><span data-stu-id="ef0ab-173">givenname</span></span> | <span data-ttu-id="ef0ab-174">user.givenname</span><span class="sxs-lookup"><span data-stu-id="ef0ab-174">user.givenname</span></span> |
    | <span data-ttu-id="ef0ab-175">surname</span><span class="sxs-lookup"><span data-stu-id="ef0ab-175">surname</span></span> | <span data-ttu-id="ef0ab-176">user.surname</span><span class="sxs-lookup"><span data-stu-id="ef0ab-176">user.surname</span></span> |
    | <span data-ttu-id="ef0ab-177">emailaddress</span><span class="sxs-lookup"><span data-stu-id="ef0ab-177">emailaddress</span></span> | <span data-ttu-id="ef0ab-178">user.mail</span><span class="sxs-lookup"><span data-stu-id="ef0ab-178">user.mail</span></span> |
    | <span data-ttu-id="ef0ab-179">名稱</span><span class="sxs-lookup"><span data-stu-id="ef0ab-179">name</span></span> | <span data-ttu-id="ef0ab-180">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="ef0ab-180">user.userprincipalname</span></span> |
    
    <span data-ttu-id="ef0ab-181">a.</span><span class="sxs-lookup"><span data-stu-id="ef0ab-181">a.</span></span> <span data-ttu-id="ef0ab-182">按一下 hello 屬性 tooopen hello**編輯屬性**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-182">Click on hello attribute tooopen hello **Edit Attribute** dialog.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-mypolicies-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="ef0ab-184">b.</span><span class="sxs-lookup"><span data-stu-id="ef0ab-184">b.</span></span> <span data-ttu-id="ef0ab-185">從 hello 刪除 hello URL 值**命名空間**。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-185">Delete hello URL value from hello **Namespace**.</span></span>
    
    <span data-ttu-id="ef0ab-186">c.</span><span class="sxs-lookup"><span data-stu-id="ef0ab-186">c.</span></span> <span data-ttu-id="ef0ab-187">按一下**確定**toosave hello 設定。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-187">Click **Ok** toosave hello setting.</span></span>
    
6. <span data-ttu-id="ef0ab-188">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-188">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_certificate.png) 

7. <span data-ttu-id="ef0ab-190">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-190">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-mypolicies-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="ef0ab-192">在 hello **myPolicies 組態**區段中，按一下**設定 myPolicies** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-192">On hello **myPolicies Configuration** section, click **Configure myPolicies** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ef0ab-193">複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="ef0ab-193">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_configure.png) 

9. <span data-ttu-id="ef0ab-195">tooconfigure 單一登入上**myPolicies**端，您需要下載 toosend hello **Certificate(Base64)**和**SAML 單一登入服務 URL**太[myPolicies 支援小組](mailto:support@mypolicies.com)。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-195">tooconfigure single sign-on on **myPolicies** side, you need toosend hello downloaded **Certificate(Base64)** and **SAML Single Sign-On Service URL** too[myPolicies support team](mailto:support@mypolicies.com).</span></span> 

> [!TIP]
> <span data-ttu-id="ef0ab-196">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="ef0ab-196">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ef0ab-197">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-197">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ef0ab-198">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ef0ab-198">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ef0ab-199">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ef0ab-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="ef0ab-200">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="ef0ab-202">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="ef0ab-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ef0ab-203">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-203">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ef0ab-205">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-205">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ef0ab-207">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-207">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ef0ab-209">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="ef0ab-209">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ef0ab-211">a.</span><span class="sxs-lookup"><span data-stu-id="ef0ab-211">a.</span></span> <span data-ttu-id="ef0ab-212">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-212">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ef0ab-213">b.</span><span class="sxs-lookup"><span data-stu-id="ef0ab-213">b.</span></span> <span data-ttu-id="ef0ab-214">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ef0ab-215">c.</span><span class="sxs-lookup"><span data-stu-id="ef0ab-215">c.</span></span> <span data-ttu-id="ef0ab-216">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-216">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ef0ab-217">d.</span><span class="sxs-lookup"><span data-stu-id="ef0ab-217">d.</span></span> <span data-ttu-id="ef0ab-218">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-218">Click **Create**.</span></span>
 
### <a name="creating-a-mypolicies-test-user"></a><span data-ttu-id="ef0ab-219">建立 myPolicies 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ef0ab-219">Creating a myPolicies test user</span></span>

<span data-ttu-id="ef0ab-220">在本節中，您要在 myPolicies 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-220">In this section, you create a user called Britta Simon in myPolicies.</span></span> <span data-ttu-id="ef0ab-221">使用[myPolicies 支援小組](mailto:support@mypolicies.com)hello myPolicies 平台中新增 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-221">Work with [myPolicies support team](mailto:support@mypolicies.com) to add hello users in hello myPolicies platform.</span></span> <span data-ttu-id="ef0ab-222">您必須先建立和啟動使用者，然後才能使用單一登入。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-222">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ef0ab-223">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="ef0ab-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ef0ab-224">在本節中，您可以授與存取 toomyPolicies 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access toomyPolicies.</span></span>

![指派使用者][200] 

<span data-ttu-id="ef0ab-226">**tooassign 許 Simon toomyPolicies，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="ef0ab-226">**tooassign Britta Simon toomyPolicies, perform hello following steps:**</span></span>

1. <span data-ttu-id="ef0ab-227">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="ef0ab-229">在 [hello] 應用程式清單中，選取**myPolicies**。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-229">In hello applications list, select **myPolicies**.</span></span>

    ![設定單一登入](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_app.png) 

3. <span data-ttu-id="ef0ab-231">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="ef0ab-233">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-233">Click **Add** button.</span></span> <span data-ttu-id="ef0ab-234">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="ef0ab-236">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ef0ab-237">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ef0ab-238">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ef0ab-239">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="ef0ab-239">Testing single sign-on</span></span>

<span data-ttu-id="ef0ab-240">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ef0ab-241">當您按一下的 hello myPolicies 磚 hello 存取面板中時，您應該取得自動登入 tooyour myPolicies 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-241">When you click hello myPolicies tile in hello Access Panel, you should get automatically signed-on tooyour myPolicies application.</span></span>
<span data-ttu-id="ef0ab-242">如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="ef0ab-242">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ef0ab-243">其他資源</span><span class="sxs-lookup"><span data-stu-id="ef0ab-243">Additional resources</span></span>

* [<span data-ttu-id="ef0ab-244">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ef0ab-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ef0ab-245">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="ef0ab-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_203.png

