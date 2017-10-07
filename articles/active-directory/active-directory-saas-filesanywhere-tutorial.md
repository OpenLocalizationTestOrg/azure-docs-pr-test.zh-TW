---
title: "教學課程：Azure Active Directory 與 FilesAnywhere 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 FilesAnywhere 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: jeedes
ms.openlocfilehash: 376364a5c75f8d069ea6390c58586acb378cd8b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filesanywhere"></a><span data-ttu-id="d5c72-103">教學課程：Azure Active Directory 與 FilesAnywhere 整合</span><span class="sxs-lookup"><span data-stu-id="d5c72-103">Tutorial: Azure Active Directory integration with FilesAnywhere</span></span>

<span data-ttu-id="d5c72-104">在此教學課程中，您學會如何 toointegrate FilesAnywhere 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="d5c72-104">In this tutorial, you learn how toointegrate FilesAnywhere with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d5c72-105">與 Azure AD 整合 FilesAnywhere 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="d5c72-105">Integrating FilesAnywhere with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d5c72-106">您可以控制存取 tooFilesAnywhere Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="d5c72-106">You can control in Azure AD who has access tooFilesAnywhere</span></span>
- <span data-ttu-id="d5c72-107">您可以啟用您的使用者 tooautomatically get 登入 tooFilesAnywhere （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="d5c72-107">You can enable your users tooautomatically get signed-on tooFilesAnywhere (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d5c72-108">您可以管理您的帳戶，在單一中央位置-hello Azure 管理入口網站</span><span class="sxs-lookup"><span data-stu-id="d5c72-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="d5c72-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="d5c72-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d5c72-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="d5c72-110">Prerequisites</span></span>

<span data-ttu-id="d5c72-111">tooconfigure FilesAnywhere 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="d5c72-111">tooconfigure Azure AD integration with FilesAnywhere, you need hello following items:</span></span>

- <span data-ttu-id="d5c72-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d5c72-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d5c72-113">啟用 FilesAnywhere 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d5c72-113">A FilesAnywhere single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="d5c72-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="d5c72-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="d5c72-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="d5c72-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d5c72-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="d5c72-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="d5c72-117">如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="d5c72-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="d5c72-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="d5c72-118">Scenario description</span></span>
<span data-ttu-id="d5c72-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d5c72-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d5c72-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="d5c72-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d5c72-121">從 hello 圖庫加入 FilesAnywhere</span><span class="sxs-lookup"><span data-stu-id="d5c72-121">Adding FilesAnywhere from hello gallery</span></span>
2. <span data-ttu-id="d5c72-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d5c72-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-filesanywhere-from-hello-gallery"></a><span data-ttu-id="d5c72-123">從 hello 圖庫加入 FilesAnywhere</span><span class="sxs-lookup"><span data-stu-id="d5c72-123">Adding FilesAnywhere from hello gallery</span></span>
<span data-ttu-id="d5c72-124">tooconfigure hello 整合 FilesAnywhere 到 Azure AD，您需要 tooadd FilesAnywhere hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d5c72-124">tooconfigure hello integration of FilesAnywhere into Azure AD, you need tooadd FilesAnywhere from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d5c72-125">**tooadd FilesAnywhere 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="d5c72-125">**tooadd FilesAnywhere from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d5c72-126">在 hello  **[Azure 管理入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="d5c72-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d5c72-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="d5c72-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d5c72-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="d5c72-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="d5c72-131">按一下**新增**上 hello hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="d5c72-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="d5c72-133">在 [hello] 搜尋方塊中，輸入**FilesAnywhere**。</span><span class="sxs-lookup"><span data-stu-id="d5c72-133">In hello search box, type **FilesAnywhere**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_search.png)

5. <span data-ttu-id="d5c72-135">在 hello 結果 窗格中，選取  **FilesAnywhere**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d5c72-135">In hello results panel, select **FilesAnywhere**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d5c72-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d5c72-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d5c72-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 FilesAnywhere 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d5c72-138">In this section, you configure and test Azure AD single sign-on with FilesAnywhere based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d5c72-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 FilesAnywhere 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="d5c72-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FilesAnywhere is tooa user in Azure AD.</span></span> <span data-ttu-id="d5c72-140">換句話說，Azure AD 使用者與 hello FilesAnywhere 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="d5c72-140">In other words, a link relationship between an Azure AD user and hello related user in FilesAnywhere needs toobe established.</span></span>

<span data-ttu-id="d5c72-141">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** FilesAnywhere 中。</span><span class="sxs-lookup"><span data-stu-id="d5c72-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in FilesAnywhere.</span></span>

<span data-ttu-id="d5c72-142">tooconfigure 及 FilesAnywhere 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="d5c72-142">tooconfigure and test Azure AD single sign-on with FilesAnywhere, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d5c72-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="d5c72-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d5c72-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="d5c72-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d5c72-145">**[建立測試使用者 FilesAnywhere](#creating-a-filesanywhere-test-user)**  -toohave 許 Simon 是連結的 toohello Azure AD 表示她的 FilesAnywhere 中對應項目。</span><span class="sxs-lookup"><span data-stu-id="d5c72-145">**[Creating a FilesAnywhere test user](#creating-a-filesanywhere-test-user)** - toohave a counterpart of Britta Simon in FilesAnywhere that is linked toohello Azure AD representation of her.</span></span>
3. <span data-ttu-id="d5c72-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d5c72-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
4. <span data-ttu-id="d5c72-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="d5c72-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d5c72-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d5c72-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d5c72-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 管理入口網站中，並 FilesAnywhere 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="d5c72-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your FilesAnywhere application.</span></span>

<span data-ttu-id="d5c72-150">**tooconfigure Azure AD 單一登入與 FilesAnywhere，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="d5c72-150">**tooconfigure Azure AD single sign-on with FilesAnywhere, perform hello following steps:**</span></span>

1. <span data-ttu-id="d5c72-151">在 hello Azure 管理入口網站上 hello **FilesAnywhere**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="d5c72-151">In hello Azure Management portal, on hello **FilesAnywhere** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="d5c72-153">在 [hello**單一登入**] 對話方塊中，做為**模式**選取**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d5c72-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_samlbase.png)

3. <span data-ttu-id="d5c72-155">在 hello **FilesAnywhere 網域和 Url**區段中，如果您想 tooconfigure hello 應用程式中的**IDP 初始化模式**:</span><span class="sxs-lookup"><span data-stu-id="d5c72-155">On hello **FilesAnywhere Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**:</span></span>

    ![設定單一登入](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url.png)
    
    <span data-ttu-id="d5c72-157">a.</span><span class="sxs-lookup"><span data-stu-id="d5c72-157">a.</span></span> <span data-ttu-id="d5c72-158">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<company name>.filesanywhere.com/saml20.aspx?c=215`</span><span class="sxs-lookup"><span data-stu-id="d5c72-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.filesanywhere.com/saml20.aspx?c=215`</span></span>
> [!NOTE]
> <span data-ttu-id="d5c72-159">請注意 hello 該值**215**是**clientid** ，只是一個範例。</span><span class="sxs-lookup"><span data-stu-id="d5c72-159">Please note that hello value **215** is a **clientid** and is just an example.</span></span> <span data-ttu-id="d5c72-160">您需要 tooreplace 它與 hello 實際 clientid 值。</span><span class="sxs-lookup"><span data-stu-id="d5c72-160">You need tooreplace it with hello actual clientid value.</span></span>

4. <span data-ttu-id="d5c72-161">在 hello **FilesAnywhere 網域和 Url**區段中，如果您想 tooconfigure hello 應用程式中的**SP 初始模式**，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="d5c72-161">On hello **FilesAnywhere Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![設定單一登入](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url1.png)

    <span data-ttu-id="d5c72-163">a.</span><span class="sxs-lookup"><span data-stu-id="d5c72-163">a.</span></span> <span data-ttu-id="d5c72-164">按一下 hello**顯示進階的 URL 設定**選項</span><span class="sxs-lookup"><span data-stu-id="d5c72-164">Click on hello **Show advanced URL settings** option</span></span>

    <span data-ttu-id="d5c72-165">b.</span><span class="sxs-lookup"><span data-stu-id="d5c72-165">b.</span></span> <span data-ttu-id="d5c72-166">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<sub domain>.filesanywhere.com/`</span><span class="sxs-lookup"><span data-stu-id="d5c72-166">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<sub domain>.filesanywhere.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d5c72-167">請注意這些不是 hello 實際值。</span><span class="sxs-lookup"><span data-stu-id="d5c72-167">Please note that these are not hello real values.</span></span> <span data-ttu-id="d5c72-168">您有 tooupdate hello 實際的登入 URL 及回覆 URL 與這些值。</span><span class="sxs-lookup"><span data-stu-id="d5c72-168">You have tooupdate these values with hello actual Sign On URL and Reply URL.</span></span> <span data-ttu-id="d5c72-169">請連絡[FilesAnywhere 支援小組](mailto:support@FilesAnywhere.com)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="d5c72-169">Contact [FilesAnywhere support team](mailto:support@FilesAnywhere.com) tooget these values.</span></span> 

5. <span data-ttu-id="d5c72-170">FilesAnywhere 軟體應用程式預期 hello SAML 判斷提示，以特定格式。</span><span class="sxs-lookup"><span data-stu-id="d5c72-170">FilesAnywhere Software application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="d5c72-171">請設定下列宣告為此應用程式的 hello。</span><span class="sxs-lookup"><span data-stu-id="d5c72-171">Please configure hello following claims for this application.</span></span> <span data-ttu-id="d5c72-172">您可以從 hello 管理 hello 這些屬性的值"**使用者屬性**」 一節，在應用程式整合頁面上。</span><span class="sxs-lookup"><span data-stu-id="d5c72-172">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="d5c72-173">hello 下列螢幕擷取畫面會顯示這個範例。</span><span class="sxs-lookup"><span data-stu-id="d5c72-173">hello following screenshot shows an example for this.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_attribute.png)
    
    <span data-ttu-id="d5c72-175">當 hello 的 FilesAnywhere 它們得到 hello 值的總使用者登**clientid**屬性從[FilesAnywhere 小組](mailto:support@FilesAnywhere.com)。</span><span class="sxs-lookup"><span data-stu-id="d5c72-175">When hello users signs up with FilesAnywhere they get hello value of **clientid** attribute from [FilesAnywhere team](mailto:support@FilesAnywhere.com).</span></span> <span data-ttu-id="d5c72-176">您可以有 tooadd hello [用戶端識別碼] 屬性與 hello FilesAnywhere 所提供的唯一值。</span><span class="sxs-lookup"><span data-stu-id="d5c72-176">You have tooadd hello "Client Id" attribute with hello unique value provided by FilesAnywhere.</span></span> <span data-ttu-id="d5c72-177">上述的所有屬性都是必要屬性。</span><span class="sxs-lookup"><span data-stu-id="d5c72-177">All these attributes shown above are required.</span></span>
    > [!NOTE] 
    > <span data-ttu-id="d5c72-178">請注意 hello 該值**2331年**的**clientid**只是一個範例。</span><span class="sxs-lookup"><span data-stu-id="d5c72-178">Please note that hello value **2331** of **clientid** is just an example.</span></span> <span data-ttu-id="d5c72-179">您需要 tooprovide hello 實際值。</span><span class="sxs-lookup"><span data-stu-id="d5c72-179">You need tooprovide hello actual value.</span></span>


6. <span data-ttu-id="d5c72-180">在 hello**使用者屬性**區段 hello**單一登入** 對話方塊中，上述 hello 映像中所示設定 SAML 權杖屬性和執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="d5c72-180">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="d5c72-181">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="d5c72-181">Attribute Name</span></span> | <span data-ttu-id="d5c72-182">屬性值</span><span class="sxs-lookup"><span data-stu-id="d5c72-182">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="d5c72-183">clientid</span><span class="sxs-lookup"><span data-stu-id="d5c72-183">clientid</span></span> | <span data-ttu-id="d5c72-184">*"uniquevalue"*</span><span class="sxs-lookup"><span data-stu-id="d5c72-184">*"uniquevalue"*</span></span> |

    <span data-ttu-id="d5c72-185">a.</span><span class="sxs-lookup"><span data-stu-id="d5c72-185">a.</span></span> <span data-ttu-id="d5c72-186">按一下**加入屬性**tooopen hello**加入屬性**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="d5c72-186">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_04.png)

    ![設定單一登入](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_05.png)
    
    <span data-ttu-id="d5c72-189">b.</span><span class="sxs-lookup"><span data-stu-id="d5c72-189">b.</span></span> <span data-ttu-id="d5c72-190">在 hello**名稱**文字方塊中，該資料列所顯示的型別 hello 屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="d5c72-190">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="d5c72-191">c.</span><span class="sxs-lookup"><span data-stu-id="d5c72-191">c.</span></span> <span data-ttu-id="d5c72-192">從 hello**值**清單，顯示該資料列的型別 hello 屬性值。</span><span class="sxs-lookup"><span data-stu-id="d5c72-192">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="d5c72-193">d.</span><span class="sxs-lookup"><span data-stu-id="d5c72-193">d.</span></span> <span data-ttu-id="d5c72-194">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="d5c72-194">Click **Ok**</span></span>

7. <span data-ttu-id="d5c72-195">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="d5c72-195">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="d5c72-197">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="d5c72-197">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_certificate.png) 

9. <span data-ttu-id="d5c72-199">在 hello **FilesAnywhere 組態**區段中，按一下**設定 FilesAnywhere** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="d5c72-199">On hello **FilesAnywhere Configuration** section, click **Configure FilesAnywhere** tooopen **Configure sign-on** window.</span></span>

    ![設定單一登入](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configure.png) 

    ![設定單一登入](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configuresignon.png)

10. <span data-ttu-id="d5c72-202">tooget SSO 組態在 FilesAnywhere 結束時，請連絡您的應用程式完成[FilesAnywhere 支援小組](mailto:support@FilesAnywhere.com)並下載 hello SAML 權杖簽署憑證和單一登入 (SSO) 的 URL 提供給他們。</span><span class="sxs-lookup"><span data-stu-id="d5c72-202">tooget SSO configuration complete for your application at FilesAnywhere end, contact [FilesAnywhere support team](mailto:support@FilesAnywhere.com) and provide them hello downloaded SAML token signing Certificate and Single Sign On (SSO) URL.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d5c72-203">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d5c72-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="d5c72-204">hello 本節目標在於 toocreate 呼叫許 Simon hello Azure 管理入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="d5c72-204">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="d5c72-206">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="d5c72-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d5c72-207">在 hello **Azure 管理入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="d5c72-207">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d5c72-209">跳過**使用者和群組**按一下**所有使用者**toodisplay hello 使用者清單。</span><span class="sxs-lookup"><span data-stu-id="d5c72-209">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d5c72-211">在 hello hello 對話方塊頂端按一下**新增**tooopen hello**使用者**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="d5c72-211">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d5c72-213">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="d5c72-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d5c72-215">a.</span><span class="sxs-lookup"><span data-stu-id="d5c72-215">a.</span></span> <span data-ttu-id="d5c72-216">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="d5c72-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d5c72-217">b.</span><span class="sxs-lookup"><span data-stu-id="d5c72-217">b.</span></span> <span data-ttu-id="d5c72-218">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="d5c72-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d5c72-219">c.</span><span class="sxs-lookup"><span data-stu-id="d5c72-219">c.</span></span> <span data-ttu-id="d5c72-220">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="d5c72-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d5c72-221">d.</span><span class="sxs-lookup"><span data-stu-id="d5c72-221">d.</span></span> <span data-ttu-id="d5c72-222">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="d5c72-222">Click **Create**.</span></span> 



### <a name="creating-a-filesanywhere-test-user"></a><span data-ttu-id="d5c72-223">建立 FilesAnywhere 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d5c72-223">Creating a FilesAnywhere test user</span></span>

<span data-ttu-id="d5c72-224">應用程式支援恰好在即時使用者佈建，以及之後驗證的使用者將會在 hello 應用程式中自動建立。</span><span class="sxs-lookup"><span data-stu-id="d5c72-224">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span> 


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d5c72-225">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="d5c72-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d5c72-226">在本節中，您可以授與他們存取 tooFilesAnywhere 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d5c72-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooFilesAnywhere.</span></span>

![指派使用者][200] 

<span data-ttu-id="d5c72-228">**tooassign 許 Simon tooFilesAnywhere，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="d5c72-228">**tooassign Britta Simon tooFilesAnywhere, perform hello following steps:**</span></span>

1. <span data-ttu-id="d5c72-229">在 hello Azure 管理入口網站中，開啟 hello 應用程式 檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="d5c72-229">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="d5c72-231">在 [hello] 應用程式清單中，選取**FilesAnywhere**。</span><span class="sxs-lookup"><span data-stu-id="d5c72-231">In hello applications list, select **FilesAnywhere**.</span></span>

    ![設定單一登入](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_app.png) 

3. <span data-ttu-id="d5c72-233">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="d5c72-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="d5c72-235">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d5c72-235">Click **Add** button.</span></span> <span data-ttu-id="d5c72-236">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="d5c72-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="d5c72-238">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="d5c72-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d5c72-239">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d5c72-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d5c72-240">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d5c72-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="d5c72-241">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="d5c72-241">Testing single sign-on</span></span>

<span data-ttu-id="d5c72-242">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="d5c72-242">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d5c72-243">當您按一下 hello FilesAnywhere 磚 hello 存取面板中的時，您應該取得自動登入 tooyour FilesAnywhere 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d5c72-243">When you click hello FilesAnywhere tile in hello Access Panel, you should get automatically signed-on tooyour FilesAnywhere application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="d5c72-244">其他資源</span><span class="sxs-lookup"><span data-stu-id="d5c72-244">Additional resources</span></span>

* [<span data-ttu-id="d5c72-245">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d5c72-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d5c72-246">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="d5c72-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_203.png
